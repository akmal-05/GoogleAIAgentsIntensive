# Context Engineering: Sessions & Memory

## Overview
**Context Engineering** is the process of dynamically assembling and managing information inside a model’s context window to make LLM agents stateful, intelligent, and personalized.  
It extends beyond static prompt engineering by orchestrating all relevant data sources—system instructions, tools, memories, and conversation history—so the agent always reasons over the most relevant context.

Stateful AI depends on two core pillars:
- **Sessions** – short-term conversational state.
- **Memory** – long-term persistence and learning.

---

## 1. Sessions

A **session** is the container for a single conversation between a user and an agent.  
It holds:
- **Events** – user inputs, agent responses, tool calls, and tool outputs.
- **State** – structured working memory or scratchpad used during reasoning.

Sessions allow continuity within one interaction but are ephemeral. Each session is tied to a user and stored in persistent databases for reliability (e.g., Agent Engine Sessions).

### Multi-Agent Sessions
In multi-agent systems, sessions can be managed in two ways:
- **Shared History:** All agents contribute to one conversation log, suitable for collaborative tasks.
- **Individual Histories:** Each agent maintains its own private log, sharing only final outputs through A2A or Agent-as-a-Tool communication.

### Production Considerations
When scaling to production, session management must ensure:
- **Security & Privacy:** Enforce user-level data isolation, redact personally identifiable information (PII).
- **Data Integrity:** Maintain chronological ordering and apply retention policies (TTL).
- **Performance:** Optimize retrieval and writing speed by reducing token size and applying compaction.

### Compaction Strategies
To manage long conversation histories efficiently:
- **Keep the last N turns.**
- **Token-based truncation.**
- **Recursive summarization** (periodic condensation into summaries).

Compaction can be triggered by:
- **Count-based thresholds** (e.g., turns, tokens).
- **Time-based inactivity.**
- **Event-based triggers** (e.g., topic completion).

---

## 2. Memory

**Memory** enables long-term knowledge persistence across sessions.  
It extracts meaningful information from interactions and stores it in a framework-agnostic form that can be retrieved later to personalize responses.

### Key Roles
- **Personalization:** Remember user preferences, facts, and interactions.
- **Context Compression:** Replace verbose transcripts with summaries or structured data.
- **Insight Generation:** Derive analytics from aggregated memories.
- **Self-Improvement:** Help agents refine reasoning strategies over time.

### Architecture
A memory system typically involves:
1. **User:** Provides data (explicitly or implicitly).
2. **Agent:** Decides what and when to remember.
3. **Framework:** Connects session data with storage and retrieval logic.
4. **Session Store:** Holds raw conversation logs.
5. **Memory Manager:** Handles extraction, consolidation, and retrieval (e.g., Memory Bank, Mem0, Zep).

### Memory vs RAG

| Aspect | RAG Engine | Memory Manager |
|:--|:--|:--|
| Purpose | Provides factual knowledge | Provides personalized knowledge |
| Data Source | Static, external documents | Dynamic user-agent interactions |
| Scope | Shared across users | Isolated per user |
| Update Pattern | Batch updates | Event-based or real-time |
| Output | Global facts | User-specific context |

Together, **RAG** makes an agent *an expert on the world*, while **Memory** makes it *an expert on the user*.

---

## 3. Memory Design

### Types of Memory
- **Declarative (“knowing what”)** – stores facts, events, and entities.
- **Procedural (“knowing how”)** – stores workflows or reasoning strategies.

### Organizational Patterns
- **Collections:** Independent memory units per topic.
- **Structured Profile:** Key-value facts continuously updated (e.g., preferences).
- **Rolling Summary:** Single evolving text summary of the agent–user relationship.

### Storage Architectures
- **Vector Databases:** For semantic similarity retrieval.
- **Knowledge Graphs:** For relational and entity-based reasoning.
- **Hybrid Systems:** Combine both for richer retrieval and reasoning.

### Creation Mechanisms
- **Explicit Memories:** User directly instructs the agent to remember.
- **Implicit Memories:** Agent automatically extracts key details.
- **Internal Memory:** Managed within the framework.
- **External Memory:** Managed by standalone services (e.g., Memory Bank).

### Memory Scope
- **User-Level:** Persistent, personalized across sessions.
- **Session-Level:** Contextual summaries within a single session.
- **Application-Level:** Global procedural or system-wide memories (sanitized).

---

## 4. Memory Generation Pipeline

Memory generation functions like an **LLM-driven ETL process**:
1. **Ingestion:** Accept raw data (e.g., session history).
2. **Extraction:** Identify meaningful facts using schemas or few-shot prompts.
3. **Consolidation:** Merge, update, or delete conflicting or redundant data.
4. **Storage:** Persist the refined information in a vector DB or graph.

This process is asynchronous, maintaining responsiveness while continuously updating knowledge.

### Provenance & Trust
Memories include metadata describing origin, age, and confidence level to maintain reliability.  
The system tracks:
- **Source Type:** Bootstrapped data, user input, or tool output.
- **Confidence Evolution:** Trust grows via corroboration and decays over time.

---

## 5. Memory Operations

### Triggering Generation
Memory creation can be triggered by:
- **Session completion**
- **Fixed turn intervals**
- **Real-time after every turn**
- **Explicit user commands** (“Remember this”)

### Memory-as-a-Tool
Agents can autonomously decide when to generate memories by invoking a `create_memory` tool.  
This approach shifts decision-making to the agent, improving adaptability.

### Background vs Blocking Operations
Memory generation is computationally heavy, so it should run **asynchronously** in the background to keep user interactions responsive.

### Memory Retrieval
Effective retrieval ranks memories using a **hybrid scoring system**:
- **Relevance** (semantic similarity)
- **Recency** (time-based freshness)
- **Importance** (defined significance)

---

## Core Takeaway
- **Sessions** provide **short-term context** for coherent conversations.  
- **Memory** provides **long-term intelligence** for personalization and adaptation.  
Together, they enable agents to evolve from static chatbots into **stateful, learning systems** capable of continuity, reasoning, and understanding across time.

---

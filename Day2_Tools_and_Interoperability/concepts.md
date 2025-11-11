## 🧠 Overview
Day 2 focuses on **how AI Agents use external tools** and the **Model Context Protocol (MCP)** that standardizes these interactions for scalability, interoperability, and security.  
It bridges the gap between foundation models and real-world applications.

---

## Core Concepts

### 1. Foundation Models & Tools
- Foundation models alone are **pattern predictors**, unable to fetch new data or perform actions.
- **Tools** extend their abilities — acting as the agent’s *eyes* (to perceive) and *hands* (to act).

### 2. Definition of a Tool
- A **function or program** that performs tasks beyond the model’s native capacity.
- Two main purposes:
  - **To know:** Retrieve or access data.
  - **To do:** Execute actions through APIs or code.

### 3. Types of Tools
| Type | Description | Example |
|------|--------------|----------|
| **Function Tools** | Custom-defined external functions (e.g., using Google ADK) | Adjusting brightness via `set_light_values` |
| **Built-in Tools** | Predefined model-integrated tools | Gemini’s Google Search, URL Context, Code Execution |
| **Agent Tools** | Sub-agents invoked as tools using `AgentTool()` | A capital-finder agent called by a main user-agent |

---

## Taxonomy of Agent Tools
| Category | Function | Design Focus |
|-----------|-----------|---------------|
| **Information Retrieval** | Fetch structured/unstructured data | Define schemas, handle data types |
| **Action / Execution** | Execute real-world operations | Ensure authorization and error handling |
| **System / API Integration** | Connect with software systems | Secure API keys, manage errors |
| **Human-in-the-Loop** | Collaborate with users | Clarify decisions, require approvals |

---

## ⚙️ Best Practices for Tool Design

### a. Documentation
- Clear names and descriptions
- Defined input/output types
- Short, readable parameter lists
- Default values and practical examples

### b. Describe Actions, Not Implementations
- Tell the model *what* to do, not *how* to do it.
- Avoid redundant or conflicting tool instructions.

### c. Publish Tasks, Not API Calls
- Represent **actions**, not complex backend APIs.
- Tools should encapsulate user-facing, specific tasks.

### d. Granularity
- Keep tools small, single-purpose, and modular.
- Avoid multi-step “super tools” unless necessary.

### e. Concise Output
- Avoid returning large datasets.
- Use external databases or storage for bulky results.

### f. Validation & Error Messages
- Implement schema validation for inputs/outputs.
- Provide human-readable error messages that guide the LLM.

---

## 🔗 Model Context Protocol (MCP)

### Purpose
- Solves the **N × M integration problem** — eliminates the need for custom connectors for every model-tool pair.
- Enables **standardized, modular** communication between agents and external systems.

### Architecture
| Component | Role |
|------------|------|
| **Host** | Manages client creation, user experience, and security |
| **Client** | Connects to servers, sends commands, receives results |
| **Server** | Publishes available tools, executes commands, enforces policies |

### Communication Layer
- **Base Protocol:** JSON-RPC 2.0  
- **Message Types:** Request, Result, Error, Notification  
- **Transports:**  
  - `stdio` for local  
  - `Streamable HTTP` for remote (replaces SSE)

---

## 🧱 MCP Key Primitives

| Entity | Role |
|--------|------|
| **Tools** | Core server capability, describes callable functions |
| **Resources** | Provide contextual/static data |
| **Prompts** | Template prompt examples |
| **Sampling** | Server requests LLM completion from client |
| **Elicitation** | Server requests user data via the client |
| **Roots** | Define file-system scope boundaries |

*(Tools are the most widely implemented and critical capability.)*

---

## 🧩 Tool Definition Schema (JSON)
**Fields:**  
`name`, `title`, `description`, `inputSchema`, `outputSchema`, `annotations`  
- **Annotations examples:** destructiveHint, idempotentHint, readOnlyHint.

---

## ⚠️ Error Handling
Two mechanisms:
1. **Protocol Errors:** Invalid tool or server issue (JSON-RPC level)
2. **Execution Errors:** Returned via `isError: true` with textual explanation

---

## 🧭 Advantages of MCP
- Simplifies integrations and accelerates development  
- Encourages **plug-and-play** reusable tool ecosystem  
- Enables **dynamic tool discovery** at runtime  
- Encourages **standardized tool definitions**  
- Promotes **modular architecture** for flexibility and maintenance  
- Supports **human-in-the-loop** governance and consent mechanisms  

---

## 🚨 Challenges & Security Risks

### 1. Performance
- Context window overload from many tool definitions  
- Degraded reasoning quality  
- Stateful protocol complexity  
**Future direction:** dynamic tool retrieval (RAG-like search for tools).

### 2. Enterprise Gaps
- Weak authentication & authorization standards  
- No unified identity propagation  
- Limited observability (no native logging/tracing)  

### 3. Security Threats
| Threat | Description | Mitigation |
|--------|--------------|-------------|
| **Dynamic Capability Injection** | Server adds/changes tools dynamically | Enforce allowlists, version pinning, change notifications |
| **Tool Shadowing** | Malicious tools mimic legitimate ones | Check naming collisions, enforce TLS, human-in-loop confirmation |
| **Malicious Tool Definitions** | Deceptive descriptions or prompt injections | Input/output sanitization, strict resource validation |
| **Sensitive Data Leaks** | Unauthorized access through conversation context | Tag sensitive outputs, enforce least privilege |
| **No Scope Limitation** | Broad permissions per server | Scoped credentials, side-channel authentication |

---

## ⚡ Appendix: “Confused Deputy Problem”
An AI model (the “confused deputy”) can unintentionally command a privileged MCP server to execute unauthorized actions on behalf of an attacker — such as copying confidential code — if it lacks proper privilege checks.

---

## 🏁 Conclusion
- **Tools** transform models into active agents.  
- **MCP** provides the universal protocol for tool interoperability.  
- However, **security, governance, and standardization** are critical to ensure enterprise readiness.  
- The future of MCP likely involves **centralized control layers** and **secure agent frameworks** to prevent vulnerabilities.
"""

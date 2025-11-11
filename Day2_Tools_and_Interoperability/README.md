# Day 2: Agent Tools & Interoperability with MCP

## Overview
Day 2 of the **Google AI Agents Intensive** explores how agents gain real-world functionality through **tools** and how the **Model Context Protocol (MCP)** standardizes their integration for scalable, secure, and interoperable systems.

Agents evolve from simple pattern predictors into autonomous systems by leveraging external tools, APIs, and structured communication protocols.

---

## Learning Objectives
By the end of this session, you should be able to:
- Understand how tools extend a foundation model’s perception and action abilities  
- Integrate tools into an agentic architecture using APIs and SDKs  
- Explore the **Model Context Protocol (MCP)** for tool standardization  
- Identify best practices in tool design, documentation, and error handling  
- Recognize enterprise and security implications of MCP deployments  

---

## Topics Covered
### 🔧 Tool Fundamentals
- What defines a *tool* in AI systems  
- Difference between **Function Tools**, **Built-in Tools**, and **Agent Tools**  
- Examples from **Google ADK** and **Gemini API**  

### 🧩 Best Practices
- Clear tool documentation (name, description, parameters)  
- Describe actions, not implementations  
- Publish *tasks*, not direct API calls  
- Keep tools **granular** and **concise**  
- Validate inputs and outputs with schemas  
- Provide informative error messages  

### 🌐 Model Context Protocol (MCP)
- Solves the **N × M integration problem** by creating a unified standard  
- Core components: **Host**, **Client**, and **Server**  
- Communication via **JSON-RPC 2.0** over `stdio` or `Streamable HTTP`  
- Defines entities: **Tools**, **Resources**, **Prompts**, **Sampling**, **Elicitation**, **Roots**  

### ⚙️ Tool Definition in MCP
- Structured using JSON schema fields:  
  `name`, `description`, `inputSchema`, `outputSchema`, `annotations`  
- Supports hints like `readOnlyHint`, `idempotentHint`, and `destructiveHint`  
- Tools return structured or unstructured results with validation and error handling  

---

## Security & Enterprise Considerations
### 🚨 Key Risks
- **Dynamic Capability Injection** – unauthorized tool updates  
- **Tool Shadowing** – malicious duplicate tools  
- **Malicious Tool Definitions** – deceptive or unsafe APIs  
- **Sensitive Data Leaks** – unfiltered user or enterprise data  
- **Confused Deputy Problem** – privileged MCP servers misused by low-trust models  

### 🛡️ Mitigations
- Enforce allowlists and version pinning  
- Validate inputs, outputs, and tool definitions  
- Use scoped credentials and principle of least privilege  
- Separate trusted/untrusted planners  
- Add human-in-the-loop checkpoints for critical actions  

---

## Daily Goals
- Integrate at least **2–3 tools** with an agent (e.g., API, search, or control function)  
- Build a **custom tool** to perform a defined user task  
- Understand the **MCP host–client–server architecture**  
- Document your integration steps in `concepts.md`  

---

## Resources
- **notebook_template.ipynb** – for hands-on MCP experiments  
- **Day_2_AI_Agents_Notes.md** – detailed conceptual notes  
- **Day_2_v6.pdf** – official course whitepaper reference  
- **../Resources/** – supplementary materials and SDK documentation  

---

## Next Steps
Proceed to **Day 3: Context and Memory**  
Learn how agents manage internal state, retrieve past information, and use memory for reasoning and decision-making in autonomous workflows.

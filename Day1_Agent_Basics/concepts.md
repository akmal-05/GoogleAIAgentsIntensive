# Day 1: Agent Basics - Key Concepts

## Learned Today

### Core Concepts

- An **AI agent** is a system that perceives its environment, makes decisions, and takes actions to achieve a goal.  
- Unlike a regular chatbot, agents can **reason, act, remember, and adapt**.  
- **Memory** allows agents to store previous interactions and context.  
- **Tools** and APIs let agents extend capabilities beyond just generating text.  
- Common frameworks for agents include **LangChain, AutoGen, CrewAI, and Google Gemini Agents**.

### Agent Architecture

- **ReAct Pattern (Reason + Act)**: Agent first reasons about the task, then takes action.  
- **Tool-Using Agents**: Agents can call APIs or use calculators to complete tasks.  
- **Multi-Agent Systems**: Different agents handle different parts of a workflow and collaborate.  
- **Loop-Based Architecture**: *Observe → Think → Act → Reflect* cycle is how agents handle complex problems.  

### Key Insights

- Agents are **more than chatbots**; they’re autonomous problem-solvers.  
- Using reasoning before acting (ReAct) improves accuracy and decision-making.  
- Even simple experiments can help understand agent workflows without needing complex code.  
- Today’s focus is **understanding how agents think and act**, not writing full applications yet.  

### Code Examples

```python
# Simple reasoning loop (ReAct-style)
task = "Find a good productivity book"
thought = "I should look for popular books on motivation or habits."
action = "Search 'best productivity books'"
result = "Atomic Habits by James Clear is top rated."

print(f"Thought: {thought}")
print(f"Action: {action}")
print(f"Result: {result}")

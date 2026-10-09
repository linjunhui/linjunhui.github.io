# What is An AI Agent?
- Goal-oriented to accomplish user objectives
- Core capabilities: Perception, Planning/Decision, Action, Reflection
- Execution Paradigm: ReAct (Reason + Act)
- Agent = Model + Harness

## Four Components of Agent
### Model
- LLM reasoning engine
  - OpenAI-compatible endpoints
  - Anthropic, etc.

### Tools
- External skills / capabilities
- MCP (Model Context Protocol)

### Memory
- Short-term memory: in-context conversation history
- Long-term memory: persisted storage, vector DB

### Loop
- The runtime cycle that ties everything together
- Supports different paradigms: ReAct, Plan-and-Execute, Reflexion

# Memory
## Short-Term Memory
### Pain Points
- Multi-turn conversations cause context bloat
- Skyrocketing token costs; API calls are charged based on input and output tokens
- Degraded model performance: Attention Dilution and Lost in the Middle

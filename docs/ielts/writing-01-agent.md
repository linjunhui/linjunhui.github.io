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

### Short-Term Memory Manage Strategy
#### Strategy 1: Simple "Forgetting" — Fixed Window Truncation (Context Truncation)
The simplest and most straightforward approach is to retain only the most recent events, known as **fixed window truncation**.

**Idea**: Define a fixed window size, for example keeping only the latest N turns of conversation, or more precisely, the latest N tokens. When the conversation history exceeds this threshold, the oldest turn is discarded, ensuring the total context length remains roughly constant.

**Pros**: Extremely easy to implement with low computational overhead. It reliably keeps the context length within bounds, preventing runtime errors and unbounded cost escalation.

**Applicable Scenarios**: Suited for use cases where information value decays rapidly over time, such as chatbots or basic customer service Q&A systems.

**Boundary Limitations**: This is a "one-size-fits-all" forgetting strategy. If critical information from early in the conversation (e.g., the core objective set by the user in the first turn) gets truncated, the Agent will suffer "memory loss" again and break the logical flow of dialogue.

**Performance Pitfalls**: Even if the maximum window limit is not breached, truncation triggered only when the window is nearly full means the Agent constantly operates with context close to the length limit. Due to **attention dilution**, this degrades the model’s capability to handle complex tasks.

In `AgentScope`, this capability is implemented by the `Formatter` component. You may pass the `max_tokens` parameter during `Formatter` initialization to constrain the context length.

> Terminology notes (consistent with LLM/Agent engineering convention):
> - Token: kept untranslated (standard term)
> - AgentScope: project name, retain original casing
> - Formatter: component name, retain original casing
> - attention dilution: attention机制稀释效应，采用领域通用译法
> - context truncation: 上下文截断
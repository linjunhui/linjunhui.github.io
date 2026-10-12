# Harness: The Engineering Backbone of LLM Agent
## 1. Core Definition
**Agent = LLM + Harness**
- **LLM**: The brain of the Agent. It understands objectives and makes decisions.
- **Harness**: The entire supporting system excluding the LLM. It schedules and governs the whole workflow of the Agent, ensuring the LLM executes tasks stably and reliably.

> Traditional chatbots can only generate text responses. They cannot operate external tools or complete tasks autonomously. An Agent can perform tasks independently, and Harness is the engineering system that enables this capability.

> Background: Before the first half of 2026, the definition of Agent was vague. An application was often called an Agent as long as it used an LLM to finish certain tasks, with core features including perception, planning and tool calling.
> In the second half of 2026, the industry converged to the formula: **Agent = LLM + Harness**.

## 2. Core Components of Harness
| Component | Function |
| ---- | ---- |
| Memory System | Stores historical interactions and provides context for the model. |
| Tools | The "hands" of the Agent. They convert the model’s decisions into real actions, such as file reading and API calls. |
| Rules | Code of conduct for the Agent. It defines what actions are allowed or forbidden, and sets output specifications. |
| Task Loop Controller | The core of Harness. It coordinates all modules and decides whether to continue or terminate the loop (Think → Act → Check). |
| Extensible Modules | No fixed component list. New modules can be added on demand. For example, context management filters relevant information from full memory for the current task to avoid context waste and reduce irrelevant interference. |

## 3. Workflow (Code Review Agent Example)
1. **Assemble context**: After receiving a task, Harness assembles system prompts, user instructions, rules and filtered historical memory into a complete context and sends it to the LLM.
2. **Execute tool calls**: The LLM returns tool call commands, and Harness executes the corresponding tool operations.
3. **Iterative loop**: Harness appends tool return results to the context and sends it to the LLM for another round of reasoning. This loop repeats.
4. **Final output**: When the LLM stops requesting tool calls and directly produces the final conclusion, Harness captures and formats the result, then terminates the task.

## 4. Four Operating Modes of DeepSeek Harness
- **Standard Mode**: Equipped with rich built-in tools, supporting shell, file editing and web search.
- **ETC Mode**: Uses TypeScript code to implement multi-step tool calls.
- **Minimal Mode**: Only keeps shell and file editing for a lightweight environment.
- **Custom Agent Mode**: The mode demonstrated in the video. Users can define tool permissions and business rules to build dedicated Agents.

## 5. Key Takeaway
The capability ceiling of the LLM determines the potential of an Agent.
**The engineering quality of Harness determines whether this potential can be stably delivered.**
No matter how powerful the LLM is, it is prone to errors and out-of-control behavior in real-world scenarios without a reliable scheduling system.
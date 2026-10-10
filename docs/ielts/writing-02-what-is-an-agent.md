# What is an Agent?

> Written as an IELTS writing practice piece — and, going forward, as a place to
> connect my daily work with what I'm learning about LLM Agents.

## The one-sentence answer

An **agent** is a system that **perceives its environment, decides what to do, and takes actions** to reach a goal — rather than simply answering a question once and stopping.

That last part is what separates an agent from a plain chatbot. A chatbot *responds*; an agent *acts*.

## The loop that defines it

Most definitions, from robotics to modern AI, boil down to the same cycle:

```
Perceive  →  Think / Plan  →  Act  →  Observe the result  →  (repeat)
```

- **Perceive** — take in the current state of the world (a request, a data feed, a screen, a sensor).
- **Think / Plan** — decide which step moves closest to the goal.
- **Act** — do something that changes the world (call an API, write a file, send a message).
- **Observe** — see what happened, then loop again until the goal is met.

An agent is not defined by *being smart*, but by **running this loop and being allowed to change things**.

## A helpful contrast

| | Chatbot | Agent |
| --- | --- | --- |
| Behaviour | One reply, then stops | Repeats a perceive–act loop until done |
| Tools | Usually none | Calls tools / APIs to affect the world |
| Memory | Per message | Keeps state across steps |
| Failure mode | A wrong answer | A wrong *action* |

> A chatbot tells you how to book a flight. An agent actually books it — and checks the confirmation.

## Why LLM agents are different

Before large language models, an agent's "brain" had to be hand-programmed: every rule, every branch. That is why classic agents were brittle — they only handled situations someone had anticipated.

An **LLM agent** uses a language model as the reasoning core. The model can interpret messy, open-ended language, break a goal into steps, and choose which tool to call next. Suddenly the "think" step becomes flexible, and the same agent can handle tasks nobody explicitly wrote rules for.

The typical anatomy of an LLM agent:

| Part | Role |
| --- | --- |
| **Model** | The reasoning core — plans and decides |
| **Tools** | The hands — APIs, search, code execution, file access |
| **Memory** | Continuity — what happened so far |
| **Loop controller** | Decides when to stop, retry, or ask for help |

## Where it shows up at work

This is the part I want to keep writing about, because it connects directly to my day job:

- **Automation** — an agent that watches a queue, classifies requests, and routes them.
- **Copilots** — an agent that drafts, reviews, or refactors work inside an existing tool.
- **Data workflows** — an agent that pulls data, runs analysis, and reports back.
- **Multi-agent systems** — several agents, each with a narrow role, cooperating on one goal.

## The honest caveats

Agents are not magic, and writing about them honestly matters more than writing about them enthusiastically:

1. **Reliability** — a wrong action is worse than a wrong answer; guardrails are essential.
2. **Cost & latency** — every loop step costs money and time.
3. **Evaluation** — "did it succeed?" is much harder to measure than "was the answer correct?".
4. **Autonomy vs control** — the more an agent can do, the more it can do *wrongly*. Human checkpoints matter.

## One-line takeaway

> **A chatbot answers; an agent acts. An LLM agent acts *adaptively*, because its reasoning core can handle goals nobody explicitly programmed.**

---

*Next, I plan to write about how agents plan, how they use tools, and what I'm actually building at work.*

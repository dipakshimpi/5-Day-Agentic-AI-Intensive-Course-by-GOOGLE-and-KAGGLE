# 🚀 5-Day Agentic AI Intensive Course by GOOGLE

A comprehensive course on building intelligent AI agents using the Google Agent Development Kit (ADK). This repository contains materials for a 5-day intensive course covering everything from prompt engineering to production-ready agent systems.

## 📚 Course Overview

### [Day 1 — From Prompt to Agent Architectures](Day_1/)
**Learn the fundamentals of AI agent development**
- Prompt fundamentals: intent, context, constraints, and examples
- Mapping prompts to actions: parsing, templates, and structured instructions
- Agent design basics: perception → decision → action loop
- Agent architectures: reactive, deliberative, hierarchical, and tool-augmented agents
- Reasoning patterns: chain-of-thought and stepwise decomposition
- Evaluation & safety considerations

**Notebooks:**
- `day-1a-from-prompt-to-action.ipynb` - Practical walkthrough of prompt design and action execution
- `day-1b-agent-architectures.ipynb` - Overview and comparisons of agent architectures

### [Day 2 — Agent Tools & Best Practices](Day_2/)
**Build powerful, actionable agents that interact with the world**
- Custom function tools: turning Python functions into agent tools
- Agents as tools: creating specialist agents for reliable task execution
- Model Context Protocol (MCP): connecting to external services
- Long-running operations: human-in-the-loop approval workflows
- Resumable agent workflows with state management

**Key Components:**
- `FunctionTool`, `BuiltInCodeExecutor`, `AgentTool`
- `McpToolset` for external service integration
- `ToolContext` and `request_confirmation()` for pausable operations
- `App` with `ResumabilityConfig` for stateful agents

### [Day 3 — Memory & Sessions](Day_3/)
**Build stateful agents with short-term and long-term memory**
- Session management: `Sessions`, `Events`, and `State`
- `InMemorySessionService` and `DatabaseSessionService`
- Context compaction for efficient long conversations
- Long-term memory: searchable knowledge stores
- Memory consolidation: extracting key facts from conversations

**Notebooks:**
- `day-3a-agent-sessions.ipynb` - Session management and short-term memory
- `day-3b-agent-memory.ipynb` - Long-term memory and knowledge stores

### [Day 4 — Agent Observability & Evaluation](Day_4/)
**Make agents observable, debuggable, and production-ready**
- Agent observability: tracking traces, logs, and reasoning steps
- Tool usage analysis and latency monitoring
- Human-in-the-loop and automated evaluation
- Regression testing for agent workflows
- LLM-based scoring and custom evaluation pipelines

**Tools & Frameworks:**
- LangSmith for observability and evaluation
- Weights & Biases for metrics visualization
- Custom evaluation pipelines

### [Day 5 — AgentOps & Enterprise-Grade Agent Deployment](Day_5/)  
Day 5 focused on **AgentOps**, the discipline required to turn simple AI agent prototypes into **reliable, scalable, enterprise-ready systems**.  
The key idea: **Building an agent is easy. Operating it in production is hard.**

## 🚀 Quick Start

### Prerequisites
- Python 3.10+
- Gemini API key from [Google AI Studio](https://aistudio.google.com/app/api-keys)

### Installation
```bash
pip install google-adk
```

### 💡 Key Concepts
**Agent Architectures:** Choose the right pattern for your use case

**Tool Integration:** Extend agent capabilities with custom and external tools

**Memory Management:** Balance short-term context with long-term knowledge

**Observability:** Understand and debug agent decision-making

**Evaluation:** Ensure reliable and safe agent behavior

**Human-in-the-Loop:**  Critical for high-stakes operations

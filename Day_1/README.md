# Day 1 — From Prompt to Agent Architectures

What you'll learn
- Prompt fundamentals: intent, context, constraints, and examples — how to structure prompts for reliable outputs.
- Mapping prompts to actions: parsing, templates, and extracting structured instructions to drive tools or APIs.
- Action types and tooling: common actions (API calls, search, file ops, calculators) and how to wrap them as tools.
- Agent design basics: perception → decision → action loop, memory patterns, and simple control flow for agents.
- Agent architectures: reactive, deliberative/planning, hierarchical, and tool-augmented agents — tradeoffs and when to use each.
- Reasoning patterns: chain-of-thought, stepwise decomposition, and planning-to-action strategies.
- Evaluation & safety: correctness, robustness, latency, cost considerations, and basic guardrails for unsafe or ambiguous instructions.
- Hands-on practice: apply concepts in the notebooks linked below and compare approaches.

Files
- [.gitignore](.gitignore)
- [Day_1/day-1a-from-prompt-to-action.ipynb](Day_1/day-1a-from-prompt-to-action.ipynb) — Notebook: practical walkthrough of prompt design, parsing, and executing actions.
- [Day_1/day-1b-agent-architectures.ipynb](Day_1/day-1b-agent-architectures.ipynb) — Notebook: overview and comparisons of agent architectures.
- [Day_1/README.md](Day_1/README.md) — This file.

Suggested exercises
- Design a prompt that reliably extracts a structured task (e.g., "extract a date and action") and implement a parser in a notebook.
- Build a minimal tool wrapper (e.g., calculator or web search simulator) and connect it to a prompt-driven agent loop.
- Implement two small agents (reactive vs. deliberative) for the same task and compare outcomes and costs.

Quick start
1. Open the notebooks:
   - VS Code: File → Open Folder → select the repository root, then open the notebooks from the Explorer.
   - Jupyter: run `jupyter notebook` or `jupyter lab`.
2. Run the cells in [Day_1/day-1a-from-prompt-to-action.ipynb](Day_1/day-1a-from-prompt-to-action.ipynb) then [Day_1/day-1b-agent-architectures.ipynb](Day_1/day-1b-agent-architectures.ipynb).
3. Try the suggested exercises and iterate on prompts and tool designs.

Next steps
- Move to Day 2 to expand toolsets, integrated environments, and multi-step planning patterns.
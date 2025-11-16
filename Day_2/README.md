# Day 2 - Agent Tools & Best Practices

Welcome to Day 2 of the 5-Day Agentic AI course! This session moves beyond basic agents and into building powerful, actionable agents that can interact with the world, execute code, and perform complex, multi-step tasks.

This day is split into two main parts:
1.  **Agent Tools:** Learning to create custom tools from Python functions and using other agents as tools.
2.  **Tool Patterns & Best Practices:** Learning to connect to external services (MCP) and building resumable workflows that require human approval (Long-Running Operations).

---

## 🧠 What We Learned in Day 2

### Part 1: Building Custom Agent Tools (`day-2a-agent-tools.ipynb`)

We started by learning why tools are essential: they give agents access to live data, allow them to overcome knowledge cutoffs, and empower them to take real-world actions.

#### 🛠️ Key Learning 1: Custom Function Tools

You can turn **any Python function** into a tool that an agent can use. We built a Currency Converter agent to demonstrate this.

* **How:** Simply define your Python function and pass it into the `tools=[]` list when creating an `LlmAgent`.
* **Example:** We created `get_fee_for_payment_method` and `get_exchange_rate` functions. The agent's LLM learned to call these functions in sequence to answer a user's query.
* **Best Practices:**
    * **Clear Docstrings:** The LLM uses the docstring to understand what the tool does and when to use it.
    * **Type Hints:** Use type hints (e.g., `method: str`) so the ADK can build a correct schema.
    * **Structured Returns:** Return a dictionary (e.g., `{"status": "success", ...}` or `{"status": "error", ...}`) so the agent can understand the tool's result and handle failures.

#### 🤖 Key Learning 2: Agents as Tools (for Reliable Code Execution)

LLMs are not reliable at complex math. To solve this, we learned to delegate tasks to specialist agents.

* **The Problem:** The currency agent needed to calculate the final amount, but LLM math can be wrong.
* **The Solution:** We built a `calculation_agent` whose only job was to execute Python code using the `BuiltInCodeExecutor()`.
* **The Concept:** We then used this `calculation_agent` as a tool for our main `enhanced_currency_agent` by wrapping it with `AgentTool(agent=calculation_agent)`.

This powerful pattern allows a "manager" agent to delegate specialized, reliable tasks (like code execution or database lookups) to other "specialist" agents.

---

### Part 2: Advanced Tool Patterns (`day-2b-agent-tools-best-practices.ipynb`)

In the second half, we explored production-ready patterns for complex, real-world workflows.

#### 🌐 Key Learning 3: Model Context Protocol (MCP)

* **What is it?** MCP is an **open standard** that lets agents use community-built integrations for external services (like GitHub, Slack, Google Maps, or databases) without you having to write custom API clients.
* **How:** We used the `McpToolset` component to connect our agent to an external MCP server.
* **Example:** We connected to the `@modelcontextprotocol/server-everything` test server and used its `getTinyImage` tool. The agent was able to call this external tool just as easily as it called our local Python functions.

#### ⏳ Key Learning 4: Long-Running Operations (Human-in-the-Loop)

This is the most advanced concept from Day 2. We learned how to build agents that can **pause, wait for human approval, and then resume** their work.

* **When to use:** For critical actions that need approval, such as financial transactions, bulk deletions, or high-cost operations.
* **Example:** We built a `place_shipping_order` tool that would auto-approve small orders (≤5 containers) but **pause** and request human approval for large orders (>5 containers).

This introduced a new, resumable workflow with three key components:

1.  **The Tool (`place_shipping_order`):**
    * The function signature now accepts a `tool_context: ToolContext`.
    * When approval is needed, it calls `tool_context.request_confirmation(...)` and returns a `{"status": "pending"}`. This **pauses** the agent.
    * When the agent is resumed, the `tool_context.tool_confirmation` object will be populated, and the tool can check `tool_context.tool_confirmation.confirmed` to see the human's decision.

2.  **The App (`ResumabilityConfig`):**
    * A simple `LlmAgent` is stateless and cannot be resumed.
    * To support pausing, you must wrap the agent in an `App` and enable resumability:
        ```python
        shipping_app = App(
            root_agent=shipping_agent,
            resumability_config=ResumabilityConfig(is_resumable=True),
        )
        ```

3.  **The Workflow (The Calling Code):**
    * The code that *runs* the agent must now be built to handle the pause.
    * **Step 1:** Call `shipping_runner.run_async(...)` and save the `invocation_id` from the events.
    * **Step 2:** Your code must check the events for the special `adk_request_confirmation` event.
    * **Step 3:** If this event is found, the agent is paused. Your application would show a UI to get the human's decision (we simulated this with `auto_approve=True`).
    * **Step 4:** To resume, you call `shipping_runner.run_async(...)` **again**, passing in the human's decision *and the original `invocation_id`*. This tells the ADK to load the saved state and continue exactly where it left off.

---

## SUMMARY: Day 2 Key Concepts & Components

| Component | What It Is | When to Use It |
| :--- | :--- | :--- |
| **`FunctionTool`** | A custom Python function given to an agent. | For custom business logic (e.g., `get_exchange_rate`). |
| **`BuiltInCodeExecutor`** | A built-in tool that runs sandboxed Python code. | For reliable math or data processing. |
| **`AgentTool`** | A wrapper that lets one agent be used as a tool by another. | To create "specialist" agents and delegate tasks. |
| **`McpToolset`** | A tool to connect to external, standardized MCP servers. | To use 3rd-party services (Maps, DBs) without writing API clients. |
| **`ToolContext`** | An argument automatically passed to a tool. | To build long-running tools that can pause. |
| **`request_confirmation()`** | A method on `ToolContext` that pauses agent execution. | To request human-in-the-loop approval. |
| **`App` & `ResumabilityConfig`** | A wrapper for an agent that enables state saving. | **Required** for all long-running, pausable operations. |
| **`invocation_id`** | A unique ID for an agent's execution run. | To tell the ADK which paused session to resume. |
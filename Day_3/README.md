# Kaggle 5-Day Agents Course - Day 3: Memory & Sessions

This repository contains the notebooks for Day 3 of the Kaggle 5-day Agents course, focusing on memory management using the Google Agent Development Kit (ADK).

These notebooks explore how to build stateful agents that can remember information both within a single conversation (short-term memory) and across multiple conversations (long-term memory).

## Notebooks Included

1.  **`day-3a-agent-sessions.ipynb`**: **Part 1 - Session Management**
    * **Concept**: Learn how to manage short-term memory within a single conversation thread.
    * **Key Topics**:
        * Understanding `Sessions`, `Events`, and `State`.
        * Using `InMemorySessionService` for temporary, in-memory state.
        * Using `DatabaseSessionService` (with SQLite) for persistent sessions that survive restarts.
        * Managing long conversations efficiently with **Context Compaction**.
        * Using custom tools to read from and write to the `session.state`.

2.  **`day-3b-agent-memory.ipynb`**: **Part 2 - Memory Management**
    * **Concept**: Learn how to build a long-term, searchable knowledge store for your agent.
    * **Key Topics**:
        * Distinguishing between short-term **Sessions** and long-term **Memory**.
        * Populating the memory store using `add_session_to_memory()`.
        * Enabling agents to retrieve information using the `load_memory` (reactive) and `preload_memory` (proactive) tools.
        * Automating memory storage using ADK callbacks (`after_agent_callback`).
        * Conceptual overview of **Memory Consolidation** (extracting key facts from raw conversation).

## 🚀 Getting Started

### 1. Prerequisites

* Python 3
* The `google-adk` library. You can install it via pip:
    ```bash
    pip install google-adk
    ```

### 2. Configure Your Gemini API Key

These notebooks require a Gemini API key to function.

1.  **Get your API key**: If you don't have one, create an API key in [Google AI Studio](https://aistudio.google.com/app/api-keys).
2.  **Add the key to Kaggle Secrets**:
    * In the Kaggle notebook editor, select `Add-ons` > `Secrets`.
    * Create a new secret with the label `GOOGLE_API_KEY`.
    * Paste your API key into the "Value" field and click "Save".
    * Ensure the checkbox next to `GOOGLE_API_KEY` is selected to attach the secret to the notebook.

### 3. Running the Notebooks

* Open either `.ipynb` file in a Jupyter environment (like Kaggle, Google Colab, or VS Code).
* Run the cells in order from top to bottom.
* **Important**: As noted in the notebooks, avoid using the **"Run all"** command. This can trigger rate limits (429 errors) when calling the Gemini API.

### ℹ️ Course Information

As mentioned in the notebooks, these are for hands-on practice and learning. **No submission is required** to complete the course. For help, please refer to the Kaggle Discord server mentioned in the notebook instructions.
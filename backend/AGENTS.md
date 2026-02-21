# Backend Agent Guidelines

## Component Overview
**Role:** Core logic, database connectivity, agent orchestration, and analysis.
**Tech:** Python, LangGraph, FastMCP, Pandas Profiling.

## Setup & Dev
1. **Navigate:** `cd backend`
2. **Install:** `pip install -r requirements.txt`
3. **Run API/Agent:**
   ```bash
   python src/main.py
   ```

## Structure
- `src/`: Main application logic.
- `adapters/`: Database connectors (Postgres, Snowflake, etc.).
- `agents/`: LangGraph workflows.
- `tests/`: Unit and integration tests.

## Testing
- **Run All Tests:** `pytest tests/`
- **Specific Module:** `pytest tests/test_adapters.py`

## Logging
- **Critical:** All database interactions and agent decisions MUST be logged.
- **Files:**
  - `../logs/ingestion.jsonl` for DB extraction.
  - `../logs/agent_runs.jsonl` for LangGraph execution steps.
- **Example Log:**
  ```json
  {
    "timestamp": "2026-02-21T14:30:00Z",
    "component": "backend.agent.orchestrator",
    "operation": "plan_query",
    "steps": ["received_user_intent", "selected_tool_sql_gen"],
    "outputs": { "tool": "sql_generator" }
  }
  ```

# Intelligent Data Dictionary Agent

## Project Overview
**Goal:** Build an intelligent agent that connects to enterprise databases, extracts metadata, performs quality analysis, and provides a conversational interface for data discovery.

**Tech Stack:**
- **Frontend:** Streamlit
- **Backend:** Python, LangGraph, FastMCP, Pandas Profiling
- **Database Support:** PostgreSQL, SQL Server, Snowflake
- **LLM:** OpenAI / Anthropic

## Global Setup
1. **Python Environment:**
   ```bash
   python -m venv venv
   source venv/bin/activate  # Windows: venv\Scripts\activate
   ```
2. **Install Dependencies:**
   ```bash
   pip install -r backend/requirements.txt
   pip install -r frontend/requirements.txt
   ```
3. **Environment Variables:**
   - Copy `.env.example` to `.env`
   - Configure database credentials and LLM API keys.

## Global Conventions
- **Code Style:** Black (Python), Flake8.
- **Commits:** Conventional Commits (e.g., `feat: add snowflake adapter`, `fix: metadata extraction bug`).
- **Pathing:** Use absolute paths or project-root relative paths.

## Structured Logging Conventions
All components must log to `/logs/` in JSON lines (`.jsonl`) format.

### Log File Names
- `agent_runs.jsonl`: Core agent workflow execution.
- `ingestion.jsonl`: Database metadata extraction tasks.
- `processing.jsonl`: Data quality and statistical analysis.
- `system.jsonl`: General system events and errors.

### Log Entry Structure
Each log entry must be a valid JSON object with the following schema:
```json
{
  "timestamp": "2026-02-21T10:00:00Z",  // ISO8601
  "component": "backend.adapter.snowflake", // or "frontend.chat"
  "level": "INFO", // INFO, WARN, ERROR, DEBUG
  "operation": "extract_schema",
  "inputs": { "table": "orders" },
  "steps": ["connected", "queried_information_schema", "closed"],
  "outputs": { "column_count": 15 },
  "error": null
}
```

### Reading Logs
Agents should parse these logs to understand past execution states or debug failures.

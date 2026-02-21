# Frontend Agent Guidelines

## Component Overview
**Role:** User Interface for the Intelligent Data Dictionary.
**Tech:** Streamlit (Python).

## Setup & Dev
1. **Navigate:** `cd frontend`
2. **Install:** `pip install -r requirements.txt`
3. **Run:**
   ```bash
   streamlit run src/app.py
   ```

## Code Style
- **Formatter:** Black
- **Linting:** Pylint/Flake8
- **Structure:**
  - `src/app.py`: Main entry point.
  - `src/components/`: Reusable UI widgets (chat bubble, sidebar).
  - `src/utils/`: Helper functions.

## Testing
- **Unit Tests:** `pytest tests/`
- **UI Tests:** Playwright (optional for later).

## Logging
- Write logs to `../logs/frontend.jsonl` (or via API to backend logger).
- **Format:**
  ```json
  {
    "timestamp": "...",
    "component": "frontend.ui",
    "operation": "user_query",
    "inputs": { "query": "Show me the orders table" },
    "outputs": { "response_time_ms": 120 }
  }
  ```

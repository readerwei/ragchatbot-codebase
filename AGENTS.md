# Repository Guidelines

## Project Structure & Module Organization
- `backend/` hosts the FastAPI service: `app.py` exposes routes, `rag_system.py` orchestrates retrieval, `vector_store.py` wraps Chroma, and `document_processor.py` ingests course files.
- `backend/tests/` contains pytest suites for config, vector store, and API coverage; mirror this layout when adding new modules.
- `frontend/` holds the static client (`index.html`, `script.js`, `style.css`) served by FastAPI; update assets here for UI work.
- `docs/` stores reference material such as `query_flow_diagram.txt`; revise diagrams when flows or data sources shift.
- Utility artifacts include `scripts/` for shared automation and `run.sh` for combined backend/frontend startup.

## Build, Test, and Development Commands
- `uv sync [--group dev]` installs runtime (and optionally dev) dependencies defined in `pyproject.toml`.
- `./run.sh` launches the stack with default ports; use it for smoke-testing UI plus API changes.
- `cd backend && uv run uvicorn app:app --reload --port 8000` runs the API only for backend debugging.
- `uv run pytest` executes the full test suite; append `-m "unit"` or similar markers for focused runs.
- `./scripts/format.sh` auto-applies isort/black then lint/type checks; `./scripts/lint.sh` runs the same checks read-only.

## Coding Style & Naming Conventions
- Python follows Black’s 88-character formatting, 4-space indentation, snake_case modules/functions, and PascalCase classes.
- Maintain full type annotations; mypy runs in strict mode, so prefer explicit return types and typed dataclasses.
- Organize imports per isort’s Black profile, grouping first-party modules under `backend`.
- Frontend JS stays in ES6 style with camelCase helpers, while CSS selectors remain kebab-case.

## Testing Guidelines
- Place new tests under `backend/tests` and name files `test_*.py`; share fixtures via `conftest.py`.
- Use pytest markers (`@pytest.mark.unit`, `integration`, `api`, `slow`) to signal scope; avoid shipping new slow tests without justification.
- Mock external services (Anthropic, Chroma) via pytest fixtures or `httpx.AsyncClient` to keep runs deterministic.
- Run `uv run pytest --maxfail=1 --disable-warnings` before submitting changes to catch regressions early.

## Commit & Pull Request Guidelines
- Write short, imperative commit messages around one change set (e.g., `Add dark/light theme toggle feature`).
- Separate concerns such as dependency bumps or static asset updates into their own commits for easier review.
- PRs should include a behavior summary, linked issue or task, and screenshots for UI-visible updates.
- Confirm `./scripts/lint.sh` and `uv run pytest` pass locally; note any skipped checks directly in the PR description.

## Environment & Configuration
- Store secrets in an untracked `.env` (e.g., `ANTHROPIC_API_KEY`) and load them through `dotenv` in `backend/config.py`.
- Document new configuration flags both in `config.py` defaults and the README so deploy scripts stay aligned.

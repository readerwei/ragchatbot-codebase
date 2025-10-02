# Course Materials RAG System

## Project Overview

A Retrieval-Augmented Generation (RAG) system designed to answer questions about course materials using semantic search and AI-powered responses. This is a full-stack web application that enables users to query course materials and receive intelligent, context-aware responses using ChromaDB for vector storage and Anthropic's Claude for AI generation.

### Architecture Overview

The application consists of both frontend and backend components:

**Backend (Python/FastAPI):**
- `app.py`: Main FastAPI application with API routes and static file serving
- `rag_system.py`: Main orchestrator coordinating document processing, vector storage, and AI responses
- `vector_store.py`: ChromaDB-based vector storage with dual collections (course catalog and content)
- `ai_generator.py`: Anthropic Claude API integration with tool-based search capabilities
- `document_processor.py`: Handles document ingestion and chunking
- `search_tools.py`: Implements tool-based search system
- `session_manager.py`: Manages conversation history

**Frontend (HTML/CSS/JS):**
- Single-page application with chat interface
- Real-time course statistics display
- Markdown rendering for AI responses
- Responsive design with sidebar for course information

## Key Technologies

- **Backend:** Python 3.13+, FastAPI, Uvicorn
- **Frontend:** HTML, CSS, JavaScript (ES6)
- **AI Service:** Anthropic Claude (claude-sonnet-4-20250514)
- **Vector Store:** ChromaDB
- **Embeddings:** Sentence Transformers (all-MiniLM-L6-v2)
- **Package Manager:** uv
- **Testing:** pytest

## Building and Running

### Prerequisites

- Python 3.13 or higher
- uv (Python package manager)
- Anthropic API key

### Setup

1. **Install uv:**
   ```bash
   curl -LsSf https://astral.sh/uv/install.sh | sh
   ```

2. **Install dependencies:**
   ```bash
   uv sync
   ```

3. **Set up environment:**
   Create a `.env` file in the root directory:
   ```
   ANTHROPIC_API_KEY=your_anthropic_api_key_here
   ```

### Running the Application

**Quick Start:**
```bash
chmod +x run.sh
./run.sh
```

**Manual Start:**
```bash
cd backend
uv run uvicorn app:app --reload --port 8000
```

The application will be available at:
- Web Interface: `http://localhost:8000`
- API Documentation: `http://localhost:8000/docs`

### Testing

Run all tests:
```bash
uv run pytest
```

Run specific test markers:
```bash
uv run pytest -m "unit"
```

## Development Conventions

### Code Style
- Python follows Black formatting with 88-character line length and 4-space indentation
- Use snake_case for Python modules/functions and PascalCase for classes
- Frontend JavaScript uses camelCase helpers and ES6 style
- CSS selectors use kebab-case
- Maintain full type annotations throughout codebase

### Project Structure
- `backend/`: FastAPI service with modules for rag_system, vector_store, document processing, etc.
- `frontend/`: Static client files (index.html, script.js, style.css)
- `docs/`: Course material documents for the RAG system
- `backend/tests/`: Pytest suites following naming convention `test_*.py`
- `scripts/`: Utility scripts for formatting, linting, and other automation

### Import Organization
- Use `isort` with Black profile for organizing imports
- Group first-party modules under `backend`

### Testing Guidelines
- Use pytest markers: `@pytest.mark.unit`, `integration`, `api`, `slow`
- Mock external services (Anthropic, Chroma) for deterministic test runs
- Place new tests in `backend/tests` directory with `test_*.py` naming

### Commit & Pull Request Guidelines
- Write short, imperative commit messages focused on one change set
- Separate concerns like dependency updates or static asset changes into individual commits
- Include behavior summary and linked issues in PRs
- Run `./scripts/lint.sh` and `uv run pytest` before submitting changes

### Environment & Configuration
- Store secrets in an untracked `.env` file
- Configuration managed through `backend/config.py` dataclass
- Document new configuration flags in both config.py defaults and README

### Code Quality Tools
Install development dependencies:
```bash
uv sync --group dev
```

Format code (modifies files):
```bash
./scripts/format.sh
```

Lint code (read-only):
```bash
./scripts/lint.sh
```

## Data Flow

1. Course documents (PDF, DOCX, TXT) in `docs/` directory are loaded on startup
2. DocumentProcessor chunks content and extracts course metadata
3. VectorStore stores metadata and content in separate ChromaDB collections
4. User queries trigger AI generation with access to search tools
5. AI uses CourseSearchTool to find relevant content and generates responses
6. Frontend displays responses with source attribution
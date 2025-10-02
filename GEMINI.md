# GEMINI.md

## Project Overview

This is a full-stack web application that provides a Retrieval-Augmented Generation (RAG) system for answering questions about course materials.

**Main Technologies:**

*   **Backend:** Python, FastAPI, Uvicorn
*   **Frontend:** HTML, CSS, JavaScript
*   **AI:** Anthropic's Claude
*   **Vector Store:** ChromaDB
*   **Embeddings:** Sentence Transformers
*   **Package Manager:** uv

**Architecture:**

The application is composed of a frontend and a backend.

*   The **backend** is a FastAPI application that exposes a REST API for querying the RAG system. It handles document processing, vector storage, and AI-powered response generation.
*   The **frontend** is a single-page application that provides a chat interface for users to interact with the RAG system.

## Building and Running

**Prerequisites:**

*   Python 3.13 or higher
*   uv (Python package manager)
*   An Anthropic API key

**Installation:**

1.  **Install uv:**
    ```bash
    curl -LsSf https://astral.sh/uv/install.sh | sh
    ```

2.  **Install Python dependencies:**
    ```bash
    uv sync
    ```

3.  **Set up environment variables:**

    Create a `.env` file in the root directory:
    ```bash
    ANTHROPIC_API_KEY=your_anthropic_api_key_here
    ```

**Running the Application:**

*   **Quick Start:**
    ```bash
    chmod +x run.sh
    ./run.sh
    ```

*   **Manual Start:**
    ```bash
    cd backend
    uvicorn app:app --reload --port 8000
    ```

The application will be available at:

*   **Web Interface:** `http://localhost:8000`
*   **API Documentation:** `http://localhost:8000/docs`

**Testing:**

To run the tests, use the following command:

```bash
pytest
```

## Development Conventions

*   **Code Style:** The project uses `black` for code formatting, `isort` for import sorting, and `flake8` for linting.
*   **Type Checking:** The project uses `mypy` for static type checking.
*   **Testing:** The project uses `pytest` for testing. Tests are located in the `backend/tests` directory.

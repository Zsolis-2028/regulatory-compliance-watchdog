# api.py — FastAPI RAG & Agent Backend

A Python backend built with **FastAPI** and **LangChain** that provides two AI-powered endpoints: a Retrieval-Augmented Generation (RAG) endpoint for answering questions grounded in EPA documents, and a zero-shot ReAct agent endpoint for more general reasoning tasks.

---

## Overview

This service is the backend component of a regulatory research tool. Documents are sourced from the **Federal Register API**, loaded as PDFs, split into chunks of 1000 characters (with 200-character overlap), embedded using a local HuggingFace model, and stored in a persistent **Chroma** vector database. At query time, the top 5 most relevant chunks are retrieved and passed as context to a local **Llama 3.2** model served via Ollama, ensuring answers stay grounded in the source documents rather than model hallucinations. The backend serves a connected frontend GUI.

---

## Tech Stack

| Component | Library / Model |
|---|---|
| Web Framework | FastAPI |
| LLM | Ollama (`llama3.2`) |
| Embeddings | HuggingFace `all-MiniLM-L6-v2` |
| Vector Store | Chroma (persisted at `./chroma_db`) |
| Document Loader | LangChain `PyPDFLoader` |
| Text Splitting | `RecursiveCharacterTextSplitter` — chunk size: 1000, overlap: 200 |
| Agent Framework | LangChain `initialize_agent` (`ZERO_SHOT_REACT_DESCRIPTION`) |
| Data Validation | Pydantic `BaseModel` |

---

## Prerequisites

- Python 3.10+
- Ollama installed and running locally with the `llama3.2` model pulled:

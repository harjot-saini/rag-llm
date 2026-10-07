# rag-llm

A Retrieval-Augmented Generation (RAG) system that answers questions over your own documents by combining semantic search with a Large Language Model (LLM).

Instead of relying only on what the LLM learned during training, this project retrieves relevant passages from your documents and passes them to the model as context. This produces answers that are grounded in your data and reduces hallucinations.

## Table of Contents

- [How It Works](#how-it-works)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
- [Usage](#usage)
- [Configuration](#configuration)
- [License](#license)

## How It Works

```
 Documents ──► Chunking ──► Embeddings ──► Vector Store
                                               │
 User Question ──► Embed Query ──► Similarity Search
                                               │
                                     Top-k Relevant Chunks
                                               │
                        Prompt (Question + Context) ──► LLM ──► Answer
```

1. **Ingest**: Load documents (PDF, TXT, Excel, etc.) and split them into chunks.
2. **Embed**: Convert each chunk into a vector using an embedding model.
3. **Index**: Store the vectors in a vector database.
4. **Retrieve**: Embed the user's question and find the most similar chunks.
5. **Generate**: Send the question and retrieved context to the LLM to produce a grounded answer.

## Features

- Document ingestion and chunking
- Semantic search using vector embeddings
- Context-aware answer generation with an LLM
- Configurable chunk size, overlap, and top-k retrieval
- Easily swappable embedding models, vector stores, and LLMs

## Tech Stack

> Update this section to match your implementation.

| Component       | Technology                            |
| --------------- | ------------------------------------- |
| Language        | Python 3.10+                          |
| Orchestration   | LangChain                             |
| Embeddings      | Sentence-Transformers                 |
| Vector Store    | FAISS                                 |
| LLM             | GROQ                                  |
| Interface       | CLI                                   |

## Project Structure

> Adjust to match your actual layout.

```
rag-llm/
├── data/               # Source documents
├── notebook/           # worksheet for testing code
├── src/
│   ├── __init__.py     
│   ├── data_loader.py  # Load documents
│   ├── embedding.py    # Chunk and embed documents
│   ├── search.py       # Search logic
│   |── vector_store.py # Manages document embeddings
├── app.py              # Entry point
├── .env.example        # Environment variable template
├── requirements.txt
└── README.md
```

## Getting Started

### Prerequisites

- Python 3.10 or higher
- An API key for your chosen LLM provider (or a local model via Ollama)

### Installation

```bash
# Clone the repository
git clone https://github.com/harjot-saini/rag-llm.git
cd rag-llm

# Create and activate a virtual environment
python -m venv venv
source venv/bin/activate        # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
```

### Environment Setup

Copy the example environment file and add your keys:

```bash
cp sample.env .env
```

```env
GROQ_API_KEY=your_api_key_here
```

## Usage

**1. Add your documents** to the `data/` folder.

**2. Ask questions:**

```bash
python src/app.py
```

Example:

```
Q: What are the key points in the uploaded report?
A: Based on the provided documents, the key points are ...
```

## Configuration

| Parameter       | Description                              | Default |
| --------------- | ---------------------------------------- | ------- |
| `CHUNK_SIZE`    | Characters/tokens per chunk              | 1000    |
| `CHUNK_OVERLAP` | Overlap between consecutive chunks       | 200     |
| `TOP_K`         | Number of chunks retrieved per query     | 4       |
| `TEMPERATURE`   | LLM sampling temperature                 | 0.0     |


## License

This project is licensed under the MIT License. See the `LICENSE` file for details.

## Author

**Harjot Saini** · [GitHub](https://github.com/harjot-saini)

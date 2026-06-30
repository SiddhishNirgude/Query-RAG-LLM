# Query-RAG-LLM

Query-RAG-LLM is a Streamlit-powered application that combines Retrieval-Augmented Generation (RAG) with Large Language Models (LLMs) to answer questions using context retrieved from a curated knowledge base. Users can chat with the bot about tech leaders' opinions on AI, drawn from podcast transcripts, and explore an interactive walkthrough of how RAG works under the hood.

🔗 Live app: https://siddhishnirgude-query-rag-llm.streamlit.app/

## Features

- **Tech Leader Chatbot**: Ask questions about how figures like Satya Nadella, Sam Altman, Jensen Huang, and Mark Zuckerberg view AI, agents, and the future of tech. Answers are generated from real podcast transcripts, with sourced YouTube links included in every response.
- **How RAG Works (Interactive Demo)**: A guided, no-API-cost walkthrough showing each stage of the RAG pipeline (Retrieve, Augment, Generate) using a frozen example query and response.
- **Document-Based Retrieval**: A second knowledge base built from "Famous Five" book chapters demonstrates that the underlying retrieval pipeline generalizes beyond tech podcasts to other document types.
- **Top-K Semantic Search**: Uses cosine similarity over OpenAI embeddings to retrieve the top 3 most relevant chunks for any given query.
- **Source Attribution**: Every chatbot response includes the originating YouTube video title, channel, and link.

## How It Works

1. **Preparing the Data** — Source material (podcast transcripts, book chapters) is split into manageable text chunks.
2. **Generating Embeddings** — Each chunk is converted into a vector embedding using OpenAI's `text-embedding-3-large` model and stored alongside its metadata (speaker, video source, timestamp, etc.).
3. **Querying** — When a user submits a question, it's embedded the same way, and cosine similarity is used to retrieve the top 3 most relevant chunks from the stored vectors.
4. **Augmenting the Prompt** — The retrieved chunks, along with their source metadata, are combined with the user's original question into a single, context-rich prompt.
5. **Generating a Response** — The augmented prompt is sent to OpenAI's `gpt-3.5-turbo`, which produces a structured, source-cited answer.

## Tech Stack

- **Frontend**: Streamlit
- **LLM & Embeddings**: OpenAI API (`gpt-3.5-turbo`, `text-embedding-3-large`)
- **Retrieval**: Cosine similarity (scikit-learn) over precomputed embeddings stored in JSON
- **Text Processing**: LangChain text splitters for chunking source documents

## Project Structure

```
├── streamlit_app.py          # Main app: navigation, chatbot UI, RAG demo
├── build/
│   └── custom_functions.py   # Embedding generation, retrieval logic, text splitting
├── documents/                 # Source markdown files (Famous Five book chapters)
├── tech_*.json                 # Precomputed embeddings for tech leader podcast transcripts
├── famous_five_*.json          # Precomputed embeddings for book content
├── sqlite/                     # Vector data stored in SQLite/JSON form
└── requirements.txt
```

## Roadmap

- Integrate Graph RAG to better capture relationships between concepts and improve multi-hop reasoning.
- Allow users to upload their own documents or paste YouTube links for custom, on-the-fly RAG queries.
- Move toward an AI agent architecture that can process diverse inputs and provide more tailored, context-driven insights.

---

Created by Siddhish Nirgude 🚀

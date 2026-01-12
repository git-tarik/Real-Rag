# ⚡ NexusRAG: High-Performance Open Source RAG Pipeline

![Python](https://img.shields.io/badge/Python-3.11+-3776AB?style=for-the-badge&logo=python&logoColor=white)
![LlamaIndex](https://img.shields.io/badge/LlamaIndex-Orchestration-8A2BE2?style=for-the-badge)
![DeepSeek](https://img.shields.io/badge/DeepSeek-V3-4B0082?style=for-the-badge)
![Qdrant](https://img.shields.io/badge/Qdrant-Vector_DB-D91846?style=for-the-badge)
![Docker](https://img.shields.io/badge/Docker-Containerized-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)

## 📖 Overview

**NexusRAG** is a state-of-the-art **Retrieval-Augmented Generation (RAG)** pipeline designed to solve the common pitfalls of naive RAG systems (hallucinations, low recall, and poor context handling). 

Built entirely with **latest open-source components** (2025/2026 standards), this project prioritizes modularity, privacy, and performance. It implements **Advanced RAG** patterns including Hybrid Search (Sparse + Dense), Cross-Encoder Reranking, and Semantic Chunking to deliver enterprise-grade Q&A capabilities on local hardware.

## ✨ Key Features

* **🧠 SOTA Open Source LLM:** Powered by **DeepSeek-V3**, offering top-tier reasoning capabilities comparable to proprietary models, hosted locally via Ollama.
* **🔍 Hybrid Search Engine:** Combines **Dense Vector Search** (semantic meaning) with **Sparse BM25** (keyword matching) using **Qdrant** for maximum retrieval accuracy.
* **⚖️ Cross-Encoder Reranking:** Utilizes the `BAAI/bge-reranker-v2-m3` model to re-evaluate and filter retrieved contexts, ensuring the LLM only sees the most relevant data.
* **🌐 Universal Embeddings:** Implements `BAAI/bge-m3` for state-of-the-art multi-lingual and multi-granularity embeddings.
* **💬 Modern UI:** Features a clean, chat-interface frontend built with **Chainlit**.
* **🐳 Dockerized:** Fully containerized environment for consistent deployment across any machine.

## 🛠️ Tech Stack

| Component | Technology | Description |
| :--- | :--- | :--- |
| **Orchestrator** | [LlamaIndex](https://www.llamaindex.ai/) | The data framework for LLM applications. |
| **LLM** | [DeepSeek-V3](https://github.com/deepseek-ai/DeepSeek-V3) | Running via [Ollama](https://ollama.com/) for local inference. |
| **Vector DB** | [Qdrant](https://qdrant.tech/) | High-performance vector search engine with Hybrid support. |
| **Embeddings** | [BAAI/bge-m3](https://huggingface.co/BAAI/bge-m3) | One-stop model for dense, sparse, and colbert embeddings. |
| **Reranker** | [bge-reranker-v2-m3](https://huggingface.co/BAAI/bge-reranker-v2-m3) | Cross-encoder for precise context scoring. |
| **Frontend** | [Chainlit](https://docs.chainlit.io/get-started/overview) | Production-ready Conversational AI UI. |

## 🏗️ Architecture

```mermaid
graph TD
    A[User Query] --> B(Hybrid Retrieval)
    B --> C{Qdrant Vector DB}
    C -->|Dense Vectors| D[Semantic Results]
    C -->|Sparse BM25| E[Keyword Results]
    D & E --> F[Reciprocal Rank Fusion]
    F --> G[Cross-Encoder Reranker]
    G --> H[Top-K Context]
    H --> I[DeepSeek-V3 LLM]
    I --> J[Final Answer]

# ⚡ Ultimate RAG Pipeline (2026 Open Source Edition)

![Status](https://img.shields.io/badge/Status-Active_Development-brightgreen?style=for-the-badge)
![Python](https://img.shields.io/badge/Python-3.11+-3776AB?style=for-the-badge&logo=python&logoColor=white)
![DeepSeek](https://img.shields.io/badge/LLM-DeepSeek_V3-4B0082?style=for-the-badge)
![LlamaIndex](https://img.shields.io/badge/Orchestrator-LlamaIndex-8A2BE2?style=for-the-badge)
![Qdrant](https://img.shields.io/badge/Vector_DB-Qdrant-D91846?style=for-the-badge)
![Docker](https://img.shields.io/badge/Deployment-Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)

## 🎯 Project Goal

The goal of this project is to architect and implement the **"Ultimate" Retrieval-Augmented Generation (RAG) Pipeline** using *only* the latest and most capable open-source components available as of 2026. 

Unlike standard RAG tutorials, this project focuses on **State-of-the-Art (SOTA) performance**, tackling complex challenges like:
* **Hybrid Search** (Dense + Sparse retrieval)
* **Re-ranking** for high precision
* **Agentic Routing** (Reasoning before searching)
* **Local Privacy** (Running entirely offline/self-hosted)

We are building this **step-by-step** to demonstrate how modern AI components fit together to create a production-grade system.

## 🏗️ The "Best-in-Class" Tech Stack

We have hand-picked these components based on benchmarks and community consensus for "Best Open Source" performance.

| Component | Selected Tech | Why this component? |
| :--- | :--- | :--- |
| **Large Language Model** | **DeepSeek-V3** | Currently the undisputed king of open-source coding and reasoning models, rivaling GPT-4 and Claude 3.5. |
| **Orchestration Framework** | **LlamaIndex** | Chosen over LangChain for its superior data connectors, indexing strategies, and native support for advanced RAG patterns. |
| **Vector Database** | **Qdrant** | A high-performance, Rust-based vector engine that natively supports **Hybrid Search** (Vector + Keyword) without complex overhead. |
| **Embedding Model** | **BAAI/bge-m3** | The most versatile open-source embedding model. It generates dense, sparse, and multi-vector embeddings in a single pass. |
| **Reranker** | **BGE-Reranker-V2** | A Cross-Encoder model that scores the relevance of retrieved documents. Essential for filtering out "noise" before it reaches the LLM. |
| **Inference Engine** | **vLLM / Ollama** | For serving the DeepSeek model with high throughput and low latency on local GPUs. |
| **User Interface** | **Chainlit** | A "ChatGPT-style" UI built specifically for Python RAG apps, allowing for rapid iteration. |

## 🗺️ Implementation Roadmap (Step-by-Step)

We are building this pipeline in distinct phases.

### Phase 1: The Foundation (Ingestion & Indexing)
- [ ] Set up **Qdrant** in Docker.
- [ ] Implement **Semantic Chunking** (splitting text by meaning, not just character count).
- [ ] Generate **Dense Embeddings** using `bge-m3`.
- [ ] Generate **Sparse Embeddings (BM25)** for keyword matching.
- [ ] Store both in Qdrant collections.

### Phase 2: The Retrieval Engine
- [ ] Implement **Hybrid Search**: Querying both Dense and Sparse vectors simultaneously.
- [ ] Apply **Reciprocal Rank Fusion (RRF)** to intelligently merge results from both search methods.
- [ ] **Goal:** Ensure we never miss a relevant document, whether the query is conceptual or keyword-specific.

### Phase 3: Precision Tuning (Reranking)
- [ ] Integrate the **Cross-Encoder Reranker**.
- [ ] Pipeline: Retrieve top 25 docs -> Rerank -> Keep top 5.
- [ ] **Goal:** Drastically reduce hallucinations by feeding the LLM only high-quality context.

### Phase 4: Generation & Chat
- [ ] Connect **DeepSeek-V3** (via Ollama) to the pipeline.
- [ ] Design the prompt template to strictly ground answers in the retrieved context.
- [ ] Build the **Chainlit UI** for streaming responses and citing sources.

### Phase 5: Advanced Features (Agentic RAG)
- [ ] Add a **Query Router**: The system decides if it needs to search the DB, search the web, or just answer from memory.
- [ ] Implement **Query Transformation**: Rewriting complex user questions into better search queries automatically.

## 📐 Architecture Diagram

```mermaid
graph TD
    User[User Query] --> Router{Query Router}
    
    subgraph "Retrieval Pipeline"
    Router -->|Needs Context| Hybrid[Hybrid Search]
    Hybrid -->|Semantic| Dense[Dense Vector Search]
    Hybrid -->|Keywords| Sparse[Sparse BM25 Search]
    Dense & Sparse --> Fusion[Rank Fusion (RRF)]
    Fusion --> Rerank[Cross-Encoder Reranker]
    end
    
    subgraph "Generation"
    Rerank --> Context[Top 5 Chunks]
    Context --> LLM[DeepSeek-V3]
    Router -->|Chit-Chat| LLM
    end
    
    LLM --> Response[Final Answer]

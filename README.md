# 🧩 Modular RAG (Working Title)

> A composable, production-oriented Retrieval-Augmented Generation (RAG) stack built from **best-in-class open-source components**.

This repository is **not a framework**.  
It is a **modular system** that lets you assemble RAG pipelines using independently excellent components from the open-source ecosystem.

---

## Why this exists

Most RAG solutions today are **monolithic**:
- one repo
- one opinion
- one way to chunk, retrieve, rerank, and prompt

In practice, this doesn’t match reality.

Different problems need:
- different chunking strategies  
- different retrieval methods  
- different latency / cost tradeoffs  

And the open-source community already builds **amazing single-purpose components**.

This repo exists to:
- define **clean interfaces**
- provide **glue code**
- enable **swap-ability**
- encourage **benchmark-driven choices**

---

## Design principles

### 1. Modular by default
Each RAG stage is an independent module that can be replaced without touching the rest of the pipeline.

```

Ingestion → Chunking → Embedding → Storage → Retrieval → Reranking → Generation

```

No module assumes implementation details of another.

---

### 2. Interfaces over implementations
This repo defines **contracts**, not winners.

If a component follows the interface, it can plug in.

---

### 3. Production-first
Every abstraction here is designed with:
- observability
- latency awareness
- failure handling
- cost visibility  

in mind.

---

### 4. Opinionated structure, neutral components
We are opinionated about:
- directory layout
- interfaces
- lifecycle

We are neutral about:
- which open-source project is “best”

That evolves over time.

---

## Repository structure (high level)

```

modular-rag/
│
├── core/                 # Interfaces, base types, shared utilities
│
├── components/           # Adapters to external open-source components
│   ├── chunking/
│   ├── embeddings/
│   ├── storage/
│   ├── retrieval/
│   ├── reranking/
│   └── generation/
│
├── pipelines/            # Reference RAG pipelines (minimal, composable)
│
├── benchmarks/           # Evaluation & comparison harnesses
│
├── examples/             # End-to-end runnable examples
│
├── docs/                 # Deep dives, design notes, decisions
│
└── CONTRIBUTING.md

```

---

## Core concepts

### Components
A **component** does one thing well.

Examples:
- chunk a document
- embed text
- retrieve candidates
- rerank results

Each component:
- implements a well-defined interface
- declares its assumptions
- exposes metrics

---

### Pipelines
A **pipeline** wires components together.

Pipelines are:
- explicit
- readable
- debuggable

No hidden magic.

---

### Benchmarks
Benchmarks exist to answer questions like:
- “Is this chunker better for this data?”
- “Does reranking help enough to justify latency?”
- “What breaks at scale?”

Benchmarks drive defaults, not opinions.

---

## What this repo is NOT

- ❌ Not a low-code abstraction
- ❌ Not a wrapper around a single vendor
- ❌ Not another all-in-one RAG framework
- ❌ Not optimized for demos only

---

## Who this is for

- Engineers building **production RAG systems**
- Researchers experimenting with **retrieval strategies**
- Teams who want **control without reinvention**
- Contributors who enjoy improving one thing deeply

---

## Current status

🚧 **Early & evolving**

- Interfaces are stabilizing
- Components are being evaluated and integrated incrementally
- README will evolve as understanding improves

Expect breaking changes early on.

---

## How to contribute

You can contribute by:
- exploring and integrating a component
- improving interfaces
- adding benchmarks
- documenting tradeoffs
- sharing real-world lessons

See `CONTRIBUTING.md`.

---

## Philosophy

> Let specialists build the best tools.  
> Let systems engineers assemble them cleanly.
```

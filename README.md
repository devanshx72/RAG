# RAG

A collection of Retrieval-Augmented Generation systems, each built as a self-contained implementation exploring a different retrieval architecture — from simple pipelines to agentic, structure-aware, and self-correcting approaches.

Every variant lives in its own folder with its own code, dependencies, and README. Nothing is shared across folders by design — each implementation should be runnable on its own without pulling in the others.

---

## Structure

```
RAG/
├── <implementation-name>/
│   ├── README.md          # what this variant does, how it's different, how to run it
│   ├── backend/  (or src/, app/, etc. — whatever fits the implementation)
│   └── ...
├── <implementation-name>/
│   └── ...
└── README.md               # this file
```

Each folder's own README covers:
- The retrieval strategy it uses and why
- Architecture / pipeline diagram
- Tech stack
- Setup and run instructions
- Design tradeoffs specific to that approach

This top-level README stays high-level — it's the index, not the documentation.

---

## Why this repo

RAG isn't one technique — it's a design space. Chunking vs. no chunking, vector search vs. structural retrieval, single-pass vs. agentic multi-step retrieval, verification vs. none — each choice trades off latency, cost, accuracy, and infrastructure complexity differently.

This repo is a working comparison: each folder is a real, runnable implementation of one point in that design space, not a toy example.

---

## Implementations

| Folder | Approach | Status |
|---|---|---|
| _(added as built)_ | | |

See each folder's own README for details on that implementation.

---

## Getting Started

Each implementation is independent. To run one:

```bash
cd <implementation-name>
# follow that folder's README for setup
```

There's no shared root-level dependency install — check the specific variant's README for its stack and requirements.

---

## Tech

Mentioned in each folder's README.md

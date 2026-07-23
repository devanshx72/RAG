# RAG Architecture Comparison & Benchmark Workspace

A curated collection of production-grade **Retrieval-Augmented Generation (RAG)** systems. Each implementation explores a fundamentally different point in the RAG design space — ranging from vectorless, structure-aware document reasoning to self-correcting, evaluator-guided search graph workflows.

Every variant lives in its own dedicated, self-contained directory with its own code, frontend/backend architecture, dependencies, and detailed documentation.

---

## 📂 Implementations Overview

| Folder | Name & Paradigm | Key Highlights & Technologies | Status |
| :--- | :--- | :--- | :---: |
| [**`corrective-rag`**] | **Corrective RAG (CRAG)** | • Retrieval Evaluator ($0.7 / 0.3$ thresholds)<br>• Sentence-level Knowledge Refinement (*Decompose-Filter-Recompose*)<br>• Structured LLM Query Rewriter<br>• Tavily Web Search API Fallback<br>• **Stack**: LangGraph, LangChain, Mistral AI, FAISS, Tavily | `Production-Ready` |
| [**`vectorless-agentic-rag`**] | **PageMind (Vectorless Agentic RAG)** | • Embedding-free, tree-based retrieval (*PageIndex*)<br>• Per-page Mistral OCR markdown parsing<br>• Hierarchical section outline router<br>• Second-pass LLM answer verifier with retry loop<br>• **Stack**: FastAPI, React 19, LangGraph, Mistral AI | `Production-Ready` |

---

## 🎯 Architectural Design Space Comparison

Different RAG tasks demand different trade-offs across latency, cost, retrieval accuracy, and structural awareness:

| Feature / Dimension | Corrective RAG (`corrective-rag`) | Vectorless Agentic RAG (`vectorless-agentic-rag`) |
| :--- | :--- | :--- |
| **Indexing Strategy** | Chunk-based Dense Embeddings (FAISS + Mistral Embeddings) | Hierarchical Section Tree (*PageIndex* via Mistral OCR) |
| **Vector Store Required?** | **Yes** (FAISS) | **No** (Vectorless) |
| **State Machine** | LangGraph (Cyclic evaluation & fallback graph) | LangGraph (Intent classification, router, verifier loop) |
| **Context Refinement** | Sentence-level decomposition & LLM filtering (`KeepOrDrop`) | Exact page-range retrieval based on outline tree |
| **Fallback Mechanism** | Automated LLM Query Rewriting + Tavily Web Search | Page range expansion + Verifier retry feedback loop |
| **Verification Pass** | Evaluates document relevance *before* generation | Evaluates answer groundedness & hallucinations *after* generation |
| **Best Used For** | Web-integrated QA, dynamic knowledge bases, open-domain RAG | Long document QA, structured PDFs, textbooks, contracts |

---

## 📁 Repository Structure

```text
RAG/
├── corrective-rag/                  # Self-correcting RAG with web fallback & query rewriting
│   ├── documents/                   # PDF vector store source files
│   ├── retrieval-refinement.ipynb   # Knowledge Refinement module
│   ├── retrieval-evaluator.ipynb    # Retrieval Evaluator & Verdict Routing module
│   ├── web_search_refinement.ipynb  # Basic Web Search Fallback module
│   ├── query_rewrite.ipynb          # End-to-end CRAG with Query Rewriter
│   └── README.md                    # CRAG Documentation
│
├── vectorless-agentic-rag/          # PageMind: Embedding-free Agentic PDF RAG
│   ├── backend/                     # FastAPI & LangGraph graph pipeline
│   ├── frontend/                    # React 19 + Vite UI
│   └── README.md                    # PageMind Documentation
│
└── README.md                        # Master Index & Comparison Workspace (This file)
```

---

## 🚀 Getting Started

Each implementation is designed to be completely independent. To run or explore a specific RAG variant, navigate to its directory and follow its standalone README:

### Running Corrective RAG:
```bash
cd corrective-rag
# Follow corrective-rag/README.md for API setup & notebook execution
```

### Running Vectorless Agentic RAG (PageMind):
```bash
cd vectorless-agentic-rag
# Follow vectorless-agentic-rag/README.md for FastAPI backend & React frontend setup
```

---

## 📜 References & Research

1. **Corrective Retrieval-Augmented Generation (CRAG)**: Yan et al., 2024. [arXiv:2401.15884](https://arxiv.org/abs/2401.15884)
2. **LangGraph**: Stateful, multi-actor orchestration for LLM applications. [LangChain Docs](https://langchain-ai.github.io/langgraph/)
3. **Mistral AI**: Document OCR & Chat Models. [Mistral AI Docs](https://docs.mistral.ai/)

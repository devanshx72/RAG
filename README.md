# RAG Architecture Comparison & Benchmark Workspace

A curated collection of production-grade **Retrieval-Augmented Generation (RAG)** systems. Each implementation explores a fundamentally different point in the RAG design space — ranging from vectorless, structure-aware document reasoning to self-correcting, evaluator-guided search graph workflows and self-reflective feedback loops.

Every variant lives in its own dedicated, self-contained directory with its own code, frontend/backend architecture, dependencies, and detailed documentation.

---

## 📂 Implementations Overview

| Folder | Name & Paradigm | Key Highlights & Technologies | Status |
| :--- | :--- | :--- | :---: |
| [**`corrective-rag`**](file:///Users/devansh/Coding/RAG/corrective-rag/README.md) | **Corrective RAG (CRAG)** | • Retrieval Evaluator ($0.7 / 0.3$ thresholds)<br>• Sentence-level Knowledge Refinement (*Decompose-Filter-Recompose*)<br>• Structured LLM Query Rewriter<br>• Tavily Web Search API Fallback<br>• **Stack**: LangGraph, LangChain, Mistral AI, FAISS, Tavily | `Production-Ready` |
| [**`self-rag`**](file:///Users/devansh/Coding/RAG/self-rag/README.md) | **Self-Reflective RAG (Self-RAG)** | • 4 Reflection Checkpoints (`IS_RETRIEVE`, `IS_REL`, `IS_SUP`, `IS_USE`)<br>• Adaptive retrieval routing<br>• Topic-level document filtering<br>• Strict Quote-Only Revision Loop<br>• **Stack**: LangGraph, LangChain, Mistral AI, OpenAI, FAISS | `Production-Ready` |
| [**`vectorless-agentic-rag`**](file:///Users/devansh/Coding/RAG/vectorless-agentic-rag/README.md) | **PageMind (Vectorless Agentic RAG)** | • Embedding-free, tree-based retrieval (*PageIndex*)<br>• Per-page Mistral OCR markdown parsing<br>• Hierarchical section outline router<br>• Second-pass LLM answer verifier with retry loop<br>• **Stack**: FastAPI, React 19, LangGraph, Mistral AI | `Production-Ready` |

---

## 🎯 Architectural Design Space Comparison

Different RAG tasks demand different trade-offs across latency, cost, retrieval accuracy, and structural awareness:

| Feature / Dimension | Corrective RAG (`corrective-rag`) | Self-Reflective RAG (`self-rag`) | Vectorless Agentic RAG (`vectorless-agentic-rag`) |
| :--- | :--- | :--- | :--- |
| **Indexing Strategy** | Chunk-based Dense Embeddings (FAISS + Mistral Embeddings) | Chunk-based Dense Embeddings (FAISS + OpenAI/Mistral Embeddings) | Hierarchical Section Tree (*PageIndex* via Mistral OCR) |
| **Vector Store Required?** | **Yes** (FAISS) | **Yes** (FAISS) | **No** (Vectorless) |
| **State Machine** | LangGraph (Evaluation & web fallback graph) | LangGraph (Multi-critique self-reflection graph) | LangGraph (Intent classification, router, verifier loop) |
| **Adaptive Retrieval?** | No (Retrieves first, then evaluates) | **Yes** (`IS_RETRIEVE` node decides if retrieval is needed) | **Yes** (Classifies intent before tree lookup) |
| **Context Refinement** | Sentence-level decomposition & LLM filtering (`KeepOrDrop`) | Topic-level document filtering (`IS_REL`) | Exact page-range retrieval based on outline tree |
| **Groundedness & Revision** | Pre-generation retrieval score thresholds | **Post-generation `IS_SUP` critique + Quote-Only Revision Loop** | Post-generation verifier + page range expansion retry |
| **Usefulness Verification** | N/A | **Yes** (`IS_USE` node checks if query intent is met) | Verified during answer generation feedback loop |
| **Fallback Mechanism** | Automated LLM Query Rewriting + Tavily Web Search | Direct LLM generation / No Answer Found fallback | Page range expansion + Verifier retry feedback loop |
| **Best Used For** | Web-integrated QA, dynamic knowledge bases, open-domain RAG | High-precision factual QA, strict hallucination avoidance | Long document QA, structured PDFs, textbooks, contracts |

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
├── self-rag/                        # Self-Reflective RAG with critique tokens & revision loops
│   ├── documents/                   # Enterprise PDF knowledge base
│   ├── self-rag-step1.ipynb         # Step 1: Adaptive Retrieval (IS_RETRIEVE)
│   ├── self-rag-step2.ipynb         # Step 2: Relevance Filtering (IS_REL)
│   ├── self-rag-step3.ipynb         # Step 3: Contextual Generation & Fallback
│   ├── self-rag-step4.ipynb         # Step 4: Groundedness Critique (IS_SUP) & Revision
│   ├── self-rag-step5.ipynb         # Step 5: Full Self-RAG Pipeline (IS_USE)
│   └── README.md                    # Self-RAG Documentation
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

### Running Self-Reflective RAG:
```bash
cd self-rag
# Follow self-rag/README.md for API setup & notebook execution
```

### Running Vectorless Agentic RAG (PageMind):
```bash
cd vectorless-agentic-rag
# Follow vectorless-agentic-rag/README.md for FastAPI backend & React frontend setup
```

---

## 📜 References & Research

1. **Corrective Retrieval-Augmented Generation (CRAG)**: Yan et al., 2024. [arXiv:2401.15884](https://arxiv.org/abs/2401.15884)
2. **Self-RAG: Learning to Retrieve, Generate, and Critique through Self-Reflection**: Asai et al., 2023. [arXiv:2310.11511](https://arxiv.org/abs/2310.11511)
3. **LangGraph**: Stateful, multi-actor orchestration for LLM applications. [LangChain Docs](https://langchain-ai.github.io/langgraph/)
4. **Mistral AI**: Document OCR & Chat Models. [Mistral AI Docs](https://docs.mistral.ai/)

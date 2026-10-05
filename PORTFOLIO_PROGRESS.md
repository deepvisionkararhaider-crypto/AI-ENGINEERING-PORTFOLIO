# AI Engineering Portfolio — Progress Tracker

A 50-project AI/ML/LLM/RAG/Agent/MLOps engineering portfolio. Each project is a
self-contained repository: real implementation, deterministic tests, and a
professional README. **Source-code focused — no deployment, no live demo links.**

Legend: `COMPLETE` = built, tested, pushed · `IN PROGRESS` = being built ·
`PENDING` = not started · `PRE-EXISTING` = already in the account before this series

---

## Status table

| #  | Project | Repo | Status | Tests | Notes |
|----|---------|------|--------|-------|-------|
| 01 | Vanilla RAG | [`01-vanilla-rag`](https://github.com/deepvisionkararhaider-crypto/01-vanilla-rag) | PRE-EXISTING | PASS | FastAPI, from-scratch pipeline |
| 02 | LangChain RAG | — | PRE-EXISTING* | — | No repo — see note |
| 03 | LlamaIndex RAG | — | PRE-EXISTING* | — | No repo — see note |
| 04 | Advanced RAG | — | PRE-EXISTING* | — | No repo — see note |
| 05 | HyDE RAG | — | PRE-EXISTING* | — | No repo — see note |
| 06 | Multi-Query RAG | [`06-multi-query-rag`](https://github.com/deepvisionkararhaider-crypto/06-multi-query-rag) | COMPLETE | PASS (39) | Query expansion + RRF fusion + dedup |
| 07 | Parent-Document RAG | [`07-parent-document-rag`](https://github.com/deepvisionkararhaider-crypto/07-parent-document-rag) | COMPLETE | PASS (21) | Two-level parent/child index |
| 08 | Hybrid RAG | [`08-hybrid-rag`](https://github.com/deepvisionkararhaider-crypto/08-hybrid-rag) | COMPLETE | PASS (22) | BM25 + dense → RRF |
| 09 | Reranker RAG | [`09-reranker-rag`](https://github.com/deepvisionkararhaider-crypto/09-reranker-rag) | COMPLETE | PASS (19) | Bi-encoder recall → cross-encoder rerank |
| 10 | Contextual RAG | | PENDING | | |
| 11 | Corrective RAG | | PENDING | | |
| 12 | Self-RAG | | PENDING | | |
| 13 | Graph RAG | | PENDING | | |
| 14 | Agentic RAG | | PENDING | | |
| 15 | Adaptive RAG | | PENDING | | |
| 16 | Multimodal RAG | | PENDING | | |
| 17 | Table RAG | | PENDING | | |
| 18 | Code RAG | | PENDING | | |
| 19 | SQL RAG | | PENDING | | |
| 20 | Enterprise RAG | | PENDING | | |
| 21 | LLM API Platform | | PENDING | | |
| 22 | Hugging Face LLM Platform | | PENDING | | |
| 23 | Local LLM Platform | | PENDING | | |
| 24 | LLM Fine-Tuning (LoRA) | | PENDING | | |
| 25 | LLM QLoRA | | PENDING | | |
| 26 | LLM Evaluation Platform | | PENDING | | |
| 27 | LangGraph Agent | | PENDING | | |
| 28 | Research Agent | | PENDING | | |
| 29 | SQL Agent | | PENDING | | |
| 30 | Customer Support Agent | | PENDING | | |
| 31 | Multi-Agent System | | PENDING | | |
| 32 | Coding Agent | | PENDING | | |
| 33 | Document Agent | | PENDING | | |
| 34 | Personal AI Assistant | | PENDING | | |
| 35 | Multimodal LLM App | | PENDING | | |
| 36 | Vision RAG | | PENDING | | |
| 37 | Document Vision System | [`document-vision-system`](https://github.com/deepvisionkararhaider-crypto/document-vision-system) | PRE-EXISTING | — | Existing repo |
| 38 | Production Tabular ML | | PENDING | | |
| 39 | Time-Series Forecasting | | PENDING | | |
| 40 | Recommendation System | | PENDING | | |
| 41 | MLOps Platform | | PENDING | | |
| 42 | LLMOps Platform | | PENDING | | |
| 43 | AI Observability Platform | | PENDING | | |
| 44 | AI API Gateway | | PENDING | | |
| 45 | Production RAG Platform | [`production-rag-platform`](https://github.com/deepvisionkararhaider-crypto/production-rag-platform) | PRE-EXISTING | — | Existing repo |
| 46 | Enterprise Knowledge Platform | | PENDING | | |
| 47 | AI Research Platform | | PENDING | | |
| 48 | Autonomous Data Analyst | | PENDING | | |
| 49 | Full-Stack AI Agent Platform | | PENDING | | |
| 50 | Production AI Platform | | PENDING | | |

\* PRE-EXISTING* = the brief lists this project as already complete, but **no matching
repository exists** under that (or the `NN-` prefixed) name in the GitHub account —
verified via the GitHub API on 2026-10-05 (`langchain-rag`, `llamaindex-rag`,
`advanced-rag`, `hyde-rag` all return HTTP 404). Per the instruction to start from
Project 06 and not duplicate completed work, no alternative repo was created.

---

## Account audit (2026-10-05)

Repositories found on `deepvisionkararhaider-crypto` at the start of this series:

- `AI-ENGINEERING-PORTFOLIO` — master tracker (README)
- `01-vanilla-rag` — FastAPI/Python production-quality RAG (**template for this series**)
- `vanilla-rag`, `hybrid-rag`, `reranker-rag`, `document-vision-system`,
  `production-rag-platform` — pre-existing Cloudflare Workers / JS implementations
- `deep-learning-models`, `nlp-models`, `machine-learning-models`

> **Naming note:** the account already contained Cloudflare/JS repos named
> `hybrid-rag` and `reranker-rag` from an earlier effort. Projects **08-hybrid-rag**
> and **09-reranker-rag** in this series are **new, separate** repositories (Python /
> FastAPI, following the `01-vanilla-rag` architecture) and do **not** modify or
> duplicate those pre-existing JS repos.

---

## Standard architecture for this series

Every project follows the `06-multi-query-rag` structure (derived from the proven
`01-vanilla-rag`):

```
<nn>-<project>/
├── app/            api · core · ingestion · retrieval · llm · models · <feature>
├── frontend/       zero-build HTML + vanilla JS UI
├── data/           runtime persistence (git-ignored)
├── tests/          deterministic, offline test suite
├── scripts/        seed / utility scripts
├── Dockerfile · docker-compose.yml
├── requirements.txt · requirements-ml.txt · requirements-dev.txt
├── pyproject.toml · .env.example · .gitignore
└── README.md · ARCHITECTURE.md
```

**Offline-first principle:** every project runs and tests with **no API key and no
network** using deterministic fallbacks (hashing embedder, numpy vector store,
extractive generator, rule-based/lexical components). Real transformer embeddings,
FAISS and LLM providers activate automatically via environment variables.

Shared, reusable modules live in `/home/user/portfolio/_base/` and are copied into
each project by `/home/user/portfolio/_tools/newproj.sh` (chunking, loaders,
embeddings, vector store, retriever, RRF, LLM provider, Docker/git/CI scaffolding).

---

## Progression

- **RAG (06–20):** multi-query ✅ → parent-document ✅ → hybrid ✅ → reranker ✅ →
  contextual → corrective → self → graph → agentic → adaptive → multimodal → table →
  code → sql → enterprise
- **LLM platforms (21–26):** API platform → HF platform → local LLM → LoRA → QLoRA →
  evaluation
- **Agents (27–34):** LangGraph → research → sql → support → multi-agent → coding →
  document → personal assistant
- **Multimodal (35–37):** multimodal app → vision RAG → document vision
- **ML/MLOps (38–44):** tabular ML → forecasting → recommender → MLOps → LLMOps →
  observability → API gateway
- **Platforms (45–50):** production RAG → enterprise knowledge → research → data
  analyst → full-stack agent platform → production AI platform

---

## Session scope note

This session built and pushed **Projects 06, 07, 08, 09** (all with passing
deterministic test suites). Projects **10–50 remain PENDING** and were not started —
a 45-project build cannot be completed within a single session budget. The shared
scaffold (`_base/` + `_tools/newproj.sh`) is in place so subsequent projects are
fast, consistent, and independent.

# AI Engineering Portfolio — Live RAG Projects

Five production-style **Retrieval-Augmented Generation** projects, each built, tested, deployed and verified on **Cloudflare Workers** (Workers AI embeddings + cross-encoder reranker, Groq LLM, Cloudflare D1). Every app has a working web UI and a JSON API.

> All live URLs below were verified returning HTTP 200. Each demo seeds sample documents so it works immediately — just open the link and ask a question.

| # | Project | Live Demo (open for students) | API | GitHub |
|---|---------|-------------------------------|-----|--------|
| 01 | **Vanilla RAG** — ingestion → chunking → embeddings → vector search → LLM + citations | https://vanilla-rag.deepvision-aiportfolio.workers.dev | `POST /api/query` | https://github.com/deepvisionkararhaider-crypto/vanilla-rag |
| 02 | **Hybrid RAG** — BM25 + dense vectors + Reciprocal Rank Fusion | https://hybrid-rag.deepvision-aiportfolio.workers.dev | `POST /api/search` | https://github.com/deepvisionkararhaider-crypto/hybrid-rag |
| 03 | **Reranker RAG** — bi-encoder recall → cross-encoder rerank | https://reranker-rag.deepvision-aiportfolio.workers.dev | `POST /api/search` | https://github.com/deepvisionkararhaider-crypto/reranker-rag |
| 04 | **Document Vision System** — invoices/receipts/forms → validated JSON | https://document-vision-system.deepvision-aiportfolio.workers.dev | `POST /api/extract` | https://github.com/deepvisionkararhaider-crypto/document-vision-system |
| 05 | **Production RAG Platform** — full pipeline + observability (capstone) | https://production-rag-platform.deepvision-aiportfolio.workers.dev | `GET /api/analytics` | https://github.com/deepvisionkararhaider-crypto/production-rag-platform |

## What each project teaches

1. **Vanilla RAG** — the whole RAG pipeline from scratch: sentence-aware chunking, 384-d embeddings, cosine similarity search over a D1 vector store, grounded generation with `[Source N]` citations.
2. **Hybrid RAG** — why lexical (BM25) and semantic (dense) retrieval are complementary, and how **Reciprocal Rank Fusion** (k=60) merges their rankings without score normalization.
3. **Reranker RAG** — the difference between a **bi-encoder** and a **cross-encoder**, and why reranking a short candidate list improves precision at low cost. Exposes `rank_before` vs `rank_after`.
4. **Document Vision System** — LLM structured extraction with **strict per-type JSON schemas** and validation (line-item sums, numeric types), persisted history, JSON export.
5. **Production RAG Platform** — the capstone: hybrid recall + RRF + cross-encoder rerank + LLM in one instrumented pipeline, **multi-tenant collection filtering**, graceful degradation, and **real observability** (per-request stage latencies + `/api/analytics`).

## Stack
Cloudflare Workers · Hono · Cloudflare Workers AI (`bge-small-en-v1.5` embeddings, `bge-reranker-base` cross-encoder) · Cloudflare D1 · Groq LLM (`openai/gpt-oss-120b`) · TailwindCSS

## Verification
- Live health check: **all 5 return `{"status":"healthy"}` (HTTP 200)**
- Smoke tests per project: 01 = 7/7, 02 = 7/7, 03 = 6/6, 04 = 6/6, 05 = 7/7 (verified against the live deployment)
- Real LLM answers verified on every project (Groq), with citations

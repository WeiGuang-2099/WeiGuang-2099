<div align="center">

[![Typing SVG](https://readme-typing-svg.demolab.com?font=Fira+Code&weight=700&size=26&pause=1000&color=58A6FF&center=true&vCenter=true&width=650&lines=Hi%2C+I'm+WeiGuang+(Yuheng+Li);Full-Stack+Dev+%2B+AI+Tinkerer;I+build+things+and+then+measure+them)](https://git.io/typing-svg)

![Status](https://img.shields.io/badge/-Always%20Building-%2300d26a?style=for-the-badge)
![Stack](https://img.shields.io/badge/Stack-Full--Stack%20%2B%20AI-%236366F1?style=for-the-badge)
![Vibe](https://img.shields.io/badge/Vibe-Ship%20it%20%26%20iterate-%23F97316?style=for-the-badge)

Final-year Software Engineering (Honours) @ University of Adelaide · graduating Dec 2026 · Adelaide, AU

[![Email](https://img.shields.io/badge/Email-liyuhengduigong%40gmail.com-EA4335?style=flat-square&logo=gmail&logoColor=white)](mailto:liyuhengduigong@gmail.com)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-yuheng--li-0A66C2?style=flat-square&logo=linkedin&logoColor=white)](https://linkedin.com/in/yuheng-li-1a79b3393)

</div>

---

## whoami

```typescript
const WeiGuang = {
  status:     "Building stuff, measuring it, then fixing what the numbers expose",
  stack:      ["TypeScript", "Python", "Java", "Node.js", "React", "Vue", "FastAPI", "Spring Boot"],
  focusedOn:  ["RAG pipelines", "multi-agent systems", "high-concurrency backends"],
  seeking:    "Graduate / junior AI engineer & software engineer roles in Australia (from Dec 2026)",
  philosophy: "Make it work -> make it right -> make it fast -> prove it with an eval",
};
```

---

## Featured Projects

### [Production-RAG](https://github.com/WeiGuang-2099/Production-RAG) -- Production-Grade RAG System

End-to-end Retrieval-Augmented Generation built like a service you would actually run: hybrid retrieval (Qdrant dense vectors + BM25 fused via Reciprocal Rank Fusion, GraphRAG expansion, Cohere reranking) feeding grounded generation that cites sources as `[n]` and refuses questions the corpus cannot answer. Every design choice is justified by a retrieval ablation harness, not adjectives.

**Highlights:**
- Ablation-verified retrieval: hybrid RRF lifts recall@5 from 0.934 to 0.972 at no latency cost; a 4.6x adversarial corpus scale-up shows the reranker becoming the highest-value component
- Grounded, cited answers with refusal (5/5 correct refusals on unanswerable questions vs 0/5 for a baseline prompt)
- API-edge guardrails (prompt-injection blocking, PII redaction), task-based model routing with fallback, semantic cache, per-query cost accounting
- MCP server (FastMCP) so Claude Desktop can drive search / grounded QA / ingestion directly; React demo UI with streamed, cited answers
- 219 fully mocked pytest tests in CI, one-command Docker Compose deploy

`Python` `FastAPI` `Qdrant` `BM25` `GraphRAG` `Cohere Rerank` `RAGAS` `LangSmith` `MCP` `Docker`

---

### [Smart Code Assistant](https://github.com/WeiGuang-2099/Smart_Code_Assistant) -- AI Code Intelligence Platform

AI code generation, review, and analysis platform that combines LLM-driven code intelligence with a code knowledge graph. An AST parser builds a Neo4j dependency graph (CALLS / IMPORTS / INHERITS / CONTAINS) alongside ChromaDB embeddings; hybrid GraphRAG retrieval fans both out in parallel. A LangChain agent orchestrates four code-analysis tools (structure, smells, complexity, security), streamed to a React 19 frontend over typed SSE events.

**Highlights:**
- 50-question golden-set eval harness (retrieval scored against expected files and graph neighbours, generation scored by an LLM judge); three measured iterations lifted hybrid hit rate@5 from 0.60 to 0.68
- ~300 backend pytest tests (60%+ coverage) + 54+ Vitest tests, CI with lint / type-check / coverage gates, k6 load tests
- OpenTelemetry tracing, Prometheus metrics, JWT + Argon2 auth with token revocation
- MCP server exposing the code graph to Claude Code

`React 19` `TypeScript` `FastAPI` `LangChain` `Neo4j` `ChromaDB` `GraphRAG` `MCP` `Docker`

---

### [High-Concurrency Auction Platform](https://github.com/WeiGuang-2099/High-concurrency-Distributed-Event-Driven-System) -- Distributed Event-Driven Backend

Real-time auction and ticketing platform on a distributed event-driven microservices architecture (Java 17, Spring Boot 3, Spring Cloud): Kafka domain events with idempotent producers and dead-letter topics, RabbitMQ delayed messages for timeouts, MongoDB event sourcing with CQRS projections and replay, and atomic Redis Lua scripts protecting the hot write paths.

**Highlights:**
- k6-proven correctness: 2,000 concurrent reserve attempts on 100 stock sell exactly 100, zero oversell, zero errors (verified by a post-run invariant, not assumed)
- ~3,560 bids/s with zero lost bids on the pure-Redis bid path (p95 71 ms), durability deferred to Kafka -> MySQL
- Redis Lua optimistic path benchmarked at ~1.5x the throughput of `SELECT ... FOR UPDATE` at equal correctness
- Distributed tracing (Micrometer + Zipkin) sharing one trace id with structured ELK logs; 86 unit tests + Testcontainers integration tests

`Java 17` `Spring Boot 3` `Spring Cloud` `Kafka` `RabbitMQ` `Redis` `MongoDB` `MySQL` `k6` `Docker`

---

### [AgentForge](https://github.com/WeiGuang-2099/AgentForge) -- Out-of-the-box Multi-Agent Collaboration Framework

Full-stack platform for quickly deploying AI agent applications. Ships with 6+ pre-built agent templates (assistant, coder, researcher, translator, writer, data analyst) and multi-agent team presets. Supports single-agent chat, multi-agent collaboration, and workflow modes with conditional branching, backed by short-term (session) and long-term (vector DB) memory.

**Highlights:**
- 5-minute setup from clone to running via Docker Compose
- Unified LLM interface through LiteLLM (OpenAI, Claude, Gemini, local models)
- Interactive workflow builder with React Flow visualization

`Next.js` `FastAPI` `Docker` `LiteLLM` `ChromaDB` `PostgreSQL` `Redis`

---

## Open Source

**[internetarchive/openlibrary PR #12748](https://github.com/internetarchive/openlibrary/pull/12748)** -- Performance PR to Internet Archive's Open Library (high-traffic production Python codebase): batched 6 N+1 query hotspots across 4 modules by replacing per-iteration `site.get()` calls with a single `site.get_many()` per request path. Backend-only refactor with no behaviour change, resolving a pre-existing TODO; iterated across 22 commits in maintainer review.

---

<details>
<summary><b>More Projects</b></summary>
<br>

- **[ecoCart](https://github.com/WeiGuang-2099/ecoCart)** -- Privacy-first carbon footprint scanner for Australian shoppers: in-browser barcode decoding (ZXing WASM + YOLOv8n ONNX, no images leave the device), Australian-localized carbon model (ANZ LCA v3.1 + NGA transport factors), ACCC anti-greenwash checks, and an eco-store map. PWA installable, EN/中文 i18n. `React 19` `Vite` `Node.js` `Express` `ONNX Runtime` `Leaflet` `PWA`

- **[RAG-it](https://github.com/WeiGuang-2099/RAG-it)** -- Graph RAG code analysis system. Upload source code, auto-build dependency graphs with NetworkX, and query your codebase architecture (cycle detection, shortest path, impact analysis) via streaming AI chat with semantic code search. `FastAPI` `React` `TypeScript` `NetworkX` `GLM-4` `WebSocket` `SQLite`

- **[graphRAG](https://github.com/WeiGuang-2099/graphRAG)** -- IT operations assistant that builds a Neo4j knowledge graph of microservice dependencies and uses LLM-driven fault tracing for root cause analysis. `Neo4j` `GLM` `Vue 3` `D3.js` `FastAPI`

- **[MovieWhisper](https://github.com/WeiGuang-2099/MovieWhisper)** -- Explainable movie recommendation engine combining collaborative + content-based filtering at 50/50 weight, with explicit justifications for every recommendation. `Python` `Streamlit` `scikit-learn` `Plotly`

- **[CRUD-Demo-Project](https://github.com/WeiGuang-2099/CRUD-Demo-Project)** -- Interactive full-stack teaching platform with 11 visual modules covering CRUD, CORS, HTTP lifecycle, WebSocket, transactions, and more. `React` `Node.js` `Express` `WebSocket`

- **[pdf2md](https://github.com/WeiGuang-2099/pdf2md)** -- PDF to Markdown converter. Because PDF is the final boss of document formats. `TypeScript`

</details>

---

## Tech Stack

**Languages**

![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white)
![Java](https://img.shields.io/badge/Java-ED8B00?style=flat-square&logo=openjdk&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat-square&logo=javascript&logoColor=black)

**Frontend**

![React](https://img.shields.io/badge/React-20232A?style=flat-square&logo=react&logoColor=61DAFB)
![Next.js](https://img.shields.io/badge/Next.js-000000?style=flat-square&logo=nextdotjs&logoColor=white)
![Vue](https://img.shields.io/badge/Vue.js-35495E?style=flat-square&logo=vue.js&logoColor=4FC08D)
![TailwindCSS](https://img.shields.io/badge/Tailwind-38B2AC?style=flat-square&logo=tailwind-css&logoColor=white)

**Backend**

![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white)
![Spring Boot](https://img.shields.io/badge/Spring_Boot-6DB33F?style=flat-square&logo=spring-boot&logoColor=white)
![Node.js](https://img.shields.io/badge/Node.js-339933?style=flat-square&logo=node.js&logoColor=white)
![Express](https://img.shields.io/badge/Express-000000?style=flat-square&logo=express&logoColor=white)

**AI / LLM**

![LangChain](https://img.shields.io/badge/LangChain-1C3C3C?style=flat-square&logo=langchain&logoColor=white)
![OpenAI](https://img.shields.io/badge/OpenAI-412991?style=flat-square&logo=openai&logoColor=white)
![Qdrant](https://img.shields.io/badge/Qdrant-DC244C?style=flat-square)
![ChromaDB](https://img.shields.io/badge/Chroma-FFC107?style=flat-square&logo=chroma&logoColor=black)

**Infrastructure & Data**

![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![Kafka](https://img.shields.io/badge/Kafka-231F20?style=flat-square&logo=apachekafka&logoColor=white)
![RabbitMQ](https://img.shields.io/badge/RabbitMQ-FF6600?style=flat-square&logo=rabbitmq&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=flat-square&logo=postgresql&logoColor=white)
![MongoDB](https://img.shields.io/badge/MongoDB-47A248?style=flat-square&logo=mongodb&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-DC382D?style=flat-square&logo=redis&logoColor=white)
![Neo4j](https://img.shields.io/badge/Neo4j-4581C3?style=flat-square&logo=neo4j&logoColor=white)

---

## Stats

<div align="center">

<img height="170em" src="https://github-readme-stats.vercel.app/api?username=WeiGuang-2099&show_icons=true&theme=tokyonight&hide_border=true&count_private=true&include_all_commits=true"/>
<img height="170em" src="https://github-readme-stats.vercel.app/api/top-langs/?username=WeiGuang-2099&layout=compact&theme=tokyonight&hide_border=true&langs_count=6"/>

</div>

<div align="center">

![GitHub Streak](https://streak-stats.demolab.com/?user=WeiGuang-2099&theme=tokyonight&hide_border=true)

</div>

---

## My Contributions, but Make It Snek

<div align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)"  srcset="https://raw.githubusercontent.com/WeiGuang-2099/WeiGuang-2099/output/github-contribution-grid-snake-dark.svg"/>
    <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/WeiGuang-2099/WeiGuang-2099/output/github-contribution-grid-snake.svg"/>
    <img alt="snake" src="https://raw.githubusercontent.com/WeiGuang-2099/WeiGuang-2099/output/github-contribution-grid-snake.svg"/>
  </picture>
</div>

---

<div align="center">

*Currently exploring multi-agent workflows, graph-based RAG, high-concurrency backends, and whatever catches my curiosity next.*

*Open to graduate / junior software & AI engineering roles in Australia -- say hi: liyuhengduigong@gmail.com*

</div>

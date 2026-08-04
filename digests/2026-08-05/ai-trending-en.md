# AI Open Source Trends 2026-08-05

> Sources: GitHub Trending + GitHub Search API | Generated: 2026-08-04 23:06 UTC

---

# AI Open Source Trends Report — 2026-08-05

## 1. Today's Highlights

The AI open-source ecosystem today is dominated by **agent infrastructure** and **coding-agent companion tools**. The biggest star-gainers are skill/plugin frameworks that extend coding agents like Claude Code, Cursor, and Codex — with `superpowers` (+777) and `compound-engineering-plugin` (+33) signaling a growing "methodology as code" movement. Notably, **memory and context management** has emerged as a critical pain point, evidenced by TencentCloud's `TencentDB-Agent-Memory` (+1,138 today) and the sustained traction of `claude-mem` (89K stars). The trending list also spotlights **efficiency and cost reduction** — from `airllm` (+1,716) enabling 70B inference on 4GB GPUs to `reverse-skill` (+2,310) adding security-pentest capabilities to coding agents. A smaller but telling signal: `firecrawl/pdf-inspector` (+2,524) shows that **document intelligence** — PDF classification and extraction — is becoming a foundational building block for AI workflows.

## 2. Top Projects by Category

### 🔧 AI Infrastructure
- [ollama](https://github.com/ollama/ollama) — ⭐177,783 — The de-facto standard for local LLM inference, now supporting Kimi-K2.6, GLM-5.2, DeepSeek, and more.
- [airllm](https://github.com/lyogavin/airllm) — ⭐0 (+1,716 today) — Breakthrough memory optimization enabling 70B-class model inference on a single 4GB GPU.
- [firecrawl](https://github.com/firecrawl/firecrawl) — ⭐161,010 — The context API for web scraping and interaction at scale; also launching today's `pdf-inspector` Rust library (+2,524).
- [picollm](https://github.com/Picovoice/picollm) — ⭐316 — On-device LLM inference using X-Bit quantization for edge deployments.
- [rig](https://github.com/0xPlaygrounds/rig) — ⭐8,168 — Modular Rust framework for building scalable LLM applications.
- [tiny-llm](https://github.com/skyzh/tiny-llm) — ⭐4,440 — Educational course for systems engineers to build a tiny vLLM + Qwen from scratch.

### 🤖 AI Agents / Workflows
- [AutoGPT](https://github.com/Significant-Gravitas/AutoGPT) — ⭐185,811 — The long-standing open-source vision for accessible, buildable AI agents.
- [langchain-ai/langchain](https://github.com/langchain-ai/langchain) — ⭐143,424 — The agent engineering platform, now positioning itself as the canonical framework for agent workflows.
- [browser-use/browser-use](https://github.com/browser-use/browser-use) — ⭐107,872 — Makes websites accessible to AI agents; today's `video-use` spinoff (+306) extends this to video editing.
- [obra/superpowers](https://github.com/obra/superpowers) — ⭐0 (+777 today) — A methodology-plus-framework for building reliable software agents — "the agentic development method that works."
- [ESengine/DeepSeek-Reasonix](https://github.com/esengine/DeepSeek-Reasonix) — ⭐30,742 (+924 today) — DeepSeek-native terminal coding agent optimized for prefix-cache stability.
- [TencentCloud/TencentDB-Agent-Memory](https://github.com/TencentCloud/TencentDB-Agent-Memory) — ⭐0 (+1,138 today) — Team-level memory hub converting conversations/docs/code into four reusable memory assets for agents.
- [livekit/agents](https://github.com/livekit/agents) — ⭐0 (+432 today) — Framework for building realtime voice AI agents — audio and video channel.
- [Eigenwise/atomic-agents](https://github.com/Eigenwise/atomic-agents) — ⭐6,115 — Building AI agents "atomically" — a modular, component-based approach.

### 📦 AI Applications
- [open-webui/open-webui](https://github.com/open-webui/open-webui) — ⭐147,850 — The most popular user-friendly interface for local LLM stacks (Ollama, OpenAI API).
- [dify](https://github.com/langgenius/dify) — ⭐151,339 — Collaborative workspace for building agentic workflows and RAG pipelines.
- [CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio) — ⭐49,406 — AI productivity studio with 300+ assistants and unified access to frontier LLMs.
- [harry0703/MoneyPrinterTurbo](https://github.com/harry0703/MoneyPrinterTurbo) — ⭐101,607 — AI-powered one-click generation of HD short videos from a topic or keyword.
- [Panniantong/Agent-Reach](https://github.com/Panniantong/Agent-Reach) — ⭐66,462 — One CLI giving agents eyes across Twitter, Reddit, YouTube, Bilibili, and more.
- [hugohe3/ppt-master](https://github.com/hugohe3/ppt-master) — ⭐43,000 — AI turns documents into native PowerPoint decks with animations, charts, and narration.
- [ZhuLinsen/daily_stock_analysis](https://github.com/ZhuLinsen/daily_stock_analysis) — ⭐60,061 — LLM-driven multi-market stock analysis with real-time news and dashboards.

### 🧠 LLMs / Training
- [huggingface/transformers](https://github.com/huggingface/transformers) — ⭐163,336 — The canonical model-definition framework for state-of-the-art ML models.
- [LLMs-from-scratch](https://github.com/rasbt/LLMs-from-scratch) — ⭐100,559 — Step-by-step implementation of a ChatGPT-like LLM in PyTorch — the go-to learning resource.
- [open-compass/opencompass](https://github.com/open-compass/opencompass) — ⭐7,273 — Comprehensive LLM evaluation platform over 100+ datasets.
- [AarambhDevHub/aarambh-studio](https://github.com/AarambhDevHub/aarambh-studio) — ⭐62 — Decoder-only LLM built from scratch in pure Rust using Candle; gated DeltaNet, sparse attention, MoE.
- [awesome-llm-unlearning](https://github.com/chrisliu298/awesome-llm-unlearning) — ⭐617 — Curated resources on machine unlearning in LLMs — a growing research niche.

### 🔍 RAG / Knowledge
- [firecrawl/pdf-inspector](https://github.com/firecrawl/pdf-inspector) — ⭐0 (+2,524 today) — Fast Rust PDF inspection/classification for smart routing between scanned vs. text-based documents.
- [RAGFlow](https://github.com/infiniflow/ragflow) — ⭐86,818 — Leading open-source RAG engine fusing with agent capabilities for a superior context layer.
- [mem0ai/mem0](https://github.com/mem0ai/mem0) — ⭐62,520 — The universal memory layer for AI agents completing session-to-session persistence.
- [milvus-io/milvus](https://github.com/milvus-io/milvus) — ⭐45,510 — High-performance cloud-native vector database for scalable ANN search.
- [qdrant/qdrant](https://github.com/qdrant/qdrant) — ⭐33,779 — High-performance, massive-scale vector database for the next generation of AI.
- [Graphify-Labs/graphify](https://github.com/Graphify-Labs/graphify) — ⭐102,476 — Turn any codebase, docs, SQL schemas into a queryable knowledge graph via deterministic AST parsing.
- [headroomlabs-ai/headroom](https://github.com/headroomlabs-ai/headroom) — ⭐64,756 — Compress tool outputs, logs, and RAG chunks before they reach the LLM — up to 95% token reduction on JSON.
- [StarTrail-org/LEANN](https://github.com/StarTrail-org/LEANN) — ⭐12,760 — MLsys2026 paper: 97% storage savings for private, on-device RAG.

## 3. Trend Signal Analysis

**Explosive community attention** today centers on the **coding-agent skill ecosystem** — reusable, composable instruction sets that extend Claude Code, Cursor, Codex, and similar tools. The trending list's `superpowers` (+777), `reverse-skill` (+2,310), and `compound-engineering-plugin` (+33) point to a shift from "agents as monoliths" to "agents as platforms" with installable skills (graphify's 102K stars is the trailblazer here). This suggests the community now treats coding agents like IDEs — extensible, configurable, and supplemented by a skill marketplace.

**Memory and context** is the other dominant theme. TencentCloud's `TencentDB-Agent-Memory` (+1,138 today) and `claude-mem` (89K stars) both attack the same problem: agents have no persistent team or session memory. This is the "operating system" layer of multi-agent, multi-session workflows — and it's not yet solved. Expect heavy corporate investment here soon.

**First-time signals:** the rise of Rust in the AI toolchain is notable — `pdf-inspector`, `rig`, `picollm`, `aarambh-studio`, and `qdrant` all favor Rust for performance-critical AI components. Also, "vectorless RAG" is appearing — see `PageIndex` (35K) and `LEANN` — challenging the assumption that vector DBs are mandatory for retrieval.

**Industry connection:** today's trends align with the broader push toward **on-device and low-resource AI** — `airllm` (4GB GPU 70B) and `LEANN` (97% storage reduction) respond to the cost/scale ceiling of cloud-centric AI architectures. Meanwhile, the surge in agent-memory and knowledge-graph projects signals that the post-scaling era is about **context engineering** — what you pipe in, how you compress it, and what the agent remembers.

## 4. Community Hot Spots

- **Coding-agent skills market** — `superpowers` (+777), `compound-engineering-plugin` (+33), and `reverse-skill` (+2,310) all define "skills as a distribution unit" for AI coding clients. This is the fastest-growing niche in today's trending data.
- **Agent memory and persistence** — `TencentDB-Agent-Memory` (+1,138 today) and `claude-mem` (89,557 stars) are solving the biggest blocker to production-grade agent teams: shared, governed, reusable memory.
- **Document intelligence as infrastructure** — `firecrawl/pdf-inspector` (+2,524 today) shows that PDF classification and extraction are becoming a must-have foundational layer for enterprise RAG. Expect more specialized document parsers.
- **DeepSeek-specific tooling** — `DeepSeek-Reasonix` (+924 today) demonstrates DeepSeek's rising weight in the open-source coding-agent space, competing with OpenAI/Anthropic-centric tooling.
- **Low-resource inference** — `airllm` (+1,716 today) proves there is huge appetite for running frontier-scale models on consumer hardware; watch for more quantization/offloading innovations.

---
*This digest is auto-generated by [agents-radar](https://github.com/kky-wollu/agents-radar).*
# AI Open Source Trends 2026-08-10

> Sources: GitHub Trending + GitHub Search API | Generated: 2026-08-09 22:35 UTC

---

# AI Open Source Trends Report — 2026-08-10

## Step 1: AI Relevance Filter

**Excluded (non-AI):**
- `pranshuparmar/witr` (process tracing CLI)
- `goauthentik/authentik` (identity management)
- `msitarzewski/agency-agents` (AI-adjacent marketing tool, no core AI tech)

**Included (AI-related):** All remaining trending repos + 79 topic-search repos (deduplicated to ~60 unique projects by removing cross-topic duplicates).

---

## Step 2: Categorization

### 🔧 AI Infrastructure
- `affaan-m/ECC`, `addyosmani/agent-skills`, `google/skills`, `google-deepmind/weathernext`, `ollama/ollama`, `huggingface/transformers`, `langchain-ai/langchain`, `langchain-ai/langgraph`, `tensorflow/tensorflow`, `pytorch/pytorch`, `ultralytics/ultralytics`, `roboflow/supervision`, `Picovoice/picollm`, `dg/ai-access`, `langchain4j/langchain4j`, `skyzh/tiny-llm`

### 🤖 AI Agents / Workflows
- `PrimeIntellect-ai/prime-agent`, `NousResearch/hermes-agent`, `Significant-Gravitas/AutoGPT`, `Panniantong/Agent-Reach`, `santifer/career-ops`, `CherryHQ/cherry-studio`, `HKUDS/nanobot`, `zhayujie/CowAgent`, `siyuan-note/siyuan`, `bojieli/ai-agent-book`, `agentscope-ai/QwenPaw`, `esengine/DeepSeek-Reasonix`, `iOfficeAI/AionUi`, `Gitlawb/openclaude`, `Eigenwise/atomic-agents`, `harveyai/harvey-labs`, `browser-use/browser-use`, `headroomlabs-ai/headroom`, `mem0ai/mem0`, `thedotmack/claude-mem`, `pingdotgg/t3code`

### 📦 AI Applications
- `ZhuLinsen/daily_stock_analysis`, `hugohe3/ppt-master`, `harry0703/MoneyPrinterTurbo`, `Comfy-Org/ComfyUI`, `kennethleungty/Finance-LLMs`, `vitali87/code-graph-rag`, `Graphify-Labs/graphify`

### 🧠 LLMs / Training
- `rasbt/LLMs-from-scratch`, `jingyaogong/minimind`, `open-compass/opencompass`, `llm-jp/awesome-japanese-llm`, `chrisliu298/awesome-llm-unlearning`, `AIDASLab/Awesome-Diffusion-LLM`, `0xPlaygrounds/rig`, `genieincodebottle/generative-ai`, `liguge/Awesome-large-language-model-for-Prognostics-and-health-management`, `HKBU-LAGAS/Awesome-Item-ID-Gen-RecSys`

### 🔍 RAG / Knowledge
- `infiniflow/ragflow`, `Shubhamsaboo/awesome-llm-apps`, `Mintplex-Labs/anything-llm`, `FlowiseAI/Flowise`, `run-llama/llama_index`, `milvus-io/milvus`, `qdrant/qdrant`, `weaviate/weaviate`, `alibaba/zvec`, `lancedb/lancedb`, `oramasearch/orama`, `topoteretes/cognee`, `meilisearch/meilisearch`, `VectifyAI/PageIndex`, `neuml/txtai`, `oceanbase/oceanbase`, `databendlabs/databend`, `paulburgess1357/nvim-mcp`

---

## Step 3: Structured Report

---

# AI Open Source Trends Report — 2026-08-10

## 1. Today's Highlights

Today's GitHub trending landscape is dominated by **Agent Skills** — a rapidly crystallizing new format for packaging engineering knowledge as consumable agent capabilities. Two independent repositories — Google's official [google/skills](https://github.com/google/skills) (+532★) and Addy Osmani's [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills) (+670★) — both hit trending simultaneously, signaling platform-level standardization around this concept. Meanwhile, [PrimeIntellect-ai/prime-agent](https://github.com/PrimeIntellect-ai/prime-agent) surged +2,319★ with its "self-improving RLM agent" for autonomous coding, representing a shift toward agents that modify their own reward models. The RAG stack is consolidating around knowledge graphs, with [vitali87/code-graph-rag](https://github.com/vitali87/code-graph-rag) and [Graphify-Labs/graphify](https://github.com/Graphify-Labs/graphify) both trending with AST-based, no-vector-store approaches. Notably, [ollama/ollama](https://github.com/ollama/ollama) now references Kimi-K2.6, GLM-5.2, MiniMax, and gpt-oss — confirming a world of rapidly commoditized frontier models that further accelerates the agent-tooling gold rush.

---

## 2. Top Projects by Category

### 🔧 AI Infrastructure

- **[affaan-m/ECC](https://github.com/affaan-m/ECC)** — 239,013★ — "The agent harness performance optimization system" that layers skills, instincts, memory, and security on top of Claude Code, Cursor, and other coding CLIs.
- **[ollama/ollama](https://github.com/ollama/ollama)** — 178,136★ — Now runs Kimi-K2.6, GLM-5.2, MiniMax, DeepSeek, gpt-oss, and Qwen locally; the definitive local inference entry point.
- **[addyosmani/agent-skills](https://github.com/addyosmani/agent-skills)** — 0★ (+670 today) — Production-grade engineering skills for AI coding agents; a canonical, high-quality collection that may set the standard.
- **[google/skills](https://github.com/google/skills)** — 0★ (+532 today) — Google's official Agent Skills library for its products and technologies; validates the skills-as-packages paradigm.
- **[esengine/DeepSeek-Reasonix](https://github.com/esengine/DeepSeek-Reasonix)** — 33,421★ — A DeepSeek-native terminal coding agent built around prefix-cache stability for long-running sessions.
- **[Picovoice/picollm](https://github.com/Picovoice/picollm)** — 316★ — On-device LLM inference powered by X-bit quantization; notable for extreme edge deployment.

### 🤖 AI Agents / Workflows

- **[PrimeIntellect-ai/prime-agent](https://github.com/PrimeIntellect-ai/prime-agent)** — 0★ (+2,319 today) — Self-improving RLM agent for coding; today's biggest mover, signaling demand for agents that evolve their own reward models.
- **[NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent)** — 227,915★ — "The agent that grows with you" — a personalized, adaptive agent framework from a leading open-weight model lab.
- **[Significant-Gravitas/AutoGPT](https://github.com/Significant-Gravitas/AutoGPT)** — 186,460★ — The pioneering autonomous-agent platform, still a baseline reference for task-driven AI.
- **[zhayujie/CowAgent](https://github.com/zhayujie/CowAgent)** — 46,432★ — An open-source multi-model, multi-megachannel assistant/agent harness (formerly chatgpt-on-wechat).
- **[browser-use/browser-use](https://github.com/browser-use/browser-use)** — 108,478★ — Makes websites accessible to AI agents; the leading browser automation layer for agents.
- **[Panniantong/Agent-Reach](https://github.com/Panniantong/Agent-Reach)** — 69,690★ — Gives agents eyes to the entire internet (Twitter, Reddit, YouTube, Bilibili, Xiaohongshu) via a single zero-cost CLI.
- **[mem0ai/mem0](https://github.com/mem0ai/mem0)** — 62,877★ — Universal memory layer for AI agents, now essential tooling in the agent stack.
- **[harveyai/harvey-labs](https://github.com/harveyai/harvey-labs)** — 0★ (+87 today) — A benchmark for evaluating legal-work agents; a pioneer of domain-specific agent evaluation.

### 📦 AI Applications

- **[Comfy-Org/ComfyUI](https://github.com/Comfy-Org/ComfyUI)** — 0★ (+333 today) — The most powerful modular diffusion GUI and graph/nodes backend for generative art pipelines.
- **[ZhuLinsen/daily_stock_analysis](https://github.com/ZhuLinsen/daily_stock_analysis)** — 61,142★ (+287 today) — LLM-driven multi-market stock analysis with real-time news, decision dashboards, and automated push.
- **[hugohe3/ppt-master](https://github.com/hugohe3/ppt-master)** — 44,090★ — Generates native PowerPoint decks with shapes, transitions, narration, and data-backed charts from documents.
- **[harry0703/MoneyPrinterTurbo](https://github.com/harry0703/MoneyPrinterTurbo)** — 102,328★ — Generates short videos from a topic or keyword via automated AI workflows.
- **[vitali87/code-graph-rag](https://github.com/vitali87/code-graph-rag)** — 0★ (+59 today) — "The ultimate RAG for your monorepo": query, understand, and edit multi-language codebases with knowledge graphs.
- **[kennethleungty/Finance-LLMs](https://github.com/kennethleungty/Finance-LLMs)** — 135★ — Curated real-world LLM & AI agent use cases in financial services.

### 🧠 LLMs / Training

- **[rasbt/LLMs-from-scratch](https://github.com/rasbt/LLMs-from-scratch)** — 102,020★ — Step-by-step implementation of a ChatGPT-like LLM in PyTorch; the standard educational path.
- **[jingyaogong/minimind](https://github.com/jingyaogong/minimind)** — 54,497★ — Train a 64M-parameter LLM from scratch in 2 hours; lowers the entry barrier to pretraining.
- **[0xPlaygrounds/rig](https://github.com/0xPlaygrounds/rig)** — 8,219★ — Rust framework for building modular, scalable LLM applications; a fast-growing non-Python option.
- **[open-compass/opencompass](https://github.com/open-compass/opencompass)** — 7,287★ — Open-source LLM evaluation platform supporting 100+ datasets and most major models.
- **[skyzh/tiny-llm](https://github.com/skyzh/tiny-llm)** — 4,454★ — Teaches you to build a tiny vLLM + Qwen inference stack on Apple Silicon — systems-level LLM education.

### 🔍 RAG / Knowledge

- **[infiniflow/ragflow](https://github.com/infiniflow/ragflow)** — 87,123★ — Leading open-source RAG engine with deep document understanding, now fused with agent capabilities.
- **[Mintplex-Labs/anything-llm](https://github.com/Mintplex-Labs/anything-llm)** — 64,527★ — A local-first "everything" toolkit for RAG and agentic responses, focused on data ownership.
- **[milvus-io/milvus](https://github.com/milvus-io/milvus)** — 45,571★ — High-performance cloud-native vector database; the de facto standard at scale.
- **[qdrant/qdrant](https://github.com/qdrant/qdrant)** — 33,888★ — High-performance vector search engine built for next-gen AI workloads.
- **[topoteretes/cognee](https://github.com/topoteretes/cognee)** — 29,889★ — The open-source AI memory platform that gives agents persistent long-term memory via a knowledge-graph engine.
- **[Graphify-Labs/graphify](https://github.com/Graphify-Labs/graphify)** — 104,596★ — Converts any codebase, docs, SQL, configs, and PDFs into a queryable knowledge graph — no vector store needed.
- **[VectifyAI/PageIndex](https://github.com/VectifyAI/PageIndex)** — 35,100★ — Vectorless, reasoning-based RAG for documents; an explicit alternative to embeddings.

---

## 3. Trend Signal Analysis

Today's hot list reveals several aligned signals that are reshaping the open-source AI ecosystem.

**1. Agent Skills as a distributable artifact.** The simultaneous appearance of [google/skills](https://github.com/google/skills) and [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills) is not coincidental — it marks the "npm moment" for AI agent capabilities. Skills — packaged prompts/workflows that teach agents specific engineering competencies — are becoming the primary way organizations share and version agent expertise. With [iOfficeAI/AionUi](https://github.com/iOfficeAI/AionUi) and [Gitlawb/openclaude](https://github.com/Gitlawb/openclaude) enabling cross-CLI orchestration, we are seeing convergence on a universal agent-runtime layer where skills are swappable.

**2. From passive LLM apps to self-improving agents.** [PrimeIntellect-ai/prime-agent](https://github.com/PrimeIntellect-ai/prime-agent) (+2,319★ in a day) is a clear breakout. Its "RLM" (reinforcement learning for models) approach — where the agent continuously updates its own reward model based on task outcomes — points toward a future where systems are no longer statically configured but continuously adapted to user workflows. This is a meaningful departure from function-calling-based agents.

**3. The end of the vector-store monopoly.** The simultaneous traction of [vitali87/code-graph-rag](https://github.com/vitali87/code-graph-rag), [Graphify-Labs/graphify](https://github.com/Graphify-Labs/graphify), and [VectifyAI/PageIndex](https://github.com/VectifyAI/PageIndex) signals a decisive industry shift: semantically-rich, explainable knowledge graphs with deterministic AST parsing are displacing opaque embeddings for code-heavy and document-heavy RAG. "Vectorless RAG" is officially a category.

**4. Context + memory as first-class infrastructure.** [headroomlabs-ai/headroom](https://github.com/headroomlabs-ai/headroom) (60–95% token compression), [thedotmack/claude-mem](https://github.com/thedotmack/claude-mem) (session memory), and [mem0ai/mem0](https://github.com/mem0ai/mem0) are converging on a "context layer" that sits between LLMs and applications. Expect this to consolidate into a formal protocol.

**5. Local-first and open-weights normalization.** [ollama/ollama](https://github.com/ollama/ollama) now ships Kimi-K2.6, GLM-5.2, and gpt-oss by default — a sign that the open-weights ecosystem has reached parity with closed APIs for local deployment. Enterprise developers are increasingly treating local inference as the default, not the exception.

---

## 4. Community Hot Spots

- **Agent Skills Ecosystem (watch this closely).** Both [google/skills](https://github.com/google/skills) and [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills) are loading within hours. If you are building agent tooling, supporting the "skill" format will likely become mandatory.

- **Self-improving agents.** [prime-agent](https://github.com/PrimeIntellect-ai/prime-agent) is today's fastest riser. RLM (reward-model learning) codifying self-improvement is likely the next major agent paradigm beyond function calling.

- **Knowledge graphs over vector stores.** [cognee](https://github.com/topoteretes/cognee), [graphify](https://github.com/Graphify-Labs/graphify), and [code-graph-rag](https://github.com/vitali87/code-graph-rag) represent an architectural correction. Whatever you are building in RAG, consider a hybrid graph + embedding approach.

- **Legal and domain-specific agent benchmarks.** [harvey-labs](https://github.com/harveyai/harvey-labs) is the first major benchmark for legal-agent quality. Watch for analogous benchmarks in finance, healthcare, and coding — these will define the next generation of evaluation methodology.

- **Memory and context compression.** [headroom](https://github.com/headroomlabs-ai/headroom) and [claude-mem](https://github.com/thedotmack/claude-mem) address the most urgent practical bottleneck in agentic workflows: context window exhaustion. Expect aggressive consolidation here.

---

*Report generated from 2026-08-10 GitHub trending + topic search data.*

---
*This digest is auto-generated by [agents-radar](https://github.com/kky-wollu/agents-radar).*
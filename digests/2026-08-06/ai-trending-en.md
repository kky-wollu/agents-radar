# AI Open Source Trends 2026-08-06

> Sources: GitHub Trending + GitHub Search API | Generated: 2026-08-05 23:05 UTC

---

## AI Open Source Trends Report — 2026-08-06

---

### Step 1: Filter

From the 13 trending repositories, **10 are clearly AI/ML related** and retained:

| Project | Included? | Reason |
|---|---|---|
| cloudflare/computer | ✅ | Agent computer-use runtime |
| huangruiteng/loopx | ✅ | Agent loop state kernel |
| TencentCloud/TencentDB-Agent-Memory | ✅ | Agent memory hub |
| donnemartin/system-design-primer | ❌ | General engineering education |
| firecrawl/pdf-inspector | ✅ | AI-driven PDF routing/classification |
| esengine/DeepSeek-Reasonix | ✅ | Coding agent |
| addyosmani/agent-skills | ✅ | Skills for coding agents |
| obra/superpowers | ✅ | Agent skills framework |
| roboflow/supervision | ✅ | Computer vision tooling |
| vercel/next.js | ❌ | General frontend framework |
| tailwindlabs/tailwindcss | ❌ | General CSS framework |
| uber/ADR | ✅ | Enterprise agent security |
| lyogavin/airllm | ✅ | Low-resource LLM inference |

**(9 → Actually 10 retained: DeepSeek-Reasonix appears twice in trend list? No — counted once. Final: 10/13 AI-relevant.)**

All 80 topic-search results are AI-related and carried forward.

---

### Step 2: Categorization

| Category | Projects |
|---|---|
| 🔧 AI Infrastructure | cloudflare/computer, firecrawl/pdf-inspector, esengine/DeepSeek-Reasonix, uber/ADR, airllm, vllm, ollama, langchain, transformers, milvus, qdrant, lancedb, meilisearch, zvec, txtai, rig, atomic-agents, tiny-llm, picollm, aarambh-studio |
| 🤖 AI Agents / Workflows | loopx, TencentDB-Agent-Memory, addyosmani/agent-skills, obra/superpowers, AutoGPT, browser-use, hermes-agent, Agent-Reach, career-ops, cowagent, nanobot, CopilotKit, QwenPaw, claude-mem, headroom, openclaude, ECC, jeecgboot, airflow, hello-agents, ai-agent-book |
| 📦 AI Applications | CherryHQ/cherry-studio, MoneyPrinterTurbo, ppt-master, daily_stock_analysis, OpenBB, supervision, faceswap, telegram-summary-bot, siyuan, AionUi, anything-llm, open-webui |
| 🧠 LLMs / Training | opencompass, awesome-japanese-llm, AwesomeOPD, awesome-llm-unlearning, Awesome-Diffusion-LLM, Finance-LLMs, Awesome-PHM-LLM, Awesome-Item-ID-Gen-RecSys, generative-ai, ML-For-Beginners, keras, pytorch, tensorflow |
| 🔍 RAG / Knowledge | dify, ragflow, llama_index, mem0, cognee, RAG_Techniques, Graphify, PageIndex, LEANN, orama, graphify, langchain4j, milvus, qdrant, weaviate |

---

### Step 3: Report

---

## 1. Today's Highlights

Today's AI open-source landscape is dominated by **agent memory and persistence infrastructure**. TencentCloud's Agent-Memory hub surged +1,891 stars — the strongest signal that team-level shared memory for agents has moved from experimental to production-critical. The second major theme is **agent skills as a formal engineering practice**: obra/superpowers (+931) and addyosmani/agent-skills (+203) both treat skills as versionable, shareable artifacts — a clear normalization of the "agent skill" concept. Third, **inference efficiency on constrained hardware** remains white-hot: airllm's single-4GB-GPU 70B inference jumped +833 stars, and firecrawl's rust-based pdf-inspector (+1,583) shows classical AI tasks being rebuilt for speed. Finally, **Uber's ADR (+354) marks enterprise agent security/observability as a first-class open-source category** — a bellwether for corporate adoption.

---

## 2. Top Projects by Category

### 🔧 AI Infrastructure

| Project | Stars | Why today |
|---|---|---|
| [cloudflare/computer](https://github.com/cloudflare/computer) | 0 (+796 today) | Cloudflare's agent computer-use runtime — a large cloud provider entering agent infrastructure directly. |
| [firecrawl/pdf-inspector](https://github.com/firecrawl/pdf-inspector) [Rust] | 0 (+1,583 today) | Fast PDF classification/scan-detection library for smart document routing in agent pipelines. |
| [esengine/DeepSeek-Reasonix](https://github.com/esengine/DeepSeek-Reasonix) [Go] | 31,551 (+747 today) | DeepSeek-native terminal coding agent tuned for prefix-cache stability — cost-efficient long sessions. |
| [uber/ADR](https://github.com/uber/ADR) [Python] | 0 (+354 today) | Enterprise agent observability, security benchmarking, and threat detection — battle-tested at Uber. |
| [lyogavin/airllm](https://github.com/lyogavin/airllm) [Jupyter Notebook] | 0 (+833 today) | Runs 70B models on a single 4GB GPU — critical for local, privacy-preserving inference. |
| [vllm-project/vllm](https://github.com/vllm-project/vllm) | 88,278 | The de-facto high-throughput LLM serving engine; continued relevance as agent traffic grows. |

### 🤖 AI Agents / Workflows

| Project | Stars | Why today |
|---|---|---|
| [TencentCloud/TencentDB-Agent-Memory](https://github.com/TencentCloud/TencentDB-Agent-Memory) [TypeScript] | 0 (+1,891 today) | **Today's top gainer.** Team-level agent memory hub: Chat Memory, Skills, LLM-Wiki, Code-Graph — governed and shared. |
| [obra/superpowers](https://github.com/obra/superpowers) [Shell] | 0 (+931 today) | Agentic skills framework + software development methodology — treats agent skills as engineering discipline. |
| [huangruiteng/loopx](https://github.com/huangruiteng/loopx) [Python] | 0 (+327 today) | Lightweight loop-engineering state kernel for long-running agent teams — durable goals, quota-aware auto-wake, verifiable handoffs. |
| [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills) [JavaScript] | 0 (+203 today) | Production-grade engineering skills for coding agents — by a well-known Google engineering leader. |
| [NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent) | 226,044 | Self-evolving agent platform — the largest agent repo in the topic search. |
| [affaan-m/ECC](https://github.com/affaan-m/ECC) | 238,008 | Agent harness performance optimization — skills, instincts, memory, security, research-first. Most-starred repo across all topics today. |
| [Significant-Gravitas/AutoGPT](https://github.com/Significant-Gravitas/AutoGPT) | 185,834 | The original autonomous agent platform — still a reference point and active. |

### 📦 AI Applications

| Project | Stars | Why today |
|---|---|---|
| [Panniantong/Agent-Reach](https://github.com/Panniantong/Agent-Reach) | 67,014 | One CLI to read/search Twitter, Reddit, YouTube, GitHub, Bilibili, Xiaohongshu — zero API fees. |
| [CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio) | 49,643 | AI productivity studio with 300+ assistants and autonomous agents — unified access to frontier LLMs. |
| [hugohe3/ppt-master](https://github.com/hugohe3/ppt-master) | 43,249 | AI turns documents into native PowerPoint decks with animations, charts, and audio narration. |
| [ZhuLinsen/daily_stock_analysis](https://github.com/ZhuLinsen/daily_stock_analysis) | 60,186 | LLM-powered multi-market stock analysis with decision dashboards and automated notifications. |
| [OpenBB-finance/OpenBB](https://github.com/OpenBB-finance/OpenBB) | 71,444 | Open data platform for analysts and AI agents — financial intelligence at scale. |
| [roboflow/supervision](https://github.com/roboflow/supervision) | 48,893 (+132 today) | Reusable computer vision tools — a stable, widely-used CV utility layer. |

### 🧠 LLMs / Training

| Project | Stars | Why today |
|---|---|---|
| [open-compass/opencompass](https://github.com/open-compass/opencompass) | 7,277 | LLM evaluation platform over 100+ datasets — increasingly critical as more models ship. |
| [skyzh/tiny-llm](https://github.com/skyzh/tiny-llm) | 4,443 | Hands-on course: build a tiny vLLM + Qwen on Apple Silicon — educational pipeline for inference engineering. |
| [AarambhDevHub/aarambh-studio](https://github.com/AarambhDevHub/aarambh-studio) | 63 | Decoder-only LLM from scratch in pure Rust (Candle) — Gated DeltaNet, MoE, quantization-aware. |
| [llm-jp/awesome-japanese-llm](https://github.com/llm-jp/awesome-japanese-llm) | 1,423 | Japanese LLM ecosystem overview — non-English model landscape continues to grow. |
| [thinkwee/AwesomeOPD](https://github.com/thinkwee/AwesomeOPD) | 804 | On-policy distillation resource list — latest training efficiency direction. |

### 🔍 RAG / Knowledge

| Project | Stars | Why today |
|---|---|---|
| [Graphify-Labs/graphify](https://github.com/Graphify-Labs/graphify) | 103,014 | Turns any codebase into a queryable knowledge graph — vectorless, deterministic AST parsing. |
| [thedotmack/claude-mem](https://github.com/thedotmack/claude-mem) | 89,740 | Persistent cross-session agent memory — captures, compresses, and reinjects context for any agent. |
| [mem0ai/mem0](https://github.com/mem0ai/mem0) | 62,610 | Universal memory layer for AI agents — the standard for agent memory abstraction. |
| [infiniflow/ragflow](https://github.com/infiniflow/ragflow) | 86,904 | Leading open-source RAG engine with agent capabilities — a mature production choice. |
| [headroomlabs-ai/headroom](https://github.com/headroomlabs-ai/headroom) | 65,038 | Compresses tool outputs/logs/RAG chunks before they hit the LLM — 20-95% token reduction. |
| [topoteretes/cognee](https://github.com/topoteretes/cognee) | 29,797 | Self-hosted knowledge-graph memory engine for agents — persistent long-term memory. |

---

## 3. Trend Signal Analysis

**Three explosive directions dominate today:**

**(1) Agent memory as the new competitive frontier.** TencentDB-Agent-Memory (+1,891), claude-mem, mem0, cognee, and loopx all attack the same problem: agents today are amnesiac. The community is converging on memory as a **shared infrastructure layer** — not per-agent state, but team-level, governed, queryable memory assets. This is the natural next step after agent frameworks matured.

**(2) Agent skills as a formal engineering practice.** obra/superpowers and addyosmani/agent-skills both treat skills as first-class artifacts — versionable, shareable, reviewable. This normalizes "agent skills" the way "packages" and "libraries" were normalized decades ago. Expect skill registries and package managers for agents to emerge.

**(3) Efficient inference on commodity hardware.** airllm's 4GB-GPU 70B inference and aarambh-studio's pure-Rust LLM signal that the community is actively fighting GPU scarcity. Combined with prefix-cache engineering in DeepSeek-Reasonix, the message is clear: **the winner in agents is whoever minimizes tokens and maximizes context re-use.**

Notable new appearance: **enterprise agent security (uber/ADR)** — observability, threat detection, and benchmarking for agents. This is the "DevOps moment" for agents: security tooling arriving after rapid adoption, aimed at CIO approval.

The stack is consolidating around TypeScript/Rust for infrastructure and Python for AI logic — with Go making inroads (DeepSeek-Reasonix, RAGFlow).

---

## 4. Community Hot Spots

- **TencentDB-Agent-Memory** — Team-level memory hub with four memory asset types. If you're building multi-agent systems, this is today's must-read architecture reference.
- **obra/superpowers** — Agentic skills framework + methodology. Represents the formalization of agent skills into engineering practice — watch for a "skill ecosystem" to emerge.
- **cloudflare/computer** — A hyperscaler entering agent-computer interaction. Signals that agent infrastructure is becoming a platform play with serious vendor backing and edge distribution.
- **airllm** — Local 70B inference on 4GB GPU. For any developer facing GPU constraints, this is the most actionable efficiency trick in today's list.
- **uber/ADR** — Enterprise agent security. The first credible open-source answer to "how do we safely deploy agents in production?" — relevant for any team approaching org-wide rollouts.
- **Graphify** — Vectorless, reasoning-based RAG with 103k stars. Challenges the vector-database default with a deterministic AST/knowledge-graph approach — worth evaluating if you're hitting RAG quality limits.

---
*This digest is auto-generated by [agents-radar](https://github.com/kky-wollu/agents-radar).*
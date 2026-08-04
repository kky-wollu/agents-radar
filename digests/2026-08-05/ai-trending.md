# AI 开源趋势日报 2026-08-05

> 数据来源: GitHub Trending + GitHub Search API | 生成时间: 2026-08-04 23:06 UTC

---

# 🤖 AI 开源趋势日报

**日期：2026-08-05** | **数据来源：GitHub Trending & 主题搜索**


## 📌 今日速览

1. **AI 智能体生态迎来“记忆”大战**：今日 Trending 榜首 TencentDB-Agent-Memory 单日斩获 1138 stars，聚焦团队级智能体记忆共享；同时 mem0、claude-mem、cognee 等多款记忆方案在主题搜索中表现活跃，智能体持久化记忆正成为基础设施级刚需。

2. **Python 之外的 LLM 工程语言崛起**：Go 语言编写的 DeepSeek-Reasonix（AI 终端编码助手）今日 +924 stars，Rust 生态的 PDF 智能识别库 pdf-inspector 更是暴涨 +2524 stars 登顶今日 Trending——AI 工具链不再被 Python 垄断，系统级语言正加速入场。

3. **Agent Skills（技能包）模式全面爆发**：从 superpowers 框架到 reverse-skill（安全渗透技能包），再到 EveryInc 的 compound-engineering-plugin，“可插拔技能”已成为智能体开发的主流范式。

4. **视频生成/编辑成为 AI 应用新热点**：browser-use 团队推出的 video-use 以 AI 智能体驱动视频编辑，首日即获 306 stars，继文本、图像之后，视频正在成为 AI 应用的下一主战场。

5. **本地化、轻量化推理持续升温**：AirLLM 以单张 4GB GPU 运行 70B 模型今日 +1716 stars，侧面反映出社区对低成本本地推理的旺盛需求。


## 📂 各维度热门项目

### 🔧 AI 基础工具（框架、SDK、推理引擎、开发工具、CLI）

- **[firecrawl/pdf-inspector](https://github.com/firecrawl/pdf-inspector)** — ⭐ 新增 +2524（今日最热）
  基于 Rust 的高性能 PDF 检测与文本提取库，可智能区分扫描版与文本版 PDF。今日暴涨 +2524 stars，成为单日最大黑马，是 RAG 数据预处理链路的利器。

- **[lyogavin/airllm](https://github.com/lyogavin/airllm)** — ⭐ +1716 today
  仅需单张 4GB 显存即可运行 70B 参数大模型，极大降低了本地大模型推理门槛，是“轻量化推理”方向的代表性项目。

- **[ollama/ollama](https://github.com/ollama/ollama)** — ⭐ 177,783
  本地运行大模型的事实标准工具，现已支持 Kimi-K2.6、GLM-5.2、DeepSeek 等最新模型，持续巩固其作为本地推理入口的地位。

- **[huggingface/transformers](https://github.com/huggingface/transformers)** — ⭐ 163,336
  模型定义与训练的事实标准框架，支持文本、视觉、音频、多模态模型，持续引领开源模型生态。

- **[langchain-ai/langchain](https://github.com/langchain-ai/langchain)** — ⭐ 143,424
  Agent 工程化平台，已从单纯的 LLM 编排框架演进为完整的智能体开发平台。

- **[0xPlaygrounds/rig](https://github.com/0xPlaygrounds/rig)** — ⭐ 8,168
  基于 Rust 的模块化 LLM 应用开发框架，代表 Rust 在 AI 工程领域的新兴力量。

- **[googleworkspace/cli](https://github.com/googleworkspace/cli)** — ⭐ 30,199
  Google Workspace 官方 CLI 工具，基于 Discovery Service 动态构建，内置 AI Agent skills，支持 Drive、Gmail、Calendar 等全家桶操作。


### 🤖 AI 智能体/工作流（Agent 框架、自动化、多智能体）

- **[TencentCloud/TencentDB-Agent-Memory](https://github.com/TencentCloud/TencentDB-Agent-Memory)** — ⭐ +1138 today
  腾讯云推出的团队级智能体记忆中枢，将对话、文档、代码转化为四类可复用记忆资产（Chat Memory、Skill、LLM-Wiki、Code-Graph），解决多智能体场景下的知识共享与治理问题，是今日榜单中企业级 AI 基础设施的代表。

- **[obra/superpowers](https://github.com/obra/superpowers)** — ⭐ +777 today
  一套完整的 Agentic Skills 框架与软件开发方法论，重新定义了基于智能体的开发工作流。

- **[esengine/DeepSeek-Reasonix](https://github.com/esengine/DeepSeek-Reasonix)** — ⭐ +924 today（⭐ 总量 30,742）
  基于 Go 的 DeepSeek 原生终端 AI 编码助手，专为 prefix-cache 稳定性优化，可长期驻留运行，将 Go 的高性能与 AI 编码结合，代表“非 Python 系” AI 工具的新方向。

- **[browser-use/browser-use](https://github.com/browser-use/browser-use)** — ⭐ 107,872
  让网站对 AI 智能体完全可访问的浏览器自动化框架，是 AI 操作 Web 的核心基础设施。

- **[EveryInc/compound-engineering-plugin](https://github.com/EveryInc/compound-engineering-plugin)** — ⭐ +33 today
  官方发布的 Compound Engineering 插件，兼容 Claude Code、Codex、Cursor 等多个 AI 编码工具，推动“复合工程”方法的普及。

- **[Significant-Gravitas/AutoGPT](https://github.com/Significant-Gravitas/AutoGPT)** — ⭐ 185,811
  “AI 民主化”的旗帜性项目，提供人人可用的自主智能体平台，持续迭代。

- **[zhayujie/CowAgent](https://github.com/zhayujie/CowAgent)** — ⭐ 46,318
  开源超级 AI 助手与 Agent Harness（前身 chatgpt-on-wechat），支持任务规划、工具调用、技能扩展、自我进化，多模型多渠道，轻量可扩展。

- **[HKUDS/nanobot](https://github.com/HKUDS/nanobot)** — ⭐ 46,617
  超轻量、开源、自托管的个人 AI Agent 框架，纯 Python 实现，内置 WebUI、工具调用、记忆、MCP、多智能体工作流等能力。


### 📦 AI 应用（具体应用产品、垂直场景解决方案）

- **[browser-use/video-use](https://github.com/browser-use/video-use)** — ⭐ +306 today
  browser-use 团队推出的“用编码智能体编辑视频”工具，将 AI 智能体能力延伸到视频创作领域，创新性地打通了 AI 编程与音视频处理的边界。

- **[zhaoxuya520/reverse-skill](https://github.com/zhaoxuya520/reverse-skill)** — ⭐ +2310 today（今日第二热）
  面向逆向工程/渗透测试/安全研究的 AI 技能路由包，支持 Claude Code、Cursor、Cline 等主流 AI 编码客户端，为 AI 智能体注入安全攻防能力。

- **[livekit/agents](https://github.com/livekit/agents)** — ⭐ +432 today
  构建实时语音 AI 智能体的框架，覆盖语音、视频等多模态交互场景，是实时 AI 交互方向的热门选择。

- **[CherryHQ/cherry-studio](https://github.com/CherryHQ/cherry-studio)** — ⭐ 49,406
  AI 生产力工作室，提供智能聊天、自主智能体、300+ 助手，统一接入前沿 LLM，支持多模型协同。

- **[harry0703/MoneyPrinterTurbo](https://github.com/harry0703/MoneyPrinterTurbo)** — ⭐ 101,607
  利用 AI 大模型和自动化工作流一键生成高清短视频，是 AIGC 内容生产工具的标杆项目。

- **[ZhuLinsen/daily_stock_analysis](https://github.com/ZhuLinsen/daily_stock_analysis)** — ⭐ 60,061
  LLM 驱动的多市场股票智能分析系统，支持多源行情、实时新闻、决策看板与自动推送，零成本定时运行。

- **[hugohe3/ppt-master](https://github.com/hugohe3/ppt-master)** — ⭐ 43,000
  AI 将文档或主题转化为原生 PowerPoint 演示文稿，支持原生形状、转场动画、数据图表、音频旁白，并兼容自定义 .pptx 模板。

- **[santifer/career-ops](https://github.com/santifer/career-ops)** — ⭐ 62,788
  开源 AI 求职助手：扫描职位门户，用结构化 A-F 评分表评估岗位并给出 1.0-5.0 评分，定制简历、跟踪申请进度，完全本地运行于 AI 编码 CLI。


### 🧠 大模型/训练（模型权重、训练框架、微调工具）

- **[microsoft/generative-ai-for-beginners](https://github.com/microsoft/generative-ai-for-beginners)** — ⭐ +784 today
  微软出品的生成式 AI 入门教程，21 课系统讲解从基础到实战的完整路径，今日新增 784 stars 说明 AI 学习需求持续高涨。

- **[rasbt/LLMs-from-scratch](https://github.com/rasbt/LLMs-from-scratch)** — ⭐ 100,559
  从零开始用 PyTorch 实现 ChatGPT 类 LLM 的经典教程仓库，step-by-step 教学深受社区欢迎。

- **[NousResearch/hermes-agent](https://github.com/NousResearch/hermes-agent)** — ⭐ 225,471
  “与你一同成长的智能体”——NousResearch 推出的自适应学习智能体，代表 Agent 自我进化方向。

- **[open-compass/opencompass](https://github.com/open-compass/opencompass)** — ⭐ 7,273
  全面的 LLM 评估平台，支持 Llama3、GPT-4、Qwen、GLM、Claude 等 100+ 数据集上的评测，是模型选型和基准测试的重要工具。

- **[skyzh/tiny-llm](https://github.com/skyzh/tiny-llm)** — ⭐ 4,440
  面向系统工程师的 LLM 推理服务课程：在 Apple Silicon 上构建微型 vLLM + Qwen，深入理解推理系统原理。


### 🔍 RAG/知识库（向量数据库、检索增强、知识管理）

- **[infiniflow/ragflow](https://github.com/infiniflow/ragflow)** — ⭐ 86,818
  领先的开源 RAG 引擎，将 RAG 与 Agent 能力相结合，为 LLM 构建高质量上下文层。

- **[run-llama/llama_index](https://github.com/run-llama/llama_index)** — ⭐ 51,375
  LlamaIndex 已成为领先的文档 Agent 与 OCR 平台，覆盖从数据接入到知识服务的全链路。

- **[mem0ai/mem0](https://github.com/mem0ai/mem0)** — ⭐ 62,520
  AI Agent 的通用记忆层，为智能体提供跨会话的持久化记忆能力，是“智能体记忆”赛道的重要玩家。

- **[milvus-io/milvus](https://github.com/milvus-io/milvus)** — ⭐ 45,510
  高性能云原生向量数据库，专为大规模向量 ANN 搜索设计，是 RAG 架构中的核心存储组件。

- **[thedotmack/claude-mem](https://github.com/thedotmack/claude-mem)** — ⭐ 89,557
  跨会话的 Agent 持久上下文记忆工具——捕获 Agent 会话中的一切，用 AI 压缩并注入未来会话，支持 Claude Code、Codex、Gemini 等主流工具。

- **[topoteretes/cognee](https://github.com/topoteretes/cognee)** — ⭐ 29,777
  开源 AI 记忆平台，通过自托管知识图谱引擎为 Agent 提供跨会话的持久长期记忆。

- **[StarTrail-org/LEANN](https://github.com/StarTrail-org/LEANN)** — ⭐ 12,760
  [MLsys2026] 在个人设备上实现 97% 存储节省的高效私有 RAG，兼顾速度、准确性与隐私。


## 📈 趋势信号分析

**1. “智能体记忆”成为今日最大赛道：** TencentDB-Agent-Memory 登顶、mem0 62K stars、claude-mem 89K stars、cognee 29K stars——多家团队不约而同押注“记忆层”。AI 智能体正从“无状态工具调用”向“有状态持续学习”演进，这与 LLM 上下文窗口的技术瓶颈直接相关。Agent 的记忆能力正在成为继模型能力之后的新竞争焦点。

**2. 非 Python 语言进军 AI 工具链：** pdf-inspector（Rust）+2524、DeepSeek-Reasonix（Go）+924、rig（Rust）8.1K stars——Rust/Go 在性能敏感场景（推理引擎、CLI 工具、数据处理）的优势开始凸显。AI 工程正从“快速原型”走向“生产级性能”，系统级语言迎来窗口期。

**3. “技能包（Skills）”生态爆发：** superpowers（+777）、reverse-skill（+2310）、compound-engineering-plugin 等项目的走红，标志着 AI 编程从“问答式辅助”转向“可组合、可插拔的技能系统”。这一趋势与 Anthropic 推动的 Agent Skills 标准形成呼应。

**4. 安全/红队成为 AI 新场景：** Uber 的 ADR（企业 AI Agent 安全）、reverse-skill（渗透测试技能包）同期上榜，说明随着 Agent 大规模落地，安全防护与攻防对抗成为刚需。

**5. 企业级 AI 基础设施加速入局：** 腾讯云推出 Agent Memory、Google 发布 Workspace CLI、Uber 开源 ADR——大厂正将内部 AI 实践开源，企业级 AI 基础设施的竞争已从模型层蔓延到 Agent 编排与治理层。


## 🔥 社区关注热点

- **🔥 TencentDB-Agent-Memory（腾讯云）** — 企业级 Agent 记忆基础设施，四类记忆资产（对话、技能、知识、代码图谱）设计极具前瞻性，云厂商入局 Agent 生态的重要信号。

- **🔥 firecrawl/pdf-inspector** — 单日 +2524 stars 的 Rust 黑马，PDF 分类与文本提取是 RAG 数据预处理的核心痛点，性能敏感场景的 Rust 优势正在兑现。

- **🔥 zhaoxuya520/reverse-skill** — 单日 +2310 stars，将 AI 编码智能体与网络安全攻防结合，开辟了 AI Agent 的全新垂直应用场景。

- **🔥 AirLLM** — 4GB 显存运行 70B 模型，极大降低本地推理门槛，适合关注低成本部署的开发者，是边缘推理的代表项目。

- **🔥 browser-use/video-use** — AI 智能体驱动视频编辑，代表 AI 内容生产从文本/图像向视频跃迁的前沿方向，值得内容工具开发者重点关注。

---

*本报告由 AI 开源生态分析系统自动生成，仅供技术趋势参考。*

*报告生成时间：2026-08-05*

---
*本日报由 [agents-radar](https://github.com/kky-wollu/agents-radar) 自动生成。*
# Hugging Face 热门模型日报 2026-08-05

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-08-04 23:06 UTC

---

# 🤖 Hugging Face 热门模型日报 — 2026-08-05

## 📌 今日速览

本周 Hugging Face 生态迎来**多模态模型大爆发**：MiniMax-H3、Kimi-K3、GLM-5.2 等新一代旗舰模型集中亮相，下载量均突破百万级别。值得关注的是，**Qwen 3.6 系列微调社区异常活跃**，多个民间微调版本（如 HauhauCS、DavidAU、LuffyTheFox）冲入榜单前列，下载量甚至超过部分官方模型。此外，**DeepSeek-V4-Flash 系列**延续热度，两个版本合计下载超 300 万，成为本周下载量之最。量化与推理优化也成为重要赛道，unsloth、nota-ai 等团队持续输出高质量 GGUF 和 NVFP4 量化方案。

---

## 🏆 热门模型

### 🧠 语言模型（LLM、对话模型、指令微调）

| 模型 | 作者 | 点赞 | 下载 | 一句话说明 |
|------|------|------|------|-----------|
| [Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3) | moonshotai | 10,005 | 1.13M | 本周最高赞模型，月之暗面新一代多模态大模型，支持压缩张量，生态热度极高 |
| [GLM-5.2](https://huggingface.co/zai-org/GLM-5.2) | zai-org | 4,819 | 2.23M | 智谱旗舰 MoE 模型，采用 DSA 架构，下载量仅次于 DeepSeek |
| [DeepSeek-V4-Flash](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash) | deepseek-ai | 2,011 | 2.74M | 本周下载冠军，DeepSeek 新一代轻量级对话模型 |
| [DeepSeek-V4-Flash-0731](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) | deepseek-ai | 2,288 | 433K | V4-Flash 的近期更新版（0731），性能进一步优化 |
| [K-EXAONE-2.0-750B-A37B](https://huggingface.co/LGAI-EXAONE/K-EXAONE-2.0-750B-A37B) | LGAI-EXAONE | 116 | 325 | LG 最新 750B 参数 MoE 模型，激活 37B，韩语/多语能力突出 |
| [Solar-Open2-250B-Nota-NVFP4](https://huggingface.co/nota-ai/Solar-Open2-250B-Nota-NVFP4) | nota-ai | 174 | 69K | Solar Open2 的 NVFP4 量化版，面向 vLLM 优化部署 |
| [Laguna-S-2.1](https://huggingface.co/poolside/Laguna-S-2.1) | poolside | 920 | 82K | poolside 新一代代码生成 LLM，专注软件工程场景 |
| [LFM2.5-2.6B](https://huggingface.co/LiquidAI/LFM2.5-2.6B) | LiquidAI | 137 | 47K | Liquid AI 2.6B 小参数模型，适合边缘侧部署 |
| [Nanbeige4.2-3B](https://huggingface.co/Nanbeige/Nanbeige4.2-3B) | Nanbeige | 664 | 37K | 零一万物 3B 小模型，轻量级 LLM 热门选择 |
| [Qwen3.6-35B-A3B-Escha-W2](https://huggingface.co/EschaLabs/Qwen3.6-35B-A3B-Escha-W2) | EschaLabs | 191 | 2.9K | Qwen3.6 架构的 MoE 高效变体，激活参数 3B |
| [XYZ-Aquila-mini](https://huggingface.co/XYZAILab/XYZ-Aquila-mini) | XYZAILab | 404 | 1.3K | XYZAILab 发布的 Aquila 轻量版，基于 Qwen 架构 |
| [XYZ-Aquila-pro](https://huggingface.co/XYZAILab/XYZ-Aquila-pro) | XYZAILab | 358 | 1.4K | Aquila 专业版，主打 Agentic Search 能力 |

### 🎨 多模态与生成（图像、视频、音频、文本到X）

| 模型 | 作者 | 点赞 | 下载 | 一句话说明 |
|------|------|------|------|-----------|
| [MiniMax-H3](https://huggingface.co/MiniMaxAI/MiniMax-H3) | MiniMaxAI | 1,984 | 0 | MiniMax 新一代文生视频/图生视频模型，直接对标 Sora，发布即爆火 |
| [Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3) | moonshotai | 10,005 | 1.13M | 多模态 LLM，支持图像+文本输入，是本周综合热度最高的模型 |
| [Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR) | baidu | 3,880 | 2.70M | 百度通用 OCR 大模型，下载量突破 270 万，应用场景极为广泛 |
| [Mage-VL](https://huggingface.co/microsoft/Mage-VL) | microsoft | 254 | 436K | 微软多模态视觉语言模型，通用视觉理解能力出色 |
| [Qwen3-VL-32B-Ultra-Heretic-MiniMax-H3-ComfyUI-INT8-ConvRot](https://huggingface.co/ethanfel/Qwen3-VL-32B-Ultra-Heretic-MiniMax-H3-ComfyUI-INT8-ConvRot) | ethanfel | 186 | 0 | 融合 Qwen3-VL 与 MiniMax-H3 的 ComfyUI 集成版，INT8 量化 |
| [Audio8-TTS-Preview-0.6b](https://huggingface.co/Audio8/Audio8-TTS-Preview-0.6b) | Audio8 | 246 | 11K | Audio8 新 TTS 模型，基于 ArkTTS 架构，支持多语种 |
| [Inflect-Micro-v2](https://huggingface.co/owensong/Inflect-Micro-v2) | owensong | 409 | 2K | 主打 CPU/边缘设备部署的超轻量 TTS 引擎 |
| [Kroma](https://huggingface.co/lodestones/Kroma) | lodestones | 174 | 0 | 基于 Krea 2 的 LoRA 文生图模型，美术风格化能力突出 |
| [MiniMax-H3_GGUFs](https://huggingface.co/realrebelai/MiniMax-H3_GGUFs) | realrebelai | 102 | 40K | MiniMax-H3 的 GGUF 量化版，便于本地部署与 ComfyUI 集成 |

*注：MiniMax-H3 及 Kroma 下载量为 0，可能为刚发布或处于演示阶段。*

### 🔧 专用模型（代码、数学、医疗、OCR、Agent）

| 模型 | 作者 | 点赞 | 下载 | 一句话说明 |
|------|------|------|------|-----------|
| [Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR) | baidu | 3,880 | 2.70M | 百度通用 OCR 模型，覆盖文档、票据、手写等多场景文字识别 |
| [KAT-Coder-V2.5-Dev](https://huggingface.co/Kwaipilot/KAT-Coder-V2.5-Dev) | Kwaipilot | 471 | 15K | 基于 Qwen3.5 MoE 的代码生成模型，开发版持续迭代 |
| [Laguna-S-2.1](https://huggingface.co/poolside/Laguna-S-2.1) | poolside | 920 | 82K | 专注软件工程的代码生成模型，由 poolside 打造 |

### 📦 微调与量化（社区微调、GGUF、AWQ）

| 模型 | 作者 | 点赞 | 下载 | 一句话说明 |
|------|------|------|------|-----------|
| [Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive) | HauhauCS | 3,296 | 1.93M | Qwen3.6 社区微调版，主打"去审查"风格，下载量超高 |
| [Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF) | DavidAU | 1,510 | 1.63M | DavidAU 标志性"缝合"微调+GGUF，参数组合复杂但效果拔群 |
| [Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V6-GGUF](https://huggingface.co/LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V6-GGUF) | LuffyTheFox | 363 | 309K | Hermes V6 风格微调 + GGUF 量化，低门槛即可运行 |
| [Qwen3.5-9B-The-Defiant-Fable-Uncensored-Heretic-NEO-IMATRIX-MAX-MTP-GGUF](https://huggingface.co/DavidAU/Qwen3.5-9B-The-Defiant-Fable-Uncensored-Heretic-NEO-IMATRIX-MAX-MTP-GGUF) | DavidAU | 265 | 323K | 9B 小尺寸 GGUF 微调版，兼顾性能与部署成本 |
| [DeepSeek-V4-Flash-0731-GGUF](https://huggingface.co/unsloth/DeepSeek-V4-Flash-0731-GGUF) | unsloth | 466 | 112K | unsloth 官方出品 DeepSeek V4 GGUF 量化版 |
| [Kimi-K3-GGUF](https://huggingface.co/unsloth/Kimi-K3-GGUF) | unsloth | 304 | 170K | Kimi-K3 的 GGUF 量化版，供本地部署使用 |
| [MiniMax-H3](https://huggingface.co/Comfy-Org/MiniMax-H3)（Comfy-Org 版） | Comfy-Org | 592 | 2 | ComfyUI 官方适配版 MiniMax-H3，用于 ComfyUI 工作流 |
| [Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V6-GGUF](https://huggingface.co/LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V6-GGUF) | LuffyTheFox | 363 | 309K | 结合 Hermes 指令微调与 GGUF 量化，社区热门选择 |

---

## 📊 生态信号

**1. 三足鼎立格局初现：** 本周 Hugging Face 榜单清晰呈现三股势力——DeepSeek、Kimi、GLM 三大中文大模型家族形成第一梯队，其中 Kimi-K3 以超 1 万点赞断层领先，GLM-5.2 下载量突破 223 万；同时 MiniMax-H3 和微软 Mage-VL 在视频/视觉赛道上强势入场。

**2. 多模态全面渗透：** 纯文本模型不再是唯一主角，`image-text-to-text` 和 `text-to-video` 任务类型霸榜。30 个模型中约 1/3 涉及多模态能力，Kimi-K3、MiniMax-H3、Unlimited-OCR 直接承接了推理、视频生成、OCR 三大应用场景。

**3. Qwen 生态社区繁荣，微调活动高度活跃：** Qwen3.6 系列周内被社区大量二次创作——从 "Uncensored-Aggressive" 到 "Fable-Fusion" 再到 "Hermes-Genesis"，展示了开源权重模型强大的二次开发能力。值得玩味的是，这些社区微调的下载热度远超部分官方模型。

**4. 量化成为标配：** 几乎所有热门大模型都同步推出 GGUF 量化版本，unsloth 成为量化生态的中坚力量。NVFP4（NVIDIA FP4）方案也开始在 Solar-Open2 等大模型上落地，配合 vLLM 进行生产级部署。

---

## 🔬 值得探索

1. **Kimi-K3**（[链接](https://huggingface.co/moonshotai/Kimi-K3)）— 本周最值得关注的现象级模型。一周获得 1 万点赞，说明社区反馈极佳。其多模态能力 + 压缩张量特性对于构建实际应用非常值得尝试。

2. **MiniMax-H3**（[链接](https://huggingface.co/MiniMaxAI/MiniMax-H3)）— 视频生成赛道最新挑战者，支持图生视频和文生视频。虽刚发布下载量未起，但其 1,984 的点赞暗示了市场对高质量视频生成模型的强烈期待。

3. **HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive**（[链接](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)）— 非官方微调模型下载量近 200 万，远超多个官方模型。这一现象值得研究：社区微调的质量、审查策略与用户需求之间的平衡，正成为开源模型生态的重要变量。

---

> 📅 **数据统计口径：** Hugging Face Hub 热门模型榜单，按周点赞数排序，2026-08-05 快照。点赞数与下载数为该时间点的累计值。

---
*本日报由 [agents-radar](https://github.com/kky-wollu/agents-radar) 自动生成。*
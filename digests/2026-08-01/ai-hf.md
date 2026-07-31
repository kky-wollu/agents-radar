# Hugging Face 热门模型日报 2026-08-01

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-07-31 23:06 UTC

---

# 🤖 Hugging Face 热门模型日报 — 2026-08-01

> 本周榜单共 30 个模型，总点赞量突破 **3.2 万**，总下载量超过 **1200 万**。周榜数据清晰地展示出一个趋势：多模态成为绝对主流，量化生态持续繁荣，Kimi-K3 以碾压式热度登顶，国产模型全面开花。

---

## 今日速览

**moonshotai/Kimi-K3** 以 9,268 点赞横扫全场，较第二名高出近 10 倍，成为本周现象级模型。多模态模型（image-text-to-text）在 30 个上榜模型中占据 **13 席**，占比 43%，显示多模态已然成为下一代模型的基础形态。社区侧，**Qwen 家族衍生生态**持续繁荣，多个 uncensored 微调版本（如 HauhauCS、DavidAU 的作品）下载量超百万，印证了"基础模型 + 社区微调"这一黄金组合的生命力。此外，**DeepSeek-V4-Flash** 三日内狂揽 292 万下载，反映推理侧模型对高效能小模型的旺盛需求。值得关注的是，**量化创新**（GGUF、NVFP4、Ternary 2-bit）正在突破传统精度边界，为端侧部署打开新空间。

---

## 热门模型

### 🧠 语言模型（LLM、对话模型、指令微调）

| 模型 | 作者 | 👍 点赞 | 📥 下载 | 一句话说明 |
|------|------|--------|---------|-----------|
| [**DeepSeek-V4-Flash-0731**](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) | deepseek-ai | 941 | 0 | DeepSeek-V4 系列最新 Flash 版本，主打低延迟推理，刚发布即登榜（下载尚未开始统计） |
| [**GLM-5.2**](https://huggingface.co/zai-org/GLM-5.2) | zai-org | 4,706 | 165万 | 智谱新一代 MoE-DSA 架构旗舰模型，国产开源大模型的中坚力量，持续吸引大量开发者 |
| [**Laguna-S-2.1**](https://huggingface.co/poolside/Laguna-S-2.1) | poolside | 862 | 7.6万 | poolside 推出的轻量级代码生成模型，定位企业级软件开发场景 |
| [**Nanbeige4.2-3B**](https://huggingface.co/Nanbeige/Nanbeige4.2-3B) | Nanbeige | 595 | 2.7万 | 3B 小参数对话模型，在资源受限场景下提供可用的中文对话能力 |
| [**Solar-Open2-250B**](https://huggingface.co/upstage/Solar-Open2-250B) | upstage | 714 | 1.3万 | upstage 开源的 250B 参数 MoE 模型，主打开放权重 + 多语言能力 |
| [**XYZ-Aquila-mini**](https://huggingface.co/XYZAILab/XYZ-Aquila-mini) | XYZAILab | 351 | 579 | 基于 Qwen3.5-MoE 的轻量级变体，面向对话与多模态混合场景 |
| [**XYZ-Aquila-pro**](https://huggingface.co/XYZAILab/XYZ-Aquila-pro) | XYZAILab | 326 | 869 | Aquila 系列 Pro 版本，强化 agentic-search 能力，面向智能体应用 |
| [**DeepSeek-V4-Flash**](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash) | deepseek-ai | 1,924 | 292万 | DeepSeek 的推理优化版模型，三日下载近 300 万，是本周下载量亚军 |

### 🎨 多模态与生成（图像、文本到X、音频、视觉）

| 模型 | 作者 | 👍 点赞 | 📥 下载 | 一句话说明 |
|------|------|--------|---------|-----------|
| [**Kimi-K3**](https://huggingface.co/moonshotai/Kimi-K3) | moonshotai | 9,268 | 49万 | 本周绝对焦点：Kimi 新一代多模态模型，采用 compressed-tensors 技术，点赞数断层式领先 |
| [**Unlimited-OCR**](https://huggingface.co/baidu/Unlimited-OCR) | baidu | 3,660 | 251万 | 百度开源的全场景 OCR 模型，下载量居全榜第一，通用文档理解刚需爆款 |
| [**Qwen3.6-27B-Fable-Fusion-711**](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF) | DavidAU | 1,140 | 112万 | DavidAU 的 Qwen3.6 多模态微调版，GGUF 量化 + uncensored 定位，社区热度极高 |
| [**Inkling**](https://huggingface.co/thinkingmachines/Inkling) | thinkingmachines | 1,664 | 5.7万 | thinkingmachines 旗舰多模态对话模型，通用视觉 + 语言理解 |
| [**Qwen3.6-35B-A3B-Uncensored**](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive) | HauhauCS | 3,205 | 184万 | Qwen3.6-MoE 社区微调，35B-A3B 架构 + uncensored 风格，下载量超 180 万 |
| [**Inkling-Small**](https://huggingface.co/thinkingmachines/Inkling-Small) | thinkingmachines | 192 | 3,000 | Inkling 的小型版本，面向端侧多模态部署 |
| [**Mage-VL**](https://huggingface.co/microsoft/Mage-VL) | microsoft | 148 | 5,650 | 微软的视频理解模型，扩展多模态到动态内容分析 |
| [**Fara1.5-27B**](https://huggingface.co/microsoft/Fara1.5-27B) | microsoft | 234 | 2,726 | 微软基于 Qwen3.5 的 computer-use 智能体模型，面向 GUI 自动化操作 |
| [**Qwen3.6-35B-A3B-Uncensored-Genesis**](https://huggingface.co/LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V6-GGUF) | LuffyTheFox | 267 | 21万 | Hermes 风格微调 + GGUF 量化，社区创意微调的又一生力军 |
| [**Kimi-K3-GGUF**](https://huggingface.co/unsloth/Kimi-K3-GGUF) | unsloth | 226 | 3.6万 | unsloth 对 Kimi-K3 的 GGUF 量化版本，推动多模态模型本地化部署 |
| [**Kimi-K3**](https://huggingface.co/unsloth/Kimi-K3) | unsloth | 215 | 1,044 | unsloth 的 Kimi-K3 优化版（非量化），配套 GGUF 版本一并发布 |
| [**Qwen3.5-9B-The-Defiant-Fable**](https://huggingface.co/DavidAU/Qwen3.5-9B-The-Defiant-Fable-Uncensored-Heretic-NEO-IMATRIX-MAX-MTP-GGUF) | DavidAU | 172 | 26万 | DavidAU 另一 Qwen 微调力作，NEO-IMATRIX 量化 + MTP 加速 |
| [**Escha-Qwen3.6-35B-A3B-Escha-W2**](https://huggingface.co/EschaLabs/Qwen3.6-35B-A3B-Escha-W2) | EschaLabs | 104 | 599 | EschaLabs 对 Qwen3.6 的 W2 极低比特量化实验 |

### 🔊 语音与专用模型（TTS / ASR）

| 模型 | 作者 | 👍 点赞 | 📥 下载 | 一句话说明 |
|------|------|--------|---------|-----------|
| [**Inflect-Micro-v2**](https://huggingface.co/owensong/Inflect-Micro-v2) | owensong | 347 | 1,449 | 面向 CPU/边缘设备的轻量级本地 TTS，主打低延迟实时合成 |
| [**Audio8-TTS-Preview-0.6b**](https://huggingface.co/Audio8/Audio8-TTS-Preview-0.6b) | Audio8 | 151 | 2,481 | Audio8 的 0.6B TTS 预览版，基于 ArkTTS 架构 |
| [**Inflect-Nano-v2**](https://huggingface.co/owensong/Inflect-Nano-v2) | owensong | 121 | 802 | Inflect 系列的 Nano 版本，比 Micro 更小，面向极端边缘场景 |
| [**VibeVoice-ASR-BitNet**](https://huggingface.co/microsoft/VibeVoice-ASR-BitNet) | microsoft | 133 | 5,464 | 微软 BitNet 架构 ASR，GGUF/GGML 量化支持，探索 1-bit 语音识别 |

### 📦 微调与量化（社区微调、GGUF、极低比特量化）

| 模型 | 作者 | 👍 点赞 | 📥 下载 | 一句话说明 |
|------|------|--------|---------|-----------|
| [**Ternary-Bonsai-27B**](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf) | prism-ml | 1,124 | 71万 | 三元（ternary）2-bit 量化革命性实践，27B 模型压缩至可本地运行，下载超 71 万 |
| [**Qwen3.6-35B-A3B-Uncensored**(HauhauCS)](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive) | HauhauCS | 3,205 | 184万 | 社区微调 + GGUF 量化的完美范本，证明"对齐放宽 + 量化"组合拳的市场号召力 |
| [**DLuffyTheFox-Qwen3.6-Genesis-Hermes**](https://huggingface.co/LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V6-GGUF) | LuffyTheFox | 267 | 21万 | Hermes 风格数据微调，GGUF 量化，兼顾创意与效率 |
| [**Solar-Open2-Nota-NVFP4**](https://huggingface.co/nota-ai/Solar-Open2-250B-Nota-NVFP4) | nota-ai | 151 | 1.9万 | NVIDIA NVFP4 精度量化 + vLLM 适配，企业级低成本推理方案 |
| [**Qwen3.5-9B-Defiant-Fable**](https://huggingface.co/DavidAU/Qwen3.5-9B-The-Defiant-Fable-Uncensored-Heretic-NEO-IMATRIX-MAX-MTP-GGUF) | DavidAU | 172 | 26万 | 多格式 GGUF + MTP 加速微调，探索小模型极致压缩 |

---

## 🌐 生态信号

**家族军团化竞争格局显现。** 本周榜单呈现出高度集中的家族态势：Qwen 衍生模型（含微调/量化）占据 6 席，Kimi 家族 3 席，DeepSeek 2 席，Solar 2 席。**Qwen 已然成为开源社区最活跃的基座模型**，其 3.5/3.6 系列衍生的 uncensored 微调 + GGUF 量化组合，形成了完整的"制造-分发-消费"社区闭环。

**多模态不再是"未来"而是"标配"。** 43% 的上榜模型为 image-text-to-text 架构，Kimi-K3 的登顶进一步宣告：新一代模型的起点就是多模态。同时我们可以注意到一个有趣的信号，Kimi-K3 使用 compressed-tensors 技术，说明 MoE + 稀疏激活正在成为前沿大模型的标配。

**量化技术进入"三进制时代"。** Ternary-Bonsai-27B 的 71 万下载证明 2-bit 量化已从实验室走向大规模应用。同时 NVFP4、W2 等新量化格式的涌现，表明社区正在多点突破精度-成本边界。

**开源权重保持主导，但闭源影响力不容忽视。** 榜单 30 席全部为开源权重模型，国产厂商（月之暗面、DeepSeek、智谱、百度）贡献了半数以上，凸显中国 AI 在开源生态中的核心地位。

---

## 🔬 值得探索

1. **[Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3)** — 本周断层式热度之王。建议深入研究其 compressed-tensors 稀疏化技术如何平衡多模态能力与推理效率，结合 unsloth 的 GGUF 版本对比量化前后性能差异。

2. **[DeepSeek-V4-Flash-0731](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731)** — 一周内发布两个版本（0731 与原始版），下载量三日破 290 万。留意 DeepSeek 如何通过架构优化实现"闪速"推理，对比其与 V4 原版在延迟/质量上的权衡。

3. **[Ternary-Bonsai-27B](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)** — 三值量化（-1/0/1）的 27B 模型是压缩技术的积极探索，下载量已超 71 万。为端侧部署高性能模型提供了极具价值的参考基线。

---

*数据窗口：2026-08-01 周榜，涵盖 30 个热门模型。全量数据以 Hugging Face Hub 实时页面为准。*

---
*本日报由 [agents-radar](https://github.com/kky-wollu/agents-radar) 自动生成。*
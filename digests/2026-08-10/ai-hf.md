# Hugging Face 热门模型日报 2026-08-10

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-08-09 22:35 UTC

---

# 🤖 Hugging Face 热门模型日报 — 2026-08-10

---

## 📰 今日速览

今日 Hugging Face 榜单呈现明显的“多模态+视频生成”主导格局：MiniMaxAI 的 **MiniMax-H3** 以 3,236 周点赞登顶视频生成赛道，且围绕其衍生出大量 ComfyUI 工作流、GGUF 量化与 LoRA 微调生态（多个衍生模型合计下载超 500 万）。语言模型方面，**GLM-5.2**（4,913 赞）、**DeepSeek-V4-Flash-0731**（2,939 赞）与 **Kimi-K3**（10,395 赞）形成“三国鼎立”态势。特别值得注意的是，本周榜单中出现了多款以 “Heretic/Uncensored” 为标签的社区微调模型（如 Qwen3.6-27B 系），反映出开放权重模型在越狱/去审查方向的活跃生态。此外，**FLUX.1-dev** 以 14,057 赞继续稳坐图像生成榜首，而 **baidu/Unlimited-OCR** 以 3,985 赞成为本周最亮眼的专用模型。

---

## 🏆 热门模型

### 🧠 语言模型

| 模型 | 作者 | 点赞 | 下载 | 说明 |
|------|------|------|------|------|
| [**GLM-5.2**](https://huggingface.co/zai-org/GLM-5.2) | zai-org | 4,913 | 248.8万 | 智谱新一代 MoE 大模型，采用 GLM_MoE_DSA 架构，对话能力与推理表现双强，成为本周最受关注的国产开源 LLM。 |
| [**DeepSeek-V4-Flash-0731**](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) | deepseek-ai | 2,939 | 86.9万 | 深度求索 V4 系列的 Flash 版本，主打快速推理与低延迟，下载量断层领先同类模型。 |
| [**Kimi-K3**](https://huggingface.co/moonshotai/Kimi-K3) | moonshotai | 10,395 | 145.6万 | 月之暗面新一代多模态 LLM（image-text-to-text），采用压缩张量技术，点赞数碾压同期竞品。 |
| [**LFM2.5-2.6B**](https://huggingface.co/LiquidAI/LFM2.5-2.6B) | LiquidAI | 448 | 8.6万 | Liquid AI 的 2.6B 小参数高效语言模型，主打低成本部署。 |
| [**maple-preview**](https://huggingface.co/deepgrove/maple-preview) | deepgrove | 287 | 1,089 | DeepGrove 的 MoE 架构文本生成模型（预览版），暂未大规模铺开。 |
| [**Ling-3.0-flash**](https://huggingface.co/inclusionAI/Ling-3.0-flash) | inclusionAI | 244 | 4,747 | 零一万物系团队的新一代对话模型，采用 hybrid 架构。 |

---

### 🎨 多模态与生成

| 模型 | 作者 | 点赞 | 下载 | 说明 |
|------|------|------|------|------|
| [**MiniMaxAI/MiniMax-H3**](https://huggingface.co/MiniMaxAI/MiniMax-H3) | MiniMaxAI | 3,236 | 3.5万 | 今日视频生成赛道顶流，支持图像+文本→视频，同时兼容文本/图像到视频双向生成。 |
| [**FLUX.1-dev**](https://huggingface.co/black-forest-labs/FLUX.1-dev) | black-forest-labs | 14,057 | 48.7万 | 黑森林实验室的开源图像生成模型，持续霸榜，本周点赞数依旧全榜第一。 |
| [**NVIDIA-NemotronLabs-VoiceChat-11B**](https://huggingface.co/nvidia/NVIDIA-NemotronLabs-VoiceChat-11B) | nvidia | 260 | 543 | 英伟达语音对话模型，整合多篇语音交互相关论文成果，面向实时语音场景。 |
| [**Audio8-TTS-Preview-0.6b**](https://huggingface.co/Audio8/Audio8-TTS-Preview-0.6b) | Audio8 | 332 | 1.3万 | 基于 ArkTTS 的轻量级语音合成模型，0.6B 参数主打高效 TTS。 |
| [**Minimax-h3-Turbo**](https://huggingface.co/lightx2v/Minimax-h3-Turbo) | lightx2v | 233 | 6,117 | MiniMax-H3 的 Turbo 加速版本，专注于 i2v（图像到视频）快速生成。 |

---

### 🔧 专用模型

| 模型 | 作者 | 点赞 | 下载 | 说明 |
|------|------|------|------|------|
| [**baidu/Unlimited-OCR**](https://huggingface.co/baidu/Unlimited-OCR) | baidu | 3,985 | 288.9万 | 百度推出的高精度 OCR 模型，不限场景/语言/版式，一周内下载近 300 万，企业级应用潜力巨大。 |
| [**KAT-Coder-V2.5-Dev**](https://huggingface.co/Kwaipilot/KAT-Coder-V2.5-Dev) | Kwaipilot | 552 | 1.9万 | 基于 Qwen3.5-MoE 的代码生成模型，面向开发场景。 |
| [**Shieldstral-1.0-3B**](https://huggingface.co/mistralai/Shieldstral-1.0-3B) | mistralai | 211 | 5,651 | Mistral 的安全/内容审核专用模型，3B 参数支持 vLLM 部署。 |

---

### 📦 微调与量化

| 模型 | 作者 | 点赞 | 下载 | 说明 |
|------|------|------|------|------|
| [**Comfy-Org/MiniMax-H3**](https://huggingface.co/Comfy-Org/MiniMax-H3) | Comfy-Org | 1,069 | 494.8万 | MiniMax-H3 的 ComfyUI 适配版，单文件格式，下载近 500 万，是视频生成社区的核心枢纽。 |
| [**DeepSeek-V4-Flash-0731-GGUF**](https://huggingface.co/unsloth/DeepSeek-V4-Flash-0731-GGUF) | unsloth | 627 | 18.9万 | Unsloth 出品的 DeepSeek-V4 GGUF 量化版，便于本地部署。 |
| [**Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF**](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF) | DavidAU | 1,804 | 239.1万 | 社区“缝合怪”式微调模型，基于 Qwen3.6 融合多风格并去审查，GGUF 格式方便本地运行。 |
| [**Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V7-GGUF**](https://huggingface.co/LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V7-GGUF) | LuffyTheFox | 454 | 39.6万 | Qwen3.6 MoE 架构的 Hermes 风格去审查 GGUF 版本。 |
| [**Minimax-H3-nvfp4-INT4-INT8-Convrot**](https://huggingface.co/Abiray/Minimax-H3-nvfp4-INT4-INT8-Convrot) | Abiray | 155 | 51.1万 | MiniMax-H3 混合精度量化版（NVFP4+INT4/INT8），适配消费级显卡推理。 |
| [**MiniMax-H3-Turbo-Lora**](https://huggingface.co/larryvrh/MiniMax-H3-Turbo-Lora) | larryvrh | 543 | 0 | MiniMax-H3 的 LoRA 微调适配器，兼作文生视频与音频。 |
| [**MiniMax-H3_GGUFs**](https://huggingface.co/realrebelai/MiniMax-H3_GGUFs) | realrebelai | 187 | 16.1万 | MiniMax-H3 社区 GGUF 量化集合。 |
| [**LFM2.5-2.6B-GGUF**](https://huggingface.co/LiquidAI/LFM2.5-2.6B-GGUF) | LiquidAI | 173 | 6.8万 | LiquidAI 官方 GGUF 版本，支持 llama.cpp 本地运行。 |

---

## 📡 生态信号

- **MiniMax-H3 生态“虹吸效应”显著**：围绕 MiniMax-H3 已衍生出 ComfyUI 适配、GGUF 量化（realrebelai）、混合精度量化（Abiray）、LoRA 微调、Turbo 加速等多层次生态，单模型衍生品合计下载超 600 万，构成完整的视频生成开源生态闭环，这一现象此前仅见于 SD/FLUX 等图像生成模型。

- **中国开源模型唱主角**：GLM、DeepSeek、Kimi、MiniMax、百度、零一万物（Ling）等国产模型霸榜，在语言、视频、OCR 等多条赛道上均占据头部位置，开源权重趋势不可逆。

- **“去审查/Uncensored”微调成为社区狂欢**：多款以 Qwen3.6 为基座的 Heretic/Uncensored 微调模型上榜，表明开放权重模型在安全对齐与“解放”之间的张力持续存在，社区需求旺盛。

- **量化与本地部署工具链成熟**：Unsloth、GGUF、NVFP4 等量化方案覆盖 LLM 与视频模型，4-bit/8-bit 精度成为主流，有效拉低了本地部署门槛。

---

## 🔭 值得探索

1. **[MiniMax-H3](https://huggingface.co/MiniMaxAI/MiniMax-H3) + [Comfy-Org 生态](https://huggingface.co/Comfy-Org/MiniMax-H3)** — 视频生成领域的新“爆款”，建议从 Comfy-Org 的 ready-to-use 版本入手，搭配 GGUF 量化在本地体验完整工作流。

2. **[Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3)** — 点赞 10k+ 的“隐形冠军”，其压缩张量技术（compressed-tensors）值得深入研究，尤其适合对多模态推理效率感兴趣的开发者。

3. **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** — 下载近 300 万次的实用性王者，不限格式/语言的 OCR 能力可快速落地到文档处理、票据识别等真实业务场景。

---

*本报告基于 2026-08-10 Hugging Face Hub 热门模型榜单（前 30 名）自动生成。*

---
*本日报由 [agents-radar](https://github.com/kky-wollu/agents-radar) 自动生成。*
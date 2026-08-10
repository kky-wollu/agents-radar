# Hugging Face 热门模型日报 2026-08-11

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-08-10 22:42 UTC

---

# 🤖 Hugging Face 热门模型日报 — 2026-08-11

---

## 📌 今日速览

今日 Hugging Face 趋势榜被 **MiniMax-H3 视频生成生态** 强势霸榜，官方权重、ComfyUI 适配、Turbo/LoRA 变体及量化版本合计占据 10+ 席位，社区围绕该模型的微调与部署工具链已全面铺开。语言模型方面，**DeepSeek-V4-Flash-0731** 以 95 万+ 下载量领跑文本生成赛道，GGUF 量化版亦同步上榜；**Kimi-K3** 和 **FLUX.1-dev** 分别以 1 万+ 周点赞稳居多模态与图像生成头部。值得关注的是，**Muse-Glimmer-30B**（Meta）与 **BigBang-v1** 等新架构模型开始出现，但首周下载量普遍为 0，仍处于早期社区验证阶段。此外，NVIDIA、Mistral 等大厂在语音、安全对齐等垂直方向亦有布局。

---

## 🏆 热门模型

### 🧠 语言模型（LLM / 对话 / 指令微调）

| 模型 | 作者 | 👍 点赞 | 📥 下载 | 一句话说明 |
|---|---|---|---|---|
| [**DeepSeek-V4-Flash-0731**](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) | deepseek-ai | 3,047 | 954,441 | DeepSeek V4 Flash 版本，以近百万下载量领跑今日榜单，主打高效对话生成。 |
| [**Kimi-K3**](https://huggingface.co/moonshotai/Kimi-K3) | moonshotai | 10,468 | 1,510,032 | 月之暗面 Kimi 系列新一代多模态模型，1 万+ 周点赞登顶总榜，采用压缩张量技术。 |
| [**LFM2.5-2.6B**](https://huggingface.co/LiquidAI/LFM2.5-2.6B) | LiquidAI | 488 | 89,680 | Liquid AI 的液体基础模型 2.5 代，2.6B 小参数主打高效推理，含 GGUF 版同榜。 |
| [**deepgrove/maple-preview**](https://huggingface.co/deepgrove/maple-preview) | deepgrove | 309 | 1,344 | 预览版 MoE 因果语言模型，新团队入场，值得关注后续发展。 |
| [**inclusionAI/Ling-3.0-flash**](https://huggingface.co/inclusionAI/Ling-3.0-flash) | inclusionAI | 287 | 5,261 | Ling 系列 Flash 版本，采用 bailing_hybrid 架构的对话模型。 |

### 🎨 多模态与生成（图像 / 视频 / 音频 / 文本到X）

| 模型 | 作者 | 👍 点赞 | 📥 下载 | 一句话说明 |
|---|---|---|---|---|
| [**MiniMaxAI/MiniMax-H3**](https://huggingface.co/MiniMaxAI/MiniMax-H3) | MiniMaxAI | 3,420 | 47,468 | MiniMax 新一代图生视频/文生视频模型，今日最大热点，带动整个生态爆发。 |
| [**Comfy-Org/MiniMax-H3**](https://huggingface.co/Comfy-Org/MiniMax-H3) | Comfy-Org | 1,142 | 6,009,639 | ComfyUI 官方适配版，600 万+ 下载，是社区使用 H3 的核心入口。 |
| [**lightx2v/Minimax-h3-Turbo**](https://huggingface.co/lightx2v/Minimax-h3-Turbo) | lightx2v | 259 | 15,087 | H3 Turbo 加速版，支持图生视频/文生视频/区域生视频。 |
| [**larryvrh/MiniMax-H3-Turbo-Lora**](https://huggingface.co/larryvrh/MiniMax-H3-Turbo-Lora) | larryvrh | 596 | 0 | H3 Turbo 的 LoRA 微调适配器，支持文本/音频到视频。 |
| [**Meta-Models/Muse-Glimmer-30B**](https://huggingface.co/meta-models/Muse-Glimmer-30B) | meta-models | 671 | 0 | Meta 视觉语言模型新作，30B 参数，刚发布处于早期测试阶段。 |
| [**black-forest-labs/FLUX.1-dev**](https://huggingface.co/black-forest-labs/FLUX.1-dev) | black-forest-labs | 14,076 | 480,762 | FLUX.1 开发版，今日最高赞模型，文本到图像生成的标杆。 |
| [**baidu/Unlimited-OCR**](https://huggingface.co/baidu/Unlimited-OCR) | baidu | 4,001 | 2,921,751 | 百度通用 OCR 模型，290 万+ 下载，图像到文本的实用工具。 |
| [**Abiray/Minimax-H3-nvfp4-INT4-INT8-Convrot**](https://huggingface.co/Abiray/Minimax-H3-nvfp4-INT4-INT8-Convrot) | Abiray | 162 | 530,052 | H3 的混合精度量化版（NVFP4/INT4/INT8），探索视频模型压缩。 |

### 🔧 专用模型（安全 / 语音 / 其他）

| 模型 | 作者 | 👍 点赞 | 📥 下载 | 一句话说明 |
|---|---|---|---|---|
| [**NVIDIA-NemotronLabs-VoiceChat-11B**](https://huggingface.co/nvidia/NVIDIA-NemotronLabs-VoiceChat-11B) | nvidia | 295 | 597 | NVIDIA 语音对话模型，11B 参数，聚焦实时语音交互场景。 |
| [**mistralai/Shieldstral-1.0-3B**](https://huggingface.co/mistralai/Shieldstral-1.0-3B) | mistralai | 221 | 6,343 | Mistral 安全对齐模型，3B 小参，基于 Mistral3 架构的审核/护栏工具。 |

### 📦 微调与量化（社区微调 / GGUF / 量化）

| 模型 | 作者 | 👍 点赞 | 📥 下载 | 一句话说明 |
|---|---|---|---|---|
| [**DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF**](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF) | DavidAU | 1,857 | 2,439,083 | Qwen3.6 社区微调融合版（Uncensored 风格），GGUF 格式，240 万+ 下载。 |
| [**unsloth/DeepSeek-V4-Flash-0731-GGUF**](https://huggingface.co/unsloth/DeepSeek-V4-Flash-0731-GGUF) | unsloth | 636 | 199,167 | Unsloth 出品的 DeepSeek V4 GGUF 量化版，推动本地部署。 |
| [**realrebelai/MiniMax-H3_GGUFs**](https://huggingface.co/realrebelai/MiniMax-H3_GGUFs) | realrebelai | 192 | 174,862 | H3 视频模型的 GGUF 量化版，适配 ComfyUI 生态。 |
| [**LiquidAI/LFM2.5-2.6B-GGUF**](https://huggingface.co/LiquidAI/LFM2.5-2.6B-GGUF) | LiquidAI | 183 | 89,611 | 官方同步发布的 GGUF 版，llama.cpp 友好。 |
| [**unsloth/Muse-Glimmer-30B-GGUF**](https://huggingface.co/unsloth/Muse-Glimmer-30B-GGUF) | unsloth | 195 | 0 | Muse-Glimmer 的 GGUF 量化版，降低本地部署门槛。 |
| [**sakamakismile/Qwen3-VL-32B-Heretic-MiniMax-H3-NVFP4**](https://huggingface.co/sakamakismile/Qwen3-VL-32B-Heretic-MiniMax-H3-NVFP4) | sakamakismile | 151 | 0 | 将 Qwen3-VL 作为 H3 的文本编码器，NVFP4 量化，社区混搭创新。 |
| [**SyzygyResearch/Mach-1-Additive-35B**](https://huggingface.co/SyzygyResearch/Mach-1-Additive-35B) | SyzygyResearch | 114 | 2,129 | 基于 Qwen3.5-MoE 的三元加法实验模型，新架构探索。 |
| [**SexGod1979/PinkCherry_MiniMax-H3**](https://huggingface.co/SexGod1979/PinkCherry_MiniMax-H3) | SexGod1979 | 248 | 0 | H3 社区微调风格版（NSFW 向），Apache-2.0 许可。 |
| [**lightx2v/MiniMax-H3-Prompt-Rewriter-LoRA**](https://huggingface.co/lightx2v/MiniMax-H3-Prompt-Rewriter-LoRA) | lightx2v | 116 | 268 | H3 专用 Prompt 重写 LoRA，提升提示词质量。 |
| [**endless-frontier/BigBang-v1**](https://huggingface.co/endless-frontier/BigBang-v1) | endless-frontier | 150 | 617 | 基于 Qwen3.5-MoE 的新多模态模型，社区早期验证中。 |
| [**Kijai/MiniMax-H3_comfy**](https://huggingface.co/Kijai/MiniMax-H3_comfy) | Kijai | 256 | 0 | Kijai 的 H3 ComfyUI 适配版，资深 ComfyUI 开发者出品。 |
| [**Kijai/MiniMax-H3-experimental**](https://huggingface.co/Kijai/MiniMax-H3-experimental) | Kijai | 183 | 0 | H3 实验性版本，探索新功能边界。 |
| [**drbaph/MiniMax-H3-Turbo-Lora-ComfyUI**](https://huggingface.co/drbaph/MiniMax-H3-Turbo-Lora-ComfyUI) | drbaph | 250 | 0 | H3 Turbo LoRA 的 ComfyUI 剪枝版，优化推理。 |
| [**ethanfel/Qwen3-VL-32B-Ultra-Heretic-H3-ComfyUI-INT8-ConvRot**](https://huggingface.co/ethanfel/Qwen3-VL-32B-Ultra-Heretic-H3-ComfyUI-INT8-ConvRot) | ethanfel | 439 | 0 | 混搭 Qwen3-VL 编码器 + INT8 量化的 H3 工作流版。 |
| [**meta-models/Muse-Glimmer-30B-GGUF**](https://huggingface.co/meta-models/Muse-Glimmer-30B-GGUF) | meta-models | 137 | 0 | Meta 官方 GGUF 版，加速 30B 模型本地部署。 |

---

## 🔍 生态信号

**MiniMax-H3 无疑是今日绝对主角**，其生态之完整令人瞩目：官方权重（3,420👍）→ ComfyUI 适配（600 万+下载）→ Turbo 加速 → LoRA 微调 → GGUF/混合精度量化，全链路社区工具已在 24 小时内迅速补齐。这标志着视频生成正在复制 LLM 的“大模型+量化+微调”生态范式。**DeepSeek-V4 与 Kimi-K3** 形成双雄格局，前者以高性能 Flash 版本吸引开发者（95 万下载），后者凭 10K+ 点赞证明多模态模型的传播力。**开源权重生态持续繁荣**，包括 Meta（Muse-Glimmer）、MiniMax、DeepSeek、Qwen 系（3.6/3.5-MoE）多线并进。量化侧，GGUF 已从 LLM 向视频模型（H3-GGUF）蔓延，**4-bit 以下视频模型量化是前沿探索方向**；社区“缝合怪”微调（Uncensored × ComfyUI × 多量化格式混搭）长尾效应明显，但质量参差，约有三分之一上榜模型下载量为 0，尚待时间检验。

---

## 🧪 值得探索

1. **[MiniMaxAI/MiniMax-H3](https://huggingface.co/MiniMaxAI/MiniMax-H3)** — 今日生态爆发核心，值得围绕其 Turbo/LoRA/量化分支深入测试，评估视频生成能力新上限。

2. **[moonshotai/Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3)** — 1 万+ 周点赞全榜第一，压缩张量技术值得研究，150 万下载验证了实用性，值得试用其多模态能力。

3. **[SyzygyResearch/Mach-1-Additive-35B](https://huggingface.co/SyzygyResearch/Mach-1-Additive-35B)** — “三元加法”架构 + Qwen3.5-MoE 底座，属于前沿架构探索，适合研究者密切关注其性能报告。

---
*本日报由 [agents-radar](https://github.com/kky-wollu/agents-radar) 自动生成。*
# Hugging Face 热门模型日报 2026-08-15

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-08-14 22:28 UTC

---

# 🤖 Hugging Face 热门模型日报 — 2026-08-15

## 📌 今日速览

本周 Hugging Face 榜单被 **Qwen3.8**、**DeepSeek-V4** 和 **MiniMax-H3** 三大势力主导。**moonshotai/Kimi-K3** 以 10,666 周点赞登顶榜首，成为最大黑马；Qwen3.8-27B 凭借 8,869 点赞紧随其后，其 MoE 变体 Qwen3.8-2.4T-A95B 也已上线。视频生成赛道热度持续飙升，**MiniMax-H3** 系列占据榜单近 1/3 席位，衍生出大量社区 LoRA 与 ComfyUI 生态适配。此外，NVIDIA Nemotron-3.5 Lightning 系列与 LiquidAI LFM2.5 等高效架构模型值得关注。

---

## 🏆 热门模型

### 🧠 语言模型（LLM、对话模型、指令微调）

| 模型 | 作者 | 点赞 | 下载 | 一句话说明 |
|------|------|------|------|-----------|
| [**Kimi-K3**](https://huggingface.co/moonshotai/Kimi-K3) | moonshotai | 10,666 | 197.5万 | 本周点赞之王，多模态大模型，最大亮点是采用**压缩张量**技术，推理效率大幅提升 |
| [**Qwen3.8-2.4T-A95B**](https://huggingface.co/Qwen/Qwen3.8-2.4T-A95B) | Qwen | 909 | 3,832 | 2.4T 参数 MoE 架构（激活 95B），Qwen3.8 的旗舰级文本生成变体 |
| [**DeepSeek-V4-Pro-0813**](https://huggingface.co/deepseek-ai/DeepSeek-V4-Pro-0813) | deepseek-ai | 429 | 245 | V4 Pro 最新迭代版本，性能进一步优化，当前下载量较小，潜力未被充分发掘 |
| [**NVIDIA-Nemotron-3.5-Lightning-30B-A3B-NVFP4**](https://huggingface.co/nvidia/NVIDIA-Nemotron-3.5-Lightning-30B-A3B-NVFP4) | nvidia | 257 | 11.96万 | 30B 总参数、3B 激活的 MoE 架构，采用 NVFP4 精度，主打高效推理 |
| [**NVIDIA-Nemotron-3.5-Lightning-30B-A3B-BF16**](https://huggingface.co/nvidia/NVIDIA-Nemotron-3.5-Lightning-30B-A3B-BF16) | nvidia | 141 | 3.41万 | 与上一模型同源，BF16 全精度版本，适合对精度要求更高的场景 |
| [**LFM2.5-2.6B**](https://huggingface.co/LiquidAI/LFM2.5-2.6B) | LiquidAI | 614 | 12.42万 | **液体神经网络**架构的 2.6B 模型，以极小参数量实现出色推理性能 |
| [**dots3-note-prev**](https://huggingface.co/dots-studio/dots3-note-prev) | dots-studio | 134 | 11 | 新兴多模态对话模型预览版，规模较小但值得跟踪 |

### 🎨 多模态与生成（图像、视频、音频、文本到X）

| 模型 | 作者 | 点赞 | 下载 | 一句话说明 |
|------|------|------|------|-----------|
| [**Qwen3.8-27B**](https://huggingface.co/Qwen/Qwen3.8-27B) | Qwen | 8,869 | 2 | Qwen3.8 系列主力多模态模型，支持图像+文本输入，下载数据尚未传导 |
| [**Muse-Glimmer-30B**](https://huggingface.co/meta-models/Muse-Glimmer-30B) | meta-models | 1,507 | 16.53万 | Meta 系多模态模型，在图像-文本-对话场景表现亮眼 |
| [**MiniMax-H3**](https://huggingface.co/MiniMaxAI/MiniMax-H3) | MiniMaxAI | 3,916 | 199.75万 | **视频生成赛道王者**，支持文生视频和图生视频，下载量近 200 万 |
| [**MiniMax-Music3**](https://huggingface.co/MiniMaxAI/MiniMax-Music3) | MiniMaxAI | 645 | 63 | 文本生成音乐的最新模型，MiniMax 生态向音频领域延伸 |
| [**DeepSeek-V4-Flash-0731**](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) | deepseek-ai | 3,378 | 160.65万 | V4 系列轻量快速版，下载量巨大，适合高并发场景 |
| [**Minimax-h3-Turbo**](https://huggingface.co/lightx2v/Minimax-h3-Turbo) | lightx2v | 493 | 14.99万 | H3 的 **Turbo 加速版**，由社区 lightx2v 提供，主打更快推理 |
| [**MiniMax-H3-Turbo-Lora**](https://huggingface.co/larryvrh/MiniMax-H3-Turbo-Lora) | larryvrh | 741 | 0 | H3 Turbo 的 LoRA 微调版本，刚发布下载量尚未累积 |
| [**MiniMax-H3-Turbo-Lora-ComfyUI**](https://huggingface.co/drbaph/MiniMax-H3-Turbo-Lora-ComfyUI) | drbaph | 318 | 11.30万 | 专为 ComfyUI 工作流优化的 H3 Turbo LoRA |
| [**PinkCherry_MiniMax-H3**](https://huggingface.co/SexGod1979/PinkCherry_MiniMax-H3) | SexGod1979 | 309 | 473 | H3 社区微调风格化版本，标注 Apache-2.0 |
| [**MiniMax-H3-Realism-People-LoRA**](https://huggingface.co/fal/MiniMax-H3-Realism-People-LoRA) | fal | 174 | 9,060 | 聚焦**人物写实**渲染的 H3 LoRA，由 fal.ai 团队发布 |
| [**LTX-2.5**](https://huggingface.co/Lightricks/LTX-2.5) | Lightricks | 847 | 20.78万 | 全功能视频模型，支持图生视频/文生视频/视频转视频 |
| [**Anima-2.9B**](https://huggingface.co/Gazingstars123/Anima-2.9B) | Gazingstars123 | 158 | 10,106 | 文生图单文件模型，ComfyUI 适配 |

### 🔧 专用模型（代码、数学、医疗、嵌入、语音）

| 模型 | 作者 | 点赞 | 下载 | 一句话说明 |
|------|------|------|------|-----------|
| [**NVIDIA-NemotronLabs-VoiceChat-11B**](https://huggingface.co/nvidia/NVIDIA-NemotronLabs-VoiceChat-11B) | nvidia | 380 | 1,366 | 语音对话专用模型，NVIDIA Labs 出品，结合 ASR+TTS+LLM 能力 |
| [**Ling-3.0-tiny**](https://huggingface.co/inclusionAI/Ling-3.0-tiny) | inclusionAI | 232 | 2,283 | 混合架构（bailing_hybrid）小型模型，MIT 协议，主打低成本部署 |

### 📦 微调与量化（社区微调、GGUF、AWQ）

| 模型 | 作者 | 点赞 | 下载 | 一句话说明 |
|------|------|------|------|-----------|
| [**Qwen3.8-27B-GGUF**](https://huggingface.co/unsloth/Qwen3.8-27B-GGUF) | unsloth | 734 | 0 | Qwen3.8-27B 官方量化版，unsloth 出品，刚发布下载尚未累积 |
| [**Muse-Glimmer-30B-GGUF**](https://huggingface.co/unsloth/Muse-Glimmer-30B-GGUF) | unsloth | 414 | 59.68万 | Muse-Glimmer-30B 的高质量 GGUF 量化版本 |
| [**Muse-Glimmer-30B-GGUF**](https://huggingface.co/meta-models/Muse-Glimmer-30B-GGUF) | meta-models | 268 | 22.84万 | 官方版 Muse-Glimmer-30B GGUF 量化版本 |
| [**Fable-Fusion-711-Uncensored-Heretic-NM-DAU**](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF) | DavidAU | 2,014 | 289.15万 | 基于 Qwen3.6 的社区"**去审查**"微调，GGUF 量化，下载量近 300 万 |
| [**Qwen3.8-27B-FP8**](https://huggingface.co/Qwen/Qwen3.8-27B-FP8) | Qwen | 282 | 0 | 官方 FP8 精度版本，推理更省显存 |
| [**Qwen3.8-2.4T-A95B-FP8**](https://huggingface.co/Qwen/Qwen3.8-2.4T-A95B-FP8) | Qwen | 183 | 9,334 | MoE 旗舰的 FP8 量化版 |
| [**MiniMax-H3-GGUF**](https://huggingface.co/unsloth/MiniMax-H3-GGUF) | unsloth | 155 | 13.68万 | **视频模型也能 GGUF**？unsloth 对 H3 的量化尝试，降低部署门槛 |
| [**MiniMax-H3_comfy**](https://huggingface.co/Kijai/MiniMax-H3_comfy) | Kijai | 339 | 0 | H3 的 ComfyUI 工作流封装版本，方便本地使用 |
| [**MiniMax-H3**](https://huggingface.co/Comfy-Org/MiniMax-H3) | Comfy-Org | 1,316 | 1,176.86万 | **下载量王者**（超千万），ComfyUI 官方适配版 H3 |

---

## 🔍 生态信号

**模型家族势能：** 本周生态呈现明显的**三足鼎立**格局——Qwen3.8 系列（多模态+MoE 双线推进）、DeepSeek-V4（Flash/Pro 分化迭代）、MiniMax-H3（视频生成现象级产品）。其中 **MiniMax-H3 的生态外溢最为显著**，衍生出 Turbo 版、多款 LoRA、ComfyUI 适配及 GGUF 量化，呈现出"模型即平台"的特征。

**开源权重继续领跑：** 榜单 30 席中**全部为开源权重模型**，且以可商用的宽松协议为主。Kimi-K3 以压缩张量技术实现差异化竞争，融合稀疏化与量化优势，指明大模型高效化的重要演进方向。

**量化与微调热度空前：** unsloth 持续扮演"量化基础设施"角色（多款 GGUF 上榜）；社区微调呈现**垂直分化**——从"去审查"到"人物写实"均有覆盖，但高质量风格化微调仍存在大量供给缺口。

**关键信号：** 视频生成模型生态成熟度快速逼近文本模型，GGUF 量化、LoRA 适配、ComfyUI 集成等周边基础设施已全面就位。

---

## 🧪 值得探索

1. **[Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3)** — 本周点赞冠军，压缩张量技术在保持性能的同时大幅降低推理成本，是研究**高效多模态架构**的最新范本。

2. **[MiniMax-H3-GGUF](https://huggingface.co/unsloth/MiniMax-H3-GGUF)** — 视频生成模型被 GGUF 量化是重大信号，意味着视频模型可能走向消费级硬件本地部署，值得亲自测试效果与速度的平衡点。

3. **[LFM2.5-2.6B](https://huggingface.co/LiquidAI/LFM2.5-2.6B)** — 液体神经网络落地产品，2.6B 参数挑战同量级所有模型，对**端侧部署**和**低资源场景**有重要参考价值。

---
*本日报由 [agents-radar](https://github.com/kky-wollu/agents-radar) 自动生成。*
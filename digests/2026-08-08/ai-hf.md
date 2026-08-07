# Hugging Face 热门模型日报 2026-08-08

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-08-07 22:41 UTC

---

# 🤖 Hugging Face 热门模型日报 — 2026-08-08

## 📌 今日速览

本周 Hugging Face 生态呈现 **“三足鼎立”** 格局：**MiniMax-H3 视频生成家族**以绝对数量优势霸榜（8 个相关条目），覆盖从官方权重到社区 LoRA、GGUF 量化、ComfyUI 适配的完整链条；**DeepSeek-V4-Flash** 与 **Qwen3.6 系列**的社区微调/量化版本持续发酵，显示头部开源 LLM 的二次创作生态异常活跃；此外，**GLM-5.2**、**Kimi-K3** 等重量级新模型发布后迅速获得数万下载，验证了国内 AI 团队在开源社区的话语权。多模态（语音、OCR、图像编辑）与专用模型（代码、安全）也有亮眼表现，整体生态呈现“通用能力收敛、细分场景爆发”的态势。

---

## 🏆 热门模型

### 🧠 语言模型（LLM、对话、指令微调）

| 模型 | 作者 | 点赞 | 下载 | 说明 |
|------|------|------|------|------|
| [**DeepSeek-V4-Flash-0731**](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) | deepseek-ai | 2,737 | 702,709 | DeepSeek 第四代 Flash 版本，70 万下载印证其作为开源主力对话模型的统治力 |
| [**GLM-5.2**](https://huggingface.co/zai-org/GLM-5.2) | zai-org | 4,886 | 2,430,330 | 智谱新一代 MoE 架构模型（glm_moe_dsa），240 万+ 下载量，对话与推理能力全面升级 |
| [**Kimi-K3**](https://huggingface.co/moonshotai/Kimi-K3) | moonshotai | 10,274 | 1,308,186 | 月之暗面旗舰多模态 LLM，支持压缩张量，周点赞破万，社区热度极高 |
| [**LFM2.5-2.6B**](https://huggingface.co/LiquidAI/LFM2.5-2.6B) | LiquidAI | 376 | 77,973 | Liquid AI 基于 LFM2 架构的小参数高效模型，主打低资源部署 |
| [**maple-preview**](https://huggingface.co/deepgrove/maple-preview) | deepgrove | 222 | 686 | DeepGrove 预览版 MoE 因果 LM，新面孔值得关注 |
| [**Ling-3.0-flash**](https://huggingface.co/inclusionAI/Ling-3.0-flash) | inclusionAI | 202 | 3,065 | 零一万物 Ling 系列 Flash 版，Hybrid 架构轻量对话模型 |

### 🎨 多模态与生成（图像、视频、音频）

| 模型 | 作者 | 点赞 | 下载 | 说明 |
|------|------|------|------|------|
| [**MiniMaxAI/MiniMax-H3**](https://huggingface.co/MiniMaxAI/MiniMax-H3) | MiniMaxAI | 2,939 | 18,112 | MiniMax 官方 H3 视频生成模型，支持文/图生视频，本周绝对主角 |
| [**Comfy-Org/MiniMax-H3**](https://huggingface.co/Comfy-Org/MiniMax-H3) | Comfy-Org | 931 | 3,139,920 | ComfyUI 官方优化的 H3 单文件版，**310 万+ 下载**，生态工具链核心 |
| [**baidu/Unlimited-OCR**](https://huggingface.co/baidu/Unlimited-OCR) | baidu | 3,953 | 2,836,694 | 百度通用 OCR 模型，文本+视觉融合，280 万下载，生产力利器 |
| [**microsoft/Mage-VL**](https://huggingface.co/microsoft/Mage-VL) | microsoft | 301 | 456,140 | 微软多模态理解模型，45 万下载，企业级视觉语言能力 |
| [**Audio8-TTS-Preview-0.6b**](https://huggingface.co/Audio8/Audio8-TTS-Preview-0.6b) | Audio8 | 305 | 12,633 | 新一代 TTS 模型，基于 ArkTTS 架构，语音合成新势力 |
| [**FLUX.1-dev**](https://huggingface.co/black-forest-labs/FLUX.1-dev) | black-forest-labs | 14,026 | 512,841 | 文生图标杆模型，本周点赞最高（1.4 万），仍是图像生成王者 |

### 🔧 专用模型（代码、安全、语音）

| 模型 | 作者 | 点赞 | 下载 | 说明 |
|------|------|------|------|------|
| [**KAT-Coder-V2.5-Dev**](https://huggingface.co/Kwaipilot/KAT-Coder-V2.5-Dev) | Kwaipilot | 531 | 17,399 | 快手代码模型，基于 Qwen3.5-MoE，支持多模态代码理解 |
| [**Shieldstral-1.0-3B**](https://huggingface.co/mistralai/Shieldstral-1.0-3B) | mistralai | 183 | 2,480 | Mistral 安全审查模型，vLLM 兼容，内容安全新防线 |
| [**NVIDIA-NemotronLabs-VoiceChat-11B**](https://huggingface.co/nvidia/NVIDIA-NemotronLabs-VoiceChat-11B) | nvidia | 226 | 359 | 英伟达语音对话模型，整合多篇论文技术 |

### 📦 微调与量化（社区微调、GGUF）

| 模型 | 作者 | 点赞 | 下载 | 说明 |
|------|------|------|------|------|
| [**Qwen3.6-27B-Fable-Fusion-711...**](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF) | DavidAU | 1,704 | 2,217,339 | Qwen3.6 社区超长命名微调版，GGUF 量化，220 万下载 |
| [**DeepSeek-V4-Flash-GGUF**](https://huggingface.co/unsloth/DeepSeek-V4-Flash-0731-GGUF) | unsloth | 585 | 161,253 | Unsloth 官方量化版 DeepSeek V4，llama.cpp 即下即用 |
| [**Qwen3.6-35B-A3B-Uncensored...**](https://huggingface.co/LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V7-GGUF) | LuffyTheFox | 426 | 332,992 | Qwen3.6 MoE 解禁版 GGUF，33 万下载，社区热度极高 |
| [**MiniMax-H3-Turbo-Lora**](https://huggingface.co/larryvrh/MiniMax-H3-Turbo-Lora) | larryvrh | 407 | 0 | H3 Turbo LoRA，刚发布暂无下载，但值得持续关注 |
| [**LFM2.5-2.6B-GGUF**](https://huggingface.co/LiquidAI/LFM2.5-2.6B-GGUF) | LiquidAI | 143 | 31,489 | 官方 GGUF 版，方便本地部署 |
| [**Minimax-H3-nvfp4-INT4-INT8**](https://huggingface.co/Abiray/Minimax-H3-nvfp4-INT4-INT8-Convrot) | Abiray | 127 | 452,420 | H3 量化版，45 万下载，低精度视频生成的探索者 |
| [**MiniMax-H3_GGUFs**](https://huggingface.co/realrebelai/MiniMax-H3_GGUFs) | realrebelai | 168 | 87,870 | H3 GGUF 量化合集，基于 Comfy-Org 版 |

---

## 🌐 生态信号

**模型家族势力版图：** 本周最强势的三大阵营——**MiniMax-H3**（视频生成全家桶）、**DeepSeek-V4**（通用对话+量化）、**Qwen3.6**（MoE+社区微调）。MiniMax 通过官方+ComfyUI+社区三方联动，构建了从权重到部署的完整闭环，其“闪电战”策略值得关注。国产模型（GLM、Kimi、Ling）持续霸榜，开源权重已成国内大厂的标配打法。

**开源 vs 闭源：** 榜单 30 个模型中 28 个为开源权重，闭源 API 模型已几乎从 HF 热度榜消失。开源模型的“民主化”效应催生了海量社区微调（uncensored、角色扮演、垂直优化），但**同质化严重**——大量模型仅靠命名差异化，真实能力增益有限。

**量化活动指数级增长：** GGUF 成为绝对主流格式（6 个条目），NVFP4/INT4/INT8 混合精度方案在视频模型中兴起。Unsloth 作为量化基础设施提供方，已从“工具”升级为“生态入口”。建议关注**量化质量基准缺失**的问题——当前社区更关注“能不能跑”而非“跑得多好”。

---

## 🔭 值得探索

1. **[GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** — 智谱最新 MoE 旗舰，240 万下载量背后是社区对其推理能力的强烈认可。其“glm_moe_dsa”架构（动态稀疏注意力）可能是下一代高效 Transformer 的重要方向，强烈建议实测其长上下文与推理性能。

2. **[MiniMax-H3 系列](https://huggingface.co/MiniMaxAI/MiniMax-H3)** — 本周生态系统的“中心”。建议从 [Comfy-Org 版](https://huggingface.co/Comfy-Org/MiniMax-H3)入手体验视频生成，再对比 [nvfp4 量化版](https://huggingface.co/Abiray/Minimax-H3-nvfp4-INT4-INT8-Convrot) 的精度损失，评估低精度视频生成的可行性。

3. **[Shieldstral-1.0-3B](https://huggingface.co/mistralai/Shieldstral-1.0-3B)** — 3B 参数的安全审查模型，小而精。在开源模型大规模部署的当下，内容安全将成为刚需，这个模型可能是构建“安全层”的最佳起点，值得提前布局研究。

---
*本日报由 [agents-radar](https://github.com/kky-wollu/agents-radar) 自动生成。*
# Hugging Face 热门模型日报 2026-08-06

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-08-05 23:05 UTC

---

# 🤖 Hugging Face 热门模型日报 — 2026-08-06

---

## 📌 今日速览

今日榜单呈现出**多模态推理（LMM）主导、经典开源家族新版本集中爆发**的格局。**Kimi-K3** 以超过 10,000 周点赞登顶总榜，成为最强人气王；**GLM-5.2**（4.8K 赞）与 **DeepSeek-V4-Flash** 系列双双位居前列，国产开源模型在全球生态中继续领跑。视频生成方面，**MiniMax-H3** 携官方版与 Comfy-Org 集成版同时上榜，展示出文生视频领域的强劲热度。值得注意的是，围绕 **Qwen3.6 系列的社区微调与量化模型密度极高**（本榜共 6 个），再次印证了“顶级基座 + 繁荣微调生态”的良性循环。此外，**百度 Unlimited-OCR** 以近 400 万下载量成为工具型模型的流量黑马。

---

## 🔥 热门模型

### 🧠 语言模型（LLM、对话模型、指令微调）

| 模型 | 作者 | 点赞 | 下载 | 说明 |
|---|---|---|---|---|
| [**Kimi-K3**](https://huggingface.co/moonshotai/Kimi-K3) | moonshotai | 10,118 | 1,125,935 | 月之暗面新一代旗舰多模态模型，以压倒性热度登顶总榜，支持压缩张量，兼具图文理解与对话能力 |
| [**GLM-5.2**](https://huggingface.co/zai-org/GLM-5.2) | zai-org | 4,848 | 2,234,662 | 智谱最新 MoE 对话模型，周点赞榜第二，与 Kimi 形成“双雄”格局，下载量超 200 万 |
| [**DeepSeek-V4-Flash-0731**](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash-0731) | deepseek-ai | 2,483 | 433,284 | DeepSeek V4 系列 Flash 版本，主打高效对话生成，是当日最“新鲜”的版本迭代 |
| [**DeepSeek-V4-Flash**](https://huggingface.co/deepseek-ai/DeepSeek-V4-Flash) | deepseek-ai | 2,030 | 2,737,621 | DeepSeek V4 家族主力模型，下载量全榜第一（超 270 万），社区基座之选 |
| [**LFM2.5-2.6B**](https://huggingface.co/LiquidAI/LFM2.5-2.6B) | LiquidAI | 278 | 47,393 | Liquid AI 的轻量文本生成模型，2.6B 参数量主打高效推理，适合边缘部署场景 |
| [**Inkling-Small**](https://huggingface.co/thinkingmachines/Inkling-Small) | thinkingmachines | 308 | 15,500 | 小型多模态对话模型，延续 Inkling 系列，主打轻量级图文交互 |
| [**K-EXAONE-2.0-750B-A37B**](https://huggingface.co/LGAI-EXAONE/K-EXAONE-2.0-750B-A37B) | LGAI-EXAONE | 129 | 325 | LG 超大规模 MoE 模型（750B 总参数/37B 激活），代表韩系开源模型的最新进展 |

### 🎨 多模态与生成（图像、视频、音频、文本到X）

| 模型 | 作者 | 点赞 | 下载 | 说明 |
|---|---|---|---|---|
| [**MiniMax-H3**](https://huggingface.co/MiniMaxAI/MiniMax-H3) | MiniMaxAI | 2,480 | 10,841 | MiniMax 最新文生视频模型，支持图像/文本到视频双输入，当日视频生成领域头号热度 |
| [**Unlimited-OCR**](https://huggingface.co/baidu/Unlimited-OCR) | baidu | 3,905 | 2,703,366 | 百度通用 OCR 模型，下载量全榜第二，面向任意场景的文本识别，工具属性极强 |
| [**Mage-VL**](https://huggingface.co/microsoft/Mage-VL) | microsoft | 274 | 435,784 | 微软视觉语言模型，多模态推理能力扎实，下载量可观，企业级背书 |
| [**Audio8-TTS-Preview-0.6b**](https://huggingface.co/Audio8/Audio8-TTS-Preview-0.6b) | Audio8 | 273 | 11,276 | 基于 ArkTTS 架构的语音合成模型，0.6B 轻量参数，快速预览版 |
| [**Kroma**](https://huggingface.co/lodestones/Kroma) | lodestones | 190 | 0 | 基于 Krea 2 的 LoRA 文生图模型，尚处早期发布阶段（下载量为 0），值得跟踪 |
| [**Inflect-Micro-v2**](https://huggingface.co/owensong/Inflect-Micro-v2) | owensong | 417 | 2,072 | 面向 CPU/边缘设备的轻量本地 TTS 模型，主打低延迟语音合成 |
| [**NVIDIA-NemotronLabs-VoiceChat-11B**](https://huggingface.co/nvidia/NVIDIA-NemotronLabs-VoiceChat-11B) | nvidia | 123 | 80 | 英伟达语音对话模型，融合多篇论文成果，主打实时语音交互 |

### 🔧 专用模型（代码、数学、医疗、嵌入）

| 模型 | 作者 | 点赞 | 下载 | 说明 |
|---|---|---|---|---|
| [**KAT-Coder-V2.5-Dev**](https://huggingface.co/Kwaipilot/KAT-Coder-V2.5-Dev) | Kwaipilot | 493 | 15,381 | 基于 Qwen3.5-MoE 架构的开发者版代码模型，定位编程助手场景 |
| [**Shieldstral-1.0-3B**](https://huggingface.co/mistralai/Shieldstral-1.0-3B) | mistralai | 129 | 166 | Mistral 官方安全审查模型，用于生成内容合规过滤，支持 vLLM 部署 |

### 📦 微调与量化（社区微调、GGUF、AWQ）

| 模型 | 作者 | 点赞 | 下载 | 说明 |
|---|---|---|---|---|
| [**Qwen3.6-27B-Fable-Fusion-711-…-GGUF**](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF) | DavidAU | 1,584 | 1,633,405 | Qwen3.6 社区微调的极致融合版本，叠加多种优化策略，下载超 160 万 |
| [**DeepSeek-V4-Flash-0731-GGUF**](https://huggingface.co/unsloth/DeepSeek-V4-Flash-0731-GGUF) | unsloth | 500 | 111,678 | unsloth 官方量化版，与新模型同日发布，主打本地部署低门槛 |
| [**Kimi-K3-GGUF**](https://huggingface.co/unsloth/Kimi-K3-GGUF) | unsloth | 316 | 170,055 | Kimi-K3 量化版，当日发布即获 17 万下载，顶级模型的轻量化首选 |
| [**Qwen3.6-35B-A3B-U…-GGUF**](https://huggingface.co/LuffyTheFox/Qwen3.6-35B-A3B-Uncensored-Genesis-Hermes-V7-GGUF) | LuffyTheFox | 384 | 308,857 | Qwen3.6 的 Hermes 风格微调 + GGUF，主打“Uncensored”社区赛道 |
| [**Qwen3.5-9B-The-Defiant-…-GGUF**](https://huggingface.co/DavidAU/Qwen3.5-9B-The-Defiant-Fable-Uncensored-Heretic-NEO-IMATRIX-MAX-MTP-GGUF) | DavidAU | 280 | 323,116 | DavidAU 另一款 Qwen3.5 极致魔改版本，Imatrix + MTP 优化，热度持续 |
| [**MiniMax-H3_GGUFs**](https://huggingface.co/realrebelai/MiniMax-H3_GGUFs) | realrebelai | 133 | 40,010 | MiniMax-H3 社区量化版，为 ComfyUI 本地视频生成提供低配方案 |
| [**Qwen3.6-35B-A3B-Escha-W2**](https://huggingface.co/EschaLabs/Qwen3.6-35B-A3B-Escha-W2) | EschaLabs | 209 | 2,987 | Qwen3.6 架构的 MoE 微调变体，35B 总参/3B 激活，主打高性价比 |
| [**Qwythos-27B-v1**](https://huggingface.co/empero-ai/Qwythos-27B-v1) | empero-ai | 144 | 2,243 | Qwen3.5 多模态微调版本，社区风格化定制 |

---

## 🌐 生态信号

**多模态推理全面上位。** 榜单前两名（Kimi-K3、GLM-5.2）均将视觉理解与文本生成深度融合，“image-text-to-text”成为主流标签，纯粹单模态新模型几乎绝迹。

**Qwen 系列仍是社区微调的“宇宙中心”。** 本榜 30 个模型中有 6 个直接基于 Qwen3.5/3.6，且下载量普遍极高（多款超 30 万），头部基座 + 长尾微调的生态仍在加速。MiniMax-H3 与 DeepSeek-V4 的生态配套（量化、ComfyUI 集成）也已快速跟上，说明新一代基座正在复制 Qwen 的成功路径。

**量化部署是刚需。** GGUF/量化版本下载量显著高于官方原版（如 Kimi-K3-GGUF 发布当日即获 17 万下载），社区对“能本地跑”的需求极为强烈。

**开源权重占据绝对主导。** 榜单 Top10 全部为开源模型，闭源 API 模型仅通过文档间接影响生态。开源模型正从“跟随者”变身为“定义者”，特别是在视频生成与多模态推理赛道上。

---

## 🔭 值得探索

1. **[Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3)** — 周赞破万，建议立刻研究。其强调的“compressed-tensors”能力可能代表下一代多模态模型的参数效率范式，且官方快速推出 GGUF 版本，完整生态动作值得拆解。

2. **[MiniMax-H3](https://huggingface.co/MiniMaxAI/MiniMax-H3)** — 文本到视频的新一代代表。官方版与 Comfy-Org 集成版同时上线，打通了工作流工具链，是研究“视频生成模型如何嵌入创作者生态”的极佳案例。

3. **[Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** — 虽然定位“工具型”而非“旗舰级”，但近 400 万下载量证明了实用型模型的巨大潜力，也提示多模态赛道的下一个竞争热点可能从“生成”转向“理解与提取”。

---

> 日报数据来源: Hugging Face Hub 热门模型榜（按周点赞排序）| 生成时间: 2026-08-06

---
*本日报由 [agents-radar](https://github.com/kky-wollu/agents-radar) 自动生成。*
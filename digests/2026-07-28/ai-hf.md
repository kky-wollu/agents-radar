# Hugging Face 热门模型日报 2026-07-28

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-07-27 23:08 UTC

---

# Hugging Face 热门模型日报（2026-07-28）

## 今日速览

本周 Hugging Face 榜单呈现三大亮点：**多模态大模型全面爆发**，moonshotai 推出的 **Kimi-K3** 以近 6000 点赞高居榜首，Qwen3.6-35B-A3B 系列在量化与微调版本中表现活跃；**OCR 领域迎来重量级选手**，百度出品的 **Unlimited-OCR** 下载量突破 260 万，成为实用型模型的新标杆；**量化生态持续升温**，GGUF 格式模型占据榜单近三分之一席位，1-bit / 2-bit 量化技术（如 Bonsai 系列）正在成为社区关注焦点。值得注意的还有微软的多款图像编辑模型（Mage-Flow 系列）以及 NVIDIA 新发布的 Cosmos3-Edge 视觉模型。

---

## 热门模型

### 🧠 语言模型（LLM、对话模型、指令微调）

| 模型 | 作者 | 点赞 | 下载 | 一句话说明 |
|------|------|------|------|------------|
| [Laguna-S-2.1](https://huggingface.co/poolside/Laguna-S-2.1) | poolside | 753 | 63,605 | poolside 推出的 2.1 版文本生成模型，以「拉古纳」命名，定位高性能对话与推理 |
| [Solar-Open2-250B](https://huggingface.co/upstage/Solar-Open2-250B) | upstage | 628 | 3,761 | 韩国 AI 领军企业 Upstage 开源 250B 参数大模型，主打开放权重与长文本理解 |
| [Nanbeige4.2-3B](https://huggingface.co/Nanbeige/Nanbeige4.2-3B) | Nanbeige | 491 | 16,518 | 3B 参数轻量级语言模型，适合本地部署与边缘场景推理 |
| [GLM-5.2](https://huggingface.co/zai-org/GLM-5.2) | zai-org | 4,547 | 1,003,547 | 智谱 AI 开源大模型最新版本 GLM-5.2，采用 MoE 架构，下载量已破百万 |
| [Motif-3-Beta](https://huggingface.co/Motif-Technologies/Motif-3-Beta) | Motif-Technologies | 199 | 2,532 | Motif 团队发布的第三代对话模型 Beta 版，面向角色扮演与个性化交互 |

### 🎨 多模态与生成（图像、视频、音频、文本到X）

| 模型 | 作者 | 点赞 | 下载 | 一句话说明 |
|------|------|------|------|------------|
| [Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3) | moonshotai | 5,965 | 2,850 | 月之暗面最新多模态模型，支持图像与文本联合理解，本周点赞数最高 |
| [Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR) | baidu | 3,326 | 2,645,773 | 百度开源 OCR 模型，号称「不限场景」的文字识别模型，下载量惊人 |
| [Inkling](https://huggingface.co/thinkingmachines/Inkling) | thinkingmachines | 1,602 | 36,196 | Thinking Machines 推出的多模态对话模型，擅长度图、看图说话 |
| [Mage-Flow](https://huggingface.co/microsoft/Mage-Flow) | microsoft | 384 | 1,691 | 微软推出的文本到图像生成模型，支持图像编辑与风格迁移 |
| [Qwen3.6-35B-A3B](https://huggingface.co/Qwen/Qwen3.6-35B-A3B) | Qwen | 2,546 | 6,187,853 | 阿里通义千问官方多模态 MoE 模型，35B 参数仅激活 3B，极高效率 |
| [Cosmos3-Edge](https://huggingface.co/nvidia/Cosmos3-Edge) | nvidia | 132 | 33,127 | NVIDIA 发布 Cosmos 系列第三版视觉模型，面向边缘设备部署 |
| [Mage-Flow-Edit-Turbo](https://huggingface.co/microsoft/Mage-Flow-Edit-Turbo) | microsoft | 100 | 1,115 | 微软图像编辑 Turbo 版，支持指令式图像修改 |
| [Inflect-Nano-v2](https://huggingface.co/owensong/Inflect-Nano-v2) | owensong | 91 | 349 | 极轻量级本地 TTS 模型，专为 CPU 和边缘 AI 优化 |
| [Inflect-Micro-v2](https://huggingface.co/owensong/Inflect-Micro-v2) | owensong | 221 | 483 | 更小体积的本地语音合成模型，微秒级响应，适合嵌入式场景 |

### 🔧 专用模型（代码、视觉、OCR、嵌入）

| 模型 | 作者 | 点赞 | 下载 | 一句话说明 |
|------|------|------|------|------------|
| [KAT-Coder-V2.5-Dev](https://huggingface.co/Kwaipilot/KAT-Coder-V2.5-Dev) | Kwaipilot | 240 | 5,312 | 基于 Qwen3.5 MoE 的代码生成模型，针对开发者场景优化 |
| [Fara1.5-27B](https://huggingface.co/microsoft/Fara1.5-27B) | microsoft | 130 | 1,406 | 微软计算机视觉多模态模型，支持 GUI 操作与图像理解 |
| [OvisOCR2](https://huggingface.co/ATH-MaaS/OvisOCR2) | ATH-MaaS | 327 | 42,152 | 基于 Qwen3.5 的 OCR 专用模型，面向文档识别与版面分析 |
| [krea2-identity-edit](https://huggingface.co/conradlocke/krea2-identity-edit) | conradlocke | 554 | 0 | Krea 2 模型的 LoRA 插件，专门用于身份一致性的图像编辑 |
| [antares-1b](https://huggingface.co/fdtn-ai/antares-1b) | fdtn-ai | 207 | 6,421 | 1B 参数的安全专用模型，采用 GraniteMoEHybrid 架构，聚焦安全与对齐 |

### 📦 微调与量化（社区微调、GGUF、AWQ）

| 模型 | 作者 | 点赞 | 下载 | 一句话说明 |
|------|------|------|------|------------|
| [Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF) | DavidAU | 742 | 634,146 | 极端微调的 Qwen3.6 版本，融合多种风格的长串名称暗示其「缝合」属性 |
| [Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf) | prism-ml | 1,068 | 648,938 | 27B 参数的三值量化模型（2-bit），在性能与压缩比之间取得突破 |
| [Bonsai-27B-gguf](https://huggingface.co/prism-ml/Bonsai-27B-gguf) | prism-ml | 657 | 2,257,928 | 首创 1-bit 量化 27B 参数模型，以极低存储占用实现对话能力 |
| [Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive) | HauhauCS | 3,132 | 1,894,395 | 解禁版 Qwen3.6 MoE 量化模型，强调激进对话风格，下载量近 200 万 |
| [Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF) | empero-ai | 2,487 | 1,336,263 | 基于 Qwen3.5 的推理量化模型，模仿 Claude 神话风格，受欢迎度极高 |
| [Laguna-S-2.1-GGUF](https://huggingface.co/unsloth/Laguna-S-2.1-GGUF) | unsloth | 217 | 117,456 | Unsloth 团队出品的 Laguna-S-2.1 GGUF 量化版本，优化推理速度 |
| [GLM-5.2-Vision-NVFP4](https://huggingface.co/baseten/GLM-5.2-Vision-NVFP4) | baseten | 124 | 2,276 | GLM-5.2 视觉版 NVFP4 量化模型，针对 NVIDIA 平台优化 |
| [Laguna-S-2.1-NVFP4](https://huggingface.co/poolside/Laguna-S-2.1-NVFP4) | poolside | 148 | 158,308 | 官方推出的 Laguna-S-2.1 原生 FP4 量化版本，支持 vLLM |

---

## 生态信号

### 模型家族势头
**Qwen3.6 系列**成为本周最大赢家，其原生模型（#28）下载量突破 600 万，同时出现至少 5 个社区微调/量化版本，覆盖从 35B MoE 到 27B 的各种口味。**GLM-5.2** 紧随其后，以 MoE-DSA 架构和百万级下载证明国产大模型在开源社区的竞争力。**Kimi-K3** 虽下载量不高，但点赞数最高，说明其技术价值获得社区高度认可。

### 开源权重 vs 闭源趋势
本周榜单中，开源模型仍占绝对主导地位。值得注意的是，**百度 Unlimited-OCR** 和 **NVIDIA Cosmos3-Edge** 这两个企业级模型选择完全开源权重（safetensors），表明大型企业正加速将核心能力开放，以构建生态护城河。闭源 API 模型已基本从 Hugging Face 热门榜消失。

### 量化与微调活动
**极端量化成为新话题**：prism-ml 团队同时推出 1-bit 和 2-bit 量化模型，验证了「只要量化得当，27B 模型也能在低资源设备运行」的思路。社区微调呈现「拼贴艺术」风格——多个长名称模型融合童话（Fable）、解禁（Uncensored）、神话（Mythos）等元素，显示出用户对角色扮演与风格化对话的强烈需求。**Unsloth** 和 **vLLM** 作为量化与推理框架，频繁出现在模型标签中，已成为社区基础设施级工具。

---

## 值得探索

1. **[Kimi-K3](https://huggingface.co/moonshotai/Kimi-K3)** — 本周点赞冠军，月之暗面最新多模态大模型。如果你关注国产多模态前沿、压缩感知或高效特征提取，这是必须试用的模型。其「compressed-tensors」标签暗示了模型压缩方面的创新。

2. **[Bonsai-27B-gguf](https://huggingface.co/prism-ml/Bonsai-27B-gguf)** — 1-bit 量化 27B 模型，下载量已超 225 万。对于研究模型量化极限、探索低比特推理可行的研究者而言，这是一个里程碑式作品。建议与同团队的 Ternary-Bonsai-27B 对比使用，感受量化精度与能力的权衡。

3. **[OvisOCR2](https://huggingface.co/ATH-MaaS/OvisOCR2)** — 基于 Qwen3.5 的 OCR 专用模型，下载量稳步上升。如果你有文档理解、表格识别或版面分析需求，这个模型提供了一个高效的专精方案，值得与百度的 Unlimited-OCR 对比测试。

---
*本日报由 [agents-radar](https://github.com/kky-wollu/agents-radar) 自动生成。*
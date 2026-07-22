# Hugging Face 热门模型日报 2026-07-23

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-07-22 23:09 UTC

---

好的，这是为您生成的《Hugging Face 热门模型日报》。

---

### **Hugging Face 热门模型日报 | 2026-07-23**

#### **今日速览**

本周 Hugging Face 生态呈现出 **“多模态为王”** 与 **“极致量化”** 两大显著趋势。**Google 的 Gemma 4** 系列与 **百度** 的 OCR 模型继续以压倒性的下载量领跑，展现了巨头在通用视觉语言模型上的统治力。与此同时，社区对模型效率的追求达到新高度，以 **prism-ml** 为代表的 1-bit 和 2-bit 量化模型（如 Bonsai 系列）获得了极高热度，标志着边缘部署和超低资源推理成为主流。此外，**Kimi** 和 **GLM** 等国产大模型凭借强大的性能，在开源社区中势头强劲。

---

#### **热门模型**

##### 🧠 语言模型（LLM、对话模型、指令微调）

- **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)**
  - 作者: zai-org | 点赞: 4,334 | 下载: 545k
  - 一句话说明：智谱AI的新一代开源MoE大模型，凭借强大的综合能力和极高的社区关注度，成为本周热议的焦点。
- **[google/gemma-4-31B-it](https://huggingface.co/google/gemma-4-31B-it)**
  - 作者: google | 点赞: 3,327 | 下载: 12.1M
  - 一句话说明：Google 发布的最新指令微调模型，参数规模与性能兼备，是当前下载量最高的模型之一，代表了顶级开源LLM的水平。
- **[moonshotai/Kimi-K2.7-Code](https://huggingface.co/moonshotai/Kimi-K2.7-Code)**
  - 作者: moonshotai | 点赞: 1,222 | 下载: 722k
  - 一句话说明：月之暗面推出的代码专用版本，标志着Kimi系列在专业领域的深耕，受到开发者社区的广泛欢迎。
- **[Nanbeige/Nanbeige4.2-3B](https://huggingface.co/Nanbeige/Nanbeige4.2-3B)** & **[upstage/Solar-Open2-250B](https://huggingface.co/upstage/Solar-Open2-250B)**
  - 作者: Nanbeige / upstage | 点赞: 223 / 203
  - 一句话说明：分别代表高效小模型（3B）和超大参数模型（250B）的两个端，尽管下载量尚未爆发，但代表了生态的多样性。

##### 🎨 多模态与生成（图像、视频、音频、文本到X）

- **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)**
  - 作者: baidu | 点赞: 2,700 | 下载: 2.2M
  - 一句话说明：百度推出的全能OCR模型，以其无限制场景的文字识别能力创造了惊人的下载量，是多模态落地应用的标杆。
- **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)**
  - 作者: HauhauCS | 点赞: 2,998 | 下载: 1.99M
  - 一句话说明：基于 Qwen3.6 的社区微调MoE版本，结合了视觉、MoE和“非审查”特性，精准踩中了社区对高性能、无限制多模态模型的需求。
- **[microsoft/Mage-Flow](https://huggingface.co/microsoft/Mage-Flow)**
  - 作者: microsoft | 点赞: 115 | 下载: 0
  - 一句话说明：微软最新发布的文本到图像生成模型，虽然下载数据刚起步，但作为科技巨头的文生图新作，具备很高的研究价值。
- **[OpenMOSS-Team/MOSS-Transcribe-Diarize](https://huggingface.co/OpenMOSS-Team/MOSS-Transcribe-Diarize)**
  - 作者: OpenMOSS-Team | 点赞: 308 | 下载: 92k
  - 一句话说明：专为音频转写和说话人识别设计的模型，填补了音频内容理解领域的空白，实用性强。
- **[nvidia/Cosmos3-Edge](https://huggingface.co/nvidia/Cosmos3-Edge)** & **[nvidia/nemotron-3.5-asr-streaming-0.6b](https://huggingface.co/nvidia/nemotron-3.5-asr-streaming-0.6b)**
  - 作者: nvidia | 点赞: 87-914
  - 一句话说明：NVIDIA持续在边缘计算和多模态领域发力，Cosmos3-Edge专注视觉边缘，Nemotron-3.5则针对流式语音识别，展现了其在硬件生态外的模型布局。

##### 🔧 专用模型（代码、数学、医疗、嵌入）

- **[ATH-MaaS/OvisOCR2](https://huggingface.co/ATH-MaaS/OvisOCR2)**
  - 作者: ATH-MaaS | 点赞: 249 | 下载: 17k
  - 一句话说明：专注于OCR的专用模型，是百度Unlimited-OCR的有力竞争者，表明文档理解场景是当前热点。
- **[nvidia/Nemotron-3-Embed-1B-BF16](https://huggingface.co/nvidia/Nemotron-3-Embed-1B-BF16)**
  - 作者: nvidia | 点赞: 102 | 下载: 93k
  - 一句话说明：专为嵌入和语义相似度任务设计的模型，是RAG（检索增强生成）系统的重要组件，下载量可观。
- **[openbmb/MiniCPM-RobotManip](https://huggingface.co/openbmb/MiniCPM-RobotManip)** & **[openbmb/MiniCPM-RobotTrack](https://huggingface.co/openbmb/MiniCPM-RobotTrack)**
  - 作者: openbmb | 点赞: 114-154
  - 一句话说明：面壁智能（OpenBMB）推出的机器人操作和追踪模型，代表视觉-语言-动作（VLA）这一前沿方向。

##### 📦 微调与量化（社区微调、GGUF、AWQ）

- **[prism-ml/Bonsai-27B-gguf](https://huggingface.co/prism-ml/Bonsai-27B-gguf)**
  - 作者: prism-ml | 点赞: 593 | 下载: 1.4M
  - 一句话说明：1-bit 量化的 27B 模型，是极致量化技术的代表作，下载量巨大，证明社区对“让大模型在消费级硬件上跑起来”的强烈需求。
- **[prism-ml/Ternary-Bonsai-27B-gguf](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)** & **[Bonsai-27B-mlx-1bit](https://huggingface.co/prism-ml/Bonsai-27B-mlx-1bit)**
  - 作者: prism-ml | 点赞: 937 / 165
  - 一句话说明：prism-ml 的 Bonsai 系列（2-bit/1-bit/MLX版）集体霸榜，展现了其在模型压缩领域的绝对领导力。
- **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)**
  - 作者: empero-ai | 点赞: 2,416 | 下载: 2.1M
  - 一句话说明：基于 Qwen3.5 的高质量社区微调和量化版，融合了Claude数据集的“神话”风格，是社区微调成功的范例。
- **[DavidAU/Qwen3.6-27B-Fable-Fusion-...-GGUF](https://huggingface.co/DavidAU/Qwen3.6-27B-Fable-Fusion-711-Uncensored-Heretic-NM-DAU-NEO-MAX-MTP-GGUF)**
  - 作者: DavidAU | 点赞: 317 | 下载: 63k
  - 一句话说明：典型的社区魔改模型，将多个特性（非审查、Fable风格、GGUF量化）融合，体现了“自定义大模型”文化的繁荣。

---

#### **生态信号**

1.  **模型家族竞争白热化**：**Qwen**（Qwen3.5/3.6）家族生态最为繁荣，围绕其进行的微调和量化模型数量最多；**GLM-5.2** 作为国产新锐，依靠原生MoE架构在学术和社区层面获得了广泛认可；**Gemma 4** 则以谷歌的品牌和资源垄断了“通用多模态”赛道的绝对下载量。

2.  **量化技术进入“1比特时代”**：以 **prism-ml** 的 Bonsai 系列为代表，1-bit / 2-bit / Ternary（三值）量化模型已不再是试验品，而是成为了高下载量的主流选择。这意味着在个人电脑甚至手机上部署 27B 级别模型已成为现实，这是推动大模型民主化的关键一步。

3.  **“非审查”与“专家MoE”是社区微调的关键词**：众多高赞的社区模型（如 HauhauCS, DavidAU）都带有“Uncensored”和“MoE”标签。这表明社区用户对模型输出的自由度有很高要求，同时认可MoE架构在保持高性能的同时降低推理成本的价值。

---

#### **值得探索**

1.  **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)**：作为目前点赞数最高的模型，它是检验国产MoE模型能力上限的最佳选择。其独特的 DSA（动态稀疏注意力）架构值得深入研究，对于关注大模型前沿架构（MoE）的工程师而言是必看之选。

2.  **[prism-ml/Bonsai-27B-gguf](https://huggingface.co/prism-ml/Bonsai-27B-gguf)**：这是“模型瘦身”技术的里程碑产品。如果您对模型量化、边缘部署或是在有限预算下运行强大模型感兴趣，这个 1-bit 模型绝对值得一试，它可能会改变你对“需要多少显存才能跑大模型”的认知。

3.  **[openbmb/MiniCPM-RobotManip](https://huggingface.co/openbmb/MiniCPM-RobotManip)**：代表了多模态模型的最终落地形态——机器人操作。虽然目前点赞数不高，但它预示着未来。对于希望看到AI从“聊天”走向“与世界互动”的研究者和开发者，这个模型非常值得探索。

---
*本日报由 [agents-radar](https://github.com/kky-wollu/agents-radar) 自动生成。*
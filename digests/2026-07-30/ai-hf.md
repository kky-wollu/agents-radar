# Hugging Face 热门模型日报 2026-07-30

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-07-29 23:01 UTC

---

好的，作为AI模型生态分析师，这是为您生成的2026年7月30日《Hugging Face 热门模型日报》。

---

### **Hugging Face 热门模型日报 | 2026年7月30日**

#### **1. 今日速览**

本周Hugging Face生态呈现三大热点：**国产多模态模型爆发**，月之暗面的Kimi-K3系列与智谱GLM-5.2系列凭借强劲性能与高下载量霸榜，标志着中国AI力量在开源社区的强势崛起；**极致量化与社区魔改**趋势不减，基于Qwen 3.6/3.5的社区微调版与GGUF量化版本（如2-bit、1-bit）占据大量席位，反映了用户对边缘部署和个性化模型的高度需求；**OCR与代码专用模型**异军突起，百度Unlimited-OCR与KAT-Coder等垂直领域模型表现出色，显示大模型正加速向解决具体商业问题渗透。

#### **2. 热门模型**

##### 🧠 语言模型（LLM、对话模型、指令微调）

| 模型 | 作者 | 点赞 | 下载 | 一句话说明 |
| :--- | :--- | :--- | :--- | :--- |
| **GLM-5.2** ([链接](https://huggingface.co/zai-org/GLM-5.2)) | zai-org | 4,639 | 1.27M | 智谱最新一代MoE对话模型，凭借强大的对话与文本生成能力，成为本周社区最受关注的语言模型之一。 |
| **Solar-Open2-250B** ([链接](https://huggingface.co/upstage/Solar-Open2-250B)) | upstage | 693 | 4.8K | Upstage发布的开源250B参数超大语言模型，目标对标闭源前沿，代表了开源社区在超大模型领域的持续探索。 |
| **Nanbeige4.2-3B** ([链接](https://huggingface.co/Nanbeige/Nanbeige4.2-3B)) | Nanbeige | 553 | 18.9K | 一款小而强的3B参数LLM，在低资源场景下提供高效的文本生成能力，适合部署在本地设备上。 |
| **Laguna-S-2.1** ([链接](https://huggingface.co/poolside/Laguna-S-2.1)) | poolside | 825 | 67.3K | Poolside推出的代码生成语言模型，在软件工程领域表现突出，是专业开发者社区的热门选择。 |

##### 🎨 多模态与生成（图像、视频、音频、文本到X）

| 模型 | 作者 | 点赞 | 下载 | 一句话说明 |
| :--- | :--- | :--- | :--- | :--- |
| **Kimi-K3** ([链接](https://huggingface.co/moonshotai/Kimi-K3)) | moonshotai | 8,617 | 99.2K | 本周现象级模型，月之暗面发布的图像理解与对话模型，以极高点赞数登顶榜首，标志着国产多模态模型的突破。 |
| **Unlimited-OCR** ([链接](https://huggingface.co/baidu/Unlimited-OCR)) | baidu | 3,511 | 2.69M | 百度推出的高精度、高速度OCR模型，下载量接近270万，已成为行业级文档识别的首选工具。 |
| **Qwen3.6-35B-A3B** ([链接](https://huggingface.co/Qwen/Qwen3.6-35B-A3B)) | Qwen | 2,586 | 6.16M | 阿里通义千问的官方MoE模型，以35B总参数但仅激活3B参量的高效架构，成为多模态领域的开发基座。 |
| **Inkling** ([链接](https://huggingface.co/thinkingmachines/Inkling)) | thinkingmachines | 1,640 | 39.1K | Thinking Machines发布的多模态对话模型，专注于图像与文本的深度交互理解，风格类似“会看图的聊天机器人”。 |
| **Kimi-K2.7-Code** ([链接](https://huggingface.co/moonshotai/Kimi-K2.7-Code)) | moonshotai | 1,333 | 681K | Kimi系列的代码版模型，结合图像理解与代码生成，能直接根据截图或UI视觉稿生成代码，实用性强。 |
| **Inflect-Micro-v2** ([链接](https://huggingface.co/owensong/Inflect-Micro-v2)) | owensong | 288 | 645 | 极轻量的TTS模型，专为CPU和边缘设备设计，推动了语音合成的端侧部署发展。 |

##### 🔧 专用模型（代码、数学、医疗、嵌入）

| 模型 | 作者 | 点赞 | 下载 | 一句话说明 |
| :--- | :--- | :--- | :--- | :--- |
| **KAT-Coder-V2.5-Dev** ([链接](https://huggingface.co/Kwaipilot/KAT-Coder-V2.5-Dev)) | Kwaipilot | 315 | 6.3K | 基于Qwen 3.5 MoE的代码专项模型，在软件开发任务上进行了深度优化，是程序员的得力助手。 |
| **Fara1.5-27B** ([链接](https://huggingface.co/microsoft/Fara1.5-27B)) | microsoft | 199 | 1.5K | 微软推出的“计算机使用”模型，能够理解图像并执行桌面操作，代表了AI从对话走向Agent控制的关键一步。 |
| **OvisOCR2** ([链接](https://huggingface.co/ATH-MaaS/OvisOCR2)) | ATH-MaaS | 345 | 47.1K | 专业的OCR识别模型，优化了复杂版面与手写体识别，与百度Unlimited-OCR形成专业互补态势。 |
| **antares-1b** ([链接](https://huggingface.co/fdtn-ai/antares-1b)) | fdtn-ai | 230 | 7.7K | 专注于安全领域的1B参数语言模型，为AI安全审计与威胁分析提供了轻量化解决方案。 |

##### 📦 微调与量化（社区微调、GGUF、AWQ）

| 模型 | 作者 | 点赞 | 下载 | 一句话说明 |
| :--- | :--- | :--- | :--- | :--- |
| **Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive** ([链接](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)) | HauhauCS | 3,171 | 1.86M | 基于Qwen 3.6的高人气社区微调版，移除了安全限制（Uncensored），迎合了部分开发者对创造性内容生成的需求。 |
| **prism-ml/Ternary-Bonsai-27B-gguf** ([链接](https://huggingface.co/prism-ml/Ternary-Bonsai-27B-gguf)) | prism-ml | 1,094 | 665K | 首创三值量化（2-bit）的27B模型，将超大模型压缩到极致，极大降低了本地运行门槛。 |
| **prism-ml/Bonsai-27B-gguf** ([链接](https://huggingface.co/prism-ml/Bonsai-27B-gguf)) | prism-ml | 687 | 2.34M | 采用1-bit量化的极低精度版本，下载量高达234万，证明了社区对“能跑的巨型模型”的旺盛需求。 |
| **empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF** ([链接](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)) | empero-ai | 2,515 | 1.26M | 基于Qwen 3.5的社区微调与GGUF量化版，融合了Claude风格的思考模式，是社区进行模型蒸馏与风格迁移的典型作品。 |

#### **3. 生态信号**

- **模型家族势头正旺**：**Qwen 3.5/3.6系列**无疑是本周最大的流量生态，不仅官方模型下载量超600万，更衍生出数十个社区微调与量化版本，形成了类似“Android生态”的繁荣局面。同时，**Kimi-K3**和**GLM-5.2**的强势崛起，预示着国产大模型家族正在形成“三足鼎立”的竞争格局。
- **开源权重的强大生命力**：与闭源模型相比，本周榜单上的模型均为开源权重（safetensors/gguf）。特别是通过**GGUF**和**NVFP4**等量化方式，用户能够在消费级硬件上运行100B级模型，这极大地降低了使用门槛，强化了开源生态的吸引力。
- **社区微调呈现“极端化”**：社区活动呈现出“Uncensored”（无审查）和“极限量化”（1-bit/2-bit）两大趋势。前者反映了用户对模型创造自由度的追求，后者则体现了对大模型本地化、私有化部署的巨大需求。

#### **4. 值得探索**

1.  **moonshotai/Kimi-K3**：作为本周“顶流”，它代表了国产多模态大模型的最前沿水平。推荐所有从事图像理解、视觉问答和跨模态应用的开发者重点研究其技术报告或直接试用。
2.  **prism-ml/Ternary-Bonsai-27B-gguf**：对于硬件资源有限但又想体验27B级模型的用户，这个2-bit量化版是绝佳选择。它测试了模型压缩能力的极限，是研究模型精简技术的理想样本。
3.  **microsoft/Fara1.5-27B**：微软的“Computer Use”模型代表了下一代AI Agent的方向。如果你关注自动化办公、GUI测试或智能助理，这个模型的思路非常值得探索。

---
*本日报由 [agents-radar](https://github.com/kky-wollu/agents-radar) 自动生成。*
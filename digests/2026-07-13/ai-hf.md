# Hugging Face 热门模型日报 2026-07-13

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-07-12 21:25 UTC

---

好的，作为AI模型生态分析师，以下是基于2026年7月13日数据生成的《Hugging Face热门模型日报》。

---

### **Hugging Face 热门模型日报 | 2026年7月13日**

#### **今日速览**

1.  **多模态MoE模型成为绝对主流**：本周榜单被大量集成视觉能力的Qwen 3.5/3.6系列MoE变体模型（如`Qwythos-9B`、`Qwen3.6-35B`）及其量化版本占据，表明社区对**高效多模态推理**的需求已超过传统纯文本模型。
2.  **中国力量与开源巨头发力**：腾讯（`Hy3`）、智谱（`GLM-5.2`）、百度（`Unlimited-OCR`）等国内大厂的模型入围，同时NVIDIA、Unsloth等也贡献了关键模型，开源生态正由中国和美国顶级实验室共同驱动。
3.  **GGUF量化生态全面爆发**：榜单中近一半模型提供GGUF格式，`empero-ai`的`Qwythos-9B`和`unsolth`的`Qwen3.6-27B`下载量均突破百万，个人开发者通过量化部署大型模型的趋势已不可逆转。
4.  **专用模型与核心框架的紧密绑定**：百度`Unlimited-OCR`、NVIDIA `LocateAnything-3B` 等任务型模型表现亮眼，它们深度依赖`transformers`框架，预示着AI能力正从通用对话向**更专业、更基础设施化**的层面渗透。

---

### **热门模型分类详情**

#### 🧠 **语言模型（LLM、对话模型、指令微调）**

*   **[tencent/Hy3](https://huggingface.co/tencent/Hy3)** | 作者: tencent | 👍 714 | ⬇️ 8,655
    *   一句话：腾讯发布的第三代Hunyuan大语言模型，在文本生成和对话任务上表现强劲，代表了国内顶尖实验室的最新权重开放。
*   **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)** | 作者: zai-org | 👍 3,852 | ⬇️ 441,413
    *   一句话：智谱AI开源的新一代 GLM 大模型，采用MoE架构，在对话和推理任务上获得社区极高的关注度和点赞数，是本周最受关注的模型之一。
*   **[meituan-longcat/LongCat-2.0](https://huggingface.co/meituan-longcat/LongCat-2.0)** | 作者: meituan-longcat | 👍 182 | ⬇️ 1,767
    *   一句话：美团长文本大模型的2.0版本，专注于长上下文对话和生成，体现了特定场景（如客服、文档处理）下模型专业化趋势。
*   **[migtissera/Tess-4-27B](https://huggingface.co/migtissera/Tess-4-27B)** | 作者: migtissera | 👍 91 | ⬇️ 971
    *   一句话：基于Qwen 3.5的社区微调模型，定位为多模态助手，展示了社区在通用模型基础上进行创意改造的能力。
*   **[nineninesix/gepard-1.0](https://huggingface.co/nineninesix/gepard-1.0)** | 作者: nineninesix | 👍 84 | ⬇️ 2,263
    *   一句话：一个集成了文本生成与语音合成的多功能模型，探索了文生图模路线。

#### 🎨 **多模态与生成（图像、视频、音频、文本到X）**

*   **[InternScience/Agents-A1](https://huggingface.co/InternScience/Agents-A1)** | 作者: InternScience | 👍 506 | ⬇️ 29,038
    *   一句话：面向智能体应用的MoE多模态模型，能够处理图像和文字并执行复杂任务，反映了AI Agent生态的快速扩张。
*   **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)** | 作者: baidu | 👍 1,941 | ⬇️ 1,430,656
    *   一句话：百度开源的“无限”OCR模型，支持多种场景下的文字识别，因其强大的实用性和高下载量成为本周最成功的工具型模型之一。
*   **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)** | 作者: nvidia | 👍 2,714 | ⬇️ 1,501,653
    *   一句话：NVIDIA发布的定位与识别模型，可理解并定位图像中的任何物体，在视觉特征提取任务中极具价值，高赞高下载。
*   **[CohereLabs/cohere-transcribe-arabic-07-2026](https://huggingface.co/CohereLabs/cohere-transcribe-arabic-07-2026)** | 作者: CohereLabs | 👍 95 | ⬇️ 9,860
    *   一句话：Cohere针对阿拉伯语的专用语音识别模型，表明了多语种ASR领域的细分需求。
*   **[OpenMOSS-Team/MOSS-Transcribe-Diarize](https://huggingface.co/OpenMOSS-Team/MOSS-Transcribe-Diarize)** | 作者: OpenMOSS-Team | 👍 125 | ⬇️ 14,491
    *   一句话：专注于语音转录和说话人分离的模型，为会议记录、电话分析等场景提供了关键的开源工具。
*   **[robbyant/lingbot-world-v2-14b-causal-fast](https://huggingface.co/robbyant/lingbot-world-v2-14b-causal-fast)** | 作者: robbyant | 👍 82 | ⬇️ 0
    *   一句话：视频生成领域的“世界模型”，强调因果推理和快速生成，代表视频生成技术从文本驱动向理解物理世界的进化。

#### 🔧 **专用模型（代码、数学、医疗、嵌入）**

*   **[google/tabfm-1.0.0-pytorch](https://huggingface.co/google/tabfm-1.0.0-pytorch)** | 作者: google | 👍 354 | ⬇️ 20,973
    *   一句话：Google发布的表格数据基础模型，支持零样本分类和回归，为结构化数据分析提供了一个通用且强大的新范式。
*   **[nvidia/Nemotron-Labs-Audex-30B-A3B](https://huggingface.co/nvidia/NVidia-Nemotron-Labs-Audex-30B-A3B)** | 作者: nvidia | 👍 131 | ⬇️ 901
    *   一句话：NVIDIA的实验室系列模型之一，可能专注于音频理解或处理，体现了NVIDIA在多模态和科学计算领域的持续布局。
*   **[SupraLabs/Supra-Router-51M](https://huggingface.co/SupraLabs/Supra-Router-51M)** | 作者: SupraLabs | 👍 105 | ⬇️ 1,434
    *   一句话：一个轻量级的模型“路由器”，用于智能调度和选择不同LLM，是构建复杂LLM Agent或混合专家系统的关键基础设施。

#### 📦 **微调与量化（社区微调、GGUF、AWQ）**

*   **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)** | 作者: empero-ai | 👍 2,041 | ⬇️ 1,967,677
    *   一句话：基于 Qwen 3.5 的社区微调模型，融合了“Mythos”风格，其GGUF量化版本下载量极高，是目前个人部署多模态模型的标杆。
*   **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)** | 作者: HauhauCS | 👍 2,672 | ⬇️ 2,596,384
    *   一句话：本周下载量冠军！这是对 Qwen 3.6 的 “Uncensored” 及激进风格微调，展现了开源社区对模型“个性”和“去限制”的强烈需求。
*   **[unsloth/DeepSeek-V4-Flash-GGUF](https://huggingface.co/unsloth/DeepSeek-V4-Flash-GGUF)** | 作者: unsloth | 👍 151 | ⬇️ 44,614
    *   一句话：Unsloth对DeepSeek V4的Flash版本进行量化，显著降低了运行门槛，是高效微调与推理框架提供商的典型产品。
*   **[unsloth/Qwen3.6-27B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF)** | 作者: unsloth | 👍 1,057 | ⬇️ 2,905,019
    *   一句话：Unsloth对Qwen 3.6 27B模型应用了其高效的“MTP”(Multi-Token Prediction) 量化技术，在保证性能的同时大幅提升推理速度，下载量接近300万。
*   **[bottlecapai/ThinkingCap-Qwen3.6-27B-GGUF](https://huggingface.co/bottlecapai/ThinkingCap-Qwen3.6-27B-GGUF)** | 作者: bottlecapai | 👍 82 | ⬇️ 312,299
    *   一句话：旨在增强 Qwen 3.6 推理能力的微调模型，其GGUF版本备受社区欢迎，反映了对“Chain-of-Thought”能力的追求。
*   **[yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)** | 作者: yuxinlu1 | 👍 1,158 | ⬇️ 445,368
    *   一句话：针对谷歌Gemma 4模型进行的Agentic能力和编码能力增强微调，其GGUF版本的流行表明开发者正在积极将Google模型应用于自动化与编码场景。
*   **[deepreinforce-ai/Ornith-1.0-35B-GGUF](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B-GGUF)** | 作者: deepreinforce-ai | 👍 855 | ⬇️ 1,347,036
    *   一句话：一个基于 Qwen 架构的35B模型量化版本，证明了中等规模（35B）的MoE模型在量化后拥有极佳的性价比，深受社区欢迎。

---

### **生态信号**

1.  **Qwen 家族成为开源生态“新基石”**：本周榜单中，基于Qwen 3.5/3.6的模型（包括直接原生、微调或量化版本）占据了半壁江山，其强大的MoE架构和开放的许可使得它接替了早期Llama的生态位，成为当前最活跃的模型家族。
2.  **“量化即正义”时代到来**：GGUF格式几乎成为模型流行度的通行证。社区的关注点已从“模型多大”转向“模型在本地能跑多快、多好”。像`unsloth`这样的工具提供商不仅提供了量化服务，更通过技术（如MTP）提升了量化模型的性能，形成了模型生态与工具链的良性循环。
3.  **多模态MoE成为新配置**：纯文本模型的讨论热度在下降，取而代之的是集成视觉能力的模型。同时，MoE（混合专家）架构以其在参数量和性能之间的优秀平衡，已成为新发模型的主流配置，尤其在中文社区非常明显。

---

### **值得探索**

1.  **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)**：如果你对文档处理、信息提取或任何与图像中的文字相关的任务感兴趣，这款模型无疑是当前的选择。其“无限”的特性预示着它能处理从清晰印刷体到复杂场景文字的各种情况，是强大的基础设施。
2.  **[unsloth/Qwen3.6-27B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF)**：如果你希望在消费级硬件上体验顶级多模态推理能力，这个模型是绝佳的选择。它不仅量化得当，还加入了Unsloth最新的推理优化技术，其极高的下载量证明了其出色的综合体验。
3.  **[google/tabfm-1.0.0-pytorch](https://huggingface.co/google/tabfm-1.0.0-pytorch)**：如果你主要处理表格数据（Excel、SQL），这个模型值得深入研究。它代表了AI从处理非结构化数据（文本、图像）向处理结构化数据迈出的重要一步，为自动化数据分析提供了通用基础。

---
*本日报由 [agents-radar](https://github.com/kky-wollu/agents-radar) 自动生成。*
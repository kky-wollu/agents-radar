# Hugging Face 热门模型日报 2026-07-13

> 数据来源: [Hugging Face Hub](https://huggingface.co/) | 共 30 个模型 | 生成时间: 2026-07-12 20:39 UTC

---

好的，作为AI模型生态分析师，以下是根据您提供的2026-07-13数据生成的《Hugging Face 热门模型日报》。

---

### **Hugging Face 热门模型日报 | 2026-07-13**

#### **今日速览**

本周Hugging Face生态活力十足，**MoE（混合专家）架构**和**多模态模型**成为绝对主角。腾讯的`Hy3`、智谱的`GLM-5.2`等原生MoE模型在通用对话领域获得极高关注，而Qwen家族（尤其是3.5/3.6系列）则成为社区微调与量化的首选基座，涌现了大量衍生模型。此外，**NVIDIA**在视觉定位（`LocateAnything-3B`）与端侧推理（`Nemotron`系列）领域持续发力，**Baidu**的通用OCR模型也因其实用性获得了海量下载。量化方面，GGUF格式依然是本地部署的主流选择，Unsloth等团队持续提供高质量的高效推理版本。

---

#### **热门模型**

##### 🧠 语言模型（LLM、对话模型、指令微调）

1.  **[tencent/Hy3](https://huggingface.co/tencent/Hy3)**
    *   作者: tencent | 点赞: 714 | 下载: 8,655
    *   一句话说明：腾讯发布的全新MoE架构对话模型，基于Hunyuan技术栈，在通用文本生成任务上表现优异，是当日热度最高的原生“大厂模型”。

2.  **[zai-org/GLM-5.2](https://huggingface.co/zai-org/GLM-5.2)**
    *   作者: zai-org | 点赞: 3,852 | 下载: 441,413
    *   一句话说明：智谱AI的GLM系列最新版本，采用MoE-DSA架构，以顶尖的对话能力和高周点赞数证明了其在开源社区中的强大号召力。

3.  **[internscience/Agents-A1](https://huggingface.co/InternScience/Agents-A1)**
    *   作者: InternScience | 点赞: 506 | 下载: 29,038
    *   一句话说明：基于Qwen3.5-MoE的智能体模型，专为复杂的工具调用和任务规划场景设计，反映了Agent原生大模型的发展趋势。

4.  **[meituan-longcat/LongCat-2.0](https://huggingface.co/meituan-longcat/LongCat-2.0)**
    *   作者: meituan-longcat | 点赞: 182 | 下载: 1,767
    *   一句话说明：美团推出的长文本对话模型，专注于处理超长上下文场景，是产业界在长窗口LLM应用中的重要探索。

5.  **[nvidia/NVIDIA-Nemotron-Labs-3-Puzzle-75B-A9B-NVFP4](https://huggingface.co/nvidia/NVIDIA-Nemotron-Labs-3-Puzzle-75B-A9B-NVFP4)**
    *   作者: nvidia | 点赞: 111 | 下载: 34,796
    *   一句话说明：NVIDIA推出的75B参数级MoE模型（仅9B活跃参数），并引入了创新的NVFP4精度，兼顾了高性能与更极致的量化效率。

##### 🎨 多模态与生成（图像、视频、音频、文本到X）

1.  **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)**
    *   作者: nvidia | 点赞: 2,714 | 下载: 1,501,653
    *   一句话说明：NVIDIA的通用视觉定位模型，可以识别并定位图像中的任何物体，下载量极高，是当前最热门的“多模态基础模型”之一。

2.  **[baidu/Unlimited-OCR](https://huggingface.co/baidu/Unlimited-OCR)**
    *   作者: baidu | 点赞: 1,941 | 下载: 1,430,656
    *   一句话说明：百度推出的通用OCR模型，支持多种场景的文字识别，凭借其强大的实用性和开源属性，下载量位居前列。

3.  **[CohereLabs/cohere-transcribe-arabic-07-2026](https://huggingface.co/CohereLabs/cohere-transcribe-arabic-07-2026)**
    *   作者: CohereLabs | 点赞: 95 | 下载: 9,860
    *   一句话说明：Cohere Labs推出的阿拉伯语语音识别模型，体现了针对小语种和多语言场景的专业模型正在获得关注。

4.  **[OpenMOSS-Team/MOSS-Transcribe-Diarize](https://huggingface.co/OpenMOSS-Team/MOSS-Transcribe-Diarize)**
    *   作者: OpenMOSS-Team | 点赞: 125 | 下载: 14,491
    *   一句话说明：集成了语音转录和说话人分离（Diarization）的音频转文本模型，是会议记录等场景的优质开源选择。

5.  **[nineninesix/gepard-1.0](https://huggingface.co/nineninesix/gepard-1.0)**
    *   作者: nineninesix | 点赞: 84 | 下载: 2,263
    *   一句话说明：一个新兴的文本转语音（TTS）模型，使用Qwen3.5作为文本编码器，探索了LLM与语音生成结合的新范式。

6.  **[robbyant/lingbot-world-v2-14b-causal-fast](https://huggingface.co/robbyant/lingbot-world-v2-14b-causal-fast)**
    *   作者: robbyant | 点赞: 80 | 下载: 0
    *   一句话说明：探索性的“世界模型”，专注于从图像生成视频（I2V），代表了视频生成领域从“像素预测”向“因果推理”演进的趋势。

##### 🔧 专用模型（代码、数学、医疗、嵌入）

1.  **[google/tabfm-1.0.0-pytorch](https://huggingface.co/google/tabfm-1.0.0-pytorch)**
    *   作者: google | 点赞: 354 | 下载: 20,973
    *   一句话说明：Google发布的表格数据基础模型，支持零样本分类与回归，为表格数据领域带来了“预训练+微调”的全新范式。

2.  **[SupraLabs/Supra-Router-51M](https://huggingface.co/SupraLabs/Supra-Router-51M)**
    *   作者: SupraLabs | 点赞: 105 | 下载: 1,434
    *   一句话说明：一个轻量级（51M）的路由器模型，主要用于MoE架构的专家选择或模型集成，是MoE生态中关键的“基础设施”。

##### 📦 微调与量化（社区微调、GGUF、AWQ）

1.  **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)**
    *   作者: empero-ai | 点赞: 2,039 | 下载: 1,967,677
    *   一句话说明：基于Qwen3.5的GGUF量化版“神话”型微调模型，下载量近200万，是社区高质量微调成果与大范围本地部署结合的典范。

2.  **[HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive](https://huggingface.co/HauhauCS/Qwen3.6-35B-A3B-Uncensored-HauhauCS-Aggressive)**
    *   作者: HauhauCS | 点赞: 2,671 | 下载: 2,596,384
    *   一句话说明：Qwen3.6的35B MoE模型（3B活跃参数）去审查版，下载量巨大，反映了社区对“无限制”内容和高效推理性能的强劲需求。

3.  **[yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF](https://huggingface.co/yuxinlu1/gemma-4-12B-agentic-fable5-composer2.5-v2-3.5x-tau2-GGUF)**
    *   作者: yuxinlu1 | 点赞: 1,158 | 下载: 445,368
    *   一句话说明：专为编程和终端Agent场景微调的Gemma-4模型GGUF版，是“编程助手”类模型在本地布局的热门选择。

4.  **[deepreinforce-ai/Ornith-1.0-35B-GGUF](https://huggingface.co/deepreinforce-ai/Ornith-1.0-35B-GGUF)**
    *   作者: deepreinforce-ai | 点赞: 855 | 下载: 1,347,036
    *   一句话说明：一个35B规模的通用文本生成模型GGUF版，下载量超过130万，是“非知名团队”通过高质量量化实现“逆袭”的典型案例。

5.  **[unsloth/Qwen3.6-27B-MTP-GGUF](https://huggingface.co/unsloth/Qwen3.6-27B-MTP-GGUF)**
    *   作者: unsloth | 点赞: 1,057 | 下载: 2,905,019
    *   一句话说明：Unsloth团队提供的Qwen3.6-27B模型MTP（Multi-Token Prediction）版本GGUF量化，以行业领先的推理速度和极高的下载量，巩固了其在量化领域的领先地位。

---

#### **生态信号**

本周生态呈现三大趋势：第一，**“大厂”与“社区”双轮驱动，MoE全面开花**。腾讯、智谱、NVIDIA、InternScience等团队的MoE模型（`Hy3`， `GLM-5.2`, `Nemotron`, `Agents-A1`）在基础能力上持续迭代，同时社区基于Qwen系列进行的MoE微调（`HauhauCS/Qwen3.6-35B-A3B`）极为活跃，MoE已成为一线模型与社区微调的事实标准。第二，**Qwen3.5/3.6成为“开源基座之王”**。从榜单可以看出，超过一半的模型直接或间接基于Qwen家族，其强大的性能、开放的许可证及优秀的MoE设计，使其成为社区进行推理增强、多模态融合和二次微调的首选平台。第三，**量化质量与效率的新竞赛**。GGUF不再是简单的“缩小”模型，Unsloth的MTP版本、NVIDIA的NVFP4精度、以及复杂的混合标签模型（如`gemma-4-12B-agentic...`）表明，量化技术正向着“保留更多推理能力并提升特定场景性能”的精细化方向发展。

---

#### **值得探索**

1.  **[nvidia/LocateAnything-3B](https://huggingface.co/nvidia/LocateAnything-3B)**: 强烈推荐。它展示了多模态模型在“精确感知”方面的巨大潜力。3B的小巧体积与强大的“万物定位”能力结合，使其在机器人、自动驾驶、工业质检等real-world场景中具有极高的应用价值，是“纯视觉基础模型”的绝佳实践。

2.  **[google/tabfm-1.0.0-pytorch](https://huggingface.co/google/tabfm-1.0.0-pytorch)**: 值得关注。它标志着AI的“香农型”任务——结构化表格数据——终于迎来了自己的“Transformer时刻”。如果你日常工作涉及大量特征工程和表格预测，这个模型将极大改变你的工作流，是少见的“非LLM”但极具变革性的模型。

3.  **[empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF](https://huggingface.co/empero-ai/Qwythos-9B-Claude-Mythos-5-1M-GGUF)**: 值得一试。它代表了社区微调的最高水平。虽然名为“Claude-Mythos”，但其本质是对Qwen3.5能力的深度挖掘与风格化改造。你可以在本地轻松运行，体验最前沿的社区“炼丹”成果，是了解当前开源模型能力边界的绝佳入口。

---
*本日报由 [agents-radar](https://github.com/kky-wollu/agents-radar) 自动生成。*
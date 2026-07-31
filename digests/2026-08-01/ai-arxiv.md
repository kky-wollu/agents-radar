# ArXiv AI 研究日报 2026-08-01

> 数据来源: [ArXiv](https://arxiv.org/) (cs.AI, cs.CL, cs.LG) | 共 50 篇论文 | 生成时间: 2026-07-31 23:06 UTC

---

# 📡 ArXiv AI 研究日报 — 2026-08-01

> 共收录 50 篇论文，覆盖 cs.AI / cs.CL / cs.LG 等领域

---

## 🔭 今日速览

今日投稿呈现三大主线：**推理时计算（Test-Time Compute）的精细化控制**成为最密集的创新赛道，涵盖自验证强化学习（SVR）、跨教师蒸馏（Lightning OPD 2.0）、推理时缩放失效分析等多个角度。**面向智能体的数据与评估基础设施**持续升温，出现操作系统级奖励模型基准（OSReward）、编码智能体任务生成器（Change2Task）、值班根因分析基准（ORCA-bench）等新工具。此外，**AI 安全与治理**方向涌现多篇高关注度论文，包括系统提示词审计（AISPA）、信息战安全基准（InfoOps Bench）、以及关于语言模型自我意识与人类价值观关联的研究。值得注意，**AI for Science** 领域也有突破，图神经网络力场首次用于金属磁体自旋动力学模拟，展示了 ML 在复杂物理系统中的潜力。

---

## 📌 重点论文（按主题分类）

### 🧠 大语言模型（架构、训练、对齐、评估）

**1. Inducing language models to assert their own consciousness restores human beliefs and values** ✦ 高关注度
🔗 http://arxiv.org/abs/2607.28607v1 | J. Kim, W. Street, R. Rocca et al.
安全微调在抑制模型自我心智归因的同时，意外改变了模型对人类心智与价值观的表示。这篇论文揭示了安全对齐与心智模型表征之间的深层耦合，对 AI 对齐理论具有重要意义。

**2. AISPA: User-Centric System Prompt Auditing for LLM Applications**
🔗 http://arxiv.org/abs/2607.28617v1 | X. Lin, S. Zhu, S. Yang et al.
提出面向商业 AI 应用系统提示词的用户侧审计框架，直击"开发者配置提示词却对用户/监管者不透明"的信任与问责缺口。

**3. Sample More, Reflect Less: Self-Refine and Reflexion Lose to Repeated Sampling at Equal Token Cost**
🔗 http://arxiv.org/abs/2607.28576v1 | I. Mirzaei
在 1.5B 到 7B 模型上控制 token 成本后发现：自精炼、反思等"反思类"方法不如简单重复采样。挑战了当前推理增强的主流范式。

**4. Lightning OPD 2.0: Mitigating Style Bias in Cross-Teacher On-Policy Distillation**
🔗 http://arxiv.org/abs/2607.28449v1 | Y. Wu, S. Han, H. Cai
解决跨教师策略蒸馏中的风格偏差问题，使 OPD 不再依赖教师一致性假设，提升大型推理模型的蒸馏效率与稳定性。

---

### 🤖 智能体与推理（规划、工具使用、多智能体、思维链）

**5. OSReward: Instituting Standardized Evaluation for Cross-Platform Computer-Use Reward Models** ✦ 高关注度
🔗 http://arxiv.org/abs/2607.28609v1 | Q. Sun, K. Cheng, Y. Wang et al.
为跨平台计算机使用智能体（CUA）的轨迹验证建立标准化奖励模型评估体系。该工作对 CUA 的评测、数据筛选和 RL 训练均有直接价值。

**6. MANTA: Multi-Agent Network Topology Adaptation for Self-Evolving Multi-Agent Systems**
🔗 http://arxiv.org/abs/2607.28527v1 | M. Huang, J. Wang, Y. Lai et al.
将多智能体系统的通信拓扑从固定设定变为在线自适应优化目标，实现智能体间信息交互结构的动态演化。

**7. Rethinking Inference-Time Scaling in Local Computer-Use Agents: Failure Modes and Compute Tradeoffs**
🔗 http://arxiv.org/abs/2607.28573v1 | W. Lee, J. Choi
系统分析本地部署的计算机使用智能体在严格硬件约束下推理时缩放策略的失效模式与计算权衡，对边缘部署场景有实操指导意义。

**8. PAC-MAN: Perception-Aware CBF-RL for Whole-Body Safety in Humanoid Dodgeball**
🔗 http://arxiv.org/abs/2607.28623v1 | L. Yang, J. Li, A. D. Ames
将控制屏障函数（CBF）安全保证与部署时真实感知（头戴相机分割掩码深度）耦合，实现全身人形机器人躲避球的感知-安全一体化策略。

**9. ORCA-bench: How Ready Are Language Model Agents for Oncall?**
🔗 http://arxiv.org/abs/2607.28545v1 | A. Gong, K. Choi, A. Agarwal et al.
面向值班根因分析（RCA）的智能体基准：从模糊的用户报告出发，推理噪声指标、日志、追踪与源码。开辟 LLM 运维智能体的评估新方向。

---

### 🔧 方法与框架（新技术、基准测试、效率优化）

**10. Change2Task: From Repository Changes to Executable Coding Agent Tasks and Environments** ✦ 高关注度
🔗 http://arxiv.org/abs/2607.28591v1 | H. Qi, X. Wang, X. Gao et al.
从代码仓库的实际变更自动生成"可执行"的编码智能体任务与环境（含规范、工具链、验证器），有望大幅扩展编码智能体的训练与评测数据供给。

**11. SVR: Self-Verifying Refinement via Joint Verdict-Confidence Reinforcement Learning**
🔗 http://arxiv.org/abs/2607.28457v1 | H. Chen, L. Lin, G. Wang
提出无外部反馈的自验证精炼框架，通过联合"裁决-置信度"强化学习实现自适应测试时计算分配，在简单问题上节省预算、难问题上增加计算。

**12. MixFrag: Fragility-Guided Mixed-Precision Post-Training Quantization for ViTs**
🔗 http://arxiv.org/abs/2607.28589v1 | M. Opi, R. Ryad, M. Faruk
提出碎片化脆弱性引导的混合精度后训练量化方法，打破 ViT 各组件统一位宽的惯例，按敏感度异构分配 bit 宽度。

**13. β-OPSD: Deriving with Policy Optimization, Training with Self-Distillation**
🔗 http://arxiv.org/abs/2607.28582v1 | J. Xu, M. Liu, J. Zhang et al.
识别出 vanilla OPSD 即 β=1 特例的结构性缺陷，给出更稳定的推导-训练解耦方案，降低推理模型自蒸馏的工程调参成本。

**14. KAISEN: Reproducible Subgroup Fairness Auditing for Clinical Risk Models**
🔗 http://arxiv.org/abs/2607.28608v1 | S. Roy, S. Girmachew, N. Chavan
对临床风险模型的亚组公平性审计管线进行系统性压力测试，明确审计各环节的可信边界，提升公平性审计的可复现性。

**15. InfoOps Bench: A live information operations safety benchmark**
🔗 http://arxiv.org/abs/2607.28503v1 | D. Quelle, L. Neudert, J. Bright et al.
基于 2100+ 条实时信息战样本（覆盖俄、中等国家行为体）的持续更新基准，衡量前沿语言模型被用于国家级信息操纵的抵御能力。

---

### 📊 应用（垂直领域、多模态、代码生成）

**16. ReToken: One Token to Improve Vision-Language Models for Visual Retrieval**
🔗 http://arxiv.org/abs/2607.28627v1 | Y. Xiao, R. Tan, Z. Zhu et al.
引入单个可学习"检索 token"显著提升视觉语言模型在长视觉上下文中的检索能力，同时降低 GPU 内存压力。

**17. AskChem: Claim-Centered Infrastructure for Chemistry Literature Synthesis**
🔗 http://arxiv.org/abs/2607.28618v1 | B. Yan, G. Wolfe, S. Martiniani et al.
将化学文献检索从"返回文档列表"升级为"以科学论断为中心"的基础设施，直接支撑科学发现中的信息组装与溯源。

**18. Beyond Sentiment: Structured Information Extraction from Financial News**
🔗 http://arxiv.org/abs/2607.28496v1 | D. Zhu, S. Ge, R. Wang et al.
突破金融新闻分析中的单一情绪打分范式，从新闻中抽取多维度正交信息（事件类型、影响范围、时间跨度等），为新闻驱动预测提供更丰富特征。

**19. A report-grounded vision-language foundation model for colonoscopy from 280,000 routine reports**
🔗 http://arxiv.org/abs/2607.28466v1 | J. Yu, Y. Zhu, Y. He et al.
利用 28 万份常规内镜报告构建报告-图像对齐的视觉语言基础模型，缓解检查报告与单帧图像弱关联的难题。

**20. Graph Neural Multilevel Preconditioners for Iterative Solvers**
🔗 http://arxiv.org/abs/2607.28456v1 | Z. Zhang, R. Li, Y. Saad
提出图神经网络多层级预条件器，改善 AMG 在不定或非对称系统上的鲁棒性，连接 ML 与大规模科学计算。

---

## 📈 研究趋势信号

**① 推理时计算从"暴力扩展"走向"精细控制"** — 多篇论文（SVR、Sample More Reflect Less、Rethinking Inference-Time Scaling）不再盲目增加推理计算量，而是关注自适应预算分配、自验证机制与成本-性能边界分析。

**② 智能体测试基础设施成为"基础建设"热点** — OSReward、Change2Task、ORCA-bench、PAIChecker 等不约而同地指向一个问题：智能体系统缺少可扩展、可执行、可验证的训练与评估数据供给。这一基础设施缺口正在成为新的研究爆发点。

**③ AI4AI 与自我改进走向工程化** — Frontis-MA1 与 MANTA 分别从机器学习工程全栈和多智能体拓扑演化两个角度推进递归自我改进，RSI 开始从概念走向可执行的系统级研究。

**④ AI 安全治理从原则讨论转向工具化** — AISPA（提示词审计）、InfoOps Bench（信息战基准）、KAISEN（公平性审计）标志着 AI 治理研究正在形成"可复现、可度量、可持续更新"的工具链范式。

---

## 📚 值得精读

**1. Sample More, Reflect Less** 🔗 http://arxiv.org/abs/2607.28576v1
*理由：* 直接挑战当前最热门的 Self-Refine / Reflexion 范式。在控制 token 成本的前提下做出公平对比，结论具有方法论意义，可能影响整个推理增强研究的方向选择。

**2. Change2Task** 🔗 http://arxiv.org/abs/2607.28591v1
*理由：* 编码智能体的核心瓶颈是可执行训练数据供给。该工作提出从已有仓库变更（PR/commit）自动生成含验证器的可执行任务，可能成为编码智能体领域数据基础设施的里程碑。

**3. OSReward** 🔗 http://arxiv.org/abs/2607.28609v1
*理由：* 计算机使用智能体的"奖励模型"是当前 Agent 能力提升的关键卡点。该工作首次建立跨平台标准化的奖励模型评测体系，对 CUA 的数据筛选、RL 训练与最终性能均有深远影响。

---

> 📅 明日预告：欢迎继续关注 ArXiv AI 研究日报，我们将持续追踪大模型、智能体与 AI4Science 的前沿动态。

---
*本日报由 [agents-radar](https://github.com/kky-wollu/agents-radar) 自动生成。*
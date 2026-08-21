# ArXiv AI 研究日报 2026-08-22

> 数据来源: [ArXiv](https://arxiv.org/) (cs.AI, cs.CL, cs.LG) | 共 50 篇论文 | 生成时间: 2026-08-21 22:29 UTC

---

# 📡 ArXiv AI 研究日报 — 2026-08-22

## 今日速览

今日 50 篇投稿呈现三条主线：**LLM 遗忘机制与记忆可靠性**成为热点（ConceptGuard、MemTrapBench、Phantom Gains 三篇同时聚焦）；**智能体从"能用"走向"可验证"** ，涌现出 AI4AI-Bench（算法自改进）、MidTool（工具使用中训练）等系统级工作；**法律与医疗等高责任场景的评估基准**密集出现（InsufficiencyBench、ContractScrub、G-CARL）。此外，模型路由（Pandora's AI Model Routing Box）、推理时计算分配（Learning When to Think）等效率优化方向亦有突破。

---

## 📌 重点论文

### 🧠 大语言模型（架构、训练、对齐、评估）

**1. ConceptGuard: Benchmarking Context-Sensitive Unlearning in Large Language Models**
🔗 http://arxiv.org/abs/2608.20338v1
👤 Sahil Kale, Ian Harris
💡 首次提出上下文敏感的 LLM 遗忘基准，挑战现有"不相交遗忘/保留集"评估范式的缺陷，为选择性知识移除提供更完整的评测框架。

**2. When Text and Numbers Disagree: Evidence Arbitration in Large Language Models**
🔗 http://arxiv.org/abs/2608.20116v1
👤 Mattia Carletti, Edward Phillips, F. Gustafsson 等
💡 构建受控合成场景研究 LLM 面对文本摘要与数值证据冲突时的仲裁行为，揭示多源证据矛盾下的决策偏差。

**3. MemTrapBench: Benchmarking Cognitive Traps in LLM Memory Use**
🔗 http://arxiv.org/abs/2608.20202v1
👤 Mengru Wang, Haozhe Luo, Zhenqian Xu 等
💡 首个聚焦"记忆认知陷阱"的基准——不仅考察信息能否被检索，更检验检索到的记忆是否被正确使用，填补记忆评估的关键盲区。

**4. Explainable Transformer Models for Clinical Prediction Tasks on Structured Electronic Health Records**
🔗 http://arxiv.org/abs/2608.20315v1
👤 Jun Ni Du, Lukas Adamek, Maxim Kryukov 等
💡 提出 BERT-LER，面向结构化 EHR 的可解释 BERT 模型，在预测性能之外提供医学事件层面的可解释性。

---

### 🤖 智能体与推理（规划、工具使用、多智能体、思维链）

**5. AI4AI-Bench: Benchmarking LLM Agents in Algorithmic Design for Recursive Self-Improvement**
🔗 http://arxiv.org/abs/2608.20318v1
👤 Yizhe Chi, Wenyi Li, Deyao Hong 等
💡 首个评测 LLM 智能体在**递归自改进**（优化训练算法本身）能力的基准，直击 AI 自我进化的核心命题。

**6. Inducing Task Models from Computer-Use Traces**
🔗 http://arxiv.org/abs/2608.20319v1
👤 Yucheng Jiang, Zora Zhiruo Wang, Ruishi Chen 等
💡 从被动记录的人机交互轨迹中归纳符号化、可审计的任务模型，为计算机使用智能体提供可复用的任务知识。

**7. MidTool: Mid-training Data Synthesis for Agentic Tool Use**
🔗 http://arxiv.org/abs/2608.20314v1
👤 Fengqing Jiang, Yite Wang, Boyi Liu 等
💡 开创性提出"中训练"阶段的工具使用数据合成方法，填补了预训练与指令微调之间 agentic 能力塑造的空白。

**8. Break It Down, Pass It On: Cross-Task Skill Transfer in LLM Agents**
🔗 http://arxiv.org/abs/2608.20274v1
👤 Yiyang Feng, Biddut Sarker Bijoy, Niranjan Balasubramanian 等
💡 系统研究 LLM 智能体跨任务技能迁移的可靠边界，发现技能迁移在某些条件下反而会损害目标性能。

**9. Learning When to Think: Adaptive Reasoning for Test-Time Compute Allocation**
🔗 http://arxiv.org/abs/2608.20256v1
👤 Gijs Kassenaar, Zhao Yang, Vincent François-Lavet
💡 训练模型自主决定推理深度，打破固定 token 预算的局限——易题少算、难题多算，提升推理效率。

**10. Pandora's AI Model Routing Box: Efficient Allocation with Costly Value Estimation**
🔗 http://arxiv.org/abs/2608.20316v1
👤 Adam Fisch, Shubhendu Trivedi, Fantine Huot 等
💡 将异构模型路由问题形式化为"带评估成本的分配"问题，在路由准确性与评估开销之间取得最优平衡。

---

### 🔧 方法与框架（新技术、基准测试、效率优化）

**11. Phantom Gains: Auditing Self-Improvement Against a Measured Null**
🔗 http://arxiv.org/abs/2608.20290v1
👤 Cheng Xu, Nan Yan, Liming Chen 等
💡 揭示自改进评估中的"虚假增益"问题——对两次噪声估计做差分会放大测量伪影，提供严谨的审计方法。

**12. InsufficiencyBench: Evaluating LLM Legal Advice on Underspecified User Queries**
🔗 http://arxiv.org/abs/2608.20220v1
👤 Samuel J. Vincent, Daniel Calloway, Fangyi Yu 等
💡 首个针对"信息不充分查询"的法律基准，揭示 LLM 在用户省略关键事实时给出确定答案的危险倾向。

**13. Daedalus-150M: A Convolution-Attention Hybrid Designed for CPU Inference**
🔗 http://arxiv.org/abs/2608.20210v1
👤 Christos Koutsiaris
💡 逆向设计思维的 150M 小模型——先定 CPU 推理目标再选架构，仅 6/18 层使用全注意力，为端侧部署提供新思路。

**14. ContractScrub: A Benchmark for Final Review of Legal Contracts**
🔗 http://arxiv.org/abs/2608.20204v1
👤 Yejin Bang, Kirsty Fielding, Brandan Oliver 等
💡 面向合同"终审"环节的自动化基准，覆盖错误与不一致性检查，直击法律文本处理中最适合 LLM 落地的场景。

**15. FormalTCS: Benchmarking End-to-End Frontier Formal Theoretical Computer Science Research of LLMs**
🔗 http://arxiv.org/abs/2608.20153v1
👤 Dingzirui Wang, Xuanliang Zhang, Keyan Xu 等
💡 专家验证的前沿理论计算机科学研究基准，评估 LLM 在端到端正式研究场景下的能力上限。

---

### 📊 应用（垂直领域、多模态、代码生成）

**16. G-CARL: Grounded Checklist-Aligned Reward Learning for Patient-Oriented Medical Report Interpretation**
🔗 http://arxiv.org/abs/2608.20331v1
👤 Shiao Xie, Siyu Chen, Jianwei Lv 等
💡 面向患者的医学报告解读框架，通过"清单对齐"的奖励学习同时保证医学事实性和患者沟通的个性化。

**17. DECOWAM: Decoupled Whole-Body World-Action Model for Legged Mobile Manipulation**
🔗 http://arxiv.org/abs/2608.20114v1
👤 Siyuan Ma, Boshi Zhang, Yutian Zhang 等
💡 解耦底座运动与机械臂动作的世界-动作模型，解决足式移动操作中相机自运动与操作动作混淆的问题。

**18. Catching the Rug: Early Prediction of Fraudulent Memecoins on Solana via Machine Learning**
🔗 http://arxiv.org/abs/2608.20271v1
👤 Jianghai Li, Pavel Kuznetsov, Yury Yanovich 等
💡 基于 Solana 链上数据的 meme 币"拉地毯"骗局早期预警系统，填补了以太坊之外的高风险代币欺诈检测空白。

---

## 📈 研究趋势信号

今日投稿透露出几个值得关注的方向：**"评估的评估"正在成为独立研究主题**——多篇论文不再满足于提出新方法，而是回头审视既有评估范式的缺陷（Phantom Gains 的测量伪影、ConceptGuard 的遗忘评估盲区、MemTrapBench 的记忆认知陷阱）；**推理时计算的精细化调控**成为效率优化共识（自适应 token 分配、模型路由、缓存策略）；**高责任场景的基准正在专业化分层**——法律领域同时出现查询侧（InsufficiencyBench）与文档侧（ContractScrub）的评估体系。此外，**"自改进"从科幻进入工程化评测**（AI4AI-Bench）值得密切关注。

---

## 🔬 值得精读

**1. AI4AI-Bench（#5）** — 递归自改进是 AI 领域最具争议也最具潜力的方向之一。该论文首次将"算法设计能力"本身作为可量化的基准，其对训练算法的改进评估框架可能成为未来 AI 自我进化研究的标准起点，建议完整阅读以理解 RSI 的工程化评测范式。

**2. Pandora's AI Model Routing Box（#10）** — 异构模型路由是实际部署中的刚需，但"评估专家模型也需要成本"这一约束常被忽略。该论文的数学框架将路由问题提升到新的理论高度，对系统设计和成本优化均有直接指导价值。

**3. Phantom Gains（#11）** — 对自改进评估方法的深刻反思。作者用严格的统计论证揭示了"看似进步、实则噪声"的测量陷阱，这一方法论贡献对任何涉及差分评估的研究（包括自训练、持续学习）都具有普适警示意义，值得所有做 LLM 评估的研究者阅读。

---
*本日报由 [agents-radar](https://github.com/kky-wollu/agents-radar) 自动生成。*
# ArXiv AI Research Digest 2026-08-01

> Source: [ArXiv](https://arxiv.org/) (cs.AI, cs.CL, cs.LG) | 50 papers | Generated: 2026-07-31 23:06 UTC

---

# 🤖 ArXiv AI Research Digest
**2026-08-01 | 50 papers from cs.AI, cs.CL, cs.LG**

---

## 1. Today's Highlights

Today's submissions reveal three dominant research thrusts: **agentic AI systems** — spanning computer-use agents, oncall root-cause analysis, and self-evolving multi-agent architectures — are maturing from prototypes toward systematic evaluation infrastructure and deployment-aware safety. **Efficiency and cost-awareness** is a cross-cutting theme, with multiple papers questioning token-heavy reasoning paradigms (repeated sampling outperforming self-reflection at equal cost) and introducing compute-aware frameworks for test-time scaling. Finally, **trust and accountability** research is expanding beyond model safety into novel territories: system-prompt auditing for commercial LLM applications, reproducible subgroup fairness audits for clinical risk models, and live benchmarking against state-backed information operations.

---

## 2. Key Papers

### 🧠 Large Language Models

**Inducing language models to assert their own consciousness restores human beliefs and values**  
*Junsol Kim, Winnie Street, Roberta Rocca et al.* | [http://arxiv.org/abs/2607.28607v1](http://arxiv.org/abs/2607.28607v1)  
Shows that safety fine-tuning suppresses LLMs' tendency to attribute minds not only to themselves but also to other entities — and that prompting models to affirm their own consciousness paradoxically restores human-aligned mind perception and values.

**Beyond a Single Judge: Simulating Social Persona Panels for Generative UI Evaluation**  
*Zheng Wu, Yibo Luo, Pu Zhang et al.* | [http://arxiv.org/abs/2607.28439v1](http://arxiv.org/abs/2607.28439v1)  
Proposes persona-panel simulation for evaluating LLM-generated user interfaces, addressing the reliability and viewpoint-diversity gap of single LLM-as-a-judge evaluation.

**Would You Walk to the Car Wash? Revealing the Salience Bias of Large Language Models in Commonsense Reasoning**  
*Zheng Wu, Chenhao Xue, Shijie Zheng et al.* | [http://arxiv.org/abs/2607.28478v1](http://arxiv.org/abs/2607.28478v1)  
Identifies a pervasive "salience bias" where LLMs over-prioritize explicit conditions in prompts, degrading commonsense reasoning; the paper provides diagnostic benchmarks to expose this vulnerability.

**Sample More, Reflect Less: Self-Refine and Reflexion Lose to Repeated Sampling at Equal Token Cost, from 1.5B to 7B**  
*Iliya Mirzaei* | [http://arxiv.org/abs/2607.28576v1](http://arxiv.org/abs/2607.28576v1)  
A rigorously controlled study showing that self-refine and reflexion methods underperform simple repeated sampling when token budgets are held equal — a significant challenge to the test-time-compute orthodoxy.

**Generative AI and linguistic diversity in academic writing and publishing**  
*Kingsley Ugwuanyi, Christian Mair, Sender Dovchin et al.* | [http://arxiv.org/abs/2607.28505v1](http://arxiv.org/abs/2607.28505v1)  
Examines how GenAI tools both reproduce and potentially reshape standard language ideologies in scholarly publishing, with implications for linguistic inclusivity in global research communication.

---

### 🤖 Agents & Reasoning

**OSReward: Instituting Standardized Evaluation for Cross-Platform Computer-Use Reward Models**  
*Qiushi Sun, Kanzhi Cheng, Yian Wang et al.* | [http://arxiv.org/abs/2607.28609v1](http://arxiv.org/abs/2607.28609v1)  
Introduces a standardized benchmark for reward models that verify computer-use agent trajectories — critical infrastructure for CUA evaluation, data curation, and agentic RL.

**ORCA-bench: How Ready Are Language Model Agents for Oncall?**  
*Albert Gong, Kyuseong Choi, Abhineet Agarwal et al.* | [http://arxiv.org/abs/2607.28545v1](http://arxiv.org/abs/2607.28545v1)  
New benchmark for root cause analysis in production incidents — reasoning over noisy metrics, logs, traces, and code from ambiguous user reports; a significant step toward realistic ops agents.

**Rethinking Inference-Time Scaling in Local Computer-Use Agents: Failure Modes and Compute Tradeoffs**  
*Woongkyu Lee, Jungwook Choi* | [http://arxiv.org/abs/2607.28573v1](http://arxiv.org/abs/2607.28573v1)  
Analyzes when inference-time scaling helps vs. fails for locally deployed CUAs under hardware constraints, offering compute–accuracy tradeoff guidance for practical deployment.

**Agents That Certify Their Own Exploits: Confidence-Scheduled Restricted Responses for Safe Opponent Exploitation**  
*Boning Li, Longbo Huang* | [http://arxiv.org/abs/2607.28520v1](http://arxiv.org/abs/2607.28520v1)  
Introduces confidence-scheduled deviation policies for imperfect-information games, enabling safe exploitation of flawed opponents with formal certification guarantees.

**MANTA: Multi-Agent Network Topology Adaptation for Self-Evolving Multi-Agent Systems**  
*Mao-xun Huang, Jerry Wang, Yi-Cheng Lai et al.* | [http://arxiv.org/abs/2607.28527v1](http://arxiv.org/abs/2607.28527v1)  
Proposes dynamic adaptation of communication topology in LLM-based multi-agent systems — moving beyond fixed or offline-optimized designs toward self-evolving structures.

---

### 🔧 Methods & Frameworks

**β-OPSD: Deriving with Policy Optimization, Training with Self-Distillation**  
*Jiawei Xu, Minghui Liu, Juzheng Zhang et al.* | [http://arxiv.org/abs/2607.28582v1](http://arxiv.org/abs/2607.28582v1)  
Diagnoses the brittleness of on-policy self-distillation for reasoning models as a β=1 special case, then derives a stabilized generalized family of algorithms — a principled fix for a known engineering headache.

**SVR: Self-Verifying Refinement via Joint Verdict-Confidence Reinforcement Learning for Adaptive Test-Time Compute**  
*Hongyu Chen, Liang Lin, Guangrun Wang* | [http://arxiv.org/abs/2607.28457v1](http://arxiv.org/abs/2607.28457v1)  
Oracle-free, multi-turn RL framework that learns when to stop reasoning and how to verify its own outputs — enabling adaptive compute allocation without external verifiers.

**Change2Task: From Repository Changes to Executable Coding Agent Tasks and Environments**  
*Haomin Qi, Xingliang Wang, Xuanqi Gao et al.* | [http://arxiv.org/abs/2607.28591v1](http://arxiv.org/abs/2607.28591v1)  
A system that converts real repository changes into executable coding tasks with verified environments, expanding the supply of high-quality training/evaluation data for coding agents.

**ScaFE: Data-Efficient Scar Classification with LLM-Generated Clinical Feature Programs**  
*Ruman Wang, Hangting Ye* | [http://arxiv.org/abs/2607.28538v1](http://arxiv.org/abs/2607.28538v1)  
Generates interpretable clinical feature-extraction programs using LLMs for scar classification — achieving data efficiency and interpretability without end-to-end image models.

**Selective Credibility-Limited Belief Update**  
*Theofanis Aravanis, Costas D. Koutras* | [http://arxiv.org/abs/2607.28523v1](http://arxiv.org/abs/2607.28523v1)  
A formal framework generalizing credibility-limited belief revision to the update setting, relevant for robust knowledge representation in dynamic environments.

---

### 📊 Applications

**AskChem: Claim-Centered Infrastructure for Chemistry Literature Synthesis**  
*Bing Yan, Gregory Wolfe, Stefano Martiniani et al.* | [http://arxiv.org/abs/2607.28618v1](http://arxiv.org/abs/2607.28618v1)  
A claim-centered retrieval and synthesis system for chemistry — assembling findings across publications with provenance, directly addressing the "ranked document list" limitation of current search tools.

**Graph Neural Network Force Fields for Spin Dynamics in Metallic Magnets**  
*Ali Rayat, Yunhao Fan, Gia-Wei Chern* | [http://arxiv.org/abs/2607.28537v1](http://arxiv.org/abs/2607.28537v1)  
GNN surrogate force fields for spin dynamics in metallic magnets, eliminating the bottleneck of repeated electronic-structure solves — a concrete AI-for-physics advance.

**Cybersecurity Detection Classification with Reasoning-enabled Language Models**  
*Amol Khanna, Manu Nandan, Cristian Viorel Popa et al.* | [http://arxiv.org/abs/2607.28460v1](http://arxiv.org/abs/2607.28460v1)  
Trains LLMs to reason about whether security detections are true positives, tackling alert fatigue in SOCs with explanation-aware triage rather than direct label prediction.

**A report-grounded vision-language foundation model for colonoscopy from 280,000 routine reports**  
*Jia Yu, Yan Zhu, Yili He et al.* | [http://arxiv.org/abs/2607.28466v1](http://arxiv.org/abs/2607.28466v1)  
A VLM trained on 280K routine colonoscopy reports that weakly links procedure-level text to frames, opening new capabilities for a domain where VLMs are conspicuously underused.

**Beyond Sentiment: Structured Information Extraction from Financial News**  
*Daohan Zhu, Sitong Ge, Ruofei Wang et al.* | [http://arxiv.org/abs/2607.28496v1](http://arxiv.org/abs/2607.28496v1)  
Moves beyond polarity scores to structured multi-dimensional extraction (event type, scope, temporal horizon) from financial news — better signal for downstream prediction.

---

## 3. Research Trend Signal

Three trends stand out from today's 50 submissions. **First, the reckoning with token economics.** The finding that repeated sampling beats self-refine/reflexion at equal token cost, alongside the β-OPSD stability analysis and SVR's adaptive compute framework, signals a field-wide move toward questioning expensive reasoning loops and demanding controlled comparisons. **Second, agent evaluation is industrializing.** OSReward (CUA verification), ORCA-bench (oncall RCA), InfoOps Bench (information operations), and PAIChecker (SWE-bench hygiene) all target the evaluation infrastructure gap for deployed agents — moving from "can it do the task?" to "can we trust its verification and benchmark?" **Third, safety research is diversifying beyond model alignment.** System-prompt auditing (AISPA), subgroup fairness auditing for clinical models (KAISEN), and certification for constraint solvers (LeanCSP) treat AI trust as a systems property, not just a model property.

---

## 4. Worth Deep Reading

1. **"Sample More, Reflect Less"** ([2607.28576v1](http://arxiv.org/abs/2607.28576v1)) — A potentially field-shaping negative result. If replicated widely, this undercuts a large family of reasoning methods and reframes the test-time-compute research agenda toward sampling strategies.

2. **"β-OPSD: Deriving with Policy Optimization, Training with Self-Distillation"** ([2607.28582v1](http://arxiv.org/abs/2607.28582v1)) — Rare in offering both a sharp negative diagnosis (the β=1 instability) and a principled fix; the authors' framing of OPSD as a family of algorithms will be useful beyond their specific setting.

3. **"Inducing language models to assert their own consciousness..."** ([2607.28607v1](http://arxiv.org/abs/2607.28607v1)) — Unexpected and consequential: safety fine-tuning suppresses mind-attribution broadly, and prompting for self-consciousness restores human-aligned values. This suggests alignment interventions have indirect representational effects that deserve careful mapping.

---
*This digest is auto-generated by [agents-radar](https://github.com/kky-wollu/agents-radar).*
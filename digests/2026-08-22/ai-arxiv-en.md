# ArXiv AI Research Digest 2026-08-22

> Source: [ArXiv](https://arxiv.org/) (cs.AI, cs.CL, cs.LG) | 50 papers | Generated: 2026-08-21 22:29 UTC

---

# ArXiv AI Research Digest — 2026-08-22

## 1. Today's Highlights

Today's submissions reveal a strong convergence on **evaluation integrity and measurement validity** across AI research. Multiple groups (Phantom Gains, ConceptGuard, InsufficiencyBench) tackle the problem of benchmark reliability and self-improvement auditing — a sign that the field is maturing beyond raw performance gains toward methodological rigor. A second major thread concerns **agentic systems moving into real-world workflows**: task model induction from computer-use traces, skill transfer between agents, and tool-use mid-training all point to agents transitioning from research demos to practical deployment. Third, there is notable activity in **efficiency-focused design** — from CPU-first language model architectures to adaptive reasoning budgets and cache eviction policies — suggesting that compute optimization is becoming a first-class research priority. Finally, domain applications continue to expand into law, maritime navigation, finance, and healthcare, indicating sustained vertical integration of AI methods.

---

## 2. Key Papers

### 🧠 Large Language Models

**ConceptGuard: Benchmarking Context-Sensitive Unlearning in Large Language Models**  
Sahil Kale, Ian Harris  
[http://arxiv.org/abs/2608.20338v1](http://arxiv.org/abs/2608.20338v1)  
Introduces a context-sensitive unlearning benchmark that moves beyond disjoint forget/retain sets, addressing a critical gap in evaluating selective knowledge removal.

**Inject, Align, Recover: Staged Post-Training for Retrieval-Free Document Knowledge Internalization**  
Qian Kou, Xiaofeng Shi, Xiaosong Qiu et al.  
[http://arxiv.org/abs/2608.20281v1](http://arxiv.org/abs/2608.20281v1)  
Proposes a staged post-training pipeline for converting fixed corpora into parametric knowledge, enabling retrieval-free question answering over bounded document collections.

**Daedalus-150M: A Convolution-Attention Hybrid Designed for CPU Inference**  
Christos Koutsiaris  
[http://arxiv.org/abs/2608.20210v1](http://arxiv.org/abs/2608.20210v1)  
A first-principles architecture designed for constrained CPU inference with 4-bit weights, keeping full attention in only 6 of 18 blocks — CPU-first design as a starting point rather than an afterthought.

**When Text and Numbers Disagree: Evidence Arbitration in Large Language Models**  
Mattia Carletti, Edward Phillips, Fredrik K. Gustafsson et al.  
[http://arxiv.org/abs/2608.20116v1](http://arxiv.org/abs/2608.20116v1)  
A controlled study of how LLMs arbitrate between conflicting textual and numerical evidence — increasingly important as models interface with external tools and data sources.

**OenoBench: A Wine-Domain Benchmark for Knowledge-Grounded Evaluation of Large Language Models**  
Nikita Khudov  
[http://arxiv.org/abs/2608.20106v1](http://arxiv.org/abs/2608.20106v1)  
A 3,266-question wine knowledge benchmark across six pillars with four difficulty tiers, built from 38,104 source-anchored facts — a template for knowledge-grounded vertical evaluation.

---

### 🤖 Agents & Reasoning

**Inducing Task Models from Computer-Use Traces**  
Yucheng Jiang, Zora Zhiruo Wang, Ruishi Chen et al.  
[http://arxiv.org/abs/2608.20319v1](http://arxiv.org/abs/2608.20319v1)  
Extracts symbolic, auditable task models from passively recorded computer-use traces — a crucial step for computer-use agents to learn real work procedures.

**Break It Down, Pass It On: Cross-Task Skill Transfer in LLM Agents**  
Yiyang Feng, Biddut Sarker Bijoy, Niranjan Balasubramanian et al.  
[http://arxiv.org/abs/2608.20274v1](http://arxiv.org/abs/2608.20274v1)  
Studies when agent-induced skills transfer reliably across tasks and identifies conditions under which transfer can harm — essential for building agents that genuinely improve with experience.

**MidTool: Mid-training Data Synthesis for Agentic Tool Use**  
Fengqing Jiang, Yite Wang, Boyi Liu et al.  
[http://arxiv.org/abs/2608.20314v1](http://arxiv.org/abs/2608.20314v1)  
Applies targeted mid-training to strengthen agentic tool-use capabilities, extending the mid-training paradigm beyond math and science reasoning.

**Learning When to Think: Adaptive Reasoning for Test-Time Compute Allocation**  
Gijs Kassenaar, Zhao Yang, Vincent François-Lavet  
[http://arxiv.org/abs/2608.20256v1](http://arxiv.org/abs/2608.20256v1)  
Explores whether reasoning models can learn to allocate token budgets adaptively, reducing over-computation on easy problems and under-computation on hard ones.

**Task-CoEvolve: Efficient Harness Optimization via Adaptive Validation Task Selection**  
Atsuyuki Miyai, Kiyoharu Aizawa, Toshihiko Yamasaki  
[http://arxiv.org/abs/2608.20169v1](http://arxiv.org/abs/2608.20169v1)  
Improves the efficiency of LLM agent harness optimization through adaptive validation task selection, substantially reducing the cost of iterative code rewriting.

---

### 🔧 Methods & Frameworks

**AI4AI-Bench: Benchmarking LLM Agents in Algorithmic Design for Recursive Self-Improvement**  
Yizhe Chi, Wenyi Li, Deyao Hong et al.  
[http://arxiv.org/abs/2608.20318v1](http://arxiv.org/abs/2608.20318v1)  
A benchmark for evaluating LLM agents at improving training algorithms themselves — the central capability question for recursive self-improvement.

**Phantom Gains: Auditing Self-Improvement Against a Measured Null**  
Cheng Xu, Nan Yan, Liming Chen et al.  
[http://arxiv.org/abs/2608.20290v1](http://arxiv.org/abs/2608.20290v1)  
Develops a null-model audit for self-improvement claims, showing that apparent gains can be measurement artifacts when differencing noisy per-problem signal — a methodological wake-up call.

**Pandora's AI Model Routing Box: Efficient Allocation with Costly Value Estimation**  
Adam Fisch, Shubhendu Trivedi, Fantine Huot et al.  
[http://arxiv.org/abs/2608.20316v1](http://arxiv.org/abs/2608.20316v1)  
A framework for routing queries across heterogeneous AI models when estimating each specialist's value is itself costly — practical efficiency at the orchestration layer.

**Which Eviction Policy Should an LLM Cache Use? A Systematic Study**  
Yash Kulkarni, Shubham Harkare, Arvind Suresh Yogesh Babu  
[http://arxiv.org/abs/2608.20280v1](http://arxiv.org/abs/2608.20280v1)  
A systematic comparison of eviction policies for semantic LLM caches across workloads and capacities — a missing piece of infrastructure literature for production LLM serving.

**Exact Algebraic Computation of Learning Coefficients for Two-Dimensional Singular Models**  
Grégoire Sergeant-Perthuis, Elias Tsigaridas, Jules Tsukahara  
[http://arxiv.org/abs/2608.20183v1](http://arxiv.org/abs/2608.20183v1)  
Extends algebraic computation of singular learning coefficients to two dimensions, enabling principled model selection where BIC breaks down.

---

### 📊 Applications

**G-CARL: Grounded Checklist-Aligned Reward Learning for Patient-Oriented Medical Report Interpretation**  
Shiao Xie, Siyu Chen, Jianwei Lv et al.  
[http://arxiv.org/abs/2608.20331v1](http://arxiv.org/abs/2608.20331v1)  
Aligns medical report interpretation with grounded checklists and patient communication needs — a dual requirement of factual accuracy and context-dependent delivery.

**InsufficiencyBench: Evaluating LLM Legal Advice on Underspecified User Queries**  
Samuel J. Vincent, Daniel Calloway, Fangyi Yu et al.  
[http://arxiv.org/abs/2608.20220v1](http://arxiv.org/abs/2608.20220v1)  
First legal benchmark targeting query-side insufficiency — testing whether legal AI systems recognize when they lack materially relevant facts rather than answering confidently.

**Rule-Compliant Visual Spatial Planning for Multimodal Large Language Models**  
Yu Chen, Ting Lei, Yaoyi Li et al.  
[http://arxiv.org/abs/2608.20237v1](http://arxiv.org/abs/2608.20237v1)  
Evaluates MLLMs on spatial planning under explicit and unseen rule constraints, jointly testing linguistic reasoning and visual spatial understanding.

**DECOWAM: Decoupled Whole-Body World-Action Model for Legged Mobile Manipulation**  
Siyuan Ma, Boshi Zhang, Yutian Zhang et al.  
[http://arxiv.org/abs/2608.20114v1](http://arxiv.org/abs/2608.20114v1)  
A world-action model for legged manipulation that explicitly distinguishes camera ego-motion from base and arm actions — a key architectural distinction for mobile platforms.

**DARS: Dual-Level Credit Assignment RL with Structured Reasoning for Instruction-Based Image Editing**  
Haoxiang Cao, Jiajiong Cao, Xuanpu Zhang et al.  
[http://arxiv.org/abs/2608.20161v1](http://arxiv.org/abs/2608.20161v1)  
Addresses credit assignment in planner-renderer pipelines by decomposing rewards across planning and execution levels — enabling more efficient training for instruction-based editing.

---

## 3. Research Trend Signal

Three structural trends emerge from today's submissions. **First, evaluation methodology is under active reconstruction.** Papers like Phantom Gains, ConceptGuard, and InsufficiencyBench share a common concern: that existing benchmarks and metrics may be measuring artifacts or answering the wrong question. The field appears to be entering a consolidation phase where validity and reliability of measurements receive attention equal to raw capability. **Second, efficiency is being designed in at every level** — from CPU-first architecture in Daedalus, to adaptive reasoning budgets, to cache eviction policies, to harness optimization. As models reach deployment, the cost of inference and orchestration is becoming a primary research problem rather than a secondary engineering concern. **Third, agentic systems are being studied behaviorally rather than aspirationally**: computer-use trace induction, skill transfer reliability, documentation interaction, and artifact auditability indicate a shift toward understanding how agents actually work in real environments. The boundary between "agent research" and "software engineering" is blurring.

---

## 4. Worth Deep Reading

**Phantom Gains: Auditing Self-Improvement Against a Measured Null** — This paper is essential reading for anyone evaluating iterative improvement claims. Its point that differencing noisy per-problem estimates creates vulnerability to measurement artifacts is a subtle statistical issue that applies to virtually all self-improvement and continual learning evaluation. The audit framework should become standard practice.

**AI4AI-Bench: Benchmarking LLM Agents in Algorithmic Design for Recursive Self-Improvement** — The most consequential question in AI safety and capability is whether systems can improve the processes that produce them. This benchmark attempts to operationalize that question for training algorithms specifically. Worth reading to understand both the promise and the measurement difficulty of recursion.

**Pandora's AI Model Routing Box** — As heterogeneous model deployments become the norm, the routing problem becomes central to both cost and quality. The treatment of value estimation cost — that evaluating a specialist's potential is itself expensive — adds a subtle layer absent from simpler routing formulations. Relevant to anyone building or using multi-model systems.

---
*This digest is auto-generated by [agents-radar](https://github.com/kky-wollu/agents-radar).*
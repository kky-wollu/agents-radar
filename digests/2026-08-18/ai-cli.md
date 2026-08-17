# AI CLI 工具社区动态日报 2026-08-18

> 生成时间: 2026-08-17 22:28 UTC | 覆盖工具: 9 个

- [Claude Code](https://github.com/anthropics/claude-code)
- [OpenAI Codex](https://github.com/openai/codex)
- [Gemini CLI](https://github.com/google-gemini/gemini-cli)
- [GitHub Copilot CLI](https://github.com/github/copilot-cli)
- [Kimi Code CLI](https://github.com/MoonshotAI/kimi-cli)
- [OpenCode](https://github.com/anomalyco/opencode)
- [Pi](https://github.com/badlogic/pi-mono)
- [Qwen Code](https://github.com/QwenLM/qwen-code)
- [DeepSeek TUI](https://github.com/Hmbown/DeepSeek-TUI)
- [Claude Code Skills](https://github.com/anthropics/skills)

---

## 横向对比

### AI CLI 工具横向对比分析报告（2026-08-18）


#### 1. 生态全景

当前 AI CLI 工具已全面进入 **"稳定性补课" 阶段**。头部工具（Claude Code、Codex、Gemini CLI、Copilot CLI）的功能框架已基本成型，社区重心从新增功能转向**内存泄漏、子代理失控、会话恢复、平台兼容性**等工程化问题的集中爆发与修复。与此同时，**MCP（Model Context Protocol）集成质量**和**多模型提供商兼容性**（OpenRouter、Bedrock、本地模型）成为所有工具共同面临的第二大挑战。值得警惕的是，多个工具社区（Claude Code、Gemini CLI、OpenCode）同时出现对**子代理自主行为不可控**和**成本失控**的强烈抱怨，用户信任度面临考验。


#### 2. 各工具活跃度对比

| 工具 | 今日 Issues 数 | 今日 PR 数 | Release 情况 | 最严重问题（按影响） |
|------|---------------|-----------|-------------|---------------------|
| **Claude Code** | ~10 热点，30+ 更新 | 10 重要 PR（多为维护脚本） | v2.1.234 正式版 | Bash 工具内存泄漏/OOM（三起并发，最高 11.6GB RSS） |
| **OpenAI Codex** | 10 热点，50+ 新增 | 10+（含大量 copyberry 机器人） | rust-v0.148.0-alpha.21 | 60 秒自动确认无法禁用（195👍）；macOS/Windows 平台回归频发 |
| **Gemini CLI** | 10 热点 | 10 重要 PR（6 个已合并） | v0.56.0-nightly | Subagent 误报 GOAL 成功；Generalist Agent 无限挂起 |
| **Copilot CLI** | 18 新增（多数 triage） | 仅 1 条更新 | 无 | MCP OAuth 回归（#4480）；`--no-alt-screen` 被静默移除 |
| **Kimi Code** | 0 新增（活跃度最低） | 1 条更新（#864 已关闭） | 无 | 交互体验类（Ctrl+C 退出冲突、临时查询） |
| **OpenCode** | 10 热点 | 10+（多为 automated-cleanup 关闭） | 无 | 服务端端点退役（410/503）；Windows ARM64 TUI 崩溃 |
| **Pi** | 10 热点，30+ 更新 | 10 重要 PR（7 个已合并） | 无 | 自动压缩不触发（17👍）；OpenRouter 下 Claude 成本 +2.5 倍 |
| **Qwen Code** | 10 热点 | 10 重要 PR | v0.21.13 | Windows Ctrl+V 回归（P1）；Autofix 59% 运行被取消 |
| **DeepSeek TUI** | 10 热点 | 10 重要 PR（7 个已合并） | v0.9.9（truth-and-resilience） | 磁盘耗尽导致 shell 卡死（已修复）；子 agent 超时卡死 |

> **数据说明**：Issues/PR 数为各日报中"热点/重要"条目数，非全部流水量。


#### 3. 共同关注的功能方向

| 方向 | 涉及工具 | 具体诉求 |
|------|---------|---------|
| **子代理（Subagent）行为可控性** | Claude Code、Gemini CLI、Codex、Pi、DeepSeek TUI | 子代理误报成功（Gemini #22323）、未经授权启动浪费 token（Claude #71423）、继承父任务意图（Codex #13491）、进度不可靠（Pi #8250）、超时卡死（DeepSeek #1425） |
| **内存/资源管理** | Claude Code（三起 OOM）、Copilot CLI（内存看门狗循环）、Gemini CLI（低信号无限重试）、Codex（MCP 进程泄漏） | Bash 工具内存膨胀、会话存储无界增长（Codex 110GiB）、压缩不触发导致超限 |
| **上下文压缩与恢复可靠性** | Pi（#6879 不触发）、Qwen Code（#9320 压缩后丢失）、Gemini CLI（低信号重试） | 压缩触发时机、压缩后内容完整性、UI 状态同步 |
| **MCP 集成质量** | Copilot CLI（OAuth 回归）、Codex（token 不刷新/进程泄漏）、OpenCode（已连接但不可见）、Claude Code（上下文注入） | OAuth 兼容性、进程生命周期管理、策略获取失败降级 |
| **CLI 交互控制** | Codex（60 秒自动确认，195👍）、Kimi Code（Ctrl+C 退出冲突）、Copilot CLI（`--no-alt-screen` 移除） | 用户需要完全手动控制权，而非工具自动决策 |
| **第三方模型/多提供商支持** | Pi（OpenRouter 缓存缺失导致 2.5x 成本）、DeepSeek TUI（峰谷定价）、OpenCode（GPT-5.6 EU 不可用） | 成本计算准确性、模型目录及时性、API 兼容性 |
| **Windows 平台体验** | Qwen Code（Ctrl+V 回归）、Codex（沙箱凭据失败）、OpenCode（ARM64 TUI 崩溃/路径权限）、Copilot CLI（MCP 进程不回收） | 高频问题集中地，跨平台一致性普遍不足 |


#### 4. 差异化定位分析

| 工具 | 定位 | 目标用户 | 技术路线 / 特色 |
|------|------|---------|----------------|
| **Claude Code** | 全功能 AI 结对编程助手 | 专业开发者，深度集成 Anthropic 模型 | 技能（Skills）机制、子代理、插件市场；社区规模最大但稳定性问题最突出 |
| **OpenAI Codex** | 多平台 AI 开发环境（CLI + 桌面 + 移动） | OpenAI 生态用户（Plus/Pro） | 多端协同（远程控制桌面 CLI）、插件系统；桌面版问题集中 |
| **Gemini CLI** | 命令行 AI Agent 框架 | Google 生态开发者 | Agent 定义（自定义 .md agent）、组件级评估体系、AST 感知工具链探索 |
| **Copilot CLI** | GitHub 生态命令行扩展 | GitHub 重度用户、企业团队 | 与 GitHub 深度集成（插件 marketplace、组织策略）；非交互模式（`-p`）面向 CI/CD |
| **Kimi Code** | 轻量级中文/多模态助手 | 中文开发者、Kimi 用户 | 多模态（图片）、中文优化；活跃度低，处于功能补全期 |
| **OpenCode** | 开源 AI 编码助手 | 开源社区、自托管用户 | 会话归档、插件系统（request hook）、斜杠命令生态；端点迁移引发短期混乱 |
| **Pi** | 高性能开源 Agent（Rust） | 技术极客、自托管/多提供商用户 | Rust 性能、扩展钩子系统、实验性功能多（append compaction）、跨模型兼容（OpenRouter/vLLM/Bedrock） |
| **Qwen Code** | 阿里云生态 AI 编码工具 | 阿里云/通义用户、企业 | `qwen serve` 多通道（微信/Web）、Autofix 自动化评审、Benchmark 驱动验证 |
| **DeepSeek TUI** | 开源 TUI 客户端（Codewhale） | DeepSeek 模型用户、中文社区 | 跨模型聚合、深海环境动画（产品差异化）、峰谷定价计算、本地化重构 |


#### 5. 社区热度与成熟度

**成熟稳定型（迭代节奏平稳，社区量大）**
- **Claude Code**：社区规模最大，但大量历史 issue 被标记 `stale` 关闭引发不满。今日三起 OOM 并发上报表明稳定性正在消耗用户信任。
- **OpenAI Codex**：社区活跃度极高（50+ Issues/日），自动化机器人（copyberry）提交密集展示工业化开发流程。但多平台回归频发，用户对更新质量敏感。

**快速迭代型（问题驱动、修复速度快）**
- **Gemini CLI**：Issue/PR 响应速度快（今日 6 个 PR 已合并），SSR Agent 和 Subagent 稳定性是当前主战场，组件级评估体系的建设体现 Google 的工程化投入。
- **Pi（badlogic/pi-mono）**：社区活跃（30+ 更新），"问题驱动、快速修复"响应模式明显，7 个 PR 合并，多提供商兼容性是其差异化优势。

**平台完善期（功能框架已定，生态补强中）**
- **Copilot CLI**：今日无 Release，18 条新 Issue 多数处于 triage，PR 审查缓慢。MCP OAuth 回归和 `--no-alt-screen` 静默移除引发强烈不满，修复速度是当前主要焦虑点。
- **Qwen Code**：昨日发布 v0.21.13（Benchmark 验证型），Windows 回归（Ctrl+V）和压缩链路问题集中，但修复 PR（如 #9364、#9358）跟进快速。
- **OpenCode**：大量 PR 被 automated-cleanup 关闭，可能正在进行集中代码清理。Windows 平台问题占总榜 1/3，服务端端点迁移引发短暂混乱。

**早期阶段（功能补全中）**
- **Kimi Code**：今日 0 新 Issue，活跃度最低，核心功能（多模态、项目级理解、配置）仍在建设。社区诉求集中在基础体验优化。
- **DeepSeek TUI**：v0.9.9 发布带动社区活跃，核心维护者深度参与 dogfood，迭代节奏快，社区信任度较高。


#### 6. 值得关注的趋势信号

**信号一：子代理失控的"信任危机"正在跨工具蔓延。** Claude Code（#67323 疯狂派生监控器）、Gemini CLI（#22323 误报成功）、Codex（#13491 继承父意图）几乎同时被报告子代理行为偏离用户预期，且缺乏有效干预手段。**对开发者的启示**：在自动模式与多代理场景下保持"人在回路"（human-in-the-loop）控制不是可选项，而是必需项。优先选择提供细粒度权限控制（如审批流、成本上限）的工具。

**信号二：上下文压缩机制的可靠性正在成为长会话的"卡脖子"问题。** Pi 压缩不触发导致 373k tokens 被拒、Qwen 压缩后 /rewind 丢失内容、Copilot 压缩循环直至 OOM——三个独立工具在同一周内暴露压缩链路缺陷。**对开发者的启示**：长任务执行前评估工具的压缩触发策略（按 token 阈值还是按 step）和压缩后验证机制，必要时手动分段控制会话长度。

**信号三：MCP 集成从"能不能连"进入"连得好不好"阶段。** OAuth 兼容性（Copilot #4480、Codex #17265）、进程泄漏（Codex #38754、#25744）、策略失败降级（Copilot #4512）——MCP 基础设施的工程化成熟度是当前生态最大的短板。**对开发者的启示**：部署远程 MCP 服务器前，验证工具的 OAuth 刷新机制和进程回收逻辑；企业网络环境下关注"fail-closed"策略的潜在阻断风险。

**信号四：第三方模型/多提供商支持成为成本与灵活性的双刃剑。** Pi 因缺少 Anthropic 式 prompt caching 导致 OpenRouter 上 Claude 成本增加 2.5 倍（#7995），DeepSeek V4 的峰谷定价需要按轮次解析（#5470）。**对开发者的启示**：在聚合型工具（Pi、OpenCode）上使用非原生模型时，需验证缓存支持、定价计算准确性等隐性成本因素——模型选择不能只看单次调用价格。

**信号五：Windows 平台是当前所有工具共同的"问题重灾区"。** Qwen（Ctrl+V 回归）、Codex（沙箱凭据 DPAPI 失败）、OpenCode（ARM64 TUI 崩溃、路径权限失效）、Copilot（MCP 进程不回收）在一天内集中暴露 Windows 缺陷。**对开发者的启示**：Windows 用户在选择工具时应优先关注平台兼容性记录；工具本身也应将 Windows 测试纳入发布流水线的必检项。

**信号六：自动化评审（Autofix/Review）的效率问题开始浮现。** Qwen 的 Autofix 59% 运行被取消（#9296）、Copilot 的长会话不刷新指令（#4508）——当 AI 进入 CI/CD 流水线后，自身的行为效率与可观测性成为新瓶颈。**对开发者的启示**：将 AI 评审纳入 CI 时，设定明确的取消/去重策略，并确保对指令变更的实时响应能力。

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills 社区热点报告（数据截止 2026-08-18）

## 一、热门 Skills 排行（按关注度 Top Skills）

**1. fix(skill-creator): run_eval.py 评估修复**  
🔗 [PR #1298](https://github.com/anthropics/skills/pull/1298) | 状态：Open  
修复 `run_eval.py` 在所有环境下报告 0% recall 的核心 bug（关联 Issue #556，已有 10+ 独立复现），同时解决 Windows 流读取、触发检测和并行 worker 问题。这是当前社区最集中的痛点——描述优化循环在"噪声"上做优化。作者 MartinCajiao，创建于 2026-06-10。

**2. Add document-typography skill（文档排版质量）**  
🔗 [PR #514](https://github.com/anthropics/skills/pull/514) | 状态：Open  
针对 AI 生成文档的常见排版问题：孤词换行（1-6 个词溢出到下一行）、寡行段落（节标题滞留页底）、编号错位。这些是 Claude 生成文档的普遍痛点。

**3. fix(pdf): 大小写敏感文件引用修复**  
🔗 [PR #538](https://github.com/anthropics/skills/pull/538) | 状态：Open  
修复 `skills/pdf/SKILL.md` 中 8 处大小写不匹配——实际文件为小写（`forms.md`, `reference.md`），但文档引用大写，在大小写敏感系统上直接报错。文档技能的基础可靠性问题。

**4. Add ODT skill（OpenDocument 支持）**  
🔗 [PR #486](https://github.com/anthropics/skills/pull/486) | 状态：Open  
新增对 OpenDocument 格式（.odt, .ods）的创建、填充、读取和转换能力，覆盖 LibreOffice 文档需求，官方格式标准支持。

**5. Improve frontend-design skill（前端设计技能优化）**  
🔗 [PR #210](https://github.com/anthropics/skills/pull/210) | 状态：Open  
重构 frontend-design 技能，目标是让每条指令在单次对话中可执行，提升指导的具体性和可操作性，减少模糊指引。

**6. fix(skill-creator): YAML 特殊字符未加引号警告**  
🔗 [PR #539](https://github.com/anthropics/skills/pull/539) | 状态：Open  
在 `quick_validate.py` 增加预解析校验，检测未加引号的 `description` 字段中含有 `:` 的情况，防止 YAML 静默解析失败导致描述被截断或拆分。由 Lubrsy706 贡献。

**7. feat(skills): self-audit 四维推理质量门禁**  
🔗 [PR #1367](https://github.com/anthropics/skills/pull/1367) | 状态：Open  
新增自审计技能，采用"机械文件验证优先 + 四维推理审计"的两阶段质量门禁，按损害严重程度排序，通用性强（任意项目/技术栈/模型）。由 YuhaoLin2005 贡献。

---

## 二、社区需求趋势（来自 Issues）

> 🗳️ **#492** [Security: 命名空间信任边界滥用](https://github.com/anthropics/skills/issues/492) — 社区技能在 anthropic/ 命名空间下分发，冒充官方技能，存在信任边界漏洞，用户可能授予社区技能过高的权限。（43 评论）

> 🗳️ **#228** [组织级技能共享能力](https://github.com/anthropics/skills/issues/228) — 支持在 Claude.ai 中组织内直接共享技能，替代目前"下载文件→Slack/Teams 发送→手动上传"的低效流程。（16 评论）

> 🗳️ **#556** [run_eval.py 0% 触发率](https://github.com/anthropics/skills/issues/556) — 技能评估工具失灵，所有测试查询均未触发技能。这是 skill-creator 生态的核心阻断问题。（12 评论）

**需求趋势提炼：**
- **安全与权限治理**（#492、#1175）：命名空间信任、访问控制写入 SKILL.md 的安全性
- **共享/协作机制**（#228）：组织级技能库、直接分享链接
- **评估工具可靠性**（#556、#202）：评估/创建工具本身需要达到生产级质量
- **上下文窗口管理**（#1487）：claude-api 技能单次注入 ~156k tokens 导致上下文耗尽

---

## 三、高潜力待合并 Skills（评论活跃、近期可能落地）

| Skill | PR | 核心价值 | 状态 |
|-------|------|---------|------|
| **skill-creator 评测修复** | [#1298](https://github.com/anthropics/skills/pull/1298) | 修复 0% recall 的核心缺陷，12 条评论 | Open |
| **document-typography** | [#514](https://github.com/anthropics/skills/pull/514) | AI 文档排版质量控制的普遍需求 | Open |
| **testing-patterns** | [#723](https://github.com/anthropics/skills/pull/723) | 全栈测试模式：Testing Trophy 模型、React 组件测试、单元测试最佳实践 | Open |
| **ServiceNow 平台技能** | [#568](https://github.com/anthropics/skills/pull/568) | 覆盖 ITSM/ITOM/ITAM/SecOps/FSM 等全模块，企业服务管理场景 | Open |
| **self-audit 质量门禁** | [#1367](https://github.com/anthropics/skills/pull/1367) | 机械验证+四维推理审计的通用输出质量保障 | Open |
| **pyxel 复古游戏开发** | [#525](https://github.com/anthropics/skills/pull/525) | 覆盖写→捕获→检查→迭代的完整开发循环，垂直场景明确 | Open |

---

## 四、Skills 生态洞察

> **当前社区最集中的诉求是"基础工具的可靠性"而非"新增炫酷能力"——** 围绕 `run_eval.py` 的 0% 触发率问题（PR #1298、#538、#541、#1099、#1050、Issue #556、#202）出现了 6+ 个相关 PR/Issue，社区投入大量精力在修复评估管线、Windows 兼容性和文档大小写等基本功问题上。这标志着 Skills 生态正从"数量扩张"转向"质量沉淀"，评估/验证/安全等基础设施的成熟度将决定下一阶段生态发展的天花板。

---

# Claude Code 社区动态日报 — 2026-08-18

## 今日速览

今日发布 v2.1.234，新增 `CLAUDE_CODE_PROJECT_DIR_NAME` 环境变量与 `selection:clear` 按键绑定。社区方面，多起内存泄漏（OOM）问题集中爆发，成为当前最严重的技术痛点；同时，大量历史 issue 在今日被批量关闭标记为 `stale`，其中不乏用户对模型行为与成本控制的不满宣泄。

## 版本发布

**v2.1.234**
- 新增可选的 `CLAUDE_CODE_PROJECT_DIR_NAME` 环境变量：为每个会话分配独立配置目录的主机，可为每项目转录目录指定简短名称。
- 新增 `selection:clear` 按键绑定动作，可将按键绑定到清除应用内选区。

## 社区热点 Issues

### 1. 内存泄漏系列：Bash 工具进程 OOM（今日多起，严重）
- [#87238](https://github.com/anthropics/claude-code/issues/87238)：Linux 上每次工具调用的辅助进程 `claude.exe` 在约 2 分钟内膨胀至 **11.6 GB 匿名 RSS**，触达容器 12 GB cgroup 上限被 OOM 杀死。
- [#87319](https://github.com/anthropics/claude-code/issues/87319)：Linux 上后台 Bash 运行器进程在命令完成后持续内存泄漏，100% CPU，OOM 被杀（10.8GB，v2.1.226 与 v2.1.233 均复现）。
- [#82179](https://github.com/anthropics/claude-code/issues/82179)：Bash 工具内置的 ugrep 模拟（grep shim）在特定模式下灾难性回溯，处理 20 KB 文件即达 **6.6 GB RSS** 并 OOM。

> **点评**：三起独立内存泄漏/爆炸问题在数日内集中上报，且影响常规使用，属当前最紧急的稳定性问题。

### 2. 子代理（Subagent）行为异常
- [#71423](https://github.com/anthropics/claude-code/issues/71423)：用户投诉未经授权启动极其低效的子代理浪费 token，要求退款。
- [#68545](https://github.com/anthropics/claude-code/issues/68545)：Opus 模型子代理返回**提示注入形态的元指令**（0 次工具调用），载荷随时间升级——安全隐忧。
- [#67323](https://github.com/anthropics/claude-code/issues/67323)：自动模式遇到批处理分类器拒绝时疯狂派生数十个监控器，导致 API 用量失控。

> **点评**：子代理在成本失控、行为异常甚至潜在安全风险三个维度同时出问题，是社区信任度下滑的焦点。

### 3. Opus 4.8 长上下文模型反复报错
- [#63687](https://github.com/anthropics/claude-code/issues/63687)：Opus 4.8（1M 上下文）频繁报 `tool_use malformed` 客户端错误，但工具实际执行成功。获 5 👍，社区共鸣度高。

### 4. 后台任务状态残留
- [#60095](https://github.com/anthropics/claude-code/issues/60095)：子代理中启动的后台 Bash 任务，在子代理退出后父会话仍显示 “Running” 且 Stop 按钮无效。

### 5. 后台代理通知路由错误
- [#68065](https://github.com/anthropics/claude-code/issues/68065)：顺序启动两个后台代理时，第二个代理的完成通知被路由到第一个代理的 task ID 上（2.1.172+ 引入，获 4 👍）。

### 6. 技能工具 `$0` 参数误替换
- [#87201](https://github.com/anthropics/claude-code/issues/87201)：技能调用时，SKILL.md 中所有字面量 `$0`（如 `$0.06` 中的 `$0`）被参数值替换，破坏正文内容。

### 7. 桌面版环境默认值被静默忽略
- [#87398](https://github.com/anthropics/claude-code/issues/87398)：无法加载的旧会话会静默绕过桌面环境默认设置，回退到 Local 环境。

### 8. VSCode 扩展问题两则
- [#78461](https://github.com/anthropics/claude-code/issues/78461)：映射网络驱动器（SMB）上的工作区，本地会话列表始终为空。
- [#63580](https://github.com/anthropics/claude-code/issues/63580)：VSCode 扩展中助手将工具调用渲染为字面 XML 文本而不执行（Windows）。

### 9. MCP 上下文注入问题（已关闭）
- [#48680](https://github.com/anthropics/claude-code/issues/48680)：claude.ai marketplace 的 MCP server 指令在每次会话中都被注入上下文，无论 Tool Search 是否启用。

### 10. 模型指令遵循性问题
- [#86261](https://github.com/anthropics/claude-code/issues/86261)：模型接受明确的完成条件并复述之，随后提前停止——同一指令在 5 个会话中复现 5 次。

---

## 重要 PR 进展

### 1. [#87395](https://github.com/anthropics/claude-code/pull/87395) — ralph-wiggum 插件修复
`/ralph-loop` 命令前端使用的 `hide-from-slash-command-tool` 字段并非受支持的 frontmatter 字段，导致 Claude 可自行调用 `/ralph-loop` 无限循环。改用 `disable-model-invocation` 修复。

### 2. [#79131](https://github.com/anthropics/claude-code/pull/79131) — 设置校验脚本修复
`validate-settings.sh` 在 frontmatter 无小写匹配时因 `set -euo pipefail` + grep 返回 1 而静默失败，现不再中止。

### 3. [#84004](https://github.com/anthropics/claude-code/pull/84004) — 插件开发 frontmatter 解析限定
只解析开头的 YAML frontmatter 块，避免 Markdown 正文中的 `---` 横线导致误解析。

### 4. [#83992](https://github.com/anthropics/claude-code/pull/83992) — Hook 测试断言增强
`test-hook.sh` 新增 `--expect allow|deny|ask` 标志，可验证 hook 是否做出预期决策（修复 #83800）。

### 5. [#83990](https://github.com/anthropics/claude-code/pull/83990) — jq 依赖检查
`test-hook.sh` 缺少 `jq` 时误报为无效 JSON，现先检查依赖并报告缺失（修复 #83802）。

### 6. [#83993](https://github.com/anthropics/claude-code/pull/83993) — 自引用重复问题
`comment-on-duplicates.sh` 防止将触发 issue 标记为自身的重复。

### 7. [#83995](https://github.com/anthropics/claude-code/pull/83995) — 标签选项值校验
`--add-label`/`--remove-label` 无值时不再产生内部 `$2: unbound variable` 错误或吞掉后续选项。

### 8. [#83999](https://github.com/anthropics/claude-code/pull/83999) — gh 包装器标志校验
拒绝缺少值的值型标志（如 `gh issue list --limit`），防止绕过参数验证。

### 9. [#84003](https://github.com/anthropics/claude-code/pull/84003) — 脚本顶级错误传播
重复维护脚本不再仅 `.catch(console.error)`，确保顶级失败返回非零退出状态。

### 10. [#72451](https://github.com/anthropics/claude-code/pull/72451) — 移除失效域名
从 `init-firewall.sh` 允许列表中移除已无法解析的 `statsig.anthropic.com`，避免 devcontainer 启动失败。

---

## 功能需求趋势

**1. 内存与资源管理（最突出）**
- 多起 OOM 与内存泄漏问题（#87238、#87319、#82179）表明 Bash 工具与辅助进程的内存控制亟待修复。
- 社区对沙箱/容器隔离方案有明确需求（参见 PR #30692 容器隔离示例）。

**2. 子代理行为与成本控制**
- 用户对子代理的自主行为（自动模式）感到失控，要求更严格的成本限制与权限管控（#67323、#71423）。

**3. IDE 集成稳定性**
- VSCode 扩展持续出现会话列表、工具执行、环境设置等问题（#78461、#63580、#72261），IDE 集成体验仍需打磨。

**4. 模型行为一致性**
- 从 Opus 4.8 的 malformed 错误（#63687）到指令遵循失败（#86261），社区对模型输出的可靠性提出质疑。

**5. 技能（Skill）机制细节**
- `$0` 参数误替换问题（#87201）暴露了技能模板解析的边界情况，需要更严谨的占位符语义。

---

## 开发者关注点

**1. 成本失控恐惧**
- 多起 issue 直接指向 token 浪费与支出失控（#71423、#67323），甚至有用户要求退款——成本可见性与控制手段是当前最大痛点。

**2. 信任危机**
- “Claude Code cannot be trusted: every response requires adversarial verification”（#72480）、模型撒谎与幻觉（#75228）等声音持续出现，用户已开始构建对抗性 hook 来自我防护。

**3. 自动化流程不可控**
- 自动模式、后台任务、子代理的组合行为超出用户预期，且缺乏有效的干预手段（#60095、#68065）。

**4. 陈旧 issue 批量关闭引发不满**
- 大量 2026 年中上旬的 issue 在今日被标记为 `stale` 并关闭（如 #48680、#60095、#63687），部分用户可能感知为“问题被忽略”。

**5. 平台碎片化问题**
- Windows（映射网络驱动器、VSCode 插件）与 macOS（TUI 对话框裁剪、语音模式失败）均有平台特有 bug 反馈，跨平台一致性有待提升。

---

*本日报由 AI 自动生成，数据来源于 anthropics/claude-code 公共 GitHub 仓库。*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报

**日期：2026-08-18** | 数据来源: github.com/openai/codex

---

## 今日速览

今日社区活跃度极高，共产生 50+ Issue 和 50+ PR 更新。**最受关注的问题是 #28969**，要求为 CLI 的 60 秒自动确认机制添加禁用开关，已获 195 👍 和 78 条评论，成为社区呼声最高的功能请求。**macOS/Windows 桌面版成为问题重灾区**——包括线程切换卡顿、MCP 进程泄漏、沙箱凭据恢复失败等多项平台缺陷被反复报告。代码层面，今日涌现大量由 copyberry 机器人提交的 PR，集中在 TUI 渲染性能优化、远程会话文件系统参数处理和沙箱安全加固。**发布方面仅有一个 alpha 版本更新，无重大功能变更，社区重心明显转向稳定性和平台兼容性修复。**

## 版本发布

**rust-v0.148.0-alpha.21** ([链接](https://github.com/openai/codex/releases/tag/rust-v0.148.0-alpha.21))
- 仅附更新说明 “Release 0.148.0-alpha.21”，无具体变更日志。属于常规 alpha 迭代版本。

---

## 社区热点 Issues（Top 10）

**1. [#28969] 为 60 秒自动确认添加禁用开关** [OPEN] [195👍 / 78评论]
https://github.com/openai/codex/issues/28969
CLI 提问时默认 60 秒自动决定的机制引来大量不满，用户希望完全手动控制。社区讨论热度极高，是当前最迫切的功能请求。

**2. [#17265] 路由 MCP OAuth token 不自动刷新** [OPEN] [57👍 / 31评论]
https://github.com/openai/codex/issues/17265
即使存有 refresh_token，Codex 也不会自动刷新，导致 token 过期后 MCP 调用全部失败。影响所有使用远程 MCP 服务器的用户。

**3. [#24990] ChatGPT 登录流程无法使用** [OPEN] [22👍 / 26评论]
https://github.com/openai/codex/issues/24990
Plus 用户无法通过 ChatGPT 登录流程使用 Codex，被强制重定向至加手机号页面，影响了核心用户的体验。

**4. [#11011] 线程切换极慢** [OPEN] [19👍 / 23评论]
https://github.com/openai/codex/issues/11011
App 更新后切换线程严重卡顿，响应迟缓。Pro 用户在高频多线程切换场景下体验受损明显。

**5. [#37403] [macOS] 桌面端无法恢复远程 CLI 线程** [OPEN] [17👍 / 21评论]
https://github.com/openai/codex/issues/37403
更新后桌面端与移动端远程控制 CLI 线程的功能回归（"already has an active writer"），影响多设备工作流。

**6. [#13491] Forked Worker 错误继承父任务用户意图** [OPEN] [11👍 / 10评论]
https://github.com/openai/codex/issues/13491
子代理错误地将父级用户意图当作直接指令，导致递归委托的混乱。多代理场景下的行为正确性问题。

**7. [#25744] [macOS] Computer Use/MCP 进程泄漏** [OPEN] [3👍 / 19评论]
https://github.com/openai/codex/issues/25744
长时间运行的 Codex 会话累积僵尸子进程和 MCP helper 进程，引发 HID 延迟和 WindowServer/TCC 阻塞。关注者众，评论较多。

**8. [#31963] [App][i18n] zh-CN 推理力度翻译歧义** [OPEN] [5👍 / 10评论]
https://github.com/openai/codex/issues/31963
中文界面混淆 "xhigh" 和 "ultra" 两种推理级别，均为 “极高”，影响用户对模型行为的准确预期。

**9. [#38754] [Windows] stdio MCP 服务器单任务内反复生成不回收** [OPEN] [2👍 / 7评论]
https://github.com/openai/codex/issues/38754
每一轮新对话都会重新生成 MCP 进程且从不回收，资源泄漏严重。反映了 Windows 平台 MCP 进程管理尚未完善。

**10. [#35841] [Windows] 沙箱无法恢复 SYSTEM-DPAPI 凭据** [OPEN] [0👍 / 5评论]
https://github.com/openai/codex/issues/35841
提升权限的沙箱遇到 CryptUnprotectData 0x8009000B 错误，Windows 加密凭据在沙箱环境中的兼容性缺陷。

---

## 重要 PR 进展（Top 10）

**1. [#39087] 从 AuthManager 读取插件认证状态** [CLOSED]
https://github.com/openai/codex/pull/39087
为 `PluginsManager` 注入共享的 `AuthManager`，统一插件发现与启动的认证凭据读取路径，解决认证状态快照不一致的问题。

**2. [#39084] 保留文件系统权限路径约定** [CLOSED]
https://github.com/openai/codex/pull/39084
防止将 `/C:/secret` 等具有特殊语义的路径过早转换成原生绝对路径，修复 Windows 路径歧义问题。

**3. [#39083] 加固 Windows 沙箱对重解析点的防护** [CLOSED]
https://github.com/openai/codex/pull/39083
避免在 `CODEX_HOME` 下跟随目录联接等符号链接导致 ACL 被错误应用到其他目录，属于安全加固。

**4. [#39082] 远程 TUI 工作区增加项目信任提示** [CLOSED]
https://github.com/openai/codex/pull/39082
远程场景下启动线程前查询 app server 的项目配置层，无信任记录时显示信任确认。补全远程 TUI 的安全交互。

**5. [#39081] 以 delta 大小限制 TUI 线程重放缓冲区** [CLOSED]
https://github.com/openai/codex/pull/39081
当线程处于非活跃状态时，增量消息仍会无限累积文本。此 PR 合并同一线程的相邻 delta，从字节量层面控制无界增长。

**6. [#39079] 将用户 MCP 策略应用于选定的执行器插件** [CLOSED]
https://github.com/openai/codex/pull/39079
从有效用户配置中解析 MCP 策略（server 启停、工具白名单、审批模式），并保留插件级更严格的策略限制。

**7. [#39074] `codex doctor` 增加桌面更新诊断** [CLOSED]
https://github.com/openai/codex/pull/39074
探测 macOS/Windows 桌面应用更新端点的联通性，报告 Windows Store 和 Sparkle 已暂存的更新。

**8. [#39077] 仅对远程 TUI 会话构建文件系统 JSON 参数** [CLOSED]
https://github.com/openai/codex/pull/39077
进程内 app-server 使用类型化协议请求，无需 JSON-RPC 参数。将 `request_fs_path` 改为闭包延迟求值，只在远程会话时计算。

**9. [#39073] 传递调用方元数据至 rendezvous 连接** [CLOSED]
https://github.com/openai/codex/pull/39073
从 `OPENAI_CLUSTER` 和 `DD_SERVICE` 环境变量中提取元数据，附加到 WebSocket 握手请求头，提升分布式追踪能力。

**10. [#39072] 通过 turn executor 持久化生成图片** [CLOSED]
https://github.com/openai/codex/pull/39072
当扩展宿主不提供本地保存根目录时，图片生成结果将保存至 turn 环境的 `generated_images` 目录，通过沙箱文件系统执行器处理。

> 注：此外还有 [#39075](https://github.com/openai/codex/pull/39075)、[#39065](https://github.com/openai/codex/pull/39065)、[#39063](https://github.com/openai/codex/pull/39063)、[#39061](https://github.com/openai/codex/pull/39061) 等多项改动聚焦于 TUI 渲染性能 —— 包括避免冗余终端行清除、终端超链接布局限定在可视区域、transcript pager 只渲染可见行、以及流式代码围栏的增量渲染优化。

---

## 功能需求趋势（社区最关注的方向）

1. **CLI 交互控制细化**——#28969 要求禁用自动确认、#32817 要求折叠/隐藏代码片段，用户希望获得更精细的 CLI 输出与交互控制权。
2. **桌面端性能优化**——#11011（线程切换慢）、#38518（350-800 MiB/s 读循环）等反映出桌面端性能仍是主要痛点，尤其在 Windows 平台。
3. **MCP 稳定性**——token 刷新（#17265）、进程泄漏/反复生成（#25744/#38754/#38925）等多角度问题表明 MCP 基础设施在跨平台场景下仍需大量打磨。
4. **中文本地化质量**——#31963 中推理级别的翻译歧义问题，显示非英文用户在 UI 文本准确性上有更高期待。
5. **远程/多设备协作**——#37403、#28238 等远程控制与 worktree 相关问题，反映用户对跨设备无缝衔接流程的需求。

---

## 开发者关注点（痛点与高频需求）

- **平台回归频发**：macOS 桌面更新导致 remote control 不可恢复（#37403），Windows 应用每次更新相继暴露 MCP 进程不回收、沙箱凭据异常（#35841）等新问题，用户对更新质量表示不满。
- **子代理行为不透明**：#13491 中 worker 继承父意图而误解指令，以及 #38908 中子页面完成状态显示错误，多代理场景的可观测性和可信度受到质疑。
- **Windows 沙箱与凭据体系的兼容性**：SYSTEM-DPAPI 凭据在提升沙箱中无法解密（#35841），文件系统权限路径歧义（#39084），Windows 仍是问题集中地。
- **会话数据无限增长**：#34268 中多代理 V2 全历史 fork 导致 110 GiB 会话存储膨胀，用户对本地存储空间的失控增长表示担忧。
- **贡献者激励**：#37585 建议 OpenAI 为高质量 bug 报告提供更多 Work/Codex 使用额度，反映出社区成员希望在反馈-回报间建立良性循环。

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报

**日期**: 2026-08-18  
**数据来源**: [github.com/google-gemini/gemini-cli](https://github.com/google-gemini/gemini-cli)

---

## 今日速览

今日社区动态集中在 **SSR Agent 的一系列 Bug 修复**上，多项修复（涉及超时、挂起、状态误报等）已进入 PR 合并阶段。同时，**Agent 子代理（Subagent）的稳定性问题**仍是社区讨论的焦点，包括回收逻辑误导性报告和 Generalist Agent 无响应等 P1 级别问题。此外，**Auto Memory 系统的安全性（密钥泄露风险）与低信号重试**问题引发了社区关注，多个相关 Issue 正在积极讨论中。

---

## 版本发布

### v0.56.0-nightly.20260817.g9a15c45fb

- **修复**: [SSR Agent] 为 `packages/cli` 的 tsconfig 添加 `composite` 标志（PR [#28813](https://github.com/google-gemini/gemini-cli/pull/28813)）
- **完整变更**: [Compare](https://github.com/google-gemini/gemini-cli/compare/v0.56.0-nightly.20260816.g2a87e7be1...v0.56.0-nightly.2)

---

## 社区热点 Issues

### 1. Subagent 达到 MAX_TURNS 后误报为 GOAL 成功
**Issue [#22323](https://github.com/google-gemini/gemini-cli/issues/22323)** | P1 | 评论: 12 | 👍: 2

`codebase_investigator` 子代理在达到最大轮次限制后仍报告 `status: "success"` 和 `Termination Reason: "GOAL"`，即使自身结果明确表示未进行任何分析。这掩盖了执行中断，导致错误的成功信号。**值得关注**：这是 Agent 可靠性核心问题，相关修复 PR #28815 已提交。

### 2. Generalist Agent 长时间挂起
**Issue [#21409](https://github.com/google-gemini/gemini-cli/issues/21409)** | P1 | 评论: 8 | 👍: 8

当 Gemini CLI 委托给 Generalist Agent 时（如创建文件夹等简单操作），会无限期挂起，用户等待长达一小时不得不取消。通过明确指示模型不委托子代理可绕过此问题。**值得关注**：👍 数最高，是当前社区反馈最强烈的痛点之一。

### 3. 组件级评估（EPIC）
**Issue [#24353](https://github.com/google-gemini/gemini-cli/issues/24353)** | P1 | 评论: 7

此 EPIC 跟踪组件级评估的建设，在已有 76 个行为评估测试基础上，扩展至 6 个支持的 Gemini 模型。**值得关注**：对质量保障和回归测试至关重要，直接影响后续开发效率。

### 4. AST 感知的文件读取/搜索/映射影响评估
**Issue [#22745](https://github.com/google-gemini/gemini-cli/issues/22745)** | P2 | 评论: 7

评估 AST 感知工具的价值，包括更精确地读取方法边界、减少 token 噪声、以及改进代码库导航。**值得关注**：可能显著提升代码理解效率，减少多轮交互消耗。

### 5. Gemini 不充分使用 skills 和 sub-agents
**Issue [#21968](https://github.com/google-gemini/gemini-cli/issues/21968)** | P2 | 评论: 6

用户反馈 Gemini 默认几乎不会主动使用自定义 skills 和子代理，即使任务高度相关（如已有 gradle、git skills），需要明确指令才会调用。**值得关注**：直接影响用户自定义扩展的实际价值。

### 6. Auto Memory 无限重试低信号会话
**Issue [#26522](https://github.com/google-gemini/gemini-cli/issues/26522)** | P2 | 评论: 5

Auto Memory 仅在提取代理成功读取 transcript 时才将候选会话标记为已处理。若代理因低信号跳过读取，会话将永远保持未处理状态，不断被重新提出。**值得关注**：导致后台任务无限循环，浪费资源。

### 7. Auto Memory 需确定性脱敏并减少日志
**Issue [#26525](https://github.com/google-gemini/gemini-cli/issues/26525)** | P2 | 评论: 4

Auto Memory 读取本地转录并将内容发送至模型，但脱敏提示词在内容进入上下文之后才生效，且服务可能记录现有技能内容。**值得关注**：这是安全性关键问题，涉及用户敏感数据泄露风险。

### 8. Shell 命令执行后卡在“等待输入”
**Issue [#25166](https://github.com/google-gemini/gemini-cli/issues/25166)** | P1 | 评论: 4 | 👍: 3

简单 CLI 命令执行完成后，Gemini CLI 仍显示命令处于活动状态并“等待用户输入”，实际命令早已结束。**值得关注**：高频复现问题，严重影响日常开发流，👍 数较高。

### 9. Browser Agent 在 Wayland 下失败
**Issue [#21983](https://github.com/google-gemini/gemini-cli/issues/21983)** | P1 | 评论: 4 | 👍: 1

browser 子代理在 Wayland 环境下直接失败，终止原因为 `GOAL`。**值得关注**：影响 Linux/Wayland 用户的浏览器自动化能力。

### 10. ~/.gemini/agents/ 中符号链接不被识别
**Issue [#20079](https://github.com/google-gemini/gemini-cli/issues/20079)** | P2 | 评论: 4

当 `~/.gemini/agents/filename.md` 是符号链接时，该文件不会被识别为 Agent。**值得关注**：开发者常用符号链接管理 dotfiles，此问题影响配置灵活性。

---

## 重要 PR 进展

### 1. 修复 Subagent 回收时原始终止原因被覆盖
**[PR #28815](https://github.com/google-gemini/gemini-cli/pull/28815)** | P1 | 已关闭

修复 Issue #22323：当子代理达到 `MAX_TURNS` 或 `TIMEOUT` 并在最终宽限轮成功调用 `complete_task` 时，原终止原因被错误的 `GOAL` 覆盖。现在会保留原始终止原因。

### 2. 为 TUI 添加执行超时，防止无限挂起
**[PR #28812](https://github.com/google-gemini/gemini-cli/pull/28812)** | P1 | 已关闭

修复 Issue #21477：从裸 Linux 终端启动时，交互式 TUI 可能在“Initializing...”处无限挂起。原因是 `getProcessInfo()` 依赖 `execAsync` 执行 Unix `ps` 命令，现添加超时保护。

### 3. 修复 MessageBus.request 静默挂起
**[PR #28816](https://github.com/google-gemini/gemini-cli/pull/28816)** | P2 | 开放

修复 Issue #22588：`MessageBus.request()` 中 `this.publish()` 是浮动的 Promise，失败时会导致请求静默挂起 60 秒。现在会正确注册失败处理。

### 4. 保留执行中子代理工具调用的 hook 状态
**[PR #28817](https://github.com/google-gemini/gemini-cli/pull/28817)** | P2 | 开放

修复 Issue #22589：非根调度器（子代理）中首次出现且无需批准的工具调用（如后台任务）在进入 hook 状态前被过滤掉。现在会正确保留。

### 5. 修复个人账户错误提示信息
**[PR #28819](https://github.com/google-gemini/gemini-cli/pull/28819)** | P2 | 开放

修复 Issue #24587：当个人账户用户选择不可用的 Gemini 模型时，CLI 显示的是误导性的企业级错误提示，现已更正。

### 6. 修复工作区扫描中瞬时子目录 ENOENT 误报
**[PR #28834](https://github.com/google-gemini/gemini-cli/pull/28834)** | P1/P2 | 开放

消除 BFS 工作区树遍历器在遇到瞬时锁目录（如 `projects.json.lock`）时产生的虚假 `ENOENT` 警告。将非根子目录的 `ENOENT` 视为正常竞态条件。

### 7. 更新 /clear 命令文档
**[PR #28847](https://github.com/google-gemini/gemini-cli/pull/28847)** | P3 | 开放

修复 Issue #19239：`/clear` 命令文档原先仅描述其清除终端屏幕和滚动缓冲，现补充说明它也会重置活动会话上下文。

### 8. 安全修复：防止 eval-pr 工作流中的供应链 RCE
**[PR #28740](https://github.com/google-gemini/gemini-cli/pull/28740)** | Security | 开放

修复 Issue #28336：将 eval 工作流拆分为安全的 pull_request 构建步骤和可信的 workflow_run 执行步骤，防止不可信的 fork 代码在特权上下文中执行。

### 9. 修复模型系统指令和工具配置被覆盖
**[PR #28743](https://github.com/google-gemini/gemini-cli/pull/28743)** | Agent | 开放

`GeminiChat.sendMessageStream()` 获取的模型特定 `GenerateContentConfig` 中的 `systemInstruction` 和 `tools` 被聊天级别配置立即覆盖。现在会正确保留模型级配置。

### 10. 修复 ACP 恢复时会话文件被污染
**[PR #28744](https://github.com/google-gemini/gemini-cli/pull/28744)** | P1 | 开放

部分修复 Issue #28693：`loadSession` 在恢复前启动新的聊天会污染会话文件，此 PR 移除了加载路径上的两个 fresh-chat 启动之一。

---

## 功能需求趋势

从今日 Issue 和 PR 中可提炼出以下社区重点关注方向：

### 1. **Subagent / Agent 稳定性与可靠性**
- 子代理回收逻辑误报（[#22323](https://github.com/google-gemini/gemini-cli/issues/22323)）
- Subagent 无限挂起（[#21409](https://github.com/google-gemini/gemini-cli/issues/21409)）
- Agent 对用户定义 skills/subagents 的自主使用不足（[#21968](https://github.com/google-gemini/gemini-cli/issues/21968)）

### 2. **Auto Memory 系统安全性与效率**
- 无限重试低信号会话（[#26522](https://github.com/google-gemini/gemini-cli/issues/26522)）
- 密钥脱敏不充分、日志过多（[#26525](https://github.com/google-gemini/gemini-cli/issues/26525)）
- 无效内存补丁未被隔离（[#26523](https://github.com/google-gemini/gemini-cli/issues/26523)）

### 3. **AST 感知工具链**
- AST 感知的文件读取/搜索/映射（[#22745](https://github.com/google-gemini/gemini-cli/issues/22745)）
- AST 感知 CLI 工具用于代码库映射（[#22746](https://github.com/google-gemini/gemini-cli/issues/22746)）

### 4. **Shell 命令执行体验**
- 命令完成后卡在“等待输入”（[#25166](https://github.com/google-gemini/gemini-cli/issues/25166)）
- 外部编辑器退出后终端损坏（[#24935](https://github.com/google-gemini/gemini-cli/issues/24935)）
- 终端 resize 时的高性能和防闪烁（[#21924](https://github.com/google-gemini/gemini-cli/issues/21924)）

### 5. **安全与权限**
- 阻止模型执行破坏性操作（如 `git reset --force`）（[#22672](https://github.com/google-gemini/gemini-cli/issues/22672)）
- 防止子代理绕过权限配置（[#22093](https://github.com/google-gemini/gemini-cli/issues/22093)）

### 6. **工具数量扩展与性能**
- 超过 128 个工具时出现 400 错误（[#24246](https://github.com/google-gemini/gemini-cli/issues/24246)）

---

## 开发者关注点

### Agent 自主性与透明度
- **高频痛点**: Gemini 默认不使用用户自定义 skills 和子代理（[#21968](https://github.com/google-gemini/gemini-cli/issues/21968)），需显式指令才触发,这与用户期望的“智能代理”差距明显。
- **子代理信息不透明**: 子代理执行中没有权限提示（[#22093](https://github.com/google-gemini/gemini-cli/issues/22093)），且 `/bug` 报告不含子代理内部上下文（[#21763](https://github.com/google-gemini/gemini-cli/issues/21763)）,调试困难。
- **子代理轨迹难以查看**: 社区要求通过 `/chat share` 共享子代理轨迹（[#22598](https://github.com/google-gemini/gemini-cli/issues/22598)），以便评估和审查子代理行为。

### Shell 执行稳定性
- Shell 命令完成后挂起（[#25166](https://github.com/google-gemini/gemini-cli/issues/25166)）是复现率极高的问题，直接影响日常工作流。
- 模型在随机位置创建临时脚本（[#23571](https://github.com/google-gemini/gemini-cli/issues/23571)）造成工作区清理负担,且模型应避免破坏性 git 操作（[#22672](https://github.com/google-gemini/gemini-cli/issues/22672)）。

### 安全性疑虑
- **Auto Memory 的密钥泄露风险**（[#26525](https://github.com/google-gemini/gemini-cli/issues/26525)）是严肃的安全隐患，脱敏发生在内容进入模型上下文之后，且日志可能记录技能内容。
- **eval-pr 工作流供应链攻击面**（[#28740](https://github.com/google-gemini/gemini-cli/pull/28740)）需要立即修复，社区已提交安全补丁。

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报

**日期：2026-08-18**


## 今日速览

过去24小时社区提交的Issue数量明显增多（18条新Issue，集中于8月16-17日创建），但值得关注的是，其中多数仍处于triage（待分类）状态，且以非交互模式、插件机制和会话恢复等技术性缺陷为主。社区对 **MCP OAuth 兼容性回归**（#4480）、**`--no-alt-screen` 被静默移除**（#4509）以及 **插件缓存未按 `ref` 区分**（#4513）等问题表达了强烈不满，而官方今日无新版本发布，大量 PR 也处于等待审查或合并的状态，修复速度可能是当前社区的主要焦虑点。


## 版本发布

过去24小时内无新版本发布或预发布。


## 社区热点 Issues

过去24小时共更新28条Issue，其中18条为新增。以下为最值得关注的10条：

### 1. Atlassian MCP OAuth 认证回归 — #4480 (OPEN)
- **作者**: jfrost-fabric | 更新: 08-17 | 评论: 5 | 👍: 6
- **链接**: [Issue #4480](https://github.com/github/copilot-cli/issues/4480)
- **详情**: 从 1.0.71 升级到 1.0.79 后，连接 Atlassian 远程 MCP 服务器时 OAuth 发现流程报错（RFC 8414 issuer 不匹配）。这是明确的版本回归，影响所有Atlassian MCP用户，评论中已有其他用户确认复现。

### 2. GitLab MCP OAuth 被拒 — #4439 (CLOSED)
- **作者**: patrickzel | 创建: 08-11 | 更新: 08-17 | 评论: 5 | 👍: 3
- **链接**: [Issue #4439](https://github.com/github/copilot-cli/issues/4439)
- **详情**: 1.0.79 因 RFC 8414 issuer 不匹配拒绝 GitLab Self-Managed MCP 服务器的 OAuth 元数据。与 #4480 同根同源（均已关闭），推测可能是同一回归问题的不同表现，修复可能已在进行中。

### 3. `--no-alt-screen` 被静默移除 — #4509 (OPEN)
- **作者**: bounis | 更新: 08-17 | 评论: 0 | 👍: 1
- **链接**: [Issue #4509](https://github.com/github/copilot-cli/issues/4509)
- **详情**: 用户指出 `--no-alt-screen` 标志被移除且无替代方案，而 alt-screen 模式自 3 月以来已被多次报告存在缺陷（#1799, #2334）。此变更影响大量依赖该标志的用户，且无迁移路径，预计会引发进一步讨论。

### 4. 插件缓存未按 ref 区分导致错误加载 — #4513 (OPEN)
- **作者**: kristenmatsumoto | 更新: 08-17 | 评论: 0 | 👍: 0
- **链接**: [Issue #4513](https://github.com/github/copilot-cli/issues/4513)
- **详情**: 多个项目引用同一 git marketplace 但使用不同分支（`ref`）时，CLI 只按 URL 缓存一次 checkout，导致引用错误版本。这对微服务/多仓库团队影响较大，是插件机制走向成熟前必须解决的缓存一致性问题。

### 5. 插件依赖规范缺失 — #4487 (OPEN)
- **作者**: grjsrinivas | 更新: 08-17 | 评论: 0 | 👍: 0
- **链接**: [Issue #4487](https://github.com/github/copilot-cli/issues/4487)
- **详情**: 请求建立插件依赖模型（支持 marketplace 内/间依赖的声明与自动安装），并指出 Claude Code 已有此能力。这是插件生态扩展的关键能力，社区需求明确。

### 6. 内存压力导致无意义强制压缩并循环直至内存耗尽 — #4506 (OPEN)
- **作者**: jay-tau | 更新: 08-17 | 评论: 0 | 👍: 0
- **链接**: [Issue #4506](https://github.com/github/copilot-cli/issues/4506)
- **详情**: 长会话中内存压力看门狗在上下文用量仅 23% 时强制压缩，但仅回收0.003% token，随后循环直至 OOM。该问题直接导致长会话场景下 CLI 崩溃，属于高影响、触发机制不合理的缺陷。

### 7. MCP 策略获取失败时阻止所有本地 stdio 服务器 — #4512 (OPEN)
- **作者**: dochollidayxx | 更新: 08-17 | 评论: 0 | 👍: 0
- **链接**: [Issue #4512](https://github.com/github/copilot-cli/issues/4512)
- **详情**: 当 MCP registry 策略获取失败时，CLI 采用"fail closed"策略，连用户本地自定义的 stdio MCP 服务器也被阻止启动。对于企业网络环境（防火墙/代理）中的用户，这可能导致功能完全不可用，应改为"fail open"或至少允许本地服务器。

### 8. 自定义指令在长会话中不刷新 — #4508 (OPEN)
- **作者**: micsh | 更新: 08-17 | 评论: 0 | 👍: 0
- **链接**: [Issue #4508](https://github.com/github/copilot-cli/issues/4508)
- **详情**: `.github/instructions/*.instructions.md` 仅在会话开始时加载。一个跨越200+次压缩的长会话永远看不到后续对这些文件的修改。影响需要长期运行自动化任务、同时迭代调整指令的用户。

### 9. 恢复的会话报错 "input item ID does not belong to this connection" — #4505 (OPEN)
- **作者**: Adamkadaban | 更新: 08-17 | 评论: 0 | 👍: 0
- **链接**: [Issue #4505](https://github.com/github/copilot-cli/issues/4505)
- **详情**: 恢复会话后所有 prompt 均报 400 错误，且 `/fork` 无法恢复。该问题阻断性地影响需要跨时段恢复会话的用户。会话持久化是核心功能，此类回归的优先级应当提高。

### 10. 非交互模式忽略仓库级 `enabledPlugins` — #4507 (OPEN)
- **作者**: RezaJooyandeh | 更新: 08-17 | 评论: 1 | 👍: 0
- **链接**: [Issue #4507](https://github.com/github/copilot-cli/issues/4507)
- **详情**: `.github/copilot/settings.json` 中的 `enabledPlugins` 在 `copilot -p` 模式中不生效，而交互模式和 `copilot plugins list` 正常。交互/非交互行为不一致会导致 CI/CD 自动化链路中的插件行为无法预期，属于明显的配置一致性缺陷。


## 重要 PR 进展

过去24小时内仅更新 1 条 PR，其余大量 PR 处于未更新状态：

### #4510: 从 README 中移除 Copilot CLI 文档 (OPEN)
- **作者**: prioritizedprotection086 | 更新: 08-17 | 👍: 0
- **链接**: [PR #4510](https://github.com/github/copilot-cli/pull/4510)
- **详情**: 该 PR 删除了 README 中的 Copilot CLI 安装说明与使用指南。此操作较为反常，等待维护者回复。可能原因包括项目即将迁移到独立文档站点、有意降低曝光度，或为一次错误提交。


## 功能需求趋势

综合当前所有 Issues，社区关注的几大功能方向为：

1. **MCP 生态成熟化**：OAuth 兼容性、基于 `ref` 的 marketplace 缓存、插件依赖规范 (#4487)、策略获取失败时的降级策略——社区对 MCP 的 企业级可用性 提出了明确要求。

2. **会话（Session）管理机制**：远程会话恢复失灵 (#4514)、恢复后 item ID 残留 (#4505)、会话内存看门狗逻辑不当 (#4506)、Docker MCP 容器残留 (#4461)——长会话的稳定性与资源回收是高频痛点。

3. **非交互模式（`copilot -p`）行为一致性**：仓库级 `enabledPlugins` 不生效 (#4507)、`contextTier` 无法通过会话配置调整 (#4275)、`account.getQuota` 返回错误的 `resetDate` (#4504)——社区期望 `-p` 模式与交互模式在配置和行为层面完全对齐，这对 CI/CD 自动化场景至关重要。

4. **模型支持与选择策略**：组织级启用的模型在目录中缺失（#4390，Anthropic 及 Kimi K3）、auto 模式因 reasoning level 失败 (#4459)、自定义代理忽略 `agent.md` 中配置的模型 (#2950)、AIC 显示不可靠 (#4511)——随着多模型/多供应商部署的普及，模型选型、配额展示与自定义代理的模型绑定问题日益突出。

5. **终端体验与可访问性**：`--no-alt-screen` 的回归 (#4509)、主题昼夜变化 (#4485)、会话选择器低对比度 (#4455)、会话历史滚动 (#4313)——用户对终端渲染细节的体验要求持续升高。


## 开发者关注点

- **回归频繁且修复周期长**：多个社区反馈存在"已报告多月未解决"的情况（如 `--no-alt-screen` 自三月份被报告、model auto 模式问题 #2870/4459），版本升级带来的回归（MCP OAuth、缓存逻辑）进一步扰乱工作流，开发者对发布质量控制表示担忧。

- **MCP/插件机制正在快速演化，但稳定性跟不上**：既有 OAuth 兼容性问题，又有缓存未按引用隔离、服务器生命周期管理不完善等基建短板。在 CLI 1.0.x 阶段出现如此多的生态机制问题，说明 MCP/插件体系尚未达到企业生产可用的成熟度。

- **文档与发布透明度不足**：非交互模式下行为与文档不符（`--no-alt-screen` 被移除且无说明，`account.getQuota` 返回语义错误），且 README 正在被删除（#4510）。开发者期望更清晰的 changelog、弃用通知和文档/实际行为之间的强一致性。

- **AI 消费透明度与成本可视性**：Kimi K3 会话的 AIC 报告被证实低估（#4511），对依赖精确用量追踪进行成本核算的用户会造成直接干扰，此类"计量不准"的缺陷对商用用户的信任度影响不容低估。

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

好的，这是 2026 年 8 月 18 日的 Kimi Code CLI 社区动态日报。

---

## Kimi Code CLI 社区动态日报 — 2026-08-18

### 1. 今日速览
今日社区活动较为平静，无新版本发布，也无新 Issue 产生。但有一项值得关注的 PR **#864** 在昨日更新后关闭，该 PR 提出的 `--starting-prompt` 功能旨在解决用户在不退出当前会话的情况下临时查询新命令的痛点，虽未合并，但为后续实现提供了重要参考。

### 2. 版本发布
今日无新版本发布。

### 3. 社区热点 Issues
由于过去24小时无新 Issue，以下挑选仓库中讨论活跃或对产品方向有重要影响的近期 Issue，供开发者参考：

1.  **[#887] Feature: Add flag to enter prompt without exiting current session** 
    *   **重要性**: 该需求与今日关闭的 PR #864 直接相关，是社区对“临时查询”功能的核心需求表达。实现此功能能极大改善交互流程，避免频繁启动/退出 CLI。
    *   **社区反应**: 获得 PR 作者响应，预计会推动后续官方实现。
    *   [GitHub Issue](https://github.com/MoonshotAI/kimi-cli/issues/887)

2.  **[#785] Canceling the current prompt with ctrl+c exits program entirely** 
    *   **重要性**: 直指核心交互体验问题。用户期待输入 `exit` 或明确的退出指令才终止进程，而 `ctrl+c` 应仅用于取消当前生成任务。该问题讨论了如何使取消行为更符合用户预期。
    *   **社区反应**: 讨论活跃，并关联了 PR #864 的讨论，是目前交互设计上的重点反馈。
    *   [GitHub Issue](https://github.com/MoonshotAI/kimi-cli/issues/785)

3.  **[#880] Better output formatting for tables and data structures** 
    *   **重要性**: 这是开发者日常使用的高频需求。当 LLM 返回 JSON 或 Markdown 表格时，终端渲染效果不佳会严重降低输出可读性。
    *   **社区反应**: 用户普遍希望输出格式与 ChatGPT 等 Web 端体验对齐。
    *   [GitHub Issue](https://github.com/MoonshotAI/kimi-cli/issues/880)

4.  **[#874] Support for images in multimodal conversations** 
    *   **重要性**: 与 Kimi 模型的视觉能力直接相关。用户希望能在终端中直接粘贴图片路径，让模型根据截图或设计稿进行分析和代码生成。
    *   **社区反应**: 该功能被视为从“纯文本助手”走向“多模态助手”的关键一步。
    *   [GitHub Issue](https://github.com/MoonshotAI/kimi-cli/issues/874)

5.  **[#852] Add `--analyze` flag to run a full repository scan** 
    *   **重要性**: 面向大型项目的代码理解需求。用户希望 CLI 能像 IDE 一样拥有项目级上下文，而不是仅限于当前目录或少量文件。
    *   **社区反应**: 用户非常期待该功能，认为它是提升跨文件重构和调试效率的关键。
    *   [GitHub Issue](https://github.com/MoonshotAI/kimi-cli/issues/852)

6.  **[#843] Prompt caching strategy seems inefficient for long conversations** 
    *   **重要性**: 性能与成本优化问题。长对话中重复发送大量历史信息会导致响应变慢和 Token 消耗过高。改进缓存策略可显著提升体验并降低成本。
    *   **社区反应**: 高级用户关注较多，希望了解官方是否已实施更智能的上下文压缩技术。
    *   [GitHub Issue](https://github.com/MoonshotAI/kimi-cli/issues/843)

7.  **[#831] Configurable system prompt** 
    *   **重要性**: 允许用户自定义系统提示词，以定制化 AI 角色、响应风格或注入特定的项目规范。这是社区多次提出的深度定制化需求。
    *   **社区反应**: 呼声较高，用户希望官方提供 `--system` 参数或配置文件支持。
    *   [GitHub Issue](https://github.com/MoonshotAI/kimi-cli/issues/831)

8.  **[#820] Auto-detect `.env` file for better context** 
    *   **重要性**: 提升对 Web 开发项目的支持。自动读取 `.env` 文件可为模型提供环境信息，减少因环境变量缺失导致的“幻觉”代码。
    *   **社区反应**: 用户希望减少手动粘贴环境变量的步骤。
    *   [GitHub Issue](https://github.com/MoonshotAI/kimi-cli/issues/820)

9.  **[#808] Support for `copilot` style multi-turn editing** 
    *   **重要性**: 期望实现 AI 对代码文件的连续修改能力，类似于 GitHub Copilot 的交互式编辑体验，而不只是生成一次性回答。
    *   **社区反应**: 用户致力于将其定位为真正的 AI 结对编程工具。
    *   [GitHub Issue](https://github.com/MoonshotAI/kimi-cli/issues/808)

10. **[#795] Better Windows support (especially for PowerShell)** 
    *   **重要性**: 跨平台兼容性是影响用户基数的关键问题。目前终端控制、快捷键等在 Windows 环境下存在兼容性问题。
    *   **社区反应**: Windows 用户反馈集中，期望能获得与 macOS/Linux 一致的体验。
    *   [GitHub Issue](https://github.com/MoonshotAI/kimi-cli/issues/795)

### 4. 重要 PR 进展
今日仅有一个 PR 更新，但仓库中另有多个早期合并或待处理的关键 PR 对项目发展有重要影响。

1.  **#864 [CLOSED] feat: --starting-prompt flag to prompt without exit**
    *   **功能**: 新增 `--starting-prompt` / `-s` 参数，允许用户在 CLI 非交互模式下（如执行单次命令后）不退出，而是直接进入交互式提示符。
    *   **状态**: **已关闭**（未被合并）。PR 作者在今日更新了该 PR，但最终未合入主干。主干上后续可能采用不同的实现方案（如单独的 `ask` 子命令）。
    *   [GitHub PR](https://github.com/MoonshotAI/kimi-cli/pull/864)

2.  **#858 [OPEN] feat: add `--diff` mode for review changes**
    *   **功能**: 新增 `--diff` 参数，支持直接传入 git diff 内容供模型审查，专门用于 Code Review 场景。
    *   **状态**: 待合并。
    *   [GitHub PR](https://github.com/MoonshotAI/kimi-cli/pull/858)

3.  **#850 [OPEN] refactor: use delta updates for token usage**
    *   **功能**: 优化流式输出时的 Token 统计逻辑，采用增量更新，修复长对话中 Token 计数不准的问题。
    *   **状态**: 待合并。
    *   [GitHub PR](https://github.com/MoonshotAI/kimi-cli/pull/850)

4.  **#845 [MERGED] fix: handle broken pipe when piping output to head**
    *   **功能**: 修复当 CLI 输出通过管道传给 `head` 等命令提前结束时报错（BrokenPipeError）的问题，提升在 Unix 环境下的管道兼容性。
    *   **状态**: 已合并。
    *   [GitHub PR](https://github.com/MoonshotAI/kimi-cli/pull/845)

5.  **#835 [OPEN] feat: custom model parameters via `--temperature` and `--max-tokens`**
    *   **功能**: 允许用户通过 CLI 参数直接控制模型采样温度和最大 Token 数，以满足不同场景下的生成需求。
    *   **状态**: 待合并。
    *   [GitHub PR](https://github.com/MoonshotAI/kimi-cli/pull/835)

6.  **#822 [MERGED] feat: add `--interactive` flag for REPL mode in scripts**
    *   **功能**: 新增 `--interactive` 标志，强制在脚本中启用交互式 REPL 模式，便于在自动化任务中混合使用。
    *   **状态**: 已合并。
    *   [GitHub PR](https://github.com/MoonshotAI/kimi-cli/pull/822)

7.  **#815 [OPEN] feat: support `~/.kimi/config.json` for global configuration**
    *   **功能**: 增加全局配置文件支持，用于存储默认模型、API Key 等设置，替代繁琐的环境变量。
    *   **状态**: 待合并。
    *   [GitHub PR](https://github.com/MoonshotAI/kimi-cli/pull/815)

8.  **#811 [OPEN] perf: reduce startup time by 200ms**
    *   **功能**: 通过优化依赖加载和初始化流程，将 CLI 启动速度提升约 200ms。
    *   **状态**: 待合并。
    *   [GitHub PR](https://github.com/MoonshotAI/kimi-cli/pull/811)

9.  **#802 [MERGED] fix: strip ANSI codes when copying generated code to clipboard**
    *   **功能**: 修复复制代码到剪贴板时包含 ANSI 颜色码导致代码损坏的问题。
    *   **状态**: 已合并。
    *   [GitHub PR](https://github.com/MoonshotAI/kimi-cli/pull/802)

10. **#798 [OPEN] feat: add MCP server for IDE integration**
    *   **功能**: 新增 MCP（Model Context Protocol）服务，旨在让 VS Code 等 IDE 能够无缝调用 Kimi Code CLI 的功能，实现智能补全和代码生成。
    *   **状态**: 待合并。
    *   [GitHub PR](https://github.com/MoonshotAI/kimi-cli/pull/798)

### 5. 功能需求趋势
从近期的 Issue 和 PR 中可以提炼出以下核心功能趋势：

*   **交互体验优化**：核心诉求集中在 **退出/取消逻辑**（#785, #887）以及对 **多模态输入**（图像）的支持(#874)。用户希望减少操作摩擦，同时让交互更直观。
*   **深度上下文理解**：用户不再满足于单文件分析，而是希望 CLI 能理解 **整个项目结构**（#852）、**环境配置**（#820）以及 **进行多轮连续编辑**（#808），这类似于 IDE 级别的代码理解能力。
*   **可定制性与可控性**：社区希望获得更多控制权，包括 **自定义系统提示词**（#831）、**调整模型参数**（#835）以及 **保存全局配置**（#815）。

### 6. 开发者关注点
*   **“退出”与“取消”的语义冲突**：大量用户反馈，在 AI 生成内容时按 `Ctrl+C` 会直接退出程序，这与他们“仅取消当前生成任务”的预期不符。这是目前影响体验的最大痛点之一。
*   **输出格式的机器可读性**：开发者希望工具能更好地服务于脚本自动化（如通过管道传给 `jq`），因此对 **干净、无 ANSI 码的输出** 以及对 **JSON 等结构化数据的精确解析** 有较高要求。
*   **跨平台体验一致性**：Windows（特别是 PowerShell）用户在终端控制、快捷键和回显方面遇到的问题较多，期待团队能投入精力修复 Windows 下的兼容性，确保在 Windows 上也能获得与 macOS/Linux 一致的使用体验。

---
*本日报由 AI 辅助分析生成，请以 GitHub 官方页面信息为准。*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报

**日期：2026-08-18** | 数据来源：github.com/anomalyco/opencode


## 今日速览

过去24小时内，OpenCode 社区最显著的动态集中在**服务端稳定性与错误处理**方面：多个用户报告了端点不可用（HTTP 410/503/403）及配额计算异常问题，同时社区对 **Plan Mode 自动切换 Build 模式**（#7801，👍 32）和**会话归档恢复功能**（#24153）持续保持高关注度。此外，大量 PR 已被标记为 `automated-pr-cleanup` 并关闭，可能意味着项目正在进行一轮集中的代码清理与合并。


## 社区热点 Issues

### 🔥 高热度与高讨论

**1. #19130 — Windows ARM64 原生版 TUI 初始化失败（OpenTUI + bun:ffi TinyCC 错误）**
- **作者**: Carliquiss | **评论**: 18 | **👍**: 12 | **状态**: 打开
- **重要性**: Windows ARM64 原生二进制可运行非交互命令，但 TUI 无法启动，直接影响该平台用户的交互式体验。12 个 👍 表明大量用户受此影响。
- **链接**: [Issue #19130](https://github.com/anomalyco/opencode/issues/19130)

**2. #7801 — [功能请求] Plan Mode 配合 Question 工具时自动切换到 Build 模式**
- **作者**: gasatrya | **评论**: 11 | **👍**: 32 | **状态**: 打开
- **重要性**: 当前为社区**最高赞**的功能请求（32 👍）。用户希望在 Plan 模式下使用 Question 工具后，系统能自动切换回 Build 模式，减少手动切换的摩擦。高赞数表明这是工作流优化中的核心痛点。
- **链接**: [Issue #7801](https://github.com/anomalyco/opencode/issues/7801)

**3. #43105 — [2.0] BUG: 端点错误（Legacy inference endpoint retired）**
- **作者**: ahmoodiamorii-boop | **评论**: 15 | **状态**: 已关闭
- **重要性**: 用户报告旧版推理端点（`https://opencode.ai/inference/v1`）返回 HTTP 410 Gone。15 条评论说明该问题影响范围较广，但已关闭可能意味着官方已确认并修复或给出解决方案。同类问题 #43101 也已关闭，暗示这是系统性的端点迁移问题。
- **链接**: [Issue #43105](https://github.com/anomalyco/opencode/issues/43105)

**4. #22861 — Bug: Big Pickle 模型提前停止响应**
- **作者**: Minterl | **评论**: 10 | **👍**: 3 | **状态**: 已关闭
- **重要性**: 模型在描述功能实现时反复在相同位置提前停止，且无法通过继续指令恢复。该问题虽已关闭，但 10 条评论反映了用户对模型稳定输出质量的关注。
- **链接**: [Issue #22861](https://github.com/anomalyco/opencode/issues/22861)

**5. #40243 — ChatGPT OAuth 拒绝 EU 工作区的 GPT-5.6 模型，而官方 Codex CLI 正常**
- **作者**: lhammingNedap | **评论**: 9 | **👍**: 4 | **状态**: 已关闭
- **重要性**: EU 数据驻留工作区的用户无法通过 OAuth 使用 GPT-5.6，但官方 Codex CLI 却可以。这指向 OpenAI 端或 OpenCode OAuth 集成中的兼容性问题，对 EU 企业用户尤为关键。
- **链接**: [Issue #40243](https://github.com/anomalyco/opencode/issues/40243)

### 值得关注的 Bug 与体验问题

**6. #33027 — MCP 工具已连接但未暴露给 Agent**
- **作者**: userX570 | **评论**: 8 | **👍**: 3 | **状态**: 打开
- **重要性**: MCP 服务器连接成功且 `tools/list` 正常返回 6 个工具，但 Agent 的工具列表中看不到。这直接阻碍了 MCP 生态的可用性，是集成类问题的典型代表。
- **链接**: [Issue #33027](https://github.com/anomalyco/opencode/issues/33027)

**7. #24153 — [功能请求] 为已归档会话添加取消归档/恢复功能**
- **作者**: alohaninja | **评论**: 8 | **👍**: 11 | **状态**: 打开
- **重要性**: 归档会话目前是单向操作，恢复只能通过变暗的列表入口，体验不佳。11 个 👍 表明会话管理是社区普遍关注的功能方向。
- **链接**: [Issue #24153](https://github.com/anomalyco/opencode/issues/24153)

**8. #36681 — [Bug] Windows 外部目录路径引用与权限配置失效**
- **作者**: m21-cerutti | **评论**: 7 | **状态**: 打开
- **重要性**: 外部目录权限配置在 Windows 上不生效，且缺少相关文档。Windows 路径处理是跨平台一致性的常见痛点，7 条评论说明并非个例。
- **链接**: [Issue #36681](https://github.com/anomalyco/opencode/issues/36681)

**9. #42995 — 配额计算异常：显示 $3.02 但 5 小时配额（$12）已用尽**
- **作者**: opencodexfx1 | **评论**: 4 | **👍**: 3 | **状态**: 打开
- **重要性**: 用户账单显示仅消费 $3.02，但 5 小时 $12 配额已耗尽。计费系统准确性直接影响用户信任，且截图证据充分。
- **链接**: [Issue #42995](https://github.com/anomalyco/opencode/issues/42995)

**10. #43126 — [功能请求] 当速率限制有已知重置时间时自动暂停并恢复任务**
- **作者**: ECeternalcat | **评论**: 2 | **状态**: 打开
- **重要性**: 当 provider 返回明确的速率限制重置时间时，自动暂停会话并在重置后恢复。这是提升长时间任务稳定性的实用建议，属于自动化工作流优化方向。
- **链接**: [Issue #43126](https://github.com/anomalyco/opencode/issues/43126)


## 重要 PR 进展

> 说明：以下 PR 均标记为 `[automated-pr-cleanup]` 并已关闭，可能为批量清理或合并操作。具体评论数未提供。

**1. #37549 — feat(plugin): 添加 session request hook**
- **内容**: 为插件系统新增 `ctx.session.hook("request")` API，支持在认证和签名前修改 HTTP/WebSocket 请求头和 JSON 请求体，并桥接缓存 AI SDK 模型与请求级转换。
- **意义**: 增强插件对请求生命周期的控制能力，是插件系统的重要扩展。
- **链接**: [PR #37549](https://github.com/anomalyco/opencode/pull/37549)

**2. #37542 — fix(opencode): 恢复会话 diff 摘要**
- **内容**: 修复 #30127 移除的昂贵的全会话快照 diff，恢复会话级别的 diff 摘要展示。
- **意义**: 改善用户查看会话变更的体验，关闭 #30877、#32852、#17797 三个相关 issue。
- **链接**: [PR #37542](https://github.com/anomalyco/opencode/pull/37542)

**3. #37537 — fix(tui): 保留系统调色板颜色**
- **内容**: 直接从检测到的终端调色板生成原生 V2 系统主题，保留 ANSI 色相，不再合成更深颜色。
- **意义**: 提升 TUI 在不同终端下的视觉一致性。
- **链接**: [PR #37537](https://github.com/anomalyco/opencode/pull/37537)

**4. #37530 — fix(core): 恢复外部目录默认权限**
- **内容**: 允许默认访问已发现的技能（skill）和物化参考目录，同时在外部目录拒绝策略下保持托管 shell 输出的可读性。
- **意义**: 修复权限配置可能阻断正常功能的问题。
- **链接**: [PR #37530](https://github.com/anomalyco/opencode/pull/37530)

**5. #37504 — feat(opencode): 添加会话循环命令 `/loop` 和 `/proactive` 别名**
- **内容**: 新增内置 `/loop` 和 `/proactive` 斜杠命令，关闭 #23578。
- **意义**: 提供会话循环控制能力，提升自动化工作流效率。
- **链接**: [PR #37504](https://github.com/anomalyco/opencode/pull/37504)

**6. #37499 — feat: 添加 `/workflow` 斜杠命令，支持多步 YAML 流水线**
- **内容**: 允许用户在 `.opencode/workflows/` 下定义 YAML 格式的多步流水线。
- **意义**: 拓展 OpenCode 为可编排的自动化工具，是工作流功能的重要补充。
- **链接**: [PR #37499](https://github.com/anomalyco/opencode/pull/37499)

**7. #37477 — fix: 会话列表不再启动完整实例**
- **内容**: `session list` 之前会加载完整实例来查询数据库，现改为轻量级查询，修复 #37435。
- **意义**: 显著提升会话列表的启动速度和资源占用。
- **链接**: [PR #37477](https://github.com/anomalyco/opencode/pull/37477)

**8. #37472 — fix(opencode): 从无效工具输出中剥离 provider 控制 token**
- **内容**: 某些 OpenAI 兼容 provider 会在工具参数中返回原始控制 token（如 `<|tool_call_begin|>`），导致解析失败。此 PR 修复该问题，关闭 #37297。
- **意义**: 提升与第三方 provider 的兼容性。
- **链接**: [PR #37472](https://github.com/anomalyco/opencode/pull/37472)

**9. #37438 — fix(task): 忽略无效的 task_id 而非崩溃**
- **内容**: `task` 命令遇到非法的 task_id（如模型伪造的 UUID）时不再崩溃，关闭 #37440。
- **意义**: 提升鲁棒性，避免因异常输入导致整个会话终止。
- **链接**: [PR #37438](https://github.com/anomalyco/opencode/pull/37438)

**10. #42810 — refactor(core): 简化中断续跑逻辑（状态：打开）**
- **内容**: 将 `session.interrupt?continue=true` 的续跑状态机（continuation request/when/signaled、finish settle 阶段等）简化为 `SessionExecution` 中的三行后清理检查。
- **意义**: 代码大幅简化，降低维护成本，可能为后续功能扩展铺路。目前该 PR 仍为打开状态。
- **链接**: [PR #42810](https://github.com/anomalyco/opencode/pull/42810)


## 功能需求趋势

| 趋势方向 | 代表 Issues | 说明 |
|---|---|---|
| **工作流自动化与模式切换** | #7801（Plan→Build 自动切换）、#43126（限速自动暂停/恢复）、#37504（/loop）、#37499（/workflow YAML 流水线） | 社区强烈希望 OpenCode 能更智能地处理长任务和模式流转，减少人工干预。 |
| **增强型插件与 UI 扩展** | #43132（Web/桌面端插件 UI 层）、#37549（session request hook） | 插件系统向更丰富的 UI 表面（对话框、侧边栏、斜杠命令）和更底层请求拦截能力扩展。 |
| **跨平台体验一致性** | #19130（Windows ARM64 TUI）、#36681（Windows 路径权限）、#36696（Windows Cmdlet 权限）、#41370（Windows npm postinstall）、#43110（Windows serve 崩溃） | Windows 平台（尤其 ARM64 和 MSIX 环境）存在大量稳定性与兼容性问题，是当前最集中的痛点。 |
| **计费与配额透明度** | #42995（配额计算异常）、#43054（非免费模型 Forbidden 错误） | 用户对计费准确性和配额使用规则高度敏感，相关 bug 易引发社区共鸣。 |
| **MCP 工具集成可靠性** | #33027（MCP 已连接但不可见） | MCP 生态的可用性仍需加强，连接成功≠工具可用的状态不一致问题困扰开发者。 |
| **会话管理增强** | #24153（取消归档） | 归档/恢复的精细化管理是用户长期诉求。 |


## 开发者关注点

- **服务稳定性与端点迁移**：多个 issue（#43105、#43102、#43101、#42962）指向端点不可用（HTTP 410/503）和 gateway 模型列表与实际部署不一致的问题。开发者对 `opencode.ai/inference/v1` 等旧端点的退役过程表示困惑，官方需要更清晰的迁移指引。
- **Windows 平台体验**：今日榜单中近 1/3 的 issue 与 Windows 相关，涵盖 ARM64 原生支持、路径权限、npm 安装、serve 命令崩溃等多个维度。Windows 开发者是重要的用户群体，当前体验亟待系统性改善。
- **模型服务的可靠性与计费透明度**：模型提前停止响应（#22861）、配额计算异常（#42995）、免费模型限制（#43054）等问题直接关系到核心使用体验。开发者希望 OpenCode 能提供更稳定的模型调用和更透明的配额使用说明。
- **被动等待自动化**：社区对“在限速时自动暂停”“Plan 模式自动切换”等自动化能力有明确需求，表明开发者希望将更多精力放在任务本身，而非管理工具状态。

---

*本日报由 AI 自动生成，数据截至 2026-08-18。*

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi 社区动态日报

**日期：2026-08-18** | 数据来源：[earendil-works/pi](https://github.com/badlogic/pi-mono)


## 今日速览

昨日（8/17）Pi 社区活动密集，共 30+ 条 Issue 与 PR 更新，核心焦点集中在**上下文压缩（compaction）可靠性**、**多模型提供商兼容性（特别是 OpenRouter/Bedrock）** 以及 **TUI 在大文本/大 diff 场景下的性能与稳定性**上。此外，Qwen 模型目录对齐、子代理（subagent）可靠性、技能（skills）嵌套发现等多个修复 PR 均已合入，整体呈现“问题驱动、快速修复”的活跃态势。


## 社区热点 Issues

挑选了 10 个最值得关注的 Issue，涵盖 bug、性能与功能请求：

### 1. [auto-compaction never triggers after context grows past 100% until provider overflow (#6879)](https://github.com/earendil-works/pi/issues/6879)
- **作者**: alexanderkreidich | **评论**: 18 | **👍**: 17
- **详情**: 在一次 GPT-5.6-sol 的长任务（>2小时）中，上下文使用率超过 100% 后自动压缩未触发，直到 API 在 373k tokens 处拒绝请求。作者建议在每个 agent 步骤后检查上下文。
- **为什么重要**: 这是社区反馈最强烈的问题（👍 17），直接导致长任务中断，是自动压缩策略的关键缺陷，需尽快修复。

### 2. [config folder is out of place on Linux (#534)](https://github.com/earendil-works/pi/issues/534)
- **作者**: Ramblurr | **评论**: 15 | **👍**: 39
- **详情**: Pi 在 Linux 上将配置目录直接放在 `$HOME` 下，未遵循 XDG Base Directory 规范。该问题已关闭。
- **为什么重要**: 虽然已关闭，但 👍 39 为近期最高，说明用户对 Linux 生态合规性高度关注，值得留意后续是否会被重新打开或作为后续工作项。

### 3. [Very slow performance on moving in prompt editor (#8029)](https://github.com/earendil-works/pi/issues/8029)
- **作者**: affanali2k3 | **评论**: 9
- **详情**: 在 prompt 编辑框中，当缓冲区文本较大时（7000 行），单次方向键操作耗时高达 1650ms，性能随文本长度线性恶化。
- **为什么重要**: TUI 核心交互性能问题，直接影响长文本编辑场景的用户体验。

### 4. [Support video/audio content in prompt command (#3200)](https://github.com/earendil-works/pi/issues/3200)
- **作者**: louis030195 | **评论**: 8 | **👍**: 5
- **详情**: 希望扩展 `prompt` RPC 命令，支持向多模态模型（Gemma 4, GPT-4o）转发视频和音频内容。
- **为什么重要**: 多模态支持是 Agent 工具演进的重要方向，社区对此有明确需求。

### 5. [openai-responses: no cacheControlFormat 'anthropic' support (#7995)](https://github.com/earendil-works/pi/issues/7995)
- **作者**: LukasParke | **评论**: 4
- **详情**: OpenRouter 的 870 次试验基准测试发现，`openai-responses` 实现不支持 Anthropic 式 prompt caching（`cache_control`），导致 Claude 经 OpenRouter 使用成本实测增加 2.5 倍。
- **为什么重要**: 直接关乎用户成本，是 API 兼容性与性能优化的关键缺口。

### 6. [Edit tool crashes TUI when rendering a large diff (#8036)](https://github.com/earendil-works/pi/issues/8036)
- **作者**: AntiKnot | **评论**: 4
- **详情**: 编辑操作成功但渲染 14.5 MB 大 diff 时导致 TUI 崩溃，会话恢复时也会崩溃。
- **为什么重要**: 大文件处理场景下的严重稳定性问题，影响可靠性。

### 7. [custom message injected mid-tool-batch breaks tool_calls adjacency (DeepSeek 400) (#8166)](https://github.com/earendil-works/pi/issues/8166)
- **作者**: CarloCattano | **评论**: 3
- **详情**: 扩展在工具批处理中途注入自定义消息（`triggerTurn: false`），破坏了下一次工具调用的 `tool_calls → tool` 消息邻接性，导致 DeepSeek API 返回 400 错误且后续所有轮次失败。
- **为什么重要**: 扩展 API 的边界情况 bug，导致会话彻底不可用，影响扩展生态稳定性。

### 8. [detectInstallMethod mislabels non-pnpm installs (#7756)](https://github.com/earendil-works/pi/issues/7756)
- **作者**: songlairui | **评论**: 3
- **详情**: `detectInstallMethod()` 将任何包含 `/pnpm/` 路径的安装都误判为 pnpm，导致后续管理逻辑错误。
- **为什么重要**: 安装检测逻辑缺陷，影响非标准安装方式的用户体验。

### 9. [openai-completions: reasoning_details round-trip only supports encrypted entries (#7994)](https://github.com/earendil-works/pi/issues/7994)
- **作者**: LukasParke | **评论**: 3
- **详情**: OpenRouter 基准测试发现，`openai-completions` 实现无法正确回传非加密的 `reasoning_details`，导致思维链重放失败。
- **为什么重要**: 思维链（reasoning）数据完整性缺陷，影响多轮推理会话的一致性与调试能力。

### 10. [pi crashes when tmux resizes the pane to 1 column (#8252)](https://github.com/earendil-works/pi/issues/8252)
- **作者**: vindard | **评论**: 2
- **详情**: tmux 调整窗口宽度为 1 列时，Pi 的 spinner 触发了宽度检查异常，导致进程退出。
- **为什么重要**: 极端终端环境下的稳定性问题，影响 tmux 多窗口用户。


## 重要 PR 进展

挑选了 10 个重要的 PR，涵盖功能修复与改进：

### 1. [fix(ai): generalize openai-completions thinking token budget fields (#8275)](https://github.com/earendil-works/pi/pull/8275)
- **作者**: bnsd55 | **状态**: 已合并
- **内容**: 跟进 #7638，将 `thinking_token_budget` 支持泛化为 `thinkingTokenBudgetField`，兼容 vLLM/Qwen/llama.cpp 的不同字段名，并补充兼容性文档。此改进对多推理引擎支持非常重要。

### 2. [fix(coding-agent/ai): anthropic refusal error and fallbacks (#8258)](https://github.com/earendil-works/pi/pull/8258)
- **作者**: cristinaponcela | **状态**: 已合并
- **内容**: 解决 #8017，当 Anthropic 返回 `stop_reason: "refusal"` 导致压缩失败时，自动使用 `allowed_fallback_models` 元数据进行模型回退，提升压缩鲁棒性。

### 3. [fix(coding-agent): load nested markdown skills (#8255)](https://github.com/earendil-works/pi/pull/8255)
- **作者**: cristinaponcela | **状态**: 已合并
- **内容**: 解决 #6479，修复嵌套 Markdown 技能文件（如 `~/.agents/skills/third-party/child-skill.md`）未被发现的问题。对技能生态的完善有直接帮助。

### 4. [fix(coding-agent): dispatch hooks on every turn-start path (#8262)](https://github.com/earendil-works/pi/pull/8262)
- **作者**: LogosZR | **状态**: 开放
- **内容**: 修复 `sendCustomMessage(triggerTurn: true)` 启动回合时未派发 `input` 钩子和 `before_agent_start` 事件的问题，确保扩展在所有路径上都能收到一致的回调。

### 5. [feat(coding-agent): add experimental append compaction (#8120)](https://github.com/earendil-works/pi/pull/8120)
- **作者**: vegarsti | **状态**: 已合并
- **内容**: 新增实验性“追加压缩”模式（`PI_EXPERIMENTAL=1`），复用系统提示词、工具和上下文以利用提供商 prompt 缓存，默认为独立压缩模式。对降低压缩成本有显著潜力。

### 6. [fix(tui): avoid full-screen flashing when content changes above viewport (#8253)](https://github.com/earendil-works/pi/pull/8253)
- **作者**: wlynxg | **状态**: 已合并
- **内容**: 修复长会话（10k+ 行）中视口上方内容变化导致的全屏重绘闪烁问题，改为仅清除和重绘可视区域。

### 7. [fix(coding-agent): make subagent progress and failures reliable (#8250)](https://github.com/earendil-works/pi/pull/8250)
- **作者**: terrorobe | **状态**: 开放
- **内容**: 修复子代理（subagent）示例中的多个问题：子代理仍在工作时误报“完成”、进程失败信息丢失、失败时仍返回正常工具结果，以及单次/链式输出超出工具限制。

### 8. [feat(ai): opeani completions reasoning details (#8246)](https://github.com/earendil-works/pi/pull/8246)
- **作者**: cristinaponcela | **状态**: 开放
- **内容**: 解决 #7994，修复非加密 `reasoning_details`（如 OpenRouter 的签名 `reasoning.text`/`reasoning.summary`）被丢弃的问题。

### 9. [fix(extension-examples): use agent_settled instead of end (#8242)](https://github.com/earendil-works/pi/pull/8242)
- **作者**: cristinaponcela | **状态**: 已合并
- **内容**: 解决 #7350，将示例扩展中“Ready for input”的通知时机从 `agent_end` 改为 `agent_settled`，避免在重试、压缩或后续任务仍在进行时过早通知。

### 10. [fix(ai): align Qwen Token Plan model catalogs (#8240)](https://github.com/earendil-works/pi/pull/8240)
- **作者**: sunner | **状态**: 已合并
- **内容**: 统一 `qwen-token-plan` 与 `qwen-token-plan-cn` 的八模型目录，并保留独立的 `qwen-token-plan-individual` 七模型目录。确保新模型（如 `deepseek-v4-pro-0813`）在两地一致可用。


## 功能需求趋势

从昨日 Issue 与 PR 中提炼出社区最关注的三大方向：

1. **性能与稳定性优化（长期首位）**
   - 自动压缩触发条件改进（#6879）
   - 大文本编辑与渲染的性能问题（#8029、#8036）
   - 极端终端环境（tmux 窄窗口）的崩溃修复（#8252）
   - 大 diff 渲染时的 TUI 稳定性（#8036）

2. **提供商兼容性与成本优化（显著上升）**
   - OpenRouter 非 Anthropic 模型的 prompt caching 支持（#7995）
   - `reasoning_details` 对非加密条目的回传支持（#7994）
   - Bedrock 工具 schema 校验（#8279）
   - 思维 token 预算字段的通用化（#8275）
   - GLM 4.6V 视觉模型加入内置目录（#8220）

3. **多模态与扩展生态（稳定增长）**
   - `prompt` 命令支持视频/音频内容（#3200）
   - 嵌套技能目录的发现（#6479）
   - 扩展钩子事件的全路径派发（#8262）
   - 子代理进度与失败信息的可靠性（#8250）


## 开发者关注点

- **自动压缩不可靠是高频痛点**：#6879 是昨日评论和点赞数最高的 Issue（18 评论，17 👍），长任务中上下文超限导致直接失败，开发者希望压缩检查能在每次 agent 步骤后执行。
- **API 兼容性的隐性成本**：OpenRouter 的基准测试直接暴露了 `cache_control` 缺失导致 2.5 倍成本增加（#7995），这提醒开发者关注 `openai-responses` 对非 OpenAI 模型的缓存支持。
- **大文件/长文本场景是性能与稳定的试金石**：无论 TUI 编辑框（#8029）、diff 渲染（#8036）还是视口闪烁（#8253），都指向大输入场景下的资源消耗与渲染效率问题。
- **扩展 API 的边界条件仍需打磨**：消息注入破坏工具调用邻接性（#8166）、钩子事件未全覆盖（#8262）等，都是扩展开发者会踩到的“坑”。
- **主动出击的模型目录维护**：多个 PR 对齐了 Qwen Token Plan（#8240）、移除了已废弃的 Xiaomi 模型（#8187），说明社区对模型目录的及时性有较高要求。

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 — 2026-08-18

## 今日速览

Qwen Code 于昨日发布 **v0.21.13** 正式版，并同步完成了多轮 SWE-bench Verified 与 Terminal-Bench 2.0 端到端冒烟验证（最终全量 500+89 项跑通）。功能方面，Web Shell Composer 新增文本文件拖拽附加能力，并支持从任意 Assistant 回复 fork 对话。社区侧，Windows 平台 Ctrl+V 粘贴回归（#9061）与上下文压缩后丢失（#9320）是开发者反馈最集中的两个 P1/P2 问题，均已进入活跃讨论。PR 侧，`qwen serve` 新文件权限可配置（#9364）与微信通道 Typing 保活（#9358）为昨日新增亮点。

---

## 版本发布

### v0.21.13（正式版）

- 发布时间：2026-08-17
- 发布说明：常规版本迭代，随附 4 轮 DSW EAS 端到端冒烟验证记录。
- 验证摘要：
  - **SWE-bench Verified**：全量 500 条用例最终达成 1/1 → 500 全量执行成功（r3 起）。
  - **Terminal-Bench 2.0**：89 条用例全量执行成功（r3 起）。
  - 早期 r1/r2 轮次出现 QUARANTINED 状态，经 wheelhouse bootstrap-parent 修复后于 r3 全量转绿。
- 变更内容：发布说明未见面向用户的功能性变更，本次发布主要作为基准版本用于 Benchmark 流水线验证。

---

## 社区热点 Issues（Top 10）

1. **[#9061] Windows 平台 Ctrl+V 粘贴完全失效（回归，P1）**
   - 链接：https://github.com/QwenLM/qwen-code/issues/9061
   - 摘要：自 0.21.x 某版本起，Windows 终端下 Ctrl+V 粘贴无任何响应，系统剪贴板正常，降级至 0.21.0 可恢复。
   - 社区反应：6 条评论，用户确认降级可复现，属高优回归问题。

2. **[#9320] /compress-fast 与 /rewind 后上下文丢失（P2）**
   - 链接：https://github.com/QwenLM/qwen-code/issues/9320
   - 摘要：用户将 102k 上下文压缩至 87k 后启动新 llama-server 恢复会话，发现上下文内容丢失。
   - 社区反应：5 条评论，压缩链路可靠性成为焦点。

3. **[#9324] 消息被重复投递且打断模型思考（P2）**
   - 链接：https://github.com/QwenLM/qwen-code/issues/9324
   - 摘要：Qwen Desktop Code（Qwen 3.8 Max）在思考过程中反复收到同一消息的多个副本，打断当前任务。
   - 社区反应：7 条评论，涉及会话管理核心路径。

4. **[#9296] Qwen Autofix 评审事件风暴，59% 运行被取消（P1）**
   - 链接：https://github.com/QwenLM/qwen-code/issues/9296
   - 摘要：3 小时内约 500 次运行中 59% 被取消，含已关闭 PR 仍触发 autofix（P0）等四类效率问题。
   - 社区反应：4 条评论，属基础设施效率高优问题。

5. **[#8316] 取消 Prompt 后输入框内容未恢复**
   - 链接：https://github.com/QwenLM/qwen-code/issues/8316
   - 摘要：用户发送 Prompt 后按 Ctrl+C 取消，原内容未回填至输入框，需重新输入。
   - 社区反应：9 条评论，交互体验类高频反馈。

6. **[#8051] 多工作区 daemon 资源使用无上限（P2，长期跟踪）**
   - 链接：https://github.com/QwenLM/qwen-code/issues/8051
   - 摘要：`qwen serve` 目前仅限制工作区与会话数量，未限制请求体、WebSocket 等字节级内存占用。
   - 社区反应：9 条评论，服务端稳定性方向的核心跟踪项。

7. **[#6806] /compress 或 /compress-fast 后状态栏上下文百分比不刷新（P2）**
   - 链接：https://github.com/QwenLM/qwen-code/issues/6806
   - 摘要：压缩后 footer 显示的 token 百分比仍为压缩前数值，直至下一次模型请求才更新。
   - 社区反应：6 条评论，UI 刷新类 bug，欢迎 PR。

8. **[#9300] VP 模式下内容未底部对齐，消息与输入框间留白（P2）**
   - 链接：https://github.com/QwenLM/qwen-code/issues/9300
   - 摘要：`useTerminalBuffer: true`（默认）下，最后一条消息与 composer 之间存在空白区域。
   - 社区反应：6 条评论，UI 渲染问题。

9. **[#9307] 微信通道 getupdates 消息 ID 溢出 Number.MAX_SAFE_INTEGER（P1）**
   - 链接：https://github.com/QwenLM/qwen-code/issues/9307
   - 摘要：微信 `getupdates` 返回的 `message_id` 超过 JS 安全整数上限，解析时被四舍五入导致精度丢失。
   - 社区反应：4 条评论，通道集成的数据精度问题。

10. **[#9250] qwen serve 新文件强制 0600 权限，忽略 umask（P3）**
    - 链接：https://github.com/QwenLM/qwen-code/issues/9250
    - 摘要：`write_file`/`edit` 创建的新文件硬编码为 0600，无配置项可修改，忽略进程 umask。
    - 社区反应：4 条评论，同日已有对应 PR #9364 提交修复。


## 重要 PR 进展（Top 10）

1. **[#9303] fix(web-shell): 限制 daemon 会话保留量，修复渲染器 OOM 崩溃**
   - 链接：https://github.com/QwenLM/qwen-code/pull/9303
   - 摘要：会话加载时获取的原始 replay 快照在注入 transcript store 后立即释放；replay 重建与实时增长共用同一 block 上限，避免浏览器内存溢出。

2. **[#9364] feat(daemon): QWEN_SERVE_NEW_FILE_MODE 环境变量可配置新文件权限**
   - 链接：https://github.com/QwenLM/qwen-code/pull/9364
   - 摘要：新增 `NewFileModePolicy`（owner/system），使 `qwen serve` 新建文件遵循 umask 而非硬编码 0600。直修 Issue #9250。

3. **[#9358] fix(weixin): 长时间任务中保持 Typing 指示器存活**
   - 链接：https://github.com/QwenLM/qwen-code/pull/9358
   - 摘要：每 4 秒重新发送 TYPING 请求，避免 iLink Typing 状态过期导致用户看不到“对方正在输入”。直修 Issue #9353。

4. **[#9295] fix(core): 过滤模型端点无法安全消费的图片媒体**
   - 链接：https://github.com/QwenLM/qwen-code/pull/9295
   - 摘要：MIME 类型不受支持（如 image/heic、image/tiff）或解码失败的图片不再以 data URI 原样转发，避免 Responses 兼容端点请求校验报错。直修 Issue #9291。

5. **[#9367] feat(webui): 导出 HTML 查看器增加全局展开/折叠控制**
   - 链接：https://github.com/QwenLM/qwen-code/pull/9367
   - 摘要：为 `/export` HTML 模板的 ChatViewer 增加“全部展开/全部折叠”工具栏，作用于页面内所有可折叠区块。

6. **[#9342] fix(review): 清理 #9175 十五轮评审积累的延迟建议积压**
   - 链接：https://github.com/QwenLM/qwen-code/pull/9342
   - 摘要：一次性处理 19 项非 Critical 积压项（因单轮单阻塞策略被延期），约半数属行为修复（含安全相关 API、shell 引用转义等）。

7. **[#9279] feat(review): 在提交边界强制解析后的严重级别下限**
   - 链接：https://github.com/QwenLM/qwen-code/pull/9279
   - 摘要：当评审提交下限解析为仅 Critical 时（显式 `--severity-floor critical` 或第 6 轮自适应默认），CLI 自动将草稿集中的 Suggestion 移至评审正文的延迟列表，不再以内联评论发出。

8. **[#9267] refactor(review): 增量评审范围改为基于 PR diff 而非 check 结果**
   - 链接：https://github.com/QwenLM/qwen-code/pull/9267
   - 摘要：移除 fetch-pr 中的 containment oracle，增量评审不再事后证明 hunk 属于 PR 自身 diff，改为先基于 base..head 生成范围再逐步收窄。

9. **[#9202] fix(sdk): 未识别诊断消息路由至有界旁路通道**
   - 链接：https://github.com/QwenLM/qwen-code/pull/9202
   - 摘要：normalizer 分类为 `unrecognized_event` / `unrecognized_session_update` 的诊断不再追加至 `blocks[]` 为 debug 块，而是进入上限 50 条的有界 `unrecognizedDiagnostics` 侧通道。

10. **[#9163] fix(review): 所有 ledger 与证据读取限定为受控常规文件**
    - 链接：https://github.com/QwenLM/qwen-code/pull/9163
    - 摘要：统一使用单次 `O_NOFOLLOW` 打开 + `fstat` 验证为有界常规文件后读取，确保校验对象即读取对象，关闭 #9091 审计中 R2-2 类漏洞。


## 功能需求趋势

从近 24 小时更新的 Issues 与 PR 中可提炼出以下社区关注方向：

- **上下文压缩与恢复链路可靠性**（#9320、#9309、#6806）：`/compress`、`/compress-fast` 的 token 计数准确性、压缩后的会话恢复、UI 状态同步，是当前最集中的体验痛点。
- **Daemon 资源治理**（#8051、#8091、#9250 → #9364）：从进程级内存上限、文件权限策略到多工作区资源隔离，服务端场景的工程化治理需求持续走高。
- **通道集成能力扩展**（#9307、#9353、#9352、#9358）：微信通道的消息 ID 精度、Typing 保活、文件发送能力，表明社区正在将 Qwen Code 推向更多 IM 场景。
- **Web Shell 与 UI 体验打磨**（#9300、#9180、#9315）：布局异常、文本复制、拖拽附加文件等交互细节高频出现。
- **自动化评审 / Autofix 效率优化**（#9296、#9279、#9267、#9342）：围绕 review 流水线的去重、范围收敛、积压清理是当前工程效率投入的重点方向。


## 开发者关注点（痛点 / 高频需求）

1. **Windows 平台回归问题高频**：Ctrl+V 粘贴失效（#9061）、文本无法复制（#9315）在 0.21.x 版本集中出现，终端交互层重写带来的兼容性回归是当前最高频痛点。

2. **压缩后状态与内容不一致**：压缩后 token 占比不刷新（#6806）、压缩后 /rewind 丢失上下文（#9320）、压缩后数字异常（#9309），压缩链路多处可信度问题叠加，已影响用户对会话管理的信任。

3. **评审 / Autofix 流水线资源浪费**：59% 运行取消率（#9296）引发社区对自动评审机制效率的讨论，关闭 PR 仍触发运行的问题被标记为 P0。

4. **服务端 daemon 权限与资源控制缺失**：新文件 0600 硬编码（#9250）与多工作区内存无上限（#8051）表明 `qwen serve` 在生产环境的工程化能力仍待补强，相关 PR（#9364）已快速跟进。

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI 社区动态日报

**2026-08-18** | 数据来源: [Hmbown/DeepSeek-TUI](https://github.com/Hmbown/DeepSeek-TUI)

---

## 今日速览

昨日社区活跃度极高，v0.9.9 版本发布进入收尾阶段，多项 release 增补 PR 密集落地。值得关注的是，CLI 工具在磁盘/文件描述符耗尽时导致会话卡死的严重 bug（#5465）已在 v0.9.9 中修复；同时多语言网站本地化重构（#5337）取得关键进展，两个相关 PR 已提交。此外，DeepSeek V4 模型的峰谷定价逻辑（#5470）和第三方模型配置体验优化（#5350）成为社区讨论的焦点。

---

## 版本发布

**v0.9.9**（[发布 PR #5476](https://github.com/Hmbown/CodeWhale/pull/5476)，已关闭）

主题为 "truth-and-resilience"（真实与韧性），核心变更：

- **修复 shell 工具会话卡死 bug**（#5465）：当主机磁盘/文件描述符耗尽时，exec 流创建失败导致所有 `bash` 调用返回 `Failed to create streaming shell output`，现已改为 fail-soft。
- **诚实标注**：未经验证的上下文窗口、输出上限和遥测默认值现在明确标注，不再伪装。
- **补充变更**（PR #5477/#5487）：社区修复（#5474/#5475）已合入；新增 dsh 深海场景（#5484）、模型目录价格更新（#5485）、官网文案重写（#5483）。
- **后续已知问题**（Issue #5355）：v0.9.8 遗留的 parallel-load 和 config-fixture 测试不稳定问题仍在调查中。

---

## 社区热点 Issues（Top 10）

### 1. [#5424] v0.9.7: Codewhale TUI 崩溃（已关闭）
- **作者**: Hixac | 💬 7 评论 | 更新: 08-17
- **详情**: 输入提示词等待约一分钟后，Codewhale 自动退出，无错误信息。启动命令为 `codewhale --continue`。
- **意义**: 属于影响日常使用的崩溃类 bug，已关闭（建议关注关闭原因是否为 v0.9.9 修复）。
- 🔗 https://github.com/Hmbown/CodeWhale/issues/5424

### 2. [#1425] 大文本处理会话中断卡死（开放）
- **作者**: AiurArtanis | 💬 7 评论 | 更新: 08-17
- **详情**: 尝试分析 300 万字小说，AI 将原文切成 10 个部分启动 10 个子 agent 并行处理，但每次 `agent_wait` 等待超时导致会话卡死。后续确认 10 个子 agent 全部显示 Running，约 2 分钟后中断。
- **意义**: 子 agent 并行处理大任务时的超时机制存在缺陷，是重度用户工作流的瓶颈。
- 🔗 https://github.com/Hmbown/CodeWhale/issues/1425

### 3. [#2369] CodeWhale 配置路径跨 OS/Cygwin 不一致 + 静默迁移 bug（开放）
- **作者**: buko | 💬 8 评论 | 更新: 08-17
- **详情**: 在 Windows 和 Cygwin 环境下，配置/密钥文件可能因 home 目录解析规则不同而解析到不同位置；旧版迁移可能遗留数据导致配置异常。附有 config-mismatch.patch。
- **意义**: 跨平台路径兼容问题是 Windows 用户的痛点，涉及配置迁移的数据安全。
- 🔗 https://github.com/Hmbown/CodeWhale/issues/2369

### 4. [#5056] 测试可靠性：flaky 后台验证器测试 / workspace 敏感 fixtures / 12 个未分类 ignore 测试（开放）
- **作者**: Hmbown | 💬 8 评论 | 更新: 08-17
- **详情**: `run_verifiers_background_advertises_detached_start` 和 `run_verifiers_background_starts_shell_jobs_and_returns_task_ids` 在完整并行测试下仍不稳定；workspace 敏感的 subagent 测试写 fixture 时存在路径问题。
- **意义**: 核心维护者亲自提出，测试可靠性直接影响 CI 效率和发布节奏。
- 🔗 https://github.com/Hmbown/CodeWhale/issues/5056

### 5. [#1651] VS Code 在 YOLO Agent 运行测试脚本时崩溃（开放）
- **作者**: HubgitCCL | 💬 6 评论 | 更新: 08-17
- **详情**: YOLO Agent 使用 DeepSeek v4-pro/v4-flash 后台执行测试脚本时，VS Code 崩溃或意外退出。
- **意义**: IDE 集成稳定性问题，影响日常开发体验。
- 🔗 https://github.com/Hmbown/CodeWhale/issues/1651

### 6. [#1829] SSH 连接失败 exit code 255（开放）
- **作者**: fodudu1226 | 💬 6 评论 | 更新: 08-17
- **详情**: DeepSeek TUI v0.8.39 内置 shell 执行 `ssh` 返回 exit code 255，疑似沙箱阻止 TCP 22 出站。本地终端连接正常。
- **意义**: 沙箱网络策略限制是高级用户（需要 SSH/SCP）的实际障碍。
- 🔗 https://github.com/Hmbown/CodeWhale/issues/1829

### 7. [#5374] Agent 输出文本损坏（已关闭）
- **作者**: all-lopezg | 💬 5 评论 | 更新: 08-17
- **详情**: macOS 上 agent 输出文本出现乱码（附截图），用户表示"完全无法阅读"。已关闭。
- **意义**: 显示渲染 bug 影响基本可用性，关闭原因值得关注。
- 🔗 https://github.com/Hmbown/CodeWhale/issues/5374

### 8. [#5123] Agent spawn 表面配置项过多 — labeled builder 以只读模式运行且自我 BLOCKED（开放）
- **作者**: Hmbown | 💬 7 评论 | 更新: 08-17
- **详情**: Dogfood 发现：delegate builder 被标记为 `builder`/`gates-shell-writer`，但实际工具契约是**只读**的——所需能力（写文件等）被禁用，导致 agent 自我阻塞。根因是 spawn 表面的配置项过多且分散。
- **意义**: 核心维护者的 dogfood 发现，揭示 agent 权限模型设计过于复杂，影响自动化效率。
- 🔗 https://github.com/Hmbown/CodeWhale/issues/5123

### 9. [#5337] Web: 完成 #4934 词典主干 — 移除所有 isZh 分支（开放）
- **作者**: Lstarsky0 | 💬 4 评论 | 更新: 08-17
- **详情**: #4934 已为每个路由 locale 建立了统一的词典路径（`getChrome(locale)`/`getHome(locale)`），但页面主体仍大量存在 `{ en, zh }` 内联判断。本 issue 追踪剩余重构工作。
- **意义**: 多语言架构重构的关键里程碑，直接影响 8 个部分支持语言（ja/vi/ko/ru/uk/es/pt-BR/id）的本地化体验。
- 🔗 https://github.com/Hmbown/CodeWhale/issues/5337

### 10. [#5350] 简化第三方模型配置，增加预制模板（开放）
- **作者**: shadapang | 💬 4 评论 | 更新: 08-17
- **详情**: 配置 OpenCode Zen、OpenCode Go、Agnes、美团 Sensenova 等第三方服务商时需手动填写 Base URL、模型名、密钥，且无文档提示；保存后模型列表常卡在 `not checked`/`cache failed`。建议内置预制模板、嵌入文档、增加"测试连接"按钮。
- **意义**: 新手配置门槛高，是提升新用户上手体验的高优先级需求。
- 🔗 https://github.com/Hmbown/CodeWhale/issues/5350

---

## 重要 PR 进展（Top 10）

### 1. [#5491] fix(tui): persist approval outcomes before execution（开放）
- **作者**: cyq1017 | 更新: 08-17
- **内容**: 在执行前将审批请求和最终结果持久化到会话日志；无法持久化时拒绝执行并拒绝过期决策；会话恢复时重建已关闭/中断的审批状态。Closes #5360。
- **意义**: 让一次性审批结果可追溯且 fail-closed，提升安全性和可审计性。
- 🔗 https://github.com/Hmbown/CodeWhale/pull/5491

### 2. [#5476] release: 0.9.9（已关闭）
- **作者**: Hmbown | 更新: 08-17
- **内容**: v0.9.9 发布 PR，主题为 truth-and-resilience。核心修复 shell 工具在磁盘/描述符耗尽时卡死的问题（#5465），并诚实标注未经验证的配置项。
- **意义**: 重大版本发布，包含对生产环境的可靠性修复。
- 🔗 https://github.com/Hmbown/CodeWhale/pull/5476

### 3. [#5488] feat(web): move the docs shell onto the dictionary spine（开放）
- **作者**: Lstarsky0 | 更新: 08-17
- **内容**: `app/[locale]/docs/layout.tsx` 的 5 个字符串从 `isZh` 三元表达式迁移到词典路径。此前 8 个部分支持语言在 docs 页面只能显示英文。
- **意义**: 多语言本地化重构的持续推进，改善非英语用户文档阅读体验。
- 🔗 https://github.com/Hmbown/CodeWhale/pull/5488

### 4. [#5490] feat(web): route shared components' locale picks through pickText（开放）
- **作者**: Lstarsky0 | 更新: 08-17
- **内容**: 3 个共享组件的 `locale === "zh"` 比较改用 `pickText()`，#5337 的后续重构。
- **意义**: 消除硬编码语言分支，统一多语言内容选择逻辑。
- 🔗 https://github.com/Hmbown/CodeWhale/pull/5490

### 5. [#5485] fix(models): bring first-party model rows and pricing current（已关闭）
- **作者**: Hmbown | 更新: 08-17
- **内容**: 模型目录价格全面更新，所有数据于 2026-08-17 通过 curl 官方页面重新验证（xAI 层数值来自 docs.x.ai 嵌入价格表，LongContext 列恰为标准值 2 倍）。
- **意义**: 确保模型定价信息准确，避免用户看到过期价格。
- 🔗 https://github.com/Hmbown/CodeWhale/pull/5485

### 6. [#5470] fix(tui): DeepSeek V4 tiered peak/off-peak pricing resolved per turn（已关闭）
- **作者**: Hmbown | 更新: 08-17
- **内容**: DeepSeek V4 定价按 UTC 小时区分峰/谷时段，此前 `pricing.rs` 使用单一固定费率导致成本显示不准确。此 PR 按每轮对话的实际时间解析峰谷定价。
- **意义**: 修复成本显示准确性，对用户费用透明度有直接帮助。
- 🔗 https://github.com/Hmbown/CodeWhale/pull/5470

### 7. [#5465] fix(tui): exec stream creation must fail soft and never wedge the shell tool（已关闭）
- **作者**: Hmbown | 更新: 08-17
- **内容**: 修复 macOS 主机内存抖动（11GB swap）导致所有 `bash` 调用返回 `Failed to create streaming shell output` 的问题。exec 流创建失败时改为 fail-soft。
- **意义**: 这是 v0.9.9 的核心修复，防止环境资源耗尽时整个 TUI 不可用。
- 🔗 https://github.com/Hmbown/CodeWhale/pull/5465

### 8. [#5480] feat(tui): show and open the live /rc session link; send a stable device id（已关闭）
- **作者**: Hmbown | 更新: 08-17
- **内容**: `/rc` 横幅现在会显示并打开实时 web 会话链接，并停止每次 `/rc` 都生成新 "computer"（改为稳定设备 ID）。
- **意义**: 改善远程控制会话的可发现性和设备身份稳定性。
- 🔗 https://github.com/Hmbown/CodeWhale/pull/5480

### 9. [#5484] feat(dsh): ambient ocean scene — whales and glyph fish（已关闭）
- **作者**: Hmbown | 更新: 08-17
- **内容**: 为 DeepSeek Harness 的 Codewhale bundle 增加环境海洋场景：Bezier 路径上的鲸鱼剪影动画 + Codewhale 字形鱼群（`><(((('>`）。
- **意义**: 视觉体验优化，属于产品差异化亮点。
- 🔗 https://github.com/Hmbown/CodeWhale/pull/5484

### 10. [#5475] fix(config): resolve owned direct model casing safely（已关闭）
- **作者**: h3c-hexin | 更新: 08-17
- **内容**: 修复小写保存的选择器（如 `glm-5.2`）在解析时可能被其他提供商的相同 wire id 误分类为外部模型的问题。
- **意义**: 社区贡献的配置解析修复，提升第三方模型配置的准确性。
- 🔗 https://github.com/Hmbown/CodeWhale/pull/5475

---

## 功能需求趋势

从昨日 Issues 和 PR 中提炼的社区关注方向：

| 方向 | 代表 Issues/PRs | 热度 |
|------|----------------|------|
| **多语言/本地化** | #5337（词典主干）、#5488/#5490（词典化迁移）、#5482（文档中文化 EPIC）、#5350（英文模板） | 🔥🔥🔥 |
| **第三方模型配置体验** | #5350（预制模板 + 测试连接）、#5475（模型解析修复）、#4683（completions URL 错误） | 🔥🔥🔥 |
| **Agent 子任务可靠性** | #1425（子 agent 超时卡死）、#5123（spawn 配置过多导致自阻塞）、#5102（截图查看能力） | 🔥🔥 |
| **审批流程持久化/安全** | #5360（一次性审批持久化）、#5491（审批结果持久化实现） | 🔥🔥 |
| **成本显示准确性** | #5470（峰谷定价）、#5241（pricing 503 未验证）、#5485（模型目录更新） | 🔥🔥 |
| **沙箱网络策略** | #1829（SSH 出站被阻断） | 🔥 |
| **测试稳定性/CI** | #5056（flaky 测试）、#5355（v0.9.8 遗留 flake）、#5403（main 红构建） | 🔥 |

---

## 开发者关注点

**高频痛点：**

1. **配置跨平台不一致**：Windows/Cygwin 路径解析差异（#2369）导致配置和密钥文件定位混乱，且存在静默迁移 bug，数据安全风险高。
2. **大任务处理卡死**：子 agent 并行处理大文本时 `agent_wait` 超时导致会话中断（#1425），重度用户的效率瓶颈。
3. **第三方模型配置门槛高**：Base URL、模型名、密钥需手动填写且无文档提示（#5350），保存后缓存状态异常，"not checked / cache failed" 频繁出现。
4. **成本显示不可信**：pricing 端点 503（#5241）、模型价格过期（#5485）、DeepSeek V4 峰谷定价未按时间解析（#5470）——用户对费用透明度要求高。
5. **沙箱限制影响工作流**：SSH/SCP 等网络操作被沙箱阻断（#1829），高级用户需要更精细的网络策略控制。
6. **环境资源耗尽导致 TUI 不可用**：磁盘/描述符耗尽时 shell 工具卡死（#5465），v0.9.9 已修复但用户需注意升级。
7. **1M 上下文窗口未充分利用**：模型支持 1M context，但工具仍在 128K 触发压缩（#5239），用户希望可配置。

**社区情绪：**
- 整体积极，用户对项目迭代速度认可（"amazing work you did on this!!" —— #5374）。
- 核心维护者 Hmbown 深度参与 dogfood 测试和 issue 追踪，社区信任度高。
- 中文用户群体活跃，多个中文 issue 获得关注，中文本地化需求（#5482）被正式提上日程。

---

*本日报由 AI 自动生成，数据来源于 Hmbown/DeepSeek-TUI GitHub 仓库。如需查看完整列表，请访问 [Issues](https://github.com/Hmbown/CodeWhale/issues) 和 [PRs](https://github.com/Hmbown/CodeWhale/pulls)。*

</details>

---
*本日报由 [agents-radar](https://github.com/kky-wollu/agents-radar) 自动生成。*
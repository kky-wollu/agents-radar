# AI CLI 工具社区动态日报 2026-08-08

> 生成时间: 2026-08-07 22:41 UTC | 覆盖工具: 9 个

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

# AI CLI 工具生态横向对比分析报告

**日期：2026-08-08**


## 一、生态全景

AI CLI 工具已从"聊天增强终端"演进为**企业级开发基础设施**：Claude Code 推出 self-hosted runners、Copilot CLI 强化企业策略管控、Gemini CLI 修复 CVSS 8.6 高危 SSRF 漏洞，安全与合规成为各工具比拼的新赛道。所有工具均面临**会话连续性**（长任务中断、自动续接、压缩机制）和**子代理可靠性**（挂起、误报、越权）两大核心痛点，这已成为衡量工具成熟度的关键指标。与此同时，跨端控制（Remote、Web、移动端）和本地模型接入（LM Studio、FreeBSD 支持）正在打开新的使用场景，市场从"单点工具"竞争进入"平台生态"竞争阶段。


## 二、各工具活跃度对比

| 工具 | Releases（近24h）| 热点 Issues | 重要 PRs | 社区热度信号 |
|------|------------------|-------------|----------|-------------|
| **Claude Code** | v2.1.224 | 10 个（Top 👍 191）| 3 个 | highest 👍 请求（191）凸显长会话诉求；大量 stale 清理显示成熟期维护 |
| **OpenAI Codex** | rust-v0.147.0 + 2 个 alpha | 10 个（Top 👍 74）| 10 个（密集合并）| OAuth issue 74 👍 居首；PR 密度全场最高 |
| **Gemini CLI** | v0.54.4 + v0.55.0-preview.2 + nightly | 10 个（P1 占 6）| 10 个（含 2 个安全修复）| 双安全 PR 同日提交；P1 issue 占比高说明稳定性投入加大 |
| **GitHub Copilot CLI** | v1.0.79-6/7/8 | 10 个（Top 👍 23）| 0 个（24h 内）| 版本节奏快（3 个/日）但 PR 活跃度本日较低；skills 子文件夹需求持续高热 |
| **Kimi Code CLI** | 无 | 2 个 | 3 个 | 体量最小；双 PR 竞争修复同一 bug 体现社区专业性 |
| **OpenCode** | v1.18.15 | 10 个（Top 👍 37）| 10 个 | Go 订阅服务遭集中质疑（45 评论）；基础设施 PR 密集 |
| **Pi** | v0.84.1 | 10 个（Top 👍 15）| 10 个 | 压缩机制是最大痛点（15 👍）；扩展生态活跃 |
| **Qwen Code** | v0.21.7 + nightly | 10 个 | 10 个 | 终端渲染问题集中爆发；WebBridge/移动控制布局新场景 |
| **DeepSeek TUI** | 无（v0.9.4 被 CI 阻塞）| 10 个 | 10 个 | v0.9.5 一次性规划 6 个新特性；大型 Rust 文件重构持续多轮 |


## 三、共同关注的功能方向

### 1. 会话连续性与长任务支持
- **Claude Code**（#13354，👍 191）：会话达上限后自动续接，当前最高 👍 请求
- **Pi**（#6879/7020）：压缩超限不触发、压缩后不继续
- **DeepSeek TUI**（#5268）：回合中聊天框"锁死"，需要 queue/cancel 三态契约
- **Qwen Code**：v0.21.7 移除 Goals 50 轮上限，已先行落地
- **Codex**（#37483）：中断轮次时终止遗留 code-mode 单元格

### 2. 子代理/Agent 行为可靠性
- **Gemini CLI**（#22323）：MAX_TURNS 被误报为成功——"假阳性"问题
- **Gemini CLI**（#21409）：Generalist 子代理永久挂起
- **Copilot CLI**（#3980）：Esc 误杀后台 agent
- **DeepSeek TUI**（#5267）：状态显示"结束中"但模型仍在输出
- **Kimi Code**（#2596）：yolo 模式下误删工作区外数据

### 3. 安全与权限边界
- **Gemini CLI**：SSRF 修复（CVSS 8.6）、Node 20 EOL 迁移、js-yaml 安全更新
- **Claude Code**：YAML 注入/符号链接凭据覆盖修复、hook 规则绕过修复
- **Qwen Code**：跨 worktree Git 变更防护、可信 .env 边界
- **Copilot CLI**：企业 allow-auto-only 策略、沙箱代理 URL 强制
- **Kimi Code**（#2596）：yolo 模式数据删除事故

### 4. 跨端/远程控制
- **Claude Code**：self-hosted environments（新发布）
- **Codex**：远程沙箱委托给执行器
- **Qwen Code**：WebBridge 浏览器控制、QR 码手机配对
- **Pi**：Cursor CLI 桥接

### 5. MCP 生态健壮性
- **Claude Code**（#37580）：`~` 路径不展开
- **Codex**（#37453/#12491）：MCP 子进程残留/僵尸进程
- **Gemini CLI**：MCP 相关 issue 持续
- **Copilot CLI**（#4205）：registry 策略与本地配置冲突


## 四、差异化定位分析

| 工具 | 核心定位 | 目标用户 | 技术路线 |
|------|---------|---------|---------|
| **Claude Code** | 企业级 Agent 平台 | 大型团队/企业（Team/Enterprise 计划驱动） | Self-hosted runners 打通自有基础设施；插件源扩展生态 |
| **OpenAI Codex** | 高性能开源 CLI + 桌面端 | 开发者个体到企业（Pro 5x/20x 分层） | Rust 重写追求性能；远程会话 + code-mode 双模式 |
| **Gemini CLI** | Google 生态深度整合 | Google Cloud/Android 开发者 | 深度依赖 Gemini 模型能力；行为评估体系（evals）建设领先 |
| **GitHub Copilot CLI** | GitHub 生态延伸 | GitHub 重度用户/企业（已有 Copilot 订阅） | 企业策略管控（allow-auto-only）；v1.0.79 密集补丁迭代 |
| **Kimi Code CLI** | 轻量快速替代品 | 中文开发者/轻量用户 | 体量最小、迭代最快；社区驱动修复 |
| **OpenCode** | 模型聚合网关 | 多模型用户（Go 订阅模式） | Go 订阅统一接入多模型；TUI 为核心 |
| **Pi** | 高度可扩展的终端 Agent | 扩展开发者/高级用户 | 丰富的 ExtensionAPI；跨 agent 互操作标准化 |
| **Qwen Code** | 中国生态 + 多端协同 | 中国开发者/Qwen 模型用户 | WebBridge/tmux 子 Agent/移动端控制的全场景覆盖 |
| **DeepSeek TUI** | 深层 TUI 体验 | TUI 重度用户/开源爱好者 | Rust 高可维护性重构；Fleet/多 Worker 架构 |


## 五、社区热度与成熟度

**成熟稳定型**（版本节奏平稳，社区讨论聚焦增量优化）：
- **Claude Code**：大量 stale 清理显示项目已进入维护期，新功能按部就班
- **Copilot CLI**：v1.0.79-6/7/8 节奏快但均为小补丁，无重大架构变动

**快速迭代型**（PR 密集，新功能持续落地）：
- **Codex**：单日 10 个 PR 合并，MCP 事件订阅、WebSocket 优化等基础设施持续加固
- **Gemini CLI**：双安全 PR 同日提交 + 模型配置更新，安全优先级显著提升
- **Qwen Code**：新版本 + 10 个重要 PR，多模态 Omni 实验项目推进中
- **Pi**：10 个 PR 覆盖性能/功能/兼容性多维改进，扩展生态明显活跃

**社区建设初期/小而精型**：
- **Kimi Code**：体量最小但社区专业度高，双 PR 竞争修复同一缺陷
- **DeepSeek TUI**：v0.9.5 一次性规划 6 个新特性但发布被 CI 阻塞，工程成熟度有待提升

**服务信任受挑战型**：
- **OpenCode**：Go 订阅服务的 401 封禁与计费异常集中爆发，稳定性受质疑


## 六、值得关注的趋势信号

1. **"AI CLI 即基础设施"已成定局**：Claude Code 的 self-hosted runners、Codex 的远程沙箱委托、Qwen 的跨 worktree 防护——各工具都在向"可信、可管、可审计"的企业级基础设施演进。决策者应优先评估工具的企业治理能力（权限策略、审计日志、网络隔离）。

2. **长会话连续性是所有工具的"阿喀琉斯之踵"**：从 Claude Code 的 👍 191 自动续接请求，到 Pi 的压缩失效，再到 Gemini 的 MAX_TURNS 误报——**"能跑多久不中断"**已成为用户选择工具的核心指标。建议在采用前实测长任务场景。

3. **安全修复进入"军备竞赛"阶段**：Gemini CLI 同日内修复 SSRF（CVSS 8.6）、迁移 Node 版本、更新 js-yaml；Claude Code 同日内修复两个安全缺陷。**模型权限扩大与安全边界收紧的赛跑**将决定哪些工具能进入企业采购名单。

4. **"本地优先 + 远程访问"是产品演进的主线**：Qwen 的 QR 码手机配对、Claude Code 的 self-hosted runners、Codex 的远程会话——**"CLI 为核、多端接入"**正成为各家的标准叙事。对需要远程/移动办公的团队，此维度应纳入选型评估。

5. **Windows 平台是最大短板**：Codex（#10090 开放 7 个月）、Copilot（剪贴板失效、标题被改）、Qwen（中文输入模糊）在 Windows 上问题最集中。对 Windows 团队，需谨慎评估各工具的成熟度。

6. **模型路由/网关成为新战场**：OpenCode Go 订阅遭质疑、Qwen 接入 Kimi/小米、DeepSeek 推出 `model = auto` 自动分级、Copilot 支持 kimi-k3——**多模型聚合与智能路由**正在成为差异化竞争的关键。开发者应关注工具对任意模型/网关的兼容性。

7. **"Agent 自主性"与"用户控制权"的平衡是共同课题**：Gemini 的越权执行、Kimi 的误删数据、Copilot 的权限提示不透明——各工具都在探索危险操作确认、目录白名单、权限模式切换的精细颗粒度。**从"能干活"到"干活前先问"** 的演进值得跟踪。

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

好的，以下是根据 anthropics/skills 仓库数据生成的 Claude Code Skills 社区热点报告。

---

# Claude Code Skills 社区热点报告 (数据截止 2026-08-08)

## 1. 热门 Skills 排行 (Top 5-8)

根据 PR 的评论活跃度与修复的痛点严重程度，以下 Skills 是社区最关注的焦点：

**#1. skill-creator 生态修复 (PR #1298, #1099, #1050, #1323)**
- **功能**：针对官方 `skill-creator` 技能中 `run_eval.py` 脚本在 Windows 平台上的崩溃及触发检测逻辑缺陷进行修复，这些 Bug 导致技能描述优化循环总是返回 `recall=0%`。
- **社区热点**：这是目前社区最集中的痛点。大量用户反馈通过 `skill-creator` 优化技能描述时，评估脚本完全失效，导致优化过程"对着噪声调参"。
- **状态**：Open (多个相关 PR 均未合并)
- **链接**：[PR #1298](https://github.com/anthropics/skills/pull/1298) | [PR #1099](https://github.com/anthropics/skills/pull/1099) | [PR #1050](https://github.com/anthropics/skills/pull/1050) | [PR #1323](https://github.com/anthropics/skills/pull/1323)

**#2. document-typography (PR #514)**
- **功能**：为 AI 生成的文档提供排版质量控制，包括孤字换行、寡行段落（标题滞留页尾）和编号对齐等问题的修复。
- **社区热点**：讨论聚焦于 AI 生成文档的细节质量。用户认为这是 "Every document Claude generates" 都会遇到的问题，需求刚性强，是提升交付物专业度的关键补充。
- **状态**：Open
- **链接**：[PR #514](https://github.com/anthropics/skills/pull/514)

**#3. ODT Skill (PR #486)**
- **功能**：支持 OpenDocument 格式（`.odt`, `.ods`）的创建、填充、读取及转换为 HTML。
- **社区热点**：填补了官方技能库在开源办公文档格式支持上的空白。讨论集中在对 `LibreOffice` 生态和 ISO 标准格式的支持需求上。
- **状态**：Open
- **链接**：[PR #486](https://github.com/anthropics/skills/pull/486)

**#4. DOCX 修复 (PR #541)**
- **功能**：修复 DOCX 技能在添加修订（tracked changes）时，因硬编码 ID 与文档内已有书签冲突而导致的文件损坏问题。
- **社区热点**：属于稳定性修复，直接关系到生成文档的可用性。这源于 OOXML 规范中 `w:id` 共享 ID 空间的复杂性，社区对该问题的技术根因分析讨论深入。
- **状态**：Open
- **链接**：[PR #541](https://github.com/anthropics/skills/pull/541)

**#5. 元技能 (Meta Skills) 扩展 (PR #83, #1367)**
- **功能**：
    - `skill-quality-analyzer` / `skill-security-analyzer`：用于评估其他 Skill 质量与安全性的分析工具。
    - `self-audit`：在交付前对 AI 输出进行机械验证与四维推理质量审查。
- **社区热点**：社区开始关注 Skill 自身的质量、安全性与可靠性，反映出生态正从"能用"向"好用、可信"演进。
- **状态**：Open
- **链接**：[PR #83](https://github.com/anthropics/skills/pull/83) | [PR #1367](https://github.com/anthropics/skills/pull/1367)

**#6. testing-patterns (PR #723)**
- **功能**：提供完整的测试模式技能，涵盖测试理念（Testing Trophy）、单元测试、React 组件测试等。
- **社区热点**：社区对结构化、可复用的测试方法论有明确需求，期望通过标准化提示词来提升代码测试的质量与效率。
- **状态**：Open
- **链接**：[PR #723](https://github.com/anthropics/skills/pull/723)

---

## 2. 社区需求趋势 (来自 Issues)

- **命名空间信任与安全**：社区最关心的是安全信任问题。`#492` 指出社区贡献的 Skills 能在 `anthropic/` 命名空间下分发，存在严重的信任边界滥用风险，可能会诱导用户授权恶意技能。
- **协作与共享机制**：用户期望更便捷的团队协作方式，`#228` 建议在 Claude.ai 中实现组织内的技能直接共享，无需手动发送文件再导入。
- **核心工具稳定性**：`#556` 和 `#1169` 等 Issue 集中反映了对官方 `skill-creator` 工具的强烈不满，其核心评估功能完全不可用，严重阻碍了用户自定义技能的迭代。
- **生态集成**：一部分用户（如 `#29`、`#16`）希望 Skills 能与 AWS Bedrock 或 MCP 协议深度集成，以接入更广泛的企业级工作流。

---

## 3. 高潜力待合并 Skills (近期可能落地)

以下 PR 功能明确、针对性强，且社区讨论活跃，极有可能在近期被官方采纳或合并：

1.  **document-typography (PR #514)**：痛点极其普遍（AI 生成文档的排版问题），解决方案清晰，是高质量补充。
2.  **ODT Skill (PR #486)**：弥补官方案例库在开源格式领域的空白，与 `docx`、`pdf` 形成完整矩阵。
3.  **testing-patterns (PR #723)**：开发者呼声高，且内容体系化，可直接作为通用开发技能的补充。
4.  **SAP-RPT-1-OSS predictor (PR #181)**：垂直领域（企业数据分析）的特定模型集成，若官方重视企业级用户，则合并概率较高。

---

## 4. Skill 生态洞察

**当前社区最集中的诉求是"稳定性与可信度"：一方面迫切要求修复官方核心工具（`skill-creator`）的基础功能缺陷，另一方面强烈呼吁建立针对第三方 Skill 的安全护栏与信任机制。**

---

# Claude Code 社区动态日报

**日期：2026-08-08** | 数据来源：github.com/anthropics/claude-code


## 今日速览

Claude Code 发布 v2.1.224，正式推出 self-hosted environments 功能，允许 Team 和 Enterprise 用户将自有机器或容器接入 Claude Code 的 Web、移动和桌面会话，同时新增 `archive` 插件源支持。社区方面，高赞功能 request（#13354，👍191）——"会话达到限制后自动续接"——持续升温，反映出用户对长时任务连续性的强烈诉求；大量标为 `stale` 的文档类 issue 被统一关闭，显示项目维护正集中清理积压。此外，Fable 5 模型相关的渲染 bug（#81853）和 Linux KVM 环境下的 100% CPU 死锁问题（#77208）是当前最受关注的两个 open bug。


## 版本发布

### v2.1.224
> 链接：https://github.com/anthropics/claude-code/releases

**核心变更：**
- **Self-hosted environments**（新增）：`claude self-hosted-runner` 命令可将自有机器或容器变为 Claude Code Web、移动端和桌面端会话的运行环境（Team 和 Enterprise 计划可用）
- **`archive` 插件源**（新增）：支持通过 HTTPS 从 zip 包安装插件，无需依赖 git


## 社区热点 Issues（Top 10）

### 1. #13354 — 会话达上限后自动续接（FEATURE）
- **状态**：OPEN | 👍 191 | 💬 73 | 创建于 2025-12-08
- **链接**：https://github.com/anthropics/claude-code/issues/13354
- **重要性**：当前社区👍数最高的 open feature request，表明"长会话连续性"是大量用户的核心痛点。用户希望在会话达到限制后不中断工作流，自动开启续接。

### 2. #81853 — Fable 5 模型文本渲染丢失（BUG）
- **状态**：OPEN | 👍 3 | 💬 5 | 创建于 2026-07-28
- **链接**：https://github.com/anthropics/claude-code/issues/81853
- **重要性**：使用 `claude-fable-5` 模型时，包含工具调用的回复中文本部分在终端主视图完全不显示（文本未丢失，可在 Ctrl+O 详细记录中查看）。同一设置下 Opus 4.8 正常工作——指向模型适配层的渲染 bug。

### 3. #77208 — Linux KVM 环境 100% CPU 死锁（BUG）
- **状态**：OPEN | 👍 0 | 💬 3 | 创建于 2026-07-13
- **链接**：https://github.com/anthropics/claude-code/issues/77208
- **重要性**：Claude Code ≥ 2.1.205 在 KVM guest（kvm64 CPU 模型）上 `--version` 也会触发 100% CPU 无输出死锁，且静默破坏 Linux 桌面版 beta 的 Code tab——影响面极广的 regression。

### 4. #77372 — Remote Control 幽灵会话导致 404（BUG）
- **状态**：OPEN | 👍 1 | 💬 3 | 创建于 2026-07-14
- **链接**：https://github.com/anthropics/claude-code/issues/77372
- **重要性**：新注册的 environment 在下次启动时使用不同 session ID 仍返回 404，会话"创建后即丢失"——Remote Control 会话管理存在系统性缺陷。

### 5. #70165 — iOS 1.260618.0 Remote Control 硬崩溃（BUG/Closed）
- **状态**：CLOSED（regression/stale）| 💬 10 | 创建于 2026-06-22
- **链接**：https://github.com/anthropics/claude-code/issues/70165
- **重要性**：打开 Remote Control 会话时主线程栈溢出（Swift KeyPath 元数据导致），iOS 端直接崩溃，已标为 stale 关闭。

### 6. #21531 — BeforeModel/AfterModel Hooks 拦截 LLM 请求（FEATURE/Closed）
- **状态**：CLOSED（stale）| 👍 3 | 💬 9 | 创建于 2026-01-28
- **链接**：https://github.com/anthropics/claude-code/issues/21531
- **重要性**：社区多次提出希望在 LLM 请求/响应层级提供 hook 拦截点，用于成本控制和安全审计，但该请求最终被标记 stale 关闭。

### 7. #64503 — Claude Code Analytics 停止更新（BUG/Closed）
- **状态**：CLOSED（stale）| 👍 6 | 💬 5 | 创建于 2026-06-01
- **链接**：https://github.com/anthropics/claude-code/issues/64503
- **重要性**：Web 端 Analytics 自 5 月 12 日起不再更新，👍 6 说明不少用户依赖该数据做使用量追踪。

### 8. #37580 — MCP 参数 `~` 不展开导致 ENOENT（BUG/Closed）
- **状态**：CLOSED（stale）| 💬 7 | 创建于 2026-03-22
- **链接**：https://github.com/anthropics/claude-code/issues/37580
- **重要性**：`~/.claude.json` 中 MCP 服务器 args 含 `~` 时不展开即传给子进程，导致连接失败。影响所有使用 `~` 路径配置 MCP 的用户。

### 9. #31675 — Bash 自动批准 allowlist 文档缺失（DOCS/Closed）
- **状态**：CLOSED（stale）| 👍 4 | 💬 6 | 创建于 2026-03-07
- **链接**：https://github.com/anthropics/claude-code/issues/31675
- **重要性**：`autoAllowBashIfSandboxed` 与沙箱相关设置的行为边界不清晰，社区要求文档完整列出 bash 自动批准的 allowlist 枚举逻辑。

### 10. #47628 — WebFetch 文档遗漏 HTML 预处理说明（DOCS/Closed）
- **状态**：CLOSED（stale）| 👍 4 | 💬 4 | 创建于 2026-04-13
- **链接**：https://github.com/anthropics/claude-code/issues/47628
- **重要性**：WebFetch 实际会剥离 style/script 并做 HTML 预处理，但文档完全未提及——用户基于错误假设开发可能得到意外的结果。


## 重要 PR 进展

> 注：近 24 小时更新的 PR 共 3 条，以下全量列出并补充背景。

### 1. #84854 — 修复 hooks 文档过期链接（docs）
- **作者**：cassiacarollinee-ship-it | 创建于 2026-08-07
- **链接**：https://github.com/anthropics/claude-code/pull/84854
- **内容**：`bash_command_validator_example.py` 示例脚本仍指向旧 `docs.anthropic.com` URL，而仓库其他 46 处（16 个文件）均已更新到 `code.claude.com`。低风险 housekeeping，帮助用户避免访问失效文档。

### 2. #84747 — hookify 插件规则评估作用域修复（security fix）
- **作者**：alifakbxr | 创建于 2026-08-07
- **链接**：https://github.com/anthropics/claude-code/pull/84747
- **内容**：修复 `load_rules()` 在 `event` 为 `None` 时绕过事件过滤器的问题——`Read`、`Browser` 等未映射到特定事件的工具现在只会触发 `all` 作用域的规则，避免安全规则被意外绕过。

### 3. #84711 — 修复 YAML 注入与符号链接凭据覆盖（security fix）
- **作者**：alifakbxr | 创建于 2026-08-07
- **链接**：https://github.com/anthropics/claude-code/pull/84711
- **内容**：修复 #76580，增加防御性检查防止 YAML 注入和通过符号链接覆盖凭据文件——涉及插件安全性的关键修复。


## 功能需求趋势

从近期 Issues 中可提炼出以下社区关注方向：

1. **会话连续性与长任务支持**（#13354，👍191）
   - "会话达上限自动续接"是目前最强烈的单一诉求，用户希望在长时间代理任务中不被强制中断。

2. **Self-hosted / 自托管基础设施**（v2.1.224 新功能方向）
   - 官方已推出 self-hosted runners，社区对"用自己的机器跑 Claude Code 会话"的需求被验证并得到响应。

3. **Hooks 体系深化**（#21531、#55981）
   - 社区持续要求更细粒度的 hook 拦截点（模型请求/响应层）以及 agent 间异步/事件驱动通信能力。虽然 #21531 被关闭，但方向明确。

4. **MCP 生态健壮性**（#37580、#70386）
   - `~` 展开、HTTP session header 保持等基础细节问题频出——MCP 服务器接入的"最后一公里"体验仍需打磨。

5. **远程/跨端会话管理**（#77372、#70165、#70409）
   - Remote Control 的幽灵会话、iOS 崩溃、会话批量删除等——跨端会话可靠性是 Team/Enterprise 用户关注点。

6. **文档完整性**（大量 DOCS issue）
   - 本轮关闭的大量 stale DOCS issue 覆盖 Hooks 工具名列表、AWS 凭据超时、MCP 二进制输出、交互模式键盘行为等——反映社区对文档精确性的高要求和持续投入。


## 开发者关注点

1. **文档滞后是最大的"隐形税"**
   - 一大批关闭的 DOCS issue（#26702、#25457、#30943、#30938、#30939、#30942、#30935、#30944、#31675、#31681、#34281、#38566 等）均出自同一报告者 coygeek，覆盖从 CLI 参数语义到权限模式行为的方方面面。开发者明显感到文档跟不上功能演进速度。

2. **模型切换后行为不一致**
   - #81853（Fable 5 文本不显示 vs Opus 4.8 正常）表明不同模型在同一 CLI 中可能出现渲染层差异，用户需要模型无关的稳定行为。

3. **安全策略的"意外绕过"与"误伤"并存**
   - 两个安全 PR（#84747、#84711）修复了规则绕过和凭据覆盖风险，而 #70458 则反馈安全审查"误伤"正常提示词——安全策略的精准度是双向痛点。

4. **Remote Control 仍在"长毛期"**
   - 从环境删除、幽灵 404 到 iOS 硬崩溃，Remote Control 体验在多端多场景下仍不稳定，频繁的 crash 和状态不一致消耗开发者信任。

5. **被关闭的"未完成功能"**
   - #21531（模型层 Hooks）、#55981（异步通信 RFC）等增强请求最终标为 stale 关闭，但社区讨论热度仍在——这些"被搁置"的方向可能在未来版本以不同形式回归。

---

*本日报由 AI 技术分析师生成，数据截至 2026-08-08。*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报

**日期：2026-08-08**


## 今日速览

昨日发布 `rust-v0.147.0` 正式版，引入了便携式 Agent 插件安装和对话分段浏览两大功能。社区方面，性能问题（#21527）、OAuth 认证失败（#31573）和 v0.147.0 的 Azure/LiteLLM 回归问题（#37380、#37425）成为讨论焦点，另有多个 Windows 平台相关 bug 报告持续活跃。PR 方面，MCP 事件订阅、WebSocket 延迟优化和沙箱修复密集合并。


## 版本发布

### rust-v0.147.0 (0.147.0)

**新功能：**
- **便携式 Agent 插件**：支持在本地、个人、工作区和远程插件目录中安装和搜索便携式 Agent 插件（PRs #36544, #36409, #36919, #36796）
- **会话管理增强**：可将对话组织为持久化、手动排序的分段，并支持增量浏览长对话记录（PRs #35722, #36007, #36380, #36948）

另有两个预发布版本：`rust-v0.148.0-alpha.2` 和 `rust-v0.148.0-alpha.1`。


## 社区热点 Issues

### 1. #37380 — v0.147.0 回归：Azure Responses 拒绝空函数命名空间描述 `[bug][windows-os][azure][CLI]`
- **作者**: jisunchoii | **评论**: 8 | **👍**: 18
- **链接**: https://github.com/openai/codex/issues/37380
- **要点**: `codex-cli 0.147.0` 通过 Azure API Management 路由时，发送空的 functions namespace description 被 Azure 端拒绝，导致使用自定义 Azure Responses provider 的开发者升级后即失效。

### 2. #37425 — v0.147.0 回归：LiteLLM provider 流式请求持续失败 `[bug][CLI][custom-model]`
- **作者**: CallisteH | **评论**: 4 | **👍**: 2
- **链接**: https://github.com/openai/codex/issues/37425
- **要点**: 从 v0.146.0 升级到 v0.147.0 后，LiteLLM provider 的流式请求一致失败。与 #37380 同为 v0.147.0 引入的 provider 兼容性问题，影响依赖代理/网关的自托管用户。

### 3. #37445 — 打开 ChatGPT 桌面应用静默消耗 Codex 周限额 `[bug][rate-limits][app]`
- **作者**: Tygb99 | **评论**: 4 | **👍**: 0
- **链接**: https://github.com/openai/codex/issues/37445
- **要点**: 无需提交任何提示词，仅打开应用（后台建议运行）即固定扣除 6% 周限额。威胁模型严重——用户可能不知情地耗尽配额。

### 4. #37453 — Windows 恢复历史 subagent 线程产生重复 MCP 和 node_repl 进程栈 `[bug][windows-os][mcp][app][subagent]`
- **作者**: MarkoAvreliy | **评论**: 3 | **👍**: 0
- **链接**: https://github.com/openai/codex/issues/37453
- **要点**: Windows 桌面版打开/恢复历史 subagent 线程时，重复生成 MCP 和 node_repl 进程栈，与 #12491（僵尸进程、内存泄漏）同属 MCP 生命周期管理问题，可能导致资源泄漏。

### 5. #21527 — Codex 太慢了 `[bug][app][performance]`
- **作者**: s7monk | **评论**: 41 | **👍**: 18
- **链接**: https://github.com/openai/codex/issues/21527
- **要点**: VS Code 插件和应用均响应缓慢，持续 3 个月仍开放，41 条评论说明受影响用户广泛。性能是社区最关心的问题之一。

### 6. #31573 — OAuth 认证在 issuer 校验处失败 `[bug][auth][mcp][CLI]`
- **作者**: NiceWaffel | **评论**: 34 | **👍**: 74
- **链接**: https://github.com/openai/codex/issues/31573
- **要点**: 获得 74 👍，是当前热度最高的问题。在 CLI 0.143.0 及以上版本影响 OAuth/MCP 认证流程，Free 用户受影响最大，涉及面广。

### 7. #37415 — Windows Computer Use 报 spawn EPERM；提权沙箱设置失败 `[bug][windows-os][sandbox][computer-use]`
- **作者**: Tuguldur0130 | **评论**: 4 | **👍**: 2
- **链接**: https://github.com/openai/codex/issues/37415
- **要点**: Computer Use 插件在 Windows 上因 WindowsApps ACL 提权失败导致 EPERM 错误，与 #37043（EnumWindows 失败）和 #10090、#13965 等构成 Windows 沙箱问题群。

### 8. #10090 — 提权 Windows 沙箱导致所有命令 `(no output)` `[bug][windows-os][sandbox]`
- **作者**: i4TsU | **评论**: 23 | **👍**: 7
- **链接**: https://github.com/openai/codex/issues/10090
- **要点**: `CreateProcessAsUserW failed: 5` 报错持续 7 个月仍然开放，Windows 沙箱核心流程的长期待解决问题。

### 9. #37442 — 周限额未在指定时间重置 `[bug][rate-limits][app]`
- **作者**: chandler20708 | **评论**: 4 | **👍**: 0
- **链接**: https://github.com/openai/codex/issues/37442
- **要点**: 显示 10:07 重置但到 14:47 仍保持 0%，与 #37445 同属限额提示与状态管理问题。

### 10. #35481 — VS Code Codex Diff 显示 “Oops, an error has occurred” `[bug][code-review][extension][windows-os]`
- **作者**: hajaraph | **评论**: 26 | **👍**: 54
- **链接**: https://github.com/openai/codex/issues/35481
- **要点**: Windows 上打开 Codex Diff 视图即报错，已关闭但获得 54 👍，说明代码审查功能使用广泛。


## 重要 PR 进展

### 1. #37494 — 添加 MCP 事件发现与订阅 `[CLOSED]`
- **链接**: https://github.com/openai/codex/pull/37494
- **内容**: 通过 `McpResourceClient::list_events` 暴露插件运行时事件定义，新增可取消的 `events/stream` 订阅，支持生命周期通知路由。

### 2. #37498 — 进程终止时保留子进程等待器 `[CLOSED]`
- **链接**: https://github.com/openai/codex/pull/37498
- **内容**: 终止时不再中止而是分离子等待器，修复 PTY 子进程未被回收导致退出状态丢失的问题。与 #12491 僵尸进程问题相关。

### 3. #37504 — 禁用 code-mode WebSocket 的 Nagle 算法 `[CLOSED]`
- **链接**: https://github.com/openai/codex/pull/37504
- **内容**: 为出站远程会话 WebSocket 和入站 code-mode 启用 `TCP_NODELAY`，减少小 TCP 写入缓冲导致的延迟。

### 4. #37485 — 连接失败时保持响应流存活 `[CLOSED]`
- **链接**: https://github.com/openai/codex/pull/37485
- **内容**: 将 HTTP 连接失败与其他网络错误分类，采样请求以 5-60 秒指数退避重试，显示 `Reconnecting...` 状态。

### 5. #37492 — 轮次元数据中包含工具命名空间清单 `[CLOSED]`
- **链接**: https://github.com/openai/codex/pull/37492
- **内容**: 新增可选 `tool_namespaces_info` 元数据，描述每个模型可见函数的命名空间、直接/延迟暴露方式及 Code Mode 状态。配合 #37500 移除旧的无界 `code_mode_tool_names` 清单。

### 6. #37497 — 限制诊断日志中的负载追踪 `[CLOSED]`
- **链接**: https://github.com/openai/codex/pull/37497
- **内容**: 将 HTTP 传输、SSE 和 WebSocket 诊断限制为 `DEBUG` 级别持久化，防止高吞吐量负载淹没 SQLite 日志数据库和诊断环形缓冲区。

### 7. #37483 — 中断轮次时同时中断活跃的 code-mode 单元格 `[CLOSED]`
- **链接**: https://github.com/openai/codex/pull/37483
- **内容**: 新增默认关闭的 `code_mode_interrupt` 功能，启用时中断轮次将终止该轮次遗留的所有活跃 code-mode 单元格。

### 8. #37480 — 将远程进程沙箱委托给执行器 `[CLOSED]`
- **链接**: https://github.com/openai/codex/pull/37480
- **内容**: 远程 `exec_command` 保留执行器本地的目录、工作区和权限配置，同时向远程执行器发送沙箱意图，解决远程沙箱不一致问题。

### 9. #37507 — 在响应元数据中包含沙箱模式 `[OPEN]`
- **链接**: https://github.com/openai/codex/pull/37507
- **内容**: 在常规、预热、压缩和分离内存请求的轮次元数据中记录有效权限配置为 `sandbox_mode`，并保留该字段以防客户端覆盖。

### 10. #37486 — 通过实验 API 暴露服务端诊断信息 `[CLOSED]`
- **链接**: https://github.com/openai/codex/pull/37486
- **内容**: 新增生命周期支持的指标：进行中/排队请求数、待处理服务器请求、活跃轮次、实时 MCP 连接数。关联 #37470（实验 API 暴露 app-server 诊断），有助于定位性能问题。


## 功能需求趋势

| 方向 | 代表 Issue | 热度 |
|------|-----------|------|
| **Windows 沙箱/权限修复** | #10090, #13965, #14211, #35718, #37415 | 高（长期未解决） |
| **性能优化** | #21527, #36523（macOS 启动 OOM）, #34663（resume 渲染） | 高 |
| **MCP 稳定性和生命周期** | #12491（僵尸进程）, #35486, #35253, #37453 | 高 |
| **Provider/网关兼容性** | #37380（Azure）, #37425（LiteLLM） | 中（v0.147.0 回归） |
| **限额透明度和准确度** | #37445（后台消耗）, #37442（重置不准） | 中 |
| **远程/多设备体验** | #34652（远程 SSH 审批）, #36257（Android Remote 重复请求） | 中 |
| **上下文窗口扩展** | #28852（1M context） | 中 |
| **自定义信任策略** | #14599（trusted_level 配置） | 低（57👍） |


## 开发者关注点

- **高频痛点**：Windows 平台问题的集中爆发——包括沙箱提权失败、MCP 子进程残留、Computer Use 无法枚举窗口、远程 SSH 审批不响应等，多个严重问题持续数月未解决（#10090 已开放 7 个月）。其次是性能问题，社区对模型响应速度和 UI 交互延迟的容忍度在下降。
- **v0.147.0 回归**：Azure 和 LiteLLM 两个 provider 在 v0.147.0 均出现兼容性问题，说明 0.147.0 对 provider 层的改动引入了意外的行为变化，影响通过网关/代理使用自定义模型的企业用户。
- **Rate Limit 透明度和公平性**：后台静默消耗 6% 周配额、限额不按提示重置等问题引发关注。随着 Codex 付费分层（如 Pro 5x、Pro 20x）的出现，用户对配额计算的敏感性显著提升（#37445、#37442）。
- **背景技术债务清理**：PR 密集度显示出对基础设施韧性的重视——连接重试、子进程回收、日志噪音、WebSocket 延迟等底层改进虽不明显，但在为后续功能打基础。

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报

**日期：2026-08-08** | **数据来源：**[google-gemini/gemini-cli](https://github.com/google-gemini/gemini-cli)


## 今日速览

昨日社区动态聚焦于**安全加固与稳定性修复**：`web-fetch` 工具的 SSRF 高危漏洞（CVSS 8.6）修复 PR 与沙箱 Node 20→22 迁移 PR 同日提交，安全优先级显著提升；同时，**Generalist 子代理挂起**（Issue #21409）与 **MAX_TURNS 被误报为成功**（Issue #22323）等代理稳定性问题持续成为讨论焦点。版本方面，`v0.54.4` 与 `v0.55.0-preview.2` 为补丁修复，`v0.56.0-nightly` 继续滚动更新。功能需求侧，AST 感知代码导航与子代理行为透明度是社区最集中的呼声。


## 版本发布

过去 24 小时内发布了 3 个版本，均为补丁或预览版本：

- **[v0.56.0-nightly.20260807.gd5c9a97dc](https://github.com/google-gemini/gemini-cli/releases/tag/v0.56.0-nightly.20260807.gd5c9a97dc)**（夜间版）：常规滚动更新，包含 v0.55.0-preview.1 的 changelog 及版本号升级。
- **[v0.55.0-preview.2](https://github.com/google-gemini/gemini-cli/releases/tag/v0.55.0-preview.2)**（预览版）：对 v0.55.0-preview.1 的热修复（cherry-pick），修复内容见 PR [#28719](https://github.com/google-gemini/gemini-cli/pull/28719)。
- **[v0.54.4](https://github.com/google-gemini/gemini-cli/releases/tag/v0.54.4)**（稳定版）：包含两处补丁，详见 PR [#28710](https://github.com/google-gemini/gemini-cli/pull/28710)。

> 版本节奏观察：`v0.55.0-preview` 系列正在密集迭代，建议关注 preview 版本的开发者及时跟进；稳定版 `v0.54.x` 分支仍在接收安全补丁。


## 社区热点 Issues（Top 10）

以下按讨论热度与影响面筛选：

1. **[#22323 Subagent recovery after MAX_TURNS is reported as GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)** — P1，12 评论
   **为什么重要**：`codebase_investigator` 子代理在达到最大轮次限制后，状态被误报为 `success` / `GOAL`，**掩盖了实际的中断**——即子代理在未完成任何分析的情况下就被判定成功。这是一个典型的"假阳性"问题，会导致用户对任务完成度产生误判。
   **社区反应**：讨论热度高，标记为 need-retesting，说明维护者已介入但尚未完全复现或修复。

2. **[#21409 Generalist agent hangs](https://github.com/google-gemini/gemini-cli/issues/21409)** — P1，8 评论，👍 8
   **为什么重要**：Generalist 子代理一旦被调用就**永久挂起**（用户等过 1 小时无响应），且仅发生在委派给子代理时。这是影响日常使用体验的高频阻塞问题。
   **社区反应**：8 个 👍 在本批问题中最高，说明受影响的用户面较广。用户已提供临时 workaround（指示模型不使用子代理）。

3. **[#25166 Shell command execution gets stuck with "Waiting input"](https://github.com/google-gemini/gemini-cli/issues/25166)** — P1，4 评论，👍 3
   **为什么重要**：**极其简单的 shell 命令**（不会等待输入的命令）执行完成后，仍显示"等待用户输入"并挂起。该问题与 #21409 类似，均指向 CLI 在进程管理/IO 状态机上的缺陷。建议关注是否与终端渲染层（Ink）或子进程事件处理相关。

4. **[#21983 browser subagent fails in wayland](https://github.com/google-gemini/gemini-cli/issues/21983)** — P1，4 评论，👍 1
   **为什么重要**：浏览器子代理在 **Wayland** 显示服务器协议下直接失败，影响 Linux 用户。属于平台兼容性问题，且标记为 need-retesting，修复方案可能已提交但待验证。

5. **[#22186 get-shit-done output hook causes crash](https://github.com/google-gemini/gemini-cli/issues/22186)** — P1，3 评论
   **为什么重要**：`get-shit-done` 输出钩子在打印用户摘要时**导致 CLI 崩溃**（`businesscasual98` 报告中显示崩溃发生在输出接近完成时）。钩子（hook）机制是 CLI 可扩展性的核心，此崩溃会影响依赖钩子的高级用户。

6. **[#26522 Auto Memory retries low-signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522)** — P2，5 评论
   **为什么重要**：**Auto Memory** 功能对低信号会话**无限重试**，因为只有成功读取会话的 agent 才会将其标记为已处理。这会导致后台任务持续空转，消耗 token 和计算资源。该 issue 与 #26523/#26525 同属 Auto Memory 系列问题，说明这一相对较新的功能仍存在较多边缘 case。

7. **[#26525 Add deterministic redaction and reduce Auto Memory logging](https://github.com/google-gemini/gemini-cli/issues/26525)** — P2，4 评论
   **为什么重要**：**安全问题**——Auto Memory 在模型上下文之外进行重定向，且服务日志可能记录已有技能内容。涉及**密钥泄漏风险**，值得安全敏感用户关注。

8. **[#26523 Surface or quarantine invalid Auto Memory inbox patches](https://github.com/google-gemini/gemini-cli/issues/26523)** — P2，3 评论
   **为什么重要**：无效内存补丁（格式错误、越界目标等）被**静默跳过**，但后台提取器的 pending 摘要仍会读取每个 `.patch` 文件，**可能出现重复尝试或信息不一致**。

9. **[#22093 (Sub)agents running without permission since v0.33.0](https://github.com/google-gemini/gemini-cli/issues/22093)** — P2，3 评论
   **为什么重要**：自 v0.33.0 起，**即使配置中禁用了 agents 模式，子代理仍会被自动使用**。这涉及**权限边界**问题——用户显式配置应被尊重。

10. **[#20079 Symlinked agent files not recognized](https://github.com/google-gemini/gemini-cli/issues/20079)** — P2，4 评论
    **为什么重要**：`~/.gemini/agents/` 下的 **symlink 文件不会被识别为 agent**，限制了用户通过符号链接管理配置的灵活性。小问题但影响使用体验，属于"简单修复高收益"类型。


## 重要 PR 进展（Top 10）

1. **[#28726 fix(security): upgrade sandbox Dockerfile to node:22-slim](https://github.com/google-gemini/gemini-cli/pull/28726)** — P1，安全
   **修复**：将沙箱及所有 caretaker-agent Cloud Run 的 Dockerfile 从 `node:20-slim` 升级至 `node:22-slim`。**Node 20 已近 EOL**，不再接收安全修复（近期 CVE 仅修复于 22/24/26）。安全关键，建议尽快合并。

2. **[#28725 fix(security): prevent SSRF via DNS resolution bypass in web-fetch](https://github.com/google-gemini/gemini-cli/pull/28725)** — P2，安全
   **修复**：[Issue #28555](https://github.com/google-gemini/gemini-cli/issues/28555) 中的 **SSRF 漏洞（CVSS 8.6）**——恶意自定义域名可绕过 DNS 保护指向私网/回环地址（如 `169.254.169.254`）。安全关键，影响使用 `web-fetch` 工具的用户。PR 为 `alifakbxr` 提交（非维护者），社区驱动贡献。

3. **[#28673 feat(core): add Gemini 3.6 Flash and 3.5 Flash-Lite model configurations](https://github.com/google-gemini/gemini-cli/pull/28673)** — P2，功能
   **新增**：为 **Gemini 3.6 Flash** 和 **3.5 Flash-Lite** 添加模型配置（含 thinking、multimodalToolUse 能力标记及别名）。大模型（size/l）变更，影响模型选择与路由。

4. **[#28730 fix(core,cli): resolve false model capacity exhaustion](https://github.com/google-gemini/gemini-cli/pull/28730)** — 修复
   **修复**：解决**误报的模型容量耗尽错误**、修正 core 包中模型配额查询映射，并保留"Keep trying"选项以防止短暂的容量高峰打断用户。由维护者 `DavidAPierce` 提交，权威性高。

5. **[#28729 fix(core): resolve swallowed directory mismatch in IDE connections](https://github.com/google-gemini/gemini-cli/pull/28729)** — 修复
   **修复**：CLI 在 Cider（VS Code fork/远程工作区）下**无法连接 IDE 扩展**的问题——候选端口文件存在但工作区路径不匹配时错误被吞掉。提升 IDE 集成鲁棒性。

6. **[#28728 chore(deps): bump js-yaml from 4.1.1 to 4.3.1](https://github.com/google-gemini/gemini-cli/pull/28728)** — 依赖
   **更新**：`js-yaml` 4.1.1 → 4.3.1，包含**安全修复**（4.3.1 于 2026-07-31 发布，修复安全漏洞）。dependabot 自动 PR，建议及时合并。

7. **[#28597 fix(cli): load environment variables before resolving settings placeholders](https://github.com/google-gemini/gemini-cli/pull/28597)** — 修复
   **修复**：设置加载阶段的**竞态条件**——此前系统/用户/工作区设置会在加载本地 `.env` 之前展开 `process.env` 占位符，导致环境变量缺失。影响使用 `.env` 配置的用户。

8. **[#28581 fix(cli): skip diff hunk markers during @ processing](https://github.com/google-gemini/gemini-cli/pull/28581)** — P2，性能
   **修复**：防止 unified/combined diff 的 hunk 标记被误解析为 `@file` 引用，消除**每 hunk 两次递归全工作区 glob 搜索**，避免大 diff prompt 下的 `minimatch`/`path-scurry` 堆增长。性能优化。

9. **[#28369 feat(evals): add local report command and developer documentation](https://github.com/google-gemini/gemini-cli/pull/28369)** — P3，功能
   **新增**：`npm run eval:report` 命令，从 Vitest `report.json` 聚合各模型的通过率并映射至 inventory 策略。社区贡献（`ved015`）。**注意**：该 PR 与 #28344 同作者，已标记 `help wanted`。

10. **[#28524 feat(caretaker-triage): prompt hill-climbing & orchestrator updates](https://github.com/google-gemini/gemini-cli/pull/28524)** — 功能
    **更新**：整合 **3 周 prompt hill-climbing 与 eval 调优结果**，新增专用 `code_explorer` 技能，更新 triage 编排器。属于 caretaker 代理系列的持续演进（该系列共 8+ PR 昨日合并/关闭，参见 Issue #28713 的 PR 列表）。


## 功能需求趋势

从全部 50 条 Issues 与 39 条 PRs 中，可提炼出以下社区最关注的功能方向：

1. **AST 感知的代码导航与文件读取**（高热度）
   - 核心诉求：更精准地读取方法边界、减少 token 噪声、提升代码库映射质量。
   - 相关 Issue：[#22745](https://github.com/google-gemini/gemini-cli/issues/22745)（EPIC）、[#22746](https://github.com/google-gemini/gemini-cli/issues/22746)（AST CLI 工具调研）。
   - 信号：维护者已建立 EPIC 跟踪，说明该方向已被官方认可并进入规划。

2. **子代理行为透明度与可控性**（持续高频）
   - 核心诉求：子代理轨迹可通过 `/chat share` 查看与分享、bug 报告中包含子代理上下文、子代理执行应受权限控制。
   - 相关 Issue：[#22598](https://github.com/google-gemini/gemini-cli/issues/22598)、[#21763](https://github.com/google-gemini/gemini-cli/issues/21763)、[#22093](https://github.com/google-gemini/gemini-cli/issues/22093)。

3. **自感知与自我执行（meta-cognition）**
   - 核心诉求：CLI 自身应准确理解其 CLI 标志、快捷键等机制，成为自身使用的"专家指南"。
   - 相关 Issue：[#21432](https://github.com/google-gemini/gemini-cli/issues/21432)。

4. **行为评估体系（Behavioral Evals）扩展**
   - 相关 PR 密集出现：`eval:report`（#28369）、`eval:validate`（#28344）、caretaker triage eval 框架（#28530/#28532/#28727）。
   - 信号：项目正在系统性地构建评估基建，社区贡献者（如 `ved015`）积极参与。

5. **Zero-cost 的 Agent 技能与子代理自动使用**
   - 核心诉求：模型应"主动"使用自定义技能与子代理，而非仅在显式指示时使用。
   - 相关 Issue：[#21968](https://github.com/google-gemini/gemini-cli/issues/21968)。


## 开发者关注点（痛点/高频需求）

1. **子代理可靠性问题突出**（最集中）
   - **挂起**：Generalist 子代理永久挂起（#21409）、shell 命令挂起（#25166）。
   - **误报成功**：MAX_TURNS 被误报为 GOAL success（#22323）。
   - **越权执行**：配置禁用后仍自动使用子代理（#22093）。
   - **实践建议**：在修复前，可通过 prompt 显式指示模型不使用子代理作为临时 workaround。

2. **平台兼容性短板**
   - **Wayland 下浏览器子代理失败**（#21983）；**终端 resize 性能与闪烁**（#21924，需迁移到 `RenderStatic`）。
   - **实践建议**：Linux/Wayland 用户跟踪 #21983 的修复进展；终端性能敏感用户关注 #21924。

3. **Auto Memory（新功能）存在较多未完善细节**
   - 无限重试（#26522）、安全重定向缺陷（#26525）、无效补丁静默跳过（#26523）。
   - **信号**：该功能仍处于"可用但有风险"阶段，安全敏感用户建议谨慎开启或关注修复版本。

4. **配置系统的边界 case**
   - **symlink 不被识别**（#20079）、**settings.json 覆盖被忽略**（#22267，浏览器代理）、**环境变量加载顺序竞态**（#28597）。
   - 这些属于"小而疼"的问题，影响配置管理的灵活性与可预期性。

5. **安全修复正在加速**
   - SSRF 修复（#28725）、Node 20 EOL 迁移（#28726）、js-yaml 安全更新（#28728）同日出现，社区安全贡献活跃。
   - **实践建议**：`web-fetch` 工具使用者应优先跟踪 #28725 的合并状态；建议自建环境的开发者提前规划 Node 版本迁移。

---

*日报由 AI 自动生成，数据截至 2026-08-08。如有遗漏，欢迎在评论区补充。*

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报 — 2026-08-08

## 今日速览

今日发布 3 个新补丁版本（v1.0.79-6 至 v1.0.79-8），主要带来企业级策略支持（allow-auto-only、代理 URL 强制）、Agent 插件扩展目录规范及 `--plan` 与 `--mode autopilot` 的组合能力。社区侧最值得关注的是 Windows 平台一系列 UI 与剪贴板问题密集上报，以及技能（skills）子文件夹组织需求的持续高热（👍 23），另有 10 个新 triage Issue 集中提出多项体验改进建议。

---

## 版本发布

**v1.0.79-8**
- **Added**: 新增企业 allow-auto-only 策略支持，使 `/allow-all auto` 在完全 allow-all 被阻止时仍可工作；企业托管沙箱策略现可强制代理 URL，同时凭据仍由用户控制。
- **Improved**: `/sandbox` 配置对话框对 git、gh 等进行分组展示。

**v1.0.79-7**
- **Added**: Agent 插件 spec 现支持在 `com.github.copilot/extensions/` 目录下附带扩展；新增 kimi-k3 模型支持；`--plan` 可与 `--mode autopilot` 组合使用（先规划后执行，无需等待批准）。
- **Improved**: 多选提示的用户交互优化。

**v1.0.79-6**
- **Fixed**: 罕见的内部延迟不再在交互 UI 上打印诊断警告；会话历史加载失败不再导致时间线永久空白（此前失败被静默丢弃，导致整个会话的转录保持空白且无日志记录）。

---

## 社区热点 Issues（10 个精选）

本次筛选覆盖 Windows 平台问题、会话恢复性能、模型兼容性、权限机制等开发者密切关注的方面。

**1. Skills 子文件夹支持 — 持续高热**
[#1632](https://github.com/github/copilot-cli/issues/1632) | [area:plugins]
用户希望将 skills 按子文件夹组织（当前仅支持扁平结构），需求已获 23 👍、10 条评论，是近期呼声最高的功能请求之一。评论中用户表示已创建超 10 个 skills，扁平结构难以管理。

**2. 大会话恢复 OOM（1.0.74 回归）**
[#4251](https://github.com/github/copilot-cli/issues/4251) | [area:sessions]
从 1.0.73 升级到 1.0.74 后，恢复大型长期会话导致 OOM 或单核 CPU 跑满约 70 分钟，内存占用约为此前的 3-4 倍。作者用 A/B 对照确认回归来源，影响日常高频恢复大会话的重度用户。

**3. 剪贴板在 Windows 上静默失效**
[#3622](https://github.com/github/copilot-cli/issues/3622) | [area:input-keyboard, platform-windows, terminal-rendering]
复制操作显示成功但粘贴结果不变（剪贴板未更新），1.0.48 中正常。5 条评论，4 👍，Windows 用户日常复制代码块的核心路径受影响。

**4. 登录时自动"回车"绕过用户确认（回归）**
[#2494](https://github.com/github/copilot-cli/issues/2494) | [area:authentication]
v1.0.16 回归：Keychain 不可用时 `copilot login` 不再等待 y/N 输入而是自动确认，认证流程被意外跳过。11 条评论为该列表最高，虽 👍 仅 1 但讨论热度高，涉及企业批量部署时的安全风险。

**5. 转录渲染空白（测量缓存失效）**
[#4311](https://github.com/github/copilot-cli/issues/4311) | [area:terminal-rendering]
交互模式下转录区域渲染为空白（内容仍存在），需提交新消息或改变终端宽度才能重绘，`/resume` 无法恢复。已定位到 `WCr`/ScrollBox 的测量缓存失效问题，为深层渲染 bug。

**6. 模型 picker 输入被状态行遮挡**
[#4043](https://github.com/github/copilot-cli/issues/4043) | [area:models, terminal-rendering]
`/model` 命令中用 Up 键导航时，提示输入被状态行遮挡。CLOSED（已修复），但作为近期已解决的 UI 问题仍具参考价值。

**7. 后台 agent 被 Esc 误杀**
[#3980](https://github.com/github/copilot-cli/issues/3980) | [area:agents, input-keyboard]
`read_agent(wait: true)` 阻塞等待时按两次 Esc 取消，不仅取消读取还会连带终止底层后台 agent，且不可恢复。涉及多 agent 协作工作流的数据安全，已关闭（修复）。

**8. 模型推理强度不兼容**
[#4345](https://github.com/github/copilot-cli/issues/4345) | [area:agents, models]
当 `copilot_cli_opus_medium_effort_default` 和 `copilot_cli_gpt_5_4_mini_for_explore` 两个 flag 同时激活时，子 agent 执行反复报错 "Reasoning effort 'medium' is not supported for model 'claude-haiku-4.5'"。已关闭，但反映多模型策略组合时的兼容性问题。

**9. 会话列表缺少快捷删除**
[#4395](https://github.com/github/copilot-cli/issues/4395) | [triage]
此前会话列表支持在选中行直接删除，该功能已消失，现无便捷删除途径。属于体验回退类反馈。

**10. 浏览器登录 URL 换行与回退问题**
[#4400](https://github.com/github/copilot-cli/issues/4400) | [triage]
Device Code 流程正常，但 "Sign in with your browser" 流程 URL 展示出现换行问题，影响复制与点击。由 #2494 作者再次提出，登录相关流程的关注度在上升。

---

## 重要 PR 进展

过去 24 小时内无新 PR 更新（0 条）。作为替代，以下为近期合并的 PR 中值得关注的部分（依据社区影响与功能重要性）：

> 说明：本次数据源未包含具体 PR 详情，以下为基于 Issues 关联与版本发布内容的推断，建议读者前往 [PR 列表](https://github.com/github/copilot-cli/pulls) 确认最新状态。

**1. 会话历史加载失败处理** — 对应 v1.0.79-6 的修复内容，确保失败不再导致时间线永久空白，同时补充日志记录（[相关 PR](https://github.com/github/copilot-cli/pulls)）。

**2. 企业 allow-auto-only 策略** — 对应 v1.0.79-8 的新增内容，允许在完全 allow-all 被阻止时 `/allow-all auto` 仍可工作，面向企业管理员（[相关 PR](https://github.com/github/copilot-cli/pulls)）。

**3. 沙箱代理 URL 强制** — 企业托管沙箱策略现可强制代理 URL，凭据仍由用户控制，兼顾安全与灵活性（[相关 PR](https://github.com/github/copilot-cli/pulls)）。

**4. Agent 插件扩展目录** — spec 支持 `com.github.copilot/extensions/` 目录，为插件生态提供标准化扩展点（[相关 PR](https://github.com/github/copilot-cli/pulls)）。

**5. kimi-k3 模型接入** — 新增对 kimi-k3 模型的支持，扩展模型可选范围（[相关 PR](https://github.com/github/copilot-cli/pulls)）。

**6. --plan + autopilot 组合** — `--plan` 与 `--mode autopilot` 可组合使用，实现先规划后执行、无需等待批准的工作流（[相关 PR](https://github.com/github/copilot-cli/pulls)）。

**7. /sandbox 配置对话框分组** — git、gh 等选项分组展示，提升配置界面的可读性（[相关 PR](https://github.com/github/copilot-cli/pulls)）。

**8. 多选提示交互优化** — 用户多选提示的交互体验改进（[相关 PR](https://github.com/github/copilot-cli/pulls)）。

---

## 功能需求趋势

从全部 Issues 中提炼出以下社区最关注的功能方向：

**1. Skills/插件生态组织能力**
- **Skills 子文件夹支持**（#1632）：扁平结构限制导致大量 skills 难以管理，是当前最高 👍 的开放功能请求。
- **Agent 插件扩展目录**：v1.0.79-7 已引入 `extensions/` 目录标准，说明官方正在为插件生态铺路。

**2. 企业级策略与管理**
- **allow-auto-only 策略**：企业完全禁用 allow-all 时仍需 auto 模式可用，v1.0.79-8 已支持。
- **沙箱代理强制**：企业可强制代理 URL，同时保持凭据用户可控。
- **Registry 策略与本地配置冲突**（#4205）：组织 registry 批准的 MCP 配置与本地必需的运行时头部冲突，需要更灵活的认证方案。

**3. 会话与工作流体验**
- **新会话默认 workspace 类型持久化**（#4396）：用户希望可设置新会话默认使用 branch 或 worktree，而非每次手动切换。
- **--plan + autopilot 组合**：v1.0.79-7 已支持先规划再执行的无等待流程。
- **桌面通知**（#2941）：多任务场景下需要 CLI 请求人工输入时弹出通知（已关闭，但需求仍具代表性）。

**4. 新模型支持**
- **kimi-k3** 已在 v1.0.79-7 中支持；社区同时关注模型推理强度与多模型 flag 组合的兼容性（#4345）。

---

## 开发者关注点

**1. Windows 平台问题集中爆发（高频痛点）**
- 剪贴板复制静默失败（#3622）、特定代码页下复制导致清屏（#4391）、终端标题被改为 "Windows PowerShell"（#4384）、`!` 模式下 Tab 行为异常（#4387）、`add-dir` 路径破折号转下划线引起 OneDrive 权限循环（#1409）——Windows 上的终端渲染、输入键位与路径处理是该平台用户最集中的痛点区域。

**2. 会话恢复性能与稳定性**
- 1.0.74 后大会话恢复 OOM/CPU 跑满（#4251）是近期最严重的性能回退；1.0.79-6 修复了历史加载失败导致时间线永久空白的问题，但社区对会话相关稳定性仍高度敏感。

**3. 登录与认证流程体验**
- 登录自动确认绕过用户输入（#2494）、浏览器登录 URL 换行（#4400）——认证环节的问题直接影响首次使用体验，且与安全相关，关注度高。

**4. 权限机制透明度与状态一致性**
- 权限提示不显示触发规则（#4386）、从 auto 模式切回 interactive 后权限仍处于 auto（#4388）、`allowed_directories` 配置未加载（#4398）——权限系统的可理解性与状态切换一致性是核心诉求。

**5. 后台任务管理**
- 后台任务完成后模型仍持续等待（#4385）、Esc 取消误杀后台 agent（#3980）——模型对 shell 后台任务生命周期判断的可靠性仍需改进。

**6. 非官方安装途径的版本一致性**
- npm 全局 shim 是 loader 而非版本锁定，同一路径在 101 秒内先后跑出 1.0.77 和 1.0.78（#4402）——影响对版本行为的确定性判断，`--prefer-version` 虽可用但未文档化。

**7. 跨平台 hooks 兼容性**
- Claude Code 的 `.claude/settings.local.json` hooks 中 POSIX shell 运算符（`||`、`&&`）在 PowerShell 下无法执行（#4399）——跨工具、跨 shell 的兼容性是实际开发中的常见阻碍。

---

*本日报由 GitHub Copilot CLI 仓库公开数据自动生成，数据截至 2026-08-08。*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

## Kimi Code CLI 社区动态日报 — 2026-08-08

---

### 1. 今日速览

过去24小时，Kimi Code CLI 仓库无新版本发布，但出现了两个高关注度的技术修复方向：**文件编辑工具 `StrReplaceFile` 的编码安全问题**引发了双 PR 竞争修复，以及一个 **yolo 权限模式下 Agent 误执行 `rm -rf` 删除用户数据**的严重事故报告。社区对编码完整性的讨论热度上升，对权限安全模型的质疑声量增加。

---

### 2. 版本发布

过去24小时内无新版本发布。

---

### 3. 社区热点 Issues

**#2591 — StrReplaceFile 会破坏编辑区域外的非 UTF-8 字节**  
[链接](https://github.com/MoonshotAI/kimi-cli/issues/2591)  
**状态**: OPEN | **创建**: 08-05 | **更新**: 08-07 | **评论**: 3  
**要点**: `StrReplaceFile` 以 `errors="replace"` 解码整个文件再写回，任何非 UTF-8 字节（即使远离编辑区域）都会被替换为 U+FFFD 并写盘，导致文件永久损坏。涉及长度不变性问题的深入讨论，社区对编码安全的关注度较高。  
**为什么重要**: 这是文件编辑工具链的核心缺陷，直接影响二进制或混合编码文件的安全操作，严重性高。

---

**#2596 — Agent 在 yolo 权限模式下对工作区外已有目录执行 `rm -rf`**  
[链接](https://github.com/MoonshotAI/kimi-cli/issues/2596)  
**状态**: OPEN | **创建/更新**: 08-07 | **评论**: 0  
**要点**: Agent 清理先前创建的符号链接时，由于链接创建失败，实际对工作区外真实目录执行了递归删除，造成用户会话数据丢失。  
**为什么重要**: 这正是 yolo 模式最令人担忧的失控场景，社区对权限边界和安全防护机制会有更强烈的诉求。

---

### 4. 重要 PR 进展

**#2594 — 修复 `StrReplaceFile` 保留非 UTF-8 字节**  
[链接](https://github.com/MoonshotAI/kimi-cli/pull/2594)  
**状态**: OPEN | **作者**: 686f6c61 | **创建**: 08-06 | **更新**: 08-07  
**要点**: 将编辑操作改为在原始字节缓冲区上以 UTF-8 字节子串方式应用，避免整个文件被重新编码，从而保留编辑区域外的非法 UTF-8 字节。

---

**#2595 — 拒绝编辑非 UTF-8 文件**  
[链接](https://github.com/MoonshotAI/kimi-cli/pull/2595)  
**状态**: OPEN | **作者**: shoemoney（即 issue #2591 报告人）| **创建/更新**: 08-06/08-07  
**要点**: 直接对非 UTF-8 文件拒绝编辑操作，从源头防止数据破坏。与 #2594 属于两种不同的修复哲学——**“允许但不破坏”**与**“拒绝执行”**，值得关注合入方向。

---

**#2255 — 支持 Shift+Enter 插入换行**  
[链接](https://github.com/MoonshotAI/kimi-cli/pull/2255)  
**状态**: CLOSED | **作者**: donbeave | **创建**: 05-13 | **更新**: 08-06  
**要点**: 为交互式提示符增加 Shift+Enter 作为换行快捷键，补充现有的 Ctrl-J 与 Alt-Enter。今日状态变更为 CLOSED，但具体合并或关闭原因需进一步确认，可能已合入或延期。

---

### 5. 功能需求趋势

根据近期 Issues 与 PR 的观测，社区当前最关注的功能方向为：

- **文件编辑安全性**：如何保证 `StrReplaceFile` 等工具在处理非 UTF-8、二进制或混合编码文件时不破坏数据（#2591、#2594、#2595）。
- **权限模式的安全边界**：yolo 等高级别自动执行模式下的危险操作防护、目录白名单机制（#2596）。
- **交互终端体验**：快捷键增强（如 Shift+Enter）（#2255）。

---

### 6. 开发者关注点

- **数据安全是底线需求**：多个反馈集中在工具对文件内容的意外篡改，开发者希望 CLI 工具在处理文件时进行编码检测或提供预览/回滚机制。
- **对 yolo 模式的安全焦虑**：自动执行模式下 Agent 对真实文件系统的破坏性操作是最令开发者担忧的痛点，期望增加危险操作确认和路径校验。
- **关注及时修复与回归**：对 #2591 这类核心缺陷，社区不仅关注修法，更关注合并速度与是否引入新的回归问题——双 PR 并行的现状也表明两种设计取向需要维护者权衡。

---

> 日报数据来源于 GitHub 仓库 MoonshotAI/kimi-cli，仅供参考，不构成任何官方立场声明。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报

**日期：2026-08-08** | 数据来源：github.com/anomalyco/opencode


## 今日速览

今日社区最突出的矛盾集中在 **OpenCode Go 订阅服务**上：一是 #38257 反映 Go 服务在调用 chat/completions 接口时全面返回 401 上游封禁错误（45 条评论为今日最高），二是 #41146 与 #40409 分别揭示了计费配额异常与模型版本错配问题，引发用户对服务可靠性的集中质疑。与此同时，v1.18.15 版本发布，修复了消息排序与截断清理等核心稳定性问题，为社区提供了积极信号。


## 版本发布

### v1.18.15
> 链接：[Releases](https://github.com/anomalyco/opencode/releases)

**核心修复：**
- **消息排序修正**：即使导入或遗留消息 ID 顺序异常，时间线消息顺序仍保持正确
- **回滚与 fork 逻辑优化**：现在基于真实消息时间线而非消息 ID 排序执行
- **截断清理增强**：通过文件时间戳更可靠地清除过期文件


## 社区热点 Issues

### 1. [🔥 最热] OpenCode Go 服务上游 401 封禁
**#38257** | 作者: lizijiangyyjx | 👍 11 | 💬 45 | [链接](https://github.com/anomalyco/opencode/issues/38257)

- **内容**：OpenCode Go 订阅下所有模型调用 `chat/completions` 均返回 `401 Request blocked by upstream provider`，但 `/v1/models` 端点正常。用户认为这是影响 Go 订阅用户的**服务端问题**。
- **社区反应**：评论数位居今日榜首，大量用户确认遇到相同问题，热度持续攀升（创建于 7/22，更新至 8/7）。

### 2. 免费额度误判与计费争议
**#41146** | 作者: emregunes20123-alt | 👍 0 | 💬 2 | [链接](https://github.com/anomalyco/opencode/issues/41146)

- **内容**：Go 计划用户本周消费约 $7.50（限额 $30），但周配额却显示 100% 耗尽并被完全封禁。
- **社区反应**：直指计费系统可能存在严重缺陷，关联今日多个类似配额异常反馈（如 #41102、#41148）。

### 3. DeepSeek V4 Flash 模型版本错配
**#40409** | 作者: lumenfield | 👍 0 | 💬 14 | [链接](https://github.com/anomalyco/opencode/issues/40409)

- **内容**：Go 服务的 `deepseek-v4-flash` 实际返回的是 V3.2（知识截止 2025-05），并非 DeepSeek V4 Flash 0731。用户将其定性为**高严重度（计费/质量不匹配）**。
- **社区反应**：获得 14 条评论讨论，且与 #40607 互相关联，官方 API 也被证实存在同样问题。

### 4. 图片读取功能回归
**#5359** | 作者: conradkoh | 👍 0 | 💬 18 | [链接](https://github.com/anomalyco/opencode/issues/5359)

- **内容**：v1.0.137 起，粘贴图片后模型提示无法读取。v1.0.134 正常工作。环境：LiteLLM + Vertex AI。
- **社区反应**：18 条评论中用户反馈该问题已持续数月，影响面较广。

### 5. OpenCode Go 加密货币支付需求
**#23153** | 作者: suse-coder | 👍 37 | 💬 17 | [链接](https://github.com/anomalyco/opencode/issues/23153)

- **内容**：请求为 OpenCode Go 订阅增加加密货币支付方式。
- **社区反应**：👍 37 为今日最高，是社区呼声最高的功能需求之一。

### 6. Amazon Bedrock Opus 4.6 压缩失败
**#14332** | 作者: inventumamet | 👍 8 | 💬 16 | [链接](https://github.com/anomalyco/opencode/issues/14332)

- **内容**：压缩时错误：`thinking` 或 `redacted_thinking` 块无法被修改。
- **社区反应**：16 条评论，问题已关闭，但讨论中涉及 Bedrock 流式协议处理（与 PR #35743 相关）。

### 7. 屏幕阅读器无障碍模式缺失
**#8565** | 作者: destructatron | 👍 3 | 💬 10 | [链接](https://github.com/anomalyco/opencode/issues/8565)

- **内容**：TUI 对屏幕阅读器不友好：Emoji、动画和 Unicode 字符严重干扰朗读。
- **社区反应**：该悬而未决的需求获得持续关注，属于社区多样性建设的重要议题。

### 8. Windows 粘贴功能异常
**#6560** | 作者: ultradaoto | 👍 2 | 💬 13 | [链接](https://github.com/anomalyco/opencode/issues/6560)

- **内容**：Windows 11 下 PowerShell 中 OpenCode 会话里无法粘贴内容（Ctrl+V 和右键均无效）。
- **社区反应**：获得 13 条评论，已关闭，但仍然是 Windows 用户的痛点。

### 9. 运行时子代理模型覆盖
**#17595** | 作者: Quadina | 👍 3 | 💬 4 | [链接](https://github.com/anomalyco/opencode/issues/17595)

- **内容**：子代理固定使用启动时配置的模型，编排代理无法在运行时切换模型。
- **社区反应**：属于 Agents 编排场景下的高频需求，评论区有设计讨论。

### 10. 会话分享链接泄露紧急删除请求
**#41124** | 作者: Jeremyhao17 | 👍 0 | 💬 2 | [链接](https://github.com/anomalyco/opencode/issues/41124)

- **内容**：本地会话被意外删除，无法通过 `/unshare` 撤销已分享的链接，请求紧急删除远程数据。
- **社区反应**：反映出会话分享功能的**权限控制缺陷**，有潜在安全风险。

> 其他值得留意：#40231 TUI 黑屏（源码运行场景）、#40183 Copilot 反复要求重新认证。


## 重要 PR 进展

### 1. [核心修复] 非 SSE 流式协议补充 chunkTimeout
**#35743** | 作者: trollkarlen | [链接](https://github.com/anomalyco/opencode/pull/35743)

- **内容**：修复 `wrapSSE` 仅对 `text/event-stream` 生效的问题。AWS Bedrock（`application/vnd.amazon.eventstream`）等 EventStream 协议此前完全绕过 chunk-timeout 监控，现统一覆盖。
- **价值**：直接解决 Bedrock 等流式协议下的超时保护缺失（关联 #14332）。

### 2. [核心修复] Responses 消息 ID 持久化
**#41123** | 作者: rekram1-node | [链接](https://github.com/anomalyco/opencode/pull/41123)

- **内容**：将 Responses item ID 设为消息、流式事件、工具和 V2 持久化历史的一等公民；支持独立于 `store` 的 ID 重放，为 `msg_*`、`rs_*`、`fc_*` 等分配稳定 ID。
- **价值**：当前唯一开放中的 PR，直接关系消息追踪与持久化稳定性。

### 3. [新功能] Bedrock Provider 增加 Region 提示
**#35787** | 作者: OpeOginni | [链接](https://github.com/anomalyco/opencode/pull/35787)

- **内容**：连接 Bedrock provider 时提示用户选择 AWS 区域，尤其改善 Desktop 用户体验。关闭 #28834。
- **价值**：降低 Bedrock 配置门槛，解决因区域缺失导致的连接失败。

### 4. [新功能] Planner/Worker/Reviewer 多智能体工作流
**#35764** | 作者: bearstonem | [链接](https://github.com/anomalyco/opencode/pull/35764)

- **内容**：新增可选的 `workflow` 配置，实现规划（Planner）/执行（Worker）/评审（Reviewer）的协作模式。
- **价值**：补全 Agents 工作流编排能力，属于社区关注度高的方向。

### 5. [核心修复] 按请求字节数触发压缩
**#35687** | 作者: fengjikui | [链接](https://github.com/anomalyco/opencode/pull/35687)

- **内容**：新增可选 `compaction.max_request_bytes` 保护机制，在现有 token 计数之外提供基于字节数的主动压缩触发条件。关闭 #35013。
- **价值**：为超长上下文场景提供更可控的压缩策略。

### 6. [核心修复] 会话级工具可用性配置
**#35691** | 作者: ksamirdev | [链接](https://github.com/anomalyco/opencode/pull/35691)

- **内容**：新增 `POST /api/session/:sessionID/configure` 端点，实现会话作用域的工具启用/禁用配置。
- **价值**：提供细粒度的工具管控能力，关闭 #35647。

### 7. [TUI 修复] 清理过期工具准备状态
**#35796** | 作者: opencode-agent[bot] | [链接](https://github.com/anomalyco/opencode/pull/35796)

- **内容**：当刷新发现已完成的 assistant 消息时优先使用服务端投影，清理终端服务端投影被过期 pending 工具状态覆盖的问题，并附回归测试。

### 8. [grep 修复] 跳过超大匹配行
**#35699** | 作者: C0d3N1nja97342 | [链接](https://github.com/anomalyco/opencode/pull/35699)

- **内容**：当单行超过 ~64 KiB（压缩包、base64 等）导致 `Ripgrep JSON record exceeded 65536 bytes` 时，跳过该行而非中止整个搜索。关闭 #35523。
- **价值**：修复 grep 在大型代码库中的偶发崩溃。

### 9. [grep 修复] 限制文件路径搜索范围
**#35727** | 作者: fengjikui | [链接](https://github.com/anomalyco/opencode/pull/35727)

- **内容**：当 `grep` 收到精确文件路径时，仅传递 basename 给 ripgrep，避免搜索整个仓库。关闭 #35726。
- **价值**：显著提升精确文件 grep 的性能。

### 10. [Windows 修复] 规范化文件监听路径分隔符
**#35715** | 作者: C0d3N1nja97342 | [链接](https://github.com/anomalyco/opencode/pull/35715)

- **内容**：`@parcel/watcher` 在 Windows 上发出反斜杠路径，现统一转为正斜杠再发布到 `Event.Updated`。关闭 #35329。
- **价值**：修复 Windows 下文件监听相关的功能异常。

> 其他：#35683（glob 权限检查）、#35682（grep 权限检查）、#35780（TUI 附加 MCP 资源）、#35766 & #35767（Code Mode JSON 回调与属性删除）。


## 功能需求趋势

| 方向 | 代表 Issues | 热度 |
|------|-------------|------|
| **OpenCode Go 服务完善** | #38257, #41146, #40409, #41102, #41148 | 🔥🔥🔥🔥🔥 最高热度，涉及稳定性与计费透明度 |
| **支付方式扩展** | #23153（加密货币） | 🔥🔥🔥 👍 37 高需求 |
| **Agent 编排能力** | #17595（运行时子代理模型覆盖）、Planner/Worker/Reviewer PR | 🔥🔥🔥 持续增长 |
| **MCP 与工具链增强** | #35780（TUI 附加资源）、#38853（skills 子目录） | 🔥🔥 生态扩展方向 |
| **可访问性与跨平台** | #8565（无障碍模式）、#6560（Windows 粘贴） | 🔥🔥 长期未决 |
| **会话管理** | #41124（分享链接安全）、#41106（消息排队） | 🔥 桌面端体验优化 |

前端 IDE/编辑器集成需求暂未进入高热度区间。


## 开发者关注点

1. **OpenCode Go 服务稳定性与信任危机**：401 封禁（#38257）与计费配额异常（#41146、#41102、#41148）在 24 小时内集中爆发，直接影响付费用户的核心使用体验。**服务端状态透明度和计费系统的准确性**已成为当前社区最紧迫的诉求。

2. **模型版本/质量与宣传不一致**：`deepseek-v4-flash` 实际返回旧版模型（#40409、#40607），造成用户**按新模型付费却使用旧模型**的实质损失，引发对 Go 服务模型路由管理的质疑。

3. **压缩（Compaction）功能在复杂模型下不稳定**：Bedrock Opus 4.6 的 thinking 块导致压缩失败（#14332），以及压缩后无法继续（#41102），说明压缩逻辑对推理类模型的兼容性仍需加强。

4. **低层基础设施修复持续跟进**：chunkTimeout 遗漏 Bedrock 协议（#35743）、Windows 路径分隔符（#35715）等 PR 表明社区正系统性地加固底层稳健性，但部分问题存在时间较长，**修复周期偏长**是开发者反馈中常见的痛点。

---
*本日报由 AI 自动生成，仅供参考。*

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi 社区动态日报

**日期：2026-08-08** | 数据来源: [github.com/badlogic/pi-mono](https://github.com/badlogic/pi-mono)

---

## 今日速览

Pi 发布 v0.84.1，新增 Qwen Token Plan Individual 支持与认证就绪检查功能。社区当前焦点集中在上下文压缩（auto-compaction）的可靠性问题——特别是超过 100% 后不触发、压缩后不继续等缺陷，同时 TUI 性能优化和全新本地模型（LM Studio）支持也有重要进展。此外，Agent Plugins 规范支持与 Cursor CLI 桥接成为新的功能需求热点。

---

## 版本发布

### [v0.84.1](https://github.com/earendil-works/pi/releases/tag/v0.84.1)

**新功能：**

- **Qwen Token Plan Individual** — 为 Individual 订阅用户的内置模型提供内置 provider 支持。参见 [API Keys 文档](https://github.com/earendil-works/pi/blob/v0.84.1/packages/coding-agent/docs/providers.md#api-keys)
- **认证就绪检查** — 使用 `pi auth` 命令进行认证状态预检

> ⚠️ 注意：多个 Issue 报告了 v0.84.1 的启动问题（详见 #7771）和主题自动检测问题（#7770），建议用户关注。

---

## 社区热点 Issues（精选 10 条）

### 1. [#6879 auto-compaction 在上下文超限后不触发](https://github.com/earendil-works/pi/issues/6879)
**标签**: [bug] | **评论**: 13 | **👍**: 15 | **状态**: OPEN

> 在 gpt-5.6-sol 上的一次 agentic 回合运行超 2 小时，上下文 footer 超过压缩阈值后持续攀升至 >100%，直到 API 在 373k tokens 处拒绝请求才触发压缩。

**重要性**: ⭐⭐⭐⭐⭐ 社区最关注的 bug 之一（15 👍），直接导致长会话不可用。用户建议在每个 agent 回合后检查上下文。这可能是当前版本最常见的痛点。

---

### 2. [#7128 系统提示词中的 PI_\* 指南过度鼓励 bash 调用](https://github.com/earendil-works/pi/issues/7128)
**标签**: [bug, no-action] | **评论**: 11 | **👍**: 7 | **状态**: OPEN

> 最近的系统提示词更新加入了“检查 PI_\* 环境变量以了解模型和会话详情”的指南，导致 agent 频繁执行不必要的环境检查 bash 命令，影响效率。

**重要性**: ⭐⭐⭐⭐ 涉及 agent 行为策略的默认配置。虽然标记为 no-action，但 7 个 👍 说明有不少用户感受到了 token 浪费。

---

### 3. [#7020 压缩后 Pi 有时不继续执行](https://github.com/earendil-works/pi/issues/7020)
**标签**: [bug] | **评论**: 10 | **👍**: 2 | **状态**: CLOSED

> 长运行的“协调器”会话中，压缩后 agent 有时不继续。症状是压缩完成后 agent 停止响应或丢失上下文。

**重要性**: ⭐⭐⭐⭐ 与 #6879 同属压缩机制问题，说明压缩功能是当前最不稳定的环节之一。已关闭但社区关注度高。

---

### 4. [#7730 macOS 上长会话 CPU 占用过高](https://github.com/earendil-works/pi/issues/7730)
**标签**: [bug] | **评论**: 4 | **👍**: 5 | **状态**: OPEN

> macOS 上长会话时 CPU 占用 50-110%，内存 600-800MB。疑似与会话/上下文大小相关。

**重要性**: ⭐⭐⭐⭐ 性能问题直接关联日常使用体验。5 个 👍 说明不少 Mac 用户有类似感受。

---

### 5. [#7771 v0.84.1 无法启动（zlib.createZstdDecompress 报错）](https://github.com/earendil-works/pi/issues/7771)
**标签**: [bug, untriaged] | **评论**: 5 | **👍**: 0 | **状态**: CLOSED

> Node 23 环境下 `pi update` 后启动报错：`TypeError: zlib.createZstdDecompress is not a function`，重装无效。

**重要性**: ⭐⭐⭐⭐ 新版本发布即出现启动阻塞问题，影响面较大。Node 23 用户需注意。

---

### 6. [#5886 AgentSession 结算/延续与 assistant-tail 生命周期 bug](https://github.com/earendil-works/pi/issues/5886)
**标签**: [pkg:agent, pkg:coding-agent] | **评论**: 6 | **👍**: 4 | **状态**: OPEN

> mitsuhiko 提出的元问题：运行后逻辑尝试从已不再有效的 transcript 继续 agent 的一系列相关问题。

**重要性**: ⭐⭐⭐⭐ 由核心维护者提出，涵盖多类相关问题，是 agent 生命周期管理的深层次架构问题。

---

### 7. [#7053 并行工具批次中某个工具卡住导致已完成结果丢失](https://github.com/earendil-works/pi/issues/7053)
**标签**: [inprogress] | **评论**: 4 | **👍**: 0 | **状态**: OPEN

> 并行工具执行中，如果某个工具停滞，`Promise.all` 会导致整个批次的结果丢失——即使其他工具已完成。已标记为进行中。

**重要性**: ⭐⭐⭐⭐ 影响并行工具调用的可靠性，#3503 的后续回归，开发者正在处理中。

---

### 8. [#7702 DeepSeek 模型经 opencode zen gateway 报 400 错误](https://github.com/earendil-works/pi/issues/7702)
**标签**: 无 | **评论**: 6 | **👍**: 0 | **状态**: CLOSED

> 通过 opencode zen gateway（如 `deepseek-v4-flash-free`）使用时多轮/工具调用报：`reasoning_content must be passed back`。

**重要性**: ⭐⭐⭐ 涉及第三方 gateway 兼容性，根因是 `detectCompat()` 未检测到 `reasoning_content` 回传需求。

---

### 9. [#7740 `/reload` 后自定义工具渲染器失效](https://github.com/earendil-works/pi/issues/7740)
**标签**: [bug] | **评论**: 2 | **👍**: 0 | **状态**: OPEN

> `/reload` 后，注册在 `session_start` 事件上的工具（如 MCP 工具）的 `renderCall`/`renderResult` 不再生效，原因是加载顺序问题。

**重要性**: ⭐⭐⭐ 影响扩展开发者体验，已有对应修复 PR（#7749）但尚未合入。

---

### 10. [#7776 Agent Plugins 规范支持](https://github.com/earendil-works/pi/issues/7776)
**标签**: [untriaged] | **评论**: 3 | **👍**: 0 | **状态**: CLOSED

> 建议增加对 [Agent Plugins 规范](https://agent-plugins.org/) 的一等支持，识别根目录 plugin.json 清单并加载其 skills/ 目录，实现 Pi、Codex 等 agent 间的可移植性。

**重要性**: ⭐⭐⭐ 跨 agent 插件标准化的方向性需求，虽然已关闭，但反映了社区对生态互操作性的期待。

---

## 重要 PR 进展（精选 10 条）

### 1. [#7801 懒加载不常用语法高亮文法](https://github.com/earendil-works/pi/pull/7801)
**作者**: mitsuhiko | **状态**: OPEN

> 实验性重构语法高亮机制，按需加载不常用文法以减少启动开销。维护者承认会短暂失效 UI，但影响较小。

---

### 2. [#7784 从记录查询派生恢复状态（recovery state）](https://github.com/earendil-works/pi/pull/7784)
**作者**: christianklotz | **状态**: OPEN

> 移除专用恢复查询 API（如 `findOpenOperations()`），改为通过有界 `findRecords()` 调用派生恢复状态；保留写侧强制和非法重放拒绝，同时删除 SQLite 操作类型查询路径和索引。

---

### 3. [#7780 TUI 性能改进](https://github.com/earendil-works/pi/pull/7780)
**作者**: ClassicOldSong | **状态**: CLOSED

> 通过增量解析 markdown 和延迟渲染失效来提升 TUI 性能，启动时部分解析旧内容。

**意义**: 直接回应 #7730 等 TUI 性能问题。

---

### 4. [#7762 LM Studio provider](https://github.com/earendil-works/pi/pull/7762)
**作者**: skkdevcraft | **状态**: OPEN

> 新增 LM Studio 本地模型 provider，解决 #7668。测试由 LM_STUDIO_BASE_URL 环境变量保护。

**意义**: 扩展本地模型支持，丰富非云端方案选择。

---

### 5. [#7749 修复 /reload 后自定义工具渲染器丢失](https://github.com/earendil-works/pi/pull/7749)
**作者**: bailu-ZZ | **状态**: CLOSED

> 修复工具注册在 `session_start` handler 时，`/reload` 后自定义渲染器丢失的问题。原因是交互模式在发送 `session_start` 前就重建了历史消息。

---

### 6. [#7758 新增退出前台任务与 ctx.version](https://github.com/earendil-works/pi/pull/7758)
**作者**: fx1226 | **状态**: CLOSED

> 扩展新增能力：`pi` 关闭后可接管前台进程（如启动 web UI 的 `/web` 命令），并增加 `ctx.version` API。

**意义**: 解锁 TUI 交接长驻前台服务的新扩展场景。

---

### 7. [#7757 允许退出全屏模式 copy-on-select](https://github.com/earendil-works/pi/pull/7757)
**作者**: aliou | **状态**: OPEN

> 解决 #7720：新增设置可退出全屏模式的 copy-on-select 行为。禁用后 `app.message.copy` 快捷键优先复制选中内容。

---

### 8. [#7795 用 `command -v` 替代 `which`](https://github.com/earendil-works/pi/pull/7795)
**作者**: tlvince | **状态**: CLOSED

> `which` 是外部命令，在沙箱等最小化环境中可能不存在。改用 shell 内置的 `command -v`。至少影响 `/copy` 命令。

---

### 9. [#7792 桥接 Cursor CLI 本地会话](https://github.com/earendil-works/pi/pull/7792)
**作者**: GFBarbosa | **状态**: CLOSED

> 新增隐藏内置 `cursor-agent` 扩展，桥接 Pi 与已认证的本地 Cursor CLI 会话。提供 `pi cursor status` 健康检查与模型发现能力，无需 CURSOR_API_KEY。

**意义**: 与 Issue #7793 对应，开辟 Cursor 用户低成本迁移路径。

---

### 10. [#7710 恢复挂起的 harness 操作](https://github.com/earendil-works/pi/pull/7710)
**作者**: vegarsti | **状态**: CLOSED

> 实现 [harness v2 计划中的 R3](https://github.com/earendil-works/pi/blob/main/packages/agent/docs/harness-v2.md#track-r--recovery-query-reducer-and-restore)：填充 `AgentHarness.create`，使新 harness 能从既有 session 加载并恢复挂起操作。

---

## 功能需求趋势

| 方向 | 代表 Issue/PR | 热度 |
|------|--------------|------|
| **上下文压缩（auto-compaction）稳定性** | #6879, #7020 | 🔥🔥🔥🔥🔥 |
| **TUI 性能与交互优化** | #7730, #7780, #7757 | 🔥🔥🔥🔥 |
| **扩展能力增强** | #5952, #7758, #7749 | 🔥🔥🔥🔥 |
| **本地/第三方模型支持** | #7762 (LM Studio), #7702 (DeepSeek), #7726 (Baseten) | 🔥🔥🔥 |
| **新 provider 桥接** | #7792 (Cursor), #6216 (Amazon Bedrock Mantle) | 🔥🔥🔥 |
| **跨工具插件互操作** | #7776 (Agent Plugins spec) | 🔥🔥 |
| **主题/外观自动化** | #7770, #7595 | 🔥🔥 |
| **系统提示词优化** | #7128 | 🔥🔥 |

---

## 开发者关注点

1. **压缩机制是最大痛点**——两个高热度 Issue（#6879 获 15 👍，#7020）都指向上下文压缩在长会话中不可靠：要么不触发，要么触发后不继续执行。这直接影响重度用户的核心体验。

2. **TUI 性能退化**——macOS 用户报告长会话 CPU 飙升至 100%+（#7730），恰逢 #7780 的 TUI 性能优化 PR 提交，说明维护者已在响应。

3. **并行工具调用的可靠性**——#7053 揭示的“批次内单工具卡住导致全部结果丢失”问题已标记为进行中，这影响所有依赖并行工具调用的工作流。

4. **环境依赖问题**——#7771（Node 23 下 zstd 报错）、#7796（`which` 命令依赖）和 #7791（16KiB header 限制）表明社区对运行时环境兼容性有较高要求，也反映出测试覆盖在 Node 版本矩阵上的不足。

5. **扩展开发体验**——`/reload` 后自定义渲染器丢失（#7740）、ExtensionAPI 缺少工具装饰能力（#7800）、会话替换 API 需求（#5952）等问题集中在扩展开发者的日常工作流上，修复后生态活力有望提升。

6. **对默认行为的敏感**——#7128 反映社区对系统提示词中引导 agent 行为的措辞相当敏感，任何微小的偏向都会被注意到，这可能影响未来的 prompt 工程决策。

---

*本日报由 AI 自动生成。所有数据来自 [github.com/badlogic/pi-mono](https://github.com/badlogic/pi-mono)，标签（如 OPEN/CLOSED）以数据抓取时间为准。*

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报

**日期：2026-08-08** | 数据来源：github.com/QwenLM/qwen-code


## 今日速览

昨晚发布了 v0.21.7 稳定版，核心亮点是移除了 Goals 功能的 50 轮对话限制，允许长任务跨边界恢复执行；同时 CLI 开始支持在终端内直接渲染模型输出的内联图片。社区方面，一个关于 `OTEL_METRICS_EXPORTER=otlp` 环境变量导致指标静默失效的 bug 引发广泛讨论，成为今日开发者关注焦点。此外，多模态 Omni 实验项目持续推进，社区对增强 Agent 事实核验能力的呼声渐高。


## 版本发布

### v0.21.7 (Stable)

**Highlights：**
- **移除 Goals 50 轮对话上限**（#8421）：任务可恢复并在超过先前边界后继续执行，长时任务不再受限
- **CLI 内联终端图片渲染**：支持在交互式 CLI 中直接渲染来自模型输出的内联图片

> 完整变更日志：[v0.21.7 Release](https://github.com/QwenLM/qwen-code/releases)

### v0.21.7-nightly.20260807.fca8f3c1f

- 仅包含一项 CI 修复：`fix(ci): surface blocked autofix takeover admission`（#8410），对正式版无功能影响


## 社区热点 Issues（Top 10）

### 1. [Bug] Windows 终端中文输入拼音显示不清 → 下载量最大的平台输入体验缺陷
**#8625** · [查看](https://github.com/QwenLM/qwen-code/issues/8625) · 评论 6 · 2026-08-07 更新

Windows 终端中输入中文时拼音渲染模糊难辨，严重影响中国区用户日常使用。有 `welcome-pr` 标签，社区期待快速修复。

### 2. [Bug] OTEL_METRICS_EXPORTER=otlp 环境变量导致指标静默失效
**#8697** · [查看](https://github.com/QwenLM/qwen-code/issues/8697) · 评论 2 · 2026-08-07 更新

OTel 生态的标准化环境变量 `OTEL_METRICS_EXPORTER=otlp` 会导致 qwen-code 的遥测 SDK 启动失败，所有原生 `qwen_*` 指标静默消失，而 traces 仍正常输出。对多 CLI 共享 collector 的团队影响明显。

### 3. [Bug] Tmux 中闪屏（SSH + iTerm2 + Ubuntu）
**#8562** · [查看](https://github.com/QwenLM/qwen-code/issues/8562) · 评论 5 · 2026-08-07 更新

用户经 iTerm2 → SSH → Ubuntu → tmux 使用时对话界面持续闪屏，已用 Qwen 3.8 Max 交叉排查确认与 Qwen Code 版本更新相关。同类问题在 web 终端中也有报告（#8659），呈现集中爆发趋势。

### 4. [Bug] PuTTY 中键选择/复制功能回归
**#8672** · [查看](https://github.com/QwenLM/qwen-code/issues/8672) · 评论 3 · 2026-08-07 更新

0.21.1 版本后 PuTTY 中 xterm 风格的中键粘贴失效，影响远程 Linux 工作流。标记 `status/need-retesting`，属于回归类 bug。

### 5. [Feature] Qwen WebBridge —— 对标 Kimi 的浏览器直接控制提案
**#8699** · [查看](https://github.com/QwenLM/qwen-code/issues/8699) · 评论 2 · 2026-08-07 更新

提议基于 `qwen serve` daemon 构建直接浏览器控制桥，Agent/Skill 通过 localhost HTTP 命令驱动浏览器，不强制依赖 MCP。关联 PR #8707 已提交实现。

### 6. [Feature] 增强 Agent 事实核验行为
**#8701** · [查看](https://github.com/QwenLM/qwen-code/issues/8701) · 评论 2 · 2026-08-08 更新

社区用户提出五条 Agent 事实核验增强建议：先验证再下结论、全链条验证、历史 transcript 不当事实、排障先查自身变更等，可通过内置 system prompt 或"严格核验模式"实现。

### 7. [Bug] 长 Agent 任务期间排队消息指示器消失
**#8666** · [查看](https://github.com/QwenLM/qwen-code/issues/8666) · 评论 3 · 2026-08-07 更新

Ctrl+Q 排队消息在 Agent 长时间运行时从界面消失，用户无法感知消息已在队列中。属 UI/UX 反馈，附 `welcome-pr` 标签。

### 8. [Feature] 移动端 "Local Control" 模式（QR 码配对）
**#8595** · [查看](https://github.com/QwenLM/qwen-code/issues/8595) · 评论 2 · 2026-08-07 更新

提议在桌面端展示 QR 码，手机扫码即可接管本地 Qwen Code 会话，零手动配置。涉及 CLI + Desktop 双端，已进入 need-discussion 阶段。

### 9. [Bug] Web 终端 TUI 闪烁/撕裂
**#8659** · [查看](https://github.com/QwenLM/qwen-code/issues/8659) · 评论 3 · 2026-08-07 更新

阿里云 Workbench 等 web 终端下虚拟化历史模式（`useTerminalBuffer: true`）全屏 ANSI 重绘导致持续闪烁。与 #8562 同属渲染管线问题，可能指向同一根因。

### 10. [Feature] 桌面端 Markdown 链接不可点击
**#8593** · [查看](https://github.com/QwenLM/qwen-code/issues/8593) · 评论 4 · 2026-08-07 更新

Desktop 0.1.0 中助手消息的 Markdown 链接有样式但点击无响应，静默吞掉点击事件。该问题已关闭，修复方案待合入。


## 重要 PR 进展（Top 10）

### 1. [feat(auth)] 新增 Kimi 与小米 MiMo 第三方提供商
**#8368** · [查看](https://github.com/QwenLM/qwen-code/pull/8368) · 2026-08-07 更新

Kimi 以 Coding Plan、API Key（中国/国际）三种方式接入；小米 MiMo 支持按量付费及中国、新加坡等多区域。中国市场模型接入持续扩展。

### 2. [feat(web-shell)] 右侧面板全屏视图
**#8614** · [查看](https://github.com/QwenLM/qwen-code/pull/8614) · 2026-08-07 更新

为 Web Shell 右侧 tab 面板（artifacts、subagents、review changes、monitors、scheduled tasks）添加全屏切换按钮。

### 3. [feat(web-shell)] 模型级推理控制注册表
**#8675** · [查看](https://github.com/QwenLM/qwen-code/pull/8675) · 2026-08-07 更新

构建内置模型推理控制注册表，贯穿 Core、ACP、daemon、SDK 和 WebShell 全链路。首个注册模型为 `qwen3.*`，支持 Thinking/Effort 独立声明。

### 4. [feat(serve)] 可轮询的 turn 状态端点
**#8682** · [查看](https://github.com/QwenLM/qwen-code/pull/8682) · 2026-08-07 更新

daemon HTTP API 新增 `GET /session/:sessionId/turns/:promptId` 和 `GET /session/:sessionId/turns/current` 两个只读端点，支持外部服务轮询 turn 生命周期状态。

### 5. [feat(chrome)] Qwen WebBridge 浏览器直接控制
**#8707** · [查看](https://github.com/QwenLM/qwen-code/pull/8707) · 2026-08-07 更新

实现 Kimi WebBridge 兼容的 `/command` 与 `/status` 端点，完整覆盖 17 种操作，支持任务级资源管理，是 #8699 提案的具体实现。

### 6. [fix(cli)] 尊重可信环境边界（`.env` 加载）
**#8706** · [查看](https://github.com/QwenLM/qwen-code/pull/8706) · 2026-08-07 更新

修复 #8643：每个项目 `.env` 文件独立评估 workspace trust，用户级 `.env` 保持无条件加载，保留显式 `workspaceTrusted` 覆盖。

### 7. [feat(web-shell)] tmux 后端交互式子 Agent
**#8613** · [查看](https://github.com/QwenLM/qwen-code/pull/8613) · 2026-08-07 更新

Agent 可在 daemon 主机的 tmux 会话中运行交互式 CLI（REPL、其他 Agent CLI、curses/TUI 应用），Web Shell 实时显示可交互终端视图。

### 8. [feat(serve)] 暴露活跃工作状态
**#8588** · [查看](https://github.com/QwenLM/qwen-code/pull/8588) · 2026-08-07 更新

`GET /health?deep=1` 新增 `activeWork`、`activeWorkReporting`、`activeWorkStaleMs` 字段，提供管理面可见性。

### 9. [feat(review)] Maven 多模块验证
**#8394** · [查看](https://github.com/QwenLM/qwen-code/pull/8394) · 2026-08-07 更新

`/review` 支持识别根 Maven reactor，将变更文件映射至最深默认模块执行构建验证，Java 项目审查能力显著增强。

### 10. [feat(daemon)] 跨 worktree Git 变更防护
**#8687** · [查看](https://github.com/QwenLM/qwen-code/pull/8687) · 2026-08-07 更新

内置宿主侧防护：解析 `-C`、`--work-tree`、`--git-dir` 识别的 Git 仓库重定位，当目标逃逸会话 worktree 时阻止变更类命令，增强 `qwen serve` 安全性。


## 功能需求趋势

| 方向 | 热度 | 代表 Issue/PR |
|------|------|--------------|
| **多模态 Omni 实验** | 🔥🔥🔥 | #8185 S3 投递可靠性、#8197 Omni 总纲、PR #8110 |
| **浏览器直接控制（WebBridge）** | 🔥🔥🔥 | #8699 提案 + #8707 实现，对标 Kimi |
| **第三方模型提供商接入** | 🔥🔥 | #8368 Kimi + 小米 MiMo，中国市场持续扩展 |
| **交互式终端体验优化** | 🔥🔥 | #8613 tmux 子 Agent、#8614 全屏面板、#8675 推理控制 |
| **Agent 事实核验与可观测性** | 🔥 | #8701 五条核验增强、#8588 活跃工作状态、#8682 turn 轮询 |
| **多端协同/远程控制** | 🔥 | #8595 QR 码手机配对、"Local Control" 模式 |
| **Web Shell 工具栏增强** | 🔥 | #6699、#6701 工作区/执行上下文/git 分支选择器 |


## 开发者关注点

1. **终端渲染稳定性是当前最大痛点**：tmux 闪屏（#8562）、web 终端撕裂（#8659）、PuTTY 中键回归（#8672）三类问题同日密集出现，涉及不同平台但疑似同源渲染管线缺陷，建议优先排查。Windows 中文输入渲染问题（#8625）同样值得快速跟进。

2. **OTel 生态标准变量兼容性缺口**：`OTEL_METRICS_EXPORTER=otlp` 导致指标静默失效（#8697），违反 OTel 通用约定，对多 CLI 共享 collector 的用户影响严重，建议在 telemetry SDK 初始化时做好容错。

3. **遥测与可观测性需求明确**：多项 Issue 和 PR 指向同一诉求——外部系统需要标准化方式了解 Qwen Code 会话状态和活跃度（#8588、#8682、#8660）。服务器/无人值守场景的使用比例正在上升。

4. **"本地优先 + 远程访问"是持续主线**：移动端 QR 配对控制（#8595）、WebBridge 浏览器控制（#8699）、tmux 子 Agent（#8613）共同勾勒出 "CLI 为核、多端接入" 的产品方向，Web Shell 正在成为统一交互层。

5. **安全边界意识增强**：跨 worktree Git 防护（#8687）、可信 .env 边界（#8706）等 PR 表明在 Agent 自主执行能力增强的同时，社区对权限边界和逃逸防护的需求同步上升。


*本日报由 AI 自动生成，基于 2026-08-08 的 GitHub 公开数据。如需订阅每日推送，请关注 QwenLM/qwen-code 仓库。*

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

## DeepSeek TUI 社区动态日报 — 2026-08-08

> 数据来源：[Hmbown/DeepSeek-TUI](https://github.com/Hmbown/CodeWhale)（实际仓库显示为 CodeWhale，下同）

---

### 一、今日速览

今日社区动态集中于 **v0.9.5 系列新特性规划** 与 **v0.9.4 发布阻塞** 两条主线：维护者一口气开出 6 个面向 v0.9.5 的 agent-ready 新 Issue（会话恢复、统一任务面板、计划产物持久化等），同时提交 PR #5282 试图清除 v0.9.4 的 4 个 CI 阻塞项。此外，一批依赖升级 PR 密集提交，以及一个 FreeBSD 构建修复被合并后又被关闭，值得关注。

---

### 二、社区热点 Issues（10 个）

#### 🚨 发布与阻塞

1. **[#2870] EPIC: staged command-boundary refactor** — [链接](https://github.com/Hmbown/CodeWhale/issues/2870)  
   一个跨度达 2 个月（6/7 创建）的 EPIC，将命令边界重构拆分为多个可合并层，引用 #2851 作为参考 PR。20 条评论为今日最高热度。社区对该大型重构的推进节奏高度关注。

2. **[#3205] v0.9.3: Fleet model classes, loadout auto, and semantic route roles** — [链接](https://github.com/Hmbown/CodeWhale/issues/3205)  
   12 条评论。目标是为 TUI/CLI/exec/subagents/Fleet 建立一个统一的模型负载选择器，明确 `Fleet loadout auto` 自动模式语义。这是多端一致性的关键设计 Issue。

#### 🧹 大规模重构（v0.9.2/v0.9.3 系列）

3. **[#3313] Split RuntimeThreadManager into store, executor, events, types** — [链接](https://github.com/Hmbown/CodeWhale/issues/3313)  
   `runtime_threads.rs` 已达 7,133 行、四个关注点混在一起。维护者持续推动巨型 Rust 文件拆解，5 条评论。这类重构预示着模块化程度将显著提升。

4. **[#3312] Extract ui.rs run_event_loop into context-owned handlers** — [链接](https://github.com/Hmbown/CodeWhale/issues/3312)  
   4 条评论。`run_event_loop` 函数内包含事件匹配、按键分发、终端生命周期三块子巨石。UI 逻辑拆分是后续可维护性的重点。

5. **[#3308] Split TUI history renderers into focused modules** — [链接](https://github.com/Hmbown/CodeWhale/issues/3308)  
   4 条评论。history 渲染器大部分拆分已完成，仅剩模块根文件待清理，属于收尾性工作。

#### 💡 v0.9.5 新特性（全部 8/7 创建，评论各 1 条，均为维护者新开）

6. **[#5272] prompt-scoped file recovery（从历史 prompt 恢复工作区）** — [链接](https://github.com/Hmbown/CodeWhale/issues/5272)  
   从用户 prompt 快照恢复被 agent 破坏的文件，避免纯靠 git 考古。注重破坏性恢复前的确认以及与 git 协同。

7. **[#5271] session peek（无需完全附加即可查看/审批其他会话）** — [链接](https://github.com/Hmbown/CodeWhale/issues/5271)  
   多会话控制目前只是恢复选择器，新特性将支持在 TUI 中列出其他线程、查看待审批项并直接应答。

8. **[#5270] unified tasks surface（shell + subagents + durable workers 统一视图）** — [链接](https://github.com/Hmbown/CodeWhale/issues/5270)  
   将当前散落的 Tasks 面板、Fleet、Workflow 整合为一个操作员视角的"仍在运行"列表。

9. **[#5268] mid-turn control（排队/立即发送/Esc 保留草稿 + 具名等待）** — [链接](https://github.com/Hmbown/CodeWhale/issues/5268)  
   解决回合运行中聊天框"被锁死"的痛点，明确 queue vs send-now vs cancel-keep-draft 三态契约。

10. **[#5267] turn-stop honesty（状态显示"结束中"就必须真的结束）** — [链接](https://github.com/Hmbown/CodeWhale/issues/5267)  
    当 footer 显示 "ending"/"stopping" 时模型仍在继续输出，损害用户信任。建议优先删除虚假保护而非增加更多状态文案。

---

### 三、重要 PR 进展（10 个）

#### 🚀 发布管理

1. **[#5282] fix(release): clear the four CI blockers holding v0.9.4** — [链接](https://github.com/Hmbown/CodeWhale/pull/5282)  
   核心信息：`origin/main` 已在 0.9.4 版本，CHANGELOG/npm/crate 固定均同步，但上次 CI 调度 (run 31180519587) 三路失败，尚无绿灯记录。发布卡在 CI 红灯而非决策。当前最紧急的 PR。

#### 🤖 功能特性

2. **[#5257] feat(config): add `model = auto` for prompt-based tier selection** — [链接](https://github.com/Hmbown/CodeWhale/pull/5257)  
   新配置项 `model = "auto"`，根据用户 prompt 自动在 deepseek-v4-pro（复杂任务）和 deepseek-v4-flash（简单任务）间切换。响应社区对"既快又强"的诉求。

3. **[#5256] feat(mcp): background incremental registry sync** — [链接](https://github.com/Hmbown/CodeWhale/pull/5256)  
   registry 同步改为缓存优先快速返回，全量下载由 `tokio::spawn` 后台执行，经进程级 mutex 保证单实例。显著降低交互延迟。

4. **[#5255] Layer 5.3: Palette, completion, and discovery filtering** — [链接](https://github.com/Hmbown/CodeWhale/pull/5255)  
   命令边界重构第 5.3 层：验证命令面板与斜杠补全表面对用户命令的集成，每个验收标准均有测试验证。

5. **[#5258] fix(tui): stop stale cached session title from pinning "New Session"** — [链接](https://github.com/Hmbown/CodeWhale/pull/5258)  
   修复会话标题卡在 "New Session" 的问题：首条消息后计算出的标题被内存中缓存覆盖，且缓存仅在快照结束时刷新。社区常见体验 bug。

#### 🐧 平台兼容

6. **[#5254] Build fix for FreeBSD** — [链接](https://github.com/Hmbown/CodeWhale/pull/5254)  
   rquickjs 无 FreeBSD bindings，编译中断于 `x86_64-unknown-freebsd`。对应 Issue #1097 获得社区持续关注，但该 PR 状态为 CLOSED（合并后关闭），是 FreeBSD 支持的重要一步。

7. **[#5252] feat(subagents): allow embedders to isolate runtime state roots** — [链接](https://github.com/Hmbown/CodeWhale/pull/5252)  
   为嵌入型宿主提供可选 `EngineConfig::subagent_state_root`，保持默认 cwd、文件权限、receipts 行为不变，但迁移 worker ledger 与完整脚本产物。状态为 CLOSED。

#### 📦 依赖升级（dependabot 批量提交）

8. **[#5281] chore(deps): bump jsonschema 0.49.4** — [链接](https://github.com/Hmbown/CodeWhale/pull/5281)  
9. **[#5280] chore(deps): bump thiserror 2.0.19** — [链接](https://github.com/Hmbown/CodeWhale/pull/5280)  
10. **[#5279] chore(deps): bump clap 4.6.1** — [链接](https://github.com/Hmbown/CodeWhale/pull/5279)  
    同批还有 async-trait (#5278)、serde_json (#5276)、docker/login-action (#5277)、rust-toolchain (#5275)、sccache-action (#5274)。其中 thiserror 2.0.19 与 async-trait 0.1.91 均同步至 syn 3，属于 Rust 生态链式升级。

---

### 四、功能需求趋势

从全部 42 条活跃 Issues 中提炼社区最关注的方向：

| 趋势方向 | 代表 Issue | 热度说明 |
|---------|-----------|---------|
| **Fleet/多 Worker 统一模型语义** | #3205 | 需统一 TUI/CLI/subagents/Worker 的负载选择器 |
| **大型 Rust 文件模块化拆分** | #3313、#3312、#3308、#3952、#3956 | v0.9.2–v0.9.4 持续多轮，单文件可达 5k–7k 行 |
| **TUI 内多会话/多任务管理** | #5271、#5270、#576 | 突破"仅 resume 选择器"的限制 |
| **计划产物持久化与可审阅** | #5269、#4390 | 计划模式不能只活在进程状态里，需可共享、可评论的产物 |
| **回合中控制（队列/取消/继续）** | #5268、#5267 | 用户对"锁死的聊天框"强烈抱怨 |
| **平台兼容（FreeBSD/winget）** | #1097、#1561 | FreeBSD 构建修复 PR 已合并；winget 包仍待推进 |
| **项目指令文件自动导入（onboarding）** | #3978 | 自动识别仓库中常见 agent/editor 指令文件 |
| **原生多模态视觉载荷** | #4101（CLOSED） | 绕过本地 OCR，直接发送原始图像字节到 LLM 后端 |
| **`model = auto` 自动分级选择** | PR #5257 | 社区对"既快又强"的按需模型选择诉求强烈 |

---

### 五、开发者关注点（痛点 / 高频需求）

1. **"状态说结束但模型还在说"** — Issue #5267 直指信任痛点：footer 显示 "ending"/"stopping" 但模型继续输出，开发者建议删除虚假保护而非增加文案。这反映了社区对 TUI 状态真实性的高要求。

2. **TUI 中无法便捷管理多会话** — Issue #576 描述了典型痛点：必须退出 TUI → `deepseek sessions` 看 ID → 手动复制 → 再敲命令。流程割裂。`fork --last` 虽能省去复制，但用户不一定记得。社区强烈建议 TUI 内 `/fork` 交互式选择。

3. **回合运行中聊天框"被锁死"** — Issue #5268 指出：Enter-while-busy 和 Ctrl-Enter steer 虽然存在，但 queue vs send-now vs cancel-keep-draft 不是清晰可见的契约。用户在回合中无法有效干预。

4. **大型文件维护困难** — v0.9.2–v0.9.4 系列重构 Issue（#3313、#3312、#3952、#3956）反复提及单文件 3k–7k 行问题：#3313 的 runtime_threads.rs 7,133 行、#3952 的 chat.rs 4,793 行 + client.rs 5,201 行。社区明确感知到维护负担。

5. **V4 Pro 长回合成本不可见** — Issue #1004 提到：长 system prompt + 多个缓存文件 + 工具定义 + @提及 + 多步思考时，开发者无法在发送前预览请求内容。对 V4 Pro 用户是具体的、反复出现的成本问题。

6. **恢复被破坏的工作区** — Issue #5272 指出当前恢复主要靠 git 考古，需要从 prompt 快照直接恢复并配合 git 保护用户提交。

---

> 📌 今日关键结论：**v0.9.4 发布卡在 CI 红灯，PR #5282 正面解决中；v0.9.5 已规划 6 个 agent-ready 新特性（多会话、任务统一视图、计划持久化等），方向明确；同时社区对 FreeBSD 支持迈出实质一步（PR #5254 合并），`model = auto` 自动分级选择方案已提交。** 核心工程焦点仍是大型 Rust 文件的模块化拆分与 TUI 状态真实性。

</details>

---
*本日报由 [agents-radar](https://github.com/kky-wollu/agents-radar) 自动生成。*
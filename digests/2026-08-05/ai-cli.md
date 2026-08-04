# AI CLI 工具社区动态日报 2026-08-05

> 生成时间: 2026-08-04 23:06 UTC | 覆盖工具: 9 个

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

### AI CLI 工具横向对比分析报告（2026-08-05）


### 一、生态全景

AI CLI 工具已从“编码助手”全面迈向“自主 Agent”时代，工具链深度与社区复杂度同步飙升。各工具普遍面临数据安全（worktree 隔离、SSH 为）与成本控制（配额烧毁、静默降级）两大信任危机，同时向桌面端、IDE 与移动端多入口延伸。Windows/WSL 混合环境成为各家共同的兼容性短板，而 MCP 与 ACP 协议则演变为生态卡位的新战场。


### 二、各工具活跃度对比

| **工具** | **今日版本发布** | **热点 Issues（Top 10 累计）** | **重要 PR** | **最热 Issue（👍/评论）** | **社区热度信号** |
|:---|:---:|:---:|:---:|:---:|:---|
| **Claude Code** | v2.1.222, v2.1.221 | 72 评论，48 👍 | 3 | 图片处理错误烧配额（29 评论） | 高（安全修复+功能更新，用户基数大） |
| **OpenAI Codex** | 4 个 alpha（0.147.0 系列） | 74 评论，52 👍 | 10 | 会话同步需求（21 👍）；WSL 文件访问（15 评论） | 极高（24h 内 4 版迭代，高频演进） |
| **Gemini CLI** | 无 | 61 评论，13 👍 | 10 | Subagent 假成功（12 评论）；通用代理挂起（8 👍） | 中高（P1 Bug 密集，维护者响应积极） |
| **GitHub Copilot CLI** | v1.0.79-1, v1.0.78 | 27 评论，24 👍 | 2 | 会话分支（25 👍）；自定义主题（23 👍） | 中（功能需求呼声高，PR 节奏偏慢） |
| **Kimi Code CLI** | 无（最新 0.31.1） | 29 评论，24 👍 | 3 | 跨设备远程控制（24 👍）；持久记忆（17 评论） | 中（ACP 生态活跃，功能需求集中） |
| **OpenCode** | v1.18.13, v1.18.12 | 70 评论，126 👍 | 10 | Go 用量 API（126 👍）；模型服务故障（15 评论） | 极高（模型故障引发 Issue 爆发式增长） |
| **Pi** | 无 | 64 评论，18 👍 | 10 | Compaction 企业故障（19 评论，18 👍） | 中（企业级功能稳定性成焦点） |
| **Qwen Code** | v0.21.5 | 66 评论 | 10 | 确定性工具执行边界（17 评论）；tmux 闪屏（11 评论） | 中高（安全与取消语义讨论深入） |
| **DeepSeek TUI** | 无（v0.9.4 发布列车推进中） | 12 评论 | 10 | File 工具静默假成功；编译性能 Epic | 中（维护者主导性能优化，社区围观） |


### 三、共同关注的功能方向

| **功能方向** | **涉及工具** | **具体诉求** |
|:---|:---|:---|
| **会话同步与跨设备协作** | Codex（#14722，21👍）、Kimi（#1282，24👍）、OpenCode | Codex 求 CLI/App 实时同步；Kimi 求手机/平板无缝续跑；OpenCode 桌面端配置加载回归 |
| **上下文压缩与成本控制** | Claude Code（#62466）、Qwen（#8452）、Pi（#7553）、Codex（#30816） | Claude 用户投诉错误烧配额；Qwen 微压缩使提示缓存反复失效；Pi 要求可配置 summarization 模型；Codex 计费周期不透明 |
| **Windows + WSL 体验优化** | Codex（#27552）、Copilot CLI（#4328）、Claude Code（#61021）、Kimi（#2584） | WSL 文件访问错配、`Ctrl+H` 误判、文本选择复制失效、IME 泰语重复输入 |
| **MCP 服务器生命周期管理** | Codex（#21984）、Copilot CLI（#4349）、DeepSeek TUI（#5130） | MCP 进程堆积、企业策略解析失败阻断全部 MCP、需要编程式生命周期管理 API |
| **自定义模型/端点（BYOK）** | Copilot CLI（#4139）、Pi（#7610）、OpenCode（#20491） | 接入第三方/本地 LLM、内置 LLM Gateway 与新路由器、Kiro（AWS）provider |
| **安全与信任边界** | Qwen（#8102）、Codex（#36960）、Claude Code（v2.1.222）、Gemini（#26525） | 确定性工具执行、目录信任明确确认、worktree 隔离、Auto Memory 确定性脱敏 |


### 四、差异化定位分析

| **工具** | **功能侧重** | **目标用户** | **技术路线** |
|:---|:---|:---|:---|
| **Claude Code** | 深度软件工程（安全隔离、插件系统、桌面远程） | 专业开发者/企业 | 安全优先，VSCode 深度集成，worktree 强隔离 |
| **OpenAI Codex** | 全平台覆盖（CLI/桌面/IDE），MCP 生态，高发布频率 | 多端重度用户/订阅用户 | Rust 核心，alpha 高频迭代，注重协议兼容（SSE） |
| **Gemini CLI** | Agent 子系统（Subagent）、评估体系（EPIC）、Auto Memory | Google 生态开发者/研究 | 组件级评估驱动，AST 感知工具前瞻，重视可观测性 |
| **GitHub Copilot CLI** | GitHub 生态深度绑定，企业策略管理，终端 TUI 打磨 | GitHub 企业用户 | 安全沙箱+策略控制，发布节奏稳健，关注配置兼容性 |
| **Kimi Code CLI** | ACP 协议深度——移动端/第三方客户端后端大脑 | 移动端/第三方客户端用户 | 协议驱动集成（ACP），轻量级，迎合移动化趋势 |
| **OpenCode** | 多 Provider 聚合，桌面端即时体验，Go 服务 | 对服务稳定性敏感的用户 | 大面积服务异常暴露运维短板，API 兼容性（Responses API）有缺口 |
| **Pi** | 企业级 Copilot 席位支持，RPC 开放，全屏 TUI | 企业用户/嵌入式客户端 | 聚焦企业认证链路（421/ OAuth），重视供应链安全 |
| **Qwen Code** | 确定性 Agent 运行时，安全加固，IDE（JetBrains）集成 | 追求 Agent 可信度的开发者 | 取消语义系统性修复，hook 信任边界加固，终端细节打磨 |
| **DeepSeek TUI** | 构建性能优化，Runtime HTTP API 补齐，ACP 工具执行 | 自托管/高性能用户 | 巨型 crate 拆分路线，发布列车模式（77 commits），侧重工程效率 |


### 五、社区热度与成熟度

**最活跃/爆发期**：**OpenAI Codex**（24h 4 个 alpha 版本，Issue/PR 双高，处于高频演进期）、**OpenCode**（模型故障引发 Issue 激增，但社区反馈说明用户量大且容忍度在下降）。

**成熟稳定期**：**Claude Code**（安全修复为主，社区讨论深刻但增量放缓，用户基数大）、**GitHub Copilot CLI**（版本节奏稳定，功能需求呼声高但 PR 推进慢，社区讨论深度较浅）。

**快速追赶期**：**Qwen Code**（安全与取消语义讨论深入，自动化 PR 密集）、**Gemini CLI**（P1 Bug 修复积极，评估体系有前瞻性，但社区 👍 数偏低，活跃度集中在核心用户）。

**转型/蓄力期**：**Kimi Code CLI**（ACP 生态带动新需求，但整体 Issue/PR 量偏小，依赖外部生态倒逼迭代）、**DeepSeek TUI**（维护者主导性能重构，社区参与度有限）、**Pi**（聚焦企业稳定与安全，但 👍 数普遍偏低，新功能需求响应快）。


### 六、值得关注的趋势信号

1. **“取消（Cancel）≠ 停止执行”成为 Agent 安全新议题**：Qwen Code 同一作者连续提交 5 个 cancel 语义 Bug（文件写入、shell、流式控制），揭示 Agent 在异步中断路径上的系统性安全缺陷。**参考价值**：在自动化场景中，取消动作必须级联终止所有副作用，否则将造成数据污染或资源失控。

2. **服务端稳定性成为信任分水岭**：OpenCode 的 DeepSeek V4 Flash 大面积故障（空白响应、HTTP 500、版本错配）引发 Issue 爆发，而 Claude Code 的“图片处理错误烧配额”和“Opus 4.8 故障烧毁周配额”同样直指成本与产出失衡。**参考价值**：工具的服务端运维质量正取代功能丰富度，成为用户留存的关键变量。

3. **企业级支持与个人开发者的诉求开始分化**：Pi 与 Copilot CLI 的关注点集中在企业席位、策略解析、OAuth 刷新等 B 端痛点；而 Kimi、Codex 社区则更关注移动端续跑、跨设备同步等个人效率场景。**参考价值**：选择工具时需根据团队规模（个人/企业）判断优先级，企业用户应优先考察认证健壮性与策略兼容性。

4. **协议层竞争加剧——ACP 成为新的生态卡位点**：Kimi 的 ACP 权限切换（PR #2364）与模型发现（#2583）、DeepSeek TUI 的 ACP 工具执行（PR #5225）、Qwen 的 JetBrains ACP 集成对比（#8544），多方力量正围绕 ACP 协议争夺第三方客户端的入口权。**参考价值**：注重 IDE 与移动端集成体验的开发者，应优先关注 ACP 协议成熟度与工具对 ACP 的支持深度。

5. **构建性能与工程效率开始被“正式立项”**：DeepSeek TUI 维护者一口气提交 5 个构建性能 Epic（crate 拆分、依赖裁剪、profile 分层），Qwen 引入成本账本（PR #8471）将性能排查从“考古”变为“读报表”。**参考价值**：随着 AI CLI 工具规模膨胀（66 万行代码、708 依赖包），编译时延与资源占用正成为重度用户的核心痛点，工具选择时应关注其工程可维护性。

6. **上下文压缩策略的“双刃剑”效应显现**：Qwen 微压缩反复使缓存失效推高成本、Pi compaction 在企业账号下 421 失败、Gemini `/compress` 会话卡死——压缩功能虽为长会话刚需，但实现质量参差。**参考价值**：长会话用户应关注压缩逻辑的触发条件与失败模式，必要时手动控制压缩时机或显式配置压缩模型，避免“省钱不成反烧钱”。

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

好的，以下是根据 `anthropics/skills` 仓库数据（截至 2026-08-05）生成的社区热点报告。

---

### 1. 热门 Skills 排行

以下依据 PR 评论数及引发的连锁讨论（如相关 Issue）排序，列出当前社区关注度最高的 5 个 Skill 及其状态。

**#1. `skill-creator` 修复与优化（含多个 PR）**
- **功能**：并非新 Skill，而是对官方 `skill-creator` 技能自身的修复，涉及 `run_eval.py` 触发检测、Windows 兼容性、并行进程隔离等。
- **社区热点**：这是当前最集中的“痛点”。多个 PR（#1298、#1099、#1050、#1323、#1261）都在修复 `skill-creator` 的评估脚本在 Windows 上崩溃、或错误地报告 `recall=0%` 的问题。该问题导致描述优化循环无法正常工作，严重影响了 Skill 开发者的核心工作流。
- **状态**：全部为 Open。但 Issue #556 有 12 条评论，社区高度关注，修复难度较大。
- **链接**：[PR #1298](https://github.com/anthropics/skills/pull/1298)、[Issue #556](https://github.com/anthropics/skills/issues/556)

**#2. `self-audit` 技能（#1367）**
- **功能**：一个通用型技能，在交付 AI 输出前进行“机械验证 + 四维推理质量门禁”，按损害严重性排序检查输出。
- **社区热点**：关注如何系统化地保证 AI 输出质量，特别是防止“幻觉”和文件缺失。其配套的流程提案（Issue #1385）也获得了关注。
- **状态**：Open（v1.3.0），作者在积极迭代。
- **链接**：[PR #1367](https://github.com/anthropics/skills/pull/1367)

**#3. `color-expert` 技能（#1302）**
- **功能**：一个全面、独立的色彩专业知识技能，涵盖色彩命名系统（ISCC-NBS、Munsell 等）、色彩空间选择表（OKLCH vs OKLAB）等。
- **社区热点**：填补了设计类技能中“色彩理论基础”的空白，讨论焦点在于其知识体系的完整性和实用性。
- **状态**：Open，更新频繁，讨论度高。
- **链接**：[PR #1302](https://github.com/anthropics/skills/pull/1302)

**#4. `document-typography` 技能（#514）**
- **功能**：针对 AI 生成文档的排版质量控制，解决孤行、寡行标题和编号错位问题。
- **社区热点**：精准解决了 AI 文档生成的一个普遍痛点（排版细节），讨论集中于此问题的普遍性和技能的边界。
- **状态**：Open。
- **链接**：[PR #514](https://github.com/anthropics/skills/pull/514)

**#5. `SAP-RPT-1-OSS` 预测器技能（#181）**
- **功能**：用于调用 SAP 开源表格基础模型 `SAP-RPT-1-OSS` 进行业务数据预测分析。
- **社区热点**：代表了企业级场景的需求，关注如何将专业模型封装为易用的 Agent 技能。
- **状态**：Open。
- **链接**：[PR #181](https://github.com/anthropics/skills/pull/181)

---

### 2. 社区需求趋势

从 Issues 中提炼出四个主要方向，按热度排序：

1.  **开发者工具链的完善（最高需求）**：社区并非在等待更多新技能，而是强烈要求**修复现有 `skill-creator` 的工具链缺陷**。尤其集中在 Windows 兼容性（Issue #1061）和评估逻辑错误（Issue #556）上。这反映了大量开发者正在尝试创建自己的技能，但被官方工具“卡脖子”。
2.  **安全与信任边界**：核心诉求是**建立安全、可信的技能分发与使用机制**。最强烈的声音是反对在 `anthropic/` 命名空间下分发社区技能（Issue #492），并开始关注技能本身带来的上下文窗口耗尽（Issue #1487）和数据安全（Issue #1175）风险。
3.  **组织级协作与分享**：企业用户迫切希望**实现技能的组织内共享**，而不是通过手动下载和上传 `.skill` 文件（Issue #228）。
4.  **系统化质量控制**：除了“修复”，社区也在探索**新技能来主动保证输出质量**，例如 `self-audit`（#1367）和 `plan-file-hygiene`（#1479）等，反映了从“被动修复”转向“主动预防”的趋势。

---

### 3. 高潜力待合并 Skills

以下 PR 评论活跃且契合社区需求，落地可能性较高：

- **`self-audit` (监听输出质量)**：[PR #1367](https://github.com/anthropics/skills/pull/1367) — 直接回应了社区对“保证输出质量”的呼声，且有配套的流程框架（Issue #1385），概念清晰，关注度高。
- **`color-expert` (设计领域增强)**：[PR #1302](https://github.com/anthropics/skills/pull/1302) — 内容详实，是设计类技能的有力补充，作者维护积极。
- **`plan-file-hygiene` (工作流治理)**：[PR #1479](https://github.com/anthropics/skills/pull/1479) — 针对规划文件生命周期管理的新兴痛点，虽然提出较晚但精准命中了长期运行 Agent 的上下文管理需求。
- **`document-typography` (文档质量修复)**：[PR #514](https://github.com/anthropics/skills/pull/514) — 解决的是非常明确且普遍的痛点，讨论中没有反对意见。

---

### 4. Skills 生态洞察

**一句话总结**：当前社区在 Skills 层面的最集中诉求是“**工具链可靠性**”——开发者们一边为官方 `skill-creator` 的评估/Windows 缺陷所困，一边在呼吁建立更安全、可治理的分发与质量保障机制，从追求“更多技能”转向“更稳、更安全地制造和使用技能”。

---

# Claude Code 社区动态日报 — 2026-08-05

## 今日速览

今日发布 v2.1.222 与 v2.1.221 两个版本，重点修复了 worktree 隔离绕过与 PreToolUse 钩子绕过两个安全漏洞，并在 VSCode 端新增了 Focus view 专注模式。社区侧，#62466（图片处理 API 错误持续消耗配额）以 29 条评论成为最热 Issue，同时多条关于 worktree 隔离失效的 Issue 集中关闭，暗示相关问题已获修复。

---

## 版本发布

### v2.1.222（最新）
- **安全修复**：修复 worktree 隔离会话及其子代理可对主检出运行破坏性 git 命令的问题；现在隔离机制适用于所有会话类型的文件编辑和 Bash 操作。
- **安全修复**：修复后台代理任务中 PreToolUse auto-allow 钩子绕过工具限制的问题。

### v2.1.221
- **[VSCode] 新增 Focus view**：聊天菜单中新增开关，可将工具活动隐藏在可展开的每轮摘要之后，并带有实时运行工具指示器。可通过 `Ctrl+Alt+F` 或 "Claude Code: Toggle Focus view" 命令切换。
- **Linux**：新增 `mode: "mask"` 用于沙箱凭据文件。

---

## 社区热点 Issues

精选 10 个最值得关注的 Issue：

**1. #62466 — [BUG] 图片处理 API 错误反复消耗使用配额**（🔥 29 评论，20 👍，OPEN）
作者报告 "Image couldn't be processed" 错误反复出现且持续消耗 API 配额，却未产出任何有效结果。评论数居首，说明大量用户受影响。核心痛点在于**错误既不致命也不成功，白白烧钱**。
[查看 Issue](https://github.com/anthropics/claude-code/issues/62466)

**2. #68514 — [BUG] macOS Sequoia 上 rootfs.img.zst 校验和不匹配**（16 评论，CLOSED/stale）
macOS ARM64 用户安装时反复遇到 rootfs 镜像校验失败。虽已标记 stale 关闭，但评论数高表明曾引发广泛讨论。
[查看 Issue](https://github.com/anthropics/claude-code/issues/68514)

**3. #61021 — [BUG] 无法轻松选择文本复制粘贴**（15 评论，11 👍，OPEN）
Windows + VSCode 终端用户反馈：运行 Claude Code 后鼠标选文本 + Ctrl+C 复制失效。影响日常开发效率，是**高频基础体验问题**。
[查看 Issue](https://github.com/anthropics/claude-code/issues/61021)

**4. #72123 — [BUG] 朗读功能播放中途音质劣化**（7 评论，OPEN）
Windows Desktop 用户报告 "Read Out Loud" 播放过程中声音变小、变速、变调直至消失。属于较新的桌面端功能缺陷。
[查看 Issue](https://github.com/anthropics/claude-code/issues/72123)

**5. #70108 — [BUG] iOS 版 Claude App 连接 Claude Code 时崩溃**（5 评论，6 👍，CLOSED/stale）
移动端与桌面端联动场景崩溃，与 Cowork 功能相关。虽已关闭，但点赞数表明关注度较高。
[查看 Issue](https://github.com/anthropics/claude-code/issues/70108)

**6. #70069 — [BUG] Worktree 隔离失效：编辑落到主检出分支**（4 评论，CLOSED）
会话报告显示在 worktree（`-w`）中运行，`cwd` 和 `gitBranch` 均正确，但所有文件编辑实际写入主检出的 `master` 分支。与 v2.1.222 修复直接对应，确认是已被解决的严重数据安全风险。
[查看 Issue](https://github.com/anthropics/claude-code/issues/70069)

**7. #69905 — [BUG] `/compact` 后代理丢失会话上下文**（4 评论，CLOSED/stale）
代理在 `/compact` 后混淆自身编辑与既有代码，导致简单的 UI 调整演变为漫长的错误修正。指向**上下文压缩后模型状态一致性**的问题。
[查看 Issue](https://github.com/anthropics/claude-code/issues/69905)

**8. #70242 — [BUG] Opus 4.8 安全分类器故障烧毁付费用户周配额**（2 评论，CLOSED）
200€+/月用户报告：6月22日 Opus 4.8 平台故障级联导致多小时的代理任务零输出但持续消耗配额。涉及**成本控制与故障补偿**，是企业用户核心关切。
[查看 Issue](https://github.com/anthropics/claude-code/issues/70242)

**9. #83815 — [BUG] 桌面 SSH 在仅密钥主机上陷入死胡同密码提示**（1 评论，OPEN，今日新）
新建 Issue：目标主机仅支持 `publickey` 认证，但应用弹出永远无法成功的密码对话框，且静默忽略不存在的 identity 文件。影响远程开发工作流。
[查看 Issue](https://github.com/anthropics/claude-code/issues/83815)

**10. #83643 — [BUG] 桌面远程会话插件同步遗漏 hooks/ 目录**（1 评论，OPEN）
桌面应用通过 SSH 驱动远程主机时，插件中的 hooks 从不触发（skills 和 commands 正常）。插件钩子逻辑在远程场景下缺失，属于较新的缺陷。
[查看 Issue](https://github.com/anthropics/claude-code/issues/83643)

---

## 重要 PR 进展

**1. #83890 — Create pylint.yml**（OPEN，2026-08-04）
新增 pylint CI 工作流配置。社区贡献者 KrypticKode007 提交，可能为仓库引入 Python 静态检查。
[查看 PR](https://github.com/anthropics/claude-code/pull/83890)

**2. #83374 — docs(plugin-dev): 记录 MessageDisplay 流式语义**（OPEN，2026-08-02）
修复官方 Hook Development skill 中 `MessageDisplay` 事件缺失的问题，补充到触发描述、事件指南和速查表。对插件开发者具有直接帮助。
[查看 PR](https://github.com/anthropics/claude-code/pull/83374)

**3. #83738 — Fix/83484 symlink 路径展开**（OPEN，2026-08-04）
修复部分 Linux 安装中 `claude install` 创建指向字面量 `%h` 占位符的损坏符号链接问题。安装可靠性的直接改进。
[查看 PR](https://github.com/anthropics/claude-code/pull/83738)

---

## 功能需求趋势

从近期 Issues 中提炼出社区最关注的方向：

| 方向 | 代表性 Issue | 热度信号 |
|------|-------------|---------|
| **工作树（Worktree）隔离可靠性** | #70069、#72714 | 数据安全核心关切，已促使 v2.1.222 专项修复 |
| **权限/审批 UX 一致性** | #64689、#70057 | VSCode 扩展的权限提示缺少 "session/project/always" 选项，且 "Always allow" 命令文本截断 |
| **桌面端远程/SSH 体验** | #83643、#83815 | SSH 密钥认证与 hooks 同步问题集中出现，远程开发场景逐渐普及 |
| **成本可见性与配额控制** | #62466、#70242 | 错误/故障导致配额消耗是付费用户最大痛点 |
| **终端/TUI 基础体验** | #61021、#70265、#70276 | 文本选择、渲染错误、Windows 终端可配置性 |
| **模型上下文一致性** | #69905、#70273、#70264 | `/compact` 后上下文丢失、模型冻结与幻觉对话 |
| **VSCode 集成深化** | #61021、#64689、#70057 | 插件权限、终端交互、命令显示等多点待完善 |

---

## 开发者关注点

**高频痛点：**

1. **配额消耗与产出不成正比**：多个 Issue（#62466、#70242、#70272）反映 API 错误或模型效率低下导致高额配额消耗但零输出，是社区情绪最激烈的板块。
2. **Worktree 数据安全风险**：隔离机制曾存在绕过路径（#70069、#72714），开发者担心编辑或 git 操作误入主分支。v2.1.222 已针对性修复，建议用户尽快升级验证。
3. **上下文压缩后行为漂移**：`/compact` 后模型混淆自身编辑与既有代码（#69905），以及模型生成虚假的 `Human:`/`Assistant:` 对话（#70264），是影响长会话可靠性的关键问题。
4. **权限提示细节缺失**：VSCode 扩展的权限对话框缺少细粒度选项（#64689）和命令文本截断（#70057），降低信任度与操作效率。
5. **Windows 平台体验滞后**：终端硬编码 PowerShell 5.1 无法配置（#70276）、选择复制失效（#61021），Windows 用户的桌面体验明显落后于 macOS/Linux。

**建议关注：**
- 安全修复（v2.1.222）涉及两条高危路径，建议所有用户优先升级。
- 今日新 Issue #83815（SSH 密钥验证）和 #83643（插件 hooks 同步）均为远程工作流的新缺陷，使用桌面远程功能的开发者应留意后续修复动态。

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报 — 2026-08-05

## 今日速览

过去24小时内，OpenAI Codex 发布了 4 个 `rust-v0.147.0` 系列 alpha 版本（`.alpha.7` / `.alpha.6.4` / `.alpha.6.3` / `.alpha.6.1`），节奏密集。社区 Issue 方面，Windows + WSL 模式下的文件访问与配置隔离问题持续发酵（#27552 以 15 条评论成为最热 Issue），而 PR 侧则有一批由 `copyberry[bot]` 提交的基础设施与安全增强（本地目录信任确认、并发请求分发、技能缓存共享修复等）。值得留意的是，多个新上报的 Bug 直指浏览器插件/工具在 `node_repl` 和 macOS 应用内运行时因 `process` 属性重定义而启动失败（#32936、#36988）。

## 版本发布

- **rust-v0.147.0-alpha.7** [查看](https://github.com/openai/codex/releases/tag/rust-v0.147.0-alpha.7)
- **rust-v0.147.0-alpha.6.4** [查看](https://github.com/openai/codex/releases/tag/rust-v0.147.0-alpha.6.4)
- **rust-v0.147.0-alpha.6.3** [查看](https://github.com/openai/codex/releases/tag/rust-v0.147.0-alpha.6.3)
- **rust-v0.147.0-alpha.6.1** [查看](https://github.com/openai/codex/releases/tag/rust-v0.147.0-alpha.6.1)

> 说明：各个 Release 均标注为 `0.147.0-alpha.x`，发布说明简短，未见显著功能变更摘要，推测为持续推进 0.147 稳定版过程中的内部迭代与 Bug 修复。

## 社区热点 Issues

1. **[#27552] Codex Desktop Windows: 图片附件保存至 Temp 但 WSL agent 无法访问** [查看](https://github.com/openai/codex/issues/27552)
   评论 15 | 👍 9 | 状态: Open
   当前最热 Issue。Windows 桌面版在 WSL 工作区下，模型生成的图片附件被保存到 Windows Temp 目录，但 WSL 侧的 agent 无法通过 `view_image` 访问。社区高频反馈的 Windows + WSL 混合环境痛点又添一例。

2. **[#21984] MCP servers 每次会话都急切启动，导致 headless browser 进程堆积** [查看](https://github.com/openai/codex/issues/21984)
   评论 13 | 👍 4 | 状态: Open
   配置的 MCP 服务器在每次 session 创建/恢复时都会无条件启动，即使对应工具未被使用。对于有头浏览器类 MCP 服务器，长时间运行的会话会累积大量可见浏览器进程，造成资源浪费。

3. **[#29787] Codex 应用更新后无法重新启动** [查看](https://github.com/openai/codex/issues/29787)
   评论 12 | 👍 2 | 状态: CLOSED
   点击更新按钮后应用关闭且不再重新打开。Windows 11 x64 平台，影响 ChatGPT Pro 订阅用户。该问题已关闭，但评论数说明了 Windows 桌面版更新流程的可靠性问题。

4. **[#22991] Codex 应用在超大 rollout/history JSONL 文件时冻结** [查看](https://github.com/openai/codex/issues/22991)
   评论 11 | 👍 1 | 状态: Open
   长会话产生的本地 JSONL 历史文件可超过 500 MB，继续工作时应用显著卡顿甚至冻结。性能类问题在长会话场景下是社区的重要关切。

5. **[#14794] VS Code Codex 扩展沙箱将可写 devcontainer 工作区呈现为只读** [查看](https://github.com/openai/codex/issues/14794)
   评论 10 | 👍 8 | 状态: Open
   在 Linux 上使用 devcontainer 时，沙箱机制导致本应可写的工作区在 IDE 中显示为只读。8 个 👍 说明受影响的开发者不在少数，IDE 集成沙箱行为是高频关注点。

6. **[#14722] 同步 CLI 与 app-server 会话** [查看](https://github.com/openai/codex/issues/14722)
   评论 9 | 👍 21 | 状态: CLOSED
   该 Enhancement 已关闭，但 21 个 👍 显示了社区对跨设备会话同步的强烈需求——通过 `codex resume` 从另一设备（如 SSH）连接时，希望原会话内容能实时同步显示。

7. **[#30816] 订阅 ChatGPT Plus 后每周用量重置日期意外改变** [查看](https://github.com/openai/codex/issues/30816)
   评论 8 | 👍 4 | 状态: Open
   订阅升级后，周用量计费周期被重置，用户感到困惑并认为影响使用规划。订阅类型与 rate-limit 计费周期的一致性问题。

8. **[#23211] Auto-review 拒绝使用 `codex exec`，因会向不受信任的外部服务发送内容** [查看](https://github.com/openai/codex/issues/23211)
   评论 7 | 👍 2 | 状态: CLOSED
   在 Auto-review 流程中调用 `codex exec` 会被安全机制拦截。涉及 sandbox 与 exec 的信任边界设计，社区对此类安全策略的讨论度较高。

9. **[#33037] CLI 在 Zellij 中 FocusGained 时冻结** [查看](https://github.com/openai/codex/issues/33037)
   评论 4 | 👍 1 | 状态: CLOSED
   在 Zellij 多路复用器中，CLI 每次焦点切换时同步查询终端调色板导致界面冻结。影响使用 tmux/zellij 等终端复用器的开发者。

10. **[#36673] Codex Desktop 间歇性地暴露无处理器注册的线程工具** [查看](https://github.com/openai/codex/issues/36673)
    评论 2 | 👍 0 | 状态: Open
    新近上报（2026-08-03），模型可以看到 `list_threads`、`read_thread`、`send_message` 等工具 schema，但调用时返回 `No handler registered for tool`。属 app-server 层会话状态管理的不稳定问题。

## 重要 PR 进展

1. **[#36992] 允许注入模型目录缓存** [查看](https://github.com/openai/codex/pull/36992)
   新增公共异步 `ModelsCache` 契约，允许模型提供方和 `OpenAiModelsManager` 注入自定义缓存实现，默认仍采用文件缓存。

2. **[#36987] 为 exec-server 增加可选并发请求分发** [查看](https://github.com/openai/codex/pull/36987)
   新增 `--concurrent-requests <COUNT>` 参数，避免长请求阻塞同一连接上的健康检查与清理操作，默认保持顺序处理。

3. **[#36960] 信任本地项目目录前弹出确认** [查看](https://github.com/openai/codex/pull/36960)
   安全增强：信任目录将启用项目级配置、hooks 与 exec 策略，存在提示注入风险。现在要求用户显式确认，而非自动信任未知项目。

4. **[#36976] 仅允许显式调用的 orchestrator skills** [查看](https://github.com/openai/codex/pull/36976)
   修复 `allow_implicit_invocation: false` 的 orchestrator skill 仍出现在模型可见目录中的问题，改为仅支持直接调用时可见。

5. **[#36989] 保留共享的内置 skill 缓存** [查看](https://github.com/openai/codex/pull/36989)
   修复同一 `CODEX_HOME` 下多进程共享系统 skill 缓存时，某服务禁用内置 skill 导致其他服务缓存文件被错误删除的问题。

6. **[#36966] 允许禁用内置图片查看器** [查看](https://github.com/openai/codex/pull/36966)
   新增稳定的 `features.view_image` 配置项（默认启用），关闭时不再对模型暴露 `view_image` 工具（包括 fresh-context 子代理和 guardian reviewer 轮次）。

7. **[#36981] 为 Amazon Bedrock 启用远程压缩（compaction）** [查看](https://github.com/openai/codex/pull/36981)
   为 Bedrock 增加 v1 协议的远程压缩能力，自动和手动压缩均使用 `/v1/responses/compact` 端点。

8. **[#36990] 移除遗留的协作模式变体** [查看](https://github.com/openai/codex/pull/36990)
   从 `ModeKind` 中删除隐藏的 `PairProgramming` 和 `Execute` 变体，清理废弃的 prompt 模板，模式处理仅保留 `Default` 和 `Plan`。

9. **[#36986] 为 ChatGPT 请求增加进程级 PSP 路由** [查看](https://github.com/openai/codex/pull/36986)
   添加隐藏的全局 `--psp` 运行时标志，贯穿 TUI、exec、app-server 等所有启动路径，用于为第一方 ChatGPT 请求附加 `oai-chat-psp=true` cookie。

10. **[#36984] 在 HTTP 客户端中支持配置的 ChatGPT cookies** [查看](https://github.com/openai/codex/pull/36984)
    让 `HttpClientFactory` 可携带额外 ChatGPT cookies，并在克隆的 factory 间共享 cookie 存储，支持按路由或用户显式启用。

## 功能需求趋势

- **会话同步与跨设备协作（#14722）**：21 个 👍 为本周最高，社区对跨 CLI/App 的实时会话同步有明确期待。
- **MCP 服务器生命周期管理（#21984）**：按需启动而非会话创建即启动，避免资源浪费，说明 MCP 生态正在扩展，开发者开始关注其运行效率。
- **Windows + WSL 混合体验优化（#27552、#25745、#25747 等）**：大量 Windows 用户在 WSL 模式下遇到文件路径、配置读取（AGENTS.md / config.toml）不一致的问题，期望桌面 App 与 WSL 工作区深度对齐。
- **沙箱与安全策略可配置性（#14794、#23211）**：开发者希望在安全可控的前提下，拥有更灵活的沙箱读写权限和外部服务调用策略。
- **新模型与订阅计费透明性（#30816、#29362、#32344）**：关于模型用量统计不准确、订阅计划识别错误、计费周期重置等反馈较密集，社区对用量数据的准确性和透明度要求不断提高。

## 开发者关注点

- **Windows 桌面版体验是当前最大痛点**：更新后无法重启（#29787）、超大会话文件冻结（#22991）、WSL 模式下配置与文件访问错配（#27552、#25745、#25747）——建议使用 Windows 的开发者关注相关 Issue 的修复进展。
- **内存与性能问题开始浮现**：长会话 JSONL 文件膨胀导致 UI 卡顿（#22991），Windows 下共享/GPU 内存无法回收造成系统性内存增长（#32778），建议开发者定期清理历史会话或关注官方性能优化。
- **安全与信任边界持续收紧**：PR #36960（目录信任确认）和 #36976（显式调用 skill）显示官方正在主动补齐提示注入防护面，开发者升级后可能遇到更多交互确认提示，属预期行为。
- **浏览器工具链的 `node_repl` 兼容性问题不可忽视**：#32936 和 #36988 均指向 `Cannot redefine property: process`，影响 Chrome 插件导入与 macOS 内嵌浏览器初始化，涉及 `process` 全局变量冲突，建议在相关场景下留意工具版本兼容性。
- **发布节奏稳定**：0.147.0 系列 alpha 在 24 小时内连续迭代 4 个版本，说明项目处于高频演进期，开发者可保持关注 alpha 版本更新以提前验证新特性（如并发 exec-server、可配置 token budget 等）。

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报 — 2026-08-05

> 数据来源: [github.com/google-gemini/gemini-cli](https://github.com/google-gemini/gemini-cli)

---

## 今日速览

尽管今日无新版本发布，但社区在 Agent 子系统稳定性（尤其是 Subagent 恢复逻辑与浏览器代理）和 Auto Memory 功能的安全性优化上讨论热烈，多个 `priority/p1` 级别的 Bug 正在被积极复测。PR 侧则迎来一批针对崩溃、挂起和配置解析等问题的修复提交，其中不乏 `help wanted` 标记，社区贡献者参与度显著。

---

## 社区热点 Issues（Top 10）

**1. Subagent 到达 MAX_TURNS 后误报成功**｜[#22323](https://github.com/google-gemini/gemini-cli/issues/22323) （P1 · 12 评论）
`codebase_investigator` 子代理在达到最大轮次限制且未完成分析时，状态却显示为 `success` 和 `GOAL`。这一"假成功"反馈会掩盖真实的中断原因，严重误导用户对任务完成情况的判断。社区共收到 12 条讨论，位列当前 Issue 热度榜首。

**2. 通用代理（Generalist agent）挂起无响应**｜[#21409](https://github.com/google-gemini/gemini-cli/issues/21409) （P1 · 8 评论 · 8 👍）
当委托给 generalist agent 处理简单操作（如创建文件夹）时，CLI 永久挂起，有用户反映等待一小时仍无结果。该问题已获 8 个赞，是社区近期痛点之一。一种 workaround 是明确指示模型不要使用 sub-agents。

**3. 组件级评估体系（EPIC）**｜[#24353](https://github.com/google-gemini/gemini-cli/issues/24353) （P1 · 7 评论）
此 EPIC 关注生成式 AI 的行为评估。目前已为 6 个受支持的 Gemini 模型生成了 76 个行为评估测试，该 Issue 作为后续组件级评估工作（如 AST 感知的文件读取评估）的跟踪入口，对确保 Agent 代码质量升级至关重要。

**4. 评估 AST 感知工具的价值（EPIC）**｜[#22745](https://github.com/google-gemini/gemini-cli/issues/22745) （P2 · 7 评论）
该 EPIC 跟踪一系列关于"AST 感知的文件读取、搜索与代码库映射"能否提升效率的调研，旨在减少工具调用次数和上下文噪声。相关实验方向（如推荐调研 `tilth` 或 `glyph`）也延续至下游 Issue。

**5. 自定义技能与 Subagents 利用不足**｜[#21968](https://github.com/google-gemini/gemini-cli/issues/21968) （P2 · 6 评论）
社区反馈 Gemini CLI 在独立运行时几乎不会主动调用已配置的自定义 skills 和 sub-agents，只有用户明确指令才会使用。作者以 "gradle" 和 "git" skill 为例，认为现有提示词未能有效激活它们。

**6. Shell 命令执行完成后卡死**｜[#25166](https://github.com/google-gemini/gemini-cli/issues/25166) （P1 · 4 评论 · 3 👍）
一个执行极简单 CLI 命令后，即使命令已完成，界面仍显示"Waiting input"的卡死 Bug，非常影响日常使用体验。

**7. Auto Memory 无限重试低信号会话**｜[#26522](https://github.com/google-gemini/gemini-cli/issues/26522) （P2 · 5 评论）
Auto Memory 系统在判断某会话为低信号并跳过读取后，该会话不会被标记为已处理，导致被反复呈现在待处理索引中，造成资源浪费并增加冗余日志。

**8. Auto Memory 日志与脱敏机制需改进**｜[#26525](https://github.com/google-gemini/gemini-cli/issues/26525) （P2 · 4 评论）
当前 Auto Memory 在将本地内容送入模型前，秘密信息的脱敏仅依赖模型提示，且后台进程可能记录本不应持久化的数据。该 Issue 建议引入确定性脱敏并削减冗余日志。

**9. Wayland 环境下 Browser Agent 运行失败**｜[#21983](https://github.com/google-gemini/gemini-cli/issues/21983) （P1 · 4 评论 · 1 👍）
Browser subagent 在 Wayland 显示协议下无法正常工作并直接终止，属于限制用户环境的兼容性问题。

**10. `.gemini/agents/` 下符号链接不被识别**｜[#20079](https://github.com/google-gemini/gemini-cli/issues/20079) （P2 · 4 评论）
当 `~/ .gemini/agents/filename.md` 为符号链接时，CLI 无法将其识别为 Agent，社区用户希望官方能支持符号链接以方便配置管理。

---

## 重要 PR 进展（Top 10）

**1. [CLOSED] 支持 Issue 评论触发重新分诊**｜[#28690](https://github.com/google-gemini/gemini-cli/pull/28690)
通过监听 `issue_comment.created` 事件，使 care-taker agent 能响应 `@caretaker-agent` 提及或 `/caretaker triage` 命令，对 `NEEDS_INFO` 状态的问题进行再分诊，并回执评论。

**2. 防止窄宽度下文本换行死循环**｜[#28641](https://github.com/google-gemini/gemini-cli/pull/28641) （P2 · `help wanted`）
修复 `InputPrompt.tsx` 中 `getGhostTextLines` 在输入宽度小于单个宽字节（如 CJK/emoji）时出现死循环的问题，并新增回归测试。Fixes #19985。

**3. 修复日志截断工具对非正 `maxChars` 的处理**｜[#28639](https://github.com/google-gemini/gemini-cli/pull/28639) （P1）
修复 `formatTruncatedToolOutput` 当 `maxChars <= 0` 时因负索引切片导致的输出膨胀约 2 倍的问题。Fixes #28620。

**4. OAuth 流支持 Cloud Workstations 代理动态重定向**｜[#28688](https://github.com/google-gemini/gemini-cli/pull/28688) （P3 · 安全）
修复在 Cloud Workstations VM 中因固定回调 `localhost` 导致的 OAuth 失败，改为动态解析代理的 redirect URI。

**5. 修复 `/compress` 会话卡死与配额回退的上下文损坏**｜[#28672](https://github.com/google-gemini/gemini-cli/pull/28672)（`maintainer only` · `help wanted`）
该 PR 包含两个独立修复：一是解决 `/compress` 因会话恢复文件读取失败而永久卡死；二是防止在触发配额回退时丢失工具响应而污染上下文。

**6. 修复上下文损坏与配额错误回退问题**｜[#28671](https://github.com/google-gemini/gemini-cli/pull/28671)
处理工具执行被中断（如配额回退或用户 ESC 中断）后的历史强化与"自动补全"前缀延续问题，以防御性逻辑保护上下文。

**7. 增加 `IdeClient` 进程遍历超时机制**｜[#28677](https://github.com/google-gemini/gemini-cli/pull/28677) （P1 · `help wanted`）
为 `IdeClient.getInstance()` 增加 3 秒超时，避免进程树遍历挂起导致 TUI 在无 IDE 环境下无限显示"Initializing..."。

**8. MCP 扩展更新许可与 stdio 环境加固**｜[#28664](https://github.com/google-gemini/gemini-cli/pull/28664)
原先许可提示只展示 MCP 服务配置的部分字段，该 PR 补全了 `env`、`cwd`、`headers` 等执行影响字段的展示与一致性比对。

**9. 修复 `GEMINI_API_KEY` 认证时的 401 错误**｜[#28546](https://github.com/google-gemini/gemini-cli/pull/28546) （P1 · 安全）
当用户使用 `GEMINI_API_KEY` 认证时，残留的 `Authorization` 请求头会导致 Google API 返回 `ACCESS_TOKEN_TYPE_UNSUPPORTED` 错误。此 PR 修复该冲突，Fixes #28538。

**10. 修复终端信号转发至子进程**｜[#28676](https://github.com/google-gemini/gemini-cli/pull/28676) （P2 · `help wanted`）
`relaunchAppInChildProcess` 现在会将 SIGTERM、SIGHUP 等终止信号转发给子进程，避免杀掉引导父进程后遗留孤儿进程。

---

## 功能需求趋势

- **AST 感知的代码库操作**：多个 EPIC 表明官方正在评估引入 AST 以精确读取方法边界、优化代码检索与映射，减少 Token 消耗。
- **Auto Memory 体验与安全优化**：社区关注点集中在提高会话筛选效率、增加确定性脱敏、以及更精细的日志控制。
- **自研/定制 Agent 的自动化使用**：用户期望 Gemini CLI 能更主动地在合适场景调用自定义 skills 与 sub-agents，减少手动干预。
- **云开发环境（Cloud Workstations）适配**：针对该环境的 OAuth 认证流程代理支持被提出。
- **本地模型后端支持（SGLang 等 OpenAI 兼容端点）**：[PR #28681](https://github.com/google-gemini/gemini-cli/pull/28681) 正在尝试扩展模型后端接入能力。

---

## 开发者关注点

- **关键路径稳定性**：Subagent 挂起、Shell 命令假死、错误成功状态误报等 P1 问题高频出现，直接影响开发者的自动化任务流。
- **上下文完整性保护**：针对配额回退、中断压缩等场景，社区着手修复工具响应丢失与上下文损坏问题，表明开发者对长任务可靠性有较高要求。
- **可观测性与诊断改进（Bugreport）**：社区期待 `/bug` 报告能包含 subagent 内部上下文，以解决复杂问题排查困难。
- **安全与配置透明度**：MCP 服务配置（`env`、`cwd` 等）的完整展示、OAuth 回调资源清理等问题，反映出开发者对配置透明与安全性的敏感度提升。
- **终端兼容性与用户体验**：针对 CJK/emoji 输入、终端 resize 闪烁等问题，存在持续的 UI 稳定性修复需求。

---
*本次日报由 AI 工具辅助分析生成，供技术交流参考，内容不代表 Google 官方立场。*

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报

**日期：2026-08-05**


## 今日速览

昨日发布了 v1.0.79-1 与 v1.0.78 两个版本，带来了**沙箱配置项的破坏性更名**（`allowDevToolCaches` → `allowDevToolAccess`）以及**工具调用耗时实时显示**两项关键更新。社区方面，围绕 **WSL2 按键冲突**、**企业策略解析导致 MCP 服务器被阻断**以及 **内置 view 工具路径误判**等问题的讨论最为激烈；功能需求上，**自定义主题**、**自定义模型端点（BYOK）** 与**会话分支**呼声最高。


## 版本发布

### v1.0.79-1
- **🚨 破坏性变更**：沙箱配置项 `allowDevToolCaches` 更名为 `allowDevToolAccess`（由于实际授予的权限范围已扩大至 dev-tool 配置与注册表）。旧键名将被静默忽略，若此前显式设置 `false` 将回退为默认开启，需手动重命名。
- **其他改进**：具体细节未完整披露。

### v1.0.78
- **界面改进**：时间线头部新增每个工具调用的耗时显示（右对齐，运行中实时跳动），仅对耗时 ≥5 秒的调用生效。默认开启，可通过 `/settings showToolDurations` 关闭。
- **插件更新**：第一方插件在会话启动时自动更新至最新版本。
- **其他**：还包括若干未列出的扩展改进。


## 社区热点 Issues（Top 10）

### 1. [#4328 Ctrl+H 在 WSL2 下被误判为 Ctrl+Backspace](https://github.com/github/copilot-cli/issues/4328)
**标签**：`input-keyboard` / `platform-windows` | **评论** 5 | **👍** 0
> 因 Windows Terminal 泄露 `WT_SESSION` 环境变量，WSL2 中 `/help` 文档声明的 "ctrl+h 删除前一字符" 实际表现为删除整个单词。属于 Windows 平台下的典型按键映射冲突，影响 WSL2 用户的日常编辑效率。

### 2. [#4202 内置 view 工具对存在的文件误报 "Path does not exist"](https://github.com/github/copilot-cli/issues/4202)
**标签**：`non-interactive` / `tools` | **评论** 4 | **👍** 1
> v1.0.73 中内置 `view` 工具对已存在的文本文件报错，而 v1.0.71 正常，问题自 v1.0.72 引入。开发者提供了可控复现步骤，大概率属于回归缺陷，影响自动化脚本的稳定性。

### 3. [#4349 企业策略枚举值校验失败，阻断所有本地/自定义 MCP 服务器](https://github.com/github/copilot-cli/issues/4349)
**标签**：`enterprise` / `configuration` / `mcp` | **评论** 1 | **👍** 0
> GHE 托管策略返回 `"enable"` 作为 `disableBypassPermissionsMode` 的值，但 CLI 校验器仅接受字面量 `"disable"`，导致启动时策略拉取失败并以关闭（fail-closed）方式阻断所有自定义 MCP 服务器。企业用户的配置兼容性问题，影响范围较大。

### 4. [#4361 插件技能斜杠命令回归：被重写为 doomed RPC 调用](https://github.com/github/copilot-cli/issues/4361)
**标签**：`triage` | **评论** 1 | **👍** 0
> 桌面端调用插件技能（如 `/grill-me`）时，原本应被客户端重写为自然语言指令，现在直接触发 `session.commands.invoke` RPC 并失败。影响通过桌面 App 使用 CLI 插件的用户。

### 5. [#1504 自定义主题支持（含分享能力）](https://github.com/github/copilot-cli/issues/1504)
**标签**：`theming-accessibility` | **评论** 8 | **👍** 23
> 提议在 `/theme` 中允许用户创建自定义主题，并以 JSON 文件形式分享。属于呼声较高的可定制性需求，已积累 23 个 👍。

### 6. [#1697 会话分支：将对话分支为并行会话并共享上下文](https://github.com/github/copilot-cli/issues/1697)
**标签**：`sessions` / `context-memory` | **评论** 3 | **👍** 25
> 面对多步骤任务的自然分叉点，用户希望无需丢失当前上下文即可并行处理两个独立问题。本需求获得 25 个 👍，是当前最高赞的开放功能请求之一。

### 7. [#4005 企业版无法保存记忆："Copilot billing entity isn't selected"](https://github.com/github/copilot-cli/issues/4005)
**标签**：`enterprise` / `context-memory` | **评论** 3 | **👍** 3
> 企业环境下记忆保存功能报错，但其余功能正常，且此前可正常使用。属于企业版特有回归，影响上下文记忆的持久化。

### 8. [#4267 原生 Windows zellij 下输入框被 DA1 设备属性回复预填充](https://github.com/github/copilot-cli/issues/4267)
**标签**：`input-keyboard` / `platform-windows` / `terminal-rendering` | **评论** 2 | **👍** 0
> 启动时输入框被原始终端转义序列 `[?61;6;7;…c` 预填充，属于终端能力协商时序问题。影响 zellij + Windows 用户。

### 9. [#4365 sessionStart 提示钩子在 /new 和 /clear 时不触发](https://github.com/github/copilot-cli/issues/4365)
**标签**：`triage` | **评论** 0 | **👍** 0
> 钩子名称暗示每当新会话开始时触发，但实际 `/new` 和 `/clear` 均跳过 `sessionStart` 钩子，行为与命名不一致。影响依赖钩子做会话初始化的自动化工作流。

### 10. [#4352 增加禁用 OSC 9;4 进度条转义序列的选项](https://github.com/github/copilot-cli/issues/4352)
**标签**：`CLOSED` | **评论** 1 | **👍** 0
> 在 kitty 等终端下 OSC 9;4 进度条渲染为视觉干扰，且无任何环境变量或设置可关闭。已被关闭，但反映出终端兼容性配置的精细化需求。


## 重要 PR 进展

> 过去 24 小时内仅 2 个 PR 有更新，无重要的功能合并或修复提交。

| PR | 说明 |
|---|---|
| [#4366 安全扫码修复（fundamentals）](https://github.com/github/copilot-cli/pull/4366) | Vault 机器人自动提交的安全基线修复，待人工审查并替换 `<UPDATE_ME>` 占位值后合入，涉及 ci/production 环境。 |
| [#4355 Merge](https://github.com/github/copilot-cli/pull/4355) | 无描述的合并请求，信息不足，暂无法评估内容。 |


## 功能需求趋势

从近期 Issue 中可提炼出以下社区最关注的功能方向：

1. **自定义模型端点（BYOK 深化）** — [#4139](https://github.com/github/copilot-cli/issues/4139) 等持续要求支持接入第三方/本地 LLM（Azure OpenAI、Google Cloud AI 等），且 [#4196](https://github.com/github/copilot-cli/issues/4196) 显示 BYOK 场景下流式 `reasoning_content` 会导致重试风暴，说明 BYOK 路径的稳定性亟需加强。
2. **会话管理增强** — 会话分支（#1697）、云同步会话（#1947）、删除会话命令（#2019）等需求密集，社区对会话生命周期的精细控制诉求强烈。
3. **可定制性与可访问性** — 自定义主题（#1504）、持久化上下文/token 指示器（#2532）、OSC 序列禁用开关（#4352）等，反映用户对 CLI 外观与终端兼容性的个性化需求上升。
4. **企业/组织级能力修复** — 组织级 Agent 不显示（#1285）、企业策略解析失败（#4349）、企业记忆保存失败（#4005）等，企业用户的配置兼容性成为高频痛点。


## 开发者关注点

- **配置变更的破坏性影响**：v1.0.79-1 中沙箱设置更名虽合理（权限范围扩大），但旧键被**静默忽略**意味着已有的 `false` 显式关闭将**静默回退为开启**，存在安全隐患。建议升级时主动检查并重命名配置项。
- **Windows/WSL2 生态问题集中**：`Ctrl+H` 误判（#4328）、原生 Windows zellij 下的 DA1 预填充（#4267）、Windows 持续崩溃（#4026，自 5 月未解决）等现象密集，Windows 平台的输入与终端兼容性仍是短板。
- **企业策略解析健壮性**：#4349 的 fail-closed 行为导致 MCP 服务器全部被阻断，属于高影响故障；建议在策略解析失败时提供降级或明确报错而非静默阻断。
- **钩子语义一致性**：#4365 的 `sessionStart` 命名与行为不一致，开发者呼吁明确 `sessionStart` 的触发边界（是否涵盖 `/new` 与 `/clear`）。
- **高赞需求待回应**：#1697（会话分支，👍25）与 #1504（自定义主题，👍23）是当前社区最想要的功能，官方尚未给出明确 roadmap 回应。

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报

**日期：2026-08-05** | 数据来源：github.com/MoonshotAI/kimi-cli

---

## 今日速览

昨日社区讨论热度有所回暖，核心焦点集中在 **跨设备远程控制**（#1282）与 **持久化记忆系统**（#1283）两大功能需求上，两者合计获得近 30 条评论。同时，**ACP 协议能力扩展** 成为新晋热点——既有新 Issue 提出模型列表发现与会话中切换的需求（#2583），也有 PR 推进权限模式切换（#2364），表明外部 ACP 客户端的集成需求正在上升。Windows 平台 IME 输入重复字符的 Bug 为昨日新增，目前仍无回复，值得关注。

---

## 版本发布

过去 24 小时内无新版本发布。最新版本仍为 **0.31.1**（Windows 用户反馈中提到的版本）。

---

## 社区热点 Issues

以下为过去 24 小时内更新或创建的最值得关注的 Issue：

### 1. [#1283 Feature Request: Memory System - Persistent context across sessions](https://github.com/MoonshotAI/kimi-cli/issues/1283) 🔥
- **作者**: CatKang | **更新**: 08-04 | **评论**: 17 | **👍**: 0
- **为什么重要**: 这是社区长期追踪的高频需求（自 2 月创建至今仍在活跃讨论）。该 Issue 提议实现一套包含**自动记忆（AI 管理）** 与**手动记忆（用户自定义指令）** 的完整记忆系统，帮助 CLI 在跨会话中保持项目模式与用户偏好。尽管 👍 数较少，但评论区讨论热度高（17 条），说明社区对更智能的上下文管理有持续需求。
- **社区反应**: 讨论中出现了关于记忆存储格式、隐私控制及跨设备同步的延伸探讨。

### 2. [#1282 Feature Request: Remote Control - Continue local sessions from any device](https://github.com/MoonshotAI/kimi-cli/issues/1282) 🔥🔥
- **作者**: CatKang | **更新**: 08-04 | **评论**: 12 | **👍**: 24
- **为什么重要**: **今日获 👍 数最高** 的 Issue。用户希望在手机、平板或任意浏览器上继续本地 CLI 会话，实现“桌面-移动”无缝切换。这与当前远程开发/AI 编程助手移动化的趋势高度吻合，24 个 👍 表明需求覆盖面较广，并非个例。
- **社区反应**: 高热度，评论区有用户提到与 `kimi acp` 配合移动端 App（如 Happy Coder）的使用场景，与该 Issue 的关联性强。

### 3. [#2584 Bug: Thai (and other IME-based) characters duplicated when typing in the prompt on Windows](https://github.com/MoonshotAI/kimi-cli/issues/2584) 🐛 新增
- **作者**: mgprona | **创建**: 08-04 | **评论**: 0 | **👍**: 0
- **为什么重要**: 昨日新增的 Windows 平台输入法 Bug。泰语等多字节 IME 字符在 prompt 中出现**重复输入**，直接影响非英语用户的日常使用。当前版本 0.31.1，Windows 11 环境，尚无维护者回复。
- **社区反应**: 暂无讨论，属于待确认的输入兼容性问题。

### 4. [#2583 feat(acp): advertise available models and support mid-session model switching](https://github.com/MoonshotAI/kimi-cli/issues/2583) 新增
- **作者**: tizerluo | **创建**: 08-04 | **评论**: 0 | **👍**: 0
- **为什么重要**: 针对 **ACP (Agent Client Protocol)** 模式的功能增强请求。当通过 ACP 客户端（如 Happy Coder 移动端、Zed）驱动 `kimi acp` 时，客户端**无法发现可用模型列表**，也不能在会话中切换模型。这对于希望将 kimi 作为后端、在移动端自由切换模型的用户（与 #1282 呼应）是关键缺失。
- **社区反应**: 暂无讨论，但需求指向明确，来自第三方客户端开发者的直接反馈。

---

## 重要 PR 进展

过去 24 小时内共有 3 个 PR 有更新动态：

### 1. [#2364 feat(acp): support permission mode switching](https://github.com/MoonshotAI/kimi-cli/pull/2364) 🚀
- **作者**: huntharo | **更新**: 08-04 | **状态**: OPEN
- **功能说明**: 在协议层面为 Kimi 会话支持 **ACP 权限模式切换**。此 PR 广告 `default` 权限模式，并允许客户端在会话中动态切换权限级别（如从 `default` 切换到更严格的模式）。⚠️ **注意**：该 PR 依赖 #2363，需按顺序合并。
- **价值**: 这补齐了 ACP 协议的关键一环，使得 kimi 能被更安全地嵌入到需要细粒度权限管控的第三方应用或企业环境中。

### 2. [#2585 feat(cli): set AI_AGENT for subprocesses](https://github.com/MoonshotAI/kimi-cli/pull/2585) 新增
- **作者**: complynx | **创建**: 08-04 | **状态**: OPEN
- **功能说明**: 为 **pip/uv 与独立二进制** 两种入口启动的子进程统一暴露 `AI_AGENT=kimi` 环境变量标记。
- **价值**: 为上层编排工具（orchestrator）或包装脚本提供**统一的 Agent 识别能力**，便于在复杂工具链中做分支逻辑判断。这是社区工具链生态建设的一小步，但对集成方很实用。

### 3. [#2200 fix(shell): adapt timeouts for long commands](https://github.com/MoonshotAI/kimi-cli/pull/2200)
- **作者**: he-yufeng | **更新**: 08-04 | **状态**: OPEN
- **功能说明**: 自动延长**常见慢命令**（如 git submodule cleanup、git clone/fetch、包安装、构建）的超时时间，普通命令维持 60 秒默认值，若调用方设置了显式超时则优先保留。
- **价值**: 解决长时间运行命令被错误中断的问题，提升 `kimi` 在真实项目中的健壮性，属于体验优化类 PR。

---

## 功能需求趋势

综合近期 Issues 与 PR 讨论，社区最关注的五大功能方向如下：

1. **ACP 协议深化与移动端集成** 🔥
   - 代表：#2583（模型列表发现与会话中切换）、#2364（权限切换 PR）、#1282（跨设备远程控制）
   - 趋势解读：社区对 kimi 作为 **“可嵌入任意前端的后端大脑”** 的期待迅速升温。从单纯的终端工具向 **Agent 后端服务** 延伸，移动端与 IDE（Zed 等）成为关键场景。

2. **跨会话持久记忆（Memory System）** 🔥
   - 代表：#1283
   - 趋势解读：从“聊天助手”进化为“长期协作者”的必经之路。用户希望 CLI 能记住项目约定与个人偏好，减少重复提示。讨论热度（17 条评论）与实际 👍 数（0）的巨大反差，暗示该需求可能主要由深度用户推动，但尚未获得大众广泛关注。

3. **多模型支持与模型自由切换**
   - 代表：#2583（ACP 侧）、历史 Issue
   - 趋势解读：用户不再满足于固定模型，期望在会话中动态切换（尤其在 ACP 模式下），这关系到成本控制与任务适配。

4. **Windows 平台输入与本地化体验** 🐛
   - 代表：#2584（IME 重复字符）
   - 趋势解读：非英语用户开始暴露输入法兼容性问题，提示 CLI 在 **Windows 下的字符处理** 仍需打磨，尤其针对 CJK 及泰语等复杂 IME。

5. **子进程环境标准化与可观测性**
   - 代表：#2585（AI_AGENT 标记）
   - 趋势解读：社区工具链（如工作流编排）希望**标准化识别 AI Agent**，便于在复杂 pipeline 中做统一调度与日志分析。

---

## 开发者关注点

### 高频痛点
- **跨设备工作流中断**: 多个 Issue 与讨论集中指向“离开桌面即断线”的痛点，远程控制（#1282）呼声最高，用户希望能在手机/平板上无缝接力。
- **模型选择黑盒**: 特别是 ACP 客户端用户，无法获知可用模型列表，导致“不知道能用什么”的困惑（#2583）。
- **长命令执行焦虑**: 构建/克隆等长任务易超时中断，虽然已有 PR（#2200）修复，但暴露了 **shell 执行超时策略粗糙** 的问题。

### 高频需求
- **上下文不丢失**: 用户对会话切换、模型切换过程中的上下文保留有较高期待（#1283 与 #2583 的关联点）。
- **权限细粒度控制**: 在企业级或第三方工具集成场景中，用户希望可以**动态调整 ACP 权限模式**，而非一成不变（#2364）。
- **环境变量标准化**: 第三方工具期望通过 `AI_AGENT` 等标记快速识别 kimi 子进程，减少集成摩擦（#2585）。

---

> 💡 **分析师点评**: 昨日社区需求呈现出 **“从终端工具向智能体后端服务演进”** 的清晰脉络。ACP 生态的活跃（移动端、Zed）正在倒逼 kimi 在协议层面补齐能力（模型发现、权限切换），而 #1282 的 24 个 👍 则说明“随时随地继续工作”是用户最迫切的愿望。维护者若能在 ACP 能力上快速跟进（#2583、#2364），有望进一步巩固 kimi 在第三方客户端中的渗透率。Windows IME 问题虽小，建议尽快回应以防负面情绪积累。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 — 2026-08-05

## 今日速览

OpenCode 遭遇大规模服务异常：**DeepSeek V4 Flash 模型在 OpenCode Go 服务上出现大范围故障**，大量用户报告模型"卡在思考中"或返回空白响应（#40467、#40469、#40473 等），并伴随 HTTP 500 错误及模型版本错配问题（#40409、#40480），社区反馈集中爆发。与此同时，项目发布了 v1.18.13 补丁版本，修复了 TUI 的 GitHub PR review 上下文和桌面端 RTL 布局问题，但未能解决模型服务故障。此外，一个长期未解决的剪贴板问题相关 PR（#30472）仍在推进中。

---

## 版本发布

### v1.18.13
- **TUI 修复**：GitHub Pull Request reviews 现在会在上下文中包含 PR 编号和 URL。
- **桌面端修复**：
  - 修复了多个标签页、抽屉、窗口缩放和标题栏交互中的 RTL（从右到左）布局问题。
  - 修复了共享的 RTL UI 行为，如方向性图标显示异常。

### v1.18.12
- **核心修复**：修复了启用 reasoning 时 Azure GPT-5.5+ 补全请求失败的问题（感谢 @frederiknsgo）。
- **桌面端修复**：
  - 减少了草稿中包含大型粘贴图片或附件时的编辑器卡顿。
  - 项目搜索现在可匹配任意已知的最近项目，而非仅限前五个。

---

## 社区热点 Issues（Top 10）

1. **#16017 [FEATURE]: 添加 Go 计划用量/余额 API 端点** 👍126 · 评论 29
   用户希望公开 Go 订阅计划的用量数据 API，目前仅仪表盘可见。高点赞数表明用户对用量透明化和自动化监控有强烈需求。
   https://github.com/anomalyco/opencode/issues/16017

2. **#39845 DeepSeek V4 Flash 突然要求开启"启用中国托管模型"选项** 评论 15
   用户会话中途突然被要求对中国区托管模型进行 opt-in，严重影响工作流。怀疑与 OpenCode Go 的区域路由策略调整有关。
   https://github.com/anomalyco/opencode/issues/39845

3. **#40471 OpenCode Agents 不回复（已关闭）** 评论 13
   多个用户报告 Agent 卡在"思考中"且无任何响应输出。此问题已关闭，但同批报告较多。
   https://github.com/anomalyco/opencode/issues/40471

4. **#40480 [BUG] OpenCode Go deepseek-v4-flash 返回 HTTP 500，而 mimo-v2.5 正常** 评论 8
   用户对比确认：同一 API Key、同一网络下，`mimo-v2.5` 返回 200，`deepseek-v4-flash` 返回 500，指向服务端问题而非客户端配置。
   https://github.com/anomalyco/opencode/issues/40480

5. **#40483 Bug: Windows 11 桌面端 DeepSeek v4 Flash Free (New) 返回空白响应** 评论 7
   界面显示"思考中"动画并播放完成音效，但响应区域完全空白。UI 看似卡死，影响 Windows 桌面端用户体验。
   https://github.com/anomalyco/opencode/issues/40483

6. **#40475 响应问题（已关闭）** 评论 6
   附截图证明模型不响应、卡在思考状态。用户尝试切换多个模型均无效。
   https://github.com/anomalyco/opencode/issues/40475

7. **#40409 OpenCode Go `deepseek-v4-flash` 服务并非实际提供 DeepSeek V4 Flash 0731（返回 V3.2，知识截止日期 2025-05）** 评论 5
   用户发现计费/质量不匹配：模型声称是最新版本，实际返回旧版本，涉及账单与体验的双重问题，严重性为 High。
   https://github.com/anomalyco/opencode/issues/40409

8. **#38723 `opencode run` 间歇性挂起——约 56% 失败率** 评论 4
   初始化阶段无任何输出、无错误、进程存活，仅能通过外部超时终止。间歇性问题排查难度大，影响自动化场景。
   https://github.com/anomalyco/opencode/issues/38723

9. **#40171 [BUG] Go 服务 /v1/responses 返回 HTTP 200 但 SSE 事件流不完整** 评论 3
   流式响应缺少 `response.output_item.added` 和 `response.content_part.added` 事件，导致 Codex 风格客户端无法正常工作。API 兼容性问题。
   https://github.com/anomalyco/opencode/issues/40171

10. **#40516 桌面端：provider/model/MCP 启动时加载失败** 评论 2 · 影响多个用户
    约 80% 启动时无法加载配置，且确认是 v1.18.5 至 v1.18.13 的回归问题，降级到 v1.18.4 可正常使用。
    https://github.com/anomalyco/opencode/issues/40516

---

## 重要 PR 进展（Top 10）

1. **#30472 fix(tui): 支持通过 tmux `set-clipboard on` 配置在 SSH 下复制**（开放）
   修复多个 SSH + Tmux 环境下的剪贴板问题（#25253、#19982、#36646 等），是长期困扰 Linux 用户的痛点。已开放两月，值得关注。
   https://github.com/anomalyco/opencode/pull/30472

2. **#40531 fix(opencode): 重试空的未知响应**（开放，bot 提交）
   自动检测未产出文本/推理/工具调用的空响应，并通过现有重试机制处理。直接回应了今天"空白响应"的故障，但该 PR 本身只处理客户端重试，不解决服务端根因。
   https://github.com/anomalyco/opencode/pull/40531

3. **#15771 feat(tui): 添加可配置的粘贴摘要阈值**（开放）
   新增 `paste_min_lines` 和 `paste_min_length` 实验配置，让用户控制粘贴内容摘要触发的阈值，提升大段粘贴体验。
   https://github.com/anomalyco/opencode/pull/15771

4. **#35310 fix(session): 将日期从 env block 移至用户消息**（已关闭）
   解决系统提示在午夜变化导致会话缓存失效的问题。长期维护项，已关闭清理。
   https://github.com/anomalyco/opencode/pull/35310

5. **#35245 fix(shell): 通过 scope teardown 限制 bash 工具挂起**（已关闭）
   解决 bash 工具因孙子进程继承 stdio 导致 `close` 事件永不触发而无限挂起的问题。对自动化任务稳定性至关重要。
   https://github.com/anomalyco/opencode/pull/35245

6. **#35289 fix(tui): 刷新 OSC 52 剪贴板写入，回退时传播错误**（已关闭）
   修复 Linux Wayland 下复制到剪贴板后粘贴内容为旧数据的问题。影响 Ubuntu 24.04 等 Wayland 用户。
   https://github.com/anomalyco/opencode/pull/35289

7. **#35284 fix(llm): 接受 OpenAI 兼容流中的 `reasoning` 字段**（已关闭）
   修复 `OpenAIChatDelta` schema 未声明 `reasoning` 字段导致的解析问题，确保来自 OpenAI 兼容端点的推理内容被正确识别。
   https://github.com/anomalyco/opencode/pull/35284

8. **#35259 feat(desktop): 添加关闭到系统托盘行为**（已关闭）
   关闭最后一个窗口时隐藏到托盘/Dock 而非退出，保留后台任务（如正在运行的 agent）。
   https://github.com/anomalyco/opencode/pull/35259

9. **#20491 feat(opencode): 添加 Kiro provider（AWS）**（开放）
   以插件形式集成 Kiro (AWS) 作为新 provider。社区对 AWS 生态支持有持续需求。
   https://github.com/anomalyco/opencode/pull/20491

10. **#40528 fix(app): 防止提示输入框底部溢出**（已关闭）
    修复 V2 提示提交按钮在模型选择器溢出时的可见性问题，提升窄窗口和 RTL 布局下的可用性。
    https://github.com/anomalyco/opencode/pull/40528

---

## 功能需求趋势

- **用量与计费透明化**（#16017）：用户强烈要求公开 Go 订阅的 API 用量/余额端点，用于自动化监控和成本管理。
- **RTL 与国际化**（#40446、v1.18.13 修复）：多个 RTL 相关 Issue 和修复表明阿拉伯语等 RTL 用户群体在增长，社区关注布局与交互的本地化完善。
- **桌面端体验优化**（#40510、#35259）：包括退出确认、关闭到托盘等桌面行为细节，反映出桌面应用用户对"类原生应用"体验的期望提升。
- **配置简化与 Provider 聚合**（#40506）：用户希望简化多 LLM Provider 的切换流程，OmniRoute 集成需求说明社区对统一路由层的兴趣。
- **新 Provider 支持**（#20491）：Kiro (AWS) 的 PR 显示社区在持续扩展云厂商模型的接入。

---

## 开发者关注点

- **服务稳定性是当前最大痛点**：DeepSeek V4 Flash 故障引发大量 Issue（空白响应、HTTP 500、模型版本错配、中国区限制），范围广、影响大，开发者无法正常工作。此类问题严重影响信任度。
- **"卡在思考中"是高频词汇**：多语言用户（英语、西班牙语、葡萄牙语、土耳其语）均报告此现象，说明这是普遍性问题，不是个别环境导致。
- **版本回归引发不满**：#40516 明确指出 v1.18.5 起桌面端配置加载失败，且持续至 v1.18.13 未修复，用户被迫降级。回归问题对社区信心打击大。
- **长期未解决的剪贴板/SSH 问题**：#36646 等剪贴板问题长期开放，虽有 PR #30472 在推进，但至今未合并，影响 Linux 重度用户。
- **API 兼容性受关注**：#40171 的 SSE 事件流不完整问题，关注 OpenAI Responses-API 兼容性的第三方客户端生态用户增加。

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi 社区动态日报 — 2026-08-05

> 数据来源: github.com/badlogic/pi-mono


## 今日速览

今日 Pi 社区的核心焦点集中在 **Compaction（上下文压缩）在企业级 Copilot 席位上的稳定性问题**，多条 issue 指向 421 Misdirected Request 与 baseUrl 解析丢失，且已有对应 PR 在途修复。与此同时，社区对新模型/新网关提供商（LLM Gateway、Cortecs、Grok 4.5）的支持呼声较高，RPC 协议与全屏 TUI 的键位/组件 bug 也构成了今日的次要热点。


## 社区热点 Issues

1. **[#6768] Compaction 在 Copilot Enterprise 下不可用（已关闭，19 评论）**
   - 摘要：使用 Copilot Enterprise License 进行 context 压缩时，OpenAI 路径返回 421 Misdirected Request，Anthropic 路径同样失败。
   - 重要性：企业用户的核心功能受损，且多模型路径均受影响，社区关注度最高（👍18）。
   - 链接: https://earendil-works/pi Issue #6768

2. **[#7579] Compaction 在 Copilot enterprise seats 上 421 失败：summarization 丢失已解析的 baseUrl（已关闭，4 评论）**
   - 摘要：`pi -ne` 复现，正常 turn 正常，仅 compaction 失败。Root cause 指向 `ModelRuntime.prepareRequest()` 的重写逻辑未作用于 summarization 路径。
   - 重要性：是 #6768 的直接技术根因线索，与修复 PR #7602 关联。
   - 链接: https://earendil-works/pi Issue #7579

3. **[#7413] GHE.com 企业账户 Compaction 失败 — "unknown stamp" 错误（开启中，6 评论）**
   - 摘要：`/compact` 在 GHE.com 账户上稳定复现，报错 `400 IDE authentication failed: invalid token: unknown stamp "prod-cus-01"`。
   - 重要性：独立于 #6768 的认证层问题，反映企业场景下的多故障点。
   - 链接: https://earendil-works/pi Issue #7413

4. **[#7553] Compaction 需要可配置的 thinking level/model（开启中，6 评论）**
   - 摘要：当前 compaction 无条件复用会话的 thinking level，用户无法为 summarization 单独设定思考预算。
   - 重要性：直接催生了 PR #7602，是今日最明确的功能需求到实现的闭环。
   - 链接: https://earendil-works/pi Issue #7553

5. **[#7508] Copilot/Codex OAuth 刷新无请求超时，卡死会话约 5 分钟（已关闭，5 评论）**
   - 摘要：token 刷新在 credential-store 锁内无超时，网络抖动可导致整个会话冻结。
   - 重要性：高频稳定性痛点，直指基础认证链路的健壮性缺失。
   - 链接: https://earendil-works/pi Issue #7508

6. **[#7547] Windows 用户使用 Pi 的情况与问题征集（开启中，11 评论）**
   - 摘要：维护者主动发起 Windows 生态盘点，收集运行方式与痛点以确定投入优先级。
   - 重要性：官方对 Windows 支持的重视信号，社区反馈活跃。
   - 链接: https://earendil-works/pi Issue #7547

7. **[#7465] iTerm2 内联图片需携带 size 参数（开启中，7 评论）**
   - 摘要：`encodeITerm2()` 缺少 `size=<decoded byte count>`，导致 xterm.js image addon 静默拒绝渲染。
   - 重要性：直接阻碍 xterm.js 终端用户查看图片输出，已有对应 PR #7612。
   - 链接: https://earendil-works/pi Issue #7465

8. **[#7574] 全屏模式下 Home/End/PageUp/PageDown 被 transcript 视口吞掉（已关闭，4 评论）**
   - 摘要：编辑器聚焦时这些按键仍被视口消费，`tui.editor.cursorLineStart` 等绑定永不触发。
   - 重要性：全屏模式基础编辑体验缺陷，影响日常重度用户。
   - 链接: https://earendil-works/pi Issue #7574

9. **[#7628] 0.83.0 shrinkwrap 固定了有漏洞的 undici 与 brace-expansion（已关闭，1 评论）**
   - 摘要：`npm-shrinkwrap.json` 固定 `undici@8.5.0`（首个修复版 8.9.0）与 `brace-expansion@5.0.7`（修复版 5.0.8/5.0.9）。
   - 重要性：安全审计告警，供应链风险需及时处理。
   - 链接: https://earendil-works/pi Issue #7628

10. **[#5023] 终端无故滚动到开头（已关闭，11 评论）**
    - 摘要：模型输出过程中终端随机跳转到会话开头并快速滚动到底部，无用户交互触发。
    - 重要性：长期存在且复现频繁的诡异 TUI 行为，虽已关闭仍是用户体感痛点。
    - 链接: https://earendil-works/pi Issue #5023


## 重要 PR 进展

1. **[#7602] 可配置的 summarization 模型（开启中）**
   - 内容：为 compaction 与 branch summaries 增加独立模型与 thinking level 配置，并处理上下文窗口限制错误。直接关闭 #7553。
   - 链接: https://earendil-works/pi PR #7602

2. **[#7624] 渲染 Mermaid 图表（开启中）**
   - 内容：在 markdown 中渲染 mermaid 图，关闭 #7623。引入新渲染依赖。
   - 链接: https://earendil-works/pi PR #7624

3. **[#7610] 新增 LLM Gateway 与 LLM Gateway DevPass 提供商（开启中）**
   - 内容：以 `openai-completions` 协议内置 OpenRouter 风格路由，替换被误关的 #7480。
   - 链接: https://earendil-works/pi PR #7610

4. **[#7571] 内置 Cortecs 欧洲 AI 提供商（已关闭）**
   - 内容：新增欧洲 provider/router（类似 OpenRouter），基于 models.dev 自动支持。
   - 链接: https://earendil-works/pi PR #7571

5. **[#7612] 为 iTerm2 OSC 1337 增加 size 参数（开启中）**
   - 内容：补充 `size=<decoded byte count>`，满足 xterm.js image addon 0.9.0 的校验。
   - 链接: https://earendil-works/pi PR #7612

6. **[#7619] 在 /tree 中选中失败 turn 可重试（开启中）**
   - 内容：选中因断连等错误结束的 assistant 条目可直接重试，保留错误历史并续写新回复。关闭 #7609。
   - 链接: https://earendil-works/pi PR #7619

7. **[#7621] RPC 暴露参数补全 get_argument_completions（已关闭）**
   - 内容：新增 RPC 命令，供嵌入式客户端（如 web UI）获取斜杠命令的子命令/参数补全。
   - 链接: https://earendil-works/pi PR #7621

8. **[#7597] 全屏模式下扩展选择器 diff 可滚动（开启中）**
   - 内容：diff 标题放入 ScrollView，固定 yes/no 操作，增加 `tui.select.scrollUp/Down` 键位。
   - 链接: https://earendil-works/pi PR #7597

9. **[#7604] 非严格 Anthropic tool schema 保留 $defs（已关闭）**
   - 内容：修复非严格 `input_schema` 重建时丢弃 `$defs` 导致的悬空 `$ref` 问题。
   - 链接: https://earendil-works/pi PR #7604

10. **[#7605] OAuth 错误信息不再包含响应体（已关闭）**
    - 内容：防止 token 响应体（含 access/refresh token）泄漏进日志、遥测与用户对话框。
    - 链接: https://earendil-works/pi PR #7605


## 功能需求趋势

- **企业级 Copilot 支持完善**：Compaction 在企业/GHE 账户下的认证与 baseUrl 处理是当前最大痛点，社区期待针对性修复与配置项。
- **可配置的上下文压缩策略**：用户希望独立控制 summarization 的模型与 thinking level，而非强制复用当前会话设置。
- **新模型与新网关接入**：Grok 4.5 模型在 Copilot Business 下的缺失、LLM Gateway/Cortecs 等路由器的内置支持，反映社区对多模型生态的持续追求。
- **TUI 全屏模式体验打磨**：键位冲突、组件裁剪、滚动缺失等问题集中涌现，表明全屏模式用户基数在增长并开始提出精细化需求。
- **RPC 协议能力开放**：参数补全、provider 认证、socket 监听等 RPC 扩展，为嵌入式/web 客户端铺路。


## 开发者关注点

- **Compaction 稳定性**：多条 issue 直指 enterprise/GHE 账户下 compaction 的 421 与认证错误，且正常对话不受影响，定位与修复优先级高。
- **OAuth 刷新与安全**：无超时的刷新流程可冻结会话 5 分钟；同时 token 泄漏风险促使 PR #7605 快速合入，供应链漏洞（undici）亦被迅速标记。
- **Windows 支持短板**：`find` 工具路径模式失效、技能加载 `RangeError`、终端滚动异常等，均需在 Windows 环境下针对性修复。
- **非严格 schema 兼容性**：开发者多次遇到 `unknown role: developer`（Deepseek）与 tool schema `$defs` 丢失问题，提示协议适配需更宽容。
- **扩展生态基础缺失**：`node:sqlite` 未随发布二进制打包、扩展加载失败等，影响第三方扩展的可靠性。

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 — 2026-08-05

## 今日速览

今日最受关注的是 #8102「确定性工具执行边界」提案，社区围绕可信 Agent 运行时的讨论持续升温（17 条评论），直指 Qwen Code 从「编码助手」转向「自主 Agent」过程中的核心信任问题。与此同时，桌面端 Electron 向 Tauri 迁移的更新桥正式落地（v0.21.5），以及 `--resume` 可复现已修复的「悬挂未签名思考」安全缺陷（#8535）成为今日焦点。值得注意的趋势是，同一作者 ryan-mt 连续提交了 5 个 cancel 语义相关的 bug 报告，揭示出「中断/取消」路径的系统性问题。

**版本发布**

- [v0.21.5](https://github.com/QwenLM/qwen-code/releases/tag/v0.21.5) — 为 macOS 用户引入 opt-in 的一次性更新桥，帮助从 Electron 桌面应用平滑迁移至新的 Tauri shell（[#8392](https://github.com/QwenLM/qwen-code/pull/8392)）


## 社区热点 Issues

### 1. [#8102 确定性工具执行边界](https://github.com/QwenLM/qwen-code/issues/8102) — 17 条评论
**标签**: `P3` `feature-request` `core/security` `need-discussion`
提议将 LLM 置于信任边界之外，让运行时能够**确定性**地约束、授权、观察和评估模型产生的工具调用。这是关于 Agent 运行时信任模型最深入的讨论线程，评论量远超其他 issue，值得细读。

### 2. [#8519 tmux 中严重闪屏](https://github.com/QwenLM/qwen-code/issues/8519) — 11 条评论
**标签**: `P2` `bug` `ui/linux/interactive`
用户报告在 tmux 中几乎每秒闪屏一两次，严重影响交互体验。CLOSED 状态但评论活跃，Linux 终端用户基数大，反馈热度高。

### 3. [#8051 多工作区守护进程资源使用追踪](https://github.com/QwenLM/qwen-code/issues/8051) — 9 条评论
**标签**: `P2` `feature-request` `core/performance` `daemon`
当前 `qwen serve` 多工作区守护进程仅限制工作区和会话数量，但未对请求体、WebSocket 组装等占用的**字节数**设限，存在内存失控风险。服务端稳定性方向的代表性提案。

### 4. [#8136 Provider 警告清理器泄露密码](https://github.com/QwenLM/qwen-code/issues/8136) — 6 条评论
**标签**: `P2` `bug` `security/cli`
`sanitizeProviderWarning` 在处理含端口或密码含 `@` 的 URL 时存在截断过短和凭据泄露双重 bug，直接影响 `/status` 负载中的敏感信息保护。

### 5. [#8356 APIUserAbortError 后会话记录中断](https://github.com/QwenLM/qwen-code/issues/8356) — 5 条评论
**标签**: `P2` `bug` `core/session-management`
用户中止（abort）后，后续轮次不再写入本地会话转录文件。影响会话连续性和审计能力，与 ryan-mt 提交的一组 cancel 语义 bug 相互印证。

### 6. [#8493 已取消的文件工具仍可修改文件](https://github.com/QwenLM/qwen-code/issues/8493) — 5 条评论
**标签**: `P2` `bug` `core/file-operations`
`write_file` 和 `edit` 在异步准备阶段收到 abort 信号后，仍会继续执行文件系统写入。取消 ≠ 停止执行，这是 Agent 安全性的硬伤。

### 7. [#8533 Content[]/Part[] 无法编码按提供商区分的推理回放契约](https://github.com/QwenLM/qwen-code/issues/8533) — 4 条评论
**标签**: `P2` `enhancement` `core/content-generation` `need-discussion`
作者 `netbrah` 以 RFC 风格提出：当前内容模型无法安全表达不同提供商（如 Anthropic vs OpenAI）的推理（reasoning）回放契约，是 `--resume` 系列问题的根源。

### 8. [#8544 JetBrains 中 ACP 任务列表不渲染](https://github.com/QwenLM/qwen-code/issues/8544) — 3 条评论
**标签**: `P2` `bug` `integration/ide-acp`
Qwen Code 通过 ACP 接入 JetBrains AI Assistant 时，任务列表（todo/plan）从不显示，而 Claude Code 和 Codex 在相同界面下正常。IDE 集成完整度差距的直接用户反馈。

### 9. [#8535 --resume 可复现已修复的悬挂未签名思考缺陷](https://github.com/QwenLM/qwen-code/issues/8535) — 3 条评论
**标签**: `P2` `bug` `core/content-generation` `need-discussion`
PR #8260 修复的「未签名尾部思考紧邻 tool_use」安全缺陷，可通过 `--resume`/`--continue` **重新构造**——因为修复只处理了实时会话路径，未覆盖会话恢复路径。安全修复不彻底的典型。

### 10. [#8452 微压缩反复使提示缓存失效](https://github.com/QwenLM/qwen-code/issues/8452) — 3 条评论
**标签**: `P2` `bug` `performance/caching`
大小触发的微压缩会在连续 ToolResult 轮次中**反复重写**已缓存的对话前缀，导致提供方提示缓存（prompt cache）持续失效，token 成本飙升。长会话成本问题的代表性反馈。


## 重要 PR 进展

### 1. [#8396 修复 Hook 执行的四个信任边界漏洞](https://github.com/QwenLM/qwen-code/pull/8396) — `autofix/takeover`
HTTP hooks 不再跟随重定向（绕过 URL 白名单与 DNS 级 SSRF 检查的经典路径）；同时修复另外三个仓库配置触及代码执行或网络出口的信任边界漏洞。安全加固类合入。

### 2. [#8388 review capture-tui：终端渲染证据截图（Phase 2）](https://github.com/QwenLM/qwen-code/pull/8388) — `autofix/takeover`
新增 `qwen review capture-tui` 子命令，可在**私有 tmux 服务器**中运行被审查代码并精确捕获终端渲染输出，让「面板在 80 列处被截断」这类渲染缺陷具备可验证的像素级证据。代码审查基础设施的持续投入。

### 3. [#8496 Web Shell 流式响应中立即执行只读信息命令](https://github.com/QwenLM/qwen-code/pull/8496) — `autofix/takeover`
`/stats`、`/about`、`/context` 等只读命令在 turn 流式输出过程中可直接运行，不再被静默吞掉。交互体验打磨。

### 4. [#8482 未投递的 MCP 调用应视为首次投递而非重放](https://github.com/QwenLM/qwen-code/pull/8482) — `autofix/takeover`
修复自 #8387 重放安全门合入后一直红的主线测试：服务器已知断开时，从未真正投递的 MCP 调用应走重连而非被误判为重放。测试确定性修复。

### 5. [#8455 退出时将恢复命令回显到主屏幕](https://github.com/QwenLM/qwen-code/pull/8455) — `autofix/takeover`
VP（Virtual Viewport）模式下「恢复此会话」的提示绘制在退出时会被丢弃的备用缓冲区中，用户永远看不到。此 PR 在退出时将恢复命令回显至主屏幕。小改动解决实际可用性问题。

### 6. [#8439 VP 模式恢复 Ctrl+点击超链接和右键菜单](https://github.com/QwenLM/qwen-code/pull/8439) — `autofix/takeover`
启用 SGR 鼠标追踪后，终端原生的「点击超链接打开」「右键弹出上下文菜单」两项能力被静默破坏，此 PR 恢复并保持状态跟踪。终端交互细节修复。

### 7. [#8471 从磁盘已有记录构建成本账本](https://github.com/QwenLM/qwen-code/pull/8471) — `autofix/takeover`
「0.21.3 没问题，0.21.4 变慢」的排查需要重放完整 review 并手工聚合遥测输出，耗时数小时。此 PR 让每次 review 自动产出成本账本（模型调用数/输入 token 等），性能排查从「考古」变为「读报表」。

### 8. [#8445 Web Shell 会话刷新支持守护进程认证](https://github.com/QwenLM/qwen-code/pull/8445) — `autofix/takeover`
允许精确的 Web Shell 会话文档导航在 bearer 认证前加载公共 HTML 壳，同时保持非文档请求和 API 子路径在认证门后。认证流程的精确化调整。

### 9. [#8318 Autofix 要求隔离的目标化 E2E 证明](https://github.com/QwenLM/qwen-code/pull/8318) — `autofix/takeover`
为「post-merge E2E 失败」创建的 Autofix issue 增加 fail-closed 验证链：将不可变失败元数据置于可编辑 issue 正文之外，将维护者批准绑定到精确的 issue 标题和正文。自动化修复的信任基础设施。

### 10. [#8490 测试 diff 的反向依赖闭包，失败时放开为全量测试](https://github.com/QwenLM/qwen-code/pull/8490) — `autofix/takeover`
Agent 7 的 `build-test` 是每次 review 的墙上时钟关键路径（小 PR 也要 13–16 分钟）。此 PR 将测试集限定到 diff 的反向依赖闭包，失败时自动放开为全量套件——墙钟时间与测试覆盖的权衡。

> **注**：全部 10 个 PR 当前均为 OPEN 状态且标记 `autofix/takeover`，多为自动化流程驱动的持续迭代，尚无人工合入确认。


## 功能需求趋势

1. **确定性工具执行与信任边界**（#8102）— 社区开始从「模型能力」转向「运行时可信度」的讨论，要求对工具调用做确定性约束、授权和审计。这是 Agent 走向生产环境的必答题。
2. **IDE/ACP 集成完整度**（#8544、#8513、#8514）— JetBrains 生态内任务列表、上下文用量显示、推理强度配置（5 档）均落后于 Codex/Claude Code。IDE 集成方向需求密集。
3. **会话管理韧性**（#8356、#8535、#8495）— 中断、恢复、重放路径的语义一致性成为高频话题，尤其是 `--resume` 引入的安全语义回退。
4. **资源使用可观测性与成本控制**（#8051、#8452、#8471）— 守护进程内存、提示缓存失效、review 成本账本，社区开始要求「资源可计量、成本可追踪」。
5. **扩展系统 hooks 兼容性**（#8539）— 支持 Claude 扩展格式但不执行扩展内置 hooks，说明社区已有 Claude Code 迁移用户，对生态兼容有明确预期。


## 开发者关注点

- **取消（cancel/abort）≠ 停止执行**：ryan-mt 连续提交 5 个相关 bug（#8491、#8493、#8494、#8495、#8492），覆盖文件写入、shell 命令、流式控制和 MCP 元数据热加载。取消路径的系统性缺陷已成为当前最集中的 bug 类别。
- **安全修复不彻底**：#8535 表明已合入的安全修复（#8260）只覆盖了实时路径，`--resume` 可绕过；#8396 一次性合入 4 个信任边界修复，说明 hook 系统安全面仍在持续收敛。反馈者期望安全修复覆盖所有入口路径，而非单点修补。
- **长会话成本失控**：#8452（微压缩反复使提示缓存失效）和 #8463（超出阈值后每轮重写历史）指向同一根因：大小触发的压缩逻辑在长会话中进入滚动重写稳态，直接推高 token 成本。社区对「省钱」的诉求非常具体。
- **Desktop 迁移阵痛**：macOS 用户从 Electron 迁向 Tauri 的桥已就位（v0.21.5），但迁移后的桌面端仍有 #8538「复制响应按钮无效」等遗留问题，迁移体验需持续打磨。
- **终端体验细节**：tmux 闪屏（#8519）、VP 模式超链接/右键恢复（#8439）、恢复会话提示不可见（#8455）——终端 UI 细节的反馈密度说明 CLI 仍是核心使用场景，交互细节决定留存。

---
*本日报基于 QwenLM/qwen-code GitHub 仓库公开数据自动生成。*

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI 社区动态日报 — 2026-08-05

> 数据来源: [github.com/Hmbown/DeepSeek-TUI](https://github.com/Hmbown/DeepSeek-TUI)（CodeWhale）


## 今日速览

今日社区聚焦"性能优化"与"发布流程整顿"：维护者 Hmbown 连续提交 5 个 build 性能优化 Epic Issue，直指 TUI 巨型 crate（68 万行、620 文件）拖累 edit/commit/test 全流程的痛点；同时 v0.9.4 发布列车（#5135，77 commits）持续推进，多个 Runtime API 功能 PR 密集涌入。此外，模型上下文窗口静默降级（#5239/#5244）和 OAuth 登录流程缺陷（#5243）成为用户侧最尖锐的体验问题。


## 社区热点 Issues

挑选 10 个值得关注的 Issue，涵盖 bug、性能与体验问题。

- **[#4978]** [bug] Anthropic API 频繁报错 `'type' must be in ["enabled", "disabled", "auto"]` — 使用 OpenModel 兼容端点时高频出现，重试后偶发通过，无固定规律。6 条评论，社区有同类遭遇但尚未定位根因。[链接](https://github.com/Hmbown/CodeWhale/issues/4978)

- **[#5209]** [bug] File 工具 `action=edit` 静默接受错误参数名（如 `new_str`），返回伪造的"替换成功"，导致同一处需 3-5 次重复编辑。参数校验缺失，极易误导 Agent 与用户。[链接](https://github.com/Hmbown/CodeWhale/issues/5209)

- **[#5241]** [bug] 升级 0.8.67 → 0.9.3 后定价端点 503，所有会话显示 `unverified_live_pricing`，成本显示完全失效，涉及全部 provider。[链接](https://github.com/Hmbown/CodeWhale/issues/5241)

- **[#5239]** [bug/question] 模型支持 1M 上下文，但工具仅在 128K 触发压缩。用户质疑"为什么不能设置为 1M"，直指默认值保守且无提示。[链接](https://github.com/Hmbown/CodeWhale/issues/5239)

- **[#5244]** [enhancement] 未知模型 ID 静默降级到 128K 传统上下文窗口，无任何 fallback 提示。系 #5239 背后的遗留类 bug，0.9.4 已有部分缓解但仍需完整修复。[链接](https://github.com/Hmbown/CodeWhale/issues/5244)

- **[#5249]** [Epic] build-time lane：终止 monolith 税 — 提出将 68 万行 TUI crate 拆分或优化编译单元，改善 edit-compile、commit、test、release 全链路时延。0 评论但为维护者亲自提交，方向性极强。[链接](https://github.com/Hmbown/CodeWhale/issues/5249)

- **[#5248]** [Epic] 依赖裁剪：将 708 个包的构建图缩减 — 95 个 build-script、52 个 proc-macro，至少 10 个依赖存在多版本并存，`codewhale-tui` 携带冗余栈。[链接](https://github.com/Hmbown/CodeWhale/issues/5248)

- **[#5245]** [Epic] 本地 git commit 强制全量重建 TUI + CLI — build script 监控 git ref 导致 SHA 更新即全量重编，成本与收益倒挂。[链接](https://github.com/Hmbown/CodeWhale/issues/5245)

- **[#5246]** [Epic] 拆分 shipping profile 与本地 release gate — `lto = true` fat LTO + `codegen-units = 1` 使每次预推送构建都付出完整发布级优化代价。[链接](https://github.com/Hmbown/CodeWhale/issues/5246)

- **[#5243]** [enhancement] OAuth 登录成功后未自动采用新铸造的 token — 需二次回到 provider 选择器手动按 `e` 才能生效（xAI + ChatGPT/Codex），dogfood 当日即暴露。[链接](https://github.com/Hmbown/CodeWhale/issues/5243)


## 重要 PR 进展

筛选 10 个功能/修复类 PR，覆盖运行时 API、ACP、MCP 与发布列车。

- **[#5135]** release: v0.9.4 release train — 77 commits ahead of main，包含 18 个列车提交与 2026-08-01 源码候选，为当前最核心的集成分支。[链接](https://github.com/Hmbown/CodeWhale/pull/5135)

- **[#5242]** feat(tui/subagent): 从 checkpoint 恢复中断的子 Agent — `followup` 之前对 `interrupted_continuable` 子任务只能投递死信，现在可真正续跑长任务（文档审查、多步搜索）。[链接](https://github.com/Hmbown/CodeWhale/pull/5242)

- **[#5225]** feat(acp): 通过 session/prompt 暴露 file/search/git/patch/shell 工具 — ACP 服务器此前只流式返回文本，不执行工具调用；此 PR 使 Zed 等编辑器驱动的 Agent 具备真实代码编辑能力。[链接](https://github.com/Hmbown/CodeWhale/pull/5225)

- **[#5133]** feat(runtime-api): 暴露持久 goal-loop 状态与完成控制 — 新增 `GET /v1/threads/{id}/goal` 等端点，使托管客户端可读取活跃目标状态并驱动生命周期转换。[链接](https://github.com/Hmbown/CodeWhale/pull/5133)

- **[#5132]** Runtime API: 暴露 verifier 收据与证据 — 此前只有失败计数器，现新增 `GET /v1/fleet/runs/{run_id}/receipts` 等端点，可定位失败任务与原因。[链接](https://github.com/Hmbown/CodeWhale/pull/5132)

- **[#5130]** feat(runtime-api): MCP server 生命周期管理 — 此前只读库存，现支持 `POST /v1/apps/mcp/servers` 创建、更新与删除，免去手改 TOML/JSON。[链接](https://github.com/Hmbown/CodeWhale/pull/5130)

- **[#5129]** feat(runtime-api): skill 生命周期端点 — install/update/uninstall/trust/audit 全套 HTTP 接口，补全 TUI 之外的托管客户端能力。[链接](https://github.com/Hmbown/CodeWhale/pull/5129)

- **[#5240]** feat(tui/shell): 在工具内容中展示真实等待耗时 — `duration_ms` 原只在元数据中，模型不可见；现在 wait 结果可直接感知任务进程，避免盲目轮询。[链接](https://github.com/Hmbown/CodeWhale/pull/5240)

- **[#5238]** feat(mcp): MCP Registry 发现 + Registry-first 工具选择 — 模型在调用 `exec_shell` 前先咨询公共 MCP Registry 寻找匹配的零环境 stdio server，减少自定义实现。[链接](https://github.com/Hmbown/CodeWhale/pull/5238)

- **[#5234]** fix(tui): 鼠标捕获期间保持 alternate scroll 关闭 — 修复滚轮不滚动对话、反而切换输入历史的回归（#5223 的修复）。[链接](https://github.com/Hmbown/CodeWhale/pull/5234)


## 功能需求趋势

从今日 Issues 与 PR 提炼社区最关注的方向：

- **构建性能与编译时延**：今日最大热点。5 个 Epic Issue（#5249、#5248、#5245、#5246、#5247）全部由维护者发起，直指 TUI crate 单块编译、依赖图臃肿（708 包）、git commit 触发全量重建、fat LTO 过重、25 个集成测试二进制链接耗时。趋势明确：拆分 crate、精简依赖、优化 profile 分层。
- **Runtime HTTP API 补齐**：4 个 PR（#5133、#5132、#5130、#5129）清一色由 Copilot 编写，覆盖 goal、verifier、MCP、skill 四类资源的管理端点，说明托管客户端（桌面/Web）对编程式控制的需求在加速落地。
- **ACP 工具执行能力**：PR #5225 让 ACP 从"聊天-only"走向"可执行工具"，编辑器/桥接类集成（如 Zed）是直接受益方。
- **上下文窗口透明化**：#5239 + #5244 组合拳，用户强烈要求"支持 1M 就真的用 1M"，未知模型 ID 不得静默降级。
- **Agent 恢复与续跑**：#5242 使中断的子 Agent 可从 checkpoint 恢复，属于多步骤长任务场景的刚需。

### 开发者关注点

- **参数校验缺失**（#5209）：File 工具静默接受错误参数名并返回成功，是典型"假成功真返工"问题，Agent 自动化场景下危害放大。
- **成本可见性受损**（#5241）：升级即丢失定价能力，跨 provider 全挂，直接影响用户对费用的掌控。
- **登录流程割裂**（#5243）：OAuth 铸造 token 后不自动采用，需手动二次操作，dogfood 当天即踩坑。
- **上下文默认值保守**（#5239/#5244）：128K 触发压缩对 1M 窗口模型是明显瓶颈，且无任何提示告知用户"这是 fallback"。
- **编译等待成为日常痛点**（#4991、#5249 等）：开发者已公开讨论"等待编译的时间"，维护者用 Epic Issue 系统性回应，社区共识是 monolith crate 已到拆分临界点。

---

以上为 2026-08-05 DeepSeek TUI 社区动态日报，信息来源均为 GitHub 公开数据。

</details>

---
*本日报由 [agents-radar](https://github.com/kky-wollu/agents-radar) 自动生成。*
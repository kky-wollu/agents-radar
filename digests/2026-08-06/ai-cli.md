# AI CLI 工具社区动态日报 2026-08-06

> 生成时间: 2026-08-05 23:05 UTC | 覆盖工具: 9 个

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

**日期：2026-08-06**


## 1. 生态全景

AI CLI 工具已从"聊天增强终端"全面进化为**核心开发工作流基础设施**，七大主流工具（Claude Code、Codex、Gemini CLI、Copilot CLI、Kimi Code、OpenCode、Qwen Code、Pi、DeepSeek TUI）均在今日呈现出密集的 Issue 反馈与 PR 合并节奏。社区讨论焦点已从"模型能力对比"转向**稳定性、安全性、成本控制与生态集成**——多工具同时出现子代理失控烧配额（Claude Code #69332、Gemini #22323）、安全过滤误伤（Codex #37161、Qwen #8582）、终端渲染兼容性（Claude #80131、Qwen #8580、Copilot #1799）等同类问题，表明行业正集体穿越"功能完备→生产可靠"的关键阶段。同时，MCP 生态兼容性、跨平台支持（尤其 Windows/WSL）、会话持久化与记忆系统成为全行业的共同攻坚方向。


## 2. 各工具活跃度对比

| 工具 | 今日活跃 Issues | 重要 PR 进展 | 版本发布 | 社区热度信号 |
|------|:---:|:---:|:---:|------|
| **Claude Code** | 10（2 新增） | 8（7 合并/1 新增） | 无 | 🔥 高；遗留 Issue 批量关闭，Cowork 兼容性讨论热 |
| **OpenAI Codex** | 10（2 新增） | 10 | **rust-v0.146.1** + 4 个 alpha | 🔥 极高；Windows 问题密集，多模型兼容性关注（30👍） |
| **Gemini CLI** | 10 | 10（7 合并/3 开放） | 无 | 🔥 高；P1 级子代理可靠性问题集中，SDK 修复节奏快 |
| **Copilot CLI** | 10（5 新增） | 0 | **v1.0.79-2/3/4**（预发布） | ⚠️ 中高；MCP 兼容性问题单日新增 4 个，v1.0.73 回归 Bug 未修复 |
| **Kimi Code** | 4（4 新增） | 2（均开放） | 无 | ⚠️ 中；社区体量较小但问题质量高（500K token 退化分析） |
| **OpenCode** | 10 | 10 | **v1.18.14** | 🔥 高；VS Code 扩展 134👍 居首，Intel Mac AVX2 崩溃持续发酵 |
| **Pi** | 10（含已关闭） | 10（9 合并/1 开放） | 无 | ⚠️ 中高；修复效率高（OSC 8、AGENTS.override.md 当日合并） |
| **Qwen Code** | 10（含已关闭） | 10（含已合并） | **v0.21.6** + preview + nightly + desktop-v0.1.0 | ⚠️ 中高；安全漏洞与 CI 稳定性是焦点，桌面端初版上线 |
| **DeepSeek TUI** | 4（2 新增） | 10（7 项 Runtime API 并行） | 无（v0.9.4 发布列车积蓄中） | ⚠️ 中；从 TUI 向可编程 Runtime 平台转型 |


## 3. 共同关注的功能方向

### 3.1 会话持久化与记忆系统（跨 4 个工具）
- **Kimi Code** #1283：跨会话持久记忆，活跃 5 个月获 18 评论
- **Copilot CLI** #4005：企业环境记忆保存失败
- **Gemini CLI** #26522/#26525：Auto Memory 无限重试、密钥先泄露风险
- **DeepSeek TUI** #5131：通过 Runtime API 暴露内存端点

### 3.2 MCP 生态兼容性（跨 3 个工具）
- **Copilot CLI**：#4370（FastMCP -32602）、#4371（OAuth 3LO）、#4378（GHEC 数据驻留）、#4374（Azure DevOps 400）
- **Kimi Code** #2588：MCP 工具返回图像后中止运行
- **DeepSeek TUI** #5130：MCP 配置管理 API

### 3.3 成本控制与用量透明度（跨 3 个工具）
- **Claude Code**：#82506（Max 额度异常消耗）、#82101（大型工作流无警告）、#69332（子代理递归耗尽配额）
- **Copilot CLI** #4377：主模型静默委托 Opus 导致成本失控
- **Gemini CLI** #28670：容量耗尽后死循环重试

### 3.4 子代理/多 Agent 可靠性（跨 4 个工具）
- **Gemini CLI**：#22323（MAX_TURNS 误报成功）、#21409（通用代理挂起）
- **Claude Code** #69332：子代理递归自生成级联发散
- **Copilot CLI** #3013：后台代理不触发 Hooks（安全漏洞）
- **DeepSeek TUI** #5242：checkpoint 恢复中断的子代理任务

### 3.5 终端兼容性与渲染稳定性（跨 5 个工具）
- **Claude Code**：#80131（iTerm2 SIGTTIN 挂起）、#68755（滚动缓冲破坏）
- **Qwen Code**：#8580（tmux <3.5 闪烁）、#8557（窗口缩小重复输出）
- **Copilot CLI** #1799（alt-screen 争议，8👍 今日最高）
- **Pi**：#7399（OSC 8 超链接截断）、#7465（iTerm2 图片 size 参数）
- **Gemini CLI** #25166：终端卡在 "Waiting input"

### 3.6 Windows/WSL 支持（跨 3 个工具）
- **Codex**：#35119（WSL 仓库误判）、#27117（PSModulePath 哈希失败）、#33786（系统级输入卡顿）
- **Kimi Code** #2587：Windows 正常会话崩溃
- **Qwen Code** #8538：Windows 复制按钮失效


## 4. 差异化定位分析

| 工具 | 功能侧重 | 目标用户 | 技术路线 |
|------|---------|---------|---------|
| **Claude Code** | 多代理协作、插件/Hook 生态、Cowork 跨设备 | 企业级用户、复杂工作流 | 全屏 TUI（NO_FLICKER）、Hook 事件驱动、代理递归调度 |
| **OpenAI Codex** | 桌面 App + CLI 双端、多模型路由、Computer Use | 重度 IDE 用户、多模型团队 | Electron + Rust 核心、MCP 贡献上下文、会话分叉 |
| **Gemini CLI** | 子代理调度、Auto Memory、多模型（GCA 模式） | Google 生态用户、长会话分析师 | AST 感知文件操作（EPIC #22745）、零依赖沙箱提案 |
| **Copilot CLI** | GitHub 深度集成、企业策略、MCP 注册表 | GitHub 企业客户、MCP 重度用户 | 预发布快速迭代、非交互模式、SDK 探针 |
| **Kimi Code** | Agent 长时运行、扩展生态、跨平台 | Moonshot 生态开发者、长任务自动化 | 独立扩展 SDK、MCP 工具、语音 ACP |
| **OpenCode** | 多 Provider 聚合、V2 架构重构、局域网模型发现 | 自托管用户、多模型切换者 | Tauri 桌面端候选、mDNS 自动发现、加密货币支付 |
| **Pi** | 快速迭代修复、多 Provider 适配、扩展 API | 开发者工具链集成者（Neovim/JetBrains） | Bun 运行时、AGENTS.override.md 上下文分层、事件总线扩展 |
| **Qwen Code** | 全栈（VSCode/CLI/WebShell/Desktop）、中国区模型 | 中国开发者、多端协同 | Tauri 桌面统一、Live Voice、钉钉/飞书集成 |
| **DeepSeek TUI** | 沙箱安全、Runtime API、ACP 编码 Agent | Rust 开发者、编辑器集成 | Ratatui + Rust、HTTP API 完整暴露、checkpoint 恢复 |


## 5. 社区热度与成熟度

### 第一梯队（高活跃 + 高成熟度）
- **Claude Code**：社区体量最大，Issue 质量高（用户能做深度根因分析），但官方响应速度与修复节奏仍有提升空间（多个遗留 Issue 已关闭，Cowork 问题关闭但未解决）。
- **OpenAI Codex**：活跃度最高，版本迭代密集（1 个补丁 + 4 个 alpha），但 Windows 平台问题积压严重（多个 Issue 持续 2 个月未修复），多模型兼容性是新痛点。社区对 Rust 重构后的稳定性有疑虑。

### 第二梯队（高活跃 + 快速迭代）
- **Gemini CLI**：修复速度最快（当日 7 个合并），SDK 防御性增强明显；P1 级子代理可靠性问题仍待实质解决（#22323 具误导性）。
- **OpenCode**：社区热情高涨（VS Code 扩展 134👍），V2 架构迁移期带来大量 PR，但 Intel Mac AVX2 崩溃是长期技术债。
- **Pi**：合并效率最高（9/10 当日合并），"小步快跑"模式适配嵌入式场景；功能深度（OSC 8 修复）优于广度。

### 第三梯队（成长中）
- **Qwen Code**：发布频率高（4 个版本），但 desktop-v0.1.0 基础体验待打磨（语言切换、链接点击）；安全漏洞（#8582）暴露了安全分类器的盲区。
- **Copilot CLI**：预发布节奏稳定，但最近 24h 无 PR；MCP 兼容性问题呈集中爆发趋势，企业环境（GHEC 数据驻留）问题影响商业客户信任。
- **Kimi Code / DeepSeek TUI**：社区体量较小，但问题分析深度高（如 500K token 阈值测量）。DeepSeek 正借 v0.9.4 发布列车实现架构转型。


## 6. 值得关注的趋势信号

### 6.1 "安全即默认"成为硬性要求（信号强度：🔴 极强）
- **Qwen Code** #8582 只读 Shell 逃逸、**Copilot CLI** #3013 后台代理绕过 Hooks、**Gemini CLI** #28557 SSRF 漏洞、**Pi** #26525 密钥先泄露——安全边界已经从"功能特性"上升为"阻塞性问题"，且攻击面从模型提示词注入扩展到工具链架构设计（分类器绕过、代理隔离失效）。**开发者启示：采用 AI CLI 时，需审查其沙箱实现与认证机制，而非仅看模型能力。**

### 6.2 多 Agent/子代理调度是"双刃剑"（信号强度：🔴 极强）
- **Claude Code** #69332 递归扇出烧配额、**Gemini CLI** #22323 误报成功、**Copilot CLI** #4377 静默委托 Opus——所有主流工具都在多代理调度上出现可靠性或成本失控问题。**开发者启示：选择多代理工具需关注终止机制、成本预警和模型路由透明度；建议设置严格的任务隔离和配额上限。**

### 6.3 成本透明化与用户控制权（信号强度：🟠 强）
- **Claude Code** #82506（未使用即扣费）、#82101（大型工作流无警告）、**Copilot CLI** #4377（偷偷调 Opus）——用户对"看不见的消耗"容忍度趋近于零。**开发者启示：优先选择提供**细粒度成本预估、模型路由可见、用量预警阈值**的工具，并主动监控 API 账单。**

### 6.4 Windows/WSL 支持成"兵家必争之地"（信号强度：🟠 强）
- **Codex** 三个 Windows Issue 同时打开（WSL 误判、pwsh 哈希失败、系统卡顿）、**Kimi Code** Windows 崩溃、**Pi** 发起 Windows 调查——Windows 开发者基数庞大但长期被忽视。**开发者启示：Windows 用户选择工具时需提前验证 WSL/原生兼容性，关注官方对 Windows 问题的响应速度。**

### 6.5 记忆系统是"下一站"但安全未跟上（信号强度：🟡 中强）
- **Kimi Code** #1283 社区呼声高涨、**Gemini CLI** Auto Memory 在安全与可靠性上被质疑、**Copilot CLI** 企业记忆功能遇阻——跨会话记忆是刚需，但脱敏前置、低价值内容过滤、索引失败恢复等问题尚无成熟方案。**开发者启示：使用记忆功能前，审查数据脱敏策略；建议禁用"自动记忆"或定期清理记忆库。**

### 6.6 从 TUI 到 Runtime/API 平台化（信号强度：🟡 中强）
- **DeepSeek TUI** 7 项 Runtime API 并行（内存/MCP/技能/目标循环）、**Gemini CLI** SDK 防御性增强、**Copilot CLI** 非交互模式回归——AI CLI 正在从"终端玩具"进化为"可编程开发基础设施"。**开发者启示：关注工具是否提供可编程接口（HTTP API、SDK），这将决定其能否嵌入 CI/CD、构建自定义工作流。**

### 6.7 终端兼容性打磨成为"长期主义"（信号强度：🟡 中）
- 5 个工具同时在处理 tmux/iTerm2/Ghostty 的渲染兼容问题——TUI 的"最后一公里"体验标准化尚未实现。**开发者启示：在 tmux 或远程开发场景下，务必测试候选工具的渲染行为；优先选择主动适配主流终端的工具。**

### 6.8 中国模型生态独立性增强（信号强度：🟡 中）
- **Qwen Code** 完成 WebShell Live Voice 原生支持、**DeepSeek TUI** 支持 GLM 多模型切换、**OpenCode** 处理中国区模型策略问题（#39845）——国产模型工具链正在形成完整生态，且与全球生态差异化竞争。**开发者启示：同时使用国内外模型的团队，需要工具提供灵活的多 Provider 路由和区域策略适配。**

---

*本报告基于 2026-08-06 各工具 GitHub 公开数据生成，数据采集时间截至当日 24:00 UTC+8。*

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills 社区热点报告（数据截止 2026-08-06）

## 一、热门 Skills 排行

**1. skill-creator 系列修复（#1298 / #1099 / #1050 / #1323 / #1261）**
- **功能**：修复 `run_eval.py` 在 Windows 上的崩溃、触发检测失效、并行 worker 冲突等问题，解决描述优化循环中 recall=0% 的长期缺陷
- **讨论热点**：`claude -p` 从不触发 skill，导致优化循环在噪声上迭代；Windows 子进程管道读取崩溃；`w:id` 与现有书签冲突导致文档损坏
- **状态**：全部 Open。 #556（Issue）有 12 条评论、7 个 👍，说明该 bug 影响面广，社区对 skill-creator 工具链的可靠性诉求强烈
- **链接**：[#1298](https://github.com/anthropics/skills/pull/1298) | [#1099](https://github.com/anthropics/skills/pull/1099) | [#1050](https://github.com/anthropics/skills/pull/1050) | [#1323](https://github.com/anthropics/skills/pull/1323) | [#1261](https://github.com/anthropics/skills/pull/1261)

**2. 文档排版技能 document-typography（#514）**
- **功能**：防止 AI 生成文档中的孤行（1-6 个单词溢出到下一行）、寡行段落（标题孤悬页底）和编号错位
- **讨论热点**：直击 AI 生成文档的普遍痛点——用户很少主动要求好的排版，但排版问题影响所有 Claude 生成的文档
- **状态**：Open
- **链接**：[#514](https://github.com/anthropics/skills/pull/514)

**3. 自审计技能 self-audit（#1367）**
- **功能**：交付前审计 AI 输出——先做机械性文件验证（每个声称输出的文件必须存在），再按损害严重度排序进行四维推理审计。通用性强，适用于任何项目、技术栈和模型
- **讨论热点**：与 #1385 Issue（三闸门推理质量管道）互相呼应，社区对「输出质量门禁」类技能兴趣浓厚
- **状态**：Open，更新至 2026-07-02，仍活跃
- **链接**：[#1367](https://github.com/anthropics/skills/pull/1367)

**4. 色彩专家技能 color-expert（#1302）**
- **功能**：涵盖色彩命名系统（ISCC-NBS、Munsell、XKCD、RAL、Ridgway 1912）、色彩空间选择表（OKLCH 用于色阶、OKLAB 用于渐变、CAM16 等）、无障碍对比度、品牌色系统等
- **讨论热点**：自包含的完整色彩知识库，适合设计类工作流，讨论集中在「何时用哪个色彩空间」的实用决策表
- **状态**：Open，更新至 2026-07-21，仍在活跃讨论
- **链接**：[#1302](https://github.com/anthropics/skills/pull/1302)

**5. 测试模式技能 testing-patterns（#723）**
- **功能**：覆盖完整测试栈——测试哲学（Testing Trophy 模型）、单元测试（AAA 模式、测试命名、纯函数、边界情况）、React 组件测试（Testing Library）、端到端测试
- **讨论热点**：社区对「什么该测 vs 什么不该测」的哲学探讨，以及具体的模式落地
- **状态**：Open
- **链接**：[#723](https://github.com/anthropics/skills/pull/723)

**6. 复古游戏开发技能 pyxel（#525）**
- **功能**：为 pyxel-mcp（Pyxel 复古游戏引擎的 MCP 服务器）编写技能，触发条件是用户想用 Python 创建复古/像素风/8-bit 游戏，覆盖「写 → 运行捕获 → 检查 → 迭代」的完整工作流
- **讨论热点**：MCP + Skill 组合范式，作者是 Pyxel 引擎原作者 kitao，社区关注度持续（更新至 2026-07-15）
- **状态**：Open
- **链接**：[#525](https://github.com/anthropics/skills/pull/525)

**7. ODT 文档技能（#486）**
- **功能**：创建、填充、读取和转换 OpenDocument 格式（.odt、.ods），触发器包括任何关于 ODT/ODS/ODF/OpenDocument/LibreOffice 的提及，或产生开源/ISO 标准格式文档的请求
- **讨论热点**：与 #538（PDF 大小写敏感文件引用修复）同属文档处理增强，社区对开源格式的完整支持有持续需求
- **状态**：Open
- **链接**：[#486](https://github.com/anthropics/skills/pull/486)

**8. 计划文件卫生技能 plan-file-hygiene（#1479）**
- **功能**：解决规划工件无生命周期管理的问题（#1417）——规划文件堆积，没有清理机制
- **讨论热点**：多人协作提出，明确引用社区成员命名问题，体现「规划工件生命周期」是一个被多方感知的痛点
- **状态**：Open，更新至 2026-07-27
- **链接**：[#1479](https://github.com/anthropics/skills/pull/1479)


## 二、社区需求趋势

**1. 信任与安全边界**（#492，43 条评论）
- 社区技能在 `anthropic/` 命名空间下分发，伪装成官方技能，形成信任边界漏洞。用户可能将权限授予认为是官方的社区技能。这是当前评论数最高的 Issue，说明安全信任是社区最大焦虑。→ **诉求：官方命名空间治理 + 技能来源验证机制**

**2. 组织级技能共享**（#228，16 条评论，8 👍）
- 技能应能在组织内直接共享，而非手动下载 .skill 文件、通过 Slack/Teams 发送、再手动上传到 Settings > Capabilities。→ **诉求：共享技能库或直接共享链接**

**3. 工具链可靠性**（#556，#1169）
- `run_eval.py` 从不触发技能，导致所有评估循环都得到 recall=0% 并针对噪声优化。这直接催生了 5 个相关 PR，说明社区对 skill 开发工具链的稳定性有强烈不满。→ **诉求：skill-creator 工具链的稳定性与跨平台兼容性**

**4. 技能去重**（#189，6 条评论，9 👍）
- installing 两个插件（document-skills 和 example-skills）安装相同内容，导致上下文窗口重复加载。→ **诉求：插件依赖治理和内容去重**

**5. 上下文窗口安全**（#1487）
- `claude-api` 技能一次性注入约 156k token，单次工具调用耗尽上下文窗口。→ **诉求：技能资源注入的惰性加载或大小上限**

**6. 新技能方向**（#1329、#412）
- 紧凑记忆（符号化表示紧凑代理状态）、代理治理（AI 代理系统的安全模式——策略执行、威胁检测、信任评分、审计追踪）。→ **诉求：代理长期运行的记忆管理 + 代理安全治理框架**


## 三、高潜力待合并 Skills

**1. skill-creator 修复集群（#1298、#1099、#1050、#1323、#1261）**
- **潜力**：直接修复 #556（12 条评论，7 👍）和 #1169，且社区已有 10+ 次独立重现。合并后将大幅提升 skill 创建工具的可用性，让所有后续 skill 开发受益
- **阻力**：5 个 PR 存在功能重叠，需要 Anthropic 维护者协调合并策略，可能合并为一个综合修复

**2. self-audit 技能（#1367）**
- **潜力**：通用质量门禁理念在 #1385 Issue 中有 4 条评论持续讨论，截至 2026-08-01 仍在活跃，作者持续迭代。形式新颖（机械验证 + 推理审计），与 Anthropic 安全价值观契合，近期落地概率高

**3. color-expert 技能（#1302）**
- **潜力**：更新至 2026-07-21，作者保持活跃。自包含、无外部依赖、质量高，且填补了设计领域的空白。7 月仍在活跃，说明作者持续投入，合并概率大

**4. pyxel 技能（#525）**
- **潜力**：作者是 Pyxel 引擎原作者 kitao，MCP + Skill 组合是新兴最佳实践。更新至 2026-07-15，讨论持续但节奏平缓。独特的游戏开发场景有利于生态多样性

**5. plan-file-hygiene（#1479）**
- **潜力**：7 月刚创建，引用社区多方意见，直接回应 #1417。生命周期管理是真实痛点，且作者明确表达了合作意愿，近期落地概率较高


## 四、Skills 生态洞察

**当前社区最集中的诉求是「工具链可靠性」**—— skill-creator 的 bug（Windows 兼容性、触发检测失效、并行写入冲突）占据了热门 PR 的前五席，直接导致所有 skill 开发者在「针对噪声优化」；紧随其后的焦虑是「信任与安全」（官方命名空间治理、上下文窗口安全、技能去重），体现了社区从「造技能」到「管技能」的成熟度跃迁。

---

# Claude Code 社区动态日报 — 2026-08-06

## 今日速览

截至今日，官方仓库暂无新版本发布，社区活跃度集中在遗留 Issue 的批量关闭与讨论深化上。值得关注的是，**Cowork 跨平台兼容性问题**（macOS 下载 Linux 二进制）和 **Claude Max 用量异常消耗** 成为讨论热度最高的两大议题；同时，**全屏 TUI 渲染器（NO_FLICKER）在 iTerm2 中因 SIGTTIN 挂起** 的 Bug 成为用户最新反馈焦点。此外，多笔针对插件开发脚本健壮性的 PR 集中出现。

## 社区热点 Issues（Top 10）

1. **[#48827] Cowork 在 Intel Mac 上错误下载 Linux 二进制导致崩溃（已关闭）** — 🔥 22 评论
   Cowork 功能在 Claude Desktop 中下载了 ELF 格式的 Linux 可执行文件，导致 Intel Mac 立即崩溃（exit code 132 / SIGILL）。该问题从根本上揭示了 Cowork 二进制分发机制的架构缺陷，已关闭但仍具警示意义。
   [链接](https://github.com/anthropics/claude-code/issues/48827)

2. **[#82506] Claude Max 会话额度异常消耗（未使用即被扣除）** — 🔥 17 评论
   用户报告在未实际使用的情况下，Claude Max 会话限制被消耗。涉及计费与配额系统，直接影响用户信任度，是当前少数保持开放的高热度 Issue 之一。
   [链接](https://github.com/anthropics/claude-code/issues/82506)

3. **[#58750] Cowork Desktop (macOS): AskUserQuestion 卡片无法送达渲染进程** — ⚠️ 11 评论
   请求卡片从未到达渲染进程，UI 无任何显示，退出时静默解析为“已取消”。此问题影响 Cowork 核心交互流程，且长期未解决。
   [链接](https://github.com/anthropics/claude-code/issues/58750)

4. **[#21132] 功能请求：Claude Code 应能自主清理自身上下文** — 👍 15 票
   尽管已于年初关闭，但该功能请求获得 15 个赞，说明社区对“上下文/记忆管理”有持续需求，开发者希望模型在上下文过载时能主动重置或压缩。
   [链接](https://github.com/anthropics/claude-code/issues/21132)

5. **[#80131] 全屏渲染器在 iTerm2 中因 SIGTTIN 挂起（开放）** — 🆕 新增关注
   使用 `CLAUDE_CODE_NO_FLICKER=1` 全屏模式时，应用启动即失去终端前台进程组并挂起，鼠标跟踪泄漏至 shell，而 Ghostty 下工作正常。该问题与 #70435 相互印证，表明全屏渲染器在终端兼容性方面存在系统性缺陷。
   [链接](https://github.com/anthropics/claude-code/issues/80131)

6. **[#82101] 大型多代理工作流未触发预期警告阈值（开放）** — 🆕 新增关注
   实测超过 25 个代理或 150 万 tokens 时，系统未发出任何“Large workflow”警告。对于使用复杂工作流的高阶用户，缺少成本保护机制是显著痛点。
   [链接](https://github.com/anthropics/claude-code/issues/82101)

7. **[#70435] 全屏渲染器输入无回显直至提交** — ⚠️ 已关闭
   输入内容在提交前不显示，用户交互反馈缺失，与 #80131 问题相关。
   [链接](https://github.com/anthropics/claude-code/issues/70435)

8. **[#61930] iOS Code 标签页：语音输入后软键盘遮挡发送按钮** — 👍 5 票
   移动端远程操控场景下，语音输入后无法发送消息，直接影响 iOS 用户使用体验。
   [链接](https://github.com/anthropics/claude-code/issues/61930)

9. **[#68755] 内联渲染器在终端中破坏滚动缓冲** — 👍 4 票
   内联渲染器在 Ghostty 等终端中回写/覆盖滚动历史，导致输出错乱。TUI 渲染层的稳定性问题持续引发关注。
   [链接](https://github.com/anthropics/claude-code/issues/68755)

10. **[#69332] 后台通用子代理递归自生成导致级联发散，耗尽用量限制** — 🔥 高严重性
    子代理递归自我生成导致指数级扇出，严重烧毁用量配额（报告为 Opus 4.8 高容量会话）。虽已关闭，但暴露了代理系统在任务隔离和终止机制上的风险。
    [链接](https://github.com/anthropics/claude-code/issues/69332)

## 重要 PR 进展（Top 8）

1. **[#84004] 插件开发：限定 frontmatter 解析范围**
   修复 `sed` 解析在 Markdown 正文包含 `---` 时，误将后续文本当作 frontmatter 解析的问题。提升插件元数据解析的健壮性。
   [链接](https://github.com/anthropics/claude-code/pull/84004)

2. **[#84003] 脚本：上层失败状态传播**
   修复评分/维护脚本在顶层失败时仍返回成功状态的问题，改进 CI 与错误报告流程。
   [链接](https://github.com/anthropics/claude-code/pull/84003)

3. **[#83999] 脚本：校验 gh 标志值**
   修复 `gh` 包装器未检测末尾缺失值参数的问题，确保非法命令被拦截并正确报错。
   [链接](https://github.com/anthropics/claude-code/pull/83999)

4. **[#83995] 脚本：校验 label 选项值**
   修复 `--add-label`/`--remove-label` 缺少参数时导致的 `unbound variable` 错误，并防止误将后续选项作为 label 值。
   [链接](https://github.com/anthropics/claude-code/pull/83995)

5. **[#83993] 脚本：拒绝自引用重复评论**
   修复重复评论脚本可能将同一 Issue 标识为自身的重复项并错误发布自引用评论的问题。
   [链接](https://github.com/anthropics/claude-code/pull/83993)

6. **[#83992] 插件开发：断言预期 Hook 决策**
   为 `test-hook.sh` 新增 `--expect allow|deny|ask` 参数，使测试能验证 Hook 是否按预期拒绝操作，而非仅验证其执行。
   [链接](https://github.com/anthropics/claude-code/pull/83992)

7. **[#84138] 为 Cowork 自签名证书错误提供变通方案**
   针对 Bun 运行时未加载系统证书导致 macOS 用户出现“Self-signed certificate detected”错误的问题，在 Hook 层提供 workaround。
   [链接](https://github.com/anthropics/claude-code/pull/84138)

8. **[#84004] 插件开发：限定 frontmatter 解析范围**
   修复 `sed` 表达式在 Markdown 正文包含 `---` 时，将正文误认为 frontmatter 的问题，避免错误的配置读取。
   [链接](https://github.com/anthropics/claude-code/pull/84004)

## 功能需求趋势

- **上下文与记忆管理**：社区强烈希望模型能自主管理/清除上下文（#21132），甚至自动切换上下文以避免过载。
- **成本与用量控制**：多个 Issue 聚焦于用量限额的透明度与控制力，如技能执行前的成本预估与确认（#68703）、大型工作流触发更积极的警告提示（#82101）。
- **Hook 与插件生态的完善**：对 Hook 事件类型（如权限解决后的回调 #64170）和插件开发工具链（#83990-#84004）有明确增强需求。
- **终端兼容性与 TUI 稳定性**：全屏/内联渲染器在多家终端（iTerm2、Ghostty、Terminal.app）的兼容性和无障碍（VoiceOver）支持需要提升。

## 开发者关注点

- **资源与用量安全**：“后台子代理递归失控耗尽配额”（#69332）和“大型工作流无预警”（#82101）表明用户对不可控的用量消耗感到焦虑。
- **TUI 渲染稳定性**：内联渲染器破坏滚动缓冲（#68755）、全屏模式在 iTerm2 挂起（#80131）和输入无回显（#70435）共同指向渲染层是最影响日常体验的痛点。
- **跨平台与远程体验**：Intel Mac 的 Cowork 二进制分发错误、iOS 端键盘遮挡和远程/本地会话管理混乱（#64895）反映出跨设备体验打磨尚不足。
- **错误响应机制**：HTTP 529 被误判为限流且无退避策略（#68502）、ECONNRESET 重试循环（#70417）等问题亟需更精细的错误处理与用户引导。

> 数据来源：[anthropics/claude-code](https://github.com/anthropics/claude-code) 截至 2026-08-06 的公开信息汇总。

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex 社区动态日报

**日期：2026-08-06**


## 今日速览

今日 Codex 发布了补丁版本 `rust-v0.146.1`，针对高能力网络模型（cyber-capable models）收紧了自动审查默认策略，并在终端界面中说明了权限变更。社区方面，Windows 平台相关问题持续高发，包括 WSL 仓库误报、Electron 主进程性能瓶颈和系统级输入卡顿等，成为开发者反馈最集中的领域。此外，大量 PR 集中在代码架构重构（如工具审批集中化、技能调用辅助函数统一），表明项目正在为后续功能扩展打基础。


## 版本发布

### rust-v0.146.1（补丁版本）
- **Bug 修复**：为高能力网络模型应用更安全的自动审查默认值，并在终端界面中说明权限变更（PR #37057）。
- 完整变更：https://github.com/openai/codex/compare/rust-v0.146.0...rust-v0.146.1

另外，`rust-v0.147.0-alpha.6.5`、`rust-v0.147.0-alpha.10/11/12` 等多个 alpha 版本也在今日发布，但暂无详细变更日志。


## 社区热点 Issues（Top 10）

### 1. [Windows][WSL] 26.721.3404 将有效 WSL 仓库误判为非 Git 仓库并报告 "Git is unavailable" (#35119)
- **链接**: https://github.com/openai/codex/issues/35119
- **评论/点赞**: 16 条评论 / 14 👍 | **状态**: OPEN
- **详情**: 从 26.715.10079.0 升级到 26.721.3404 后，位于 WSL ext4 文件系统上的有效 Git 仓库被错误识别。**影响面较大，阻塞 Windows + WSL 用户的日常开发流程。**

### 2. Windows 独立更新时 pwsh 继承 PSModulePath 导致 Get-FileHash 失败 (#27117)
- **链接**: https://github.com/openai/codex/issues/27117
- **评论/点赞**: 12 条评论 / 11 👍 | **状态**: OPEN
- **详情**: 从 PowerShell 7 启动 Codex 时，更新流程调用 `powershell.exe` 会继承 PS7 的模块路径，导致哈希校验失败。**持续两个月未修复，Windows 更新路径的稳定性问题值得关注。**

### 3. Codex Desktop 26.715 大线程每几秒完整重放，导致系统级输入卡顿 (#33786)
- **链接**: https://github.com/openai/codex/issues/33786
- **评论/点赞**: 11 条评论 / 2 👍 | **状态**: OPEN
- **详情**: 已完成的大型线程在后台被反复重放（每几秒一次），Windows 10 上引发全系统输入延迟。**性能严重问题，与 #32516 可能相关。**

### 4. Codex App 26.715.9868.0: spawn_agent 拒绝 gpt-5.6-luna 配合 multi_agent_v2 (#34700)
- **链接**: https://github.com/openai/codex/issues/34700
- **评论/点赞**: 11 条评论 / 30 👍 | **状态**: OPEN
- **详情**: 启用 multi_agent_v2 后，`spawn_agent` 对 `gpt-5.6-luna` 模型的请求被拒绝。**30 个 👍 表明该问题影响大量多智能体功能用户，是新模型兼容性的关键问题。**

### 5. 将侧边对话持久化为附加到主线程的子线程 (#26227)
- **链接**: https://github.com/openai/codex/issues/26227
- **评论/点赞**: 9 条评论 / 21 👍 | **状态**: OPEN
- **详情**: 侧边对话（side chats）目前是临时的，会话关闭即丢失。社区希望将其持久化为主线程的子线程。**21 个 👍 显示这是一个强烈的产品功能需求。**

### 6. Codex 网络安全请求过滤的严重误报问题 (#37161)
- **链接**: https://github.com/openai/codex/issues/37161
- **评论/点赞**: 4 条评论 / 1 👍 | **状态**: OPEN（今日创建）
- **详情**: 安全过滤器对合法任务（静态分析、模糊测试、编译器等）产生大量误报。**值得注意的是，今日发布的 rust-v0.146.1 补丁可能与此问题相关。**

### 7. Desktop App 文件引用行号跳转不可靠 (#28643)
- **链接**: https://github.com/openai/codex/issues/28643
- **评论/点赞**: 8 条评论 / 7 👍 | **状态**: OPEN
- **详情**: 点击文件引用（带行号）时经常无法跳转到目标行。**影响日常代码审查和导航体验。**

### 8. [Feature Request] 每线程 Auto 模式，同时路由模型和推理力度 (#34278)
- **链接**: https://github.com/openai/codex/issues/34278
- **评论/点赞**: 5 条评论 / 2 👍 | **状态**: OPEN
- **详情**: 希望在单个线程内实现 Auto 模式，自动选择模型和推理力度。维护者已进行 triage 总结（2026-08-01）。

### 9. 严重误报：网络安全请求过滤 (#37161 相关) 与 [Windows][26.730.7989.0] Computer Use 因 EPERM lstat 失败 (#37029)
- **链接**: https://github.com/openai/codex/issues/37029
- **评论/点赞**: 4 条评论 / 1 👍 | **状态**: OPEN（今日创建）
- **详情**: 在 Windows 上启动 Computer Use 功能时，因 Codex runtime 的 `EPERM lstat` 错误导致失败。**与 #37161 一起，反映出安全/权限相关回归问题在今日集中出现。**

### 10. 从对话消息分叉新会话而不影响原线程 (#13087)
- **链接**: https://github.com/openai/codex/issues/13087
- **评论/点赞**: 7 条评论 / 1 👍 | **状态**: CLOSED
- **详情**: 在转录中滚动到某条消息并按 `f` 分叉新对话，而不修改当前线程。该请求已被关闭（可能已实现或被拒绝），但体现了社区对更灵活会话管理的需求。


## 重要 PR 进展（Top 10）

### 1. #37175 — 为分页历史添加旧版 rollout 迁移
- **链接**: https://github.com/openai/codex/pull/37175
- **内容**: 新增 `LocalThreadStore::migrate_rollouts`（含 dry-run 和应用模式），将旧的 JSONL 记录规范化迁移到分页历史结构，支持线程选择、吞吐限制和逐条结果输出。

### 2. #37174 — 在 `codex-skills` 中集中技能调用辅助函数
- **链接**: https://github.com/openai/codex/pull/37174
- **内容**: 将工具提及解析、技能名称计数和隐式调用检测移入 `codex-skills` 公共 API，并从 `SkillLoadOutcome` 中解耦隐式调用检测。

### 3. #37168 — 限制远程 MCP 握手的 HTTP 请求
- **链接**: https://github.com/openai/codex/pull/37168
- **内容**: 修复流式 HTTP MCP 握手超时后执行器仍被阻塞的问题——跟踪剩余初始化截止时间，避免串行执行器被卡死。

### 4. #37167 — 向 MCP 贡献者公开会话来源
- **链接**: https://github.com/openai/codex/pull/37167
- **内容**: 新增 `session_source()` 方法到 `McpServerContributionContext`，在线程级 MCP 解析中传播每个线程的 `SessionSource`。

### 5. #37162 — 通过技能扩展加载宿主技能根
- **链接**: https://github.com/openai/codex/pull/37162
- **内容**: 将递归宿主技能根改由技能扩展的宿主加载器加载，插件特定根保留在原有加载器上，以保证插件快照缓存和命名空间隔离。

### 6. #37157 — 强化 TUI 中命名会话查找
- **链接**: https://github.com/openai/codex/pull/37157
- **内容**: 在 resume 和 archive 命令间共享精确名称候选查找，优先使用有效的 SQLite 名称，同时恢复旧版索引名称且不覆盖新元数据。

### 7. #37151 — 合并并发 Git 状态扫描
- **链接**: https://github.com/openai/codex/pull/37151
- **内容**: 对同一仓库根的并发工作区元数据请求共享同一个 `git status --porcelain` 调用，减少重复扫描（关联问题 #35119 中 Git 相关）。

### 8. #37132 — 本地强制托管认证要求
- **链接**: https://github.com/openai/codex/pull/37132
- **内容**: 在存储或环境凭据可用之前（包括云要求未拉取的引导阶段），通过本地 `requirements.toml` 允许列表强制执行认证限制。

### 9. #37129 — Windows 路径 URI 比较改为 ASCII 大小写不敏感
- **链接**: https://github.com/openai/codex/pull/37129
- **内容**: 对推断的 Windows 盘符和 UNC 路径，`PathUri` 的相等性和哈希忽略 ASCII 大小写（POSIX 行为保持大小写敏感）。

### 10. #37128 — 在 `Session` 中集中工具审批处理
- **链接**: https://github.com/openai/codex/pull/37128
- **内容**: 将权限钩子、审查者路由、审批缓存和用户审批请求全部移入会话级审批流程，shell、统一执行和 apply-patch 运行时统一以 `ApprovalAction` 描述请求。


## 功能需求趋势

从今日活跃的 Issues 和 PR 中可提炼出以下社区关注方向：

1. **会话与线程管理**（#26227、#13087、#34278）：持久化侧边对话为子线程、支持从消息分叉新会话、per-thread Auto 模式。**核心诉求是让对话结构更灵活、可复用。**
2. **模型与权限控制**（#34700、#37161、#37145、#37132）：新模型（如 gpt-5.6-luna）兼容性、安全过滤误报率降低、按模型能力门控功能、本地认证策略。**随着模型能力增强，细粒度的模型路由和权限管控需求上升。**
3. **多平台支持与稳定性**（#35119、#27117、#33786、#37029）：WSL 仓库识别、Windows 更新流程、Electron 性能问题、Computer Use 权限问题。**Windows 生态（含 WSL）的稳定性成为最大痛点。**
4. **远程与移动端体验**（#37142、#37173、#33358）：移动端远程控制桌面 Codex 时，需支持 SSH 项目展示、线程上下文传递、文件下载到手机。**Remote 工作流的完整性有待提升。**
5. **技能系统架构演进**（#37174、#37162、#37144、#37149）：大量 PR 围绕技能的发现、快照、符号链接和编排。**内部架构正在为更强大的技能生态做准备。**


## 开发者关注点（痛点或高频需求）

1. **Windows 平台问题积压严重**：WSL 仓库误判（#35119）、系统级输入卡顿（#33786）、Electron 主进程高 CPU 循环（#32516）、桌面重绘冻结（#37172）——**Windows 用户是目前反馈最密集的群体，多个问题长期未解决。**

2. **更新与升级体验不稳定**：Windows 独立更新因 PSModulePath 继承失败（#27117）、macOS 自动更新破坏 Monterey 支持（#37019）、Chrome 插件更新后 manifest 指向缺失文件（#37159）——**更新流程的健壮性需要加强。**

3. **安全过滤与审查机制易误伤**：网络安全相关请求过滤误报率高（#37161），尤其影响安全研究、静态分析等合法场景。今日发布的 0.146.1 补丁正是在此方向上的努力。**如何平衡安全与开发者自由度是关键。**

4. **性能与资源消耗**：Electron 主进程后台循环、ScreenCaptureKit 流未关闭导致 GPU 高占用（#35659）、大线程重放导致输入卡顿（#33786）——**资源泄漏和无效循环在桌面应用中频繁出现。**

5. **移动端 Remote 体验不完整**：Android/iOS 远程控制桌面 Codex 时存在线程上下文缺失（#37173）、SSH 项目不显示（#37142）、无法下载文件到手机（#33358）——**Remote 是高频使用场景，但功能缺口明显。**

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报 — 2026-08-06

> 数据来源: github.com/google-gemini/gemini-cli

---

## 今日速览

当日无新版本发布，社区讨论集中在 **Agent 子代理行为异常**（如 `MAX_TURNS` 被误报为成功、通用代理挂起）与 **Auto Memory 可靠性** 两大 P1 级问题上。SDK 层收到多个聚焦 **工具参数解析容错** 的 PR，核心代理的稳定性是目前社区与维护者的共同焦点。

---

## 社区热点 Issues（Top 10）

**1. Subagent recovery after MAX_TURNS is reported as GOAL success, hiding interruption** ⭐️
- **Issue**: [#22323](https://github.com/google-gemini/gemini-cli/issues/22323)
- **优先级**: P1 | 评论 12 | 👍 2
- **要点**: `codebase_investigator` 子代理在已达最大轮次限制时仍报告 `status: "success"` 与 `Termination Reason: "GOAL"`，掩盖了实际中断。这会让上层调用误判任务已成功完成，**极具误导性**。

**2. Generalist agent hangs** ⭐️
- **Issue**: [#21409](https://github.com/google-gemini/gemini-cli/issues/21409)
- **优先级**: P1 | 评论 8 | 👍 8
- **要点**: 当 CLI 将任务委派给 generalist 代理时**无限期挂起**（持续一小时无响应），用户明确指示"不委派子代理"后问题消失，强烈指向子代理调度/执行环节的缺陷，点赞数高，影响面大。

**3. Robust component level evalutions**
- **Issue**: [#24353](https://github.com/google-gemini/gemini-cli/issues/24353)
- **优先级**: P1 | 评论 7
- **要点**: **EPIC**，旨在为 6 个受支持的 Gemini 模型、76 个行为测试建立更稳健的**组件级评估体系**，是为防止如 #22323、#21409 等回归的基础设施级工作。

**4. Shell command execution gets stuck with "Waiting input" after command completes**
- **Issue**: [#25166](https://github.com/google-gemini/gemini-cli/issues/25166)
- **优先级**: P1 | 评论 4 | 👍 3
- **要点**: 执行简单 CLI 命令后终端卡在 "Awaiting user input"，即使命令本身不等待输入。属于高频交互阻断型 Bug，用户体感明显。

**5. Assess the impact of AST-aware file reads, search, and mapping**
- **Issue**: [#22745](https://github.com/google-gemini/gemini-cli/issues/22745)
- **优先级**: P2 | 评论 7
- **要点**: **EPIC**，探索 **AST 感知** 的文件读取/搜索/代码映射以降低 token 消耗、提高调用精度。这是对代码库认知架构的升级方向。

**6. Gemini does not use skills and sub-agents enough**
- **Issue**: [#21968](https://github.com/google-gemini/gemini-cli/issues/21968)
- **优先级**: P2 | 评论 6
- **要点**: 用户反馈模型**不会主动使用**自定义 skills 和子代理，即使任务高度相关，只有在明确指令下才会调用。反映模型对工具/代理的自主调度能力不及预期。

**7. Leverage model's bash affinity via Zero-Dependency OS Sandboxing & Post-Execution Intent Routing**
- **Issue**: [#19873](https://github.com/google-gemini/gemini-cli/issues/19873)
- **优先级**: P2 | 评论 8
- **要点**: 提案旨在利用 Gemini 3 的原生 bash 能力，通过**零依赖沙箱**与"执行后意图路由"机制，在保障安全的前提下绕过工具限制、直接执行 shell。

**8. Model frequently creates tmp scripts in random spots**
- **Issue**: [#23571](https://github.com/google-gemini/gemini-cli/issues/23571)
- **优先级**: P2 | 评论 3
- **要点**: 模型在禁用 shell 工具后，会**在项目各处生成临时脚本**，污染工作区，增加清理成本。属代码生成行为的卫生性问题。

**9. Stop Auto Memory from retrying low-signal sessions indefinitely**
- **Issue**: [#26522](https://github.com/google-gemini/gemini-cli/issues/26522)
- **优先级**: P2 | 评论 5
- **要点**: Auto Memory 的索引处理存在缺陷，低价值会话可能被**无限次重试处理**，消耗系统资源并产生噪音。

**10. Add deterministic redaction and reduce Auto Memory logging**
- **Issue**: [#26525](https://github.com/google-gemini/gemini-cli/issues/26525)
- **优先级**: P2 | 评论 4
- **要点**: **安全**相关：Auto Memory 在将对话内容发送给模型后再提示脱敏，存在**密钥先泄露**的风险。要求改为确定性的前置脱敏逻辑，并降低日志噪音。

---

## 重要 PR 进展（Top 10）

**1. fix(sdk): don't abort sendStream on malformed tool arguments**
- **PR**: [#28695](https://github.com/google-gemini/gemini-cli/pull/28695)（已合入）
- **要点**: 修复 SDK `sendStream()` 中未加保护的 `JSON.parse()` —— 模型输出的工具参数为非法 JSON 时会直接**抛出异常中断流**。现改为防御性解析，保证流不中断。

**2. fix(sdk): keep sendStream alive on malformed tool arguments**
- **PR**: [#28660](https://github.com/google-gemini/gemini-cli/pull/28660)（开放中）
- **要点**: 与 #28695 思路互补：在解析失败时将非法参数转为结构化 `functionResponse` **错误反馈**给模型，而非静默丢弃，帮助模型自我纠正。

**3. fix(core): preserve functionCall thoughtSignature when stripping thought parts**
- **PR**: [#28607](https://github.com/google-gemini/gemini-cli/pull/28607)（已合入）
- **要点**: 修复 v0.53.0 回归——清理上下文时移除 thought 部分导致 **API 400 缺 thought_signature** 错误，现保留签名。

**4. fix(core): stop a new user message fusing into an unanswered tool response**
- **PR**: [#28700](https://github.com/google-gemini/gemini-cli/pull/28700)（已合入）
- **要点**: 修复"模型接话而非回答"Bug：工具调用中断（流失败或按 ESC）后，用户下一条消息被错误地并入上一轮，模型把指令当上下文续写。现改为正确拆分。

**5. fix(core): ensure correct fallback on model capacity errors for GCA agent mode**
- **PR**: [#28670](https://github.com/google-gemini/gemini-cli/pull/28670)（已合入）
- **要点**: 修复 Gemini Code Assist 模式下**容量耗尽（429）后死循环重试**同一模型的问题，现在会正确切换至 Flash 等备用模型。

**6. fix(core,cli): repair /compress session reload and quota-fallback tool response loss**
- **PR**: [#28672](https://github.com/google-gemini/gemini-cli/pull/28672)（已合入）
- **要点**: 两个独立修复：`/compress` 命令压缩后**会话恢复失败**；以及触发配额限制后**工具调用结果丢失**，均影响长会话体验。

**7. fix(core): dynamically resolve Cloud Workstations proxy redirect URI for OAuth flows**
- **PR**: [#28688](https://github.com/google-gemini/gemini-cli/pull/28688)（开放中）
- **要点**: 修复 Cloud Workstations 中 OAuth 流程静态重定向到 `localhost` 的问题，改为**动态解析代理主机**，解决浏览器在本地而请求在远端 VM 的认证失败。

**8. fix(core): add timeout to IdeClient.getInstance() process traversal**
- **PR**: [#28677](https://github.com/google-gemini/gemini-cli/pull/28677)（开放中）
- **要点**: `IdeClient.getInstance()` 进程树遍历可能永久挂起导致 TUI 卡在 "Initializing..."，现添加 **3 秒超时** 并回退到无 IDE 模式，提升启动鲁棒性。

**9. fix(release): handle npm dist-tag deletion failures on registries that forbid it**
- **PR**: [#28694](https://github.com/google-gemini/gemini-cli/pull/28694)（已合入）
- **要点**: 修复夜间发布流程中**目标镜像仓库禁止删除 dist-tag 导致发布失败**的问题（如 Wombat Dressing Room 返回 403），处理容错逻辑。

**10. fix: resolve SSRF vulnerability in web-fetch.ts by using async DNS resolution**
- **PR**: [#28557](https://github.com/google-gemini/gemini-cli/pull/28557)（开放中）
- **要点**: **安全修复**：`isBlockedHost` 仅检查字面量 IP，域名解析到内网地址（如 `169.254.169.254`）可绕过校验。改为**异步 DNS 解析**后校验，封堵 SSRF 漏洞。此 PR 状态为待评审，建议关注合入进度。

---

## 功能需求趋势

- **子代理执行可靠性（高频）**：多起 P1/P2 Issue 集中在子代理的**错误终结状态报告**（#22323）、**意外挂起**（#21409）、以及**不使用用户自定义子代理**（#21968）。核心痛点在于"模型在什么条件下、以何种状态调用子代理"，而非子代理本身能力。
- **模型自主 bash 能力释放**：如 #19873 所示，社区期望让模型直接用原生 bash 处理任务，而非受限于隔离的脚本工具。
- **代码库认知升级（AST 感知）**：EPIC #22745 与 #22746 探索通过 AST 感知工具实现精确读取、搜索与映射，以减少 token 消耗与噪音。
- **Auto Memory 安全与可靠性**：关于 Auto Memory 的数据脱敏前置化（#26525）、低价值会话无限重试（#26522）、无效补丁静默跳过（#26523）等，说明**记忆系统在安全边界和状态管理上仍需打磨**。

---

## 开发者关注点

1. **交互卡死与误导性状态**：终端卡在 "Waiting input"（#25166）或代理任务实际失败却报告成功（#22323），这类问题对自动化流程是致命的——用户无法信任 CLI 的输出状态。
2. **子代理自主性与可控性**：模型"过度使用"（#22093）与"不够主动"（#21968）两种反馈并存，说明目前的**启发式触发策略不够稳定**，用户需要更可预测的行为开关。
3. **会话恢复与持久化**：`/compress` 后会话损坏（#28672）、退出编辑器后终端渲染错乱（#24935）等，影响长会话场景下的使用信心。
4. **安全边界**：SSRF 漏洞（#28557）与 Auto Memory 密钥泄露风险（#26525）是社区明确提出的安全隐患，开发者认为**安全应成为默认设计而非事后补救**。

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报

**日期：2026-08-06**


## 今日速览

昨日社区讨论热度集中在 MCP（模型上下文协议）生态兼容性上，多个新提交的 Issue 指向了 MCP 服务器连接、策略获取与 OAuth 认证失败问题，值得引起重视。版本方面发布了 1.0.79 系列的三个预发布版本，主要围绕 `/worktree` 命令和终端 UI 交互进行优化。此外，社区对新模型（如 `gpt-5.6-terra`、`claude-haiku-4.5`）的支持问题保持高度关注。


## 版本发布

过去 24 小时内发布了 3 个预发布版本：

- **v1.0.79-4**：常规预发布版本，未附带特别说明。
- **v1.0.79-3**：新增 `/worktree new` 命令，可在新建 worktree 中直接启动新会话。
- **v1.0.79-2**：优化终端 UI——将固定（pinned）提示行上移一行，与标签栏预留空间对齐，保持提示形态并节省一行时间线空间。在低于 30 行的终端中默认关闭该固定提示功能，避免挤压输出区域（可通过 `pinnedPrompts` 配置调整）。

> 另发现两个回归 Bug 值得关注：`[#4202]` 报告 1.0.73 中内置 `view` 工具对已存在文件报 "Path does not exist" 错误（1.0.71 时正常）——该问题疑似在 1.0.72 中引入且至今未修复；`[#4370]` 报告 1.0.79-1 在 FastMCP 服务器返回 `-32602` 时导致 MCP 初始化失败。


## 社区热点 Issues（10 个）

### 1. [#4202] 内置 view 工具对已存在文件报"路径不存在"（1.0.72 起回归）
- **标签**：`[area:non-interactive, area:tools]`
- **反馈**： 👍 1 · 💬 5
- **详情**：自 1.0.72 起，`view` 对已存在文件报错，1.0.71 正常。开发者使用隔离的 SDK 探针确认同一调用在 1.0.71 中始终成功。
- **链接**：https://github.com/github/copilot-cli/issues/4202

### 2. [#4345] claude-haiku-4.5 不支持 medium 推理强度
- **标签**：`[area:agents, area:models]`
- **反馈**： 👍 4 · 💬 2
- **详情**：当 `copilot_cli_opus_medium_effort_default` 与 `copilot_cli_gpt_5_4_mini_for_explore` 同时启用时，子代理执行反复报错："Reasoning effort 'medium' is not supported for model 'claude-haiku-4.5'"。模型能力与配置未对齐造成执行中断。
- **链接**：https://github.com/github/copilot-cli/issues/4345

### 3. [#1799] 如何关闭 alt-screen 视图？
- **标签**：`[area:configuration, area:terminal-rendering]`
- **反馈**： 👍 8（今日最高）· 💬 12
- **详情**：用户反映最近引入的 alt-screen 模式带来了不少问题（如与 tmux 或终端复制的冲突），希望提供配置项切回传统渲染方式。该问题自 3 月创建以来持续获得关注，近期更新表明仍无解决方案。
- **链接**：https://github.com/github/copilot-cli/issues/1799

### 4. [#4005] 企业版提示"Copilot billing entity isn't selected"导致无法保存 memories
- **标签**：`[area:enterprise, area:context-memory]`
- **反馈**： 👍 3 · 💬 4
- **详情**：企业环境中一切功能正常，但保存上下文记忆时持续报错"billing entity 未选择"。用户确认此前可正常保存。企业级部署的记忆功能因此不可用。
- **链接**：https://github.com/github/copilot-cli/issues/4005

### 5. [#4378] GHEC 数据驻留实例上 MCP 注册表策略获取失败，静默丢弃用户 MCP 服务器
- **标签**：`[triage]`
- **反馈**： 👍 0 · 💬 0（新提交）
- **详情**：在带数据驻留的 GHEC（`<tenant>.ghe.com`）实例上，所有用户配置的 MCP 服务器均被静默丢弃，仅平台默认项（`github-mcp-server`、`playwright`）可用。根因指向 MCP 注册表策略获取时返回 401/403。
- **链接**：https://github.com/github/copilot-cli/issues/4378

### 6. [#4374] 非 GitHub 远程仓库（Azure DevOps）中 /mcp search 报 400
- **标签**：`[triage]`
- **反馈**： 👍 4（新提交）· 💬 0
- **详情**：在 git 远程指向 `dev.azure.com` 的仓库中运行 `/mcp search` 始终报 "Failed to fetch MCP registry policy: 400 Bad Request"。社区用户已遇到同样问题，影响非 GitHub 远程环境中的 MCP 使用。
- **链接**：https://github.com/github/copilot-cli/issues/4374

### 7. [#4370] 1.0.79-1 对 FastMCP 的 server/discover 处理不当导致初始化失败
- **标签**：`[triage]`
- **反馈**： 👍 1 · 💬 2
- **详情**：CLI 会在初始化完成前发送 `server/discover` 请求，但 FastMCP 未实现该方法并返回 `-32602`，CLI 将其视为致命错误。与 FastMCP 生态的兼容性问题。
- **链接**：https://github.com/github/copilot-cli/issues/4370

### 8. [#4377] GPT-5.6 Terra 主会话却委托 Opus 子代理
- **标签**：`[triage]`
- **反馈**： 👍 0 · 💬 0（新提交）
- **详情**：用户明确配置 `gpt-5.6-terra` 后，账单显示大量 Opus 消费——主模型在未告知的情况下将任务委托给 Opus 子代理，可能导致成本失控与模型选择预期不符。
- **链接**：https://github.com/github/copilot-cli/issues/4377

### 9. [#4371] MCP OAuth 3LO（授权码）流程报错 -32042
- **标签**：`[triage]`
- **反馈**： 👍 0 · 💬 0（新提交）
- **详情**：连接配置了 OAuth 3LO 的 MCP Gateway 时，工具调用失败，提示 "This request requires more information"。客户端不支持 OAuth 3LO 流程所需的 URL elicitation，无法引导用户完成认证，MCP 生态集成受阻。
- **链接**：https://github.com/github/copilot-cli/issues/4371

### 10. [#3013] 后台（任务）代理不触发 Hooks——安全隐患
- **标签**：`[area:permissions, area:agents, area:plugins]`
- **反馈**： 👍 0 · 💬 3
- **详情**：若配置 Hook 阻止危险命令，用户可通过后台/任务代理绕过钩子直接执行。用户指出这属于安全漏洞（jailbreak 攻击面）。该问题自 4 月提交，仍在开放状态。
- **链接**：https://github.com/github/copilot-cli/issues/3013


## 重要 PR 进展

过去 24 小时内无 PR 更新或合并。


## 功能需求趋势

综合近期 Issue（含 8 月 5 日新增的多条），社区关注方向集中在以下几个维度：

1. **MCP 生态兼容性（重点）**：昨日新增了 4 个 MCP 相关问题——FastMCP `server/discover` 兼容（#4370）、MCP OAuth 3LO 认证（#4371）、GHEC 数据驻留下策略获取失败（#4378）、Azure DevOps 远程仓库 `/mcp search` 报 400（#4374）。MCP 已进入规模落地阶段，但兼容性与认证问题成为主要瓶颈。
2. **多模型支持与切换**：`claude-haiku-4.5` 不支持 `medium` 推理强度（#4345）、`GPT-5.6 Terra` 静默委托 Opus（#4377）、BYOM 提供商不支持运行中切换模型（#4376）。社区希望模型选择更透明可控，并支持会话内动态切换。
3. **终端渲染与交互**：alt-screen 模式引发持续争议（#1799）、pinned prompt 布局优化（1.0.79-2）、剪贴板占用冲突提示（#3172）。终端体验仍是高频反馈区。
4. **企业级功能稳定性**：billing entity 选择（#4005）、MCP 策略拉取数据驻留问题（#4378）。企业环境的多租户/合规特性带来新的技术挑战。


## 开发者关注点

- **模型选择透明性需求强烈**：用户最关心谁能看见/花费 token，不希望主模型偷偷调用更贵的 Opus。建议为子代理模型选择增加明确提示和预算控制能力。
- **新版回归问题是最大痛点**：#4202（view 工具误报）已存在约 2 周、横跨多个版本；#4370（FastMCP 兼容）在 1.0.79-1 中仍存在。开发者对新版本更新持谨慎态度，希望官方加快修复节奏。
- **安全边界绕行问题**：后台代理不触发 Hook（#3013）被社区标记为安全漏洞，该 Issue 已开放 3 个月仍无明确排期，开发者期待尽快修复。
- **MCP 配置的"隐形失败"现象**：多处反馈 MCP 问题均以静默方式出现（如 #4378、#3934），缺乏明确的错误提示。开发者呼吁提供可诊断的详细错误信息与日志，降低排查成本。
- **终端环境适配诉求长期未解决**：alt-screen 开关（#1799）已持续 5 个月，影响了重度依赖 tmux/screen 的用户。期待以配置项方式提供渲染模式的选择权。

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报

**日期：2026-08-06** | 数据来源：github.com/MoonshotAI/kimi-cli


## 今日速览

今日社区焦点集中在 **稳定性与可靠性** 议题：一条高赞 Issue 曝光了约 500K token 上下文高填充时 Agent 出现重复动作循环与指令漂移的严重退化；另一条 Issue 指出 `StrReplaceFile` 会意外破坏编辑区域外的非 UTF-8 字节。同时，社区对 Request #1283 **跨会话持久记忆系统** 的呼声持续走高（18 条评论），而 #2588 报告的错误提示不明确问题已有 PR #2590 提交修复。整体来看，官方尚无新版本发布，社区重心从功能新增转向了深层可靠性优化。


## 版本发布

过去 24 小时内无新版本发布。


## 社区热点 Issues

### #2586 [CLOSED] 高上下文填充时 Agent 可靠性退化：重复动作循环、无升级、指令漂移（约500K tokens时观察）
- **作者**: GrokBuildMJ | 更新: 2026-08-05 | 评论: 1
- **链接**: https://github.com/MoonshotAI/kimi-cli/issues/2586
- **为什么重要**: 这是难得的从真实长时运行任务中提炼出的深度问题——用户测量出约 500K tokens 的阈值（非官方文档限制），低于此值时同一工作流正常运行，超过后开始出现循环与漂移。这种"隐性上限"对 Agent 类 CLI 工具的可信度影响极大，值得官方明确文档化或修复。
- **社区反应**: 评论数 1（已被标记为 CLOSED），关注度还在发酵中。

### #1283 [OPEN] 功能需求：记忆系统 —— 跨会话持久上下文
- **作者**: CatKang | 创建: 2026-02-27 | 更新: 2026-08-05 | 评论: 18 👍: 0
- **链接**: https://github.com/MoonshotAI/kimi-cli/issues/1283
- **为什么重要**: 获得 18 条评论的长青需求，跨越近半年仍在活跃讨论。用户期望 AI 自动记忆项目模式与用户偏好，同时支持手动定义指令。作为 Agent 工具，"记忆"直接决定了从"一次性助手"升级为"长期协作者"的可能。
- **社区反应**: 评论热度高，表明这是社区长期未满足的核心诉求。

### #2591 [OPEN] StrReplaceFile 破坏编辑区域外的不可解码字节
- **作者**: shoemoney | 创建: 2026-08-05 | 更新: 2026-08-05 | 评论: 0
- **链接**: https://github.com/MoonshotAI/kimi-cli/issues/2591
- **为什么重要**: 严重的数据损坏 bug。`StrReplaceFile` 使用 `errors="replace"` 解码整个文件，意味着任何非 UTF-8 字节（即使远离编辑区域）都会被替换为 U+FFFD 并写回磁盘。对二进制文件或混合编码项目是致命的。
- **社区反应**: 新提交未获评论，属待官方确认的"潜伏雷"。

### #2588 [OPEN] 声明的模型缺少 capabilities：返回图像的 MCP 工具在副作用发生后中止运行，且无修复提示
- **作者**: tic-top | 创建: 2026-08-05 | 更新: 2026-08-05 | 评论: 0
- **链接**: https://github.com/MoonshotAI/kimi-cli/issues/2588
- **为什么重要**: 暴露出两个问题：1）能力声明缺失（如 `capabilities`）时应在调用前校验，而非工具执行副作用后才中止；2）错误信息未指明修复方式——PR #2590 已针对第二点提交修复，是"边用边补文档"的典型案例。
- **社区反应**: 已有 PR 跟进，说明得到维护者关注。

### #2587 [OPEN] 正常推进会话时 kimi cli 异常退出
- **作者**: Sdongmaker | 创建: 2026-08-05 | 更新: 2026-08-05 | 评论: 0
- **链接**: https://github.com/MoonshotAI/kimi-cli/issues/2587
- **为什么重要**: Windows 平台（NT 10.0.26200 x64）v0.29.2 + K3 high 模型，正常推进会话时进程崩溃，附截图。跨平台稳定性问题直接影响 Windows 用户的核心工作流。
- **社区反应**: 暂无评论，等待官方复现与定位。


## 重要 PR 进展

### #2590 [OPEN] fix(soul): 在 unsupported-capability 错误中指明配置修复方式
- **作者**: ayaangazali | 更新: 2026-08-05
- **链接**: https://github.com/MoonshotAI/kimi-cli/pull/2590
- **内容**: 针对 #2588 中小而独立的部分——错误信息只说缺少能力但不说改什么。修复后提示将直接给出 `config.toml` 中需补的 `capabilities` 字段，提升排障效率。

### #2589 [OPEN] docs: 将 qwen-audio-agent 列为语音 ACP 客户端
- **作者**: x-lixu | 更新: 2026-08-05
- **链接**: https://github.com/MoonshotAI/kimi-cli/pull/2589
- **内容**: ACP（Agent Client Protocol）目前只列了 Zed、JetBrains 等编辑器客户端。此 PR 在 ACP 段落后增加一句介绍 qwen-audio-agent——一个开源全双工语音运行时，可启动 `kimi acp` 让用户免提对话。作者已声明自己是该项目贡献者（disclosure included），文档补充价值高。


## 功能需求趋势

从今日活跃 Issues 看，社区最关注的方向是：

1. **稳定性与可靠性**（#2586、#2587、#2591）：长上下文下的行为退化、Windows 崩溃、字节损坏——随着用户将 kimi-cli 用于真实生产工作，稳定性已超过新功能成为首要期待。
2. **持久记忆系统**（#1283：跨会话上下文保持）：已活跃 5 个月，评论 18+，是社区呼声最持久的功能方向。
3. **MCP 生态完善**（#2588）：模型能力声明与 MCP 工具返回值（如图像）的协同需要更严谨的校验与更清晰的错误指引。
4. **语音交互（ACP 方向扩展）**（#2589）：语音作为 CLI 的免提交互方式开始进入社区视野。


## 开发者关注点

- **长时运行信任危机**：多个 Issue 指向 Agent 在复杂多步任务中的不可预测行为——无论是 500K 阈值后的静默退化（#2586），还是错误发生在副作用之后（#2588），都表明开发者需要更强的"事前校验 + 明确报错 + 安全回滚"机制。
- **文件操作的字节级安全**：StrReplaceFile 的字节破坏（#2591）提醒开发者，任何"读-改-写全量文件"的实现都必须考虑非 UTF-8 内容的保真。
- **跨平台体验一致性**：Windows 用户的崩溃报告（#2587）说明平台适配仍有盲区；同时本地环境差异（如非文档化的 context 上限）需要官方给出明确规格。
- **错误信息"可行动性"**：开发者反馈集中在"知道错了但不知道怎么改"——从 #2588 到 PR #2590，一个简单的 `capabilities` 字段修复提示就能大幅降低用户的排障成本。这也呼应了 #1283 对"AI 主动记忆并指导"的深层需求。

---

*本日报由 AI 自动汇总生成，数据以 GitHub 公开信息为准。*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

## OpenCode 社区动态日报 — 2026-08-06

### 📌 今日速览

今日社区焦点集中在**桌面端与 IDE 生态集成**（VS Code 扩展呼声极高，获 134 👍）与**旧版 Intel Mac 兼容性崩溃**（三条相关 Issue 持续发酵）。版本方面，v1.18.14 发布，优化了 xAI 登录流程并修复了流式错误处理。此外，**V2 架构迁移**相关的 PR 清理与数据迁移工作也在密集推进。

---

### 🚀 版本发布

**v1.18.14**
- **Core Improvements**：简化 xAI 登录为单一设备码流程，更好地支持无头（headless）和远程环境。
- **Bugfixes**：
  - 保留结构化流式 Provider 错误，使兼容的 Provider 能重试失败的响应。
  - 增加对瞬时 Provider 和网络错误的重试机制。

---

### 🔥 社区热点 Issues（Top 10）

1. **[FEATURE] 官方 VS Code 扩展** ([#11176](https://github.com/anomalyco/opencode/issues/11176))
   - 作者：c2b247 | 评论：27 | 👍：134
   - **要点**：社区呼声最高的需求，请求 OpenCode 提供原生 VS Code 扩展，以便原生运行。高 👍 数表明 IDE 集成是当前最迫切的功能缺口。

2. **zsh: illegal hardware instruction opencode** ([#8345](https://github.com/anomalyco/opencode/issues/8345))
   - 作者：yujianfeikong | 评论：21 | 👍：6
   - **要点**：老牌 Issue，用户在 macOS 上运行旧版（v1.1.19）即崩溃。与下方 #24876、#29039 共同指向**旧款 Intel Mac 的 AVX2 指令集不兼容**问题，影响范围较广。

3. **DeepSeek V4 Flash 突然要求启用“中国托管模型”** ([#39845](https://github.com/anomalyco/opencode/issues/39845))
   - 作者：capi | 评论：17 | 👍：22
   - **要点**：会话中途服务中断，提示需显式开启中国区模型选项。涉及订阅服务的地区策略变更，影响用户连续性，反馈激烈。

4. **[FEATURE] 支持加密货币支付** ([#23153](https://github.com/anomalyco/opencode/issues/23153))
   - 作者：suse-coder | 评论：16 | 👍：36
   - **要点**：用户强烈希望 OpenCode Go 订阅支持加密货币支付，反映社区对支付方式多样性的需求。

5. **[FEATURE] 跨项目会话列表/选择器（TUI）** ([#31932](https://github.com/anomalyco/opencode/issues/31932))
   - 作者：mskadu | 评论：14 | 👍：6
   - **要点**：内置 `/sessions` 命令仅限当前项目，多仓库开发者希望有一个全局会话视图。

6. **[FEATURE] 支持 SKILL.md 中的 `disable-model-invocation: true`** ([#34498](https://github.com/anomalyco/opencode/issues/34498))
   - 作者：yooo1999 | 评论：13 | 👍：49
   - **要点**：请求支持 SKILL.md frontmatter 中的该字段，以对标 Claude Code 等工具的能力。👍 数较高，是技能（Skill）系统的重要增强方向。

7. **旧款 Intel Mac 崩溃（AVX2 不兼容）** ([#24876](https://github.com/anomalyco/opencode/issues/24876))
   - 作者：marcioganzer | 评论：7
   - **要点**：明确报告 `EXC_BAD_INSTRUCTION (SIGILL)`，在 dyld 初始化阶段即崩溃，确认与 AVX2 指令集相关。

8. **macOS x64 "baseline" 二进制需 AVX2/FMA** ([#29039](https://github.com/anomalyco/opencode/issues/29039))
   - 作者：KrishanCHOUDHARY-1998 | 评论：7
   - **要点**：进一步证实问题，即使在声明为 "baseline" 的构建中，仍会在 Ivy Bridge CPU 上崩溃。

9. **[FEATURE] “自动模式” LLM 分类器自动批准权限** ([#37564](https://github.com/anomalyco/opencode/issues/37564))
   - 作者：dylbarne | 评论：6 | 👍：11
   - **要点**：请求实现类似其他 Agent 工具的自动权限批准机制，由 LLM 分类器决定操作是否需人工确认，以提升自动化效率。

10. **TUI 自动补全不列出配置引用内的文件** ([#34040](https://github.com/anomalyco/opencode/issues/34040))
    - 作者：jomarescudero | 评论：5
    - **要点**：当引用（reference）指向外部目录时，输入 `@home` 只能补全别名，无法继续补全该目录下的文件，影响多项目工作流效率。

---

### 🛠️ 重要 PR 进展（Top 10）

1. **feat(app): 可选垂直标签栏** ([#38308](https://github.com/anomalyco/opencode/pull/38308))
   - 作者：BYK | 状态：OPEN
   - **内容**：为 V2 应用添加可选的垂直标签布局，可在设置中开启，支持宽度调整与折叠，水平标签仍为默认。

2. **feat(opencode): 本地 LAN Provider 发现 + 自动模型发现** ([#27554](https://github.com/anomalyco/opencode/pull/27554))
   - 作者：androidand | 状态：OPEN
   - **内容**：在 `/connect` 中添加 `Local (LAN)` 发现，使用 mDNS 等方式自动发现本地 OpenAI 兼容服务器及其模型。

3. **feat(app): 新布局中的 Workspace 流程** ([#38790](https://github.com/anomalyco/opencode/pull/38790))
   - 作者：Hona | 状态：OPEN
   - **内容**：为 V2 新布局添加本地/新建/现有 Workspace 会话选择流程，支持长列表搜索、分支上下文等。

4. **fix(core): 连接自定义 Provider** ([#40761](https://github.com/anomalyco/opencode/pull/40761))
   - 作者：opencode-agent[bot] | 状态：OPEN
   - **内容**：修复自定义 Provider（如 litellm）在未声明环境凭证时无法在 `/connect` 中显示的问题，并增加回归测试。

5. **feat(core): 将 V1 数据迁移到 V2** ([#40723](https://github.com/anomalyco/opencode/pull/40723))
   - 作者：thdxr | 状态：OPEN
   - **内容**：实现 REST 触发的 V1 会话历史迁移，支持断点续传，并导入 V2 会话数据和旧版凭证。

6. **fix (core): 同一仓库的多个克隆应视为不同项目** ([#35311](https://github.com/anomalyco/opencode/pull/35311))
   - 作者：belisoful | 状态：OPEN
   - **内容**：修复多个克隆路径被识别为同一项目的问题，关闭了 14 个相关 Issue，是重要的项目隔离修复。

7. **refactor: 移除遗留 workspace 控制平面** ([#40760](https://github.com/anomalyco/opencode/pull/40760))
   - 作者：kitlangton | 状态：OPEN
   - **内容**：清理 V2 中过时的 workspace 生命周期、事件、请求输入等逻辑，保留 `Location.workspaceID` 等核心概念，是 V2 架构精简的一环。

8. **fix(cli): 更新后重启过期客户端** ([#35455](https://github.com/anomalyco/opencode/pull/35455))
   - 作者：kitlangton | 状态：CLOSED
   - **内容**：防止旧客户端干扰新守护进程，并优化版本号比较逻辑（如 `next-9999` vs `next-15000`）。

9. **fix(provider): 对不兼容的 OpenAI 兼容主机跳过 includeUsage** ([#35446](https://github.com/anomalyco/opencode/pull/35446))
   - 作者：Fatty911 | 状态：CLOSED
   - **内容**：修复火山方舟、千帆、DashScope 等国内网关因 `stream_options.include_usage` 返回 400 错误的问题。

10. **fix(opencode): 停止静默的会话标题生成失败** ([#35440](https://github.com/anomalyco/opencode/pull/35440))
    - 作者：1837620622 | 状态：CLOSED
    - **内容**：修复会话自动命名（`ensureTitle`）静默失败导致会话显示为 “New session - timestamp” 的问题。

---

### 📈 功能需求趋势

- **IDE 与编辑器集成**：官方 VS Code 扩展（#11176）以 134 👍 高居榜首，另有 PyCharm ACP 进程问题（#40696）和桌面端 SSH 远程支持（#33273），显示**桌面/IDE 生态体验是最大增长点**。
- **TUI 交互与自动化**：跨项目会话选择（#31932、#35581）、命令中段自动补全（#40719、#40689）、根目录技能补全（#40720）等，反映用户对**终端内高效操作**的强烈诉求。
- **模型与 Provider 管理**：SKILL.md 增强（#34498）、自定义 Provider 流程完善（#34004、#40761）、中国区模型策略问题（#39845），表明**多模型支持和策略透明度**是重要方向。
- **系统兼容性**：旧款 Intel Mac 崩溃相关 Issue（#8345、#24876、#29039）持续活跃，用户期待提供真正的“baseline”二进制或放弃 AVX2 依赖。

---

### 🧑‍💻 开发者关注点

- **崩溃与兼容性痛点**：**旧款 Intel Mac（AVX2）崩溃**是当前最突出的技术债，多条 Issue 互相印证，影响特定用户群体。
- **数据与会话管理**：全局规则（`AGENTS.md`）被遗忘（#40348）、项目文件夹重命名后服务端残留旧路径（#35240）、旧项目数据无法清除（#40699）等，显示**配置持久化和项目生命周期管理**需要加强。
- **资源消耗问题**：PyCharm AI Assistant 启动时衍生 15-22 个 `opencode.exe` 进程导致内存耗尽（#40696），是 IDE 集成场景下的重大性能问题。
- **支付与订阅**：加密货币支付（#23153）呼声较高，结合中国区模型限制问题（#39845），**商业化策略与用户体验的平衡**是社区争论焦点。

---

> 日报基于 GitHub 数据自动生成，仅供参考。

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi 社区动态日报 — 2026-08-06

## 今日速览
Pi 社区近期围绕 **Qwen 3.8 新模型支持**、**Copilot 登录模型不可用**、**OSC 8 超链接截断**等议题密集提交了多项 PR；同时，社区对 **`AGENTS.override.md` 上下文覆盖**与**多行 Bash 命令解析**等易用性改进表现出强烈兴趣。今日无新版本发布，但有多项修复与功能 PR 已合并。

---

## 社区热点 Issues（Top 10）

**1. [Windows] 使用 Pi 的现状与问题调查** [#7547](https://github.com/earendil-works/pi/issues/7547)  
作者发起关于 Windows 下 Pi 运行方式的讨论（原生/WSL/虚拟机等），旨在收集痛点以合理分配修复精力。该话题收到 **17 条评论**，反映出 Windows 开发者基数庞大且配置方式多样，但官方支持优先级尚不明朗。

**2. `truncateToWidth()` 截断 OSC 8 超链接导致悬挂链接** [#7399](https://github.com/earendil-works/pi/issues/7399)（已关闭）  
`truncateToWidth()` 在截断超链接标签时未平衡 OSC 8 序列，导致终端出现无闭合的超链接。定位明确，已由 PR #7657 修复。

**3. 使用 Anthropic 订阅时会话卡在 “Working…”** [#5291](https://github.com/earendil-works/pi/issues/5291)（已关闭）  
会话偶发卡死，打断/恢复有时无效，影响 Anthropic Enterprise 订阅用户。获得 **3 个 👍**，社区关注度较高，目前已关闭。

**4. `pi update --self` 因瞬时网络错误直接放弃更新** [#6675](https://github.com/earendil-works/pi/issues/6675)（已关闭）  
自更新仅尝试一次请求最新版本号，瞬时连接失败即中止，缺少重试机制。建议增加指数退避重试。

**5. 新增上下文窗口大小选项** [#5064](https://github.com/earendil-works/pi/issues/5064)（已关闭）  
用户希望 Pi 提供选择上下文窗口大小的选项，对齐 Copilot CLI 的类似功能。

**6. 支持 prompt 命令中传递视频/音频内容** [#3200](https://github.com/earendil-works/pi/issues/3200)  
建议将 `prompt` RPC 的 `images` 支持扩展至视频/音频，以配合 Gemma 4、GPT-4o 等多模态模型。获得 **4 个 👍**，反映多模态需求正在上升。

**7. 压缩（Compaction）支持独立配置 thinking level/model** [#7553](https://github.com/earendil-works/pi/issues/7553)  
自动/手动压缩会话当前强制复用会话的 thinking 设置，无法独立控制。对于使用推理模型的用户，压缩的思考预算与常规对话不可分离，影响摘要质量。

**8. iTerm2 内联图片缺少 `size` 参数导致 xterm.js 拒绝渲染** [#7465](https://github.com/earendil-works/pi/issues/7465)（已关闭）  
`encodeITerm2()` 未包含 `size=` 字段，而 `@xterm/addon-image@0.9.0` 强制要求该参数，导致图片在 xterm.js 终端中静默失败。

**9. 改进 Vertex + GCP 元数据服务器支持** [#5323](https://github.com/earendil-works/pi/issues/5323)  
当前 Vertex 认证状态检查使用同步 `existsSync` 判断 `GOOGLE_APPLICATION_CREDENTIALS` 或 `~/.config/gcloud/...`，未适配 GCP 元数据服务器等场景，建议改为异步探测。

**10. WebSocket 重试仅覆盖两种错误码，其他 transient 错误直接终止回合** [#7444](https://github.com/earendil-works/pi/issues/7444)  
`openai-codex-responses.js` 中仅对 `previous_response_not_found` 和 `websocket_connection_limit_reached` 重试，其余 `response.failed` 或 `error` 帧直接抛出 `CodexApiError`，中断整个回合。

---

## 重要 PR 进展（Top 10）

**1. 修复事件总线监听器泄漏** [#7656](https://github.com/earendil-works/pi/pull/7656)（已合并）  
修复 #7193：将 `pi.events.on()` 订阅作用域限定在注册它的扩展运行时内，并在 reload/disposal 时清理过期监听器，同时不影响宿主监听器。附回归测试。

**2. 支持 `AGENTS.override.md` 作为目录级上下文覆盖** [#7664](https://github.com/earendil-works/pi/pull/7664)（已合并）  
在上下文发现中优先加载 `AGENTS.override.md`（高于 `AGENTS.md`/`CLAUDE.md`），保留祖先目录分层与嵌套 worktree 去重逻辑。配套 CLI 支持 PR #7679 与另一项实现 #7681 均已合并。

**3. 修复截断的 OSC 8 超链接（BEL 终止）** [#7657](https://github.com/earendil-works/pi/pull/7657)（已合并）  
关闭 `truncateToWidth()` 截断超链接标签时留下的悬挂 OSC 8 序列，保留其 BEL/ST 终止符。跟随 PR #7665 优化为跳过不含 OSC 8 的明文前缀，避免无谓的逐字符 ANSI 解析。

**4. 修复审阅意见中逗号后接 `lgtm` 无法识别** [#7663](https://github.com/earendil-works/pi/pull/7663)（已合并）  
`LGTM, please submit a minimal patch!` 这类 `lgtm` 措辞现可被正确识别为批准意见。修复 #7399 回归问题（由 #7023 引入）。

**5. 为 openai-completions 端点增加 thinking_token_budget 支持** [#7638](https://github.com/earendil-works/pi/pull/7638)（已合并）  
解决 OpenAI 兼容端点中推理与回答共享 `max_tokens` 的问题：推理过长时可能耗尽配额导致无文本、无工具调用，agent-loop 误判任务完成。现已支持 `thinking_token_budget` 独立预算。

**6. Copilot 模型策略恢复** [#7672](https://github.com/earendil-works/pi/pull/7672)（已合并）  
以 `model_picker_enabled` 为主信号，仅当 Individual 端点无可用 picker 模型时回退到策略显式启用的模型；非 Individual 账户保持严格 picker 语义。修复 Copilot 登录后 `availableModelIds` 为空的问题。

**7. 编译产物禁用 bunfig 自动加载** [#7685](https://github.com/earendil-works/pi/pull/7685)（已合并）  
使用 `--no-compile-autoload` 编译发布/本地二进制，避免项目 cwd 下 `bunfig.toml` 的 preload（如 MDX 插件）在 `pi` 代码执行前崩溃启动，包括 `pi --version`。

**8. 支持 `@file#L<start>-L<end>` 行号范围引用** [#7679](https://github.com/earendil-works/pi/pull/7679)（已合并）  
在 CLI `@file` 引用中支持基于 1 的闭区间行号选择器，为 Neovim 插件等可视化选择提供基础能力，并将生效的行元数据包含在文件 prompt 标签中。

**9. 新增可配置 Harness 工厂** [#7686](https://github.com/earendil-works/pi/pull/7686)（开放中）  
为实验性 Harness 增加内部工厂，保留调用方提供的工具、激活策略、prompt 策略及 Harness 选项，并为内置工具附加 prompt 元数据，实现活动工具对象的 prompt 动态重建。

**10. 工具 prompt 贡献与工具定义同置** [#7671](https://github.com/earendil-works/pi/pull/7671)（开放中）  
将每个内置工具的系统 prompt 片段与指南移到其实现旁边，保持旧版工具定义 prompt 输出不变，并新增全量回归测试（含条件 Bash 指南）。

---

## 功能需求趋势

| 方向 | 典型 Issue / PR | 热度 |
|------|-----------------|------|
| **新模型/Provider 支持** | Qwen Token Plan Individual Provider（#7659、#7631）、Qwen 3.8 GA 切换（#7670）、Copilot 模型修复（#7634 / #7672） | 高 |
| **TUI/终端渲染健壮性** | 截断 OSC 8 链接（#7399、#7657）、iTerm2 图片 size 参数（#7465）、Bash 多行命令换行折叠（#7666） | 高 |
| **上下文/Agent 内存管理** | `AGENTS.override.md` 覆盖（#7642 / #7664 / #7681）、上下文窗口大小可选（#5064）、Compaction thinking 独立配置（#7553） | 中高 |
| **扩展 API 能力** | 事件总线泄漏修复（#7193 / #7656）、扩展持久化 API key（#7658）、`onRetry` 回调（#7649） | 中 |
| **多模态支持** | prompt 传递视频/音频（#3200） | 中 |
| **模型选择器/排序体验** | 自然排序模型变体（#7693 / #7690 / #7692）、页面键绑定（#7680） | 中低 |
| **平台/运维** | Windows 使用现状调查（#7547）、bunfig 预加载崩溃（#7684 / #7685）、SSH 登录 Anthropic 重定向到 localhost（#7691） | 中 |

---

## 开发者关注点

- **Windows 支持优先级不明确**：#7547 评论数最多（17 条），开发者希望官方明确原生 vs WSL 的定位，并集中精力修复高频问题。
- **瞬时网络错误缺乏重试机制**：#6675 与 #7444 分别暴露了自更新与 WebSocket 通道在 transient 错误下直接失败的脆弱性，开发者希望统一具备指数退避重试。
- **TUI 细节体验影响实际使用**：OSC 8 悬挂链接、iTerm2 图片 `size` 缺失、多行 Bash 命令新行折叠为空格等问题虽小，但频繁打断工作流，社区反馈积极且修复速度快。
- **扩展生命周期管理是嵌入场景的痛点**：事件总线监听器在 session reload 后残留，需要手动清理；扩展无法持久化 API key 到 `auth.json`，限制了自定义 provider 的落地。
- **编辑工具链集成意愿强**：`@file` 行号范围支持（Neovim 插件场景）和 JetBrains 作为语言后端（#7641）均获得反馈，说明开发者正在将 Pi 嵌入既有 IDE 流程。
- **模型选择器排序体验有待打磨**：`@1m` 与 `@200k` 词法排序混乱、`/model` 与 `/scoped-models` 顺序不一致，影响多上下文窗口模型时代的导航效率。

---

*本日报由 AI 生成，数据截至 2026-08-06，来源为 [earendil-works/pi](https://github.com/earendil-works/pi)。*

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 — 2026-08-06

## 今日速览

Qwen Code 发布 v0.21.6 稳定版及多个预览/夜间版本，主打 WebShell 原生 Live Voice 实验性支持（macOS）与桌面端（Tauri）v0.1.0 里程碑。社区焦点集中在安全漏洞（只读 Shell 逃逸、Provider 警告泄露密码）、CI 稳定性（/review 超时、模拟磁盘满误报）以及 WebShell 与桌面客户端的交互与鉴权问题。功能需求方面，“Local Control”（手机扫码接管会话）与“/slow”低成本异步模式等新方向获得关注。

---

## 版本发布

**v0.21.6** (Release)
- 亮点：WebShell 在 macOS 上新增实验性的原生 Live Voice 支持，通过全局快捷键进行实时音频交互 ([#7859](https://github.com/QwenLM/qwen-code/pull/7859))；Web Shell 在后台活动期间保持对话轮次展开。

**v0.21.6-preview.0** (Preview)
- 功能：浏览器扩展新增 alpha 就绪诊断 ([#6739](https://github.com/QwenLM/qwen-code/pull/6739))；新增 headless Goal 工作流文档。

**v0.21.5-nightly.20260805** (Nightly)
- 与 preview.0 同批变更，含浏览器扩展诊断与 headless 文档。

**desktop-v0.1.0** (Desktop)
- 首个桌面端独立版本，修复 Web Shell 预设问题与 CI 容器任务默认 shell 配置。

---

## 社区热点 Issues（Top 10）

**安全类（高优先级）**

1. **[P1/安全] 只读 Shell 分类器可通过行延续或 `${var@P}` 绕过自动批准执行任意命令** ([#8582](https://github.com/QwenLM/qwen-code/issues/8582))
   - AST 分类器与运行时替换门控均存在绕过路径，影响只读 Shell 的安全边界。评论 4 条，社区关注度高。

2. **[P2/安全] Provider 警告清理器截断含端口消息，且泄露含 `@` 的密码** ([#8136](https://github.com/QwenLM/qwen-code/issues/8136))
   - `sanitizeProviderWarning` 在解析 URL 凭据时存在两处 bug，导致密码泄露至 `/status` 负载。评论 8 条，为当日最热 Issue。

**CLI / 终端**

3. **[P2] `qwen mcp list` 在 SSE 服务器不发送 `endpoint` 时无限挂起** ([#8550](https://github.com/QwenLM/qwen-code/issues/8550))
   - 慢/无响应 SSE 服务器导致命令永久阻塞（非超时）。评论 4 条，标记 ready-for-agent。

4. **[P2] TUI 在 tmux < 3.5 下持续闪烁** ([#8580](https://github.com/QwenLM/qwen-code/issues/8580))
   - Ink 渲染器的整屏清除+重绘逻辑仅依赖未查询的 DEC 2026，导致 tmux 3.4 下每秒闪烁 2–3 次。与另一 tmux 闪屏报告 [#8562](https://github.com/QwenLM/qwen-code/issues/8562) 相互印证。

5. **[P3] 缩小终端窗口导致滚动缓冲区内容重复打印** ([#8557](https://github.com/QwenLM/qwen-code/issues/8557))
   - macOS + Warp 环境下缩小窗口时，已打印的转录块被重复输出。

**Web Shell / Desktop**

6. **[P2] Web Shell 会话深链接刷新返回 401 未授权** ([#8560](https://github.com/QwenLM/qwen-code/issues/8560))
   - `qwen serve --token` 启用后，刷新 `/session/<id>` 深链接返回 401。评论 3 条，状态 in-review。

7. **[P2] Desktop：设置中切换 UI 语言无效** ([#8592](https://github.com/QwenLM/qwen-code/issues/8592))
   - 语言下拉框选择后界面仍保持英文，切换逻辑未生效。

8. **[P2] Desktop：Markdown 链接可样式化但点击无响应** ([#8593](https://github.com/QwenLM/qwen-code/issues/8593))
   - 链接具有悬停/指针样式，但点击既不打开浏览器也无任何反馈。

**VSCode 插件**

9. **[P2] VSCode 插件：Edit/Write 文件链接解析错误** ([#8606](https://github.com/QwenLM/qwen-code/issues/8606))
   - 文件链接始终解析为 `<workspace-root>/<basename>`，嵌套文件报 "file not found"。

**CI/CD**

10. **[P1] CI /review：反向审计扇出启动静默挂起直至超时杀死运行** ([#8597](https://github.com/QwenLM/qwen-code/issues/8597))
    - 8 月 4 日 12 次超时、8 月 5 日再 9 次，4/5 失败源于同一模式，消耗完整 360 分钟预算。

---

## 重要 PR 进展（Top 10）

**核心修复**

1. **[feat] WebShell 原生 Live Voice（macOS）** ([#7859](https://github.com/QwenLM/qwen-code/pull/7859)) — 已合并
   - Codex 平级 Live 架构，默认关闭，仅 macOS WebShell 可用。

2. **[fix] 将核心 dist 打入 review CLI bundle** ([#8612](https://github.com/QwenLM/qwen-code/pull/8612))
   - 修复 review 阶段恢复 bundle 时缺少核心包构建产物的问题。

3. **[fix] 在还有时间报告时停止反向审计循环** ([#8468](https://github.com/QwenLM/qwen-code/pull/8468)) — 已合并
   - 防止反向审计耗尽 5 轮上限后仍无结果，CI 运行 #30786453681 实证该问题。

4. **[fix] 限制长单轮会话中反向转录页面的边界扩展** ([#8553](https://github.com/QwenLM/qwen-code/pull/8553))
   - 将页面对齐扩展限制为最多额外一页窗口，防止分页膨胀。

**CLI / 终端体验**

5. **[feat] 终端内联图片渲染** ([#8305](https://github.com/QwenLM/qwen-code/pull/8305))
   - 扩展终端图片基础设施至模型/工具的 `inlineData`，保留文本/图片有序性。

6. **[feat] VP 模式下恢复 Ctrl+点击超链接与右键菜单** ([#8439](https://github.com/QwenLM/qwen-code/pull/8439))
   - 虚拟视口模式启用 SGR 鼠标追踪后，恢复原生终端能力。

7. **[feat] 流式输出期间可点击展开/折叠思考块** ([#8443](https://github.com/QwenLM/qwen-code/pull/8443))
   - 移除 pending 状态下点击禁用限制，支持流式中展开思考过程。

**桌面 / WebShell**

8. **[fix] 移动端空会话 composer 固定至聊天面板底部** ([#8601](https://github.com/QwenLM/qwen-code/pull/8601))
   - 修复 760px 宽度以下 composer 位置漂移问题。

9. **[feat] WebShell 侧边栏暴露频道会话** ([#8457](https://github.com/QwenLM/qwen-code/pull/8457))
   - 新增 Tasks/Channels 切换，展示钉钉、飞书、企微集成会话。

10. **[fix] 钉钉状态卡片保持连续与可归因** ([#8565](https://github.com/QwenLM/qwen-code/pull/8565))
    - 任务运行期间创建单一连续卡片，跨响应边界流式输出可见内容。

---

## 功能需求趋势

- **手机远程控制（Local Control）**：[#8595](https://github.com/QwenLM/qwen-code/issues/8595) 提出扫码登录 + 手机接管本地会话，属于新方向。
- **低成本异步批处理**：[#8605](https://github.com/QwenLM/qwen-code/issues/8605) 提出 `/slow`/`/batch` 模式走异步 API 降本。
- **桌面端架构统一**：多个 Issue（[#8092](https://github.com/QwenLM/qwen-code/issues/8092)、[#8596](https://github.com/QwenLM/qwen-code/issues/8596)）主张废弃 Electron 应用、统一至 Tauri shell（desktop-v0.1.0 已初步落地）。
- **后台 Agent 可观测性**：[#8586](https://github.com/QwenLM/qwen-code/issues/8586) 要求显式 `activeWork` 事实用于深层健康检查与恢复路径。
- **SDK 生命周期钩子**：[#8591](https://github.com/QwenLM/qwen-code/issues/8591) 希望在 TypeScript SDK `query()` 中支持内联 hooks 配置。
- **本地化**：[#8551](https://github.com/QwenLM/qwen-code/issues/8551) 申请增加韩语文档与 README 语言栏入口。

---

## 开发者关注点

- **安全边界有效性**：Provider 警告泄露密码（[#8136](https://github.com/QwenLM/qwen-code/issues/8136)）与只读 Shell 逃逸（[#8582](https://github.com/QwenLM/qwen-code/issues/8582)）表明安全边界存在验证盲区，需要更系统的分类器与清理器回归测试。
- **CI 成本与时延**：/review 工作流频繁耗尽 360 分钟预算（[#8597](https://github.com/QwenLM/qwen-code/issues/8597)），CI 日志中模拟磁盘满错误误导排障（[#8532](https://github.com/QwenLM/qwen-code/issues/8532)）。建议区分模拟错误与真实环境错误输出。
- **终端渲染兼容性**：tmux/SSH 场景闪屏（[#8562](https://github.com/QwenLM/qwen-code/issues/8562)、[#8580](https://github.com/QwenLM/qwen-code/issues/8580)）窗口尺寸变化时滚动缓冲区重复输出（[#8557](https://github.com/QwenLM/qwen-code/issues/8557)），终端适配仍是痛点。
- **桌面端基础体验**：语言切换无效（[#8592](https://github.com/QwenLM/qwen-code/issues/8592)）、Markdown 链接不可点击（[#8593](https://github.com/QwenLM/qwen-code/issues/8593)）与 Windows 复制按钮失效（[#8538](https://github.com/QwenLM/qwen-code/issues/8538)）显示 desktop v0.1.0 仍需打磨基础交互。

---

*数据采集时间：2026-08-06 00:00 UTC+8*

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI 社区动态日报 — 2026-08-06

> 数据来源：github.com/Hmbown/DeepSeek-TUI（注：项目现以 CodeWhale 名义迭代）

---

## 今日速览

今日社区无新版本发布，活跃度集中在 **v0.9.4 发布列车（#5135）** 的密集合并期——7 项 Runtime API 增强 PR 同时推进，标志着项目正从 TUI 工具向**可编程 Agent 运行时平台**转型。Issue 侧，多 API Key 管理（#5250）与沙箱文件路径白名单（#5005）成为社区最迫切的配置需求，另有对未知模型 ID 静默降级缺陷（#5244）的持续关注。

---

## 版本发布

过去 24 小时无新 Release。当前主线为 v0.9.4 发布列车（PR #5135），已积累 77 个 commit（相对 main），涵盖 Runtime API、内存管理、MCP 配置等多项重大能力。

---

## 社区热点 Issues

| Issue | 标题 | 状态 | 热度 | 重要性 |
|--------|------|------|------|--------|
| [#5250](https://github.com/Hmbown/CodeWhale/issues/5250) | [enhancement] 仅能保存一个 API Key，多服务商使用困难 | 🟡 OPEN | 💬 1 | **高** — 多模型（DeepSeek + GLM）切换时被迫反复获取新 Key，是配置管理的核心痛点 |
| [#5005](https://github.com/Hmbown/CodeWhale/issues/5005) | [enhancement] 沙箱支持文件系统路径白名单 | ✅ CLOSED | 💬 2 | **高** — Xcode 构建产物位于工作区外（DerivedData），当前 workspace-write 模式无法访问，阻塞 iOS 开发者 |
| [#5244](https://github.com/Hmbown/CodeWhale/issues/5244) | [enhancement] 未知模型 ID 静默降级至 128K 上下文 | 🟡 OPEN | 💬 1 | **高** — 1M 窗口模型被静默截断至 128K 且无提示，属设计缺陷（#5239 遗留），0.9.4 已部分缓解 |
| [#4029](https://github.com/Hmbown/CodeWhale/issues/4029) | planning to create an interface similar to Reasonix? | 🟡 OPEN | 💬 4，👍 0 | **中** — 社区对类 Reasonix 交互界面有探索兴趣，已开放近 1 个月 |

> 注：24 小时内另有 4 条 Issue 更新，其中 #5250 与 #5244 为新增动态。总计 4 条活跃讨论条目。

---

## 重要 PR 进展

### 🚀 Runtime API 系列（v0.9.4 核心，7 项并行）
| PR | 功能 |
|-----|------|
| [#5131](https://github.com/Hmbown/CodeWhale/pull/5131) | **内存端点** — `/v1/memory` 提供内存检测与生命周期控制 |
| [#5130](https://github.com/Hmbown/CodeWhale/pull/5130) | **MCP 管理** — 支持通过 API 增删改查 MCP 服务器配置 |
| [#5133](https://github.com/Hmbown/CodeWhale/pull/5133) | **目标循环** — 暴露持久化 goal 状态与完成控制 |
| [#5132](https://github.com/Hmbown/CodeWhale/pull/5132) | **验证者凭证** — 任务失败明细、证据与重试判断 |
| [#5129](https://github.com/Hmbown/CodeWhale/pull/5129) | **技能生命周期** — 安装/更新/卸载/信任/审计全链路 |

> 本批 PR 将 TUI 的能力通过 HTTP API 完整暴露给托管客户端，为桌面/Web 前端铺路。全部由 Copilot 提交。

### 🐛 关键修复
- **[#5234](https://github.com/Hmbown/CodeWhale/pull/5234) fix(tui)** — 鼠标捕获时滚轮误触 composer 输入历史，根因是 xterm alternate-scroll 与鼠标捕获同时启用
- **[#5192](https://github.com/Hmbown/CodeWhale/pull/5192) fix(tui)** — 锁定 ratatui 0.30.0，规避 `Terminal::clear()` 的 CPR 查询与事件循环死锁竞争
- **[#5095](https://github.com/Hmbown/CodeWhale/pull/5095) fix(ohos)** — 修复 Windows 下 OpenHarmony SDK 含空格路径时 linker 参数被拆分的编译错误（已合并）

### ✨ 功能增强
- **[#5240](https://github.com/Hmbown/CodeWhale/pull/5240)** — Bash wait 工具将真实等待时长暴露给模型，避免模型误判长任务为死循环而盲目轮询
- **[#5242](https://github.com/Hmbown/CodeWhale/pull/5242)** — 支持从 checkpoint 恢复中断的子代理任务，无需重新分发
- **[#5225](https://github.com/Hmbown/CodeWhale/pull/5225)** — ACP 服务器补齐 file/search/git/patch/shell 工具执行能力，为 Zed 等编辑器提供真正的编码 Agent
- **[#5229](https://github.com/Hmbown/CodeWhale/pull/5229)** — 新增中文版 Windows 新手指南，覆盖安装、配置、模型切换、权限等

---

## 功能需求趋势

1. **Runtime API 完整化** — 内存、MCP、技能、目标循环、验证者凭证的系统化暴露（7 个 PR 集中体现）
2. **多服务商/多 Key 管理支持**（#5250）— 随着 DeepSeek、GLM 等国产模型的普及，配置灵活性成为刚需
3. **沙箱路径白名单/外部资源访问**（#5005，#5236）— 真实构建场景需要访问工作区外的日志与产物
4. **ACP 协议能力对齐**（#5225）— 编辑器接入需求从"聊天"升级为"可执行工具的 Agent"
5. **模型上下文窗口透明化**（#5244）— 未知模型 ID 的降级行为需要明确提示而非静默

---

## 开发者关注点

- **配置管理零碎化**：单 API Key 槽位 + 跨服务商切换需手动获取新 Key，是当前最高频的配置痛点
- **外部工具链访问受阻**：沙箱对构建产物（Xcode DerivedData）等外部路径的封锁，直接影响 CI 场景落地
- **静默降级危害认知增强**：1M 上下文模型被静默截断至 128K 的缺陷，暴露了模型 ID 与能力映射的健壮性问题
- **前端生态接入加速**：ACP 工具执行补齐 + Runtime API 系列 PR 密集合并，预示桌面/Web 客户端为下一阶段重点
- **Windows 文档缺口**：中文 Windows 指南提交（#5229）表明社区对新手友好度的诉求仍在持续

</details>

---
*本日报由 [agents-radar](https://github.com/kky-wollu/agents-radar) 自动生成。*
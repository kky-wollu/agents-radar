# AI CLI 工具社区动态日报 2026-08-10

> 生成时间: 2026-08-09 22:35 UTC | 覆盖工具: 9 个

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

好的，作为资深技术分析师，基于您提供的2026-08-10各主流AI CLI工具的社区动态摘要，我为您生成以下横向对比分析报告。

---

### 1. 生态全景

AI CLI 工具已从单纯的编码辅助演变为复杂的**自动化代理平台**，社区反馈表明行业正经历“成长的烦恼”。核心矛盾集中在三个方面：**一是代理的自主性与可靠性**，关于子代理挂起、误报成功、状态错乱等问题在各工具中频发，成为开发者最核心的信任障碍；**二是安全与权限控制的精细化**，粗放的安全过滤器频繁误报、权限系统存在绕过路径，严重干扰合法工作流；**三是平台化演进带来的架构挑战**，多会话协调、上下文管理、远程控制等高级功能需求旺盛，但实现稳定性和跨平台一致性（尤其Windows和Linux）仍显不足。此外，存储空间失控、静默失败等问题也普遍存在。

### 2. 各工具活跃度对比

| 工具 | 今日 Issues 更新 | 今日 PR 动态 | 版本发布 | 社区热点 |
| :--- | :--- | :--- | :--- | :--- |
| **Claude Code** | ~50条 (Top 10) | 3个 | 无 | 安全过滤器误报、流式响应延迟、Agent团队指针黏滞 |
| **OpenAI Codex** | ~10条 (Top 10) | 7个 (均为bot自动更新) | 无 | Linux桌面版需求、Windows端Computer Use不稳定、存储膨胀 |
| **Gemini CLI** | ~10条 (Top 10) | 10个 | v0.56.0-nightly | 子代理挂起/误报、Auto Memory安全缺陷、ACP会话恢复 |
| **GitHub Copilot CLI** | ~10条 (Top 10) | 无 | 无 | MCP基础设施稳定性、远程会话失败、并行工具调用错乱 |
| **Kimi Code CLI** | 2个 (Top 2) | 1个 | 无 | 跨会话记忆系统需求、ACP流式响应挂死 |
| **OpenCode** | ~10条 (Top 10) | 10个 | 无 | 复制粘贴失效、代理网关模型名bug、嵌套子代理权限挂起 |
| **Pi** | ~10条 (精选) | 10个 | 无 | TUI交互体验、Copilot登录429、llama.cpp默认模型启动失败 |
| **Qwen Code** | 24条 | 50条 | 无 | 多会话协调、Web Shell与daemon稳定性、Windows安装问题 |
| **DeepSeek TUI** | ~10条 (Top 10) | 10个 | v0.9.6 准备PR已合入 | Context压缩不透明、多Provider管理、TUI权限请求默认值变更 |

*(注：各工具活跃度数据来自各日报中的“今日速览”及“热点”板块，为不完全统计，仅反映报告覆盖的Top级动态。)*

### 3. 共同关注的功能方向

- **代理（Agent）可靠性与组合性**
  - **Claude Code**: Agent 团队模式指针黏滞，子代理路由错误。
  - **Gemini CLI**: 多个 P1 级子代理 Bug（挂起、误报成功、Wayland下崩溃），社区提出“允许代理调用代理”。
  - **OpenCode**: 嵌套子代理权限请求导致会话静默挂起（虽已出修复，但反映问题存在）。
  - **Qwen Code**: 提出了多会话原生协调的 RFC，以支持更复杂的多代理工作流。
  - **GitHub Copilot CLI**: 并行工具调用响应顺序错乱，导致 Agent 状态混乱。

- **“静默失败”与状态真实性**
  - **Claude Code**: 工具调用参数被“静默吸收”，Plan 模式被“静默绕过”。
  - **Gemini CLI**: 子代理到达 MAX_TURNS 被误报为成功。
  - **GitHub Copilot CLI**: Prompt 被“静默丢弃”，新会话永久空闲。
  - **DeepSeek TUI**: 工具接受错误参数名却返回“假成功”，配置改动被“静默遮蔽”。
  - **Pi**: 自动压缩后任务停止而非恢复，表现为“静默停止”。

- **跨平台支持与体验一致性**
  - **OpenAI Codex**: Linux桌面版需求极高（945👍), Windows端Computer Use功能不可用。
  - **Gemini CLI**: 浏览器子代理在 Wayland 环境（Linux）下失败。
  - **Qwen Code**: Windows 安装程序存在缺陷。
  - **OpenAI Codex** 与 **Qwen Code**: 均存在因 `OTEL_METRICS_EXPORTER` 环境变量导致可观测性数据“静默禁用”的相似问题。

- **存储与资源管理**
  - **OpenAI Codex**: Crashpad 日志以每天 +5GB 速度膨胀，会话存储可增至 TiB 级。
  - **Claude Code**: 社区提议子代理扇出时需“内存感知的节流”，避免 OOM。
  - **Pi**: Mac 上长会话导致高 CPU 占用（50-110%）。

- **安全与权限控制**
  - **Claude Code**: 安全过滤器大规模误报，将合法运维操作（IAM加固、系统审计）误判为攻击。
  - **Gemini CLI**: Auto Memory 功能存在“先发送后脱敏”的安全设计缺陷。
  - **GitHub Copilot CLI**: MCP 临时空策略导致用户服务器被“永久拉黑”。

### 4. 差异化定位分析

- **Claude Code**: 定位为功能全面的**专业级代理平台**，但安全策略过于激进，影响体验。社区关注点偏向于大规模、复杂工作流下的**系统稳定性**。
- **OpenAI Codex**: 依托其强大的模型能力，Qwen Code 正积极向**移动端与桌面端扩展**（Local Control, Remote），并探索复杂工作流的架构统一。社区对**跨平台**（Linux桌面）和**桌面端体验**有较高呼声。
- **Gemini CLI**: 背靠 Google，**测试驱动与工程化**是其特色，如将“组件级评估体系”设为 P1 项目，并主动修复供应链安全漏洞。社区反馈更聚焦于**代理的基础可靠性**。
- **GitHub Copilot CLI**: 深度整合 GitHub 生态，是企业用户的优先选择。当前的主要痛点集中在 **MCP 生态的稳定性与容错**，以及 `/remote` 功能在组织场景下的可用性。
- **OpenCode**: 通过兼容 Claude Code 的 `CLAUDE.md` 和 Skills 来吸引迁移用户，但自身在 **TUI 的基础交互体验**（如复制粘贴）上存在长期未解决的痛点，且其订阅服务（Go）的可靠性受到质疑。
- **Pi**: 社区氛围活跃，**迭代速度快**，有大量来自社区的高质量 PR。定位上偏向**本地优先和高度可扩展**，对 llama.cpp 等本地模型支持较好，但稳定性（TUI渲染、并发竞态）是其主要挑战。
- **Qwen Code**: 发展势头强劲，PR 数量多，正从单会话工具向**多代理、工作流引擎平台**演进。社区关注点在于多会话协调、Web Shell 与 daemon 架构的稳定性。
- **Kimi Code**: 社区规模相对较小，核心诉求集中在**跨会话记忆**和 **ACP 集成稳定性**上，处于功能补全和生态建设阶段。
- **DeepSeek TUI**: 同样处于快速迭代期，社区关注点在于**配置透明度**（compaction行为、provider切换）和 **多 Provider 管理**，中文支持是其独特优势。

### 5. 社区热度与成熟度

- **成熟稳健型**: **Claude Code**、**GitHub Copilot CLI**。用户基数大，讨论深入，但Issue关闭流程僵化（stale标记），修复节奏偏慢。相比“功能数量”，社区更关注“功能质量”和“可靠性”。
- **高速迭代型**: **OpenCode**、**Pi**、**Qwen Code**、**DeepSeek TUI**。PR 活跃，社区贡献度高，Bug 修复速度快。但同时也反映出基础稳定性打磨不足，问题多且杂。其中 **OpenCode** 和 **Pi** 的社区参与度极高，**Qwen Code** 的 PR 量最大。
- **平台扩展型**: **OpenAI Codex**、**Gemini CLI**。社区热度集中于特定的大功能（如Linux支持）或平台级问题，日常讨论相对分散。**Gemini CLI** 的维护者直接介入（如提交Auto Memory相关Issue），表现出对工程质量的高关注度。

### 6. 值得关注的趋势信号

- **“可信赖的代理”成为核心竞争力**：当工具开始承担更多自动化任务时，“说真话”变得比“能力强”更重要。Gemini 的 MAX_TURNS 误报、DeepSeek 的假成功、GitHub Copilot 的静默丢消息等，都是这一趋势下的反面案例。**开发者应优先选择或构建状态透明、可观测性强的工具**。
- **自动化安全与合规的平衡艺术**：Claude Code 的误报和 Gemini Auto Memory 的设计缺陷表明，盲目使用过滤器或设计不当的隐私流程，会严重损害用户体验甚至引发合规风险。**未来的安全机制需要具备可解释性和可配置性**。
- **多代理协作仍是未竟之地**：从 Claude Code 的团队模式到 Gemini 的“代理调用代理”提案，再到 Qwen Code 的协调RFC，行业对多代理协作的前景充满期待，但**状态管理、任务路由、权限传递等基础问题尚未解决**，是未来技术创新的关键突破口。
- **“平台化”与“本地化”的两极分化**：一端是如 Codex、Qwen Code 在积极构建桌面/移动控制面，向“平台”演进；另一端是如 Pi、DeepSeek TUI 等深耕本地模型支持和终端体验，向“个人工具”回归。**对于开发者而言，选择哪种路线取决于对数据隐私、工作流复杂度和平台依赖性的权衡**。
- **存储与资源管理成为不可忽视的运维问题**：Codex 日志的快速增长和会话存储膨胀问题，为所有长时间运行的 AI 工具敲响警钟。**开发者需要建立对这类工具资源占用的监控和清理机制**，否则它们将成为吃磁盘的“隐形黑洞”。

---

## 各工具详细报告

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills 社区热点

> 数据来源: [anthropics/skills](https://github.com/anthropics/skills)

好的，作为一名专注于 Claude Code 生态的技术分析师，根据您提供的 `anthropics/skills` 仓库数据（截止 2026-08-10），我为您生成以下社区热点报告。

---

### 1. 热门 Skills 排行（按 PR 关注度与讨论深度）

**#1. skill-creator 全套修复（关键 Bug）**
- **链接**: [PR #1298](https://github.com/anthropics/skills/pull/1298)
- **功能**: 修复 `run_eval.py` 在 Windows 上的崩溃问题，并解决触发检测机制失效的致命 Bug（#556）。
- **热点**: `skill-creator` 是生成和优化 Skill 的核心工具。PR #1298 指向其核心评估循环（`run_loop.py`）在 Windows 环境下完全失效的问题（`recall=0%`），这意味着优化循环在针对噪音进行优化。此 PR 是社区针对该问题提出的综合性解决方案。
- **状态**: `Open`

**#2. document-typography（文档排版质量）**
- **链接**: [PR #514](https://github.com/anthropics/skills/pull/514)
- **功能**: 防止 AI 生成文档中常见的排版错误（孤行、寡行、编号错位）。
- **热点**: 社区认为该 Skill 精准解决了 AI 生成文档的一个高发痛点，讨论聚焦于其对文档专业度的提升价值。
- **状态**: `Open`

**#3. ODT Skill（OpenDocument 支持）**
- **链接**: [PR #486](https://github.com/anthropics/skills/pull/486)
- **功能**: 支持创建、填充、读取和转换 ODT/ODS 等 OpenDocument 格式文件，并支持解析为 HTML。
- **热点**: 填补了官方仓库对开源办公格式支持的空白，社区对于无缝集成 LibreOffice 工作流表现出高度兴趣。
- **状态**: `Open`

**#4. skill-quality-analyzer & skill-security-analyzer（元技能）**
- **链接**: [PR #83](https://github.com/anthropics/skills/pull/83)
- **功能**: 引入两个"元技能"：一个用于评估 Skill 质量（结构、文档、示例等五维评分），另一个用于扫描 Skill 的安全风险。
- **热点**: 社区关注点集中在生态治理上——如何确保第三方 Skill 的质量与安全性，该 PR 提供了一种自动化解决方案。
- **状态**: `Open`

**#5. testing-patterns（测试模式库）**
- **链接**: [PR #723](https://github.com/anthropics/skills/pull/723)
- **功能**: 涵盖完整测试栈，包括测试哲学（Testing Trophy）、单元测试（AAA 模式）、React 组件测试等指导。
- **热点**: 开发者的核心需求之一。该 Skill 将测试最佳实践直接注入 Claude 的上下文，可显著提升生成测试代码的质量。
- **状态**: `Open`

**#6. color-expert（色彩专家）**
- **链接**: [PR #1302](https://github.com/anthropics/skills/pull/1302)
- **功能**: 提供全面的色彩知识，包括色彩命名系统、色彩空间选择（OKLCH/OKLAB）等。
- **热点**: 社区反馈积极，认为这是目前在 UI/UX 设计和数据可视化领域极具价值的专业性技能，能有效解决 AI 在色彩选择上的痛点。
- **状态**: `Open`

**#7. docx 修复：tracked change w:id 冲突**
- **链接**: [PR #541](https://github.com/anthropics/skills/pull/541)
- **功能**: 修复 DOCX 技能在添加修订记录时与已有书签发生 ID 冲突导致的文档损坏。
- **热点**: 这是一类高价值的小而精的修复，直接解决了 OOXML 交互中的一个隐蔽工程难题，体现了社区对细节质量的追求。
- **状态**: `Open`

---

### 2. 社区需求趋势（来自 Issues）

1.  **安全与信任边界**：社区对"伪装成官方技能"的安全风险感到担忧（[#492](https://github.com/anthropics/skills/issues/492)，43 条评论），同时也在寻求在内部文档（如 SharePoint）中安全使用技能的模式（[#1175](https://github.com/anthropics/skills/issues/1175)）。**这是关注度最高的话题。**
2.  **稳定性与可靠性修复**：`skill-creator` 的评估脚本在特定平台（Windows）和场景下失效的问题（[#556](https://github.com/anthropics/skills/issues/556)、[#1169](https://github.com/anthropics/skills/issues/1169)）是开发者的核心痛点，说明工具链的稳定性亟需提升。
3.  **组织级共享与协作**：随着技能数量的增加，用户希望能在团队或组织内直接共享，而不必手动下载和上传（[#228](https://github.com/anthropics/skills/issues/228)，8 个 👍）。
4.  **上下文窗口优化**：高数量的评论和 Issue 显示，开发者非常关注技能对上下文窗口的占用，避免因注入过多 token 导致任务无法执行（如 [#1487](https://github.com/anthropics/skills/issues/1487) 指出 `claude-api` 注入 156k tokens）。
5.  **专业化垂直技能**：除了通用文档处理，社区开始提出更细分的专业需求，例如**代理治理/安全模式**（[#412](https://github.com/anthropics/skills/issues/412)）和**紧凑记忆管理**（[#1329](https://github.com/anthropics/skills/issues/1329)）。

---

### 3. 高潜力待合并 Skills（近期可能落地）

- **[#1298](https://github.com/anthropics/skills/pull/1298) & [#1050](https://github.com/anthropics/skills/pull/1050) & [#1099](https://github.com/anthropics/skills/pull/1099)**: 这三个 PR 都在解决核心工具 `skill-creator` 在 Windows 上的致命崩溃问题。由于这是开发流程的致命伤，**一旦验证通过，预计会合并其中最优的方案**。
- **[#514](https://github.com/anthropics/skills/pull/514)（document-typography）**: 该议题在 PR 和 Issue 中讨论度高，痛点明确，如果没有重大冲突，**合并可能性较大**。
- **[#486](https://github.com/anthropics/skills/pull/486)（ODT）**: 这是一个功能完整、需求明确的新技能，能为官方仓库补齐生态位，**落地概率较高**。

---

### 4. Skills 生态洞察

当前社区在 Skills 层面最集中的诉求是**提高可维护性、可靠性与安全性**，而非单纯增加新技能的“横向扩张”——开发者们正在从“造轮子”转向“修引擎”，并高度关注 Skill 在组织内分发和运行时的信任与资源边界。

---

# Claude Code 社区动态日报 — 2026-08-10

> 数据来源：github.com/anthropics/claude-code


## 今日速览

昨日无版本发布，社区讨论热度集中于六大类问题：**安全策略误报**占据 Issue 榜半壁江山（云 IAM 管理、随机按键输入等均被安全过滤器误拦）；**流式响应延迟**（慢首字节、180 秒空闲超时）成为高赞 complaint；**Agent 团队模式指针黏滞**、**工具调用解析器静默丢失参数**等影响稳定性问题引发关注。PR 侧，两个修复类 PR（YAML 块标量解析、技能命名规范）值得关注。

> 注：多个 `[Bug][aup]` / `[Bug][cyber]` Issue（#70766–#70824）为同一批次误报，实质为同一问题，下文合并叙述。


## 版本发布

过去 24 小时无新版本发布，当前版本为 CLI 2.1.157（模型 `claude-opus-4-8`，详见 Issue #66095）。


## 社区热点 Issues（Top 10）

本次 50 条更新 Issue 中，约 40 条为 6 月下旬的旧 Issue 被批量标记 `stale` 进入关闭流程。**#61185、#84362、#85095** 三条为本阶段真正值得关注的活跃 Issue。

### 1. #61185 [已关闭] 安全误报：系统审计命令被拦截、上下文污染导致会话恢复失败
- **作者**：Zejzz | **评论 17** | 👍 7 | 标签：`bug`, `platform:linux`, `area:model`
- **摘要**：常规系统审计（sysadmin）命令被执行时被安全机制误判为「网络攻击」；新会话中写操作被错误阻止；安全过滤器的上下文污染破坏了会话恢复能力。
- **重要性**：评论数、点赞数均为全场最高。说明安全过滤器误报已成为社区最集中的痛点；会话恢复（resume）受损直接破坏核心工作流。
- 🔗 [查看 Issue](https://github.com/anthropics/claude-code/issues/61185)

### 2. #66095 [已关闭] 流式响应延迟：慢首字节 + 180 秒空闲超时中断
- **作者**：daira | **评论 6** | 👍 2 | 标签：`platform:linux`, `area:networking`, `api:anthropic`, `stale`
- **摘要**：服务器接受 `/v1/messages` 请求后长时间不发字节，超过 180 秒被客户端看门狗中断。环境：CLI 2.1.157（Opus 4.8）。
- **重要性**：直接影响响应速度与可用性，高赞说明开发者对「慢首字节」体验的密切关注。可惜已标记 `stale`，需关注是否会被重新激活。
- 🔗 [查看 Issue](https://github.com/anthropics/claude-code/issues/66095)

### 3. #84362 [开放] 标签语法解析器静默吸收参数块 — 6.2% 参数流失
- **作者**：isaac-ranger | **评论 4** | 👍 0 | 标签：无（新 Issue）
- **摘要**：工具调用的 tag-grammar 解析器在模型输出不匹配/畸变的闭合标签时，会将后续参数块「吸收」进前一个字符串字段，导致参数无法绑定，调用**静默成功但数据丢失**（实测 6.2%）。
- **重要性**：**当前最值得关注的活跃 Issue**。静默数据丢失比显式报错更危险——可能引发错误决策。原 Issue #44826 曾被关闭，此次重提，社区持续关注。
- 🔗 [查看 Issue](https://github.com/anthropics/claude-code/issues/84362)

### 4. #85095 [开放] Plan 模式静默退出，ExitPlanMode 被当作普通工具结果
- **作者**：V-Pridhvi | **评论 4** | 👍 0 | 标签：`bug`
- **摘要**：Plan 模式中，Agent 未经过显式确认流程即退出，并将 `ExitPlanMode` 当作普通工具结果处理，可能绕过计划评审。
- **重要性**：涉及工作流完整性——若 Plan 模式可被静默绕过，用户对计划的审查将失去意义。
- 🔗 [查看 Issue](https://github.com/anthropics/claude-code/issues/85095)

### 5. #64550 [已关闭] Agent 团队：lead 指针黏滞，路由错误
- **作者**：suhang56 | **评论 5** | 标签：`platform:windows`, `area:agents`, `stale`
- **摘要**：长时间/压缩会话后，team-lead 的「活跃代理」指针停留在队友身上，导致 lead 以队友身份路由、子代理创建失败（“Teammates cannot spawn other teammates”）。
- **重要性**：Agent 团队（多代理协作）是未来方向，状态错乱将导致整条团队链失效。
- 🔗 [查看 Issue](https://github.com/anthropics/claude-code/issues/64550)

### 6. #42138 [已关闭] Telegram 插件：MCP 入站通知未注入会话
- **作者**：Pampidu | **评论 8** | 👍 1 | 标签：`bug`, `stale`
- **摘要**：Telegram 插件接收的入站 MCP 通知（`notifications/claude/channel`）没有进入当前会话上下文，命令如 `/telegram` 可能因此失效。
- **重要性**：社区关注度第 4 高；插件生态是扩展 Claude Code 的关键路径，此类问题影响集成体验。
- 🔗 [查看 Issue](https://github.com/anthropics/claude-code/issues/42138)

### 7. 安全策略误报 — 多个 Issue（#70773、#70796、#70790 等，均 [已关闭]）
- **作者**：sworrl（同一用户提交了 15+ 条同批次误报）| 标签：`platform:linux`, `area:model`, `area:security`, 大量 `duplicate`/`stale`
- **典型场景**：① 云 IAM 租户管理操作（枚举域名、IAM 加固）被 cyber 过滤器拦截；② 纯随机按键输入（“ASDF”）被误判为网络安全话题；③ 只读 IR 邮箱排查 + 凭据加固被阻止；④ PII 脱敏脚本被拦。
- **重要性与社区反应**：虽是重复/已关闭，但**数量庞大且高度重复**，强烈暗示 AI 安全过滤器存在**术语误判**问题：将「枚举」「IAM」「加固」等安全术语与攻击行为混淆。用户在授权、合法的工作域中被反复打断。
- 🔗 [#70773](https://github.com/anthropics/claude-code/issues/70773) | [#70796](https://github.com/anthropics/claude-code/issues/70796) | [#70790](https://github.com/anthropics/claude-code/issues/70790) | [#70772](https://github.com/anthropics/claude-code/issues/70772) | [#70824](https://github.com/anthropics/claude-code/issues/70824)

### 8. #69033 [已关闭] 工作流编排：子代理扇出时缺少内存感知的节流
- **作者**：spitfire94 | **评论 3** | 👍 1 | 标签：`enhancement`, `perf:memory`, `area:agents`, `stale`
- **摘要**：大型工作流扇出（deep-research，84–92 个子代理）导致主机 OOM、终端崩溃。并发上限是**基于数量**（`min(16, cores-2)`），**不考虑内存**。
- **重要性**：高赞说明开发者认可。在资源受限环境（CI、云开发机）中，「数量并发 + 内存不感知」的设计过于粗糙。
- 🔗 [查看 Issue](https://github.com/anthropics/claude-code/issues/69033)

### 9. #69952 [已关闭] `--resume` 失败：账户权限重置后找不到会话（macOS）
- **作者**：apolednik | **评论 3** | 标签：`platform:macos`, `area:core`, `stale`
- **摘要**：账户权限重置后，`--resume` 报「No conversation found」，但本地会话文件完好。
- **重要性**：账户/权限变动后的会话恢复是高频场景，目前无法复用本地会话。
- 🔗 [查看 Issue](https://github.com/anthropics/claude-code/issues/69952)

### 10. #70773 [已关闭] 自动模式分类器拒绝 — 长期 watcher 自动提交批量误报
- **作者**：sworrl | **评论 5** | 标签：`area:permissions`, `stale`
- **摘要**：Claude Code 的自动模式分类器拒绝了一个合法操作；用户试图通过「长期运行的 watcher 自动提交误报」来缓解。
- **重要性**：反映用户的**挫败感**——误报频率过高，以至于需要自动化工具来批量上报，侧面说明误报问题的严重性。
- 🔗 [查看 Issue](https://github.com/anthropics/claude-code/issues/70773)


## 重要 PR 进展

昨日共 3 个 PR 更新，均为插件/技能相关。

### 1. #85323 [开放] 修复插件开发：正确解析块标量（Block Scalar）的 Agent 描述
- **作者**：erichanwang | 创建/更新：2026-08-09
- **内容**：修复 #83803 遗留的 YAML 块标量解析缺陷。`validate-agent.sh` 现在从缩进内容测量多行 `description: |` / `description: >` 值，而非将标量标记当作整个描述。
- **影响**：解决 `AGENTS.md` 中多行描述的解析错误，提升 Agent 配置可靠性。
- 🔗 [查看 PR](https://github.com/anthropics/claude-code/pull/85323)

### 2. #85243 [开放] 技能（Skills）名称改为符合规范
- **作者**：bechor25 | 创建/更新：2026-08-09
- **内容**：8 个内置技能使用含空格的大小写混合 `name:`（如 `Writing Hookify Rules`、`Agent Development`），不符合规范。统一改为规范形式。
- **影响**：提升技能生态的一致性与兼容性。
- 🔗 [查看 PR](https://github.com/anthropics/claude-code/pull/85243)

### 3. #17395 [已关闭] 新增 `agent-session-commit` 插件：迭代维护 `AGENTS.md`
- **作者**：Olshansk | 创建：2026-01-10，更新：2026-08-09
- **内容**：将 `AGENTS.md` 设为权威项目指令文件，`CLAUDE.md` 改为最小化指针；支持手动 `/session-commit` 与 Stop hook 自动触发。
- **意义**：**1 月创建，8 月才被更新/关闭**，说明项目组仍在评估；`AGENTS.md` 生态的迭代维护是社区关心的方向。
- 🔗 [查看 PR](https://github.com/anthropics/claude-code/pull/17395)


## 功能需求趋势

从近期 Issues 中可提炼出以下社区关注方向：

1. **AI 安全过滤器的可解释性与可配置性** — 误报场景集中在：安全术语误判（IAM/枚举）、无意义输入误判（随机按键）、合法管理员操作（加固、审计）被拦截。**强烈呼吁**：提供过滤器解释、敏感性调节、关闭选项、申诉渠道。
2. **流式响应性能优化** — 「慢首字节 + 180 秒空闲超时」组合严重影响长任务的感知速度，开发者期望更快的首帧与更宽容的空闲阈值。
3. **多代理协作稳定性** — Agent 团队（Teams）中「lead 与 teammate 路由态混淆」、子代理无法递归创建、内存感知的并发节流（避免 OOM）。
4. **会话恢复（Resume）的韧性** — 账户/权限变化导致会话不可恢复；需保证本地会话文件的复用能力。
5. **插件与工具生态的可靠性** — Telegram/MCP 入站通知需正确注入对话上下文；YAML 解析、技能命名规范等基础能力保障。

## 开发者关注点

1. **安全过滤器误报已到「规模化」程度** — 同一用户一次性提交 15+ 条误报，说明**误报率已严重到影响日常工作流**，亟需根本性改进（而非逐条修复）。
2. **「静默」类问题比报错更可怕** — 工具调用参数静默丢失（#84362）、Plan 模式静默退出（#85095），这类问题会让开发者对输出产生「错误的信任」，建议优先排查与修复。
3. **旧 Issue 批量关闭引发「流程疲劳」** — 大量 `[stale]` 关闭提示：活跃 Issue 从创建到关闭约 1.5–2 个月，修复节奏偏慢，开发者需持续跟进并重新提起（如 #84362 正是 re-raise）。建议：关注新提交的、未标记 `stale` 的活跃 Issue 更有效。
4. **对高赞 `enhancement` 建议接受度高** — #69033（内存感知节流）获 👍 1、#66095（流式响应）获 👍 2，说明社区对「工程稳健性」类改进呼声较高，可作为产品路线参考。

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# 🤖 OpenAI Codex 社区动态日报

**日期：2026-08-10** | 数据来源：[github.com/openai/codex](https://github.com/openai/codex)

---

## 今日速览

今日无新版本发布，社区讨论持续聚焦在 **Codex Desktop 跨平台支持**（Linux 桌面端需求呼声高涨，获赞 945 次）与 **Windows 端计算机操作（Computer Use）稳定性问题**两大方向。此外，多个与 TUI 交互体验、会话存储膨胀相关的 Bug 报告和修复 PR 同步推进，开发节奏稳健。

---

## 社区热点 Issues（Top 10）

### 🔥 1. Codex Desktop Linux 版本需求（持续高热）
- **Issue**: [#11023](https://github.com/openai/codex/issues/11023) | 评论 205 | 👍 945
- **作者**: Suhaibinator | 状态: OPEN
- **要点**: 因 macOS 端存在功耗问题（[#10432](https://github.com/openai/codex/issues/10432)），用户强烈期待 Linux 桌面版。**已连续 6 个月保持极高热度**，是当前社区第一大需求。

### 🔥 2. Windows 端 Computer Use 功能受阻
- **Issue**: [#37383](https://github.com/openai/codex/issues/37383) | 评论 10 | 👍 4
- **作者**: dystopia78 | 状态: OPEN
- **要点**: 应用/窗口发现阶段报错 `0x80070003`，Windows 11 Pro 25H2 环境下无法使用 Computer Use。**同一时间段内还有 [#37281](https://github.com/openai/codex/issues/37281)（`node_repl exec context not found`）在报告同类问题**，表明 Windows 端该功能上线初期仍不稳定。

### 📊 3. 自定义状态栏（Status Line）需求
- **Issue**: [#17827](https://github.com/openai/codex/issues/17827) | 评论 39 | 👍 150
- **作者**: pkondaurov | 状态: OPEN
- **要点**: 对标 Claude Code，希望 TUI 底部可显示 token 用量、模型名、速率限制、上下文窗口、git 分支等实时信息。

### 🔥 4. 桌面端 Crashpad 日志无限膨胀
- **Issue**: [#25921](https://github.com/openai/codex/issues/25921) | 评论 16 | 👍 7
- **作者**: Jolg42 | 状态: OPEN
- **要点**: 崩溃日志目录 `~/Library/Application Support/com.openai.codex/web/Crashpad/pending` **以每天 +5GB（54,504 个文件）的速度增长**，严重消耗磁盘空间，属于高危存储类 Bug。

### 📱 5. 移动端无法显示 SSH 远程项目
- **Issue**: [#23527](https://github.com/openai/codex/issues/23527) | 评论 13 | 👍 19
- **作者**: jameBoy | 状态: OPEN
- **要点**: Mac 主机可正常接入 SSH 远程项目，但 ChatGPT 移动端同步时无法看到这些项目，远程工作流出现断层。

### ⚙️ 6. 自动压缩后 Agent 陷入死循环
- **Issue**: [#34322](https://github.com/openai/codex/issues/34322) | 评论 3 | 👍 2
- **作者**: villagestonehouse | 状态: OPEN
- **要点**: 上下文自动优化（auto-compact）后，Agent 反复进入 resume 循环，严重破坏会话连续性。

### 🪟 7. Windows 桌面端 Work 页面持续闪烁
- **Issue**: [#34299](https://github.com/openai/codex/issues/34299) | 评论 5 | 👍 0
- **作者**: mengxi0830-prog | 状态: OPEN
- **要点**: 更新至 26.715.31925 后，Work 页面在 Windows 11 25H2 上持续闪烁。**同类问题在 [#34351](https://github.com/openai/codex/issues/34351)（Insider Build）和 [#35101](https://github.com/openai/codex/issues/35101)（macOS Tahoe）上也有报告**，疑似为跨平台渲染回归。

### 📂 8. Git Worktree 下 hooks.json 被静默忽略
- **Issue**: [#27133](https://github.com/openai/codex/issues/27133) | 评论 7 | 👍 2
- **作者**: yaodiff | 状态: OPEN
- **要点**: 在 git worktree 中运行时，项目级 `.codex/hooks.json` 完全不生效，钩子机制跨场景一致性受影响。

### 💾 9. 会话存储可膨胀至数百 GiB
- **Issue**: [#34337](https://github.com/openai/codex/issues/34337) | 评论 2 | 👍 1
- **作者**: fengjikui | 状态: OPEN
- **要点**: CLI 与 Desktop 共享的本地 rollout/session 存储，在长时间运行时**可静默增长至百 GiB 甚至 TiB 级**，需引起存储管理重视。

### 🔌 10. Windows 端远程控制无法启动
- **Issue**: [#30372](https://github.com/openai/codex/issues/30372) | 评论 3 | 👍 2
- **作者**: hiwuhuazhang-ops | 状态: OPEN
- **要点**: Windows 上 CLI 报告 daemon 生命周期为 Unix-only，**Codex 移动端远程控制功能完全不可用**，跨平台能力受损。

---

## 重要 PR 进展（Top 10）

> 今日 7 条 PR 全部来自 `copyberry[bot]` 的自动化更新（**无人工提交**），风格偏向内部重构与可观测性建设。

### ✅ 1. [#37723](https://github.com/openai/codex/pull/37723) — 会话配置导入失败增加 I/O 错误子类型
- **状态**: 已合并（CLOSED）
- **内容**: 为 `failed_to_load_session_config` 增加稳定的 `std::io::ErrorKind` 分类（`invalid_data`、`not_found`、`permission_denied`），**提升排障定位效率**。

### ✅ 2. [#37709](https://github.com/openai/codex/pull/37709) — 修复 TUI 输入框换行空白异常
- **状态**: 已合并（CLOSED）
- **内容**: 修复 composer 中溢出空白独占一行的问题，文本换行更自然（grapheme-safe），提升输入体验。

### ✅ 3. [#37654](https://github.com/openai/codex/pull/37654) — 声明环境配置读取能力
- **状态**: 已合并（CLOSED）
- **内容**: exec-server 环境能力新增 `environmentConfigRead`，**对旧执行器默认关闭以保持兼容**。

### ✅ 4. [#37645](https://github.com/openai/codex/pull/37645) — 插件安装失败分析增强
- **状态**: 已合并（CLOSED）
- **内容**: 远程仓库、变更集、包下载失败均增加 HTTP 状态子类型，便于**区分可操作的失败原因**。

### ✅ 5. [#37644](https://github.com/openai/codex/pull/37644) — 钩子处理器执行逻辑泛化
- **状态**: 已合并（CLOSED）
- **内容**: 按 handler kind 统一路由至 hooks 引擎，保留命令钩子行为；拒绝无法用 TOML 表示（如 `null`）的 MCP 工具输入，**增强信任哈希可靠性**。

### ✅ 6. [#37641](https://github.com/openai/codex/pull/37641) — 命令审批前缀规则改用步骤上下文
- **状态**: 已合并（CLOSED）
- **内容**: 从活动 step 上下文中读取 `allow_prefix_rules`，用于 exec 策略选择和审批请求构建，**规则判断更精确**。

### 🤖 7. [#31817](https://github.com/openai/codex/pull/31817) — 自动更新 models.json
- **状态**: 仍开启
- **内容**: bot 例行更新，无实质变更。

---

## 功能需求趋势

| 方向 | 代表 Issue | 热度 |
|------|-----------|------|
| **Linux 桌面端支持** | [#11023](https://github.com/openai/codex/issues/11023) | 🔥🔥🔥 极高（945👍） |
| **TUI 可定制状态栏** | [#17827](https://github.com/openai/codex/issues/17827) | 🔥🔥 高（150👍） |
| **TUI 内嵌微编辑器** | [#36711](https://github.com/openai/codex/issues/36711) | 低、新方向 |
| **持久化角色化 AI 团队** | [#37736](https://github.com/openai/codex/issues/37736) | 低、Web 端扩展 |
| **自动任务补跑策略** | [#24327](https://github.com/openai/codex/issues/24327) | 中 |

**核心结论**：① 桌面端生态扩展（Linux）是社区最大诉求；② TUI 的"可配置性"正在成为刚需；③ Web/移动端与桌面端的无缝协作是持续关注点。

---

## 开发者关注点

### 🚨 痛点问题（高频）

1. **Windows 端 Computer Use 不可用**：多个 Issue 反映该功能在窗口发现和控制阶段即崩溃（`0x80070003`、`node_repl exec context not found`），功能上线初期体验较差。

2. **桌面端渲染闪烁回归**：Windows 与 macOS 平台均有用户报告 Work 页面持续闪烁，**跨平台 UI 稳定性存疑**。

3. **存储空间失控**：
   - Crashpad 日志每天 +5GB（[#25921](https://github.com/openai/codex/issues/25921)）
   - 会话 rollout 可膨胀至 TiB 级（[#34337](https://github.com/openai/codex/issues/34337)）
   - `logs_2.sqlite` 即使设置 10 天保留也不回收空间（[#35823](https://github.com/openai/codex/issues/35823)）

4. **远程控制功能 Windows 缺失**：daemon 生命周期仅支持 Unix（[#30372](https://github.com/openai/codex/issues/30372)），Windows 用户完全无法使用移动端远程控制。

5. **会话恢复体验受损**：打开聊天有 5 秒固定超时等待（[#37398](https://github.com/openai/codex/issues/37398)）；auto-compact 导致 Agent 陷入死循环（[#34322](https://github.com/openai/codex/issues/34322)）；远程线程报 `already has an active writer`（[#37403](https://github.com/openai/codex/issues/37403)）。

6. **Hook 机制不一致**：worktree 中 hooks.json 被忽略（[#27133](https://github.com/openai/codex/issues/27133)）；PreToolUse deny 对 `apply_patch` 不生效（[#27833](https://github.com/openai/codex/issues/27833)），**权限控制可靠性需加强**。

### 📌 高频需求归纳

- **安全性**：hook 权限约束必须严格执行
- **可靠性**：日志与存储增长必须可控
- **跨平台**：Linux 桌面端 + Windows 远程控制是"两极"
- **可配置性**：TUI 状态栏、输入提示等需要开放配置接口

---

*本日报由 AI 自动生成，数据截至 2026-08-10。如发现信息遗漏，欢迎在评论区补充。* 📮

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI 社区动态日报 — 2026-08-10

> 数据来源：github.com/google-gemini/gemini-cli


## 今日速览

昨日的社区讨论集中在**子代理（Subagent）的可靠性问题**——多个长期悬而未决的高优先级 Bug（如子代理挂起、MAX_TURNS 误报成功）正在密集推进重测。同时，**Auto Memory 系统的安全与质量缺陷**成为新的关注焦点，三个相关 Issue 均在持续更新中。PR 侧，一项修复 ACP 会话恢复逻辑的关键 PR 已提交。

## 版本发布

- **[v0.56.0-nightly.20260809.gcf22ac7e8](https://github.com/google-gemini/gemini-cli/releases/tag/v0.56.0-nightly.20260809.gcf22ac7e8)** — 常规 nightly 版本，包含最新的功能与修复，完整变更见 [Changelog](https://github.com/google-gemini/gemini-cli/compare/v0.56.0-nightly.20260808.gcf22ac7e8...v0.56.0-nightly.20260809.gcf22ac7e8)。


## 社区热点 Issues（Top 10）

### 1. Subagent 恢复被误报为成功 🔥
- **#22323** · [Subagent recovery after MAX_TURNS is reported as GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323) · `P1` · `kind/bug` · 评论 12
- **问题**：`codebase_investigator` 子代理在达到最大轮次限制后，系统报告 `status: "success"` 且 `Termination Reason: "GOAL"`，掩盖了实际的中断。
- **影响**：这是一个高优先级、创建近 5 个月仍未被关闭的 P1 Bug。它直接**破坏了用户对代理状态的信任**——系统显示"成功"，但实际上分析从未执行。错误的状态报告可能导致用户基于不完整的信息做出错误决策。

### 2. 通用代理无限期挂起
- **#21409** · [Generalist agent hangs](https://github.com/google-gemini/gemini-cli/issues/21409) · `P1` · `kind/bug` · 评论 8 · 👍 8
- **问题**：当 Gemini CLI 将任务委托给通用代理时（即使是最简单的文件夹创建），代理会无限期挂起，用户最长等待 1 小时。
- **影响**：社区对该问题反馈强烈（👍 8 为当前列表最高）。这是一个严重影响日常使用的问题——任何需要子代理的简单操作都会卡死。虽然社区已发现"指示模型不要使用子代理"可绕过，但这显然不是可持续的解决方案。

### 3. 组件级评估体系建设
- **#24353** · [Robust component level evaluations](https://github.com/google-gemini/gemini-cli/issues/24353) · `P1` · 评论 7
- **内容**：该 EPIC 追踪行为评估测试的扩展工作——目前已有 76 个测试覆盖 6 个 Gemini 模型，目标是构建更健壮的组件级评测体系。
- **影响**：这是维护者主导的基础设施项目，直接关系到 Gemini CLI 各模型版本的质量保障能力。

### 4. AST 感知工具可行性评估
- **#22745** · [Assess the impact of AST-aware file reads, search, and mapping](https://github.com/google-gemini/gemini-cli/issues/22745) · `P2` · `kind/feature` · 评论 7
- **内容**：这是一个 EPIC，追踪 AST（抽象语法树）感知的文件读取/搜索/代码库映射工具是否值得投入。
- **影响**：如果此评估通过，引入 AST 工具可显著减少令牌消耗和轮次（如精确定位方法边界），并改善浏览大代码库时的导航体验。同时关联的 **#22746** 建议从 tilth 或 glyph 项目入手。这代表着长时间来看的底层能力升级。

### 5. 模型不自发使用自定义技能与子代理
- **#21968** · [Gemini does not use skills and sub-agents enough](https://github.com/google-gemini/gemini-cli/issues/21968) · `P2` · `kind/bug` · 评论 6
- **问题**：用户反馈，Gemini 几乎**不会主动**使用用户自定义的 skills 和 sub-agents，除非被明确指示。
- **影响**：这是一个核心的产品质量问题——如果模型不主动使用这些优化工具，用户配置它们的动力就会大打折扣。

### 6. Shell 命令执行完成后挂起
- **#25166** · [Shell command execution gets stuck with "Waiting input"](https://github.com/google-gemini/gemini-cli/issues/25166) · `P1` · `kind/bug` · 评论 4 · 👍 3
- **问题**：极简单的 CLI 命令执行完成后，终端仍显示"正在等待输入"并挂起。
- **影响**：另一个 P1 级别的高频阻塞问题（👍 3）。系统会误判命令状态，导致整个会话卡死，必须手动干预。

### 7. 浏览器代理在 Wayland 环境失败
- **#21983** · [browser subagent fails in wayland](https://github.com/google-gemini/gemini-cli/issues/21983) · `P1` · `kind/bug` · 评论 4
- **问题**：浏览器子代理在 Wayland 显示服务器协议下直接失败。
- **影响**：Linux 用户群体中 Wayland 的使用率持续上升，这对该用户群体是硬伤。

### 8. Auto Memory 无限重试低信号会话
- **#26522** · [Stop Auto Memory from retrying low-signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522) · `P2` · `kind/bug` · 评论 5
- **问题**：Auto Memory 的提取程序对低信号会话会无限重试——只有成功读取才会标记为已处理。
- **影响**：这可能导致后台服务陷入死循环，浪费计算资源。来自维护者的自查 Issue，表明团队在主动加固该新功能。

### 9. Auto Memory 安全缺陷：先发送后脱敏
- **#26525** · [Add deterministic redaction and reduce Auto Memory logging](https://github.com/google-gemini/gemini-cli/issues/26525) · `P2` · 评论 4
- **问题**：Auto Memory 在读取本地转录后，**先将内容发送给模型，然后才在提示词中要求脱敏**。同时服务可能记录已有的敏感技能。
- **影响**：这是一个安全隐私问题。当前设计中秘密信息已进入模型上下文后才执行脱敏，这在合规要求下是不可接受的。值得密切关注其修复进度。

### 10. 自定义代理 symlink 不被识别
- **#20079** · [~/.gemini/agents/filename.md is not recognized if it is a symlink](https://github.com/google-gemini/gemini-cli/issues/20079) · `P2` · `kind/bug` · 评论 4
- **问题**：当 `~/.gemini/agents/` 下的代理文件是 symlink 时，不会被系统识别。
- **影响**：使用 dotfiles 管理仓库管理配置的用户（通过 symlink 链接）会受影响，阻碍了配置的版本化管理。

> **说明**：有数个与 Auto Memory 安全/质量相关的 Issue（#26516、#26523）同为维护者 SandyTao520 创建，暗示一次有组织的功能加固，值得关注后续合并。


## 重要 PR 进展（Top 10）

### 1. 修复 ACP 会话恢复被"毒化" 🚀
- **#28744** · [fix(acp): don't start a fresh chat before resuming, it poisons the session file](https://github.com/google-gemini/gemini-cli/pull/28744) · `P1` · `area/core`
- **问题**：`loadSession` 在恢复会话前调用了 `geminiClient.initialize()`，这个调用会**无意识地启动一个新会话**，从而污染目标会话文件。PR 旨在修复这一陷阱，为 ACP 集成扫清障碍。

### 2. 允许子代理调用子代理
- **#28738** · [Allow agents to call agents](https://github.com/google-gemini/gemini-cli/pull/28738) · `P2` · `area/agent` · `help wanted`
- **内容**：通过 `tools:` frontmatter 允许子代理委派给其他子代理，甚至递归调用自身，修复 #22092。
- **意义**：这是**Agent 组合能力**的重要增强，但功能复杂且标注了 `help wanted`，社区参与需谨慎。

### 3. 保留模型配置中的 systemInstruction 与 tools
- **#28743** · [fix(core): preserve resolved model config systemInstruction and tools](https://github.com/google-gemini/gemini-cli/pull/28743) · `area/agent`
- **内容**：修复 `sendMessageStream()` 中已解析的 `systemInstruction` 和 `tools` 被会话级变量覆盖的问题。
- **影响**：直接影响自定义模型行为配置的准确性，属于核心逻辑修复。

### 4. 策略引擎多项关键修复
- **#26540** · [fix(core): resolve policy engine bugs affecting tool approvals](https://github.com/google-gemini/gemini-cli/pull/26540) · `P1` · 🔒 maintainer only
- **内容**：修复正则匹配的 null-byte 缺陷，解决 YOLO/AUTO_EDIT 模式下的过度审批提示。
- **影响**：对使用宽松权限模式（YOLO）的用户体验有显著改善，但处于长时间未合并状态，进展待观察。

### 5. 修复 eval-pr 工作流的供应链 RCE ⚠️
- **#28740** · [fix(security): prevent supply chain RCE in eval-pr workflows](https://github.com/google-gemini/gemini-cli/pull/28740) · `area/security` · `size/l`
- **内容**：拆分 `pull_request_target` 工作流为两步，防止不受信任的 fork 代码在特权上下文中执行（修复 #28336）。
- **意义**：这是一个**供应链安全关键修复**，消除了一个可被利用的远程代码执行漏洞。

### 6. 更新 .gitignore 忽略 .env 文件
- **#28619** · [Update .gitignore to ignore .env and .ai files; add unit tests](https://github.com/google-gemini/gemini-cli/pull/28619) · `P1` · 已关闭
- **内容**：将 `.env` 和 `.ai` 文件加入 `.gitignore` 并添加测试。该 PR 已被关闭，是否被采纳需要进一步确认。

### 7. 披露 MCP Plan Mode 只读状态的信任边界
- **#28549** · [fix(mcp): disclose that Plan Mode read-only status is a server claim](https://github.com/google-gemini/gemini-cli/pull/28549) · `area/security` · `size/m`
- **问题**：`readOnlyHint` 注解是 MCP 服务器的自声明，未经 CLI 验证，却被用来提升 Plan Mode 中的工具权限。
- **意义**：改善透明性，指出 "read only" 仅是基于服务器的自声明。

### 8. 修复 caretaker-agent 技能命名规范
- **#28742** · [fix(caretaker-agent): use spec-valid names for two triage-worker skills](https://github.com/google-gemini/gemini-cli/pull/28742) · `size/s` · 状态 `need-issue`
- **内容**：将 `code_explorer` 和 `spec_generator` 中的下划线改为符合 Agent Skills 规范的连字符命名。

### 9. 用 debugLogger 替换直接 console.error
- **#28613** · [fix: replace console.error with debugLogger in sdk session](https://github.com/google-gemini/gemini-cli/pull/28613) · `size/xs` · 状态 `need-issue`
- **内容**：将 `session.ts` 中的直接 `console.error` 调用替换为项目标准的 `debugLogger`，属于小幅改动但贴合项目日志规范。

### 10. Nightly 版本自动升级
- **#28739** · [chore/release: bump version to 0.56.0-nightly.20260809.gcf22ac7e8](https://github.com/google-gemini/gemini-cli/pull/28739) · 机器人自动 PR
- **内容**：常规 nightly 版本号更新。


## 功能需求趋势

1. **代理自主性与可靠性**：社区对子代理挂起（#21409）、不使用自定义技能（#21968）、误报执行状态（#22323）等问题高度关注，希望代理在策略范围内自主规划执行，且**如实**报告执行状态。
2. **子代理的可见性与协作**：希望子代理轨迹可通过 `/chat share` 分享（#22598）、子代理可互相调用（#22092 / PR #28738），增加对多代理系统的需求。
3. **Auto Memory 与长期记忆**：5 月 5 日由维护者集中提交，包括低信号会话重试（#26522）、无效补丁处理（#26523）、记忆质量提升（#26516）及安全脱敏（#26525），意图将这一功能打磨为稳定产物。
4. **代码理解能力**：评估引入 AST 感知工具（#22745、#22746），优化代码阅读与检索效率。
5. **配置灵活性与生态兼容**：支持 symlink 代理（#20079）、设置覆盖生效（#22267），以及用户自定义 skills 与子代理被模型自动采用（#21968）。
6. **安全与权限边界**：供应链 RCE 修复（#28740）、MCP 只读提示透明化（#28549），以及对模型潜在破坏性命令（`git reset --force`，#22672）的限制。


## 开发者关注点

**1. 子代理的稳定性是最大痛点。** 多个 P1 级别的子代理相关 Bug（挂起、误报成功、Wayland 下崩溃）至今长时间未关闭，说明这一领域的工程质量尚未达到稳定水平。大量 Issue 被标记为 `status/need-retesting` 和 `🔒 maintainer only`（属于维护者内部流程），暗示正在集中处理但仍未解决。

**2. 权限与控制预期不一致。** 有用户反馈 v0.33.0 起子代理在配置为禁用时仍被调用（#22093），另有对 `git reset`/`--force` 等危险命令的执行担忧（#22672），说明当前权限系统（policy engine）与实际控制预期存在差距。

**3. Auto Memory 的安全设计引发警觉。** 提取流程中"先入上下文、再脱敏"的设计缺陷（#26525）在敏感环境有合规风险，开发者们会关注其最新动态。

**4. 新功能场景值得关注。** "允许代理调用代理"（PR #28738）的设计若能落地，将为复杂任务编排带来更大的想象空间，但该 PR 标有 `help wanted`，需要评估其成熟度。

**5. `status/need-retesting` 类目变化频繁。** 多条热点 Issue 标记此状态，开发者可主动提供测试反馈，加速问题解决进程。

---
*本日报由 AI 自动生成，数据截至 2026-08-10，仅代表数据来源展示的信息供技术参考。*

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI 社区动态日报

**日期：2026-08-10**


## 今日速览

昨日社区提交量激增，但绝大多数为 triage 阶段的待分类问题，覆盖 MCP 基础设施稳定性、模型可用性以及并行工具调用中的严重缺陷。与此同时，多个长期悬而未决的 issue 出现新讨论，尤其是 `/remote` 命令在组织仓库中的失败问题，值得团队关注。

## 版本发布

过去 24 小时内无新版本发布。


## 社区热点 Issues

### 1. `/remote` 在组织仓库中报错，远程会话功能受阻
**#2751** | 👍 13 | 💬 8 | 状态：OPEN
在 v1.0.28 中，对组织拥有的仓库执行 `/remote` 命令时报错 `Remote session disabled: could not resolve repository`。该问题直接影响企业用户的远程协作核心功能，且持续近四个月未修复，社区关注度持续走高，是当前最影响企业用户体验的阻塞性问题之一。
🔗 https://github.com/github/copilot-cli/issues/2751

### 2. 无法取消已排队的消息
**#1857** | 👍 26 | 💬 9 | 状态：OPEN
当 agent 忙碌或执行 `/compact` 时，用户无法撤销已通过 `Ctrl+Q`/`Ctrl+Enter` 排队的消息或斜杠命令。该问题被认为是输入控制的核心体验缺陷，获得 26 个 👍，说明用户对操作可控性的需求强烈。
🔗 https://github.com/github/copilot-cli/issues/1857

### 3. Anthropic 请求缺少 cache_control 断点，导致长上下文重复计费
**#4256** | 👍 3 | 💬 2 | 状态：CLOSED
请求未设置 `cache_control` 断点，导致系统提示词、工具定义等固定上下文被反复处理，成本与延迟双高。该问题已关闭，但社区对 Token 成本优化的需求值得持续关注。
🔗 https://github.com/github/copilot-cli/issues/4256

### 4. MCP 初始化握手硬编码 60 秒超时且无重试
**#4421** | 👍 0 | 💬 0 | 状态：OPEN
`initialize` 握手预算固定 60 秒，超时后该 MCP server 在整个会话中不再重试，导致 `npx` 启动的 stdio 服务器约有 29% 的会话直接失败且无法恢复。对依赖 MCP 生态的用户而言，这是高优稳定性缺陷。
🔗 https://github.com/github/copilot-cli/issues/4421

### 5. Prompt 被静默丢弃：新会话工作区已创建但 Agent 未收到消息
**#4423** | 👍 0 | 💬 0 | 状态：OPEN
从 App 创建新会话并传入初始 Prompt 时，git worktree 和分支均创建成功，但 kickoff prompt 未被送达 Agent，会话永久空闲且无任何报错。属于典型的“静默失败”，排查困难，对自动化工作流影响严重。
🔗 https://github.com/github/copilot-cli/issues/4423

### 6. 并行工具调用响应顺序错乱，Agent 状态混乱
**#4420** | 👍 0 | 💬 0 | 状态：OPEN
harness 在并行工具调用时无法保持请求与响应的关联性，导致 Agent 收到错配的响应而产生逻辑混乱。该问题直指 agent 可靠性的底层缺陷，可能影响所有涉及并行 task 调用的复杂任务。
🔗 https://github.com/github/copilot-cli/issues/4420

### 7. 个人企业账号下所有 Claude 模型不可用
**#4422** | 👍 0 | 💬 0 | 状态：OPEN
用户反馈此前可正常使用的 Claude 模型（sonnet 5、4.8 等）今日起全部报 `This model is disabled by your organization`，且回滚版本无效，疑似服务端配置变更导致。
🔗 https://github.com/github/copilot-cli/issues/4422

### 8. MCP 托管策略临时空列表导致用户服务器被永久拉黑
**#4419** | 👍 0 | 💬 0 | 状态：OPEN
在解析托管设置期间，CLI 安装了临时的“拒绝一切”MCP 策略（`[[]]`），任何在该窗口内注册的用户 MCP server 都会被永久拒绝，且该问题在无托管策略的账号上亦可复现。
🔗 https://github.com/github/copilot-cli/issues/4419

### 9. Auto-mode 模型选择范围受限，缺少灵活配置
**#4411** | 👍 0 | 💬 1 | 状态：CLOSED（标记为 invalid）
用户希望 Auto-mode 支持自定义模型强度范围与偏好，但该 issue 被标记为 invalid 关闭。
🔗 https://github.com/github/copilot-cli/issues/4411

### 10. 并行 explore 子 Agent 触发模型级 429 限流，无降级策略
**#4416** | 👍 0 | 💬 0 | 状态：OPEN
并行启动多个子 Agent 时，所有 `explore` Agent 默认使用同一轻量模型，导致该模型触发限流，且无退避重试或自动切换机制。
🔗 https://github.com/github/copilot-cli/issues/4416


## 重要 PR 进展

过去 24 小时内无新 PR 或更新。


## 功能需求趋势

从近期 Issue 中可提炼出以下社区关注方向：

### 1. 本地化（i18n）
**#4407** 请求为桌面端与 CLI 添加中文（zh-CN）界面，表明 GitHub Copilot 的用户群体已明显全球化，界面语言支持成为协作工具的基础配置项。

### 2. 可定制 UI（HUD）
**#4418** 请求将 CLI 的上下文状态、分支等信息以可配置 HUD 呈现，并提供第三方实现作为参考方案，体现出高阶用户对终端内信息可视化与高度定制化的诉求。

### 3. 更智能的模型路由策略
**#4411 / #4412** 提出 Auto-mode 应支持自定义模型强度范围、设置 max/min 模型与偏好权重。社区正在逐步接受“自动按任务复杂度选择模型”的理念，并希望拥有更强控制力。

### 4. 非 GitHub 平台支持
**#2922** 请求 `/remote` 支持非 GitHub 的 Git 仓库（GitLab、Bitbucket 等），反映出企业用户常采用混合 Git 托管平台，远程会话功能不应绑定于特定平台。

### 5. 高可用与容错机制
**#4421 / #4419 / #4416** 均指向基础设施的容错机制缺失：MCP 握手无重试、临时策略导致永久拒绝、模型限流无降级。社区对系统稳定性的预期正在提升。


## 开发者关注点

- **MCP 生态稳定性**：多起 issue 集中于 MCP 初始化失败、OAuth 认证异常（如 #4371、#4408、#4421），严重阻碍开发者将自定义 MCP server 接入 CLI，是当前最突出的集成痛点。
- **模型可用性不一致**：Claude 模型突然不可用（#4422）与组织模型配置缺失（#4390）反复出现，开发者对“配置可见但不可用”的状态尤为困惑。
- **资源消耗异常**：CPU 占用 100%（#4415）、长会话输入延迟恶化（#4299）等问题影响日常交互体验，尤其在长时间运行复杂任务时变得难以忍受。
- **输入与执行的可控性**：无法取消已排队消息（#1857）、并行工具调用响应错乱（#4420）导致用户对 Agent 行为的掌控感不足。
- **静默失败难以排查**：prompt 被静默丢弃（#4423）、远程会话禁用无提示（#4409）等问题缺乏明确报错，给问题定位带来极大困难。

---
*本日报由 AI 自动生成，数据来源为 GitHub Issues 与 PR 的公开信息。*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI 社区动态日报

**2026-08-10**


## 今日速览

昨日社区讨论焦点集中于**内存系统**与 **ACP 流式输出稳定性**两大方向：一个长期开放的 Memory System 功能请求（#1283）获得高热度关注；同时，用户报告了 ACP 模式下流式响应挂死的严重问题（#2598）。PR 方面，一个修复 Google GenAI 与 MCP 工具兼容性的补丁（#739）有新进展。


## 社区热点 Issues

### 1. #1283 [Feature Request] Memory System - Persistent context across sessions
- **作者**: CatKang | **更新**: 2026-08-09 | **评论**: 27
- **链接**: [Issue #1283](https://github.com/MoonshotAI/kimi-cli/issues/1283)
- **关注点**: 社区高度期待引入跨会话持久化记忆系统，支持 AI 自动记忆（项目模式、用户偏好）与用户手动指令记忆。
- **开发者反应**: 27 条评论表明需求强烈，讨论焦点集中在记忆的存储格式、作用域（全局 vs 项目级）以及隐私控制上。长期开放（自 2 月）但热度不减，是当前社区最关注的功能之一。

### 2. #2598 [Bug] ACP/print 流式响应静默挂死（0.31.1 仅覆盖 Esc 场景）
- **作者**: ai-agent-workbench | **更新**: 2026-08-09 | **评论**: 0
- **链接**: [Issue #2598](https://github.com/MoonshotAI/kimi-cli/issues/2598)
- **关注点**: ACP 模式下流式响应在内容发送完成后连接挂死——`[DONE]` 帧不回、无超时、后续消息被静默顶替且已流式内容不落盘（无 `content.part`）。这是影响自动化的严重稳定性问题。
- **开发者反应**: 为昨日新提交的 issue，暂无评论，但问题描述细致（含版本与场景对比），直击 ACP 集成稳定性的要害，预计会引发快速响应。


## 重要 PR 进展

### 1. #739 [fix] Strip JSON Schema metadata from Google GenAI tool parameters
- **作者**: xiaoju111a | **创建**: 2026-01-28 | **更新**: 2026-08-09 | **评论**: 0
- **链接**: [PR #739](https://github.com/MoonshotAI/kimi-cli/pull/739)
- **功能/修复内容**: 修复 Google GenAI provider 与 MCP 工具（如 Exa MCP）联用时因保留标准 JSON Schema 元数据（`title`、`description` 等）而导致的校验错误。该补丁可剥离这些冗余元数据以提升兼容性。
- **开发者关注点**: 长期开放（自 1 月）但持续活跃，解决的是真实用户痛点。若合并，将显著改善使用 Google Gemini + MCP 工具链的体验，值得关注。


## 功能需求趋势

截至 2026-08-10 的 Issues 数据中，社区最集中的功能方向为：

- **跨会话记忆系统**（#1283）：打破会话边界，实现项目级与用户级长期上下文管理，是当前呼声最高的功能需求。
- **ACP 流式稳定性与超时控制**（#2598）：要求为 `session/prompt` 增加空闲超时、错误恢复与更稳健的 finish 帧处理，保障自动化集成可靠性。


## 开发者关注点

从近期高频反馈（结合 #2598 等）来看，开发者对 ACP/自动化协议集成路径下的稳定性与可观测性尤为敏感，集中在：**流式空闲超时缺省**、**部分输出不落盘**（不写 `wire.jsonl`），以及 **挂死轮次被静默顶替** 等问题。官方配置文档中尚无可控超时项是明确痛点，建议后续版本优先补齐。另外，**Google GenAI + MCP 工具的参数兼容问题**（#739）仍待合入，间接影响多云模型生态的落地的顺畅度。

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode 社区动态日报 — 2026-08-10

> 数据来源：github.com/anomalyco/opencode

---

## 今日速览

今日社区焦点集中在 **OpenCode Go 代理网关的模型名 bug**——多个 issue 报告 `deepseek-v4-flash` 请求被注入了前导空格导致 HTTP 400，该问题虽然已有 PR 被关闭但仍被验证为未修复。此外，**复制粘贴功能失效**（#4283）以 122 条评论继续高居热门榜首，成为社区长期痛点；针对 **嵌套子代理权限请求静默挂起**（#13715）的修复 PR 已合并，是今日最重要的正向进展。功能需求方面，**Claude Code hooks 原生兼容**（#12472）呼声持续上升。

---

## 社区热点 Issues（Top 10）

### 1. 🔥 复制到剪贴板失效 — 122 条评论 | 110 👍
**#4283** | [查看 Issue](https://github.com/anomalyco/opencode/issues/4283)  
用户 `maheshmuttintdev` 反馈在终端中选中响应文本后无法复制到剪贴板，附带系统信息。该 issue 自 2025 年 11 月创建至今评论数高达 122 条，是社区长期未解决的高频痛点之一，同类问题（#39588 VS Code 扩展上复制粘贴完全不可用）也在持续出现，说明跨平台、跨界面（TUI/IDE）的复制功能均有问题。

### 2. 能否禁用流式（streaming）模式？— 29 条评论 | 38 👍
**#785** | [查看 Issue](https://github.com/anomalyco/opencode/issues/785)  
部分代理提供商（如 Credal OpenAI Proxy）不支持流式响应，导致 `AI_APICallError`。该请求自 2025 年 7 月提出，持续获得关注，反映社区对非流式 API 兼容性的刚性需求。

### 3. Claude Code hooks 原生兼容（PreToolUse/PostToolUse/Stop）— 17 条评论 | 38 👍
**#12472** | [查看 Issue](https://github.com/anomalyco/opencode/issues/12472)  
OpenCode 已兼容 Claude Code 的 `CLAUDE.md` 规则和 skills 目录，但 hooks 系统（`~/.claude/settings.js` 中定义的 PreToolUse、PostToolUse、Stop）尚未支持。该需求获得 38 个 👍，是工具链迁移场景下的核心缺口。

### 4. 嵌套子代理权限请求静默挂起 — 11 条评论 | 24 👍
**#13715** | [查看 Issue](https://github.com/anomalyco/opencode/issues/13715)  
子代理再派生子代理时，内层子代理触发的权限请求（如 bash）不会渲染到 TUI 界面，会话永久挂起等待一个永远等不到的响应。**相关修复 PR #36046 已合并**，是今日最重要的修复进展之一。

### 5. OpenCode Go 代理注入前导空格导致 deepseek-v4-flash 返回 HTTP 400 — 6 条评论
**#41300** | [查看 Issue](https://github.com/anomalyco/opencode/issues/41300)  
使用 `opencode-go/deepseek-v4-flash` 时，请求发送的模型名为 `" deepseek-v4-flash"`（含前导空格），上游返回 `invalid_request_error`。同批相关报告包括 #41306、#41322、#41314，均为同一根因。虽然 #41211 曾被标记关闭，但 **#41306 已验证该 bug 在 2026-08-09 仍然存在**，说明修复未生效。

### 6. 深度求索 V4 Flash 突然停止工作 — 9 条评论 | 11 👍
**#39838** | [查看 Issue](https://github.com/anomalyco/opencode/issues/39838)  
用户报告 DeepSeek V4 Flash 在某次更新后完全无法使用，附带截图；多个类似报告（如 #39582 输出中途截断）显示该模型稳定性存在系统性问题。

### 7. OpenCode Go 订阅：托管与代理模型区分不明确 — 16 条评论 | 32 👍
**#24649** | [查看 Issue](https://github.com/anomalyco/opencode/issues/24649)  
用户要求澄清 OpenCode Go 文档中哪些模型是自托管、哪些通过第三方代理，并质疑基础设施声明。32 个 👍 表明定价透明度是社区关注重点。

### 8. “terminated” 错误 — 9 条评论 | 4 👍
**#30221** | [查看 Issue](https://github.com/anomalyco/opencode/issues/30221)  
OpenCode Go 订阅下所有活跃会话持续以 `UnknownError: "terminated"` 终止，与模型选择无关；直接使用 DeepSeek 或 Z.AI 的 API 端点则正常。

### 9. MCP 工具已连接但未暴露给 Agent — 7 条评论 | 3 👍
**#33027** | [查看 Issue](https://github.com/anomalyco/opencode/issues/33027)  
MCP 服务器 `pdfrag` 成功连接并通过 `tools/list` 暴露 6 个工具，但 Agent 的工具列表中不出现这些工具。MCP 生态兼容性问题持续累积。

### 10. Xcode 27 ACP 集成忽略 opencode.json 模型配置 — 15 条评论
**#34743** | [查看 Issue](https://github.com/anomalyco/opencode/issues/34743)  
macOS 27 beta 2 + Xcode 27 beta 2 环境下，通过 ACP 调用 opencode 时忽略 `opencode.json` 中指定的模型，转而使用默认模型 `big-pickle`。反映 IDE 集成场景下配置透传问题。

---

## 重要 PR 进展（Top 10）

### 1. 修复嵌套子代理权限提示不渲染
**#36046** | 作者：NaturalSelect | [查看 PR](https://github.com/anomalyco/opencode/pull/36046)  
**CLOSED** — 修复 #13715：嵌套子代理触发的权限请求不再被静默丢弃，现在能正确渲染到 TUI。这是社区长期痛点的重要修复。

### 2. Claude Code 兼容性 PR 未见，但以下为今日活跃 PR：worktree 工作区切换
**#36052** | 作者：haxllo | [查看 PR](https://github.com/anomalyco/opencode/pull/36052)  
**CLOSED** — 基于 git worktree 的工作区切换功能，包含 `opencode worktree create|list|remove` 等 CLI 子命令，并支持 stash 快速切换。核心工作流能力增强。

### 3. 引入 Bun canary 修复 NAPI 退出崩溃
**#36023** | 作者：BenSharir | [查看 PR](https://github.com/anomalyco/opencode/pull/36023)  
**CLOSED** — 修复所有平台（Windows/macOS/Linux x64）在退出时的 NAPI 崩溃问题，关闭 #28046、#31563、#36027 三个相关 issue。

### 4. 保留粘贴图片路径供 MCP 工具使用
**#36051** | 作者：hb-0 | [查看 PR](https://github.com/anomalyco/opencode/pull/36051)  
**CLOSED** — 路径型 MCP 工具（如图片读取器）需要文件路径访问粘贴的图片，此前粘贴的剪贴板图片路径丢失，此 PR 修复该问题（关闭 #17771）。

### 5. 改进 Gemini 经 OpenRouter 的缓存能力
**#36070** | 作者：AbdoKnbGit | [查看 PR](https://github.com/anomalyco/opencode/pull/36070)  
**CLOSED** — Gemini 经由 OpenRouter 的请求未使用 OpenCode 已支持的显式缓存断点，此 PR 补齐该功能（关闭 #36069）。

### 6. 接受 Ollama 的 reasoning 字段
**#36068** | 作者：twhittock | [查看 PR](https://github.com/anomalyco/opencode/pull/36068)  
**CLOSED** — Ollama 的 `/v1/chat/completions` 在流式和非流式响应中使用 `reasoning` 字段而非 DeepSeek/LM Studio 的 `reasoning_content`，Schema.Struct 会剔除未知键导致推理内容静默丢失，此 PR 修复。

### 7. 修复插件返回空 hook 导致 provider 列表崩溃
**#36102** | 作者：CryptArchy | [查看 PR](https://github.com/anomalyco/opencode/pull/36102)  
**CLOSED** — 插件条目解析后没有 hooks 时被直接推入 hooks 数组，后续 Provider 状态构建时崩溃，现跳过 falsy 返回值（关闭 #35772）。

### 8. 重构非模态设置界面
**#40845** | 作者：Hona | [查看 PR](https://github.com/anomalyco/opencode/pull/40845)  
**OPEN**（beta）— 将设置导航重组，拆分外观与通知为独立页面，新增 Projects 和 Extensions 视图，改进多服务器选择与默认服务器排序。桌面端 UI 体验的大幅更新。

### 9. 工作区流程接入新布局
**#38790** | 作者：Hona | [查看 PR](https://github.com/anomalyco/opencode/pull/38790)  
**OPEN**（beta）— 新会话可选择本地仓库、隔离新工作区或已有工作区，composer 展示分支上下文。配合 #40845 构建设桌面端体验的整体升级。

### 10. 保持 Copilot 响应续接对齐官方客户端
**#41452** | 作者：rekram1-node | [查看 PR](https://github.com/anomalyco/opencode/pull/41452)  
**OPEN** — 对齐无状态 Copilot Responses 续接行为与 VS Code 官方客户端，持久化已完成推理条目的 ID 与加密状态，支持推理内容的续接处理。

---

## 功能需求趋势

**1. Claude Code 生态兼容性深化**（#12472）  
规则和 skills 已兼容，hooks 系统（PreToolUse/PostToolUse/Stop）成为下一个迁移障碍。社区对 Claude Code 工作流的平移需求在持续增长。

**2. 非流式 API 支持**（#785）  
企业代理多为网关中转，不支持流式是常见限制，但 OpenCode 目前强依赖流式，构成实际使用门槛。

**3. 多窗口/多标签桌面体验**（#14657）  
用户期望桌面端支持多服务器并行窗口，切换服务器时不应重载整个 UI，反馈当前切换延迟明显。

**4. 图片粘贴与拖放支持**（#31791）  
主聊天输入已支持图片粘贴/拖放，但 agent 调用 question 工具时的结构化问答界面仍不支持附加图片，影响多模态交互场景。

**5. 持久会话守护进程与记忆召回**（#41453）  
用户希望存在一个常驻守护进程，支持跨会话的零工具调用记忆召回，避免每次新会话都从零开始。

---

## 开发者关注点

**高频痛点集中在四类：**

1. **复制粘贴问题长期未解决**  
   TUI（#4283，122 条评论）与 VS Code 扩展（#39588）均有报告，横跨 2025 至 2026 年仍未修复，是社区积累怨气最多的单点问题。

2. **OpenCode Go 订阅可靠性存疑**  
   模型名注入空格 bug（#41300/#41306/#41314/#41322）修复后被验证未生效（#41306）；`terminated` 全会话中断（#30221）、支付后订阅未激活（#41430）、免费额度误判（#32971/#41448）等问题叠加，开发者对 Go 服务的信任度承压。

3. **模型参数透传断层**  
   `reasoningEffort` 在自定义 `@ai-sdk/openai-compatible` provider 下被静默丢弃（#27361、#41294），AI SDK 层对模型 config 的透传链路不完整，影响 OpenRouter 等依赖扩展参数的服务。

4. **嵌套子代理的权限与可见性问题**  
   权限请求挂起（#13715）已随 #36046 修复，但 TUI 侧边栏对子代理状态的可视化（#36042）仍是新建功能，说明多 agent 拓扑下的可观测性还在完善中。

5. **本地/代理 MCP 工具的稳定接入**  
   MCP 工具已连接但 agent 不可见（#33027）、路径型 MCP 工具拿不到剪贴板图片路径（#36051 修复）等，反映 MCP 生态接入的细节打磨仍在进行。

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi 社区动态日报 — 2026-08-09/10

> 数据来源: github.com/badlogic/pi-mono（earendil-works/pi）

---

## 今日速览

昨日社区提交量激增，共有超过35条Issue更新和11条PR动态。热点集中在**GitHub Copilot登录因并发策略启用触发429限流**（#7850，PR #7851和#7844均已提交修复），以及 **TUI界面交互体验问题**（滚动跳变、自动复制、分页键缺失等）的系统性修复。此外，一批针对AI21 API断服、EPIPE崩溃和并发RPC会话竞态的高质量问题已在24小时内关闭。

---

## 社区热点 Issues（精选10条）

### 1. [bug] GitHub Copilot 登录失败 429（Rate Limiting）— 高热度
**#7850** | 作者: tuunit | 👍 0 | 💬 1 | [链接](https://github.com/earendil-works/pi/issues/7850)
> 设备授权成功后，Pi在登录Copilot时因组织拥有20+模型、并发启用策略触发限流而失败。**直接影响大量企业级用户**，已由两项PR（#7851、#7844）提出不同修复方案。

### 2. [bug] 默认模型设为 llama.cpp 模型时启动显示 "No models available"
**#6922** | 作者: highlyunavailable | 👍 14 | 💬 9 | [链接](https://github.com/earendil-works/pi/issues/6922)
> 当 `defaultProvider` 为 `"llama.cpp"` 时启动失败。**社区反映最强烈的问题之一（👍14）**，与 #6948（异步模型刷新竞态）相关，PR #7072 已提交修复但合并流程较长。

### 3. [bug] Mac OS 长会话高 CPU 占用（50-110%）
**#7730** | 作者: gterzian | 👍 6 | 💬 6 | [链接](https://github.com/earendil-works/pi/issues/7730)
> 长会话导致 Mac 上 CPU 飙升至 100% 以上，内存 600-800MB。**与上下文长度相关**，目前仍开放，无明确修复方案，影响 macOS 重度用户。

### 4. [bug] TUI 滚动跳变：长输出流式输出时无法保持阅读位置
**#7861** | 作者: jingyulong | 👍 0 | 💬 1 | [链接](https://github.com/earendil-works/pi/issues/7861)
> 流式输出时向上滚动阅读，视图不断跳回底部，输出结束后才停止。**与 #7616（工具块超高时视图跳跃）属同类渲染器问题**，影响长任务阅读体验。

### 5. [bug] 渲染器硬崩溃：行宽超过终端宽度即中止会话
**#7868** | 作者: intelligentrascal | 👍 0 | 💬 1 | [链接](https://github.com/earendil-works/pi/issues/7868)
> TUI 渲染器在单行超出终端宽度时直接中止整个 agent 会话，而非截断。**已导致实际工作中断**，属于高优先级渲染健壮性问题。

### 6. [bug] 自动压缩（Auto-compaction）后任务停止而非恢复
**#7848** | 作者: jagadeepmamidi | 👍 0 | 💬 1 | [链接](https://github.com/earendil-works/pi/issues/7848)
> 长任务触发上下文压缩后，Pi 有时停止执行未完成任务，等待用户输入。**影响长时间自动化任务的可靠性**。

### 7. [bug] ExtensionContext.exec 超时后无法强制杀死忽略 SIGTERM 的子进程
**#7864** | 作者: fettpl | 👍 0 | 💬 2 | [链接](https://github.com/earendil-works/pi/issues/7864)
> `proc.killed` 仅表示信号发送成功而非进程退出，导致忽略 SIGTERM 的子进程永远存活，`exec()` promise 永不 resolve。**扩展开发者的关键阻塞问题**。

### 8. [bug] 并发 RPC 会话替换导致运行时空闲竞争
**#7862** | 作者: fettpl | 👍 0 | 💬 2 | [链接](https://github.com/earendil-works/pi/issues/7862)
> `new_session`、`switch_session`、`fork`、`clone` 可并发替换共享的 `AgentSessionRuntime`，两项替换命令可能同时通过预检查并拆除运行时。**RPC 架构级并发缺陷**。

### 9. [bug] 0.84.0/0.84.1 在 Bun 运行时下无法启动
**#7846** | 作者: and1truong | 👍 0 | 💬 1 | [链接](https://github.com/earendil-works/pi/issues/7846)
> `zlib.createZstdDecompress is not a function` — undici 与 Bun 的 zlib 兼容性问题。**Bun 用户完全无法使用新版本**。

### 10. [bug] ai21 API 已废弃，返回 410 错误
**#7869** | 作者: Josako | 👍 0 | 💬 2 | [链接](https://github.com/earendil-works/pi/issues/7869)
> AI21 旧版 API 已退役，需迁移至 Gateway。**外部服务变更导致的突发故障**，提醒用户关注上游 API 生命周期。

---

## 重要 PR 进展（精选10条）

### 1. [已关闭] fix(coding-agent): 缓存 llama.cpp 模型目录
**#7072** | 作者: davidbrai | [链接](https://github.com/earendil-works/pi/pull/7072)
> 修复 #6948 — 内置 llama.cpp provider 启动时模型未应用的问题。**通过缓存解决异步模型刷新的竞态条件**，长期悬而未决的默认模型问题有望解决。

### 2. [已关闭] feat(tui): 新增 copyOnSelect 选项（TuiAltScreen）
**#7866** | 作者: re2zero | [链接](https://github.com/earendil-works/pi/pull/7866)
> 为全屏 TUI 模式添加 `copyOnSelect` 选项，允许用户禁用鼠标选择即复制的行为。**回应 #7720 功能需求**，默认 `true` 保持现有行为。

### 3. [已关闭] fix(tui): 基础 SelectList 和 model-selector 支持 pageUp/pageDown
**#7865** | 作者: re2zero | [链接](https://github.com/earendil-works/pi/pull/7865)
> 为缺失的组件补齐 `tui.select.pageUp/pageDown` 键位绑定。**修复 #7616 提到的长列表导航问题**，改善选择器可用性。

### 4. [已关闭] feat(protocol): 新增远程会话线协议
**#7344** | 作者: christianklotz | [链接](https://github.com/earendil-works/pi/pull/7344)
> 新增 `@earendil-works/pi-protocol` 包：定义远程会话命令、事件、快照与错误的验证模式，实现严格有界 CBOR 编码和增量长度前缀帧。**为远程会话能力奠定协议基础**。

### 5. [已关闭] fix(coding-agent): 无论 expandPromptTemplates 设置如何都路由扩展命令
**#7858** | 作者: softpudding | [链接](https://github.com/earendil-works/pi/pull/7858)
> 修复 `sendUserMessage()` 因 `expandPromptTemplates: false` 跳过扩展命令处理的问题。**修复 #7859 中文档模式失效的 bug**。

### 6. [开放] feat(agent): sendUserMessage 暴露 expandPromptTemplates 参数
**#7857** | 作者: mrexodia | [链接](https://github.com/earendil-works/pi/pull/7857)
> 开放 `expandPromptTemplates` 参数供扩展开发者使用，便于触发扩展命令。**与 #7858 互补**，当前仍开放讨论中。

### 7. [已关闭] fix(ai): 修复 JSON 序列化结构化工具参数验证
**#7856** | 作者: alan-vaultn | [链接](https://github.com/earendil-works/pi/pull/7856)
> 修复 Provider 双重序列化嵌套工具参数导致验证失败的问题。**消除 `must be object` 硬失败**，提高工具调用的容错性。

### 8. [已关闭] fix(coding-agent): 修复 RPC 示例中的拼写错误
**#7853** | 作者: JafarAbdi | [链接](https://github.com/earendil-works/pi/pull/7853)
> 将 `--no-extension` 修正为 `--no-extensions`。**小修复但影响文档使用者**，避免用户复制错误命令。

### 9. [已关闭] fix(provider): GitHub Copilot 模型策略顺序启用
**#7851** | 作者: tuunit | [链接](https://github.com/earendil-works/pi/pull/7851)
> 将 Copilot 模型的策略启用从并发改为顺序执行。**避免大型组织因并发请求触发 429 限流**，修复 #7850。

### 10. [已关闭] fix(provider): 登录期间避免批量策略更新
**#7844** | 作者: ChekTek | [链接](https://github.com/earendil-works/pi/pull/7844)
> 移除登录时的批量模型启用逻辑，模型仍可通过 Copilot Chat 显式启用。**与 #7851 相似方案**，从不同角度解决 429 问题。

---

## 功能需求趋势

| 趋势方向 | 代表 Issue/PR | 热度 |
|---------|--------------|------|
| **TUI 交互体验优化** | #7720（禁用选择复制）、#7865（PageUp/Down）、#7852（鼠标点击定位）、#7495（编辑区固定） | 🔥🔥🔥 |
| **渲染器健壮性** | #7868（超宽行崩溃）、#7861/#7616（滚动跳变） | 🔥🔥🔥 |
| **Copilot 登录稳定性** | #7850、PR #7851/#7844 | 🔥🔥🔥 |
| **llama.cpp 本地模型支持** | #6922、#6948、PR #7072 | 🔥🔥 |
| **扩展系统能力提升** | #7864（exec超时）、#7859/#7858（命令触发）、#7857（参数暴露） | 🔥🔥 |
| **新 Provider/模型支持** | #7847（Qwen Token Plan中国版）、#7870（GLM-5.2上下文窗口） | 🔥 |
| **远程会话协议** | PR #7344（pi-protocol 包） | 🔥 |
| **性能优化** | #7730（Mac高CPU） | 🔥 |

---

## 开发者关注点

1. **TUI 渲染可靠性是当前最大痛点**：多条 Issue 围绕渲染器在长输出、超宽行、滚动场景下的异常行为，影响核心使用体验（#7861、#7868、#7616、#7495）。好消息是相关修复 PR（#7865、#7866）已快速提交。

2. **Copilot 登录 429 问题影响面广**：大型组织用户无法正常登录，好在社区 24 小时内提交了两套修复方案（#7851 顺序启用 vs #7844 移除批量更新），体现了活跃的协作氛围。

3. **扩展开发者的工具链不完善**：`exec` 超时无法强制杀进程（#7864）、`sendUserMessage` 无法触发命令（#7859）、自定义工具渲染失效（#7740）——扩展生态的稳定性仍有提升空间。

4. **Bun 运行时兼容性回归**：#7846 显示 0.84.x 在 Bun 下完全不可用，属于阻塞性 bug，需优先修复。

5. **渲染器超长行、异步竞态、EPIPE 崩溃**等问题的 PR 集中在同一天提交，说明核心开发者正在集中处理稳定性问题，预计下一版本会有较大改善。

6. **模型目录与上下文窗口数据错误**（#7870）反映了远程目录覆盖本地正确配置的问题，需要更好的优先级策略。

---

*日报生成时间: 2026-08-10 | 数据窗口: 2026-08-09 至 2026-08-10*

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code 社区动态日报 — 2026-08-10

## 今日速览

昨日社区维持高活跃度，共更新 24 条 Issue 与 50 条 PR。核心动态集中在两大方向：一是 **多会话/多代理协调** 相关提案（#8718、#8775）进入深入讨论阶段，标志着项目正从单会话工具向复杂工作流平台演进；二是 **Web Shell 与 daemon 架构** 的稳定性修复成为绝对主力，多个 autofix 驱动的 PR 针对事件渲染、会话恢复等问题进行密集修补。此外，Windows 平台安装与编码问题持续受到社区关注。

---

## 社区热点 Issues（10 条）

**1. [#8718 RFC: Native coordination for independent Qwen sessions](https://github.com/QwenLM/qwen-code/issues/8718)**
- **类型**: 功能需求 / P2 / 多代理路线图
- **动态**: 创建于 08-08，更新于 08-09，8 条评论
- **要点**: 提议为多个独立 Qwen Code 会话增加原生协调路径，使 leader 能派发 2-3 个 worker 并保持自身交互，同时观察关联的运行时状态并收集结构化结果。
- **关注理由**: 这是多代理路线图的核心提案，讨论度极高，可能定义未来协作架构。

**2. [#8775 Proposal: unify the session reasoning loops on a Turn-based SessionRuntime](https://github.com/QwenLM/qwen-code/issues/8775)**
- **类型**: 增强 / P2 / 会话管理路线图
- **动态**: 新建于 08-09，已获 2 条评论
- **要点**: 指出会话推理循环（发送 prompt → 流式事件 → 分发工具 → 重复）在当前仓库中被至少 6 处独立实现（`useGeminiStream`、`runNonInteractive`、ACP `Session`、`acp-bridge`、`serve` dispatch 等），提议统一为基于 Turn 的 SessionRuntime。
- **关注理由**: 直击架构重复建设痛点，若实施将大幅降低维护成本。

**3. [#7118 Windows standalone installer fails when powershell.exe cannot resolve Get-FileHash](https://github.com/QwenLM/qwen-code/issues/7118)**
- **类型**: Bug / P2 / Windows 安装 / welcome-pr
- **动态**: 已开放 3 周，更新于 08-09，6 条评论，👍 3 次
- **要点**: Windows 独立安装程序在 SHA-256 校验时因 PowerShell 无法解析 `Get-FileHash` 而失败，降级建议使用 `--method npm`。
- **关注理由**: 社区点赞最高的 Issue 之一，Windows 用户高频遇到安装障碍。

**4. [#8784 Streamable HTTP: optional GET/SSE stream rejected with 404 kills the whole MCP connection](https://github.com/QwenLM/qwen-code/issues/8784)**
- **类型**: Bug / P2 / MCP
- **动态**: 新建于 08-09，5 条评论
- **要点**: MCP Streamable HTTP 服务器在完成 POST 握手后，客户端额外探测可选 GET/SSE 流，若服务器返回 404 则整个 MCP 连接被终止。
- **关注理由**: MCP 集成的重要兼容性缺陷，影响与多种第三方 MCP 服务器的互操作。

**5. [#8823 bug(sdk): hidden unrecognized diagnostics mutate and evict transcript state](https://github.com/QwenLM/qwen-code/issues/8823)**
- **类型**: Bug / P2 / SDK / daemon
- **动态**: 新建于 08-09，3 条评论
- **要点**: 未识别的 daemon 事件被规范化为 `debug` 事件后可能被 Web Shell 隐藏，但它们在进入共享 transcript reducer 时已产生两个用户可见的副作用。
- **关注理由**: 与今日多个 Web Shell 修复 PR 直接关联，反映 daemon 架构深入应用后的边界问题。

**6. [#8822 Main CI failed: E2E Tests — cli/monitor.test.ts](https://github.com/QwenLM/qwen-code/issues/8822)**
- **类型**: CI Bug / P2 / autofix/skip
- **动态**: 新建于 08-09，4 条评论
- **要点**: `monitor` 工具的 E2E 测试持续失败，已标记 autofix，但被 skip。
- **关注理由**: CI 稳定性是开发效率的关键，这类失败需要社区关注 autofix 是否有效。

**7. [#8678 fix(serve): Preserve the current session when a large restore times out](https://github.com/QwenLM/qwen-code/issues/8678)**
- **类型**: Bug / P1 / 会话管理 / 延迟 / 内存
- **动态**: 更新于 08-09，PR1（#8691）已合并
- **要点**: 大会话恢复超时时需保留当前会话，PR1 已实现超时契约、迟到请求安全性和可观测性。
- **关注理由**: P1 优先级，直接关系到大型工作区的用户体验。

**8. [#8769 Proposal: rebuild /review Step 3–5 orchestration on the workflow engine](https://github.com/QwenLM/qwen-code/issues/8769)**
- **类型**: 增强 / P2 / 多代理路线图
- **动态**: 创建于 08-08，更新于 08-09，4 条评论
- **要点**: 提议将 `/review` 技能的编排逻辑从模型驱动迁移到 workflow 引擎，使 fan-out 结构、per-agent prompts 和循环收敛变成确定性代码。
- **关注理由**: workflow 引擎的又一重要落地场景，体现其架构价值。

**9. [#8697 OTEL_METRICS_EXPORTER=otlp in environment silently disables metrics export](https://github.com/QwenLM/qwen-code/issues/8697)**
- **类型**: Bug / P2 / 遥测
- **动态**: 已关闭，3 条评论
- **要点**: 当环境变量 `OTEL_METRICS_EXPORTER=otlp` 存在时（多 CLI 共享 collector 的常见配置），qwen-code 遥测 SDK 内部启动失败导致指标静默禁用，而 traces 正常。
- **关注理由**: 影响与 Claude Code、Codex 等共用 OTel collector 的复杂环境，值得注意。

**10. [#8411 Caller-supplied session IDs are not coordinated across daemon transports and workspaces](https://github.com/QwenLM/qwen-code/issues/8411)**
- **类型**: 增强 / P2 / 会话管理
- **动态**: 已关闭，更新于 08-09
- **要点**: PR #7836 增加了 `/session` 的调用方 `sessionId` 支持，但该契约仅限 REST 创建路径，daemon 多入口和跨工作区时缺少协调。
- **关注理由**: 会话管理一致性问题的系统梳理，供后续实现参考。

---

## 重要 PR 进展（10 条）

**1. [#8812 fix(web-shell): stop rendering unrecognized daemon events in transcripts](https://github.com/QwenLM/qwen-code/pull/8812)**
- **作者**: wenshao | 状态: OPEN / autofix/takeover
- **内容**: Web Shell 不再将 daemon 的 debug 投影渲染为对话内容。normalizer 为每个 debug 事件标记结构化 `debugReason`，Web Shell 据此判断。
- **意义**: 直接回应用户可见的幽灵消息问题（#8823）。

**2. [#8798 fix(web-shell): reconcile mid-turn messages with daemon state](https://github.com/QwenLM/qwen-code/pull/8798)**
- **作者**: ytahdn | 状态: OPEN
- **内容**: 让 daemon 成为已接受 mid-turn 消息的权威来源，Web Shell 按稳定 message ID 协调共享队列，刷新或切换会话后恢复排队的消息，避免重复提交。
- **意义**: 提升 Web Shell 在复杂会话场景下的一致性。

**3. [#8735 fix(workflows): make replay journal durable](https://github.com/QwenLM/qwen-code/pull/8735)**
- **作者**: qqqys | 状态: OPEN
- **内容**: 将 workflow 重放状态变为持久化、版本化的 checkpoint 契约，通过 per-run 队列序列化日志写入，恢复时校验已提交日志前缀。
- **意义**: 提升 workflow 引擎在崩溃恢复场景下的可靠性。

**4. [#8813 fix(test): stop background-shell tests sharing a fixed /tmp sidecar path](https://github.com/QwenLM/qwen-code/pull/8813)**
- **作者**: wenshao | 状态: OPEN / autofix/takeover
- **内容**: 修复 `backgroundShellRegistry.test.ts` 所有测试共享 `outputPath: '/tmp/s1.output'` 导致的 CI 测试相互干扰问题。
- **意义**: 消除 CI 不稳定源，提升开发者本地测试体验。

**5. [#8795 fix(core): deflake the shell-registry fixtures, and share the display-strip helper](https://github.com/QwenLM/qwen-code/pull/8795)**
- **作者**: wenshao | 状态: OPEN / autofix/takeover
- **内容**: 为每个测试 fixture 分配独立的 `/tmp` 路径，并提取共享的显示清洗辅助函数。
- **意义**: 配合 #8813 系统性地解决 shell registry 测试的 flakiness。

**6. [#8816 fix(ci): watchdog silent sandbox hangs and reap the containers they leak](https://github.com/QwenLM/qwen-code/pull/8816)**
- **作者**: wenshao | 状态: OPEN / autofix/takeover
- **内容**: 增加空闲看门狗（`QWEN_IDLE_TIMEOUT_MS`，默认 20 分钟），超时后杀掉 agent 并清理泄漏的容器。
- **意义**: 解决 CI 中 2 小时静默挂起问题，大幅提升 autofix 循环效率。

**7. [#8801 fix(acp-bridge): bound live journal replay chunks](https://github.com/QwenLM/qwen-code/pull/8801)**
- **作者**: wenshao | 状态: OPEN / autofix/takeover
- **内容**: 压缩未完成轮次中连续的 assistant 文本/思考块，每个重放条目最多聚合 256 个源事件，同时保留工具调用等元数据边界。
- **意义**: 防止长任务的实时重放过载。

**8. [#8818 fix(core): catch content-only thinking-tag leaks on all OpenAI-compatible providers](https://github.com/QwenLM/qwen-code/pull/8818)**
- **作者**: yiliang114 | 状态: OPEN
- **内容**: 将 thinking-tag 泄漏防御推广到所有 OpenAI 兼容端点，并修复两个绕过路径，替代原先的供应商特定覆写。
- **意义**: 直接解决 #6666（qwen 3.7 max 将思考内容写入 `content` 字段）的根因，惠及所有兼容供应商。

**9. [#8806 fix(desktop): open Local Control on the active session](https://github.com/QwenLM/qwen-code/pull/8806)**
- **作者**: yiliang114 | 状态: OPEN
- **内容**: Local Control 现在捕获当前活动的 Desktop 会话，扫码后打开同一会话而非空白 Web Shell，且只传递会话路径与 workspace ID，替换私有凭据。
- **意义**: 完善手机远程控制体验，兼顾安全性。

**10. [#8749 fix(cli): avoid duplicate context usage in footer and status line](https://github.com/QwenLM/qwen-code/pull/8749)**
- **作者**: yiliang114 | 状态: OPEN / review/self-reported
- **内容**: 当预设状态行已包含 `context-used` 或 `context-remaining` 时，隐藏 footer 中的重复上下文用量指示器。
- **意义**: 消除 CLI 界面冗余信息，提升信息展示效率。

---

## 功能需求趋势

1. **多会话协调与编排**：RFC #8718、#8775 及 #8769 共同指向同一方向——qwen-code 正从单会话 CLI 演变为支持多代理、多会话协同的平台。社区对 leader/worker 模式、Turn-based 统一运行时、workflow 引擎接管复杂编排有明确期望。

2. **Workflow 引擎深度应用**：除原有 workflow 相关提案外，#8769（`/review` 编排迁移）展示了社区希望将更多模型驱动逻辑转变为确定性代码的倾向。

3. **外部上下文与记忆集成**：提案 #7449、#7585（均为 P3 但持续讨论中）体现出企业用户对 monorepo 共享上下文、外部记忆服务 provider-neutral 集成的需求，持续获得关注。

4. **Local Control / 移动端访问**：PR #8806 与已关闭的 #8595 表明社区对手机远程控制本地会话的功能兴趣浓厚，QR 码配对方式将显著提升移动办公效率。

5. **可观测性与调试工具**：工作流重放日志持久化（#8735）、OTEL 指标导出的静默失败修复（#8697）说明高级用户对可观测性要求日益增长。

---

## 开发者关注点

1. **测试稳定性持续受影响**：多个 CI 失败（#8756、#8822、#8799、#8766）均集中在 E2E 测试，且 shell-registry 测试共享 `/tmp` 路径的 flakiness 问题需两个 PR 协同解决，反映出测试基础设施仍需系统性加固。

2. **Windows 平台支持仍需改进**：安装失败（#7118）持续有赞，配合 shell 输出 mojibake 修复（#7955），Windows 用户体验仍是反馈热点。

3. **Web Shell 与 daemon 的事件一致性问题**：#8823、#8812、#8798 三个条目聚焦同一深层问题——daemon 事件规范化与 Web Shell 渲染之间的状态一致性，是当前架构深入应用后的关键边界。

4. **安全与 Shell 分类器绕过**：#8575 的关闭与 PR #8590 的提出表明，只读 Shell 分类器的安全性持续被社区主动审视，行续行和 `${var@P}` 展开等绕过方式需要不断修补。

5. **MCP 互操作性需加强**：#8784 暴露出可选 GET/SSE 流被拒导致整个连接终止的缺陷，说明与第三方 MCP 服务器的兼容性测试仍有盲区。

---

*日报数据截至 2026-08-10 00:00 UTC，涵盖过去 24 小时 GitHub 仓库动态。*

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI 社区动态日报 — 2026-08-10

> 数据来源：`Hmbown/DeepSeek-TUI`（CodeWhale 项目）

---

## 1. 今日速览

昨日社区无新 Release，但 **v0.9.6 发布 PR 已合入**（#5313），作为“减法”版本移除编译期约束并重构了 compaction 链路。社区热度集中在 **context 压缩不可见问题**（#5096/#5239）、**Fleet 配置影子化**（#5098）以及 **TUI 权限请求默认选项变更**（#5293）等可靠性痛点；此外，由 `Copilot` 提交的 Runtime API 系列 PR 全部合入，标志着面向托管客户端的控制面进一步完善。另一个值得注意的信号是，多位中文用户提交了翻译与 UX 相关 Issue（#4949、#5023），中文社区的反馈正在增加。

---

## 2. 版本发布

过去 24 小时无新 Release。但 v0.9.6 的发布准备 PR（#5313）已合并，该版本为“减法”运行时释放——移除 harness 阻塞，同时保留显式预算、截止时间、取消机制与真实的 provider 状态，并围绕“provider 单一摘要 + committed successor handoff”重建了 compaction 逻辑。

---

## 3. 社区热点 Issues（Top 10）

### #4949 — “Constitution” 中文翻译之争： “宪法” vs “协作准则”
- **作者**: SparkofSpike | **评论**: 8 | **状态**: OPEN
- **要点**: 中文母语者社区对 `Constitution` 一词的翻译产生分歧，作者认为“宪法”体现基础性权威，但部分用户担心中文语境下的政治色彩。此讨论已成为中文社区参与度最高的公共话题。
- **链接**: https://github.com/Hmbown/CodeWhale/issues/4949

### #5096 — Compaction 触发后 token 计数器无变化（用户不可见）
- **作者**: jbousquie | **评论**: 3 | **状态**: OPEN
- **要点**: `/compact` 命令显示“触发/完成”但 token 计数不变（37K/128K 不回落），用户感知为功能未生效。被评为可靠性 bug，涉及 TUI 与 compaction 的联动显示。
- **链接**: https://github.com/Hmbown/CodeWhale/issues/5096

### #5239 — 模型支持 1M 上下文，但工具为何在 128K 就触发压缩？
- **作者**: hardy922 | **评论**: 1 | **状态**: OPEN
- **要点**: 与 #5096 同源的核心困惑——`context_window_for_model` 对未知模型 ID 静默回退到 128K 默认值（#5244 为此提出改进）。该问题被多位用户反复提出，说明默认行为带来的“隐性降级”是当前最令人困惑的体验之一。
- **链接**: https://github.com/Hmbown/CodeWhale/issues/5239

### #5293 — TUI 权限请求默认高亮选项从“允许”变为“拒绝”
- **作者**: JayBeest | **评论**: 4 | **👍**: 1 | **状态**: OPEN
- **要点**: v0.9.4 起权限对话框默认高亮从“允许”切换为“拒绝”，改变了长期形成的交互习惯，用户可能因快速确认而误拒绝操作。安全性提升与 UX 惯性之间的张力需要平衡。
- **链接**: https://github.com/Hmbown/CodeWhale/issues/5293

### #5098 — Fleet 配置层级过多，且存在静默影子化
- **作者**: Hmbown | **评论**: 2 | **状态**: OPEN
- **要点**: 编辑 `~/.codewhale/agents/builder.toml` 不生效——配置存在多重层级但无优先级提示，改动被静默遮蔽。属于 TUI/Fleet 可靠性问题的典型代表。
- **链接**: https://github.com/Hmbown/CodeWhale/issues/5098

### #5209 — File 工具 `edit` 模式静默接受错误参数名，返回假成功
- **作者**: yekern | **评论**: 3 | **状态**: OPEN
- **要点**: 使用 `new_str` 等非标准参数时，工具不报错而是返回“Replacement successful”，导致每处编辑需要 3-5 次重试。这是“假成功”类 bug 的典型——比直接失败更影响代理可靠性。
- **链接**: https://github.com/Hmbown/CodeWhale/issues/5209

### #5023 — Windows 11 下 IME 候选窗口位置跳动/不稳定
- **作者**: BrathonBai | **评论**: 2 | **状态**: OPEN
- **要点**: 中日韩用户输入法候选窗在 TUI 快速重绘期间漂移，影响中文/日文输入体验。对应 PR #5205 已合入，但问题仍开放。是本地化体验的关键阻塞项。
- **链接**: https://github.com/Hmbown/CodeWhale/issues/5023

### #5250 — 仅能保存一个 API Key，多 provider 切换困难
- **作者**: ffyuhf | **评论**: 2 | **状态**: OPEN
- **要点**: 使用 DeepSeek 与 GLM 等多模型时，每次切换 provider 都需要重新输入 key——当前仅持有一个 key 槽位，覆盖式保存。属于多 provider 工作流的高频痛点。
- **链接**: https://github.com/Hmbown/CodeWhale/issues/5250

### #5034 — 切换 provider 后默认模型未同步更新（遗留问题）
- **作者**: Hmbown | **评论**: 3 | **状态**: OPEN
- **要点**: 切换到 OpenAI 后默认模型仍可能是继承自其他路由的 `gpt-5.5`，provider 与 model 的解析未作为一致整体更新。这是本次数据中多个 provider 相关问题的根因之一。
- **链接**: https://github.com/Hmbown/CodeWhale/issues/5034

### #5314 — “Copy message” 复制内容包含 UI 装饰（● ▏）
- **作者**: maimik | **评论**: 1 | **状态**: OPEN
- **要点**: 右键“复制消息”会携带角色符号 `●` 与续行 rail `▏`，而框选复制则不会。对需要将对话粘贴到文档/工单的用户而言，这是一个琐碎但高频袭扰的 UX 缺陷。
- **链接**: https://github.com/Hmbown/CodeWhale/issues/5314

---

## 4. 重要 PR 进展（Top 10）

### #5313 — chore(release): prepare v0.9.6
- **作者**: Hmbown | **状态**: CLOSED | **更新**: 2026-08-09
- **要点**: v0.9.6 发布准备——重构 compaction（provider 单一摘要 + successor handoff），移除 mailbox 冻结问题，并对工具执行采取“减法”策略；明确移除 harness 自动注入但保留显式预算/截止能力。
- **链接**: https://github.com/Hmbown/CodeWhale/pull/5313

### #5133 — feat(runtime-api): expose persistent goal-loop state and completion controls
- **作者**: Copilot | **状态**: CLOSED | **更新**: 2026-08-09
- **要点**: v0.9.4 Runtime HTTP API 新增 goal 资源：`GET /v1/threads/{id}/goal` 读取活跃目标状态，并提供生命周期控制端点。托管客户端首次获得目标循环的可编程控制面。
- **链接**: https://github.com/Hmbown/CodeWhale/pull/5133

### #5132 — Runtime API: expose verifier receipts and evidence beyond the aggregate counter
- **作者**: Copilot | **状态**: CLOSED | **更新**: 2026-08-09
- **要点**: Fleet 此前仅有 `verifier_failed` 计数器，无法区分失败任务与原因。新增三个只读端点（`receipts`/`receipts/{id}`/`receipts/{id}/evidence`）用于任务级验证追溯与重试决策。
- **链接**: https://github.com/Hmbown/CodeWhale/pull/5132

### #5130 — feat(runtime-api): bounded MCP server configuration and lifecycle management
- **作者**: Copilot | **状态**: CLOSED | **更新**: 2026-08-09
- **要点**: 为 MCP server 提供完整的增删改查路由（`POST/PUT/DELETE /v1/apps/mcp/servers`），并支持列表/详情查询。替代手工编辑 TOML/JSON 的流程。
- **链接**: https://github.com/Hmbown/CodeWhale/pull/5130

### #5129 — feat(runtime-api): add skill lifecycle endpoints — install, update, uninstall, trust, audit
- **作者**: Copilot | **状态**: CLOSED | **更新**: 2026-08-09
- **要点**: Skill 管理从“发现 + 启用/禁用”扩展到完整生命周期：安装、更新、卸载、信任标记与审计日志，全部经 `require_runtime_token` 保护。
- **链接**: https://github.com/Hmbown/CodeWhale/pull/5129

### #5131 — feat: Runtime API memory endpoints — bounded inspection and lifecycle controls
- **作者**: Copilot | **状态**: CLOSED | **更新**: 2026-08-09
- **要点**: Memory 资源从不可见变为可编程管理：`GET /v1/memory` 查看内容、作用域与来源；`DELETE` 支持定向清理。面向需要细粒度内存查看的托管客户端（如桌面/Web 应用）。
- **链接**: https://github.com/Hmbown/CodeWhale/pull/5131

### #5295 — feat: add Mistral AI as a first-class provider route
- **作者**: xavierpestel-ai（首次贡献者） | **状态**: CLOSED | **更新**: 2026-08-09
- **要点**: 新增 Mistral AI（la Plateforme）为一等 provider，支持 `provider = "mistral"`、`CODEWHALE_PROVIDER=mistral` 及 `--provider` 参数，默认模型 `mistral-code-latest`。由社区贡献者独立完成。
- **链接**: https://github.com/Hmbown/CodeWhale/pull/5295

### #5205 — Stabilize IME candidate positioning in Tabby
- **作者**: Copilot | **状态**: CLOSED | **更新**: 2026-08-09
- **要点**: 针对 Tabby 终端（Electron/xterm.js）中文输入法候选窗跳动问题，增加 `TERM_PROGRAM=Tabby` 检测、低动态渲染模式与有界重绘节奏。与 #5023 形成对应关系。
- **链接**: https://github.com/Hmbown/CodeWhale/pull/5205

### #5301 — fix(tui): make compaction live and pressure-aware
- **作者**: Hmbown | **状态**: CLOSED | **更新**: 2026-08-08
- **要点**: `/compact` 改为非阻塞入队，结合类型化生命周期 ID 序列化；128K/272K/1M 自动压缩阈值对齐完整请求压力；改进活动操作的重新锚定逻辑。
- **链接**: https://github.com/Hmbown/CodeWhale/pull/5301

### #5308 — fix(release): use CNB asset download URLs
- **作者**: Hmbown | **状态**: CLOSED | **更新**: 2026-08-09
- **要点**: 修复镜像模式下发布资产下载回退到 HTML 而非实际资产字节的问题，改用 CNB 仓库标准 slug 与 `/-/releases/download/vX.Y.Z/` 路径。
- **链接**: https://github.com/Hmbown/CodeWhale/pull/5308

---

## 5. 功能需求趋势

- **Compaction 行为透明化与可配置化**：围绕“模型支持 1M 但 128K 就压缩”的困惑持续升温（#5096、#5239、#5134、#5043），用户不仅要求正确的上下文窗口推导，还要求“降级时明确提示”（#5244）以及“压缩保留意图、决策与工具连续性”的结构化合同（#4394）。
- **多 Provider / 多 Key 管理**：不再满足于单一 provider 的深度适配——社区明确表达需要同时保存多个 API Key、switch provider 时模型/密钥同步切换（#5250、#5034），以及更多一等公民 provider（Mistral 已入，见 #5295）。
- **TUI 与 CLI/API 的面向外部的控制面一致性**：Copilot 系列 PR（#5129-#5133）补全了 Runtime API 的 goal/memory/skill/MCP 管理能力，与 #4022 中“CLI/TUI parity”的目标形成闭环——用户希望同样强大的能力不被困在终端里。
- **可观察性与真实性**：用户对“显示成功但实际未生效”的容忍度极低。多个 Issue（#5096、#5209、#5098）指向同一诉求——界面显示的每一个状态都必须是真实可信的，不允许静默失败或静默回退。

---

## 6. 开发者关注点

- **静默降级与假成功的信任危机**：未知模型缩到 128K 不提示（#5244）、误用参数名却返回成功（#5209）、配置改了但没反映到运行状态（#5098）——三个 Issue 指向同一个核心诉求：开发者不怕失败，怕“看起来成功”的假象。
- **中文输入法与本地化体验**：IME 候选窗跳动（#5023）、翻译选词争议（#4949）以及“Copy message 带装饰符”（#5314）显示中文社区作为活跃用户群体的日常摩擦正在被看见并被讨论。
- **多 Provider 工作流仍是现实痛点**：多个 key 无法共存（#5250）、provider 切换后模型残留（#5034）说明“多模型日常混用”已成为 TUI 用户的标准工作方式，而工具的设计仍偏向单 provider 假设。
- **权限对话框默认选项变更引发 UX 惯性冲突**：#5293 虽有安全理由，但“习惯性回车”的用户可能因此误拒绝操作。安全设计与高效交互之间的默认值权衡，值得产品层审慎决策。

</details>

---
*本日报由 [agents-radar](https://github.com/kky-wollu/agents-radar) 自动生成。*
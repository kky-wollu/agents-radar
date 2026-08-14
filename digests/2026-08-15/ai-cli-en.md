# AI CLI Tools Community Digest 2026-08-15

> Generated: 2026-08-14 22:28 UTC | Tools covered: 9

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

## Cross-Tool Comparison

# Cross-Tool AI CLI Comparison Report
**Date:** 2026-08-15

---

## 1. Ecosystem Overview

The AI CLI tool ecosystem is entering a **maturity phase characterized by scaling pains**. Across all seven tools analyzed, the dominant themes are reliability issues under real-world workloads (silent failures, resource leaks, concurrency bugs) and a collective push toward persistent memory, sub-agent orchestration, and cross-platform parity. Windows remains the weakest platform across nearly every tool, with performance regressions (Codex), shell instability (Kimi, Gemini), and adoption barriers (Pi) concentrated there. Enterprise adoption is driving demand for OAuth compliance, model availability consistency, and audit-friendly telemetry, while the community's most vocal frustrations center on **silent cost leaks, false success reporting, and configuration that silently fails**.

---

## 2. Activity Comparison

| Tool | Releases (24h) | Hot Issues | Key PRs | Notable Signals |
|---|---|---|---|---|
| **Claude Code** | 2 (v2.1.232, v2.1.233) | 10 tracked | 5 | Subagent forking default-on; GitLab MR support |
| **OpenAI Codex** | 6 alphas (v0.148.0-a.13–18) | 10 tracked | 10 merged | Windows perf regression crisis; unified exec default |
| **Gemini CLI** | 1 nightly | 10 tracked | 9 merged + 1 open | SSR Agent initiative; 8 PRs landed; PTY leak fixes |
| **Copilot CLI** | 1 (v1.0.80) | 10 tracked | 3 | MCP OAuth regression; enterprise model availability broken |
| **Kimi CLI** | 0 | 4 tracked | 0 | Stalled; memory feature remains top ask |
| **OpenCode** | 0 | 10 tracked | 10 closed/merged | **Critical 48-bit timestamp wraparound bug**; dynamic model discovery PR lands |
| **Pi** | 1 (v0.84.2) | 10 tracked | 10+ | Windows support survey; compaction improvements |
| **Qwen Code** | 2 (v0.21.12 + preview) | 10 tracked | 10+ | Web Shell uploads; security hardening; CI flakiness |
| **DeepSeek/Codewhale** | 1 (v0.9.8) | 10 tracked | 10 | Rebrand; red CI; P0 web UI regression |

**Release velocity leaders:** OpenAI Codex (6 alphas/day), Claude Code, Qwen Code, Pi

**Community engagement leaders:** Claude Code (73 comments on top issue), OpenCode (131 comments on memory megathread), Codex (100 comments on Windows issue)

---

## 3. Shared Feature Directions

| Direction | Tools | Specific Needs |
|---|---|---|
| **Persistent memory / cross-session context** | Claude Code, Kimi CLI, OpenCode, Gemini CLI, Copilot CLI | Structured memory protocols beyond single `agent.md`; auto-maintained project patterns; deterministic redaction before sending to model (Gemini #26525); bounded memory retries (OpenCode memory megathread) |
| **Sub-agent orchestration & observability** | Claude Code, Gemini CLI, Copilot CLI, OpenCode, Codewhale | Centralized permission/approval pane (Claude #70591); truthful termination reporting (Gemini #22323); agent-to-agent delegation (Gemini #28738); fleet identity clarity (Codewhale #5287) |
| **Configurable input/keybindings** | Claude Code (#2054, 147👍), Gemini, Copilot CLI | Enter-to-send → configurable; CJK users disproportionately affected |
| **Cross-platform parity (especially Windows)** | Codex, Kimi, Pi, Gemini CLI, Qwen Code | Windows performance regressions; shell tool stability (PowerShell); WSL login hangs; native vs. WSL path confusion |
| **Provider/model breadth & auto-discovery** | OpenCode (#42660), Qwen Code (#8368), Pi (#8113), Copilot CLI | Dynamic model discovery from OpenAI-compatible endpoints; first-class presets for third-party providers (Kimi, SiliconFlow, Xiaomi) |
| **Rate-limit transparency & accurate accounting** | Claude Code (#79773), Gemini (#1473, #1474), Pi (#8075), OpenCode (#42606) | False 429s; Max-tier limits not applied; cache-token accounting accuracy; "paid but no balance" billing bugs |
| **Context compaction fidelity** | Codex (#29356), Claude Code, OpenCode, Pi, Gemini CLI | Preserve operational steps; never lose reasoning context; compaction marker identity |
| **Remote session handoff / multi-device** | Kimi (#2269), Codex (#28919), Claude Code | Continue sessions across devices; remote device control on all platforms |
| **Notifications for background work** | Claude Code (#65241), Qwen Code | IDE/VS Code notifications on limit resets, task completion — don't watch terminal |

---

## 4. Differentiation Analysis

| Tool | Primary Focus | Target User | Technical Approach | Distinctive Strengths | Key Weaknesses |
|---|---|---|---|---|---|
| **Claude Code** | Enterprise safety, deep IDE integration | Professional dev teams, proxy deployments | Fork-based subagents, prompt-cache inheritance, apps gateway | Most mature safety/permissions; GitLab-aware worktrees; largest community | Silent cost leaks (image processing); safety-filter false positives on security work |
| **OpenAI Codex** | Cross-platform desktop + CLI unification | Windows-heavy users, Chrome ecosystem | Rust alpha line; gRPC code-mode; Electron desktop | Fastest iteration; aggressive unification (exec, skills removal) | **Windows performance crisis** eroding confidence; context compaction unreliable |
| **Gemini CLI** | Agent autonomy, SSR agent architecture | Power users, sandboxed execution | SSR Agent (subagent recovery); PTY management; Auto Memory | Self-aware agent design; strong contributor velocity; good hang fix cadence | Generalist agent hangs; false GOAL success; privacy concerns with Auto Memory |
| **Copilot CLI** | GitHub-centric automation, marketplace | Enterprise GitHub users, CI/CD pipelines | MCP integration; autopilot; permissions config | GitHub Actions hardening; org policy integration; plugin ecosystem | MCP OAuth broken (Atlassian/GitLab); enterprise model availability broken; session data loss |
| **Kimi CLI** | Lightweight, focused CLI experience | Individual developers, Chinese-market users | Minimal feature surface; agent.md-based memory | Simplicity; active user desire for memory layer | **Stalled development**; no releases/PRs; Windows shell bugs unaddressed |
| **OpenCode** | Hackable, provider-agnostic TUI | Tinkerers, self-hosters, LangChain ecosystem | Go core; sub-agent question queueing; protocol refactoring | Strong maintainer community; excellent contributor velocity (10 PRs/day); dynamic model discovery | **Time-based ID wraparound** critical bug; TUI perf under concurrency; billing trust issues |
| **Pi** | Terminal-native, minimal config | Terminal purists, extension developers | Fullscreen transcript; compaction via prompt-cache reuse; heterogeneous providers | Excellent UX polish (clipboard, transcripts, search); active provider contributions | Windows fragmentation; OAuth 429 rate-limiting; compiler-driven extension ecosystem still maturing |
| **Qwen Code** | Full-stack AI dev (CLI + Web Shell + SDK) | Chinese-market + English, Web Shell advocates | Daemon architecture; ACP bridge; Web Shell as canonical UI | Security hardening (PAT isolation, file containment); review infrastructure (capture-tui) | CI flakiness; daemon resource leaks; SDK/CLI inconsistencies |
| **Codewhale** | Auto-review, agentic workflows | Security review teams, multi-agent workflows | Model Guardian two-layer review; write-claim scoping; thinking ladder vocabulary | Novel auto-review denial rationale; contributor-driven turnarounds | **Red CI on release**; P0 web UI regression; output-token clamp |

---

## 5. Community Momentum & Maturity

### Mature, Large Communities (100+ weekly issue comments)
- **Claude Code** — Largest issue engagement (#60334 at 73 comments); strongest third-party extension ecosystem; most stable release cadence
- **OpenAI Codex** — Very high user volume; 100-comment Windows issue; ~20 merged PRs/day across ecosystem; but quality confidence is flagging due to Windows regressions

### Rapidly Iterating with Strong Contributor Velocity
- **OpenCode** — 10+ PRs merged in 24h; opencode-agent[bot] contributing fixes; healthy maintainer-response loop (ID wraparound acknowledged within hours)
- **Gemini CLI** — 8 PRs landed in 24h targeting SSR Agent; community contributors fixing PTY leaks independently
- **Qwen Code** — Fast release cadence (v0.21.12 + previews); security fixes landing quickly; Web Shell feature velocity high

### Emerging or Niche Communities
- **Pi** — Growing steadily; maintainer-driven roadmap; contributor momentum around providers (SiliconFlow, xAI); Windows adoption push is community-led
- **Codewhale (DeepSeek)** — Small but passionate community; contributors (Lstarsky0) filing and fixing CI issues within hours; rebrand signals product ambition

### Stalled
- **Kimi CLI** — No releases, no PRs, no maintainer response to top issues in 24h; community engagement persists but development appears paused

---

## 6. Trend Signals

### High-Confidence Signals (Recurring Across 3+ Tools)

1. **Silent failures are the #1 trust killer.** From Claude's image-processing cost leak (#60334) to Codex's idle CPU spin (#38547) to Gemini's false GOAL success (#22323) to Codewhale's session-index data loss (#5380) — tools that report success while failing will lose users. **Action:** Prioritize explicit failure diagnostics, even if it means more noise.

2. **Windows is the new "second-class citizen" — and it's costly.** Codex's Windows regressions dominate its backlog; Kimi's shell bugs go unfixed; Pi's Windows survey is a roadmap; Qwen has only nightly Windows coverage. **Action:** Treat Windows as a first-class target immediately — the community is actively pushing back.

3. **Enterprise adoption is being blocked by three issues:**
   - **OAuth compliance** (Copilot's RFC 8414 miss, Pi's Copilot 429s)
   - **Model availability consistency** (Copilot's org-enabled models missing)
   - **Audit-friendly telemetry** (Claude's `forward_user_identity`; Codex's permission profile snapshots)
   Closing these gaps is table-stakes for enterprise procurement.

4. **Memory systems are the next battleground.** Kimi users demand it; OpenCode maintains a 131-comment megathread; Gemini's Auto Memory has privacy concerns; Claude ships context inheritance in forks. The winner will nail **deterministic, private, and bounded** memory — not just "we remember stuff." Redaction must happen before model context, not in-prompt.

5. **Sub-agent orchestration is moving from feature to platform.** Users want delegation, observation, permission centralization, and truthful status reporting across concurrent agents. The tools that standardize this (Claude's fork model, Gemini's SSR Agent, Codex's gRPC code-mode) will define the multi-agent UX patterns for 2027.

6. **Config that silently doesn't take effect is a recurring wound.** `MCP_TIMEOUT` capped at 60s (Claude), Max-20x limits not applied (Claude), `allowed_directories` not suppressing prompts (Copilot), `permission_mode="auto"` rejected by SDK (Qwen). **Action:** Add validation and explicit error reporting when configuration cannot be honored as written.

### Emerging Signals (Still Formative)

7. **Release-quality confidence is dipping for fast-moving tools.** Codex's consecutive Windows regressions and Codewhale's red CI on release day suggest velocity is outpacing quality gates. Community calls for "revert please" are increasing.

8. **Security hardening is becoming a differentiator.** Qwen's PAT isolation, Copilot's `pull_request_target` migration, and Codewhale's file-containment hardening are building trust. Expect security to be a checklist item in procurement.

9. **Scriptability/CI automation is an undervalued gap.** Users want headless, pure-CLI operation (Pi #8114, Qwen's `NO_TOOL_RESULT_PROGRESS` brittleness). Tools that nail deterministic headless mode will win automation-heavy teams.

10. **Provider-agnosticism is the backstop.** As model churn accelerates (GLM, Kimi, xAI, MiniMax), tools with dynamic discovery (OpenCode #42660) and built-in provider breadth (Pi, Qwen, Codewhale) will retain users who switch models frequently.

---

*Report compiled from community digest data for 9 tools across 24h on 2026-08-15. For decision-makers: prioritize fixes in this order — (1) silent failure diagnostics, (2) Windows parity, (3) enterprise OAuth/model availability, (4) memory system trust, (5) sub-agent orchestration reliability.*

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

Here is the Claude Code Skills community highlights report based on the provided data.

---

### 1. Top Skills Ranking

The most active discussions revolve around fixing and enhancing the **skill-creator** meta-skill, alongside proposals for new domain-specific skills.

- **Fix skill-creator `run_eval.py` (PR #1298, #1099, #1050)** — This cluster of PRs addresses a critical bug in the skill-creator's evaluation loop, which consistently reports `recall=0%` and renders the tool useless for optimizing skill descriptions. Issues #556 and #1169 document the problem in detail. The fixes target Windows subprocess stream handling, encoding bugs, and artifact installation.
    - **Functionality**: These are bug fixes for the `skill-creator` utility, not standalone skills.
    - **Discussion Highlights**: The emphasis is on making the evaluation loop functional cross-platform (specifically Windows) and ensuring it tests against installed skills rather than a temporary file.
    - **Status**: All are **Open** and unmerged, indicating this is a persistent and acknowledged pain point in the developer workflow.
    - **Links**: [PR #1298](https://github.com/anthropics/skills/pull/1298), [PR #1099](https://github.com/anthropics/skills/pull/1099), [PR #1050](https://github.com/anthropics/skills/pull/1050)

- **Add document-typography skill (PR #514)** — Proposes a skill for typographic quality control on generated documents (e.g., preventing orphan words, stranded headers).
    - **Functionality**: Prevents common, subtle typographic issues in AI-generated documents that affect professional quality.
    - **Discussion Highlights**: Addresses a highly universal problem—these typographic issues affect every document Claude generates—making it a potentially high-value addition for any documentation or report generation workflow.
    - **Status**: **Open**, awaiting merge or further refinement.
    - **Link**: [PR #514](https://github.com/anthropics/skills/pull/514)

- **Add ServiceNow platform skill (PR #568)** — This is a large, ambitious PR proposing a comprehensive skill to act as a platform assistant for ServiceNow.
    - **Functionality**: Covers a wide range of ServiceNow modules (ITSM, ITOM, SecOps, HR, CSM, etc.) as a broad assistant rather than a narrow scripting helper.
    - **Discussion Highlights**: The discussion likely centers on the skill's massive scope and how to keep it maintainable and actionable within a single skill.
    - **Status**: **Open** and continuously updated (last updated 2026-08-12), demonstrating active community interest in enterprise platform support.
    - **Link**: [PR #568](https://github.com/anthropics/skills/pull/568)

- **Add testing-patterns skill (PR #723)** — Adds a comprehensive skill covering the full testing stack, including philosophy (Testing Trophy), unit testing, and React component testing.
    - **Functionality**: Serves as a guide and agent instructions for writing high-quality tests across the stack.
    - **Discussion Highlights**: Responds to a clear community need for reliable, structured test generation and coaching.
    - **Status**: **Open**, awaiting review.
    - **Link**: [PR #723](https://github.com/anthropics/skills/pull/723)

- **Add pyxel skill for retro game development (PR #525)** — A new skill for creating retro/pixel-art/8-bit games in Python using the Pyxel engine and an MCP server.
    - **Functionality**: Streamlines a specific creative workflow (write code → run game → capture screen → iterate).
    - **Discussion Highlights**: Highlights the community's interest in using Skills for specialized, creative development loops.
    - **Status**: **Open** and actively updated (last updated 2026-07-15).
    - **Link**: [PR #525](https://github.com/anthropics/skills/pull/525)

---

### 2. Community Demand Trends

Analysis of the top issues reveals several clear demands from the community:

- **Reliable Skill Development Tools**: The single largest trend is the demand for a working **skill-creator**. The recurring `recall=0%` bug (Issues #556, #1169) and the desire to bring skills back under the "Agent Skills spec" (PR #1538) show that developers want robust, deterministic tooling to build and test skills effectively.
- **Security & Trust Boundaries**: Issue #492, with 43 comments, highlights deep concern about **trust and security**. The community is worried about malicious skills distributed under the official `anthropic/` namespace, requesting clear security analysis and safe distribution mechanisms.
- **Enterprise & Workflow Automation**: There is interest in Skills that cater to enterprise platforms (**ServiceNow** PR #568) and governance (**agent-governance** Issue #412). This points to a demand for Skills that automate complex, domain-specific work processes.
- **Document/File Handling**: Issues regarding SharePoint Online (Issue #1175) and white-space corruption in OOXML (Issue #12) show a continuous need for **robust and secure document manipulation** skills, particularly for enterprise collaboration suites.
- **Skill Lifecycle & Management**: Issue #228 (org-wide sharing) and Issue #189 (duplicate skills from plugins) indicate the community is outgrowing the basic skill installation model and needs **better distribution, sharing, and lifecycle management** at scale.

---

### 3. High-Potential Pending Skills

These are active PRs with clear value propositions that have not yet been merged but could land soon:

- **ServiceNow Platform Skill (PR #568)**: This is the most prominent pending skill, addressing a massive enterprise market. Despite its large scope, it is actively maintained and will be a major addition if merged.
- **Self-Audit Skill (PR #1367)**: Proposes a meta-skill for auditing AI output—mechanical file verification followed by a reasoning quality gate. This aligns with the growing community focus on quality and safety.
- **Plan-File-Hygiene Skill (PR #1479)**: Addresses a common problem of accumulated planning artifacts by adding a lifecycle management skill.
- **Testing-Patterns Skill (PR #723)**: A comprehensive, universally useful skill that will likely be welcomed by developers looking for structured coding support.
- **Document-Typography Skill (PR #514)**: The broad applicability of this fix makes it a likely candidate for merging.

---

### 4. Skills Ecosystem Insight

The community's most concentrated demand is for **enterprise-grade reliability, security, and developer tooling (specifically a working `skill-creator`)**, indicating a shift from creating novelty skills to building a trustworthy and robust ecosystem for professional use.

---

# Claude Code Community Digest
**2026-08-15**

---

## Today's Highlights

Two significant releases landed this week: **v2.1.232** turns on subagent forking by default (a major workflow change — forked subagents now inherit the full conversation and prompt cache, with background execution for non-teammate agents), and **v2.1.233** adds GitLab MR URL support in worktrees and an opt-in `forward_user_identity` gateway setting for proxy deployments. The community is also buzzing about a long-running image-processing bug (#60334) that has burned ~70% of some users' rate-limit windows, making it the most active issue at 73 comments.

---

## Releases

### v2.1.233
- **GitLab merge request URL support** added to the `--worktree` flag and the `claude agents` view (MRs display as `!N`)
- **Opt-in `forward_user_identity`** apps gateway setting on Anthropic upstreams — sends signed-in user identity as headers, enabling richer authentication in proxy setups

### v2.1.232
- **Subagent forking is now default-on**: `subagent_type: "fork"` subagents inherit the full conversation and prompt cache
- **Background execution**: non-teammate agent spawns in interactive sessions now run in the background by default
- **Session mention**: type `@` in the prompt to mention another Claude session by name

---

## Hot Issues

1. **[#60334 — Image processing failures causing conversation token waste](https://github.com/anthropics/claude-code/issues/60334)** *(CLOSED, 73 comments, 19 👍)*
   The top community pain point this week. Users report API errors like *"an image in the conversation could not be processed and was removed"* burning ~70% of their 5-hour rate-limit window with no visible images in the conversation. High severity: it's a silent cost leak.

2. **[#2054 — Insert new line with Enter instead of sending](https://github.com/anthropics/claude-code/issues/2054)** *(OPEN, 28 comments, 147 👍)*
   The most-upvoted open enhancement (147 👍). CJK-language users (and many others) accidentally send incomplete messages because Enter submits. The request: an option to change the keybinding so Enter inserts a newline and something else (e.g., Shift+Enter or Ctrl+Enter) sends.

3. **[#16837 — MCP_TIMEOUT longer than 60 seconds not obeyed](https://github.com/anthropics/claude-code/issues/16837)** *(OPEN, 15 comments, 16 👍)*
   A reproducible bug on Linux where the `MCP_TIMEOUT` environment variable is capped at 60 seconds regardless of configured value. This breaks long-running MCP tools that legitimately need more time.

4. **[#82092 — Apps gateway serves Claude Desktop an OTLP endpoint without headers](https://github.com/anthropics/claude-code/issues/82092)** *(OPEN, 13 comments, 5 👍)*
   A subtle infrastructure bug: the apps gateway serves Claude Desktop an `otlpEndpoint` pointing to its own bearer-gated OTLP ingest but omits `otlpHeaders`. Every desktop telemetry flush gets rejected with `missing_token` — telemetry is silently broken.

5. **[#79773 — Max 20x upgrade not reflected in weekly limits](https://github.com/anthropics/claude-code/issues/79773)** *(OPEN, 7 comments)*
   Users who upgraded to Max 20x on July 16 report that weekly limits are still depleting at the Max 5x rate or worse. Billing and rate-limit accounting appear out of sync.

6. **[#84474 — Workflow-backed code review PR comment posting silently fails](https://github.com/anthropics/claude-code/issues/84474)** *(OPEN, 3 comments)*
   A reliability concern for CI users: the "post review to the PR" step reports `completed` with full findings, but the comment never lands on the PR. Silent failure makes this hard to troubleshoot.

7. **[#71950 — Intermittent reasonless permission denial on Edit/Write](https://github.com/anthropics/claude-code/issues/71950)** *(CLOSED, 3 comments, 1 👍)*
   `Edit` and `Write` tool calls intermittently denied with a bare message — even with `bypassPermissions` enabled. No explanation string is included, making it difficult to debug why a denial occurred.

8. **[#65502 — Permissions docs omit `$HOME` path matching for Read deny rules](https://github.com/anthropics/claude-code/issues/65502)** *(CLOSED, 4 comments)*
   Documentation gap: the permissions page doesn't explain how `~/path` home-directory patterns are matched for Bash `Read(...)` deny rules. Users configuring deny rules for home paths may be surprised by behavior.

9. **[#70591 — Centralized Permission & Approval Notifications for Multi-Agent Workflows](https://github.com/anthropics/claude-code/issues/70591)** *(CLOSED, 4 comments)*
   A feature request for a unified view of permission prompts and approvals across parallel agents. Multi-agent workflows currently scatter approval requests across sessions, making review difficult.

10. **[#65241 — Notification system for VS Code extension](https://github.com/anthropics/claude-code/issues/65241)** *(CLOSED, 3 comments)*
    Request for native notifications in the VS Code extension for limit resets, task completions, and session events — so developers don't have to watch the terminal.

*Note: The issue list contains a cluster of ~20 related closed issues from user `sworrl` (#71916–#71992) about cybersecurity safety-filter false positives blocking legitimate drone/security research work. These were all triaged as duplicates and closed, but the volume suggests a systematic problem with the safety classifier on legitimate security/RE tasks.*

---

## Key PR Progress

1. **[#86746 — fix(security-guidance): preserve Python probe errors](https://github.com/anthropics/claude-code/pull/86746)** *(OPEN)*
   Fixes #86709 by preserving stderr from Python interpreter probes and reporting diagnostics when `python3`, `python`, and `py -3` all fail. Previously, errors were discarded to `/dev/null`, leaving users with a generic failure message.

2. **[#86626 — feat: add shell completions (bash, zsh, fish)](https://github.com/anthropics/claude-code/pull/86626)** *(OPEN)*
   Adds tab-completion scripts for the `claude` CLI across bash (including stock macOS 3.2), zsh, and fish, with an install README. Keeps completions in sync with the installed CLI.

3. **[#86537 — Fix duplicated word in CHANGELOG.md](https://github.com/anthropics/claude-code/pull/86537)** *(OPEN)*
   Documentation-only typo fix: corrects "to to" in the `CLAUDE_BASH_NO_LOGIN` changelog entry from v1.0.124.

4. **[#83890 — Create pylint.yml](https://github.com/anthropics/claude-code/pull/83890)** *(OPEN)*
   Adds a pylint CI workflow. Low-risk quality-infrastructure addition, though the description is empty.

5. **[#41611 — add the missing source to claude code](https://github.com/anthropics/claude-code/pull/41611)** *(OPEN)*
   Open since March 2026. The PR aims to add a missing source reference. Long-dormant — likely stale or needs maintainer review.

---

## Feature Request Trends

1. **Input keybinding flexibility** — The #2054 request (Enter-to-send → configurable) has 147 👍 and is the single most-requested enhancement. CJK users are disproportionately affected, but the ask is universal: let users remap submit vs. newline.

2. **Centralized multi-agent control** — Multiple requests (#70591, plus v2.1.232's background-agent changes) point to a growing need for unified monitoring, approval, and permission management across concurrent agents. Users want a single pane of glass for multi-agent workflows.

3. **IDE/editor notifications** — #65241 asks for VS Code notifications on limit resets, task completion, and session events. As Claude Code becomes more background-oriented, users want to leave the terminal without missing events.

4. **Proxy/gateway authentication** — The `forward_user_identity` gateway setting in v2.1.233 addresses a real enterprise need: passing signed-in user identity through proxies for audit and authorization. Expect more work here.

5. **Rate-limit transparency** — Issue #79773 highlights that users want clearer visibility into how subscription tier upgrades affect their actual usage limits — and accounting bugs when it goes wrong.

6. **Shell completions** — PR #86626 (bash/zsh/fish completions) has clear community appetite for better terminal ergonomics.

---

## Developer Pain Points

1. **Silent cost leaks** — Image processing failures (#60334, 73 comments) quietly consume rate limits without user awareness. This is the top pain point: users can't tell what's burning their window until it's gone. The closed-but-echoing issue history suggests the release pressure around this was significant, but the community wants better diagnostics.

2. **Silent failures** — From PR comment posting (#84474) to permission denials (#71950) to telemetry drops (#82092), a recurring theme is **failures that report success**. The `bypassPermissions` issue (#71950) is especially worrying — denial with no reason even in bypass mode.

3. **Safety-filter false positives** — The `sworrl` cluster of ~20 closed issues documents systematic false-positive blocks on legitimate security research, reverse engineering, and drone/device work. All were closed as duplicates, but the volume suggests a real problem: the safety classifier is overly aggressive on legitimate security/RE tasks, halting sessions mid-work.

4. **Configuration not honored** — `MCP_TIMEOUT` capped at 60s (#16837) and Max-20x limits not applied (#79773) are examples of configurations that silently don't take effect. When settings fail silently, troubleshooting is expensive.

5. **Keybinding accidents** — #2054's 147 👍 and CJK-specific pain point highlight that the default Enter-to-send binding causes real daily friction for a large user base. The fix is simple (configurable binding); the demand is clear.

---

*Digest generated from 2 releases, 30+ issues, and 5 PRs at [github.com/anthropics/claude-code](https://github.com/anthropics/claude-code) on 2026-08-15.*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-08-15

## Today's Highlights

The Codex team shipped a rapid sequence of Rust alpha releases (v0.148.0-alpha.13 through alpha.18) alongside a batch of ~20 merged PRs focused on TUI startup reliability, gRPC code-mode session limits, and MCP protocol discovery. However, the community's attention is dominated by a spike of Windows-specific performance regressions — multiple new reports describe severe system-wide mouse lag, CPU busy loops, and stuttering in the latest desktop app builds (26.810.x), with users calling for an immediate revert. Additionally, a new architectural shift is underway: PR #38625 enables unified exec on Windows by default, and PR #38635 removes repository-local Codex skills.

## Releases

Six pre-release alpha builds were published in the last 24 hours: `rust-v0.148.0-alpha.13` through `rust-v0.148.0-alpha.18`. Release notes are minimal ("Release 0.148.0-alpha.X"), suggesting focused iterative fixes rather than large feature bundles.

## Hot Issues

1. **[#20214 — Codex App frequently freezes/stutters on Windows 11 Pro](https://github.com/openai/codex/issues/20214)** — 100 comments, 84 👍. The longest-running Windows performance complaint continues to accumulate upvotes. Users with sufficient RAM/CPU report persistent UI freezes; this issue now serves as a canonical aggregation point for similar reports.

2. **[#34260 — Unbounded taskkill.exe/conhost.exe cleanup storm exhausts WMI](https://github.com/openai/codex/issues/34260)** — 35 comments. A deeply technical report describing a process-cleanup loop on Windows Desktop where hundreds of `taskkill` processes query Win32_Process, exhausting WMI provider quotas. Critical infrastructure issue with a clear performance kill-chain.

3. **[#28919 — Windows Codex app missing "Control other devices" tab](https://github.com/openai/codex/issues/28919)** — 33 comments, 34 👍. Users on Windows cannot access the remote control/devices settings tab present on other platforms. High engagement suggests remote session capability is a widely needed workflow.

4. **[#29356 — Context compaction loses operational continuity in long tasks](https://github.com/openai/codex/issues/29356)** — 21 comments. Users with long-running sessions report that context compaction drops operational steps, forcing re-work. Community suggests preserving last five operational steps verbatim.

5. **[#38547 — Idle main-process CPU busy loop in Chrome plugin app-server](https://github.com/openai/codex/issues/38547)** — 11 comments. New regression (introduced in 26.810.4967.0) causing persistent Electron main-process CPU spin while completely idle — no browsing needed. One of today's most impactful new reports.

6. **[#38583 — ChatGPT/Codex causes persistent system-wide mouse lag and ~10% CPU while idle](https://github.com/openai/codex/issues/38583)** — 10 comments. Build 26.813.12317 introduces system-wide input lag with ~10% idle CPU. Multiple users confirm; community is frustrated by the pattern of regressions across consecutive releases.

7. **[#38546 — System-wide mouse stutter when running without elevation](https://github.com/openai/codex/issues/38546)** — 7 comments. A distinct but related performance report. Users note that running Codex as admin sometimes "fixes" the stutter, pointing to possible permission-related code path differences.

8. **[#38323 — Codex CLI 0.146.0: /compact endpoint returns 404](https://github.com/openai/codex/issues/38323)** — 5 comments. CLI users hit a hard failure: `/backend-api/codex/responses/compact` returns 404 in 0.146.0. Breaks context compaction for `gpt-5.6-sol` on macOS — a functional regression, not just performance.

9. **[#38629 — Opening active conversation in another VS Code window transfers ownership](https://github.com/openai/codex/issues/38629)** — 4 comments. IDE extension bug allowing concurrent turns when a session is opened in two windows, silently transferring ownership. Concurrency concern for multi-window VS Code users.

10. **[#38637 — "New Codex release very unstable and high CPU usage on mac, crashes constantly!"](https://github.com/openai/codex/issues/38637)** — 4 comments. Signal that performance regressions are not Windows-only; macOS build 26.810.41047 crashes within minutes and struggles with long chats. Community requests immediate revert.

## Key PR Progress

1. **[#38625 — Enable unified exec by default on Windows](https://github.com/openai/codex/pull/38625)** — Stabilizes `unified_exec` on all platforms, standardizing `exec_command`/`write_stdin` on Windows (replacing `shell_command`). Cross-platform behavior unification milestone.

2. **[#38635 — Remove repository-local Codex skills](https://github.com/openai/codex/pull/38635)** — Removes `codex-bug`, `codex-issue-digest`, and `pushing-ci-changes` skills from the repo. Indicates a platform-level strategy shift away from self-hosting community maintenance skills.

3. **[#38630 — Remove the gRPC code-mode open session limit](https://github.com/openai/codex/pull/38630)** — Removes `MAX_IN_FLIGHT_REQUESTS` cap on open sessions; keeps limits on in-flight, control requests, and active cells. Unlocks parallel code-mode workflows.

4. **[#38641 / #38642 / #38643 — TUI startup input handling + provisional composer](https://github.com/openai/codex/pull/38641)** — A coordinated set of TUI UX improvements: hardens startup against stray keystrokes, keeps the composer editable while app-server initializes, and delays composer until first-login onboarding completes.

5. **[#38628 — Make Guardian v2 risk classification configurable](https://github.com/openai/codex/pull/38628)** — Guardian v2 becomes tunable: classifier instructions, review thresholds, reasoning effort, and token limits can be configured, plus transcript controls.

6. **[#38634 — Add MCP protocol discovery metrics](https://github.com/openai/codex/pull/38634)** — Observability for MCP client discovery: counter/duration, tagged by mode (`legacy`/`auto`) and outcome (`modern`/`legacy`/`failure`). Helps identify migration bottlenecks.

7. **[#38623 — Preserve MCP namespace descriptions in tool catalog cache](https://github.com/openai/codex/pull/38623)** — Fixes missing server instructions for lazily-started MCP connections; cached definitions now expose namespace descriptions immediately.

8. **[#38645 — Deliver gRPC code-mode notifications without truncation](https://github.com/openai/codex/pull/38645)** — Removes the 1,024-byte truncation on code-mode notification text and adds multibyte integration tests.

9. **[#38651 — Move permission profile snapshots into the protocol](https://github.com/openai/codex/pull/38651)** — Introduces `PermissionProfileSnapshot` as a formal protocol model; decouples core state from concrete `PermissionProfile` implementation.

10. **[#38650 — Canonicalize default namespaces in gRPC subscription filters](https://github.com/openai/codex/pull/38650)** — Treats missing/empty namespaces as aliases for the `functions` namespace, fixing filter matching mismatches for tool invocations.

## Feature Request Trends

- **Per-project/per-chat execution environments** ([#36098](https://github.com/openai/codex/issues/36098)): Users on Windows dual-environments (PowerShell + WSL) request selective tool-shell assignment per project or chat, with reliable path handling.
- **`/cd` command for the CLI** ([#38585](https://github.com/openai/codex/issues/38585)): Move the active conversation to a different working directory without restarting.
- **Local project selection from Chrome side panel** ([#32610](https://github.com/openai/codex/issues/32610)): When starting new chats via browser extension, let users pick a specific local Codex project.
- **Preserve operational context across compaction** ([#29356](https://github.com/openai/codex/issues/29356), [#31375](https://github.com/openai/codex/issues/31375)): Cross-cutting request for more faithful context compression — users repeatedly lose reasoning and operational steps.
- **Remote device control on Windows** ([#28919](https://github.com/openai/codex/issues/28919)): Feature parity request; missing "Control other devices" tab makes Windows the odd one out for remote session workflows.

## Developer Pain Points

- **Windows performance regressions dominate the backlog**: The majority of top-engaged issues this week are Windows Desktop performance degradations spanning multiple releases: mouse lag (#38583, #38546), CPU busy loops (#38547), process storms (#34260), and legacy freezes (#20214). The density of "revert please" sentiment — including macOS reports (#38637) — suggests release-quality confidence is dipping.
- **Process/WMI resource exhaustion**: Windows-specific resource leaks (`taskkill` storms, PID 4 Section-handle growth (#35775), monotonic `logs_2.sqlite` growth (#35823)) are a recurring class. Developers flag these as serious workstation stability threats, not just Codex slowness.
- **Context compaction breaking long tasks**: Across CLI and Desktop, compaction is glitchy: remote fails with network errors (#31375), endpoint returns 404 in CLI (#38323), or drops operational context (#29356). This is a high-frequency functional friction point for serious users.
- **MCP and sandbox integration fragility on Windows**: MSIX PowerShell sandbox permission errors (#35871), Computer Use EPERM failures (#38636), and MCP stack retention across chats (#32154) show that Windows packaging and sandboxing remain a weak area.
- **Session/concurrency ownership surprises**: Opening across windows (#38629) and stuck remote handshakes (#22733) highlight that session-state ownership and transport remain brittle when users multi-home across app, IDE, and mobile.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-08-15

## Today's Highlights

**Releases:** v0.56.0-nightly.20260814.gc0d192452 was published in the last 24 hours, focusing on test stabilization for the file-system-interactive E2E suite and introducing context-aware silent retries with availability TTL for capacity errors. Meanwhile, the community is actively submitting and getting merges for the SSR Agent initiative, with 8 PRs landed yesterday addressing hangs, TypeScript strict-null errors, PTY leaks, and subagent recovery logic.

---

## Releases

- **v0.56.0-nightly.20260814.gc0d192452** ([Release](https://github.com/google-gemini/gemini-cli/releases/tag/v0.56.0-nightly.20260814.gc0d192452))
  - Stabilized the `file-system-interactive` E2E test on slow runners ([PR #28793](https://github.com/google-gemini/gemini-cli/pull/28793))
  - Implemented context-aware silent retries and availability TTL for capacity errors ([#28761](https://github.com/google-gemini/gemini-cli/pull/28761))

---

## Hot Issues

1. **#22323 — Subagent recovery after MAX_TURNS is reported as GOAL success, hiding interruption** ([Issue](https://github.com/google-gemini/gemini-cli/issues/22323))
   - **Why it matters:** `codebase_investigator` reports `success` and `Termination Reason: GOAL` even when hitting its max turn limit mid-analysis, masking a truncated investigation—a trust problem for users relying on subagent results
   - **Community reaction:** 12 comments; a fix is already merged ([PR #28815](https://github.com/google-gemini/gemini-cli/pull/28815)), preserving the original termination reason during recovery; currently in need-retesting

2. **#21409 — Generalist agent hangs** ([Issue](https://github.com/google-gemini/gemini-cli/issues/21409))
   - **Why it matters:** Flagship pain—whenever actions defer to the generalist agent (even simple folder creation), the CLI hangs indefinitely (up to an hour before cancellation); forcing no-subagent mode is the only workaround, reducing overall agent usefulness
   - **Community reaction:** 8 👍 and 8 comments, indicating broad impact; still open without a firm fix

3. **#1473 — rateLimitExceeded error 429 for no good reason** ([Issue](https://github.com/google-gemini/gemini-cli/issues/1473))
   - **Why it matters:** Long-running, sentinel issue for false-positive rate-limit errors resulting in false "success" from subagents; users report clear errors despite normal usage; now closed after requiring more information, but historical severity (10 comments) is a recurring theme
   - **Community reaction:** 10 comments; closed as status/need-information

4. **#1474 — Hitting usage limits by just asking to create a gemini.md file** ([Issue](https://github.com/google-gemini/gemini-cli/issues/1474))
   - **Why it matters:** Extremely low-effort requests exhausting quota immediately—a supply-side pain point causing frustration; 4 👍 indicates significant awareness
   - **Community reaction:** 9 comments; closed but the underlying trend persists (see #1473)

5. **#25166 — Shell command execution gets stuck with "Waiting input" after command completes** ([Issue](https://github.com/google-gemini/gemini-cli/issues/25166))
   - **Why it matters:** Even simple `ls`-type commands hang as if awaiting input after finishing, blocking the whole session; the PTY fd leak was fixed in related PRs (below), but this issue remains open as a symptom
   - **Community reaction:** 3 👍, 4 comments; still open

6. **#21968 — Gemini does not use skills and sub-agents enough** ([Issue](https://github.com/google-gemini/gemini-cli/issues/21968))
   - **Why it matters:** Anecdotal but widely shared: the agent ignores custom skills and sub-agents unless explicitly instructed, reducing agent efficiency and making power-user workflows require excessive hand-holding
   - **Community reaction:** 6 comments, 0 👍; acknowledged, but the "needs retesting" label suggests pending release verification

7. **#26522 — Stop Auto Memory from retrying low-signal sessions indefinitely** ([Issue](https://github.com/google-gemini/gemini-cli/issues/26522))
   - **Why it matters:** Auto Memory marks a session unprocessed when the extractor skips a low-signal transcript, causing the same session to be repeatedly surfaced and re-read; waste of tokens and model cycles
   - **Community reaction:** 5 comments; still open, part of a larger memory-system quality epic (#26516)

8. **#26525 — Add deterministic redaction and reduce Auto Memory logging** ([Issue](https://github.com/google-gemini/gemini-cli/issues/26525))
   - **Why it matters:** Privacy/security: transcript content is sent to the model *before* redaction, and the service may log existing skill transcripts—this is a compliance and data-leak risk for enterprise users
   - **Community reaction:** 4 comments; still open

9. **#24246 — Gemini CLI encounters 400 error with > 128 tools** ([Issue](https://github.com/google-gemini/gemini-cli/issues/24246))
   - **Why it matters:** When more than 128 tools are available, the model hits a 400 error; users expect smarter tool-scoping rather than a hard limit, especially with MCP servers and enabled tools growing
   - **Community reaction:** 3 comments; still open

10. **#26523 — Surface or quarantine invalid Auto Memory inbox patches** ([Issue](https://github.com/google-gemini/gemini-cli/issues/26523))
    - **Why it matters:** The memory inbox silently swallows malformed or out-of-root patches, and dismiss only removes valid ones; users get no visibility into hidden failures and risk data integrity issues
    - **Community reaction:** 3 comments; still open

---

## Key PR Progress

1. **#28815 — [SSR Agent] Preserve original termination reason during subagent recovery** ([PR](https://github.com/google-gemini/gemini-cli/pull/28815))
   - Fixes #22323 directly by ensuring `LocalAgentExecutor` does not convert MAX_TURNS recovery-completion into a GOAL-success; restores truthful termination reporting for debugging and evals

2. **#28812 — [SSR Agent] Prevent indefinite TUI hang by adding execution timeouts** ([PR](https://github.com/google-gemini/gemini-cli/pull/28812))
   - Fixes #21477: bare Linux TUI hangs forever at "Initializing…" because `getProcessInfo()` blocks on `execAsync`; adds timeouts to avoid indefinite stalls—important contributor to the generalist hang complaints above

3. **#28816 — [SSR Agent] Fix silent hang in MessageBus.request when publish fails** ([PR](https://github.com/google-gemini/gemini-cli/pull/28816))
   - Fixes a floating-promise bug causing a 60-second silent hang on publish failure; now surfaces failures to the caller properly

4. **#28817 — [SSR Agent] Retain executing subagent tool calls in hook state** ([PR](https://github.com/google-gemini/gemini-cli/pull/28817))
   - Fixes #22589: first-seen subagent tool calls in `Executing` state were dropped; now they correctly feed the hook system, enabling pipeline integrations and observability

5. **#20916 — prevent PTY file descriptor leak in ShellExecutionService** ([PR](https://github.com/google-gemini/gemini-cli/pull/20916))
   - Merged for #15945: root-caused missing `destroy()` on PTY processes, plus race condition where kill before spawn did nothing; prevents system-wide PTY exhaustion (macOS limit 511)

6. **#27154 — prevent PTY memory leak by synchronously deleting active entries** ([PR](https://github.com/google-gemini/gemini-cli/pull/27154))
   - Complements #20916: `activePtys.delete()` moved out of a Promise `.then()` to synchronously remove PTY entries, avoiding memory leaks when log cleanup stalls

7. **#28597 — load environment variables before resolving settings placeholders** ([PR](https://github.com/google-gemini/gemini-cli/pull/28597))
   - Fixes load-order race: `.env` was expanded after settings files, meaning `process.env` placeholders resolved empty—now env is loaded first to properly template settings

8. **#28603 — upgrade sandbox Dockerfile to Node 22** ([PR](https://github.com/google-gemini/gemini-cli/pull/28603))
   - Resolves #28584 (Node 20 EOL); security-focused fix since sandbox runtime executes model-directed commands; EOL runtime was an unacceptable supply-chain risk

9. **#28596 — add `--list-all-sessions` to list sessions across all workspaces** ([PR](https://github.com/google-gemini/gemini-cli/pull/28596))
   - New feature: lists chat sessions across all registered workspaces, grouped by path—addresses the recurring pain of losing sessions across folders

10. **#28738 — allow agents to call agents** ([PR](https://github.com/google-gemini/gemini-cli/pull/28738, OPEN))
    - Fixes #22092 by letting subagents delegate to other subagents or recurse via `tools:` frontmatter; currently open and awaiting review, but is the most requested architecture direction from this digest

---

## Feature Request Trends

- **Subagent orchestration & observability** — multiple issues (#22323, #21968, #22598, #21763) show demand for subagent delegation, trajectory visibility, and "self-aware" use of skills. Users want a system that organically uses sub-agents without being instructed
- **AST-aware tooling** — EPIC #22745 and #22746 propose AST-aware file reads, search, and codebase mapping to reduce turn count and token noise; significant interest from maintainers, with tilth and glyph as candidate tools
- **Agent self-awareness** — #21432 wants the CLI to know its own hotkeys, flags, and inner APIs so it can guide users accurately—a form of "dogfooding" the agent on itself
- **Environment compatibility (WSL/Windows/macOS)** — PRs and issues for WSL2 clipboard paste (#27588), Windows ripgrep `EFTYPE` fix (#25378), and browser subagent on Wayland (#21983) all point to a strong, vocal cross-platform user base
- **Memory system hardening** — Auto Memory issues (#26522, #26523, #26525, #26516) reveal a heavy push to make memory extraction deterministic, private, and non-wasteful

---

## Developer Pain Points

- **Hangs and false success** — The most vocal recurring frustration: subagents either hang indefinitely (generalist #21409) or report GOAL success after MAX_TURNS interruptions (#22323), eroding trust in agent status reporting
- **Resource leaks** — PTY fd exhaustion (#15945, #20916) and silent memory leaks (#27154) have been real-timeblockers for long-running sessions; community contributions (#20916) show users are blocked enough to fix it themselves
- **Rate-limit and quota surprises** — False 429s (#1473) and instant quota exhaustion from trivial prompts (#1474) are the top complaints from users new to the CLI
- **Settings/env-order bugs** — Race conditions in loading `.env` before settings placeholders (#28597) caused confusing misconfigurations in enterprise setups
- **Privacy & security concerns with Auto Memory** — Reading local transcripts *before* redaction (#26525) is a serious concern for enterprise users; redaction must happen pre-context, not in-prompt
- **Tool overload** — 400 errors when >128 tools are available (#24246) represents a real scalability limit for MCP-heavy workflows; users want dynamic tool-scoping, not just a raised cap

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest
**2026-08-15**

---

## Today's Highlights

Release v1.0.80 shipped with model configuration updates, but the community is buzzing about a regression in MCP OAuth authentication (RFC 8414 issuer mismatch) affecting Atlassian and GitLab MCP servers. Enterprise users are reporting widespread issues with Claude models being unavailable, and a cluster of new issues around session management, plugin updates, and autopilot stability suggests growing pains as adoption scales.

---

## Releases

### v1.0.80 — 2026-08-14
- Update model configurations
- v1.0.80-1: Fixes and changes

**Link:** [github/copilot-cli/releases](https://github.com/github/copilot-cli/releases)

---

## Hot Issues

1. **[#4480 — Atlassian MCP OAuth fails with "Incompatible authorization server" on 1.0.79](https://github.com/github/copilot-cli/issues/4480)** — Regression from 1.0.71. Community reaction: 6 👍. High-impact because MCP integrations are central to the agentic workflow; broken auth blocks Atlassian tooling entirely. Also surfaces as [#4490](https://github.com/github/copilot-cli/issues/4490) for v1.0.80, indicating the fix didn't land.

2. **[#4345 — Reasoning effort 'medium' unsupported for claude-haiku-4.5](https://github.com/github/copilot-cli/issues/4345)** — Error thrown during sub-agent execution when specific feature flags are active. 4 👍 and 6 comments. Points to insufficient model capability validation when feature flags enable unsupported combinations.

3. **[#4390 — Enabled organization models missing from catalogue (Claude Sonnet 5/Opus 5, Kimi K3)](https://github.com/github/copilot-cli/issues/4390)** — Models explicitly enabled by Copilot Business orgs are unavailable. Related to [#4422](https://github.com/github/copilot-cli/issues/4422) (All Claude models disabled for Enterprise) and [#4494](https://github.com/github/copilot-cli/issues/4494) (newly enabled models require cache clearing). This is the #1 enterprise friction point this week.

4. **[#4439 — GitLab MCP OAuth metadata rejected (RFC 8414 issuer mismatch)](https://github.com/github/copilot-cli/issues/4439)** — GitLab Self-Managed MCP servers fail OAuth discovery. Same root cause as Atlassian issues; suggests broad OAuth compatibility problem in the MCP client.

5. **[#4499 — Fatal "Committing semi space failed" OOM in autopilot](https://github.com/github/copilot-cli/issues/4499)** — V8 heap crash at only ~0.6/4.3 GB. Host-RAM commit failure, not heap limit. Concerning for long-running autopilot sessions; likely related to memory fragmentation or native allocation issues.

6. **[#4306 — Subtasks freeze and stop responding](https://github.com/github/copilot-cli/issues/4306)** — Autopilot loops between agents (speckit-implement ↔ speckit-converge) freeze mid-session. 2 👍. Long-running issue (since July 30) still unfixed; affects complex multi-agent workflows.

7. **[#4511 — /restart fails in sessions created with -w](https://github.com/github/copilot-cli/issues/4493)** — Option conflict when restarting worktree sessions. Session recovery is a core workflow; this breaks it for a common flag combination.

8. **[#4477 — Session and prompt lost when hitting stop button](https://github.com/github/copilot-cli/issues/4477)** — Entire session (including original prompt and edits) deleted on stop. Data-loss bug; multiple reports. High frustration potential.

9. **[#4488 — Plugin updates fail with "Access is denied" when other sessions open](https://github.com/github/copilot-cli/issues/4488)** — File locks held by unrelated Copilot CLI/VS Code sessions block plugin updates. Multi-session workflows are now standard; this imposes a serialization constraint.

10. **[#4346 — MCP registry policy fetch returns 403 for Actions GITHUB_TOKEN](https://github.com/github/copilot-cli/issues/4346)** — Blocks all non-default MCP servers in CI with the documented PAT-less Actions setup. Closed, but significant impact on CI/CD adoption of MCP tools.

---

## Key PR Progress

1. **[#4497 — Handle fork PR associations in invalid-label writer](https://github.com/github/copilot-cli/pull/4497)** — Fixes label automation when GitHub doesn't populate PR association for fork runs. Searches via trusted workflow-run metadata requiring exactly one open PR.

2. **[#4449 — Migrate pull request automation away from pull_request_target](https://github.com/github/copilot-cli/pull/4449)** — **Security-hardening PR.** Replaces `pull_request_target` with issue-scoped tokens and no-permission `pull_request` signals. Reduces supply-chain attack surface for fork-originated PRs.

3. **[#4496 — Workflow migration canary (PR #4449)](https://github.com/github/copilot-cli/pull/4496)** — Temporary documentation-only PR verifying fork-originated PR automation post-migration; closed after confirmation.

---

## Feature Request Trends

1. **Model support & availability improvements** — GPT-5.6 `reasoning.mode` parameter support ([#4495](https://github.com/github/copilot-cli/issues/4495)); consistent model availability across org/enterprise policies and local cache refresh ([#4390](https://github.com/github/copilot-cli/issues/4390), [#4494](https://github.com/github/copilot-cli/issues/4494)).

2. **Plugin ecosystem maturity** — Dependency specification and resolution for marketplace plugins ([#4487](https://github.com/github/copilot-cli/issues/4487)); fix file-lock conflicts during parallel updates ([#4488](https://github.com/github/copilot-cli/issues/4488)).

3. **Observability enhancements** — Protobuf OTLP export support (`OTEL_EXPORTER_OTLP_PROTOCOL=http/protobuf`) ([#2934](https://github.com/github/copilot-cli/issues/2934)). The `application/json`-only constraint limits integration with standard OTel collectors.

4. **Session UX improvements** — Persist agent selection when resuming sessions ([#4489](https://github.com/github/copilot-cli/issues/4489)); clarify `copilot-instructions.md` startup message to specify repo-scoped file ([#4475](https://github.com/github/copilot-cli/issues/4475)).

5. **Protocol compliance** — Follow MCP `tools/list` pagination (`nextCursor`) ([#4006](https://github.com/github/copilot-cli/issues/4006)); case-insensitive MCP server name collision detection ([#4478](https://github.com/github/copilot-cli/issues/4478)).

---

## Developer Pain Points

1. **MCP OAuth instability** — Recurring RFC 8414 issuer mismatches against Atlassian ([#4480](https://github.com/github/copilot-cli/issues/4480)) and GitLab ([#4439](https://github.com/github/copilot-cli/issues/4439)) servers. Regression in 1.0.79 persists in 1.0.80 ([#4490](https://github.com/github/copilot-cli/issues/4490)). MCP integration trust is eroding.

2. **Enterprise model access broken** — Claude models unavailable despite org settings showing enabled ([#4422](https://github.com/github/copilot-cli/issues/4422), [#4390](https://github.com/github/copilot-cli/issues/4390)). Enterprise users cannot use paid-tier models with no documented workaround beyond cache clearing.

3. **Session data loss** — Stop button deletes entire sessions ([#4477](https://github.com/github/copilot-cli/issues/4477)); `/restart` breaks with `-w` ([#4493](https://github.com/github/copilot-cli/issues/4493)). Destructive failure modes erode trust for long-running agentic workflows.

4. **Autopilot stability** — OOM crashes despite headroom ([#4499](https://github.com/github/copilot-cli/issues/4499)); sub-agent freezes in multi-agent loops ([#4306](https://github.com/github/copilot-cli/issues/4306)). Autopilot remains risky for unattended workloads.

5. **CI/CD friction** — MCP registry 403 with GITHUB_TOKEN ([#4346](https://github.com/github/copilot-cli/issues/4346)) and false-positive cybersecurity risk flags during routine debugging ([#4479](https://github.com/github/copilot-cli/issues/4479)) interrupt automation pipelines.

6. **Permissions configuration gaps** — `allowed_directories` in `permissions-config.json` doesn't suppress path prompts ([#4482](https://github.com/github/copilot-cli/issues/4482)); `/add-dir` works but config file doesn't. Threshold for trusting the documented configuration surface drops.

7. **Permissions request timeouts** — Edit permission requests time out instead of persisting ([#4486](https://github.com/github/copilot-cli/issues/4486)). Breaks overnight/multi-session workflows and forces users to babysit the CLI.

---

*Data compiled from [github/copilot-cli](https://github.com/github/copilot-cli) — 1 release, 30 issues, 3 PRs updated in the last 24 hours.*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

**Kimi Code CLI Community Digest – 2026-08-15**

**1. Today's Highlights**
The community’s focus remains firmly on persistent memory and cross-session context, with two of the most active issues (#1283, #1478) continuing to accrue discussion despite being months old. While there were no new releases or pull requests in the last 24 hours, the sustained engagement signals that users are hitting scaling pain points on large projects. Notably, a long-standing shell enhancement PR (#1136) was closed, indicating the team may be addressing Windows PowerShell issues through alternative channels.

**2. Releases**
No new releases were published in the last 24 hours. The most recent tagged version remains unchanged on the repository’s default branch.

**3. Hot Issues**

- **[#1283] Feature Request: Memory System - Persistent context across sessions**  
  *Author: CatKang | Comments: 39 | 👍: 0*  
  The most-discussed open feature request. Proposes a dual-layer memory system (automatic AI-managed notes + manual user instructions). The sustained 6-month engagement from multiple users suggests this is a top priority for large-scale workflows.  
  [Link](https://github.com/MoonshotAI/kimi-cli/issues/1283)

- **[#2269] Remote Control / Multi-Device Session Handoff**  
  *Author: lucianalima777 | Comments: 6 | 👍: 1*  
  Requests starting a session on one device and continuing it on another (laptop, web, mobile). As cloud-IDE adoption grows, this is increasingly seen as a missing piece for hybrid workflows.  
  [Link](https://github.com/MoonshotAI/kimi-cli/issues/2269)

- **[#1478] Can the memory layer be optimized? / 能否优化记忆层?**  
  *Author: hahy36 | Comments: 2 | 👍: 0*  
  Openly criticizes the current memory implementation, noting the documentation only references `agent.md` and lacks a structured memory protocol. Includes a reference to an alternative tool’s memory layout (SOUL.md, MEMORY.md), implying users are comparing Kimi unfavorably to competitors.  
  [Link](https://github.com/MoonshotAI/kimi-cli/issues/1478)

- **[#1136] [Closed] feat(shell): enhance shell tool with version-aware PowerShell context**  
  *Author: QIN2DIM | Comments: 0*  
  Identify three Windows-specific bugs in the shell tool (ambiguous shebang handling, PATH resolution mismatch, and encoding issues). Closed without merge, which may concern Windows users, but could indicate a private fix or a broader shell refactor in progress.  
  [Link](https://github.com/MoonshotAI/kimi-cli/pull/1136)

**4. Key PR Progress**
No pull requests were updated or opened in the last 24 hours. The repository currently has no open PRs in active review as of this digest. Users are encouraged to check the closed PR #1136 for context on Windows shell behavior.

**5. Feature Request Trends**
- **Persistent Memory/Context (#1283, #1478):** The dominant theme. Users want the CLI to auto-maintain project patterns and user preferences across sessions, not just a single `agent.md` file.
- **Remote Session Synchronization (#2269):** A secondary trend toward multi-device workflows, indicating demand for a server-side state layer rather than purely local-session tools.

**6. Developer Pain Points**
- **Context Loss on Large Projects:** Developers explicitly state that scaling to "big projects" is painful without a memory layer, leading to repeated clarification of project conventions every session.
- **Documentation Gap:** Users note that memory features are not adequately documented (only `agent.md` is discoverable), forcing them to dig through issues or look at competitor implementations.
- **Windows Shell Instability:** Although closed, the PowerShell context issues raised in #1136 reflect a recurring concern for Windows-native developers regarding command execution reliability.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-08-15

## Today's Highlights

The community experienced a **critical 48-bit timestamp wraparound bug** that silently froze pre-existing sessions — a sharp reminder of the dangers of date-based ID generators. This dominated the day alongside a major **performance issue** in the TUI render thread (97% CPU during multi-subagent sessions). On a positive note, a long-awaited **dynamic model discovery PR** (#42660) landed, aiming to close six long-standing feature requests for auto-discovering models from OpenAI-compatible providers.

---

## Releases

No new releases in the last 24 hours.

---

## Hot Issues

Here are the 10 most noteworthy issues from the past 24 hours, sorted by community impact:

1. **[#42608 — 48-bit ID timestamp wraparound on 2026-08-14 12:39:55 UTC wedges all pre-existing sessions](https://github.com/anomalyco/opencode/issues/42608)**
   **Author:** klly14 | **Comments:** 5 | 👍 3
   **Why it matters:** This is the **root cause behind #42605** and a spike of "agent stops responding" reports. A silent, time-based ID generator rollover froze all pre-existing sessions. This is a systemic bug, not a user error — and a strong argument for switching to monotonic/random IDs.

2. **[#20695 — Memory Megathread](https://github.com/anomalyco/opencode/issues/20695)**
   **Author:** thdxr | **Comments:** 131 | 👍 98
   **Why it matters:** The community's central hub for memory issues. Maintainers explicitly ask users **not to run their LLM for solutions** — they're collecting heap snapshots to debug properly. High engagement signals this is a persistent, unresolved pain point.

3. **[#42657 — TUI lag with multi-subagent sessions (97% CPU on render thread)](https://github.com/anomalyco/opencode/issues/42657)**
   **Author:** BenjaMolina | **Comments:** 2 | 👍 0
   **Why it matters:** Reproduced across Warp, Windows Terminal, and WezTerm. With 2–4 concurrent subagents, the TUI becomes nearly unusable (1–3s typing delay). This is a **new** report, but aligns with broad complaints about degraded responsiveness under concurrency.

4. **[#42605 — The session remains open, but the agent does not process subsequent prompts](https://github.com/anomalyco/opencode/issues/42605)**
   **Author:** ekatake-125 | **Comments:** 4 | 👍 0
   **Why it matters:** Likely a **symptom of #42608**. The agent finishes a task, asks a question, then silently ignores the next message. Several users filed similar reports (#42594, #42611), all pointing to the same root cause.

5. **[#38791 — Run loop can never exit when message ids are not time-sortable](https://github.com/anomalyco/opencode/issues/38791)**
   **Author:** dkindlund | **Comments:** 6 | 👍 0
   **Why it matters:** A **sibling issue to #42608**. The run loop compares message IDs as plain strings, assuming chronological embedding. Third-party importers break this assumption, causing endless loops. This suggests the ID-generation design is fragile beyond just the wraparound.

6. **[#42613 — OpenAI Responses: assistant messages rejected by strict OpenAI-compatible servers](https://github.com/anomalyco/opencode/issues/42613)**
   **Author:** j34ni | **Comments:** 2 | 👍 0
   **Why it matters:** Sending `{role: "assistant", content: [{type: "output_text"}]}` to `/responses` endpoints **violates the OpenAI spec** — it rejects this shape. A raw protocol-compliance bug that breaks strict providers.

7. **[#42616 — Zen Go Anthropic endpoint: tools requests fail for all GLM models](https://github.com/anomalyco/opencode/issues/42616)**
   **Author:** goldyard2022 | **Comments:** 2 | 👍 0
   **Why it matters:** All GLM models fail when any `tools` array is non-empty. Works fine without tools, and fine for other models (e.g., Kimi). A provider-specific adapter bug affecting the Anthropic-compatible route.

8. **[#42635 — TUI system theme never refreshes terminal palette without a ?997 report](https://github.com/anomalyco/opencode/issues/42635)**
   **Author:** CripWal | **Comments:** 2 | 👍 0
   **Why it matters:** Inside multiplexers that cache host color schemes (like `herdr`), the `system` theme never re-detects palette changes unless the terminal explicitly reports `\e[?997` or SIGUSR2. A niche but real theme-refresh gap.

9. **[#42611 — Session went non responsive](https://github.com/anomalyco/opencode/issues/42611)**
   **Author:** rohit1409 | **Comments:** 2 | 👍 0
   **Why it matters:** Another **re-report of #42608**. "I restarted that session, but it's not reading or taking new chats." Confirms the wraparound issue is widespread and not isolated to one environment.

10. **[#42637 — Credit non utilisable / Paid but no balance](https://github.com/anomalyco/opencode/issues/42637)**
    **Author:** amausolution | **Comments:** 3 | 👍 0
    **Why it matters:** As OpenCode moves toward monetization (Go/Zen credits), billing bugs are surfacing — from "paid but no balance" (#42606) to "FreeUsageLimitError" persisting past 24h (#42215). Trust and reliability concerns around paid tiers.

---

## Key PR Progress

The most impactful PRs from the last 24 hours, including a notable feature for dynamic model discovery:

1. **[#42660 — feat(provider): add dynamic model discovery for custom providers](https://github.com/anomalyco/opencode/pull/42660)**
   **Author:** Gr33ndev | **Status:** Open
   **What it does:** Closes **six** long-standing feature requests (#13891, #29308, #28999, #25624, #23327, #26863). Auto-discovers models from OpenAI-compatible providers (via `/v1/models`) — removing the need to manually list every model in `opencode.json`. This has been a **top community ask** for months.

2. **[#42656 — refactor(protocol): move worktree routes out of experimental namespace](https://github.com/anomalyco/opencode/pull/42656)**
   **Author:** jlongster | **Status:** Closed
   **What it does:** Promotes worktree APIs from `/api/experimental/...` to a stable top-level resource (`/api/worktree/:projectID`). A signal that worktree support is maturing and on track for GA.

3. **[#36943 — fix(core): keep interrupted sessions stopped](https://github.com/anomalyco/opencode/pull/36943)**
   **Author:** opencode-agent[bot] | **Status:** Closed (auto-cleanup)
   **What it does:** Fixes a race where interrupted sessions would **wake up again** via stale durable admission sequences. Suppresses prompt wakes admitted before the interrupt, while preserving genuinely newer prompts.

4. **[#36916 — fix: queue concurrent subagent questions](https://github.com/anomalyco/opencode/pull/36916)**
   **Author:** lucas-gaitzsch | **Status:** Closed
   **What it does:** Closes #36915. Orders pending questions across the full root session tree by request ID, keeping the active request selected. Should mitigate some multi-subagent TUI chaos.

5. **[#36906 — fix(tui): keep home shortcuts right-aligned](https://github.com/anomalyco/opencode/pull/36906)**
   **Author:** opencode-agent[bot] | **Status:** Closed
   **What it does:** Fixes a TUI layout regression where home shortcuts were left-aligned when no session directory existed. Small but user-visible polish.

6. **[#36880 — fix(tui): restore compaction model marker](https://github.com/anomalyco/opencode/pull/36880)**
   **Author:** kitlangton | **Status:** Closed
   **What it does:** Restores the `Compaction · <model>` marker that regressed in V2. Verified against V1 behavior (v1.17.20) where compaction summaries stored provider/model identity. Helps users see which model performed compaction.

7. **[#36869 — feat(opencode): per-tool execution timeout with abort + session recovery](https://github.com/anomalyco/opencode/pull/36869)**
   **Author:** FahadBinHussain | **Status:** Closed
   **What it does:** Addresses tool hangs (built-in and MCP) with per-tool timeouts, plus abort and session recovery. Ties into long-running complaints (#20096, #34888, etc.). A **significant reliability upgrade**.

8. **[#36861 — fix(session): recover cache tokens from openai-compatible metadata usage fallback](https://github.com/anomalyco/opencode/pull/36861)**
   **Author:** ulises-jeremias | **Status:** Closed
   **What it does:** Closes #30663. Custom baseURL providers may report cache tokens via metadata (e.g., `prompt_tokens_details`). This PR recovers those tokens for accurate cache accounting.

9. **[#36860 — fix(opencode): strip MiniMax trailing tool_call leak suffix from assistant text](https://github.com/anomalyco/opencode/pull/36860)**
   **Author:** ulises-jeremias | **Status:** Closed
   **What it does:** Closes #30684. MiniMax models sometimes append a serialized tool-call artifact (e.g., `]<\`]minimax[>[/<\`/tool_call>`) to plain assistant text. Strips it to avoid corrupting the message stream.

10. **[#36851 — chore(db): enable auto-vacuum and add periodic maintenance](https://github.com/anomalyco/opencode/pull/36851)**
    **Author:** BYK | **Status:** Closed
    **What it does:** Re-filed after auto-cleanup (age-based, not technical). Enables auto-vacuum and adds periodic maintenance — directly relevant to the **memory megathread** and growing database bloat complaints.

---

## Feature Request Trends

Across all open issues in the last 24 hours, the most consistent feature directions are:

1. **Dynamic / self-discovering model providers** — #27553 (auto-discover from `/v1/models`) and the new PR #42660. **Domain: Config / Providers.** This is the single most-requested *config* enhancement right now.

2. **Hot-reload of configs, agents, skills, and commands** — #8751 (91 👍). Users want to edit agents/skills/commands while OpenCode is running, without restarting. **Domain: Developer Experience.**

3. **Configurable OAuth callback host** — #33966. After PR #30022 bound the OAuth server to `127.0.0.1` only, users who need remote callback hosts are blocked. **Domain: Auth / Networking.**

4. **Context cache invalidation control** — #37489. When switching modes or during compaction, cache re-computation causes severe performance degradation with local LLMs (vLLM, Ollama). Users want control over when/whether the cache is invalidated. **Domain: Performance / Context.**

5. **Websearch / tool parity across model routes** — #40568. Tools like `websearch` appear on Zen models out-of-the-box, but require an undocumented env var (`OPENCODE_ENABLE_EXA=1`) on Go routes. Users want **consistent tool availability** without hidden config. **Domain: Tooling / Parity.**

---

## Developer Pain Points

Recurring frustrations from the past 24h (and the megathreads they feed):

1. **Silent session freezes / non-responsiveness** — Multiple issues (#42608, #42605, #42611) all trace to the **ID wraparound**. The broader lesson: monitoring session state and avoiding time-based IDs. High priority for maintainers right now.

2. **TUI performance under concurrency** — Profiling shows **97% CPU on the render thread** with 4 concurrent subagents. Combined with #36916 (question queueing), the TUI is struggling to keep up with the agent loop's parallelism.

3. **Provider-specific protocol strictness** — Multiple issues where OpenCode sends slightly non-compliant payloads (OpenAI Responses `output_text`, GLM/Kimi tool schema failures). Causes "works on some models, breaks on others."

4. **Billing / credit reliability** — As monetization rolls out, users report "paid but no balance" (#42606, #42637) and incorrect free-tier limits (#42215). Trust issues are emerging.

5. **Opaque / undocumented config** — The `OPENCODE_ENABLE_EXA` env var (#40568) and hidden provider behaviors are frustrating. Users want features to work **out-of-the-box**, not via undocumented flags.

6. **Compaction and cache rebuild costs** — Especially with local LLMs, mode switches / compaction trigger full cache recomputation, causing "significant performance issues." Users want finer control. (#37489)

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-08-15

## 1. Today's Highlights
Pi v0.84.2 ships with fullscreen transcript search and configurable default tools, while the community rallies around Windows support (issue #7547) as a major adoption barrier. The TUI's CPU spin during streaming (#6665) and Copilot login rate-limiting (#7850) are the most active debugging fronts, alongside growing contributor momentum around new providers (xAI, SiliconFlow, Bedrock Mantle) and compaction improvements.

## 2. Releases
**v0.84.2** — Key additions include:
- **Fullscreen transcript search** with match navigation, now properly scoped to visible viewport via alternate-screen rendering
- **Configurable default tools** with startup customization

## 3. Hot Issues (Top 10)

1. **[#7547 — Windows support survey](https://github.com/earendil-works/pi/issues/7547)** (open, 27 comments)
   Maintainer-driven call for Windows usage patterns. The issue is a landscape map of Windows pain points—WSL vs native, bash tool gaps, Unix socket failures—making it the definitive roadmap for Windows adoption. Community responses have been detailed and passionate.

2. **[#6187 — Pi login hangs in WSL after Copilot authorization](https://github.com/earendil-works/pi/issues/6187)** (closed, 26 comments, 👍6)
   Critical WSL onboarding bug: device authorization completes but the client never detects it. A top adoption blocker for WSL-based developers; the fix is highly anticipated.

3. **[#5223 — Anthropic thinking blocks cause 400 with Opus 4.8](https://github.com/earendil-works/pi/issues/5223)** (closed, 17 comments, 👍6)
   Multi-turn sessions with adaptive thinking fail mid-conversation. The provider sends `thinking` blocks in the latest message, violating API constraints. Signaled strong community demand for adaptive thinking support.

4. **[#6665 — TUI pins a full core while streaming](https://github.com/earendil-works/pi/issues/6665)** (open, in-progress, 12 comments, 👍3)
   Uncached `Intl.Segmenter` plus per-chunk Markdown rebuild in the render timer. Root-caused with spindump; fix in progress. This is a silent annoyance for long sessions and a battery drain on laptops.

5. **[#5023 — Terminal scrolls to beginning without reason](https://github.com/earendil-works/pi/issues/5023)** (closed, 12 comments, 👍2)
   Spontaneous viewport jumps during streaming, most likely related to caret positioning math. Frequently reported as "random" but likely tied to specific terminal emulators.

6. **[#7850 — Copilot login fails with 429 for orgs with many models](https://github.com/earendil-works/pi/issues/7850)** (closed, 9 comments, 👍7)
   GitHub device authorization succeeds but Copilot login hits rate limits for large orgs. The fix involved aligning Pi's request pattern with GitHub's token budget; important for enterprise adoption.

7. **[#8096 — Z.AI defaults reference a removed model](https://github.com/earendil-works/pi/issues/8096)** (closed, 5 comments)
   `defaultModelPerProvider` still points to `glm-5.1` while the generated catalog contains newer models. A reminder that provider catalogs drift quickly; caught promptly by a vigilant user.

8. **[#8092 — pnpm + jiti extension dependency resolution](https://github.com/earendil-works/pi/issues/8092)** (closed, 5 comments)
   Extensions installed via pnpm fail because jiti doesn't realpath entries before resolving imports. A blocker for pnpm-heavy projects; the fix was already landed (see PR #8112).

9. **[#8010 / #7850 — Copilot 429 rate limit pair](https://github.com/earendil-works/pi/issues/8010)** (closed, 4 comments)
   Second report of the same 429 issue in 72 hours; consolidated into the broader model-count fix. Community was quick to file duplicates, showing this is a common enterprise pain.

10. **[#5581 — `triggerTurn` bypasses `before_agent_start`](https://github.com/earendil-works/pi/issues/5581)** (open, 3 comments, 👍1)
    Extension developers hitting lifecycle-event inconsistencies. This breaks extension design expectations and needs deeper architectural alignment between message routing and the agent loop.

## 4. Key PR Progress (Top 10)

1. **[#8120 — Experimental append compaction](https://github.com/earendil-works/pi/pull/8120)** (open)
   Reuses the active system prompt, tools, and routing session to preserve provider prompt caches during compaction. A significant win for token economics and latency; opt-in via `PI_EXPERIMENTAL=1`.

2. **[#8076 — Dev branch with new harness](https://github.com/earendil-works/pi/pull/8076)** (draft, open)
   A draft harness rework from the maintainer. Early days, but the kind of structural change that could reshape testing and plugin development.

3. **[#8143 — Fullscreen transcripts survive compaction](https://github.com/earendil-works/pi/pull/8143)** (closed)
   TUI now keeps the complete human transcript visible while model context is compacted, using exact block-height rendering. Directly addresses a long-standing UX gap.

4. **[#8124 — Route xAI through Responses, default Grok 4.6](https://github.com/earendil-works/pi/pull/8124)** (open)
   Moves xAI off the completions API to Responses, adds user-agent, bumps default. Mirrors the industry shift toward the Responses protocol.

5. **[#8109 — Detect api.kimi.com as Moonshot endpoint](https://github.com/earendil-works/pi/pull/8109)** (closed)
   Fixes a hard failure for Kimi Coding custom endpoints by teaching `detectCompat` to recognize Kimi hosts; also addressed in PR #8104 (user-agent alignment).

6. **[#8119 — Track Kimi cached tokens](https://github.com/earendil-works/pi/pull/8119)** (open)
   Advertised as "cached tokens are free" is misleading; this PR ensures accurate usage accounting for Kimi's top-level `usage.cached_tokens`, giving users correct cache-read metrics. Addresses #8075.

7. **[#8110 — Honest clipboard copy in TUI](https://github.com/earendil-works/pi/pull/8110)** (closed)
   Routes selection copy through the host clipboard instead of blindly writing OSC 52 and flashing "Copied!". A correctness fix for macOS Terminal.app and GNOME Terminal users who saw empty clipboards.

8. **[#5262 / #6216 — Anthropic Vertex & Bedrock Mantle providers](https://github.com/earendil-works/pi/pull/5262)** (open)
   Long-running PRs (both since May/July) adding enterprise-cloud-native endpoints. Vertex is a thin adapter over Anthropic SDK; Bedrock Mantle rides on OpenAI's Bedrock provider. A signal of enterprise demand.

9. **[#8113 — SiliconFlow provider](https://github.com/earendil-works/pi/pull/8113)** (closed)
   Adds SiliconFlow as an OpenAI-compatible built-in provider with its own model catalog and `SILICONFLOW_API_KEY` env var. Merges cleanly via the established moonshot/minimax pattern.

10. **[#8103 — Configurable agent state file mode](https://github.com/earendil-works/pi/pull/8103)** (closed)
    `PI_AGENT_FILE_MODE` env var (e.g., `0660`) allows shared Unix groups to read/write agent state files, breaking the hardcoded 600 assumption. Needed for multi-user servers.

11. *(Honorable mention)* **[#8011 — Fix single edit object normalization](https://github.com/earendil-works/pi/pull/8011)** (open)
    Some models (e.g., GLM via OpenRouter) return a bare single edit object instead of an array; Pi would crash. A subtle robustness fix in `prepareEditArguments`.

## 5. Feature Request Trends
- **Scriptability / CI pipelines** (#8114, #8133): Users want pi to be driven by pure CLI args/env vars for automatable, no-config-file workflows.
- **Per-model behavior**: Compaction settings per model (#8133), thinking-level mapping (#8135), and per-session model state (#8100) signal a demand for finer-grained model governance.
- **Provider breadth**: New providers (SiliconFlow #8113, Bedrock Mantle #6216, xAI Responses #8124) show a community pulling toward a multi-provider world with OAuth-native flows.
- **TUI polish**: Autocomplete placement (#8132), skill-name completion in-prompt (#8144), and fullscreen transcript fidelity (#8143) reflect a maturing terminal UX focus.

## 6. Developer Pain Points
- **Copilot OAuth and 429 rate limiting** (#7850, #8010): Enterprise orgs with many models hit rate limits during login. The duplicate reports and high 👍 counts show this is a common deployment blocker.
- **Provider catalog drift** (#8096): Default model references break when catalogs regenerate. This is a recurring theme: ensure defaults are validated against the live catalog at build time.
- **Windows support fragmentation** (#7547, #8047, #8108): Multiple execution modes (WSL, native, git-bash) with distinct bugs—Unix socket test failures, bash resolution, login hangs. The community is pushing for a single, recommended Windows path.
- **Token/cache accounting accuracy** (#8075, #8119): Misleading cache-read metrics frustrate power users who rely on usage data for cost optimization.
- **Terminal emulator-specific clipboard behavior** (#7761, #8110): The "Copied!" lie (OSC 52 without fallback) caused silent data loss; a reminder that TUI fixlets need compatibility testing across emulators.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-08-15

## Today's Highlights

The v0.21.12 release line introduces Web Shell workspace file uploads with drag-and-drop support and progress tracking, while the team continues extensive end-to-end validation (SWE-bench Verified + Terminal-Bench 2.0 at 89). Multiple CI failures on `main` are being tracked and auto-fixed, with several security-hardening PRs around PAT isolation and file read containment landing this week.

---

## Releases

**v0.21.12** — Main release. Adds workspace file uploads to the Web Shell composer (drag-and-drop or `@` file panel) with progress tracking, plus an autofix review diff growth brake to limit runaway diffs. ([#8874](https://github.com/QwenLM/qwen-code/pull/8874))

**v0.21.12-preview.4 / preview.3** — Preview iterations. Bugfix preserving standalone session target in web-shell; earlier preview shipped the workspace upload feature. ([#9038](https://github.com/QwenLM/qwen-code/pull/9038))

**v0.21.11-nightly.20260814.45c2e73080** — Nightly with web-shell session-target fix and workspace upload support.

**dsw-eas-tb-e2e-20260814-r6** — Full end-to-end validation: Release → Actions → DSW SWE-bench Verified 500 → Publisher → Terminal-Bench 2.0 89, benchmarked against v0.21.2.

---

## Hot Issues

**#8957 — [Regression] Qwen code crashes on image load since 0.21.2** (12 comments)
Critical P2 regression: image loading crashes the CLI since 0.21.2. Community reports 0.21.1 works. Needs retesting; pending maintainer confirmation. ([Issue](https://github.com/QwenLM/qwen-code/issues/8957))

**#8678 — [Closed] Preserve current session when large restore times out** (9 comments)
P1 daemon bug: session restore timeouts were losing the current session. Closed as *partially addressed and superseded*; late-result safety and attachment fencing remain follow-ups. ([Issue](https://github.com/QwenLM/qwen-code/issues/8678))

**#8051 — [Open] Bound multi-workspace daemon resource usage** (9 comments)
Count-only limits don't bound bytes held by request bodies/WebSocket buffers. Needs byte-based accounting. A long-running P2 tracking issue with community input. ([Issue](https://github.com/QwenLM/qwen-code/issues/8051))

**#4063 — [Open] core + cli architecture review — 12 structural problems** (8 comments, 1 👍)
Chinese-language audit: `@google/genai` types couple 136 files; recommends decoupling. Community-backed refactor proposal with P0/P1/P2 severity breakdown. ([Issue](https://github.com/QwenLM/qwen-code/issues/4063))

**#9143 — [Open] Main CI failed: E2E Tests on c5bf22247432** (7 comments)
Bot-tracked failure before any test result. Auto-opened per commit; needs triage for flaky vs. real regression. ([Issue](https://github.com/QwenLM/qwen-code/issues/9143))

**#9002 — [Open] SDK Python rejects `permission_mode="auto"`** (6 comments)
CLI supports it; SDK client-side validation rejects it. Simple but frustrating inconsistency between CLI and SDK. ([Issue](https://github.com/QwenLM/qwen-code/issues/9002))

**#9146 — [Open] Make `utils/` a leaf layer — 107 upward imports create cyclic graph** (4 comments)
Architecture debt: utilities import domain code in 51 files. Refactor proposal to fix directory-cycle maintainability. ([Issue](https://github.com/QwenLM/qwen-code/issues/9146))

**#9026 — [Open] `NO_TOOL_RESULT_PROGRESS` hard-fails headless runs** (3 comments)
Headless runs abort when a model ends a turn quietly after a tool result — brittle error handling hurts automation reliability. ([Issue](https://github.com/QwenLM/qwen-code/issues/9026))

**#8871 — [Open] ACP child process fails with "Unknown argument: acp" in serve mode** (5 comments)
Flag-passing bug causes auth failure (`401 invalid access token`). Configuration regression with clear repro. ([Issue](https://github.com/QwenLM/qwen-code/issues/8871))

**#8582 — [Closed] Read-only shell classifier auto-approves command substitution via `${var@P}`** (5 comments)
Security hole: AST classifier missed substitutions hidden by line continuation or `${var@P}`. Closed with fix; important context for shell-security posture. ([Issue](https://github.com/QwenLM/qwen-code/issues/8582))

**#2128 — [Open] Memory grows unboundedly during long sessions** (4 comments)
`useHistoryManager.history` array grows without bound in long sessions. P1 memory leak affecting power users running 24/7 sessions. ([Issue](https://github.com/QwenLM/qwen-code/issues/2128))

**#9089 — [Open] autofix: PAT-bearing jobs share host with untrusted branch code** (3 comments)
Security: GitHub Actions PAT jobs run on shared runners with untrusted PR branches. Needs runner-level isolation — cannot be fixed inside a step. ([Issue](https://github.com/QwenLM/qwen-code/issues/9089))

---

## Key PR Progress

**#9175 — fix(review): repair seven pipeline defects found by live runs** ([PR](https://github.com/QwenLM/qwen-code/pull/9175))
Two structural defects fixed in incremental anchoring; five pipeline bugs found by watching four live reviews end-to-end.

**#9127 — feat: support session media references end-to-end** ([PR](https://github.com/QwenLM/qwen-code/pull/9127))
Images uploaded once, referenced by media ID + metadata across daemon, ACP bridge, TS SDK, and Web Shell. Big feature for multi-tool workflows.

**#9087 — feat(web-shell): adopt canonical Goal v3 controls** ([PR](https://github.com/QwenLM/qwen-code/pull/9087))
Goals creatable before first message; inspect/edit/pause/resume/replace/clear without routing commands through the model. Compact composer row UI.

**#9082 — fix(ci): force-push release branch so retries replace failed attempts** ([PR](https://github.com/QwenLM/qwen-code/pull/9082))
Stale release branches block retries; force-push replaces them. Directly addresses the v0.21.12-preview.2 publish failure (#9137).

**#8894 — feat(review): capture-tui — rendering claims get pixels, not prose** ([PR](https://github.com/QwenLM/qwen-code/pull/8894))
Drives code under review in a private tmux server, captures the pane exactly as rendered. Evidence-driven review for UI claims.

**#9027 — feat(cli): plain-prose /review comments; severity markers follow attribution** ([PR](https://github.com/QwenLM/qwen-code/pull/9027))
Reviews posted in reviewer's voice, not template voice. Readability-first for everything landing on PRs; severity markers follow `review.attribution`.

**#9087 — feat(web-shell): adopt canonical Goal v3 controls** ([PR](https://github.com/QwenLM/qwen-code/pull/9087))
Goals creatable before first message; inspect/edit/pause/resume/replace/clear without routing commands through the model. Compact composer row UI.

**#9007 — fix(serve): Bound ACP HTTP pre-attach buffers by bytes** ([PR](https://github.com/QwenLM/qwen-code/pull/9007))
Companion to #8051: byte-based buffering bounds for ACP pre-attach, complementing count-only workspace limits.

**#9039 — feat(core): Add privacy-safe tool-result boundary diagnostics** ([PR](https://github.com/QwenLM/qwen-code/pull/9039))
Diagnostics that don't leak tool-result content; helps debug without exposing sensitive data.

**#9163 — fix(review): confine every ledger and evidence read to contained regular files** ([PR](https://github.com/QwenLM/qwen-code/pull/9163))
Closes the R2-2 finding family: every read uses `O_NOFOLLOW` + `fstat` on the same descriptor — the object validated is the object read.

**#9189 — feat(autofix): defer verified out-of-footprint findings to a surviving follow-up queue** ([PR](https://github.com/QwenLM/qwen-code/pull/9189))
Fourth disposition for address-review: verified-but-out-of-footprint findings go to machine-readable queue, preventing silent drift.

**#9027 — feat(cli): plain-prose /review comments; severity markers follow attribution** ([PR](https://github.com/QwenLM/qwen-code/pull/9027))
Reviews posted in reviewer's voice, not template voice. Readability-first for everything landing on PRs.

**#8368 — feat(auth): add Kimi and Xiaomi MiMo providers** ([PR](https://github.com/QwenLM/qwen-code/pull/8368))
First-class presets: Kimi (Coding Plan, API Key CN + Intl), Xiaomi MiMo (PAYG + China/Singapore endpoints). Community-requested provider coverage.

**#8332 — feat(cli): add audio bridge for attachments** ([PR](https://github.com/QwenLM/qwen-code/pull/8332))
Transcribes audio attachments via batch voice model when primary model lacks audio support; explicitly untrusted transcription replacement.

---

## Feature Request Trends

- **Daemon resource bounding** — Multiple issues (#8051, #9007) push for byte-based accounting, not just count-based workspace/session limits
- **Architecture decoupling** — Persistent refactors: making `utils/` a leaf layer (#9146), removing ACP integration dependencies on serve internals (#8084), decoupling from `@google/genai` (#4063)
- **Web Shell as canonical UI** — Expanding Web Shell for export rendering (#9186), Electron desktop evaluation (#9168), Goal v3 adoption (#9087)
- **Provider breadth** — Kimi and Xiaomi MiMo additions (#8368) signal demand for broader third-party model support
- **Media handling** — Audio bridge (#8332), session media references (#9127), and image-load reliability (#8957) show media workflows are front-of-mind

---

## Developer Pain Points

1. **CI flakiness on `main`** — Multiple bot-tracked failures (#9143, #9159, #9160) interrupt workflow; flaky E2E tests block merges and slow delivery
2. **Session/daemon reliability** — Unbounded memory growth (#2128), session restore timeouts (#8678), and resource leaks in long-running sessions frustrate power users
3. **Security-sensitive shell handling** — Command-substitution bypasses (#8582) and PAT exposure on shared runners (#9089) keep security top-of-mind; users want safer-by-default execution
4. **Headless/automation brittleness** — `NO_TOOL_RESULT_PROGRESS` hard-fails (#9026) and SDK/CLI inconsistencies (#9002) break workflows that depend on scripted usage
5. **Review infrastructure complexity** — The sheer volume of review-pipeline tracking issues (deferrals, comparability windows, ledger confinement) suggests the review system itself is a significant maintenance burden — a meta-level pain point for contributors

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-08-15

**Data Source:** [Hmbown/DeepSeek-TUI](https://github.com/Hmbown/CodeWhale)

---

## 1. Today's Highlights

The v0.9.8 release is out (rebranded as **Codewhale**), bringing first-class local DS4 provider setup, a two-layer model-guardian Auto-Review system, and a new "thinking ladder" vocabulary. However, the release is marred by **red CI on all platforms** — three separate assertion failures were filed and fixed within 24 hours, and a **P0 web UI regression** was reported. Community contributors (Lstarsky0, EvanProgramming, cyq1017) drove rapid turnarounds on concurrency bugs, CI fixes, and schema simplifications.

---

## 2. Releases

### [v0.9.8](https://github.com/Hmbown/CodeWhale/releases) — Released 2026-08-14

- **Codewhale rebranding**: Product now ships as `codewhale` (npm/CLI); legacy `deepseek-tui` npm package is deprecated with no further releases.
- **First-class local DS4 (DwarfStar)** setup — keyless loopback preset via `/setup provider ds4`.
- **Model Guardian tier for Auto-Review** — deterministic floor stays non-bypassable; fallback holds escalate to a one-shot model reviewer.
- **Thinking ladder vocabulary** — new reasoning-effort presets replacing off/high/max shortcuts.
- **Moonshot schema degradation** — conditional schemas degrade gracefully instead of being refused.
- **Markdown blockquote rendering** in TUI with a proper quote rail.

---

## 3. Hot Issues (Top 10)

### [#5324 — Agent tool: simplify the 32-field schema](https://github.com/Hmbown/CodeWhale/issues/5324)
*OPEN · 8 comments · Author: Hmbown*
The model-facing `agent` tool carries a 32-property JSON schema with zero required fields and eight actions. Models error on it. **Why it matters:** This is the highest-leverage UX fix for agentic reliability — a bloated schema directly degrades model compliance.

### [#5370 — P0: web UI looks totally broken](https://github.com/Hmbown/CodeWhale/issues/5370)
*OPEN · 1 comment · Author: Hmbown*
Hunter reports the public web UI at codewhale.net is **"totally broken"** — both looks and features. **Why it matters:** A P0 from the maintainer himself; scope covers the Next.js web app and the managed CWC product.

### [#5383 — main is red: provider-count assertions hold pre-release numbers](https://github.com/Hmbown/CodeWhale/issues/5383)
*OPEN · 1 comment · Author: Lstarsky0*
CI fails on two assertions expecting 43/38 providers; v0.9.8 shipped 45/40.

### [#5377 — main is red on macOS/Windows: nine reasoning-effort tests assert pre-ladder vocabulary](https://github.com/Hmbown/CodeWhale/issues/5377)
*OPEN · 1 comment · Author: Lstarsky0*
Not a flake — bisects to one commit, reproduces every run.

### [#5380 — Session-index JSONL writes are unsynchronized; silent data loss](https://github.com/Hmbown/CodeWhale/issues/5380)
*CLOSED · 1 comment · Author: EvanProgramming*
`StateStore::append_thread_name` rewrites `session_index.jsonl` outside the `Arc<Mutex<Connection>>`; concurrent clones can lose data.

### [#5372 — Stale write-claims from closed sessions block new sub-agents](https://github.com/Hmbown/CodeWhale/issues/5372)
*CLOSED · 1 comment · Author: Hmbown*
A dead agent (`agent_8fbd3df6`) still holds claims on directories after session close, causing write-scope contention for new children.

### [#5373 — Output-token ceiling clamped below documented limit; truncation kills turns](https://github.com/Hmbown/CodeWhale/issues/5373)
*CLOSED · 1 comment · Author: Hmbown*
Codewhale requests 65,536 output tokens but the models.dev catalogue documents 384,000. DeepSeek V4 tasks crash under the clamp.

### [#5379 — WebhookHookSink::new panics on HTTP client build failure](https://github.com/Hmbown/CodeWhale/issues/5379)
*CLOSED · 1 comment · Author: EvanProgramming*
A fallback `.expect("build fallback HTTP client")` turns a transient env failure into a hard crash.

### [#5374 — The writing is weird (rendering corruption in TUI)](https://github.com/Hmbown/CodeWhale/issues/5374)
*OPEN · 4 comments · Author: all-lopezg*
On macOS, agent output renders as corrupted text. **Community reaction:** A warm "amazing work" post that quickly got maintainer attention — likely a ratatui rendering regression.

### [#5350 — Simplify third-party model config with pre-built templates](https://github.com/Hmbown/CodeWhale/issues/5350)
*OPEN · 2 comments · Author: shadapang*
Bilingual request (中文/English) to add pre-built templates for OpenCode Zen/Go, Agnes, and Meituan Sensenova — new users can't complete configuration without external docs.

---

## 4. Key PR Progress (Top 10)

### [#5384 — [test/cli] Re-pin provider-count assertions to v0.9.8 registry](https://github.com/Hmbown/CodeWhale/pull/5384)
*OPEN · Author: Lstarsky0 · Closes #5383*
Two integers — updates 43/38 → 45/40 for registry/catalog kinds. Documents the Google Gemini backend split.

### [#5382 — [fix(state)] Serialize session-index writes to prevent silent data loss](https://github.com/Hmbown/CodeWhale/pull/5382)
*CLOSED · Author: EvanProgramming · Closes #5380*
Moves index-file operations under the same `Arc<Mutex>` as the SQLite handle.

### [#5381 — [fix(hooks)] Do not panic when webhook HTTP client fails to build](https://github.com/Hmbown/CodeWhale/pull/5381)
*CLOSED · Author: EvanProgramming · Closes #5379*
Replaces `.expect()` with a graceful error path in `WebhookHookSink::new`.

### [#5378 — [test(tui)] Re-pin thinking-ladder assertions](https://github.com/Hmbown/CodeWhale/pull/5378)
*CLOSED · Author: Lstarsky0 · Closes #5377*
Nine tests updated from off/high/max to the new ladder vocabulary — no production changes, unblocks macOS/Windows CI.

### [#5376 — [fix(tui)] Keep internal runtime events out of the session peek](https://github.com/Hmbown/CodeWhale/pull/5376)
*CLOSED · Author: Lstarsky0 · Closes #5375*
Fixes a repro where internal `PROJECTION`/`PEEK` events leaked into the session peek view.

### [#5365 — [feat(provider)] First-class local DS4 setup](https://github.com/Hmbown/CodeWhale/pull/5365)
*CLOSED · Author: Hmbown*
Keyless loopback preset for DwarfStar, reusing the OpenAI-compatible transport — no new protocol adapter.

### [#5353 — [feat(tui)] Model guardian tier for Auto-Review (v0.9.8)](https://github.com/Hmbown/CodeWhale/pull/5353)
*CLOSED · Author: Hmbown*
Two-layer Auto-Review: deterministic floor stays non-bypassable; fallback holds escalate to a one-shot model guardian. Codex reviewer semantics, Kimi vocabulary, Codewhale fail-closed defaults.

### [#5358 — [feat(engine)] Auto-review denial rationale + turn circuit breaker](https://github.com/Hmbown/CodeWhale/pull/5358)
*CLOSED · Author: Lstarsky0 · First P0 slice of #5352*
Blocks now carry rationale (why denied) plus a circuit breaker so the model stops re-phrasing the same denied action.

### [#5364 — [feat(tui)] Render markdown blockquotes with a quote rail](https://github.com/Hmbown/CodeWhale/pull/5364)
*CLOSED · Author: SparkofSpike*
New `Block::Quote` parser with nesting, inline formatting, wrapping, and correct selection-copy.

### [#5369 — [fix(tools)] Degrade Moonshot schemas instead of refusing conditionals](https://github.com/Hmbown/CodeWhale/pull/5369)
*CLOSED · Author: Lstarsky0 · Prerequisite for #5324*
Splits the schema-slice work so it can land independently.

---

## 5. Feature Request Trends

| Direction | Signal | Evidence |
|---|---|---|
| **Simpler provider onboarding** | High (2 distinct asks this week) | #5350 (pre-built templates), #3192 (agentclientprotocol registry) |
| **Agent schema/semantic simplification** | High (maintainer-driven) | #5324 (32-field schema), #5369 (Moonshot degradation) |
| **Plugin ecosystem maturity** | Medium | #5311 (Kimi-level plugin system + federated marketplaces) |
| **TUI update UX** | Medium | #5053 (update notice + one-chord update-and-relaunch) |
| **Fleet/sub-agent identity clarity** | Medium | #5287 (display fleet/session name, not opaque IDs) |
| **Web UI feature parity** | Urgent (P0) | #5370 (rebuild against harness references), #5290 (localized routes) |

---

## 6. Developer Pain Points

- **Red CI on release day**: Three separate assertion failures (#5383, #5377, #5355) — tests pinned to pre-release numbers while production moved ahead. **Recurring theme:** test fixtures lag registry/catalogue changes.
- **Concurrency data loss**: Session-index and webhook sink bugs (#5380, #5379) show `Arc<Mutex>` coverage is incomplete — clone-friendly `StateStore` design makes this easy to regress.
- **Dead-agent claims blocking new work** (#5372): Write-scope contention after session close is a real-world blocker for multi-agent workflows.
- **Output-token clamp**: Hardcoded 65,536 vs. documented 384,000 — a concrete, documented limitation that kills long tasks.
- **Third-party config friction** (#5350): Users cannot complete setup without external docs; model list stuck at `not checked` / `cache failed`.
- **Community contributors stepping up**: Lstarsky0 and EvanProgramming filed and fixed most CI/concurrency issues within hours — a sign of healthy, technically deep contributors.

---

*Digest compiled from public GitHub data. All links point to the `Hmbown/CodeWhale` repository.*

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/kky-wollu/agents-radar).*
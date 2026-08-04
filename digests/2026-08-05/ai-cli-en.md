# AI CLI Tools Community Digest 2026-08-05

> Generated: 2026-08-04 23:06 UTC | Tools covered: 9

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

# AI CLI Tools Cross-Tool Comparison Report

**2026-08-05**

---

## 1. Ecosystem Overview

The AI CLI tool landscape is maturing rapidly, with eight major tools shipping frequent patch releases and actively engaging with community feedback. Security hardening and reliability fixes dominate this week's release activity, particularly around worktree isolation (Claude Code), trust-boundary enforcement (Qwen Code, Codex), and hook execution security. Cross-cutting themes include persistent memory systems, session continuity across devices, MCP lifecycle management, and Windows/WSL platform friction — reflecting the shift from demo-ready tools to production-grade developer infrastructure. Notably, the ecosystem is converging on protocol-level interoperability (ACP) while differentiating on model support, sandboxing approaches, and enterprise feature depth.

---

## 2. Activity Comparison

| Tool | Issues Updated | PRs Active | Releases (24h) | Release Cadence Signal |
|------|---------------|------------|----------------|----------------------|
| **Claude Code** | ~10 hot issues | 3 PRs | 2 patches (v2.1.221, v2.1.222) | High — security-critical fixes shipped within 24h |
| **OpenAI Codex** | 10 hot issues | 10 PRs | 4 alpha builds | Very High — rapid iteration on `rust-v0.147.0-alpha` |
| **Gemini CLI** | 10 hot issues | 10+ PRs | 0 | Medium — active maintenance, no new releases |
| **GitHub Copilot CLI** | 43 issues updated | 2 PRs | 1 patch (v1.0.79-1) | Medium — breaking rename shipped |
| **Kimi Code CLI** | 10 hot issues | 10 PRs | 0 | Low-Medium — long-open PRs (3+ months) |
| **OpenCode** | 10 hot issues | 10 PRs | 2 patches (v1.18.12, v1.18.13) | High — consistent patch cadence |
| **Pi** | 10 hot issues | 10 PRs | 0 | Medium — infrastructure-heavy PR pipeline |
| **Qwen Code** | 10 hot issues | 10 PRs | 1 (v0.21.5) | Medium-High — active feature work |
| **DeepSeek TUI** | 9 hot issues | 10 PRs | 0 | Low — v0.9.4 train in flight |

---

## 3. Shared Feature Directions

| Feature Direction | Tools | Specific Community Needs |
|-------------------|-------|--------------------------|
| **Session Continuity & Sync** | Claude Code, Codex, Copilot CLI, Kimi CLI, OpenCode | Cross-device resume, cloud sync, session forking (Copilot #1697), live-sync across devices (Codex #14722), multi-device continuity (Kimi #1282, #2203) |
| **Persistent Memory** | Copilot CLI, Kimi CLI, Pi, Gemini CLI | Cross-session memory systems (Kimi #1283), memory disabling honored (Copilot #3859), auto-memory retry/resource leaks (Gemini #26522), memory lifecycle APIs (DeepSeek #5131) |
| **MCP Lifecycle Control** | Codex, Gemini CLI, Kimi CLI, OpenCode, DeepSeek TUI | Lazy startup/shared servers (Codex #21984), full config visibility in consent (Gemini #28664), server lifecycle management via API (DeepSeek #5130), enterprise MCP block due to validation bug (Copilot #4349) |
| **Windows/WSL Friction** | Claude Code, Codex, Copilot CLI, Kimi CLI, OpenCode, Pi, Qwen Code | Text selection broken (Claude #61021), image temp paths in WSL (Codex #27552), Ctrl+H misbehavior (Copilot #4328), IME duplication (Kimi #2584), copy-paste in Tmux (OpenCode #36646), path glob failures (Pi #6817), copy button broken (Qwen #8538) |
| **Compaction/Context Reliability** | Gemini CLI, Pi, Qwen Code, DeepSeek TUI, Claude Code | Compaction failures on enterprise (Pi #6768, #7413), prompt cache invalidation (Qwen #8452), context corruption on quota fallback (Gemini #28671), silent 128K context degradation (DeepSeek #5244) |
| **Build Performance / Monolith Decomposition** | DeepSeek TUI, Gemini CLI | 682K-line monolith recompilation tax (DeepSeek #5249), AST-aware file reads to reduce tokens (Gemini #22745) |
| **Tool-Call Observability** | Copilot CLI, OpenCode, DeepSeek TUI, Qwen Code | Live duration timers (Copilot v1.0.78), real elapsed time visible to model (DeepSeek #5240), retry of empty/unknown responses (OpenCode #40531), execution-specific outcome tracking (Qwen v0.21.5) |
| **Credential/Secret Handling** | Gemini CLI, Pi, Qwen Code, Claude Code | Pre-redaction transcript exposure (Gemini #26525), OAuth error body leakage (Pi #7605), provider warning sanitizer bugs (Qwen #8136), credential file masking (Claude v2.1.221) |

---

## 4. Differentiation Analysis

| Tool | Feature Focus | Target Users | Technical Approach |
|------|--------------|--------------|-------------------|
| **Claude Code** | Security isolation, VSCode UX, plugin ecosystem | Enterprise developers, VSCode users | Worktree isolation enforcement, Focus view, hook system |
| **OpenAI Codex** | Protocol infrastructure, model routing, desktop app | OpenAI ecosystem developers | Rust CLI, concurrent exec-server dispatch, PSP routing |
| **Gemini CLI** | Subagent reliability, OAuth flows, local model support | Google Cloud / GCP developers | SGLang/local endpoints, OTLP telemetry, AST-aware tools |
| **GitHub Copilot CLI** | Enterprise config, theming, sandbox granularity | GitHub Enterprise customers | Managed settings policies, plugin auto-update, sandbox key rename |
| **Kimi Code CLI** | ACP ecosystem expansion, memory systems | Multi-model agent users | ACP protocol work, AI_AGENT env standardization, mobile ecosystem |
| **OpenCode** | TUI polish, provider compatibility, Go subscription | Broad OSS community | DeepSeek V4 Flash support, tmux clipboard, session retry logic |
| **Pi** | Compaction configurability, Windows tracking, RPC/embedding | Terminal power users, PiServer operators | SQLite lanes rework, RPC over sockets, Mermaid rendering |
| **Qwen Code** | Trust boundaries, ACP/IDE integration, cancellation semantics | Qwen model users, JetBrains users | Deterministic execution boundaries, cooperative pause/resume, Tauri migration |
| **DeepSeek TUI** | Build performance, runtime API surface, MCP registry | DeepSeek model users, managed clients | Monolith decomposition, runtime API endpoints, sandbox opt-out request |

---

## 5. Community Momentum & Maturity

**Rapidly Iterating (High Release Velocity):**
- **OpenAI Codex** — 4 alpha builds in 24h, 10 active PRs covering infrastructure, security, and protocol work. Aggressive iteration signals strong investment.
- **Claude Code** — 2 security-focused patches in 24h demonstrate responsive maintenance. Mature community with well-defined plugin ecosystem.
- **OpenCode** — Consistent patch cadence, active contributor PRs, high-traction feature requests (126👍 for billing API).

**Steady Maintenance (Moderate Activity):**
- **Gemini CLI** — Large PR volume but no releases; extensive bug-fix work on quota handling and OAuth. Community carries many `status/need-retesting` labels.
- **Qwen Code** — Active feature development (Tauri migration, trust boundaries) with 10 PRs; security posture is a differentiator.
- **Pi** — Infrastructure-heavy PR pipeline (SQLite, RPC, server sessions) signals architectural investment. Enterprise compaction failures are the top reliability concern.

**Slower Cadence (Lower Release Velocity):**
- **Kimi Code CLI** — 10 open PRs, some 3+ months old (#2200 shell timeouts). Feature requests are high-demand but delivery lags.
- **DeepSeek TUI** — v0.9.4 train in flight with 77 commits; maintainer-filed epics show active triage. Build-performance overhaul is the priority.

**Enterprise-Ready Signals:**
- **GitHub Copilot CLI** — Enterprise configuration friction (#4349, #4005) and managed settings policies indicate enterprise adoption is happening.
- **Pi** — Three separate enterprise compaction failures (#6768, #7413, #7579) suggest production deployment at larger organizations.

---

## 6. Trend Signals

1. **Security Hardening Is the New Battleground.** Claude Code shipped worktree isolation fixes; Qwen Code closed four trust-boundary holes in hooks; Codex added prompt-before-trust for local project directories; Pi keeps response bodies out of OAuth errors. Tools are racing to prove production-safe execution.

2. **Windows Support Is an Ecosystem-Wide Weakness.** Every tool has at least one Windows-specific bug — from IME duplication (Kimi) to text selection (Claude Code) to WSL path handling (Codex, Pi). Pi's maintainers opened a dedicated Windows tracking issue (#7547), acknowledging the problem. Expect Windows investment to differentiate tools in 2026.

3. **Cost Transparency Is a Trust Issue.** Multiple reports of API errors consuming quota with zero output (Claude Code #62466, #70242) and broken pricing endpoints (DeepSeek #5241) are eroding user trust. OpenCode's 126👍 billing API feature request signals demand for programmatic usage visibility.

4. **Compaction Is the New Reliability Frontier.** Across Gemini (quota-fallback corruption), Pi (enterprise failures), Qwen (prompt cache invalidation), and Claude Code (worktree isolation), context compaction is emerging as a common failure point. Users are demanding configurability (compaction models, thinking levels) and reliability.

5. **ACP (Agent Client Protocol) Is Becoming Table Stakes.** Kimi, DeepSeek TUI, and Qwen Code are all investing in ACP support — model discovery, permission modes, tool execution over ACP. This protocol is becoming the interoperability standard for agent-to-IDE/editor communication.

6. **Silent Failures Are the Most Frustrating Failure Mode.** Fake success reports (DeepSeek #5209), hooks silently not firing (Claude #83643), unknown model IDs degrading silently (DeepSeek #5244), and blank responses (OpenCode #40483) consistently surface as top complaints. Tools that surface explicit errors and warnings will win developer trust.

7. **Build Performance Is Becoming a Developer Experience Differentiator.** DeepSeek TUI's monolith decomposition epics and Gemini's AST-aware file read investigation (#22745) signal that development velocity on the tools themselves matters — slow builds mean slow iteration on the codebase, which means slower bug fixes for users.

8. **Enterprise Configuration Is a Double-Edged Sword.** Copilot CLI's managed settings validation bug (#4349) blocking all MCP servers, and Pi's enterprise compaction failures, show that enterprise features introduced without sufficient testing create outsized damage when they fail — the blast radius is greater than consumer-facing bugs.

---

*Report compiled from 2026-08-05 community digests across 9 AI CLI tools: Claude Code, OpenAI Codex, Gemini CLI, GitHub Copilot CLI, Kimi Code CLI, OpenCode, Pi, Qwen Code, and DeepSeek TUI.*

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report

*Data as of 2026-08-05 | Source: github.com/anthropics/skills*

---

## 1. Top Skills Ranking

The most-discussed Skill submissions, ranked by community attention and technical significance:

### 1. skill-creator fixes (Multiple PRs — #1298, #1323, #1099, #1050, #1261, #539)
**Author:** MartinCajiao, Polluelo978, joshuawowk, gstreet-ops, alvingarcia, Lubrsy706  
**Status:** Open | **Created:** 2026-03 through 2026-06

This cluster of fixes addresses critical bugs in the `skill-creator` evaluation pipeline. The primary issue (#556) causes `run_eval.py` to report **`recall=0%`** for every skill description, rendering the description-optimization loop useless. Root causes include:
- Windows subprocess incompatibilities (`claude.cmd` vs `claude`, `WinError 10038`, cp1252 encoding)
- Trigger detection failures (missing real skill name, bailing on non-Skill tools)
- Command files written to live project `.claude/commands/` instead of isolated eval directories

**Why it matters:** The skill-creator is the meta-skill that generates other skills. A broken evaluation loop means no skill descriptions get properly optimized. This is the community's highest-priority pain point.

[PR #1298](https://github.com/anthropics/skills/pull/1298) · [PR #1323](https://github.com/anthropics/skills/pull/1323) · [PR #1099](https://github.com/anthropics/skills/pull/1099) · [PR #1050](https://github.com/anthropics/skills/pull/1050) · [PR #1261](https://github.com/anthropics/skills/pull/1261) · [PR #539](https://github.com/anthropics/skills/pull/539)

### 2. document-typography — Typographic quality control
**Author:** PGTBoos | **Status:** Open | **Created:** 2026-03-04

Prevents typographic defects in AI-generated documents: orphan word wrap, stranded widow headers, and numbering misalignment. These are silent quality issues affecting every document Claude generates.

The discussion highlights that users rarely request typographic fixes explicitly — making this a latent-value skill those quality issues go unnoticed.

[PR #514](https://github.com/anthropics/skills/pull/514)

### 3. ODT skill — OpenDocument handling
**Author:** GitHubNewbie0 | **Status:** Open | **Created:** 2026-03-01

Covers creation, template filling, reading, and conversion of OpenDocument formats (.odt, .ods, .odf). Fills a clear gap: the official collection has DOCX and PDF skills but no ODT equivalent, blocking LibreOffice-centric workflows.

[PR #486](https://github.com/anthropics/skills/pull/486)

### 4. self-audit — Mechanical + reasoning quality gate
**Author:** YuhaoLin2005 | **Status:** Open | **Created:** 2026-06-28

A universal audit skill: first verifies every claimed output file exists (mechanical check), then performs a four-dimension reasoning audit in damage-severity priority order. Works with any project, stack, or model. The companion issue #1385 proposes a three-gate pipeline (pre-task → adversarial review → delivery).

[PR #1367](https://github.com/anthropics/skills/pull/1367) · [Issue #1385](https://github.com/anthropics/skills/issues/1385)

### 5. pyxel — Retro game development
**Author:** kitao | **Status:** Open | **Created:** 2026-03-05

Wraps `pyxel-mcp` (MCP server for the Pyxel retro game engine). Covers the write → run_and_capture → inspect → iterate loop for pixel-art/8-bit games with Python. Notable for connecting two ecosystems: Claude Code Skills and MCP servers.

[PR #525](https://github.com/anthropics/skills/pull/525)

### 6. testing-patterns — Full-stack testing methodology
**Author:** 4444J99 | **Status:** Open | **Created:** 2026-03-22

Comprehensive testing skill: Testing Trophy model, AAA pattern, React component testing with Testing Library, and philosophy on what *not* to test. Represents the testing category's flagship submission.

[PR #723](https://github.com/anthropics/skills/pull/723)

### 7. frontend-design clarity revision
**Author:** justinwetch | **Status:** Open | **Created:** 2026-01-05

Revises the existing frontend-design skill to make every instruction actionable within a single conversation. The discussion centers on making skills behaviorally specific rather than conceptually educational — a recurring theme across submissions.

[PR #210](https://github.com/anthropics/skills/pull/210)

### 8. color-expert — Color knowledge skill
**Author:** meodai | **Status:** Open | **Created:** 2026-06-10

Self-contained color expertise: naming systems (ISCC-NBS, Munsell, RAL), color-space selection tables (OKLCH vs OKLAB vs CAM16), and contrast rules. A niche but focused specialization with clear trigger conditions.

[PR #1302](https://github.com/anthropics/skills/pull/1302)

---

## 2. Community Demand Trends

From Issues, the clearest demand signals:

| Trend | Signal | Evidence |
|-------|--------|----------|
| **Skill quality & security tooling** | #492 (43 comments) — community skills distributed under `anthropic/` namespace are indistinguishable from official ones, enabling trust boundary abuse | Issue #492 |
| **Skill-creator reliability** | #556 (12 comments) and #1169 (3 comments) — the evaluation loop reports 0% recall for *everything*, meaning nobody can trust skill optimization | Issues #556, #1169 |
| **Org-wide skill sharing** | #228 (16 comments) — users want skill libraries and sharing links instead of manual .skill file transfers | Issue #228 |
| **Duplicate content across plugins** | #189 (6 comments, 9 👍) — `document-skills` and `example-skills` install identical skills, wasting context window | Issue #189 |
| **Context-window safety** | #1487 (4 comments) — `claude-api` skill injects ~156k tokens in a single tool call, exhausting context | Issue #1487 |
| **Windows compatibility** | #1061 (3 comments) — skill-creator scripts are Unix-first; blocking native Windows users | Issue #1061 |

**Emerging demand:** Quality assurance and audit skills (self-audit, agent-governance #412, reasoning gates #1385) represent a growing "meta" category — the community wants skills that verify *other skills' output*, not just produce artifacts.

---

## 3. High-Potential Pending Skills

Active PRs likely to merge soon:

| Skill | Why it stands out | PR |
|-------|------------------|----|
| **plan-file-hygiene** | Addresses #1417 — planning artifacts accumulate with no lifecycle, wasting context. Built on explicit community framing from two other users; multi-author alignment | [PR #1479](https://github.com/anthropics/skills/pull/1479) |
| **self-audit (v1.3.0)** | Universal, model-agnostic, dual-mechanism (mechanical + reasoning). Companion issue has 4 comments of active development | [PR #1367](https://github.com/anthropics/skills/pull/1367) |
| **testing-patterns** | Fills a gap with no current coverage; comprehensive scope spanning unit → component → philosophy | [PR #723](https://github.com/anthropics/skills/pull/723) |
| **SAP-RPT-1-OSS predictor** | Bridges enterprise data science with Claude Code; SAP's open-source tabular foundation model | [PR #181](https://github.com/anthropics/skills/pull/181) |
| **skill-quality-analyzer + skill-security-analyzer** | Meta-skills for auditing other skills' quality and security — directly addresses the #492 trust concern | [PR #83](https://github.com/anthropics/skills/pull/83) |
| **compact-memory** | Symbolic notation for compact agent state; targets the context-window exhaustion problem with a concrete proposal | [Issue #1329](https://github.com/anthropics/skills/issues/1329) |

---

## 4. Skills Ecosystem Insight

The community's most concentrated demand is for **trustworthy, quality-assured skills infrastructure** — fixing the broken skill-creator evaluation loop, auditing existing skills for security and context-window safety, and adding verification/audit layers — before expanding into new functional domains.

---

# Claude Code Community Digest
**2026-08-05**

---

## 1. Today's Highlights

Two patch releases shipped within 24 hours. v2.1.221 introduces a significant UX improvement for VS Code users with a new "Focus view" that collapses tool activity into per-turn summaries, alongside credential file masking on Linux. v2.1.222 closes a critical security gap by enforcing worktree isolation for destructive git commands and fixing a PreToolUse hook bypass in background agent tasks. Meanwhile, the community continues to surface concerns around API error handling, cost consumption from failed requests, and Windows/VSCode-specific permission and UX friction.

---

## 2. Releases

**v2.1.222** — Security-focused patch
- Fixed worktree-isolated sessions and subagents being able to run destructive git commands against the main checkout; isolation now applies to file edits and Bash in every session type
- Fixed PreToolUse auto-allow hooks bypassing tool restrictions in background agent tasks

**v2.1.221** — UX and platform improvements
- [VSCode] Added Focus view: a chat-menu toggle that hides tool activity behind an expandable per-turn summary with a live running-tool indicator, toggled with `Ctrl+Alt+F` or the "Claude Code: Toggle Focus view" command
- Added `mode: "mask"` for sandbox credential files on Linux

---

## 3. Hot Issues

**#62466 — Repeated "Image couldn't be processed" API errors consuming usage limit**
[GitHub](https://github.com/anthropics/claude-code/issues/62466) | 29 comments | 20 👍
Open since May, this issue has gained significant traction. Users report image processing failures that burn API quota with zero output. The sustained 29-comment thread and 20 upvotes suggest this is a recurring, costly problem — particularly painful for paid subscribers on usage-based plans.

**#61021 — Text selection/copy broken in VSCode terminal**
[GitHub](https://github.com/anthropics/claude-code/issues/61021) | 15 comments | 11 👍
A Windows + VSCode-specific regression where running Claude Code in the integrated terminal breaks native text selection and Ctrl+C copy behavior. High upvote count indicates broad impact on daily developer workflows.

**#68514 — Checksum mismatch for rootfs.img.zst on macOS Sequoia**
[GitHub](https://github.com/anthropics/claude-code/issues/68514) | 16 comments | 4 👍
Closed as stale, but the 16-comment thread suggests users encountered real installation friction on Apple Silicon Macs. The closure without visible resolution may frustrate affected users.

**#72123 — Read Out Loud audio degrades mid-playback**
[GitHub](https://github.com/anthropics/claude-code/issues/72123) | 7 comments | 1 👍
A niche but reported Windows desktop issue: voice playback degrades mid-reading, becoming soft, speeding up, changing pitch, and fading. Accessibility-relevant for users relying on audio output.

**#80614 — /model selection not persisted across restarts**
[GitHub](https://github.com/anthropics/claude-code/issues/80614) | 2 comments | 0 👍
Open and recent (July 23). The CLI explicitly confirms "saved as your default for new sessions" but the setting does not survive restarts — a clear bug with confusing UX messaging.

**#83643 — Desktop remote sessions: plugin hooks never fire**
[GitHub](https://github.com/anthropics/claude-code/issues/83643) | 1 comment | 0 👍
New (Aug 3): plugin-loaded hooks are silently omitted during SSH remote session sync. Skills and commands work, but hooks don't. Silent failure makes this particularly insidious for automation-heavy workflows.

**#83815 — Desktop SSH dead-end password prompt on key-only hosts**
[GitHub](https://github.com/anthropics/claude-code/issues/83815) | 1 comment | 0 👍
Fresh (Aug 4): when connecting to key-only SSH hosts, Claude Code shows a password dialog that can never succeed. The nonexistent identity file is silently ignored with no fallback to the default key.

**#72714 — /worktree writes core.hooksPath into MAIN repo config**
[GitHub](https://github.com/anthropics/claude-code/issues/72714) | 1 comment | 0 👍
A subtle but dangerous bug: the `/worktree` feature can write `core.hooksPath` into the main repository's shared `.git/config`, silently disabling global git hooks. Long-term side effects beyond the worktree session.

**#70242 — Opus 4.8 safety classifier outages burned weekly quota**
[GitHub](https://github.com/anthropics/claude-code/issues/70242) | 2 comments | 0 👍
A scathing report from a 200€+/month user: an urgent client session was destroyed by platform-side outages, consuming his entire weekly quota with zero output. Highlights the cost risk when reliability fails at the platform level.

**#70069 — Worktree isolation broken: edits land on main checkout**
[GitHub](https://github.com/anthropics/claude-code/issues/70069) | 4 comments | 0 👍
Filed June 22, closed but directly relevant to what v2.1.222 claims to fix. Sessions with `-w` silently applied edits to the main branch despite reporting the worktree in cwd and gitBranch. Community will be watching whether the fix holds.

---

## 4. Key PR Progress

**#83374 — docs(plugin-dev): document MessageDisplay streaming semantics**
[GitHub](https://github.com/anthropics/claude-code/pull/83374) | Opened Aug 2
The bundled Hook Development skill omits `MessageDisplay` from its trigger description, event guidance, and quick-reference table. This PR documents it — small but valuable for plugin developers who need complete hook event documentation.

**#83738 — Fix/83484 symlink path expansion**
[GitHub](https://github.com/anthropics/claude-code/pull/83738) | Opened Aug 4
Fixes issue #83484 where `claude install` creates a broken symlink at `~/.local/bin/claude` pointing to a literal `%h` placeholder instead of the expanded home directory path on some Linux installs.

**#83890 — Create pylint.yml**
[GitHub](https://github.com/anthropics/claude-code/pull/83890) | Opened Aug 4
Adds a GitHub Actions workflow for pylint CI. The intent is presumably to enforce Python linting, though the PR lacks a description — reviewers should verify it targets the right codebase and doesn't add noisy check failures.

---

## 5. Feature Request Trends

**MessageDisplay hook documentation** — The desire for complete, accurate hook event documentation in the bundled plugin-development skill points to broader demand for first-class plugin authoring support.

**Configurable terminal shell on Windows** — Users want to override the hardcoded PowerShell 5.1 terminal shell path via settings.json. PATH manipulation is insufficient because the full path is baked in.

**Permission prompt UX improvements** — The VSCode extension's permission dialogs lag behind the CLI: missing "Allow for session/project/always" options (closed #64689) and truncated command text in "Always allow" (closed #70057). Several stale-closed issues but the underlying UX gap persists.

**"Press Enter" hint for auth code paste** — A small but telling UX gap on Windows: the terminal gives no affordance that you must press Enter after pasting an auth code.

**Focus view / reduced tool noise** — The new v2.1.221 Focus view directly addresses a recurring theme: users want to reduce visual tool-call noise and get concise per-turn summaries. Expect more requests in this direction.

---

## 6. Developer Pain Points

**Cost without output** — The most emotionally charged complaints center on API errors or platform outages consuming weekly quotas or session limits with zero useful output (#62466, #70242, #70272). For paying users, this erodes trust in the product's reliability and billing model.

**Worktree isolation bugs** — Multiple issues and a dedicated fix release in 24h underscore how problematic worktree isolation has been: edits landing on main checkout (#70069), destructive git commands escaping isolation (fixed in v2.1.222), and hooksPath corruption in shared config (#72714). Dangerous for users managing multiple branches.

**VSCode extension friction** — Windows-specific UX problems keep recurring: broken text selection (#61021), truncated permission prompts (#70057), and missing approval options (#64689). Indicates the VSCode extension path has inconsistent testing across Windows environments.

**Silent failures** — Issues where things fail without errors are called out repeatedly: plugin hooks silently not firing in remote sessions (#83643), silent self-contamination of tool-call XML (#70241), and agent-side silent extraction failures (#70258). Debugging blind is the most frustrating failure mode.

**Session/context management** — Users report agents losing context after `/compact` (#69905), model freezes followed by non-sequitur replies (#70273), and slowness drawing obvious conclusions from existing evidence (#70261). Context reliability remains a top concern as models scale to 1M-token contexts.

---

*Digest generated from github.com/anthropics/claude-code data on 2026-08-05.*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-08-05

## Today's Highlights
A rapid-fire sequence of `rust-v0.147.0-alpha` releases landed in the last 24 hours, signaling active iteration on the CLI. The maintainers merged a large batch of infrastructure improvements—including concurrent exec-server dispatch, configurable token-budget identity, and a prompt-before-trust security guard—while the community continues to surface Windows/WSL integration friction and MCP lifecycle issues as the top pain points.

## Releases
Four new alpha builds shipped in the last 24 hours:
- **rust-v0.147.0-alpha.7** ([release](https://github.com/openai/codex/releases/tag/rust-v0.147.0-alpha.7))
- **rust-v0.147.0-alpha.6.4** ([release](https://github.com/openai/codex/releases/tag/rust-v0.147.0-alpha.6.4))
- **rust-v0.147.0-alpha.6.3** ([release](https://github.com/openai/codex/releases/tag/rust-v0.147.0-alpha.6.3))
- **rust-v0.147.0-alpha.6.1** ([release](https://github.com/openai/codex/releases/tag/rust-v0.147.0-alpha.6.1))

No detailed changelogs were published with these cutting-edge builds. Given the high PR throughput seen today (see below), these likely bundle the concurrent exec-server dispatch, model catalog cache injection, and token-budget identity work.

## Hot Issues
1. **[#27552 — Codex Desktop Windows: image attachment saved to Temp but not accessible to WSL agent](https://github.com/openai/codex/issues/27552)** (15 comments, 9 👍)
   The top-voted open issue. Image attachments in the Windows desktop app land in a Temp path that the WSL-side agent cannot read, breaking `view_image` workflows. High engagement reflects the ongoing pain of hybrid Windows/WSL environments.

2. **[#21984 — MCP servers eagerly start per session](https://github.com/openai/codex/issues/21984)** (13 comments, 4 👍)
   Long-lived Codex sessions each spin up their own headed-browser MCP servers, leaking visible processes. Community is asking for lazy startup or shared server instances.

3. **[#29787 — Codex app doesn't restart after update](https://github.com/openai/codex/issues/29787)** (12 comments, 2 👍)
   Windows users report clicking the update button closes the app permanently. Closed as of today, but the thread captures a sharp onboarding bug.

4. **[#22991 — App freezes with very large rollout/history JSONL files](https://github.com/openai/codex/issues/22991)** (11 comments, 1 👍)
   Sessions growing to 500 MB+ make the desktop app unusable. Points to a need for compaction or lazy-loading of session history.

5. **[#14794 — VS Code extension sandbox makes devcontainer workspace read-only in Linux](https://github.com/openai/codex/issues/14794)** (10 comments, 8 👍)
   Sandboxed extension runs break writable devcontainer workspaces. High 👍 count signals widespread IDE-sandbox friction.

6. **[#14722 — Sync CLI and app-server sessions](https://github.com/openai/codex/issues/14722)** (9 comments, 21 👍)
   The most-upvoted issue in the thread. Users want `codex resume` from another device to live-sync with the active session. Closed, but demand is clearly high for cross-device session continuity.

7. **[#30816 — Weekly usage reset date changed after subscribing to ChatGPT Plus](https://github.com/openai/codex/issues/30816)** (8 comments, 4 👍)
   Rate-limit bookkeeping confusion: upgrading to Plus unexpectedly reset the weekly window, angering users who planned usage around the old cadence.

8. **[#32778 — Windows Codex causes system-wide memory growth through shared/GPU memory](https://github.com/openai/codex/issues/32778)** (3 comments)
   Newer report of memory not being released on Windows, attributed to unaccounted shared/GPU memory. Performance-related issues remain a recurring theme.

9. **[#32936 — Chrome/Browser plugin fails to import in node_repl: Cannot redefine property: process](https://github.com/openai/codex/issues/32936)** (3 comments, 2 👍)
   The bundled browser plugin breaks in the `node_repl` trusted-module runtime. Related to **#36988**, filed today with the same root error on macOS.

10. **[#36673 — Codex Desktop intermittently exposes thread tools without registered handlers](https://github.com/openai/codex/issues/36673)** (2 comments)
    Model sees `list_threads`/`read_thread`/`send_message` tools but invocations fail with "No handler registered." Points to a race in tool registration on the app-server path.

## Key PR Progress
1. **[#36992 — Allow injecting model catalog caches](https://github.com/openai/codex/pull/36992)**
   Adds a public `ModelsCache` contract, letting providers and `OpenAiModelsManager` accept caller-supplied cache implementations while retaining the default file-backed cache.

2. **[#36990 — Remove legacy collaboration mode variants](https://github.com/openai/codex/pull/36990)**
   Drops hidden `PairProgramming` and `Execute` mode kinds and their unused prompt templates, simplifying mode handling to `Default` and `Plan`.

3. **[#36987 — Add opt-in concurrent exec-server request dispatch](https://github.com/openai/codex/pull/36987)**
   New `--concurrent-requests <COUNT>` flag prevents long-running requests from blocking health checks and cleanup on the same connection—a direct answer to observed lifecycle issues.

4. **[#36986 — Add process-scoped PSP routing for ChatGPT requests](https://github.com/openai/codex/pull/36986)**
   Hidden global `--psp` flag propagated through TUI, exec, app-server, and remote-control startup paths, attaching the `oai-chat-psp=true` cookie for first-party ChatGPT traffic.

5. **[#36981 — Enable remote compaction for Amazon Bedrock](https://github.com/openai/codex/pull/36981)**
   Marks Bedrock as v1-only so manual and automatic compaction use `/v1/responses/compact`, preserving v2 behavior elsewhere.

6. **[#36977 — Improve connector detection for migrated sessions](https://github.com/openai/codex/pull/36977)**
   Fixes a bug where session IDs derived from file stems could cross-contaminate connector attribution during batched migrations.

7. **[#36976 — Honor explicit-only orchestrator skills](https://github.com/openai/codex/pull/36976)**
   Skills with `allow_implicit_invocation: false` are now hidden from the model-visible catalog while remaining directly invocable.

8. **[#36970 — Make token budget context identity configurable](https://github.com/openai/codex/pull/36970)**
   Adds `features.token_budget.mode` setting (`thread` vs `name`), defaulting to thread ID while allowing the agent name to be retained.

9. **[#36960 — Prompt before trusting local project directories](https://github.com/openai/codex/pull/36960)**
   Security hardening: project-local config, hooks, and exec policies now require an explicit trust decision instead of auto-trusting, addressing prompt-injection exposure.

10. **[#36966 — Allow disabling the built-in image viewer](https://github.com/openai/codex/pull/36966)**
    New stable `features.view_image` flag (default-enabled) omits the native `view_image` tool when disabled, including for subagent and guardian turns.

## Feature Request Trends
- **Session continuity and sync** — Users want `codex resume` to live-sync with active sessions across devices (#14722), and desktop-app sessions to be resumable in the WSL TUI (#25741).
- **MCP lifecycle control** — Eager per-session MCP startup needs opt-in lazy loading or shared server processes (#21984).
- **Configuration parity across WSL/Windows** — The app should respect WSL-side `AGENTS.md`, `config.toml`, and skills when running in WSL mode (#25747, #25745, #21438).
- **Better large-session handling** — Compaction, lazy-loading, or rollup strategies for multi-hundred-MB history files (#22991).
- **Rate-limit transparency** — Clearer resets, pro-rata calculations, and plan-downgrade handling (#30816, #23206, #32344).

## Developer Pain Points
- **Windows/WSL hybrid friction** dominates the open issue list: image temp paths, config file selection, session resumption, and archiving all misbehave when mixing Windows app with WSL workspaces.
- **Session-history bloat** leads to app freezes and slow startups; users report files reaching 500 MB+ with no mitigation.
- **Plugin/runtime incompatibilities** — the browser plugin crashing in `node_repl` with "Cannot redefine property: process" affects both Windows and macOS paths, indicating a systemic bootstrap issue.
- **Rate-limit accounting surprises** — resets on plan changes, phantom Lite-plan detection, and usage ticking down after killed sessions erode user trust in usage reporting.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-08-05

---

## 1. Today's Highlights

The Gemini CLI project saw a significant influx of pull requests focused on hardening core infrastructure, with 28 PRs updated in the last 24 hours targeting OAuth/auth reliability, error propagation, and process handling. No new releases shipped today, but a wave of bug-fix PRs (including fixes for `/compress` failures, quota-fallback corruption, and shell hangs) signals active maintenance. Notably, the community's longest-standing pain points remain concentrated around subagent reliability, shell process hangs, and configuration edge cases, with many issues carrying the `status/need-retesting` label suggesting an active triage cycle.

---

## 2. Releases

No new releases were published in the last 24 hours.

---

## 3. Hot Issues

**#22323 — Subagent recovery after MAX_TURNS is reported as GOAL success** (12 comments, 👍2)  
[Link](https://github.com/google-gemini/gemini-cli/issues/22323)  
The `codebase_investigator` subagent falsely reports `GOAL` success after hitting max-turns, masking real failures. This is a correctness issue that could silently undermine user trust in agent outcomes. High comment count suggests debugging complexity.

**#21409 — Generalist agent hangs indefinitely** (8 comments, 👍8)  
[Link](https://github.com/google-gemini/gemini-cli/issues/21409)  
A critical reliability bug: the generalist agent hangs on trivial operations like folder creation, requiring user cancellation after up to an hour. High 👍 count indicates widespread impact; workaround requires disabling subagents entirely.

**#24353 — Robust component-level evaluations (EPIC)** (7 comments)  
[Link](https://github.com/google-gemini/gemini-cli/issues/24353)  
Tracks expanding the behavioral eval harness from 76 tests across 6 Gemini models — a major quality-assurance initiative aiming to reduce regressions in agent behavior.

**#22745 — Assess impact of AST-aware file reads/search/mapping** (7 comments, 👍1)  
[Link](https://github.com/google-gemini/gemini-cli/issues/22745)  
Investigates whether AST-aware tools could reduce token noise and turn count when reading code. Promising efficiency gain if proven — could meaningfully reduce cost per session.

**#25166 — Shell command hangs at "Waiting input" after completion** (4 comments, 👍3)  
[Link](https://github.com/google-gemini/gemini-cli/issues/25166)  
Reproducible hang after simple commands finish — extremely common scenario, causing persistent session stalls. The P1 priority confirms real-world friction.

**#21968 — Gemini does not use skills/sub-agents autonomously** (6 comments)  
[Link](https://github.com/google-gemini/gemini-cli/issues/21968)  
Anecdotal but resonant: even when skills and subagents exist with clear descriptions, the model rarely invokes them unprompted. Undermines the value proposition of custom skill extension.

**#26522 — Auto Memory retries low-signal sessions indefinitely** (5 comments)  
[Link](https://github.com/google-gemini/gemini-cli/issues/26522)  
Sessions are never marked processed if the agent decides not to read them — a subtle resource leak that continuously re-surfaces stale sessions.

**#26525 — Add deterministic redaction and reduce Auto Memory logging** (4 comments)  
[Link](https://github.com/google-gemini/gemini-cli/issues/26525)  
Security concern: transcripts are sent to the model *before* redaction occurs, and the service may log existing skill content. Sensitive-data exposure risk.

**#22232 — Enhance browser_agent resilience: automatic session takeover** (4 comments)  
[Link](https://github.com/google-gemini/gemini-cli/issues/22232)  
The "fail-fast" strategy on locked browser profiles is too brittle for persistent sessions — orphaned processes block legitimate usage.

**#11802 — Add OTLP headers for telemetry** (3 comments, 👍7)  
[Link](https://github.com/google-gemini/gemini-cli/issues/11802)  
Long-standing feature request (since Oct 2025) to support custom authentication headers for OTLP telemetry export — blocking users who need auth'd collector endpoints.

---

## 4. Key PR Progress

**#28690 — [CLOSED] feat(ingestion): issue comment handling and re-triage workflow**  
[Link](https://github.com/google-gemini/gemini-cli/pull/28690)  
Adds `issue_comment.created` webhook support to the Caretaker Agent, enabling `@caretaker-agent` mentions and `/caretaker triage` slash commands to re-triage `NEEDS_INFO` issues. Improves maintainer workflow responsiveness.

**#28689 — fix(core): unwrap nested gaxios streaming errors**  
[Link](https://github.com/google-gemini/gemini-cli/pull/28689)  
Parses errors from `error.cause.message` for structured rate-limit/capacity errors — directly addresses confusing quota failure UX.

**#28639 — fix(core): guard formatTruncatedToolOutput against non-positive maxChars**  
[Link](https://github.com/google-gemini/gemini-cli/pull/28639)  
Fixes a subtle bug where `maxChars <= 0` inflated output ~2x due to JavaScript `slice` negative-index behavior. Includes regression tests.

**#28641 — fix(cli): prevent ghost text wrapping infinite loop**  
[Link](https://github.com/google-gemini/gemini-cli/pull/28641)  
Fixes an infinite loop in `getGhostTextLines` when input width is narrower than a single CJK/emoji codepoint — a real edge-case freeze.

**#28688 — fix(core): dynamically resolve Cloud Workstations proxy redirect URI**  
[Link](https://github.com/google-gemini/gemini-cli/pull/28688)  
Fixes OAuth flows failing inside Cloud Workstations VMs by dynamically resolving the redirect URI instead of hardcoding `localhost`.

**#28664 — fix(mcp): reflect full server config in consent; harden stdio env**  
[Link](https://github.com/google-gemini/gemini-cli/pull/28664)  
Consent prompt now shows `env`, `cwd`, and `headers` — not just command/args — closing a visibility gap where users could approve configs they didn't fully see.

**#28681 — feat(core,cli): add support for SGLang and local OpenAI-compatible endpoints**  
[Link](https://github.com/google-gemini/gemini-cli/pull/28681)  
Large feature addition enabling local/self-hosted model inference — significant for privacy-sensitive teams and offline workflows.

**#28671 — fix(core,cli): resolve context corruption and quota error fallback issues**  
[Link](https://github.com/google-gemini/gemini-cli/pull/28671)  
Defensive history hardening against interrupted tool executions and ESC queries — targets a class of hard-to-reproduce corruption bugs.

**#28672 — fix(core,cli): repair /compress session reload and quota-fallback tool response loss**  
[Link](https://github.com/google-gemini/gemini-cli/pull/28672)  
Two independent fixes: `/compress` failing to reload resumed sessions, and quota-limit hits corrupting tool responses. Both are high-traffic failure modes.

**#28677 — fix(core): add timeout to IdeClient.getInstance() process traversal**  
[Link](https://github.com/google-gemini/gemini-cli/pull/28677)  
Prevents TUI stalling on "Initializing..." forever when `getIdeProcessInfo()` hangs — adds a 3-second timeout with fallback to no-IDE client.

---

## 5. Feature Request Trends

**Local/self-hosted model support is the strongest new direction**  
PR #28681 adding SGLang and local OpenAI-compatible endpoints is the clearest signal. Combined with ongoing OAuth/telemetry improvements, this suggests community demand for enterprise-friendly, network-isolated deployments.

**AST-aware codebase analysis keeps gaining momentum**  
Issues #22745 and #22746 both explore AST-aware file reads, search, and mapping via tools like `tilth` or `glyph`. Expected benefits: fewer turns, smaller token footprint, more precise method-boundary reads.

**Subagent visibility and control**  
Issues #22598 (subagent trajectory sharing via `/chat share`) and #21432 (agent self-awareness of its own flags/hotkeys) point to a desire for more introspection and governance of agent internals.

**Browser agent resilience**  
Issue #22232 requests automatic session takeover and lock recovery for persistent browser profiles — a reliability gap for automation-heavy users.

---

## 6. Developer Pain Points

**Subagent reliability remains the #1 friction point**  
Three P1 issues (#22323, #21409, #22186) involve subagent failure modes: false success reporting, infinite hangs, and crashes. Workaround for developers: disable subagents entirely — a blunt but effective escape hatch.

**Shell process management is fragile**  
Issue #25166 shows the CLI hanging at "Waiting input" after simple commands finish. PRs #28676 (signal forwarding) and #28677 (IDE client timeout) address adjacent process-management bugs — a cluster of related issues suggests an area of systemic weakness.

**Quota/error handling produces confusing or corrupt state**  
PRs #28671 and #28672 both address quota-fallback corruption; PR #28689 improves error parsing. The pattern: users hit rate limits, and the CLI corrupts history or shows unhelpful errors, losing work.

**Configuration edge cases are still biting**  
Symlinked agent files not recognized (#20079), browser agent ignoring `settings.json` overrides (#22267), Vite interactive prompts hanging (#22465), and escape-sequence bugs (#22466) — these small correctness issues erode trust in everyday workflows.

**Security-scoped cleanups are actively underway**  
Auto Memory sends transcripts to models pre-redaction (#26525), OAuth timeouts leak resources (#28678), and stale Authorization headers cause 401s (#28546) — the maintainer team appears to be prioritizing hardening the supply chain and secret handling.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-08-05

---

## 1. Today's Highlights

A new patch release (v1.0.79-1) introduces a **breaking rename** of the sandbox setting `allowDevToolCaches` to `allowDevToolAccess`, expanding its scope to dev-tool configs and registries — existing opt-outs will silently revert to default-on, so users must update their settings. The previous release (v1.0.78) added **live tool-call duration timers** in timeline headers (configurable via `/settings showToolDurations`) and **automatic first-party plugin updates** at session start. Community activity remains high around theming, session management, and enterprise configuration friction, with 43 issues updated in the last 24 hours.

---

## 2. Releases

**No releases published in the last 24 hours.**

| Version | Date | Key Changes |
|---------|------|-------------|
| v1.0.79-1 | Aug 4, 2026 | **⚠️ BREAKING:** Sandbox setting `allowDevToolCaches` renamed to `allowDevToolAccess` (now grants dev-tool config and registries, not just caches). Old key is silently ignored; existing `false` opt-outs revert to default-on. Users must rename the key in settings. |
| v1.0.78 | Aug 3, 2026 | • Timeline headers now show tool-call durations (right-aligned, live-ticking for calls ≥5s), on by default — disable with `/settings showToolDurations`<br>• First-party plugins auto-update to latest at session start |

---

## 3. Hot Issues (Top 10)

### [#1504 — Custom theme support](https://github.com/github/copilot-cli/issues/1504) · **OPEN** · 👍 23 · 8 comments
*[area:theming-accessibility]*
Users want custom, shareable themes (even as JSON files) via `/theme`. The demand signals growing interest in personalization and consistent branding across teams.

### [#1697 — Session forking](https://github.com/github/copilot-cli/issues/1697) · **OPEN** · 👍 25 · 3 comments
*[area:sessions, area:context-memory]*
When a multi-step task branches into two independent problems, users currently must choose one path and lose context. Forking would let developers branch a conversation into parallel sessions with shared context — the highest-reacted open feature request.

### [#4328 — Ctrl+H misinterpreted under WSL2](https://github.com/github/copilot-cli/issues/4328) · **OPEN** · 5 comments
*[area:input-keyboard, area:platform-windows]*
`Ctrl+H` (delete previous character) behaves like `Ctrl+W` (delete word) under WSL2 due to `WT_SESSION` leaking from Windows Terminal. A precise, reproducible input-handling bug affecting a large WSL2 developer segment.

### [#4202 — `view` tool reports "Path does not exist" for existing files](https://github.com/github/copilot-cli/issues/4202) · **OPEN** · 4 comments
*[area:non-interactive, area:tools]*
Regression introduced in v1.0.72 where the built-in `view` tool fails on existing files; v1.0.71 succeeds. Critical tooling reliability issue in non-interactive workflows.

### [#1947 — Cloud-synced sessions for cross-device continuity](https://github.com/github/copilot-cli/issues/1947) · **CLOSED** · 4 comments · 👍 6
*[area:sessions]*
Sessions stored locally in `~/.copilot/` tie developers to one machine. Request for cloud sync to enable seamless device switching — a recurring theme in session management requests.

### [#4005 — "Copilot billing entity isn't selected" blocks memory saving](https://github.com/github/copilot-cli/issues/4005) · **OPEN** · 3 comments
*[area:enterprise, area:context-memory]*
Enterprise users can't save memories despite everything else working. The error message is misleading and provides no remediation path — an enterprise adoption blocker.

### [#3859 — Subconscious sidekick spawns even with memory disabled](https://github.com/github/copilot-cli/issues/3859) · **CLOSED** · 2 comments
*[area:agents, area:context-memory, area:plugins]*
The per-prompt memory "voting" agent keeps spawning even when `/memory off` and `"memory": false` are set. Settings are not honored — a trust-breaking bug for privacy-conscious users.

### [#4139 — BYO LLM models / custom model endpoints](https://github.com/github/copilot-cli/issues/4139) · **CLOSED** · 1 comment · 👍 6
*[area:models, area:configuration]*
Request to connect Copilot CLI to third-party LLMs (Google Cloud AI, Azure OpenAI, local models), similar to Claude CLI. Strong signal for provider flexibility despite closure — likely to resurface.

### [#4349 — Managed settings policy fails closed on valid enum value](https://github.com/github/copilot-cli/issues/4349) · **OPEN** · 1 comment
*[area:enterprise, area:configuration, area:mcp]*
The CLI's schema validator rejects `"enable"` for `permissions.disableBypassPermissionsMode` (only accepts `"disable"`), blocking **all local/custom MCP servers** in enterprise environments. A validation bug with broad blast radius.

### [#4361 — Plugin skill slash commands no longer work](https://github.com/github/copilot-cli/issues/4361) · **OPEN** · 1 comment
*[area:triage]*
Regression: invoking `/plugin-skill-name` now fires a doomed `session.commands.invoke` RPC instead of the previous client-side rewrite to natural language. Plugin ecosystem degradation reported today.

---

## 4. Key PR Progress

> ⚠️ **Only 2 PRs updated in the last 24 hours.** Both are listed. For broader PR context, see prior digests.

### [#4366 — Action required: Fundamental security findings resolution for copilot-cli](https://github.com/github/copilot-cli/pull/4366) · **OPEN**
Automated security remediation PR resolving "Fundamentals" findings for Vault app `copilot-cli` in `ci, production`. Requires maintainer review and replacement of `<UPDATE_ME>` placeholders — likely infrastructure/secret management hardening.

### [#4355 — Merge](https://github.com/github/copilot-cli/pull/4355) · **OPEN**
Minimal PR with no description — likely an incomplete or accidental submission. Expected to be closed without action.

---

## 5. Feature Request Trends

### 1. **Session management & continuity** (High demand, 👍 25–13)
- **Session forking** (#1697, 👍 25): Branch conversations with shared context
- **Cloud-synced sessions** (#1947, 👍 6): Cross-device continuity
- **Session deletion command** (#2019, 👍 13): Explicitly delete sessions from `~/.copilot/`
- **Remote session heartbeat/status** (#1343): Monitor active sessions from a phone

### 2. **Customization & theming** (Growing interest, 👍 23)
- **Custom shareable themes** (#1504, 👍 23): JSON-based theme files via `/theme`
- **Persistent context bar** (#2532): Always-visible token usage indicator

### 3. **Model/provider flexibility** (Steady demand, 👍 6)
- **BYO LLM models** (#4139, 👍 6): Support Google Cloud AI, Azure OpenAI, local models

### 4. **Plugin ecosystem improvements** (Repeated requests, 👍 29)
- **Auto-updating plugins** (#1709, 👍 29): Automatically sync plugins to latest versions — this was **partially delivered** in v1.0.78 for first-party plugins, but community is watching for third-party support

### 5. **Tool control & observability**
- **Sandbox config to selectively enable tools** (#4298, 👍 2): Whitelist bundled tools per-project
- **Token/context usage in ACP protocol** (#4174): Expose cost/context data in protocol messages

---

## 6. Developer Pain Points

### 🔴 **Windows / WSL2 terminal issues** (3 active issues)
- `Ctrl+H` misbehavior under WSL2 (#4328)
- Input box pre-filled with DA1 device-attributes reply under native-Windows zellij (#4267)
- Repeated crashes on Windows across versions since May 2026 (#4026)

### 🔴 **Enterprise configuration friction** (2 issues)
- Managed settings policy fails closed on valid enum values, blocking MCP servers (#4349)
- "Billing entity isn't selected" error preventing memory saving (#4005)

### 🟠 **Settings not honored / regression-prone**
- Memory disabling ignored, Subconscious sidekick still spawns (#3859)
- `view` tool regression in v1.0.72–73 (#4202)
- Plugin skill slash command regression (#4361)

### 🟠 **Plugin ecosystem maturity gaps**
- Repo-level plugin skills not invocable as slash commands (#4048)
- Manual plugin updates burdensome (addressed for first-party only in v1.0.78)

### 🟡 **Non-interactive / automation gaps**
- Token usage not exposed in ACP protocol messages (#4174)
- BYOK streaming failures with `reasoning_content` deltas (#4196)

### 🟡 **Noise & hygiene**
- Spam/invalid issues (#4367, #4368, #4369) suggest missing issue templates or moderation — a sign of the project's growth attracting low-quality submissions.

---

*Digest compiled from 43 updated issues and 2 PRs on 2026-08-05. Data source: [github/copilot-cli](https://github.com/github/copilot-cli).*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest
**2026-08-05**

---

## 1. Today's Highlights

The community is actively shaping Kimi Code CLI's long-term roadmap, with **persistent memory systems** and **remote session continuity** remaining the top two most-requested features (Issues #1283, #1282). Meanwhile, this week's activity focuses on **protocol-level enhancements** — two significant PRs are advancing ACP (Agent Client Protocol) support with permission mode switching (#2364) and model discovery (#2583), signaling a push toward making Kimi a first-class citizen in multi-model agent ecosystems. Additionally, a notable bug affecting **Thai IME input on Windows** (#2584) highlights ongoing cross-platform input handling challenges.

---

## 2. Releases

No new releases published in the last 24 hours.

---

## 3. Hot Issues

Listed below are 10 noteworthy issues currently drawing attention from the community.

| Issue | Title | Status | Comments | 👍 | Significance |
|-------|-------|--------|----------|-----|--------------|
| [#1283](https://github.com/MoonshotAI/kimi-cli/issues/1283) | **Feature Request: Memory System — Persistent context across sessions** | Open | 17 | 0 | The most requested feature. Proposes both automatic (AI-managed notes) and manual (user-defined instructions) memory for persistent context. Community discussion indicates strong desire for cross-session learning. |
| [#1282](https://github.com/MoonshotAI/kimi-cli/issues/1282) | **Feature Request: Remote Control — Continue local sessions from any device** | Open | 12 | 24 | Highly upvoted. Wants seamless workflow continuity via phone/tablet/browser access to local sessions. Builds on the existing mobile-ecosystem investment. |
| [#2584](https://github.com/MoonshotAI/kimi-cli/issues/2584) | **Bug: Thai (and other IME-based) characters duplicated when typing on Windows** | Open | 0 | 0 | New Windows-specific input bug in v0.31.1 causing IME character duplication. No workaround posted yet. Directly impacts non-English users. |
| [#2583](https://github.com/MoonshotAI/kimi-cli/issues/2583) | **feat(acp): Advertise available models and support mid-session model switching** | Open | 0 | 0 | ACP clients (e.g., Happy Coder, Zed) cannot discover or switch the underlying model mid-session. Critical for the emerging ACP ecosystem. |
| [#2538](https://github.com/MoonshotAI/kimi-cli/issues/2538) | **Feature Request: Support for git worktrees** | Open | 0 | 0 | Developers working with multiple branches concurrently need native worktree awareness and safe command execution. |
| [#2495](https://github.com/MoonshotAI/kimi-cli/issues/2495) | **Bug: Occasional crash on exit with non-zero code during cleanup** | Open | 0 | 0 | Flaky exit behavior undermines CI/CD automation reliability. |
| [#2451](https://github.com/MoonshotAI/kimi-cli/issues/2451) | **Feature Request: Custom command alias support** | Open | 0 | 0 | Users want shorter, personalized command aliases (e.g., `k` for `kimi`) to speed up daily workflows and scripting. |
| [#2398](https://github.com/MoonshotAI/kimi-cli/issues/2398) | **Feature Request: Offline mode / local document indexing** | Open | 0 | 0 | Appetite for running without connectivity; desire to index local docs and use lightweight local models for fallback. |
| [#2317](https://github.com/MoonshotAI/kimi-cli/issues/2317) | **Feature Request: Session search and replay** | Open | 0 | 0 | Users want to search past conversation sessions and replay a prior session's command sequence for reproducibility. |
| [#2203](https://github.com/MoonshotAI/kimi-cli/issues/2203) | **Feature Request: Multi-device session sync** | Open | 0 | 0 | Complements #1282; users want sessions synced across machines, not just mirrored remotely. |

---

## 4. Key PR Progress

Below is a selection of key pull requests listed in the update window.

| PR | Title | Status | Description |
|----|-------|--------|-------------|
| [#2200](https://github.com/MoonshotAI/kimi-cli/pull/2200) | **fix(shell): adapt timeouts for long commands** | Open | Automatically extends shell timeouts for slow patterns (git submodule cleanup, clone/fetch, installs, builds) while keeping normal commands at 60s default; preserves caller-supplied explicit timeouts. Still open after 3 months — community eagerly awaits merge. |
| [#2364](https://github.com/MoonshotAI/kimi-cli/pull/2364) | **feat(acp): support permission mode switching** | Open | Adds protocol-level ACP permission mode switching for Kimi sessions (advertises `default` mode). Stacks on #2363; resolves Issue #1414. Helps mobile/desktop ACP clients control permission granularity. |
| [#2585](https://github.com/MoonshotAI/kimi-cli/pull/2585) | **feat(cli): set AI_AGENT for subprocesses** | Open | Sets `AI_AGENT=kimi` in subprocess environments for both pip/uv and standalone binary entrypoints. Preserves explicit wrapper-supplied values; covers missing and blank cases. Standardizes agent detection for scripts. |
| [#2368](https://github.com/MoonshotAI/kimi-cli/pull/2368) | **feat(init): generate `kimi.code` config by default** | Open | Introduces a default config file to reduce per-user boilerplate; part of a broader onboarding polish effort. |
| [#2244](https://github.com/MoonshotAI/kimi-cli/pull/2244) | **fix(windows): resolve IME-related input handling** | Open | Attempts to address IME composition issues on Windows, closely tied to #2584. Not merged yet; likely path for a fix. |
| [#2112](https://github.com/MoonshotAI/kimi-cli/pull/2112) | **feat: render markdown tables in terminal** | Open | Improves inline markdown table rendering in TUI — a common ergonomics request for data-heavy outputs. |
| [#2028](https://github.com/MoonshotAI/kimi-cli/pull/2028) | **feat: add `--resume` flag to kimi chat** | Open | Adds `--resume` to attach to the most recent session — long-awaited session continuity improvement. |
| [#1954](https://github.com/MoonshotAI/kimi-cli/pull/1954) | **feat: llm() callability in LLM toolchain** | Open | Enables direct LLM invocation from the agentic loop. Considered core infrastructure for the "AI writes its own helpers" workflow. |
| [#1744](https://github.com/MoonshotAI/kimi-cli/pull/1744) | **refactor(acp): protocol cleanup for session lifecycle** | Open | Part of the broader ACP stabilization effort; foundational cleanup that unblocks several upstream ACP features. |
| [#1633](https://github.com/MoonshotAI/kimi-cli/pull/1633) | **feat: auto-run git status before agent execution** | Open | Nudges agents to check repo state before running commands — a safety/context-awareness improvement. |

---

## 5. Feature Request Trends

The most requested feature directions distill into a few clear clusters:

1. **Persistence & Memory (Highest demand)**
   - Persistent memory system (#1283) — auto/manual notes across sessions
   - Session search, replay, and resume (#2317, #2028)
   - Cross-device sync continuation (#1282, #2203)

2. **Agent Client Protocol (ACP) Ecosystem Expansion**
   - Mid-session model switching and discovery (#2583)
   - Permission mode switching (#2364)
   - General ACP protocol stabilization
   - Clients like Zed and mobile apps increasingly drive usage expectations

3. **Workflow Ergonomics**
   - Git worktrees support (#2538)
   - Custom command aliases (#2451)
   - Auto-run `git status` before agent actions (#1633)
   - Improved terminal output rendering (markdown tables, #2112)

4. **Config & Onboarding**
   - Default config file generation (`kimi.code`, #2368)
   - AI agent environment marker for subprocesses (#2585)
   - Simplified first-run setup

5. **Offline & Local-First**
   - Offline mode / local document indexing (#2398)
   - Local model fallback for offline scenarios

---

## 6. Developer Pain Points

Common frustrations appear consistently across issues and PRs:

- **Shell timeout failures on legitimate long-running commands** (PR #2200 has remained open since May). Developers are paying real time for timeouts in git-heavy or build-heavy flows.
- **Windows and IME input handling is a recurring fragility.** The Thai IME duplication bug (#2584) is only the latest in a series of Windows-specific input issues (#2244). The community is actively waiting for a consolidated fix.
- **ACP client discoverability & control gaps.** Without model listing or permission-mode switching, external agents (mobile apps, Zed) feel like second-class citizens.
- **Session continuity friction.** The inability to resume, search, or hand off sessions across devices/machines is a top complaint, especially for developers working across a laptop and a desktop.
- **No offline path.** Users without stable connectivity (or working in air-gapped environments) have no reliable fallback with local indexes or local models.
- **Absence of a standardized agent identity** for subprocesses: scripts and orchestrators cannot reliably know when they are running inside a Kimi agent loop (PR #2585 starts addressing this).

---

*Digest generated from MoonshotAI/kimi-cli GitHub activity up to 2026-08-05.*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-08-05

## Today's Highlights

OpenCode shipped two patch releases (v1.18.12, v1.18.13) addressing Azure GPT-5.5+ reasoning failures, composer lag, TUI pull-request review context, and desktop RTL support. A wave of user reports emerged overnight around DeepSeek V4 Flash "thinking forever" then returning blank responses or HTTP 500s—the highest-signal thread points to a possible model-served/wrong-model mismatch (billing/quality concern). Community PRs continue to pile up for clipboard handling, session retry logic, and provider stream robustness.

## Releases

### v1.18.13
- **TUI:** GitHub pull request reviews now include PR number and URL in context.
- **Desktop:** Fixed several right-to-left (RTL) layout issues across tabs, drawers, resizing, and titlebar interactions; also fixed shared RTL UI behaviors such as directional icons.

### v1.18.12
- **Core:** Fixed Azure GPT-5.5+ completion requests failing when reasoning is enabled. (Thanks @frederiknsgo)
- **Desktop:** Reduced composer lag when drafts include large pasted images or attachments; project search now matches any known recent project instead of only the first five.

## Hot Issues

1. **#16017 — [FEATURE]: Add Go plan usage/balance API endpoint (rolling/weekly/monthly windows)** — 29 comments, 126 👍  
   Long-requested (since March) visibility into Go subscription usage via a public API. High community demand signals billing-transparency needs.  
   [GitHub](https://github.com/anomalyco/opencode/issues/16017)

2. **#39845 — DeepSeek V4 Flash suddenly requires "Enable models hosted in China" opt-in for Go subscription** — 15 comments, 22 👍  
   Mid-session breakage; model now demands explicit opt-in due to China-hosted availability. Disruptive for existing workflows.  
   [GitHub](https://github.com/anomalyco/opencode/issues/39845)

3. **#40480 — OpenCode Go `deepseek-v4-flash` returns HTTP 500 while mimo-v2.5 works** — 8 comments, 3 👍  
   Direct API requests return HTTP 500; same key/endpoint works for mimo-v2.5. Suggests a backend/route-specific issue.  
   [GitHub](https://github.com/anomalyco/opencode/issues/40480)

4. **#40409 — OpenCode Go `deepseek-v4-flash` is NOT serving DeepSeek V4 Flash 0731 (returns V3.2, knowledge cutoff 2025-05)** — 5 comments  
   Critical billing/quality mismatch: model ID serves an older model. High severity flagged by the reporter.  
   [GitHub](https://github.com/anomalyco/opencode/issues/40409)

5. **#40483 — DeepSeek v4 Flash Free (New) returns blank response in Desktop App on Windows 11** — 7 comments  
   UI shows "thinking," plays completion sound, but response area stays blank. Common across several platforms.  
   [GitHub](https://github.com/anomalyco/opencode/issues/40483)

6. **#38723 — `opencode run` intermittently hangs during init — no session, no output, no error (~56% failure rate)** — 4 comments, 1 👍  
   Intermittent init hang with zero stdout; only external timeout helps. Unclear root cause; concerning for CI usage.  
   [GitHub](https://github.com/anomalyco/opencode/issues/38723)

7. **#40171 — Go service `/v1/responses` returns HTTP 200 but emits incomplete SSE event stream (Codex-style clients break)** — 3 comments, 2 👍  
   Missing `response.output_item.added`/`response.content_part.added` events breaks OpenAI Responses-API streaming clients.  
   [GitHub](https://github.com/anomalyco/opencode/issues/40171)

8. **#40516 — Desktop app provider/model/MCP fail to load on startup (~80% of starts)** — 2 comments  
   Regression from v1.18.5 onward; v1.18.4 works. Affects multiple users in an organization; severe for adoption.  
   [GitHub](https://github.com/anomalyco/opencode/issues/40516)

9. **#36646 — Copy-paste doesn't work properly (Tmux + Kitty Linux)** — 4 comments  
   Long-standing copy-on-select issue in TUI; community workarounds exist but no fix yet.  
   [GitHub](https://github.com/anomalyco/opencode/issues/36646)

10. **#40502 — Web interface does not auto-refresh conversations in real-time** — 3 comments  
   Manual refresh required to see new messages; expected real-time behavior for web client.  
    [GitHub](https://github.com/anomalyco/opencode/issues/40502)

## Key PR Progress

1. **#30472 — fix(tui): support copying over ssh with `set-clipboard on` tmux config** — Open  
   Closes multiple clipboard-related issues (incl. #36646). Adds tmux clipboard support over SSH—highly awaited by TUI users.  
   [GitHub](https://github.com/anomalyco/opencode/pull/30472)

2. **#40531 — [contributor] fix(opencode): retry empty unknown responses** — Open  
   Detects provider attempts that finish with unknown reason and no output; routes through retry policy. Directly addresses the "blank response" plague.  
   [GitHub](https://github.com/anomalyco/opencode/pull/40531)

3. **#15771 — feat(tui): add configurable paste summary thresholds** — Open  
   Adds `paste_min_lines`/`paste_min_length` to control when pasted content is summarized. Useful for large pastes.  
   [GitHub](https://github.com/anomalyco/opencode/pull/15771)

4. **#35289 — fix(tui): flush OSC 52 clipboard write, propagate errors on fallback** — Closed  
   Fixes clipboard paste returning old content on Linux Wayland; also propagates errors instead of silent toast.  
   [GitHub](https://github.com/anomalyco/opencode/pull/35289)

5. **#35284 — fix(llm): accept `reasoning` field in OpenAI-compatible streams** — Closed  
   Enables reasoning content in streaming deltas; relevant to DeepSeek/other reasoning models.  
   [GitHub](https://github.com/anomalyco/opencode/pull/35284)

6. **#35245 — fix(shell): bound bash-tool hangs via scope teardown instead of multiple timeouts** — Closed  
   Fixes indefinite hangs when subprocess forks grandchildren that inherit stdio.  
   [GitHub](https://github.com/anomalyco/opencode/pull/35245)

7. **#35210 — fix(session): move datetime from env block to user message** — Closed  
   Avoids re-sending static env block with dynamic date; reduces token waste and session churn.  
   [GitHub](https://github.com/anomalyco/opencode/pull/35210)

8. **#35268 — fix(opencode): settle pending tool errors** — Closed  
   Preserves actual tool failures instead of cleanup abort markers; adds regression coverage.  
   [GitHub](https://github.com/anomalyco/opencode/pull/35268)

9. **#35259 — feat(desktop): add close-to-tray behavior** — Closed  
   Hides last window to tray/Dock instead of quitting; keeps background work running.  
   [GitHub](https://github.com/anomalyco/opencode/pull/35259)

10. **#39425 — fix(acp): respect provider currency in usage_update instead of hardcoding USD** — Open  
    Fixes billing events showing wrong currency for non-USD providers.  
    [GitHub](https://github.com/anomalyco/opencode/pull/39425)

## Feature Request Trends

- **Billing transparency:** Strong demand for Go plan usage/balance API endpoints (weekly/monthly windows).
- **UI flexibility:** Requests for movable/dockable panels and RTL layout adjustments (e.g., chat position control).
- **Provider simplification:** Users want easier provider switching and setup (e.g., OmniRoute integration).
- **Flatpak integration:** Proper auto-updater behavior and portal-based updates for Flatpak users.
- **Safety/confirmation prompts:** Configurable confirmation before exit (Ctrl+D on macOS).

## Developer Pain Points

- **DeepSeek V4 Flash instability:** Multiple reports of "thinking forever," blank responses, HTTP 500s, and model-serving mismatches; likely a backend issue but compounding trust.
- **Session init hangs:** `opencode run` intermittently hangs with no diagnostics—critical for automation/CI.
- **Desktop regression on provider load:** v1.18.5+ breaks startup provider/model/MCP loading for some users.
- **Clipboard inconsistency:** Still unresolved for Tmux/Kitty/WSL despite multiple fixes and workarounds.
- **Web real-time updates:** Lack of auto-refresh for conversations is a UX gap for web users.

---
*Generated from public GitHub data; links provided for each item.*

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-08-05

## Today's Highlights

The Pi ecosystem is seeing a flurry of activity around **compaction reliability for enterprise Copilot seats** — at least three separate issues ( #6768, #7413, #7579) report failures on Copilot Enterprise/GHE.com, which is emerging as a critical pain point. Meanwhile, **Windows support** has moved to the forefront with a dedicated tracking issue (#7547), and the **PR pipeline is dominated by infrastructure work**: SQLite rework for lanes (#7591), server session backends (#7396), and RPC enhancements (#7599, #7621) signal a major architectural push under the hood.

## Releases

No new releases in the last 24 hours.

## Hot Issues

1. **[#6768 — Compaction using Copilot Enterprise not possible](https://github.com/earendil-works/pi/issues/6768)** (19 comments, 18 👍 — CLOSED)
   Enterprise users hit `421 Misdirected Request` when compacting context with Copilot Enterprise, for both OpenAI and Anthropic models. High reactivity signals this affects many paying users.

2. **[#7547 — How do you use Pi on Windows? What issues are you seeing?](https://github.com/earendil-works/pi/issues/7547)** (11 comments — OPEN)
   A community-wide call to action for Windows feedback. The maintainers acknowledge too many usage paths exist and want to know where to focus energy — bugs, docs, or out-of-box experience.

3. **[#5023 — Terminal scrolls to beginning without reason](https://github.com/earendil-works/pi/issues/5023)** (11 comments — CLOSED)
   Spontaneous terminal jumps during model output. Disruptive for users monitoring long generations; appears to be a TUI rendering race condition.

4. **[#7161 — anthropic-messages never sends x-client-request-id](https://github.com/earendil-works/pi/issues/7161)** (10 comments — CLOSED)
   Proxy users with multiple Claude accounts can't maintain session affinity because the Anthropic path omits the request ID header that OpenAI paths include. Gateway operators will feel this.

5. **[#7465 — Add payload size to iTerm2 inline images](https://github.com/earendil-works/pi/issues/7465)** (7 comments — OPEN)
   `@xterm/addon-image@0.9.0` requires a `size` param; missing it silently rejects images. Breaks Pi image rendering in xterm.js terminals (VS Code, Hyper, etc.).

6. **[#7413 — Compaction fails on GHE.com — "unknown stamp" error](https://github.com/earendil-works/pi/issues/7413)** (6 comments — OPEN)
   A distinct compaction failure mode for GHE.com enterprise accounts: `400 invalid token: unknown stamp "prod-cus-01"`. Normal chat works — only compaction breaks.

7. **[#7244 — Enhance `version` to show runtime (bun|node|deno)](https://github.com/earendil-works/pi/issues/7244)** (6 comments — OPEN)
   A quality-of-life improvement: many bug reports lack runtime info. Adding it to `pi --version` will dramatically improve triage accuracy.

8. **[#7553 — Configurable thinking level/model for compaction](https://github.com/earendil-works/pi/issues/7553)** (6 comments — OPEN)
   Compaction unconditionally reuses the session's thinking level. For reasoning models with high thinking budgets, this silently doubles or triples compaction costs.

9. **[#7128 — New PI_* guideline over-encourages unnecessary bash calls](https://github.com/earendil-works/pi/issues/7128)** (6 comments — CLOSED)
   A system prompt guideline — "Inspect PI_* environment variables" — biases agents toward unnecessary `env` inspection commands, wasting tokens and time.

10. **[#6817 — `find` returns no results for path patterns on Windows](https://github.com/earendil-works/pi/issues/6817)** (5 comments — OPEN)
   `src/**/*.ts` patterns fail on Windows while `*.ts` works. The bug is located in `packages/coding-agent/src/core/tools/find.ts` — likely a path-separator issue.

## Key PR Progress

1. **[#7624 — Render Mermaid diagrams](https://github.com/earendil-works/pi/pull/7624)** — OPEN
   Adds Mermaid diagram rendering in markdown output using `grok-mermaid`. Closes #7623.

2. **[#7602 — Configurable summarization models](https://github.com/earendil-works/pi/pull/7602)** — OPEN
   Directly addresses #7553: configurable models and thinking levels for compaction. Includes handling for provider context-window limits during compaction.

3. **[#7612 — Add size param to iTerm2 image encoder](https://github.com/earendil-works/pi/pull/7612)** — OPEN
   Fixes #7465 by including the decoded byte count in OSC 1337 sequences, unblocking xterm.js image rendering.

4. **[#7396 — Server session backend](https://github.com/earendil-works/pi/pull/7396)** — CLOSED
   Durable JSONL-based server sessions with cross-process locking and crash recovery. A foundational piece for PiServer reliability.

5. **[#7591 — SQLite update for lanes](https://github.com/earendil-works/pi/pull/7591)** — CLOSED
   Lane-aware SQLite storage: lane moves, global facts, branch-cache support, split by table. Infrastructure for the v2 harness.

6. **[#7599 — RPC over sockets](https://github.com/earendil-works/pi/pull/7599)** — CLOSED
   First-time contributor adds `--listen` for RPC over Unix sockets or TCP plus a `connectAddress` option on `RpcClient`. Expands Pi's embedded integration surface.

7. **[#7621 — Expose argument completions via RPC](https://github.com/earendil-works/pi/pull/7621)** — CLOSED
   New `get_argument_completions` RPC command so web/embedded UIs can surface slash-command subcommand completions.

8. **[#7619 — Resume failed turn by selecting it in /tree](https://github.com/earendil-works/pi/pull/7619)** — OPEN
   Selecting an error-state assistant turn now retries it instead of leaving the user at a dead end. Closes #7609.

9. **[#7605 — Keep response bodies out of OAuth error messages](https://github.com/earendil-works/pi/pull/7605)** — CLOSED
   Security fix: token-endpoint response bodies (which can echo credentials) were leaking into logs and user-facing dialogs.

10. **[#7604 — Keep $defs in non-strict Anthropic tool schemas](https://github.com/earendil-works/pi/pull/7604)** — CLOSED
   Fixes dangling `$ref` pointers in Anthropic tool schemas — any zod-derived schema with shared shapes was silently broken.

## Feature Request Trends

- **Compaction configurability** (via #7553, #7602): Users want per-compaction model/thinking-level control, especially for reasoning models.
- **Windows as a first-class citizen** (via #7547, #6817, #7427): A coordinated effort to consolidate Windows pain points and drive fixes.
- **RPC/embedding enablement** (via #7599, #7621, #7590): Exposing auth flows, argument completions, and socket transport — clearly aimed at web-based and IDE-embedded UIs.
- **Diagram rendering** (via #7623, #7624): Mermaid-in-markdown as a native capability, replacing external rendering tools.
- **Context window configuration** (#5064): Per-session context size selection — still open, matching Copilot CLI feature parity.

## Developer Pain Points

- **Compaction is fragile on enterprise setups**: Three separate issues (#6768, #7413, #7579) describe different Enterprise/GHE.com failure modes. This is the top reliability gap and is likely blocking rollout at larger organizations.
- **Console rendering inconsistencies**: TUI glitches — scroll jumps (#5023), oversized dialogs crashing the process (#7528), fullscreen keybinding conflicts (#7574) — continue to erode trust in the terminal UX.
- **Windows path handling**: From `find` glob failures (#6817) to the `ignore` library RangeError on recursive skills (#7427), Windows users face recurring path-separator bugs. The dedicated tracking issue (#7547) is a welcome first step.
- **Retry/error UX**: Red error lines persist even after successful retries (#7613), and stalled OAuth refreshes can freeze the session for ~5 minutes (#7508). Both make successful operations look broken.
- **Dependency health concerns**: The shrinkwrap pins for `undici@8.5.0` and `brace-expansion@5.0.7` have known vulns (#7628), and `node:sqlite` is missing from the release binary (#7594) — an inconsistency between the source build and the shipped artifact.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-08-05

## Today's Highlights

Qwen Code v0.21.5 ships with a significant macOS migration bridge, enabling Electron desktop users to transition to the new Tauri shell. The community is actively surfacing reliability concerns around cancellation semantics, with multiple bugs reported around aborted operations still mutating state. Security remains a hot topic, with PRs addressing trust-boundary holes in hook execution and new proposals for deterministic tool-execution boundaries.

## Releases

**v0.21.5** — Includes an opt-in one-time update bridge for macOS users to migrate from the Electron desktop app to the new Tauri shell ([#8392](https://github.com/QwenLM/qwen-code/pull/8392)). Also adds detailed execution-specific outcome tracking for tool calls and fixes a web-shell table dialog rendering issue.

## Hot Issues

1. [**#8102**](https://github.com/QwenLM/qwen-code/issues/8102) — **Proposal: deterministic tool-execution boundaries for a trustworthy agent runtime** *(17 comments)*. This P3 feature request proposes keeping the LLM outside the trust boundary while making the runtime capable of deterministically constraining, authorizing, observing, and evaluating model actions. The high engagement signals strong community interest in security posture.

2. [**#8519**](https://github.com/QwenLM/qwen-code/issues/8519) — **Severe screen flickering in tmux** *(11 comments)*. Users report near-constant flickering (~1-2 times per second) when running Qwen Code inside tmux on Linux. This UI bug is impacting terminal-heavy workflows.

3. [**#8051**](https://github.com/QwenLM/qwen-code/issues/8051) — **Bound multi-workspace daemon resource usage** *(9 comments)*. A tracking issue for delivering bounded resource usage in `qwen serve`. Current count-only limits don't constrain bytes held by request bodies, WebSocket buffers, and other memory consumers.

4. [**#8136**](https://github.com/QwenLM/qwen-code/issues/8136) — **Provider warning sanitizer bugs** *(6 comments)*. The sanitizer truncates messages containing ports and leaks passwords containing `@`. A security-relevant bug in credential handling within the CLI's provider status reporting.

5. [**#8356**](https://github.com/QwenLM/qwen-code/issues/8356) — **Session transcript loss after APIUserAbortError** *(5 comments)*. Subsequent turns after an abort error are not written to the local session transcript in Windows environments using OpenAI-compatible endpoints.

6. [**#8493**](https://github.com/QwenLM/qwen-code/issues/8493) — **Cancelled file tools can still mutate files** *(5 comments)*. `write_file` and `edit` can modify the filesystem even after invocation is cancelled, because asynchronous preparation work continues into the filesystem write even after the abort signal fires.

7. [**#8533**](https://github.com/QwenLM/qwen-code/issues/8533) — **Content[]/Part[] cannot safely encode per-provider reasoning-replay contracts** *(4 comments)*. A foundational architectural concern about how reasoning-replay data is structured across different providers.

8. [**#8452**](https://github.com/QwenLM/qwen-code/issues/8452) — **Microcompaction repeatedly invalidates prompt cache** *(3 comments)*. Size-triggered microcompaction rewrites already-cached conversation prefixes, defeating provider prompt caching in long active sessions.

9. [**#8538**](https://github.com/QwenLM/qwen-code/issues/8538) — **Copy-response button broken on Windows** *(3 comments)*. The copy button below assistant messages does nothing on Windows 10 desktop app v0.0.5, even after restarts and system reboots.

10. [**#8514**](https://github.com/QwenLM/qwen-code/issues/8514) — **Expose reasoning effort tiers via ACP** *(3 comments)*. Community request to expose the 5-tier reasoning effort system (`low`/`medium`/`high`/`xhigh`/`max`) as a session config option for ACP clients like JetBrains AI Assistant.

## Key PR Progress

1. [**#8396**](https://github.com/QwenLM/qwen-code/pull/8396) — **fix(hooks): close four trust-boundary holes in hook execution**. HTTP hooks no longer follow redirects, addressing URL whitelist and SSRF check bypasses. Also fixes three other related trust-boundary issues.

2. [**#8388**](https://github.com/QwenLM/qwen-code/pull/8388) — **feat(review): capture-tui — rendering claims get pixels, not prose**. Phase 2 of evidence images lets the review verifier drive code in a private tmux server and capture exact rendering for claims about terminal output.

3. [**#8496**](https://github.com/QwenLM/qwen-code/pull/8496) — **feat(web-shell): run read-only info commands immediately mid-turn**. `/stats`, `/about` and `/context` now execute during streaming instead of being silently swallowed until the turn completes.

4. [**#8482**](https://github.com/QwenLM/qwen-code/pull/8482) — **fix(core): a never-delivered MCP call is a first delivery, not a replay**. Fixes a deterministic test failure on main since the replay-safety gate merged, where reconnecting to a known-disconnected MCP server was incorrectly treated as timeout.

5. [**#8435**](https://github.com/QwenLM/qwen-code/pull/8435) — **fix(autofix): serialize scan-and-pick issue runs**. Fixes a mutual-exclusion hole where the concurrency group fell back to `github.run_id` for every run, potentially allowing parallel scan-and-pick runs.

6. [**#8320**](https://github.com/QwenLM/qwen-code/pull/8320) — **feat(workflows): add cooperative pause and resume**. Pause-aware per-run scheduler for Dynamic Workflows: stops dequeuing new dispatches, lets in-flight work converge, and holds results at a gate until resumed.

7. [**#8318**](https://github.com/QwenLM/qwen-code/pull/8318) — **feat(autofix): require isolated targeted E2E proof**. Adds fail-closed verification chain for autofix issues from post-merge E2E failures, transporting immutable failure metadata outside editable issue prose.

8. [**#8455**](https://github.com/QwenLM/qwen-code/pull/8455) — **fix(cli): echo resume command to main screen on exit**. The resume session hint was previously invisible because it was rendered on the alternate buffer, which is discarded on teardown.

9. [**#8439**](https://github.com/QwenLM/qwen-code/pull/8439) — **feat(cli): Ctrl+click hyperlinks and right-click context menu in VP mode**. Virtual Viewport mode's SGR mouse tracking had silently broken native hyperlink opening and context menus. This restores both.

10. [**#8490**](https://github.com/QwenLM/qwen-code/pull/8490) — **feat(review): test diff's reverse-dependency closure**. Addresses the wall-clock critical path (13–16 min on small PRs) by scoping tests to the reverse-dependency closure, falling back to full suite when needed.

## Feature Request Trends

1. **Deterministic execution guarantees** — Strong demand for reliable cancellation semantics, bounded resource usage, and deterministic tool-execution boundaries (#8102, #8493, #8491).

2. **ACP/IDE integration maturity** — Multiple requests for better JetBrains integration: task list rendering, reasoning effort tiers, and usage updates (#8544, #8514, #8513).

3. **Security hardening** — TRust-boundary improvements, credential sanitization fixes, SSRF protection, and local auth reuse (#8396, #8136, #8461).

4. **Performance & caching efficiency** — Fixing prompt-cache invalidation, bounding memory usage, and optimizing test execution (#8452, #8051, #8490).

5. **Extension hooks support** — Community asking for full compatibility with Claude-style extension hooks (#8539).

## Developer Pain Points

1. **Cancellation semantics are unreliable** — Multiple bugs across file tools, shell commands, and session controls where cancelled operations still mutate state or report success. This is a recurring theme damaging trust in the runtime.

2. **Memory/resource management in serve mode** — The daemon's resource limits are too coarse (count-only, host-derived memory ceilings not divided by child count), causing production issues for multi-workspace deployments.

3. **Prompt caching being defeated** — Size-triggered microcompaction and rolling-rewrite steady states are silently increasing costs by invalidating provider prompt caches.

4. **Terminal rendering issues** — Flickering in tmux, lost hyperlink/context-menu capabilities in VP mode, and invisible resume hints show UI polish gaps.

5. **ACP client experience gaps** — JetBrains users missing features that work in Claude Code/Codex: task lists, usage indicators, and reasoning effort controls.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-08-05

## 1. Today's Highlights

The DeepSeek TUI (CodeWhale) community is focused on a major build-performance overhaul, with maintainers filing a coordinated set of epics targeting the 682K-line `codewhale-tui` monolith. Three v0.9.4-track PRs (skill/MCP/memory lifecycle APIs) from Copilot remain open, and a batch of Russian-documented bugs around silent `File`-tool failures and 128K context degradation are drawing attention. No new releases in the last 24 hours — the v0.9.4 train (#5135) is still in flight.

## 2. Releases

No new releases in the last 24 hours.

## 3. Hot Issues

- **[#5244] Unknown model ids silently degrade to the 128K legacy context default — say so out loud** — Maintainer-filed follow-up to #5239. Any unrecognized model ID falls back to 128K without surfacing a hint, so 1M-window models compact early. The fix is to make fallback explicit. ([link](https://github.com/Hmbown/CodeWhale/issues/5244))

- **[#5239] The model supports 1M context, but why does the tool only trigger context compression at 128K** — `context_window_for_model` doesn't recognize the 1M-window model used by the reporter, so compression kicks in at 128K. Community: 1 comment, acknowledging the mismatch. ([link](https://github.com/Hmbown/CodeWhale/issues/5239))

- **[#5209] File (action=edit) silently accepts wrong parameter names and reports fake success** — `new_str` instead of `replace` returns "Replacement successful" but the edit is a no-op, forcing 3–5x re-edits per location. This is a high-friction tooling bug for both agents and humans. ([link](https://github.com/Hmbown/CodeWhale/issues/5209))

- **[#4978] Frequent Anthropic API error: 'type' must be in ["enabled", "disabled", "auto"]** — Using OpenModel's Anthropic-compatible provider triggers intermittent HTTP 400s. 6 comments suggest the community sees it as flaky rather than reproducibly broken. ([link](https://github.com/Hmbown/CodeWhale/issues/4978))

- **[#5241] Pricing endpoint returns 503 — all sessions show unverified_live_pricing** — After upgrading 0.8.67 → 0.9.3, cost display silently breaks across every provider; every turn is unpriced with `unverified_live_pricing`. Cost visibility regression. ([link](https://github.com/Hmbown/CodeWhale/issues/5241))

- **[#5249] Epic: v0.9.5 build-time lane — stop the monolith tax** — Maintainer epic for the 682K-line, 620-file `codewhale-tui` crate: 86% of the workspace, recompiles as one unit; 25 integration-test binaries each link the full graph. Part of a 7-issue performance sweep filed same-day. ([link](https://github.com/Hmbown/CodeWhale/issues/5249))

- **[#5243] OAuth login must adopt the token it just minted** — After a successful xAI device login, the session ends up with no working credentials; the user must re-open the provider picker and press `e` to actually use the stored token. Second-trip-to-picker UX bug at the core of onboarding. ([link](https://github.com/Hmbown/CodeWhale/issues/5243))

- **[#4991] Discussion: Compilation times and the TUI crate monolith** — Community member opens the conversation that later becomes the #5249 epic; 4 comments, all around wait times. Direct evidence of pain driving the build-performance lane. ([link](https://github.com/Hmbown/CodeWhale/issues/4991))

- **[#4955] Request: zero-sandbox / --no-sandbox mode for local dev** — The kernel-level Seatbelt sandbox breaks basic shell commands daily; the reporter exhausted all workarounds and wants a full opt-out. ([link](https://github.com/Hmbown/CodeWhale/issues/4955))

- **[#5245] build: local git commit forces a full rebuild of codewhale-tui and codewhale-cli** — Build scripts watch the git branch ref to embed a short SHA, so every commit invalidates the crate even when no source changed. Explicit admission that the cost is "wrong-way-round." ([link](https://github.com/Hmbown/CodeWhale/issues/5245))

## 4. Key PR Progress

- **[#5135] release: Codewhale v0.9.4 release train** — Main integration train, 77 commits ahead of `main`; supersedes #5044. All v0.9.4 source candidate contained. This is the gate for everything else this week. ([link](https://github.com/Hmbown/CodeWhale/pull/5135))

- **[#5242] feat(tui/subagent): resume interrupted children from checkpoint via followup** — Previously `agents/followup` on an interrupted child queued a dead-letter; now the checkpoint's `continuation_handle` actually resumes the run. Fixes a real loss-of-work issue for long tasks. ([link](https://github.com/Hmbown/CodeWhale/pull/5242))

- **[#5240] feat(tui/shell): surface real wait elapsed time in tool content** — `duration_ms` lived only in tool metadata, invisible to the model; all waits looked identical. Now the model sees actual elapsed time and can stop busy-polling short waits. ([link](https://github.com/Hmbown/CodeWhale/pull/5240))

- **[#5238] feat(mcp): MCP Registry discovery with Registry-first tool selection** — Adds `registry_sync` so the model checks a public MCP Registry for a zero-environment stdio server before reaching for `exec_shell` or manual code. ([link](https://github.com/Hmbown/CodeWhale/pull/5238))

- **[#5225] feat(acp): expose file/search/git/patch/shell tools over session/prompt** — ACP server only streamed model text; now it executes tool calls. Editors (Zed, community adapters like `acp-deepseek-adapter`) get a real editing agent, not a chat-only interface. ([link](https://github.com/Hmbown/CodeWhale/pull/5225))

- **[#5133] feat(runtime-api): expose persistent goal-loop state and completion controls** — Adds `GET/POST/DELETE /v1/threads/{id}/goal` so managed clients can read and drive goal lifecycle through the canonical boundary. ([link](https://github.com/Hmbown/CodeWhale/pull/5133))

- **[#5132] Runtime API: expose verifier receipts and evidence beyond the aggregate counter** — `verifier_failed` was the only signal; now `GET /v1/fleet/runs/{run_id}/receipts` lists durable task receipts for per-task failure analysis. ([link](https://github.com/Hmbown/CodeWhale/pull/5132))

- **[#5131] feat: Runtime API memory endpoints — bounded inspection and lifecycle controls** — New `/v1/memory` routes with `require_runtime_token` gating; managed clients can inspect memory scope/provenance and apply lifecycle controls. ([link](https://github.com/Hmbown/CodeWhale/pull/5131))

- **[#5130] feat(runtime-api): bounded MCP server configuration and lifecycle management** — Read-only MCP inventory was insufficient; now `POST/PATCH/DELETE /v1/apps/mcp/servers` allows create/update/remove without hand-editing TOML/JSON. ([link](https://github.com/Hmbown/CodeWhale/pull/5130))

- **[#5129] feat(runtime-api): add skill lifecycle endpoints** — TUI-only skill lifecycle is now HTTP-accessible: install, update, uninstall, trust, audit — all under the existing runtime token middleware. ([link](https://github.com/Hmbown/CodeWhale/pull/5129))

## 5. Feature Request Trends

Distilled from all Issues/PRs in the last 24h:

- **Build-time reduction & monolith decomposition** — the largest single theme (issues #5244–#5249, #4991, #5245–#5248). Community explicitly asking to break up the 682K-line TUI crate, decouple build-SHA stamps, split release profile from local gate, and consolidate 25 integration-test binaries.
- **Zero-sandbox / opt-out modes for local dev** (#4955) — kernel-level sandboxing repeatedly breaking shell workflows; users want full control on their own machines.
- **Context-window fidelity** (#5239, #5244) — model IDs must map to real advertised context windows; unknown IDs should not silently degrade to 128K without a visible warning.
- **Runtime API & ACP surface completion** (#5130–#5133, #5225) — managed clients (editors, fleet, web) want the same lifecycle control the TUI has: goals, memory, skills, MCP servers, and actual tool execution over the wire.
- **MCP Registry-first tool selection** (#5238) — treat the public registry as a first-class tool provider before falling back to shell or custom code.

## 6. Developer Pain Points

- **Build latency everywhere**: every edit, commit, test, and release pays the monolith tax; 25 integration-test link jobs per `cargo test`; fat LTO on pre-push builds. Direct quotes from #5245: the SHA stamp cost is "wrong-way-round."
- **Silent failure modes**: #5209's `File(action=edit)` accepting wrong parameter names and reporting fake success; #5244's silent 128K context fallback; #5241's pricing endpoint 503 with no user-facing error. Each requires 3–5x extra work to detect.
- **Post-login credential gaps**: #5243 — a successful OAuth device login that ends with no working credentials forces a second trip through the provider picker.
- **No observability into agent state**: #5240 — models couldn't distinguish a 1-second wait from a 5-minute stall, driving busy-polling and misjudged timeouts.
- **Sandbox friction on local dev**: #4955 — daily breakage of basic shell commands under the Seatbelt sandbox; the reporter "exhausted every workaround."
- **Provider compat whack-a-mole**: #4978 — Anthropic-compatible provider flakiness (`'type' must be in ["enabled","disabled","auto"]`) with no deterministic repro.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/kky-wollu/agents-radar).*
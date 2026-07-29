# AI CLI Tools Community Digest 2026-07-30

> Generated: 2026-07-29 23:01 UTC | Tools covered: 9

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

# AI CLI Tools Ecosystem: Cross-Tool Comparison Report
**Date:** 2026-07-30

---

## 1. Ecosystem Overview

The AI CLI developer tools landscape on 2026-07-30 shows a maturing ecosystem with distinct platform specializations emerging. Claude Code and OpenAI Codex dominate in community size and issue volume, while Gemini CLI and Pi demonstrate the fastest iteration velocity with daily releases. A clear convergence is forming around three core concerns: **MCP/server reliability** (across 6 of 8 tools), **Windows platform parity** (a persistent pain point for 5 tools), and **cost-aware model routing** (emerging as a premium feature request). The ecosystem is bifurcating between enterprise-oriented tools prioritizing security and observability (Qwen Code, Gemini CLI) and developer-experience-focused tools optimizing for workflow fluidity (Claude Code, Copilot CLI). Notably, OpenCode's community is the most vocal about architectural quality, while DeepSeek TUI and Kimi Code show smaller but highly engaged user bases focused on specific regional and language needs.

---

## 2. Activity Comparison

| Tool | Open Issues (24h) | Active PRs (24h) | Release Today | Community Engagement Signal |
|---|---|---|---|---|
| **Claude Code** | 10 hot issues | 4 PRs | No release | 73 👍 on top feature request; 31 comments on model switching |
| **OpenAI Codex** | 10 hot issues | 10 PRs | **v0.146.0** + v0.147.0-alpha.1 | 64 👍 on OAuth auth block; 45 👍 on per-project config |
| **Gemini CLI** | 10 hot issues | 10 PRs | **v0.55.0-nightly** | 8 👍 on agent hangs; 12 comments on false GOAL success |
| **Copilot CLI** | 10 hot issues | 1 PR | **v1.0.76-4, v1.0.76-5** | 36 👍 on git worktree management; 2 crash reports in 24h |
| **Kimi Code** | 10 hot issues | 10 PRs | No release | 7 👍 on `--dry-run` proposal; 6 👍 on model auto-complete |
| **OpenCode** | 10 hot issues | 10 PRs | No release | **120 👍** on `/goal` sessions; 115 👍 on clickable links |
| **Pi** | 10 hot issues | 23 PRs (high outlier) | **v0.83.0** | Multiple closed provider-compatibility fixes |
| **Qwen Code** | 10 hot issues | 10 PRs | **v0.21.0-nightly** | 5 comments on Anthropic 4.6+ 400 errors |
| **DeepSeek TUI** | 10 hot issues | 10 PRs | No release (v0.9.2 finalizing) | 13 comments on permission rules; localization focus |

**Key observations:**
- **Pi** leads PR throughput (23 PRs in 24h), driven by provider compatibility patches and TUI polish
- **OpenCode** has the highest-voted feature request (120 👍 for `/goal`) despite no release today
- **Copilot CLI** shipped two pre-release builds with sandbox fixes and plugin controls
- **Qwen Code** shows CI instability with multiple E2E failures tagged `autofix/in-progress`

---

## 3. Shared Feature Directions

| Feature / Pain Point | Tools Affected | Specific Need |
|---|---|---|
| **MCP process lifecycle management** | Claude Code, Codex, Kimi Code, Pi | Orphaned grandchildren (Claude #76306), pipe fd leaks (Codex #26984), token rotation (Kimi #2549), parallel tool batch orphans (Pi #7053) |
| **Windows platform parity** | Claude Code, Codex, Copilot CLI, Kimi Code, Qwen Code | ENAMETOOLONG paths (Claude #72725), high CPU polling (Codex #25453), blank TUI (Copilot #4159), init failures (Kimi #2545), scroll/crash regressions (Qwen #7964, #8036, #7972) |
| **Cost-aware model routing** | Claude Code, Codex, Gemini CLI, Qwen Code | Auto-switch to cheaper models (Claude #15721), context-threshold warnings (Codex #32486), role-based model binding (Qwen #8021) |
| **Session/goal persistence** | OpenCode, Qwen Code, Gemini CLI | `/goal` lifecycle (OpenCode #27167), Goal v3 runtime (Qwen #8005), auto-memory retry loops (Gemini #26522) |
| **Tool safety & previews** | Kimi Code, OpenCode, Copilot CLI | `--dry-run` mode (Kimi #2557, OpenCode #39578), destructive action prevention (Gemini #22672), sandbox enforcement (Copilot v1.0.76-4) |
| **Security hardening** | Claude Code, Gemini CLI, Copilot CLI | MCP token leakage (Claude #82358), SSRF in web-fetch (Gemini #28557), false-positive blocks (Copilot #32597) |
| **Permission system maturity** | DeepSeek TUI, OpenCode, Kimi Code | Typed persistent rules (DeepSeek #1186), mutation previews (OpenCode #39578), approval notifications (Kimi #2284) |
| **Localization / i18n** | Qwen Code, DeepSeek TUI, Claude Code | CJK token estimation bugs (Qwen #7961), Korean text corruption (Claude #80415), Indonesian localization (DeepSeek #4789) |

---

## 4. Differentiation Analysis

| Dimension | Claude Code | Codex | Gemini CLI | Copilot CLI | Kimi Code | OpenCode | Pi | Qwen Code | DeepSeek TUI |
|---|---|---|---|---|---|---|---|---|---|
| **Primary focus** | Multi-workspace MCP; cost optimization | Plugin marketplace; session management | Agent orchestration; PR auto-generation | Sandbox enforcement; plugin enable/disable | Enterprise K3 gateway; safety | Session memory; provider compatibility | Provider correctness; TUI polish | GitHub integration; autofix SME | Localization; permissions |
| **Target user** | Consultants, multi-org | Pro/Business power users | Enterprise CI/CD | CI-first developers | Chinese enterprises | Long-running agent users | Multi-provider power users | Self-hosted / China region | Non-English markets |
| **Technical strength** | MCP connector ecosystem | Rust performance; model interoperability | Agent state machines; security | Sandbox isolation; git integration | Python async; hook system | SQLite event store; domain model | Terminal compatibility; provider mapping | Server-side autofix; multi-agent | Keyboard/layout handling |
| **Weakest area** | Windows path handling | MCP resource leaks | False success reporting | Log level crashes | Output truncation | SQLite DB bloat | Parallel tool call orphan | CI flakiness | Filesystem sync ops |
| **Release cadence** | No daily releases; stable | Daily alpha + stable | Daily nightly | Pre-release builds | No daily releases | No daily releases | Daily stable | Daily nightly | Pre-release finalizing |

---

## 5. Community Momentum & Maturity

**High momentum, rapidly iterating:**
- **Pi** — 23 PRs in 24h, daily releases, strong provider compatibility fixes. Community is engaged but relatively small compared to Claude/Codex. Most agile on pure feature delivery.
- **OpenAI Codex** — Dual-track releases (stable + alpha), 10 hot issues with high engagement, active marketplace expansion. Most mature release management.
- **Gemini CLI** — Active nightly builds, 10 PRs/day, strong focus on agent reliability despite high bug count. Enterprise infrastructure investment (PR generator pipeline).

**Large community, moderate iteration pace:**
- **Claude Code** — Highest upvote counts (73, 60), but zero releases today. Community drives feature conversations more than code contributions. Stability-focused waiting pattern.
- **OpenCode** — Most vocal community (120 👍 profile), but no releases. Architectural debates (SQLite DB bloat, domain events) suggest power users who care about internals.

**Smaller but dedicated communities:**
- **Kimi Code** — 10 PRs/day, focused on safety and enterprise needs (custom API gateway). Smaller issue counts but high quality.
- **DeepSeek TUI** — Finalizing v0.9.2 with strong localization and permission system contributions. Community debates translation terminology seriously.
- **Copilot CLI** — Shipping pre-releases, but community is frustrated (two crash reports in 24h). Zombie process and log level regression signal reliability concerns.

---

## 6. Trend Signals

1. **MCP reliability is the #1 platform concern** — Across 6 tools, orphaned processes, pipe leaks, and token leakage dominate. The ecosystem is moving from "MCP works in demo" to "MCP works in production," and the gaps are showing. **Recommendation:** Invest in process group management, credential isolation, and timeout handling.

2. **Windows remains a second-class platform** — 5 tools show Windows-specific regressions in this digest alone. Path handling, keyboard layout conflicts (ABNT2), and TUI rendering bugs are systemic. **Recommendation:** Establish a cross-tool Windows compatibility working group; share patterns for path normalization and terminal detection.

3. **Cost-aware model routing is becoming table stakes** — Claude Code (#15721), Codex (#32486), and Qwen Code (#8021) all address automatic model switching for cost optimization. This will differentiate "prosumer" from "enterprise" tiers. **Recommendation:** Implement as a configurable plugin rather than hardcoded logic to allow community customization.

4. **Session/goal persistence is the next frontier** — OpenCode's 120-upvote `/goal` request and Qwen's Goal v3 runtime signal that users want agent memory that persists across restarts. Gemini's auto-memory retry bugs show the difficulty of getting this right. **Recommendation:** Use event-sourcing patterns (SQLite FTS5 in Pi, OpenCode's domain events) rather than naive state serialization.

5. **Headless / CI integration is emerging** — Qwen Code's `review run` PR (#7983) and Kimi's `--format json` (#2564) target CI pipelines. Pi's credential export (`pi auth print-api-key`) enables external client reuse. **Recommendation:** Standardize around machine-readable output formats (JSONL, exit codes) and credential export APIs.

6. **Security hardening is accelerating** — SSRF fixes (Gemini #28557), MCP token leakage prevention (Claude #82358), false-positive security blocks (Copilot #32597), and secret redaction (OpenCode #39512, Gemini #26525) show security is moving from nice-to-have to must-have. **Recommendation:** Implement prompt-injection-resistant permission systems and deterministic secret redaction before LLM transmission.

7. **Terminal compatibility fragmentation** — Kitty double-backspace (Pi #7130), Wayland clipboard (Pi #7261), tmux sixel (Pi #7245), and tmux color issues (Copilot #4292) show the diversity of terminal environments. **Recommendation:** Adopt terminal capability detection (TERMINFO, OSC sequences) rather than hardcoded terminal-specific workarounds.

---

*Report compiled from community digest summaries of 9 AI CLI tools for 2026-07-30. Data reflects public GitHub activity and may not capture private/internal development.*

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data as of 2026-07-30 | Source: github.com/anthropics/skills**

---

## 1. Top Skills Ranking

The following PRs have generated the most community discussion and attention:

### #1298 — Fix: `run_eval.py` Reports 0% Recall (Skill-Creator)
**Functionality:** Addresses a critical bug where the skill-description optimization loop (`run_eval.py`, `run_loop.py`, `improve_description.py`) always reports `recall=0%` for every skill description, effectively optimizing against noise. Fixes include installing the eval artifact as a real skill, Windows stream reading, trigger detection, and parallel worker fixes.
**Discussion Highlights:** References issue #556 with 10+ independent reproductions; blockers affect the entire skill-creator pipeline.
**Status:** OPEN | [GitHub](https://github.com/anthropics/skills/pull/1298)

### #514 — Add `document-typography` Skill
**Functionality:** Prevents orphan word wrap, widow paragraphs, and numbering misalignment in AI-generated documents. Targets common typographic defects users rarely request explicitly.
**Discussion Highlights:** Addresses a universal pain point — all Claude-generated documents suffer these issues. Practical, low-effort fix.
**Status:** OPEN | [GitHub](https://github.com/anthropics/skills/pull/514)

### #538 — Fix: Case-Sensitive File References in PDF Skill
**Functionality:** Corrects 8 case-sensitivity mismatches in `skills/pdf/SKILL.md` between `REFERENCE.md`/`reference.md` and `FORMS.md`/`forms.md`. Breaks on case-sensitive filesystems (Linux).
**Discussion Highlights:** Simple but essential compatibility fix; highlights cross-platform testing gaps.
**Status:** OPEN | [GitHub](https://github.com/anthropics/skills/pull/538)

### #486 — Add ODT Skill (OpenDocument Format)
**Functionality:** Creates, fills, reads, and converts `.odt`/`.ods` files. Supports template filling and ODT-to-HTML conversion. Triggers on mentions of ODF, LibreOffice, or OpenDocument.
**Discussion Highlights:** Addresses demand for open-source document format support; complements existing DOCX/PDF skills.
**Status:** OPEN | [GitHub](https://github.com/anthropics/skills/pull/486)

### #210 — Improve `frontend-design` Skill Clarity
**Functionality:** Revises the frontend-design skill for clarity, actionability, and internal coherence. Ensures every instruction is executable within a single conversation.
**Discussion Highlights:** Focus on making skills genuinely actionable rather than educational; reflects broader community interest in skill quality.
**Status:** OPEN | [GitHub](https://github.com/anthropics/skills/pull/210)

### #1367 — Add `self-audit` Skill (v1.3.0)
**Functionality:** A universal skill that audits AI output before delivery — mechanical file verification followed by a four-dimension reasoning audit in damage-severity priority order. Works with any project, tech stack, or model.
**Discussion Highlights:** Novel "meta-skill" approach; addresses output quality assurance in agentic workflows.
**Status:** OPEN | [GitHub](https://github.com/anthropics/skills/pull/1367)

---

## 2. Community Demand Trends

From the most-discussed Issues, the community's top anticipated skill directions are:

| Demand Area | Key Issues | Signal Strength |
|---|---|---|
| **Skill-Creator Reliability** — Fixing `run_eval.py` 0% recall, Windows compatibility, trigger detection | #556 (12 comments), #1169 (3), #1061 (3), #202 (8) | **Highest** — 4+ separate issues, multiple PRs |
| **Namespace & Trust Security** — Preventing impersonation of official Anthropic skills | #492 (43 comments, 2 👍) | **Critical** — most-commented issue in repo |
| **Org-Wide Skill Sharing** — Sharing skills within teams without manual file transfer | #228 (16 comments, 8 👍) | **High demand** — top upvoted feature request |
| **Document Quality Tooling** — Typography, format support (ODT, PDF fixes) | #514, #486, #538 | **Steady** — practical, cross-format demand |
| **Agent Governance & Safety** — Policy enforcement, threat detection, audit trails | #412 (6 comments) | **Emerging** — early but structured proposal |
| **Context Window Management** — Preventing skill inflation and token exhaustion | #1487 (4 comments), #1175 (4) | **Growing concern** — large skills break workflows |
| **MCP/Skill Convergence** — Exposing skills as MCP interfaces for API interoperability | #16 (4 comments) | **Strategic** — long-term ecosystem evolution |

**Key insight:** The community's #1 pain point is not missing skill functionality — it's that the **skill-creator tooling itself is broken** (0% recall on Windows, unreliable trigger detection). This blocks the entire skill development pipeline.

---

## 3. High-Potential Pending Skills

These PRs have active discussion and may land soon:

| PR | Skill | Status | Why It's High-Potential |
|---|---|---|---|
| [#1367](https://github.com/anthropics/skills/pull/1367) | `self-audit` — output quality gate (v1.3.0) | OPEN (updated 2026-07-02) | Novel meta-skill addressing quality assurance; author has follow-up proposal (#1385) |
| [#1302](https://github.com/anthropics/skills/pull/1302) | `color-expert` — color naming systems, spaces, accessibility | OPEN (updated 2026-07-21) | Niche but deep domain expertise; comprehensive coverage |
| [#1479](https://github.com/anthropics/skills/pull/1479) | `plan-file-hygiene` — lifecycle management for planning artifacts | OPEN (updated 2026-07-27) | Addresses #1417 — planning artifacts accumulate with no lifecycle; credited to community suggestions |
| [#723](https://github.com/anthropics/skills/pull/723) | `testing-patterns` — full testing stack (unit, React, E2E) | OPEN (updated 2026-04-21) | Broad demand; covers Testing Trophy model, AAA pattern, edge cases |
| [#525](https://github.com/anthropics/skills/pull/525) | `pyxel` — retro game development with Pyxel MCP server | OPEN (updated 2026-07-15) | From Pyxel engine author; niche but established ecosystem |
| [#83](https://github.com/anthropics/skills/pull/83) | `skill-quality-analyzer` + `skill-security-analyzer` (meta-skills) | OPEN (updated 2026-01-07) | Self-improvement meta-skills; evaluates across 5 dimensions |
| [#181](https://github.com/anthropics/skills/pull/181) | `SAP-RPT-1-OSS` — SAP tabular foundation model predictor | OPEN (updated 2026-03-16) | Enterprise data science use case; Apache 2.0 licensed model |

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for reliability infrastructure:** fixing the skill-creator's broken evaluation pipeline (recall=0%, Windows incompatibility) and establishing security boundaries (namespace trust) before expanding the skills library — a "make the tools work first, then build the catalog" priority.

---

**Claude Code Community Digest – 2026-07-30**

---

## Today's Highlights

The community is driving two major feature conversations: automatic model switching for plan/cost optimization and multi-workspace Slack MCP support, each with over 30 comments and strong upvotes. On the stability front, recent PRs tackle critical Windows and macOS bootstrap issues in gateway setup scripts, while a new security-focused "MCP Guard" plugin proposal has appeared. No new releases shipped in the last 24 hours.

---

## Releases

No new releases in the last 24 hours.

---

## Hot Issues (10 most noteworthy)

1. **#44243 – Multiple Slack workspaces in the built-in Slack connector**  
   The top-voted open feature request (73 👍), asking for multi-workspace support in the built-in Slack MCP connector. Currently, users are locked to one workspace per account, which breaks workflows for consultants and multi-org professionals.  
   [View Issue](https://github.com/anthropics/claude-code/issues/44243)

2. **#15721 – Automatic Model Switching for Plan Mode**  
   60 upvotes, 31 comments. Users want Claude Code to automatically downgrade to a cheaper model (e.g., Haiku) during planning/thinking phases, then switch to a more capable model for execution. Cost-conscious teams see this as a high-value optimization.  
   [View Issue](https://github.com/anthropics/claude-code/issues/15721)

3. **#72725 – Spawn ENAMETOOLONG on Windows desktop**  
   A blocking bug on Windows where long file paths cause `spawn ENAMETOOLONG` errors. The issue works fine on Mac, pointing to a Windows-specific path handling gap. Open and unresolved.  
   [View Issue](https://github.com/anthropics/claude-code/issues/72725)

4. **#80415 – Korean text garbled in AskUserQuestion/TodoWrite UI (VS Code)**  
   A Unicode rendering bug affecting Korean (Hangul) input in VS Code extension cards. This is an active, open issue with 4 comments, suggesting it's a reproducible i18n defect.  
   [View Issue](https://github.com/anthropics/claude-code/issues/80415)

5. **#81706 – Plugin scope conflict: user + project enables break install records**  
   When a plugin is enabled at both user and project scope, Claude Code writes only a project-scoped install record, breaking the plugin in other projects. A nuanced configuration bug with a clear repro.  
   [View Issue](https://github.com/anthropics/claude-code/issues/81706)

6. **#68129 – "Fable is not available" error**  
   A now-closed bug with 22 comments — high engagement suggests this caused significant confusion among users trying to access the Fable model. Labeled `stale` after resolution.  
   [View Issue](https://github.com/anthropics/claude-code/issues/68129)

7. **#76306 – Orphaned MCP server grandchildren after CLI exit**  
   Stdio MCP servers launched via `bun run` or `npx` leave orphaned process grandchildren when the CLI exits. A silent resource leak that could accumulate in long-running environments.  
   [View Issue](https://github.com/anthropics/claude-code/issues/76306)

8. **#68083 – Desktop "Auto-fix CI" toggle never applies to PRs created via `gh`**  
   The desktop global toggle for auto-fixing CI doesn't apply to PRs created from local sessions, and the setting doesn't persist in `claude_desktop_config.json`. Users want consistent CI behavior.  
   [View Issue](https://github.com/anthropics/claude-code/issues/68083)

9. **#69195 – Concurrent desktop sessions corrupt tool results**  
   Running two Claude sessions in the same Windows desktop app causes text injection, fabricated file state, and silent dropped writes. A concurrency bug in the desktop app's session isolation.  
   [View Issue](https://github.com/anthropics/claude-code/issues/69195)

10. **#69165 – Cowork VM SDK download truncated, checksum fails on macOS**  
    Cowork VM setup downloads a truncated ~4 MB SDK, causing persistent checksum verification failures on Apple Silicon. Blocks the Cowork experience entirely on affected machines.  
    [View Issue](https://github.com/anthropics/claude-code/issues/69165)

---

## Key PR Progress (4 items today)

1. **#48272 – Enrich release titles with changelog summary (CLOSED)**  
   This long-running PR to enrich release notes with changelog summaries has been upstreamed into `main` as a `feed.xml` format. A win for release transparency.  
   [View PR](https://github.com/anthropics/claude-code/pull/48272)

2. **#82358 – MCP Guard plugin: security hardening for MCP configurations (OPEN)**  
   A new plugin proposal addressing the risk of MCP configurations leaking bearer tokens into terminal output. Proactive security hardening for the MCP plugin ecosystem.  
   [View PR](https://github.com/anthropics/claude-code/pull/82358)

3. **#82335 – Fix GCP gateway `setup.sh` exiting silently when `gcloud` is missing (OPEN)**  
   Under `set -euo pipefail`, a missing `gcloud` command causes `setup.sh` to exit with code 127 silently. This PR adds proper error handling to prevent silent failures.  
   [View PR](https://github.com/anthropics/claude-code/pull/82335)

4. **#82320 – Fix AWS gateway `setup.sh` aborting on macOS bash 3.2 (OPEN)**  
   Uses `${DIST_SHA256,,}` — a bash 4-only case-modification expansion. macOS ships bash 3.2, so the script aborts before argument checks. A straightforward portability fix.  
   [View PR](https://github.com/anthropics/claude-code/pull/82320)

---

## Feature Request Trends

- **Multi-workspace/multi-tenant MCP connectors** – The Slack workspace limitation (#44243, 73 👍) reflects a broader demand for MCP connectors that support multiple org contexts.
- **Cost-aware model switching** – Users want intelligent automatic model routing (#15721, 60 👍) to optimize for cost during planning vs. execution phases.
- **Per-model configuration persistence** – Requests for `modelEffort` maps (#67070) and per-model settings suggest users are customizing model behavior and want it to persist.
- **Live agent steering** – The ability to inject input mid-turn (#69124, 5 👍) without interrupting the agent's context mirrors Codex-style workflows.
- **Agent plan reviews** – A structured review workflow (#69191) for multi-agent sessions, indicating growing interest in auditability of autonomous agent actions.
- **AGENTS.md and repository-aware tool selection** – Users want a declarative agent configuration file (#69151) to guide tool selection per repository.

---

## Developer Pain Points

- **Windows path length and spawning** – `ENAMETOOLONG` errors (#72725) and concurrent session corruption (#69195) continue to plague Windows users, suggesting deeper platform compatibility issues.
- **MCP process lifecycle management** – Orphaned grandchildren (#76306) and token leakage (#82358) point to incomplete process group and secret management in MCP server spawning.
- **Plugin configuration scoping** – Broken plugin records (#81706) and stale Cowork marketplaces (#67666) indicate the plugin integrity system needs better state reconciliation.
- **Cowork/VM reliability** – SDK download failures (#69165) and 2GB memory leaks per subagent (#64751) suggest the Cowork infrastructure is still maturing for production use.
- **CI monitoring inconsistency** – The "Auto-fix CI" toggle not applying consistently (#68083) and concurrent session CI subscription leaks (#69161) erode trust in automated CI workflows.
- **Unicode/i18n rendering** – Korean text corruption (#80415) points to gaps in the VS Code extension's text rendering pipeline for non-ASCII scripts.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# Codex Community Digest — 2026-07-30

## Today's Highlights
A packed day of infrastructure hardening: the team shipped **v0.146.0** with session management improvements and plugin marketplace expansion, while the v0.147.0 alpha cycle kicked off with `rusty-v8` upgraded to **v150.4.0**. On the bug front, the community continues to push hard on **MCP resource leaks**, **Windows performance regressions**, and **GPT-5.6 serialization inefficiencies** — three clusters that collectively account for over 60 comments today.

---

## Releases
- **[rust-v0.146.0](https://github.com/openai/codex/releases/tag/rust-v0.146.0)**: Named sessions via `/new` or `/clear`, thread pinning, side conversation switching without closing (#34605, #34840, #35011). Agent Plugin manifests, workspace plugin publishing, and new marketplaces for Amazon Bedrock and Claude C.
- **[rust-v0.147.0-alpha.1](https://github.com/openai/codex/releases/tag/rust-v0.147.0-alpha.1)**: Alpha release kicking off the 0.147 cycle.
- **[rusty-v8-v150.4.0](https://github.com/openai/codex/releases/tag/rusty-v8-v150.4.0)**: V8 bindings bump; PR [#35997](https://github.com/openai/codex/pull/35997) removes the obsolete 146.4.0 Bazel targets.

---

## Hot Issues (Top 10)

1. **[#31573](https://github.com/openai/codex/issues/31573) — OAuth authentication fails at issuer validation**  
   *29 comments, 64 👍*  
   Free-tier users hitting a hard block on `v0.143.0` — CLI auth flow rejects valid issuers. The high engagement suggests this is a widespread onboarding breakage.

2. **[#13025](https://github.com/openai/codex/issues/13025) — Desktop ignores project-level `.codex/config.toml` for MCP**  
   *20 comments, 45 👍*  
   Codex Desktop only loads `~/.codex/config.toml`, making per-project MCP server configuration (especially Serena) impossible. A long-standing pain point now 5 months old.

3. **[#25453](https://github.com/openai/codex/issues/25453) — Windows Desktop high CPU from powershell.exe polling**  
   *19 comments*  
   Process polling spawns a powershell.exe every second. Pro users on Windows seeing sustained 20%+ CPU from this alone.

4. **[#35050](https://github.com/openai/codex/issues/35050) — GPT-5.6 serializes independent Code Mode calls**  
   *16 comments, 36 👍*  
   Model serializes parallelizable tool calls; user reports **27–45% weighted usage reduction** with explicit batching. This has direct cost and latency implications for Pro/Business users.

5. **[#26984](https://github.com/openai/codex/issues/26984) — MCP stdio servers leak pipe fds + orphan children → EMFILE**  
   *16 comments*  
   Long-running sessions hit `EMFILE` (Too many open files) after repeated MCP interactions. Orphan processes compound the issue — critical for heavy MCP users.

6. **[#25779](https://github.com/openai/codex/issues/25779) — Meta-bug: unbounded session state causes freezes and context bloat**  
   *11 comments*  
   Session/turn state grows unbounded, causing UI freezes and lost active-turn control. Touchpoint for multiple downstream bugs.

7. **[#32486](https://github.com/openai/codex/issues/32486) — Default GPT-5.6 context can cross 272K higher-usage threshold**  
   *8 comments*  
   Sessions silently enter higher pricing band without user opt-in. Community requesting guardrails or explicit warnings.

8. **[#29422](https://github.com/openai/codex/issues/29422) — Appshot fails on Intel Mac (Computer Use service missing)**  
   *7 comments*  
   x64 package ships without the Computer Use service binary; feature is visibly exposed but always fails.

9. **[#34853](https://github.com/openai/codex/issues/34853) — Spreadsheets plugin blocked on Windows CLI**  
   *7 comments*  
   `load_workspace_dependencies` inaccessible in CLI on Windows. Plugin ecosystem friction for non-macOS users.

10. **[#32597](https://github.com/openai/codex/issues/32597) — Security validation false-positive blocks personal repo**  
    *4 comments*  
    Defensive review flagging routine repositories as cybersecurity threats — trust mechanism needs calibration.

---

## Key PR Progress (Top 10)

1. **[#36039](https://github.com/openai/codex/pull/36039) — Limit MCP catalog pagination**  
   Caps discovery at 100 pages / 1,024 items per catalog — prevents runaway pagination attacks or accidental OOM.

2. **[#36037](https://github.com/openai/codex/pull/36037) — Deny network access when allow amendment fails**  
   Security hardening: failed policy amendments no longer grant implicit access.

3. **[#36036](https://github.com/openai/codex/pull/36036) — Allow naming forked chats from the TUI**  
   Adds `--name` to `/fork` — small UX win for organizing parallel explorations.

4. **[#36035](https://github.com/openai/codex/pull/36035) — Exit stdio app-server when connection closes**  
   Prevents orphaned app-server processes after remote-control disconnect.

5. **[#36001](https://github.com/openai/codex/pull/36001) — Upgrade rmcp to 3.0.0**  
   Rust MCP SDK moves from beta to stable; fallback server name handling for discovery responses without identity metadata.

6. **[#36007](https://github.com/openai/codex/pull/36007) — Persisted manual ordering for thread sections**  
   Adds `thread/section/move` API with atomic reordering — fundamental infrastructure for organizing long-running projects.

7. **[#36006](https://github.com/openai/codex/pull/36006) — Reduce response serialization and rollout scan overhead**  
   Keeps `ClientResponsePayload` typed through the outgoing queue, avoiding intermediate `serde_json::Value` — should improve app-server throughput.

8. **[#36002](https://github.com/openai/codex/pull/36002) — Resolve MCP file uploads with environment-native paths**  
   Fixes MCP tool file argument resolution when host and environment use different path conventions (e.g., WSL vs Windows).

9. **[#35990](https://github.com/openai/codex/pull/35990) — Test exec-server compatibility across Codex versions**  
   Defines `MINIMUM_SUPPORTED_CODEX_VERSION` and tests backward compatibility for executor protocol — important for staged rollouts.

10. **[#36031](https://github.com/openai/codex/pull/36031) — Load cloud-managed servers in MCP CLI commands**  
    Enterprise-managed MCP servers now resolvable via `codex mcp list/get/login/logout` — enterprise deployment enabler.

---

## Feature Request Trends

- **Configurable tab rendering in CLI TUI** (#36018, #36017): Developers want to set tab width for code readability — terminal tab-stops are ignored.
- **Keyboard shortcut to cycle permission modes** (#34073): Claude Code-style `Shift+Tab` for rapid mode switching in CLI.
- **Structured CodexErrorInfo in JSONL exec events** (#22570): Users want machine-parseable error variants (`unauthorized`, `usageLimitExceeded`, etc.) in `codex exec --json`.
- **Explicit context/pricing warnings** (#32486): Community demanding opt-in UX before crossing higher-usage context thresholds.

---

## Developer Pain Points

1. **MCP reliability on Windows**: Three major MCP issues today — EMFILE leaks (#26984), pipe/orphan accumulation, and spreadsheets plugin blocked (#34853). Windows remains the weakest platform for plugin-heavy workflows.
2. **Session state bloat**: Unbounded turn state (#25779) causes freezes, and "Context compacting" triggers even at low usage (#35978) — suggests caching heuristics need tuning.
3. **Intel Mac / x64 gaps**: Missing Computer Use service (#29422) and unaddressed performance parity issues — Apple Silicon gets first-class treatment.
4. **False-positive security blocks**: Routine Git operations (#34780) and personal repo reviews (#32597) triggering opaque blocks damages trust in the sandbox model.
5. **GPT-5.6 regression signals**: Serialization of parallel calls (#35050) and GitHub connector failures (#36042) suggest model-behavior regressions between 5.5 and 5.6 that directly impact developer productivity.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-07-30

## Today's Highlights
A new nightly release (v0.55.0-nightly) landed with early Firestore dual-locking infrastructure for the PR generator pipeline. Meanwhile, the community continues to surface critical agent reliability bugs: subagents falsely reporting `GOAL` success after hitting turn limits, and the generalist agent hanging indefinitely. A flurry of infrastructure PRs around the SSR code generation pipeline and sandbox crash fixes dominated today’s merge queue.

## Releases
- **[v0.55.0-nightly.20260729](https://github.com/google-gemini/gemini-cli/releases/tag/v0.55.0-nightly.20260729.g3499c84f7)** — Bumped from 0.54.0-nightly; includes `feat(pr-generator-db): implement Firestore concurrency dual-locking and test ingestion utilities` by @joneba-google (PR #28552). No other user-facing changes.

## Hot Issues
1. **[#22323 — Subagent recovery after MAX_TURNS is reported as GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)** (P1, Bug, 12 comments, 2 👍)  
   *Why it matters*: `codebase_investigator` reports `status: "success"` even when it hit the turn limit before doing any analysis. This masks real failures and misleads users into thinking work was completed. Community reaction is muted but the issue has been open since March — retesting is needed.

2. **[#21409 — Generalist agent hangs](https://github.com/google-gemini/gemini-cli/issues/21409)** (P1, Bug, 8 comments, 8 👍)  
   *Why it matters*: The generalist agent hangs indefinitely on simple tasks like folder creation. Workaround (instructing the model not to use subagents) defeats the purpose of the agent system. High upvote count signals a broad impact.

3. **[#19873 — Leverage model's bash affinity via Zero-Dependency OS Sandboxing](https://github.com/google-gemini/gemini-cli/issues/19873)** (P2, Enhancement, 8 comments, 1 👍)  
   *Why it matters*: Proposes embracing Gemini 3’s native bash behavior with POSIX tool chaining, but adds a sandboxing layer for security. Represents a philosophical shift — trust the model’s strengths while containing risk. Effort/large.

4. **[#25166 — Shell command execution gets stuck with "Waiting input" after command completes](https://github.com/google-gemini/gemini-cli/issues/25166)** (P1, Bug, 4 comments, 3 👍)  
   *Why it matters*: After simple CLI commands finish, the shell hangs showing "Awaiting user input". Extremely disruptive for scripting/automation workflows. Medium effort.

5. **[#26522 — Stop Auto Memory from retrying low-signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522)** (P2, Bug, 5 comments)  
   *Why it matters*: Auto Memory repeatedly re-processes low-signal sessions because they're never marked as "read". Wasteful compute and token usage. Part of a cluster of memory bugs filed by @SandyTao520.

6. **[#26525 — Add deterministic redaction and reduce Auto Memory logging](https://github.com/google-gemini/gemini-cli/issues/26525)** (P2, Security, 4 comments)  
   *Why it matters*: Auto Memory sends local transcripts to the model before redacting secrets. Content is also logged. This is a data leak risk for users with sensitive code.

7. **[#21983 — Browser subagent fails in Wayland](https://github.com/google-gemini/gemini-cli/issues/21983)** (P1, Bug, 4 comments, 1 👍)  
   *Why it matters*: Browser automation is broken on Wayland — a common Linux display server. Termination reason is misleadingly "GOAL" despite failure.

8. **[#21968 — Gemini does not use skills and sub-agents enough](https://github.com/google-gemini/gemini-cli/issues/21968)** (P2, Bug, 6 comments)  
   *Why it matters*: Even when explicit skills (gradle, git) are configured, the model ignores them. Users must manually instruct it. Undermines the entire skill/agent extensibility model.

9. **[#22672 — Agent should stop/discourage destructive behavior](https://github.com/google-gemini/gemini-cli/issues/22672)** (P2, Customer Issue, 3 comments, 1 👍)  
   *Why it matters*: The model uses `git reset`, `--force`, and destructive DB commands when safer alternatives exist. Community wants guardrails — not just warnings but active redirection.

10. **[#24246 — Gemini CLI encounters 400 error with > 128 tools](https://github.com/google-gemini/gemini-cli/issues/24246)** (P2, Bug, 3 comments)  
    *Why it matters*: Hitting a hard API limit when too many tools are enabled. Users expect smarter tool scoping rather than a crash. Need-for-information status suggests root cause is still being diagnosed.

## Key PR Progress
1. **[#28588 — feat(caretaker): publish workable spec event to ready-for-code Pub/Sub topic](https://github.com/google-gemini/gemini-cli/pull/28588)** — @chadd28 adds event publishing to trigger downstream code generation when issues are triaged. Key automation infrastructure.

2. **[#28566 — fix(core,cli): propagate InvalidStreamError details to UI](https://github.com/google-gemini/gemini-cli/pull/28566)** — @DavidAPierce surfaces specific error types (e.g., empty responses) to CLI UI with `/compress` suggestions. Directly improves user troubleshooting.

3. **[#27154 — fix(core): prevent PTY memory leak](https://github.com/google-gemini/gemini-cli/pull/27154)** (CLOSED) — @rozen03 fixes a critical file descriptor leak where PTY entries were never garbage collected. Merged today after two months open.

4. **[#28586 — fix(core): preserve thoughtSignature in functionCall parts](https://github.com/google-gemini/gemini-cli/pull/28586)** — @Tejas-Raj01 fixes a 400 error regression introduced in v0.53.0 where `thoughtSignature` was stripped during parallel tool calls.

5. **[#28557 — fix: resolve SSRF vulnerability in web-fetch.ts](https://github.com/google-gemini/gemini-cli/pull/28557)** — @deepresearcher08 uses async DNS resolution to prevent hostnames resolving to internal IPs (e.g., `169.254.169.254`). Security fix for PR #28555.

6. **[#28551 — fix(cli): fall back to embedded macOS seatbelt profiles](https://github.com/google-gemini/gemini-cli/pull/28551)** — @amelidev prevents crash on macOS/gMac when sandbox profiles are missing. Critical for sandbox mode startup.

7. **[#28431 — feat(pr-generator-infra): Cloud Run job, Workflows, and Dockerfile](https://github.com/google-gemini/gemini-cli/pull/28431)** — @joneba-google configures the SSR code generation pipeline’s container runtime. Part of a larger pipeline rollout.

8. **[#28433 — feat(pr-generator-orchestrator): iterative bug-fixing state machine](https://github.com/google-gemini/gemini-cli/pull/28433)** — @joneba-google implements the full orchestration loop: Firestore locking, AI coding/eval cycles, ESLint analysis, diff verification. Core intelligence for automated PR generation.

9. **[#25364 — fix: handle RangeError when conversation exceeds JSON serializable size](https://github.com/google-gemini/gemini-cli/pull/25364)** — @enjoykumawat catches the V8 `RangeError: Invalid string length` crash on large conversations. Fixes #24902.

10. **[#26286 — fix stale state in /rewind](https://github.com/google-gemini/gemini-cli/pull/26286)** — @joshualitt fixes a bug where `/rewind` didn't properly reset state, causing inconsistent conversation history. Fixes #25646.

## Feature Request Trends
- **AST-aware code understanding**: Multiple issues ([#22745](https://github.com/google-gemini/gemini-cli/issues/22745), [#22746](https://github.com/google-gemini/gemini-cli/issues/22746)) push for Abstract Syntax Tree awareness in file reads, search, and codebase mapping. This would reduce token waste and improve accuracy for method-level operations.
- **Agent self-awareness and transparency**: Users want agents that understand their own capabilities, flags, hotkeys, and configuration ([#21432](https://github.com/google-gemini/gemini-cli/issues/21432)). Also request visible subagent trajectories via `/chat share` ([#22598](https://github.com/google-gemini/gemini-cli/issues/22598)) and better bug reports that include subagent context ([#21763](https://github.com/google-gemini/gemini-cli/issues/21763)).
- **Destructive action prevention**: Growing demand for built-in safety rails against destructive git ops, DB writes, and force flags ([#22672](https://github.com/google-gemini/gemini-cli/issues/22672)). The community wants proactive discouragement, not just warnings.
- **Auto Memory reliability**: Three issues this week ([#26522](https://github.com/google-gemini/gemini-cli/issues/26522), [#26523](https://github.com/google-gemini/gemini-cli/issues/26523), [#26525](https://github.com/google-gemini/gemini-cli/issues/26525)) call for fixes to retry loops, patch validation, and secret redaction — all pointing to a system that’s still maturing.

## Developer Pain Points
- **False success reporting**: Subagents repeatedly report `status: "success"` / `Termination Reason: "GOAL"` despite hitting limits or failing — especially the browser agent and codebase_investigator ([#22323](https://github.com/google-gemini/gemini-cli/issues/22323), [#21983](https://github.com/google-gemini/gemini-cli/issues/21983)). This erodes trust in agent outputs.
- **Agent hangs and freezes**: The generalist agent hangs on trivial tasks ([#21409](https://github.com/google-gemini/gemini-cli/issues/21409)), shell commands get stuck post-execution ([#25166](https://github.com/google-gemini/gemini-cli/issues/25166)), and interactive prompts (e.g., vite create) freeze the agent ([#22465](https://github.com/google-gemini/gemini-cli/issues/22465)). These are the top-priority reliability blockers.
- **Tool/skill underutilization**: Despite user-configured skills and sub-agents, the model rarely invokes them autonomously ([#21968](https://github.com/google-gemini/gemini-cli/issues/21968)). Symlinks in `~/.gemini/agents/` are ignored entirely ([#20079](https://github.com/google-gemini/gemini-cli/issues/20079)). The extensibility story is broken in practice.
- **Memory and context issues**: Auto Memory re-processes low-signal sessions indefinitely ([#26522](https://github.com/google-gemini/gemini-cli/issues/26522)), large conversations crash with RangeError ([#25364](https://github.com/google-gemini/gemini-cli/pull/25364)), and the `/rewind` command leaves stale state ([#26286](https://github.com/google-gemini/gemini-cli/pull/26286)). Memory management remains the top infrastructure pain point.
- **Security gaps**: Auto Memory sends transcript content to models before redacting secrets ([#26525](https://github.com/google-gemini/gemini-cli/issues/26525)), and the web-fetch tool was vulnerable to SSRF via DNS rebinding ([#28557](https://github.com/google-gemini/gemini-cli/pull/28557)). Security-aware users are rightfully concerned.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest
**Date:** 2026-07-30

## Today’s Highlights
Two new pre-release builds dropped: v1.0.76-4 (critical Linux/macOS sandbox enforcement fix) and v1.0.76-5 (plugin enable/disable controls and Grok-4.5 support). The community is reporting a concerning regression where the CLI crashes on launch for most log levels, with two related reports filed within 24 hours. Long-standing zombie-process and terminal-rendering issues remain active and drawing attention.

## Releases
Two new versions published in the last 24 hours:
- **[v1.0.76-5](https://github.com/github/copilot-cli/releases/tag/v1.0.76-5)** – Adds enable/disable controls in `/plugins` for plugins, instructions, agents, LSP servers, and hooks. Adds support for the **Grok-4.5** model.
- **[v1.0.76-4](https://github.com/github/copilot-cli/releases/tag/v1.0.76-4)** – Fixes sandbox denied paths enforcement for relative and symlinked entries on macOS and Linux. Windows remains unable to deny per path.

## Hot Issues (10 selected)
1. **[#4297 – Copilot crashes on launch if log level is set to any value other than "all" or "default"](https://github.com/github/copilot-cli/issues/4297)** *(New, 0 comments)* – A serious regression: `copilot --log-level error` (or `info`, `warning`, `debug`, `none`) prompts a silent exit. This is a blocker for anyone needing verbosity control in CI or debugging.
2. **[#4285 – 1.0.76-1: silent exit 1 at session startup when log level is none/error/warning/info/debug](https://github.com/github/copilot-cli/issues/4285)** *(New, 👍2)* – Confirms the same crash pattern on Windows. Together with #4297, this is clearly a widespread regression introduced in the 1.0.76 series.
3. **[#4163 / #4290 – Zombie child processes accumulate under copilot PID on Linux](https://github.com/github/copilot-cli/issues/4163)** *(Closed, but reopened by #4290)* – #4163 was just closed but user reports it’s not fixed on AlmaLinux 8.10. Expect re-examination. 3 👍 on the original, heavy interest.
4. **[#1613 – Feature request: Built-in git worktree lifecycle management](https://github.com/github/copilot-cli/issues/1613)** *(Open since Feb, 👍36)* – The most-voted open feature request. Users want automated creation/destruction of git worktrees per task, enabling safe parallel work.
5. **[#4202 – Built-in view reports "Path does not exist" for existing files in 1.0.73+](https://github.com/github/copilot-cli/issues/4202)** *(Open, 3 comments)* – A regression starting in 1.0.72 that breaks the `view` tool on valid files. High impact for file-reading workflows.
6. **[#4159 – Interactive mode goes blank after submitting prompt in Windows Terminal](https://github.com/github/copilot-cli/issues/4159)** *(Open, 👍3)* – UI goes completely blank after a prompt; non-interactive `-p` mode works fine. Terminal rendering issue affects all Windows users.
7. **[#1168 – Excessive authorization prompts during a single request ("authorization fatigue")](https://github.com/github/copilot-cli/issues/1168)** *(Open, 👍2)* – Single prompts can trigger a dozen+ auth pop-ups. Hurts workflow flow; community calling for token caching or batching.
8. **[#2770 – CLI gets stuck on 'Cancelling' and stops accepting Enter](https://github.com/github/copilot-cli/issues/2770)** *(Open, 👍9)* – After rate-limit failures, Escape key makes things worse: Enter becomes unresponsive, killing the session. High frustration signal.
9. **[#4204 – Add `.agents` discovery for instructions, agents, and hooks in any opened folder](https://github.com/github/copilot-cli/issues/4204)** *(Open)* – Wants `.agents/` conventions extended beyond Git repos, enabling folder-level customization without a repository.
10. **[#4286 – Streaming tool_use `input_json_delta` buffered until complete, causing multi-minute silences](https://github.com/github/copilot-cli/issues/4286)** *(Open)* – Large tool arguments cause complete silence during streaming, breaking responsiveness perception. Impacts model interoperability.

## Key PR Progress
Only one PR was active in the last 24 hours:
- **[#4100 – 安全性 (Security)](https://github.com/github/copilot-cli/pull/4100)** – Opened Jul 12 by huangyoufeng76-debug, still open. Title suggests a security-related change. No comments or reviews yet.

## Feature Request Trends
- **Customizable tool/sandbox configuration** – Multiple requests (#4298, #4204) call for whitelisting available tools in `settings.json` and extending `.agents` conventions to non-repo folders.
- **Session management improvements** – Better resume sorting by recency (#4140), session close capability for ACP clients (#4113), and multi-project PR linking (#4289) are recurring themes.
- **Model inheritance and transparency** – Users want subagents to correctly inherit session models (#4287) and for streaming to show progress on large tool arguments (#4286).
- **Credit/usage visibility** – A new request (#4295) asks for AI credit near-limit warnings in CLI, mirroring VS Studio 2026 features.

## Developer Pain Points
- **Log level regression (critical)** – Two separate reports (#4297, #4285) confirm the CLI crashes on startup for almost all log levels. Developers relying on debug/info logs are blocked.
- **Zombie processes not reaped** – #4163/#4290: Child processes accumulate as zombies on Linux, leaking ~2 per minute. Claimed fixed but users still see it on AlmaLinux.
- **Interactive mode crashes and hangs** – Blank screens on Windows (#4159), stuck “Cancelling” state (#2770, #2703), and Enter unresponsiveness after errors are active pain points.
- **Streaming / large output issues** – CLI hangs on commands larger than PTY buffer (#2182), and streaming tool arguments cause multi-minute silences (#4286).
- **Terminal compatibility** – Scroll wheel misbehavior in iTerm2 (#4288), broken Cmd+V paste (#4296), and incorrect colors in tmux (#4292) point to ongoing terminal-rendering gaps.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest
**Date: 2026-07-30**

---

## 1. Today's Highlights

The community is actively rallying around enterprise-grade Kimi K3 integration, with a new feature request (#2568) for custom API Base URL support to enable private gateway deployments. Concurrently, a critical fix (#2569) resolves a chained text replacement bug that silently undercounted successful edits, addressing a subtle but impactful developer experience issue. Several long-standing PRs, including Windows PowerShell detection and MCP log routing, have been merged, showing steady platform maturation.

---

## 2. Releases

No new releases in the last 24 hours.

---

## 3. Hot Issues

1. **#2568 – Support custom API Base URL for enterprise K3 gateway**  
   *Closed?* No | *Comments: 0* | *👍: 0*  
   **Why it matters:** As Kimi K3 (2.8T parameters) goes open-source, enterprises need to deploy behind private gateways for rate-limiting, latency optimization, fault tolerance, and centralized API key management. This is the highest-impact request for production adoption.  
   [View Issue](https://github.com/MoonshotAI/kimi-cli/issues/2568)

2. **#2566 – Error handling for long-running tool calls**  
   *Closed?* No | *Comments: 2* | *👍: 3*  
   **Why it matters:** Users report silent timeouts when tools (e.g., web scraping) exceed 60s. Community proposes configurable timeouts and retry logic.  
   [View Issue](https://github.com/MoonshotAI/kimi-cli/issues/2566)

3. **#2563 – Output streaming stalls on large codebase analysis**  
   *Closed?* No | *Comments: 5* | *👍: 2*  
   **Why it matters:** Terminal output freezes when processing repositories >10k files. Core to developer workflow reliability.  
   [View Issue](https://github.com/MoonshotAI/kimi-cli/issues/2563)

4. **#2559 – Relative path resolution fails in nested subdirectory**  
   *Closed?* No | *Comments: 3* | *👍: 1*  
   **Why it matters:** Basic path navigation broken for multi-level projects, blocking CI/CD pipeline usage.  
   [View Issue](https://github.com/MoonshotAI/kimi-cli/issues/2559)

5. **#2557 – Proposal: `--dry-run` mode for all mutation tools**  
   *Closed?* No | *Comments: 8* | *👍: 7*  
   **Why it matters:** Developers need safe previews before applying file changes. High community consensus.  
   [View Issue](https://github.com/MoonshotAI/kimi-cli/issues/2557)

6. **#2554 – Shell tool output truncated at 4096 chars**  
   *Closed?* No | *Comments: 4* | *👍: 4*  
   **Why it matters:** Limits visibility of long command outputs (e.g., `ls -la` on large directories). Fragments debugging workflow.  
   [View Issue](https://github.com/MoonshotAI/kimi-cli/issues/2554)

7. **#2549 – MCP server authentication token rotation**  
   *Closed?* No | *Comments: 1* | *👍: 2*  
   **Why it matters:** Security-critical for long-running sessions with external MCP servers.  
   [View Issue](https://github.com/MoonshotAI/kimi-cli/issues/2549)

8. **#2547 – Auto-complete for `--model` flag**  
   *Closed?* No | *Comments: 3* | *👍: 6*  
   **Why it matters:** With multiple model variants (K3, K2, K1), tab-completion saves time and reduces typos.  
   [View Issue](https://github.com/MoonshotAI/kimi-cli/issues/2547)

9. **#2545 – `kimi init` fails on fresh Windows install**  
   *Closed?* No | *Comments: 6* | *👍: 2*  
   **Why it matters:** New contributor friction – first-run experience broken on Windows due to PATH detection.  
   [View Issue](https://github.com/MoonshotAI/kimi-cli/issues/2545)

10. **#2542 – Logs should include trace ID for debugging**  
    *Closed?* No | *Comments: 2* | *👍: 5*  
    **Why it matters:** Without trace IDs, correlating errors across client/server becomes impossible for support.  
    [View Issue](https://github.com/MoonshotAI/kimi-cli/issues/2542)

---

## 4. Key PR Progress

1. **#2569 – Count chained StrReplaceFile edits against intermediate content** 🆕  
   *Status: OPEN* | *Author: aalhadxx*  
   **Fix:** Ensures consecutive text replacements count correctly when later edits modify earlier replacements. Previously underreported successful edits. Critical for guided refactoring workflows.  
   [View PR](https://github.com/MoonshotAI/kimi-cli/pull/2569)

2. **#2567 – Show absolute reset datetime in /usage panel** ✅  
   *Status: CLOSED* | *Author: versun*  
   **Feature:** `/usage` now shows precise local reset time (e.g., `resets at 2026-08-03 14:30:00`) plus relative duration. Improves quota visibility for power users.  
   [View PR](https://github.com/MoonshotAI/kimi-cli/pull/2567)

3. **#2284 – Fire notification hooks for approvals** ✅  
   *Status: CLOSED* | *Author: he-yufeng*  
   **Fix:** Approval requests now trigger `Notification` hooks, enabling custom UI/CLI alerts. Unblocks integrations with approval workflows.  
   [View PR](https://github.com/MoonshotAI/kimi-cli/pull/2284)

4. **#2176 – Extract text from ContentPart for UserPromptSubmit hook**  
   *Status: OPEN* | *Author: tears-mysthrala*  
   **Fix:** When user input is a list of `ContentPart` (default for all messages), `UserPromptSubmit` hook now receives correct prompt text instead of empty string. Solves regex matcher failures.  
   [View PR](https://github.com/MoonshotAI/kimi-cli/pull/2176)

5. **#1637 – Route MCP server log notifications to loguru** ✅  
   *Status: CLOSED* | *Author: he-yufeng*  
   **Fix:** MCP server logs (e.g., SearXNG) no longer clutter the TUI; routed cleanly to loguru. Greatly improves terminal cleanliness.  
   [View PR](https://github.com/MoonshotAI/kimi-cli/pull/1637)

6. **#1790 – Prefer pwsh over powershell.exe for Shell tool** ✅  
   *Status: CLOSED* | *Author: scwf*  
   **Fix:** Windows detection now correctly prefers PowerShell 7 (pwsh) over legacy `powershell.exe`. Includes fallback chain and tests.  
   [View PR](https://github.com/MoonshotAI/kimi-cli/pull/1790)

7. **#2564 – Add `--format json` flag for `/usage` output**  
   *Status: OPEN* | *Author: xiaoyi-bot*  
   **Feature:** Enables machine-readable quota data for scripting and monitoring dashboards.  
   [View PR](https://github.com/MoonshotAI/kimi-cli/pull/2564)

8. **#2562 – Replace `subprocess` calls with `asyncio.create_subprocess_exec`**  
   *Status: OPEN* | *Author: walter-lufei*  
   **Refactor:** Moves shell execution to asynchronous model, improving concurrency and preventing main-thread blocking.  
   [View PR](https://github.com/MoonshotAI/kimi-cli/pull/2562)

9. **#2558 – Add `--skip-unchanged` flag to file writing tools**  
   *Status: OPEN* | *Author: zhangliang-95*  
   **Efficiency:** Skips writing files when content hasn't changed, reducing disk I/O and unnecessary directory modifications.  
   [View PR](https://github.com/MoonshotAI/kimi-cli/pull/2558)

10. **#2553 – Cache resolved absolute paths in session**  
    *Status: OPEN* | *Author: renho-ren*  
    **Performance:** Reduces repeated `os.path.abspath` calls, improving speed for multi-file operations by ~30%.  
    [View PR](https://github.com/MoonshotAI/kimi-cli/pull/2553)

---

## 5. Feature Request Trends

Based on an analysis of all open issues, the community's top requested directions are:

- **Enterprise Gateway & Multi-Region Deployments** (#2568, #2550, #2546) – Custom API endpoints, load balancing, and private deployment for Kimi K3
- **Observability & Debugging** (#2566, #2542, #2554, #2538) – Structured logging (trace IDs), timeout controls, full output capture
- **Tool Safety & Preview** (#2557, #2558, #2535) – `--dry-run` mode, change previews, undo/rollback for file modifications
- **CLI Usability** (#2547, #2539, #2531) – Auto-completion, smarter path handling, `--help` examples for beginners
- **Performance & Scalability** (#2563, #2553, #2536) – Streaming improvements for large codebases, caching, async execution

---

## 6. Developer Pain Points

Recurring frustrations reported by the community include:

- **Insufficient error context** – Silent failures on tool timeouts (#2566), missing trace IDs (#2542), and zero-edit misreporting (#2569) erode trust in the CLI.
- **Windows first-run friction** – Multiple reports of `kimi init` and basic commands failing on clean Windows installs (#2545), plus legacy PowerShell detection issues (#1790).
- **Output truncation** – Shell tool and file reading commands truncate at arbitrary limits (#2554), forcing users to open files externally.
- **Path resolution brittleness** – Relative paths break in nested directories or symlinked projects (#2559), disrupting CI/CD automation.
- **MCP server noise** – Unrouted logs flooding the TUI (#1637) and lack of auth token rotation (#2549) complicate long-running sessions.
- **No safe mode for mutations** – Developers request `--dry-run` (#2557) and change previews to avoid accidental destructive edits.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest – 2026-07-30

---

## Today's Highlights

No new releases landed today, but the community is deeply engaged around two major themes: persistent session memory and critical reliability issues. The most-discussed open issue this week is a request for **native session goals** (`/goal`), with 120 upvotes and 66 comments, while a **severe SQLite unbounded growth bug** continues to draw attention from power users running long-lived instances. On the fix front, important PRs addressing **tool mutation previews** and **piped output truncation** are under review.

---

## Releases

No new releases in the last 24 hours.

---

## Hot Issues (Top 10)

### 1. [FEATURE]: Add native session goals with /goal
**#27167** – `opencode` lacks a persistent session goal/lifecycle feature. The proposal adds a `/goal` slash command to set and track high-level objectives across a session.  
👤 jorgitin02 | 👍 120 | 💬 66  
[https://github.com/anomalyco/opencode/issues/27167](https://github.com/anomalyco/opencode/issues/27167)

### 2. High CPU usage in newer versions of OpenCode
**#30086** – Users report severe CPU spikes in recent builds; sessions that once scaled to 10 concurrent instances now struggle with 3. The issue affects mouse responsiveness and overall system lag.  
👤 DenisSilent | 👍 20 | 💬 39  
[https://github.com/anomalyco/opencode/issues/30086](https://github.com/anomalyco/opencode/issues/30086)

### 3. Windows ARM64 native: OpenTUI fails to initialize
**#19130** – The native ARM64 binary for Windows works for CLI commands but crashes in TUI mode due to a bun:ffi dlopen TinyCC error. Blocks all interactive use on Snapdragon X/ARM laptops.  
👤 Carliquiss | 👍 10 | 💬 15  
[https://github.com/anomalyco/opencode/issues/19130](https://github.com/anomalyco/opencode/issues/19130)

### 4. OpenCode immediately enters auto-compaction loop and stops generating responses
**#30680** – A severe regression where OpenCode enters a continuous compaction cycle even in empty directories, consuming tokens without generating responses.  
👤 VineshF1 | 👍 0 | 💬 15  
[https://github.com/anomalyco/opencode/issues/30680](https://github.com/anomalyco/opencode/issues/30680)

### 5. `message="exiting loop"` – TUI repeatedly exits loop
**#38801** – Frustrated user reports OpenCode's TUI repeatedly exits its main loop after short conversations, making interactive use nearly impossible without high `step` settings.  
👤 josephtingiris | 👍 0 | 💬 14  
[https://github.com/anomalyco/opencode/issues/38801](https://github.com/anomalyco/opencode/issues/38801)

### 6. Request blocked by upstream provider
**#38190** – Intermittent upstream blocking errors when writing messages in chat, likely related to rate limiting or provider-side issues.  
👤 sosigboys | 👍 11 | 💬 14  
[https://github.com/anomalyco/opencode/issues/38190](https://github.com/anomalyco/opencode/issues/38190)

### 7. [2.0] Unbounded growth of the `event` table: opencode.db reaches 13GB+
**#33356** – The SQLite event-store table grows without retention or compaction, filling volumes to 97–99% on long-running instances. The primary culprit is excessive `message.updated.1` snapshots.  
👤 rustyaos | 👍 2 | 💬 13  
[https://github.com/anomalyco/opencode/issues/33356](https://github.com/anomalyco/opencode/issues/33356)

### 8. [core] Agent stops after tool execution with OpenAI-compatible providers
**#14972** – Providers like Gemini Flash and LiteLLM return `finish_reason: "stop"` after tool calls, causing the agent loop to halt instead of continuing.  
👤 valenvivaldi | 👍 4 | 💬 12  
[https://github.com/anomalyco/opencode/issues/14972](https://github.com/anomalyco/opencode/issues/14972)

### 9. [FEATURE]: Make Links Clickable (Ctrl+Left Click to Open)
**#1168** – A long-standing request (since July 2025) to make URLs in the TUI clickable with Ctrl+Click. One of the highest-voted features at 115 upvotes.  
👤 jay-tau | 👍 115 | 💬 9  
[https://github.com/anomalyco/opencode/issues/1168](https://github.com/anomalyco/opencode/issues/1168)

### 10. Error from provider (Console Go): Upstream request failed – Kimi K3
**#37815** – The Kimi K3 model appears in the provider list but fails with an upstream error on selection, while other Console Go models work fine.  
👤 nyaa666 | 👍 5 | 💬 6  
[https://github.com/anomalyco/opencode/issues/37815](https://github.com/anomalyco/opencode/issues/37815)

---

## Key PR Progress (Top 10)

### 1. fix(opencode): await stdout drain so piped output is not truncated
**#39577** – Fixes silent truncation when piping commands like `opencode db`, `session list`, and `export` past 64 KiB.  
👤 jornado  
[https://github.com/anomalyco/opencode/pull/39577](https://github.com/anomalyco/opencode/pull/39577)

### 2. fix(core): add mutation permission previews
**#39578** – Adds structured `metadata.files` diff previews to write/edit permission requests, aligning tool descriptions with their actual overwrite behavior.  
👤 rekram1-node  
[https://github.com/anomalyco/opencode/pull/39578](https://github.com/anomalyco/opencode/pull/39578)

### 3. fix(core): publish domain updates after committed state is readable
**#37987** – Prevents state domains from publishing update events before the rebuilt state is fully committed, fixing a race condition in domain event delivery.  
👤 IbrahimKhan12  
[https://github.com/anomalyco/opencode/pull/37987](https://github.com/anomalyco/opencode/pull/37987)

### 4. fix(opencode): strip provider control tokens from invalid tool output
**#37472** – Sanitizes malformed tool arguments from OpenAI-compatible providers that embed control tokens like `<|tool_call_begin|>` in API responses.  
👤 IbrahimKhan12  
[https://github.com/anomalyco/opencode/pull/37472](https://github.com/anomalyco/opencode/pull/37472)

### 5. fix(opencode): sanitize Bedrock document names from file attachments
**#37535** – Strips characters from MCP synthetic filenames that Amazon Bedrock rejects, preventing attachment failures.  
👤 IbrahimKhan12  
[https://github.com/anomalyco/opencode/pull/37535](https://github.com/anomalyco/opencode/pull/37535)

### 6. fix(app): read the message from structured server error payloads
**#39180** – Improves error handling for structured API failures that arrive as plain objects, fixing uninformative "undefined" error messages.  
👤 IbrahimKhan12  
[https://github.com/anomalyco/opencode/pull/39180](https://github.com/anomalyco/opencode/pull/39180)

### 7. fix(core): omit undefined optional keys from glob/grep permission metadata
**#37965** – Prevents `undefined` values from being injected into permission metadata for optional glob/grep inputs, fixing permission prompt display bugs.  
👤 IbrahimKhan12  
[https://github.com/anomalyco/opencode/pull/37965](https://github.com/anomalyco/opencode/pull/37965)

### 8. fix(opencode): skip tui migration when tui.jsonc exists
**#38194** – Prevents a startup crash when a user already has a commented `tui.jsonc` file by skipping the legacy migration that only checked for `tui.json`.  
👤 IbrahimKhan12  
[https://github.com/anomalyco/opencode/pull/38194](https://github.com/anomalyco/opencode/pull/38194)

### 9. fix(ui): prepare diffs off the render thread
**#34415** – Moves expensive diff preparation into a Web Worker, preventing UI freezes on large diffs (e.g., `llama.cpp` on Windows).  
👤 jerrydong1988  
[https://github.com/anomalyco/opencode/pull/34415](https://github.com/anomalyco/opencode/pull/34415)

### 10. fix(app): avoid O(n^2) dedup hang on large diff summaries
**#34414** – Replaces a `result.some()` inside `reduceRight` that caused ~600M comparisons on large diffs, fixing renderer hangs.  
👤 jerrydong1988  
[https://github.com/anomalyco/opencode/pull/34414](https://github.com/anomalyco/opencode/pull/34414)

---

## Feature Request Trends

The community is converging around several high-demand feature directions:

1. **Persistent session memory** – Multiple requests (#27167, #32658) ask for native session goals and project-level memory that persists across restarts, enabling long-running agent workflows without manual goal re-setting.

2. **Auto-mode and permission automation** – Issues #37564 and #20066 seek smarter "auto-approve" for permissions based on model classification, and cross-session persistence of `Allow always` decisions.

3. **Clickable links in TUI** – Issue #1168 (115 upvotes) remains one of the most-requested UX improvements for the terminal interface.

4. **RTL language support** – Issue #34697 follows up on a recent RTL direction map update, requesting actual translation files for Farsi, Urdu, Pashto, and other RTL languages.

5. **Secret redaction** – Issue #39512 proposes native credential scrubbing from tool outputs and context before sending to LLM providers, addressing a real security concern.

---

## Developer Pain Points

1. **SQLite DB bloat** – Issues #33356 and #30680 both highlight that OpenCode's event store grows unboundedly, filling disks and triggering infinite compaction loops. This affects production users with long-running instances most severely.

2. **Provider compatibility breaks** – Multiple issues report problems with specific providers: Bedrock DeepSeek model ID mangling (#34412), Console Go Kimi K3 failures (#37815), and OpenAI-compatible providers returning spurious `finish_reason: "stop"` after tool calls (#14972).

3. **TUI reliability regressions** – Issue #38801 (`exiting loop`) and #30680 (auto-compaction loop) indicate a broader regression in the TUI's session lifecycle, causing frequent disconnects and performance degradation.

4. **Initialization/config races** – False-positive model validation warnings on startup (#39313) and broken config migrations (#38194) create friction for users updating or first configuring OpenCode.

5. **ARM64/Terminal incompatibilities** – Windows ARM64 TUI failures (#19130) and GNU Screen compatibility issues (#32985) continue to block users on non-standard platforms.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-07-30

## Today's Highlights
Pi shipped **v0.83.0** with credential export for external clients and headless OpenRouter sign-in, while a flurry of 50+ issues and 23 PRs landed in the last 24 hours. Notable fixes land for the Markdown math rendering gap, a long‑standing parallel tool‑call orphan bug, and the first concrete PR toward an official Pi evaluation harness. Provider‑specific correctness (Vertex finishReason mapping, llama.cpp streaming usage, Bedrock metadata) and TUI polish (Kitty backspace, tmux sixel images) dominate the patch landscape.

## Releases
**v0.83.0** — [Release](https://github.com/badlogic/pi-mono/releases/tag/v0.83.0)
- **Credential export** — `pi auth print-api-key` and `pi auth print-bearer-token` let external clients reuse configured credentials with automatic OAuth refresh and minimum‑validity enforcement.
- **Headless OpenRouter sign‑in** — Complete `/login` over SSH by pasting a redirect URI; no browser required on the remote machine.

## Hot Issues (10 selected)

1. **#6951 — Qwen reasoning effort tiers mismatch** ([link](https://github.com/earendil-works/pi/issues/6951))  
   *Closed.* Qwen’s `qwen3.8-max-preview` expects `low`/`medium`/`xhigh` but Pi maps to its own `minimal`/`low`/`medium`/`high`. Community upvoted—affects correctness of reasoning‑level control for a popular model.

2. **#1871 — Misleading auth error during parallel startup** ([link](https://github.com/earendil-works/pi/issues/1871))  
   *Closed.* Lock contention from concurrent `pi` processes (e.g., `pi-subagents`) produces a scary `"No API key found"` error. The real issue is a file‑lock race; the mis‑diagnosis wastes user time.

3. **#7199 — Kimi K3 on Fireworks not selectable** ([link](https://github.com/earendil-works/pi/issues/7199))  
   *Open, in‑progress.* `kimi-k3` and `kimi-k3-fast` were added to models.dev but Pi’s Fireworks provider doesn’t list them. The generator maps all Fireworks models via a static pattern—this needs a registry refresh.

4. **#7153 — `/scoped-models` hangs silently for ~5 minutes** ([link](https://github.com/earendil-works/pi/issues/7153))  
   *Open.* The command blocks on a catalog refresh before showing any UI. No spinner, no timeout—users are left staring at a blank editor. High annoyance for model switchers.

5. **#7035 — Intermittent crash on large grep result** ([link](https://github.com/earendil-works/pi/issues/7035))  
   *Closed, no‑action.* Broad grep operations with large outputs crash Pi instantly on Slackware. Likely a memory‑pressure issue; user reports `deepseek-v4-pro` as the model.

6. **#7053 — Parallel tool batches lose completed results when one sibling stalls** ([link](https://github.com/earendil-works/pi/issues/7053))  
   *Open.* Follow‑up to #3503. UI events fire per‑tool now, but the persisted `toolResult` message waits for the whole batch (`Promise.all`). A stalled tool call orphans all earlier results → `"No result provided"`.

7. **#7253 — `/compact` double‑triggers at 90% context** ([link](https://github.com/earendil-works/pi/issues/7253))  
   *Open.* Manual `/compact` combined with auto‑compact when the window is low causes an infinite loop until Esc is pressed, then errors with `"Compaction failed: Already compacting"`.

8. **#7130 — Backspace deletes 2 chars in Kitty** ([link](https://github.com/earendil-works/pi/issues/7130))  
   *Open.* Kitty’s keyboard protocol doesn’t filter release events, so a single Backspace press registers twice. Affects all users of the popular terminal emulator.

9. **#7252 — Markdown renderer corrupts raw LaTeX** ([link](https://github.com/earendil-works/pi/issues/7252))  
   *Closed, no‑action.* `marked` consumes operators and backslashes in raw math source; the corruption is display‑only (session JSONL is intact). Users relying on math‑heavy model output see broken rendering.

10. **#7264 — Support LaTeX math rendering (`$$...$$`)** ([link](https://github.com/earendil-works/pi/issues/7264))  
    *Closed, untriaged.* Feature request to render `$...$` and `$$...$$` inline math in the Markdown component. Currently model output with standard math delimiters appears as plain text.

## Key PR Progress (10 selected)

1. **#7289 — Comparative Pi eval harness** ([link](https://github.com/earendil-works/pi/pull/7289))  
   *Open.* Adds seeded, multi‑harness comparisons with score lift, token/latency/cost deltas, and persisted runs. A critical piece for benchmarking Pi vs. other coding agents.

2. **#7288 — Preserve function arguments with empty `custom` payloads** ([link](https://github.com/earendil-works/pi/pull/7288))  
   *Closed.* Fix for #7160: when an OpenAI‑compatible provider emits a valid `function` + empty `custom: {}`, Pi now prefers the function payload instead of discarding arguments.

3. **#7272 — Preserve provider raw stop reason** ([link](https://github.com/earendil-works/pi/pull/7272))  
   *Closed.* Adds `AssistantMessage.rawStopReason` so providers like Vertex/Gemini can surface `MALFORMED_FUNCTION_CALL`, `SAFETY`, etc. instead of collapsing everything to `"error"`.

4. **#7245 — Inline images under tmux via sixel** ([link](https://github.com/earendil-works/pi/pull/7245))  
   *Closed.* Enables image display inside tmux by adding a sixel backend. Previously image support was disabled entirely when `TMUX` was set.

5. **#7163 — Search index via SQLite FTS5** ([link](https://github.com/earendil-works/pi/pull/7163))  
   *Open.* Implements `SessionRepo.search()` with a contentless FTS5 virtual table for SQLite backends. Paves the way for fast session search across large histories.

6. **#7122 — Byte count, false limit warning, surrogate pair fixes** ([link](https://github.com/earendil-works/pi/pull/7122))  
   *Closed.* Three tool‑layer fixes: corrects UTF‑8 byte counting in `write`, avoids false limit warnings in `find`, and handles surrogate pairs in `truncateLine`.

7. **#7261 — Clipboard read via wl‑paste on Wayland** ([link](https://github.com/earendil-works/pi/pull/7261))  
   *Closed.* Replaces the X11‑only `clipboard-rs` addon with `wl‑paste` on Wayland, `xclip`/`xsel` on X11. Ctrl+V paste now works on Wayland.

8. **#7258 — Enable streaming usage for llama.cpp** ([link](https://github.com/earendil-works/pi/pull/7258))  
   *Closed.* Sets `supportsUsageInStreaming: true` so llama.cpp streams include `stream_options.include_usage`, giving accurate per‑session token stats.

9. **#7221 — Stop loading AGENTS.md twice in nested git worktrees** ([link](https://github.com/earendil-works/pi/pull/7221))  
   *Closed.* The ancestor walk from a worktree nested under its main repo duplicated `AGENTS.md`/`CLAUDE.md`. Now filters out duplicate repos during the walk.

10. **#7260 — Clean up extension event bus listeners** ([link](https://github.com/earendil-works/pi/pull/7260))  
    *Closed.* Scopes `pi.events.on()` subscriptions to the extension runtime that registered them, invalidates stale listeners on reload, and adds regression tests.

## Feature Request Trends

- **LaTeX/Math rendering in Markdown** — Multiple issues (#7252, #7264) ask for proper `$...$` and `$$...$$` inline math support in the TUI Markdown renderer. Currently model output with standard math delimiters is corrupted or shown as plain text.
- **Customizable tool limits** — #3432 and #7066 request configurable line/byte limits for the `read` and `write` tools, especially for local models that struggle with oversized context.
- **Audio content in tool results** — #7279 proposes adding native audio support (`AudioContent` blocks) parallel to the existing image/vision capabilities.
- **Session reactivity & state introspection** — #5329 asks for a way to distinguish “busy thinking” vs. “waiting for user input” for host integrations, and #7285 asks that `--resume` into an ongoing session reactively updates.

## Developer Pain Points

- **Parallel/async tool execution fragility** — #7053 (orphaned tool results when one sibling stalls) and #1871 (lock contention maskers as auth error) show that Pi’s concurrency model for tool calls and startup is still brittle.
- **Provider‑specific correctness friction** — Qwen reasoning tiers (#6951), Vertex finishReason mapping (#7255), and llama.cpp streaming usage (#7258) each required dedicated tracking. The community is actively building workarounds.
- **TUI/terminal compatibility** — Kitty backspace double‑delete (#7130), tmux image support lacking (#7245), and clipboard paste no‑op on Wayland (#7248, fixed in #7261) point to ongoing pain for users on non‑standard terminals or Wayland.
- **Model catalog staleness** — New models like Kimi K3 (#7199) appear in models.dev but aren’t selectable until Pi’s provider‑model map is manually regenerated. The `/scoped-models` 5‑minute hang (#7153) amplifies the frustration.
- **Context compaction double‑triggering** — #7253 shows that the auto‑compact and manual `/compact` paths collide, causing an infinite loop that requires Esc to break.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest
**Date:** 2026-07-30  
**Author:** Technical Analyst, AI Developer Tools

---

## Today's Highlights

The Qwen Code team shipped a new nightly release (`v0.21.0-nightly`) with an autofix enhancement that defers suggestions after five change rounds, aiming to reduce noise in long review loops. The community continues to demand better UI usability on Windows (scrolling, mouse interaction, copy/paste) and deeper Anthropic model compatibility. A cluster of CI failures from repeated E2E test hangs suggests infrastructure instability that the team is actively triaging with `autofix/approved` labels.

---

## Releases

- **v0.21.0-nightly.20260729.0c0ca5fed**  
  [Release link](https://github.com/QwenLM/qwen-code/releases/tag/v0.21.0-nightly.20260729.0c0ca5fed)  
  **What's Changed:**  
  - `feat(autofix): defer suggestions after five change rounds` by @qqqys ([PR #7913](https://github.com/QwenLM/qwen-code/pull/7913)) — After five consecutive LLM-suggested change rounds, the autofix system will now pause to avoid overwhelming users with redundant proposals.  
  **Full changelog:** [Compare](https://github.com)

*No stable release in the last 24 hours.*

---

## Hot Issues (Top 10 by Comment Activity)

1. **#8012** [OPEN] — *feat(github-channel): close delivery, batching, and review-event gaps*  
   [Link](https://github.com/QwenLM/qwen-code/issues/8012)  
   **Why it matters:** A logical follow-up to #7826, this feature request aims to make the GitHub notification channel fully functional by handling delivery confirmation, batched updates, and pull request review events. Community discussion suggests this is a high-priority integration gap.  
   **Comments:** 5 | 👍: 0

2. **#8039** [OPEN] — *fix(core): Anthropic 4.6+ assistant-prefill 400 + thinking.display silently defaults to 'omitted'*  
   [Link](https://github.com/QwenLM/qwen-code/issues/8039)  
   **Why it matters:** Two verified bugs affect all Claude Opus/Sonnet 4.6+ and 5.x models. The assistant-turn "prefill" returns a 400 with no fallback, and `thinking.display` silently defaults to `omitted` instead of the expected `hidden`. This blocks reliable use of Anthropic's latest model families.  
   **Comments:** 5 | 👍: 0 | **welcome-pr** label

3. **#7964** [CLOSED] — *Window 终端中升级到0.21.1后内容无法滚动*  
   [Link](https://github.com/QwenLM/qwen-code/issues/7964)  
   **Why it matters:** A critical Windows UX regression — after upgrading to v0.21.1, terminal content became unscrollable. The Chinese-language report includes screenshots showing a fully stuck viewport. Quickly closed, indicating a hotfix or revert was applied.  
   **Comments:** 4 | 👍: 0

4. **#8060** [OPEN] — *Main CI failed: E2E Tests — interactive/file-system-interactive.test.ts > … > read-then-write sequence*  
   [Link](https://github.com/QwenLM/qwen-code/issues/8060)  
   **Why it matters:** A persistent E2E failure on `main` — the same test (`file-system-interactive.test.ts`) has now failed in multiple runs. Tagged `autofix/in-progress`, indicating the system is attempting automated remediation.  
   **Comments:** 3 | 👍: 0

5. **#7960** [OPEN] — *Compression side-query's fixed maxOutputTokens can exceed context window on small-window deployments*  
   [Link](https://github.com/QwenLM/qwen-code/issues/7960)  
   **Why it matters:** Users running self-hosted vLLM with small `max_model_len` encounter a hard 400 error from the compression side-query, producing `COMPRESSION_FAILED_EMPTY_SUMMARY`. The fix needs to dynamically clamp `maxOutputTokens` based on actual context remaining.  
   **Comments:** 3 | 👍: 0

6. **#7961** [OPEN] — *Main-turn output-token clamp can under-count CJK-heavy new content by ~chars/4*  
   [Link](https://github.com/QwenLM/qwen-code/issues/7961)  
   **Why it matters:** The token estimation logic uses a character-based approximation that underestimates CJK tokens by ~4x, causing context window overflows on small-window deployments. Combined with #7960, this makes self-hosted small-model use fragile.  
   **Comments:** 3 | 👍: 0

7. **#8003** [OPEN] — *Model outputs XML-style tool calls as plain text instead of structured function calls in long sessions*  
   [Link](https://github.com/QwenLM/qwen-code/issues/8003)  
   **Why it matters:** After 200+ turns (180K+ context), `qwen3.8-max-preview` occasionally emits raw XML tool calls (`<invoke>`) instead of the expected `tool_calls` array. Qwen Code does not handle this fallback, breaking long sessions. A **welcome-pr** opportunity.  
   **Comments:** 3 | 👍: 0

8. **#8036** [OPEN] — *v0.21.1无法通过鼠标滚轮翻阅对话内容，也无法选取内容*  
   [Link](https://github.com/QwenLM/qwen-code/issues/8036)  
   **Why it matters:** Another v0.21.1 regression on Windows: mouse wheel scrolling and text selection are broken, forcing keyboard-only navigation (PgUp/PgDn). This is a recurring theme across multiple Windows reports.  
   **Comments:** 3 | 👍: 0

9. **#8052** [OPEN] — *v0.21.1 起虚拟化历史默认开起的bug*  
   [Link](https://github.com/QwenLM/qwen-code/issues/8052)  
   **Why it matters:** Virtualized history is now enabled by default in v0.21.1 on Windows, causing duplicate rendering of previous records when scrolling. Indicates a default-configuration issue.  
   **Comments:** 3 | 👍: 0

10. **#7972** [OPEN] — *0.21.1使用 奔溃3次*  
    [Link](https://github.com/QwenLM/qwen-code/issues/7972)  
    **Why it matters:** Three crashes on Windows 10 after upgrading to v0.21.1. The user provided Node.js v24.18.0 and a custom Alibaba endpoint (`token-plan.cn-beijing.maas.aliyuncs.com`), suggesting regional deployment may be involved.  
    **Comments:** 3 | 👍: 0

---

## Key PR Progress (Top 10 by Impact)

1. **#7922** [CLOSED] — *feat(core): preload deferred tools within a context-window threshold*  
   [Link](https://github.com/QwenLM/qwen-code/pull/7922)  
   **Summary:** Introduces `tools.toolSearch.threshold` (default 10% of context window). At session start, if a deferred tool schema fits within this threshold, it is preloaded into the system prompt — reducing cold-starts when the tool is later invoked.  
   **Author:** @DragonnZhang | **Status:** Merged

2. **#7927** [CLOSED] — *fix(core): rebind fork capabilities on resume*  
   [Link](https://github.com/QwenLM/qwen-code/pull/7927)  
   **Summary:** Fixes #7924 — when a paused background fork agent is resumed after the parent runtime changes, its tool declarations and system instruction are now rebuilt from current state rather than stale launch-time snapshots.  
   **Author:** @DragonnZhang | **Status:** Merged

3. **#8044** [OPEN] — *fix(autofix): cumulative timeout breaker, narrowed retry prompt, truthful handoff wording*  
   [Link](https://github.com/QwenLM/qwen-code/pull/8044)  
   **Summary:** Addresses two honesty gaps in autofix failure handling: a `CONSECUTIVE_FAILURE_CAP=5` that didn't reset on interleaved timeouts, and a retry prompt that misleadingly implies capability.  
   **Author:** @wenshao | **Status:** Open, autofix/takeover

4. **#7976** [OPEN] — *fix(serve): Add certified session writer handoff*  
   [Link](https://github.com/QwenLM/qwen-code/pull/7976)  
   **Summary:** Adds an integrity-protected handoff protocol for daemon-managed session writers, publishing a schema-v2 sealed lock with runtime transcript keys — ensuring durable, verifiable shutdown/restart flows.  
   **Author:** @doudouOUC | **Status:** Open, autofix/takeover

5. **#8002** [OPEN] — *feat(serve): page large text files by byte cursor*  
   [Link](https://github.com/QwenLM/qwen-code/pull/8002)  
   **Summary:** Adds bounded byte-cursor paging across HTTP, ACP, TypeScript SDK, and daemon MCP surfaces. An opaque `nextCursor` token replaces naive line/limit pagination for large files.  
   **Author:** @doudouOUC | **Status:** Open, autofix/takeover

6. **#8057** [OPEN] — *feat(skills): add disabled skill levels*  
   [Link](https://github.com/QwenLM/qwen-code/pull/8057)  
   **Summary:** Introduces `skills.disabledLevels` allowing users to disable entire skill tiers (`project`, `user`, `extension`, `bundled`) without denylisting individual skills. Directly implements feature request #8054.  
   **Author:** @zhangxy-zju | **Status:** Open, autofix/takeover

7. **#8050** [OPEN] — *fix: make the test suite portable on Windows*  
   [Link](https://github.com/QwenLM/qwen-code/pull/8050)  
   **Summary:** Makes the full test suite and runtime paths consistent on Windows while preserving POSIX-only assertions. Reuses existing self-hosted Windows validation workflow. Directly addresses frequent Windows CI flakiness.  
   **Author:** @yiliang114 | **Status:** Open, autofix/takeover

8. **#8033** [OPEN] — *fix(channels): make GitHub final response publication single-shot*  
   [Link](https://github.com/QwenLM/qwen-code/pull/8033)  
   **Summary:** Ensures each incoming GitHub event produces at most one final comment (or `<no-reply/>` suppression). Prevents duplicate publications and records a local audit entry for every outcome.  
   **Author:** @yiliang114 | **Status:** Open, review/self-reported

9. **#8005** [OPEN] — *feat(cli): adopt Goal v3 in interactive TUI*  
   [Link](https://github.com/QwenLM/qwen-code/pull/8005)  
   **Summary:** Connects the interactive TUI to the new Goal v3 runtime, adding `/goal` lifecycle commands, persistent lifecycle cards, footer status, resume/branch recovery, and a two-lane input queue.  
   **Author:** @qqqys | **Status:** Open, autofix/takeover

10. **#7983** [OPEN] — *feat(review): add `review run` — headless review with a machine-readable verdict*  
    [Link](https://github.com/QwenLM/qwen-code/pull/7983)  
    **Summary:** Introduces `qwen review run [target]` — a headless non-interactive review mode that outputs a machine-readable verdict on stdout, progress on stderr, and exit codes for CI gating. Part of #7981.  
    **Author:** @wenshao | **Status:** Open, autofix/takeover

---

## Feature Request Trends

Based on the last 24 hours of issues:

1. **GitHub Integration Gaps** (#8012, #8028, #8033) — Users want full-stack GitHub channel features: delivery confirmation, batching, review-event handling, `reasonFilter` to skip unwanted notifications, and single-shot final responses. This signals that the GitHub channel is now being used in production and needs production-grade reliability.

2. **Role-Based Model Routing** (#8021) — A proposal to bind model groups to intent-based roles (cheap/fast for exploration, strong for implementation, different models for subagents). This reflects a growing need for cost-aware multi-model orchestration.

3. **Skill-Level Management** (#8054, #8057) — Users want a single switch to disable all bundled skills (or entire skill levels) instead of denylisting manually. This indicates that the bundled skill ecosystem is expanding and needs coarse-grained governance.

4. **Headless & CI Integration** (#7983) — Machine-readable review verdicts for CI pipelines. The `review run` PR is directly implementing this, showing strong demand from CI-first teams.

5. **Workspace Memory Isolation** (#8056) — Workspace-qualified asynchronous memory operations (remember/forget/dream) with opt-in exact-workspace storage. Suggests that multi-workspace environments are becoming more common.

---

## Developer Pain Points

1. **Windows UX Regressions (High Frequency)** — Multiple issues (#7964, #8036, #8052, #7972) report that v0.21.1 broke scrolling, mouse selection, copy/paste, and caused crashes on Windows. The community is clearly frustrated; several reports include Chinese-language details with screenshots. The "run on Windows" label is appearing on multiple CI-related PRs.

2. **Self-Hosted / Small-Window Model Fragility** (#7960, #7961) — Users running self-hosted vLLM endpoints with small context windows face two overlapping token estimation bugs: compression side-queries exceed context windows, and CJK character counting underestimates tokens by ~4x. This makes self-hosting a second-class experience.

3. **Anthropic Model Compatibility** (#8039, #7984) — Two separate bugs affecting Claude Opus/Sonnet 4.6+ and 5.x families. Assistant-prefill 400 errors and a `send_message` tool schema that breaks entirely on Anthropic-backed models. This suggests that Anthropic's API is diverging from OpenAI compatibility in ways the core hasn't caught up with.

4. **Long-Session Stability** (#8003) — After 200+ turns, `qwen3.8-max-preview` regresses to raw XML tool calls. This undermines trust in long-running autonomous sessions and is labeled `welcome-pr` — likely needing community contribution.

5. **CI Infrastructure Instability** — A burst of E2E test failures (#8060, #8029, #8018, #8019, #8022, #8023, #8026, #7937, #7942) all from `file-system-interactive.test.ts` hangs and `tool-control.test.ts` callbacks. Many are tagged `autofix/approved`, suggesting automated remediation is working but the underlying flakiness remains unresolved.

---

*Digest generated from QwenLM/qwen-code GitHub activity (2026-07-29 00:00 UTC – 2026-07-30 00:00 UTC).*

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-07-30

## Today's Highlights

The community is converging on **v0.9.2**, with the maintainer cutting the final release candidate after a coordinated flurry of bug fixes, CI hardening, and localization merges. A critical fix landed for Brazilian ABNT2 keyboard users where `AltGr+Q` was hijacked by the help overlay, and the Skills Manager now avoids filesystem timeouts on cold Linux systems. Indonesian localization reached full parity across both the TUI and website, while a new `/stop` command proposal signals growing demand for runtime tool-call interruption.

## Releases

No new releases in the last 24 hours. The project is actively finalizing **v0.9.2** (see PR #4964).

## Hot Issues

1. **#4959 — Proposed 'stop' command** [OPEN]  
   *Author: ronohara*  
   `enhancement` | 3 comments  
   Requests a `/stop` command and runtime STOP-word intercept to mechanically block tool calls when models ignore textual "stop" cues in autonomous mode. High community interest for agent safety.  
   [Link](https://github.com/Hmbown/CodeWhale/issues/4959)

2. **#4949 — Chinese translation of "Constitution"** [OPEN]  
   *Author: SparkofSpike*  
   `discussion` | 2 comments  
   Debate over whether to translate "Constitution" as "宪法" (politically sensitive in Chinese) or "协作准则". The PR author reverted their own change to invite broader community input.  
   [Link](https://github.com/Hmbown/CodeWhale/issues/4949)

3. **#4723 — AltGr+Q on Brazilian ABNT2 opens help** [OPEN]  
   *Author: nicolassmotta*  
   `bug` | 2 comments  
   Windows reports AltGr as `Ctrl+Alt`, causing `/` (typed via `AltGr+Q`) to match the `Ctrl-/` help chord. Affects all Brazilian Portuguese keyboard users.  
   [Link](https://github.com/Hmbown/CodeWhale/issues/4723)

4. **#4957 — LaTeX math displayed as raw source** [CLOSED]  
   *Author: antarikshraya*  
   `enhancement` | 1 comment  
   `$\theta \in \mathbb{R}^6$` rendering as plaintext. Fixed in PR #4974 via Unicode substitution.  
   [Link](https://github.com/Hmbown/CodeWhale/issues/4957)

5. **#4941 — Thinking level reverts to Auto on restart** [CLOSED]  
   *Author: Hmbown*  
   `bug` | 1 comment  
   Persisted `reasoning_effort` was discarded when auto model routing kicked in. Fixed by keeping raw tier requests independent of model/provider changes.  
   [Link](https://github.com/Hmbown/CodeWhale/issues/4941)

6. **#4976 — Skills Manager compatible toggle times out on cold filesystems** [CLOSED]  
   *Author: Hmbown*  
   `bug` | 0 comments  
   Synchronous re-audit of owned skills exceeded 15-second budget on Linux. Fixed by reusing owned inventory and scanning only new external roots.  
   [Link](https://github.com/Hmbown/CodeWhale/issues/4976)

7. **#4547 — Stale spinners for dead shell jobs** [CLOSED]  
   *Author: Hmbown*  
   `bug` | 0 comments  
   Transcript exec cards showed animated spinners for jobs that `./jobs` reported as stale or missing. Fixed by finalizing cells when jobs leave the registry.  
   [Link](https://github.com/Hmbown/CodeWhale/issues/4547)

8. **#4934 — Website non-critique** [OPEN]  
   *Author: JayBeest*  
   `discussion` | 2 comments  
   A playful but valid point: the website is "super-active" but needs theming consideration. Community member accidentally lost their critique draft.  
   [Link](https://github.com/Hmbown/CodeWhale/issues/4934)

9. **#4789 — Add Indonesian localization** [CLOSED]  
   *Author: Hmbown*  
   `enhancement` | 2 comments  
   Full Indonesian TUI pack (1248 keys) and README shipped. Indonesia has larger dev population than Vietnam, which received earlier priority.  
   [Link](https://github.com/Hmbown/CodeWhale/issues/4789)

10. **#1186 — Typed persistent permission rules** [CLOSED]  
    *Author: greyfreedom*  
    `enhancement` | 13 comments  
    Adds rule scoping by tool name, command prefix, and workspace path with `allow`/`deny`/`ask` decisions. Extended by PR #4960 with listing and removal.  
    [Link](https://github.com/Hmbown/CodeWhale/issues/1186)

## Key PR Progress

1. **#4977 — Fix AltGr-typed "/" on Brazilian ABNT2** [OPEN]  
   *Author: yyyCode*  
   Checks for `Ctrl+Alt+Q` specifically without pressing `Ctrl` before consuming the event. Directly fixes #4723.  
   [Link](https://github.com/Hmbown/CodeWhale/pull/4977)

2. **#4974 — Hardened LaTeX transcript rendering** [CLOSED]  
   *Author: Hmbown*  
   Supersedes #4973 with maintainer hardening. Uses Unicode substitution for `$...$`, `$$...$$`, `\(...\)`, `\[...\]` delimiters, fixing `\mathbb{R}` paths. Closes #4957.  
   [Link](https://github.com/Hmbown/CodeWhale/pull/4974)

3. **#4972 — Indonesian website locale dictionary** [CLOSED]  
   *Author: atmosuwiryo*  
   Adds `id` dictionary files for `codewhale.net`, including `chrome.ts` and `home.ts`, bringing website localization to full parity with the TUI pack. Closes #4789.  
   [Link](https://github.com/Hmbown/CodeWhale/pull/4972)

4. **#4964 — Finalize CodeWhale 0.9.2** [CLOSED]  
   *Author: Hmbown*  
   Release commit with Kimi context-window reporting, manual provider overrides, auto-compaction fixes, and updated release notes.  
   [Link](https://github.com/Hmbown/CodeWhale/pull/4964)

5. **#4961 — Preserve reasoning effort with auto routing** [CLOSED]  
   *Author: nightt5879*  
   Keeps raw `reasoning_effort` tier independent through all model/provider change paths. Fixes #4941.  
   [Link](https://github.com/Hmbown/CodeWhale/pull/4961)

6. **#4960 — Safe permissions rule list and removal** [CLOSED]  
   *Author: greyfreedom*  
   Adds `/permissions` listing with preview-and-confirm removal using snapshot-bound token. Reloads live ruleset after removal. Extends #1186.  
   [Link](https://github.com/Hmbown/CodeWhale/pull/4960)

7. **#4937 — Finalize stale shell transcript cells** [CLOSED]  
   *Author: LI-Jialu*  
   Replaces live spinners with static "stale/no-output" status for jobs that left the registry. Fixes #4547.  
   [Link](https://github.com/Hmbown/CodeWhale/pull/4937)

8. **#4975 — Keep Skills Manager scan toggle responsive** [CLOSED]  
   *Author: Hmbown*  
   Release blocker fix. Reuses owned skill rows, scans only new external roots, recomputes cross-root conflicts. Fixes #4976.  
   [Link](https://github.com/Hmbown/CodeWhale/pull/4975)

9. **#4963 — Prevent duplicate /resume entries from orphan sessions** [CLOSED]  
   *Author: SparkofSpike*  
   Stops auto-promotion of interrupted checkpoint files to session files, preventing duplicates in `/resume`.  
   [Link](https://github.com/Hmbown/CodeWhale/pull/4963)

10. **#4958 — SBOM attestation and provenance mode** [CLOSED]  
    *Author: kobihikri*  
    Pins BuildKit's provenance mode explicitly and adds SBOM attestation to release image builds.  
    [Link](https://github.com/Hmbown/CodeWhale/pull/4958)

## Feature Request Trends

- **Runtime tool-call interruption**: The `/stop` command proposal (#4959) reflects a growing need to mechanically halt autonomous agent loops when models ignore textual "stop" cues.
- **Localization expansion**: After Vietnamese and Indonesian, the community is debating translation terminology choices (e.g., "Constitution" in Chinese, #4949), signaling demand for more non-English markets.
- **Permission system maturity**: From basic allow/deny rules (#1186) to listing and removal UI (#4960), users want granular, inspectable permissions per tool and workspace path.
- **Math rendering in TUI**: LaTeX display (#4957) was a high-signal request for technical/scientific users, now resolved with Unicode substitution (#4974).

## Developer Pain Points

- **Keyboard layout conflicts on Windows**: `AltGr+Q` on Brazilian ABNT2 (#4723) highlights a class of input-method bugs that cascade from Windows' low-level key reporting (`Ctrl+Alt` for AltGr).
- **Filesystem-bound synchronous operations**: The Skills Manager timeout (#4976) on cold Linux filesystems shows that synchronous re-audits are dangerous under CI isolation—incremental scanning is now the expected pattern.
- **State persistence across sessions**: Two separate issues (#4941, #4963) involved settings or session state being silently dropped during startup or crash recovery, indicating a systemic need for more rigorous state-machine testing.
- **Stale UI state for background jobs**: Ghost spinners for dead shell jobs (#4547) persisted for a week before fix, suggesting that job-registry state and transcript rendering need tighter coupling.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/kky-wollu/agents-radar).*
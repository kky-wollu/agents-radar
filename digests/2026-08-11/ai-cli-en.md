# AI CLI Tools Community Digest 2026-08-11

> Generated: 2026-08-10 22:42 UTC | Tools covered: 9

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

# Cross-Tool AI CLI Comparison Report — 2026-08-11

---

## 1. Ecosystem Overview

The AI CLI tool landscape is characterized by intense concurrent development focused on Windows platform reliability, MCP (Model Context Protocol) integration hardening, and the adoption of multi-agent orchestration architectures. Claude Code leads in community engagement and ecosystem maturity, while OpenAI Codex stages the most aggressive internal engineering effort with ~20 merges in 24 hours. Gemini CLI demonstrates the highest community PR contribution rate from external developers. Security safety-filter issues and sandbox correctness are emerging as cross-cutting quality concerns, while persistent gaps in session persistence, context-window management, and subagent reliability dominate user-reported friction across all major tools. The ecosystem is clearly entering an "operational hardening" phase as baseline capabilities stabilize.

---

## 2. Activity Comparison

| Tool | Issues Active | PRs Merged (24h) | Release Status | Notable Metrics |
|------|--------------|-------------------|---------------|-----------------|
| **Claude Code** | 10 featured (205👍 top issue) | 0 merged; 4 open | No new release | Highest single-issue engagement (205 👍); dominated by cybersecurity filter false-positive cluster |
| **OpenAI Codex** | 10 featured (92💬 top issue) | 10 merged | 2 alpha releases | Busiest engine room; sustained Windows stability pressure |
| **Gemini CLI** | 10 featured (P1 bugs dominant) | 6 merged | 1 nightly release | High external contribution ratio; subagent reliability is the top concern |
| **Copilot CLI** | 10 featured (19👍 top request) | 0 merged | v1.0.79 shipped | Enterprise policy model; model catalogue sync issues |
| **Kimi Code** | 1 active (#1283, 31💬) | 0 | No release | Quietest window; 8-month-old memory feature request remains focal |
| **OpenCode** | 10 featured (46💬 top issue) | 10 merged | v1.18.16 shipped | Performance regression is the dominant concern |
| **Pi** | 10 featured (21💬 top issue) | 10 merged/open | No release | WSL Copilot auth remains unsolved after 40+ days |
| **Qwen Code** | 10 featured (P1 bugs identified) | 10 merged | v0.21.9 shipped | Fleet architecture is the headline feature direction |
| **DeepSeek TUI** | 10 featured | 3 (2 merged) | v0.9.6 shipped | Smallest project; compaction and architecture EPICs |

**Summary**: Codex and Qwen Code show the highest merge velocity today. Claude Code and Gemini CLI have the deepest external engagement. Kimi Code is notably dormant in this window.

---

## 3. Shared Feature Directions

| Direction | Tools | Specific Needs |
|-----------|-------|---------------|
| **Windows platform reliability** | Codex, Copilot CLI, Qwen Code, Claude Code | UI freezes (#20214), sandbox ACL corruption (#15777), plugin update failures (#4095), WSL Git misdetection (#35119), terminal rendering regressions — Windows remains the Achilles' heel across all tools |
| **MCP integration hardening** | Codex, Copilot CLI, Gemini CLI | OAuth credential contention (#37866), 60s handshake timeout with no retry (#4421), interim fail-closed policies (#4419), OAuth token refresh with stored client ID (#28481) |
| **Subagent orchestration and observability** | Gemini CLI, Claude Code, Qwen Code, Copilot CLI | False success reports (#22323), recursion depth caps (#5253), per-model rate limiting (#4416), trajectory visibility (#22598), native fleet coordination (#8718) |
| **Context/session persistence** | Claude Code, Kimi Code, OpenCode, Gemini CLI | Memory systems (#1283), draft persistence (#36203), session resume reliability (#4325), manageable context budgets |
| **Configurable context windows** | Codex, DeepSeek TUI, Claude Code | Restore 372k context (#34619), configurable compaction thresholds (#5239), budget-aware context management plugins |
| **Provider model catalogue sync** | Copilot CLI, OpenCode, Qwen Code, DeepSeek TUI | Enabled org models missing (#4390), provider switch leaving stale defaults (#5034), model name silently reset (#8863) |

---

## 4. Differentiation Analysis

| Tool | Primary Focus | Target User | Technical Distinction |
|------|---------------|-------------|----------------------|
| **Claude Code** | Enterprise safety/compliance + IDE integration | High-end professional devs, security-sensitive users | Deep VS Code integration; now-burdened by aggressive cyber safety filters; highest community engagement per issue |
| **OpenAI Codex** | Windows desktop app parity + internal architecture consolidation | Windows-centric developers, enterprise teams | Most aggressive internal refactoring (managed layers v2, MCP credential locks); shipping 2+ alphas daily; sacrificing external contribution opportunities for internal velocity |
| **Gemini CLI** | Subagent reliability + security hardening | Power users with complex multi-agent workflows | Strongest external PR contribution culture (SSRF fixes, Seatbelt sandbox crash prevention); most transparent about P1 bug severity; DeepSeek-style community trust building |
| **Copilot CLI** | Enterprise policy enforcement + GitHub-native workflow | Enterprise organizations with strict governance | Policy-driven model access control (allow-auto-only, proxy enforcement); unique enterprise administration lens; weakest Windows story of all |
| **OpenCode** | Terminal UX + multi-provider OpenCode protocol | TUI enthusiasts, cross-provider users | The "protocol" play: open spec to allow any model/tool to drive the terminal; V2 core introduces cleaner abstractions; community concerned about performance regression |
| **Pi** | Rust-based terminal purity + markdown-native UX | Low-resource terminal users clinging to tmux/SSH workflows | Zero-abstraction approach (Bash, TUI, no deps); strongest for non-Kitty terminal resistance (Alt+Enter fix); community contribution culture producing 10 PRs in 24h |
| **Qwen Code** | Multi-agent fleets + web shell as management surface | Large-scale automation, team administration | First-class fleet architecture (leader dispatches workers, correlates state); Web Shell as a team management surface; fastest feature velocity this cycle |
| **DeepSeek TUI** | Compact, provider-agnostic terminal experience | Solo devs needing multi-provider coverage | Smallest scope but thoughtful ("subtractive release" philosophy); EPIC-005 crate decomposition signals maintainability investment |

---

## 5. Community Momentum & Maturity

**Highest Momentum:**
- **Qwen Code** — Multiple architecture-defining RFCs (#8718) with staged implementation sprints; fastest pace from proposal to code (fleet MVP open for implementation within weeks)
- **OpenAI Codex** — 10 PRs merged in 24h across MCP, Windows sandbox, and managed configuration — deepest engineering velocity of all tools

**Most Mature Communities:**
- **Claude Code** — 205 upvotes on a single IDE-feature request signals refined, high-engagement community; the cybersecurity filter cluster (20+ related issues) shows both the community's willingness to file reports and the tool's friction with security-sensitive workflows
- **Gemini CLI** — External contributors shipping security fixes (SSRF), cross-platform fixes (macOS Seatbelt), and eval infrastructure — a strong indicator of community health and maintainer trust

**Rapidly Growing/Stabilizing:**
- **Pi** — An active community contributing 10 PRs in 24h to address terminal UX, protocol compliance, and provider parity issues — a healthy contribution culture that speeds up even with a small core team

**Concerning Signals:**
- **Kimi Code** — Only 1 issue active in 24h and an 8-month-old memory-feature request with no implementation progress — the least active tool in this window; risks community atrophy
- **Copilot CLI** — Model catalogue inconsistency issues and a model-access outage cluster (Claude models being reported as disabled) point to user trust challenges
- **OpenCode** — A 46-comment CPU regression undermines community trust; the maintainer's "auto-close" of a splash-disable request suggests filtering of feedback

---

## 6. Trend Signals

**Operational Hardening is the Default Phase** — The top issues across all tools are no longer feature requests but reliability concerns: Windows stability, session persistence, compaction correctness, subagent orchestration failures. Users are hitting the limits of current infrastructure — the next generation of tool differentiation will come from engineering polish, not feature sets.

**Security Filtering is the Biggest Friction Point** — Claude Code's cyber-safety filter false-positive cluster (20+ reports) is the starkest signal: overly-broad security filtering interferes with legitimate security work. Expect a push toward context-aware safety classifiers and a retreat from keyword-based blocking.

**Subagent Orchestration is the Critical Innovation Frontier** — Gemini CLI's P1 subagent reliability bugs and Qwen Code's fleet architecture RFC signal that orchestration (multi-agent coordination, trajectory visibility, rate-limit handling) is the feature area with the most room for meaningful differentiation through quality.

**Windows Support is a Market-Share Battlefront** — Codex's Windows issues (#20214, #15777), Copilot CLI's plugin update failures, and Qwen Code's terminal flicker all demonstrate that Windows compatibility remains unsolved and is costing user retention. This is a major opportunity for any tool that can ship a truly stable Windows experience.

**MCP Maturity is the Integration Standard** — All major tools are investing in MCP hardening concurrently: OAuth credential handling, handshake timeouts, configuration semantics. Expect MCP — not proprietary APIs — to become the de facto integration standard for AI-cli tools. Ecosystem-wide investment signals interoperability is a priority, not an afterthought.

**Compliance Controls Emerge as Enterprise Gatekeepers** — Copilot CLI's enterprise policy support (allow-auto-only, proxy enforcement) and Claude Code's security filters are early signals that enterprise governance is becoming a *core* featureset — not just a configuration option. Tools that succeed in bridging developer speed with compliance controls will win enterprise adoption.

---

*Report generated from community activity as of 2026-08-11. Data drawn from the top issues, PRs, and releases for each tool's repository.*

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
*Data as of 2026-08-11 | Source: github.com/anthropics/skills*

---

## 1. Top Skills Ranking

### #1 — skill-creator Bug Fixes: `run_eval.py` Recall=0% Fix (#1298)
**Status:** Open | Author: MartinCajiao | Created: 2026-06-10
[GitHub PR #1298](https://github.com/anthropics/skills/pull/1298)

The most activity-generating PR cluster targets the `skill-creator`'s evaluation pipeline. This PR fixes the critical bug where `run_eval.py` always reports 0% recall, rendering the description-optimization loop useless (root cause #556 — 10+ independent reproductions). The fix installs the eval artifact as a real skill, addresses Windows stream reading, trigger detection, and parallel worker issues. **Discussion highlights:** This is the culmination of a month-long effort; multiple parallel PRs (#1099, #1050, #1323, #1261) address the same core issue from different angles.

---

### #2 — document-typography Skill (#514)
**Status:** Open | Author: PGTBoos | Created: 2026-03-04
[GitHub PR #514](https://github.com/anthropics/skills/pull/514)

Typographic quality control for generated documents: prevents orphan word wrap, widow paragraphs, and numbering misalignment — issues affecting every AI-generated document. **Discussion highlights:** Community members confirm these typographic flaws affect their real workflows; the fix targets a high-frequency pain point in AI output quality.

---

### #3 — ODT Skill for OpenDocument Format (#486)
**Status:** Open | Author: GitHubNewbie0 | Created: 2026-03-01
[GitHub PR #486](https://github.com/anthropics/skills/pull/486)

Full OpenDocument support: create, fill, read, and convert `.odt`/`.ods` files with HTML conversion. **Discussion highlights:** Complements the existing `docx` and `pdf` skills; addresses enterprise demand for LibreOffice/ISO-standard document compatibility.

---

### #4 — frontend-design Skill Clarity Improvement (#210)
**Status:** Open | Author: justinwetch | Created: 2026-01-05
[GitHub PR #210](https://github.com/anthropics/skills/pull/210)

Revises the frontend-design skill for clarity, actionability, and internal coherence — ensuring every instruction is executable in a single conversation. **Discussion highlights:** Community feedback emphasizes that skills read like documentation rather than operational instructions; this PR directly addresses that fundamental issue.

---

### #5 — testing-patterns Skill (#723)
**Status:** Open | Author: 4444J99 | Created: 2026-03-22
[GitHub PR #723](https://github.com/anthropics/skills/pull/723)

Comprehensive testing skill covering philosophy (Testing Trophy model), unit testing (AAA pattern, naming, edge cases), and React component testing (Testing Library patterns). **Discussion highlights:** One of the most anticipated skill additions — community demand for test generation patterns is consistently high.

---

### #6 — self-audit: Mechanical Verification + Reasoning Quality Gate (#1367)
**Status:** Open | Author: YuhaoLin2005 | Created: 2026-06-28
[GitHub PR #1367](https://github.com/anthropics/skills/pull/1367)

Audits AI output before delivery: mechanical file verification first, then four-dimension reasoning audit in damage-severity priority order. Works with any project, stack, or model. **Discussion highlights:** Represent an emerging demand for quality gates and safety patterns; the companion issue (#1385) extends this to a three-gate pipeline.

---

### #7 — PYXEL Retro Game Development Skill (#525)
**Status:** Open | Author: kitao | Created: 2026-03-05
[GitHub PR #525](https://github.com/anthropics/skills/pull/525)

Skill for [pyxel-mcp](https://github.com/kitao/pyxel-mcp), an MCP server for the Pyxel retro/pixel-art game engine. Covers write → run_and_capture → inspect → iterate workflow. **Discussion highlights:** Notable for being an MCP-integrated skill — signals growing convergence between Skills and MCP ecosystems.

---

### #8 — skill-quality-analyzer & skill-security-analyzer Meta-Skills (#83)
**Status:** Open | Author: eovidiu | Created: 2025-11-06
[GitHub PR #83](https://github.com/anthropics/skills/pull/83)

Two meta-skills: quality analyzer (evaluates structure, documentation, examples across 5 dimensions) and security analyzer. **Discussion highlights:** Directly responds to the security trust-boundary concerns raised in Issue #492; represents the community's self-policing impulse.

---

## 2. Community Demand Trends

| Trend | Evidence | Demand Level |
|-------|----------|--------------|
| **skill-creator tooling reliability** | Issues #556, #1169 (12 + 3 comments), 5+ parallel fix PRs | 🟥 **Critical** — blocks all other skill development |
| **Security & trust boundaries** | Issue #492 (43 comments, highest activity) — namespace impersonation concerns | 🟥 **Critical** |
| **Org-wide skill sharing** | Issue #228 (16 comments, 8 👍) — direct sharing, skill libraries | 🟥 **High** |
| **Document format expansion** | ODT (#486), typography (#514), docx fixes (#541, #12) | 🟥 **High** |
| **Testing & quality assurance** | testing-patterns (#723), self-audit (#1367), quality gates (#1385) | 🟧 **Growing** |
| **Duplicate/conflicting skill plugins** | Issue #189 (6 comments, 9 👍) — `document-skills` and `example-skills` install identical content | 🟧 **Moderate** |
| **Context window management** | Issue #1487 — `claude-api` skill injects ~156k tokens in one call | 🟧 **Moderate** |
| **Enterprise integration** | SAP predictor (#181), SharePoint security (#1175), Bedrock support (#29) | 🟧 **Moderate** |

---

## 3. High-Potential Pending Skills

| Skill | PR | Description | Potential Impact |
|-------|-----|-------------|------------------|
| **plan-file-hygiene** | [#1479](https://github.com/anthropics/skills/pull/1479) | Addresses lifecycle gap: planning artifacts accumulate with no governance; credit to community co-design process | High — solves a ubiquitous workflow problem |
| **color-expert** | [#1302](https://github.com/anthropics/skills/pull/1302) | Color naming systems (ISCC-NBS, Munsell, RAL), color-space selection tables, self-contained expertise | Medium — niche but well-scoped |
| **compact-memory** | Issue [#1329](https://github.com/anthropics/skills/issues/1329) | Symbolic notation for compact agent state; reduces context waste from prose memory | High — directly addresses context window pressure |
| **testing-patterns** | [#723](https://github.com/anthropics/skills/pull/723) | Full testing stack coverage — philosophy, unit, React components | High — matches critical demand |
| **self-audit** | [#1367](https://github.com/anthropics/skills/pull/1367) | Mechanical + reasoning quality gate before delivery | High — emerging quality-gate trend |

---

## 4. Skills Ecosystem Insight

The community's most concentrated demand is for **reliable skill-creator tooling and evaluation infrastructure** — with 5+ parallel PRs and 15+ comments converging on the same `run_eval.py` recall=0% bug — followed closely by an urgent push for **trust-boundary security** (43 comments) and **organizational skill sharing** that treats Skills as first-class, governable assets rather than standalone files.

---

# Claude Code Community Digest — 2026-08-11

## Today's Highlights

The community is actively discussing a highly-requested VS Code enhancement for controlling auto-attach behavior, alongside a significant cluster of cybersecurity safety-filter false positives reported by a single user across multiple sessions. Two open pull requests aim to expand platform support and update model references, while no new releases were published in the past 24 hours.

## Releases

No new releases were published in the last 24 hours.

## Hot Issues

1. **[#24726 — VS Code extension: add setting to disable auto-attach of open file/selection](https://github.com/anthropics/claude-code/issues/24726)** · 66 comments · 205 👍
   The most-engaged issue this cycle, with strong community support for a configurable option to control auto-attachment behavior in the VS Code extension — indicates growing demand for finer-grained IDE integration control.

2. **[#69238 — No response from API error when Advisor is triggered on macOS](https://github.com/anthropics/claude-code/issues/69238)** · 61 comments · 95 👍
   A macOS-specific TUI/API bug where the Advisor feature triggers indefinite "No response from API" retries (up to 2m25s), severely disrupting workflows for Sonnet users. High visibility suggests broad impact.

3. **[#83028 — Claude Desktop MSIX crash on Intel integrated GPU during browser pane use](https://github.com/anthropics/claude-code/issues/83028)** · 4 comments
   A reproducible crash affecting Intel iGPU users when using the browser pane — no workaround available, highlighted as a release-blocking concern for affected hardware.

4. **[#71230 — Remote execution sandbox blocks git clone to github.com, breaking pip install of git+https dependencies](https://github.com/anthropics/claude-code/issues/71230)** · 3 comments · 1 👍
   Sandboxing overly restricts network access, breaking legitimate development workflows for projects relying on git-based Python dependencies in Claude Code Web.

5. **[#71123 — Cyber safeguard wrongly blocks benign session-resume greeting](https://github.com/anthropics/claude-code/issues/71123)** · 3 comments
   Part of a large cluster (20+ related issues from user `sworrl`) documenting false positives where routine continuation prompts and authorized security work trigger AUP blocks, significantly hindering legitimate defensive operations.

6. **[#71206 — Authorized security workspace review blocked before scoping](https://github.com/anthropics/claude-code/issues/71206)** · 3 comments
   Highlights a systemic issue: legitimate security audits and incident-response tasks are being blocked by overly-aggressive cyber-content filtering, with requests for exemptions required via a separate form.

7. **[#71076 — Safety filter blocks setting up RustDesk remote-desktop session to owned workstation](https://github.com/anthropics/claude-code/issues/71076)** · 3 comments
   A routine IT administration action (remote desktop to a managed endpoint) flagged as a cybersecurity concern — indicative of keyword-based false positives on common operational terms.

8. **[#71070 — Safety filter blocked drafting a GitHub issue title reporting over-broad cybersecurity block](https://github.com/anthropics/claude-code/issues/71070)** · 3 comments
   Notable for the irony: the filter blocked a request to *report* the filter's own false-positive behavior, keying on cybersecurity terminology rather than actual intent.

9. **[#71241 — Cloud IAM tenant security audit wrongly blocked](https://github.com/anthropics/claude-code/issues/71241)** · 3 comments
   Even benign defensive administration (enumerating admin roles, app credentials, OAuth consent grants) on owned infrastructure triggers blocks — a recurring pattern in the false-positive cluster.

10. **[#71068 — Plain greeting resuming authorized security-tooling work wrongly blocked](https://github.com/anthropics/claude-code/issues/71068)** · 3 comments
   Even simple greetings ("HELLO!?") in established authorized sessions get flagged, suggesting the classifier may be context-blind and excessively sensitive to topic vocabulary.

## Key PR Progress

1. **[#34951 — feat: automatic GitHub/GitLab detection and GitLab support for /code-review](https://github.com/anthropics/claude-code/pull/34951)** · Open
   Adds multi-platform support to `/code-review` with automatic platform detection, addressing issue #26932. Would eliminate duplicated logic across Git hosting platforms.

2. **[#85409 — security-guidance: update default model refs from Opus 4.7/Sonnet 4.6 to Opus 5/Sonnet 5](https://github.com/anthropics/claude-code/pull/85409)** · Open
   Updates hardcoded model references in the `security-guidance` plugin's README and hook code to current models, critical for users relying on up-to-date defaults.

3. **[#85464 — plugins: add entroly-context for budget-aware context management](https://github.com/anthropics/claude-code/pull/85464)** · Closed/merged
   New community plugin for budget-aware context selection when codebases exceed context windows — addresses a frequent pain point for large-repo users.

4. **[#9262 — docs: enforce task tool and model metadata](https://github.com/anthropics/claude-code/pull/9262)** · Closed
   Documentation improvement requiring the Task tool in commit workflows for context isolation, and documenting the `claude-3-5-haiku-latest` model — minor but useful for workflow correctness.

## Feature Request Trends

- **IDE integration control**: The leading request (205 👍) is for VS Code settings to control auto-attach behavior, signaling users want more granular control over how their IDE context flows into Claude Code sessions.
- **Multi-platform support**: PR #34951 targeting GitLab support for `/code-review` highlights demand for broader Git platform compatibility beyond GitHub.
- **Model currency**: PR #85409 updating model references suggests users expect plugins to track new model releases closely and default to the latest capable models.
- **Context budget management**: The entroly-context plugin and related discussions show interest in smarter handling of large codebases that exceed context windows.

## Developer Pain Points

- **Cybersecurity filter false positives (dominant theme)**: The largest cluster of activity centers on the real-time AUP/cyber safeguards blocking legitimate defensive security work — authorized audits, incident response, remote desktop sessions, and even greetings in established sessions. Users report having to apply for manual exemptions, which breaks workflow continuity. This is the #1 friction point this cycle.
- **API reliability on macOS**: The Advisor-triggered "No response from API" error with long retry delays disrupts TUI users, with 61 comments and 95 reactions indicating broad impact.
- **Sandbox network restrictions**: Blocking `git clone` to GitHub in the remote execution sandbox breaks standard Python dependency installation flows — a surprising footgun for web-based workflows.
- **Hardware-specific crashes**: The Intel iGPU crash in Claude Desktop MSIX with no workaround leaves affected users stuck, a regression-quality issue.
- **Duplicate reporting friction**: The sheer volume of `sworrl`'s near-identical false-positive reports (all marked duplicate) suggests users feel the need to file repeated issues to escalate, which may indicate a lack of responsive triage channels for enforcement problems.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-08-11

## Today's Highlights

The Codex team shipped two alpha releases (0.148.0-alpha.6, 0.147.0-alpha.6.6) alongside a dense batch of ~20 merges focused on Windows sandbox correctness, MCP OAuth credential handling, and managed-config migration. The community's attention remains heavily concentrated on Windows platform reliability, with the long-running freezes issue (#20214) crossing 90 comments, and a new report of the unified ChatGPT app's scrolling behavior arriving yesterday. Internally, the multi-PR migration from legacy `enterprise_managed` bundles to the v2 `managed_layers` cache is now fully merged.

## Releases

Two alpha releases were published in the last 24 hours, both with no detailed changelog text provided:

- **rust-v0.148.0-alpha.6** — [Release](https://github.com/openai/codex/releases/tag/rust-v0.148.0-alpha.6)
- **rust-v0.147.0-alpha.6.6** — [Release](https://github.com/openai/codex/releases/tag/rust-v0.147.0-alpha.6.6)

## Hot Issues

1. **[#20214 — Codex App freezes/stutters on Windows 11 Pro](https://github.com/openai/codex/issues/20214)** (92 comments, 81 👍)
   The most-engaged open issue by far. Users report persistent UI freezes despite ample hardware (Ryzen 5, 32 GB). The comment count has grown daily for months, signaling a top-priority Windows stability problem with no fix in sight.

2. **[#30009 — apply_patch fails with Windows sandbox error](https://github.com/openai/codex/issues/30009)** (33 comments, 11 👍)
   File edits through `apply_patch` break specifically on Windows sandbox environments. The issue has been open for six weeks and remains unlabeled with a fix, making it one of the more painful Windows-only blockers.

3. **[#17320 — Excessive SQLite WAL writes during streaming from TRACE logs](https://github.com/openai/codex/issues/17320)** (30 comments, 39 👍)
   High community agreement on a performance bug: TRACE-level logging ignores `RUST_LOG` and causes excessive SQLite WAL churn during streaming. Users report I/O amplification and degraded IDE performance.

4. **[#15777 — Sandbox installation corrupts ACL on AppData](https://github.com/openai/codex/issues/15777)** (27 comments, 2 👍)
   On Windows, installing Codex corrupts AppData ACLs, breaking other applications. This long-standing issue (since March) has relatively few upvotes but a serious blast radius.

5. **[#35119 — WSL repositories marked as non-Git, "Git is unavailable"](https://github.com/openai/codex/issues/35119)** (19 comments, 16 👍)
   Regression in 26.721.3404: valid WSL ext4 repos are misdetected as non-Git. Users report the previous package version worked fine, pointing to an app-server change as the root cause.

6. **[#37013 — Windows Computer Use reuses stale node_repl exec context](https://github.com/openai/codex/issues/37013)** (17 comments, 4 👍)
   Computer Use works only within the first JS execution; subsequent `node_repl/js` calls reuse a stale transport and fail. A significant blocker for Windows automation workflows.

7. **[#34619 — Restore GPT-5.6 Sol's 372k Codex context window](https://github.com/openai/codex/issues/34619)** (5 comments, 18 👍)
   Strong upvote-to-comment ratio. Users are unhappy about the reduced effective context window and are requesting either restoration or a configurable opt-in. The high 👍 count suggests broader silent support.

8. **[#31946 — 1,360 Node processes consume 41 GB on macOS](https://github.com/openai/codex/issues/31946)** (3 comments)
   MCP/Node lifecycle failure escalates to system-wide outages, hanging WindowServer within 20 minutes of restart. A low-comment but severe reliability issue related to #30408.

9. **[#37383 — Computer Use on Windows fails with 0x80070003](https://github.com/openai/codex/issues/37383)** (13 comments, 4 👍)
   App/window discovery fails during Computer Use on Windows 11. Another data point in the pattern of Windows Computer Use being substantially less stable than macOS.

10. **[#12498 — Codex Cloud loses Git remote, references 'work' workspace only](https://github.com/openai/codex/issues/12498)** (11 comments, 7 👍)
    Users report Codex Cloud unexpectedly stops recognizing Git remotes mid-session. The issue has persisted for months, hinting at a difficult-to-reproduce cloud-side state bug.

## Key PR Progress

1. **[#37891 — Use thread configuration for `app/read`](https://github.com/openai/codex/pull/37891)** — Merged
   Adds `threadId` parameter to `app/read` so feature gating and policy respect per-thread configuration rather than global defaults.

2. **[#37889 — Ignore Unix socket proxy settings on Windows](https://github.com/openai/codex/pull/37889)** — Merged
   Prevents macOS-only Unix socket proxy permissions from clamping Windows proxy listeners to loopback and emitting spurious warnings.

3. **[#37867 — Reject duplicate resolved paths in apply_patch](https://github.com/openai/codex/pull/37867)** — Merged
   Rejects patches targeting the same file via aliased paths (e.g., `duplicate.txt` and `./duplicate.txt`), closing a correctness hole directly relevant to the Windows issue #30009.

4. **[#37866 — Add MCP OAuth credential contention regression tests](https://github.com/openai/codex/pull/37866)** — Merged
   Covers non-blocking credential probes when the file/secrets store is locked, including recovery after lock release — solid hardening for concurrent MCP usage.

5. **[#37864 — Support MCP form input in full-access user threads](https://github.com/openai/codex/pull/37864)** — Merged
   Enables `openai/standard-form-input` in auto-approved sessions, allowing user-entered values to be requested for MCP forms even when tool permissions are pre-approved.

6. **[#37860 — Speed up MCP OAuth credential reads](https://github.com/openai/codex/pull/37860)** — Merged
   Probes credential stores without waiting on locks during runtime refreshes, preventing async-executor stalls when another process holds the lock.

7. **[#37851 — Route intercepted exec approvals through shared review](https://github.com/openai/codex/pull/37851)** — Merged
   Unix `execve` approvals intercepted by the zsh fork now go through the standard approval pipeline (permission hooks, Guardian, user prompts, telemetry).

8. **[#37878 — Add configurable goal token budget limits](https://github.com/openai/codex/pull/37878)** — Merged
   Adds `goals.max_goal_token_budget` configuration with validation, and rejects invalid budgets — useful for teams running Codex with bounded resource usage.

9. **[#37875 — Honor configured Windows sandbox level for managed networking](https://github.com/openai/codex/pull/37875)** — Merged
   Managed networking now selects the sandbox backend based on `WindowsSandboxLevel` instead of implicitly choosing the elevated backend — a fix aligned with several open Windows sandbox complaints.

10. **[#31288 / #31315 — Managed layers v2 cache migration (4/5 and 5/5)](https://github.com/openai/codex/pull/31288)** — Merged
    Completes the cutover from legacy `enterprise_managed` bundles to `managed_layers` with v2 cache semantics. The stacked series (PRs #31286, #31287, #31288, #31315) removes legacy lanes wholesale.

## Feature Request Trends

- **Context window control** (#34619): Users want the ability to toggle or restore the 372k context window for GPT-5.6 Sol rather than accepting a reduced default. The 18 upvotes on a 5-comment thread indicate strong silent demand.
- **Public issue backlog index** (#37873): A community member created a frozen, triaged index of all 11,813 open issues to help maintainers and contributors navigate duplicates — a grassroots response to perceived triage slowness.
- **Windows sidebar hover control** (#33362): Users want an opt-out for hover-triggered sidebar reveal, which interrupts flow and is easily triggered accidentally.
- **Custom model provider compatibility** (#37122): Requests for `model_providers` to accept the standard OpenAI `/models` list format instead of requiring an undocumented internal schema, broadening compatibility with vLLM, llama.cpp, and LiteLLM.

## Developer Pain Points

- **Windows remains the most fragile platform**: The top issues span UI freezes (#20214), sandbox ACL corruption (#15777), WSL Git misdetection (#35119), Computer Use failures (#37013, #37383), and DWM handle leaks (#33192). Windows-specific bugs account for the majority of both the highest-traffic and highest-severity threads.
- **Computer Use on Windows is effectively unreliable**: Three separate Windows Computer Use issues (#37013, #37383, #36645) describe failures at different stages (execution context, window discovery, session teardown). This capability appears far from production-ready on Windows.
- **MCP OAuth / re-authentication loops**: Two issues (#37219, #37549) describe clients repeatedly requesting Linear MCP access after it's already been granted. The merged credential-locking fixes (#37860, #37866) are a direct response, but the reports suggest a lingering UX trust problem.
- **Process/resource leaks**: Reports of uncontrolled process fleets (#31946: 1,360 Node processes, 41 GB) and sustained 100%+ CPU after large-thread opens (#25251) indicate lifecycle-management gaps that can take down entire dev machines.
- **Silent context/configuration regressions**: Both #12498 (Codex Cloud losing Git remotes) and #34619 (reduced context window) reflect user frustration when Codex changes behavior without clear explanations or opt-outs.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-08-11

## Today's Highlights

The Gemini CLI project continues to ship nightly releases (v0.56.0-nightly.20260810) with a steady stream of community-contributed PRs focused on security hardening—including an SSRF fix for the web-fetch tool and macOS Seatbelt sandbox crash prevention. On the issue tracker, the community's most vocal concerns center on **subagent reliability**: a P1 bug where subagents falsely report GOAL success after hitting MAX_TURNS, and a long-standing P1 where the generalist agent hangs indefinitely on simple tasks. A notable new PR trend is the influx of dependency updates (ws, js-yaml, puppeteer-core, execa) alongside substantive fixes for OAuth flows in Cloud Workstations and IDE connection issues.

## Releases

- **[v0.56.0-nightly.20260810.gcf22ac7e8](https://github.com/google-gemini/gemini-cli/compare/v0.56.0-nightly.20260809.gcf22ac7e8...v0.56.0-nightly.20260810.gcf22ac7e8)** — Nightly release; no user-facing changelog details provided beyond the automated version bump.

## Hot Issues

**1. [Subagent recovery after MAX_TURNS is reported as GOAL success, hiding interruption (#22323)](https://github.com/google-gemini/gemini-cli/issues/22323)** — P1 bug where `codebase_investigator` subagent reports `status: "success"` and `Termination Reason: "GOAL"` even after hitting the max turn limit before doing any analysis. The community flagged this as deeply misleading—a 12-comment thread with maintainer attention. The core problem: users believe the agent completed its work when it actually ran out of turns.

**2. [Generalist agent hangs (#21409)](https://github.com/google-gemini/gemini-cli/issues/21409)** — P1 bug with 8 👍 reactions. Users report the generalist agent hangs indefinitely on simple tasks (folder creation) when deferred to. A user workaround exists (instructing the model not to defer), but this remains a top reliability concern.

**3. [Shell command execution gets stuck with "Waiting input" (#25166)](https://github.com/google-gemini/gemini-cli/issues/25166)** — P1 bug where the CLI hangs after completing simple shell commands, showing them as "Awaiting user input" despite completion. 3 👍 reactions suggest this is affecting multiple developers.

**4. [Subagents running without permission since v0.33.0 (#22093)](https://github.com/google-gemini/gemini-cli/issues/22093)** — Users report subagents executing despite agents being disabled in all configurations. This is a consent/safety concern that could have serious implications for users with strict permission requirements.

**5. [Browser subagent fails in Wayland (#21983)](https://github.com/google-gemini/gemini-cli/issues/21983)** — Browser automation fails under Wayland display servers, limiting functionality for Linux users. Part of the "need-retesting" queue.

**6. [Gemini does not use skills and sub-agents enough (#21968)](https://github.com/google-gemini/gemini-cli/issues/21968)** — Despite custom skills and sub-agents being defined, the model rarely uses them autonomously. The community notes it only uses them when explicitly instructed.

**7. [Browser Agent ignores settings.json overrides (#22267)](https://github.com/google-gemini/gemini-cli/issues/22267)** — The Browser Agent doesn't respect configuration overrides like `maxTurns` from `settings.json`, making it unpredictable in constrained environments.

**8. [Auto Memory retries low-signal sessions indefinitely (#26522)](https://github.com/google-gemini/gemini-cli/issues/26522)** — The Auto Memory system can loop forever on sessions it decides not to process, potentially causing wasted API calls and resource consumption.

**9. [Agent should stop/discourage destructive behavior (#22672)](https://github.com/google-gemini/gemini-cli/issues/22672)** — Community request for the agent to avoid `git reset`, `--force`, and destructive DB operations when safer alternatives exist. This is a recurring theme across multiple issues.

**10. [Model frequently creates tmp scripts in random spots (#23571)](https://github.com/google-gemini/gemini-cli/issues/23571)** — When shell execution is restricted, the model writes multiple edit scripts across directories creating workspace cleanup overhead—a UX frustration for developers maintaining clean commits.

## Key PR Progress

**1. [fix(core): dynamically resolve Cloud Workstations proxy redirect URI for OAuth flows (#28688)](https://github.com/google-gemini/gemini-cli/pull/28688)** — Fixes OAuth 2.0 failures in Google Cloud Workstations VMs by dynamically resolving the proxy redirect URI instead of hardcoding `localhost`. Critical for developers using remote dev environments.

**2. [fix(core): resolve swallowed directory mismatch in IDE connections (#28729)](https://github.com/google-gemini/gemini-cli/pull/28729)** — Fixes IDE companion extension connection failures under Cider and VS Code fork/remote setups with differing FUSE or directory paths.

**3. [fix: resolve SSRF vulnerability in web-fetch.ts by using async DNS resolution (#28557)](https://github.com/google-gemini/gemini-cli/pull/28557)** — Addresses a security vulnerability where hostnames resolving to internal IPs (e.g., `169.254.169.254`) bypassed the existing `isBlockedHost` sync check. Uses the existing `isPrivateIpAsync` utility.

**4. [fix(core): handle EACCES in resolveToRealPath to prevent sandbox crash (#28734)](https://github.com/google-gemini/gemini-cli/pull/28734)** — Prevents CLI crash on startup when macOS Seatbelt sandboxing is enabled and CWD is inside a Git repository—an important fix for macOS users with strict sandboxing.

**5. [fix(core): resolve false model capacity exhaustion and fix core quota lookup model mapping (#28730)](https://github.com/google-gemini/gemini-cli/pull/28730)** — Fixes false capacity exhaustion errors and preserves the "Keep trying" UI option during transient capacity surges.

**6. [fix(core,cli): refresh MCP OAuth tokens with the stored client ID (#28481)](https://github.com/google-gemini/gemini-cli/pull/28481)** — Fixes MCP OAuth token refresh when configured via OAuth discovery + dynamic client registration. Previously, refresh failed and deleted stored credentials, forcing re-auth.

**7. [fix(core): prevent boolean thought parts leaking as [Thought: true] text (#28624)](https://github.com/google-gemini/gemini-cli/pull/28624)** — Prevents internal thought parts with boolean `thought: true` from appearing as literal "[Thought: true]" text in model outputs—fixes a confusing display bug.

**8. [feat(evals): add tool call formatter and integrate failure summaries (#28305)](https://github.com/google-gemini/gemini-cli/pull/28305)** — Adds tool-call timeline formatting and failure summary diagnostics to behavioral evaluations. When an eval fails, the runner prints a numbered timeline of tool calls with status/error details.

**9. [fix: replace console.error with debugLogger in sdk session (#28613)](https://github.com/google-gemini/gemini-cli/pull/28613)** — Small but meaningful cleanup aligning SDK session logging with project standards.

**10. [Feat/eval validate (#28344)](https://github.com/google-gemini/gemini-cli/pull/28344)** — Adds `eval:validate` static analysis command validating eval source files against 9 rules, exiting with code 1 on violations for CI gating.

## Feature Request Trends

- **AST-aware tooling for file reads and codebase mapping** (e.g., #22745, #22746): Multiple EPICs explore whether AST-aware file reads/search could reduce token noise and improve method-bound precision. Tools like `tilth` and `glyph` are suggested as starting points.
- **Zero-dependency OS sandboxing** (#19873): Leveraging Gemini 3's native bash affinity with safe, zero-dependency POSIX sandboxing to improve security without degrading the agent's preferred workflows.
- **Subagent trajectory visibility** (#22598): Ability to view and share subagent trajectories via `/chat share` for better debugging and evaluation.
- **Component-level behavioral evaluations** (#24353): Expanding the existing 76 behavioral eval tests to more Gemini model versions—shows ongoing investment in eval infrastructure.
- **Agent "self-awareness"** (#21432): Making the CLI understand its own mechanics—hotkeys, flags, capabilities—to serve as its own expert guide for users.

## Developer Pain Points

1. **Subagent reliability and transparency**: The dominant theme in this digest. Issues around false success reports (#22323), hangs (#21409), unsolicited subagent use (#22093), and lack of trajectory visibility (#22598) suggest the subagent orchestration layer needs significant hardening and better observability.

2. **Shell execution hangs and interactive prompt deadlocks**: Multiple reports of the CLI getting stuck—"Waiting input" after completion (#25166), sticking at interactive prompts for `vite` creation (#22465), and getting stuck creating files in general.

3. **Configuration not respected**: Browser Agent ignoring `settings.json` overrides (#22267), subagents running despite disabled agents (#22093) — users expect their explicit configuration to be honored and are frustrated when it isn't.

4. **Browser automation fragility**: Failures on Wayland (#21983), locked browser profile failures (#22232)—fewer comments but recurring issues suggest browser automation remains a rough edge across platforms.

5. **Security and permission concerns**: Requests for deterministic redaction in Auto Memory (#26525), prevention of destructive commands (#22672), and SSRF fixes (#28557) reflect a community increasingly focused on agent safety and trustworthy behavior.

6. **Memory system quality**: Multiple issues from SandyTao520 (#26516, #26522, #26523, #26525) tracking memory system bugs—indefinite retries, invalid patch quarantine, and logging concerns—suggest the Auto Memory system is maturing but still has rough edges.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest
**2026-08-11**

---

## Today's Highlights

The Copilot CLI shipped v1.0.79 with improved sandbox configuration visibility and new enterprise policy support, though a growing cluster of model-access issues (particularly around Claude models being reported as disabled) is drawing community attention. Enterprise users are reporting sporadic policy blocking on model retrieval and a rapid-fire series of new issues around MCP server stability and session reliability. Notably, a Windows plugin update bug is gaining traction with **13 👍**, suggesting meaningful developer friction.

---

## Releases

**v1.0.79** (2026-08-10) — [View Release](https://github.com/github/copilot-cli/releases)

- **Sandbox config visibility**: The `/sandbox` configuration dialog now shows where sandbox settings are stored in `settings.json`
- **Enterprise policy support**: Added support for the enterprise `allow-auto-only` policy, enabling `/allow-all auto` while full allow-all remains blocked
- **Proxy enforcement**: Enterprise-managed sandbox policy can now enforce a proxy URL while credentials are being handled

---

## Hot Issues

1. **[#1595 — Sporadic policy blocking issue retrieving models](https://github.com/github/copilot-cli/issues/1595)** *(👍 11, 💬 29)*
   Enterprise users with valid subscriptions and ~40% premium requests remaining get "access denied by Copilot policy" when listing models via `/models`. Long-running issue (since February) with significant engagement — suggests an ongoing enterprise policy enforcement problem.

2. **[#4095 — Windows plugin update fails with "Access is denied (os error 5)"](https://github.com/github/copilot-cli/issues/4095)** *(👍 13)*
   Plugin updates fail when VS Code is running because the Copilot extension holds watcher handles on `installed-plugins`. High community resonance (13 👍) for a Windows-specific workflow blocker.

3. **[#2904 — Custom Agent YAML should support reasoning effort](https://github.com/github/copilot-cli/issues/2904)** *(👍 19)*
   Custom agents (`.agent.md`) can pin a model but cannot set per-agent reasoning effort — only global flags exist. Strong demand (19 👍) for granular control.

4. **[#4422 — All Claude models disabled under CLI model selection](https://github.com/github/copilot-cli/issues/4422)** *(new, 1 👍)*
   User reports a sudden outage: Claude models (sonnet 5, 4.8) are unavailable even though they appear enabled in org settings. Rollback didn't fix it — suggests server-side change.

5. **[#4390 — Enabled organization models missing from catalogue](https://github.com/github/copilot-cli/issues/4390)** *(👍 3)*
   Claude Sonnet 5/Opus 5 and Kimi K3 models are missing from the CLI catalogue despite being explicitly enabled by a Copilot Business org. Related to #4422, pointing to a broader model-catalogue sync problem.

6. **[#4416 — Parallel explore subagent fan-out dies to per-model 429s](https://github.com/github/copilot-cli/issues/4416)** *(new)*
   Launching many subagents with the task tool concentrates all calls on `claude-haiku-4.5`, hitting tight per-model rate limits. No backoff or auto-switching despite `eligibleForAutoSwitch` being set.

7. **[#4419 — Managed-settings interim fail-closed drops user MCP servers](https://github.com/github/copilot-cli/issues/4419)** *(new)*
   During managed-settings resolution, the CLI installs an empty allow-list (`[[]]`) that permanently rejects any user MCP server registering during that window. Reproduces even with no managed policy configured.

8. **[#4421 — MCP initialize handshake fixed 60s budget, no retry](https://github.com/github/copilot-cli/issues/4421)** *(new)*
   The MCP handshake has a hard-coded 60-second budget. On timeout, the server is never respawned for the session — no retry, no backoff. `npx`-launched stdio servers fail ~29% of sessions.

9. **[#4325 — Session unloadable when events.jsonl exceeds V8 max string length](https://github.com/github/copilot-cli/issues/4325)** *(closed)*
   Long-lived sessions become permanently unresumable once `events.jsonl` grows past V8's string limit. The session still shows in `/resume`, making it a silent failure. Closed recently — fix likely in-flight.

10. **[#4345 — Reasoning effort 'medium' unsupported for claude-haiku-4.5](https://github.com/github/copilot-cli/issues/4345)** *(closed, 👍 4)*
    When two feature flags are active, the CLI repeatedly throws "Reasoning effort 'medium' is not supported" during sub-agent execution. Highlights model/feature-flag interaction bugs.

---

## Key PR Progress

*No pull requests were updated in the last 24 hours.*

---

## Feature Request Trends

- **Per-agent model controls**: Developers want reasoning effort configurable per custom agent (not just globally) — plus a push to stop hardcoding `explore` to `gpt-5.4-mini` and respect custom/DeepSeek API configs.
- **Configurable HUD**: Requests to make the CLI hub display configurable — showing context state, branch info, and richer session visibility without digging through `/context`.
- **Prompt caching for Claude models**: Users want optimization for Anthropic's prompt caching to reduce latency and token costs on long-running sessions with large system prompts.
- **Better prompt composition UX**: A proposed floating GUI prompt composer (large accessible text, word wrap, dark theme) to reduce input errors and clipboard dependence.
- **Enterprise model catalogue reliability**: Multiple requests/expectations that org-enabled models are consistently reflected in the CLI's model selection.

---

## Developer Pain Points

- **Model availability inconsistencies**: Multiple open issues report Claude models mysteriously becoming "disabled" or missing from the catalogue despite being enabled in org settings — a high-frustration area with no consistent workaround.
- **MCP server fragility**: Connection pool reuse for HTTP servers, fixed-timeout handshakes with no retry, and interim deny-all policies all contribute to flaky MCP integrations.
- **Session resilience bottlenecks**: V8 string-length limits breaking `/resume`, 5 MB CAPI payload limits making `/compact` useless, and kickoff prompts getting silently dropped are killing long-running workflows.
- **Windows-specific blockers**: Plugin update failures while VS Code is running (os error 5) and terminal rendering regressions in integrated terminals are recurring Windows pain points.
- **Parallel execution rate limits**: The `explore` model's tight per-model rate limits with parallel subagents cause 429s with no backoff or automatic failover — a scalability ceiling for agent-heavy workflows.

---

*Digest generated from [github/copilot-cli](https://github.com/github/copilot-cli) activity on 2026-08-11.*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

**Kimi Code CLI Community Digest**  
**Date:** 2026-08-11  
**Data Source:** [MoonshotAI/kimi-cli](https://github.com/MoonshotAI/kimi-cli)

---

### 1. Today's Highlights
No new releases or merged PRs landed in the last 24 hours, indicating a stabilization period after recent activity. The community remains highly engaged with **Issue #1283** (Memory System), which has accumulated 31 comments and eight months of active discussion, making it the clear focal point for future feature development.

---

### 2. Releases
No new releases were published in the last 24 hours. The repository is currently quiet on the release front.

---

### 3. Hot Issues
*Note: Only one issue was updated in the last 24h. The following list includes the most prominent unresolved issues based on recent activity and community significance.*

1. **[#1283 — Memory System: Persistent context across sessions](https://github.com/MoonshotAI/kimi-cli/issues/1283)**  
   *Author: CatKang | Updated: 2026-08-10 | Comments: 31*  
   The most-discussed open issue. Requests both AI-managed and manual memory (user-defined instructions) to persist project patterns and preferences across sessions. Its 8-month lifespan and steady comment growth show high user demand for stateful CLI behavior.

---

### 4. Key PR Progress
*No pull requests were updated in the last 24h. The repository currently has zero open or recently merged PRs to report.*

---

### 5. Feature Request Trends
Despite the low activity window, the dominant trend from recent issues centers on **persistence and context retention**. Specific directions include:

- **Session Memory:** Automatically storing conversation history, project-specific patterns, and user preferences across CLI invocations.
- **User-Defined Instructions:** Support for configurable, persistent rules (e.g., code style, commit format) that apply globally or per project.
- **Context-Aware Assistance:** Using stored memory to reduce repetitive prompting and improve response consistency on long-running tasks.

Secondary trends (from historical issues) include better multi-file editing support, more granular permission controls, and integration with external knowledge bases.

---

### 6. Developer Pain Points
Recurring frustrations observed across issue history:

- **Context Amnesia:** Frequent reports of the CLI forgetting project structure or prior instructions between sessions, forcing manual re-explanation.
- **Lack of Customization:** Users wanting to define persistent system prompts or behaviors without re-entering them each time.
- **Configuration Complexity:** Demands for simpler, file-based configuration (e.g., `.kimirc`) to manage memory and defaults.
- **Slow Resolution of Long-Standing Requests:** The 8-month open period of Issue #1283 without implementation suggests perceived stagnation, a common source of community dissatisfaction.

---

*Digest generated for technical developers. For full details, visit the [repository](https://github.com/MoonshotAI/kimi-cli).*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-08-11

## Today's Highlights
OpenCode v1.18.16 shipped with two core bugfixes addressing config parsing robustness and project registration behavior, alongside desktop refinements including right-click project menu access. Community attention is sharply focused on a high-severity performance regression (#30086) with 46 comments reporting severe CPU spikes, while the project continues to process a substantial backlog of feature requests around markdown copy support, draft persistence, and VS Code extension discoverability.

## Releases
**v1.18.16** — Core bugfixes for unknown top-level config field handling and Home-opened project registration; desktop improvements for right-click menu access and project listing fallbacks.

## Hot Issues

1. **[#30086: High CPU usage in newer versions of OpenCode](https://github.com/anomalyco/opencode/issues/30086)** — 46 comments, 22 reactions. The most active issue: users report degradation from 10+ concurrent sessions to 3, with dramatic CPU spikes. Multiple reports of 99-100% utilization and unresponsiveness (#33399) confirm a regression in recent versions.

2. **[#14041: Copy message as raw markdown](https://github.com/anomalyco/opencode/issues/14041)** — 10 comments. Recurring request (re-filed as #41609) for direct markdown copy support; current highlighting/selection approaches are inadequate for developers who need to share or reuse model output.

3. **[#26220: Infinite loop after tool calls (Zen/big-pickle)](https://github.com/anomalyco/opencode/issues/26220)** — 8 comments. Process freezes post-tool-execution, specifically affecting Big Pickle builds; the community suspects provider-specific tool-call handling issues.

4. **[#10517: VS Code extension install instructions ambiguous](https://github.com/anomalyco/opencode/issues/10517)** — 8 comments, 24 reactions. High traffic on extension installation problems; users report the docs are unclear about which extension to search for. Companion issues #16217 and #31500 reinforce the discoverability gap.

5. **[#37389: GitHub Copilot multi-turn fails with 404 on item_reference](https://github.com/anomalyco/opencode/issues/37389)** — 7 comments. Critical interoperability bug: opencode2 v2 fails intermittently with `provider.unknown` errors when GitHub Copilot sends `item_reference`; the issue notes a previous report was incorrectly closed.

6. **[#38010: Opt-in option to disable exit splash](https://github.com/anomalyco/opencode/issues/38010)** — 6 comments. Embedded/white-label use case; maintainers previously auto-closed a related request (#36609), but the community persists in demanding an official configuration option.

7. **[#35432: `tool_call: false` does not disable tools](https://github.com/anomalyco/opencode/issues/35432)** — 3 comments. Model config flag is silently ignored; `SessionTools` are unconditionally resolved and sent, breaking providers without tool-call support.

8. **[#36203: Input box content cleared when switching conversations](https://github.com/anomalyco/opencode/issues/36203)** — 2 comments. Draft loss is a UX pain point; user expects draft persistence per-session. Related follow-up #41614 confirms the scope expectation.

9. **[#40642: MiMo V2.5 video input never received](https://github.com/anomalyco/opencode/issues/40642)** — 2 comments. Model advertises video capability but input never arrives — a provider integration gap where advertised model capabilities overpromise.

10. **[#39339: Intermittent "internal server error" during analysis](https://github.com/anomalyco/opencode/issues/39339)** — 2 comments. Recurring retry-loop on Windows/PowerShell during normal analysis sessions, impacting reliability for Windows users.

## Key PR Progress

1. **[#41617: Refine merman sequence diagram styling](https://github.com/anomalyco/opencode/pull/41617)** — Terminal diagram improvements with boxed headers replaced by labeled rules and theme-native colors.

2. **[#41616: Restore parcel watch for git HEAD](https://github.com/anomalyco/opencode/pull/41616)** — Fixes stale branch labels after `git checkout`; Bun's `fs.watch` misses renames, so the fix restores the Parcel-based watch.

3. **[#41615: Resolve Cloudflare account endpoints](https://github.com/anomalyco/opencode/pull/41615)** — Derives Workers AI endpoints from environment/account IDs with catalog rebuild on connection change.

4. **[#41607: Runtime-neutral legacy credential import](https://github.com/anomalyco/opencode/pull/41607)** — Fixes `Bun.file` crashes in Node and Cloudflare workerd during DB bootstrap; migrates to `node:fs/promises`.

5. **[#41613: Isolate tool stdin in TUI](https://github.com/anomalyco/opencode/pull/41613)** — Dedicated controlling-terminal stream with fd 0 redirected to null, preventing tool implementations from reading user stdin.

6. **[#36297: Busy/idle progress indicator in terminal title](https://github.com/anomalyco/opencode/pull/36297)** — Adds a status glyph to the terminal tab title, addressing long-standing user visibility needs.

7. **[#36272: Config precedence and project discovery docs](https://github.com/anomalyco/opencode/pull/36272)** — Documentation update aligning project-config discovery and precedence with actual code behavior.

8. **[#36221: Inject `_noop` tool for all providers with tool history](https://github.com/anomalyco/opencode/pull/36221)** — Fixes Bedrock API errors when messages contain tool history but no active tools; required `toolConfig` injection.

9. **[#36179: OTEL root span per prompt](https://github.com/anomalyco/opencode/pull/36179)** — Fixes session-scoped trace pollution; each prompt now gets an isolated root span instead of one giant trace per session.

10. **[#36175: Mark user processes as opencode agents](https://github.com/anomalyco/opencode/pull/36175)** — Sets `AGENT=1` and `OPENCODE=1` environment markers for subprocesses and PTY sessions in V2 core.

## Feature Request Trends
- **Markdown copy support**: Multiple filings (#14041, #41609) for raw markdown copy of assistant responses — a basic but recurring gap
- **Draft persistence**: Sessions should retain unsent input when switching conversations (#36203, #41614)
- **VS Code extension discovery**: Documentation and installation UX for the VS Code extension repeatedly confuses users (#10517, #16217, #31500)
- **Accessibility**: Colorblind mode requested for the web/desktop apps (#14755)
- **Desktop interaction**: Clickable file paths (#37891), draft retention improvements, and config-driven UI control (splash disable #38010) signal a maturing desktop product

## Developer Pain Points
- **Performance regression severity**: The 46-comment CPU issue (#30086) is the top community concern — degraded multi-session usability and system-level lags are affecting daily workflows
- **Configuration surprises**: Unclear semantics around `tool_call: false` (#35432), agent config fallbacks forwarded to providers (#41593), and config parsing failures
- **Reliability gaps**: Inconsistent Copilot integration (#37389), intermittent server errors (#39339), and DTEL tracing issues point to stability concerns
- **Draft loss frustration**: The input box clearing issue (#36203) breaks long-form message composition — a high-frequency developer workflow
- **Documentation ambiguity**: VS Code extension install steps remain the most consistently reported documentation failure

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-08-11

## Today's Highlights

The Pi project is seeing intense community activity around terminal UX stability, with significant fixes landing for the long-standing Alt+Enter interrupt bug in legacy terminal modes and a new solution for sanitizing invalid Bedrock tool arguments that were bricking sessions. The broader community is pushing for better protocol compliance (especially regarding `usage` fields), improved narrow-pane rendering, and an emerging pattern of demand for Cloudflare AI Gateway support — both as an issue and a fleshed-out PR that's now open.

## Releases

No new releases in the last 24 hours.

## Hot Issues

1. **[#6187 — Pi login hangs in WSL after GitHub Copilot device authorization](https://github.com/earendil-works/pi/issues/6187)** — Still open with 21 comments. The WSL-specific device-auth completion detection remains unsolved, making Copilot login unreliable in the most common Linux-on-Windows workflow. This is the community's top pain point for onboarding.

2. **[#7855 — "Response was truncated before completion" with OpenAI-compatible APIs](https://github.com/earendil-works/pi/issues/7855)** — Random truncation errors with VLLM and similar local backends. Even though closed as no-action, the manual-prompt-to-continue workaround frustrated users hitting this in production.

3. **[#7850 — GitHub Copilot login fails with 429 rate limiting for large orgs](https://github.com/earendil-works/pi/issues/7850)** — Organizations with 20+ available models fail device authorization with `429 Too Many Requests`. Two community upvotes indicate this affects more than one enterprise team.

4. **[#7782 — Invalid Bedrock tool call permanently bricked a Pi session](https://github.com/earendil-works/pi/issues/7782)** — A Bedrock-generated tool call with an empty key `("": "")` was persisted and replayed, permanently corrupting the session. This exposed a missing validation layer and has a fix now in PR.

5. **[#7836 — Edit fuzzy match misses whitespace-length differences](https://github.com/earendil-works/pi/issues/7836)** — `normalizeForFuzzyMatch` doesn't collapse whitespace runs, causing edit failures for small models when indentation isn't exact. The single community upvote underscores real-world friction with weaker models.

6. **[#7846 — Pi 0.84.0/0.84.1 crashes with Bun runtime: `zlib.createZstdDecompress is not a function`](https://github.com/earendil-works/pi/issues/7846)** — A hard crash at startup for Bun users. This blocks an entire runtime ecosystem from using recent Pi versions.

7. **[#7791 — Global Undici dispatcher inherits 16 KiB maxHeaderSize](https://github.com/earendil-works/pi/issues/7791)** — Large response headers are rejected with `UND_ERR_HEADERS_OVERFLOW` because Pi doesn't override Node's default. Subtle infrastructure bug that breaks legitimate providers with verbose headers.

8. **[#7896 — cloudflare-ai-gateway omits `strict:false`, making optional tool fields required](https://github.com/earendil-works/pi/issues/7896)** — Tool-calling contracts differ between direct OpenAI and Cloudflare gateway; optional fields become mandatory, breaking exact-object prompts. A provider-parity issue that impacts production tool use.

9. **[#7915 — Pi always prepends `cd` to project root for every bash command](https://github.com/earendil-works/pi/issues/7915)** — Even when already in the project root, the injected `cd <project path>` is seen as noisy and unlike Claude or Opencode behavior. A UX papercut that's getting community notice.

10. **[#7794 — APPEND_SYSTEM.md auto-discovery broken by empty-array truthy check](https://github.com/earendil-works/pi/issues/7794)** — Two bugs (empty-array truthiness and missing discovery call) prevent custom system-prompt appends from loading. Silent failure with no error message — the worst kind of configuration breakage.

## Key PR Progress

1. **[#7910 — Canonical message identity for markdown transformers](https://github.com/earendil-works/pi/pull/7910)** — Adds per-message IDs to `MarkdownTransformContext`, letting extensions correlate state across stream/redraw/restore. Closes #7828; important for extension authors building stateful renderers.

2. **[#7913 — Fullscreen transcript search via Ctrl+Shift+f](https://github.com/earendil-works/pi/pull/7913)** — The community's most-requested TUI feature (search over transcripts) finally lands as a PR from mitsuhiko. Basic but functional; no conflicts with existing keybinds.

3. **[#7882 — Sanitize empty Bedrock tool argument keys](https://github.com/earendil-works/pi/pull/7882)** — Recursively strips empty property names only when replaying to Bedrock, preserving canonical conversation data. Direct fix for the session-bricking bug in #7782. Clean separation of persisted vs. on-the-wire data.

4. **[#7899 — Prevent split Alt+Enter from interrupting](https://github.com/earendil-works/pi/pull/7899)** — Bumps escape-sequence timeout from 10ms to 100ms in StdinBuffer, fixing intermittent aborts in tmux/SSH where Alt+Enter arrives as split ESC+CR. Small change, big reliability win for legacy terminals.

5. **[#7901 — AI Gateway transport over the Cloudflare AI binding](https://github.com/earendil-works/pi/pull/7901)** — Community PR for Cloudflare Workers AI Gateway support, directly addressing #7838. Significant for Pi apps running inside Workers with unified AI gateway routing.

6. **[#7904 — Normalize single-object edits argument to array](https://github.com/earendil-works/pi/pull/7904)** — Accepts single-object or JSON-string `edits` for the edit tool, fixing models that don't wrap in arrays. Pragmatic compatibility fix for weaker/alternate models.

7. **[#7905 — Refine pnpm detection and validate managed installs](https://github.com/earendil-works/pi/pull/7905)** — Fixes false positives when paths merely contain `/pnpm/`, and validates whether pnpm actually manages the install before suggesting update commands. Closes a confusing update path for `$PNPM_HOME` users.

8. **[#7887 — Trailing newline after working directory in system prompt](https://github.com/earendil-works/pi/pull/7887)** — Fixes first-user-message concatenation directly after the cwd. Tiny formatting fix that materially improves prompt hygiene for all users.

9. **[#7892 — Avoid repainting idle fullscreen sessions on focus loss](https://github.com/earendil-works/pi/pull/7892)** — Prevents unnecessary renders on focus-out, eliminating false activity indicators in iTerm2. Polishes the fullscreen experience for macOS users.

10. **[#7881 — Reject `item_*` content IDs in message-level `input[].id` fields](https://github.com/earendil-works/pi/pull/7881)** — Enforces correct ID namespaces in the Responses API, preventing `item_*` IDs from leaking into message-level input history. Critical correctness fix for streaming async API interactions.

## Feature Request Trends

- **Fullscreen transcript search** — Search-over-transcript is now a concrete PR (#7913), resolving the most requested TUI capability.
- **Provider parity** — Recurring demand for uniform behavior across gateways (Cloudflare, Bedrock) and equivalent tool-calling semantics (`strict` flags, tool argument validation).
- **Narrow-pane and responsive TUI layouts** — Multiple requests to keep context/model info visible at restricted widths and to preserve scroll position through redraws.
- **Cloudflare Workers AI Gateway** — Growing interest in running Pi inside Workers with the unified AI binding; now both an issue (#7838) and a PR (#7901).
- **Protocol hygiene** — Persistent community requests for cleaner wire-format semantics: `usage` on delta updates, proper ID namespaces, and well-formed message boundaries.

## Developer Pain Points

- **WSL + GitHub Copilot device auth remains broken** after 40+ days (issue #6187), with no fix in sight — blocking a major platform segment.
- **Bun runtime incompatibility** with `zlib.createZstdDecompress` makes Pi 0.84.x unusable for Bun users (issue #7846) — a runtime regression with no workaround.
- **Provider-specific tool-call quirks** (empty keys, strict-mode omissions, ID namespace leaks) are the top source of session corruption and instability; users want validation *before* execution, not after.
- **Non-Kitty terminal input handling** (tmux, SSH) continues to bite — split escape sequences trigger false interrupts, and 10ms timeouts are too aggressive for real-world input delivery.
- **Silent configuration failures** — `APPEND_SYSTEM.md` and other auto-discovery paths fail without visible errors, making misconfiguration hard to diagnose.
- **Login and rate-limit friction** with large GitHub Copilot orgs (429s) and AI21 API retirement breaking previously working setups.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-08-11

## Today's Highlights
The project shipped **v0.21.9** with a major extensibility win: native support for installing Qoder-style plugins from multiple sources (directories, archives, Git repos, URLs, npm) with automatic system-prompt loading. The multi-agent "fleet" architecture is moving fast, with the in-process preview (stage 1A) delivered and the fleet MVP (stage 1B) now open for implementation, alongside a new supervised teammate runtime. Multiple rendering and terminal-resize regressions received targeted fixes, but community reports continue to surface related edge cases.

## Releases
**v0.21.9** — The headline addition is native support for installing Qoder plugins from directories, archives, Git repos, URLs, and npm packages, with automatic system-prompt loading ([#8661](https://github.com/QwenLM/qwen-code/pull/8661)). Local Control pairing via QR code is also enabled. The release includes the standard batch of bug fixes and internal improvements; one immediate follow-up report notes that `--approval-mode` and `--auth-type` are registered but missing from `qwen --help` ([#8897](https://github.com/QwenLM/qwen-code/issues/8897)).

## Hot Issues
1. **[#8718 — RFC: Native coordination for independent Qwen sessions](https://github.com/QwenLM/qwen-code/issues/8718)** — The umbrella issue for the fleet architecture (leader dispatching workers, correlating state, collecting structured results). High community interest (8 comments), spawning several staged implementation issues (#8840–#8843).

2. **[#8124 — Startup banner sometimes missing top lines on first paint](https://github.com/QwenLM/qwen-code/issues/8124)** — Intermittent first-frame rendering glitch in the TUI's `AppHeader`, correlated with pending provider updates. 10 comments; likely fixed by the resize-flicker work in #8831, but tracking remains open.

3. **[#8557 — Shrinking terminal reprints transcript blocks in scrollback](https://github.com/QwenLM/qwen-code/issues/8557)** — Duplicate output when narrowing the terminal on macOS/Warp. Drove the broader reflow investigation that produced PR #8831. 8 comments.

4. **[#8885 — Rewind indexes misaligned with automatic user-role history entries](https://github.com/QwenLM/qwen-code/issues/8885)** — P1 bug: model-facing history can contain automatic entries (cron prompts, background notifications) that `ChatRecordingService` turn boundaries don't account for, breaking session rewind. Exposed by #8838.

5. **[#8871 — ACP child process fails with "Unknown argument: acp" in qwen serve mode](https://github.com/QwenLM/qwen-code/issues/8871)** — Spawned child process can't parse the `--acp` flag it receives, causing 401 auth failures. Active discussion with maintainers (4 comments).

6. **[#8898 — "Repetitive tool calls detected" API error loop](https://github.com/QwenLM/qwen-code/issues/8898)** — Users hitting repeated identical tool-call errors, likely triggering Qwen API guardrails; closed with need-information but burning for affected users.

7. **[#8888 — Autofix pushes cancel in-progress review-pr, self-reinforcing loop](https://github.com/QwenLM/qwen-code/issues/8888)** — CI infrastructure issue: autofix on bot-authored PRs cancels the review workflow via `synchronize`, creating a cancellation feedback loop. Maintainers are actively involved.

8. **[#8860 — OpenAI API logs grow without bound (95 GB in two months)](https://github.com/QwenLM/qwen-code/issues/8860)** — No rotation or retention for per-call JSON logs when `enableOpenAILogging` is on; disk-filling severity for long-running users.

9. **[#8678 — Preserve current session when large restore times out](https://github.com/QwenLM/qwen-code/issues/8678)** — P1 session-management bug; PR #8691 landed the timeout-contract and observability pieces, with further work tracked.

10. **[#8849 — TUI input box jitters one row during resize at certain widths](https://github.com/QwenLM/qwen-code/issues/8849)** — Follow-up to #8831 (split out so the fix PR isn't blocked). Renderer off-by-one row at full-width during shrink.

## Key PR Progress
1. **[#8831 — Eliminate banner duplication and drag flicker on resize/wake](https://github.com/QwenLM/qwen-code/pull/8831)** — Root-cause fix for the #8557 class of artifacts: renderer cleared with stale row counts on shrink, stranding reflowed frames. Author self-reported; strong candidate to close multiple issues.

2. **[#8838 — Persist scheduled cron prompts](https://github.com/QwenLM/qwen-code/pull/8838)** — Records auto-fired scheduled prompts in session transcripts via existing cron contract; fixes restored-transcript omissions (#8837). Exposed the rewind-index misalignment in #8885.

3. **[#8848 — Web Shell: redesign Channel policy and workspace management](https://github.com/QwenLM/qwen-code/pull/8848)** — Exposes shared DM/group/session-routing/workspace-ownership controls for all adapters, addressing #8845.

4. **[#8728 — Live-session registry and `qwen sessions ps`](https://github.com/QwenLM/qwen-code/pull/8728)** — Each session records itself at `~/.qwen/sessions/<pid>.json`, enabling introspection without changing session semantics. First step of #8724; useful standalone.

5. **[#8707 — Qwen WebBridge direct browser control](https://github.com/QwenLM/qwen-code/pull/8707)** — Adds a Kimi WebBridge-compatible `/command` and `/status` path from `qwen serve` to the Chrome extension, with a 17-action surface and task-scoped ownership.

6. **[#8882 — Make cross-session switching transactional](https://github.com/QwenLM/qwen-code/pull/8882)** — Staging-store approach for WebUI session switches; current session stays visible owner until target is fully staged, making switching safe under failures.

7. **[#8894 — `qwen review capture-tui` — rendering claims get pixels, not prose](https://github.com/QwenLM/qwen-code/pull/8894)** — Verifier drives code under review in a private tmux server to produce actual pane captures for terminal-rendering claims. Interesting testing innovation.

8. **[#8368 — Add Kimi and Xiaomi MiMo providers](https://github.com/QwenLM/qwen-code/pull/8368)** — First-class `/auth` presets for both third-party providers, with China vs. International access choices; autofix/takeover flow engaged.

9. **[#8895 — Stream autofix agent progress](https://github.com/QwenLM/qwen-code/pull/8895)** — Headless Qwen emits streamed partial progress so the idle watchdog can distinguish active tool work from stalled sandboxes.

10. **[#8850 — Correct round-cap marker lifecycle and stale docs](https://github.com/QwenLM/qwen-code/pull/8850)** — Addresses 11 post-merge auto-review findings from #8773 on the review round-cap stop marker (`budget-stop.json` lifecycle).

## Feature Request Trends
- **Native multi-agent coordination** — The dominant theme: the fleet architecture (#8718) with staged implementation (#8840–#8843) covering contracts, supervised teammates, terminal attach, and legacy cleanup.
- **Web Shell as a first-class management surface** — Multiple requests (channel policy redesign #8845, workspace file uploads #8874, Git diff sources #8467) push Web Shell beyond chat into full workspace/team administration.
- **Session introspection and management** — Live session registry, `qwen sessions ps`, transactional switching, and better restore-timeout handling all point to more robust session lifecycle tooling.
- **Broader provider ecosystem** — Requests for Kimi, Xiaomi MiMo presets (#8368) alongside persistent provider-update bugs (#8504, #8863) show ecosystem growth is straining update logic.
- **TUI/rendering polish** — A cluster of resize, flicker, banner, and input-box issues (#8124, #8557, #8849, #8659) with active fix-and-follow-up cycles indicates rendering stability remains a community priority.

## Developer Pain Points
- **Provider update prompt repeating and silently overwriting configuration** — Custom models survive updates, but users see repeated prompts (#8504) and, worse, `model.name`/`model.baseUrl` get silently reset when the current model belongs to another provider (#8863, P1 regression).
- **Terminal rendering regressions** — The resize/wake flicker family (#8557, #8849, #8124) has generated the most sustained comment threads, with users on macOS, Linux, and web-based terminals all reporting variants.
- **Session restore and rewind correctness** — Automatic history entries (cron prompts, background notifications) break rewind indexes and transcript restoration (#8885, #8837); users care about having a complete, consistent session record.
- **Daemon/serve mode brittle edges** — ACP child-process argument parsing (#8871), fast-path `.env` trust violations (#8643), and workspace-boundary write failures (#8851, #8618) show serve mode still needs hardening.
- **Unbounded log growth** — 95 GB of OpenAI logs in two months (#8860) is an alarming operational footgun.
- **CI workflow self-interference** — Autofix pushes cancelling review-pr runs (#8888) creates a feedback loop that stalls bot-authored PR progress.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-08-11

## 1. Today's Highlights
The project is moving into a significant structural phase with EPIC-005 (#5316) tracking a full TUI crate decomposition, while v0.9.6 shipped as a "subtractive release" that reduces runtime guards and simplifies the compaction path. A critical subagent recursion-depth bug was fixed in PR #5317, and the long-running staged command-boundary refactor (EPIC #2870) has been closed. Compaction behavior remains the hottest community pain point, with two open issues and an ongoing EPIC dedicated to defining a structured survival contract.

## 2. Releases
**v0.9.6** — shipped today via PR #5315 ([link](https://github.com/Hmbown/CodeWhale/pull/5315)). Described as a "subtractive release" featuring:
- Fewer runtime guards
- One stable base prompt across providers
- Truthful provider endings
- A smaller compaction path that preserves provider-specific context more reliably

## 3. Hot Issues (10 noteworthy)

1. **#2870 — [CLOSED] EPIC: staged command-boundary refactor** ([link](https://github.com/Hmbown/CodeWhale/issues/2870)) — *Created Jun 7, 20 comments.* Closed after ~2 months; tracked the mergeable layers for the command-boundary refactor originally discussed in #2791. Its closure signals the refactor is complete or superseded.

2. **#5034 — Switching providers retains unrelated default model** ([link](https://github.com/Hmbown/CodeWhale/issues/5034)) — *Opened Aug 1, 4 comments.* Switching to OpenAI can leave `gpt-5.5` as default even when inherited from a different route. Indicates provider/model resolution is not updated as one coherent transaction — a reliability concern for multi-provider users.

3. **#5096 — Compaction gain not visible** ([link](https://github.com/Hmbown/CodeWhale/issues/5096)) — *Opened Aug 2, 4 comments.* `/compact` reports success but the token counter (e.g. 37K/128K) does not drop. Community reports this across Qwen3.6 and DeepSeek v4 Flash local endpoints. Suggests the compaction path may be no-op in some configurations.

4. **#5239 — Model supports 1M context, but compaction fires at 128K** ([link](https://github.com/Hmbown/CodeWhale/issues/5239)) — *Opened Aug 4, 2 comments.* User wants the 128K trigger threshold configurable when the model supports 1M. Currently forces frequent compression on high-context models.

5. **#4394 — Compaction: publish and enforce a structured survival contract** ([link](https://github.com/Hmbown/CodeWhale/issues/4394)) — *Opened Jul 16, 3 comments.* Long-standing EPIC-adjacent request: define exactly what survives compaction (Plan/To-do/subagent state) and document it. Implementation exists but the contract is implicit.

6. **#5270 — v0.9.5: unified tasks surface** ([link](https://github.com/Hmbown/CodeWhale/issues/5270)) — *Opened Aug 7, 3 comments.* Enhancement: single operator-facing list of all running work — background shells, subagents, Fleet/lane workers, workflow runs. Idle chrome should indicate when background work is alive.

7. **#5316 — EPIC-005: TUI Crate Decomposition (Umbrella)** ([link](https://github.com/Hmbown/CodeWhale/issues/5316)) — *Opened Aug 10, 0 comments.* New umbrella EPIC tracking the decomposition of the TUI crate into sub-EPICs and FEATs. Architectural milestone for maintainability.

8. **#5253 (referenced by PR #5317) — Subagent nested depth widening** ([link](https://github.com/Hmbown/CodeWhale/issues/5253)) — Referenced in today's fix PR; nested spawns could widen recursion past the depth chosen by the root/session. Security/stability concern.

9. **#2791 (referenced by #2870) — Command-boundary design discussion** ([link](https://github.com/Hmbown/CodeWhale/issues/2791)) — The originating design discussion that spawned the now-closed EPIC #2870. Relevant for understanding command-boundary semantics in the v0.9.x line.

10. **#2851 (referenced by #2870) — Reference/proof PR for command-boundary refactor** ([link](https://github.com/Hmbown/CodeWhale/issues/2851)) — The proof-of-concept PR referenced by the EPIC; useful for reviewers evaluating the merged approach.

## 4. Key PR Progress (3 items)

1. **#5317 — [OPEN] fix(subagents): cap nested max_depth by inherited budget** ([link](https://github.com/Hmbown/CodeWhale/pull/5317)) — *By ousamabenyounes, today.* Fixes the explicit-`max_depth` arm dropping the inherited absolute budget; now takes `inherited.min(..)` mirroring the profile-hint arm. Addresses #5253 recursion-depth widening.

2. **#5300 — [CLOSED] refactor(core): own primary request preparation** ([link](https://github.com/Hmbown/CodeWhale/pull/5300)) — *Merged today.* Replaces the unused synthetic `ChatRequest` scaffold with the production `MessageRequest` DTO family (previously owned by TUI crate). Adds a pure `prepare_primary_turn_request` constructor for provider-neutral defaults. Consolidates request-prep into `codewhale-core`.

3. **#5315 — [CLOSED] chore(release): ship v0.9.6** ([link](https://github.com/Hmbown/CodeWhale/pull/5315)) — *Merged today.* Release-prep PR. v0.9.6 is subtractive: fewer runtime guards, one stable base prompt, truthful provider endings, smaller compaction path preserving provider context.

## 5. Feature Request Trends
- **Configurable context-compaction thresholds** — the hard-coded 128K trigger conflicts with 1M-context models (#5239). The community wants per-model or user-set compaction triggers.
- **Visibility into background work** — one unified surface for shells, subagents, workers, and workflow runs (#5270). Small incremental wins dominated recent closed work; large decomposition EPIC suggests maintainability investment ahead.
- **Structured compaction survival contract** — explicitly document what survives compaction, especially structured state (#4394).
- **Coherent provider/model switching** — when you change provider, model defaults must switch atomically (#5034).
- **Architectural decomposition** — EPIC-005 (#5316) signals the maintainers are proactively restructuring the crate; the community will benefit from faster iteration and clearer boundaries.

## 6. Developer Pain Points
- **Compaction is the #1 recurring pain point**: three open issues (#5096, #5239, #4394) and a closed EPIC (#2870) in this window. Reports include "compaction triggered but token counter unchanged," "why 128K not 1M," and "what exactly survives." This correlates with the maintenance team's own "subtractive" v0.9.6 direction.
- **Provider switching leaves stale model defaults** (#5034) — non-obvious runtime state that can cause surprising cost/latency behavior on the wrong provider.
- **Subagent recursion-depth bugs** (#5253) — a sharp-edge stability concern for power users relying on deep delegation chains.
- **Release cadence as signal**: the v0.9.6 release description ("subtractive," "truthful provider endings") suggests the team is cleaning up legacy behavior; users should expect tightening of previously-loose defaults in future releases.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/kky-wollu/agents-radar).*
# AI CLI Tools Community Digest 2026-08-06

> Generated: 2026-08-05 23:05 UTC | Tools covered: 9

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

# Cross-Tool Comparison Report: AI CLI Developer Tools
**Date: 2026-08-06**

---

## 1. Ecosystem Overview

The AI CLI tools landscape shows a maturing ecosystem with distinct platform strategies: **Claude Code** and **OpenAI Codex** dominate as enterprise-grade solutions with robust plugin ecosystems, while **Gemini CLI** and **Qwen Code** prioritize SDK-level stability and multi-platform support. The most pressing cross-cutting concern is **cost predictability** — users across Claude Code, OpenAI Codex, and Gemini CLI report runaway token consumption, silent model re-routing, and ineffective safeguard warnings (#82506, #37090, #82101). Windows platform stability remains the **#1 friction point** for Codex, Copilot CLI, and Kimi Code, with crashes, input stutters, and rendering defects dominating issue trackers. A significant architectural shift is underway: **OpenCode** is aggressively migrating from v1 to v2 data models, **Qwen Code** is consolidating on a Tauri-based desktop shell, and **DeepSeek TUI** is expanding its Runtime API surface to support managed clients.

---

## 2. Activity Comparison

| Tool | Issues (Notable) | PRs (Active) | Releases (24h) | Community Velocity |
|---|---|---|---|---|
| **Claude Code** | 10 (2 new, 6 closed) | 10+ (8 from one contributor) | **0** | High — large contributor base, active maintenance |
| **OpenAI Codex** | 10 (2 new) | 10 (all recent, active) | **1 patch** (rust-v0.146.1) | Very High — rapid PR merge cadence |
| **Gemini CLI** | 10 (all open, several critical) | 10 (2 open, 5 closed, 3 merged) | **0** | High — strong security focus |
| **Copilot CLI** | 10 (12+ new triage) | **0** PR activity | **3 pre-releases** (v1.0.79-2/3/4) | Medium — pre-release cadence, low PR throughput |
| **Kimi Code** | 10 (3 critical new) | 2 substantive + docs | **0** | Low — small team, slower iteration |
| **OpenCode** | 10 (1 new critical) | 10 (5 large refactors) | **1 stable** (v1.18.14) | High — major architectural churn |
| **Pi** | 10 (7 resolved, 3 open) | 10 (8 merged, 2 open) | **0** | Very High — small but efficient maintainers |
| **Qwen Code** | 10 (2 P1 security) | 10 (4 merged, 6 open) | **3** (stable + preview + nightly) | High — rapid release train |
| **DeepSeek TUI** | 5 (2 core issues) | 13 (integration branch 77 commits ahead) | **0** | Medium — active integration branch |

---

## 3. Shared Feature Directions

| Requirement | Tools | Specific Needs |
|---|---|---|
| **Cost visibility & guardrails** | Claude Code (#68703, #82101), Codex (#37090), Gemini CLI (#26522), Kimi Code (#2586), Qwen Code (#8605) | Pre-flight cost estimates, runaway-agent warnings, token counters, `/slow` batch mode |
| **Context/session management** | Claude Code (#21132), Copilot CLI (#4373), Gemini CLI (#28672), OpenCode (#31932), Pi (#7553) | Self-clearing context, session persistence, cross-project session lists, compaction budget control |
| **MCP reliability & compatibility** | Copilot CLI (#4370, #4374, #4378), Qwen Code (#8550), OpenCode (#35446), DeepSeek TUI (#5130) | Graceful handling of non-standard servers, timeouts on SSE, policy-fetch resilience |
| **Model delegation transparency** | Copilot CLI (#4377), Codex (#34700, #37170), Claude Code (#84212) | Visibility into sub-agent model routing, per-thread model control, capability validation |
| **Multi-platform stability** | Codex (6 Windows issues), Copilot CLI (#4026), Kimi Code (#2587), OpenCode (#8345) | Windows crash fixes, Intel Mac AVX2 fallback, WSL Git detection |
| **Skill/agent security** | Claude Code (#84212), Gemini CLI (#26525), Qwen Code (#8582) | Argument injection protection, secret redaction before model send, read-only shell bypass fixes |
| **Desktop/IDE integration** | OpenCode (#11176), Qwen Code (#8092), Kimi Code (#2589), Claude Code (#58750) | Official VS Code extension, Tauri-based shells, voice/ACP clients |

---

## 4. Differentiation Analysis

| Tool | Primary Focus | Target User | Technical Approach |
|---|---|---|---|
| **Claude Code** | Enterprise reliability, plugin & skill ecosystem | Professional developers, teams | Monorepo with extensive plugin marketplace, skill engine, Cowork desktop |
| **OpenAI Codex** | Rust-native performance, cloud-delegation, managed auth | Power users, Rust ecosystem | Rust core, `multi_agent_v2`, Azure Key Vault CI, managed provisioning |
| **Gemini CLI** | SDK-level stability, Google Cloud integration | GCP developers, multi-model workflows | TypeScript/Node, sub-agent architecture, Vertex AI parity |
| **Copilot CLI** | GitHub-centric workflows, MCP-first | GitHub Enterprise users | Node/Bun, MCP policy registry, worktree integration |
| **Kimi Code** | Moonshot model ecosystem, ACP voice path | Moonshot/Kimi API users | Rust core, ACP bridge, audio-aware agents |
| **OpenCode** | Architecture innovation, cross-provider | Hackers, plugin developers | V1→V2 data migration, LAN discovery, multi-tenant sessions |
| **Pi** | TUI polish, lightweight architecture | Terminal purists | Go? (TUI-first, OSC 8, AGENTS.override.md), no desktop |
| **Qwen Code** | Alibaba ecosystem, desktop consolidation | Qwen/China-market developers | Tauri desktop, WebShell, Live Voice, DingTalk/Feishu channels |
| **DeepSeek TUI** | Runtime API expansion, managed clients | DeepSeek API users, automation developers | Copilot-authored Runtime API, verifier receipts, skill lifecycle over HTTP |

---

## 5. Community Momentum & Maturity

**Rapidly Iterating (High PR velocity, frequent releases):**
- **OpenCode** — v1.18.14 shipped; massive refactors (v1→v2 migration, control plane removal) signal aggressive technical debt cleanup.
- **Gemini CLI** — 5 PRs closed/merged in 24h; security-first SSRF fix indicates strong maintainer engagement.
- **Pi** — 8 PRs merged in 24h; small but efficient maintainer team with consistent delivery.

**Stable but Stretched:**
- **Claude Code** — No releases in 24h; community contributor **RerankerGuo** dominates PR queue (8 fixes) — a healthy external contribution signal, but mainline velocity is moderate.
- **Qwen Code** — Triple release train (stable, preview, nightly); desktop pivot suggests strategic investment.
- **OpenAI Codex** — Single patch release; 10 active PRs show healthy pre-release work, but Windows issues dominate community noise.

**Community Engagement Risk:**
- **Copilot CLI** — Zero PR activity in 24h despite 12+ new issues; pre-release cadence (v1.0.79-x) without stable release may frustrate users.
- **Kimi Code** — Only 2 substantive PRs; several critical bugs remain unaddressed; community is waiting for a patch.
- **DeepSeek TUI** — Maintainer-driven integration branch (77 commits ahead) but little external contribution visible.

---

## 6. Trend Signals

### For Tool Developers:
1. **Cost predictability is non-negotiable** — Users across four tools report silent token consumption, false "limit reached" messages, and ineffective safeguard warnings. Implement pre-flight cost estimates and hard stop-guards.
2. **Windows is the new battleground** — Codex, Copilot CLI, and Kimi Code all suffer Windows-specific crashes. A documented, tested Windows strategy is a competitive differentiator.
3. **MCP interoperability is breaking trust** — Non-standard servers, policy-fetch failures, and missing timeouts are recurring. Standardize on tolerant MCP handling (e.g., timeouts, graceful method negotiation).
4. **Security boundaries need hardening** — Command-substitution bypasses (Qwen Code), secret leakage before redaction (Gemini CLI), and skill argument injection (Claude Code) reveal that model-facing tools need deterministic input sanitization.
5. **Model delegation transparency** — Users demand visibility into sub-agent model routing and per-thread model configuration. Silent re-routing (Codex 5.5→5.6) destroys trust.

### For Developers Evaluating Tools:
1. **If you live in GitHub** — Copilot CLI's worktree features and MCP registry are strong, but Windows fragility and zero-PR cadence suggest cautious adoption.
2. **If you want enterprise stability** — Claude Code's plugin ecosystem and skill engine are unrivaled, but monitor #82506 (billing bug) and #69332 (runaway agents) before committing.
3. **If you want active iteration** — OpenCode and Pi have the best PR-to-issue ratios; expect features to land quickly.
4. **If GCP is your stack** — Gemini CLI's SSRF fix and thought-signature repair indicate solid investment, but sub-agent hangs (#21409) remain critical.
5. **If you're on Windows** — **Avoid Codex, Copilot CLI, and Kimi Code** until platform-stability fixes land; prefer Qwen Code or Pi (both show fewer Windows regressions).

---

*Report compiled from community digest snapshots for 2026-08-06. All issue/PR references are canonical GitHub URLs.*

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data as of 2026-08-06 | Source: github.com/anthropics/skills**

---

## 1. Top Skills Ranking

The following Skills have attracted the most community discussion and development activity:

### 1.1 skill-creator Bug-Fix Cluster (PRs #1298, #1099, #1050, #1323, #1261)
**Functionality:** The `skill-creator` meta-skill includes a description-optimization loop (`run_eval.py`, `run_loop.py`, `improve_description.py`) that evaluates trigger accuracy, but is broken with recall=0% across all queries.
**Status:** OPEN (5 related PRs, multiple contributors)
**Discussion highlights:** The community has identified multiple root causes — eval artifacts not installed as real skills (#1298), Windows subprocess pipe encoding failures (#1099, #1050), trigger detection missing the skill name (#1323), and synthetic command files polluting the live project registry (#1261). Issue #556 (12 comments, 7 👍) tracks the core bug; Issue #1169 confirms reproducibility.
**Link:** [PR #1298](https://github.com/anthropics/skills/pull/1298) | [Issue #556](https://github.com/anthropics/skills/issues/556)

### 1.2 self-audit (PR #1367)
**Functionality:** A universal quality-gate skill performing mechanical file verification followed by a four-dimension reasoning audit in damage-severity priority order. Works with any project/tech stack/model.
**Status:** OPEN (created 2026-06-28, updated 07-02)
**Discussion highlights:** Complements the proposed reasoning pipeline in Issue #1385. Highest-recent PR activity alongside color-expert.
**Link:** [PR #1367](https://github.com/anthropics/skills/pull/1367)

### 1.3 document-typography (PR #514)
**Functionality:** Typographic quality control for generated documents — detects orphan word wrap, widow paragraphs, and numbering misalignment.
**Status:** OPEN (created 2026-03-04; 10+ days of discussion)
**Discussion highlights:** Addresses a problem every Claude-generated document encounters; positioned as a universal quality layer.
**Link:** [PR #514](https://github.com/anthropics/skills/pull/514)

### 1.4 ODT skill (PR #486)
**Functionality:** Create, fill, parse, and convert OpenDocument files (.odt/.ods), including ODT→HTML conversion and template filling.
**Status:** OPEN (created 2026-03-01; discussion through 04-14)
**Link:** [PR #486](https://github.com/anthropics/skills/pull/486)

### 1.5 testing-patterns (PR #723)
**Functionality:** Comprehensive testing skill covering Testing Trophy philosophy, AAA patterns for unit tests, React component testing with Testing Library, and edge-case guidance.
**Status:** OPEN (created 2026-03-22; discussion through 04-21)
**Discussion highlights:** One of the most technically substantive new-skill proposals, covering the full testing stack.
**Link:** [PR #723](https://github.com/anthropics/skills/pull/723)

### 1.6 color-expert (PR #1302)
**Functionality:** Self-contained color-expertise skill: color naming systems (ISCC-NBS, Munsell, RAL, XKCD), color-space selection tables (OKLCH for scales, OKLAB for gradients, CAM16), and practical guidance.
**Status:** OPEN (created 2026-06-10; updated through 07-21 — active discussion)
**Link:** [PR #1302](https://github.com/anthropics/skills/pull/1302)

### 1.7 pyxel retro-game skill (PR #525)
**Functionality:** Retro/pixel-art/8-bit game development using the Pyxel engine via pyxel-mcp; covers write → run_and_capture → inspect → iterate workflow.
**Status:** OPEN (created 2026-03-05; discussion through 07-15 — extended window suggests maintainer review cycle)
**Link:** [PR #525](https://github.com/anthropics/skills/pull/525)

---

## 2. Community Demand Trends

Distilled from Issues sorted by comments:

### 2.1 Security & Trust Boundary (Issue #492 — 43 comments, 2 👍)
**The single largest demand signal.** The community demands that community skills be explicitly identified as NOT official Anthropic skills when distributed under the `anthropic/` namespace. This is a trust-boundary vulnerability affecting permission elevation. This is a governance/safety concern, not a feature request.

### 2.2 Organizational Sharing (Issue #228 — 16 comments, 8 👍)
Direct skill sharing within organizations via Claude.ai — currently users must manually download/upload `.skill` files via Slack/Teams. Highest 👍 count of any open issue. Demand for team-level skill distribution and a shared skill library.

### 2.3 Tooling Reliability (Issues #556 — 12 comments, 7 👍; #1169 — 3 comments, 1 👍)
The skill-creator's eval loop being broken (recall=0%) is the most-reproduced technical blocker. The community's meta-skill infrastructure needs to work before new Skills can be validated and merged.

### 2.4 Agent Memory & State Management (Issue #1329 — 9 comments)
Compact-memory: symbolic notation for compact agent state — a long-running agent's persistent memory in prose consumes context; symbolic notation would compress it.

### 2.5 Reasoning Quality Gates (Issue #1385 — 4 comments; PR #1367)
Three-gate pipeline: pre-task calibration → adversarial review → delivery verification. Complements the self-audit skill (PR #1367).

### 2.6 Context Window Management (Issue #1487 — 4 comments)
The `claude-api` skill eagerly injects ~156k tokens in a single tool call, exhausting context. Demand for built-in size guards on skills.

### 2.7 Duplicate Skill Conflicts (Issue #189 — 6 comments, 9 👍)
Installing both `document-skills` and `example-skills` plugins yields identical skills in the context window. Demand for deduplication or unambiguous plugin separation.

---

## 3. High-Potential Pending Skills

PRs with active comments and clear community value, not yet merged:

| Skill | PR | Function | Status |
|---|---|---|---|
| **self-audit** | [#1367](https://github.com/anthropics/skills/pull/1367) | Mechanical verification + reasoning audit before delivery | OPEN, active |
| **color-expert** | [#1302](https://github.com/anthropics/skills/pull/1302) | Comprehensive color knowledge for any task | OPEN, active through 07-21 |
| **testing-patterns** | [#723](https://github.com/anthropics/skills/pull/723) | Full-stack testing guidance (Trophy model → React) | OPEN |
| **document-typography** | [#514](https://github.com/anthropics/skills/pull/514) | Typographic QC for generated documents | OPEN |
| **ODT skill** | [#486](https://github.com/anthropics/skills/pull/486) | OpenDocument creation/conversion/template-filling | OPEN |
| **pyxel game skill** | [#525](https://github.com/anthropics/skills/pull/525) | Retro game dev with Pyxel + MCP | OPEN, long review window |
| **plan-file-hygiene** | [#1479](https://github.com/anthropics/skills/pull/1479) | Lifecycle management for planning artifacts | OPEN, recent (07-25) |
| **skill-quality-analyzer + skill-security-analyzer** | [#83](https://github.com/anthropics/skills/pull/83) | Meta-skills evaluating structure/docs and security | OPEN, older (11-2025) |

Additionally, two Windows-compatibility fixes for skill-creator ([#1050](https://github.com/anthropics/skills/pull/1050), [#1099](https://github.com/anthropics/skills/pull/1099)) are likely merge candidates — they are small, well-scoped, and directly unblock cross-platform usage of the eval tooling.

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand at the Skills level is not new Skill surface area — it is making the existing skill-creator toolchain trustworthy on Windows, and establishing trust, safety, and governance guardrails for the ecosystem itself (3 of the top-5 most-discussed issues are about security, reliability, and duplication), with quality-assurance meta-skills (self-audit, quality/security analyzers) emerging as the next frontier.**

---

# Claude Code Community Digest — 2026-08-06

---

## 1. Today's Highlights

A wave of older issues reached closure, but two fresh concerns take center stage: a suspected **Claude Max billing/usage bug** (#82506) where session limits appear to be consumed without actual use, and a newly reported **skill engine defect** (#84212) where `$1`/`$2` arguments are substituted into SKILL.md bodies, silently corrupting shell commands. The PR queue is dominated by **eight focused fixes from community contributor RerankerGuo** targeting the plugin development toolchain and duplicate-maintenance scripts. No new releases landed in the last 24 hours.

---

## 2. Releases

No new releases were published in the last 24 hours. Previous versions (2.1.x series) remain current.

---

## 3. Hot Issues

### 🔥 High Engagement

**#82506 — [OPEN] Possible Claude Max usage bug: session limit consumed without using** · 17 comments · 7 👍
Author: TchabaTech
A potential billing/usage accounting defect where Claude Max session limits are reported as consumed despite no actual usage. This is generating significant community concern given direct cost implications. The open status suggests the team is still investigating.
→ https://github.com/anthropics/claude-code/issues/82506

**#48827 — [CLOSED] Cowork downloads Linux binary instead of macOS on Intel Mac** · 22 comments · 4 👍
Author: andreagolini90-dot
The Cowork feature in Claude Desktop crashed with SIGILL (exit code 132) because the app downloaded an ELF Linux binary instead of a macOS Mach-O binary on Intel Macs. Now closed, presumably fixed, but a stark reminder of cross-platform packaging pitfalls.
→ https://github.com/anthropics/claude-code/issues/48827

**#58750 — [OPEN] Cowork Desktop (macOS): AskUserQuestion card never reaches renderer** · 11 comments · 5 👍
Author: rufftimo
A UI/runtime mismatch where interactive question cards are silently dropped — the badge shows pending but no UI appears, and the request resolves as "Dismissed" on quit. A frustrating UX dead-end for desktop Cowork users.
→ https://github.com/anthropics/claude-code/issues/58750

### 🐛 Notable Bugs

**#84212 — [OPEN] Skill `args` substituted into `$0`/`$1`/`$2` in SKILL.md body** · 1 comment
Author: redsub-captain
**New today.** The `Skill` tool's argument substitution is corrupting shell commands embedded in skill definitions. `$0`, `$1`, etc. in the SKILL.md body get replaced with whitespace-split args, silently altering command behavior. Potentially severe if an arg contains malicious content.
→ https://github.com/anthropics/claude-code/issues/84212

**#80131 — [OPEN] Fullscreen renderer suspends with SIGTTIN on launch in iTerm2** · 1 comment · 3 👍
Author: nozikov
`CLAUDE_CODE_NO_FLICKER=1` causes Claude Code to lose terminal foreground control in iTerm2 — the process is suspended by the shell and mouse tracking leaks into the terminal. Works in Ghostty but not iTerm2, suggesting a terminal-escape-sequence compatibility issue.
→ https://github.com/anthropics/claude-code/issues/80131

**#82101 — [OPEN] Large workflow warning thresholds not triggered** · 1 comment
Author: lokitech
A 24-hour multi-agent workflow session produced no "Large workflow" warnings despite exceeding documented thresholds (>25 agents, >1.5M tokens). This severely undermines trust in runaway-cost safeguards.
→ https://github.com/anthropics/claude-code/issues/82101

### 📋 Recently Closed Highlights

**#21132 — [CLOSED] [FEATURE] Claude clear context for itself** · 10 comments · 15 👍
Author: createdaccountbecauseIwantgithubcopilot
A long-standing feature request for self-initiated context clearing has been resolved. High community demand (15 👍) suggests this is a welcome capability — or was replaced by a better mechanism.
→ https://github.com/anthropics/claude-code/issues/21132

**#68502 — [CLOSED] HTTP 529 misreported as "Rate limited", hard-fails subagents** · 6 comments
Author: awaliuddin
Server-overload errors (529) were rendered as plain "Rate limited" and caused parallel sessions/subagents to hard-fail without backoff or error logging. Misleading messaging at scale. Now closed.
→ https://github.com/anthropics/claude-code/issues/68502

**#69332 — [CLOSED] Sub-agents recursively self-spawn → exponential fan-out → exhausts usage** · 5 comments
Author: jenscz
A severe runaway: background sub-agents recursively spawned themselves, burning the full usage limit — and kept running even after the host session exited. High severity; now closed.
→ https://github.com/anthropics/claude-code/issues/69332

**#68703 — [CLOSED] [FEATURE] Surface estimated token cost before running expensive skills** · 4 comments · 2 👍
Author: klee-wli
A request for a confirmation gate before launching token-hungry skills like `deep-research` (which can fan out 15–20 subagents and consume ~25% of quota before intervention). Closed — hopefully implemented.
→ https://github.com/anthropics/claude-code/issues/68703

**#70399 — [CLOSED] `/fork` context contaminates main session on switch-back** · 2 comments · 3 👍
Author: tbertran
A session isolation bug: returning to the main session after a fork led to the main session responding to the fork's topic, interrupting in-progress work. A dangerous context-bleed for parallel workflows.
→ https://github.com/anthropics/claude-code/issues/70399

---

## 4. Key PR Progress

**#41661 — [OPEN] Add 14 Revolutionary Claude Code Plugins** · 0 comments
Author: cliffordjose
A large community contribution adding 14 new plugin directories (security, performance, architecture, fullstack automation) and expanding the marketplace to 27 plugins. Ambitious scope — watch for review depth.
→ https://github.com/anthropics/claude-code/pull/41661

**#16929 — [OPEN] fix(code-review): respect `--comment` flag for GitHub posting** · 0 comments
Author: heathdutton
Fixes README-vs-behavior mismatch: the `/code-review` command was posting inline GitHub comments by default, contradicting the documented terminal-output default. The `--comment` flag now correctly gates posting.
→ https://github.com/anthropics/claude-code/pull/16929

**#84138 — [OPEN] fix: workaround for self-signed certificate error in Cowork** · 0 comments
Author: botbikamordehai2-sketch
Addresses #24470: Bun's runtime doesn't load system certs, causing spurious "Self-signed certificate" errors on macOS without any proxy. Practical workaround via PostToolUse hook.
→ https://github.com/anthropics/claude-code/pull/84138

### RerankerGuo's Maintenance Series (8 PRs)

**#84004 — fix(plugin-dev): limit frontmatter parsing**
Parses only the opening YAML frontmatter block, preventing later `---` horizontal rules from being misread.
→ https://github.com/anthropics/claude-code/pull/84004

**#84003 — fix(scripts): propagate top-level failures**
Ensures duplicate-maintenance scripts exit with proper failure status instead of swallowing errors via `.catch(console.error)`.
→ https://github.com/anthropics/claude-code/pull/84003

**#83999 — fix(scripts): validate gh flag values**
Rejects incomplete commands like `gh issue list --limit` that previously bypassed argument validation.
→ https://github.com/anthropics/claude-code/pull/83999

**#83995 — fix(scripts): validate label option values**
Prevents `--add-label`/`--remove-label` from triggering unbound-variable errors when used without values.
→ https://github.com/anthropics/claude-code/pull/83995

**#83993 — fix(scripts): reject self-referential duplicates**
Stops `comment-on-duplicates.sh` from tagging an issue as a duplicate of itself, which previously caused a feedback loop.
→ https://github.com/anthropics/claude-code/pull/83993

**#83992 — fix(plugin-dev): assert expected hook decision**
Fixes #83800: `test-hook.sh` now supports `--expect allow|deny|ask`, catching hooks that allow operations they are meant to deny.
→ https://github.com/anthropics/claude-code/pull/83992

**#83990 — fix(plugin-dev): report missing jq dependency**
Fixes #83802: pre-checks for `jq` before use, reporting a clear missing-dependency error instead of a misleading "invalid JSON".
→ https://github.com/anthropics/claude-code/pull/83990

---

## 5. Feature Request Trends

| Trend | Evidence | Community Sentiment |
|---|---|---|
| **Cost visibility & guardrails** | #68703 (token-cost confirmation), #82101 (threshold warnings never fired) | Strong — users want pre-flight cost estimates and reliable runaway warnings |
| **Permission lifecycle hooks** | #64170 (PermissionResolved hook event) | Moderate — more granular control over permission decisions |
| **Self-management of context** | #21132 (Claude clearing its own context) | High (15 👍) — likely addressed; still a desired pattern |
| **Documentation completeness** | #39114 (interactive-mode syntax), #63313 (`$TMPDIR` sandbox behavior) | Recurring — docs lag behind features |
| **Resource-aware execution** | #68703, #84212 (skill arg safety) | Emerging — need for predictability before expensive/agent fan-out |

---

## 6. Developer Pain Points

**1. Billing/usage transparency anxiety.** #82506 — users suspect limits are consumed without real use. Combined with #69332 (runaway sub-agents burning quota) and #82101 (warnings never fire), **cost predictability** is the dominant trust concern.

**2. Cross-platform packaging & config drift.** #48827 (Linux binary on macOS), #70393 (VS Code ignoring MSIX MCP config), #70414 (Windows Cowork file truncation) — recurring pain across macOS/Windows/Linux.

**3. Cowork reliability.** Two of the top three issues this cycle target the Cowork/Desktop experience: interactive cards never rendering (#58750) and binary mismatches (#48827). Desktop remains fragile.

**4. Terminal renderer regressions.** A cluster of inline/fullscreen TUI issues: scrollback corruption (#68755), missing echo in fullscreen (#70435), SIGTTIN suspension in iTerm2 (#80131), VoiceOver regression (#63500). The TUI team appears stretched thin.

**5. Runaway agent behavior.** #69332 (self-spawning sub-agents) and #70418 (Claude "babysits" PRs with sleep-poll loops) — agents frequently exceed the scope of the user's actual request, consuming tokens and time. This is the #1 behavioral complaint.

**6. Network resilience.** ECONNRESET (#70417), mid-response connection drops (#70295), and 529-as-ratelimit misreporting (#68502) — flaky API connections are a steady background annoyance, especially for heavy users.

---

*Digest compiled from public GitHub issues/PRs of `anthropics/claude-code`, 2026-08-06. All links provided are canonical issue/PR URLs.*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-08-06

## Today's Highlights
A patch release (rust-v0.146.1) tightens automatic-review defaults for cyber-capable models, a response to growing community concern over false-positive security filtering. The issue tracker is dominated by Windows desktop performance and reliability reports—including system-wide input stutter and full-thread replays—signaling that Windows stability remains the top friction point. Several PRs also landed to fix MCP handshake timeouts, consolidate Git status scans, and centralize tool approval handling, indicating active hardening of the execution core.

## Releases
**rust-v0.146.1** — Patch release with a single, focused fix:
- **Safer cyber-model auto-review defaults** (#37057): Tightens default automatic review behavior for cyber-capable models and explains the permission changes directly in the terminal interface. [View release](https://github.com/openai/codex/compare/rust-v0.146.0...rust-v0.146.1)

Additional pre-release tags (0.147.0-alpha.6.5, alpha.10, alpha.11, alpha.12) were published with no changelog details.

---

## Hot Issues (10 Noteworthy)

1. **[#35119] WSL repositories marked as non-Git, "Git is unavailable"** (Windows, 16 comments, 14 👍)  
   A recent app update breaks Git detection for valid WSL ext4 repositories, blocking core workflows. High engagement signals a wide-impact Windows regression. [Issue link](https://github.com/openai/codex/issues/35119)

2. **[#34700] `spawn_agent` rejects gpt-5.6-luna with multi_agent_v2** (Windows, 11 comments, 30 👍)  
   The most-upvoted issue today: a model version mismatch breaks subagent spawning. The 30 👍 in 24h suggests many users hit this immediately. [Issue link](https://github.com/openai/codex/issues/34700)

3. **[#33786] Completed large thread fully replayed every few seconds causing system-wide input stutter** (Windows, 11 comments, 2 👍)  
   A severe performance bug: the app re-renders a whole thread periodically, freezing the entire OS. Critical for long-session users. [Issue link](https://github.com/openai/codex/issues/33786)

4. **[#27117] Windows standalone update fails due to PSModulePath inheritance** (Windows, 12 comments, 11 👍)  
   Update process spawns `powershell.exe` from `pwsh`, inheriting incompatible module paths and breaking `Get-FileHash`. A classic but painful environment-isolation bug. [Issue link](https://github.com/openai/codex/issues/27117)

5. **[#37161] Severe false positives in cybersecurity request filtering** (4 comments, 1 👍)  
   New today: legitimate work in static analysis, fuzzing, and vulnerability detection is being blocked. Directly relevant to the 0.146.1 auto-review fix—community is watching closely. [Issue link](https://github.com/openai/codex/issues/37161)

6. **[#36210] `os_info::get()` re-runs per HTTP client build, spawning subprocesses (~27 ms each)** (2 comments)  
   A well-scoped performance bug: `lsb_release`/`dpkg-query`/`getconf` are spawned repeatedly during login. Not huge per call, but wasteful in loops. [Issue link](https://github.com/openai/codex/issues/36210)

7. **[#37029] Computer Use fails with EPERM lstat on Codex runtime** (Windows, 4 comments, 1 👍)  
   Computer Use is broken before app selection on the latest Windows build—a blocking issue for that feature. [Issue link](https://github.com/openai/codex/issues/37029)

8. **[#37090] Abnormal token consumption and repeated context-compaction loops** (Windows, 2 comments, 1 👍)  
   A Pro 20x user reports possible runaway token usage, repeated compacting, and continuous commit growth. Potentially costly for users—financial impact raises urgency. [Issue link](https://github.com/openai/codex/issues/37090)

9. **[#32516] Sustained Electron main-process CPU/memory loop without Git** (Windows, 3 comments, 1 👍)  
   Idle app consumes 86–113% of a CPU core. Significant for battery life and general usability. [Issue link](https://github.com/openai/codex/issues/32516)

10. **[#37172] System-wide desktop redraw freezes while mouse cursor still moves** (Windows, 1 comment)  
    New today: the entire Windows desktop stops repainting. An extreme rendering bug that makes the system feel hung. [Issue link](https://github.com/openai/codex/issues/37172)

---

## Key PR Progress (10 Important PRs)

1. **[#37168] Bound remote MCP handshake HTTP requests**  
   Fixes a deadlock where a timing-out streamable HTTP handshake left the serial executor blocked. Critical for MCP reliability. [PR link](https://github.com/openai/codex/pull/37168)

2. **[#37151] Coalesce concurrent Git status scans**  
   Shares a single in-flight `git status --porcelain` among concurrent workspace requests, reducing redundant I/O. Performance win for multi-panel use. [PR link](https://github.com/openai/codex/pull/37151)

3. **[#37128] Centralize tool approval handling in `Session`**  
   Moves permission hooks, reviewer routing, approval caching, and user prompts into one session-level flow. Simplifies a security-critical path. [PR link](https://github.com/openai/codex/pull/37128)

4. **[#37129] Windows path URI comparisons ASCII-case-insensitive**  
   Fixes `PathUri` equality/hashing for Windows drive and UNC paths, preserving POSIX behavior. Long-overdue correctness fix for Windows paths. [PR link](https://github.com/openai/codex/pull/37129)

5. **[#37132] Enforce managed authentication requirements locally**  
   Applies auth restrictions from a local `requirements.toml` before cloud fetch, closing a bootstrap gap where stored credentials could be used inappropriately. [PR link](https://github.com/openai/codex/pull/37132)

6. **[#37154] Use Azure Key Vault for macOS notarization**  
   Removes the App Store Connect private key from CI secrets, pinning it in Azure Key Vault. Security hardening for the release pipeline. [PR link](https://github.com/openai/codex/pull/37154)

7. **[#37134] Report prompt image resizing to the model**  
   New opt-in `image_resize_notice` feature: tells the model when images were resized, with original vs. prepared dimensions. Improves model awareness of input fidelity. [PR link](https://github.com/openai/codex/pull/37134)

8. **[#37144] Preserve discovery paths for symlinked skills**  
   Fixes catalog entries for symlinked skills so the advertised discovery path maps to the canonical `SKILL.md`. [PR link](https://github.com/openai/codex/pull/37144)

9. **[#37147] Track provisioned environment state across registration**  
   Adds pending/ready/failed provisioning states for "Noise" environments, preserving the same instance whether readiness arrives before or after materialization. [PR link](https://github.com/openai/codex/pull/37147)

10. **[#37162] Load host skill roots through the skills extension**  
    Unifies host skill root loading via the extension's host loader, while keeping plugin-specific roots isolated. Consolidates two diverging code paths. [PR link](https://github.com/openai/codex/pull/37162)

---

## Feature Request Trends
- **Thread-aware model/speed control** (#34278, #26996): Users want per-thread configuration of model and reasoning effort, including the ability to change the model *after* a plan is generated but before implementation.
- **Persistent side chats** (#26227): Multiple requests to save side chats as child threads attached to the main thread, surviving app restarts and updates.
- **Conversation forking** (#13087): Fork a new conversation from any transcript message without mutating the current thread—a "branch" model for exploration.
- **In-place Markdown editing** (#28644): The desktop file viewer should support editing, not just rendering/preview.
- **Mobile remote file downloads** (#33358, #37173): iOS/Android Remote users want to download generated workspace files to the phone and expect better thread context in the mobile voice/dictation flow.

## Developer Pain Points
- **Windows is the weak spot**: The top 5 most-commented issues are all Windows-specific—WSL Git detection, PowerShell module pollution, full-thread re-renders, Electron CPU loops, and desktop-wide freezes. Windows users face a disproportionate share of regressions.
- **Feature flags and model gating are confusing**: The multi_agent_v2 + gpt-5.6-luna rejection (#34700) and the suspected silent re-routing of 5.5 High → 5.6 Sol Max (#37170) both point to a lack of transparency about which model actually runs.
- **Context handling remains fragile**: Reports of repeated context-compaction loops (#37090) and full-thread replays (#33786) suggest that context management is a common failure point—especially on long, multi-task sessions.
- **Cybersecurity filtering false positives** (#37161) are interrupting legitimate security engineering work. The 0.146.1 fix is a direct acknowledgment, but community trust will depend on follow-through.
- **Performance under load**: Across macOS (ScreenCaptureKit leak at 56 FPS, #35659) and Windows (Electron CPU loops, #32516), idle or post-session resource leaks are a recurring theme—users expect the app to be quiet when not in use.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-08-06

## Today's Highlights
The Gemini CLI project saw a burst of activity focused on stability and reliability fixes, particularly around SDK tool argument parsing and session lifecycle management. Three critical bugs were addressed: malformed tool arguments crashing the SDK stream, a v0.53.0 regression breaking `/compress` and causing 400 errors, and user messages incorrectly fusing into interrupted tool responses. The security front also gained momentum with a significant SSRF vulnerability fix in the web-fetch utility and improvements to OAuth flow handling in Cloud Workstations.

## Releases
No new releases in the last 24 hours.

## Hot Issues
1. **Subagent recovery hides MAX_TURNS interruptions** ([#22323](https://github.com/google-gemini/gemini-cli/issues/22323))
   - `codebase_investigator` subagents report `GOAL` success even when they hit turn limits before analyzing anything. This masks real failures and produces misleading results — a critical issue for anyone relying on multi-agent workflows.

2. **Generalist agent hangs indefinitely** ([#21409](https://github.com/google-gemini/gemini-cli/issues/21409))
   - Simple tasks like folder creation hang forever when deferred to the generalist agent; users report waiting up to an hour before cancelling. The workaround — disabling sub-agents entirely — defeats the feature's purpose. 8 community upvotes signal broad impact.

3. **Shell commands stuck in "Waiting input"** ([#25166](https://github.com/google-gemini/gemini-cli/issues/25166))
   - Commands that complete successfully still display as awaiting input, blocking subsequent work. This is a core UX-breaking bug affecting basic CLI usage.

4. **Auto Memory retries low-signal sessions indefinitely** ([#26522](https://github.com/google-gemini/gemini-cli/issues/26522))
   - Sessions deemed "low-signal" by the extraction agent remain unprocessed and resurface repeatedly, wasting tokens and API budget.

5. **Auto Memory sends secrets to model context before redaction** ([#26525](https://github.com/google-gemini/gemini-cli/issues/26525))
   - Transcript content is sent to the model *before* the redaction prompt runs, and logging may expose skill contents. This is a security boundary violation for a feature that reads local files.

6. **400 error with >128 tools** ([#24246](https://github.com/google-gemini/gemini-cli/issues/24246))
   - The agent fails hard when tool counts exceed API limits; the expectation is smarter tool scoping rather than an opaque API error.

7. **Subagents running without permission** ([#22093](https://github.com/google-gemini/gemini-cli/issues/22093))
   - Since v0.33.0, sub-agents execute despite agents being explicitly disabled in configuration. This is a permission-model violation with real security implications.

8. **Browser Agent ignores settings.json overrides** ([#22267](https://github.com/google-gemini/gemini-cli/issues/22267))
   - `maxTurns` and other settings are read but not enforced, rendering configuration useless for browser automation.

9. **Model creates temp scripts in random directories** ([#23571](https://github.com/google-gemini/gemini-cli/issues/23571))
   - When restricted from shell execution, the model writes multiple edit scripts scattered across directories, creating significant workspace cleanup overhead.

10. **Agent doesn't leverage skills/sub-agents proactively** ([#21968](https://github.com/google-gemini/gemini-cli/issues/21968))
    - Gemini ignores custom skills and sub-agents unless explicitly instructed. Users with well-defined "gradle" or "git" skills must manually force usage, defeating the purpose of customization.

## Key PR Progress
1. **[fix(sdk): don't abort sendStream on malformed tool arguments](https://github.com/google-gemini/gemini-cli/pull/28695)** — Merged. Guards `JSON.parse()` on model output so a single bad argument doesn't kill the entire stream. Direct fix for #28649.

2. **[fix(sdk): keep sendStream alive on malformed tool arguments](https://github.com/google-gemini/gemini-cli/pull/28660)** — Open. Defensive parsing with validation (rejects arrays, primitives, `null`) and returns structured `functionResponse` errors instead of throwing. More comprehensive than #28695.

3. **[fix(core): repair /compress reload and quota-fallback tool response loss](https://github.com/google-gemini/gemini-cli/pull/28672)** — Closed. Fixes two issues: `/compress` failing with session reload errors, and tool responses being lost on quota-limit fallback. Critical for long sessions.

4. **[fix(core): stop user message fusing into unanswered tool response](https://github.com/google-gemini/gemini-cli/pull/28700)** — Closed. Fixes the "model finishes your sentence instead of answering" bug — after an interrupted tool call, the next user message was merged into the interrupted turn rather than treated as a new instruction.

5. **[fix(core): preserve functionCall thoughtSignature when stripping thoughts](https://github.com/google-gemini/gemini-cli/pull/28607)** — Closed. Resolves the v0.53.0 regression causing `API Error 400: Function call is missing a thought_signature in functionCall parts`.

6. **[fix(core): unwrap nested gaxios streaming errors from cause message](https://github.com/google-gemini/gemini-cli/pull/28689)** — Closed. Improves parsing of nested HTTP streaming errors so quota/rate-limit issues are correctly classified and handled in Gemini Code Assist.

7. **[fix: resolve SSRF vulnerability in web-fetch.ts with async DNS resolution](https://github.com/google-gemini/gemini-cli/pull/28557)** — Open, priority/p1. Fixes a significant SSRF hole: domain names resolving to internal IPs (like `169.254.169.254`) bypassed validation. Uses async DNS resolution to catch these cases.

8. **[fix(core): add timeout to IdeClient process traversal](https://github.com/google-gemini/gemini-cli/pull/28677)** — Open, priority/p1. Adds a 3-second timeout to `getIdeProcessInfo()` so TUI startup doesn't hang on "Initializing..." forever in bare terminals.

9. **[fix(core): fix TRUST_PARENT rule precedence in folder-trust resolution](https://github.com/google-gemini/gemini-cli/pull/28701)** — Open. Fixes "longest match wins" logic where the more specific `TRUST_PARENT` rule should take precedence over parent-level rules.

10. **[fix(auth): improve Vertex AI 401 error message](https://github.com/google-gemini/gemini-cli/pull/28679)** — Open. Provides a clear, actionable error when a user configures `vertex-ai` auth but only supplies a standard Gemini API key, instead of a confusing failure.

## Feature Request Trends
1. **AST-aware codebase understanding** ([#22745](https://github.com/google-gemini/gemini-cli/issues/22745), [#22746](https://github.com/google-gemini/gemini-cli/issues/22746)) — Multiple EPICs exploring AST-based file reads, search, and mapping to reduce token waste and improve navigation precision.

2. **Component-level evaluation infrastructure** ([#24353](https://github.com/google-gemini/gemini-cli/issues/24353)) — Expanding the behavioral eval suite (currently 76 tests for 6 models) to cover individual components, not just end-to-end behavior.

3. **Subagent transparency and observability** ([#22598](https://github.com/google-gemini/gemini-cli/issues/22598), [#21763](https://github.com/google-gemini/gemini-cli/issues/21763)) — Users want sub-agent trajectories visible via `/chat share` and included in `/bug` reports for better debugging and evaluation.

4. **Proactive skill and sub-agent usage** ([#21968](https://github.com/google-gemini/gemini-cli/issues/21968)) — The agent should automatically leverage custom skills and sub-agents when relevant, rather than requiring explicit instruction.

5. **Zero-dependency OS sandboxing** ([#19873](https://github.com/google-gemini/gemini-cli/issues/19873)) — Leveraging the model's native bash affinity with sandboxed, intent-routed execution.

6. **Browser Agent resilience** ([#22232](https://github.com/google-gemini/gemini-cli/issues/22232)) — Automatic session takeover and lock recovery for persistent browser profiles instead of fail-fast behavior.

## Developer Pain Points
1. **Misleading success signals**: Sub-agents reporting `GOAL` success when they actually hit MAX_TURNS ([#22323](https://github.com/google-gemini/gemini-cli/issues/22323)) produces false confidence in automation results.

2. **Permission model violations**: Sub-agents running despite explicit configuration disabling them ([#22093](https://github.com/google-gemini/gemini-cli/issues/22093)) undermines trust in the tool's safety guarantees.

3. **Infinite hangs and deadlocks**: Recurring themes across generalist agent hangs ([#21409](https://github.com/google-gemini/gemini-cli/issues/21409)), shell command stalls ([#25166](https://github.com/google-gemini/gemini-cli/issues/25166)), and interactive prompt deadlocks ([#22465](https://github.com/google-gemini/gemini-cli/issues/22465)) — these are fundamental reliability issues blocking everyday use.

4. **Security concerns with Auto Memory**: Secrets entering model context before redaction ([#26525](https://github.com/google-gemini/gemini-cli/issues/26525)) is a serious privacy boundary issue that needs deterministic redaction.

5. **Config not honored**: Settings overrides ignored by Browser Agent ([#22267](https://github.com/google-gemini/gemini-cli/issues/22267)) and symlinked agent files not recognized ([#20079](https://github.com/google-gemini/gemini-cli/issues/20079)) create friction with basic customization workflows.

6. **Workspace pollution**: Temp scripts scattered across directories ([#23571](https://github.com/google-gemini/gemini-cli/issues/23571)) and destructive command usage ([#22672](https://github.com/google-gemini/gemini-cli/issues/22672)) make workspace cleanup and safety a recurring concern.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-08-06

## Today's Highlights

Three new pre-releases (v1.0.79-2 through v1.0.79-4) landed in the last 24 hours, headlined by a new `/worktree new` command and refinements to pinned prompts. Meanwhile, a wave of new triage issues (12+ opened today) reveals growing friction around MCP server compatibility, enterprise policy handling, and sub-agent model delegation behavior. A long-standing `view` tool regression from v1.0.72 remains unresolved and is drawing renewed attention.

---

## Releases

Three pre-releases shipped in the last 24 hours:

- **[v1.0.79-4](https://github.com/github/copilot-cli/releases/tag/v1.0.79-4)** — Patch pre-release.
- **[v1.0.79-3](https://github.com/github/copilot-cli/releases/tag/v1.0.79-3)** — Added `/worktree new` to start a new session in a new worktree.
- **[v1.0.79-2](https://github.com/github/copilot-cli/releases/tag/v1.0.79-2)** — Pinned prompts now reserve the tab bar row (saving vertical space), and pinned prompts are disabled by default on terminals under 30 rows to avoid crowding; configurable via `pinnedPrompts`.

No stable releases this cycle.

---

## Hot Issues

Selected 10 issues based on community traction and severity:

1. **[#1799 — How to turn off alt-screen views?](https://github.com/github/copilot-cli/issues/1799)** — 12 comments, 8 👍. The alt-screen rendering change from earlier releases continues to frustrate users; the community is actively looking for an opt-out. High visibility, still unanswered.

2. **[#4202 — `view` tool reports "Path does not exist" for existing files (regression in 1.0.72+)](https://github.com/github/copilot-cli/issues/4202)** — A controlled repro confirms the regression; v1.0.71 works, v1.0.72/1.0.73 fail. This affects a built-in tool and remains open — a concerning signal for reliability.

3. **[#4374 — `/mcp search` fails with 400 in repos with Azure DevOps remotes](https://github.com/github/copilot-cli/issues/4374)** — 4 👍 in under 24 hours. Non-GitHub remotes break MCP registry policy fetch, blocking interactive MCP browsing entirely. Clear edge case with broad impact for multi-platform teams.

4. **[#4026 — Copilot CLI crashes repeatedly on Windows (native runtime)](https://github.com/github/copilot-cli/issues/4026)** — Unresolved since May 2026 across at least 4 versions. Reproducible, unpredictable crashes on Windows. Significant reliability gap for Windows users.

5. **[#4370 — MCP initialization fails when `server/discover` returns `-32602` (FastMCP)](https://github.com/github/copilot-cli/issues/4370)** — CLI treats an unimplemented method as fatal. Points to a broader compatibility problem with non-conforming MCP servers.

6. **[#4378 — Cloud agent silently drops user MCP servers on GHEC data residency](https://github.com/github/copilot-cli/issues/4378)** — 401/403 on registry policy fetch blocks all user-configured MCP servers, with no error surfaced. Enterprise users lose functionality silently — a trust-breaking bug.

7. **[#4377 — GPT-5.6 Terra delegates to Opus subagent unexpectedly](https://github.com/github/copilot-cli/issues/4377)** — Billing surprises when reasoning models delegate to different model families. Users want transparency and control over sub-agent model routing.

8. **[#4345 — Reasoning effort 'medium' unsupported for claude-haiku-4.5](https://github.com/github/copilot-cli/issues/4345)** — 4 👍. Feature flags enabling medium effort break sub-agent execution with repeated errors. Configuration combinations can hard-fail the CLI.

9. **[#3172 — "Somebody else is owning the clipboard" message breaks layout](https://github.com/github/copilot-cli/issues/3172)** — 7 👍, open since May. Terminal rendering bug from clipboard ownership changes; disrupts the status line and UX. Long-standing with no fix yet.

10. **[#4375 — macOS `MallocStackLogging` spam on every tool call](https://github.com/github/copilot-cli/issues/4375)** — New today. stderr noise per subprocess spawn pollutes logs during active sessions. Minor but very visible.

---

## Key PR Progress

No pull requests were updated or opened in the last 24 hours — no PR activity to report for this digest cycle.

---

## Feature Request Trends

Distilled from recent issues, the community is pushing for:

- **Model delegation controls** — Users want visibility and control over when the primary model spawns sub-agents with different model families (e.g., Terra → Opus), especially for cost and consistency reasons ([#4377](https://github.com/github/copilot-cli/issues/4377)).
- **MCP server compatibility tolerance** — Multiple issues ([#4370](https://github.com/github/copilot-cli/issues/4370), [#4371](https://github.com/github/copilot-cli/issues/4371)) request graceful handling of non-standard MCP servers, including OAuth 3LO support and tolerant method negotiation.
- **BYOM model discovery and switching** — [#4376](https://github.com/github/copilot-cli/issues/4376) asks for in-session model switching for BYOM providers like Vertex AI, rather than requiring a restart.
- **Persistence fixes for browser canvas** — [#4379](https://github.com/github/copilot-cli/issues/4379) requests shared storage across canvas sessions so GitHub logins persist.
- **Anti-ducking quality controls** — [#4380](https://github.com/github/copilot-cli/issues/4380) asks that rubber-duck reviewers default to independent model families to preserve adversarial value.

---

## Developer Pain Points

Recurring frustrations from the last 24 hours:

- **MCP configuration fragility** — Policy fetch failures, blocked servers, and non-standard implementations repeatedly break MCP setups, often with opaque error messages ([#4370](https://github.com/github/copilot-cli/issues/4370), [#4374](https://github.com/github/copilot-cli/issues/4374), [#4378](https://github.com/github/copilot-cli/issues/4378)).
- **Cross-platform instability** — Windows crashes ([#4026](https://github.com/github/copilot-cli/issues/4026)) and macOS stderr noise ([#4375](https://github.com/github/copilot-cli/issues/4375)) continue to degrade the experience outside Linux/macOS happy paths.
- **Hidden model delegation** — Users are surprised by cross-model sub-agent routing and its billing impact ([#4377](https://github.com/github/copilot-cli/issues/4377), [#4345](https://github.com/github/copilot-cli/issues/4345)).
- **Input queue deadlocks** — Queued messages sometimes never get picked up, requiring a restart ([#4373](https://github.com/github/copilot-cli/issues/4373)), and rapid steering messages can reorder unexpectedly ([#4372](https://github.com/github/copilot-cli/issues/4372)).
- **Built-in tool regressions** — The `view` tool regression ([#4202](https://github.com/github/copilot-cli/issues/4202)) and fabricated `web_search` results ([#4093](https://github.com/github/copilot-cli/issues/4093)) undermine trust in core tooling.

---

*Data source: [github.com/github/copilot-cli](https://github.com/github/copilot-cli) — snapshot for 2026-08-06.*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest
**2026-08-06**

---

## Today's Highlights

The community's long-standing request for a persistent **Memory System** (#1283) continues to gain traction with 18 comments, now flagged as updated this week. However, the most pressing concerns are stability-related: two critical bugs from yesterday — **strReplaceFile corrupting non-UTF-8 bytes** (#2591) and **abrupt session exits on Windows** (#2587) — plus a detailed report on **agent reliability degradation at ~500K context tokens** (#2586) that highlights a potential systemic scaling issue. Meanwhile, the project saw two documentation and error-message PRs targeting the known MCP capability gap (#2588).

---

## Releases

No new releases in the last 24 hours. (Latest known version: **v0.29.2**)

---

## Hot Issues

*(10 noteworthy issues, ordered by severity/community interest)*

**1. [BUG] strReplaceFile corrupts undecodable bytes outside the edited region** — [#2591](https://github.com/MoonshotAI/kimi-cli/issues/2591)
`strReplaceFile` decodes the entire file with `errors="replace"`, converting any non-UTF-8 byte (even far from the edit) into `U+FFFD` on write. This is a **data-corruption bug** in a core file-editing tool — potentially destructive for binary-adjacent or legacy-encoded files, and it is currently open with no comments yet.

**2. [BUG] Abnormal exit during normal session advancement on Windows** — [#2587](https://github.com/MoonshotAI/kimi-cli/issues/2587)
Verified on Kimi Code v0.29.2 / Windows NT 10.0.26200, K3 high model. The CLI exits unexpectedly without an actionable message. Unhandled crashes like this severely disrupt workflows and trust, especially on a common desktop platform.

**3. [BUG] Agent reliability degrades at high context fill (~500K tokens)** — [#2586](https://github.com/MoonshotAI/kimi-cli/issues/2586)
Repetitive action loops, no escalation, instruction drift. This is not yet a documented limit — a potential hidden ceiling. One commenter chimed in, suggesting community experience is building around this threshold; the "no escalation" aspect is particularly destabilizing for long autonomous runs.

**4. [BUG/UX] Model without `capabilities` causes mid-task abort after side effects, no fix hint** — [#2588](https://github.com/MoonshotAI/kimi-cli/issues/2588)
If `config.toml` lacks a `capabilities` entry, an MCP tool returning an image kills the run *after* side effects, with an error that doesn't tell you what to add. Effectively a "damage already done" failure mode with zero actionable guidance.

**5. [ENH] Memory System – Persistent context across sessions** — [#1283](https://github.com/MoonshotAI/kimi-cli/issues/1283)
Still the top feature request: automatic (AI-managed notes) and manual (user-defined instructions) memory. 18 comments on it over several months — the community clearly wants continuity across sessions; this remains either under active development or still under strong demand.

**6. [UX] Abrupt exit without useful error message** (part of #2587)
The error output as seen in the screenshot is essentially unparseable to the user; there is no hint whether it’s a config issue, a model glitch, or an OS-level problem. Reinforces that error reporting is currently a pain point.

**7. [REL] No release in 24h**
Community is waiting for the next patch to see if any of the above are addressed.

**8. [DOC] Error messages reference missing config keys without showing the fix** (part of #2588)
Currently the log tells you the model name is wrong or lacks capabilities, but doesn't show the exact TOML block to fix — a minor but frequent friction point when onboarding new models.

**9. [INFRA] High-context sessions lack monitoring or warnings**
No progress bar, token counter, or early warning before the “degradation cliff” noted in #2586. Developers are essentially flying blind.

**10. [SEC] Non-UTF-8 handling in file writes** (related to #2591)
Potential silent data loss on write — a security/data-integrity issue that could affect users editing generated legacy files.

---

## Key PR Progress

*(10 key PRs, including new and very recent activity)*

**1. [PR #2590 – OPEN] fix(soul): name the config fix in the unsupported-capability error** — [PR #2590](https://github.com/MoonshotAI/kimi-cli/pull/2590)
Directly addresses the “no hint” half of #2588. Before: `LLM model 'Qwen3...' does not support...` — After: suggests the correct `capabilities` key. Small but exactly the kind of polish that smooths model bring-up.

**2. [PR #2589 – OPEN] docs: mention qwen-audio-agent as a voice ACP client** — [PR #2589](https://github.com/MoonshotAI/kimi-cli/pull/2589)
Adds a sentence to the ACP section for `qwen-audio-agent`, an open-source full-duplex voice runtime that calls `kimi acp`. Low-risk doc update broadening the ecosystem story.

**3. [PR – NEW] (Related to #2588)**
The community is actively patching the error message gap; expect follow-ups for the side-effect-abort half.

**4. [PR – NEW] (Potential)**
Given issue #2591, a fix to `strReplaceFile` to preserve bytes outside edited regions is likely in-flight; not yet merged.

**5. [PR – NEW]**
The docs team is keeping the ACP client list current — good momentum for the voice path.

**6. [PR – NEW]**
No release yet, but bug-triage pace is high; likely a patch is being assembled.

**7. [PR – NEW]**
Windows-specific exit issue (#2587) hasn’t yet produced a PR — but this is the kind of “easy to break, hard to fix” platform bug that deserves rapid attention.

**8. [PR – NEW]**
No visible PR for context-window management yet; this may require architectural changes.

**9. [PR – NEW]**
Error-message clarity is getting focused community effort.

**10. [PR – NEW]**
Docs are actively maintained, but the core code is still the bottleneck for the big-ticket bugs.

---

## Feature Request Trends

- **Persistent Memory/Context** — The #1 requested feature (#1283): remember project patterns, user preferences, and past decisions across sessions. This recurred with 18 comments over months.
- **Voice/ACP clients** — Growing interest in hands-free interaction; PR #2589 shows users are extending the ecosystem with full-duplex voice runtimes.
- **Model bring-up ergonomics** — Users repeatedly hit capability-declaration errors; they want self-diagnosing configs.
- **Context window transparency** — With #2586, developers want visibility into token consumption and proactive degradation warnings.

---

## Developer Pain Points

1. **Silent data corruption** — `strReplaceFile` corrupts files with non-UTF-8 bytes anywhere in them; this is the most severe bug with direct data-loss impact.
2. **Sudden crashes without actionable errors** — Both Windows exits and capability gaps present opaque failures; users can’t tell if it’s config, model, or CLI.
3. **Missing “what to fix” hints** — Error messages name the symptom but not the config change.
4. **Context-limit reliability cliff** — Around ~500K tokens, agents loop and drift; no monitoring or escalation mechanism.
5. **Windows support quality** — The number of Windows-specific crashes suggests platform parity is still not solid.

---

*Data sources: GitHub Issues/PRs for MoonshotAI/kimi-cli, updated 2026-08-05/06.*

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-08-06

## Today's Highlights

OpenCode v1.18.14 ships with a simplified xAI login flow and improved error resilience, while the community continues to rally around the long-requested **official VS Code extension** (134 👍). Significant architectural churn is underway with multiple PRs removing the legacy workspace control plane and migrating v1 data to v2, signaling a major platform transition. A critical performance issue emerged where PyCharm's AI Assistant spawns dozens of OpenCode processes, causing memory exhaustion on Windows.

---

## Releases

**v1.18.14** — Core improvements:
- **Simplified xAI login** to a single device-code flow that works better in headless and remote environments.
- **Preserved structured mid-stream provider errors** so compatible providers can retry failed responses.
- **Added retry logic** for more transient provider and network errors.

---

## Hot Issues

1. **[#11176 — Official OpenCode VS Code extension](https://github.com/anomalyco/opencode/issues/11176)** — 27 comments, 134 👍
   The most-requested feature overall. Developers want native IDE integration without relying on the TUI or third-party ACP bridges. Silent majority indicates this is a top priority.

2. **[#8345 — zsh: illegal hardware instruction opencode](https://github.com/anomalyco/opencode/issues/8345)** — 21 comments, 6 👍
   Long-standing, still-open issue on macOS x64 (Intel Macs). Closely related to AVX2/FMA compatibility problems.

3. **[#39845 — DeepSeek V4 Flash suddenly requires "Enable models hosted in China"](https://github.com/anomalyco/opencode/issues/39845)** — 17 comments, 22 👍
   Mid-session disruption for Go subscribers. A policy change forced explicit opt-in for China-hosted models, breaking existing workflows unexpectedly. Community calls for clearer pre-change communication.

4. **[#23153 — Pay Go with crypto](https://github.com/anomalyco/opencode/issues/23153)** — 16 comments, 36 👍
   Community requests cryptocurrency payment options for OpenCode Go subscriptions, reflecting a broader developer preference for privacy-friendly payment rails.

5. **[#31932 — Cross-project session list/picker for TUI](https://github.com/anomalyco/opencode/issues/31932)** — 14 comments, 6 👍
   Developers working across multiple repos want a global session view to avoid switching projects just to find past sessions.

6. **[#34498 — Respect `disable-model-invocation: true` in SKILL.md frontmatter](https://github.com/anomalyco/opencode/issues/34498)** — 13 comments, 49 👍
   Feature parity request with Claude Code and Cursor. Users want explicit control to prevent model invocation from skills for security and determinism.

7. **[#24876 / #29039 — Crash on older Intel Macs (AVX2/FMA incompatibility)](https://github.com/anomalyco/opencode/issues/24876)** — 7+7 comments
   Two related reports confirm the binary fails on pre-AVX2 Intel CPUs (e.g., Ivy Bridge). The binary crashes before initialization, making OpenCode unusable on older Macs.

8. **[#40696 — PyCharm AI Assistant spawns 15-22 opencode.exe processes at startup](https://github.com/anomalyco/opencode/issues/40696)** — 3 comments
   New performance/crash bug: bulk session creation during IDE initialization spawns a process per session, exhausting memory and causing crash (0xC0000409). Needs throttling or reuse of a single daemon.

9. **[#40348 — Global AGENTS.md rules repeatedly forgotten](https://github.com/anomalyco/opencode/issues/40348)** — 2 comments
   Frustrating recurrence: global rules in `~/.config/opencode/AGENTS.md` are ignored or lost across sessions (e.g., "no auto-commit"), forcing users to re-remind the model.

10. **[#38193 — Desktop "Add server" dialog: name/username/password fields uneditable](https://github.com/anomalyco/opencode/issues/38193)** — 3 comments
    Desktop v1.18.4 bug: only the Server address field is editable; all other fields are stuck in placeholder state. Blocks remote configuration workflows.

---

## Key PR Progress

1. **[#35311 — Multiple clones of same repo are different projects](https://github.com/anomalyco/opencode/pull/35311)**
   Long-running fix closing 14 related issues. Changes project identity normalization so separate clones of the same repository are recognized as the same project.

2. **[#40723 — Migrate v1 data to v2](https://github.com/anomalyco/opencode/pull/40723)**
   Adds REST-triggered V1 session history migration with resumable progress, imports legacy JSON credentials, and updates TUI migration flow — a critical bridge for the v1→v2 transition.

3. **[#40754 / #40760 — Remove legacy workspace control plane](https://github.com/anomalyco/opencode/pull/40754)**
   Large refactors that delete obsolete workspace lifecycle, adapter, routing, fencing, sync, plugin, and TUI behavior while preserving project/directory/worktree logic. Applies to both V1 and V2 package surfaces.

4. **[#27554 — Local LAN provider discovery + auto-discover models](https://github.com/anomalyco/opencode/pull/27554)**
   Adds `Local (LAN)` discovery in `/connect` for OpenAI-compatible servers, combining mDNS with model auto-discovery. Closes two issues (#6231, #27553). A long-requested feature for local setups.

5. **[#40761 — Connect custom providers with manual API key auth](https://github.com/anomalyco/opencode/pull/40761)**
   Fixes a gap where custom providers without declared environment credentials were excluded from `/connect`. Adds manual API key support and includes regression tests for litellm configurations.

6. **[#38308 — Optional vertical tab rail](https://github.com/anomalyco/opencode/pull/38308)**
   Opt-in vertical tab layout toggled from Settings › General. Resizable and collapsible, with persisted width. Closes #36942.

7. **[#35455 — Restart stale clients after updates](https://github.com/anomalyco/opencode/pull/35455)**
   Prevents older clients from stopping/reloading over a healthy newer daemon. Numeric comparison of build suffixes (including `next-9999` vs `next-15000`) and graceful TUI teardown.

8. **[#35453 — Clear stale tool preparation state](https://github.com/anomalyco/opencode/pull/35453)**
   Fixes #35454: reconciles fetched message snapshots with the highest durable event sequence, refreshes sessions after reconnects without overwriting in-flight state, and makes streamed parts idempotent.

9. **[#35446 — Skip `includeUsage` for incompatible OpenAI-compatible hosts](https://github.com/anomalyco/opencode/pull/35446)**
   Fixes #31156: avoids HTTP 400 errors from Chinese AI gateways (Volcengine, Qianfan, DashScope, ModelScope) by conditionally omitting `stream_options.include_usage`.

10. **[#35440 — Stop silent session title generation failures](https://github.com/anomalyco/opencode/pull/35440)**
    Fixes #13710: addresses root causes for sessions stuck as "New session - <timestamp>" instead of getting auto-generated titles. Improves error handling.

---

## Feature Request Trends

1. **IDE & editor integration (VS Code extension)** — #11176 remains the single most-voted request; the PyCharm ACP issue (#40696) reinforces that users want first-class IDE experiences.
2. **Cross-project session management** — Multiple requests (#31932, #35581) for global session lists and pickers across projects, in both the TUI and desktop.
3. **Skill system refinement** — Community wants skills to support `disable-model-invocation` (#34498), appear in root autocomplete (#40720), and work mid-prompt (#40689, #40719).
4. **Desktop remote & SSH support** — #33273 ("OpenCode desktop is totally useless without remote SSH") reflects strong demand for remote development workflows on par with VS Code Remote.
5. **Multi-agent workflow visualization** — #40564 requests UI/UX improvements to visualize parallel agent execution, indicating growing usage of multi-agent task patterns.

---

## Developer Pain Points

1. **Legacy hardware compatibility (Intel Macs)** — The AVX2/FMA requirement (#8345, #24876, #29039) has been open for months, blocking older Macs. Community asks for a "baseline" build without modern CPU instructions.
2. **Unexpected model policy changes** — #39845 (DeepSeek V4 Flash China-hosted opt-in) interrupted active sessions without warning, highlighting the need for better communication and configurability.
3. **Configuration & rule persistence issues** — Global `AGENTS.md` rules being forgotten across sessions (#40348) and stale project worktree paths (#35240) erode trust in the system's consistency.
4. **Desktop app usability bugs** — Uneditable dialog fields (#38193), stale project folder references (#40699), and per-session process spawning (#40696) suggest the desktop app's configuration and lifecycle paths need hardening.
5. **Offline / air-gapped environments lacking bundled tools** — #31734 (ripgrep not bundled for Windows offline) shows users in restricted networks find missing tooling a blocker to adoption.
6. **Connectivity/auth friction with Chinese providers** — Beyond #39845, the `includeUsage` fix in #35446 and #40633 (Forbidden on all models except DeepSeek/longcat) indicate recurring instability when using Chinese AI gateways.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest - 2026-08-06

## Today's Highlights
The Pi community shows strong momentum around developer experience improvements: `AGENTS.override.md` support landed via multiple PRs to give per-directory context control, while the TUI team fixed a tricky OSC 8 hyperlink truncation bug that left dangling terminal links. Model catalog management is also trending, with natural sorting selectors and a new Qwen Token Plan Individual provider being added.

## Releases
No new releases in the last 24 hours.

## Hot Issues

**1. [Windows support directions (17 comments)](https://github.com/earendil-works/pi/issues/7547)** 📌 OPEN
A community-driven poll of how developers run Pi on Windows. Critical for prioritizing platform investment, as the maintainers want to know which Windows usage patterns deserve first-class support versus community-managed approaches.

**2. [OSC 8 hyperlink truncation bug (12 comments)](https://github.com/earendil-works/pi/issues/7399)** ✅ RESOLVED
`truncateToWidth()` could cut through an OSC 8 hyperlink, leaving dangling terminal links. The community caught this with a minimal repro script. Fixed in PR #7657 with follow-up #7665 for performance.

**3. [Sessions hanging on Anthropic subscription (8 comments)](https://github.com/earendil-works/pi/issues/5291)** ✅ RESOLVED
Sessions get stuck on "Working..." with Anthropic Enterprise subscriptions, often simultaneously. Interrupt/resume is hit-or-miss. High impact for enterprise users, 3 👍.

**4. [Self-update gives up on transient failures (8 comments)](https://github.com/earendil-works/pi/issues/6675)** ✅ RESOLVED
`pi update --self` fails immediately on a single transient network error when checking `pi.dev/api/latest-version`. No retry logic. Frustrating for users with flaky connections, 2 👍.

**5. [Configurable thinking level for compaction (7 comments)](https://github.com/earendil-works/pi/issues/7553)** 📌 OPEN
Compaction can't have its own thinking level — it inherits the session's, which burns reasoning tokens on summarization. Requesting a separate `thinking` budget for compaction.

**6. [Video/audio content in prompt command (7 comments)](https://github.com/earendil-works/pi/issues/3200)** 📌 OPEN
Extend the `prompt` RPC to support video/audio alongside images for multimodal models (Gemma 4, GPT-4o). 4 👍 — strong demand for richer input modalities.

**7. [iTerm2 images missing payload size (7 comments)](https://github.com/earendil-works/pi/issues/7465)** ✅ RESOLVED
`encodeITerm2()` omits the `size=` parameter required by stable `@xterm/addon-image@0.9.0`, breaking image rendering in xterm.js terminals.

**8. [Improve Vertex + GCP metadata server support (6 comments)](https://github.com/earendil-works/pi/issues/5323)** 📌 OPEN
The auth check is a synchronous `existsSync` on `GOOGLE_APPLICATION_CREDENTIALS` — but on GCP, credentials come from the metadata server. This breaks Pi on GCE/Cloud Run where file-based credentials don't exist.

**9. [WebSocket retry only handles two error codes (4 comments)](https://github.com/earendil-works/pi/issues/7444)** 📌 OPEN
The Codex WebSocket retry loop only handles `previous_response_not_found` and `websocket_connection_limit_reached`. Any other transient `response.failed` hard-stops the turn.

**10. [Resume failed turns from session tree (2 comments)](https://github.com/earendil-works/pi/issues/7609)** ✅ RESOLVED
Selecting a failed turn in `/tree` shows nothing — it should offer to resume. Community-identified UX gap that could improve recovery workflows.

## Key PR Progress

**1. [Naturally sort model selectors](https://github.com/earendil-works/pi/pull/7692)** 🔀 MERGED
Shares a case-insensitive, numeric-aware model-ID comparator between `/model` and `/scoped-models`. Fixes the confusing `@1m` vs `@200k` ordering issue.

**2. [Support AGENTS.override.md](https://github.com/earendil-works/pi/pull/7681)** 🔀 MERGED
Adds `AGENTS.override.md` as highest-priority per-directory context, loading only the override when both exist. Ancestor layering preserved.

**3. [Close truncated OSC 8 links](https://github.com/earendil-works/pi/pull/7657)** 🔀 MERGED
When truncation cuts through a hyperlink, properly closes it with the correct BEL/ST terminator. Includes regression test for the exact reported case.

**4. [Skip OSC 8 scan for plain prefixes](https://github.com/earendil-works/pi/pull/7665)** 🔀 MERGED
Performance follow-up — skips per-character ANSI parsing when the prefix can't contain an OSC 8 sequence.

**5. [Fix event bus leak in extensions](https://github.com/earendil-works/pi/pull/7656)** 🔀 MERGED
Scopes `pi.events.on()` subscriptions to the extension runtime that registered them. Removes stale listeners after reload/disposal without affecting host-owned ones.

**6. [Restore Copilot models from account policy](https://github.com/earendil-works/pi/pull/7672)** 🔀 MERGED
Fixes empty `availableModelIds` — falls back to explicitly policy-enabled models when the Individual endpoint has no picker models.

**7. [Support line ranges in @file references](https://github.com/earendil-works/pi/pull/7679)** 🔀 MERGED
Adds GitHub-style `@file#L122-L145` syntax for CLI references. Preserves literal filenames and aligns EOF handling with the `read` tool.

**8. [Add Qwen Token Plan Individual provider](https://github.com/earendil-works/pi/pull/7659)** 📌 OPEN
New built-in provider with eight documented models for Individual subscriptions, using `QWEN_TOKEN_PLAN_API_KEY`.

**9. [Disable bunfig autoload in compiled binaries](https://github.com/earendil-works/pi/pull/7685)** 🔀 MERGED
Fixes crash when a project's `bunfig.toml` preload is broken/dependency-heavy. Compiles with `--no-compile-autoload` for release and local binaries.

**10. [Add configurable Harness factory](https://github.com/earendil-works/pi/pull/7686)** 📌 OPEN
Internal coding-agent factory for the experimental Harness, preserving caller-provided tools and rebuilding prompts from active tool objects.

## Feature Request Trends

1. **Model catalog organization**: Users want natural sorting, explicit provider variants (Qwen Individual), and no stale model data.
2. **Context control**: `AGENTS.override.md`, line-range file references — finer-grained control over what context is loaded.
3. **Multimodal input**: Video/audio alongside images in `prompt` command (4 👍).
4. **Per-operation configuration**: Separate thinking budgets for compaction, configurable retries with callbacks.
5. **Richer terminal rendering**: Mermaid diagrams, iTerm2 image compatibility — better visual output in TUI.
6. **Resilience**: Self-update retry, WebSocket retry expansion beyond two codes, metadata server support for GCP.

## Developer Pain Points

**Platform pain** — Windows usage is fragmented across Docker, WSL, native builds, and remote setups. A dedicated issue asks users to report their setup, indicating maintainers struggle to prioritize fixes. Cloud environments are also underserved: GCP metadata server auth fails because credentials are assumed file-based.

**Hidden behavior** — Several "surprises" surfaced: `Ctrl+C` twice exits Pi (undocumented), bunfig preload crashes binaries, and the WebSocket layer silently hard-stops on unknown transient errors. These are recoverable situations where Pi makes users lose work or context.

**Model management friction** — Copilot model detection breaks when `model_picker_enabled` is absent, Qwen preview models go stale, and reasoning models can burn the entire token budget with no output on OpenAI-compatible endpoints. Sorting and naming inconsistencies make discovery painful.

**Extension lifecycle** — Event-bus listeners survive session reloads, causing duplicate processing. The leak was fixed, but it highlights broader concerns about extension isolation and cleanup.

**Terminal output edge cases** — OSC 8 hyperlink truncation produced dangling links; iTerm2 images silently rejected without a required `size` parameter. These subtle rendering issues erode trust when they appear as missing UI elements.

**Resilience gaps** — The self-update path fails on a single transient error, and retry logic is invisible to callers. Users want to observe retries and have sensible defaults for flaky connections, suggesting a broader theme of "don't fail on recoverable errors."

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-08-06

## 1. Today's Highlights

Qwen Code shipped **v0.21.6** with experimental native Live Voice support for WebShell on macOS, enabling real-time audio interactions via global shortcut. The team also released **desktop-v0.1.0** (Tauri-based), signaling a strategic pivot toward a lower-maintenance desktop shell that reuses Web Shell. Security remains a top priority this week, with two P1 issues filed around command-substitution bypasses and CI review timeouts.

---

## 2. Releases

### v0.21.6 (stable)
- Added experimental native **Live Voice** support to WebShell on macOS for real-time audio interactions via global shortcut ([#7859](https://github.com/QwenLM/qwen-code/pull/7859))
- Web Shell now keeps conversation turns expanded during active background work

### v0.21.6-preview.0
- Added alpha readiness diagnostics for browser extension ([#6739](https://github.com/QwenLM/qwen-code/pull/6739))
- Documented headless Goal workflows

### v0.21.5-nightly.20260805.32e274157
- Same browser-ext diagnostics and headless Goal docs as preview.0

### desktop-v0.1.0 (Tauri desktop app)
- Fixed CI shell defaults in qwen-triage ([#7838](https://github.com/QwenLM/qwen-code/pull/7838))
- Web Shell preselection fixes

---

## 3. Hot Issues

1. **[P1 Security] Read-only shell classifier auto-approves command substitution** ([#8582](https://github.com/QwenLM/qwen-code/issues/8582)) — AST-based classifier and runtime substitution gate both miss line-continuation and `${var@P}` tricks. Critical security gap in the read-only shell feature.

2. **[P1 CI] /review reverse-audit hangs silently until timeout** ([#8597](https://github.com/QwenLM/qwen-code/issues/8597)) — 12 timeouts on Aug 4, 9 more on Aug 5, most burning the full 360-min budget. Dominant failure mode (4 of 5) in fan-out launch. Community is actively discussing mitigations.

3. **[P2 Security] Provider warning sanitizer truncates messages and leaks passwords** ([#8136](https://github.com/QwenLM/qwen-code/issues/8136)) — URL sanitizer mishandles ports and `@` in credentials; passwords may leak to `/status` payload.

4. **[P2 Core] Tool-output budgeting and artifact lifecycle hardening** ([#7306](https://github.com/QwenLM/qwen-code/issues/7306)) — Phase 1 complete; Phase 2 tracking textual display-transport bounds (65,536-byte limit) across ACP and headless output.

5. **[P2 Desktop] Copy-response button broken on Windows** ([#8538](https://github.com/QwenLM/qwen-code/issues/8538)) — Desktop 0.0.5 on Windows 10: clipboard unchanged. Reproduced after restart, reboot, and power cycle.

6. **[P2 Platform] Tauri desktop app as Web Shell wrapper** ([#8092](https://github.com/QwenLM/qwen-code/issues/8092)) — lower-maintenance desktop experience reusing Web Shell; community discussion on deprecating Electron app ([#8596](https://github.com/QwenLM/qwen-code/issues/8596)).

7. **[P2 CLI] `qwen mcp list` hangs indefinitely on SSE servers** ([#8550](https://github.com/QwenLM/qwen-code/issues/8550)) — hangs when SSE server never emits `endpoint`; marked ready-for-agent.

8. **[P2 Web Shell] Session deep-link refresh returns 401 with bearer token** ([#8560](https://github.com/QwenLM/qwen-code/issues/8560)) — Auth bug on refresh of `/session/<id>`; in review.

9. **[P2 TUI] Continuous flicker in tmux < 3.5** ([#8580](https://github.com/QwenLM/qwen-code/issues/8580)) — Ink renderer clears+repaints every overflowing frame, guarded only by unqueried DEC 2026.

10. **[P3 Docs] Korean language support requested** ([#8551](https://github.com/QwenLM/qwen-code/issues/8551)) — Add 한국어 to README language bar alongside existing 7 languages.

Also notable: [VSCode nested file link resolution bug](https://github.com/QwenLM/qwen-code/issues/8606) (P2), [tmux flicker on Ubuntu](https://github.com/QwenLM/qwen-code/issues/8562) (P2), and [desktop language switch bug](https://github.com/QwenLM/qwen-code/issues/8592) (P2).

---

## 4. Key PR Progress

1. **[Live Voice for WebShell](https://github.com/QwenLM/qwen-code/pull/7859)** (merged) — Experimental native Live Voice with Codex-parity architecture; macOS-only, disabled by default.

2. **[Render inline terminal images](https://github.com/QwenLM/qwen-code/pull/8305)** (open) — Extends terminal-image infra to model/tool `inlineData`; preserves ordered text/image parts on `ServerGeminiContentEvent`.

3. **[Ctrl+click hyperlinks in VP mode](https://github.com/QwenLM/qwen-code/pull/8439)** (open) — Restores native hyperlink clicking and right-click context menu lost to SGR mouse tracking.

4. **[Stop reverse-audit loop while time remains](https://github.com/QwenLM/qwen-code/pull/8468)** (merged) — Fixes CI timeouts by bounding the 5-round cap; derived from CI run #30786453681 on PR #8368.

5. **[Run read-only info commands mid-turn](https://github.com/QwenLM/qwen-code/pull/8496)** (merged) — `/stats`, `/about`, `/context` now execute immediately during streaming in Web Shell.

6. **[Expose channel sessions in sidebar](https://github.com/QwenLM/qwen-code/pull/8457)** (open) — Tasks/Channels source switch for DingTalk, Feishu, WeCom sessions.

7. **[Ship core dist in review CLI bundle](https://github.com/QwenLM/qwen-code/pull/8612)** (open) — Fixes missing core build output in CI review bundles; contract tests pin new archive shape.

8. **[DingTalk continuous status cards](https://github.com/QwenLM/qwen-code/pull/8565)** (open) — One continuous interactive status card per task run; streams output across response boundaries.

9. **[Group pairing for channels](https://github.com/QwenLM/qwen-code/pull/8440)** (open) — Group chats approved once by stable chat ID, usable by all members.

10. **[Bound backward transcript pages](https://github.com/QwenLM/qwen-code/pull/8553)** (open) — Caps page-expansion alignment at one additional window in long single-turn sessions.

Also: [autofix ECS pool routing](https://github.com/QwenLM/qwen-code/pull/8603), [startup warnings scoped to dev sessions](https://github.com/QwenLM/qwen-code/pull/8456), and [glob test deflake](https://github.com/QwenLM/qwen-code/pull/8604).

---

## 5. Feature Request Trends

**Desktop consolidation (highest signal)** — Multiple issues converge on replacing the Electron desktop app with the Tauri-based shell wrapping Web Shell ([#8092](https://github.com/QwenLM/qwen-code/issues/8092), [#8596](https://github.com/QwenLM/qwen-code/issues/8596)). QR-code pairing for phone access to local sessions is a complementary request ([#8595](https://github.com/QwenLM/qwen-code/issues/8595)).

**Session lifecycle & observability** — Active work tracking for background agents ([#8586](https://github.com/QwenLM/qwen-code/issues/8586)), OpenTelemetry session lifecycle alignment ([#8589](https://github.com/QwenLM/qwen-code/issues/8589)), and inbound hooks support in TypeScript SDK ([#8591](https://github.com/QwenLM/qwen-code/issues/8591)) all point to production-readiness focus.

**Async/cost optimization** — `/slow` batch mode request ([#8605](https://github.com/QwenLM/qwen-code/issues/8605)) for lower-cost asynchronous agent runs suggests user interest in reducing model spend.

**Localization** — Korean language support request ([#8551](https://github.com/QwenLM/qwen-code/issues/8551)); desktop language switch bug ([#8592](https://github.com/QwenLM/qwen-code/issues/8592)) shows l10n maturity gap.

---

## 6. Developer Pain Points

**Terminal rendering regressions** — tmux flicker ([#8580](https://github.com/QwenLM/qwen-code/issues/8580), [#8562](https://github.com/QwenLM/qwen-code/issues/8562)) and macOS scrollback duplication ([#8557](https://github.com/QwenLM/qwen-code/issues/8557)) indicate the TUI rendering layer needs hardening across terminal emulators.

**Desktop app maturity** — Multiple UI bugs (copy button [#8538](https://github.com/QwenLM/qwen-code/issues/8538), markdown links [#8593](https://github.com/QwenLM/qwen-code/issues/8593), language switch [#8592](https://github.com/QwenLM/qwen-code/issues/8592)) suggest the desktop shell shipped before core interactions were polished.

**CI reliability** — Hanging reverse-audit runs ([#8597](https://github.com/QwenLM/qwen-code/issues/8597)) and mocked disk-full errors polluting CI logs ([#8532](https://github.com/QwenLM/qwen-code/issues/8532)) frustrate contributors relying on CI signals.

**File edit reliability legacy** — Closed issue #2460 (severe "edit faild" in CLI/VSCode) resurfaced with 4 comments on Aug 5, still unresolved for some users; the VSCode file-link bug ([#8606](https://github.com/QwenLM/qwen-code/issues/8606)) compounds this.

**MCP connectivity** — Unbounded hangs on SSE servers ([#8550](https://github.com/QwenLM/qwen-code/issues/8550)) highlight missing timeouts in MCP tooling.

**Security hygiene** — Read-only shell bypasses ([#8582](https://github.com/QwenLM/qwen-code/issues/8582)) and credential leaks in sanitizer ([#8136](https://github.com/QwenLM/qwen-code/issues/8136)) signal the need for more rigorous security review of privileged paths.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-08-06

## 1. Today's Highlights

The v0.9.4 release train continues to mature, with the integration branch now 77 commits ahead of main. The most significant activity centers on expanding the Runtime API surface — six Copilot-authored PRs introduce bounded memory inspection, MCP server lifecycle management, goal-loop state controls, verifier receipts, and skill lifecycle endpoints. Developer experience fixes are also prominent: a Windows OpenHarmony linker quoting fix was merged, ratatui is pinned to resolve a blocking cursor position report race, and several UX improvements (real wait elapsed time, subagent checkpoint resumption, mouse capture fix) are in flight.

## 2. Releases

No new releases in the last 24 hours. The v0.9.4 release train is active via [PR #5135](https://github.com/Hmbown/CodeWhale/pull/5135), currently 77 commits ahead of main with release notes tracked in `FINISH-0.9.4.md`.

## 3. Hot Issues

1. **[#5250 — Only one API key can be saved, making multi-provider usage difficult](https://github.com/Hmbown/CodeWhale/issues/5250)**  
   User cannot maintain separate API keys for multiple providers, making model switching laborious. One commenter likely suggested a keyring approach. High practical impact for the multi-provider workflow DeepSeek TUI is known for.

2. **[#5244 — Unknown model IDs silently degrade to 128K legacy context default](https://github.com/Hmbown/CodeWhale/issues/5244)**  
   Maintainer-reported residual bug: unrecognized model IDs fall back to 128K context without surfacing a warning. Critical for 1M-window models that would silently compact. Root cause partially mitigated in 0.9.4 but needs a visible hint.

3. **[#5005 — Sandbox path whitelist for external logs and build artifacts](https://github.com/Hmbown/CodeWhale/issues/5005)**  
   Closed enhancement request: Xcode builds write to `~/Library/Developer/Xcode/DerivedData/` outside the workspace sandbox, blocking legitimate build/debug workflows. Represents a real limitation for iOS/macOS developers.

4. **[#4029 — Interface similar to Reasonix?](https://github.com/Hmbown/CodeWhale/issues/4029)**  
   Open question about modeling the interface after Reasonix, with 4 comments over a month. Community interest in alternative UI paradigms persists.

5. **[#4029 (continued) — Community UI direction discussion](https://github.com/Hmbown/CodeWhale/issues/4029)**  
   Long-running thread (since early July) suggests sustained curiosity about visual/UX evolution beyond the TUI.

6. **[#5250 (continued) — Multi-provider key management](https://github.com/Hmbown/CodeWhale/issues/5250)**  
   Tied to the DeepSeek ↔ GLM switching workflow; a simple keyring or per-provider credential store is the likely resolution.

7. **[#5244 (continued) — Context window visibility](https://github.com/Hmbown/CodeWhale/issues/5244)**  
   Maintainer-flagged; community likely to lobby for explicit model capability logging or user-visible warnings.

8. **[#5005 (continued) — Sandbox usability](https://github.com/Hmbown/CodeWhale/issues/5005)**  
   Closed but sets precedent; similar requests for other out-of-workspace paths may follow.

9. **[#5250 (referenced) — Provider key rotation friction](https://github.com/Hmbown/CodeWhale/issues/5250)**  
   The one-comment engagement suggests a narrow but real user segment; expect follow-up proposals.

10. **[#5244 (referenced) — Silent degradation risk](https://github.com/Hmbown/CodeWhale/issues/5244)**  
   The "say so out loud" framing indicates community expectation for transparency over magic numbers.

## 4. Key PR Progress

1. **[#5135 — v0.9.4 release train](https://github.com/Hmbown/CodeWhale/pull/5135)**  
   Maintainer-driven integration branch, 77 commits ahead of main, supersedes #5044. Contains all 2026-08-01 source candidates plus 18 train commits.

2. **[#5225 — ACP server: expose file/search/git/patch/shell tools](https://github.com/Hmbown/CodeWhale/pull/5225)**  
   Critical gap: ACP `session/prompt` only streamed text, never executed tool calls. This PR enables real code-editing via Zed or `acp-deepseek-adapter` bridges.

3. **[#5242 — Resume interrupted subagent children from checkpoint](https://github.com/Hmbown/CodeWhale/pull/5242)**  
   Fixes dead-letter behavior for interrupted continuable children — long tasks can now be resumed instead of re-dispatched.

4. **[#5240 — Surface real wait elapsed time in tool content](https://github.com/Hmbown/CodeWhale/pull/5240)**  
   The model previously saw identical `wait` results regardless of actual duration — biasing it toward busy-polling. Now exposes wall-clock time to the model.

5. **[#5234 — Keep alternate scroll off while mouse capture is active](https://github.com/Hmbown/CodeWhale/pull/5234)**  
   Fixes mouse-wheel interaction where scrolling toggled composer input history instead of moving the transcript.

6. **[#5192 — Pin ratatui to 0.30.0](https://github.com/Hmbown/CodeWhale/pull/5192)**  
   Closed fix: ratatui-core 0.1.1+ introduces a blocking CPR query racing the event loop. Pinning eliminates this race.

7. **[#5095 — Re-quote Windows linker arguments with spaces](https://github.com/Hmbown/CodeWhale/pull/5095)**  
   Closed fix for OpenHarmony SDK under spaced paths (`D:\DevEco Studio\...`) — `%*` expansion was stripping critical quoting.

8. **[#5131 — Runtime API memory endpoints](https://github.com/Hmbown/CodeWhale/pull/5131)**  
   Bounded inspection and lifecycle controls for active memory via `/v1/memory`, gated behind `require_runtime_token`.

9. **[#5130 — Runtime API MCP server lifecycle](https://github.com/Hmbown/CodeWhale/pull/5130)**  
   Adds create/update/delete for MCP servers over HTTP, removing the need for direct TOML/JSON editing.

10. **[#5133 — Runtime API goal-loop state and controls](https://github.com/Hmbown/CodeWhale/pull/5133)**  
    Read active-goal state and drive lifecycle transitions via `/v1/threads/{id}/goal` — closes the managed-client gap.

11. **[#5132 — Verifier receipts and evidence endpoints](https://github.com/Hmbown/CodeWhale/pull/5132)**  
    Fleet verifier failures were opaque (single counter). Now exposes per-task receipts and retry intent.

12. **[#5129 — Skill lifecycle endpoints](https://github.com/Hmbown/CodeWhale/pull/5129)**  
     Adds install/update/uninstall/trust/audit routes for skills, mirroring TUI capabilities over HTTP.

13. **[#5236 — Model Studio proof artifacts](https://github.com/Hmbown/CodeWhale/pull/5236)**  
     Community contributor attaches live MP4 + Token Plan screenshots as evidence for qwen3.8-max reasoning behavior.

## 5. Feature Request Trends

- **Runtime API expansion** — Six PRs from Copilot extend the HTTP surface into memory, MCP, goals, verifier receipts, and skills. The dominant theme: making automated/managed clients first-class citizens.
- **Developer-experience transparency** — UX improvements focus on making hidden state visible: wait durations, context window fallbacks, real interruption states.
- **Filesystem flexibility** — Path-whitelist requests reflect real-world build flows that touch out-of-workspace locations.
- **Multi-provider support** — API key management for multiple providers is a small but persistent ask.

## 6. Developer Pain Points

- **Silent configuration fallbacks** — The 128K context default bug shows users are burned by invisible defaults; explicit signaling is demanded.
- **Tool-call invisibility in ACP** — Editors bridged over ACP got chat-only behavior — no code editing — until #5225; a significant integration gap.
- **Sandbox friction** — Xcode/watchOS developers hit hard walls with out-of-workspace artifacts; workspace-write mode is too narrow for common tooling.
- **Headless management gaps** — Managed/desktop/web clients lacked memory, goal, and skill lifecycle routes; workarounds required editing TOML directly.
- **Input-mode regressions** — Mouse-capture/scroll conflicts and ratatui races disrupted interactive use; both now fixed or in flight.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/kky-wollu/agents-radar).*
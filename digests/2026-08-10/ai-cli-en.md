# AI CLI Tools Community Digest 2026-08-10

> Generated: 2026-08-09 22:35 UTC | Tools covered: 9

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
**Date:** 2026-08-10

---

## 1. Ecosystem Overview

The AI CLI tool ecosystem is in a **rapid consolidation phase**, characterized by three dominant trends: **reliability hardening** (fixing silent failures, hangs, and data loss), **MCP integration maturity** (protocol edge cases, security, and lifecycle management), and **feature parity chasing** (with Claude Code serving as the de-facto reference implementation). The landscape spans eight major tools — Claude Code, OpenAI Codex, Gemini CLI, GitHub Copilot CLI, Kimi Code, OpenCode, Pi, Qwen Code, and DeepSeek TUI (CodeWhale) — each targeting distinct developer segments. While all tools share core agentic capabilities (subagents, MCP, session management), their communities reveal **different pain point profiles**: Claude Code grapples with safety-classifier false positives, Codex with desktop storage leaks, Gemini CLI with subagent reliability, and Copilot CLI with MCP fragility. The ecosystem is converging on **workflow determinism** — replacing model-driven improvisation with explicit, auditable workflow engines — while simultaneously expanding into **multi-surface coordination** (desktop, mobile, web, remote).

---

## 2. Activity Comparison

| Tool | Issues New/Active (24h) | PRs Active (24h) | Releases (24h) | Overall Activity Level |
|------|------------------------|------------------|----------------|------------------------|
| **Claude Code** | 10 hot issues; ~20 issue cluster closed as stale | 3 PRs (light day) | None | Moderate; triage-focused |
| **OpenAI Codex** | 10 hot issues; desktop/Windows dominant | 6 closed PRs | None | High; infrastructure hardening |
| **Gemini CLI** | 10 hot issues; subagent reliability dominant | 10 PRs (7 open, 3 closed) | 1 nightly (v0.56.0) | **Very High**; rapid iteration |
| **GitHub Copilot CLI** | **13 new issues** (triage spike) | 0 PRs | None | High; triage/prioritization cycle |
| **Kimi Code** | 2 active issues | 1 PR (stale, since Jan) | None | **Low**; review bandwidth stretched |
| **OpenCode** | 10 hot issues; Go subscription pain | 8 closed PRs + 2 open | None | High; cleanup/merge cycle |
| **Pi** | 10 hot issues; 20+ closed as untriaged | 10 PRs (9 closed, 1 open) | None | High; triage + fix cycle |
| **Qwen Code** | 10 hot issues; workflow/RFC focus | 10 PRs (all in review or merged) | Nightly failed CI | **Very High**; architectural consolidation |
| **DeepSeek TUI** | 10 hot issues; compaction/IME focus | 10 PRs (all merged) | v0.9.6 preparing | **Very High**; release-preparation mode |

**Key observations:**
- **Gemini CLI, Qwen Code, and DeepSeek TUI** are the most actively iterating, with significant PR throughput.
- **Kimi Code** shows the lowest activity — a single stale PR from January signals potential maintenance concerns.
- **Copilot CLI** has a high new-issue velocity (13 in 24h) but zero PR activity, indicating a triage bottleneck.
- **OpenCode and Pi** are in cleanup/merge cycles, closing long-standing issues and PRs.

---

## 3. Shared Feature Directions

Across all tool communities, the following requirements appear repeatedly:

### 3.1 Memory & Persistent Context
- **Kimi Code** (#1283), **DeepSeek TUI** (#5131), **Gemini CLI** (#26522, #26525): Cross-session memory systems with automatic + manual notes; deterministic redaction for privacy; bounded memory lifecycle.
- **Claude Code** (#69033): Memory-aware throttling for subagent fan-out.

### 3.2 MCP Reliability & Security
- **Copilot CLI** (#4421, #4419): Configurable timeouts, retries, and no interim deny-all policies.
- **Gemini CLI** (#28549): Disclose that MCP server read-only claims are unverified.
- **Qwen Code** (#8784): Graceful handling of optional spec paths (GET/SSE 404).
- **Claude Code** (#42138): Inbound MCP notifications injected into conversation.
- **OpenCode** (#33027): MCP tools connected but not exposed to agent.

### 3.3 Workflow Determinism & Orchestration
- **Qwen Code** (#8775, #8769): Unify session reasoning loops; rebuild review orchestration on workflow engine.
- **DeepSeek TUI** (#5133, #5132): Persistent goal-loop state, verifier receipts, and explicit runtime control.
- **Gemini CLI** (#28738): Agents calling agents recursively — deep orchestration.

### 3.4 Claude Code Feature Parity
- **OpenCode** (#12472): Native Claude Code hooks compatibility (PreToolUse, PostToolUse, Stop).
- **Codex** (#17827): Customizable status line (Claude Code's configurable status bar).
- **Pi** (#7845): Port stream rules, subagent tools, and cross-session memory.
- Universal demand for `AGENTS.md`/`CLAUDE.md` standard.

### 3.5 Tool-Call Parser Reliability
- **Claude Code** (#84362): Silent parameter loss in tag-grammar parser (6.2% rate).
- **DeepSeek TUI** (#5209): File edit tool accepts wrong params, returns false success — silent failures.

### 3.6 Storage/Disk Hygiene
- **Codex** (#25921, #35823): Crashpad dump bloat; SQLite vacuum gaps.
- **Codex** (#34337): Shared rollout storage growing to TiB scale.

---

## 4. Differentiation Analysis

| Tool | Target User | Key Strengths | Distinct Technical Approach |
|------|-------------|---------------|----------------------------|
| **Claude Code** | Professional developers; enterprise | Agent Teams, hooks, mature plugin ecosystem | Safety classifiers (ClAudit) with intent-pattern matching (overreach concern) |
| **OpenAI Codex** | Desktop/TUI users; power users | Cross-platform desktop app, mobile remote control | Electron shell + Rust CLI; crashpad/dump telemetry |
| **Gemini CLI** | Google ecosystem users; automation | Subagent orchestration (agents calling agents), ACP, nightly releases | Fast iteration speed; risk of regressions; policy-engine bug (YOLO/AUTO_EDIT) |
| **Copilot CLI** | GitHub Enterprise users | Deep GitHub integration (worktrees, org repos, Copilot models) | Tight Copilot model coupling; MCP gateway (OAuth 3LO) |
| **Kimi Code** | Moonshot AI users; MCP bridging | Lightweight; minimal feature set | Low maintenance velocity; single stale PR (review bottleneck) |
| **OpenCode** | Open-source enthusiasts; Go subscription | Worktree-based workspaces, Bun runtime, app redesign | Startup-like velocity; infrastructure reliability gaps (Go relay) |
| **Pi** | Terminal purists; multi-provider | llama.cpp local models, extension system, wire protocol (remote sessions) | Cross-platform TUI with alt-screen; TUI renderer fragility |
| **Qwen Code** | Alibaba ecosystem; multi-transport | Web Shell, Chrome extension, channel sessions (DingTalk/Feishu/WeCom), workflow engine | Deterministic workflow engine replacing model-driven logic; OTel interop |
| **DeepSeek TUI** | DeepSeek model users; local inference | Fleet/subagent model, runtime API (HTTP control), compaction pressure-awareness | Aggressive local-first; compaction as subtractive release; IME support |

**Cross-cutting differentiation:**
- **Claude Code** is the **feature reference** — other tools explicitly chase its parity (hooks, status bar, agents).
- **Qwen Code** and **DeepSeek TUI** are the most **architecturally ambitious**, moving toward deterministic workflow engines and runtime APIs.
- **Copilot CLI** is the most **enterprise-coupling** focused, with deep GitHub integration but fragile MCP.
- **Kimi Code** is the least differentiated but also the simplest; maintenance risk is its primary concern.

---

## 5. Community Momentum & Maturity

### High Momentum (Rapid Iteration)
- **Qwen Code** — Very high PR velocity; architectural RFCs; CI failures being actively addressed; nightly builds (often failing).
- **Gemini CLI** — Consistent PR throughput with 10 active PRs; nightly releases; subagent-orchestration unlock (agents-to-agents).
- **DeepSeek TUI** — All 10 PRs merged in the window; v0.9.6 release preparation; strong focus on compaction and runtime APIs.

### Moderate Momentum (Steady Triage + Fix)
- **OpenCode** — 8 closed PRs; worktree features and NAPI crash fixes are mature; but Go subscription issues persist, and clipboard has been broken for 9 months.
- **Pi** — 9 closed PRs; TUI and provider fixes; llama.cpp catalog fix was most anticipated; EPIPE fix exists but was never merged (community frustration).
- **Claude Code** — Light PR day; issues closed as stale (including the largest cluster); ClAudit false positives remain unresolved systemically.
- **Codex** — 6 closed PRs for infrastructure hardening; desktop storage and Windows parity gaps persist.

### Low/Stalled Momentum
- **Copilot CLI** — Zero PRs despite 13 new issues; triage bottleneck; MCP failures unresolved.
- **Kimi Code** — Single stale PR from January; review bandwidth stretched; critical ACP hang unfixed.

### Community Size (by engagement proxy: top-issue upvotes/comments)
| Tool | Top Issue Engagement | Signal |
|------|----------------------|--------|
| Codex | 945 👍 (Linux desktop) | Very large, vocal user base |
| OpenCode | 110 👍 / 122 comments (clipboard) | Large, frustrated base |
| Claude Code | 7 👍 (most-discussed) | Mature but engagement fragmented across many issues |
| Gemini CLI | 8 👍 (hanging agent) | Moderate size, focused on reliability |

---

## 6. Trend Signals

### 6.1 The "Identity Crisis" of MCP
MCP is the de-facto standard, but **every tool has MCP failures**: timeouts (Copilot), security claims (Gemini), tool exposure (OpenCode), inbound events (Claude Code), spec optional paths (Qwen). Expect MCP hardening to be a top platform investment across all tools.

### 6.2 Workflow Engines Replace Model-Driven Logic
Qwen Code's workflow engine, DeepSeek TUI's runtime APIs, and Gemini's agents-to-agents signals a shift: **explicit orchestration over improvisation**. Deterministic, auditable workflow code reduces silent failures and improves debuggability.

### 6.3 "Silent Failure" is the #1 Trust Killer
The most damaging bugs across tools share a pattern: **success reported, work not done** (Claude Code parameter loss, DeepSeek edit false positives, Gemini GOAL-on-max-turns, OpenCode clipboard "success"). Communities unanimously demand **fail-loud, fail-fast** behavior.

### 6.4 Storage Hygiene is a Systemic Blind Spot
Codex, Gemini CLI, and DeepSeek TUI all show storage bloat issues (logs, crashdumps, SQLite). As agents run longer and sessions persist, **bounded storage budgets and explicit vacuum/compaction policies** become table stakes.

### 6.5 Windows Remains Second-Class
Codex (Computer Use), Qwen Code (mojibake, installer), DeepSeek TUI (IME), and Copilot CLI (Worktrees) consistently report Windows-specific gaps. Cross-platform parity is a competitive differentiator and a recurring pain point.

### 6.6 Security Classifiers: Overreach vs. Bypass
Two opposing failures: Claude Code's **false positives** on sysadmin work (overreach), and Qwen Code's **read-only shell bypasses** (underreach). The ecosystem needs **domain-aware, context-sensitive safety classification** that understands intent.

### 6.7 Community Priorities for Developers
- **Memory systems** (persistent context) are the most-requested feature across Kimi, DeepSeek, Pi, and Gemini — the "blank slate" model is no longer acceptable.
- **Claude Code parity** is the reference benchmark — hooks, status line, agent teams, and plugin ecosystems set the bar.
- **Config transparency** ("which file wins?") and **state durability** (interrupted output preserved) are rising concerns.

---

## Conclusion for Decision-Makers

If you're selecting a tool, consider:
- **For enterprise GitHub workflows**: Copilot CLI (but track MCP fragility).
- **For the most battle-tested ecosystem**: Claude Code (but budget for safety-classifier friction).
- **For rapid iteration and orchestration**: Gemini CLI or Qwen Code (but expect CI/nightly churn).
- **For local-first, runtime API control**: DeepSeek TUI (CodeWhale) — the fastest-moving release cycle.
- **For terminal purists**: Pi — strong TUI and multi-provider support, but watch for renderer and crash fragility.

To monitor: Kimi Code's maintenance health, Codex storage management, Claude Code's ClAudit root-cause resolution, and the convergence of workflow-engine approaches across Qwen, DeepSeek, and Gemini.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data as of 2026-08-10 | Source: github.com/anthropics/skills**

---

## 1. Top Skills Ranking

The following Skills have attracted the most community attention through PR discussion and issue cross-referencing. All are currently **open**.

### 1. fix(skill-creator): run_eval.py always reports 0% recall
**PR [#1298](https://github.com/anthropics/skills/pull/1298)** | Author: MartinCajiao | Created: 2026-06-10

**Functionality:** Fixes the skill-creator's evaluation infrastructure — `run_eval.py`, `run_loop.py`, and `improve_description.py` all consume a signal that reports `recall=0%` for every description, making the entire description-optimization loop optimize against noise. The fix installs the eval artifact as a real skill, and addresses Windows stream reading, trigger detection, and parallel worker issues.

**Discussion highlights:** This is the most significant single PR in the repository — it directly addresses Issue [#556](https://github.com/anthropics/skills/issues/556) (12 comments, 7 👍), which documents 10+ independent reproductions of the 0% recall bug. Multiple parallel PRs (#1099, #1050, #1323, #1261) address the same root cause from different angles, making this the most crowded problem space in the repo.

**Status:** Open. The breadth of related fixes suggests a maintainer-driven consolidation may be needed.

---

### 2. Add document-typography skill
**[PR #514](https://github.com/anthropics/skills/pull/514)** | Author: PGTBoos | Created: 2026-03-04

**Functionality:** A typographic quality-control skill for generated documents. Prevents orphan word wrap (1–6 words spilling onto the next line), widow paragraphs (section headers stranded at page bottom), and numbering misalignment — issues the author notes affect every document Claude generates.

**Discussion highlights:** The PR taps into a widely felt pain point: document polish. The author's framing — "Users rarely ask for good typography, but they notice when it's bad" — resonated with the community. This is a niche but high-frequency use case for Claude Code users producing client-facing documents.

**Status:** Open since March 2026.

---

### 3. fix(pdf): correct case-sensitive file references in SKILL.md
**[PR #538](https://github.com/anthropics/skills/pull/538)** | Author: Lubrsy706 | Created: 2026-03-06

**Functionality:** Fixes 8 case-sensitivity mismatches in `skills/pdf/SKILL.md` where `REFERENCE.md` and `FORMS.md` are referenced in uppercase but the actual files are lowercase. This breaks on case-sensitive filesystems.

**Discussion highlights:** Small but critical correctness fix. The same author contributed related fixes for DOCX `w:id` collisions (PR [#541](https://github.com/anthropics/skills/pull/541)) and YAML unquoted description validation (PR [#539](https://github.com/anthropics/skills/pull/539)), making them a notable contributor to skill robustness.

**Status:** Open. Simple fix, likely mergeable with minimal review.

---

### 4. Add ODT skill — OpenDocument text creation and template filling
**[PR #486](https://github.com/anthropics/skills/pull/486)** | Author: GitHubNewbie0 | Created: 2026-03-01

**Functionality:** Comprehensive OpenDocument Format support — create, fill, read, or convert `.odt` and `.ods` files. Triggers on mentions of 'ODT', 'ODS', 'ODF', 'OpenDocument', or 'LibreOffice document', and supports ISO-standard formats.

**Discussion highlights:** Fills a clear gap: the official repo has DOCX and PDF skills but no OpenDocument equivalent. Given LibreOffice's strong presence in government and EU institutional contexts, this addresses a compliance-driven demand.

**Status:** Open since March 2026.

---

### 5. Improve frontend-design skill clarity and actionability
**[PR #210](https://github.com/anthropics/skills/pull/210)** | Author: justinwetch | Created: 2026-01-05

**Functionality:** Revises the existing frontend-design skill to improve clarity, actionability, and internal coherence. The goal: every instruction must be something Claude can follow within a single conversation, and guidance must be specific enough to steer behavior without being overly prescriptive.

**Discussion highlights:** This is a quality-over-quantity improvement PR, not a new skill. The community has shown sustained interest in refining existing skills rather than only adding new ones — a signal of ecosystem maturation.

**Status:** Open since January 2026.

---

### 6. Add self-audit — mechanical verification + four-dimension reasoning quality gate (v1.3.0)
**[PR #1367](https://github.com/anthropics/skills/pull/1367)** | Author: YuhaoLin2005 | Created: 2026-06-28

**Functionality:** A meta-skill that audits AI output before delivery. Step 0 performs mechanical verification (every claimed output file must exist); then a four-dimension reasoning audit runs in damage-severity priority order. Universal — works with any project, tech stack, or model.

**Discussion highlights:** The author also filed a related proposal (Issue [#1385](https://github.com/anthropics/skills/issues/1385), 4 comments) for a three-gate "Reasoning Quality Gate Pipeline" (pre-task calibration → adversarial review → delivery verification). This signals demand for quality assurance at the **meta level** — skills that check the output of other skills. Notably, this follows a similar self-audit skill proposed in Issue [#412](https://github.com/anthropics/skills/issues/412) (agent-governance).

**Status:** Open since late June 2026.

---

### 7. Add color-expert skill
**[PR #1302](https://github.com/anthropics/skills/pull/1302)** | Author: meodai | Created: 2026-06-10

**Functionality:** A self-contained color-expertise skill covering color naming systems (ISCC-NBS, Munsell, XKCD, RAL, Ridgway 1912, CSS named) and color spaces with a "what to use when" table (OKLCH for scales, OKLAB for gradients, CAM16 for perceptual accuracy).

**Discussion highlights:** Author meodai is the creator of the [Color Names](https://colornames.org) project — deep domain expertise. The skill addresses a consistent pain point in AI-generated UI work: Claude's tendency to pick aesthetically mediocre color palettes.

**Status:** Open since June 2026, updated as recently as July 21.

---

## 2. Community Demand Trends

From the top issues, four clear demand directions emerge:

### Security and trust boundaries (highest urgency)
Issue [#492](https://github.com/anthropics/skills/issues/492) (43 comments, 2 👍) documents a **trust boundary vulnerability**: community-made skills are distributed under the `anthropic/` namespace, impersonating official skills and risking elevated permissions for unofficial code. This is the single most-commented issue in the repository and reflects growing enterprise adoption concerns — users want assurance about what they're installing.

### Skill sharing and organizational distribution
Issue [#228](https://github.com/anthropics/skills/issues/228) (16 comments, 8 👍 — highest 👍 count) calls for org-wide skill sharing in Claude.ai. The current workflow (download .skill file → send via Slack/Teams → manual upload) is too friction-heavy for team adoption. This indicates skills are moving from individual tooling to **team infrastructure**.

### Evaluation infrastructure reliability
The cluster of issues around `run_eval.py` — [#556](https://github.com/anthropics/skills/issues/556) (12 comments, 7 👍), [#1169](https://github.com/anthropics/skills/issues/1169) — shows that **skill authors cannot trust their own tooling**. When the optimization loop reports `recall=0%` on every iteration, the feedback signal is noise. The community wants the skill-creator toolchain to be reliable before they invest in optimizing skill descriptions.

### Context window efficiency
Issue [#1487](https://github.com/anthropics/skills/issues/1487) is a sharp, recent signal: the `claude-api` skill injects ~156k tokens in a single tool call, exhausting the entire context window. Issue [#189](https://github.com/anthropics/skills/issues/189) (6 comments, 9 👍) documents duplicate skills from overlapping plugins. The community is increasingly **context-window-aware** — skills that consume more than they produce are seen as liabilities.

---

## 3. High-Potential Pending Skills

These PRs have active discussion, clear scope, and the highest likelihood of landing in the near term:

| Skill | PR | Why it may land soon |
|---|---|---|
| **Fixes for run_eval.py** (4 parallel PRs) | [#1298](https://github.com/anthropics/skills/pull/1298), [#1099](https://github.com/anthropics/skills/pull/1099), [#1050](https://github.com/anthropics/skills/pull/1050), [#1323](https://github.com/anthropics/skills/pull/1323) | The eval toolchain is fundamentally broken; maintainers cannot ignore 10+ independent reproductions. Expect consolidation of these into an official fix. |
| **plan-file-hygiene** | [#1479](https://github.com/anthropics/skills/pull/1479) | Addresses Issue [#1417](https://github.com/anthropics/skills/issues/1417) (planning artifacts accumulate with no lifecycle). Well-framed, credits prior community discussion — signals collaborative maturity. |
| **color-expert** | [#1302](https://github.com/anthropics/skills/pull/1302) | Author is a recognized domain expert (meodai of colornames.org). High-quality, self-contained, no dependencies. Updated as recently as July 21. |
| **self-audit** | [#1367](https://github.com/anthropics/skills/pull/1367) | Coupled with proposal Issue [#1385](https://github.com/anthropics/skills/issues/1385). Meta-skills (quality gates for AI output) are an emerging category with clear demand signal. |
| **testing-patterns** | [#723](https://github.com/anthropics/skills/pull/723) | Comprehensive testing skill (Testing Trophy model, React Testing Library, naming conventions). Broad applicability, low controversy. |
| **pyxel (retro game dev)** | [#525](https://github.com/anthropics/skills/pull/525) | Author kitāo is the Pyxel engine creator — high-quality, ecosystem-aligned. Niche but authoritative. |
| **skill-quality-analyzer / skill-security-analyzer** | [#83](https://github.com/anthropics/skills/pull/83) | Pre-dates the security issue [#492](https://github.com/anthropics/skills/issues/492) by 4 months — the community was asking for meta-analysis tools before the vulnerability was formally documented. |

---

## 4. Skills Ecosystem Insight

The community's most concentrated demand at the Skills level is **trustworthy infrastructure**: reliable skill-authoring tooling (functioning eval loops, case-correct files), verified provenance (no namespace impersonation), and context-window-aware skill design — quality assurance **for and of** skills, rather than just new functional capabilities.

---

# Claude Code Community Digest — 2026-08-10

## 1. Today's Highlights

The community continues to raise concerns about ClAudit's safety classifiers producing false positives on routine cloud-IAM administration, though most of these issues (filed in late June) have since been closed as duplicates or stale. Two fresh PRs target developer-experience fixes: a YAML block-scalar parsing fix for plugin agent descriptions (#85323) and a spec-conformance pass on bundled skill names (#85243). A newly surfaced open issue (#84362) reports a 6.2% silent parameter-loss rate in the tag-grammar tool-call parser on malformed close tags, which remains an active concern.

## 2. Releases

No new releases in the last 24 hours.

## 3. Hot Issues

1. **[#84362 — Tag-grammar tool-call parser silently absorbs parameter blocks (OPEN)**](https://github.com/anthropics/claude-code/issues/84362)  
   Reports a 6.2% silent field-loss rate on parameter-rich MCP calls when the model emits mismatched close tags. The call succeeds with missing parameters — dangerous for automation. Re-opened after the original (#44826) was stale-closed. 4 comments, 0 👍.

2. **[#61185 — Cyber safeguards false positive: routine sysadmin audit commands blocked (CLOSED, stale)**](https://github.com/anthropics/claude-code/issues/61185)  
   A broad report covering false-positive blocks on routine sysadmin work, write-only reporting blocked in new sessions, and context poisoning breaking session recovery. 17 comments — the most-discussed issue today — but ultimately closed as stale. 7 👍.

3. **[#66095 — Server withholds stream bytes after accepting request (CLOSED, stale)**](https://github.com/anthropics/claude-code/issues/66095)  
   On CLI 2.1.157 / Opus 4.8, the server frequently issues a request-id then sends no bytes for tens-to-hundreds of seconds, triggering 180s idle-timeout aborts. 6 comments, 2 👍.

4. **[#65095 — Plan mode silently exits and agent treats the resulting ExitPlanMode (OPEN)**](https://github.com/anthropics/claude-code/issues/85095)  
   Fresh bug: Plan mode quietly exits and the agent mishandles the resulting `ExitPlanMode`. Small but new, filed 2026-08-08. 4 comments.

5. **[#64550 — Agent Teams: lead's "active agent" pointer sticks on a teammate (CLOSED, stale)**](https://github.com/anthropics/claude-code/issues/64550)  
   After long/compacted sessions, the team lead routes *as* a teammate, and spawning new agents fails with "Teammates cannot spawn other teammates." Windows-specific. 5 comments.

6. **[#69952 — `--resume` fails with "No conversation found" after account permission reset (CLOSED, stale)**](https://github.com/anthropics/claude-code/issues/69952)  
   macOS: local session files are intact but resume breaks after a permission reset — suggesting a session-metadata/auth mismatch. 3 comments.

7. **[#69033 — Workflow harness: memory-aware throttling when fanning out subagents (CLOSED, stale)**](https://github.com/anthropics/claude-code/issues/69033)  
   A deep-research fan-out (84–92 subagents) OOM-killed the host. Concurrency cap is count-based (`min(16, cores-2)`), not memory-aware. 3 comments, 1 👍.

8. **[#42138 — Telegram plugin: inbound MCP notifications not injected into conversation (CLOSED, stale)**](https://github.com/anthropics/claude-code/issues/42138)  
   MCP `notifications/claude/channel` messages don't flow into the conversation — breaking Telegram-based remote control. 8 comments, 1 👍.

9. **[#70773 — ClAudit auto-mode classifier denial: long-running watcher false-positive (CLOSED, stale)**](https://github.com/anthropics/claude-code/issues/70773)  
   The auto-mode classifier denied a legitimate long-running watcher process. Part of the large sworrl batch of late-June false positives. 5 comments.

10. **[#70824 — Safety block stopped read-only IR mailbox triage and credential lockdown via Graph API (CLOSED, stale)**](https://github.com/anthropics/claude-code/issues/70824)  
    Another ClAudit false-positive: read-only incident-response work on the operator's own tenant was blocked. Illustrates the security-classifier overreach pattern. 3 comments.

> **Note:** The sworrl batch (#70745–#70824, filed 2026-06-25) is a cluster of ~20 near-identical false-positive reports (AUP/cyber classifiers on cloud-IAM tasks). All are now closed as duplicates/stale. Community reaction leans toward "classifier too aggressive on legitimate administrative work."

## 4. Key PR Progress

1. **[#85323 — fix(plugin-dev): parse block scalar agent descriptions (OPEN)**](https://github.com/anthropics/claude-code/pull/85323)  
   Fixes remaining YAML block-scalar parsing defect from #83803. `validate-agent.sh` now measures multiline `description: |` / `description: >` values from indented content instead of treating the scalar marker as the whole description. *(Note: 0 comments — under review.)*

2. **[#85243 — fix(skills): use spec-conformant names in plugin-dev and hookify skills (OPEN)**](https://github.com/anthropics/claude-code/pull/85243)  
   Eight bundled skills declare title-cased `name:`s containing spaces (e.g., `Writing Hookify Rules`, `Agent Development`) — violating the skills spec. Converts them to spec-conformant slugs.

3. **[#17395 — Add `agent-session-commit` plugin to incrementally iterate on AGENTS.md (CLOSED)**](https://github.com/anthropics/claude-code/pull/17395)  
   Adds `AGENTS.md` as the authoritative instruction file (with `CLAUDE.md` as a pointer), plus a plugin with `/session-commit` command and a Stop-hook prompt at session end. Merged or closed after 7 months of iteration.

*Only 3 PRs updated in the last 24h — this is a light PR day for the repo.*

## 5. Feature Request Trends

Distilled from the current issue set:

1. **Memory-aware concurrency for subagent fan-out** (#69033) — Count-based concurrency caps (`min(16, cores-2)`) are insufficient; demand for memory-aware throttling in workflow harnesses.
2. **Safety-classifier precision improvements** — Large demand (the sworrl cluster) for reducing false positives on legitimate cloud-IAM, sysadmin, and defensive-security work; requests for domain-aware exemptions.
3. **Session/context robustness** — Ability to resume after permission resets (#69952) and protection against context poisoning breaking session recovery (#61185).
4. **Plugin/skill ecosystem hardening** — Spec compliance for skill names (#85243), proper YAML block-scalar parsing (#85323), and reliable MCP inbound events (#42138).
5. **Tool-call parser reliability** — Silent parameter loss on malformed tags (#84362) points to demand for stricter validation or error surfacing rather than silent fallback.

## 6. Developer Pain Points

- **ClAudit / safety-filter false positives dominate the backlog.** The single largest cluster (20+ issues from one user) shows the cyber/AUP classifiers pattern-matching terminology rather than intent — blocking routine cloud IAM enumeration, read-only IR triage, and even placeholder keystrokes ("ASDF" fragments). Many closed as duplicates — indicating a known, yet unresolved, systemic issue.
- **Silent data loss in tool-call parsing.** The 6.2% parameter-loss rate (#84362) is alarming because failures are silent; the call "succeeds" with missing fields. This undermines trust for MCP-heavy workflows.
- **Network/stream reliability.** Slow first-byte and 180s idle-timeout aborts (#66095) on Opus 4.8 / 2.1.157 cause user-visible stalls for long-running turns.
- **Session lifecycle fragility.** `--resume` breaking after permission resets (#69952), and team-lead agent-pointer corruption after compaction (#64550), point to state-management bugs that force users to restart workflows.
- **Memory exhaustion in large fan-outs.** OOM crashes mid-run with dozens of subagents (#69033) — the count-based concurrency cap ignores per-agent memory footprints.
- **Plugin/MCP integration gaps.** Inbound MCP notifications not injected into conversations (#42138) breaks real-time remote-control workflows; bundled skill name non-compliance (#85243) suggests ecosystem tooling still maturing.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-08-10

## Today's Highlights
The Codex community remains highly engaged, with the Linux desktop app request (#11023) continuing its reign as the most popular open issue at 945 👍 and 205 comments. No new releases landed in the last 24 hours, but the team shipped six closed PRs focused on infrastructure hardening—hook execution, plugin-install analytics, and composer whitespace handling. Desktop stability concerns (crashpad storage bloat, flickering on Windows/macOS, and Windows Computer Use failures) dominate the bug tracker alongside persistent cross-platform parity gaps for Remote Control and MCP servers.

## Releases
No new releases in the last 24 hours.

## Hot Issues

1. **[#11023 — Codex desktop app for Linux](https://github.com/openai/codex/issues/11023)** — The most-voted issue in the tracker (945 👍, 205 comments). Users want a native Linux desktop app; macOS power-consumption issues make the current app unusable on laptops, pushing users to Linux desktops.

2. **[#17827 — Customizable status line](https://github.com/openai/codex/issues/17827)** — Claude Code's configurable status bar (token usage, model, rate limits, git branch) is a standout gap. 150 👍 shows real demand for TUI parity.

3. **[#25921 — Crashpad pending dumps grow +5GB/day](https://github.com/openai/codex/issues/25921)** — Severe storage leak on macOS: 54,504 files / 4.9GB in a single day. Users are concerned about SSD wear and silent disk exhaustion.

4. **[#37383 — Computer Use on Windows fails with 0x80070003](https://github.com/openai/codex/issues/37383)** — Fresh regression (Aug 7) breaking app/window discovery during Computer Use on Windows 11. Pro x5 subscribers are hitting this immediately.

5. **[#37281 — get_window_state fails: `node_repl exec context not found`](https://github.com/openai/codex/issues/37281)** — Related Windows Computer Use failure: discovery works, but state capture fails universally. Suggests a shared architectural issue in the Windows automation layer.

6. **[#27133 — Project hooks.json silently ignored in git worktrees](https://github.com/openai/codex/issues/27133)** — Dangerous silent failure: security-relevant approval hooks are skipped when running inside a worktree. This is a correctness/security issue, not just a convenience gap.

7. **[#34322 — Auto-compact resume loop](https://github.com/openai/codex/issues/34322)** — Agent repeatedly enters a resume loop after conversation optimization. Users report wasted tokens and stalled workflows in long sessions.

8. **[#23527 — SSH remote projects missing on mobile](https://github.com/openai/codex/issues/23527)** — Mac host can see SSH remotes, but they don't propagate to the mobile project selector. Breaks the "remote control from anywhere" workflow.

9. **[#35823 — logs_2.sqlite never reclaims freed pages](https://github.com/openai/codex/issues/35823)** — `auto_vacuum=INCREMENTAL` is set but never executed, so the DB grows monotonically despite 10-day retention. Subtle but impactful disk leak on Windows.

10. **[#37735 — TUI deadlocks when switching agent threads under pressure](https://github.com/openai/codex/issues/37735)** — Recently closed but notable: UI freezes during agent thread switches under high CPU/memory load, even with third-party model providers (AWS Bedrock).

## Key PR Progress

1. **[#31817 — Update models.json](https://github.com/openai/codex/pull/31817)** — Automated model catalog refresh (still open; keeps the CLI's model list current).

2. **[#37723 — Report I/O subtypes for session config import failures](https://github.com/openai/codex/pull/37723)** — Appends stable `std::io::ErrorKind` categories (`invalid_data`, `not_found`, `permission_denied`) to failure subtypes, improving debuggability of session load errors.

3. **[#37709 — Keep wrapped composer whitespace with following text](https://github.com/openai/codex/pull/37709)** — Fixes a TUI rendering bug where overflowing whitespace in the composer occupied a separate blank row. Includes grapheme-safe wrapping for Unicode whitespace.

4. **[#37654 — Advertise environment config read support](https://github.com/openai/codex/pull/37654)** — Adds `environmentConfigRead` to exec-server capabilities, defaulting to `false` for legacy executors. Enables feature detection for environment config reads.

5. **[#37645 — Improve plugin install failure analytics](https://github.com/openai/codex/pull/37645)** — Adds HTTP status subtypes for remote catalog, mutation, and bundle download failures. Low-cardinality diagnostics for actionable plugin install triage.

6. **[#37644 — Generalize hook handler execution](https://github.com/openai/codex/pull/37644)** — Refactors hook handlers to route through the hooks engine by handler kind, preserving command-hook behavior. Also rejects MCP tool inputs with `null` values that can't be TOML-hashed for trust.

7. **[#37641 — Use step context for command approval prefix rules](https://github.com/openai/codex/pull/37641)** — Reads `allow_prefix_rules` from the active step's turn when constructing unified exec approval requests—fixes a context-mismatch bug in approval policy selection.

## Feature Request Trends

- **Linux desktop support (#11023)** remains the single largest ask, with 945 👍 — no official response yet, and the community is actively discussing workarounds.
- **TUI parity with Claude Code (#17827)** is a recurring theme: customizable status line, task-aware composer placeholders (#13466), and disabling ghost suggestions (#10562) all point to "make the terminal UI as good as the competitor's."
- **Remote/Cross-device workflow gaps** — users want SSH remotes visible on mobile (#23527), Windows pairing entries (#30899), and catch-up policies for missed automations (#24327). The "start on desktop, continue on mobile" story is incomplete on Windows.
- **Session/rollout storage hygiene** — multiple requests for bounded storage (#34337, #35823, #25921) with explicit vacuum/compaction policies.
- **Power-user UX** — persistent named AI team members with roles (#37736) and an embedded micro text editor (#36711) show appetite for richer in-terminal workflows.

## Developer Pain Points

- **Silent disk bloat is the #1 systemic issue**: Crashpad dumps (#25921), `logs_2.sqlite` vacuum gaps (#35823), and shared rollout storage growing to TiB scale (#34337) collectively indicate a lack of storage-budget enforcement across the app and CLI.
- **Windows remains a second-class citizen**: Computer Use failures (#37383, #37281), missing Remote Control pairing (#30899), Unix-only daemon lifecycle (#30372), and MCP server visibility gaps (#37471) all point to incomplete Windows parity.
- **Security hooks are not reliably enforced**: Project hooks silently ignored in worktrees (#27133) and PreToolUse deny not blocking `apply_patch` (#27833) are critical trust-boundary violations that undermine the hooks security model.
- **Desktop rendering instability**: Continuous flickering on both Windows (#34299, #34351) and macOS Tahoe (#35101) after recent updates suggests a shared rendering regression in the Electron shell.
- **Process/thread lifecycle bugs**: Orphaned zsh snapshot processes burning 100% CPU (#25388) and TUI deadlocks under memory pressure (#37735) erode trust in long-running sessions.
- **Owner-discovery timeout on chat resume (#37398)** adds a fixed ~5s delay per unloaded chat—minor individually, but a frequent annoyance for users resuming many threads.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-08-10

## Today's Highlights

The Gemini CLI community is heavily focused on **agent reliability and subagent orchestration**—hanging subagents, incorrect success reporting on turn limits, and permission bypasses dominate the most active issues. Security hardening is also in motion, with a critical PR addressing supply-chain RCE in eval workflows, alongside a fix for Plan Mode's over-trust of MCP server read-only claims. A fresh nightly release (v0.56.0-nightly.20260809) ships incrementally without a notable user-facing changelog, while memory-system bugs and AST-aware tooling remain long-running EPICs awaiting attention.

---

## Releases

- **[v0.56.0-nightly.20260809.gcf22ac7e8](https://github.com/google-gemini/gemini-cli/compare/v0.56.0-nightly.20260808.gcf22ac7e8...v0.56.0-nightly.20260809.gcf22ac7e8)** — Nightly release; no user-facing changelog provided. Incremental updates only.

---

## Hot Issues

1. **[#22323: Subagent recovery after MAX_TURNS is reported as GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)** — A `codebase_investigator` subagent reports "success"/"GOAL" even after hitting max turns without doing analysis. This is misleading for automation dependability. 12 comments, 2 👍. High activity signals it's a top P1.

2. **[#21409: Generalist agent hangs (up to an hour)](https://github.com/google-gemini/gemini-cli/issues/21409)** — The generalist agent hangs forever on trivial tasks (e.g., folder creation). Workaround: instructing the model not to use subagents. Strong community resonance with 8 👍.

3. **[#24353: Robust component-level evaluations (EPIC)](https://github.com/google-gemini/gemini-cli/issues/24353)** — Follow-up to #15300; tracks 76 behavioral eval tests across 6 Gemini models. Aims to institutionalize eval coverage, but is P1 with 7 comments.

4. **[#25166: Shell command stuck on "Waiting input" after completion](https://github.com/google-gemini/gemini-cli/issues/25166)** — Even trivial CLI commands hang post-execution. P1 core bug with 4 comments and 3 👍; common and disruptive in daily workflows.

5. **[#26522: Auto Memory retries low-signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522)** — Sessions that look low-signal are never marked processed, so they resurface continuously—wasteful and annoying. P2, 5 comments.

6. **[#26525: Add deterministic redaction & reduce Auto Memory logging](https://github.com/google-gemini/gemini-cli/issues/26525)** — Privacy concern: transcript content reaches model context before redaction; logging may expose skill content. P2 security issue, 4 comments.

7. **[#21983: Browser subagent fails on Wayland](https://github.com/google-gemini/gemini-cli/issues/21983)** — Browser agent terminates with "GOAL" yet fails silently on Wayland. P1; 4 comments. Linux/DE-specific but blocks a growing user segment.

8. **[#21968: Gemini rarely uses custom skills and subagents autonomously](https://github.com/google-gemini/gemini-cli/issues/21968)** — Despite explicit skills (e.g., gradle/git), the model ignores them unless told. Undermines the agentic value proposition. 6 comments.

9. **[#20079: Symlinked agent files in ~/.gemini/agents not recognized](https://github.com/google-gemini/gemini-cli/issues/20079)** — Symlinks in the agents directory are ignored; breaks dotfile managers (e.g., chezmoi). P2, 4 comments; small but very practical.

10. **[#28745: GeminiCLI.com docs — auth failure for individual accounts](https://github.com/google-gemini/gemini-cli/issues/28745)** — Docs tell users to sign in with an individual Google account, but that client is no longer supported. Immediate onboarding friction; fresh issue (created 2026-08-09).

---

## Key PR Progress

1. **[#28744: fix(acp): don't start fresh chat before resuming — poisons session file](https://github.com/google-gemini/gemini-cli/pull/28744)** — Prevents `initialize()` from creating an empty chat before `resumeChat()`, which was corrupting session files. Closes #28693. P1, core.

2. **[#28738: Allow agents to call agents](https://github.com/google-gemini/gemini-cli/pull/28738)** — Lets subagents delegate to (or recurse into) other subagents via `tools:` frontmatter. Closes #22092. Large change, likely to be a major capability unlock.

3. **[#28740: fix(security): prevent supply chain RCE in eval-pr workflows](https://github.com/google-gemini/gemini-cli/pull/28740)** — Splits eval workflow into secure `pull_request` + trusted `workflow_run` to stop arbitrary code execution from forks. Closes #28336. Critical security fix.

4. **[#28743: fix(core): preserve resolved model config systemInstruction and tools](https://github.com/google-gemini/gemini-cli/pull/28743)** — Prevents chat-level values from overwriting model-specific `systemInstruction`/`tools` from `getResolvedConfig()`. Correctness fix for custom models.

5. **[#28549: fix(mcp): disclose that Plan Mode read-only status is a server claim](https://github.com/google-gemini/gemini-cli/pull/28549)** — `readOnlyHint` from MCP servers is unverified; this PR makes that promise explicit and reclassifies tools to require proper approval. Security-relevant, closes #28548.

6. **[#28742: fix(caretaker-agent): use spec-valid names for triage-worker skills](https://github.com/google-gemini/gemini-cli/pull/28742)** — Fixes two skill names violating the Agent Skills spec (underscores not allowed). Small but needed for ecosystem consistency.

7. **[#26540: fix(core): resolve policy engine bugs affecting tool approvals](https://github.com/google-gemini/gemini-cli/pull/26540)** — Fixes regex null-byte issues and approval persistence bugs in permissive modes (`YOLO`, `AUTO_EDIT`). Maintainer-only; held open for ~3 months. High-impact for automation UX.

8. **[#28535: fix: use resolveRipgrepPath in perf test global setup](https://github.com/google-gemini/gemini-cli/pull/28535)** — Updates perf tests to the new ripgrep resolver API. **Closed**; likely merged or superseded.

9. **[#28534: fix(ci): retry staging-tmp dist-tag removal after npm publish](https://github.com/google-gemini/gemini-cli/pull/28534)** — Adds retry script for `npm dist-tag rm` race with Wombat/npm. **Closed**; CI hardening for nightly releases.

10. **[#28619: Update .gitignore and add unit tests](https://github.com/google-gemini/gemini-cli/pull/28619)** — Adds `.env`/`.ai` to gitignore and unit tests. **Closed** — cleanup-oriented PR that appeared noise-prone (related to #28616/#28617/#28618 from same author, likely a codespace export mess).

---

## Feature Request Trends

- **Deep agent orchestration** — Users want agents to call agents recursively (#28738, #22092), better self-awareness of tools (#21432), and autonomous reuse of custom skills (#21968).
- **AST-aware codebase tooling** — EPIC-level push to make reads/searches/mapping structure-aware for precision and token efficiency (#22745, #22746).
- **Robust behavioral evals** — Scaling to 76+ eval tests across models; subagent trajectories should be shareable for debugging (#24353, #22598).
- **Memory system trust & hygiene** — Deterministic redaction, quarantine of invalid patches, and no infinite retries (#26522, #26523, #26516).
- **Browser agent resilience** — Automatic session takeover, lock recovery, honoring `settings.json` overrides (#22232, #22267).

---

## Developer Pain Points

- **Silent hangs and false successes** — Subagents report GOAL even on max-turns or failure, or hang forever on trivial commands. This erodes trust in autonomous mode (#22323, #21409, #25166, #21983).
- **Subagent/agent permission and activation surprises** — Agents and subagents run despite disabled configs; permissions seem bypassed since v0.33.0 (#22093, #22672).
- **Model not using provided skills/agents** — Workarounds (pinning prompts) are brittle and indicate weak tool-selection heuristics (#21968).
- **Config/agent setup fragility** — Symlinked agent files are ignored; settings.json overrides are silently dropped (#20079, #22267).
- **Privacy and trust concerns in memory** — Redaction happens *after* transcript content is sent to the model; logging may expose skill content (#26525).
- **Tool count limits** — 400 error with >128 tools; expectation is smarter tool-scoping rather than hard failure (#24246).
- **System integration noise** — Terminal corruption after external editors, flicker on resize, and interactive prompt deadlocks degrade UX (#24935, #21924, #22465).

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-08-10

## Today's Highlights

The Copilot CLI community saw a significant spike in triage-stage issue filings, with **13 new issues** reported in the last 24 hours covering MCP reliability, model availability, and performance regressions. The most critical themes revolve around **All Claude models being disabled for Enterprise users** (two separate reports), **MCP initialization and handshake failures** (fixed timeouts, OAuth 3LO issues, and interim deny-all policies), and **parallel tool-calling correlation bugs** that cause bots to lose context. Perfomance concerns include high CPU usage during idle waits and typing latency degradation in long sessions.

---

## Releases

No new releases were published in the last 24 hours. The latest known version remains **1.0.79-1**.

---

## Hot Issues

### 1. All Claude models disabled under CLI model selection (NEW)
**Issue [#4422](https://github.com/github/copilot-cli/issues/4422)** — Users with personal Enterprise accounts report that all Claude models (sonnet 5, 4.8, etc.) are now unavailable, despite appearing enabled in GitHub Copilot settings. The issue persisted across version rollbacks, suggesting a server-side change. **Related:** [#4390](https://github.com/github/copilot-cli/issues/4390) reports enabled organization models missing from the catalogue entirely.

### 2. Keyboard queue cancellation
**Issue [#1857](https://github.com/github/copilot-cli/issues/1857)** (👍 26) — Users want the ability to cancel enqueued messages (via `Ctrl+Q` / `Ctrl+Enter`) while the agent is busy. This long-running request (5 months old) remains one of the most-upvoted open features.

### 3. Remote sessions fail on organization repos
**Issue [#2751](https://github.com/github/copilot-cli/issues/2751)** (👍 13) — `/remote` fails with `Remote session disabled: could not resolve repository` for GitHub organization-owned repos. Enterprise users are actively affected, with 8 comments discussing workarounds.

### 4. MCP OAuth 3LO flow failure
**Issue [#4371](https://github.com/github/copilot-cli/issues/4371)** — MCP Gateway targets configured with OAuth 3LO (Authorization Code grant) fail with error `-32042` because the CLI does not support URL elicitation required for the flow. This blocks enterprise MCP integrations.

### 5. Fixed 60s MCP initialize timeout with no retry (NEW)
**Issue [#4421](https://github.com/github/copilot-cli/issues/4421)** — The MCP `initialize` handshake has a hard-coded 60-second budget. When exceeded, the CLI logs `Recorded failure for server` and **never respawns that server** for the session. `npx`-launched stdio servers fail ~29% of sessions with zero recovery options.

### 6. Interim deny-all MCP policy (NEW)
**Issue [#4419](https://github.com/github/copilot-cli/issues/4419)** — While resolving managed settings, the CLI installs an interim `managedAllowedMcpServerLists: [[]]` policy that rejects any user-configured MCP server registering during that window — even on accounts with no managed policy. The rejection is permanent for the session.

### 7. Parallel tool calling loses request correlation (NEW)
**Issue [#4420](https://github.com/github/copilot-cli/issues/4420)** — The harness does not preserve reliable association between parallel tool requests and responses. Callers receive responses without original requests, and the behavior is non-deterministic, resulting in "confused bots."

### 8. Parallel subagent fan-out hits per-model 429s (NEW)
**Issue [#4416](https://github.com/github/copilot-cli/issues/4416)** — Parallel `explore` subagents all default to the same lightweight model (`claude-haiku-4.5`), which has a much tighter per-model burst limit. No backoff and no auto-switching despite `eligibleForAutoSwitch` being set.

### 9. High CPU usage during idle wait (NEW)
**Issue [#4415](https://github.com/github/copilot-cli/issues/4415)** — Copilot CLI consumes 100% of one CPU core while merely waiting for a `sleep 550; cd /path` command. Users report the issue as a clear resource usage regression.

### 10. Kickoff prompt silently dropped (NEW)
**Issue [#4423](https://github.com/github/copilot-cli/issues/4423)** — When a new session is created with an initial prompt, the worktree/branch/CLI session are provisioned, but the prompt is never delivered to the agent. The session sits idle forever with no assistant response.

---

## Key PR Progress

No pull requests were updated in the last 24 hours. This is a notable gap given the volume of new triage issues — the maintainers appear to be in a triage/prioritization cycle rather than an active PR-merge cycle.

*No PR links to report.*

---

## Feature Request Trends

1. **Configurable MCP timeouts & retries** — Multiple issues ([#4421](https://github.com/github/copilot-cli/issues/4421), [#4419](https://github.com/github/copilot-cli/issues/4419)) push for configurable budgets, backoff, and recovery for MCP handshakes instead of hard-coded fail-closed behavior.

2. **Auto-mode model range control** — [#4412](https://github.com/github/copilot-cli/issues/4412) and the closed [#4411](https://github.com/github/copilot-cli/issues/4411) request user control over Auto-mode's model selection range (min/max strength, bias toward stronger models).

3. **Broader git host support for `/remote`** — [#2922](https://github.com/github/copilot-cli/issues/2922) asks that remote sessions work for non-GitHub repositories (GitLab, Bitbucket), decoupling session control from the git host.

4. **Chinese (zh-CN) localization** — [#4407](https://github.com/github/copilot-cli/issues/4407) requests Chinese UI localization for the desktop app and CLI integration.

5. **Configurable HUD/context display** — [#4418](https://github.com/github/copilot-cli/issues/4418) wants a configurable hub UI (the author points to a community tool, `copilot-hud`, as prior art).

---

## Developer Pain Points

1. **Model availability is inconsistent and opaque** — Two separate reports ([#4422](https://github.com/github/copilot-cli/issues/4422), [#4390](https://github.com/github/copilot-cli/issues/4390)) show Enterprise users losing access to Claude models without clear messaging, with rollbacks not helping. The "This model is disabled" error provides no actionable diagnostics.

2. **MCP integration is fragile and fail-closed** — The 60-second hard-coded timeout ([#4421](https://github.com/github/copilot-cli/issues/4421)), interim deny-all policy ([#4419](https://github.com/github/copilot-cli/issues/4419)), OAuth 3LO incompatibility ([#4371](https://github.com/github/copilot-cli/issues/4371)), and FastMCP incompatibility ([#4370](https://github.com/github/copilot-cli/issues/4370)) collectively paint a picture of a brittle MCP layer that fails permanently for the session.

3. **Parallel tool execution breaks context** — Non-deterministic response ordering ([#4420](https://github.com/github/copilot-cli/issues/4420)) and per-model rate limits on fan-out ([#4416](https://github.com/github/copilot-cli/issues/4416)) cause cascading failures in agentic workflows.

4. **Performance regressions in long sessions** — High CPU usage during idle ([#4415](https://github.com/github/copilot-cli/issues/4415)) and typing latency degradation over long sessions ([#4299](https://github.com/github/copilot-cli/issues/4299), now closed with only 2 comments) suggest resource cleanup gaps.

5. **Silent failures and dropped state** — The dropped kickoff prompt ([#4423](https://github.com/github/copilot-cli/issues/4423)), the inert `cli_remote_control_enabled` setting ([#4409](https://github.com/github/copilot-cli/issues/4409)), and the Autopilot resume bug ([#4329](https://github.com/github/copilot-cli/issues/4329)) show a pattern of features appearing enabled while failing silently.

6. **BYOK providers fail before reaching the provider** — [#4414](https://github.com/github/copilot-cli/issues/4414) reports custom OpenAI/Anthropic-compatible providers returning local 403s that never reach the configured provider, with `/login` being a misleading suggested fix.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest — 2026-08-10

## 1. Today's Highlights

The project saw a quiet release cycle, with no new versions published in the last 24 hours. However, two long-running threads captured community attention: a feature request for a persistent Memory System that has been incubating since February with 27 comments, and a newly reported critical bug where ACP streaming sessions can silently hang, leaving partial responses unwritten to the wire log. Meanwhile, an open PR targeting JSON Schema metadata stripping for Google GenAI tool parameters continues to await review.

## 2. Releases

No new releases were published in the last 24 hours.

## 3. Hot Issues

- **[#2598] — ACP/print streaming response hangs silently** (New, 0 comments)  
  A critical bug report where the CLI (v0.34.0) in ACP mode occasionally hangs after all delta content arrives, because the terminal `[DONE]` frame never comes and there is no idle timeout configuration. Worse, when the user sends the next message, the hung turn is silently replaced, and the partial response never lands in `wire.jsonl`. This strikes at the heart of debugging and traceability, and the lack of a timeout option makes it a blocker for users relying on programmatic automation.  
  [GitHub Issue #2598](https://github.com/MoonshotAI/kimi-cli/issues/2598)

- **[#1283] — Feature Request: Memory System — persistent context across sessions** (27 comments, open since Feb)  
  The most-discussed open issue: a request for a comprehensive memory system (automatic AI-managed notes + manual user-defined instructions) so the CLI retains project patterns and preferences across sessions. The sustained comment activity over five months signals strong community demand for long-term context persistence.  
  [GitHub Issue #1283](https://github.com/MoonshotAI/kimi-cli/issues/1283)

*(Only 2 issues were active in the last 24h; historically active issues of note are referenced above.)*

## 4. Key PR Progress

- **[#739] — fix(kosong): strip JSON Schema metadata from Google GenAI tool parameters** (Open, updated today)  
  A compatibility fix for MCP tools (e.g., Exa MCP) used with the Google GenAI provider, which currently rejects tool parameters that include standard JSON Schema metadata fields (like `title` or `description` that are not part of the OpenAI-style schema subset). This PR resolves #734 and is important for anyone bridging MCP ecosystems to Google-backed models. Despite being created on Jan 28, it remains open — a sign that review bandwidth is stretched.  
  [GitHub PR #739](https://github.com/MoonshotAI/kimi-cli/pull/739)

*(Only 1 PR was active in the last 24h; this is the item to watch.)*

## 5. Feature Request Trends

- **Persistent Memory & Context Across Sessions:** The #1283 request for a memory system (auto + manual) is the clearest signal. Developers want the CLI to behave more like an agent that remembers project patterns and user preferences, rather than treating each session as a blank slate.
- **Robustness in Streaming and Protocol Edge Cases:** The new issue #2598 highlights a demand for explicit idle timeouts and better handling of interrupted / superseded turns — especially around `wire.jsonl` completeness for auditability.

## 6. Developer Pain Points

- **Silent Failures and Lost State:** The most acute pain point is the silent hang in ACP streaming mode where a partial response is dropped (not written to the wire log) and replaced without warning. This undermines trust in the CLI for automation and debugging.
- **Slow Turnaround for Long-Standing Fixes:** The Google GenAI / MCP compatibility PR (#739) has been waiting since late January — over six months — which suggests that integration with third-party providers and MCP tools is not getting the review cycles the community expects.
- **Lack of Configuration for Timeout Behavior:** The official `config.toml` does not expose streaming idle timeout settings, which forces users into infinite waits on flaky network streams.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-08-10

## Today's Highlights

The OpenCode community is experiencing significant friction with the Console Go subscription tier, as multiple reports confirm the DeepSeek V4 Flash model is broken via the relay gateway due to a leading-space injection bug that survived an earlier fix attempt. Concurrently, a longstanding clipboard issue from November 2025 has surged to 122 comments with 110 upvotes, indicating widespread frustration with text-copying reliability. On the development side, several automated PR cleanups for long-standing bugs (nested subagent permission hangs, NAPI crashes, Gemini caching) are being merged, alongside promising new features like worktree-based workspace switching and a redesigned app layout with workspace flows.

## Releases

No new releases in the last 24 hours.

## Hot Issues

1. **[#4283 — Copy To Clipboard is not working](https://github.com/anomalyco/opencode/issues/4283)** — 122 comments, 110 👍
   The most active issue, open since November 2025, affecting users on OpenCode 1.0.62 where selecting response text fails to copy. The high engagement after nine months suggests either a regression or a persistent platform-specific bug. Community reaction: heavy upvoting, multiple OS reports.

2. **[#785 — Is there a way to disable streaming mode?](https://github.com/anomalyco/opencode/issues/785)** — 29 comments, 38 👍
   Long-standing request (July 2025) to support non-streaming providers. The proxy provider "Credal" lacks streaming support, blocking OpenCode usage entirely. This is likely a blocking issue for enterprise/corporate proxy users.

3. **[#12472 — Native Claude Code hooks compatibility (PreToolUse, PostToolUse, Stop)](https://github.com/anomalyco/opencode/issues/12472)** — 17 comments, 38 👍
   Requests compatibility with Claude Code's hooks system (`settings.json`). Users migrating from Claude Code want drop-in parity for lifecycle hooks. Strong signal that OpenCode is being positioned as a Claude Code alternative.

4. **[#41300 / #41306 / #41314 / #41322 — Leading space in DeepSeek V4 Flash model name breaks Go relay](https://github.com/anomalyco/opencode/issues/41300)** — multiple comments, 1-2 👍 each
   Four separate but related reports (all closed) confirming the Console Go gateway injects a leading space into the model name (`" deepseek-v4-flash"`), causing HTTP 400. Issue #41306 explicitly verified the fix in #41211 was ineffective. This is an infrastructure reliability problem affecting paid subscribers.

5. **[#13715 — Permission asks from nested subagent sessions silently hang](https://github.com/anomalyco/opencode/issues/13715)** — 11 comments, 24 👍
   Subagents spawning subagents that request permissions never render the prompt in the TUI. The session hangs indefinitely. Root cause identified in `children()` memo in the session route. **Notably, PR #36046 was closed to fix this.**

6. **[#24649 — OpenCode Go: clarify which models are self-hosted vs. proxied](https://github.com/anomalyco/opencode/issues/24649)** — 16 comments, 32 👍
   Users want transparency about infrastructure. The "Go model" curation is compelling, but the lack of clarity on proxy vs. self-hosted raises trust questions. Closed without clear resolution.

7. **[#33027 — MCP tools connected but not exposed to agent](https://github.com/anomalyco/opencode/issues/33027)** — 7 comments, 3 👍
   MCP server connects and lists 6 tools, but they never appear in the agent's tool list. Signals a possible gap in MCP tool discovery or session context population.

8. **[#30221 — "terminated" error on Go subscription](https://github.com/anomalyco/opencode/issues/30221)** — 9 comments, 4 👍
   All active sessions under Go subscription terminate with an `UnknownError: "terminated"` regardless of model. Does not occur with direct API endpoints. Suggests a Go gateway session lifecycle bug. This is a paid-tier reliability issue.

9. **[#39582 — DeepSeek V4 Flash Free: output truncated mid-sentence](https://github.com/anomalyco/opencode/issues/39582)** — 3 comments
   Free-tier model cuts output without warnings, breaking conversation flow. Community signals quality issues with the free model tier.

10. **[#41430 — Go payment processed but subscription inactive](https://github.com/anomalyco/opencode/issues/41430)** — 3 comments
    Stripe payment completed but workspace dashboard still shows "Subscribe." Billing sync issue undermines trust in the Go tier onboarding flow.

## Key PR Progress

1. **[#36052 — Worktree-based workspace switching with stash-based warp](https://github.com/anomalyco/opencode/pull/36052)** — Closed
   Adds `opencode worktree create|list|remove` CLI subcommands, enabling isolated workspaces via git worktrees. This is a significant workflow feature for developers juggling multiple contexts.

2. **[#36046 — Show permission prompts from nested subagent chains](https://github.com/anomalyco/opencode/pull/36046)** — Closed
   Directly fixes #13715, one of the most upvoted open bugs. Prevents silent hangs by rendering permission asks from multi-level subagent hierarchies.

3. **[#36023 — Upgrade Bun to canary to fix NAPI crash on exit](https://github.com/anomalyco/opencode/pull/36023)** — Closed
   Addresses NAPI crashes on exit across all platforms (Windows, macOS, Linux x64). Closes three related issues (#28046, #31563, #36027). Critical stability fix.

4. **[#36070 — Improve Gemini caching through OpenRouter](https://github.com/anomalyco/opencode/pull/36070)** — Closed
   Enables explicit cache breakpoints for Gemini requests via OpenRouter, improving cost and latency for high-volume users.

5. **[#36068 — Accept Ollama reasoning field in OpenAI Chat deltas](https://github.com/anomalyco/opencode/pull/36068)** — Closed
   Ollama emits `reasoning` (not `reasoning_content`); Schema.Struct stripped it silently. Fixes reasoning visibility for Ollama users.

6. **[#36051 — Preserve clipboard image paths for path-based MCP tools](https://github.com/anomalyco/opencode/pull/36051)** — Closed
   Fixes #17771: pasted clipboard images lost their file path, breaking path-based MCP tools like image readers. Important for multimodal workflows.

7. **[#35982 — Improve prompt caching portability](https://github.com/anomalyco/opencode/pull/35982)** — Closed
   Standardizes prompt caching across AI SDK providers, handling camelCase vs. snake_case differences and capturing cache usage stats. Benefit for token-cost-sensitive users.

8. **[#35994 — Avoid per-file directory list rebuild](https://github.com/anomalyco/opencode/pull/35994)** — Closed
   Performance optimization for the file indexer; appends parent directories once instead of rebuilding the full list per file. Favorable for large repositories.

9. **[#40845 — Redesign non-modal settings](https://github.com/anomalyco/opencode/pull/40845)** — Open (beta)
   Reorganizes settings navigation, splits appearance/notifications, adds Figma-aligned Projects and Extensions views backed by real config/MCP state. Major app UX overhaul.

10. **[#38790 — Add workspace flows to new layout](https://github.com/anomalyco/opencode/pull/38790)** — Open (beta)
    New session location selector: local repo, isolated new workspace, or existing workspace. Composer pill shows branch context. Aligns with the worktree feature above.

## Feature Request Trends

- **Claude Code Parity (High Demand)** — Users increasingly expect drop-in hooks compatibility (#12472) and `AGENTS.md` ignore controls (#4035). OpenCode is being measured against Claude Code's extensibility.
- **Workspace & Session Management** — Multiple requests for persistent session daemons (#41453), multi-window/tabs (#14657), and worktree-based isolation (PR #36052). Developers want long-lived, parallel contexts.
- **UI Interaction Polish** — Requests for `/clear` vs `/new` semantics (#38392), drag-and-drop image support in question tool UI (#31791), and configurable code concealment (#35093). Smaller QoL items with lower urgency.
- **Streaming Flexibility** — Disabling streaming (#785) remains a top request, blocking proxy-based enterprise adopters.

## Developer Pain Points

- **Go Relay Reliability is the Top Blocker** — Four separate issues in 48 hours (#41300, #41306, #41314, #41322) confirming a trivial leading-space bug persists after a supposedly successful fix. Paid subscribers are being blocked by gateway validation that inconsistently handles model IDs. The "terminated" error (#30221) and billing sync failure (#41430) compound the trust problem.
- **Clipboard Functionality Has Been Broken for Nine Months** — Issue #4283 with 122 comments shows this hasn't been prioritized, despite heavy upvoting. The same problem also affects the VS Code extension (#39588).
- **Permission System Fails in Nested Agent Scenarios** — Silent hangs (#13715) are worse than error messages; they waste time and token budget. The fix in PR #36046 is merged, but monitoring for regressions will be important.
- **MCP Tool Integration Remains Flaky** — Connected servers don't consistently expose tools (#33027), and clipboard images don't preserve paths (#36051, now fixed), indicating MCP tool lifecycle needs deeper hardening.
- **Free Tier Quality Erosion** — Truncated outputs (#39582) and rate-limit confusion (#32971, #41448) suggest the free model tier may be oversubscribed or deprioritized, eroding the "try before you buy" funnel.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-08-10

## Today's Highlights
A significant influx of triage activity hit the repo today, with over 20 issues closed as "[untriaged]" — many addressing edge-case bugs in the TUI renderer, extension command routing, and provider connectivity. The most notable fixes landed around GitHub Copilot login rate-limiting (two competing PRs), TUI copy-on-select behavior, and a long-awaited llama.cpp model catalog caching fix. No new releases were published in the last 24 hours.

## Releases
No new releases in the last 24 hours. The latest known version remains **0.84.1**.

## Hot Issues

1. **[#7730 — High CPU usage on Mac OS with long session](https://github.com/earendil-works/pi/issues/7730)** (OPEN, 6 👍)  
   Users report 50–110% CPU with 600–800MB memory during long sessions, apparently correlated with context size. This is an unresolved performance concern that could impact productivity for heavy users.

2. **[#6922 — Default model cannot be a llama.cpp model](https://github.com/earendil-works/pi/issues/6922)** (CLOSED, 14 👍, 9 comments)  
   The highest-reacted issue this week. Startup fails with "No models available" when defaulting to a llama.cpp model, related to a race condition with async model refresh. Closed as fixed via PR #7072.

3. **[#7869 — ai21 api broken](https://github.com/earendil-works/pi/issues/7869)** (CLOSED)  
   AI21 retired their legacy API, breaking Pi integrations. Users must migrate to the new AI21 Gateway. Highlights the fragility of third-party API dependencies.

4. **[#7868 — Renderer hard-crashes on wide lines](https://github.com/earendil-works/pi/issues/7868)** (CLOSED)  
   A single rendered line exceeding terminal width aborts the entire session instead of wrapping/truncating — a severe UX bug that killed real work sessions. Priority fix candidate.

5. **[#7860 — EPIPE crash when desktop host closes stdout pipe](https://github.com/earendil-works/pi/issues/7860)** (CLOSED)  
   Running Pi as an external CLI agent inside desktop apps crashes with unhandled EPIPE. A fix PR #5183 exists but was never merged — community frustration over stalled fixes.

6. **[#7861 — Scroll position jumps while streaming long output](https://github.com/earendil-works/pi/issues/7861)** (CLOSED)  
   Another TUI scroll regression: reading earlier output while streaming is impossible because the view keeps snapping back. Closely related to #7495 and #7616.

7. **[#7855 — "Response was truncated before completion"](https://github.com/earendil-works/pi/issues/7855)** (CLOSED)  
   Random truncation errors with OpenAI-compatible APIs (VLLM tested). Users must manually prompt continuation — a reliability issue with no clear reproduction path yet.

8. **[#7850 — GitHub Copilot login fails with 429 for large orgs](https://github.com/earendil-works/pi/issues/7850)** (CLOSED)  
   Organizations with 20+ models hit GitHub's rate limit during concurrent policy enablement. Fixed by two PRs (#7851, #7844) that serialize requests.

9. **[#7846 — Unable to start 0.84.x with bun runtime](https://github.com/earendil-works/pi/issues/7846)** (CLOSED)  
   `zlib.createZstdDecompress is not a function` under Bun — a dependency compatibility problem blocking Bun users entirely.

10. **[#7848 — Auto-compaction stops active task instead of resuming](https://github.com/earendil-works/pi/issues/7848)** (CLOSED)  
    After auto-compaction, Pi sometimes halts and waits for user input instead of continuing the in-progress task — particularly with larger context models. A workflow-breaking bug for long-running agents.

## Key PR Progress

1. **[#7072 — fix(coding-agent): cache llama.cpp model catalog](https://github.com/earendil-works/pi/pull/7072)** (CLOSED)  
   Fixes #6948, resolving the startup race condition where default llama.cpp models weren't applied. The most anticipated fix this cycle, already merged.

2. **[#7866 — feat(tui): add copyOnSelect option to TuiAltScreen](https://github.com/earendil-works/pi/pull/7866)** (CLOSED)  
   Addresses #7720. New `copyOnSelect` option (default `true`) lets users disable automatic copy-to-clipboard when selecting text in fullscreen TUI mode.

3. **[#7865 — fix(tui): handle tui.select.pageUp/pageDown in base SelectList and model-selector](https://github.com/earendil-works/pi/pull/7865)** (CLOSED)  
   Adds missing PageUp/PageDown keybinding support across all selector components, fixing inconsistent behavior in model and history selection UI.

4. **[#7344 — feat(protocol): add remote session wire protocol](https://github.com/earendil-works/pi/pull/7344)** (CLOSED)  
   Major architectural addition: a transport-neutral `@earendil-works/pi-protocol` package with validated commands, bounded CBOR encoding, and length-prefixed framing. Enables future remote-session capabilities. Closed — pending release?

5. **[#7858 — fix(coding-agent): route extension commands regardless of expandPromptTemplates](https://github.com/earendil-works/pi/pull/7858)** (CLOSED)  
   Fixes #7859. Extension commands queued via `sendUserMessage()` are now routed even when `expandPromptTemplates` is false, making the documented extension pattern work.

6. **[#7857 — feat(agent): expose expandPromptTemplates in sendUserMessage](https://github.com/earendil-works/pi/pull/7857)** (OPEN)  
   Companion to #7858. Exposes the option to callers so tools can explicitly request command expansion. Currently open, likely to be merged after review.

7. **[#7856 — fix(ai): repair JSON-serialized structured tool arguments during validation](https://github.com/earendil-works/pi/pull/7856)** (CLOSED)  
   Fixes double-serialized JSON strings in tool args: object-typed params no longer hard-fail, strings are JSON-parsed when applicable. Quality-of-life correctness fix.

8. **[#7851 — fix(provider): enable GitHub Copilot model policies sequentially](https://github.com/earendil-works/pi/pull/7851)** (CLOSED)  
   Serializes Copilot model policy requests to avoid 429 rate limits for orgs with many models. One of two competing fixes for #7850, both merged.

9. **[#7844 — Prevent bulk policy updates during login](https://github.com/earendil-works/pi/pull/7844)** (CLOSED)  
   Complementary fix for the same Copilot 429 issue. Removes bulk model enabling from login entirely, deferring explicit model activation.

10. **[#7840 — docs: add Aliyun Model Studio CLI (bailian-cli) to Related Tools](https://github.com/earendil-works/pi/pull/7840)** (CLOSED)  
    Simple docs addition, but signals growing ecosystem mindshare: third-party CLI integrations are being actively listed in the README as related tooling.

## Feature Request Trends

- **TUI reliability and ergonomics dominate.** Scroll-position preservation during streaming (#7861, #7495, #7616), mouse click-to-position in textarea (#7852), and copy-on-select opt-out (#7720, #7866) show heavy investment in interactive terminal UX.
- **Remote session protocol on the horizon.** PR #7344 introduces the wire protocol foundation, suggesting distributed/headless agent sessions as a strategic direction.
- **Cross-session memory and subagents are requested.** Issue #7845 proposes porting stream rules, subagent tools, and cross-session memory — a capability gap vs. competitor products.
- **Provider resilience is a recurring theme.** Qwen China Individual plan (#7847), AI21 migration (#7869), and Copilot org policies (#7850) show demand for broader, more robust provider support.

## Developer Pain Points

- **TUI scroll behavior is the #1 frustration.** Three separate issues (#7861, #7495, #7616) describe the same core problem from different angles: the viewport jumps during streaming and after tool blocks expand. The differential renderer's "safe path" full-clear is making it worse.
- **Unhandled process-level crashes.** EPIPE on closed stdout (#7860), hard renderer aborts on wide lines (#7868), and SIGTERM-ignoring children that never die (#7864) represent a class of "one bug kills the whole session" problems.
- **Silent failures and skipped work.** MutableModels.refresh() skipping providers without credentials (#7854) and auto-compaction stopping tasks instead of resuming (#7848) undermine trust in background processes.
- **Bun runtime incompatibility.** The zstd decompress error (#7846) blocks an entire runtime community — a dependency issue that should be caught in CI.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-08-10

## Today's Highlights

The Qwen Code team is driving major architectural consolidation this week: two RFCs propose unifying the fragmented session reasoning loops and adding native multi-session coordination, signaling a push toward a more deterministic workflow engine. Stability work dominates the PR queue — the autofix bot is churning through CI failures, shell-registry test flakes, and daemon transcript rendering bugs. A notable security fix closes two read-only shell classifier bypasses via line continuation and `${var@P}` expansion, and a Windows mojibake fix for non-UTF-8 code pages is ready for review.

## Releases

No new stable releases in the last 24 hours. The nightly build `v0.21.8-nightly.20260809.73e9eab626` failed its release workflow on the `integration_none` and `integration_docker` jobs ([#8771](https://github.com/QwenLM/qwen-code/issues/8771)).

## Hot Issues

1. **[RFC: Native coordination for independent Qwen sessions](https://github.com/QwenLM/qwen-code/issues/8718)** — [OPEN, P2, 8 comments] Proposes a leader-worker dispatch model where one interactive session coordinates 2–3 self-contained workers with correlated state observation. Community discussion is active around the experimental coordination path. A natural companion to the workflow-engine push.

2. **[Unify session reasoning loops on a Turn-based SessionRuntime](https://github.com/QwenLM/qwen-code/issues/8775)** — [OPEN, P2, 2 comments] Identifies that every surface (`useGeminiStream`, `runNonInteractive`, ACP `Session`, `acp-bridge`, `serve` dispatch, `AgentCore`) independently implements the same send→stream→dispatch loop. The proposal to unify on one runtime would be a significant maintainability win.

3. **[Hidden unrecognized diagnostics mutate and evict transcript state](https://github.com/QwenLM/qwen-code/issues/8823)** — [OPEN, P2, 3 comments] Unrecognized daemon events are normalized into debug events, but they mutate shared transcript state before being hidden by the renderer. This creates user-visible corruption — a subtle but high-impact bug for Web Shell users.

4. **[Streamable HTTP optional GET/SSE stream 404 kills the whole MCP connection](https://github.com/QwenLM/qwen-code/issues/8784)** — [OPEN, P2, 5 comments] A spec-optional server-push probe fails, and the entire MCP connection dies. Interop issue that will matter as more MCP servers adopt Streamable HTTP.

5. **[Windows standalone installer fails when powershell.exe cannot resolve Get-FileHash](https://github.com/QwenLM/qwen-code/issues/7118)** — [OPEN, P2, 6 comments, 👍3] Installation fails during SHA-256 verification on PowerShell-constrained environments. 3 upvotes signal real-world Windows user friction; tagged `welcome-pr`.

6. **[`fix(serve)`: Preserve the current session when a large restore times out](https://github.com/QwenLM/qwen-code/issues/8678)** — [OPEN, P1] PR1 (timeout contract + observability) is merged in #8691; the session-preservation portion remains. High priority — large-session restore timeouts are a daily pain for long-lived users.

7. **[Rebuild `/review` Step 3–5 orchestration on the workflow engine](https://github.com/QwenLM/qwen-code/issues/8769)** — [OPEN, P2, 4 comments] Proposes moving agent fan-out, verification, and reverse audit from model-driven execution to deterministic workflow code. Part of the broader workflow-engine trend.

8. **[OTEL_METRICS_EXPORTER=otlp silently disables metrics export](https://github.com/QwenLM/qwen-code/issues/8697)** — [CLOSED, P2] When sharing a collector with Claude Code, Codex, etc., the standard env var breaks native metrics while traces keep flowing. Common multi-tool setup; good that it's resolved.

9. **[Security: read-only git sub-commands can execute programs in `.git/config`](https://github.com/QwenLM/qwen-code/issues/8575)** — [CLOSED, P2] `diff.external` / `core.fsmonitor` configs can execute arbitrary programs despite the command text being classified read-only. Serious security surface; two bypasses were reproduced in #8582.

10. **[CI E2E flake: `cli/extensions-install.test.ts` > installs a local Qoder plugin](https://github.com/QwenLM/qwen-code/issues/8799)** — [CLOSED] Recurring E2E failure (also in #8766) tracking a local-plugin installation test. The autofix bot keeps tripping on it — likely an environment-dependent path or timing issue.

## Key PR Progress

1. **[fix(web-shell): stop rendering unrecognized daemon events in transcripts](https://github.com/QwenLM/qwen-code/pull/8812)** — Fixes #8823 by stamping a structured `debugReason` on debug events and branching Web Shell on it instead of pattern-matching. Clean architectural fix for the transcript corruption bug.

2. **[fix(workflows): make replay journal durable](https://github.com/QwenLM/qwen-code/pull/8735)** — Serializes journal writes through a per-run queue, makes pause/terminal state wait for durable checkpoints, and validates the committed journal prefix on recovery. Important for workflow reliability.

3. **[fix(core): close read-only classifier bypasses via line continuation and `${var@P}`](https://github.com/QwenLM/qwen-code/pull/8590)** — Closes the two security bypasses from #8582. Downgrades read-only classification when detection finds Bash line continuations or prompt expansion. Security-critical, self-reported review status.

4. **[feat(cli): adopt Goal v3 in ACP sessions](https://github.com/QwenLM/qwen-code/pull/8732)** — Replaces the legacy Stop-hook `/goal` with the canonical Goal v3 runtime (create/status/edit/pause/resume/replace/clear) already used by the CLI. Consistency win for ACP/Web Shell.

5. **[fix(core): catch content-only thinking-tag leaks on all OpenAI-compatible providers](https://github.com/QwenLM/qwen-code/pull/8818)** — Extends the `<think>`-tag leak defense from one vendor's opt-in to all OpenAI-compatible endpoints, closing two real-world bypasses.

6. **[feat(web-shell): expose channel sessions in sidebar and settings](https://github.com/QwenLM/qwen-code/pull/8457)** — Adds a Tasks/Channels source switch for DingTalk, Feishu, WeCom sessions over the project session catalog. Integration surface expanding.

7. **[feat(chrome): add Qwen WebBridge direct browser control](https://github.com/QwenLM/qwen-code/pull/8707)** — Adds a Kimi WebBridge-compatible `/command` and `/status` endpoint surface from `qwen serve` to a real Chromium profile via the Qwen Chrome extension. Full 17-action surface, task-scoped ownership.

8. **[fix(desktop): open Local Control on the active session](https://github.com/QwenLM/qwen-code/pull/8806)** — QR-code pairing now captures the active Desktop session instead of opening a blank Web Shell. Handoff keeps only session path + workspace identifier, strips private runtime credentials.

9. **[fix(core): decode shell output using full-buffer encoding detection to prevent Windows mojibake](https://github.com/QwenLM/qwen-code/pull/7955)** — Fixes CP-866/936/932 garbling by detecting encoding from the full buffer instead of the first chunk. Long-open (since 07-28), Windows users will appreciate this one.

10. **[fix(ci): watchdog silent sandbox hangs and reap the containers they leak](https://github.com/QwenLM/qwen-code/pull/8816)** — Adds an idle watchdog (`QWEN_IDLE_TIMEOUT_MS`, default 20 min) to kill hung agents with a distinct error, plus container cleanup. Targets the "silent 2-hour sandbox hangs" that have been eating autofix rounds.

## Feature Request Trends

Three clear directions are emerging from the issue tracker:

1. **Deterministic orchestration** — Two RFCs (#8769, #8775) plus the workflow-engine PRs (#8735) push toward making agent fan-out, review loops, and session reasoning explicit workflow code rather than model-driven improvisation. Expect `/review` and `/audit` to become workflow-engine showcases.

2. **External integration profiles** — Two proposals from `doudouOUC` define official, provider-neutral profiles for external memory (#7449) and direct external context providers (#7585). Documentation-first, compatibility-tested, no Core API changes — the community is asking for a "works out of the box" enterprise integration story.

3. **Multi-surface session coherence** — The daemon is becoming the authoritative session owner: Web Shell reconciliation (#8798), Local Control QR pairing (#8595→#8806), channel sessions (#8457), and session-ID coordination across transports (#8411) all point to "one session, many surfaces, no divergence."

## Developer Pain Points

Recurring themes from the last 24 hours of issues and PRs:

- **CI flakiness is eating developer time** — Five CI-failure issues in this window alone (#8756, #8822, #8799, #8766, #8771), several with the same failing test (`extensions-install.test.ts > installs a local Qoder plugin`). The autofix bot is churning, and the team is building watchdogs (#8816) to mitigate silent sandbox hangs. Test isolation (shared `/tmp/s1.output` in #8813) is a known culprit being fixed.

- **Windows remains a second-class citizen** — Installer SHA-256 failure on restricted PowerShell (#7118), mojibake from OEM code pages (#7955), and a Desktop bundled-runtime crash (`EISDIR lstat 'C:'` on startup, #8615) all landed recently. Each has a `welcome-pr` label or a pending review.

- **OpenTelemetry interop friction** — The `OTEL_METRICS_EXPORTER=otlp` silent failure (#8697) is now closed, but it highlights a broader pain: qwen-code shares a collector with other OTel-instrumented CLIs, and env-var compatibility matters for anyone running multiple agent tools.

- **MCP spec edge-cases bite** — The optional GET/SSE probe 404 killing the whole connection (#8784) shows users are hitting spec-optional paths that the client isn't handling gracefully. Expect more MCP hardening as Streamable HTTP adoption grows.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-08-10

## Today's Highlights

The project (actively developed as CodeWhale) is in heavy release-preparation mode: **v0.9.6** is being cut as a "subtractive runtime release" that removes harness-created obstruction while preserving explicit budgets, deadlines, and cancellation semantics. The v0.9.5 milestone tracker (#5266) is active, and several closed issues from the v0.9.3–v0.9.5 era have been finalized, including fleet model class resolution (#3205) and CLI/TUI parity for subagent control (#4022). Community activity is strongest around **context compaction behavior** — with users reporting that 1M-window models silently compact at 128K (#5239, #5134, #5244) — and around **Chinese localization**, with a heated discussion on how to translate "Constitution" (#4949).

---

## Releases

**v0.9.6** (preparing, PR #5313):

- "Subtractive runtime release" focused on removing harness-created obstruction
- Preserves explicit budgets, deadlines, cancellation, and truthful provider state
- Rebuilds compaction around one provider summary plus a committed successor handoff (no mailbox freezes)
- Companion fixes: CNB asset download URLs (#5308), crate publication order validation (#5306)

**v0.9.5** (recently shipped, milestone #5266):

- Compaction is now **live and pressure-aware** (PR #5301) — manual `/compact` is nonblocking, auto-compaction eligibility aligned across 128K/272K/1M windows
- Unknown model IDs no longer silently degrade to 128K fallback without warning (#5244)
- Fleet/session names now displayed for sub-agent identity instead of opaque agent IDs (#5287)
- Deny-by-default approval selection is configurable and clearly explained (#5293)

---

## Hot Issues

1. **#4949 — Chinese Translation of "Constitution"** (8 comments, open)  
   A localization debate: should "Constitution" be translated as "宪法" (constitution, with political baggage), "协作准则" (collaboration guidelines), or something else? Community is split; the author is soliciting native-speaker input. This highlights the project's global user base and the sensitivity of legal/political terminology in documentation.  
   https://github.com/Hmbown/CodeWhale/issues/4949

2. **#5239 / #5134 — 1M-Context Models Compacting at 128K** (1 and 3 comments)  
   Users with DeepSeek v4 Flash and Qwen3.6 report that compaction triggers at 128K even though the model supports 1M. #5239 includes a screenshot, and #5134 asks how to adjust the context length. Root cause tracked in #5244 (closed): unknown model IDs fall through to `LEGACY_DEEPSEEK_CONTEXT_WINDOW_TOKENS`. Community frustration is palpable — this is a daily workflow blocker for long sessions.  
   https://github.com/Hmbown/CodeWhale/issues/5239 | https://github.com/Hmbown/CodeWhale/issues/5134

3. **#5096 — Compaction Gain Not Visible** (3 comments, open)  
   After `/compact` reports success, the token counter remains unchanged (e.g., 37K/128K). Users can't tell if compaction actually freed context. The reporter (jbousquie) uses a French UI, so this is also a localization/internationalization validation case.  
   https://github.com/Hmbown/CodeWhale/issues/5096

4. **#5293 — Deny-by-Default Approval Selection** (4 comments, open, 👍 1)  
   v0.9.4 changed the default highlighted option in the TUI permission dialog. Users who habitually press Enter to approve may now accidentally deny actions. The community is asking for configurability and clearer explanation of the new default.  
   https://github.com/Hmbown/CodeWhale/issues/5293

5. **#5209 — File Edit Tool Silent False Positives** (3 comments, open)  
   The `File` tool with `action=edit` accepts wrong parameter names (e.g., `new_str` instead of `replace`), returns "Replacement successful," but doesn't actually change anything. One user reports needing 3–5x re-edits per location. This erodes trust in the tool layer — a critical reliability gap.  
   https://github.com/Hmbown/CodeWhale/issues/5209

6. **#5000 — Interrupted Output Not Durable** (2 comments, open)  
   When a turn is interrupted before `MessageComplete`, the already-emitted assistant text stays only in the TUI's local display, not in the authoritative session. The next model turn has no memory of what was said, causing context fragmentation.  
   https://github.com/Hmbown/CodeWhale/issues/5000

7. **#5023 — IME Candidate Window Jumps** (2 comments, open)  
   Chinese/Japanese IME users on Windows 11 report unstable candidate-window positioning during input. A companion PR (#5205) stabilizes Tabby specifically; this issue tracks the general case.  
   https://github.com/Hmbown/CodeWhale/issues/5023

8. **#5098 — Fleet Config Silent Shadowing** (2 comments, open)  
   Editing `~/.codewhale/agents/builder.toml` to change a model had no effect — the fleet roster and dispatches still resolved to the old model due to a hidden layer of config precedence. Users don't know which config file wins; this is a transparency problem for sub-agent management.  
   https://github.com/Hmbown/CodeWhale/issues/5098

9. **#5047 — API Keys Persist Only in Working Repo** (1 comment, open)  
   Provider API keys sometimes save to `<cwd>/.codewhale/config.toml` (plaintext, repo-visible) instead of the durable global secret store. Moving projects loses the key, and stranded plaintext keys are a security risk in shared repos.  
   https://github.com/Hmbown/CodeWhale/issues/5047

10. **#5314 — Copy Message Includes Rail Decorations** (1 comment, open)  
    Context-menu "Copy message" copies role glyphs (`●`) and rail characters (`▏`) into the clipboard, while selection-based copy is clean. A small but annoying UX bug for users who quote model output elsewhere.  
    https://github.com/Hmbown/CodeWhale/issues/5314

---

## Key PR Progress

1. **#5313 — chore(release): prepare v0.9.6** (merged)  
   The subtractive release: removes harness-created obstruction; rebuilds compaction around a single provider summary plus committed successor handoff; keeps explicit budgets/deadlines/cancellation.  
   https://github.com/Hmbown/CodeWhale/pull/5313

2. **#5301 — fix(tui): make compaction live and pressure-aware** (merged)  
   Manual `/compact` now runs nonblocking and is serialized with typed lifecycle IDs; auto-compaction eligibility aligned with full conservative request pressure across 128K/272K/1M windows; persistent status labels remain truthful.  
   https://github.com/Hmbown/CodeWhale/pull/5301

3. **#5295 — feat: add Mistral AI as a first-class provider route** (merged)  
   First-time contributor @xavierpestel-ai adds Mistral (la Plateforme) as a first-class route. Defaults to `mistral-code-latest`; supports `provider = "mistral"`, `CODEWHALE_PROVIDER=mistral`, and `codewhale --provider mistral`.  
   https://github.com/Hmbown/CodeWhale/pull/5295

4. **#5133 — feat(runtime-api): expose persistent goal-loop state and completion controls** (merged)  
   Adds `GET/POST/DELETE /v1/threads/{id}/goal` endpoints so managed clients can read active-goal state and drive lifecycle transitions through the canonical runtime boundary.  
   https://github.com/Hmbown/CodeWhale/pull/5133

5. **#5132 — Runtime API: expose verifier receipts and evidence** (merged)  
   Three new read-only endpoints under `/v1/fleet/runs/{run_id}/` — `receipts`, `failure`, and `retry` — so managed clients can identify which verifier task failed, why, and whether retry is appropriate.  
   https://github.com/Hmbown/CodeWhale/pull/5132

6. **#5131 — feat: Runtime API memory endpoints** (merged)  
   New `/v1/memory` routes (list, get, update, delete) gated by `require_runtime_token`, giving managed clients bounded inspection and lifecycle control over active memory without a second memory store.  
   https://github.com/Hmbown/CodeWhale/pull/5131

7. **#5130 — feat(runtime-api): bounded MCP server configuration and lifecycle management** (merged)  
   Adds `POST/PUT/DELETE /v1/apps/mcp/servers` so clients can add, update, and remove MCP servers via HTTP instead of editing TOML/JSON directly.  
   https://github.com/Hmbown/CodeWhale/pull/5130

8. **#5129 — feat(runtime-api): skill lifecycle endpoints** (merged)  
   Full skill lifecycle (install, update, uninstall, trust, audit) exposed via HTTP, matching TUI capabilities — all protected by existing `require_runtime_token` middleware.  
   https://github.com/Hmbown/CodeWhale/pull/5129

9. **#5205 — Stabilize IME candidate positioning in Tabby** (merged)  
   Detects `TERM_PROGRAM=Tabby`, enables low-motion rendering and bounded redraw cadence, and disables focused cursor-style updates — preventing Chinese IME candidate windows from jumping during rapid redraws.  
   https://github.com/Hmbown/CodeWhale/pull/5205

10. **#5308 — fix(release): use CNB asset download URLs** (merged)  
    Switches both updaters to the canonical `codewhale.net/codewhale` slug and adds the required `/-/releases/download/vX.Y.Z/` path so mirror mode receives binary assets instead of release HTML.  
    https://github.com/Hmbown/CodeWhale/pull/5308

---

## Feature Request Trends

- **Multiple API key support** (#5250): Users juggling DeepSeek + GLM (or other providers) want to save per-provider keys instead of a single slot that gets overwritten.
- **TUI-native session management** (#576): Forking sessions still requires CLI escape (`deepseek fork <id>`) — users want an in-TUI `/fork` interactive picker.
- **Read-before-edit guardrails** (#3364, #5209): Strong demand for enforced fresh reads before edits and loud, specific edit failures — the silent false-success case is a top reliability pain.
- **Structured compaction contract** (#4394, #5043): Community wants compaction to preserve active intent, decisions, evidence, and tool continuity — and a documented "survival contract" for what lives past compaction.
- **Provider/model resolution coherence** (#5034, #5244): Switching providers should never leave stale default models or silently fall back to 128K; users want loud warnings.
- **First-class multimodal support** (#5102): Agents need a deliberate screenshot/UI-capture tool (kimicode ReadMediaFile) rather than path-luck + File-read.

---

## Developer Pain Points

- **Context compaction is the #1 frustration**: silent 128K fallback for 1M models (#5239/#5134/#5244), no visible gain after `/compact` (#5096), and — until recently — blocking/non-transparent compaction behavior (#5301). Long-session users feel this daily.
- **Tool layer trust deficit**: At least 6 closed/open issues relate to edits failing silently or needing 3–5x retries (#5209, #3364, #5244). The community wants fail-loud, fail-fast behavior with exact diagnostics.
- **Configuration transparency**: Fleet config shadowing (#5098) and API-key repo-local persistence (#5047) both undermine user control. "Which file wins?" and "where did my key go?" are recurring questions.
- **Interrupted-work data loss**: #5000 (interrupted output not durable) and #5043 (compaction losing intent) both reflect the same core concern — the session transcript and the authoritative state must stay in sync even on partial failures.
- **Internationalization friction**: IME window instability (#5023) and terminology debates (#4949) show the non-English user base is growing — and hitting rough edges that English-first CRUD doesn't surface.
- **Flaky CI/tests**: #5056 documents 12 untriaged `#[ignore]` tests and verifier background tests that flake under parallelism; #5054 shows a permanently-dark Claude PR review gate. Both delay merges and reduce confidence in automated checks.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/kky-wollu/agents-radar).*
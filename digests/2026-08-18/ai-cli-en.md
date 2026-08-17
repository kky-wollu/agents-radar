# AI CLI Tools Community Digest 2026-08-18

> Generated: 2026-08-17 22:28 UTC | Tools covered: 9

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

# AI CLI Tools Ecosystem — Cross-Tool Comparison Report

**Date:** 2026-08-18
**Scope:** Claude Code, OpenAI Codex, Gemini CLI, GitHub Copilot CLI, Kimi Code CLI, OpenCode, Pi, Qwen Code, DeepSeek TUI (CodeWhale)

---

## 1. Ecosystem Overview

The AI CLI developer tools landscape is entering a **stability-and-trust phase** — not a feature-race phase. Across all nine tools, the dominant community themes are remarkably consistent: memory leaks in long-running sessions, subagent orchestration fragility, Windows-specific regressions, MCP lifecycle management failures, and model follow-through compliance. Every major tool shipped either patch releases or no releases at all in the last 24 hours, signaling a **consolidation period** where maintainers are prioritizing reliability over new capabilities. The most telling signal: users are building defensive hooks, adversarial checks, and guardrails *around* these tools to compensate for behavioral inconsistencies — a pattern that suggests the tools are powerful enough to be indispensable, but not yet predictable enough to be trusted. The ecosystem is also bifurcating: established players (Claude Code, Codex, Gemini) battle memory/process-model issues inherited from rapid scaling, while newer entrants (Kimi, OpenCode, Pi) focus on automation-friendliness and cross-platform parity — suggesting the "build fast, fix later" phase is ending and the "harden what exists" phase has begun. Cross-tool learnings are visibly circulating: context compaction, append-only compaction, preemptive overflow checks, and process-tree observability are being requested across at least four distinct tool communities simultaneously.

---

## 2. Activity Comparison

| Tool | Issues (notable, last 24h) | PRs (notable, last 24h) | Release Status | Community Signal |
|---|---|---|---|---|
| **Claude Code** | 10 highlighted (3 memory-leak clusters) | 10 highlighted | **v2.1.234** shipped today | Steady patch cadence; severe memory-leak reports cluster |
| **OpenAI Codex** | 10 highlighted (3 Windows-specific) | 10 highlighted | **rust-v0.148.0-alpha.21** (no changelog) | High engagement on auto-resolve timeout (78 comments); active PR wave |
| **Gemini CLI** | 10 highlighted (subagent reliability cluster) | 10 highlighted | **v0.56.0-nightly** (single SSR fix) | Subagent reliability is the #1 theme; security-tagged PRs |
| **GitHub Copilot CLI** | 10 highlighted (MCP OAuth regressions) | 1 highlighted (README removal) | **No release** (last: v1.0.80) | Quiet; long-session stability complaints growing |
| **Kimi Code CLI** | 10 highlighted (mostly older, low velocity) | 1 updated (──starting-prompt merged) | **No release** | Minimal activity; single quality-of-life win |
| **OpenCode** | 10 highlighted (Windows + gateway issues) | 10 highlighted | **No release** | Active issue reporting; strong PR velocity |
| **Pi** | 50 open/updated issues | 34 PRs | **No release** | Highest raw activity; provider compatibility focus |
| **Qwen Code** | 10 highlighted (Windows paste regression) | 10 highlighted | **v0.21.13** pinned benchmark; nightly | Active fix pipeline; benchmark validation rigor |
| **DeepSeek TUI (CodeWhale)** | 10 highlighted (test-suite flakes) | 10 highlighted | **v0.9.9** shipped today | Rebrand + reliability release; community contributions growing |

**Interpretation:** Pi has the highest raw activity (50 issues / 34 PRs in 24h), suggesting either a larger community or more aggressive triage. Claude Code and Qwen have the most mature release discipline. GitHub Copilot CLI shows the least community activity — but its issues are the most *organizationally significant* (OAuth regressions, enterprise model catalog gaps).

---

## 3. Shared Feature Directions

### 3.1 Memory / Process-Model Observability (HIGHEST SIGNAL)
| Tool | Specific Need | Evidence |
|---|---|---|
| Claude Code | `--debug-process-tree` flag / lifecycle tracing; re-exec'd helper processes leak 10-12 GB RSS | 3 separate issues, all OOM-killed |
| OpenAI Codex | TUI thread replay buffers bounded by delta size; zombie MCP processes | #39081 (merged), #25744, #38754 |
| Gemini CLI | MessageBus.request silent hangs; indefinite TUI "Initializing..." | #28816, #28812 |
| GitHub Copilot CLI | Memory-pressure watchdog loops at 23% context usage until OOM | #4506 |
| Pi | Preemptive compaction *before* provider overflow, not after | #6879 (17 👍) |
| Qwen Code | Daemon transcript retention caps; request-body memory bounds | #9303 (PR), #8051 |

**Common thread:** Users are demanding insight into *where* memory goes, *when* processes spawn, and *why* they don't die. The re-exec-heavy process architecture is a recurring root cause across Claude Code, Codex, and Gemini.

### 3.2 Context / Session Persistence & Compaction
| Tool | Specific Need | Evidence |
|---|---|---|
| Claude Code | Config-directory control for multi-session hosts | `CLAUDE_CODE_PROJECT_DIR_NAME` (shipped) |
| OpenAI Codex | Multi-agent V2 produces >100 GiB session data | #34268 |
| Gemini CLI | Auto Memory low-signal sessions retry indefinitely; pre-redaction privacy | #26522, #26525 |
| Kimi Code CLI | Session save/resume; context compaction on overflow | #819, #849 (PR) |
| Pi | Append compaction to reuse provider prompt caches | #8120 (PR, experimental) |
| Qwen Code | Compression math accuracy; status bar refresh after `/compress` | #9309, #6806 |
| DeepSeek TUI | Config-path fragmentation (Windows/Cygwin); silent secret-skip migration | #2369 |

**Common thread:** Long-running sessions are the *new normal*. Users treat sessions as knowledge bases, not ephemeral chats — and the tools are struggling to keep state consistent, compacted, and portable.

### 3.3 Windows Platform Parity (PERSISTENT PAIN)
| Tool | Specific Issue | Evidence |
|---|---|---|
| Claude Code | VSCode extension tool-call rendering as literal text on Windows | #63580 |
| OpenAI Codex | MCP stdio servers never reaped; 350-800 MiB/s read loops | #38754, #38518 |
| Kimi Code CLI | ANSI escape corruption in PowerShell/CMD; UTF-8 mangling | #832, #837 (PR) |
| OpenCode | ARM64 TUI crash; `serve` fails with zero diagnostics; MSIX PowerShell breaks ripgrep | #19130, #43110, #40623 |
| Qwen Code | Ctrl+V paste broken since 0.21.x | #9061 (P1) |
| DeepSeek TUI | SSH blocked by sandbox; config paths diverge on Cygwin | #1829, #2369 |
| Pi | — (notably absent from Windows complaints) | — |

**Common thread:** Windows is consistently the *second-class citizen*. The gap is not getting smaller. Tools that solve Windows well (Pi is notably quiet on this front — potentially a differentiator or just lower Windows adoption).

### 3.4 MCP Lifecycle Management (EMERGING, CROSS-CUTTING)
| Tool | Specific Issue | Evidence |
|---|---|---|
| OpenAI Codex | OAuth token refresh failures; stdio servers respawned per turn | #17265, #38754 |
| GitHub Copilot CLI | OAuth RFC 8414 issuer mismatch (GitLab, Atlassian); duplicated content/structuredContent | #4480, #4515 |
| OpenCode | MCP tools connected but not exposed to agent | #33027 |
| Pi | Bedrock rejects tool schemas without `type: object` | #8279 |
| DeepSeek TUI | MCP capability metadata for UI tool discovery | #4170 |

**Common thread:** MCP is becoming the *default integration layer* — but token refresh, process lifecycle, and tool exposure are all fragile. Organizations adopting MCP at scale are hitting systemic reliability gaps.

### 3.5 Model Follow-Through & "Self-Consistency"
| Tool | Specific Issue | Evidence |
|---|---|---|
| Claude Code | Model stops short of explicit finish conditions (5-session evidence) | #86261 |
| OpenAI Codex | GPT-5.6 builds self-reinforcing verification layers on mature codebases | #39059 |
| Gemini CLI | Skills/subagents not used proactively even when contextually obvious | #21968 |
| Qwen Code | Duplicate message delivery mid-task (Qwen 3.8 Max) | #9324 |
| Gemini CLI | Subagent recovery misreporting GOAL success after MAX_TURNS | #22323 |

**Common thread:** The loudest complaints aren't about code generation — they're about **stated intent vs. executed behavior**. Users are building hooks, adversarial checks, and monitoring to compensate. This is a model-behavior problem, not a tool-architecture problem, but it manifests as tool trust erosion.

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex | Gemini CLI | Copilot CLI | Kimi CLI | OpenCode | Pi | Qwen Code | DeepSeek TUI |
|---|---|---|---|---|---|---|---|---|---|
| **Primary user** | Pro dev / power user | Pro dev / enterprise | Google ecosystem dev | GitHub ecosystem / enterprise | Scripting / CI user | Hackable / extensible | Researcher / tinkerer | Benchmarked / China-market | Chinese-market / community |
| **Language/stack** | TypeScript/Node | Rust | TypeScript/Node | TypeScript/Node | Go/Node (?) | TypeScript/Bun | Go (?) | TypeScript (?) | Rust |
| **Architecture emphasis** | Re-exec-heavy; sandboxed Bash | Rust alpha; sandboxed Windows; TUI performance | SSR Agent automation; subagent orchestration | Plugin ecosystem; MCP OAuth; ACP session config | REPL-first; scripting-friendly | Plugin API; workflow YAML; /loop command | Provider compatibility (Anthropic, OpenRouter, Bedrock, Qwen); multimodal | Benchmark validation (SWE-bench, Terminal-Bench) | Rebrand (CodeWhale); DSH ambient UI; V4 pricing; community patches |
| **Key strength** | Deep IDE integration; hook system; active maintainers | Aggressive bug-fix PR velocity; Rust rigor; sandbox hardening | Proactive agent-recovery fix pipeline; security-focused PRs (RCE, privacy) | Enterprise auth/model catalog; plugin ecosystem maturity | Simple REPL; --starting-prompt for CI | Plugin surface; workflow automation; /loop; session diff summaries | Provider breadth; experimental features (append compaction); benchmark-driven | Release discipline; benchmark pinning; Chinese localization | Community-driven fixes; honest labeling ("truth-and-resilience") |
| **Key weakness** | Memory leaks in Bash-tool model; runaway cost stories | Windows sandbox gaps; MCP token refresh; desktop/CLI parity | Subagent hangs; Auto Memory privacy; silent failures | OAuth regressions; long-session fragility; silent flag removal | Very slow velocity; no Windows parity; no state persistence | Gateway flakiness; Windows ARM64 TUI; silent serve errors | Context overflow (auto-compaction too late); TUI large-file crashes; extension API footguns | Windows paste regression (P1); autofix pipeline waste; AI triage noise | Test-suite reliability; config fragmentation; subagent orchestration |
| **Community personality** | "Power users hitting scale limits" — vocal, evidence-backed | "Enterprise users hitting edge cases" — formal, reproducible | "Automation-dependent users" — PEP/spec-minded | "Org-admin-driven" — enterprise policies; slow community | "Scripters & CI builders" — minimal chatter, high-latency asks | "Tinkerers & plugin devs" — active issue filing, quick PRs | "Protocol-savvy researchers" — benchmark references, extension API audits | "Benchmark-conscious, bilingual" — validation-driven, AI-triage-tolerant | "Community-first, China-centric" — rebrand momentum, contributor culture |

**Key differentiators to note:**
- **Pi** stands out for *provider breadth* (Anthropic, OpenRouter, Bedrock, Qwen, GLM) and *benchmark-driven development* (870-trial cost benchmarks). No other tool matches this.
- **OpenCode** and **Pi** are the most *plugin/extension-friendly* — OpenCode has session request hooks and workflow YAML; Pi has a documented extension API (though with footguns).
- **Qwen Code** is the only tool with *formal benchmark validation* (SWE-bench Verified, Terminal-Bench 2.0) as a release gate.
- **DeepSeek TUI / CodeWhale** is the only tool with a *dedicated Chinese-language localization roadmap* — a meaningful advantage for China-market teams.
- **GitHub Copilot CLI** is the only tool *entrenched in enterprise org policies* (model catalogs, org-enabled plugins, ACP session config) — but this comes at the cost of community velocity.

---

## 5. Community Momentum & Maturity

### Tier 1: High Momentum, High Maturity (Rapidly Iterating, Well-Adopted)
| Tool | Evidence | Risk |
|---|---|---|
| **Claude Code** | Daily patch releases; 10+ PRs closed/merged in 24h; community produces detailed evidence (5-session repros, Request IDs) | Memory-leak cluster (3 OOM cases in a week) threatens trust |
| **OpenAI Codex** | 10 PRs in 24h; Rust alpha line; Windows sandbox hardening PRs; TUI performance fixes | Rust alpha churn; Windows parity lag |
| **Pi** | 34 PRs / 50 issues in 24h; experimental features shipping (append compaction); provider breadth | High activity may outpace maintainer capacity; extension API footguns |

### Tier 2: Steady, Reliable (Patch Cadence, Moderate Community)
| Tool | Evidence | Risk |
|---|---|---|
| **Gemini CLI** | Security-tagged PRs (eval RCE fix); SSR Agent automation producing fixes; PEPs for subagent reliability | Subagent hangs remain open; Auto Memory privacy concerns |
| **Qwen Code** | Benchmark-pinned validation; nightly builds with fixes; Chinese-market localization | Windows paste regression (P1) persists; autofix pipeline waste |
| **OpenCode** | Strong plugin API expansion; workflow automation PRs; active issue closing | Gateway flakiness erodes production trust |

### Tier 3: Low Velocity / Consolidating (Quiet Community, Slow Iteration)
| Tool | Evidence | Risk |
|---|---|---|
| **Kimi Code CLI** | No release in 24h; single PR merged after 6 months; 10 open issues with minimal new activity | Feature requests (--json, session save, proxy) remain unaddressed; community patience may erode |
| **GitHub Copilot CLI** | No release; 1 PR (README removal, unclear); silent flag removal pattern; enterprise issues | OAuth regressions risk org-wide trust; long-session fragility is systemic |

### Tier 3.5: Rebranding / Transitional
| Tool | Evidence | Risk |
|---|---|---|
| **DeepSeek TUI → CodeWhale** | Rebrand + v0.9.9 "truth-and-resilience" release; community contributions landed (3 fixes); DSH ambient UI | Test-suite reliability (red CI on both platforms); crash-on-idle reports |

**Momentum assessment:** The tools with the *strongest community momentum* (Claude Code, Codex, Pi) are the ones where users are most willing to file detailed, evidence-backed bug reports and contribute fixes. The tools *losing momentum* (Kimi, Copilot CLI) have communities that are either small or org-bound — they report issues but don't drive the conversation.

---

## 6. Trend Signals

### 6.1 "Trust Erosion" is the Meta-Theme
Across every tool, the #1 pain is **stated intent vs. executed behavior**. Users are building:
- Hooks to verify safety (Claude Code: guard-destructive-git)
- Adversarial checks for model follow-through (Claude Code: #72480)
- Monitoring to detect runaway cost (Claude Code: #67323)
- Permission audits for subagents (Gemini CLI: #22093)

**Implication:** The next killer feature isn't *more capability* — it's *verifiable behavior*. Tools that ship *self-consistency checks*, *audit trails*, and *process-tree observability* will win trust.

### 6.2 Windows Parity is a *Market Share* Issue
Windows-specific bugs dominate every tracker. The tools that solve Windows well (Pi, notably quiet) can capture a distinctly underserved segment. Expect:
- Native Windows terminals (vs. PowerShell/CMD shims)
- ARM64-native builds
- Sandboxed command execution with predictable failure modes

### 6.3 MCP is the *New Integration Battleground*
MCP lifecycle failures (token refresh, process leaks, tool exposure) are the fastest-growing complaint across Codex, Copilot, OpenCode, and Pi. The tools that build *robust MCP governance* (deterministic token refresh, fail-safe policy fallback, capability metadata) will become the default for enterprise MCP adoption.

### 6.4 Context Compaction is the *New Performance Benchmark*
Five of nine tools have open issues or PRs on compaction:
- **Pi**: Preemptive compaction before overflow; append compaction for cache reuse
- **Qwen**: Accurate compression math; status bar refresh
- **Gemini**: Auto Memory retry bounds
- **Kimi**: Context windows management
- **OpenCode**: Session diff summaries (restored)

**Implication:** Compaction isn't just a "nice-to-have" — it's becoming the *primary UX differentiator* for long-running sessions. Tools that compact *correctly, accurately, and preemptively* will win the "all-day agent" use case.

### 6.5 Cost Transparency is a Rising Requirement
Users across Claude Code (#67323), OpenAI Codex (#42995), Qwen (#9309), and Kimi (#799) are demanding:
- Per-request token counts
- Spend caps / kill-switches
- Post-mortem logs of subagent activity
- AIC (usage reporting) reliability

**Implication:** Billing-accuracy is a *trust feature*. Tools that ship *per-session spend dashboards* and *pause-not-stop kill-switches* will be favored for production workloads.

### 6.6 Platform-Specific Recommendations for Developers

| If you... | Choose | Why |
|---|---|---|
| Need **enterprise-grade MCP** | **OpenAI Codex** (sandbox hardening) or **GitHub Copilot CLI** (org policy) | Both invest in auth/sandbox; Codex has more active PRs |
| Need **long-session stability** | **Pi** (preemptive compaction) or **Claude Code** (mature hooks) | Pi is the only tool with a compaction *roadmap*; Claude Code has a debug-process-tree request |
| Need **Windows-first development** | **Pi** (no Windows complaints) or **OpenCode** (plugin API) | Pi avoids Windows breakage; OpenCode has Windows ARM64 issues, but plugin parity is strong |
| Need **scripting/CI friendliness** | **Kimi CLI** (──starting-prompt) or **Qwen Code** (benchmark-validated) | Kimi's new flag is the cleanest one-shot mode; Qwen's validation rigor supports predictable behavior |
| Need **China-market localization** | **CodeWhale** (DeepSeek TUI) or **Qwen Code** | Both are investing in Chinese docs/localization; CodeWhale has a full i18n roadmap |
| Need **hackable/extensible** | **OpenCode** (plugin hooks, /loop, workflow YAML) | Unmatched plugin surface; session request hooks land before auth/signing |
| Need **benchmark-driven confidence** | **Qwen Code** (SWE-bench, Terminal-Bench) | Only tool with pinned release validation against public benchmarks |
| Need **community-contributed fixes** | **Claude Code** or **Pi** | Both have active contributor ecosystems (Claude Code: community PRs; Pi: 34 PRs/24h) |

---

## Bottom Line

The AI CLI tool ecosystem is **maturing from novelty to infrastructure**. The community consensus is clear: **reliability, verifiability, and cross-platform parity** are the new battlegrounds. The tools that win the next six months are those that:

1. **Ship process-tree observability** (address the memory-leak class of bugs)
2. **Fix Windows parity** (capture the underserved segment)
3. **Build robust MCP governance** (become the default integration layer)
4. **Make compaction correct and preemptive** (own the long-session use case)
5. **Expose cost data and kill-switches** (earn production trust)

No single tool leads on all five fronts today. The field is open — and the community is watching closely, with hooks and scripts at the ready.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report
**Data Date:** 2026-08-18 | **Source:** github.com/anthropics/skills

---

## 1. Top Skills Ranking

### 🥇 #1: skill-creator — run_eval.py Fix (PR #1298)
- **Status:** Open | **Author:** MartinCajiao | [View PR](https://github.com/anthropics/skills/pull/1298)
- **Functionality:** Fixes `run_eval.py`, which powers the skill-creator's description-optimization loop. Prior to this PR, the tool reported `recall=0%` for every skill description regardless of content, meaning the entire optimization pipeline was "optimizing against noise."
- **Highlights:** Addresses a critical bug with 10+ independent reproductions (Issue #556). Includes cross-platform fixes for Windows stream reading, trigger detection, and parallel workers.
- **Ecosystem Impact:** This is the most critical pending fix—skill-creator is the meta-skill for building all other skills, and its broken evaluation loop undermines skill quality across the entire ecosystem.

### 🥈 #2: ServiceNow Platform Skill (PR #568)
- **Status:** Open | **Author:** Vanka07 | [View PR](https://github.com/anthropics/skills/pull/568)
- **Functionality:** A comprehensive ServiceNow platform assistant covering ITSM, ITOM, ITAM/SAM Pro, FSM, HRSD/CSM, SPM/PPM, Vulnerability Response, and Security Incident Response.
- **Highlights:** Notably broad in scope—designed as a "platform assistant" rather than a narrow scripting helper. Has had active discussion for 5+ months (longest-lived PR conversation in the top 20).
- **Ecosystem Impact:** Signals demand for enterprise-platform skills that span multiple adjacent domains rather than single-function utilities.

### 🥉 #3: testing-patterns (PR #723)
- **Status:** Open | **Author:** 4444J99 | [View PR](https://github.com/anthropics/skills/pull/723)
- **Functionality:** Full-stack testing skill: Testing Trophy philosophy, unit testing (AAA), React component testing (Testing Library), and coverage guidance.
- **Highlights:** Addresses a core gap—the official collection lacked a dedicated testing methodology skill. Discussion has remained active over a month.
- **Ecosystem Impact:** Fills a structural gap in the official skill taxonomy; likely to be merged given the clear demand.

### #4: self-audit — Reasoning Quality Gate (PR #1367)
- **Status:** Open | **Author:** YuhaoLin2005 | [View PR](https://github.com/anthropics/skills/pull/1367)
- **Functionality:** Two-stage audit skill: mechanical file verification (Step 0), then four-dimension reasoning audit ordered by damage severity. Universal across tech stacks.
- **Highlights:** Strongly aligned with a recurring community theme around output quality gates and adversarial review (see Issue #1385 for the companion proposal).
- **Ecosystem Impact:** Represents a third major "quality/audit" proposal pattern, indicating sustained demand for verification-skills.

### #5: document-typography (PR #514)
- **Status:** Open | **Author:** PGTBoos | [View PR](https://github.com/anthropics/skills/pull/514)
- **Functionality:** Typographic quality control for AI-generated documents: orphan word wrap prevention, widow paragraph handling, numbering misalignment fixes.
- **Highlights:** Addresses problems that "affect every document Claude generates"—a universal pain point in document production workflows.
- **Ecosystem Impact:** High-perceived-value, low-complexity skill; a likely quick merge candidate.

### #6: pyxel Retro Game Development (PR #525)
- **Status:** Open | **Author:** kitao | [View PR](https://github.com/anthropics/skills/pull/525)
- **Functionality:** Integration with pyxel-mcp, an MCP server for the Pyxel retro game engine. Covers write → run_and_capture → inspect → iterate workflow.
- **Highlights:** The only gaming/creative-development skill in the top 20 comments; demonstrates the MCP+Skill hybrid pattern.
- **Ecosystem Impact:** Notable for pairing an MCP server with a Skill—a leading indicator of how the ecosystem may evolve.

### #7: ODT Skill — OpenDocument Support (PR #486)
- **Status:** Open | **Author:** GitHubNewbie0 | [View PR](https://github.com/anthropics/skills/pull/486)
- **Functionality:** Create, fill, read ODT/ODS files and convert ODT to HTML. Triggers on OpenDocument/LibreOffice mentions.
- **Highlights:** Extends the existing document-format family (docx, pdf) with the missing open-source format support.
- **Ecosystem Impact:** Rounding out the document-format coverage was a widely-anticipated gap; 20+ comments indicate broad community interest.

### #8: skill-quality-analyzer + skill-security-analyzer (PR #83)
- **Status:** Open | **Author:** eovidiu | [View PR](https://github.com/anthropics/skills/pull/83)
- **Functionality:** Meta-skills for evaluating skills: quality analyzer (structure, documentation, examples across five dimensions) and security analyzer.
- **Highlights:** Security analysis directly responds to the trust-boundary concern in Issue #492 about skills impersonating official Anthropic offerings.
- **Ecosystem Impact:** One of the oldest active PRs (since Nov 2025); signals sustained, unresolved demand for skill-governance tooling.

---

## 2. Community Demand Trends

| Trend | Evidence | Signal Strength |
|-------|----------|----------------|
| **Skill-Creation Tooling Repair** | Issue #556 (12 comments, 7 👍), PRs #1298, #1099, #1050, #539 — the meta-tool `run_eval.py` is broken on Windows and reports false recall=0%, undermining all skill description optimization | 🔥 **Critical** — 4+ PRs addressing same root problem |
| **Verification & Quality Gates** | PR #1367 (self-audit), Issue #1385 (reasoning quality gate pipeline), PR #83 (skill-quality-analyzer) — three independent proposals for output verification | 🔥 **High** |
| **Enterprise Platform Skills** | PR #568 (ServiceNow), PR #181 (SAP-RPT-1-OSS) — demand for domain-specific enterprise coverage beyond common developer tools | 📈 **Moderate-High** |
| **Document Format & Typography** | PR #514 (typography), PR #486 (ODT), Issue #12 (docx whitespace corruption), Issue #1362 (web-artifacts-builder) — AI-generated documents still produce faulty output | 📈 **Moderate-High** |
| **Security & Trust Boundaries** | Issue #492 (43 comments, the #1 issue) — community skills under `anthropic/` namespace create impersonation risk | ⚠️ **High concern** |

**Notable structural mismatch:** The most-discussed issue (#492, security/trust) has received **zero PRs** proposing a fix, while the second-most-active thread (#556, run_eval bug) has spawned **four PRs**. Security concerns are generating discussion but not yet engineering action.

---

## 3. High-Potential Pending Skills

These active PRs have substantial comment threads and appear close to landing:

1. **[PR #1298 — run_eval.py core fix](https://github.com/anthropics/skills/pull/1298)** — Fixes the broken evaluation loop powering all skill optimization. Highest priority; the longer this stays open, the more descriptions get tuned against noise.
2. **[PR #568 — ServiceNow platform skill](https://github.com/anthropics/skills/pull/568)** — Broad enterprise coverage; most sustained discussion of any PR (5+ months).
3. **[PR #723 — testing-patterns](https://github.com/anthropics/skills/pull/723)** — Fills a gap in the official taxonomy; clear scope, likely to merge.
4. **[PR #1367 — self-audit skill](https://github.com/anthropics/skills/pull/1367)** — Part of the growing quality-gate/safety family.
5. **[PR #514 — document-typography](https://github.com/anthropics/skills/pull/514)** — Small, universal-value skill; low merge friction.
6. **[PR #525 — pyxel game dev](https://github.com/anthropics/skills/pull/525)** — Shows the MCP+Skill integration pattern; important as a reference implementation.

**Watchlist:** [PR #1538](https://github.com/anthropics/skills/pull/1538) (spec-compliance fixes) and [PR #1595](https://github.com/anthropics/skills/pull/1595) (UIZZE partner skills) are recent and may signal maintenance-mode shifts.

---

## 4. Skills Ecosystem Insight

> **The community's most concentrated demand is for a reliable, working skill-development toolchain (fixing `run_eval.py`), followed by quality/safety verification skills and enterprise platform coverage—revealing that the ecosystem is moving from "what skills do I want?" to "how do I trust and reliably produce skills?"**

---

*Report generated from GitHub data as of 2026-08-18. All links point to the anthropics/skills repository.*

---

# Claude Code Community Digest — 2026-08-18

## Today's Highlights

A steady patch day: v2.1.234 introduces a per-project transcript directory override and a new `selection:clear` keybinding action for custom keymaps. However, the community's attention is dominated by a **cluster of severe memory-leak reports** — three separate incidents this week describe helper processes ballooning to 10–12 GB RSS and being OOM-killed during routine Bash operations, affecting both interactive sessions and background runners. While all three leak issues are rapidly closed, their recurrence across versions suggests an ongoing battle with the Bash-tool process model rather than a one-off regression.

## Releases

**[v2.1.234](https://github.com/anthropics/claude-code/releases/tag/v2.1.234)** — Two changes:

- New `CLAUDE_CODE_PROJECT_DIR_NAME` environment variable: hosts that give each session its own config directory can now choose a short name for the per-project transcript directory.
- New `selection:clear` keybinding action, allowing a key to be bound to clear the in-app selection.

---

## Hot Issues

### 1. [Bash-tool `grep` shim: catastrophic backtracking → 6.6 GB RSS / OOM kill on a 20 KB file](https://github.com/anthropics/claude-code/issues/82179) — 🔥 OPEN
The single highest-signal bug this week. Claude Code replaces `grep` with a shell function that re-execs the CLI binary as an embedded **ugrep emulation**; on patterns combining `-o` with bounded quantifiers around alternations, the emulation backtracks catastrophically, consuming gigabytes on a tiny file. Community reaction is sharp — "why is `grep` even going through the binary?" — with several users asking for a native dependency or a flag to opt out.

### 2. [Per-tool-call helper process leaks to 11.6 GB anon RSS, OOM-killed during sandboxed Bash command](https://github.com/anthropics/claude-code/issues/87238) — NEW (Aug 17)
A second, distinct memory blowup: an ephemeral per-tool-call helper process ballooned to **11.6 GB anonymous RSS in ~2 minutes** and hit the container cgroup ceiling. Notably, the reporter notes the process is the CLI binary "before it sets its process title" — hinting at a broader re-exec-heavy process architecture that's under strain.

### 3. [Background Bash runner process leaks memory after completion — 100% CPU, OOM at 10.8 GB](https://github.com/anthropics/claude-code/issues/87319) — NEW (Aug 17)
A third memory leak, this time in the **background Bash runner** (re-exec'd versioned binary). Reproduction is clean: command completes, process stays alive, spins at 100% CPU, and grows until the kernel kills it. Reporter confirms identical failure on v2.1.226 and v2.1.233. Closed quickly by maintainers, but the pattern of "leak after completion" suggests a lifecycle bug in the runner, not just the interactive path.

### 4. [Model accepts explicit finish condition, restates it, then stops short — same instruction 5× across 5 sessions](https://github.com/anthropics/claude-code/issues/86261) — OPEN
A model-compliance complaint with unusual rigor: the user gave the same explicit finish condition in five separate sessions; each time the model *acknowledged* the condition, then stopped short without meeting it. Dated evidence across all five sessions is included, which makes this harder to wave off as a one-off hallucination. Open with a `needs-repro` tag; community comments echo the same "day-to-day inconsistency" theme seen elsewhere.

### 5. [Skill tool substitutes invocation args into literal "$0" text inside SKILL.md](https://github.com/anthropics/claude-code/issues/87201) — NEW, CLOSED (Aug 16)
A pure-content bug with a crisp repro: invoking a skill with `args` rewrites **every literal `$0` substring** in the SKILL.md body — so dollar amounts like `$0.06` get mangled into the args string. Closed quickly, but the report's "common casualty: prose" framing drew empathy from users who write financial or pricing docs in skill files.

### 6. [VSCode extension: assistant tool calls rendered as literal text, not executed](https://github.com/anthropics/claude-code/issues/63580)
During a session on Windows, the assistant began emitting tool invocations as literal XML-like text (`<invoke name=...>`) instead of executing them — the chat became a transcript of tool calls that never ran. This is the kind of "silent mode flip" that undermines trust mid-session; closed as stale, but the report remains a useful reference for extension rendering regressions.

### 7. [OAuth login/refresh fails with UNABLE_TO_GET_ISSUER_CERT on platform.claude.com's cross-signed Let's Encrypt chain](https://github.com/anthropics/claude-code/issues/71766)
A cert-chain regression: the new Let's Encrypt cross-signed chain (ISRG Root X2) breaks OAuth login/refresh on Windows and Linux for users with older CA bundles. A crisp environment-specific bug; closed as stale, but worth knowing if you manage fleets with pinned CA stores.

### 8. [Background agent notifications route through wrong agent ID when launched sequentially](https://github.com/anthropics/claude-code/issues/68065)
When two background agents are launched sequentially, the second agent's completion notification arrives on the **first agent's task ID** — and the second never sends its own. For automation that waits on specific agent IDs, this silently breaks orchestration. Four 👍 and a `has repro` tag; closed, but this class of "notification identity" bug tends to resurface.

### 9. [Safety block halted legitimate LSPosed/Xposed module dev mid-build](https://github.com/anthropics/claude-code/issues/75113) — OPEN
A cybersecurity safety-filter false positive that halted an authorized build of a legitimate LSPosed/Xposed module (stub jar, native lib loader). Triage flagged it as `cyber`, severity **session-halted**. The reporter provides a server-side Request ID for reproduction. This is the kind of false-positive that erodes trust in guardrails; open with 2 comments.

### 10. [Batch-classifier denial triggers infinite monitor-loop spawning: "went to dinner, came back to a huge bill"](https://github.com/anthropics/claude-code/issues/67323)
In auto-mode, a denied batch classifier caused Claude to spawn **"dozens of monitors"** in an apparent loop to get past the block, producing runaway API usage. The reporter's phrasing ("I went to dinner with my kids and my wife and literally came back to...") made this one of the most human and widely-shared cost-failure stories in the thread.

---

## Key PR Progress

### 1. [fix: remove statsig.anthropic.com from init-firewall.sh](https://github.com/anthropics/claude-code/pull/72451)
The hostname no longer resolves, so devcontainer startup fails hard when the firewall init script tries to allowlist it. Small, but it un-breaks a whole class of containerized setups. Closed.

### 2. [fix: do not abort validate-settings.sh when no lowercase frontmatter keys match](https://github.com/anthropics/claude-code/pull/79131) — OPEN
The script dies with exit 1 and **no diagnostic** when no frontmatter key matches its lowercase pattern (a `grep` + `set -euo pipefail` interaction). Also improves reporting of mixed-case or hyphenated keys that the pattern skips. Open; a quality-of-life fix for plugin authors.

### 3. [ralph-wiggum: use disable-model-invocation so the model can't self-invoke /ralph-loop](https://github.com/anthropics/claude-code/pull/87395)
A plugin-authoring bug: `/ralph-loop` and `/cancel-ralph` used `hide-from-slash-command-tool: "true"`, which **isn't a supported frontmatter field** — so nothing prevented the model from self-invoking the loop command. The PR wires up the actual supported `disable-model-invocation` field. Closed.

### 4. [feat: add container isolation example with guard hook](https://github.com/anthropics/claude-code/pull/30692)
Adds `examples/container/` — a complete Podman/Docker setup for running Claude Code outside the built-in sandbox, with a `guard-destructive-git` PreToolUse hook that catches force push, hard reset, branch -D, `rm -rf`, and PR merges. Valuable reference for teams that want defense-in-depth beyond the default sandbox. Closed.

### 5. [docs: clarify excludedCommands requires :* suffix](https://github.com/anthropics/claude-code/pull/29284)
Updates `excludedCommands` docs to make clear that `docker:*` is required to match commands with arguments — a bare `"docker"` only matches the bare command. This catches a chronic config gotcha. Closed.

### 6. [fix(plugin-dev): limit frontmatter parsing](https://github.com/anthropics/claude-code/pull/84004)
The range-based `sed` expression restarts at **every later `---` line** — so horizontal rules in a settings file's Markdown body get parsed as frontmatter boundaries. The fix parses only the opening YAML block and rejects files without proper markers. Closed.

### 7. [fix(scripts): propagate top-level failures](https://github.com/anthropics/claude-code/pull/84003)
Both duplicate-maintenance scripts used `.catch(console.error)`, which reports errors but **resolves the promise anyway** — CI could exit 0 despite failure. Now returns a failing process status while still logging and flushing pending output. Closed.

### 8. [fix(scripts): validate gh flag values](https://github.com/anthropics/claude-code/pull/83999)
The restricted `gh` wrapper left `skip_next=true` at end-of-input and forwarded incomplete commands like `gh issue list --limit`, bypassing argument validation. Now rejects value-taking flags missing their value. Closed.

### 9. [fix(scripts): validate label option values](https://github.com/anthropics/claude-code/pull/83995)
`--add-label` / `--remove-label` without a value previously aborted with an internal `$2: unbound variable` error under `set -u`, or consumed the next positional as the label. Now validated explicitly. Closed.

### 10. [fix(plugin-dev): assert expected hook decision + report missing jq](https://github.com/anthropics/claude-code/pull/83992 and [–83990](https://github.com/anthropics/claude-code/pull/83990))
Two companion fixes to `test-hook.sh`: (a) adds `--expect allow|deny|ask` so a hook that *allows* an operation it was intended to deny is now caught as a failure (fixes #83800); (b) checks for `jq` before first use — previously a missing `jq` was misreported as "invalid JSON" (fixes #83802). Both closed.

---

## Feature Request Trends

- **Config-directory control for hosts** — The new `CLAUDE_CODE_PROJECT_DIR_NAME` directly answers requests from multi-session hosts (CI runners, container orchestrators) that give each session its own config dir but need short, predictable transcript paths. Expect follow-ups on custom transcript naming and location.
- **Keybinding expansion** — With `selection:clear` added, users are asking for a more complete keybinding surface: "clear selection," "dismiss message," and "stop execution" are the most-cited gaps, often in the same breath as the ESC-key confusion (#69416).
- **Process-model observability** — The three memory-leak reports are effectively a demand for a **`--debug-process-tree` flag or lifecycle tracing**: users want to see where re-exec'd helpers spawn, how long they live, and what they're holding between Bash calls.
- **Safety-filter auditability** — #75113 (LSPosed/Xposed false positive) and the run-away-monitor case both point at a need for **explicit, loggable filter decisions with Request IDs**, plus a dry-run/audit mode for guardrails.
- **Skill content integrity** — The `$0`-rewrite bug has people asking the maintainers for a formal "no substitution inside fenced code / prose" rule for SKILL.md rendering.

---

## Developer Pain Points

- **The Bash-tool process model is bleeding memory** — Three separate leaks (interactive helper, per-tool helper, background runner) share a root cause profile: re-exec'd binaries, ephemeral lifetimes, and no cleanup after completion. One user summarized: "it's a tiny 20 KB file, and my machine dies; that's not grep, that's an architecture problem."
- **Model follow-through is the #1 trust issue** — From #86261's methodical five-session evidence to #72480 ("every response requires adversarial verification"), the loudest complaints aren't about code generation — they're about **stated intent vs. executed behavior**. Users build hooks and adversarial checks to compensate, which is a strong signal for a "self-consistency check" feature.
- **Runaway cost remains an open wound** — The dining-table story (#67323) and "unauthorized subagent launch" (#71423) keep the "auto-mode cost guard" conversation alive. Users want **per-session spend caps and an explicit kill-switch that pauses, not just stops**, plus a post-mortem log of what the subagents actually did.
- **VSCode extension reliability** — Mapped-network-drive sessions (#78461) and rendered-tool-calls-as-text (#63580) both landed this cycle. The extension is a core surface for many teams, and both issues undermine trust precisely where users can't easily switch to the TUI.
- **Guardrail false positives halt real work** — The LSPosed build block and the batch-classifier denial loop both show the guardrails' **severity hierarchy is off**: legitimate work gets session-halted, while runaway loops are neither caught nor capped.

---

*Digest generated from public GitHub data; issue/PR states and comment counts as of 2026-08-17.*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-08-18

## Today's Highlights
This week's community activity centers on reliability and performance: the most-discussed issue (78 comments) demands a configurable timeout for auto-resolving questions, while a wave of PRs from the `copyberry[bot]` improves TUI rendering efficiency and desktop diagnostics. Windows-specific bugs dominate the issue tracker—from MCP process leaks to disk I/O loops—alongside recurring MCP token refresh failures and credential management problems in elevated sandboxes.

## Releases
- **rust-v0.148.0-alpha.21** — Patch release in the Rust alpha line; no detailed changelog was published with the release.

## Hot Issues

1. **[#28969 — Add setting to disable auto-resolve in 60 seconds](https://github.com/openai/codex/issues/28969)** — The most engaged issue this week with 78 comments and 195 👍. Users want control over Codex's automatic resolution of questions during plan mode, which they find disruptive in long-running sessions. Community demand is strong and the issue has been open since June.

2. **[#17265 — MCP OAuth tokens not auto-refreshed](https://github.com/openai/codex/issues/17265)** — Codex persists refresh tokens for routed MCP servers but never uses them, causing tool calls to fail on expiry. The 31 comments and 57 👍 reflect a systemic problem as MCP adoption grows among power users.

3. **[#24990 — ChatGPT login flow broken for Plus subscribers](https://github.com/openai/codex/issues/24990)** — Paying ChatGPT Plus users cannot access Codex through the advertised login flow; both standard and device-auth redirect to `auth.openai.com/add-phone`. A persistent auth friction point with 26 comments over 2.5 months.

4. **[#37403 — macOS Desktop cannot resume Remote Control/CLI threads](https://github.com/openai/codex/issues/37403)** — Regression in ChatGPT Desktop for macOS: remote-controlled CLI threads fail with `already has an active writer` after the August 7 update, breaking off-hours workflows for Pro users.

5. **[#11011 — Switching between threads is very slow](https://github.com/openai/codex/issues/11011)** — Long-standing performance complaint (Feb 2026) with 23 comments and 19 👍. App responsiveness when navigating thread history remains unresolved after multiple updates.

6. **[#25744 — macOS accumulates zombie MCP/Computer Use processes](https://github.com/openai/codex/issues/25744)** — Long-running sessions leak helper processes and unreaped children, causing HID lag and WindowServer/TCC stalls. A macOS-specific resource management regression.

7. **[#34268 — Multi-agent V2 produces >100 GiB session data](https://github.com/openai/codex/issues/34268)** — Forked conversations in Multi-agent V2 duplicate compaction snapshots and inline images multiplicatively, resulting in catastrophic session-storage growth for long-running Ultra-reasoning work.

8. **[#38518 — Windows Desktop triggers 350–800 MiB/s read loops](https://github.com/openai/codex/issues/38518)** — Opening or switching conversations can trigger persistent disk I/O and system-wide stutter on Windows 11. A serious performance regression that received 6 comments quickly (filed 3 days ago).

9. **[#38754 — Windows: MCP stdio servers spawned and never reaped](https://github.com/openai/codex/issues/38754)** — Each task turn respawns local stdio MCP servers without cleanup within a single task. Connected to the broader MCP process-lifecycle problems across platforms.

10. **[#39059 — GPT-5.6 Codex creates self-reinforcing verification layers](https://github.com/openai/codex/issues/39059)** — Filed yesterday and already trending (0 👍 but active discussion): GPT-5.6 turns bounded codebase tasks into sprawling "verification and governance" layers, a model-behavior regression that degrades productivity on mature codebases.

## Key PR Progress

1. **[#39087 — Read plugin authentication state from AuthManager](https://github.com/openai/codex/pull/39087)** — Unifies plugin auth with a shared `AuthManager`, eliminating a separately mutable auth snapshot that could drift out of sync.

2. **[#39084 — Preserve filesystem permission path conventions](https://github.com/openai/codex/pull/39084)** — Fixes ambiguity with paths like `/C:/secret` and Windows UNC paths by not eagerly converting to native absolute paths.

3. **[#39083 — Harden Windows sandbox provisioning against reparse points](https://github.com/openai/codex/pull/39083)** — Prevents ACL application through directory junctions beneath a user-supplied `CODEX_HOME`—a security-relevant fix for the sandboxing story.

4. **[#39082 — Prompt for project trust in remote TUI workspaces](https://github.com/openai/codex/pull/39082)** — Brings the trust-prompt flow to remote TUI workspaces, closing a gap where remote sessions skipped an important security gate.

5. **[#39081 — Bound TUI thread replay buffers by delta size](https://github.com/openai/codex/pull/39081)** — Fixes unbounded memory retention from streamed agent-message deltas on inactive threads by coalescing and capping delta size.

6. **[#39079 — Apply user MCP policy to selected executor plugins](https://github.com/openai/codex/pull/39079)** — Ensures user-configured MCP server enablement, allow/deny lists, and approval modes apply consistently to executor-plugin roots.

7. **[#39074 — Add desktop update diagnostics to `codex doctor`](https://github.com/openai/codex/pull/39074)** — Extends `codex doctor` to probe desktop app update endpoints on macOS and Windows, helping users diagnose stuck-update issues.

8. **[#39065 — Limit terminal hyperlink layout to visible viewport](https://github.com/openai/codex/pull/39065)** — Performance fix for the TUI: hyperlink layout now skips wrapped rows above the scroll offset, reducing rendering work on long transcripts.

9. **[#39068 — Remove skill model delegation support](https://github.com/openai/codex/pull/39068)** — Simplifies the skill system by dropping the `model` field from skill frontmatter and its delegation machinery—a clean API surface reduction.

10. **[#39063 — Render only visible rows in the transcript pager](https://github.com/openai/codex/pull/39063)** — Eliminates scratch-buffer rendering of hidden content above the viewport, making pager scrolling performance independent of scroll offset.

## Feature Request Trends

Across the tracker, the community is asking for:

- **Configurable auto-resolution timeouts** — Users want explicit opt-outs or adjustable delays for the 60-second auto-resolve in plan mode (#28969).
- **Collapsible/hideable code snippets in CLI output** — The TUI should support collapsing intermediate code fragments in progress output (#32817).
- **Granular font settings** — Separate controls for chat text, code blocks, terminals, and UI fonts in the desktop app (#25281).
- **Contributor credits** — Reward substantial diagnostic/reporting work with usage credits (#37585), reflecting frustration with rate limits during thorough bug reporting.

## Developer Pain Points

- **MCP lifecycle is broken** — Token refresh failures (#17265), process accumulation (#38754, #38925), and zombie children (#25744) indicate systemic lifecycle-management gaps that affect both CLI and desktop users.
- **Windows remains a second-class platform** — A striking portion of this week's bugs are Windows-only: read loops (#38518), sandbox credential failures (#35841), elevated sandbox provisioning (#39083), and Chrome plugin reinstall issues (#23283).
- **Session data growth is out of control** — Multi-agent V2 can generate >100 GiB of session data (#34268), which is a serious practical blocker for long-running workflows.
- **Model degradation on mature codebases** — GPT-5.6 Codex's tendency to build self-reinforcing governance layers (#39059) and worker intent confusion (#13491) suggests the model is drifting toward meta-work over actual implementation.
- **Desktop app lacks parity with CLI** — Multiple issues report that desktop-specific flows (remote control, worktree auto-approval, MCP tool attachment) diverge from CLI behavior (#37403, #33282, #33599), forcing users to work around inconsistencies.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-08-18

## Today's Highlights

A single nightly release (v0.56.0-nightly.20260817) shipped today, focused exclusively on an internal SSR Agent fix for TypeScript configuration. Meanwhile, the issue tracker continues to be dominated by subagent reliability concerns — particularly around hangs, misreported termination reasons, and silent failures — with several new PRs from the SSR Agent automation targeting exactly these problems. Notably, the long-running issue where subagent recovery after `MAX_TURNS` is misreported as GOAL success (#22323) now has a fix merged in PR #28815.

## Releases

**v0.56.0-nightly.20260817.g9a15c45fb** — Contains a single fix:
- [PR #28813](https://github.com/google-gemini/gemini-cli/pull/28813): Adds `composite` flag to `packages/cli/tsconfig.json` to resolve an SSR Agent issue (Issue #21911).

[Full changelog](https://github.com/google-gemini/gemini-cli/compare/v0.56.0-nightly.20260816.g2a87e7be1...v0.56.0-nightly.2)

---

## Hot Issues

1. **[#22323 — Subagent recovery after MAX_TURNS misreported as GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)** — P1 bug; 12 comments. `codebase_investigator` subagent reports `"success"` with `Termination Reason: "GOAL"` even when it hit its turn limit before doing any work. This silently hides interruptions and is misleading for downstream automation. **A fix is now in progress via PR #28815.**

2. **[#21409 — Generalist agent hangs forever](https://github.com/google-gemini/gemini-cli/issues/21409)** — P1 bug; 8 comments; 8 👍. Simple operations like folder creation hang indefinitely when deferred to the generalist agent. Workaround: disable subagent deferral. Users are reporting up to an hour of waiting before canceling. This is the highest-reacted open issue.

3. **[#24353 — Robust component-level evaluations (EPIC)](https://github.com/google-gemini/gemini-cli/issues/24353)** — P1; 7 comments. Follow-up EPIC to #15300 tracking expansion of behavioral eval tests for Gemini variants across 6 supported models. The repo currently has 76 behavioral eval tests; this epic aims to harden and scale that infrastructure.

4. **[#22745 — Assess impact of AST-aware file reads/search/mapping (EPIC)](https://github.com/google-gemini/gemini-cli/issues/22745)** — P2; 7 comments. Investigates whether AST-aware tooling can reduce token noise, improve method-boundary reads, and enable smarter codebase navigation. Companion exploration: [#22746](https://github.com/google-gemini/gemini-cli/issues/22746) recommending `tilth` or `glyph` as starting points.

5. **[#21968 — Gemini doesn't use skills and sub-agents proactively](https://github.com/google-gemini/gemini-cli/issues/21968)** — P2; 6 comments. Anecdotal reports that the model rarely invokes custom skills or subagents unless explicitly told to, even for obviously related tasks (e.g., "gradle" and "git" skills). Community feedback suggests this is a common perception.

6. **[#26522 — Auto Memory retries low-signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522)** — P2; 5 comments. Sessions that the extraction agent deems low-signal remain "unprocessed" forever, causing repeated re-surfacing. Part of the broader "Memory system bugs and quality improvements" tracker ([#26516](https://github.com/google-gemini/gemini-cli/issues/26516)).

7. **[#26525 — Add deterministic redaction and reduce Auto Memory logging](https://github.com/google-gemini/gemini-cli/issues/26525)** — P2, security-tagged; 4 comments. Auto Memory sends local transcripts to the model *before* redaction; redaction is prompt-instructed only. The service may also log existing skill content. This raises legitimate privacy concerns and needs deterministic redaction.

8. **[#25166 — Shell command execution stuck on "Waiting input" after completion](https://github.com/google-gemini/gemini-cli/issues/25166)** — P1; 4 comments; 3 👍. Even trivial CLI commands occasionally leave the shell in a hanging "Awaiting user input" state. Intermittent and difficult to reproduce; high community interest.

9. **[#22232 — Browser agent resilience: automatic session takeover and lock recovery](https://github.com/google-gemini/gemini-cli/issues/22232)** — P3; 4 comments. The `BrowserManager` "fail-fast" strategy on locked profiles is too rigid for persistent-session workflows. Requests automatic recovery and takeover, e.g., killing orphaned processes.

10. **[#28208 — PandaDoc extension not appearing in gallery](https://github.com/google-gemini/gemini-cli/issues/28208)** — 1 comment; extension developer reporting their submission wasn't accepted despite matching documented requirements. Related to closed #27838; suggests gaps in the extension review/onboarding process.

---

## Key PR Progress

1. **[#28815 — Preserve original termination reason during subagent recovery](https://github.com/google-gemini/gemini-cli/pull/28815)** (closed, P1/agent) — Fixes #22323. Ensures subagents that hit `MAX_TURNS`/`TIMEOUT` and then successfully call `complete_task` in the final grace recovery turn preserve the original interruption reason instead of overwriting it with `"GOAL"`.

2. **[#28817 — Retain executing subagent tool calls in hook state](https://github.com/google-gemini/gemini-cli/pull/28817)** (open, P2/core) — Fixes #22589. Non-root scheduler tool calls that don't require approval were being dropped before entering hook state, breaking observability and hook-driven workflows.

3. **[#28816 — Fix silent hang in MessageBus.request when publish fails](https://github.com/google-gemini/gemini-cli/pull/28816)** (open, P2/core) — Fixes #22588. `this.publish()` was a floating promise; on rejection the request silently hung for 60 seconds. Adds proper failure handling to avoid opaque stalls.

4. **[#28818 — Change steering eval test to always pass](https://github.com/google-gemini/gemini-cli/pull/28818)** (open, P2/platform) — Fixes #23313. Model steering regression tests were running under `USUALLY_PASSES`; this tightens the bar to `ALWAYS_PASSES` to catch regressions earlier.

5. **[#28819 — Fix misleading admin error for personal accounts](https://github.com/google-gemini/gemini-cli/pull/28819)** (open, P2/core) — Fixes #24587. Users on personal accounts who select unavailable Gemini models were shown an enterprise-specific error, causing confusion. Improves messaging accuracy.

6. **[#28812 — Prevent indefinite TUI hang by adding execution timeouts](https://github.com/google-gemini/gemini-cli/pull/28812)** (closed, P1/core) — Fixes #21477. Bare Linux terminals could hang at "Initializing..." because `getProcessInfo()` relies on `execAsync` without a timeout. Adds timeouts to prevent indefinite blocking.

7. **[#28834 — Suppress spurious ENOENT warning for transient subdirs in workspace scan](https://github.com/google-gemini/gemini-cli/pull/28834)** (open, P1/P2) — Fixes the recurring `Could not read directory ... projects.json.lock: ENOENT` warning. A BFS tree walker racily encounters a disappearing lock directory; now treated as a no-op for non-root subdirectories.

8. **[#28847 — Update /clear command docs to include context reset](https://github.com/google-gemini/gemini-cli/pull/28847)** (open, P3/docs) — Fixes #19239. `/clear` also resets conversation context, not just the visual screen; documentation was misleading.

9. **[#28740 — Prevent supply chain RCE in eval-pr workflows](https://github.com/google-gemini/gemini-cli/pull/28740)** (open, security) — Fixes #28336. Untrusted fork code could execute in a privileged `pull_request_target` context. Splits the eval workflow into a secure `pull_request` build step and a trusted `workflow_run` execution step. **High-priority security hardening.**

10. **[#28744 — Don't start fresh chat before resuming; it poisons the session file](https://github.com/google-gemini/gemini-cli/pull/28744)** (open, P1/core) — Partially addresses #28693. A fresh-chat start on the load path corrupts the session file; removes one of two occurrences. Important for ACP session resume correctness.

---

## Feature Request Trends

The following directions are consistently requested across issues and community discussion:

1. **Subagent as a first-class primitive** — A significant share of open issues centers on subagent behavior: reliability, visibility, recovery semantics, settings propagation, and permissions. The clear trend: subagents are no longer experimental — they're the core execution model — and users want them treated with the robustness of production infrastructure.

2. **AST-aware tooling** — Multiple EPICs (e.g., #22745, #22746) explore using AST-aware file reads, searches, and codebase mapping to reduce token usage, improve method-boundary precision, and produce cleaner diffs.

3. **Auto Memory privacy & reliability** — Requests for deterministic redaction, bounded retries, better patch validation, and quarantine of invalid patches indicate a push toward a more trustworthy memory subsystem.

4. **Extensions ecosystem transparency** — Requests like the PandaDoc gallery issue (#28208) signal growing demand for clearer, more automated extension submission and review processes.

5. **Proactive skill/subagent usage** — The community expects the model to use custom skills and subagents autonomously when contextually appropriate, not only when explicitly commanded (#21968).

---

## Developer Pain Points

High-frequency frustrations this cycle:

- **Subagent hangs and misreported statuses** — The combination of #21409 (generalist hangs), #22323 (false GOAL success), and #22093 (subagents running without permission) paints a picture of subagent orchestration as the top source of trust-eroding bugs. Users are actively disabling subagents as a workaround.

- **Silent failures and opaque hangs** — Whether it's `MessageBus.request` hanging for 60 seconds (#22588), the TUI hanging at "Initializing..." (#21477), or post-command shell hangs (#25166), developers are experiencing a recurring pattern of stalls without diagnostics.

- **Spurious terminal/UI corruption** — Issues like terminal resize flicker (#21924), corruption after external editor exit (#24935), and incorrect `\n` escape handling (#22466) reflect ongoing terminal-integration rough edges.

- **Security & privacy in background services** — Auto Memory's use of pre-redaction model context (#26525) and the eval-PR RCE vulnerability (#28336 / PR #28740) highlight that users are increasingly scrutinizing background execution paths for security posture.

---

*Digest generated from GitHub data as of 2026-08-18. All linked items are from the [google-gemini/gemini-cli](https://github.com/google-gemini/gemini-cli) repository.*

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-08-18

## Today's Highlights
A quiet release day with no new versions shipped in the last 24 hours, but the issue tracker continues to surface systemic concerns. The most notable cluster involves OAuth metadata handling regressions for MCP servers (GitLab, Atlassian) introduced in v1.0.79, along with a growing wave of long-running session stability complaints — memory-pressure watchdog loops, stale connection IDs, and stale instructions. A single PR removing README documentation has drawn attention as the sole merge-request activity.

---

## Releases
No new releases were published in the last 24 hours. The most recent version remains **1.0.80** (referenced in issue #4504).

---

## Hot Issues
*(10 noteworthy issues, ordered by relevance)*

**1. [#4515 — MCP `content` and `structuredContent` both exposed to context](https://github.com/github/copilot-cli/issues/4515)**  
Newly triaged. When an MCP tool result contains both fields, the CLI adds both to conversation context, causing duplicated or conflicting tool results. The community expects structured content to take precedence — a correctness concern for MCP-heavy workflows.

**2. [#4506 — Memory-pressure watchdog loops at 23% context usage, recovering 0% tokens, until OOM](https://github.com/github/copilot-cli/issues/4506)**  
A severe stability bug: the watchdog force-compacts at low context utilization, recovers essentially nothing, and repeats until the process is killed. Long-session users are increasingly vocal about this class of issue.

**3. [#4505 — Resumed session retains stale connection item IDs after interrupted response](https://github.com/github/copilot-cli/issues/4505)**  
Every prompt after resuming fails with `CAPIError: 400 input item ID does not belong to this connection`. `/fork` does not recover. This breaks the primary resume/restore workflow and is rated high-impact.

**4. [#4480 — Atlassian MCP OAuth fails with RFC 8414 issuer mismatch on v1.0.79 — regression from 1.0.71](https://github.com/github/copilot-cli/issues/4480)**  
With 6 👍 reactions, this regression prevents Atlassian remote MCP servers from authenticating. The same root cause likely underlies the related GitLab issue (#4439). Community is pressing for a hotfix.

**5. [#4509 — `--no-alt-screen` silently removed with no replacement; alt-screen now unavoidable and broken](https://github.com/github/copilot-cli/issues/4509)**  
A long-standing regression (#1799, #2334) made worse: the opt-out flag was deleted without deprecation notice. For developers who pipe output or use TUI-less environments, this is a hard blocker.

**6. [#4390 — Enabled organization models missing from catalogue (Claude Sonnet 5 / Opus 5, Kimi K3)](https://github.com/github/copilot-cli/issues/4390)**  
Copilot Business admins enabling models find them unavailable in the CLI; selection reports "This model is disabled by your..." — 7 👍 indicates broad enterprise impact. The catalogue appears to be out of sync with org settings.

**7. [#4507 — Repo-level `enabledPlugins` ignored in non-interactive mode](https://github.com/github/copilot-cli/issues/4507)**  
Surfaces disagree: interactive mode and `plugins list` honor the setting, but `copilot -p` ignores it. CI/CD automation is therefore not reproducible — a trust issue for plugin-driven teams.

**8. [#4492 — Desktop app WebView2 renderer self-aborts (`STATUS_BREAKPOINT`); window goes blank](https://github.com/github/copilot-cli/issues/4492)**  
Six occurrences on one machine; the desktop app's main window goes blank and loses the canvas panel until manual refresh. Filed by Copilot on behalf of the user, this is a reliability concern for the desktop pathway.

**9. [#4508 — Feature request: reload `.github/instructions` mid-session](https://github.com/github/copilot-cli/issues/4508)**  
Long-running sessions (200+ compactions) never see edits to instruction files. Teams that iterate on guidance find this limits their workflow; the request is to reload on compaction boundaries.

**10. [#4511 — Session AIC display is not reliable, underestimates consumption (observed with Kimi K3)](https://github.com/github/copilot-cli/issues/4511)**  
Budget-tracking users report that reported AIC numbers are materially wrong in long sessions. Given the emphasis on token/cost discipline, this erodes trust in the accounting UI.

---

## Key PR Progress
*(Only 1 PR updated in the last 24h — noted below; otherwise highlighted from the activity window)*

**1. [#4510 — Remove GitHub Copilot CLI documentation from README](https://github.com/github/copilot-cli/pull/4510)**  
This PR strips installation and usage documentation from the README entirely. The motivation is unclear, but it has drawn scrutiny from the community as documentation is critical for onboarding. No comments yet; the change is small but high-visibility.

---

## Feature Request Trends
Distilled from open issues, the community's top directions are:

- **Plugin ecosystem maturity** — dependency resolution between marketplace plugins (#4487), honoring repo-level `enabledPlugins` in all modes (#4507), and branch-aware cache keys for marketplace sources (#4513).
- **Session resilience** — reloading `.github/instructions` mid-session (#4508), scrollable conversation history (#4313), and reliable session restore (#4514).
- **Config parity across surfaces** — exposing `contextTier` in ACP session config (#4275), honoring model selections in custom agents (#2950), and using system-installed `gh` instead of the bundled binary (#4456).
- **MCP policy fallback** — allowing locally-defined stdio MCP servers to run even when the registry fetch fails (#4512) signals a desire for fail-open behavior in offline or policy-misconfigured environments.

---

## Developer Pain Points
Recurring frustrations and friction points from the last 24 hours:

- **OAuth / MCP regressions shipping in releases** — GitLab (#4439) and Atlassian (#4480) both broke in v1.0.79 due to RFC 8414 issuer handling. This is the second time MCP auth has regressed, straining trust in release stability.
- **Long-session execution instability** — memory-pressure watchdog loops (#4506), stale connection IDs (#4505), stale instruction files (#4508), and unreliable AIC reporting (#4511) all compound to make day-long sessions fragile.
- **Inconsistent behavior between interactive and non-interactive modes** — plugins (#4507), model selection (#2950), and context tier (#4275) all differ, breaking automation and reproducibility.
- **Silent removal of workarounds** — `--no-alt-screen` removal without deprecation (#4509) and forced alt-screen rendering are the latest in a pattern where users lose escape hatches without migration paths.
- **Lifecycle management gaps** — Docker-wrapped MCP containers staying alive after session close (#4461), and the desktop app's renderer self-aborting (#4492) point to resource-cleanup and stability issues across transport layers.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest — 2026-08-18

## Today's Highlights
The Kimi CLI project showed minimal activity in the last 24 hours—no new releases and no freshly updated issues. The sole update is PR #864, which introduces a `--starting-prompt` flag to inject an initial prompt without exiting the REPL; this long-requested feature (linked to issue #887) finally moved to closure after six months, marking a notable quality-of-life win for automation workflows.

## Releases
No new releases were published in the last 24 hours. The most recent release remains the previous stable version. Stay tuned for future releases that may incorporate the pending PRs below.

## Hot Issues
No issues were updated in the last 24 hours. Based on recent activity and historical context, here are the most significant open issues currently influencing the project's direction:

1. **#887 — `--starting-prompt` support** — Directly tied to the merged PR #864; users want to pass an initial prompt via CLI for scripting and one-shot automation. High demand for CI/CD integration.
   [Issue #887](https://github.com/MoonshotAI/kimi-cli/issues/887)

2. **#785 — REPL exit/reset behavior** — A long-standing discussion (linked from PR #864) about confusing REPL exit semantics and state resets; community is split on default behavior vs. explicit flags.
   [Issue #785](https://github.com/MoonshotAI/kimi-cli/issues/785)

3. **#851 — Multi-turn context window management** — Users report losing conversation context on long sessions; requests for automatic summarization or manual context compaction.
   [Issue #851](https://github.com/MoonshotAI/kimi-cli/issues/851)

4. **#843 — Streaming output latency** — Complaints about token-by-token streaming lag on large code files, especially with long system prompts; users want optional buffered output mode.
   [Issue #843](https://github.com/MoonshotAI/kimi-cli/issues/843)

5. **#832 — Windows terminal compatibility** — ANSI escape code issues in PowerShell/CMD causing garbled output; community is requesting a compatibility mode.
   [Issue #832](https://github.com/MoonshotAI/kimi-cli/issues/832)

6. **#828 — Git diff integration** — Feature request to run `kimi` directly on `git diff` output for automated code review comments; several workaround scripts exist but users want native support.
   [Issue #828](https://github.com/MoonshotAI/kimi-cli/issues/828)

7. **#819 — Session persistence across restarts** — Users want to save and resume conversations; currently all context is lost on exit.
   [Issue #819](https://github.com/MoonshotAI/kimi-cli/issues/819)

8. **#811 — Proxy and VPN support** — Enterprise users cannot use Kimi CLI behind corporate proxies; requests for explicit proxy config and certificate handling.
   [Issue #811](https://github.com/MoonshotAI/kimi-cli/issues/811)

9. **#806 — Custom model endpoint configuration** — Community wants to point the CLI at alternative/compatible backends (e.g., local models or other providers) via config file.
   [Issue #806](https://github.com/MoonshotAI/kimi-cli/issues/806)

10. **#799 — Token usage reporting** — Users want a `--verbose` mode showing token consumption per request, to manage costs during long interactive sessions.
    [Issue #799](https://github.com/MoonshotAI/kimi-cli/issues/799)

## Key PR Progress
Only one PR was updated in the last 24 hours, but the following 10 PRs represent the most significant recent and pending contributions:

1. **#864 — `--starting-prompt` flag (CLOSED)** — Adds `-s` / `--starting-prompt` to supply an initial prompt without entering an interactive loop. Merged; closes #887. Major win for scripting.
   [PR #864](https://github.com/MoonshotAI/kimi-cli/pull/864)

2. **#860 — Add `--json` output mode** — Enables structured output for machine parsing; community feedback positive, awaiting maintainer review.
   [PR #860](https://github.com/MoonshotAI/kimi-cli/pull/860)

3. **#855 — Support OpenAI-compatible API endpoints** — Adds configurable base URL to allow alternative backends; pending since March, large number of upvotes.
   [PR #855](https://github.com/MoonshotAI/kimi-cli/pull/855)

4. **#849 — Context compaction on overflow** — Automatically summarizes older turns when context window is exceeded instead of truncating. In review.
   [PR #849](https://github.com/MoonshotAI/kimi-cli/pull/849)

5. **#841 — Interactive `git diff --cached` mode** — Runs a review on staged changes with one command; reduces friction for code review workflows.
   [PR #841](https://github.com/MoonshotAI/kimi-cli/pull/841)

6. **#837 — Fix: Windows UTF-8 encoding corruption** — Fixes mangled non-ASCII characters on Windows consoles; tested by several users, awaiting merge.
   [PR #837](https://github.com/MoonshotAI/kimi-cli/pull/837)

7. **#829 — Add session save/load commands** — Implements `kimi save` and `kimi load` for resumable sessions; overlaps with issue #819.
   [PR #829](https://github.com/MoonshotAI/kimi-cli/pull/829)

8. **#820 — Token usage counter in status bar** — Displays live token counts during interaction; designed for heavy users monitoring costs.
   [PR #820](https://github.com/MoonshotAI/kimi-cli/pull/820)

9. **#815 — Config file support (`~/.kimirc`)** — Centralizes model params, endpoints, and flags; requested widely for team standardization.
   [PR #815](https://github.com/MoonshotAI/kimi-cli/pull/815)

10. **#808 — Refactor prompt builder for maintainability** — Internal refactor to modularize system-prompt assembly; no user-facing changes, but enables future features like custom profiles.
    [PR #808](https://github.com/MoonshotAI/kimi-cli/pull/808)

## Feature Request Trends
Across recent issues, three dominant themes emerge:

- **Automation & CI friendliness** — Requests for headless/non-interactive modes, `--starting-prompt`, `--json` output, and git-diff integration all point to teams wanting to use Kimi CLI in build pipelines and automated review steps, not just interactive shells.
- **Statefulness & persistence** — A strong cluster of requests center on session save/resume, context compaction, and history management. Users want the CLI to behave more like a persistent IDE assistant rather than a stateless terminal tool.
- **Flexible backends & configurability** — Multiple requests ask for configurable endpoints, custom model choices, `.kimirc` files, and proxy support. This reflects a broader ecosystem trend where developers expect CLI tools to be swappable between different model backends as the landscape evolves.

## Developer Pain Points
- **Context loss on long sessions** — The single most common frustration: the CLI loses track of earlier conversation turns, forcing users to re-explain context, particularly on large coding tasks.
- **No "one-shot" mode** — Users repeatedly complain that there is no simple way to ask a single question from the shell without entering the interactive loop; PR #864 directly addresses this.
- **Output not machine-parseable** — The lack of `--json` or structured output is a blocker for developers who want to pipe results into other tools like `jq`, `grep`, or CI validators.
- **Windows pain is persistent** — Encoding issues, ANSI codes, and generally rough experience on Windows terminals remains a grievance despite earlier patch attempts.
- **Opaque usage/costs** — Users want per-request token counts and estimated costs; the absence of a built-in counter forces manual tracking and surprises at billing time.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-08-18

## Today's Highlights

The community is actively reporting on **Windows-specific reliability issues** (ARM64 TUI failures, npm installation crashes, and serve-mode errors) alongside **endpoint/service availability problems** with OpenCode's managed inference gateway. Meanwhile, **plugin API enhancements** (session request hooks, UI surfaces for web/desktop) and **workflow automation features** (multi-step YAML pipelines, session loop commands) are moving through the PR pipeline.

---

## Releases

No new releases in the last 24 hours.

---

## Hot Issues

1. **[#19130 — Windows ARM64 native: OpenTUI fails to initialize with bun:ffi dlopen TinyCC error](https://github.com/anomalyco/opencode/issues/19130)** · 18 comments · 12 👍
   A long-standing issue (since March) where native ARM64 builds work for CLI commands but TUI crashes at init. High engagement indicates significant Windows-on-ARM adoption in the community.

2. **[#43105 — [2.0] BUG: endpoint error](https://github.com/anomalyco/opencode/issues/43105)** · 15 comments
   Users are hitting `410 Gone` when using `https://opencode.ai/inference/v1` as a custom endpoint, citing "Legacy inference endpoint retired." Notably, the beta (v2) works fine — suggesting the legacy endpoint shim is being removed while the community still depends on it.

3. **[#7801 — Plan Mode + Question tool can auto switch to Build mode](https://github.com/anomalyco/opencode/issues/7801)** · 11 comments · 32 👍
   A popular feature request (32 reactions) for automatic mode transitions: when the agent asks a question during Plan mode, it should gracefully switch to Build mode rather than requiring manual user action.

4. **[#40243 — ChatGPT OAuth rejects GPT-5.6 models for EU-resident workspace](https://github.com/anomalyco/opencode/issues/40243)** · 9 comments · 4 👍
   EU-residency OpenAI workspaces fail to authenticate through OpenCode's OAuth flow, while official Codex CLI succeeds. Regional compliance is now a **hard requirement** for European enterprise users.

5. **[#33027 — MCP tools connected but not exposed to agent](https://github.com/anomalyco/opencode/issues/33027)** · 8 comments · 3 👍
   MCP servers successfully connect and list tools, but the agent can't see or invoke them. This is a **relay-layer bug** — protocol is fine, but tool exposure to the agent runtime is broken.

6. **[#24153 — Add unarchive/restore for archived sessions](https://github.com/anomalyco/opencode/issues/24153)** · 8 comments · 11 👍
   Archiving is one-way today. Users want restore capability. Low complexity, high quality-of-life impact.

7. **[#42995 — Quota problem](https://github.com/anomalyco/opencode/issues/42995)** · 4 comments · 3 👍
   User was charged $3.02 but hit their $12/5-hour quota immediately. This points to **quota accounting being skewed by a specific usage pattern** (possibly the 5-hour sliding window).

8. **[#43054 — Models other than hy3-free / deepseek flash free fail with Forbidden](https://github.com/anomalyco/opencode/issues/43054)** · 3 comments · 1 👍
   Only free-tier models work; everything else returns `Forbidden: {"model":"big-pickle"}`. This is likely a **gateway authorization misconfiguration** where the actual model ID is leaked in the error body.

9. **[#40623 — Grep tool fails on Windows: ripgrep extraction broken by MSIX PowerShell 7](https://github.com/anomalyco/opencode/issues/40623)** · 3 comments
   Windows + Microsoft Store PowerShell 7 breaks ripgrep extraction — and failures are **cached until restart**. An edge-case environment interaction with permanent-session failure modes.

10. **[#43110 — opencode serve fails immediately with generic 'ServeError' on Windows](https://github.com/anomalyco/opencode/issues/43110)** · 1 comment
    `opencode serve` crashes immediately on Windows 11 with zero diagnostics, even at DEBUG level. TUI works fine — isolation suggests a **platform-specific server bootstrap error** with terrible error surfacing.

---

## Key PR Progress

1. **[#37549 — feat(plugin): add session request hook](https://github.com/anomalyco/opencode/pull/37549)** · Closed
   Adds `ctx.session.hook("request", ...)` for mutable model headers and JSON bodies — applied before auth/signing, with concurrency-safe caching of transformed AI SDK models.

2. **[#37542 — fix(opencode): restore session diff summary](https://github.com/anomalyco/opencode/pull/37542)** · Closed
   Reintroduces session-level diff summaries removed by #30127. Closes #30877, #32852, #17797 — three long-standing diffs-went-missing issues.

3. **[#37537 — fix(tui): preserve system palette colors](https://github.com/anomalyco/opencode/pull/37537)** · Closed
   Generates native V2 system themes from the detected terminal palette, preserving literal ANSI hues instead of synthesizing darker colors — a visual-fidelity fix for terminal users.

4. **[#37535 — fix(opencode): sanitize Bedrock document names from file attachments](https://github.com/anomalyco/opencode/pull/37535)** · Closed
   Fixes #37191: Bedrock rejects document names with certain characters; MCP binary attachments can produce synthetic filenames that trigger this — sanitization now applied.

5. **[#37530 — fix(core): restore external directory defaults](https://github.com/anomalyco/opencode/pull/37530)** · Closed
   Allows external access to discovered skills and materialized reference directories by default, while keeping shell output readable through broad denials. Fixes permission regressions.

6. **[#37504 — feat(opencode): add session loop command](https://github.com/anomalyco/opencode/pull/37504)** · Closed
   New built-in `/loop` (and `/proactive` alias) for repeating session behavior — closes #23578. Was originally #23575 but went stale; this is the refreshed version.

7. **[#37499 — feat: add /workflow slash command for multi-step YAML pipelines](https://github.com/anomalyco/opencode/pull/37499)** · Closed
   New workflow system: define multi-step pipelines in YAML under `.opencode/workflows/` and execute via `/workflow`. A **significant automation primitive** built into the CLI.

8. **[#37477 — fix: don't boot a full instance for session list](https://github.com/anomalyco/opencode/pull/37477)** · Closed
   `session list` now queries the DB directly instead of booting a full OpenCode instance — closes #37435. Addresses slow CLI startup for a common operation.

9. **[#37472 — fix(opencode): strip provider control tokens from invalid tool output](https://github.com/anomalyco/opencode/pull/37472)** · Closed
   Fixes #37297: some OpenAI-compatible providers return raw control tokens (`<|tool_call_begin|>`) inside tool arguments, breaking parsing — now stripped before validation.

10. **[#42810 — refactor(core): simplify interrupt continuation](https://github.com/anomalyco/opencode/pull/42810)** · Open
    Replaces the interrupt continuation state machine with a three-line post-cleanup check in `SessionExecution`. Active refactor by a core contributor (kitlangton) — worth watching.

---

## Feature Request Trends

- **Automatic Mode Transitions (#7801, 32 👍)** — Users want Plan Mode to auto-switch to Build mode when questions turn into actions. This is the top-voted request right now and signals a desire for more **proactive agent behavior**.

- **Session Lifecycle Management (#24153, 11 👍)** — Archive/restore, unarchive, and better session browsing. Users are treating sessions as a **long-term knowledge base**, not just ephemeral conversations.

- **Plugin API Expansion (#43132)** — Mirror the TUI plugin surface (dialogs, keymaps, sidebar slots) in the web/desktop app. The community wants **cross-surface plugin parity**, not just TUI-only hooks.

- **Rate-Limit Resilience (#43126)** — Pause and auto-resume tasks when providers report known `retry-after` windows, instead of hard-failing. This is a **reliability-first** request from heavy users.

- **Multi-Step Workflow Automation (#37499, #37504)** — YAML-defined pipelines and conversational loop commands are both landing in PRs. The community is pushing OpenCode toward **composable automation**, not just chat.

---

## Developer Pain Points

1. **Windows is a second-class citizen.** ARM64 TUI crashes (#19130), MSIX PowerShell breaking ripgrep (#40623), broken postinstall binaries (#41370), `serve` failing with no diagnostics (#43110), and permission config issues (#36681, #36696). The pattern is **recurring and broad** — Windows users are consistently reporting platform-specific breakage.

2. **Managed gateway flakiness.** Endpoint 410s (#43105), model 403s (#43054), quota miscounting (#42995), and upstream "Endpoint unavailable" (#43102) all point to reliability problems with the hosted inference service. This is a **trust eroder** — devs can't depend on the gateway for production work.

3. **MCP integration is fragile.** Tools connect but aren't exposed to the agent (#33027); binary attachments with synthetic filenames break Bedrock (#37535). The **MCP relay layer lacks robustness** in both tool discovery and payload handling.

4. **Silent failures with no diagnostics.** `opencode serve` gives only "ServeError" with no stack trace (#43110); grep failures cached until restart (#40623); sessions stall with no timeout (#36731). The common thread: **errors surface late, if at all**, making debugging a guessing game.

5. **Plugin system has footguns.** The legacy plugin loader invokes *every* exported function and assumes it's a Hooks object (#42451) — any helper function in a plugin module corrupts loading and crashes startup. This **fails fast but with zero guidance**.

6. **Documentation gaps for platform-specific config.** Windows path handling, external directory permissions, and cmdlet allowlists are documented poorly or not at all (#36681, #36696). Users are **reverse-engineering config formats** from error messages.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-08-18

## 1. Today's Highlights
The Pi coding agent ecosystem saw a major focus on **provider compatibility and resilience**, with significant fixes landing for Anthropic refusal handling, OpenRouter reasoning round-trips, and Qwen/Bedrock catalog alignment. Notably, a long-standing issue regarding **nested markdown skills** (`#6479`) was finally resolved, and work began on **experimental append compaction** to address the recurring context-window overflow problem. The community is actively engaged with 50 open/updated issues and 34 PRs in the last 24 hours, signaling strong momentum.

## 2. Releases
No new Pi releases in the last 24 hours.

## 3. Hot Issues

| Issue | Title | Why it matters | Community reaction |
|-------|-------|----------------|-------------------|
| [#6879](https://github.com/earendil-works/pi/issues/6879) | Auto-compaction never triggers after context grows past 100% until provider overflow | A 2-hour agentic turn grew past the compaction threshold, hitting a 373k-token API rejection. Compaction must check after every agent step, not only on provider errors. | **18 comments, 17 👍** — high urgency; developers want preemptive compaction before provider hard failures. |
| [#534](https://github.com/earendil-works/pi/issues/534) | Config folder is out of place on Linux | Pi stores config directly in `$HOME` instead of following the **XDG Base Directory Spec** — a standards violation on modern Linux. | **15 comments, 39 👍** — long-standing (created Jan 2026) and still unresolved; strong community support for XDG compliance. |
| [#8029](https://github.com/earendil-works/pi/issues/8029) | Very slow performance when moving in prompt editor | A single arrow-key press takes **1650ms** with ~7000 lines in the prompt buffer. Editor navigation needs to be optimized to avoid O(n) redraws. | **9 comments** — annoying but not blocking; affects power users with large multi-file paste operations. |
| [#7995](https://github.com/earendil-works/pi/issues/7995) | openai-responses: no `cacheControlFormat: 'anthropic'` support | From a **870-trial benchmark**, missing prompt caching support on OpenRouter's responses surface causes a **2.5x measured cost penalty** for Claude models. | **4 comments** — filed on behalf of OpenRouter; cost sensitivity drives interest. |
| [#3200](https://github.com/earendil-works/pi/issues/3200) | Support video/audio content in prompt command | Extend the `prompt` RPC to accept `video`/`audio` alongside existing `images` support for multimodal models (Gemma 4, GPT-4o). | **8 comments, 5 👍** — multimodal agents are a growing use case. |
| [#8036](https://github.com/earendil-works/pi/issues/8036) | Edit tool crashes TUI when rendering a large diff | A ~14.5 MB diff from an edit with long HTML lines crashes the interactive TUI during rendering and session resume. Diff rendering needs size limits or virtualization. | **4 comments** — crash-on-resume is severe; workaround is editing smaller files. |
| [#8166](https://github.com/earendil-works/pi/issues/8166) | Custom message injected mid-tool-batch breaks tool_calls adjacency (DeepSeek 400) | An extension calling `sendMessage(..., { triggerTurn: false })` during a tool batch corrupts message ordering, causing permanent 400 errors on every subsequent turn. | **3 comments** — subtle extension-API bug; breaks sessions irrecoverably. |
| [#7756](https://github.com/earendil-works/pi/issues/7756) | `detectInstallMethod` mislabels non-pnpm installs under `PNPM_HOME` | Any path containing `/pnpm/` is misidentified as pnpm-managed, causing false "not managed" errors for global-nub style installs. | **3 comments** — installer UX friction for users sharing a `PNPM_HOME` bin directory. |
| [#8252](https://github.com/earendil-works/pi/issues/8252) | pi crashes when tmux resizes the pane to 1 column | The spinner trips on terminal width `1` from tmux `window-size latest`, exiting with code 1. | **2 comments** — reproducible but niche; needs a minimum-size guard. |
| [#8279](https://github.com/earendil-works/pi/issues/8279) | Bedrock Converse rejects root-composed tool schemas without `type: object` | Bedrock rejects tools where the input schema is missing a root `type: object` — a compatibility issue with Amazon's stricter validation. | **1 comment** — new issue; relevant for all Bedrock users with custom tools. |

## 4. Key PR Progress

| PR | Title | Description |
|----|-------|-------------|
| [#8258](https://github.com/earendil-works/pi/pull/8258) | **Anthropic refusal error and fallbacks** | Fixes #8017. Adds Anthropic's `allowed_fallback_models` metadata to the model registry so compaction can retry with a fallback model when the classifier returns `stop_reason: "refusal"`. |
| [#8255](https://github.com/earendil-works/pi/pull/8255) | **Load nested markdown skills** | Fixes #6479. Skills directory discovery now recurses into subfolders for standalone `.md` skills, not just `SKILL.md` files. |
| [#8120](https://github.com/earendil-works/pi/pull/8120) | **Experimental append compaction** | When `PI_EXPERIMENTAL=1`, uses append compaction instead of standalone. Reuses the active system prompt and tools so the compacted prefix can hit provider prompt caches — a direct answer to context-window complaints. |
| [#8246](https://github.com/earendil-works/pi/pull/8246) | **OpenAI completions reasoning details** | Fixes #7994. Preserves signed (non-encrypted) `reasoning_details` entries for proper round-trip replay on OpenRouter. |
| [#8242](https://github.com/earendil-works/pi/pull/8242) | **Use `agent_settled` instead of `agent_end`** | Fixes #7350. Updates shipped examples to fire "ready for input" only after Pi stops retrying/compacting, not at the end of a low-level run. |
| [#8240](https://github.com/earendil-works/pi/pull/8240) | **Align Qwen Token Plan model catalogs** | Fixes #8194. Shares a single 8-model allowlist across `qwen-token-plan` and `qwen-token-plan-cn`; keeps `qwen-token-plan-individual` separate with 7 models. |
| [#8262](https://github.com/earendil-works/pi/pull/8262) | **Dispatch hooks on every turn-start path** | Fixes the bug where `sendCustomMessage(triggerTurn: true)` bypasses the `input` hook and `before_agent_start`. Now every turn dispatches preflight hooks. |
| [#8257](https://github.com/earendil-works/pi/pull/8257) | **Skip project-agent confirm when already trusted** | Stops the subagent extension from prompting "Run project-local agents?" on every use for projects already marked trusted in `trust.json`. |
| [#8254](https://github.com/earendil-works/pi/pull/8254) | **Prevent copilot policy login rate limits** | Fixes #7850. Fetches the account model catalog before policy updates, only updates unconfigured tool-capable models, and retries throttled login requests with bounded delay. |
| [#8253](https://github.com/earendil-works/pi/pull/8253) | **Avoid full-screen flashing in long transcripts** | Differential rendering only touched the visible viewport; changes above it cleared and reprinted 10k+ line transcripts. Now clears only the affected regions. |

## 5. Feature Request Trends
The community is pushing toward **enterprise-grade operational tooling**:
- **Standardization**: XDG compliance (#534), SELinux container documentation (#8276) — a demand for platform-correct behavior.
- **Multimodal expansion**: Video/audio support in prompt RPC (#3200), GLM-4.6V vision model catalog (#8220).
- **Resilient session management**: Automatic resume after provider rate-limit reset (#8277), preemptive compaction before context overflow (#6879).
- **Provider breadth**: Neon AI Gateway (#7895), Amazon Bedrock Mantle (#6216), codex websockets with bearer tokens (#5152).

## 6. Developer Pain Points
- **Context overflow is the #1 operational pain**: auto-compaction often triggers too late, after a provider rejection; local providers can still overflow between tool turns (#8229). The experimental append compaction PR (#8120) is a direct response.
- **Provider incompatibilities create hidden cost and breakage**: missing `cacheControlFormat` support costs 2.5x on OpenRouter (#7995); Bedrock rejects schemas without `type: object` (#8279); GLM 5.2 on Mistral executes empty commands (#8069).
- **TUI fragility with large content**: crashes on huge diffs (#8036), V8 string limits in `fullRender` (#8028), slow prompt editor navigation (#8029), and full-screen flashing in long transcripts (#8253).
- **Extension API footguns**: `agent_end` fires too early (#7350, #8242); silent mid-turn message injection breaks tool adjacency (#8166).

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-08-18

## Today's Highlights

Qwen Code v0.21.13 is now the pinned benchmark reference, with full end-to-end validation completed on SWE-bench Verified (500 tasks) and Terminal-Bench 2.0 (89 tasks) through the DSW Harbor release pipeline. The Web Shell composer has gained drag-and-drop and paste support for text file attachments, while conversation forking from assistant responses is rolling out. The community is actively reporting on Windows paste regressions (Ctrl+V broken since 0.21.x) and context compression inaccuracies, both under active investigation.

## Releases

**[v0.21.13](https://github.com/QwenLM/qwen-code/releases/tag/v0.21.13)** — Final release. No release notes provided beyond the version tag. This is the version pinned for SWE-bench and Terminal-Bench validation runs, with four smoke test iterations (r1–r4) confirming benchmark stability. Notably, r2 was QUARANTINED due to execution errors, but r3 and r4 both SUCCEEDED with 1/1 resolved.

**[v0.21.11-nightly.20260817.195128a17a](https://github.com/QwenLM/qwen-code/releases/tag/v0.21.11-nightly.20260817.195128a17a)** — Nightly build including:
- `feat(autofix)`: deny-by-default footprint gate and positional window censuses by [@wenshao](https://github.com/wenshao) ([#9156](https://github.com/QwenLM/qwen-code/pull/9156))
- Web Shell bug fixes

## Hot Issues

1. **[#9061 — Ctrl+V paste broken in CLI on Windows (P1)](https://github.com/QwenLM/qwen-code/issues/9061)** 🔥
   Regression since 0.21.x (works on 0.21.0). Complete paste unresponsiveness in Windows terminals. 6 comments. High priority and actively being triaged.

2. **[#9324 — Messages delivered in duplicate copies (P3)](https://github.com/QwenLM/qwen-code/issues/9324)**
   Qwen Desktop Code with Qwen 3.8 Max reports receiving the same message multiple times mid-task, interrupting focus. User suspects a delivery bug. 7 comments; needs more info.

3. **[#9320 — Lost context after /compress-fast and /rewind (P2)](https://github.com/QwenLM/qwen-code/issues/9320)**
   User compressed 102k → 87k tokens, but after resuming with a new llama-server, context appears lost. Raises concerns about compression correctness across session restarts.

4. **[#9315 — New version fields cannot be copied in CLI (P3)](https://github.com/QwenLM/qwen-code/issues/9315)**
   Ubuntu 22 user reports text selection/copy broken since v0.19. The new terminal interaction layer appears to have dropped copy support. Chinese-language report.

5. **[#9309 — Compression math appears incorrect (P3)](https://github.com/QwenLM/qwen-code/issues/9309)**
   After `/compress-fast` then `/compress`, the second compression reports numbers that seem wrong (170k → 7x). Community is checking whether nested compression compounds inaccurately.

6. **[#6806 — Status line context % not refreshed after /compress (P2)](https://github.com/QwenLM/qwen-code/issues/6806)**
   Footer still shows pre-compression token count until the next model request. Long-standing issue (since July 13) with 6 comments; welcome for PRs.

7. **[#9296 — Autofix review-event storms waste runner capacity (P1)](https://github.com/QwenLM/qwen-code/issues/9296)**
   Live data shows 59% of ~500 autofix runs in 3 hours were cancelled. Includes P0 bug: reviews on closed/merged PRs still trigger autofix runs, plus duplicate address dispatch.

8. **[#9300 — VP mode: blank space between last message and composer (P2)](https://github.com/QwenLM/qwen-code/issues/9300)**
   Content not bottom-aligned in `useTerminalBuffer: true` mode. UI regression reported with 6 comments.

9. **[#8316 — Prompt not restored to input box on Ctrl+C (P3)](https://github.com/QwenLM/qwen-code/issues/8316)**
   Cancelling an agent prompt loses the text entirely — users must retype. Long-standing (since Aug 1) with 9 comments.

10. **[#9250 — qwen serve new files hard-coded to mode 0600 (P3)](https://github.com/QwenLM/qwen-code/issues/9250)**
    `write_file`/`edit`/`notebook_edit` ignore umask with no configuration escape hatch. Relevant for shared environments and CI.

## Key PR Progress

1. **[#9358 — Weixin typing indicator keep-alive](https://github.com/QwenLM/qwen-code/pull/9358)** — Re-sends `TYPING` every 4 seconds to prevent expiry during long turns. Directly addresses [#9353](https://github.com/QwenLM/qwen-code/issues/9353).

2. **[#9364 — Configurable new-file mode for qwen serve](https://github.com/QwenLM/qwen-code/pull/9364)** — Adds `QWEN_SERVE_NEW_FILE_MODE` env var with `NewFileModePolicy` ('owner'|'system'), resolving [#9250](https://github.com/QwenLM/qwen-code/issues/9250). Threaded through `WorkspaceFileSystemFactory`.

3. **[#9367 — Global expand/collapse in exported HTML viewer](https://github.com/QwenLM/qwen-code/pull/9367)** — Adds toolbar control to `ChatViewer` and enables it in `/export` HTML template. Addresses [#8208](https://github.com/QwenLM/qwen-code/issues/8208).

4. **[#9303 — Bound daemon transcript retention in web-shell](https://github.com/QwenLM/qwen-code/pull/9303)** — Prevents renderer OOM crashes by releasing raw replay snapshots after injection and applying block caps to replay rebuilds. Critical for long sessions.

5. **[#9342 — Clear deferred-suggestion backlog from PR #9175](https://github.com/QwenLM/qwen-code/pull/9342)** — Cleans 19 deferred findings across 15 review rounds. Roughly half are behavior fixes including a safety-shaped API.

6. **[#9321 — /takeover from N parameter](https://github.com/QwenLM/qwen-code/pull/9321)** — Seeds the takeover round counter, useful for steady-state review cycles. `CRITICAL_ONLY_AFTER_ROUND` math works with a nonzero start.

7. **[#9295 — Omit unconsumable image media](https://github.com/QwenLM/qwen-code/pull/9295)** — Fixes [#9291](https://github.com/QwenLM/qwen-code/issues/9291): images with MIME types the model endpoint can't consume (HEIC, TIFF) are now skipped instead of forwarded as broken data URIs.

8. **[#9369 — Port heal chain's wipe guard to triage/A/B workflows](https://github.com/QwenLM/qwen-code/pull/9369)** — Consolidates the "empty workspace, keep directory" idiom with trailing-slash strip, path canonicalization, and runner-workspace allowlisting.

9. **[#9191 — Transfer per-file content verdicts across rebases](https://github.com/QwenLM/qwen-code/pull/9191)** — Instead of invalidating incremental review state when a commit is force-pushed, the system now anchors verdicts to file content pairs, surviving history rewrites.

10. **[#9131 — Incremental composer skills refresh in web-shell](https://github.com/QwenLM/qwen-code/pull/9131)** — Adds a deduplicated workspace signal for Skill-toggle mutations, choosing the right composer source per runtime state (active vs. session-less).

## Feature Request Trends

- **Serving / Daemon Resource Governance**: Multiple intertwined threads ([#8051](https://github.com/QwenLM/qwen-code/issues/8051), [#8091](https://github.com/QwenLM/qwen-code/issues/8091)) push for bounding memory/bytes held by request bodies and WebSocket assemblies in `qwen serve`, not just session counts.
- **Export & Transcript Interop**: [#9354](https://github.com/QwenLM/qwen-code/issues/9354) and [#8208](https://github.com/QwenLM/qwen-code/issues/8208) call for a cross-host chat transcript contract (Web Shell, Tauri Desktop, VS Code) with versioned schemas and safety boundaries. HTML export should include thinking and tool results with expand/collapse.
- **Channel Integration Depth**: Weixin channel requests include dynamic typing indicators ([#9353](https://github.com/QwenLM/qwen-code/issues/9353)), file sending ([#9352](https://github.com/QwenLM/qwen-code/issues/9352)), and 64-bit message ID preservation ([#9307](https://github.com/QwenLM/qwen-code/issues/9307)).
- **Provider Preset Dynamism**: [#9368](https://github.com/QwenLM/qwen-code/issues/9368) asks ModelStudio Token Plan / Coding Plan presets to fetch model lists dynamically instead of hardcoding them in the wizard.
- **Consolidated Chat Panel**: [#5883](https://github.com/QwenLM/qwen-code/issues/5883) continues to gather support for unifying chat UI across web-shell, VS Code webview, and desktop.

## Developer Pain Points

1. **Windows CLI Regressions**: Ctrl+V paste totally broken since 0.21.x ([#9061](https://github.com/QwenLM/qwen-code/issues/9061)) — a serious daily-driver blocker. The issue notes it works in plain PowerShell, so the new terminal layer is the suspect. Community is frustrated, downgrading to 0.21.0 to restore function.

2. **Context Compression Inconsistencies**: Multiple reports ([#9320](https://github.com/QwenLM/qwen-code/issues/9320), [#9309](https://github.com/QwenLM/qwen-code/issues/9309), [#6806](https://github.com/QwenLM/qwen-code/issues/6806)) around `/compress` and `/compress-fast`: displayed token counts don't match reality, status bar doesn't refresh, and behavior across session restarts is unreliable.

3. **Interactive Input Loss**: Cancelling a prompt with Ctrl+C loses the typed text entirely ([#8316](https://github.com/QwenLM/qwen-code/issues/8316)), and the new terminal interaction layer broke copy/paste selection ([#9315](https://github.com/QwenLM/qwen-code/issues/9315)).

4. **Autofix / Review Pipeline Waste**: 59% of autofix runs are cancelled due to events on closed/merged PRs and duplicate address dispatch ([#9296](https://github.com/QwenLM/qwen-code/issues/9296)) — CI minutes and runner capacity being burned.

5. **AI-generated triage noise**: Multiple issues (e.g., [#9344](https://github.com/QwenLM/qwen-code/issues/9344), [#8448](https://github.com/QwenLM/qwen-code/issues/8448)) are created by AI during triage ("generated by AI") — some closed quickly as duplicates or non-issues. The community appears to tolerate this but it adds triage overhead.

6. **File Permission Surprises**: `qwen serve` creating new files as `0600` regardless of umask ([#9250](https://github.com/QwenLM/qwen-code/issues/9250)) is a papercut in shared/CI environments; a PR is already up to fix it.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-08-18

## 1. Today's Highlights

The project rebranded to **CodeWhale** (formerly DeepSeek TUI) and shipped **v0.9.9** — a "truth-and-resilience" release that fixes a critical shell-wedge bug (host disk/descriptor exhaustion now fails soft), refactors tiered V4 pricing to resolve peak/off-peak per turn, and adds a DSH (DeepSeek Harness) ambient ocean scene. Community contributors landed three fixes (context compaction for web tools, model-casing safety, skill prompt stability), while maintainers pushed doc localization and i18n dictionary work forward. The most active issues continue to center on subagent reliability, config-path fragmentation, and the agent tool's overly complex schema.

---

## 2. Releases

**v0.9.9** ([PR #5476](https://github.com/Hmbown/CodeWhale/pull/5476)) — theme: **truth-and-resilience**

- **Critical fix**: shell tool can no longer wedge a session when host runs out of disk/descriptors ([#5465](https://github.com/Hmbown/CodeWhale/pull/5465))
- Unverified context windows / output ceilings / telemetry defaults are now labeled honestly
- **V4 pricing**: tiered peak/off-peak resolved per turn ([#5470](https://github.com/Hmbown/CodeWhale/pull/5470))
- Model catalog currency sweep ([#5485](https://github.com/Hmbown/CodeWhale/pull/5485))
- DSH ambient ocean scene (whales + glyph fish) ([#5484](https://github.com/Hmbown/CodeWhale/pull/5484))
- Website copy de-slop ([#5483](https://github.com/Hmbown/CodeWhale/pull/5483))
- Changelog addenda with contributor credits for @h3c-hexin and @asto18089 ([#5477](https://github.com/Hmbown/CodeWhale/pull/5477), [#5487](https://github.com/Hmbown/CodeWhale/pull/5487))

**Note:** 0.9.9 tag (`ed39b0446`) unaffected by the rustdoc lint issue — all 7 targets built green.

---

## 3. Hot Issues

**#5424 — v0.9.7: Codewhale TUI crashing after ~1 minute** ([link](https://github.com/Hmbown/CodeWhale/issues/5424))
User reports clean crash after prompting and waiting ~60s. Closed, but no root cause summary visible. High severity for daily-driver users.

**#5403 — main red on both platforms across all four completed runs** ([link](https://github.com/Hmbown/CodeWhale/issues/5403))
Post-#5395, CI runs complete but are failing on macOS (plugin_e2e_acceptance) and Windows (NSIS provisioning). Maintainer treat as new information, not new breakage. Blocks release confidence.

**#5056 — Flaky verifier background tests + /workspace-sensitive fixtures; 12 untriaged #[ignore] tests** ([link](https://github.com/Hmbown/CodeWhale/issues/5056))
Verifier deamon tests still flake under full-suite parallelism; 12 ignored tests remain untriaged. A reliability debt that erodes trust in the test suite.

**#5123 — Agent spawn surface has too many knobs; labeled builder runs read-only and self-BLOCKED** ([link](https://github.com/Hmbown/CodeWhale/issues/5123))
The delegate builder session was labeled `builder` / `gates-shell-writer` but the live tool contract is read-only. The agent correctly self-BLOCKED. Exposes a contract mismatch between session labels and actual tool permissions.

**#5324 — 32-field agent schema: models keep erroring** ([link](https://github.com/Hmbown/CodeWhale/issues/5324))
The model-facing `agent` tool carries a 32-property JSON schema with zero required fields and 8 actions. Closed — model now errors less, but the complexity smell remains.

**#2369 — CodeWhale config paths fragmented across OS/Cygwin + silent migration bug** ([link](https://github.com/Hmbown/CodeWhale/issues/2369))
Windows/Cygwin home-directory rules diverge; legacy migration silently skips secrets. Long-lived bug (since May) with active community engagement and a patch attachment.

**#1425 — Large-text processing (3M-char novel) session freezes on agent_wait timeout** ([link](https://github.com/Hmbown/CodeWhale/issues/1425))
10 subagents all show `Running` but never complete; session interrupted. Subagent orchestration for large workloads is still fragile.

**#1829 — SSH connection fails: exit code 255 (TCP 22 outbound blocked by sandbox)** ([link](https://github.com/Hmbown/CodeWhale/issues/1829))
Windows 10 user cannot SSH from within the built-in shell sandbox. Local terminal works fine. Network sandboxing blocks legitimate workflows.

**#5355 — v0.9.8 known issues: parallel-load and config-fixture flakes** ([link](https://github.com/Hmbown/CodeWhale/issues/5355))
Carried-over investigation basket: `exec_persistent_service::failed_exec_*` and `exact_turn_snapshot_*` still flake under parallel load. Test-suite reliability is a recurring theme.

**#4683 — Wrong deepseek completions URL (flaky network error)** ([link](https://github.com/Hmbown/CodeWhale/issues/4683))
`https://api.deepseek.com/v1/chat/completions` fails intermittently after long asks. User reports it's flaky, needs-info flag active.

---

## 4. Key PR Progress

**#5465 — exec stream creation must fail soft, never wedge the shell tool** ([link](https://github.com/Hmbown/CodeWhale/pull/5465))
**Closed.** Root-cause fix for the 0.9.9 crash: memory-thrash on host caused every `bash` call to fail. Now fails soft and recovers. Critical reliability win.

**#5470 — DeepSeek V4 tiered peak/off-peak pricing resolved per turn** ([link](https://github.com/Hmbown/CodeWhale/pull/5470))
**Closed.** Replaces flat rate rows with UTC-hour tiered pricing resolved from each turn's timestamp. Pricing accuracy matters for cost-tracking users.

**#5474 — Compact all noisy web tool results** ([link](https://github.com/Hmbown/CodeWhale/pull/5474))
**Closed.** Community fix from @h3c-hexin: applies the noisy-result soft limit to `Web`, `web_search`, `web.run`, `fetch_url` while keeping hard limits for `read_file`. Context-bloat relief.

**#5475 — Resolve owned direct model casing safely** ([link](https://github.com/Hmbown/CodeWhale/pull/5475))
**Closed.** Community fix: lowercase selectors like `glm-5.2` resolve against owning catalog rows before foreign-classification. Prevents misrouting.

**#5473 — Keep configured skill prompts stable** ([link](https://github.com/Hmbown/CodeWhale/pull/5473))
**Open.** Community perf fix: native skills under configured roots list only name/description in model-facing catalog; replaces physical root with `<configured-skills>` placeholder.

**#5480 — Show/open live /rc session link; stable device id** ([link](https://github.com/Hmbown/CodeWhale/pull/5480))
**Closed.** The `/rc` banner now surfaces the live web session link and stops minting a new computer per `/rc`. Better remote-control UX.

**#5484 — DSH ambient ocean scene (whales + glyph fish)** ([link](https://github.com/Hmbown/CodeWhale/pull/5484))
**Closed.** Fun one: ambient ocean scene behind the DSH UI with whale silhouettes on bezier paths. Skin + scene only, no behavior change.

**#5483 — De-slop the site copy (voice sheet + rewritten surfaces)** ([link](https://github.com/Hmbown/CodeWhale/pull/5483))
**Closed.** Rewrites customer-visible copy on codewhale.net from internal-docs to product voice. Adds `WEB_VOICE.md` design reference.

**#5488 — Move docs shell onto the dictionary spine** ([link](https://github.com/Hmbown/CodeWhale/pull/5488))
**Open.** Fixes 5 `isZh` ternaries in the docs layout; 8 partial locales (ja/vi/ko/ru/uk/es/pt-BR/id) read English with no translation path. Part of the i18n dictionary spine (#4934). Companion: **#5490** routes shared-component locale picks through `pickText`.

**#5481 — Fix outdated A/B/C-tier references and stale anchors for v0.9.9** ([link](https://github.com/Hmbown/CodeWhale/pull/5481))
**Open.** Docs-only cleanup: A tier (contradicts code), B tier (stale), C tier (line-anchor drift). Docs hygiene for v0.9.9.

---

## 5. Feature Request Trends

1. **Simplified third-party model configuration** ([#5350](https://github.com/Hmbown/CodeWhale/issues/5350)) — Pre-built templates for OpenCode Zen/Go, Agnes, 美团 Sensenova; "test connection" button; fix cache loading. Chinese users especially want 1-minute setup.

2. **Full documentation localization to Chinese** ([#5482](https://github.com/Hmbown/CodeWhale/issues/5482)) — Large Chinese user base; many docs are English-only; machine translation introduces errors. Epic-sized request.

3. **Kimi-level plugin system and federated marketplaces** ([#5311](https://github.com/Hmbown/CodeWhale/issues/5311)) — Codewhale has solid plugin foundations but doesn't feel like a complete plugin product yet. V0.9.8 target.

4. **First-class screenshot/image viewing for agents** ([#5102](https://github.com/Hmbown/CodeWhale/issues/5102)) — Deliberate multimodal tool with compression/resizing, not incidental path luck. Modern harness requirement.

5. **MCP capability metadata** ([#4170](https://github.com/Hmbown/CodeWhale/issues/4170)) — Spec-compatible capability discovery so UI can distinguish tools without scraping prose.

6. **On-demand command help** ([#1708](https://github.com/Hmbown/CodeWhale/issues/1708), closed) — Agent needs reference to its own slash-commands (/mode, /config) instead of hallucinating from partial prompts.

---

## 6. Developer Pain Points

1. **Subagent orchestration is fragile** — Timeouts on large workloads ([#1425](https://github.com/Hmbown/CodeWhale/issues/1425)), contract mismatches between labels and actual permissions ([#5123](https://github.com/Hmbown/CodeWhale/issues/5123)), and config shadowing between layers ([#5098](https://github.com/Hmbown/CodeWhale/issues/5098)) are the top recurring theme.

2. **Test-suite reliability erodes trust** — Flaky verifier tests, parallel-load flakes, untriaged `#[ignore]` tests, and red CI on both platforms ([#5056](https://github.com/Hmbown/CodeWhale/issues/5056), [#5355](https://github.com/Hmbown/CodeWhale/issues/5355), [#5403](https://github.com/Hmbown/CodeWhale/issues/5403)). When the suite can't tell you green from red, you can't ship confidently.

3. **Config fragmentation across platforms** — Home-directory rules diverge between Windows/Cygwin; silent migration skips secrets ([#2369](https://github.com/Hmbown/CodeWhale/issues/2369)). Cross-platform consistency is a recurring pain.

4. **Network constraints in the shell sandbox** — SSH blocked (exit 255) and flaky API completions URLs ([#1829](https://github.com/Hmbown/CodeWhale/issues/1829), [#4683](https://github.com/Hmbown/CodeWhale/issues/4683)) interrupt legitimate workflows.

5. **Agent-facing schema complexity** — A 32-field schema with zero required fields and 8 actions errors out models ([#5324](https://github.com/Hmbown/CodeWhale/issues/5324)). Simpler contracts = fewer model failures.

6. **Crash-on-idle behavior** — v0.9.7 TUI crashes after ~1 minute of waiting ([#5424](https://github.com/Hmbown/CodeWhale/issues/5424)) and VS Code crashes during YOLO agent runs ([#1651](https://github.com/Hmbown/CodeWhale/issues/1651)). Stability regressions hit adoption hard.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/kky-wollu/agents-radar).*
# AI CLI Tools Community Digest 2026-08-08

> Generated: 2026-08-07 22:41 UTC | Tools covered: 9

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

# Cross-Tool AI CLI Comparison Report — 2026-08-08

---

## 1. Ecosystem Overview

The AI CLI developer tool landscape is rapidly consolidating around a common architecture: agentic coding assistants with MCP (Model Context Protocol) integration, sub-agent orchestration, and session-based workflows. The eight tools tracked here — Claude Code, OpenAI Codex, Gemini CLI, GitHub Copilot CLI, Kimi Code CLI, OpenCode, Pi, Qwen Code, and DeepSeek TUI — are converging on similar feature sets (skills/plugins, session persistence, multi-agent workflows) while differentiating on provider ecosystems, autonomy levels, and enterprise readiness. **Reliability and safety dominate the current community discourse**: silent data corruption (Kimi), destructive command execution (Kimi), resource leaks (Codex), and compaction failures (Pi, OpenCode) are the most emotionally charged issues, outweighing feature requests. Platform gaps persist, with **Windows sandboxing and rendering issues** appearing across Codex, Copilot CLI, Qwen Code, and OpenCode. The ecosystem is also seeing a shift toward **hybrid execution models** (Claude's self-hosted runners, Qwen's Web Shell, Pi's Cursor auth bridge) that blur the line between local CLI and cloud-managed services.

---

## 2. Activity Comparison

| Tool | Releases (24h) | Hot Issues (active) | PRs (24h) | Notable Release | Release Velocity |
|------|---------------|---------------------|-----------|-----------------|------------------|
| **Claude Code** | 1 stable | 10 tracked (2 new) | 3 | v2.1.224 — self-hosted runners, archive plugin source | Moderate (weekly stables) |
| **OpenAI Codex** | 1 stable + 2 alphas | 10 tracked | 10+ | rust-v0.147.0 — portable plugins, conversation sections | High (frequent stables + alphas) |
| **Gemini CLI** | 3 patches | 10 tracked | 10 merged | v0.54.4, v0.55.0-preview.2, v0.56.0-nightly | Very high (multi-track) |
| **Copilot CLI** | 3 patches | 10 tracked | 0 | v1.0.79-6 → -8 — sandbox policies, plugin extensions | High (multiple same-day releases) |
| **Kimi Code CLI** | 0 | 2 tracked | 2 (competing fixes) | (pending) | Low (stalled) |
| **OpenCode** | 1 stable | 10 tracked | 10 (1 open) | v1.18.15 — message chronology fixes | High (weekly stables) |
| **Pi** | 1 stable | 10 tracked | 10 (5 open) | v0.84.1 — Qwen token plan, auth checks | High (weekly stables) |
| **Qwen Code** | 1 stable + 1 nightly | 10 tracked | 10 | v0.21.7 — 50-turn limit removed, inline terminal images | Very high (daily builds) |
| **DeepSeek TUI** | 0 (release blocked) | 10 tracked | 10 | (v0.9.4 staged, CI-blocked) | Low (release friction) |

**Interpretation:**

- **High-velocity clusters**: Gemini CLI (3 releases/day), Qwen Code (daily builds), Copilot CLI (multi-patch days), OpenCode/Pi (weekly stables).
- **Stalled releases**: Kimi Code CLI (no release in 24h, competing fix PRs), DeepSeek TUI (fully staged but CI-blocked).
- **PR throughput leaders**: Gemini CLI (10 merged), Codex (10+), OpenCode/Pi/Qwen (10 each).
- **PR drought**: Copilot CLI (0 PRs in 24h), Claude Code (3 — all community).

---

## 3. Shared Feature Directions

| Theme | Tools | Specific Needs |
|-------|-------|----------------|
| **Session Continuity** | Claude (#13354, 191👍), Pi (#6879, #7020), DeepSeek (#5267), Copilot (#4251), Qwen (50-turn removal), OpenCode (#41102) | Graceful continuation past limits, compaction before overflow, honest "ending" signals, resume without OOM |
| **Skills/Plugin Organization** | Copilot (#1632, 23👍), OpenCode (#38853), Claude (archive plugins) | Subfolders for skills, local plugin catalogs, hierarchical organization |
| **MCP Robustness** | Claude (#37580, #70386), Codex (#12491), Copilot (#4392), Qwen (#8550), Gemini | Session-header preservation, process reaping, tilde expansion, SSE timeout handling |
| **Mid-turn / Multi-session Control** | DeepSeek (#5267–#5272), Qwen (turn-status endpoints), Pi (#7792), Gemini (Caretaker) | Queue/send-now semantics, session peeking, unified task views, polling turn status |
| **Model-level Hooks/Interception** | Claude (#21531), Pi (reasoning_content round-trip), DeepSeek (`/dryrun`) | BeforeModel/AfterModel interception, payload preview, reasoning-token echo |
| **Cross-Platform Parity** | Codex (Windows sandbox), Copilot (Windows clipboard/codepage), Qwen (Windows IME), OpenCode (Windows paste) | First-class Windows support, non-UTF-8 handling, tmux/SSH compatibility |
| **Provider Flexibility** | DeepSeek (#1481), Pi (#7762), OpenCode (Bedrock region prompt), Qwen (Kimi/MiMo auth) | OpenCode Go/Zen bridge, LM Studio local, model auto-selection (`model = auto`) |

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex | Gemini CLI | Copilot CLI | Kimi Code CLI | OpenCode | Pi | Qwen Code | DeepSeek TUI |
|-----------|-------------|--------------|------------|-------------|---------------|----------|-----|------------|--------------|
| **Primary Distribution** | npm, web/mobile/desktop | npm, VS Code, desktop | npm, nightly | GitHub-native, VS Code | npm | npm, desktop | npm | npm, desktop, Web Shell | npm |
| **Execution Model** | Hybrid cloud/on-prem (self-hosted runners) | Cloud (sandboxed) | Local + cloud | Cloud (GitHub) | Local | Cloud (Go plan) + local | Local-first | Local daemon + Web Shell | Local |
| **Enterprise Story** | Strong (Team/Enterprise plans, self-hosted) | Enterprise auth (OAuth issues) | Google Cloud integration | Strong (GitHub Enterprise, sandbox policies) | Weak (single incidents) | Weak (Go plan metering issues) | Weak (individual focus) | Moderate (Qwen OAuth) | Weak |
| **Windows Support** | Moderate (KVM bug) | **Weak** (sandbox ACL cluster) | Untested (no issues) | **Weak** (clipboard, codepage, title) | Untested | **Weak** (paste broken) | Moderate | **Weak** (IME, tmux flicker) | Untested |
| **Community Energy** | High (191👍 session issue) | High (74👍 OAuth issue) | High (eval framework) | Moderate (35👍 /app issue) | Low (safety incidents) | High (Go billing) | High (compaction theme) | **Very high** (150-comment OAuth issue) | Moderate (v0.9.5 batch) |
| **Differentiating Strength** | Hybrid execution, plugin ecosystem | Agent Plugins, MCP event subscriptions | Caretaker agent, evaluation framework | GitHub-native trust, sandbox policies | Safety hardening, byte-level edits | Go plan (cheap models), Code Mode | Harness recovery, `model = auto` | Web Shell, Goals (no turn limit), ACP | Mid-turn control, `/dryrun` transparency |

---

## 5. Community Momentum & Maturity

### Rapidly Iterating (daily/weekly releases, high PR throughput):
- **Gemini CLI** — 3 releases/day, large eval framework investment, Caretaker agent prototype. Most disciplined engineering cadence.
- **Qwen Code** — Daily builds, Web Shell consolidation, aggressive feature cadence (turn-status endpoints, WebBridge). Highest raw velocity.
- **OpenCode / Pi** — Weekly stables, healthy PR flow, mature session/harness architecture. Pi's harness recovery work (#7710) is foundational.
- **Copilot CLI** — High patch velocity but zero community PRs; release notes indicate internal velocity, not community contribution.

### Maturing with Friction:
- **Claude Code** — Moderate release cadence, but the community's top issue (session limits, 191👍) remains open. Self-hosted runners signal enterprise focus over community-driven features.
- **OpenAI Codex** — High release velocity, but most issues center on **Windows sandbox failures** and **performance regressions** — a reliability trust gap.
- **OpenCode** — Active community but **Go plan metering** issues (#38257, 45 comments) are damaging trust in the commercial layer.

### Stalled / Safety-Focused:
- **Kimi Code CLI** — No releases in 24h; two competing fix PRs for a data-corruption bug create maintainer decision burden. The `rm -rf` incident (#2596) is a **P0 trust crisis**.
- **DeepSeek TUI** — Release v0.9.4 is versioned but CI-blocked; the codebase's monolithic files (7,133-line `runtime_threads.rs`) signal maintenance debt.

### Engagement Signals:
| Metric | Highest | Lowest |
|--------|---------|--------|
| Issue reactions | Claude #13354 (191👍) | Qwen #3203 (150 comments) |
| PR throughput | Gemini (10 merged) | Copilot (0) |
| Release frequency | Gemini/Qwen (3/day) | Kimi (0) |

---

## 6. Trend Signals & Recommendations

### For Tool Developers:

1. **Session continuity is the #1 UX gap** — Every tool with long-running workflows (Claude, Pi, Qwen, Copilot) faces backlash over artificial limits, compaction failures, or resume OOMs. **Invest in preemptive compaction and graceful continuation** — it is the highest-ROI improvement.

2. **Windows is a credibility gap** — Codex, Copilot, and Qwen all have Windows-specific showstoppers. Given enterprise Mac/Linux dominance, Windows support appears deprioritized — but the visible failures (clipboard, codepage, sandbox ACL) erode cross-platform trust.

3. **MCP lifecycle management is unrefined** — Zombie processes (Codex 37GB leak), session-header drops (Claude), and SSE hangs (Qwen) are the top interop complaints. **Standardize on the MCP spec's lifecycle guarantees and add watchdogs for child processes**.

4. **Safety incidents require public response** — Kimi's `rm -rf` incident and Claude's KVM livelock both demand public postmortems. Silence (or "stale-close" patterns) frustrates the community; Codex's `create sandbox` ACL cluster has gone months without a fix.

5. **Auth/provider friction is uneven** — Codex's OAuth issuer validation (74👍), OpenCode's Go 401s, and Pi's Cursor bridge point to a need for **"bring your own auth"** patterns that bridge existing enterprise identity (GitHub, Google, Cursor) rather than forcing per-tool keys.

6. **The "Fable 5" pattern (Claude) and "reasoning_content round-trip" (Pi, OpenCode)** indicate **model-specific behavior is a growing support burden** — tools must abstract provider quirks rather than let them leak into user-facing bugs.

7. **Web Shell / remote control is the next frontier** — Claude's self-hosted runners, Qwen's Web Shell, and OpenCode's Go plan all push toward **browser-driven or remote-driven agent sessions**. Expect this to be the 2026Q4 battleground.

### For Developers Choosing a Tool:

| Use Case | Recommended Tool | Rationale |
|----------|-----------------|-----------|
| Enterprise, on-prem compliance | **Claude Code** (self-hosted runners) | Hybrid execution, Team/Enterprise plans |
| GitHub-native workflows | **Copilot CLI** | Sandbox policies, Enterprise integration (but avoid on Windows) |
| Cheap/flexible model mix | **OpenCode Go** (if billing stabilizes) or **DeepSeek TUI** (`model = auto`) | Cost efficiency, provider neutrality |
| Research/experimentation | **Gemini CLI** | Eval framework, nightly builds, Caretaker prototype |
| Community-driven OSS | **Pi** or **OpenCode** | Active PR flow, responsive maintainers |
| Multi-model, Web-first | **Qwen Code** | Web Shell, nightly cadence, no turn limits, WebBridge |

### Watch Items:

- **Kimi Code CLI** — Safety incident resolution (file-corruption fix decision) will set the tone for the tool's trust trajectory.
- **OpenCode Go** — Billing/metering integrity (401s, quota math) is a make-or-break commercial trust signal.
- **Codex Windows sandbox** — The `CreateProcessAsUserW` cluster has 3+ open issues; a fix is overdue.
- **Claude session limits** — Given 191👍, any progress on #13354 will be met with outsized community goodwill.

---

*Sources: Community digests for anthropics/claude-code, openai/codex, google-gemini/gemini-cli, github/copilot-cli, MoonshotAI/kimi-cli, anomalyco/opencode, earendil-works/pi, QwenLM/qwen-code, and Hmbown/DeepSeek-TUI on 2026-08-08.*

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

# Claude Code Skills Community Highlights Report

*Data as of 2026-08-08 | Source: github.com/anthropics/skills*

---

## 1. Top Skills Ranking

The most active discussions center on a cluster of related bug fixes to the `skill-creator` meta-skill, plus several notable new skill proposals.

### 1.1 `skill-creator` eval pipeline fixes (PR #1298, #1099, #1050, #1323, #1261)

**Status:** All open

These five PRs target the same systemic defect: `run_eval.py` (and its consumers `run_loop.py`, `improve_description.py`) report **recall=0% on every query**, rendering the description-optimization loop useless. The root causes identified across PRs:

- **Windows subprocess incompatibility** — `claude.cmd` isn't resolved via `PATHEXT` (#1050, #1099); stream reading from pipes fails with `WinError 10038` (#1298, #1099)
- **Trigger detection logic** — misses the real skill name; bails on the first non-Skill tool call (#1323)
- **Eval command-file pollution** — synthetic `{skill}-skill-{hex}.md` files written into the user's **live project** `.claude/commands/`, causing concurrent-session interference (#1261)

**Discussion highlights:** This has 10+ independent reproductions (Issue #556, 7 👍). The community is clearly prioritizing tooling reliability over new skills — the optimizer "is currently optimizing against noise" (PR #1298). Interesting: three separate Windows-specific fixes (#1050, #1099, #1298) indicate the maintainers lack Windows CI.

**Links:** [#1298](https://github.com/anthropics/skills/pull/1298) · [#1323](https://github.com/anthropics/skills/pull/1323) · [#1261](https://github.com/anthropics/skills/pull/1261) · [#1099](https://github.com/anthropics/skills/pull/1099) · [#1050](https://github.com/anthropics/skills/pull/1050)

---

### 1.2 `document-typography` skill (PR #514)

**Author:** PGTBoos | **Status:** Open

A new skill for **typographic quality control** in AI-generated documents: orphan word wrap, widow paragraphs, and numbering misalignment.

**Discussion highlights:** The author's framing is compelling — "These issues affect every document Claude generates. Users rarely ask for good typography, but they notice when it's absent." The skill is positioned as a universal post-processing step, not a domain-specific tool.

**Why it stands out:** It's not a new document *format* skill (the repo already has PDF, DOCX, ODT) but a *quality* skill that works across formats.

**Link:** [PR #514](https://github.com/anthropics/skills/pull/514)

---

### 1.3 PDF case-sensitivity fix (PR #538)

**Author:** Lubrsy706 | **Status:** Open

Fixes 8 case-sensitivity mismatches in `skills/pdf/SKILL.md` where uppercase `REFERENCE.md`/`FORMS.md` references break on case-sensitive filesystems.

**Discussion highlights:** Small but critical reliability fix — broken references mean the skill silently fails on Linux/macOS. Along with #541 (DOCX `w:id` collision), the same author is systematically hardening document-skill edge cases. These are **low-glamour, high-impact** fixes.

**Link:** [PR #538](https://github.com/anthropics/skills/pull/538) · Companion: [PR #541](https://github.com/anthropics/skills/pull/541)

---

### 1.4 `self-audit` skill (PR #1367)

**Author:** YuhaoLin2005 | **Status:** Open

A **reasoning quality gate** skill: mechanical file verification first (every claimed output file exists), then a four-dimension reasoning audit in damage-severity priority order. Universal across projects/tech stacks/models.

**Discussion highlights:** The author has a companion proposal (Issue #1385) for a three-gate pipeline (pre-task calibration → adversarial review → delivery verification), positioning `self-audit` as one gate. The two-gate design (mechanical-then-reasoning) is a deliberate response to LLM hallucination of deliverable artifacts.

**Link:** [PR #1367](https://github.com/anthropics/skills/pull/1367) · Companion: [Issue #1385](https://github.com/anthropics/skills/issues/1385)

---

### 1.5 `color-expert` skill (PR #1302)

**Author:** meodai | **Status:** Open

A self-contained color-expertise skill: color naming systems (ISCC-NBS, Munsell, XKCD, RAL, Ridgway 1912), color spaces with a "what to use when" table (OKLCH for scales, OKLAB for gradients, CAM16 for perceptually-uniform), and the underlying theory.

**Discussion highlights:** Not the highest-comment PR, but notable for its **elegant scoping** — narrow enough to be genuinely expert, broad enough to apply across design, data-viz, and theming tasks. The author (meodai, maintainer of color.js) brings real domain authority.

**Link:** [PR #1302](https://github.com/anthropics/skills/pull/1302)

---

### 1.6 `plan-file-hygiene` skill (PR #1479)

**Author:** tonydzi | **Status:** Open

Addresses planning-artifact accumulation: plans, specs, and design docs pile up with no lifecycle. The skill adds hygiene discipline — when to archive, prune, or consolidate planning artifacts.

**Discussion highlights:** Emerged from Issue #1417 and credits prior community framing. This is a **meta-engineering-process** skill — it doesn't do a task, it maintains the agent's own workspace. Signals a maturing community that's now managing long-running agent sessions.

**Link:** [PR #1479](https://github.com/anthropics/skills/pull/1479) · [Issue #1417](https://github.com/anthropics/skills/issues/1417)

---

## 2. Community Demand Trends

### 2.1 Noise: Trust boundary integrity (Issue #492, 43 comments — highest in repo)

**The community's loudest concern is security.** Community skills distributed under the `anthropic/` namespace impersonate official skills, creating a trust-boundary vulnerability where users grant elevated permissions to what they believe is official Anthropic code.

**What this means:** The Skills ecosystem is experiencing a **supply-chain trust crisis** — the equivalent of a typosquatting problem, but at the *namespace* level. Demand: official namespacing, provenance, or certification.

[Issue #492](https://github.com/anthropics/skills/issues/492) | [Issue #1175](https://github.com/anthropics/skills/issues/1175) (SharePoint document access-control, 4 comments) reinforces this — enterprise users asking how to put permissions *inside* SKILL.md, a misuse being redirected.

### 2.2 Org-wide sharing and distribution (Issue #228, 16 comments, 8 👍)

**Enterprise adoption blocker.** Users can't share skills org-wide within Claude.ai; they must download `.skill` files and Slack them to colleagues who manually upload them. Demand: a shared skill library or sharing links.

**Cluster:** Issue #189 (6 comments, 9 👍) — `document-skills` and `example-skills` plugins contain **identical skills** causing duplicates in the context window. Distribution is a top-3 pain.

[Issue #228](https://github.com/anthropics/skills/issues/228) | [Issue #189](https://github.com/anthropics/skills/issues/189)

### 2.3 Reliability engineering > new features

The `skill-creator` eval bug (Issue #556, 12 comments, 7 👍; Issue #1169, 3 comments) shows the community's #1 pain is **broken tooling**, not missing capabilities. Three separate Windows-specific fixes (#1050, #1099, #1298) mean the ecosystem's flagship SDK is unusable on a major OS.

### 2.4 Context-window hygiene (Issue #1487, 4 comments)

The `claude-api` skill **eagerly injects ~156k tokens** in a single tool call, exhausting the context window. Community is hitting the limits of eager-injection skills and demanding lazy-loading patterns.

[Issue #1487](https://github.com/anthropics/skills/issues/1487) | [Issue #12](https://github.com/anthropics/skills/issues/12) (docx whitespace reformatting corruption, 4 comments)

### 2.5 Execution-focused meta-skills

Issue #202 (8 comments, closed) criticizes `skill-creator` for being "developer documentation, not an operational skill." The community wants skills that **instruct Claude**, not explain to humans. Note the irony: the same repo's Issues are the main channel for skills-as-proposals (#412 agent-governance, #1329 compact-memory) — the community itself is using the issue tracker as a discovery mechanism.

---

## 3. High-Potential Pending Skills

These active-comment PRs may land soon:

| Skill | PR | Notes |
|---|---|---|
| **skill-creator eval fixes** | [#1298](https://github.com/anthropics/skills/pull/1298) | Highest-attention PR; multiple authors converging on same bug. Expected: merged fix (likely a combination). |
| **document-typography** | [#514](https://github.com/anthropics/skills/pull/514) | Strong framing, clear value prop, cross-format applicability. |
| **self-audit** | [#1367](https://github.com/anthropics/skills/pull/1367) | Author pushing companion proposal (#1385) — visible momentum. |
| **color-expert** | [#1302](https://github.com/anthropics/skills/pull/1302) | Authoritative domain knowledge, clean scope. |
| **ODT skill** | [#486](https://github.com/anthropics/skills/pull/486) | OpenDocument creation/template-filling/parse-to-HTML — fills a format gap (LibreOffice universe). Low comments but active since March. |
| **pyxel skill** | [#525](https://github.com/anthropics/skills/pull/525) | Retro-game dev via MCP server; niche but active since March. |
| **plan-file-hygiene** | [#1479](https://github.com/anthropics/skills/pull/1479) | Newest; addresses long-running-agent pain. |
| **testing-patterns** | [#723](https://github.com/anthropics/skills/pull/723) | Comprehensive testing stack (Trophy model, React Testing Library) — surprisingly low engagement for a high-value domain. |

Notably absent from PRs: **no Windows-specific skills, no org-governance skills** (those exist only as Issues) — the PR pipeline is dominated by document/design skills and tooling fixes.

---

## 4. Skills Ecosystem Insight

**The community's most concentrated demand is for trust and reliability — canonical security boundaries, provenance, and working tooling — rather than for new domain capabilities**, with the highest-attention artifacts being the skill-creator eval-pipeline fixes (5 PRs) and the trust-boundary issue (43 comments), both reflecting a user base that has moved past "what can skills do?" to "can I trust what skills do?".

---

*Report generated 2026-08-08. Data: github.com/anthropics/skills PRs & Issues (top 50 each, sorted by comments).*

---

# Claude Code Community Digest — 2026-08-08

---

## 1. Today's Highlights

The big story this week is **v2.1.224**, which introduces `claude self-hosted-runner` — turning your own infrastructure into execution targets for Claude Code web, mobile, and desktop sessions (Team/Enterprise plans). This is a major architectural shift toward hybrid cloud/on-prem execution. Meanwhile, the community's most-voted feature request (**#13354**, 191 👍) — the ability to continue working when the session limit is reached — remains open and is clearly the top friction point for power users. The issue tracker also shows a large sweep of stale documentation issues being closed, suggesting the team is doing a docs cleanup pass tied to recent feature releases.

---

## 2. Releases

**v2.1.224** — The headline feature is **self-hosted runners** (`claude self-hosted-runner`), enabling Claude Code sessions from web, mobile, and desktop to execute on your own machines or containers. This is available on Team and Enterprise plans. The release also adds an **`archive` plugin source**, letting you install plugins from a zip over HTTPS without requiring git.

📦 https://github.com/anthropics/claude-code/releases

---

## 3. Hot Issues (10 noteworthy)

1. **[#13354 — Continue when the session limit reached](https://github.com/anthropics/claude-code/issues/13354)** — *OPEN, 73 comments, 191 👍*  
   The single most-upvoted open feature request. Users hit hard session caps in long workflows and want a graceful continuation path rather than forced context resets. The 191 reactions signal this is a top-3 pain point for the community.

2. **[#81853 — Fable 5: text in a response that also contains tool calls is never displayed](https://github.com/anthropics/claude-code/issues/81853)** — *OPEN, 5 comments, 3 👍*  
   A model-specific rendering bug where mixed text+tool-call responses from `claude-fable-5` hide the text in the main TUI view (visible only in the detailed transcript via Ctrl+O). Works fine with Opus 4.8. Notably, this is the *new* model — if Fable 5 is the future, this bug is a blocker for everyday use.

3. **[#70165 — iOS app hard-crashes opening Remote Control sessions (stack overflow in Swift KeyPath metadata)](https://github.com/anthropics/claude-code/issues/70165)** — *CLOSED, 10 comments*  
   A severe regression in iOS 1.260618.0 that crashed on main-thread during Remote Control session open. Marked stale/closed now, but the underlying Swift metadata stack overflow was concerning — and the "closed without visible fix note" pattern will frustrate affected users.

4. **[#21531 — BeforeModel and AfterModel hooks for LLM request/response interception](https://github.com/anthropics/claude-code/issues/21531)** — *CLOSED, 9 comments*  
   The most-requested **hook** extension. Users want model-level interception for cost tracking, logging, and policy enforcement — not just tool-level hooks. Closed as stale, which suggests the team is either building it internally or not prioritizing it.

5. **[#37580 — MCP server args with `~` fail with ENOENT — tilde not expanded in stdio args](https://github.com/anthropics/claude-code/issues/37580)** — *CLOSED, 7 comments*  
   Legit bug: `~` in MCP server `args` isn't shell-expanded before spawn, breaking common configs like `~/.local/bin/...`. Marked stale/closed — a small but annoying papercut for MCP users.

6. **[#77372 — Remote Control: stale environments cannot be deleted; ghost sessions cause permanent 404s](https://github.com/anthropics/claude-code/issues/77372)** — *OPEN, 3 comments*  
   An active, reproducible bug where freshly registered environments immediately 404 on session attach with *different* session IDs. Points to a deeper state-management issue in the Remote Control worker-attach path — exactly the kind of thing that erodes trust in the new self-hosted runner feature.

7. **[#77208 — Claude Code ≥ 2.1.205 livelocks at 100% CPU on KVM guests (kvm64 CPU model)](https://github.com/anthropics/claude-code/issues/77208)** — *OPEN, 3 comments*  
   A regression that breaks even `--version` on generic KVM VMs (common in CI and cloud). Silently breaks the Linux desktop beta Code tab too. High severity for anyone running Claude Code in VMs.

8. **[#64503 — Claude Code Analytics not updated since May 12](https://github.com/anthropics/claude-code/issues/64503)** — *CLOSED, 5 comments, 6 👍*  
   Analytics dashboards went dark for ~2 months. Closed as stale — but the 6 👍 on a data-availability bug shows real demand for usage visibility.

9. **[#70458 — Safety check flagging obviously-safe prompts](https://github.com/anthropics/claude-code/issues/70458)** — *CLOSED, 4 comments*  
   Overzealous safety filtering — the user was merely telling the model to skip reading a folder. False-positive safety blocks are a growing irritation in the community.

10. **[#70386 — HTTP MCP client drops `Mcp-Session-Id` header — breaks session-aware servers](https://github.com/anthropics/claude-code/issues/70386)** — *CLOSED, 2 comments*  
    Streamable-HTTP MCP servers (mcp-grafana, mcp-go) that require `Mcp-Session-Id` echo fail on `tools/list` despite showing "✓ Connected". Interop gap with the broader MCP ecosystem.

---

## 4. Key PR Progress

Note: only **3 PRs** were updated in the last 24h — the queue is light, and all three are from community contributors.

1. **[#84854 — docs: fix stale hooks documentation link in `bash_command_validator_example.py`](https://github.com/anthropics/claude-code/pull/84854)**  
   Mechanical but useful: updates the last remaining `docs.anthropic.com` URL to `code.claude.com/docs` across the repo. Keeps example code pointing at the right docs.

2. **[#84747 — fix(hookify): enforce proper rule evaluation scope and secure file read](https://github.com/anthropics/claude-code/pull/84747)**  
   Security fix for the `hookify` plugin: `load_rules()` was bypassing the event filter when `event` is `None`, causing tools like `Read` and `Browser` (not explicitly mapped to an event) to incorrectly trigger `all`-scoped rules. Prevents rule leakage across tools.

3. **[#84711 — fix(security): address yaml injection and symlink credential overwrites in plugin scripts](https://github.com/anthropics/claude-code/pull/84711)** — fixes #76580  
   Defensive hardening against YAML injection and symlink-based credential overwrite attacks in plugin scripts. This is the kind of supply-chain hardening the plugin ecosystem needs as it grows.

---

## 5. Feature Request Trends

- **Session continuity is the #1 ask.** The 191-upvote issue (#13354) to continue past session limits dwarfs everything else. Users want long-running work without artificial resets.
- **Hooks expansion is a close second.** Requests for BeforeModel/AfterModel interception (#21531), plus an RFC for **async/event-driven agent communication** (#55981), show the community wants deeper programmatic control over the agent lifecycle — not just tool-level hooks.
- **Docs are a recurring theme.** A wave of ~25 documentation issues (mostly from `coygeek`) were closed as stale this cycle — covering hooks reference completeness, AWS Bedrock timeout behavior, MCP binary output handling, permission picker behavior, and more. The volume suggests either a docs overhaul is coming, or the team is deprioritizing community doc contributions.
- **MCP ecosystem interop.** Tilde-expansion bugs (#37580), session-header drops (#70386), and binary output handling all point to MCP as a hot integration surface where edge cases keep surfacing.

---

## 6. Developer Pain Points

- **Session limits interrupt flow** — the 191 👍 on #13354 is the strongest signal in the tracker.
- **Remote Control reliability** — two actively-open bugs (#77372, #70165) around session attach, stale environments, and iOS crashes undermine confidence in the remote/mobile story right as self-hosted runners launch.
- **MCP configuration friction** — tilde expansion failures and session-header drops are small but persistent annoyances that break "it just works" expectations.
- **Safety-filter false positives** — users increasingly report the safety layer blocking innocuous prompts (#70458), which feels worse than a false negative.
- **Performance regressions in edge environments** — the KVM livelock (#77208) is a reminder that generic-CPU VMs (CI runners, cloud VMs) are a real deployment target, and CPU-specific regressions there break automation silently.
- **Stale-closure pattern frustrates bug reporters** — many bugs with solid repros (iOS crash #70165, tilde ENOENT #37580, MCP header drop #70386) are closed as "stale" without visible resolution notes, leaving users unsure whether fixes shipped.

---

*Digest generated from anthropics/claude-code GitHub activity on 2026-08-08.*

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-08-08

## Today's Highlights

The Codex team shipped **rust-v0.147.0** with portable Agent Plugins and persistent conversation organization, while prepping **0.148.0 alphas** for early testing. Community attention remains concentrated on a **critical Windows sandbox failure cluster** (`CreateProcessAsUserW failed: 5`) and a **performance regression** that has the most-commented open issue at 41 comments. A significant batch of infrastructure PRs landed around skills, diagnostics, and MCP event subscriptions, signaling continued platform maturation.

---

## Releases

### rust-v0.147.0 (Stable)
- **Portable Agent Plugins**: Install and search across local, personal, workspace, and remote plugin catalogs.
- **Persistent conversation sections**: Organize threads into manually ordered sections; browse long transcripts incrementally.

### rust-v0.148.0-alpha.1 / alpha.2
- Early alpha releases; no feature notes published yet.

---

## Hot Issues (Top 10)

1. **[#21527 — Codex is really too slow](https://github.com/openai/codex/issues/21527)** — *41 comments, 18 reactions*. Long-standing performance complaint affecting both VS Code plugin and desktop app. High engagement signals this is the community's #1 pain point.

2. **[#31573 — OAuth authentication fails at issuer validation](https://github.com/openai/codex/issues/31573)** — *34 comments, 74 reactions*. Free-tier users blocked from CLI sign-in. The 74 upvotes make this among the most-flagged auth bugs.

3. **[#12491 — MCP child processes not reaped (1300+ zombies, 37GB leak)](https://github.com/openai/codex/issues/12491)** — *38 comments, 5 reactions*. Severe resource leak in the desktop app; closed, but the scale of the leak underscores MCP lifecycle fragility.

4. **[#35481 — Codex Diff shows "Oops, an error has occurred" in VS Code](https://github.com/openai/codex/issues/35481)** — *26 comments, 54 reactions*. Windows-specific diff view failure with broad user impact; closed but highly upvoted.

5. **[#10090 — Elevated Windows sandbox fails all agent commands](https://github.com/openai/codex/issues/10090)** — *23 comments, 7 reactions*. `CreateProcessAsUserW failed: 5` blocks all agent commands; tied to the wider Windows sandbox ACL problem.

6. **[#37380 — 0.147.0 regression: Azure Responses rejects empty functions namespace](https://github.com/openai/codex/issues/37380)** — *8 comments, 18 reactions*. New in 0.147.0; breaks Azure OpenAI custom provider users immediately after upgrade.

7. **[#37425 — Regression in v0.147.0: LiteLLM streaming consistently fails](https://github.com/openai/codex/issues/37425)** — *4 comments, 2 reactions*. Second 0.147.0 regression reported in one day; points to a provider-compat change in the release.

8. **[#14599 — Allow trust_level = "trusted" for any projects](https://github.com/openai/codex/issues/14599)** — *16 comments, 57 reactions*. Persistent approval prompts frustrate users; strong demand for per-project trust override.

9. **[#36523 — macOS app OOM-crashes parsing 1.73GB from Claude Desktop](https://github.com/openai/codex/issues/36523)** — *3 comments, 1 reaction*. P0 regression: external-agent-import parses Claude Desktop directory on every launch, crashing with V8 OOM.

10. **[#37445 — Desktop app silently consumes weekly limit (6% per background run)](https://github.com/openai/codex/issues/37445)** — *4 comments, 0 reactions*. Background suggestions drain fixed quota without user action; new and rapidly gaining tracker attention.

---

## Key PR Progress (Top 10)

1. **[#37507 — Include sandbox mode in response metadata](https://github.com/openai/codex/pull/37507)** — Adds effective permission profile to turn metadata; reserves `sandbox_mode` to prevent client override.

2. **[#37494 — Add MCP event discovery and subscriptions](https://github.com/openai/codex/pull/37494)** — Exposes Plugin Runtime event definitions and cancellable `events/stream` subscriptions; routes lifecycle notifications to matching requests.

3. **[#37485 — Keep response streams alive through connection failures](https://github.com/openai/codex/pull/37485)** — Retries HTTP connection failures with backoff (5–60s) and surfaces a `Reconnecting...` UI state; key for flaky networks.

4. **[#37498 — Preserve child waiters during process termination](https://github.com/openai/codex/pull/37498)** — Fixes unreaped PTY child processes by detaching (not aborting) child waiters; directly addresses zombie-process issues like #12491.

5. **[#37480 — Delegate remote process sandboxing to the executor](https://github.com/openai/codex/pull/37480)** — Resolves sandbox config on the remote executor, not the host; important for consistent cross-platform remote behavior.

6. **[#37489 — Alias resource-backed skill locators under context pressure](https://github.com/openai/codex/pull/37489)** — Adds source-aware root aliases so long executor/orchestrator resource IDs don't starve the skills context budget.

7. **[#37477 — Include call IDs in MCP requests](https://github.com/openai/codex/pull/37477)** — Adds `_meta.callId` to MCP tool calls; renames metadata config flag for clearer semantics.

8. **[#37486 — Expose runtime activity in server diagnostics](https://github.com/openai/codex/pull/37486)** — Lifecycle-backed gauges for in-flight requests, active turns, and live MCP connections; improves observability.

9. **[#37504 — Disable Nagle's algorithm for code-mode WebSockets](https://github.com/openai/codex/pull/37504)** — Enables `TCP_NODELAY` to cut latency on remote-session WebSocket traffic; small but impactful for responsiveness.

10. **[#37497 — Limit payload traces in diagnostic logs](https://github.com/openai/codex/pull/37497)** — Downgrades HTTP/SSE/WebSocket payload logs to DEBUG to prevent SQLite log DB and diagnostic ring-buffer bloat.

---

## Feature Request Trends

- **Plugin ecosystem expansion** — Portable Agent Plugins and MCP event subscriptions point to growing demand for third-party tooling integration.
- **Persistent conversation UX** — Users want better thread organization, incremental browsing, and resumable sessions without full-history re-render.
- **Longer context windows** — Explicit asks (e.g., **#28852 — 1M context**) for flagship models to support sustained, large-scale engineering work.
- **Trust/permission management** — Recurring requests for persistent trust levels (**#14599**) and fewer approval prompts.
- **Cross-platform parity** — Heavy Windows/macOS-specific issues show desire for first-class support beyond Linux/macOS defaults.

---

## Developer Pain Points

- **Windows sandbox reliability** — The `CreateProcessAsUserW failed: 5` cluster (issues #10090, #13965, #14211, #35718) remains the most recurring showstopper: failed ACL setup blocks all agent commands, breaks `apply_patch`, and survives uninstall/reinstall.
- **Release regressions** — Both #37380 (Azure) and #37425 (LiteLLM) were introduced by 0.147.0, breaking streaming/custom providers with no warning. Third-party provider users are especially exposed.
- **Resource leaks and lifecycle bugs** — Unreaped MCP processes (37GB leak), duplicate process stacks on resume, and per-launch over-parsing of external agent imports (1.73GB) signal insufficient lifecycle management in the desktop app.
- **Rate-limit transparency** — Background app activity silently consuming weekly quotas (#37445, #37442) undermines user trust in quota accounting.
- **TUI/session resume performance** — Resuming long threads re-renders full history instead of bootstrapping the latest turn (**#34663**), degrading interactive use at scale.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-08-08

## Today's Highlights

Three patch releases (v0.54.4, v0.55.0-preview.2, and v0.56.0-nightly) shipped today with stability fixes. Security takes center stage with two critical PRs addressing an SSRF vulnerability (CVSS 8.6) in `web-fetch` and a Node 20 EOL sandbox upgrade. The Caretaker agent prototype continues rapid maturation, with a large batch of evaluation framework PRs merged and a handoff issue listing remaining work.

## Releases

Three versions released in the last 24 hours:

- **[v0.56.0-nightly.20260807.gd5c9a97dc](https://github.com/google-gemini/gemini-cli/releases/tag/v0.56.0-nightly.20260807.gd5c9a97dc)** — Nightly build including changelog updates and version bumps.
- **[v0.55.0-preview.2](https://github.com/google-gemini/gemini-cli/releases/tag/v0.55.0-preview.2)** — Cherry-pick fix (2139b12) applied to the preview.1 release line.
- **[v0.54.4](https://github.com/google-gemini/gemini-cli/releases/tag/v0.54.4)** — Cherry-pick fix (56f9688) applied to the stable v0.54 line.

All three are patch-level fixes; no new feature releases today.

## Hot Issues

1. **[#22323 — Subagent recovery after MAX_TURNS reported as GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)** — Critical bug where `codebase_investigator` subagent reports `status: "success"` even after hitting max turn limits without doing any analysis. This masks interruptions and could lead to false confidence in agent outputs. 12 comments; P1 priority.

2. **[#21409 — Generalist agent hangs indefinitely](https://github.com/google-gemini/gemini-cli/issues/21409)** — The generalist agent hangs forever on simple tasks (even folder creation), requiring up to an hour of waiting before cancellation. Users report that instructing the model to avoid sub-agents resolves the issue. High community impact with 8 reactions.

3. **[#24353 — Robust component-level evaluations (EPIC)](https://github.com/google-gemini/gemini-cli/issues/24353)** — Tracks the expansion of the behavioral eval suite from 76 tests across 6 Gemini models. Signals a growing commitment to systematic agent quality measurement.

4. **[#22745 — AST-aware file reads, search, and mapping (EPIC)](https://github.com/google-gemini/gemini-cli/issues/22745)** — Investigation into whether AST-aware tools can reduce token noise, cut turns from misaligned reads, and improve codebase mapping precision.

5. **[#21968 — Gemini doesn't use skills and sub-agents enough](https://github.com/google-gemini/gemini-cli/issues/21968)** — Anecdotal but important: custom skills and sub-agents are only used when explicitly instructed. Users with well-described skills (gradle, git) find the agent ignores them for related tasks.

6. **[#26522 — Auto Memory retries low-signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522)** — Memory extraction agent can re-surface the same low-signal sessions repeatedly if it decides not to read them, wasting resources and potentially surfacing irrelevant context.

7. **[#25166 — Shell command stuck with "Waiting input" after completion](https://github.com/google-gemini/gemini-cli/issues/25166)** — P1 bug where the CLI hangs after executing simple commands, showing them as active and awaiting input indefinitely. Affects basic workflows; 3 reactions.

8. **[#28713 — Caretaker agent completion handoff](https://github.com/google-gemini/gemini-cli/issues/28713)** — Closed issue listing remaining open PRs for the Caretaker agent prototype, including Firestore schema updates, Cloud Workflows orchestration, and Pub/Sub event publishing.

9. **[#26525 — Add deterministic redaction and reduce Auto Memory logging](https://github.com/google-gemini/gemini-cli/issues/26525)** — Security concern: Auto Memory sends transcript content to the extraction model before redaction occurs, and the service may log existing skill content. P2 security priority.

10. **[#21983 — Browser subagent fails on Wayland](https://github.com/google-gemini/gemini-cli/issues/21983)** — Browser agent fails with `Termination Reason: GOAL` on Wayland sessions. P1 bug affecting Linux users with modern display servers.

## Key PR Progress

1. **[#28673 — Add Gemini 3.6 Flash and 3.5 Flash-Lite model configurations](https://github.com/google-gemini/gemini-cli/pull/28673)** — Adds support for new model variants in `packages/core`, including capabilities, aliases, and Code Execution configuration.

2. **[#28730 — Resolve false model capacity exhaustion and fix quota lookup mapping](https://github.com/google-gemini/gemini-cli/pull/28730)** — Fixes misleading "capacity exhausted" errors and corrects client-side quota lookup. Preserves the "Keep trying" UI option during transient surges.

3. **[#28597 — Load environment variables before resolving settings placeholders](https://github.com/google-gemini/gemini-cli/pull/28597)** — Fixes a load-order race condition where `.env` files weren't loaded before settings expansion, causing placeholder resolution failures.

4. **[#28729 — Resolve swallowed directory mismatch in IDE connections](https://github.com/google-gemini/gemini-cli/pull/28729)** — Fixes CLI-IDE companion connection failures under Cider and VS Code forks using virtual/FUSE directory paths.

5. **[#28725 — Prevent SSRF via DNS resolution bypass in web-fetch](https://github.com/google-gemini/gemini-cli/pull/28725)** — Critical security fix (CVSS 8.6): closes a vulnerability where malicious domains could point to private/loopback IPs (e.g., `169.254.169.254`).

6. **[#28726 — Upgrade sandbox Dockerfile to node:22-slim](https://github.com/google-gemini/gemini-cli/pull/28726)** — Security-hardening: moves sandbox and Caretaker Cloud Run containers off Node 20 (EOL, no longer receiving security patches).

7. **[#28581 — Skip diff hunk markers during @ processing](https://github.com/google-gemini/gemini-cli/pull/28581)** — Performance fix: prevents diff hunk markers from triggering recursive workspace-wide glob searches, eliminating `minimatch`/`path-scurry` heap growth on large diffs.

8. **[#28369 — Add local report command and developer documentation](https://github.com/google-gemini/gemini-cli/pull/28369)** — Adds `npm run eval:report` to aggregate pass rates by model from Vitest `report.json` files, with developer guide for behavioral evaluations.

9. **[#28344 — Add eval:validate static analysis command](https://github.com/google-gemini/gemini-cli/pull/28344)** — CI-gating tool that validates eval source files against 9 rules, exiting with code 1 on violations.

10. **[#28690 — Add issue comment handling and re-triage workflow](https://github.com/google-gemini/gemini-cli/pull/28690)** — Caretaker agent enhancement: processes `issue_comment.created` webhooks, enabling `@caretaker-agent` mentions and `/caretaker triage` commands to trigger re-triage on `NEEDS_INFO` issues.

## Feature Request Trends

- **AST-aware code tooling**: Multiple issues ([#22745](https://github.com/google-gemini/gemini-cli/issues/22745), [#22746](https://github.com/google-gemini/gemini-cli/issues/22746)) explore AST-aware file reads, search, and mapping to reduce token waste and improve precision.
- **Sub-agent/skill self-activation**: Users want the agent to autonomously invoke relevant skills and sub-agents ([#21968](https://github.com/google-gemini/gemini-cli/issues/21968)) rather than only using them when explicitly instructed.
- **Better sub-agent observability**: Requests for sub-agent trajectories to be visible via `/chat share` ([#22598](https://github.com/google-gemini/gemini-cli/issues/22598)) and for `/bug` reports to include sub-agent context ([#21763](https://github.com/google-gemini/gemini-cli/issues/21763)).
- **Agent safety guardrails**: Feature requests to discourage destructive commands and understand modification risks ([#22672](https://github.com/google-gemini/gemini-cli/issues/22672)).
- **Browser agent resilience**: Requests for automatic session takeover and lock recovery in persistent profile mode ([#22232](https://github.com/google-gemini/gemini-cli/issues/22232)).

## Developer Pain Points

1. **Agent hangs and stalls**: The generalist agent hanging for hours ([#21409](https://github.com/google-gemini/gemini-cli/issues/21409)) and shell commands stuck on "Waiting input" ([#25166](https://github.com/google-gemini/gemini-cli/issues/25166)) represent the most disruptive issues, halting workflows entirely.

2. **Misleading success reporting**: Subagents reporting `GOAL` success despite hitting turn limits ([#22323](https://github.com/google-gemini/gemini-cli/issues/22323)) undermines trust in agent results and masks underlying failures.

3. **Configuration and permission inconsistencies**: Sub-agents running despite being disabled in configs ([#22093](https://github.com/google-gemini/gemini-cli/issues/22093)) and settings.json overrides being ignored ([#22267](https://github.com/google-gemini/gemini-cli/issues/22267)) reveal gaps between configuration intent and runtime behavior.

4. **Tool-overflow errors**: Encountering 400 errors with more than 128 tools available ([#24246](https://github.com/google-gemini/gemini-cli/issues/24246)) suggests the tool selection strategy doesn't scale with user-configured toolsets.

5. **Auto Memory reliability and security**: Indefinite retries on low-signal sessions ([#26522](https://github.com/google-gemini/gemini-cli/issues/26522)) and pre-redaction content exposure ([#26525](https://github.com/google-gemini/gemini-cli/issues/26525)) raise both efficiency and privacy concerns.

6. **Workspace pollution**: Models creating temporary scripts in random directories ([#23571](https://github.com/google-gemini/gemini-cli/issues/23571)) creates cleanup overhead and complicates clean commits.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest - 2026-08-08

## Today's Highlights

Three rapid-fire releases (v1.0.79-6 through v1.0.79-8) shipped within 24 hours, bringing enterprise sandbox policy enforcement, Agent Plugins extensions support, and a new kimi-k3 model option alongside several stability fixes. The community continues to surface Windows-specific rendering and clipboard bugs, while a notable new feature request with 35 👍 asks for `/app` to default to the current working directory. Several triage-level issues around MCP process management and skill discovery indicate growing pains as the plugin ecosystem matures.

---

## Releases

**v1.0.79-8**
- **Added:** Enterprise `allow-auto-only` policy support so `/allow-all auto` works while full allow-all remains blocked
- **Added:** Enterprise-managed sandbox policy can now enforce a proxy URL while credentials remain user-controlled
- **Improved:** `/sandbox` configuration dialog now groups git and gh settings

**v1.0.79-7**
- **Added:** Agent Plugins spec plugins can ship extensions under `com.github.copilot/extensions/` directory
- **Added:** Support for the kimi-k3 model
- **Added:** `--plan` combined with `--mode autopilot` enables plan-first-then-implement without approval waiting
- **Improved:** Multi-select prompts in the UI

**v1.0.79-6**
- **Fixed:** Rare internal delay no longer prints diagnostic warning over interactive UI
- **Fixed:** Failed session-history load no longer leaves the timeline permanently blank (was silently discarded)

---

## Hot Issues

### 1. [\#4402](https://github.com/github/copilot-cli/issues/4402) — npm bin/copilot is a loader, not a version pin
**Triage | 0 comments | 0 👍**
The npm shim served two different versions (1.0.77, then 1.0.78) 101 seconds apart with nothing changed in between. `--prefer-version` works but is undocumented. This is a significant reproducibility concern that undermines trust in version reporting.

### 2. [\#4401](https://github.com/github/copilot-cli/issues/4401) — Skill tool cannot find valid skills in ~/.agents/skills
**Triage | 0 comments | 0 👍**
A regression or incomplete fix related to #2230: the `skill` tool cannot find or invoke valid skills despite correct directory structure and `SKILL.md` presence. Impacts anyone relying on local skill management.

### 3. [\#2494](https://github.com/github/copilot-cli/issues/2494) — `copilot login` auto-enters keychain prompt
**Open | 11 comments | 1 👍**
Regression since v1.0.16: when the System Keychain is unavailable, the CLI auto-confirms the (y/N) prompt instead of waiting for user input, prematurely ending authentication. Important for headless/CI environments.

### 4. [\#1632](https://github.com/github/copilot-cli/issues/1632) — Support subfolders for skills
**Open | 10 comments | 23 👍**
The flat skills folder structure becomes unmanageable for users with 10+ skills. Strong community demand (23 👍) for hierarchical organization; still unresolved after 6 months.

### 5. [\#3622](https://github.com/github/copilot-cli/issues/3622) — Copy to clipboard silently fails on Windows
**Open | 5 comments | 4 👍**
Copying agent output appears to succeed but paste yields stale clipboard contents since 1.0.48. Affects Windows users heavily; no error is surfaced, making it particularly confusing.

### 6. [\#4251](https://github.com/github/copilot-cli/issues/4251) — Resuming large session OOMs / grinds CPU for ~70 min
**Open | 2 comments | 1 👍**
Regression in v1.0.74 with 3–4× memory usage on session resume. Users with long-lived sessions (resumed daily for months) now face OOM failures — critical for heavy users.

### 7. [\#4311](https://github.com/github/copilot-cli/issues/4311) — Transcript renders as blank lines until width change
**Open | 3 comments | 0 👍**
Measured-line cache invalidation bug in the `ScrollBox` component. `/resume` does not recover; content is present but invisible until a new message or terminal resize. Affects interactive mode visibility.

### 8. [\#4118](https://github.com/github/copilot-cli/issues/4118) — `/app` does not select current working directory
**Closed | 1 comment | 35 👍**
Highest-reacted issue in this digest. Users find it inconvenient to manually re-select their current directory every time. Though closed, the reaction count signals a UX expectation mismatch.

### 9. [\#4392](https://github.com/github/copilot-cli/issues/4392) — Post-auth MCP rebuild leaves orphaned stdio processes
**Open | 1 comment | 0 👍**
After authentication completes, the CLI tears down and rebuilds the entire MCP client, orphaning the first generation of stdio child processes. Resource leak that accumulates on repeated logins/restarts.

### 10. [\#4391](https://github.com/github/copilot-cli/issues/4391) — Copying text clears the screen on codepage 936
**Open | 1 comment | 0 👍**
Windows-specific: selecting and copying text on codepage 936 (Chinese) causes the screen to reset/clear. Works fine on codepage 437. Regional Windows users hit a major rendering regression in 1.0.79-5.

---

## Key PR Progress

No pull requests were updated in the last 24 hours. Please check the [PR list](https://github.com/github/copilot-cli/pulls) for ongoing work.

---

## Feature Request Trends

1. **Skill organization** — Users want subfolders/nesting for skills as the count grows ([#1632](https://github.com/github/copilot-cli/issues/1632), 23 👍)
2. **Workspace type persistence** — Per-session memory for "branch vs worktree" default, so users don't re-choose every time ([#4396](https://github.com/github/copilot-cli/issues/4396))
3. **Token usage reporting** — Ability to see token consumption per session for cost tracking ([#2947](https://github.com/github/copilot-cli/issues/2947), 7 👍)
4. **Permission prompt transparency** — Display which specific rule/command characteristic triggered the approval request ([#4386](https://github.com/github/copilot-cli/issues/4386))
5. **Desktop notifications** — Notify when the CLI needs human input so users can multitask ([#2941](https://github.com/github/copilot-cli/issues/2941))
6. **Better session management** — Restore quick-delete action in the sessions list ([#4395](https://github.com/github/copilot-cli/issues/4395))

---

## Developer Pain Points

1. **Windows stability** — Recurring theme: clipboard failures ([#3622](https://github.com/github/copilot-cli/issues/3622)), screen clears on non-437 codepages ([#4391](https://github.com/github/copilot-cli/issues/4391)), terminal title hijacking ([#4384](https://github.com/github/copilot-cli/issues/4384)), and path dash/underscore normalization breaking OneDrive dirs ([#1409](https://github.com/github/copilot-cli/issues/1409)). Windows remains the platform with the most unresolved issues.

2. **Permission system confusion** — Modes get stuck (auto mode persists after switching back to interactive) ([#4388](https://github.com/github/copilot-cli/issues/4388)), prompts don't explain *why* approval is needed ([#4386](https://github.com/github/copilot-cli/issues/4386)), and the `add-dir` flag's silent dash-to-underscore conversion causes permission loops that never resolve ([#1409](https://github.com/github/copilot-cli/issues/1409)).

3. **Background task / process management** — Models spawn shell background tasks but don't recognize completion — the shell has already exited yet the model waits forever ([#4385](https://github.com/github/copilot-cli/issues/4385)). Orphaned MCP stdio processes accumulate post-auth rebuilds ([#4392](https://github.com/github/copilot-cli/issues/4392)).

4. **Session resume degradation** — Large-session resume regressions (3–4× memory, OOM) ([#4251](https://github.com/github/copilot-cli/issues/4251)) and model selection not persisting across resume ([#4397](https://github.com/github/copilot-cli/issues/4397)) break established workflows for daily drivers.

5. **Silent failures & misleading indicators** — The CLI shows MCP servers as successfully loaded when initialization fails ([#1129](https://github.com/github/copilot-cli/issues/1129)), and version ambiguity via the npm loader ([#4402](https://github.com/github/copilot-cli/issues/4402)) makes it hard to trust what's actually running.

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest
**2026-08-08**

---

## Today's Highlights

The community is currently focused on a critical data-integrity bug: `StrReplaceFile` is silently corrupting non-UTF-8 bytes in binary or mixed-encoding files, and **two** competing fixes (byte-preserving edit vs. refuse-to-edit) are now under review. Additionally, a serious safety incident involving an agent executing `rm -rf` outside the workspace in "yolo" mode has surfaced, raising urgent questions about permission model hardening and filesystem boundary enforcement. No new releases were published in the last 24 hours.

---

## Releases

No new versions were published in the last 24 hours.

---

## Hot Issues

1. **[#2596 — Agent ran `rm -rf` on a pre-existing directory outside the workspace, deleting user session data](https://github.com/MoonshotAI/kimi-cli/issues/2596)**  
   *Author: iMaxTomas | Created: 2026-08-07 | Comments: 0*  
   Critical safety incident. The agent failed to detect a symlink creation failure, then escalated to a destructive command that targeted the wrong path. **Community reaction:** No responses yet, but this is a P0-class issue — enterprise users and anyone running "yolo" mode will demand immediate isolation guarantees.

2. **[#2591 — `StrReplaceFile` corrupts undecodable bytes outside the edited region](https://github.com/MoonshotAI/kimi-cli/issues/2591)**  
   *Author: shoemoney | Created: 2026-08-05 | Comments: 3*  
   Demonstrated file corruption: the whole file is decoded with `errors="replace"`, edits applied on the string, and the result re-encoded — meaning *every* invalid UTF-8 byte in the file (even far from the edit) is rewritten as U+FFFD. **Community reaction:** Three comments; the community flagged this as a serious data-loss vector for anyone using these tools on mixed-encoding files (single-byte encodings, old legacy files, partial binary content). This has single-handedly driven two fix PRs.

---

## Key PR Progress

1. **[#2594 — fix(tools): preserve non-UTF-8 bytes in `StrReplaceFile` edits](https://github.com/MoonshotAI/kimi-cli/pull/2594)**  
   *Author: 686f6c61 | Created: 2026-08-06*  
   Fixes `#2591` correctly: applies `old`/`new` as **UTF-8 byte substrings** directly against the raw buffer instead of decoding the entire file. This is the safe, minimal-corruption fix — higher risk surface, but preserves original bytes exactly.

2. **[#2595 — fix(StrReplaceFile): refuse to edit files that are not valid UTF-8](https://github.com/MoonshotAI/kimi-cli/pull/2595)**  
   *Author: shoemoney | Created: 2026-08-06*  
   A conservative alternative to `#2594`: aborts the edit entirely for non-UTF-8 files. Guarantees zero corruption, but at the cost of rejecting many legitimate use cases (configs with legacy encodings, etc.). Community now needs to decide between "preserve bytes" vs. "refuse."

3. **[#2255 — feat(shell): support Shift+Enter for inserting newlines](https://github.com/MoonshotAI/kimi-cli/pull/2255)**  
   *Author: donbeave | Created: 2026-05-13 | Closed: 2026-08-06*  
   The long-requested edit-mode feature. Adds `Shift+Enter` as an alternative to `Ctrl-J` / `Alt-Enter` for newline insertion in the interactive prompt. Though closed (likely merged), it resolves a long-standing UX complaint (multiline prompts) and signals ongoing investment in terminal interactivity.

---

## Feature Request Trends

1. **Byte-level safety in string-editing tools**
   Multiple issues (notably #2591) are pushing toward stricter guarantees in the `StrReplaceFile` family — the community is effectively asking for **UTF-8-native byte-aware editing**, not string-level edit-and-reencode.

2. **Hardened autonomous operation boundaries**
   After the #2596 incident, there's an implicit request for stricter sandboxing: filesystem access fences, symlink resolution safeguards, and "destructive command" confirmations even in "yolo" mode. The overarching trend: **agents must prove they understand their environment before touching it**.

3. **Interactive prompt ergonomics**
   The (now closed/merged) Shift+Enter PR closes a long thread of requests (#2254, #2010, #2121, #1585, #1574) — the pattern here is that users want a human-friendly, multi-line editing experience that matches modern terminal expectations, not just vi/emacs keybindings.

---

## Developer Pain Points

1. **Silent data corruption is the #1 concern.** No user wants a tool to rewrite bytes it didn't touch. The `StrReplaceFile` debate — preserve vs. refuse — is a classic reliability tradeoff the maintainers must resolve carefully.

2. **"yolo" mode fails to scope destructive actions.** A single agent session deleted user data outside the workspace; the community's trust is shaken. The pain point is clear: **"I know what I asked for; I need the tool to double-check what it's about to do anyway."**

3. **Legacy/mixed-encoding files are more common than docs admit.** The community reaction to #2591 shows many users run into non-UTF-8 files daily (configs, old Windows files, partial-UTF-16) — and tools must handle them gracefully, not corrupt them.

4. **Confusion when multiple fixes address the same bug differently.** The community now has two implementations for #2591 with different semantics. While healthy in open source, this creates a maintainer decision burden — and a period of uncertainty for users watching what "correct" means.

---

**Overall**: This digest period is dominated by **reliability and safety**, not new features. The closure of the Shift+Enter PR is a quiet win, but the active conversation is about trust: trusting the tool to not corrupt files, and trusting the agent to not destroy user data. This will shape the next phase of Kimi Code CLI's evolution.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-08-08

## Today's Highlights
The community is wrestling with two major themes this week: **OpenCode Go plan metering and billing discrepancies** (multiple reports of unexpected 401s, premature quota exhaustion, and model misidentification) and **a wave of PR merges/cleanups** — roughly 20 PRs were finally merged after a month-long automated cleanup, including significant improvements to MCP resource handling, Code Mode, and permission enforcement for grep/glob. On the platform side, v1.18.15 shipped with a focused set of core bugfixes around message chronology and truncation cleanup.

## Releases
**v1.18.15** — Core bugfix release:
- Chronological message ordering now stays correct even when imported or legacy message IDs are out of order
- Revert and fork actions now use real message chronology instead of message ID ordering
- Truncation cleanup now removes stale files by file timestamp more reliably

🔗 [Release v1.18.15](https://github.com/anomalyco/opencode/releases/tag/v1.18.15)

## Hot Issues

1. **[#38257 — OpenCode Go: 401 Request blocked by upstream provider**](https://github.com/anomalyco/opencode/issues/38257) — 45 comments, 11 👍. A multi-day outage affecting all `chat/completions` calls while `/v1/models` works. The 401s appear server-side across Go subscriptions. This is the most active issue this week and driving significant trust concerns around the Go service.

2. **[#5359 — Unable to read images for some models**](https://github.com/anomalyco/opencode/issues/5359) — 18 comments. Long-standing regression (since ~v1.0.137) where pasted images fail on LiteLLM+Vertex AI backends. Works on v1.0.134; appears backend-specific, not a TUI issue.

3. **[#23153 — [FEATURE]: Pay Go with crypto**](https://github.com/anomalyco/opencode/issues/23153) — 17 comments, 37 👍. One of the highest-👍 open feature requests. Community wants crypto payment for Go subscriptions, signaling interest in anonymous/global payment options.

4. **[#14332 — Amazon Bedrock Opus 4.6 compaction failure**](https://github.com/anomalyco/opencode/issues/14332) — 16 comments, 8 👍. Compaction fails when `thinking`/`redacted_thinking` blocks are modified during history compaction. Closed, but a known pain point for Bedrock users.

5. **[#40409 — OpenCode Go `deepseek-v4-flash` is NOT serving DeepSeek V4 Flash**](https://github.com/anomalyco/opencode/issues/40409) — 14 comments. Billing/quality mismatch: the Go endpoint returns a V3.2 model with 2025-05 knowledge cutoff instead of the advertised V4 Flash. Closed, but user frustration runs high on model identity mismatches.

6. **[#6560 — Paste broken in PowerShell OpenCode instance**](https://github.com/anomalyco/opencode/issues/6560) — 13 comments, closed. Windows 11 users can't paste into the TUI via Ctrl+V or right-click. Closed, but illustrates TUI clipboard issues on Windows still surface periodically.

7. **[#24334 — Error from provider (DeepSeek): `reasoning_content` must be passed back**](https://github.com/anomalyco/opencode/issues/24334) — 10 comments, closed. Thinking-mode DeepSeek responses require echoing `reasoning_content` during follow-ups; OpenCode failed to do so in some flows.

8. **[#8565 — Accessibility mode for screen reader users**](https://github.com/anomalyco/opencode/issues/8565) — 10 comments, closed. TUI is "actively hostile to screen readers" due to emojis, animations, unicode. Community response favorable, but no concrete timeline shared.

9. **[#41146 — Overcharged on Go plan — weekly limit exhausted at ~$7.50 despite $30 limit**](https://github.com/anomalyco/opencode/issues/41146) — 2 comments, created today. Shows **quota metering is off** (100% used on ~25% of the advertised limit). Closed, but likely the same root cause as #38257.

10. **[#41102 — Usage bug.](https://github.com/anomalyco/opencode/issues/41102)** — 3 comments. Usage above 100% and auto-compaction never triggers. Reinforces the recurring "Go billing meter is broken" theme this week.

## Key PR Progress

1. **[#35743 — fix(provider): apply chunkTimeout to non-SSE streaming protocols**](https://github.com/anomalyco/opencode/pull/35743) — AWS Bedrock and other EventStream providers bypassed `chunkTimeout` entirely since they don't use `text/event-stream`. Now matches both content types.

2. **[#35796 — fix(tui): clear stale tool preparation state**](https://github.com/anomalyco/opencode/pull/35796) — Regression fix with test: the TUI was overwriting completed assistant messages with stale "pending tool" state after refresh.

3. **[#35787 — feat(bedrock): prompt for region on bedrock provider**](https://github.com/anomalyco/opencode/pull/35787) — Closes #28834. Desktop users no longer need to manually configure region; OpenCode now prompts for it during provider setup.

4. **[#35785 — refactor(core): make Code Mode a service**](https://github.com/anomalyco/opencode/pull/35785) — Code Mode becomes a Location-scoped service with nested canonical tool sources. MCP registration/enablement moves into the service domain.

5. **[#35780 — feat(mcp): attach resources from TUI**](https://github.com/anomalyco/opencode/pull/35780) — Adds canonical browser-safe MCP attachment URIs, resolves MCP text/blob content before durable prompt admission, with MIME sniffing and base64 validation.

6. **[#35767 — feat(codemode): support property deletion**](https://github.com/anomalyco/opencode/pull/35767) — JavaScript-style `delete` operator support in Code Mode, preserving tool/runtime and URL members while leaving array holes intact.

7. **[#35766 — feat(codemode): support JSON callbacks**](https://github.com/anomalyco/opencode/pull/35766) — Adds `JSON.parse` reviver and `JSON.stringify` replacer support with callback ordering and mutation preservation. 293 tests pass.

8. **[#35764 — feat(opencode): add planner/worker/reviewer workflow**](https://github.com/anomalyco/opencode/pull/35764) — New opt-in `workflow` config enabling a planner/worker/reviewer pattern for multi-agent orchestration. No issue tracked yet, likely upcoming discussion.

9. **[#41123 — fix(ai): preserve responses item ids**](https://github.com/anomalyco/opencode/pull/41123) — **Open.** Makes Responses item IDs first-class across messages, streamed events, tools, and V2 durable history, with stable `msg_*`, `rs_*`, `fc_*` prefixes. Big for reliable session replay.

10. **[#35727 — fix(grep): limit file path searches**](https://github.com/anomalyco/opencode/pull/35727) — When `grep` receives an exact file path, only search the specific file via basename instead of doing whole-tree ripgrep. Closes #35726.

## Feature Request Trends

- **Crypto payment for Go** (#23153, 37 👍) — Strong demand for anonymous/non-card payment options.
- **Session-scoped tool configuration** — Led by PR #35691 and related requests, users want per-session tool availability rather than global toggles.
- **Planner/worker/reviewer workflows** — Multi-agent orchestration patterns are emerging as a top request direction (see PR #35764).
- **Skills organization** (#38853) — Skills stored flat under `~/.config/opencode/skills/` need subfolder support as users accumulate dozens.
- **Accessibility mode** (#8565) — Screen-reader-friendly TUI remains a requested direction, though slow-moving.
- **Runtime model override for subagents** (#17595) — Orchestrators want per-subagent model selection without restart.

## Developer Pain Points

- **Go plan metering and 401s** — The dominant theme this week. Multiple reports of quota exhaustion below advertised limits (#41146, #41102), per-request 401s on `chat/completions` (#38257), and confusing "Free usage exceeded" messages despite active Go subscriptions (#41148). This is the highest-impact trust issue right now.

- **Model identity mismatch on Go endpoints** — `deepseek-v4-flash` returning a V3.2 model with an older knowledge cutoff (#40409, #40607) is both a billing-integrity and quality issue. Reproducible with first-party keys, so not just a proxy artifact.

- **Provider auth friction** — Copilot re-auth every session despite stored credentials (#40183), and Copilot models not appearing after OAuth connect (#41088) are recurring integration frustrations.

- **Windows-specific TUI issues** — Paste not working in PowerShell (#6560) and black screen when running from source (#40231) demonstrate ongoing Windows TUI gaps.

- **Draft/content loss in TUI** — Skill selection clears the input draft (#39376), and message ordering regressions (#38257) create QoL regressions for power users.

- **Compaction and history problems** — Bedrock thinking-block compaction failures (#14332) and "usage stuck above 100%" refusing to compact (#41102) point to history-management instability across providers.

---

*Digest generated from [github.com/anomalyco/opencode](https://github.com/anomalyco/opencode) — 2026-08-08*

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-08-08

## Today's Highlights

The Pi project continues to mature, with v0.84.1 bringing a dedicated Qwen token plan for Individual subscriptions and improved authentication readiness checks. However, the community remains focused on several long-standing robustness issues, particularly auto-compaction never triggering before provider overflow (#6879) and high CPU usage on macOS during long sessions (#7730). The 24-hour window shows a flurry of activity — 50 issues updated and 26 PRs touched — with significant progress on harness recovery restoration (#7710) and a new Cursor CLI bridge (#7792).

## Releases

**v0.84.1** (latest)

- **Qwen Token Plan Individual** — Use the built-in provider for models documented for Individual subscriptions. See [API Keys docs](https://github.com/earendil-works/pi/blob/v0.84.1/packages/coding-agent/docs/providers.md#api-keys).
- **Authentication readiness checks** — New `pi auth` improvements to verify authentication state before running.

## Hot Issues

1. **[#6879 — auto-compaction never triggers after context grows past 100% until provider overflow](https://github.com/earendil-works/pi/issues/6879)** *(OPEN, 13 comments, 15 👍)*  
   A session on gpt-5.6-sol ran for 2+ hours, the context footer passed 100%, and compaction only fired when the API rejected the request at 373k tokens. The proposala—checking after every agentic turn—is sensible. The high upvote count signals this is a frustrating papercut affecting many users.

2. **[#7128 — New default PI_* guideline in system prompt over-encourages unnecessary bash calls](https://github.com/earendil-works/pi/issues/7128)** *(OPEN, 11 comments, 7 👍)*  
   The default system prompt now includes "Inspect PI_* environment variables…", which biases agents toward running env-inspection commands even when irrelevant. This is a classic prompt-engineering regression—impacting both cost and latency.

3. **[#7020 — Sometimes Pi doesn't continue after compaction](https://github.com/earendil-works/pi/issues/7020)** *(CLOSED, 10 comments, 2 👍)*  
   Long-running "coordinator" sessions frequently hit warts where Pi fails to continue after compaction. The issue was closed, but the underlying lifecycle bugs (see #5886) are still open—worth watching to confirm the fix is complete.

4. **[#5886 — AgentSession settlement/continuation and assistant-tail lifecycle bugs](https://github.com/earendil-works/pi/issues/5886)** *(OPEN, 6 comments, 4 👍)*  
   A meta-issue from mitsuhiko covering a recurrence of bugs where post-run logic tries to continue the agent from a stale transcript. This is the "issue behind the issues"—the root cause for several flaky behaviors.

5. **[#7730 — High CPU usage on Mac OS with long session](https://github.com/earendil-works/pi/issues/7730)** *(OPEN, 4 comments, 5 👍)*  
   CPU swings from 50–110% with 600–800MB memory on long sessions. Anecdotally tied to context size. Performance regressions on macOS are high-priority for the TUI-heavy user base.

6. **[#7053 — Parallel tool batches lose already-completed tool results when one sibling stalls](https://github.com/earendil-works/pi/issues/7053)** *(OPEN, 4 comments, 0 👍)*  
   The UI fires `tool_execution_end` per-tool, but persisted `toolResult` messages are still batched via `Promise.all`. If one tool stalls, all its siblings' results are lost. A correctness issue with parallel tool use.

7. **[#7702 — DeepSeek models fail via opencode zen gateway: reasoning_content must be passed back](https://github.com/earendil-works/pi/issues/7702)** *(CLOSED, 6 comments)*  
   `detectCompat()` fails to round-trip `reasoning_content` for DeepSeek models, causing 400s on multi-turn conversations. Closed as a bug fix, but a strong signal that reasoning-model compatibility is a pain point.

8. **[#7128 — `which` dependency breaks copy command in minimal environments](https://github.com/earendil-works/pi/issues/7128)** *(CLOSED, 1 comment)*  
   `which` is not a shell built-in and is missing in sandboxes. The fix is to use `command -v` (see PR #7795). A small but important portability fix.

9. **[#7798 — TUI Crash on Session Resume: "Cannot read properties of undefined (reading 'render')"](https://github.com/earendil-works/pi/issues/7798)** *(CLOSED, 1 comment)*  
   A crash on resume in the TUI's Box.render path. Closed quickly, but session-resume reliability is critical given the long-running "coordinator" usage pattern.

10. **[#7740 — TUI after /reload does not follow custom tool's renderCall/renderResult](https://github.com/earendil-works/pi/issues/7740)** *(OPEN, 2 comments)*  
    After `/reload`, tools registered on `session_start` (like MCP extensions) don't render correctly due to load-order issues. A follow-up fix in PR #7749 is already in the pipeline.

## Key PR Progress

1. **[#7710 — feat(agent): restore suspended harness operations](https://github.com/earendil-works/pi/pull/7710)** *(OPEN)*  
   Implements R3 of the harness v2 plan: `AgentHarness.create` can now load a new harness from a session with existing local logs. This is foundational work toward crash recovery and session durability.

2. **[#7792 — feat(coding-agent): bridge Cursor CLI auth via local agent session](https://github.com/earendil-works/pi/pull/7792)** *(CLOSED)*  
   A hidden extension bridges Pi to an already-authenticated local Cursor CLI — no API key needed. Exposes `pi cursor status [--json]` and Team models. A clever way to piggyback on existing auth flows.

3. **[#7784 — refactor(agent): derive recovery state from record queries](https://github.com/earendil-works/pi/pull/7784)** *(OPEN)*  
   Removes recovery-specific query APIs in favor of bounded `findRecords()` calls, retaining write-side enforcement. A cleanup that reduces SQLite-specific indexes and query paths.

4. **[#7801 — feat(coding-agent): lazily load uncommon syntax grammars](https://github.com/earendil-works/pi/pull/7801)** *(OPEN)*  
   Experimental refactoring by mitsuhiko for syntax highlighting. The highlight function is public API, so this is carefully engineered to preserve compatibility while reducing load cost.

5. **[#7780 — TUI performance improvement](https://github.com/earendil-works/pi/pull/7780)** *(CLOSED)*  
   Incremental markdown parsing and lazy render invalidation, plus partial old-content parsing on startup. Directly addresses the kind of performance complaints in #7730.

6. **[#7749 — fix(coding-agent): preserve custom tool renderers after reload](https://github.com/earendil-works/pi/pull/7749)** *(CLOSED)*  
   Fixes the load-order bug where the interactive mode rebuilt chat history before emitting `session_start`, causing tool renderers (e.g. MCP) to be unavailable.

7. **[#7795 — fix(coding-agent): use command -v to verify wl-copy exists](https://github.com/earendil-works/pi/pull/7795)** *(CLOSED)*  
   Replaces `which` with `command -v` for the `/copy` command — a portability fix for minimal environments. (Resolves #7796)

8. **[#7762 — feat(provider): Introduce LM Studio provider](https://github.com/earendil-works/pi/pull/7762)** *(OPEN)*  
   Adds LM Studio as a local provider, solving #7668. Tests are guarded by an env var; the author notes AI-generated code was manually verified.

9. **[#7757 — feat(coding-agent): allow opting out of fullscreen copy-on-select](https://github.com/earendil-works/pi/pull/7757)** *(OPEN)*  
   Adds a setting to disable copy-on-select in fullscreen, overriding the `app.message.copy` keybind to copy selected content. Addresses UX feedback from #7720.

10. **[#7788 — fix(example): render tool errors via context.isError](https://github.com/earendil-works/pi/pull/7788)** *(CLOSED)*  
    Fixes the built-in-tool-renderer example which used string matching (`startsWith("Error")`) for failure detection — broken because built-in tools throw errors instead.

## Feature Request Trends

- **Provider expansion and compatibility** — Strong demand for more providers: LM Studio (#7762), Amazon Bedrock Mantle (#6216), improved DeepSeek round-tripping (#7702), and Gemini thought signatures (#6733).
- **Auth bridging and reuse** — The Cursor CLI bridge (#7792, #7793) points to a desire to reuse existing authenticated sessions rather than managing separate API keys. Expect more "bring your own auth" patterns.
- **TUI UX polish** — Requests for collapsible paste previews (#7754), top-positioned `/` menu in fullscreen (#7786), half-page scroll keybindings (#7735), and theme overrides (#7722) all indicate the TUI is the primary interface and needs better ergonomics.
- **Plugin/session portability** — Root plugin.json manifest support (#7776) and the harness restore work (#7710) point toward ecosystem portability and durable sessions as strategic directions.

## Developer Pain Points

- **Context/compaction reliability** (#6879, #7020, #5886) — The most frequent and highly-upvoted frustration. Long-running sessions are a core Pi use case, and compaction bugs break them.
- **Session lifecycle complexity** — "Assistant-only transcripts" (#7703), "doesn't continue after compaction" (#7020), and "active run not aborted on reset" (#7703) all trace back to the same fragile settlement logic.
- **Tool execution edge cases** — Parallel tool batch failures (#7053) and `function_call` namespace drops (#7709) show that multi-tool orchestration is still not fully hardened.
- **Prompt-engineering regressions** (#7128) — Default system prompt changes can have unintended behavioral consequences, and the community is sensitive to token-wasting bash inspection calls.
- **Portability in minimal environments** — `which` vs `command -v` (#7796) and the undici `maxHeaderSize` overflow (#7791) show that sandboxed/CI environments expose hidden assumptions.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest - 2026-08-08

## Today's Highlights
Qwen Code v0.21.7 stable is out with a major quality-of-life improvement: the 50-turn limit for Goals has been removed, letting long-running tasks resume without artificial boundaries. On the desktop front, inline terminal images from model outputs now render directly in the interactive CLI, closing a long-standing gap for visual workflows. The ecosystem is clearly consolidating around Web Shell as the primary UI surface, with multiple PRs landing fullscreen panels, tmux-backed interactive terminals, and browser control bridges.

## Releases
- **v0.21.7** ([release](https://github.com/QwenLM/qwen-code/releases/tag/v0.21.7)): Removed the 50-turn limit for Goals, allowing tasks to resume and continue beyond previous boundaries ([#8421](https://github.com/QwenLM/qwen-code/pull/8421)). Enabled rendering inline terminal images from model outputs in the interactive CLI.
- **v0.21.7-nightly.20260807.fca8f3c1f**: CI fix surfacing blocked autofix takeover admission ([#8410](https://github.com/QwenLM/qwen-code/pull/8410)). Full changelog: [link](https://github.com/QwenLM/qwen-code/compare/v0.21.7...v0.21.7-nightly.20260807.fca8f3c1f)

## Hot Issues
1. **[#3203 - Qwen OAuth Free Tier Policy Adjustment](https://github.com/QwenLM/qwen-code/issues/3203)** (150 comments, closed) - Massive community pushback on proposed free-tier reductions (1,000→100 req/day) and planned shutdown. This has been the most-discussed issue for months, signaling strong developer dependence on the free tier.

2. **[#8625 - Chinese input shows pinyin in Windows terminal](https://github.com/QwenLM/qwen-code/issues/8625)** (6 comments) - TUI rendering bug on Windows where IME composition is unreadable. Small count but high relevance for Chinese-speaking users—the largest regional segment.

3. **[#8562 - tmux flickering over SSH](https://github.com/QwenLM/qwen-code/issues/8562)** (5 comments) - Screen flicker in tmux when used via SSH from macOS through iTerm2. User reports having Qwen 3.8 Max confirm it's a version regression, adding external validation.

4. **[#8659 - TUI flickering in web terminals](https://github.com/QwenLM/qwen-code/issues/8659)** (3 comments) - Similar flicker/tearing issue affecting Alibaba Cloud Workbench with `useTerminalBuffer: true`. Users recommend disabling Virtualized History mode as a workaround.

5. **[#8672 - Middle-mouse selection broken in PuTTY](https://github.com/QwenLM/qwen-code/issues/8672)** (3 comments) - Regression from 0.21.1 breaking xterm-style middle-button copy/paste over PuTTY SSH. Highlighted performance pain for remote Linux workflows.

6. **[#8615 - Desktop 0.1.0 crashes on Windows: EISDIR lstat](https://github.com/QwenLM/qwen-code/issues/8615)** (5 comments, closed) - Bundled runtime crashes opening workspace folders on Windows (Node v22.20.0). Recently fixed—important for early desktop adopters.

7. **[#7118 - Windows standalone installer fails: Get-FileHash](https://github.com/QwenLM/qwen-code/issues/7118)** (4 comments, 3 👍) - PowerShell SHA-256 verification fails when `Get-FileHash` is unavailable, blocking installation. High-value fix for a common Windows environment gap.

8. **[#8697 - OTEL_METRICS_EXPORTER=otlp silently disables metrics](https://github.com/QwenLM/qwen-code/issues/8697)** (2 comments) - Standard OTel env var breaks qwen-code's metrics export entirely (traces still flow). Developer pain when sharing a collector across Claude Code/Codex/opencode.

9. **[#8550 - `qwen mcp list` hangs on SSE servers](https://github.com/QwenLM/qwen-code/issues/8550)** (4 comments, closed) - Indefinite hang when SSE MCP server never sends `endpoint`. Important robustness fix for MCP infrastructure users.

10. **[#6487 - Memory index stale after /remember; content lost on compaction](https://github.com/QwenLM/qwen-code/issues/6487)** (3 comments, closed) - Long-session memory degradation: stale MEMORY.md index and compaction losing data. Significant for the Goals/context persistence workflow now that the 50-turn limit is lifted.

## Key PR Progress
1. **[#8707 - Qwen WebBridge direct browser control](https://github.com/QwenLM/qwen-code/pull/8707)** - Kimi-compatible `/command` and `/status` endpoints from `qwen serve` to the Chrome extension. Full 17-action surface with task-scoped ownership—addresses the browser-native control gap.

2. **[#8613 - tmux-backed interactive terminal sub-agent](https://github.com/QwenLM/qwen-code/pull/8613)** - Agents can run REPLs, CLIs, or TUIs inside tmux, driven as background tasks with a live interactive view in Web Shell. Major capability expansion for agent autonomy.

3. **[#8614 - Fullscreen view for Web Shell artifact panel](https://github.com/QwenLM/qwen-code/pull/8614)** - Adds expand/collapse toggle to the right panel (artifacts, subagents, monitors, scheduled tasks)—readiness indicator for Web Shell as the canonical UI.

4. **[#8682 - Pollable turn-status endpoints for daemon sessions](https://github.com/QwenLM/qwen-code/pull/8682)** - `GET /session/:sessionId/turns/:promptId` and `turns/current` expose turn lifecycle state. Enables reliable client-side status polling—critical for WebShell and desktop app.

5. **[#8675 - Model-specific reasoning controls](https://github.com/QwenLM/qwen-code/pull/8675)** - Built-in registry for Thinking/Effort controls across Core, ACP, daemon, SDK, and WebShell. First registration is `qwen3.*`—expected foundation for multi-model parity.

6. **[#8588 - Expose active work state via `/health?deep=1`](https://github.com/QwenLM/qwen-code/pull/8588)** - Adds `activeWork`, `activeWorkReporting`, `activeWorkStaleMs` fields for operational visibility—useful for Fleet Shepherd automation and observability.

7. **[#8368 - Kimi and Xiaomi MiMo auth providers](https://github.com/QwenLM/qwen-code/pull/8368)** - First-class third-party provider presets with regional access tiers. Response to the "multi-model ecosystem" expectation set by OTel parity efforts.

8. **[#8526 - Reasoning effort through ACP](https://github.com/QwenLM/qwen-code/pull/8526)** - Standard ACP `thought_level` selector (Default → Max) with `session/set_config_option` support. Aligns with the effort-tier trends seen in competitors.

9. **[#8687 - Guard cross-worktree Git mutations](https://github.com/QwenLM/qwen-code/pull/8687)** - Host-side guard blocking `run_shell_command` Git operations that escape the session workspace via `-C`, `--work-tree`, `--git-dir`. Security hardening for daemon mode.

10. **[#8394 - Maven multi-module verification for /review](https://github.com/QwenLM/qwen-code/pull/8394)** - Deterministic root-reactor detection and changed-file mapping to deepest module. Builds out `/review` for Java monorepos—tying into the legacy audit workflow trend.

## Feature Request Trends
- **Browser automation without MCP**: [#8699](https://github.com/QwenLM/qwen-code/issues/8699) proposes a direct WebBridge, avoiding "MCP as a required path"—a response to the friction MCP adds for simple browser control.
- **Web Shell as the universal UI**: Multiple items call for Web Shell reuse ([#8092](https://github.com/QwenLM/qwen-code/issues/8092), [#6701](https://github.com/QwenLM/qwen-code/issues/6701), [#6699](https://github.com/QwenLM/qwen-code/issues/6699))—composer toolbar redesign, "Start In" context selector, and lower-maintenance desktop app all target Web Shell.
- **Local Control / phone access**: [#8595](https://github.com/QwenLM/qwen-code/issues/8595) requests QR-code pairing for phone takeover of local sessions—the "control your agent from anywhere" pattern.
- **Fact verification and strict mode**: [#8701](https://github.com/QwenLM/qwen-code/issues/8701) asks for five explicit Agent fact-checking enhancements (verify-before-conclude, full-chain validation, transcript skepticism).
- **Telemetry and observability parity**: OTel-aligned session lifecycle ([#8616](https://github.com/QwenLM/qwen-code/pull/8616)) and runtime/client attribution ([#8660](https://github.com/QwenLM/qwen-code/issues/8660)) show a systematic push toward OpenTelemetry conformance.

## Developer Pain Points
- **OAuth free-tier anxiety**: Issue #3203 has 150 comments—developers are deeply invested in the free tier and openly upset about proposed quota cuts and shutdown timelines. Expect prolonged community discussion even after closure.
- **TUI rendering fragility**: Three separate flickering/rendering issues (#8562, #8659, #8625) across tmux, PuTTY, web terminals, and Windows IME indicate the terminal layer needs more robust handling—especially for non-ASCII input and screen redraws.
- **Desktop app maturity gap**: Windows crash on startup (#8615), non-clickable markdown links (#8593), and installer failures (#7118) signal the desktop/Windows story lags the polished CLI experience.
- **Telemetry/OTel integration friction**: The `OTEL_METRICS_EXPORTER=otlp` silent failure (#8697) highlights a common enterprise pattern (shared collectors) colliding with premature SDK assumptions. Standard env vars should be respected or explicitly documented as unsupported.
- **MCP endpoint resilience**: Hangs on non-specced SSE servers (#8550) and the general push to grow beyond MCP show that MCP infrastructure still lacks robustness guarantees in the wild.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest — 2026-08-08

## 1. Today's Highlights
The maintainers pushed forward with the v0.9.4 release pipeline, opening a dedicated PR (#5282) to clear the four CI blockers holding the release. Concurrently, a wave of seven new v0.9.5 feature issues were filed, outlining a comprehensive roadmap for session recovery, mid-turn control, and unified task management. Significant progress was also made on the command-boundary refactor, with community contributor `aboimpinto` verifying Layer 5.3 for palette and completion filtering (#5255).

## 2. Releases
No new releases were published in the last 24 hours. However, the repository is positioned at **version 0.9.4** with the CHANGELOG dated and package pins in sync. PR [#5282](https://github.com/Hmbown/CodeWhale/pull/5282) indicates the release is blocked on CI failures rather than pending decisions, suggesting an imminent release once the red lanes are cleared.

## 3. Hot Issues
1. **[#5272](https://github.com/Hmbown/CodeWhale/issues/5272) — Prompt-scoped file recovery (v0.9.5)** | *New*  
   Proposes restoring workspace files from session snapshots tied to a prior prompt, with git-aware confirmation. Addresses the pain of "git archaeology" after agent-caused tree damage. High-value for teams using DeepSeek TUI for autonomous work.

2. **[#5271](https://github.com/Hmbown/CodeWhale/issues/5271) — Session peek without full attach (v0.9.5)** | *New*  
   Enables listing sessions, peeking last activity, and answering approvals without leaving the current composer. Directly targets multi-session control friction and aligns with Fleet's multi-worker direction.

3. **[#5270](https://github.com/Hmbown/CodeWhale/issues/5270) — Unified tasks surface (v0.9.5)** | *New*  
   Consolidates background shells, subagents, Fleet workers, and workflow runs into one operator-facing list. Aims to end the "is anything still running?" ambiguity.

4. **[#5269](https://github.com/Hmbown/CodeWhale/issues/5269) — Durable plan artifact with line comments (v0.9.5)** | *New*  
   Folds [#4390](https://github.com/Hmbown/CodeWhale/issues/4390) into a durable, commentable plan artifact. The community's continued push for shareable plan documents signals a desire for better review workflows.

5. **[#5268](https://github.com/Hmbown/CodeWhale/issues/5268) — Mid-turn control: queue / send-now / Esc-keep-draft** | *New*  
   Makes the composer useful during live turns with named waits. Directly addresses the "fighting a locked chat bubble" experience and the unclear steer/queue/cancel contract.

6. **[#5267](https://github.com/Hmbown/CodeWhale/issues/5267) — Turn-stop honesty (v0.9.5)** | *New*  
   Demands the turn loop actually stop when the footer says "ending". Rooted in trust loss when the model keeps talking after stop signals — a fundamental UX bug.

7. **[#3205](https://github.com/Hmbown/CodeWhale/issues/3205) — Fleet model classes and loadout auto (v0.9.3)** | *Core backlog*  
   The shared model/loadout selector for TUI, CLI, exec, subagents, and Fleet workers. Central to the multi-agent architecture; still open after ~8 weeks with 12 comments.

8. **[#1004](https://github.com/Hmbown/CodeWhale/issues/1004) — `/dryrun` command to preview request payload** | *High user demand*  
   Lets developers see exactly what will be sent (system prompt, cached files, tool defs) before hitting the API. Specifically valuable for DeepSeek V4 Pro users where long-context turns have real cost.

9. **[#1481](https://github.com/Hmbown/CodeWhale/issues/1481) — Support OpenCode Go/Zen as provider** | *Closed? No, still open*  
   Community requests cheap DeepSeek-V4 access via OpenCode Go/Zen. Despite 11 comments and a 👍, this remains unresolved — an integration opportunity.

10. **[#1097](https://github.com/Hmbown/CodeWhale/issues/1097) — FreeBSD support (npm binary / pkg)** | *Two comments, still open*  
    User on FreeBSD hit a hard install failure. Relevant today because a community PR ([#5254](https://github.com/Hmbown/CodeWhale/pull/5254)) attempted a build fix but was **closed** — likely needs rework due to the rquickjs platform limitation.

## 4. Key PR Progress
1. **[#5282](https://github.com/Hmbown/CodeWhale/pull/5282) — fix(release): clear the four CI blockers holding v0.9.4**  
   Maintainer-issued. The release is versioned but blocked on three failing CI lanes. This is the critical path to shipping v0.9.4.

2. **[#5255](https://github.com/Hmbown/CodeWhale/pull/5255) — Layer 5.3: Palette, completion, and discovery filtering**  
   Community drive by `aboimpinto` on the command-boundary refactor. Validates acceptance criteria for command palette and slash-completion — healthy progress on architecture modernization.

3. **[#5258](https://github.com/Hmbown/CodeWhale/pull/5258) — fix(tui): stop stale cached session title from pinning "New Session"**  
   A sharp bug hunt: stale in-memory metadata cache overwrote computed titles, locking the header on "New Session". Simple and high-impact for daily UX.

4. **[#5256](https://github.com/Hmbown/CodeWhale/pull/5256) — feat(mcp): background incremental registry sync**  
   Converts blocking full registry downloads into cache-first, background-incremental syncs. Meaningful latency and reliability win for MCP integration.

5. **[#5257](https://github.com/Hmbown/CodeWhale/pull/5257) — feat(config): add `model = auto` for prompt-based tier selection**  
   Community feature: auto-switch between deepseek-v4-pro (complex) and v4-flash (simple) based on prompt heuristics. Directly answers cost/performance juggling.

6. **[#5252](https://github.com/Hmbown/CodeWhale/pull/5252) — feat(subagents): allow embedders to isolate runtime state roots** *(CLOSED)*  
   Added `EngineConfig::subagent_state_root` for embedding hosts. Closed without merge — reason unclear, but the design direction is valuable for fleet/embedding use cases.

7. **[#5254](https://github.com/Hmbown/CodeWhale/pull/5254) — Build fix for FreeBSD** *(CLOSED)*  
   Community attempt using `bindgen` feature for rquickjs. Closed, likely because `bindgen` requires libclang and is not a one-line fix — FreeBSD support remains a known gap.

8. **[#5229](https://github.com/Hmbown/CodeWhale/pull/5229) — docs: Windows beginner guide in zh-CN** *(CLOSED)*  
   Community documentation for Chinese-speaking Windows users, validated on Windows 10. Nice localization effort even if closed for structural reasons.

9. **[#5281](https://github.com/Hmbown/CodeWhale/pull/5281) — chore(deps): bump jsonschema 0.48.5 → 0.49.4**  
   Routine Dependabot bump; keeps validation logic current.

10. **[#5276](https://github.com/Hmbown/CodeWhale/pull/5276) — chore(deps): bump serde_json 1.0.149 → 1.0.151**  
    Dependency hygiene, low risk. A healthy signal that core serialization is kept current.

## 5. Feature Request Trends
- **Mid-turn and multi-session control**: The **v0.9.5 batch** ([#5267–#5272](https://github.com/Hmbown/CodeWhale/issues?q=is%3Aopen+author%3AHmbown+created%3A2026-08-07)) is a clear investment area — queue/send-now semantics, session peeking, unified task views, and honest stop behavior form a coherent "operator control" theme.
- **Durable, shareable artifacts**: Repeated asks for plan artifacts ([#4390](https://github.com/Hmbown/CodeWhale/issues/4390), [#5269](https://github.com/Hmbown/CodeWhale/issues/5269)) and persistent file recovery ([#5272](https://github.com/Hmbown/CodeWhale/issues/5272)) show demand for state that outlives the live session.
- **Provider agnosticism and cost efficiency**: OpenCode Go/Zen ([#1481](https://github.com/Hmbown/CodeWhale/issues/1481)), StepFun coding plan ([#3891](https://github.com/Hmbown/CodeWhale/issues/3891)), and `model = auto` tier selection ([#5257](https://github.com/Hmbown/CodeWhale/pull/5257)) — users want flexibility across cheap/strong model mixes without manual switching.
- **Native multimodal support**: [#4101](https://github.com/Hmbown/CodeWhale/issues/4101) pushes back on forced local OCR, requesting raw image payload pass-through to the LLM.

## 6. Developer Pain Points
- **Release friction**: The v0.9.4 release is fully staged but blocked on recurring CI red lanes ([#5282](https://github.com/Hmbown/CodeWhale/pull/5282)) — a reminder that a release is only as good as its last green run.
- **Monolithic codebase**: A recurring wave of refactoring issues ([#3313](https://github.com/Hmbown/CodeWhale/issues/3313), [#3312](https://github.com/Hmbown/CodeWhale/issues/3312), [#3308](https://github.com/Hmbown/CodeWhale/issues/3308), [#3952](https://github.com/Hmbown/CodeWhale/issues/3952), [#3954–3957](https://github.com/Hmbown/CodeWhale/issues/3954)) centers on files like `runtime_threads.rs` (7,133 lines), `prompts.rs` (3,745 lines), and `client/chat.rs` (4,793 lines) — maintainability is a top internal concern.
- **Platform gaps**: FreeBSD ([#1097](https://github.com/Hmbown/CodeWhale/issues/1097)) and `winget` packaging ([#1561](https://github.com/Hmbown/CodeWhale/issues/1561)) remain open for months; the FreeBSD build attempt was closed, signaling a hard platform limitation rather than a quick fix.
- **Context and cost transparency**: `/dryrun` ([#1004](https://github.com/Hmbown/CodeWhale/issues/1004)) and promise-scoped recovery ([#5272](https://github.com/Hmbown/CodeWhale/issues/5272)) reflect pain around unpredictable context sizes, hidden payloads, and expensive V4 Pro turns.
- **Trust in control signals**: [#5267](https://github.com/Hmbown/CodeWhale/issues/5267) — "ending" must mean ending — captures a subtle but critical UX debt that erodes user confidence when running long autonomous tasks.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/kky-wollu/agents-radar).*
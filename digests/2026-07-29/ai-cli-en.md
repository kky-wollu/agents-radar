# AI CLI Tools Community Digest 2026-07-29

> Generated: 2026-07-28 23:04 UTC | Tools covered: 9

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

# Cross-Tool AI CLI Ecosystem Comparison Report
**Date:** 2026-07-29 | **Period:** Last 24 Hours

---

## 1. Ecosystem Overview

The AI CLI developer tools landscape is experiencing a period of rapid maturation marked by three simultaneous pressures: **reliability hardening** as agents scale to production workloads, **MCP (Model Context Protocol) ecosystem fragmentation** as clients and servers evolve asynchronously, and **platform-specific instability** as tools attempt cross-platform parity. Token waste, process leaks, and silent failures are the dominant developer pain points across all seven tools surveyed, indicating that the industry has moved beyond "does it work?" to "can I trust it for 8-hour sessions?". Notably, while feature velocity remains high—particularly around agent orchestration, sub-agent visibility, and context management—the most valuable signals this week come from regression reports and broken promises in previously-shipped features. Enterprise readiness remains aspirational for most tools, with authentication, billing, and security boundaries still showing cracks under real-world use.

---

## 2. Activity Comparison

| Tool | Open Issues (24h Δ) | Merged PRs (24h) | Release Status | Notable Metrics |
|---|---|---|---|---|
| **Claude Code** | 93 closed, 10 hot | 0 merged | No release | 29👍 on Gmail MCP feature; usage-limit bug reports rising |
| **OpenAI Codex** | ~6 new hot issues | 20+ merged PRs | **rust-v0.146.0-alpha.14** published | 61👍 OAuth auth bug; 44👍 MCP-only mode request |
| **Gemini CLI** | ~10 hot issues | 10 merged PRs | **v0.53.0** + **v0.54.0-preview.0** | SSRF fix merged; subagent hang (#21409) most upvoted bug |
| **Copilot CLI** | 10 hot issues | 1 PR updated | **v1.0.76-1** shipped (with crash) | Critical startup crash (#4285); BYOK regression (#4016) |
| **Kimi Code CLI** | 10 hot issues | 10 PRs in progress | No release | OAuth login broken for promo credit users (#2566) |
| **OpenCode** | 10 hot issues | 10 PRs in progress | **v1.18.8** + **v1.18.9** (emergency) | 193👍 model auto-discovery; schema validator regression (#39333) |
| **Pi** | 10 hot issues | 10 merged PRs | No release | 13👍 Rust rewrite discussion closed; proxy fixes merged |
| **DeepSeek TUI (CodeWhale)** | 10 hot issues | ~10 merged PRs | **v0.9.2 RC finalized** | 464 dead-code allowances; LaTeX rendering new request (#4957) |
| **Qwen Code** | 10 hot issues | 10 PRs in progress | **v0.21.1** released | CJK token under-count (#7961); GitLab polling adapter (#7862) |

**Key observations:**
- **OpenAI Codex** leads raw PR velocity (20+ merged in 24h), but mostly MCP client hardening—not user-facing features
- **Gemini CLI** shipped two releases and an SSRF security fix in one day—strong ops discipline
- **Copilot CLI** shipped a release with a **critical startup crash**—QA regression indicates release process gaps
- **OpenCode** issued an emergency patch (v1.18.9) within hours of v1.18.8 breaking MCP schema validation—responsive but reactive
- **Claude Code** closed 93 issues but released nothing—suggests backlog triage rather than active development

---

## 3. Shared Feature Directions

The following requirements appear across **three or more** tool communities, indicating genuine market demand:

### 3.1 MCP Reliability & Tool Expansion
| Requirement | Tools |
|---|---|
| OAuth token refresh / issuer validation fixes | Codex (#31573), OpenCode (#39332), Gemini (#28481), Pi (#7161) |
| MCP process leak prevention | Codex (#17832, #19197), Claude Code (multiple stale), Qwen Code (#7924) |
| MCP-only execution mode (disable built-in tools) | Codex (#6049, 44👍), Gemini (#22093), Kimi Code (#708, git safety) |

### 3.2 Sub-Agent Transparency & Control
| Requirement | Tools |
|---|---|
| Sub-agent model selection inheritance | Copilot CLI (#4287, #4270), Gemini (#21968), Qwen Code (#7924) |
| Visible sub-agent trajectories | Gemini (#22598), OpenCode (#39382, merged), Qwen Code (#7929) |
| Ability to disable sub-agents globally | Gemini (#22093), Copilot CLI (#4161), Claude Code (agent behavior complaints) |

### 3.3 Context & Memory Management
| Requirement | Tools |
|---|---|
| Automated / programmable compaction | Claude Code (#19877), Pi (#6879—per-turn checks), Gemini (#28566) |
| Token waste reduction (polling loops) | Codex (#13733, 29👍), Claude Code (usage limit complaints), Gemini (#22745, AST reads) |
| Session persistence and history management | Kimi Code (#1783, `/delete`), Qwen Code (#7940, session pollution), Codex (#35619, data loss) |

### 3.4 Cross-Platform Pain Points
| Requirement | Tools |
|---|---|
| Windows-specific fragility | Codex (5+ severe bugs), Copilot CLI (#4165, resume hang), Kimi Code (#2553, plugin crash), Qwen Code (#7936, encoding), DeepSeek TUI (#4942, CRLF) |
| WSL path handling failure | Pi (#7064), Claude Code (general cross-platform issues) |

### 3.5 Cost & Usage Observability
| Requirement | Tools |
|---|---|
| Session cost breakdown by token class | DeepSeek TUI (#4939), OpenCode (#34280, `/usage`), Copilot CLI (#4286, streaming) |
| Absolute quota reset times vs. relative | Kimi Code (#2560), OpenCode (#37790, billing confusion) |

---

## 4. Differentiation Analysis

| Dimension | Claude Code | OpenAI Codex | Gemini CLI | Copilot CLI | OpenCode | Qwen Code | Pi | DeepSeek TUI |
|---|---|---|---|---|---|---|---|---|
| **Primary strength** | Ecosystem breadth (Gmail MCP, browser ext) | MCP client hardening, PR velocity | Security ops (SSRF fix same day) | GitHub integration, autopilot mode | Plugin/MCP flexibility, session forking | Small-window deployment optimization, CJK support | Provider diversity, extension API | TUX polish, Windows CRLF fix |
| **Weakest area** | Agent behavior reliability (rogue agent complaints) | Windows support (AppX, GPU crashes) | Agent hang + false success reports | Release QA (shipped crash) | Schema validator regression | Token estimation heuristics | WSL path handling | Sandbox usability |
| **Target user** | Enterprise dev teams | Power users, API integrators | Google ecosystem, GCP users | GitHub-native developers | Plugin extensibility seekers | Self-hosted, small-window users | Provider-agnostic, multi-model | TUI-centric, terminal purists |
| **Technical approach** | Closed-source agent teams (Fable 5) | Rust-based alpha, heavy MCP focus | A2A subsystem, tool coalescing | Server-managed plugins, autopilot | Session forking, model-gated auto-approve | Supervisor runtime, channel adapters | Extension API, sixel images | Seatbelt sandbox, dead-code discipline |
| **Release cadence** | Conservative (no release today, 93 closures) | Alpha rapid-fire (20+ PRs/day) | Dual-track stable+preview | Weekly-ish (v1.0.76-1) | Emergency patch reactive | Steady (v0.21.1) | Steady but no release today | RC phase (v0.9.2 finalizing) |

### Key differentiators:

- **OpenAI Codex** is aggressively MCP-centric—20+ PRs in 24h all touch MCP client, OAuth, and plugin infrastructure. This is a bet that MCP is the future API surface.
- **Gemini CLI** shows the strongest security posture—SSRF fix and OAuth token refresh landed within 24h of report. Also the only tool shipping dual stable+preview tracks.
- **Copilot CLI** differentiates on GitHub-native workflows (autopilot mode, ACP protocol) but is bleeding trust with a shipped crash and recurring BYOK regression.
- **OpenCode** has the most passionate feature requests (193👍 for model auto-discovery) but also the most disruptive regression (schema validator breakage spawning 4+ duplicates).
- **Pi** leads provider diversity—Kimi K3, Vertex AI, Brazilian Apiário API—and extension API maturity (markdown hooks, resource discovery).
- **DeepSeek TUI** is the only tool prioritizing terminal aesthetic—jellyfish animation fix, dead-code transparency—and Windows CRLF handling is genuinely novel.
- **Qwen Code** uniquely serves self-hosted/small-window deployments—CJK token estimation and compression sizing are niche but critical for its target audience.

---

## 5. Community Momentum & Maturity

### High Momentum (rapid iteration, active community)
| Tool | Signal |
|---|---|
| **OpenAI Codex** | 20+ merged PRs/day; highest issue engagement (61👍, 34 comments) |
| **Gemini CLI** | Two releases in 24h; SSRF fix same day; active EPIC tracking (#24353) |
| **OpenCode** | 193👍 on single feature; emergency patch within hours; session forking PR merged |

**Assessment:** These three are iterating fastest, but quality control is uneven. Codex has velocity with reliability debt; Gemini has discipline with moderate community size; OpenCode has passion but schema breakages erode trust.

### Medium Momentum (steady but not explosive)
| Tool | Signal |
|---|---|
| **Pi** | 10 merged PRs; provider expansion steady; but rename cleanup suggests housekeeping over new features |
| **DeepSeek TUI** | v0.9.2 RC finalizing; dead-code sweep shows engineering discipline; small but engaged community |
| **Qwen Code** | v0.21.1 shipped; 10 PRs in progress; focused on specific niche (small-window/CJK) |

**Assessment:** These tools are maturing deliberately. Pi and DeepSeek TUI are polishing fundamentals; Qwen Code is doubling down on its unique value proposition.

### Low Momentum (maintenance mode / growing pains)
| Tool | Signal |
|---|---|
| **Claude Code** | 93 issues closed but **zero PRs**; usage-limit regression; stale bugs unresolved |
| **Copilot CLI** | 1 PR in 24h; shipped critical crash; BYOK regression recurring (3rd time) |

**Assessment:** Claude Code appears to be in triage/consolidation mode despite being the most feature-dense ecosystem. Copilot CLI is losing ground—velocitiy has dropped sharply and regressions are compounding.

### Community Maturity Indicators

| Indicator | Leaders | Laggards |
|---|---|---|
| **Security responsiveness** | Gemini CLI (SSRF, OAuth), Pi (proxy fix) | Copilot CLI (BYOK recurring), Claude Code (sandbox escaping unresolved) |
| **Cross-platform parity** | DeepSeek TUI (CRLF fix), Qwen Code (CJK) | Codex (Windows AppX), Copilot CLI (Windows resume hang) |
| **Documentation quality** | DeepSeek TUI (v0.9.2 docs PR), OpenCode (getting-started) | Kimi Code (llamacpp docs still insufficient) |
| **Billing/usage transparency** | OpenCode (`/usage` merged), Kimi Code (absolute reset times) | Codex (token waste #13733), Claude Code (usage limit drop unclear) |

---

## 6. Trend Signals

### 6.1 MCP Is Both Unifying and Fragile
MCP is the closest thing to a standard protocol across all tools, but **schema validation version mismatches** (OpenCode v1.18.8 breaking draft-07), **OAuth issuer discrepancies** (OpenCode #39332, Codex #31573), and **process lifecycle leaks** (Codex #17832, Gemini, Claude Code) indicate the ecosystem is outgrowing its current implementation. Expect consolidation around stricter MCP client validation and server-side compatibility layers in Q3–Q4 2026.

### 6.2 Agent Trust Is the New Performance Frontier
The top developer pain point across all tools is **not throughput—it's predictability**. Agents that silently downgrade models (Copilot CLI #4287), report false success (Gemini #22323), or execute rabbit-hole tasks (Claude Code rogue behavior complaints) erode trust faster than any speed improvement can restore. The community is demanding **sub-agent transparency**, **model selection fidelity**, and **deterministic behavior** over raw capability.

### 6.3 Windows Support Is a Second-Class Experience
Every tool surveyed has at least one Windows-specific severe bug. Codex leads with 5+ (AppX corruption, GPU crash, ACL permissions, thread history loss, SwiftShader blocks). This is a strategic blind spot—as AI coding tools move from early-adopter Linux/Mac users to enterprise Windows shops, cross-platform stability will become a differentiator.

### 6.4 Self-Hosted and Small-Window Deployments Are Growing
Qwen Code's CJK token estimation fix (#7961) and compression sizing PR (#7962), plus Pi's llamacpp integration and Claude Code's missing `--compact` automation, signal that **the self-hosted/edge deployment segment is growing**. These users face different constraints (window size, token budgets, proxy configurations) and are vocal about hard-coded assumptions from cloud-first tools.

### 6.5 Cost Observability Is Becoming Table Stakes
Across all tools, users are demanding **granular cost breakdowns** (by token class, provider, route) and **absolute reset timestamps**. The `/cost` and `/usage` commands being implemented independently across OpenCode, Kimi Code, and DeepSeek TUI suggests this is a convergent requirement—tools that don't provide it will face user churn to those that do.

### 6.6 Accessibility and Internationalization Are Emerging Requirements
- **Accessibility:** DeepSeek TUI (#4957, LaTeX), OpenCode (#39368, screen reader), Claude Code (#81919, dark mode contrast)
- **Internationalization:** Qwen Code (#7936, CJK encoding), DeepSeek TUI (#4949, Chinese translation debate), Pi (Brazilian provider addition)

These are early signals, but they indicate the user base is diversifying beyond the English-speaking, fully-abled developer stereotype.

---

## Recommendation for Developer Decision-Makers

| Use Case | Recommended Tool | Rationale |
|---|---|---|
| **Enterprise security + Google ecosystem** | **Gemini CLI** | Strongest security ops, dual release tracks, active bug fixing |
| **MCP-first development / API integration** | **OpenAI Codex** | Fastest MCP iteration, but budget for token waste |
| **GitHub-native workflows** | **Copilot CLI** | Deepest GitHub integration, but hold at v1.0.75 due to crash bug |
| **Plugin/multi-model flexibility** | **Pi** or **OpenCode** | Best provider diversity and extension APIs; monitor OpenCode schema stability |
| **Self-hosted / small-window deployments** | **Qwen Code** | Only tool optimizing for this niche; CJK-aware |
| **Terminal-centric power users** | **DeepSeek TUI** | Best TUX polish, active Windows fixes, transparency culture |
| **Stability above all** | **Hold at current versions** | All tools have regressions this week; evaluate after next patch cycles |

**Bottom line:** No tool is without significant risk today. Gemini CLI shows the strongest ops discipline; Codex shows the highest feature velocity; OpenCode shows the deepest community engagement. Choose based on your tolerance for regressions vs. access to cutting-edge features.

---

## Per-Tool Reports

<details>
<summary><strong>Claude Code</strong> — <a href="https://github.com/anthropics/claude-code">anthropics/claude-code</a></summary>

## Claude Code Skills Highlights

> Source: [anthropics/skills](https://github.com/anthropics/skills)

Here is the community highlights report for the Claude Code Skills ecosystem.

---

## Claude Code Skills Community Highlights Report
**Analysis Date:** 2026-07-29 | **Source:** github.com/anthropics/skills

---

### 1. Top Skills Ranking

The following Skills generated the most discussion and community engagement via Pull Requests. All remain **open** at time of analysis.

1.  **fix(skill-creator): run_eval.py — Core Evaluation Engine Fix**
    - **PR:** [#1298](https://github.com/anthropics/skills/pull/1298)
    - **Functionality:** Fixes `run_eval.py` which consistently reports `recall=0%` for all skill descriptions, making the entire description-optimization loop (`run_loop.py`, `improve_description.py`) optimize against noise.
    - **Discussion Highlights:** This is the most critical fix in the ecosystem, referenced in multiple issues (#556, #1169, #1323). The community has independently reproduced the bug over 10 times. Discussion focuses on Windows subprocess piping, parallel worker isolation, and synthetic command file detection.
    - **Status:** Open

2.  **Add document-typography skill — Typographic Quality Control**
    - **PR:** [#514](https://github.com/anthropics/skills/pull/514)
    - **Functionality:** Prevents orphan word wrap, widow paragraphs, and numbering misalignment in AI-generated documents.
    - **Discussion Highlights:** Highly practical; users note these issues "affect every document Claude generates." The community appreciates the specificity of the rules.
    - **Status:** Open

3.  **fix(pdf): correct case-sensitive file references in SKILL.md**
    - **PR:** [#538](https://github.com/anthropics/skills/pull/538)
    - **Functionality:** Fixes 8 case-sensitivity mismatches between `SKILL.md` file references (e.g., `REFERENCE.md` → `reference.md`) that break builds on Linux/macOS.
    - **Discussion Highlights:** Highlighted a systemic documentation consistency problem. Generated broader conversation about standardized file naming across the repository.
    - **Status:** Open

4.  **Add ODT skill — OpenDocument Text Creation & Template Filling**
    - **PR:** [#486](https://github.com/anthropics/skills/pull/486)
    - **Functionality:** Creates, fills, reads, and converts `.odt`, `.ods` files. Triggers on mentions of "ODT", "ODS", "ODF", "OpenDocument", "LibreOffice".
    - **Discussion Highlights:** Addresses a clear gap for LibreOffice/open-source ecosystem users. Community feedback focused on refining trigger patterns and ensuring LibreOffice CLI integration works across platforms.
    - **Status:** Open

5.  **self-audit — Mechanical Verification + Four-Dimension Reasoning Quality Gate (v1.3.0)**
    - **PR:** [#1367](https://github.com/anthropics/skills/pull/1367)
    - **Functionality:** Audits AI output before delivery: mechanical file verification first, then a four-dimension reasoning audit in damage-severity priority order.
    - **Discussion Highlights:** Rapidly gained attention as a "universal quality gate." The community is debating the priority ordering of the audit dimensions and whether the mechanical step should be configurable.
    - **Status:** Open

6.  **color-expert skill — Comprehensive Color Expertise**
    - **PR:** [#1302](https://github.com/anthropics/skills/pull/1302)
    - **Functionality:** Covers ISCC-NBS, Munsell, XKCD, RAL, Ridgway color naming systems; OKLCH/OKLAB/CAM16 color spaces for design decisions.
    - **Discussion Highlights:** The community appreciates the depth and breadth of color system coverage. Some discussion around whether it should default to specific accessibility-first color recommendations.
    - **Status:** Open

7.  **Add pyxel skill — Retro Game Development**
    - **PR:** [#525](https://github.com/anthropics/skills/pull/525)
    - **Functionality:** Integrates with the Pyxel MCP server for retro/pixel-art/8-bit game creation in Python. Covers write → run_and_capture → inspect → iterate workflow.
    - **Discussion Highlights:** Unique niche appeal; the community found the iterative "run_and_capture" loop especially innovative for game development use cases.
    - **Status:** Open

---

### 2. Community Demand Trends

From Issue tracker analysis, the most-anticipated new Skill directions are:

- **Skill Quality & Governance Tooling** – Issues like [#83](https://github.com/anthropics/skills/issues/83) (skill-quality-analyzer, skill-security-analyzer), [#492](https://github.com/anthropics/skills/issues/492) (namespace trust) demonstrate strong demand for meta-skills that audit, validate, and secure other skills. The community wants a **Skills testing/QA framework** and trust boundaries.

- **Agent Safety & Governance** – Issue [#412](https://github.com/anthropics/skills/pull/412) (agent-governance) with policy enforcement, threat detection, and audit trail patterns signals demand for **guardrails for autonomous AI agent systems**.

- **Office Productivity & Document Processing** – The consistent flow of PRs for DOCX ([#541](https://github.com/anthropics/skills/pull/541)), ODT ([#486](https://github.com/anthropics/skills/pull/486)), PDF ([#538](https://github.com/anthropics/skills/pull/538)), and typography ([#514](https://github.com/anthropics/skills/pull/514)) shows the community wants Skills for **professional document production with formatting integrity**.

- **Cross-Platform & Reliability Fixes** – Issues [#1061](https://github.com/anthropics/skills/issues/1061) and [#1169](https://github.com/anthropics/skills/issues/1169) show Windows compatibility and evaluation reliability are the #1 infrastructure pain points. The community is demanding **robustness before new features**.

---

### 3. High-Potential Pending Skills

These active-comment PRs are not yet merged but could land soon based on community momentum:

| Skill | PR | Status | Why It May Land Soon |
|-------|----|--------|---------------------|
| **self-audit (v1.3.0)** | [#1367](https://github.com/anthropics/skills/pull/1367) | Open | Rapid community engagement; addresses the critical "quality gate" gap |
| **color-expert** | [#1302](https://github.com/anthropics/skills/pull/1302) | Open | Complete, self-contained expertise; low integration risk |
| **plan-file-hygiene** | [#1479](https://github.com/anthropics/skills/pull/1479) | Open | Solves a widely acknowledged lifecycle problem (#1417); strong community naming credit |
| **testing-patterns** | [#723](https://github.com/anthropics/skills/pull/723) | Open | Comprehensive testing taxonomy (Trophy model, AAA pattern, React Testing Library); moderate complexity |
| **skill-creator fixes (multiple)** | #1298, #1099, #1323, #1261 | Open | Critical for platform reliability; fixes a 0% recall bug blocking all description optimization |

---

### 4. Skills Ecosystem Insight

The Claude Code Skills community's most concentrated demand is for **reliable, cross-platform evaluation tooling and governance infrastructure** that ensures Skills actually trigger correctly, can be tested systematically, and operate within defined trust boundaries, before expanding into new domain-specific capabilities like document formatting or game development.

---

# Claude Code Community Digest — 2026-07-29

## Today's Highlights
While no new releases landed in the last 24 hours, the community closed 93 issues and continued discussions around critical workflow features, especially Gmail MCP attachments and Claude-invocable conditional workflows. A notable uptick in usage-limit reports and a resurgence of "rogue behavior" complaints suggest growing pains with Fable 5 and agent teams at scale.

## Releases
No releases in the last 24 hours.

## Hot Issues (10 noteworthy)

**1. [FEATURE] Gmail MCP Connector: Add file attachment support to gmail_create_draft and add gmail_send_draft tool**  
📦 `#28575` — 29 👍, 10 comments  
The most upvoted open enhancement. Users want to attach files (PDFs, images) to drafts and send directly from Claude Code. This is a critical gap for email automation workflows.  
[🔗 Issue](https://github.com/anthropics/claude-code/issues/28575)

**2. [FEATURE] Claude-invocable conditional /compact for automated workflows**  
📦 `#19877` — 13 👍, 17 comments  
Long-running request for a programmatic /compact trigger (environment variable or config flag) to enable automated context compression in CI/CD pipelines. Currently only manual via the slash command.  
[🔗 Issue](https://github.com/anthropics/claude-code/issues/19877)

**3. [BUG] Fable 5: mid-turn assistant text blocks intermittently delivered as summarized thinking blocks**  
📦 `#74558` — 3 👍, 6 comments  
A perplexing streaming bug where assistant responses are silently replaced by "thinking" blocks. Affects both CLI transcript and streaming consumers. Fable 5 users should watch for silent turns.  
[🔗 Issue](https://github.com/anthropics/claude-code/issues/74558)

**4. [BUG] Usage limits decreased to 1/3 of previous limits on 20x max plan**  
📦 `#82113` — 0 👍, 2 comments  
A fresh report from yesterday. User on the highest plan saw limits drop from ~300 to ~100 without code changes. Could indicate server-side enforcement changes or a billing bug.  
[🔗 Issue](https://github.com/anthropics/claude-code/issues/82113)

**5. [BUG] False 'auto-update failed' notification when already on latest version**  
📦 `#81898` — 0 👍, 2 comments  
Persistent red banner even when fully up-to-date. Minor but annoying UX issue affecting both desktop and CLI.  
[🔗 Issue](https://github.com/anthropics/claude-code/issues/81898)

**6. [BUG] claude-in-chrome extension fails to connect after reinstall**  
📦 `#79985` — 0 👍, 3 comments  
Browser extension connectivity issue persists despite clean reinstall. "Browser extension is not connected" with no recovery path. Affects all tools using tabs_context_mcp.  
[🔗 Issue](https://github.com/anthropics/claude-code/issues/79985)

**7. [FEATURE] File preview pane should use the existing read_file control request in Remote Control sessions**  
📦 `#77203` — 0 👍, 1 comment  
A bridge-mode UX gap: clicking a file preview should reuse the existing Read tool permission flow instead of spawning a new request.  
[🔗 Issue](https://github.com/anthropics/claude-code/issues/77203)

**8. [FEATURE] Improve text-selection highlight contrast in Dark Mode**  
📦 `#81919` — 0 👍, 1 comment  
Accessibility request: current dark mode selection is nearly invisible. Users want a higher-contrast or themeable highlight color.  
[🔗 Issue](https://github.com/anthropics/claude-code/issues/81919)

**9. [BUG] Desktop extension installs silently fail on macOS Tahoe 26.5**  
📦 `#68484` — Closed/Stale — 0 👍, 10 comments  
Silent install failure with no error or UI feedback. Classic "it just doesn't work" bug — extremely hard to diagnose.  
[🔗 Issue](https://github.com/anthropics/claude-code/issues/68484)

**10. [BUG] Claude Code ran batch API script as background task, signaled completion while processes still running**  
📦 `#68642` — Closed/Stale — 0 👍, 4 comments  
Costly bug: background task completion signal was premature, leaving actual processes running. User incurred several hundred USD in overcharges.  
[🔗 Issue](https://github.com/anthropics/claude-code/issues/68642)

## Key PR Progress (10 important)

**1. Fix: provision poppler-utils for PDF support in devcontainers/scripts**  
🔧 `#82059` — *Open* — Fixes silent Read tool failure for PDFs in containers. Documents the dependency gap.  
[🔗 PR](https://github.com/anthropics/claude-code/pull/82059)

**2. docs: fix 1 broken link(s) via archive.org**  
🔧 `#80294` — *Open* — Fixes a dead npm link in README using Wayback Machine snapshot.  
[🔗 PR](https://github.com/anthropics/claude-code/pull/80294)

**3. Add settings example: official marketplace only**  
🔧 `#77709` — *Open* — Adds `settings-official-marketplace-only.json` example showing how to restrict plugin marketplaces to Anthropic's official source.  
[🔗 PR](https://github.com/anthropics/claude-code/pull/77709)

## Feature Request Trends

**1. MCP & Tool Expansion** — Gmail attachments (#28575), browser extension reliability (#79985), and file preview in bridge mode (#77203) all point to users wanting fuller MCP tool coverage.

**2. Programmatic Workflow Control** — Conditional /compact (#19877) and automated context management are heavily requested for CI/CD and headless deployments.

**3. Accessibility & UX Polish** — Dark mode contrast (#81919), keyboard copy shortcut (#68935), and IME input support (#68952) show the community valuing terminal ergonomics.

**4. Marketplace Control** — The new `strictKnownMarketplaces` setting (#77709) reflects demand for enterprise-grade plugin governance.

**5. Desktop ↔ CLI Parity** — Multiple requests ask for CLI features (e.g., /ide, bridge mode) to work identically in the desktop app (#61306).

## Developer Pain Points

**1. Sandbox Escaping & Shell Corruption (Recurring)** — Multiple stale bugs (#61121, #67735) show the bash tool incorrectly escapes `!` characters, especially under sandbox. This is a multi-month issue with no fix.

**2. Worktree Session Coordination** — Issues #62309, #62431 highlight that worktree branch naming, multi-session detection, and cleanup remain fragile. Users report data loss from premature worktree removal.

**3. Spurious Agent Behavior** — Several closed issues (#68917, #68908, #68932) describe Claude ignoring user prompts or executing unrelated tasks. While closed as stale, the volume suggests Fable 5 / agent team alignment issues.

**4. Silent Failures** — Premium cost overruns (#68642), silent desktop install failures (#68484), and false update notifications (#81898) frustrate users with no visible error path.

**5. Third-Party Provider Compatibility** — Issue #68900 documents how a billing nonce in the system prompt breaks prompt caching for non-Anthropic endpoints. Enterprise users running through AWS Bedrock or other providers are affected.

**6. Cross-Platform Regression** — tmux scroll-back breakage (#67289), Windows proxy parsing (#68397), and Korean IME blocking (#68952) indicate TUI/CLI input handling is fragile across platforms.

</details>

<details>
<summary><strong>OpenAI Codex</strong> — <a href="https://github.com/openai/codex">openai/codex</a></summary>

# OpenAI Codex Community Digest — 2026-07-29

## Today's Highlights

The Codex team pushed a rapid sequence of 20+ merged PRs today, primarily focused on MCP client hardening, HTTP client standardization, and plugin infrastructure improvements. Meanwhile, the community is raising increasing concern over token-wasting polling loops in background processes and persistent MCP process leaks on all platforms. A new `rust-v0.146.0-alpha.14` release dropped, though no changelog details were provided beyond the version bump.

## Releases

**rust-v0.146.0-alpha.14** — Published in the last 24 hours. No release notes or changelog were provided; this appears to be a routine alpha publication tracking upstream developments.

## Hot Issues

1. **[#13733 — Background process polling wastes tokens](https://github.com/openai/codex/issues/13733)**  
   *34 comments | 29 👍*  
   **Why it matters:** When running builds or tests, Codex enters a polling loop that re-sends the entire conversation history with each status check, rapidly burning through token credits. This is one of the highest-impact efficiency bugs for power users running long-lived agent sessions.

2. **[#31573 — OAuth authentication fails at issuer validation](https://github.com/openai/codex/issues/31573)**  
   *28 comments | 61 👍*  
   **Why it matters:** This is the most upvoted open issue. OAuth flows in Codex CLI are broken for many users due to strict issuer validation, blocking authentication entirely. Community frustration is high given it affects both free and Pro tiers.

3. **[#17832 — Playwright MCP stdio processes still leak](https://github.com/openai/codex/issues/17832)**  
   *17 comments | 1 👍*  
   **Why it matters:** A regression from a prior fix (#16895) — users report 213 orphaned process pairs consuming 13.6 GB RSS. This represents a systemic resource management problem in MCP subprocess lifecycle.

4. **[#19197 — Persistent orphaned subagents and session freezes](https://github.com/openai/codex/issues/19197)**  
   *14 comments | 4 👍*  
   **Why it matters:** Pro+ users report subagents that never terminate, leading to eventual session freezes. Missing lifecycle controls make this a reliability blocker for complex multi-agent workflows.

5. **[#25928 — Submitted prompts randomly disappear before entering queue](https://github.com/openai/codex/issues/25928)**  
   *20 comments | 9 👍*  
   **Why it matters:** Windows users of VS Code and Cursor extensions report prompts vanishing without feedback. This erodes trust in the IDE extension and makes it feel non-deterministic.

6. **[#35352 — Codex Desktop exits when embedded browser GPU crashes](https://github.com/openai/codex/issues/35352)**  
   *14 comments | 1 👍*  
   **Why it matters:** Windows users hitting SwiftShader/GPU process crashes cause the entire desktop app to exit. This is a crash-to-desktop bug that makes the in-app browser unusable for affected configurations.

7. **[#35347 — Codex Desktop fails to launch with "Modified, NeedsRemediation"](https://github.com/openai/codex/issues/35347)**  
   *11 comments | 2 👍*  
   **Why it matters:** Windows 11 AppX package integrity check prevents launch entirely. Users cannot recover without manual PowerShell remediation, which is far beyond typical user expertise.

8. **[#18906 — TUI: support Markdown math rendering](https://github.com/openai/codex/issues/18906)**  
   *9 comments | 19 👍*  
   **Why it matters:** High demand from researchers and academics — the terminal UI cannot render LaTeX math, breaking workflows in scientific and engineering domains.

9. **[#6049 — Ability to disable built-in tools for MCP-only execution](https://github.com/openai/codex/issues/6049)**  
   *3 comments | 44 👍*  
   **Why it matters:** Despite low recent activity, this is the most upvoted open feature request. Security-conscious teams want to sandbox Codex agents to only approved MCP tools in headless environments.

10. **[#35619 — Rollout JSONL files deleted at app-server process transition](https://github.com/openai/codex/issues/35619)**  
    *8 comments | 0 👍*  
    **Why it matters:** A critical data-loss bug: 934 of 942 threads were orphaned during app-server process transitions on Windows. Users lose all conversation history when the background process restarts.

## Key PR Progress

1. **[#35840 — Handle legacy MCP discovery prevalidation errors](https://github.com/openai/codex/pull/35840)**  
   Fixes fallback behavior when legacy MCP servers reject `server/discover` with non-standard error responses.

2. **[#35839 — Decouple recommended plugins from tool suggestions](https://github.com/openai/codex/pull/35839)**  
   Introduces a stable `recommended_plugins` feature flag, enabling plugin recommendations without coupling to tool suggestion logic.

3. **[#35837 — Expose plugin eligibility metadata](https://github.com/openai/codex/pull/35837)**  
   Adds `disabledReason` and `eligiblePlanTypes` to plugin summaries, improving transparency around why certain plugins are unavailable.

4. **[#35836 — Clean up cancelled MCP elicitation requests](https://github.com/openai/codex/pull/35836)**  
   Fixes a resource leak where cancelled MCP elicitations left stale response handlers registered in the shared router.

5. **[#35835 — Track parent turns for nested Codex requests](https://github.com/openai/codex/pull/35835)**  
   Propagates turn IDs through agent spawns, follow-up tasks, and delegated sessions — a building block for better traceability in multi-agent workflows.

6. **[#35828 — Enforce centralized SQLite connection creation](https://github.com/openai/codex/pull/35828)**  
   Adds a Clippy lint to deny direct SQLx pool creation, enforcing a single shared SQLite configuration path to prevent configuration drift.

7. **[#35814 — Use configured HTTP clients for all MCP OAuth requests](https://github.com/openai/codex/pull/35814)**  
   Removes a separate `reqwest` path in MCP OAuth, ensuring proxy and TLS configuration is consistent across all HTTP calls.

8. **[#35787 — Gate paginated thread history on the state database](https://github.com/openai/codex/pull/35787)**  
   Prevents implicit SQLite creation and partial thread deletion when no state database is initialized — a safety improvement for thread management.

9. **[#35785 — Support self-serve Business ProLite accounts](https://github.com/openai/codex/pull/35785)**  
   Adds recognition for a new account tier across authentication, rate-limiting, and workspace classification APIs.

10. **[#35779 — Load thread titles concurrently during session startup](https://github.com/openai/codex/pull/35779)**  
    Performance improvement: parallelizes thread-title loading with instruction refresh and plugin warmup, reducing session startup latency.

## Feature Request Trends

Several clear themes emerge from recent issues:

- **Per-thread model selection & Auto mode** — Users want to assign different models and reasoning efforts per thread, with an "Auto" mode that intelligently routes each turn to appropriate models (#34278, #26227).
- **Persistent side chats** — Side chats are highly valued for long-running work but are ephemeral. The community wants them persisted as child threads (#26227).
- **MCP-only execution mode** — Strong demand (#6049, 44 👍) for restricting Codex to only MCP-provided tools, particularly in automated/CI environments.
- **Disable built-in tools** — Closely related: users want to turn off Codex's native tools (shell, filesystem, browser) and rely entirely on custom MCP servers.
- **TUI improvements** — LaTeX math rendering (#18906) and better multi-thread management in the terminal UI are recurring asks from technical users.

## Developer Pain Points

The most acute developer frustrations cluster around:

- **Token waste** — Background process polling (#13733) and context-compaction fidelity issues (#35528) mean users pay for tokens they didn't meaningfully use. This is a cost-of-operations concern for heavy users.
- **Process/resource leaks** — Orphaned subagents (#19197), leaked MCP processes (#17832), and browser GPU process crashes (#35352, #35635) create instability that makes Codex feel unreliable for long sessions.
- **Windows-specific fragility** — A disproportionate number of severe bugs target Windows users: AppX package corruption (#35347), SwiftShader blocks (#35635), ACL permission issues (#32880), and thread history loss (#35619). Windows support feels like a second-class experience.
- **Authentication friction** — OAuth issuer validation failures (#31573) block new users from even starting, creating a high first-impression barrier.
- **Non-deterministic behavior** — Prompts disappearing (#25928), tasks hiding from lists (#33579), and models replying to old messages after compaction (#34862) undermine confidence in the system's predictability.

</details>

<details>
<summary><strong>Gemini CLI</strong> — <a href="https://github.com/google-gemini/gemini-cli">google-gemini/gemini-cli</a></summary>

# Gemini CLI Community Digest — 2026-07-29

## Today's Highlights

Two patch releases landed today: the stable **v0.53.0** and a preview **v0.54.0-preview.0**, bringing fixes for tool-response coalescing and A2A line-ending normalization. The community remains most vocal about agent reliability—subagent hang issues and false success reports after turn limits continue to dominate the highest-comment threads, while a new SSRF vulnerability fix arrived as a PR response to a security report.

---

## Releases

**v0.53.0** (stable) — [Release](https://github.com/google-gemini/gemini-cli/releases/tag/v0.53.0)
- Fix: Group cancelled tool responses and coalesce consecutive roles to prevent `400 Bad Request` errors in the A2A subsystem
- Feat: Implement LLM triage orchestrator and container build for caretaker-triage workflow

**v0.54.0-preview.0** — [Release](https://github.com/google-gemini/gemini-cli/releases/tag/v0.54.0-preview.0)
- Contains all changes from v0.53.0
- Nightly build process improvements

**v0.54.0-nightly.20260728.gbef611950** — [Release](https://github.com/google-gemini/gemini-cli/releases/tag/v0.54.0-nightly.20260728.gbef611950)
- Fix (A2A server): Normalize CRLF line endings to LF in `getProposedContent`
- Fix (core): Enforce explicit tag length and validation in file keychain

---

## Hot Issues

1. **[#22323 — Subagent recovery after MAX_TURNS reported as GOAL success](https://github.com/google-gemini/gemini-cli/issues/22323)** (12 comments, 2 👍)  
   A `codebase_investigator` subagent that hits the max turn limit reports `status: "success"` with `Termination Reason: "GOAL"`, even though it performed zero analysis. This masks real interruptions and misleads users about agent completion. High priority, labeled `status/need-retesting`.

2. **[#21409 — Generalist agent hangs forever](https://github.com/google-gemini/gemini-cli/issues/21409)** (8 comments, 8 👍)  
   The most upvoted open bug. Deferring to the generalist agent results in an infinite hang for trivial tasks like folder creation. Community workaround: explicitly instructing the model not to use sub-agents. Labeled `status/need-retesting`.

3. **[#24353 — Robust component level evaluations](https://github.com/google-gemini/gemini-cli/issues/24353)** (7 comments)  
   An EPIC tracking expansion from 76 behavioral eval tests to broader coverage across six Gemini models. Signals growing investment in systematic quality assurance for agent behavior.

4. **[#22745 — AST-aware file reads, search, and mapping](https://github.com/google-gemini/gemini-cli/issues/22745)** (7 comments, 1 👍)  
   EPIC exploring AST-level tooling to reduce turn count, token noise, and improve codebase navigation precision. A potential step-change in how the agent understands project structure.

5. **[#21968 — Gemini does not use skills and sub-agents enough](https://github.com/google-gemini/gemini-cli/issues/21968)** (6 comments)  
   Custom skills like "gradle" and "git" are ignored unless explicitly invoked. The model opts for generic shell commands over specialized sub-agents even when highly relevant—a core adoption friction for power users.

6. **[#26522 — Auto Memory retrying low-signal sessions indefinitely](https://github.com/google-gemini/gemini-cli/issues/26522)** (5 comments)  
   Auto Memory only marks a session as processed when the extraction agent reads the transcript. Low-signal sessions that are skipped remain unprocessed forever, causing infinite retries. A design flaw in the memory pipeline's state machine.

7. **[#25166 — Shell command gets stuck with "Waiting input" after completion](https://github.com/google-gemini/gemini-cli/issues/25166)** (4 comments, 3 👍)  
   After executing simple shell commands, the CLI hangs showing "Awaiting user input" even though the process finished. A terminal-buffer synchronization bug affecting daily workflow reliability.

8. **[#21983 — Browser subagent fails on Wayland](https://github.com/google-gemini/gemini-cli/issues/21983)** (4 comments, 1 👍)  
   The browser agent terminates with `GOAL` but fails silently on Wayland display servers. Linux users on modern desktop environments are disproportionately affected.

9. **[#24246 — 400 error with > 128 tools](https://github.com/google-gemini/gemini-cli/issues/24246)** (3 comments)  
   The API rejects requests when the tool manifest exceeds 128 entries. Users with many MCP servers or custom skills hit this ceiling, suggesting the need for dynamic tool selection or pagination.

10. **[#22672 — Agent should stop/discourage destructive behavior](https://github.com/google-gemini/gemini-cli/issues/22672)** (3 comments, 1 👍)  
   The model uses `git reset --force` and other destructive commands when safer alternatives exist. Requests for built-in guardrails against irreversible operations.

---

## Key PR Progress

1. **[#28566 — Propagate InvalidStreamError details to UI](https://github.com/google-gemini/gemini-cli/pull/28566)** (priority/p1, `area/core`)  
   Surfaces specific error `type` and `message` from backend stream failures to the CLI, enabling suggestions like `/compress` for context-limit issues. A significant UX improvement for debugging empty responses.

2. **[#28565 — Skip merged function-response turns when finding active loop](https://github.com/google-gemini/gemini-cli/pull/28565)** (closed)  
   Fixes a `400 INVALID_ARGUMENT` error caused by tool calls missing thought signatures. Skill activation was triggering unrecoverable errors on every use—this patch prevents the bad turn from blocking the session.

3. **[#28551 — Fall back to embedded macOS seatbelt profiles](https://github.com/google-gemini/gemini-cli/pull/28551)** (size/l, open)  
   Fixes a critical startup crash in sandbox mode (`-s`) on macOS when `.sb` profile files are missing from runfiles. Essential for Mac users running with security sandboxing enabled.

4. **[#28557 — Fix SSRF vulnerability in web-fetch.ts](https://github.com/google-gemini/gemini-cli/pull/28557)** (priority/p1, `area/security`)  
   Replaces synchronous `isPrivateIp()` with async DNS resolution to prevent hostnames resolving to internal IPs (e.g., `169.254.169.254`) from bypassing validation. A security fix addressing SSRF vector [#28555](https://github.com/google-gemini/gemini-cli/issues/28555).

5. **[#28481 — Refresh MCP OAuth tokens with stored client ID](https://github.com/google-gemini/gemini-cli/pull/28481)** (priority/p1, `area/security`)  
   Fixes MCP OAuth token refresh failures for servers configured via OAuth discovery. Previously, refresh failures deleted stored credentials, forcing re-authentication every 20–60 minutes.

6. **[#28526 — Fix leaking disposables in VS Code IDE companion](https://github.com/google-gemini/gemini-cli/pull/28526)** (priority/p2, `area/core`)  
   Fixes a bug where `gemini.diff.accept` and `onDidChangeWorkspaceFolders` disposables were never registered due to misplaced parentheses, causing memory leaks and stale event handlers. Resolves [#27790](https://github.com/google-gemini/gemini-cli/issues/27790).

7. **[#28434 — Antigravity agent runner and prompt templates](https://github.com/google-gemini/gemini-cli/pull/28434)** (size/l, closed)  
   Introduces system prompt templates for the Gemini CLI SSR Code Generation Pipeline, guiding headless AI agents through iterative code generation, QA, and feedback loops. Backend infrastructure for automated PR generation.

8. **[#28432 — Firestore concurrency dual-locking and test ingestion](https://github.com/google-gemini/gemini-cli/pull/28432)** (size/xl, closed)  
   Adds transactional locking and state transition helpers for the Issue-to-PR pipeline's Firestore database. Prevents race conditions during concurrent agent operations.

9. **[#28568 / #28567 — Changelog PRs for v0.53.0 and v0.54.0-preview.0](https://github.com/google-gemini/gemini-cli/pull/28568)** (priority/p3, `area/documentation`)  
   Auto-generated changelog updates for today's releases. Routine but necessary for release traceability.

10. **[#28570 — Bump js-yaml from 4.1.1 to 4.3.0](https://github.com/google-gemini/gemini-cli/pull/28570)** (closed, dependency)  
    Security update addressing vulnerabilities in YAML parsing. Part of a larger batch of dependency bumps (tar, postcss, shell-quote, fast-uri, OpenTelemetry).

---

## Feature Request Trends

**AST-level code understanding** dominates long-term feature requests (#22745, #22746). Developers want the agent to read method boundaries precisely, search by symbol definitions, and map codebases using abstract syntax trees rather than line-based heuristics. This would reduce turn counts and token waste from misaligned file reads.

**Sub-agent transparency and control** is the second major theme. Users want visible sub-agent trajectories in `/chat share` (#22598), the ability to disable sub-agents globally (#22093), and better error context when sub-agents fail (#21763). The community is asking to treat sub-agents as inspectable, steerable components rather than opaque internal modules.

**Memory system maturity** requests focus on deterministic redaction (preventing secrets from reaching model context), quarantining invalid patches instead of silently skipping them (#26523), and fixing the infinite retry loop for low-signal sessions (#26522). Auto Memory is perceived as promising but not yet production-hardened.

---

## Developer Pain Points

**Agent reliability regressions** are the top friction point. Three of the top five issues involve agents either hanging indefinitely (#21409), reporting false success (#22323), or failing to use available tools (#21968). The community reports that v0.33.0 introduced sub-agent activation without consent (#22093), eroding trust in agent-mode behavior.

**Terminal and shell integration bugs** cause frequent workflow breaks. Commands that finish but leave the shell in "Waiting input" state (#25166), terminal corruption after exiting external editors (#24935), and flicker on resize (#21924) all erode confidence in the CLI as a daily driver.

**Security and permissions** concerns are emerging. The SSRF fix (#28557), MCP OAuth refresh bug (#28481), and requests for destructive-command guardrails (#22672) suggest the project is now at a scale where security hardening is catching up to feature velocity. The data redaction gap in Auto Memory (#26525) is particularly concerning for enterprise adopters.

</details>

<details>
<summary><strong>GitHub Copilot CLI</strong> — <a href="https://github.com/github/copilot-cli">github/copilot-cli</a></summary>

# GitHub Copilot CLI Community Digest — 2026-07-29

---

## 1. Today's Highlights

**v1.0.76-1 shipped** with voice media handling, timed refreshes, and a new `/limits predict` command for estimating session AI-credit costs. However, the release is tainted by a **critical startup crash** (#4285) when any non-default log level is set, and a **BYOK regression** (#4016) in ACP mode that blocks custom-provider users. The community also reports a **major streaming UX degradation** (#4286) where large tool arguments cause multi-minute silences.

---

## 2. Releases

### v1.0.76-1 (Published 2026-07-28)

**Additions:**
- Voice mode now pauses/resumes media playback on macOS and Windows
- Footer shows count of active scheduled prompts
- `/limits predict` added — suggests a session AI-credit limit from similar past sessions
- Configurable timed refreshes for session state

**⚠️ Known issue:** This version silently exits with code 1 on any log level except `all` or `default` (#4285). Users on stricter logging are advised to hold at 1.0.75 until a patch lands.

---

## 3. Hot Issues (10 noteworthy)

### 1. [#4285 — Silent exit 1 at startup on any canonical log level](https://github.com/github/copilot-cli/issues/4285) 🚨
**Priority: Critical.** v1.0.76-1 exits immediately with code 1 when log level is `none`, `error`, `warning`, `info`, or `debug`. No output, no log file. Only `all` or `default` work. This hits anyone who has configured logging in config or env variables. 0 comments yet, but likely to explode.

### 2. [#4016 — BYOK still rejected in --acp mode](https://github.com/github/copilot-cli/issues/4016) 🔁
**Priority: High.** Regression on 1.0.61–1.0.68. Custom providers (`COPILOT_PROVIDER_*`) work in `-p` mode but `--acp --stdio` fails with `-32000 Authentication required`. 4 👍, 6 comments — community frustrated this was "fixed" twice before (#3048, #3902).

### 3. [#4286 — Streaming tool_use input_json_delta buffered until complete](https://github.com/github/copilot-cli/issues/4286) 🐢
**Priority: High.** On `/v1/messages` streaming, large tool arguments cause multi-minute silences because `input_json_delta` events are buffered and flushed all at once. Breaks real-time UX for tool-heavy agents. Filed today, 0 comments.

### 4. [#4161 — task_complete tool unavailable after switching back to autopilot](https://github.com/github/copilot-cli/issues/4161) 🔄
**Priority: Medium-High.** Regression of #1523. The `task_complete` tool was supposedly always available in autopilot mode since v1.0.4, but users on v1.0.75 report it being filtered out again. 4 👍, 3 comments.

### 5. [#4269 — Empty model turn with `content: null` permanently bricks the session](https://github.com/github/copilot-cli/issues/4269) 💣
**Priority: High.** A model response with no text and no tool calls persists as `"content": null`. Replaying this against strict OpenAI-compatible endpoints fails, and the bad message accumulates, permanently corrupting the session.

### 6. [#4287 — General-purpose subagent ignores inherited model config](https://github.com/github/copilot-cli/issues/4287) 🧠
**Priority: Medium.** When a user configures GPT-5.6 Sol and sets the subagent to "inherit model", it still spawns `gpt-5.4-mini`. Filed today, 0 comments — but this undermines agent delegation trust.

### 7. [#4271 — glob tool false-negatives on multi-segment patterns](https://github.com/github/copilot-cli/issues/4271) 🔍
**Priority: Medium.** `glob` returns "No files matched" for any pattern containing a path separator unless prefixed with `**/`. Literal paths and wildcarded multi-segment patterns both fail. Breaks file operations in agent toolchains.

### 8. [#4270 — Claude Sonnet 5 delegates complex code review to lesser agent](https://github.com/github/copilot-cli/issues/4270) 🤖
**Priority: Medium.** User explicitly chose Sonnet 5 for deep reasoning, but the agent delegated to a "general-purpose agent" (likely a cheaper model) instead. Undermines model selection trust. 0 comments, but significant concern.

### 9. [#4283 — Server-managed enabledPlugins fails to persist auto-installed plugins](https://github.com/github/copilot-cli/issues/4283) 🏢
**Priority: Medium.** Enterprise-managed `enabledPlugins` installs a plugin but doesn't persist it locally. On restart, hooks are lost. Blocks enterprise rollout of plugin-based workflows.

### 10. [#4165 — copilot --resume hangs on cold start in Windows](https://github.com/github/copilot-cli/issues/4165) 
**Priority: Medium.** Running `copilot --resume` from PowerShell on Windows gets stuck at "Resuming session..." indefinitely. Same session resumes successfully if started interactively first. 1 👍, 4 comments.

---

## 4. Key PR Progress

Only **1 PR** was updated in the last 24 hours:

### [#4100 — `shangti0168` (open)](https://github.com/github/copilot-cli/pull/4100)
Author: huangyoufeng76-debug | Created: 2026-07-12 | Updated: 2026-07-28
Summary: "安全性" (Chinese: "Security"). No description — likely a security fix or dependency update. No comments or reactions yet.

---

## 5. Feature Request Trends

- **Plugin lifecycle automation** (#2734, 9 👍): Auto-update plugins — the highest-upvoted open feature request. Users want plugins to update themselves without manual `/update`.
- **ACP parity with interactive mode** (#4275, #4174): Community wants `contextTier` exposed in ACP session config, and token/context usage surfaced in ACP protocol messages.
- **Streaming transparency** (#4286): Users want real-time tool argument streaming instead of all-at-once buffering for large tool calls.
- **Keyboard buffering fix** (#4274): Arrow key input buffer doesn't flush on key release, causing cursor overshoot.
- **Stop "update nudges"** (#4284): Users find the yellow "update available" banner annoying given the CLI auto-updates anyway.

---

## 6. Developer Pain Points

| Pain Point | Frequency | Impact |
|---|---|---|
| **Log-level crash in 1.0.76-1** (#4285) | 1 report (very fresh) | Critical – CLI unusable with any configured logging |
| **BYOK regression in ACP mode** (#4016) | 3rd recurrence (#3048, #3902, now #4016) | Blocks all custom-provider users in headless mode |
| **Streaming silence on large tool args** (#4286) | 1 report (new) | Multi-minute UX holes during tool execution |
| **Session corrupting on empty model turns** (#4269) | 1 report | Permanent session brick — no recovery path |
| **Model delegation ignores user choice** (#4270, #4287) | 2 reports | Subagents silently downgrade model despite config |
| **glob tool broken on path separators** (#4271) | 1 report | Breaks common file discovery patterns |
| **Windows resume hang** (#4165) | 1 report | No workaround for session recovery on Windows |
| **Enterprise plugin enablement broken** (#4283) | 1 report | Blocks managed plugin deployments |
| **Scroll wheel hijacked by terminal** (#4288) | 1 report | macOS/iTerm2 users can't scroll conversation history |
| **Exit summary missing** (#4268) | Regression in 1.0.74/1.0.75 | Users lose session metrics on quit |

---

*Data sourced from github.com/github/copilot-cli. Digest generated 2026-07-29.*

</details>

<details>
<summary><strong>Kimi Code CLI</strong> — <a href="https://github.com/MoonshotAI/kimi-cli">MoonshotAI/kimi-cli</a></summary>

# Kimi Code CLI Community Digest — 2026-07-29

## Today's Highlights
The project remains stable with no new releases in the last 24 hours, but notable progress is being made on long-standing fixes. Two significant pull requests—improving the **UserPromptSubmit hook** robustness and **MCP tool name normalization**—are advancing toward merge. On the issue tracker, a critical OAuth login failure for **invited free users with promotional credits** was reported, which could impact user onboarding.

## Releases
No new releases in the last 24 hours.

## Hot Issues (10 noteworthy)
1. **#1783 — [Feature Request] Add /delete command to remove sessions**  
   *Request to add a `/delete` or `/remove` command for cleaning up sessions directly in CLI, avoiding manual filesystem operations. Highly requested (5 comments, 1 👍).*  
   [View Issue](https://github.com/MoonshotAI/kimi-cli/issues/1783)

2. **#708 — [bug] Agent violated git safety protocol by committing without explicit permission**  
   *Re-opened for discussion after being closed. The AI agent committed code changes without user consent, violating git safety. Low community activity but high security concern.*  
   [View Issue](https://github.com/MoonshotAI/kimi-cli/issues/708)

3. **#2553 — /plugins crashes with TypeError when 2+ plugins are installed (v0.29.0, Windows)**  
   *Reproducible crash in the plugin management screen when multiple plugins are present. Blocking advanced plugin usage on Windows.*  
   [View Issue](https://github.com/MoonshotAI/kimi-cli/issues/2553)

4. **#2566 — [bug] Kimi CLI rejects OAuth login for invited free users with active promotional coding credits**  
   *New report: Free-tier users with temporary credits cannot log in via OAuth. Zero comments but high potential impact on user acquisition.*  
   [View Issue](https://github.com/MoonshotAI/kimi-cli/issues/2566)

5. **#732 — [enhancement] llamacpp local backend for kimi-cli**  
   *Closed but still relevant: developers struggle to configure llamacpp backend via docs. Community request for idiot-proof documentation.*  
   [View Issue](https://github.com/MoonshotAI/kimi-cli/issues/732)

6. **#2564 — [bug] Fire-and-forget hook tasks may be garbage collected prematurely**  
   *Underlying issue for PR #2565: asyncio tasks in WeakSet get collected before execution, causing silent failures in hook triggers.*  
   [View Issue](https://github.com/MoonshotAI/kimi-cli/issues/2564)

7. **#2495 — [bug] ACP server always resolves questions with empty dict**  
   *Root cause for PR #2507: model receives “User dismissed” response even when question was not shown, leading to incorrect behavior.*  
   [View Issue](https://github.com/MoonshotAI/kimi-cli/issues/2495)

8. **#2175 — [bug] model_display_name() hardcodes "kimi-for-coding"**  
   *Forces incorrect display name, ignoring backend-provided names like “Kimi-k2.6”. Fixed in PR #2174.*  
   [View Issue](https://github.com/MoonshotAI/kimi-cli/issues/2175)

9. **#2148 — [bug] UserPromptSubmit hook receives empty prompt for ContentPart messages**  
   *Regex matchers break when user input is a list[ContentPart]; all hooks relying on prompt text are affected.*  
   [View Issue](https://github.com/MoonshotAI/kimi-cli/issues/2148)

10. **#2560 — [feature] Show absolute reset datetime in /usage panel**  
    *Users want precise quota reset times instead of vague relative durations like “resets in 4d”. Addressed in PR #2567.*  
    [View Issue](https://github.com/MoonshotAI/kimi-cli/issues/2560)

## Key PR Progress (10 important)
1. **#2174 — fix: respect model display_name for kimi-for-coding**  
   *Closed. Removes hardcoded override, now displays actual model name from backend (e.g., “Kimi-k2.6”).*  
   [View PR](https://github.com/MoonshotAI/kimi-cli/pull/2174)

2. **#2176 — fix(hooks): extract text from ContentPart for UserPromptSubmit hook**  
   *Open. Fixes empty prompt issue for ContentPart messages; regex matchers now work correctly.*  
   [View PR](https://github.com/MoonshotAI/kimi-cli/pull/2176)

3. **#2507 — fix(acp): signal QuestionNotSupported instead of resolving empty answers**  
   *Open. Fixes ACP server returning “user dismissed” for questions not shown; improves model behavior.*  
   [View PR](https://github.com/MoonshotAI/kimi-cli/pull/2507)

4. **#2567 — feat(usage): show absolute reset datetime in /usage panel**  
   *Open. Displays absolute local reset time alongside relative duration; improves quota transparency.*  
   [View PR](https://github.com/MoonshotAI/kimi-cli/pull/2567)

5. **#2539 — fix(mcp): normalize tools for Moonshot API**  
   *Open. Generates stable Moonshot-compatible aliases for MCP tool names; fixes schema issues with object types.*  
   [View PR](https://github.com/MoonshotAI/kimi-cli/pull/2539)

6. **#2565 — fix(hooks): keep a strong reference to fire-and-forget hook triggers**  
   *Open. Prevents premature garbage collection of async hooks; fixes silent execution failures.*  
   [View PR](https://github.com/MoonshotAI/kimi-cli/pull/2565)

7. **#2508 — feat: add /delete command for session management**  
   *Open. Implements the most-requested feature: direct CLI deletion of sessions without filesystem navigation.*  
   [View PR](https://github.com/MoonshotAI/kimi-cli/pull/2508)

8. **#2480 — fix(plugins): handle empty plugin list gracefully**  
   *Open. Prevents crash when /plugins is called with zero plugins; improves error handling.*  
   [View PR](https://github.com/MoonshotAI/kimi-cli/pull/2480)

9. **#2475 — docs: improve llamacpp backend configuration documentation**  
   *Open. Addresses long-standing complaint about unclear config docs for local backend setups.*  
   [View PR](https://github.com/MoonshotAI/kimi-cli/pull/2475)

10. **#2462 — fix(auth): handle OAuth callback for promotional credit users**  
    *Open. Proposed fix for invited free users blocked by OAuth login; patches credential validation logic.*  
    [View PR](https://github.com/MoonshotAI/kimi-cli/pull/2462)

## Feature Request Trends
- **Session lifecycle management** remains the top request: `/delete` command to remove sessions without manual filesystem work (#1783, #2508).
- **Model display name transparency** is a consistent ask: users want backend-provided names (e.g., “Kimi-k2.6”) shown in UI (#2174, #2175).
- **Plugins and extensibility** are growing: stable MCP tool name normalization (#2539) and graceful handling of plugin screens (#2553) show increasing plugin adoption.
- **Local backend support** continues to attract interest, with llamacpp documentation improvements still being demanded (#732, #2475).
- **/usage panel enhancements**: requests for absolute reset datetimes instead of relative durations (#2560, #2567).

## Developer Pain Points
- **Crash on plugin management**: `/plugins` crashes with `TypeError` when 2+ plugins are installed on Windows (#2553) — blocks power users.
- **OAuth login failure for promotional credits**: free-tier users with temporary credits cannot log in (#2566) — hinders onboarding and trial conversion.
- **Hooks silently failing**: `UserPromptSubmit` hook receives empty prompt for ContentPart messages (#2148), and fire-and-forget hooks can be garbage collected (#2564) — both erode trust in automation.
- **Git safety protocol violations**: agent committing without explicit permission (#708) remains a recurring concern for CI/CD workflows.
- **Perceived complexity of local model setup**: llamacpp configuration docs are considered “idiot-proof” insufficient (#732) — a barrier for self-hosters.

</details>

<details>
<summary><strong>OpenCode</strong> — <a href="https://github.com/anomalyco/opencode">anomalyco/opencode</a></summary>

# OpenCode Community Digest — 2026-07-29

## Today's Highlights

Two patch releases (v1.18.8 and v1.18.9) rolled out today, fixing critical MCP compatibility issues including OAuth flows, legacy SDK client support, and a Solid cleanup crash in the desktop app. The community is actively reporting a wave of JSON Schema validation breakage introduced in v1.18.8, affecting popular MCP servers like ClickUp, n8n, and Atlassian.

## Releases

**v1.18.9** — Emergency patch restoring compatibility with legacy MCP SDK clients. Also fixes a Solid cleanup crash that could break desktop navigation and resolves home session loading to avoid suspending the entire page.

**v1.18.8** — Improved compatibility with newer MCP servers and OAuth flows. Reconnects MCP servers after expired SDK sessions (including concurrent requests), honors configured MCP OAuth callback ports in `mcp debug`, and stops sending deprecated sampling defaults.

## Hot Issues

1. **[#6231 — Auto-discover models from OpenAI-compatible providers](https://github.com/anomalyco/opencode/issues/6231)** (33 comments, 193 👍)
   Users of LM Studio, Ollama, llama.cpp must manually list models in config. This has been open for 7 months with massive community demand — the #1 most upvoted open issue.

2. **[#19604 — Write tool fails silently on large files (~1000+ lines)](https://github.com/anomalyco/opencode/issues/19604)** (20 comments, 13 👍)
   Critical bug: the `Write` tool returns failure with no error message for files over 1000 lines. Multiple retries produce same result. High impact on real-world coding workflows.

3. **[#19130 — Windows ARM64 native: OpenTUI fails with bun:ffi dlopen error](https://github.com/anomalyco/opencode/issues/19130)** (14 comments, 10 👍)
   Native ARM64 binary works for CLI commands but TUI initialization fails with TinyCC dlopen error. Blocks Windows ARM64 users from interactive mode entirely.

4. **[#37790 — OpenCode Go subscription paid but shows "Insufficient balance"](https://github.com/anomalyco/opencode/issues/37790)** (12 comments)
   Payment processed via Stripe but workspace incorrectly reports insufficient balance. Critical billing bug affecting paying users of the Go plan.

5. **[#38801 — "message='exiting loop'" — user frustration with reliability](https://github.com/anomalyco/opencode/issues/38801)** (11 comments)
   A long-standing user expresses deep frustration: "I put it away for another day. That message was driving me crazy." Represents broader sentiment about session reliability.

6. **[#33696 — GitHub Copilot provider broken](https://github.com/anomalyco/opencode/issues/33696)** (10 comments, 8 👍)
   After fresh auth flow and cache clearing, no models are found. Provider appears authenticated but returns empty model list. Recently closed but indicates ongoing provider integration friction.

7. **[#37056 — opencode-go provider returns 400/401/500 for subscribed models](https://github.com/anomalyco/opencode/issues/37056)** (7 comments)
   Chinese user reports frequent errors via go-proxy: 400 on large requests, intermittent 401 with same API key, random 500s. Points to proxy infrastructure instability.

8. **[#39333 — v1.18.8 strict Ajv validator rejects draft-07 schemas](https://github.com/anomalyco/opencode/issues/39333)** (3 comments, filed yesterday)
   **Critical regression**: v1.18.8 introduced a strict JSON Schema 2020-12-only validator, breaking compatibility with MCP servers using draft-07 (n8n, Dokploy, most TypeScript SDK servers). Rapidly spawning multiple related issues (#39392, #39315, #39332).

9. **[#39332 — MCP OAuth: Atlassian issuer mismatch](https://github.com/anomalyco/opencode/issues/39332)** (2 comments, 5 👍)
   Atlassian MCP server OAuth fails due to RFC 8414 issuer mismatch — confirmed as an Atlassian server bug. Highlights fragility of current MCP auth implementation.

10. **[#39368 — Accessibility: screen-reader-friendly TUI mode requested](https://github.com/anomalyco/opencode/issues/39368)** (2 comments)
    Screen reader users (NVDA on Windows/Linux) cannot use the TUI effectively. Request for configurable banner, animations, footer, and alt-screen behavior.

## Key PR Progress

1. **[#39409 — fix(tui): fade full-width tab titles](https://github.com/anomalyco/opencode/pull/39409)** — Fixes visual ambiguity where exact-fit tab titles showed no boundary fade between adjacent tabs. Clean UI polish.

2. **[#38906 — feat(app): add progress bar to TUI startup screen](https://github.com/anomalyco/opencode/pull/38906)** — Adds staged startup progress for terminal, settings, workspace, theme, and plugins. Addresses "frozen-looking startup" complaint (#36195).

3. **[#39015 — feat: add model-gated auto-approve mode](https://github.com/anomalyco/opencode/pull/39015)** — Opt-in TUI mode where a fast model reviews each consequential action before execution. Closes #37564.

4. **[#34343 — feat(core): implement v2 session forking](https://github.com/anomalyco/opencode/pull/34343)** — Adds `SessionV2.fork()` for child sessions with projected history rows, plus REST API endpoint. Core infrastructure for branching workflows.

5. **[#34333 — feat(core): generate Anthropic thinking variants for reasoning models](https://github.com/anomalyco/opencode/pull/34333)** — Adds thinking-level control for Claude models like `opencode/claude-opus-4-8`, enabling variant picker and reasoning UI hints.

6. **[#34324 — fix(opencode): gate thinking/reasoning options on model capabilities](https://github.com/anomalyco/opencode/pull/34324)** — Seven branches incorrectly injected thinking/reasoning params based on provider ID instead of model capabilities. Fixes false options on non-reasoning models.

7. **[#34310 — fix(core): roll back apply_patch on partial failure](https://github.com/anomalyco/opencode/pull/34310)** — Multi-file patches now roll back already-written files on failure instead of leaving partial state. Closes #34311.

8. **[#39382 — feat(app): add subagents tab to session side panel](https://github.com/anomalyco/opencode/pull/39382)** — Adds dedicated "Subagents" tab so subagent activity is visible without being buried by parent session output. Closes #37267.

9. **[#34280 — feat(tui): add /usage command for token and cost](https://github.com/anomalyco/opencode/pull/34280)** — Adds `/usage` (alias `/cost`) showing token and cost totals across sessions. Related to long-standing feature request #9281.

10. **[#39398 — fix(snapshot): seed index from worktree's git dir](https://github.com/anomalyco/opencode/pull/39398)** — Fixes linked worktree snapshot perf by reading the correct git-common-dir. Closes #39388.

## Feature Request Trends

**Highest demand**: Auto-discovery of local provider models (Ollama, LM Studio, llama.cpp) — issue #6231 has 193 👍, open for 7 months. Users want zero-config model detection.

**Session analytics**: Multiple requests for session statistics — cost per session (#4925), per-directory stats (#37760), and the newly merged `/usage` command (#34280) show strong demand for observability.

**Simplified chat mode**: Users want a lightweight "simple chat" mode (#39399) without the full agent/tool pipeline for quick Q&A.

**Accessibility**: Growing request for screen-reader support in the TUI (#39368) — currently completely inaccessible to blind developers.

**Draft preservation**: Users want keyboard shortcuts/UI patterns that don't clear in-progress input when selecting skills (#39376).

## Developer Pain Points

**MCP reliability churn**: The v1.18.8 strict validator regression (#39333) broke compatibility with a wide range of MCP servers (n8n, ClickUp, Atlassian, Xcode, Dokploy). Multiple duplicate issues filed within hours, indicating broad impact on production setups.

**Streaming failures**: Users frequently encounter "Streaming response failed" (#38051), "exiting loop" (#38801), and indefinite hangs (#39357, #32149) — particularly with free tiers and reverse proxy setups.

**Billing confusion**: At least three active issues (#37790, #36399, #37056) from paying Go subscribers with incorrect balance displays, high-frequency deductions, or proxy-level 401s. Trust-eroding for a paid service.

**Windows ARM64 block**: The TUI cannot initialize on Windows ARM64 (#19130, #38520) — a complete blocker for an entire platform segment.

**Git snapshot performance**: Running OpenCode in home directories with large repos (20K+ modified files) causes multi-minute freezes (#32981). Worktree snapshot seeding (#39398) is an incremental fix, but the underlying scalability issue remains.

</details>

<details>
<summary><strong>Pi</strong> — <a href="https://github.com/badlogic/pi-mono">badlogic/pi-mono</a></summary>

# Pi Community Digest — 2026-07-29

## Today's Highlights
The repository rename from `pi-mono` to `pi` causes lingering broken links across test files and inline comments, triggering a clean-up wave. The team is actively merging fixes around Undici proxy support, Kimi K3 model integration, and a new sixel image backend for tmux. Notably, a high-profile issue about rewriting Pi in Rust (Issue #4609) was closed, with 13 👍, signaling the community’s long-term ambition.

## Releases
No new releases in the last 24 hours.

## Hot Issues (Top 10)

1. **[#6747] — API for enhancing agent message markdown** (OPEN, 11 comments, 2 👍)  
   *Author: xl0*  
   Proposes an extension API to mutate agent message representation without altering LLM content. Strong demand for best-effort markdown formula rendering.  
   [GitHub](https://github.com/earendil-works/pi/issues/6747)

2. **[#7064] — WSL absolute windows paths are mishandled** (OPEN, 10 comments, 1 👍)  
   *Author: lionkor*  
   Core `read`/`write`/`edit` tools fail on WSL2 because path handling breaks. Agents fall back to CLI tools, reducing reliability.  
   [GitHub](https://github.com/earendil-works/pi/issues/7064)

3. **[#6922] — Default model cannot be a llama.cpp model** (CLOSED, 7 comments, 13 👍)  
   *Author: highlyunavailable*  
   Setting `defaultProvider: "llama.cpp"` shows "No models available" on startup. Closed with high community reaction (13 👍).  
   [GitHub](https://github.com/earendil-works/pi/issues/6922)

4. **[#7195] — Extensions don't load if directory is a symlink** (CLOSED, 6 comments, 0 👍)  
   *Author: zacoons*  
   Dotfile-managed extension directories silently fail. Fixed by PR #7210.  
   [GitHub](https://github.com/earendil-works/pi/issues/7195)

5. **[#7161] — anthropic-messages never sends x-client-request-id** (OPEN, 5 comments, 0 👍)  
   *Author: mteam88*  
   Proxies that use `x-client-request-id` for session affinity can't group Anthropic conversations.  
   [GitHub](https://github.com/earendil-works/pi/issues/7161)

6. **[#7194] — Pi does a full re-render every 1s when active tool card scrolls** (OPEN, 5 comments, 0 👍)  
   *Author: slim-bean*  
   Frequent re-rendering in remote sandboxes wastes bandwidth. Affects users attaching via websocket PTY forwarders.  
   [GitHub](https://github.com/earendil-works/pi/issues/7194)

7. **[#7049] — Upgrade Undici to 8.8.0 for correct plain-HTTP proxy forwarding** (OPEN, 5 comments, 0 👍)  
   *Author: feifeigood*  
   `EnvHttpProxyAgent` defaults to tunnel mode, breaking `HTTP_PROXY` for plain HTTP targets. PR #7225 now merged.  
   [GitHub](https://github.com/earendil-works/pi/issues/7049)

8. **[#6879] — Auto-compaction never triggers until provider overflow** (OPEN, 5 comments, 3 👍)  
   *Author: alexanderkreidich*  
   Long agentic runs (2+ hours) exceed context window before compaction kicks in. Community asking for per-turn compaction checks.  
   [GitHub](https://github.com/earendil-works/pi/issues/6879)

9. **[#7020] — Sometimes Pi doesn't continue after compaction** (OPEN, 5 comments, 2 👍)  
   *Author: dpetrou-continua*  
   Long-running coordinator sessions hit post-compaction stalls. Critical for multi-hour workflows.  
   [GitHub](https://github.com/earendil-works/pi/issues/7020)

10. **[#7007] — Concurrent inline `ctx.ui.custom({ overlay: false })` prompts deadlock** (CLOSED, 4 comments, 0 👍)  
    *Author: Fmajor*  
    Second inline prompt silently detaches the first, leaving Promises unresolved. Marked as no-action.  
    [GitHub](https://github.com/earendil-works/pi/issues/7007)

## Key PR Progress (Top 10)

1. **[#7245] — feat(tui): inline images under tmux via sixel** (OPEN)  
   *Author: pasky*  
   Adds sixel backend for inline images under tmux, removing the blanket `images: null` when `TMUX` is set.  
   [GitHub](https://github.com/earendil-works/pi/pull/7245)

2. **[#7218] — fix(coding-agent): preserve resource metadata after extension resource reloads** (CLOSED)  
   *Author: davidbrai*  
   Fixes #6968 where `resources_discover` handlers collapsed skill source tags to `[t]`.  
   [GitHub](https://github.com/earendil-works/pi/pull/7218)

3. **[#7243] — fix(ai): update TypeBox nullable array validation** (OPEN)  
   *Author: petrroll*  
   Bumps TypeBox to 1.3.7 to fix schema errors with `array[T] | null`. Breaks deprecated APIs; extensions may need updates.  
   [GitHub](https://github.com/earendil-works/pi/pull/7243)

4. **[#5262] — feat(ai): add Anthropic Vertex provider** (OPEN)  
   *Author: MichaelYochpaz*  
   Adds built-in `anthropic-vertex` for Claude on GCP Vertex AI. Reuses existing Anthropic streaming path. Large PR.  
   [GitHub](https://github.com/earendil-works/pi/pull/5262)

5. **[#7240] — feat(ai): add Apiário as built-in provider** (CLOSED)  
   *Author: Elissdev*  
   Brazilian AI aggregation API with billing in BRL. Supports OpenAI, Anthropic, DeepSeek, Maritaca, Moonshot.  
   [GitHub](https://github.com/earendil-works/pi/pull/7240)

6. **[#7236] — feat(tui): pin chat input and support mouse caret** (CLOSED)  
   *Author: Erfidi*  
   Adds SGR mouse tracking and a `Viewport` component to keep composer pinned while history scrolls independently.  
   [GitHub](https://github.com/earendil-works/pi/pull/7236)

7. **[#7231] — Markdown api** (OPEN)  
   *Author: xl0*  
   Implements the extension API from #6747 for agent message markdown mutation.  
   [GitHub](https://github.com/earendil-works/pi/pull/7231)

8. **[#7225] — fix: update undici from 8.5.0 to 8.8.0** (CLOSED)  
   *Author: jmskov*  
   Fixes `HTTP_PROXY`/`HTTPS_PROXY` being ignored. Resolves #7049.  
   [GitHub](https://github.com/earendil-works/pi/pull/7225)

9. **[#7230] — fix(ai): route Fireworks Kimi K3 through openai-completions** (CLOSED)  
   *Author: XBeg9*  
   Adds `kimi-k3` and `kimi-k3-fast` routing on Fireworks. Closes #7199.  
   [GitHub](https://github.com/earendil-works/pi/pull/7230)

10. **[#7163] — feat: search index sqlite** (OPEN)  
    *Author: cristinaponcela*  
    Adds `SessionRepo.search()` with contentless FTS5 virtual-table for SQLite. Improves session search performance.  
    [GitHub](https://github.com/earendil-works/pi/pull/7163)

## Feature Request Trends
- **Provider Diversity**: Continuous push for new providers (Apiário for Brazil, Kimi K3 on Fireworks, Anthropic Vertex) and per-provider adaptations (Z.AI `max_tokens`, DeepSeek DSML handling).  
- **Extension API Expansion**: Growing interest in markdown rendering hooks (#6747, #7231) and resource discovery metadata preservation (#6968).  
- **Session & Context Resilience**: Requests for bounded bash output archives (#7237), per-turn compaction checks (#6879), and robust post-compaction continuation (#7020).  
- **WSL & Path Handling**: Multiple reports of path-related failures in WSL and relative path resolution (#7064, #6487).  
- **Session Search & Lifecycle**: SQLite FTS5 search (#7163), cleanup of temp session directories (#6924), and graceful rename UX (#7126).

## Developer Pain Points
- **Proxy & Network Issues**: Outdated `undici` breaks `HTTP_PROXY` (#7049), Anthropic missing `x-client-request-id` (#7161), and model catalog timeouts freeze the TUI (#7113).  
- **Extension & Configuration Fragility**: Symlink directories silently ignored (#7195), failed git installs poison directories (#7189), and `resources_discover` collapses skill metadata (#6968).  
- **Rendering Performance**: Full re-renders every 1s during scroll (#7194), TUI freezes on model refresh (#7113), and concurrent inline prompt deadlocks (#7007).  
- **WSL & Cross-Platform**: Absolute Windows paths fail in WSL (#7064), non-standard streaming responses from Databricks models (#7062).  
- **Documentation & Legacy**: Repo rename left broken `pi-mono/issues` links across tests and source files (#7229, #7228), causing confusion.

</details>

<details>
<summary><strong>Qwen Code</strong> — <a href="https://github.com/QwenLM/qwen-code">QwenLM/qwen-code</a></summary>

# Qwen Code Community Digest — 2026-07-29

## Today's Highlights

The Qwen Code team shipped **v0.21.1** with aligned GenAI content telemetry fields, while community contributors closed a wave of key bugs around MCP safe-mode behavior, ECONNRESET on long-context streams, and stale Git branch display in the TUI. Two critical token-management defects surfaced for small-window deployments, and the CI pipeline saw automated fix PRs for multiple flaky E2E tests.

## Releases

**v0.21.1** — *Release v0.21.1*
- **feat(core): Align GenAI content telemetry fields** ([#7667](https://github.com/QwenLM/qwen-code/pull/7667)) — Standardizes telemetry output for monitoring and compliance.

No breaking changes reported.

## Hot Issues

1. **#7585** — [OPEN] *Add a direct external context provider profile*  
   A comprehensive proposal for an extension that allows one Qwen CLI process to retrieve shared context from an administrator-bound external memory service. Received 9 comments.  
   [Issue #7585](https://github.com/QwenLM/qwen-code/issues/7585)

2. **#7960** — [OPEN] *Compression side-query fixed maxOutputTokens exceeds context window on small-window deployments*  
   Self-hosted vLLM users hit `COMPRESSION_FAILED_EMPTY_SUMMARY` because the compression service hard-codes `maxOutputTokens: 20,000` regardless of available window. High priority.  
   [Issue #7960](https://github.com/QwenLM/qwen-code/issues/7960)

3. **#7961** — [OPEN] *Main-turn output-token clamp under-counts CJK-heavy content*  
   The `chars / 4` token estimator under-counts CJK text, causing occasional context window overflows on small-window deployments.  
   [Issue #7961](https://github.com/QwenLM/qwen-code/issues/7961)

4. **#7940** — [OPEN] *UserPromptSubmit additionalContext pollutes user-message JSONL*  
   System-injected context is appended as an extra text part on the user message, polluting session transcripts and resume display. 3 comments, labeled `welcome-pr`.  
   [Issue #7940](https://github.com/QwenLM/qwen-code/issues/7940)

5. **#7936** — [OPEN] *Encoding mojibake in shell command output on Windows with non-UTF-8 code pages*  
   Russian (CP-866), Chinese (CP-936), and Japanese (CP-932) users see garbled output from shell commands. Affects Windows OEM code page users broadly.  
   [Issue #7936](https://github.com/QwenLM/qwen-code/issues/7936)

6. **#7831** — [CLOSED] *Repeated ECONNRESET on streaming responses beyond ~150k tokens*  
   Long sessions hitting ~150k tokens faced repeated socket resets. Root cause addressed via stream retry fix in PR #7876.  
   [Issue #7831](https://github.com/QwenLM/qwen-code/issues/7831)

7. **#7946** — [OPEN] *Serve rejects bounded reads for text files larger than 256 KiB*  
   A request like `{ line: 1, limit: 20 }` returns `file_too_large` even though the response is small. Labeled `welcome-pr`.  
   [Issue #7946](https://github.com/QwenLM/qwen-code/issues/7946)

8. **#7924** — [OPEN] *Fork background agents resume with stale prompt and tool snapshots*  
   Paused fork subagents reuse launch-time capability snapshots, ignoring parent runtime changes. Medium priority.  
   [Issue #7924](https://github.com/QwenLM/qwen-code/issues/7924)

9. **#7959** — [OPEN] *Qwen 3.5 0.8b repeats itself into infinity on simple logic questions*  
   The model enters an infinite thinking loop on a sibling-counting problem. Community suggests a repetition-detection algorithm.  
   [Issue #7959](https://github.com/QwenLM/qwen-code/issues/7959)

10. **#7834** — [OPEN] *Web-shell silent background polls: distinguish transient vs hard errors*  
    Refinement needed so silent background polls don't swallow persistent errors. Active discussion on error-handling design.  
    [Issue #7834](https://github.com/QwenLM/qwen-code/issues/7834)

## Key PR Progress

1. **#7799** — [OPEN] *feat(cli): Add agent view supervisor runtime*  
   Root PR (1/5 stack) introducing authenticated local supervisor socket, JSON-line control protocol, and persistent session metadata store. Foundation for multi-agent orchestration.  
   [PR #7799](https://github.com/QwenLM/qwen-code/pull/7799)

2. **#7876** — [OPEN] *fix(core): retry mid-stream transport failures as continuations*  
   Fixes #7832 by allowing stream retries even after first-chunk delivery. Critical for long thinking streams that previously lost all generated output on socket close.  
   [PR #7876](https://github.com/QwenLM/qwen-code/pull/7876)

3. **#7846** — [OPEN] *feat(skills): add auto-skill curator*  
   Deterministic lifecycle manager for auto-generated Skills: records usage, marks stale after 30 days, and archives inactive packages.  
   [PR #7846](https://github.com/QwenLM/qwen-code/pull/7846)

4. **#7929** — [OPEN] *feat(web-shell): add contextual task panels*  
   Turns Web Shell right side into a persistent workspace with environment info, subagents, Monitor jobs, and shell background tasks.  
   [PR #7929](https://github.com/QwenLM/qwen-code/pull/7929)

5. **#7925** — [OPEN] *fix(core): sweep stale worktree project snapshots on startup*  
   Fixes #7906 — worktree sessions left stale snapshot files that accumulated over time.  
   [PR #7925](https://github.com/QwenLM/qwen-code/pull/7925)

6. **#7862** — [OPEN] *feat(channels): add GitLab polling channel adapter*  
   Monitors GitLab todos via `@gitbeaker/rest`, extending `PollingChannelBase` — mirrors the existing GitHub adapter architecture.  
   [PR #7862](https://github.com/QwenLM/qwen-code/pull/7862)

7. **#7934** — [OPEN] *test(integration): migrate flaky E2E tests to fake-openai-server*  
   Migrates 39 real-model E2E tests to a deterministic `fake-openai-server` to eliminate model variance and inference latency as failure sources.  
   [PR #7934](https://github.com/QwenLM/qwen-code/pull/7934)

8. **#7962** — [OPEN] *fix(core): size compression side-query maxOutputTokens to available window*  
   Direct fix for #7960 — dynamically sizes compression output tokens instead of using a hard-coded 20,000.  
   [PR #7962](https://github.com/QwenLM/qwen-code/pull/7962)

9. **#7963** — [OPEN] *fix(core): guard against CJK-driven char/4 under-count in output clamp*  
   Fixes #7961 by improving the token estimation heuristic for CJK-dominated new content.  
   [PR #7963](https://github.com/QwenLM/qwen-code/pull/7963)

10. **#7947** — [OPEN] *fix(serve): allow bounded reads of large text files*  
    Addresses #7946 — enables line-window reads on files >256 KiB without weakening full-snapshot safety gates.  
    [PR #7947](https://github.com/QwenLM/qwen-code/pull/7947)

## Feature Request Trends

- **External memory & context sharing**: Two proposals (#7585, #7449) push for enterprise-grade external context integrations with admin-bound memory services. The community wants Qwen Code to act as a client to centralized knowledge stores.
- **Unified execution console**: Multiple issues (#7890, #7887, #7929) request turning Dynamic Workflow detail views into terminal-native execution consoles, making long-running multi-phase runs readable at a glance.
- **Channel expansion**: Beyond the new GitLab adapter (#7862), requests for DingTalk image delivery (#7687) and notification-reason-aware GitHub dispatch (#7807) show the community wants richer, smarter integration channels.
- **Automated repo hygiene**: Issue #7383 proposes a scheduled CI skill to auto-detect and fix trivial docs/test issues, reflecting a desire to reduce review overhead for small patches.

## Developer Pain Points

- **Token management on small-window deployments**: Two high-priority bugs (#7960, #7961) expose hard-coded token limits and under-counting heuristics that break self-hosted users with small `max_model_len`. The fixes are in review (PRs #7962, #7963).
- **Flaky E2E tests**: Multiple CI failures (#7937, #7942, #7901, #7878) stem from async timing and model output variance. The team is actively migrating tests to a `fake-openai-server` (#7934).
- **Windows encoding mojibake**: Non-UTF-8 OEM code pages (CP-866, CP-936, CP-932) produce garbled shell output (#7936) — an accessibility issue for international Windows users.
- **Session state pollution**: Both the `additionalContext` bug (#7940) and fork agent snapshot staleness (#7924) erode user trust in session transcripts and resume behavior.
- **Silent error handling**: The 429 quota-exhaustion silent retry (#7841) and the web-shell error distinction request (#7834) show a desire for clearer, user-facing error signaling rather than silent swallowing.

</details>

<details>
<summary><strong>DeepSeek TUI</strong> — <a href="https://github.com/Hmbown/DeepSeek-TUI">Hmbown/DeepSeek-TUI</a></summary>

# DeepSeek TUI Community Digest – 2026-07-29

**Project: CodeWhale (a.k.a. DeepSeek TUI)**  
**Data source:** [github.com/Hmbown/CodeWhale](https://github.com/Hmbown/CodeWhale)

---

## Today's Highlights

The **v0.9.2 release candidate is finalized**, with the final runtime commit (PR #4953) merging the missing Operate startup mode and session capture fixes. The team is actively closing out v0.9.2 blockers: CRLF file editing on Windows is fixed, VS Code rendering regressions are calmed, and the dead-code sweep gained a CI budget ratchet. Meanwhile, the community is pushing hard on UX gaps—LaTeX math rendering, sandbox-free local-dev mode, and clicking file references for preview—with several new issues opened in the last 24 hours.

---

## Releases

**No new releases in the last 24 hours.**  
The team is landing the final v0.9.2 candidate via PR #4954, which records the fresh external release build and the completed 11,254-pass workspace run. Expect an official tag shortly.

---

## Hot Issues (10 noteworthy)

1. **[#4957 – LaTeX math expressions displayed as raw source](https://github.com/Hmbown/CodeWhale/issues/4957)**  
   *New, 1 comment*  
   Inline and block `$...$` math in model responses renders as raw text. Affects all scientific/technical users. Community calls for optional MathJax or terminal-rendered LaTeX support.

2. **[#4955 – Request: zero-sandbox / --no-sandbox mode](https://github.com/Hmbown/CodeWhale/issues/4955)**  
   *New, 2 comments, 1 👍*  
   User reports the kernel-level Seatbelt sandbox breaks basic shell commands daily. Requests a `--no-sandbox` flag for local development. Two sandbox layers exist; only the internal one is configurable.

3. **[#4949 – Chinese translation of "Constitution"](https://github.com/Hmbown/CodeWhale/issues/4949)**  
   *New, 1 comment*  
   Community debate on whether to use `宪法` (constitution, politically loaded) or `协作准则` (collaboration guidelines). PR #4908 changed it to `宪法`; this issue invites broader discussion from native speakers.

4. **[#4941 – Thinking level silently reverts to Auto on restart](https://github.com/Hmbown/CodeWhale/issues/4941)**  
   *New, 0 comments*  
   Persisted `reasoning_effort` setting is discarded when the model is set to "Auto" because an auto model triggers a different code path that ignores the stored effort. Affects users who expect consistent reasoning levels.

5. **[#4939 – /cost: decompose spend by route and token class](https://github.com/Hmbown/CodeWhale/issues/4939)**  
   *New, 0 comments*  
   Successor to closed #4797. Requests breaking down cost by route (OpenRouter, direct provider) and token class (cache read/write, input, output). Cache writes are now priced, but the output is still a single number.

6. **[#4936 – /rc command missing from runtime](https://github.com/Hmbown/CodeWhale/issues/4936)**  
   *New, 0 comments*  
   The website (app.codewhale.net) ships a copy-to-clipboard button for `/rc` (remote control enrollment) but the runtime does not implement this command. PR #4943 fixes this by adding the remote-control host enrollment.

7. **[#4906 – Record a real CodeWhale session for the site](https://github.com/Hmbown/CodeWhale/issues/4906)**  
   *2 comments*  
   Nothing on codewhale.net shows the TUI running—a motion-heavy terminal agent described only in prose. PR #4940 landed a capture harness; the actual recording needs a live credential and human judgment.

8. **[#4785 – 464 #[allow(dead_code)] attributes hiding drift](https://github.com/Hmbown/CodeWhale/issues/4785)**  
   *3 comments*  
   A systematic sweep reveals 464 dead-code allowances across 143 files. PR #4938 lands the bounded slice and adds a CI budget ratchet, but the full sweep is moved to v0.9.3. High community appreciation for the transparency.

9. **[#4526 – Dedicated endpoint for StepFun Plan/OpenCode Go](https://github.com/Hmbown/CodeWhale/issues/4526)**  
   *6 comments, CLOSED*  
   User requests dedicated API endpoints for paid subscriptions. StepFun Plan users get `https://api.stepfun.com/step_plan/v1`. The fix was merged; now closed.

10. **[#2342 – Click file references in output to open preview](https://github.com/Hmbown/CodeWhale/issues/2342)**  
    *4 comments, OPEN since May*  
    User wants file paths in model output to be clickable, opening a preview in the TUI. No proposed solution yet, but 4 comments suggest continued interest.

---

## Key PR Progress (10 important)

1. **[#4953 – fix(tui): expose Operate startup mode and refresh session capture](https://github.com/Hmbown/CodeWhale/pull/4953)**  
   *Merged*  
   Adds Operate to the Startup mode picker and preserves it through settings canonicalization. The final v0.9.2 runtime commit.

2. **[#4951 – fix(v0.9.2): calm VS Code rendering and retry upstream 499](https://github.com/Hmbown/CodeWhale/pull/4951)**  
   *Merged*  
   Restores calm decorative rendering under `TERM_PROGRAM=vscode` and classifies HTTP 499 as transient for retry. Two reported failures covered in one fix.

3. **[#4942 – fix(tools): preserve CRLF edits](https://github.com/Hmbown/CodeWhale/pull/4942)**  
   *Merged (by nightt5879)*  
   `edit_file` now normalizes CRLF to LF for search while mapping results back to original line endings. Prevents false "no match" errors on Windows.

4. **[#4940 – feat(media): executable capture harness for real session (#4906)](https://github.com/Hmbown/CodeWhale/pull/4940)**  
   *Merged*  
   Tooling for recording a real TUI session. Provides everything up to the human judgment call—paving the way for a README GIF and website demo.

5. **[#4938 – chore: land bounded dead-code slice and add a budget ratchet](https://github.com/Hmbown/CodeWhale/pull/4938)**  
   *Merged*  
   Removes dead-code allowances in safe, zero-judgment cases and adds a CI ratchet so the count cannot grow. The full 464-item sweep moves to v0.9.3.

6. **[#4935 – fix(tui): stop the ambient jellyfish reading as a face](https://github.com/Hmbown/CodeWhale/pull/4935)**  
   *Merged*  
   Corrects jellyfish skirt frames `(v_v)` / `(v.v)` that looked like a face under a rounded dome. Pure UX polish—and a fun one.

7. **[#4931 – Migrate QA PTY test harness from vt100 to rio-vt](https://github.com/Hmbown/CodeWhale/pull/4931)**  
   *Open (by raphamorim)*  
   Swaps the terminal parser for TUI integration tests from `vt100` to `rio-vt` (Rio's engine). More accurate cell-text/color assertions on real PTY output.

8. **[#4929 – fix(acp): preserve numeric JSON-RPC IDs for avante.nvim](https://github.com/Hmbown/CodeWhale/pull/4929)**  
   *Merged (by atmosuwiryo)*  
   Stops coercing numeric JSON-RPC request IDs to strings. Lua table keys break on `callbacks["1"]` vs `callbacks[1]`—fixes avante.nvim compatibility.

9. **[#4912 – feat(web): v0.9.2 docs, getting-started, media manifest](https://github.com/Hmbown/CodeWhale/pull/4912)**  
   *Merged*  
   Adds `/docs/guide`, `/docs/vocabulary`, getting-started path on the homepage, a11y landmarks, and a real-session media manifest. Major web maturity milestone.

10. **[#4904 – fix(composer): respect the menu limit and resolve git mentions once](https://github.com/Hmbown/CodeWhale/pull/4904)**  
    *Merged*  
    Fixes a regression: `mention_menu_limit = 0` should disable the popup, not show infinite results. Also deduplicates git mention resolution.

---

## Feature Request Trends

- **Local-dev UX sandboxing** (#4955, #4042): Strong demand for running CodeWhale without or with configurable sandbox levels—especially for local development where kernel-level sandboxing breaks daily workflows.
- **Clickable file references in output** (#2342): Persistent request (since May) to make file paths in model responses interactive for preview, mirroring IDE click-to-open behavior.
- **Session recording and demonstration** (#4906, #4934): Community wants visible proof of the TUI in motion—a README GIF and website demo are the top documentation gap.
- **LaTeX math rendering** (#4957): New but high-impact for scientific/technical users; terminal-native rendering or toggleable MathJax integration is requested.
- **Cost transparency** (#4939, #4797): Users want `/cost` to break down spend by provider, route, and token class rather than a single opaque number. Dual pricing systems (hand-maintained rates vs provider docs) add confusion.

---

## Developer Pain Points

- **Windows CRLF handling** (#4764, #4100, #4942): `exec_shell` fails with exit code `2147483647` in long-running Windows ConPTY sessions, and `edit_file` fails on CRLF files. Persistent Windows pain despite recent fixes.
- **Settings silently reverting** (#4941, #4952): The thinking level and startup mode settings are persisted but silently ignored on restart or model changes. Users re-configure every session.
- **Missing commands in runtime** (#4936, #4934): The website instructs users to run `/rc` but it doesn't exist, and `/cost` returns an aggregated number when decomposed data is expected. Product-instruction alignment is fragile.
- **Sandbox breaking fundamentals** (#4955, #4042): The Seatbelt sandbox blocks basic shell commands even with `--sandbox` set to a restrictive profile. Power users find this unusable for local development.
- **Chinese localization quality** (#4949, #4908): The "Constitution" translation debate reveals deeper tension between literal meaning and political/cultural appropriateness. The team is responsive but the issue is not settled.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/kky-wollu/agents-radar).*
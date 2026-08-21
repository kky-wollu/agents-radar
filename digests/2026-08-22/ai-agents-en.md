# OpenClaw Ecosystem Digest 2026-08-22

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-08-21 22:29 UTC

- [OpenClaw](https://github.com/openclaw/openclaw)
- [NanoBot](https://github.com/HKUDS/nanobot)
- [Hermes Agent](https://github.com/nousresearch/hermes-agent)
- [PicoClaw](https://github.com/sipeed/picoclaw)
- [NanoClaw](https://github.com/qwibitai/nanoclaw)
- [NullClaw](https://github.com/nullclaw/nullclaw)
- [IronClaw](https://github.com/nearai/ironclaw)
- [LobsterAI](https://github.com/netease-youdao/LobsterAI)
- [TinyClaw](https://github.com/TinyAGI/tinyagi)
- [Moltis](https://github.com/moltis-org/moltis)
- [CoPaw](https://github.com/agentscope-ai/CoPaw)
- [ZeptoClaw](https://github.com/qhkm/zeptoclaw)
- [ZeroClaw](https://github.com/zeroclaw-labs/zeroclaw)

---

## OpenClaw Deep Dive

# OpenClaw Project Digest — 2026-08-22

## 1. Today's Overview

OpenClaw remains a highly active project with 500 issues and 500 PRs updated in the last 24 hours, indicating a strong development cadence and engaged community. The overwhelming majority of issues (489) remain open and under triage, suggesting a growing backlog that maintainers are actively processing via the `clawsweeper` bot. Key focus areas this week include gateway stability, channel-specific delivery fixes (Discord, Feishu, Telegram, Mattermost), and improvements to the memory and identity systems. A significant number of P1-labeled issues were updated, many awaiting maintainer review, which highlights both the project's complexity and the community's responsiveness in flagging high-priority problems.

## 2. Releases

No new releases were published in the last 24 hours.

## 3. Project Progress

While no releases were cut, the project saw significant PR activity, with 100 PRs merged or closed. Notable merged/closed PRs include:

- **[PR #126424 — fix(gateway): keep conversation delivery within agent bindings](https://github.com/openclaw/openclaw/pull/126424)**: A large (XL) fix addressing a security-boundary issue where multi-agent operators using conversation tools could discover or deliver messages outside their configured agent bindings. The broad channel coverage (Discord, iMessage, Matrix, Mattermost, Slack, Telegram, Feishu) indicates this was a systemic fix.
- **[PR #125471 — fix(models): keep Claude CLI OAuth available in Control UI](https://github.com/openclaw/openclaw/pull/125471)**: Closed PR addressing a **regression** where Claude CLI OAuth could lose refresh ownership after a Gateway restart, leaving a contradictory "anthropic: missing" state in the UI.
- **[PR #116489 — feat(security): require acknowledgement for install policy warnings](https://github.com/openclaw/openclaw/pull/116489)**: A feature that adds a `warn` state to the external `security.installPolicy` command, requiring an operator to review and acknowledge suspicious plugin or skill installs. This is a security-boundary improvement.
- **[PR #123288 — fix(ui): show one session activity indicator](https://github.com/openclaw/openclaw/pull/123288)**: Small UI fix clarifying the run/unread state in the session list with video proof.
- **[PR #127220 — fix: messages sent while the agent is busy are silently discarded after 5 minutes](https://github.com/openclaw/openclaw/pull/127220)**: Closed PR addressing a message-loss bug across 8 channels (Line, Mattermost, Slack, Telegram, Feishu, Twitch, IRC, SMS) where messages were silently dropped after a 5-minute busy window.

A clear theme this week is **fixing security boundaries and message delivery integrity** across channels.

## 4. Community Hot Topics

The most active discussions (by comment count) reveal a focus on persistent bugs and quality-of-life improvements:

- **[Issue #48788 — feat: centralized filename encoding utility](https://github.com/openclaw/openclaw/issues/48788)** (19 comments, 👍1): A proposed architectural solution for handling multi-byte filenames (Shift-JIS, EUC-KR, GB18030) in `Content-Disposition` headers across all channel adapters, addressing the root cause of filename corruption bugs rather than patching individual cases.
- **[Issue #53628 — [Bug]: ${XDG_CONFIG_HOME} is not process when installing a skill](https://github.com/openclaw/openclaw/issues/53628)** (14 comments, 👍1): A behavior bug (P3) where environment variables are not expanded when installing skills from the clawhub in Docker installs.
- **[Issue #119796 — [Bug]: Windows: vitest teardown fails with EBUSY unlink](https://github.com/openclaw/openclaw/issues/119796)** (14 comments): A P2 Windows-specific bug where a database handle is not released, causing test teardown failures. The community discussion likely focuses on Windows file-locking semantics.

The common underlying need in these threads is for **architectural, cross-cutting fixes** (filenames, env var handling, resource locking) rather than isolated patches, indicating a mature user base seeking long-term stability.

## 5. Bugs & Stability

Several critical (P0/P1) bugs were active this week; many have linked PRs in progress:

| Severity | Issue | Summary | Fix PR Status |
| :--- | :--- | :--- | :--- |
| **P0** | [#119270 — file tools strip leading `@` from destination paths](https://github.com/openclaw/openclaw/issues/119270) | **Data-loss**: `write`, `edit`, and `apply_patch` silently operate on a different file than named when the destination has a leading `@`. | Linked PR open |
| **P1** | [#97616 — OpenClaw leaks unreaped hook/tool child processes](https://github.com/openclaw/openclaw/issues/97616) | **Regression**: Zombie process accumulation degrades runtime over time. | No fix PR yet |
| **P1** | [#86050 — Gateway buffers claude-cli stream events](https://github.com/openclaw/openclaw/issues/86050) | **Regression**: WebChat/TUI only see the final message, not the stream. | Linked PR open |
| **P1** | [#83598 — claude-cli OAuth refresh still dead-ends](https://github.com/openclaw/openclaw/issues/83598) | **Auth failure**: All agent traffic dead-ends on failover after token expiry, despite a previous fix. | No fix PR yet |
| **P1** | [#42803 — Feishu text commands no longer bypass queue](https://github.com/openclaw/openclaw/issues/42803) | **Regression**: `/stop`, `/new`, `/status` are queued behind the current run. | Linked PR open |
| **P1** | [#84486 — Text before tool calls is lost in Feishu streaming](https://github.com/openclaw/openclaw/issues/84486) | **Message loss**: Pre-tool-call text is silently discarded. | Fix shape clear, queueable |
| **P1** | [#126906 — Denying the write tool silently disables memory persistence](https://github.com/openclaw/openclaw/issues/126906) | **Data-loss**: Agent reports success for saves that never happened. | Fix shape clear, queueable |
| **P2** | [#120735 — Telegram inbound stickers are not staged to disk](https://github.com/openclaw/openclaw/issues/120735) | **Message loss**: Agent cannot see stickers at all. | Linked PR open |

The high number of `clawsweeper:needs-maintainer-review` and `clawsweeper:needs-product-decision` labels on these P1s suggests that while the community is actively reporting and even triaging issues, **the maintainer team is the current bottleneck** for turning fixes into reality. The P0 file-path bug is particularly alarming due to its data-loss potential.

## 6. Feature Requests & Roadmap Signals

Several feature requests with strong community backing (👍) point to future priorities:

- **[Issue #42840 — MathJax/LaTeX Support to Control UI](https://github.com/openclaw/openclaw/issues/42840)** (👍10): High demand for displaying mathematical formulas correctly in the UI.
- **[Issue #28300 — Theme Customization System](https://github.com/openclaw/openclaw/issues/28300)** (👍5): Preset themes + a custom theme studio for the Control UI.
- **[Issue #38714 — Discord reaction event support to Hooks system](https://github.com/openclaw/openclaw/issues/38714)** (👍2): Enabling automation on user reactions (e.g., react with ✅ to save memory).
- **[Issue #45771 — Built-in pace-aware rate limiting](https://github.com/openclaw/openclaw/issues/45771)** (👍2): Critical for autonomous agents to avoid burning through API rate limits.
- **[Issue #86963 — Orphaned/oversized native Codex thread wedges a session](https://github.com/openclaw/openclaw/issues/86963)** (👍1): A P1 bug that is also a roadmap signal for more robust Codex integration.

**Predictions for next version:**
1.  **The MathJax feature is a strong candidate** due to its high 👍 count and clear UX value.
2.  **A fix for the `write` tool deny / memory persistence issue (#126906)** is likely, as it is now labeled with `fix-shape-clear` and `queueable-fix`, indicating it is a well-defined fix that can be picked up.
3.  **Continued investment in Codex integration stability** is expected, given the number of P1s around `claude-cli` and Codex thread management.

## 7. User Feedback Summary

User pain points this week focus on **silent failures and data integrity**:

- **Silent data loss**: The P0 file path bug (@-stripping) and the P1 memory persistence bug (#126906) are particularly painful because the agent *reports success* when it has not performed the intended action. Comments on #126906 say, "nothing tells anyone — not the operator at startup, not `doctor`, and not the agent."
- **Frustrating stream experience**: [#86050](https://github.com/openclaw/openclaw/issues/86050) highlights that with `claude-cli`, users only see the final assembled message, losing the real-time experience. The reporter noted the gateway receives 46–105 events but relays *zero* of them.
- **Platform-specific discontent**: Windows users continue to face unique bugs (EBUSY on `sqlite`, gateway restart loops with `OPENCLAW_SANDBOX=1`), and macOS users are frustrated with `doctor` warnings they cannot fix ([#60612](https://github.com/openclaw/openclaw/issues/60612)).
- **Positive signals**: The community is engaged and contributing high-quality reports with detailed reproduction steps, and the `clawsweeper` bot is actively applying labels to streamline triage. Users are also requesting constructive features like theme customization and rate limiting, indicating a desire to use OpenClaw for more production-like workloads.

## 8. Backlog Watch

Several important issues have been waiting for maintainer attention for an extended period:

- **[Issue #44502 — Discord routing / mention-gating issue](https://github.com/openclaw/openclaw/issues/44502)** (P2, created 2026-03-13, 7 comments): A regression with `impact:message-loss` that has been open for over 5 months without a linked fix PR.
- **[Issue #41366 — durable natural-language rule learning](https://github.com/openclaw/openclaw/issues/41366)** (P3, created 2026-03-09, 8 comments): A product decision request that could simplify multi-agent configuration, pending for 5+ months.
- **[Issue #38714 — Discord reaction event support](https://github.com/openclaw/openclaw/issues/38714)** (P2, created 2026-03-07, 👍2): Awaiting maintainer review for 5+ months.
- **PR #118516 — fix: align extension security and thinking levels** (P1, created 2026-08-03): A **large, risky PR** still waiting on author for over 2 weeks. Its label `⏳ waiting on author` suggests the author has not addressed feedback, potentially stalling a security-adjacent improvement.
- **PR #126082 — Audit exact-bound owner-native lifecycle receipts** (P2, created 2026-08-18): An audit-related PR for compatibility, also `⏳ waiting on author`.

These long-lived issues, particularly the Discord routing bug (#44502), risk eroding user trust if not addressed. The maintainers should prioritize clearing the backlog of `clawsweeper:needs-maintainer-review` items, especially those with `impact:message-loss` or `impact:data-loss`.

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: Personal AI Assistant & Agent Open-Source Ecosystem
**Date: 2026-08-22**

---

## 1. Ecosystem Overview

The personal AI assistant/agent open-source landscape is characterized by **intense, concurrent development** across multiple projects, with a clear shift from feature velocity toward **reliability, security, and production-readiness**. Projects like OpenClaw, Hermes Agent, and ZeroClaw are processing 50+ issues and PRs daily, indicating a mature and highly engaged user base. The dominant themes across the ecosystem are **data integrity (silent data loss is the most common critical bug)**, **multi-channel message delivery consistency** (Discord, Slack, Telegram, WhatsApp, etc.), **memory system reliability**, and **security boundary enforcement**. While these projects share a common core — AI agents that operate across communication channels — they diverge significantly in target users, technical architecture, and roadmap priorities, creating a competitive yet collaborative ecosystem.

---

## 2. Activity Comparison

| Project | Issues (24h) | PRs (24h) | Release Status | Health Score¹ | Activity Tier |
|:--------|:------------|:----------|:---------------|:--------------|:--------------|
| **OpenClaw** | 500 updated (489 open) | 500 updated (100 merged/closed) | No new release | ★★★★☆ | Very High |
| **Hermes Agent** | 50 updated (6 closed) | 50 updated (8 merged/closed) | **v0.20.5** (Aug 19) | ★★★☆☆ | Very High |
| **ZeroClaw** | 50 updated (3 closed) | 50 updated (multi merged) | No new release | ★★★★☆ | Very High |
| **IronClaw** | 15 active + 5 closed | 17 merged/closed | No new release | ★★★★☆ | High |
| **CoPaw** | 34 updated (19 open) | 36 updated (15 merged/closed) | **v2.1.1-beta.1** (imminent v2.1.1) | ★★★★☆ | High |
| **NanoBot** | 5 updated (4 closed) | 37 updated (23 merged/closed) | No new release | ★★★★★ | High |
| **NanoClaw** | 1 new bug | 11 merged/closed | No new release | ★★★☆☆ | Medium-High |
| **Moltis** | 2 new | 8 updated (1 merged) | No new release | ★★★☆☆ | Medium |
| **PicoClaw** | 0 new | 4 merged/closed | No new release | ★★★★★ | Medium |
| **LobsterAI** | 2 closed (stale) | 10 merged/closed | **2026.8.21** (merged via PR) | ★★★☆☆ | Medium |
| **NullClaw** | 0 | 1 open, awaiting review | No new release | ★★☆☆☆ | Low |
| **TinyClaw** | — | — | — | — | Inactive |
| **ZeptoClaw** | — | — | — | — | Inactive |

¹ *Health score based on: issue resolution rate, maintainer responsiveness, PR merge velocity, and backlog severity. ★=critical issues unresolved, ★★★★★=excellent responsiveness.*

---

## 3. OpenClaw's Position

**Advantages vs. Peers:**
- **Scale & Community Dominance:** OpenClaw processes 10x the issues/PRs of its nearest competitor (500 vs. 50 in 24h), indicating the largest user and contributor base in the ecosystem.
- **Security-Boundary Focus:** OpenClaw shipped systemic fixes for message delivery isolation across 8 channels (#126424), demonstrating a proactive approach to multi-agent security that peers like CoPaw (#7193 memory contamination) and ZeroClaw (#9947 cron cross-agent access) are still grappling with.
- **Cross-Channel Coverage:** OpenClaw supports more channels (Discord, Slack, Telegram, Feishu, Mattermost, Matrix, iMessage, Twitch, IRC, SMS, Line) than any peer — Moltis is investing heavily in WhatsApp (2 PRs), NanoClaw in Telegram/Mattermost, but none match OpenClaw's breadth.
- **Backlog Risk:** The 489 open issues (97.8%) represent a significant triage bottleneck. While `clawsweeper` bot streamlines labeling, the P0 data-loss bug (#119270) and 5+ P1s with no fix PRs indicate the maintainer team is stretched thin.

**Technical Approach Differences:**
- **Gateway-Centric Architecture:** OpenClaw's gateway abstraction for stream buffering and channel adapters is more mature than peers — IronClaw is still consolidating CI toolchains, CoPaw is scaling its Hub control plane.
- **Memory/Identity Systems:** OpenClaw's identity layer and memory persistence (with data-loss safeguards) set the standard; Hermes Agent's SQLite `state.db` corruption and ZeroClaw's SOP state loss show peers still struggling.

**Community Comparison:**
- OpenClaw has the **most mature contribution pipeline** — PRs with video proof (#123288), architectural proposals (#48788), and community-driven triage labels that other projects lack.
- ZeroClaw's contributor `1snob` (4 duplicate PRs in 24h) highlights contamination risk that OpenClaw's review process handles better.

---

## 4. Shared Technical Focus Areas

| Focus Area | Projects | Specific Needs |
|:-----------|:---------|:---------------|
| **Message-Loss Prevention** | OpenClaw, Hermes Agent, CoPaw, Moltis, NanoClaw | Silent message drops after busy windows (OpenClaw #127220), streaming text loss (OpenClaw #84486), MCP timeout killing toolsets (Hermes #88661), send_card action drops (NanoClaw #3426) |
| **Data Integrity & Memory Reliability** | OpenClaw, Hermes Agent, ZeroClaw, CoPaw, NanoBot | Silent write failures (OpenClaw #126906), SQLite corruption (Hermes #91839), memory cross-session contamination (CoPaw #7193), blocked memory cursors (NanoBot #5441), SOP state loss (ZeroClaw #9929) |
| **Security Boundary Enforcement** | OpenClaw, ZeroClaw, IronClaw, Hermes Agent | Path traversal (OpenClaw #119270), forbidden_paths bypass (ZeroClaw #9815), credential leakage (ZeroClaw #9976), SSRF prevention (NanoBot #5414), MCP profile collision (Hermes #91654) |
| **Multi-Channel Consistency** | OpenClaw, ZeroClaw, Moltis, NanoClaw, PicoClaw | Feishu bypass (OpenClaw #42803), Matrix delegation (ZeroClaw #9855), Slack shared channels (Moltis #1224), Mattermost/Telegram pairing (NanoClaw #3436) |
| **Stream & Real-Time Experience** | OpenClaw, Hermes Agent, NanoBot, IronClaw | Stream buffering gaps (OpenClaw #86050), FTS rebuild races (Hermes #91839), LLM timeout stalls (IronClaw #7783), LaTeX rendering (NanoBot #5476, OpenClaw #42840) |
| **Install/Update Reliability** | Hermes Agent, LobsterAI, Moltis, ZeroClaw | Debian install failures (Hermes #87093), Windows path issues (Moltis #468), CI flakiness (IronClaw T1-T4, ZeroClaw #9965), release branch regressions (IronClaw #7805) |

---

## 5. Differentiation Analysis

| Dimension | OpenClaw | Hermes Agent | ZeroClaw | CoPaw | NanoBot | IronClaw | NanoClaw | Moltis | PicoClaw | LobsterAI |
|:----------|:---------|:-------------|:---------|:------|:--------|:---------|:---------|:-------|:---------|:----------|
| **Target User** | Power users, multi-agent operators | Fleet operators, downstream consumers | Security-conscious developers | Chinese-language power users | Developers via CLI/TUI | Enterprise CI/devops | Chat-first SMB users | Privacy-conscious individuals | CLI minimalists | Chinese-market desktop users |
| **Architecture** | Gateway + channel adapters | Session-state central + SQLite | Modular multi-crate (Rust) | Hub control plane + data runtime | Lightweight TUI + provider agnostic | Rust monorepo + release branches | Chat SDK + adapter wiring | Plugin-based + WhatsApp focus | Go CLI single-binary | Electron + gateway |
| **Key Strength** | Channel breadth, security awareness | Delivery velocity (~323 PRs/rollup) | Security hardening, SOP engine | Feature breadth + Chinese UX | Clean codebase, fast issue resolution | CI discipline, sandbox security | In-chat setup UX | WhatsApp production-readiness | Simplicity, stability | DeepSeek Harness, local library |
| **Key Weakness** | Backlog bottleneck (489 open issues) | Install/update fragility, P0 cache bugs | ZeroCode TUI rough edges, review backlog | Memory contamination, MCP reconnect gaps | Smaller feature surface | CI expedite still in flight | Regression risk in card handling | Small community, young project | Limited channel breadth | Stale PRs (April backlog), i18n issues |
| **Language/Stack** | TypeScript-heavy | TypeScript/JS | Rust | Python | TypeScript/Go | Rust | TypeScript | TypeScript | Go | Electron/TS + Python runtime |

---

## 6. Community Momentum & Maturity

**Tier 1 — Rapid Iteration w/ Scale (100+ daily updates):**
- **OpenClaw** — 500 issues/PRs daily, 100 PRs merged/closed. Growing but struggling with triage.
- **Hermes Agent** — 100 updates daily, v0.20.5 rollup (323 PRs), but fighting P0s (cache invalidation).
- **ZeroClaw** — 100 updates daily, aggressive security fixes, active contributor inflow (with quality issues).

**Tier 2 — High Velocity (30-50 daily updates):**
- **IronClaw** — 17 PRs merged/closed, CI expedite program in full swing, sandbox security hardening.
- **CoPaw** — 15 PRs merged/closed, converging on v2.1.1 release, balancing features vs. reliability.
- **NanoBot** — 23 PRs merged/closed, exceptional closure rate (4 issues closed), maintainer-responsive.

**Tier 3 — Medium/Consolidating:**
- **NanoClaw** — 11 PRs merged/closed, setup wizard overhaul, channel adapter ecosystem maturing.
- **Moltis** — 8 PRs updated, 1 merged, steady multi-track development (WhatsApp, browser, cron).
- **PicoClaw** — 4 PRs merged/closed, catching-up on 6-month backlog, high stability.
- **LobsterAI** — 10 PRs merged/closed (April-era backlog cleanup), release 2026.8.21 shipped.

**Tier 4 — Low/Inactive:**
- **NullClaw** — 1 PR awaiting review, provider pattern expansion (Eden AI).
- **TinyClaw, ZeptoClaw** — No activity in last 24 hours.

**Maturity Trend:** Projects are shifting from "add features" to "**stabilize and harden**." Hermes Agent's pack release, PicoClaw's backlog closure, and LobsterAI's April-PR cleanup all signal a maturing ecosystem — yet the persistence of P0s (OpenClaw #119270 data-loss, Hermes #91830 cache-loss, CoPaw #7206 regression) shows the bar for "production-ready" is still being defined.

---

## 7. Trend Signals

**1. Silent Data Loss is the #1 Trust Killer.**
Across 6 projects, the most severe bugs share a pattern: **the agent reports success but silently fails** (OpenClaw #126906 write-tool memory, Hermes #91830 cache invalidation, CoPaw #7193 memory contamination, ZeroClaw #9947 cron cross-access). Developers should treat *silent failure detection* as a core feature, not a nice-to-have — the agent must be able to verify its own writes.

**2. "Production Multi-Agent" is Emerging as a Real Use Case.**
OpenClaw's security-boundary fix (#126424), CoPaw's cross-session memory contamination (#7193), and ZeroClaw's cron scoping (#9947) all point to the same demand: **multiple agents, multiple sessions, isolated state**. The ecosystem is converging on the need for sandboxed memory/execution per agent, not just per user.

**3. Channel Breadth Alone Doesn't Win — Consistency Does.**
OpenClaw has the channel variety, but Moltis (#1224 Slack shared channels) and ZeroClaw (#9855 Matrix delegation) are finding that **enterprise-grade channel support** (shared channels, delegation, proper auth flows) is where users actually get stuck. The next differentiator will be channel *compliance* (GDPR, data residency — see NullClaw's Eden AI focus), not channel *count*.

**4. Install/Update Reliability is the New Onboarding Gate.**
Hermes Agent explicitly acknowledged "install/update is our least reliable capability." Debian failures (#87093), Windows path issues (Moltis #468), and release-branch CI breaks (IronClaw #7805) all describe the same problem: **users are lost when the setup fails**. The ecosystem collectively needs a "first-run success guarantee."

**5. The WebUI/TUI is Becoming a First-Class Surface.**
From OpenClaw's MathJax request (#42840) and session activity indicators, to Hermes's paging UX complaints (#90473), to CoPaw's "anti-human" sorting (#4816), to NanoBot's model-switching pain (#5198): **the CLI/WebUI is where users form their loyalty**. Presenting agent reasoning (CoPaw #7196), managing approvals (#7198), and exposing model control are the UX battlegrounds.

**6. Security Hardening is Moving From "Hardening" to "Default."**
ZeroClaw's `forbidden_paths` bypass, IronClaw's sandbox credential mediation, OpenClaw's install-policy warnings, and NanoBot's redirect-chain validation all suggest the ecosystem is moving toward **security-by-default**: safety features that don't require user opt-in and fail closed (IronClaw's Railway audit append fix).

**7. SDK/Provider Abstraction is the Moat-Builder.**
NanoBot's typed LLM usage contract, NullClaw's `OpenAiCompatibleProvider` abstraction, PicoClaw's Anthropic protocol prefix, and CoPaw's multi-provider Creator 1.1.0 all point to: **model-lock-in is dying**. The projects that provide the cleanest abstraction over multiple providers (OpenAI, Anthropic, Bedrock, DeepSeek, QwenCloud) will win developer trust.

---

*Report generated from community digest data for 2026-08-22. Projects with no 24h activity (TinyClaw, ZeptoClaw) are excluded from comparative analysis.*

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-08-22

## Today's Overview

NanoBot is in a phase of rapid, high-velocity consolidation. The repository saw substantial activity with 37 PRs updated in the last 24 hours, of which 23 were merged or closed, alongside 5 issues updated (4 closed). The focus is heavily on internal refactoring and architectural hardening, particularly around provider usage contracts, trajectory logging, and dead code removal, while also addressing user-facing bugs in streaming retries, Dream memory cursors, and platform-specific WebUI issues. The project appears mature in its feature set, with current efforts aimed at stability, observability, and developer experience. The maintainer team is highly responsive, closing and merging a significant volume of work daily.

## Releases

No new releases were published in the last 24 hours. The current activity is focused on development branch improvements and bug fixes, which are likely candidates for the next upcoming release.

## Project Progress

The project saw a significant number of PRs merged/closed, indicating a strong push to stabilize the codebase and add new capabilities:

**Architecture & Refactoring:**
- **Typed LLM Usage Contract (#5478, #5480, #5481):** A major refactor by `chengyongru` to define an immutable, typed `LLMUsage` contract, replacing dynamic provider usage dictionaries. This normalizes token and cache semantics across OpenAI, Anthropic, and Bedrock boundaries.
- **Unified Provider Usage Backend (#5479, #5481):** A stacking feature to record a content-free trajectory row for every retry-managed provider attempt, including fallbacks and errors.
- **Dead Code Removal (#5475):** `chengyongru` also merged a broad cleanup removing zero-consumer runtime helpers and unused dependencies.

**Bug Fixes:**
- **Cron Job Retirement (#5407):** Fixed a regression where disabling heartbeat/dream features did not stop previously persisted system cron jobs from firing, which was burning tokens.
- **Dream Cursor Advancement (#5442):** Fixed a critical bug where recovered tool errors (like a failed `edit_file`) permanently blocked the memory cursor, causing duplicated edits in subsequent runs (Fixes #5441).
- **Slack File Download Safety (#5414):** Fixed a security issue by validating file downloads across the full redirect chain to prevent potential SSRF or malicious redirects.
- **LaTeX Rendering in TUI (#5476):** Added the ability to render common LaTeX math as Unicode in the terminal UI.
- **iOS PWA Safe Area (#5477):** Fixed a WebUI issue to keep controls within the iOS safe area and improved theme-color synchronization.
- **Prompt Injection Defense (#1149):** A long-standing PR (originally from February) was merged, adding a `PromptGuard` safety module to detect prompt injection attacks.

## Community Hot Topics

- **PR #5234:** **Meta-Search Tool (MST) Integration (Open, +2 days)** — The most active PR. This feature adds a metasearch provider that aggregates results from multiple engines (DuckDuckGo, Google, Brave) using Reciprocal Rank Fusion (RRF). It addresses a core need for richer, more comprehensive web search results and is highly anticipated.
- **Issue #5198 (Closed):** **Inability to switch models in a session (Closed)** — Users expressed frustration that, unlike cloud SaaS AI UIs, NanoBot's web UI prevents switching models mid-session without a full reconfiguration. The `/model` command also apparently failed.
- **Issue #5441 (Closed):** **Dream Memory Cursor Blocking (Closed)** — A user reported that a single recovered tool error could permanently block the Dream memory processing. This was quickly fixed by PR #5442, showcasing an excellent community-to-maintainer feedback loop.

## Bugs & Stability

The project is actively squashing bugs, with several critical and high-priority ones resolved today.

- **Critical: DingTalk Task Drain (Issue #5463, Open)** — The DingTalk stream handler creates background tasks without a proper lifecycle observer, which can lead to stalled or undrained inbound tasks and possible resource leaks. This is currently open, and it is a reliability concern.
- **High: Memory Cursor Blocking (Issue #5441, Closed)** — A single recovered tool error could lead to duplicated data and a permanently blocked memory cursor. **Fix: PR #5442 merged.**
- **High: Streaming Retry Skips (Issue #5454, Closed)** — The transient-error retry logic did not work if a `server_error` occurred mid-stream after content was already sent, causing turns to fail without a retry. **Fix: Acknowledged.**
- **High: Cron Regression (Issue #5407, Closed)** — Disabled heartbeat/dream jobs were not being retired from the persisted JSON, leading to unnecessary token expenditure. **Fix: PR #5407 merged.**
- **Medium: Dispatcher Exception Boundary (PR #5457, Open)** — A fix is proposed to scope exception boundaries in the outbound message dispatcher to prevent a single error from killing the entire dispatch task.

## Feature Requests & Roadmap Signals

- **DeepSeek Vision Support (#5474, Merged)** — Support for `deepseek-v4-flash-vision-exp` has been added, signaling continued multi-provider expansion.
- **Metasearch Provider (#5234, Open)** — The requested MST integration points to a roadmap for advanced search features and better result fusion.
- **Manual-Only Skills (#5405, Open)** — A feature to allow skills (like deployment or publishing) to be restricted to explicit user invocation, preventing accidental model-triggered side effects.
- **Turn Observability (#5420, Open)** — A significant WebUI feature to project user turns into a single surface with unified activity, usage accumulation, and interruption handling, suggesting a focus on enhancing the interactive experience.

## User Feedback Summary

The community is highly engaged and provides actionable feedback, leading to rapid fixes. The closure of issues like #5441 and #5198 demonstrates that maintainers are listening and addressing pain points quickly. There is clear demand for:
- **UI/UX parity with commercial AI tools:** (Issue #5198) users expect the ability to switch models in-session.
- **Robustness and reliability:** (Issue #5441, #5454) users are pushing for more resilient handling of errors and retries.
- **Security consciousness:** (PR #1149) validation of security-in-depth is a welcome addition.
- **Ecosystem integrations:** (Issue #1168) users are actively trying to connect to services like Notion via MCP, indicating a strong need for documentation or fixes when integrations fail. The closure of this issue suggests it was answered or resolved externally.

## Backlog Watch

- **PR #5234 (Metasearch Provider):** Despite being the most active PR, it remains open after 2+ days. It is a large feature and may require more review, but due to its high community interest, it warrants a maintainer's close attention.
- **Issue #5463 (DingTalk Task Drain):** As an Open issue related to a specific channel's stability, it is a potential source of unreliability. It should be promptly reviewed and ideally receive a fix similar to the discipline seen in other bug fixes.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-08-22

## 1. Today's Overview

Hermes Agent is in a period of **high-intensity stabilization**, with 50 issues and 50 PRs updated in the last 24 hours across a broad front: session-state integrity, desktop UX, multi-profile isolation, MCP tool reliability, and installation/update robustness. The v0.20.5 patch release (v2026.8.19) went out on August 19, rolling up ~323 PRs, but the maintainers are clearly still fighting structural issues — notably **SQLite `state.db` corruption** (with a dedicated fix PR merged today), **profile-cross-contamination bugs**, and a **P0 cache-invalidation issue** that surfaced yesterday. The activity mix (6 closed issues, 8 closed/merged PRs today) suggests a productive triage day, but the volume of P1/P0 items indicates the project is under sustained load to harden core reliability before feature expansion.

## 2. Releases

**v0.20.5 (v2026.8.19)** — released August 19, 2026
- Patch release rolling up **~323 PRs** since v0.20.4
- Targeted at downstream consumers: Docker images, hosted deployments, fresh installs
- No breaking changes or migration notes provided in the release notes snippet
- The sheer size of the rollup (~323 PRs in a patch) suggests the team has been accumulating fixes without tagging — this release is a checkpoint, not a feature drop

## 3. Project Progress

Eight PRs were merged/closed today. The most significant:

- **#91839** — `fix(state): stop live FTS rebuilds from corrupting shared state.db` *(P1)*. Guards all automatic FTS rebuild paths against running when foreign processes hold `state.db` or WAL sidecars. Directly addresses the recurring corruption seen in #90806. **Merged.**
- **#91860** — `fix(cli): guard empty message text in _display_resumed_history`. Fixes the `IndexError` crash on `hermes chat --resume` with empty/whitespace-only messages (resolves #59265). **Merged.**
- **#91861** — `fmt(js): npm run fix auto-fix`. Automated formatting commit. **Merged.**

Other closed items: #88655 (cron alerting bypass) and #90456 (Bot Mode conversation mix-up) were closed, though the associated PRs are not in today's list — likely fixed earlier.

## 4. Community Hot Topics

The most active discussions reflect **operator pain with session reliability and install/update friction**:

- **[#66616] Skills index stale/degraded (71 comments)** — Automated freshness probe failing for nearly a month. A bot-reported issue with zero 👍 but an active 71-comment thread. This is infrastructure debt that the community keeps poking.
- **[#87093] Debian installation broken — uv.lock & npm install failed (19 comments, 3 👍)** — Basic `curl | bash` install fails on Debian 13.6. A community member's frustration with onboarding reliability.
- **[#90473] "Show earlier messages" paging broken UX on long sessions (13 comments)** — "Who the hell designed this?" The bluntness signals mounting user frustration with session UX at scale.
- **[#91277] Fleet update reliability tracking issue (5 comments)** — Maintainer `teknium1` opened a tracking issue acknowledging "install/update is currently our least reliable capability" with ~30 open issues and ~15 open PRs all patching corners of the same problem. This is the community converging on a systemic weakness.

The signal: **users trust Hermes as an agent, but are paying a tax on deployment, updates, and long-session UX.**

## 5. Bugs & Stability

Ranked by severity (P0 first):

| Severity | Issue | Summary | Fix Status |
|----------|-------|---------|------------|
| **P0** | [#91830](https://github.com/NousResearch/hermes-agent/issues/91830) | `proactive_prune_rearm_tokens` invalidates prompt-cache prefix for sessions >10M tokens — 100% cache loss on all providers | No fix PR yet |
| **P0** | [#89886](https://github.com/NousResearch/hermes-agent/issues/89886) | v2026.8.18: `cache_control` on `tool_result.content[]` rejected by Anthropic-format API (non-retryable 400, kills tool-using sessions) | No fix PR in list |
| **P1** | [#90806](https://github.com/NousResearch/hermes-agent/issues/90806) | `state.db` WAL sidecars replaced under live holders — recurring structural corruption with SQLite 3.53.1 | Fixed by merged PR #91839 |
| **P1** | [#91277](https://github.com/NousResearch/hermes-agent/issues/91277) | Fleet update reliability: "imperative per-platform spaghetti" — 30+ issues, 15+ PRs all patching corners | Tracking issue open |
| **P2** | [#88661](https://github.com/NousResearch/hermes-agent/issues/88661) | MCP tool timeout parks server connection — whole toolset unregisters, no auto-reconnect | No fix PR |
| **P2** | [#91654](https://github.com/NousResearch/hermes-agent/issues/91654) | MCP session/circuit-breaker registries keyed by server name only — profile multiplexing collisions | No fix PR |
| **P2** | [#91818](https://github.com/NousResearch/hermes-agent/issues/91818) | Projects leak across profiles (broken isolation) on Windows 11 | No fix PR |

**Notable fix PRs in flight:** #91852 (macOS write barriers on state.db repair), #91839 (FTS rebuild guard — merged), #89144 (Windows update: never strand `hermes.exe`), #90098 (skip notarization on unsigned desktop builds).

## 6. Feature Requests & Roadmap Signals

- **[#89995] Expose Bot Mode group chat rooms in web dashboard & gateway** — Currently desktop-only; users want web access. High-value for multi-device workflows.
- **[#48190] Session ↔ Workspace binding** (cwd + repo, group, restore) — Open since June; the community keeps it alive. Predict this lands in the next minor version given the session-state focus.
- **[#91107] Persist Accent Picker override per profile** — Small desktop polish item.
- **[#91827] Bot Mode canonical Bot Chat hardcoded English kickoff** — i18n concern; signals global user base.
- **[#14950] Per-operation timeout config for Hindsight memory provider** — Open since April; low priority but repeatedly requested.
- **PR #89555** — OpenRouter provider/quantization pinning (in review, likely next release).
- **PR #89562** — Cron-fleet model defaults and routing surfaced in desktop UI (in review).

The roadmap signal: **multi-profile and multi-environment support is the loudest ask**, followed by i18n/L10n polish.

## 7. User Feedback Summary

- **Onboarding friction:** The Debian install failure (#87093) is a direct hit on first impressions. A P1 tracking issue acknowledging the problem is a good sign, but users are still hitting walls.
- **Long-session UX:** The "show earlier messages" complaint (#90473) and the >10M token cache loss (#91830) both point to the same underlying need: **Hermes must be reliable at scale, not just in demos.**
- **Profile isolation:** Users running multiple profiles (e.g., default + trade-expert) are seeing cross-contamination (projects leaking, MCP collisions) — this erodes trust in a flagship feature.
- **Desktop quirks:** Linux app-launcher PATH issues, Windows package rebuild corruption, macOS sleep/wake session loss — the platform-support matrix is straining.
- **Positive signals:** The fleet-update tracking issue (#91277) generated constructive conversation, indicating the community is engaged and wants to help shape the fix rather than abandon ship.

## 8. Backlog Watch

These items have been open for weeks or months with no maintainer activity:

- **[#66616] Skills index stale/degraded (71 comments, open since July 18)** — Automated freshness probe has been failing for over a month. Zero maintainer response in the digest window. Infrastructure debt that needs a human.
- **[#14950] Hindsight memory provider per-op timeout (open since April 24)** — 3 comments, no maintainer response. Low priority but easy win.
- **[#63211] Model picker hides custom base_url models (open since July 12)** — Config/UX bug, 2 comments, no fix PR.
- **[#18954] Model aliases not resolved for custom providers (open since May 2)** — 4 comments, 1 👍, no PR. This is a basic compatibility issue that keeps resurfacing.
- **[#48190] Session ↔ Workspace binding (open since June 18)** — 4 comments, no maintainer action. Feature request with clear value; likely waiting on the session-state stabilization work.

---

**Overall Assessment:** Hermes Agent is a powerful, fast-moving project with a deeply engaged community — but the last 24 hours paint a picture of a team fighting fires on **state integrity, profile isolation, and install/update reliability**. The v0.20.5 rollup indicates strong delivery velocity, yet the P0 cache-invalidation issues (#91830, #89886) are critical and need immediate attention. The maintainers' own acknowledgment of install/update as "least reliable" is a healthy sign of self-awareness; the next release should prioritize the fleet-update consolidation (#91277) and the MCP profile collision fixes to restore user confidence.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

Based on the GitHub data provided for PicoClaw (github.com/sipeed/picoclaw) for 2026-08-22, here is the project digest.

---

# PicoClaw Project Digest — 2026-08-22

## 1. Today's Overview
PicoClaw is showing signs of mature consolidation. The project saw no new releases, but the activity is focused on integrating long-pending work: four pull requests from the last six months were merged or closed, indicating a significant "catch-up" and cleanup phase. While there were no new bug reports in the last 24 hours, the single open issue highlights a complex UX/architecture problem regarding turn-steering. Overall, the project appears healthy and stable, with maintainers actively finalizing previously developed features rather than pushing rapid new development.

## 2. Releases
No new releases were published for PicoClaw during this period.

## 3. Project Progress
Today's activity centered on merging and closing four substantial PRs, translating directly into feature and infrastructure improvements:

- **[PR #1158: Anthropic Messages Protocol](https://github.com/sipeed/picoclaw/pull/1158)**: Adds a new `anthropic-messages` protocol prefix, enabling compatibility with API services that only support the native Anthropic `/v1/messages` format. This resolves a long-standing issue (#269) and expands the tool's interoperability.
- **[PR #647: WebFetchTool Enhancement](https://github.com/sipeed/picoclaw/pull/647)**: Upgrades the `WebFetchTool` with HTML entity decoding and content structure preservation (adding newlines for block elements), significantly improving the readability and accuracy of extracted web text.
- **[PR #714: Skills CLI Refactor](https://github.com/sipeed/picoclaw/pull/714)**: Overhauls the skills installation process with a new `skillsCmd`, adding support for installing from specific branches (`repo@branch`) and subpaths, introducing a `reinstall` command for force overwriting, and providing more informative error messages.
- **[PR #1182: AGENTS.md Update](https://github.com/sipeed/picoclaw/pull/1182)**: Refines the contributor guidance document (AGENTS.md) to be more principle-based and efficient for AI agents, and updates the Go version reference to point to `go.mod` as the source of truth.

## 4. Community Hot Topics
The most active discussion is centered on the agent's interaction model:

- **[Issue #3342: "After-turn" steering mode](https://github.com/sipeed/picoclaw/issues/3342)**: This new feature request proposes an opt-in mode where a user's second message is queued and processed only after the current turn/task has completed, rather than being treated as an immediate "course correction" that interrupts the running task. This is likely a hot topic as it addresses a common pain point in interactive AI agents where mid-task interruptions lead to confusing results or wasted computation.

## 5. Bugs & Stability
**No new bugs, crashes, or regressions were reported in the last 24 hours.**
The project exhibits high stability in this reporting period. The single open issue is a feature request rather than a defect, and no PRs were merged to address stability concerns today.

## 6. Feature Requests & Roadmap Signals
The primary roadmap signal comes from [Issue #3342](https://github.com/sipeed/picoclaw/issues/3342). The request for an optional "after-turn" steering mode suggests the current default behavior (interrupting the active turn) may not be ideal for all use cases. Given that this is a new issue, it may be considered for a future minor release as a configurable agent behavior. Other signals point to continued focus on ecosystem compatibility (Anthropic protocol) and tooling robustness (WebFetch).

## 7. User Feedback Summary
User feedback is inferred from the PRs and issue, highlighting specific needs:

- **Need for interoperability**: The merged Anthropic protocol support (PR #1158) directly addresses user frustration with services that only support native Anthropic APIs, making PicoClaw a more flexible client.
- **Need for better tool output**: The improvement to `WebFetchTool` (PR #647) shows user demand for cleaner, more structured data extraction from the web.
- **Desire for predictable agent behavior**: Issue #3342 indicates that interruptions are problematic for some users. They prefer a "wait for my turn to finish" queueing mechanism, suggesting that the current system's "course-correction" approach can feel abrupt and may lead to incomplete tasks.

## 8. Backlog Watch
It is not possible to identify "long-unanswered" items from the data provided, as all four PRs listed were closed/merged today, and no comment counts were available for them. The project appears to have kept its backlog tidy, addressing older PRs in this update cycle. The one open issue (#3342) is brand new and requires no immediate concern.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

Here is the NanoClaw project digest for 2026-08-22, based on the provided GitHub data.

---

# NanoClaw Project Digest — 2026-08-22

## 1. Today's Overview
NanoClaw shows **high-velocity development** today, especially around setup experience and channel integrations. While only **one new bug issue** was opened, the community and core team merged/closed **11 PRs** and maintained **14 open PRs**, indicating a strong focus on stabilizing and expanding the setup flow (Telegram, Dial, and general adapter wiring). The project is clearly in a **rapid iteration phase**, with a significant portion of the work driven by a small set of dedicated contributors (amit-shafnir, zvi-fried, gavrielc). No new releases were published today, suggesting that the current `main` branch is a staging ground for a substantial upcoming version.

## 2. Releases
**None.** There were no new releases published in the last 24 hours. The project appears to be between release cycles, consolidating a large amount of merged work (particularly around channel adapters and CLI setup) before cutting a new version.

## 3. Project Progress
Today saw the closure and merge of 11 PRs, signaling significant advancement in key areas:

- **Setup & Wizard UX (Telegram/Dial):** A significant overhaul of the setup process, primarily by **amit-shafnir**, is underway. While the PRs are still open, the groundwork was laid with the merge of the Slack template flow draft (#3397, superceded by #3428). Multiple follow-up fixes and features were merged to solidify the channel setup experience, including fixing the Telegram pairing card digit count (#3431) and carrying adapter instances through pairing (#3435).
- **Channel Integrations (Mattermost):** The **Mattermost channel integration** (#3202) was finally merged, closing issue #1379. This adds a new major platform to the Chat SDK, following the established `slack.ts` pattern.
- **CI & Stability:** The CI pipeline was actively hardened by **zvi-fried**. Key merges include a fix for the required `ci` check on the main ruleset (#3430), a fix for the Matrix adapter's ESM incompatibility with Node 22 (#3403), and the introduction of a test harness for registry-backed skills (#3424).
- **Core Architecture:** A new **`SessionExecSpec` contract** was ratified (#3429), allowing drivers to describe their exec argv. This is a foundational change to support interactive terminal attachment for live sessions, a significant step for the debugging/development experience.

## 4. Community Hot Topics
The most active work is concentrated in a series of interconnected PRs by **amit-shafnir**, all revolving around the setup wizard and multi-instance support for Telegram.

- **#3436** [OPEN]: [feat(telegram): named bot instances via TELEGRAM_INSTANCES + instance-bound pairing](https://github.com/nanocoai/nanoclaw/pull/3436) - This, alongside #3435 and #3438, addresses the need for managing multiple bots/adapters for the same platform. The underlying need is for power users who want to run distinct NanoClaw agents for different use cases within a single deployment.

- **#3396** [OPEN]: [feat: create agents from templates in chat](https://github.com/nanocoai/nanoclaw/pull/3396) - A major feature allowing users to scaffold new agents directly from a conversation. This indicates a push towards a more accessible, low-code configuration experience for end-users.

The overwhelming theme is **"instantiation and configuration"** — making it trivial for users to set up new channels and agents without leaving the chat interface or dealing with complicated configuration files.

## 5. Bugs & Stability
Only one new bug was reported today, but it highlights a critical flaw in the current card handling.

- **#3426** [OPEN] [High Severity - UX & Trust]: [ [bug] send_card docs promise callback buttons that the bridge drops since #2265; agents blame the platform](https://github.com/nanocoai/nanoclaw/issues/3426). This is a serious regression in the `send_card` feature. The bridge drops actions without a `url`, but the agent is not informed. This leads to the agent incorrectly blaming the platform to the user for its own limitations, which directly harms user trust in the agent. **No fix PR exists yet**, making this the highest priority item for the core team to address.

Other fixes merged today addressed proactive infrastructure issues:

- Fixed Matrix adapter breaks under Node 22 (#3403).
- Fixed CI check reporting for the Node 22/24 matrix (#3430).
- Resolved registry helper incompatibilities for the WhatsApp Cloud skill (#3401).

## 6. Feature Requests & Roadmap Signals
The current PRs provide a clear signal for the next release's roadmap.

- **Multi-Instance Support:** The work on `TELEGRAM_INSTANCES` (#3436) and the general "carry the adapter instance" refactoring (#3435, #3437) strongly suggests native support for running multiple bots of the same platform will be a headline feature.
- **"In-Chat" Agent Creation:** PR #3396 (`create_agent` from templates) is a major UX feature that could be the cornerstone of a "no-code" configuration strategy.
- **Interactive Sessions:** The ratification of the `SessionExecSpec` (#3429) is a foundational step towards an interactive terminal feature, which might be unveiled in the next minor release.

## 7. User Feedback Summary
- **Frustration with Agent Misattribution:** The primary pain point voiced today comes from bug #3426. Users are experiencing agents providing incorrect explanations for platform limitations ("the platform cannot render buttons"), which is a direct result of a missing API contract between the agent and the bridge. This causes dissatisfaction and undermines confidence in the assistant's competence.
- **Demand for Flexible Setup:** The flurry of PRs around the setup wizard and multi-bot instances (#3436, #3438) signals a strong user desire for a frictionless, flexible setup process that can handle complex, multi-tenant configurations without manual config file editing.

## 8. Backlog Watch
- **#3287** [OPEN]: [Fix: strip agent-group suffix from inbound platform message id](https://github.com/nanocoai/nanoclaw/pull/3287). Opened on August 17th by **wakqasahmed**, this PR fixes a channel-message-ID format mismatch. It has been open for 5 days without being merged, and given the ongoing Work In Progress around the Dial channel (#3432) and incoming party message IDs, this fix is likely becoming increasingly critical to the correctness of message routing and could warrant a closer look from maintainers.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest — 2026-08-22

---

## 1. Today's Overview

NullClaw is in a **low-activity maintenance window** today: zero issues were updated in the past 24 hours, and no new releases were cut. The only meaningful movement is a single open pull request (#990) proposing Eden AI as an OpenAI-compatible gateway provider, submitted yesterday and still awaiting review. The project's current focus appears to be on **provider ecosystem expansion** — specifically, adding aggregated gateway services that route to multiple upstream vendors behind a single API key. With no merged PRs, closed issues, or bug reports today, the project health is stable but **attention from maintainers is needed on the open PR** to keep momentum.

---

## 2. Releases

No new releases were published in the last 24 hours. There are no version bumps, breaking changes, or migration notes to report. The most recent release history remains unchanged as of this digest.

---

## 3. Project Progress

**No PRs were merged or closed today.** The sole active PR is:

- **[#990 — feat(providers): add Eden AI as an OpenAI-compatible gateway](https://github.com/nullclaw/nullclaw/pull/990)** — *Open, awaiting review*
  - Author: **MVS-source** | Created: 2026-08-21
  - Adds Eden AI as a new provider, following the established pattern from #922 (NEAR AI Cloud / Atlas Cloud).
  - No new provider implementation needed; it routes through the existing `OpenAiCompatibleProvider` abstraction.
  - Key value: Eden AI aggregates multiple upstream vendors behind one key and is EU-based — relevant for users with data residency requirements.

**Feature advancement:** No code has landed today, but the PR signals active community contribution toward expanding provider coverage without adding architectural complexity.

---

## 4. Community Hot Topics

**Only one active PR**, with zero comments recorded so far:

- **[#990 — Add Eden AI as OpenAI-compatible gateway](https://github.com/nullclaw/nullclaw/pull/990)**
  - 👍: 0 | Comments: 0 | Updated: 2026-08-21
  - **Underlying need:** Users are seeking broader provider choice with **simplified key management** — Eden AI's aggregation model lets a single API key access multiple upstream models. The **EU-based hosting** angle also suggests demand for **data sovereignty / GDPR-compliant** AI routing options.
  - **Observation:** The lack of comments or reactions after 24+ hours suggests the community is either waiting for maintainer review or the PR hasn't been widely noticed yet.

---

## 5. Bugs & Stability

**No bugs, crashes, or regressions were reported today.** Zero issues were opened or updated in the last 24 hours. The project is currently stable from a defect standpoint. No severity rankings or fix statuses are applicable.

---

## 6. Feature Requests & Roadmap Signals

While no formal feature requests were filed today, the open PR provides a clear roadmap signal:

- **Provider aggregation gateways** — Following #922 (NEAR AI Cloud, Atlas Cloud) and now #990 (Eden AI), NullClaw is building a pattern of supporting **meta-providers** that sit in front of multiple upstream vendors. The `OpenAiCompatibleProvider` abstraction makes adding these low-cost.
- **Likely next steps:** Expect similar gateway providers to be proposed (e.g., OpenRouter-style aggregators, EU-hosted providers). The project may also want to consider **documentation for self-serve provider addition** to encourage more community contributions in this vein.

**Prediction:** If #990 is reviewed and merged promptly, it is likely to be included in the next minor release. The pattern is proven, low-risk, and adds immediate user value.

---

## 7. User Feedback Summary

No direct user feedback (issues, comments, or reactions) was recorded today. However, the single PR implies:

- **Use case:** Developers want to **simplify vendor management** by using one key for multiple model providers, and they care about **regional hosting** (EU) for compliance.
- **Satisfaction:** The existence of a contributor who voluntarily implemented a new provider using the existing abstraction suggests the codebase is **approachable and well-structured** for external contributions — a positive health indicator.
- **No dissatisfaction signals** were detected in the observed window.

---

## 8. Backlog Watch

**No long-unanswered critical Items** were identified in the last 24 hours. However, **PR #990 deserves immediate maintainer attention**:

- **[#990 — Add Eden AI as OpenAI-compatible gateway](https://github.com/nullclaw/nullclaw/pull/990)**
  - Since it's a **1-day-old PR with no comments**, it risks stalling if not triaged soon. Given the low activity day, maintainers should use this window to review, provide feedback, or assign it — keeping community contributors engaged and the provider ecosystem growing.

---

*Digest generated from NullClaw GitHub activity data for 2026-08-22. Project status: stable, low activity, awaiting maintainer review on one provider-expansion PR.*

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-08-22

## 1. Today's Overview

IronClaw is in a period of intense engineering activity, with 55 issues and PRs updated in the last 24 hours. The project is mid-execution on a four-track "CI expedite" initiative (T1–T4) aimed at eliminating CI flakiness, reducing the green-PR/red-queue divergence, and consolidating the 43 scattered Rust toolchain invocations across 12 workflow files. Concurrently, the WebUI design-system program is being restructured into three parallel epics with Storybook integration pending review, and the notification center is being generalized into a durable user inbox. A total of 17 PRs were merged or closed yesterday, indicating healthy pull-request throughput. The issue tracker shows 15 open active issues alongside 5 closures, reflecting a balanced triage cadence.

## 2. Releases

No new releases were published in the last 24 hours. The most recent release branch referenced in PRs is `release/2026-08-17`, which is actively receiving forward-ports from `main` (e.g., PR #7805 fixing clippy 1.98 lint failures, PR #7804 porting the `IRONCLAW_REBORN_WORKSPACE_ROOT` override).

## 3. Project Progress

**17 pull requests were merged or closed today**, covering several functional areas:

**CI Infrastructure (Tracks T1–T4):** The CI expedite program is actively landing components. PR #7805 closed the clippy 1.98 forward-port gap on `release/2026-08-17`, fixing a pre-existing failure affecting every PR into that branch. PR #7804 forward-ported the `IRONCLAW_REBORN_WORKSPACE_ROOT` override to the 1.3 branch, closing a workspace-root durability gap.

**Sandbox Security:** Two significant sandbox PRs landed (#7807, #7806): GitHub CLI credential mediation is now in place, with direct executable-plus-argument-vector sandbox execution, cancellation support, and invocation-scoped credential staging resolved from active extension declarations. PR #7796 closed a failure-propagation gap by preserving staged Railway audit appends when appending fails.

**Telegram Connectivity:** PR #7803 and #7766 separated bot pairing from personal device linking, keeping paired bots active even without a personal credential, and requiring explicit WebUI choice between the two flows with localized authority disclosures across 11 locale packs.

**Notifications:** PR #7699 closed, publishing actionable run gates (approval-required, authentication-required, blocked-run) into the durable user inbox with stable run/gate-derived IDs for retry convergence.

**Documentation & Guidance:** PR #7797 completed a massive repo-wide agent-guidance audit, pruning 21.5k lines, fixing drift across 13 guidance clusters, and consolidating tests/ onto the AGENTS.md convention.

**WebUI Refactoring (open):** PRs #7794 and #7795 introduce shared page-shell and loading primitives plus `InlineNotice` migration for Settings/Admin feedback — both open for review.

## 4. Community Hot Topics

**CI Expedite Tracks (Issues #7798–#7801)** — These four planning issues by henrypark133 are the most active, each with 2–3 comments. They represent a coordinated, measured attack on CI instability with explicit risk tracking and REPRO emission for every failed gate. The underlying need: **predictable, fast, trustworthy CI that PR authors and maintainers can rely on without manual interpretation.**

**Pluggable Memory over MCP (#7664)** — Open since 2026-08-14 with 2 comments, this tracking issue for external memory binding (Mnesis Core as first consumer) has attracted a critical prerequisite bug (#7808) about redaction/taint metadata being required before any external provider can bind. Underlying need: **the community wants memory extensibility, but security guards must land first.**

**Design System Epic Restructuring (#7038, #7781, #7782)** — The five-phase design-system program was re-scoped on 2026-08-20, splitting into three epics. The activity pattern (closed duplicates, merged phases) indicates a maintainer carefully managing scope. Underlying need: **consistent WebUI theming, component governance, and agentic interaction patterns.**

## 5. Bugs & Stability

**High — LLM Timeout Policy (#7783, CLOSED):** Structured-output finalization runs on a non-streaming client, making transport stalls invisible until a 60s wall-clock cap fires, which then destroys the run before a retry can complete. Closed with a fix (same-day). This was a medium-risk, production-impacting bug.

**Medium — Memory Write Path Redaction (#7808, OPEN):** Verbatim conversation content egresses at write time without redaction or taint metadata. This is a prerequisite for ANY external memory provider binding (#7664). No fix PR yet; strategy decision recorded 2026-08-21.

**Medium — Clippy 1.98 Regression on Release Branch (#7805, CLOSED):** Every PR into `release/2026-08-17` failed clippy regardless of changes. Fixed via forward-port and merged.

**Low — Telegram Consent Flow (#7715, CLOSED):** Users couldn't choose between bot vs. personal-account connection, with no indication of which mode was active. Fixed in #7766/#7803.

**Low — Railway Audit Append Failure (#7796, CLOSED):** Failed audit appends were silently dropped. Now fails closed with staged capture preserved for retry.

## 6. Feature Requests & Roadmap Signals

**Durable User Inbox (Epic #7687, OPEN):** The notification center is being generalized into a durable, user-scoped inbox supporting actionable (approvals, auth, blocked runs) and informational (failures, completions) notifications. PR #7700 (open) materializes run outcomes from Process Journal transitions. **Prediction: ships in next minor release.**

**AfterTurn Lifecycle Hook (PR #7765, OPEN):** A new act-capable hook point that fires after a turn reaches a terminal state, with memory curation as the first consumer (phase 1 of #7770). **Prediction: lands in next minor release.**

**Pluggable Memory (Issue #7664, OPEN):** External memory binding via MCP with configurable providers. Blocked on #7808 (redaction prerequisite). **Prediction: next release or two, contingent on security work.**

**Design System Phases 2–5 (#7781, #7782, OPEN):** DESIGN.md governance, theme update/UI reskin, agentic interactions, components, and information architecture. Phase 1 (Storybook integration) is in review (PR #7750). **Prediction: rolling through v1.4.0.**

**Coding Tool Contract (PR #7491, OPEN):** Unified six-tool coding surface (`read`, `write`, `edit`, `glob`, `grep`, `bash`) removing legacy spellings. **Prediction: significant model-facing change; likely next minor.**

## 7. User Feedback Summary

**Positive signals:** The notification pipeline is converging — users get authoritative run outcomes, actionable gates, and deduplicated references. The Telegram flow fix directly addresses user confusion about bot-vs-personal connections, with explicit consent steps and localized disclosures. The CI expedite tracks are designed around measurable developer pain (green-PR/red-queue divergence, 43 scattered toolchain invocations).

**Pain points:** LLM timeout handling is fragile — a single transport stall destroys a run. Memory write paths lack redaction, blocking external provider integration. The WebUI repeats page-shell/loading/notice markup across five routes, indicating design-system debt. The `release/2026-08-17` branch had CI broken for every PR (clippy), which would have severely impacted contributor velocity.

**Satisfaction:** The rapid closure of the LLM timeout bug and clippy regression within 24 hours indicates strong operational responsiveness.

## 8. Backlog Watch

**Pluggable Memory over MCP (Issue #7664)** — Open since 2026-08-14, tracking issue with an in-draft provider crate (#7661) but blocked on security prerequisite #7808. Needs maintainer sequencing decision.

**Durable Storage Profile-Agnostic (PR #7456)** — Open since 2026-08-10, an XL-sized PR touching core storage layout, security envelopes, and tenancy. Still open after 11 days with no comments shown. This is a foundational change that likely needs focused review time.

**Coding Tools Contract (PR #7491)** — Open since 2026-08-11, an XL change removing legacy coding-tool surfaces and introducing a six-name unified contract. Extended review period may indicate either complexity or reviewer contention.

**Design System Phase 1 (PR #7750)** — Open since 2026-08-19, recreated off current main to escape a tangle; supersedes closed #7039. Needs review to unblock Phases 2–5.

---

*Data as of 2026-08-22. All links point to github.com/nearai/ironclaw.*

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

Here is the LobsterAI project digest for 2026-08-22.

---

# 🦞 LobsterAI Project Digest — 2026-08-22

**Data Source:** [github.com/netease-youdao/LobsterAI](https://github.com/netease-youdao/LobsterAI)

---

## 1. Today's Overview

LobsterAI has shipped a new release (`2026.8.21`) and cleaned up its issue backlog, resulting in high activity metrics today. Two long-standing issues (#1217, #1223) were closed as stale, and ten April-era pull requests were merged or closed, resolving accumulated technical debt. The most significant development is the inclusion of **DeepSeek Harness (DSH) runtime v0.1.1-rc.1** and a privacy-focused refactor of usage analytics in this release. The project shows strong health: critical bugs from the backlog are being addressed, the "Local Library" (资料库) feature received two major UX overhauls, and performance optimizations for the Cowork module have been merged.

## 2. Releases

**No new tags/releases were published in the last 24 hours.**

However, the **Release PR** ([#2519](https://github.com/netease-youdao/LobsterAI/pull/2519)) merged the `release/2026.8.21` branch into `main`. This includes a new version of the **DeepSeek Harness (DSH)** runtime.

- **DSH Update:** Updated to `v0.1.1-rc.1` ([PR #2516](https://github.com/netease-youdao/LobsterAI/pull/2516)).
- **Analytics Refactor:** Moved DSH usage analytics event building from the main process to the renderer ([PR #2518](https://github.com/netease-youdao/LobsterAI/pull/2518)).
- **Known Issue:** No breaking changes or migration notes were provided in the PR description.

## 3. Project Progress

Today's activity is dominated by the 2026.8.21 release cycle and the closure of pending PRs. Two key feature areas advanced:

- **🚀 "Local Library" (资料库) UX Overhaul:** Two substantial PRs merged, reworking the local artifact experience.
    - [PR #2514](https://github.com/netease-youdao/LobsterAI/pull/2514): Optimized preview modals for different window sizes, removed local delete entry points, and distinguished between empty and no-search-results states.
    - [PR #2517](https://github.com/netease-youdao/LobsterAI/pull/2517): Improved the share/favorite interaction—now preserving Unicode filenames, adding optimistic updates with rollback for favorites, and unifying the quota modal behavior.
- **📊 DSH Analytics:** Introduced privacy-conscious usage analytics for DSH enablement and workbench usage ([PR #2515](https://github.com/netease-youdao/LobsterAI/pull/2515)).

**Stale PRs Merged (April → August):** The backlog cleanup merged several important April PRs, indicating maintainers are processing pending work.

- **Performance:** `perf(cowork)` eliminates unnecessary re-renders and N+1 queries ([#1219](https://github.com/netease-youdao/LobsterAI/pull/1219), [#1220](https://github.com/netease-youdao/LobsterAI/pull/1220)).
- **Fixes:** Includes fixes for scheduled task sorting ([#1218](https://github.com/netease-youdao/LobsterAI/pull/1218)) and IM chat handler staleness ([#1215](https://github.com/netease-youdao/LobsterAI/pull/1215)).
- **i18n:** Fixed hardcoded Chinese strings for English users ([#1224](https://github.com/netease-youdao/LobsterAI/pull/1224)).

## 4. Community Hot Topics

There was no lively discussion today (the two issues closed had few comments). The most active items represent **intense user engagement with the "Local Library" and "Digital Cowork" features**, driving the current development focus.

- **[PR #2514](https://github.com/netease-youdao/LobsterAI/pull/2514) / [PR #2517](https://github.com/netease-youdao/LobsterAI/pull/2517) (Library UX):** These merged PRs touch on many small pain points (favorites, search clear, modals). The significant number of changes indicates the community provided heavy feedback on this feature's usability before release.
- **[Issue #1223](https://github.com/netease-youdao/LobsterAI/issues/1223) (i18n & UX):** A user reported hardcoded Chinese leaking into English prompts, which is a critical oversight for international users. It was fixed by [PR #1224](https://github.com/netease-youdao/LobsterAI/pull/1224).

## 5. Bugs & Stability

Two non-stale issues were closed, but they represent a snapshot of the backlog being cleared rather than new bug reports.

- **🔴 Medium: “偶发启动网关” (Intermittent Gateway Restart)** — *Resolved/Stale*. [Issue #1217](https://github.com/netease-youdao/LobsterAI/issues/1217). This was a critical bug affecting Windows 10 users (occurring 3-5 times daily). It was closed without a public fix explanation. It is unclear if the bug was fixed in a new release or if the maintainer could not reproduce it.
- **🟠 High: Hardcoded Chinese Labels:** [Issue #1223](https://github.com/netease-youdao/LobsterAI/issues/1223). The `CoworkPromptInput` sent "输入文件" (Input file) to the AI in English environments. This was **fixed** in [PR #1224](https://github.com/netease-youdao/LobsterAI/pull/1224).

**Open Concern:** [PR #1550](https://github.com/netease-youdao/LobsterAI/pull/1550) (fixes gateway validation errors for "do not notify" scheduled tasks) is still **open** and was reported in April. This is a potential stability blocker for users who create tasks via IM.

## 6. Feature Requests & Roadmap Signals

The PRs merged today (especially in Public Library and DSH Analytics) are the clearest indicators of the project's roadmap priorities.

- **Privacy-Conscious Analytics:** The project is introducing telemetry for DSH usage but went out of its way to move this to the renderer and make it "fire-and-forget." This suggests a design philosophy of data minimization and performance.

- **Agent UX Refinements:** The fixes in [PR #1224](https://github.com/netease-youdao/LobsterAI/pull/1224) (Escape key support, double-click prevention) indicate a push for more polished, "native-feel" dialogs within the agent creation workflow.

- **DeepSeek Harness (DSH) Focus:** The rapid iteration on the DSH runtime (`0.1.1-rc.1`) suggests it is a core, actively developed experimental feature. Expect this to become more stable and potentially a flagship feature in the next few releases.

## 7. User Feedback Summary

- **Critical Pain Point (Resolved):** **Hardcoded Chinese text** is a major issue for the non-Chinese user base. The project has a clear `AGENTS.md` rule against this, showing the community values internationalization.
- **Moderate Pain Point (Resolved):** **Unpredictable Sorting** in the Scheduled Task list was confusing users. They could not find new tasks, and the list order made no sense. This was fixed in April's PR [#1218](https://github.com/netease-youdao/LobsterAI/pull/1218).
- **Implicit Feedback:** The extensive UI polish in the Artifacts/Library section ([#2514](https://github.com/netease-youdao/LobsterAI/pull/2514)) suggests users felt the feature was clunky (difficult to search, confusing states, poor modal sizing).

## 8. Backlog Watch

- **High Priority: [PR #1550](https://github.com/netease-youdao/LobsterAI/pull/1550) — “不通知” (Do Not Notify) Delivery Mode Validation Error.** This PR has been open since **April 7** and fixes a real bug where scheduled tasks created via chat/IM fail at runtime with a gateway validation error if the delivery mode is "none". This is a user-facing blocker that has seemingly been ignored for months. Maintainers should merge this or provide an update.

- **Low Concern: [Issue #1217](https://github.com/netease-youdao/LobsterAI/issues/1217) — Intermittent Gateway Restarts.** This was a high-severity bug (multiple restarts per day on Windows) that was closed as stale. If no fix was shipped, this could reappear in the community. It is worth a maintainer verifying whether the root cause is known.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-08-22

## 1. Today's Overview

Moltis is seeing moderate but focused activity today. Two new issues were opened, both involving the cron/scheduling subsystem (`heartbeat.active_hours`) and the WhatsApp connector, signaling that the recent wave of connector and scheduler work is meeting real-world edge cases. The project's main velocity is on the PR side: 8 pull requests were updated in the last 24 hours, with 7 still open and 1 merged. The open PRs cover a broad cross-section of the codebase — WhatsApp media handling, browser stealth mode, cron delivery routing, i18n (zh-TW), web sandboxing security, and Windows plugin compatibility. Overall, this suggests a healthy, multi-track development phase with maintainers actively reviewing contributions, though no new releases were cut today.

## 2. Releases

No new releases were published in the last 24 hours. The most recent release remains unspecified in this window. No migration notes or breaking changes to report.

## 3. Project Progress

**Merged/Closed PRs: 1**

- **[#1220 — fix(whatsapp): render Markdown in outbound messages](https://github.com/moltis-org/moltis/pull/1220)** *(closed/merged)*: This PR converts model-generated Markdown into WhatsApp-native markup immediately before outbound delivery. It applies to text messages and media captions, while preserving the original Markdown in session history and the web UI. This is a meaningful UX improvement for WhatsApp users interacting with AI agents, as raw Markdown (e.g., `**bold**`, `# headers`) was likely rendering as literal text in the WhatsApp client.

**Key advances in open PRs (in review):**
- **[#1228 — WhatsApp inbound file persistence](https://github.com/moltis-org/moltis/pull/1228)**: Downloads inbound WhatsApp documents/photos to a stable `local_path` for local tools, with a 20 MB size limit and dependency-free approach.
- **[#1226 — Cron delivery to originating chat](https://github.com/moltis-org/moltis/pull/1226)**: Ensures scheduled job output is routed back to the chat that scheduled it, using a transient delivery shortcut while preserving thread/topic routing.
- **[#1227 — Obscura stealth mode by default](https://github.com/moltis-org/moltis/pull/1227)**: Enables browser stealth mode by default, with a new config toggle (`tools.browser.obscura_stealth`, default `true`) for operators who want standard network behavior.

## 4. Community Hot Topics

All issues and PRs today have **0 comments** and **0 reactions**, so engagement levels are low at the moment. However, the most active threads by recency and area of focus are:

- **[#1224 — [Bug]: Tools stop working in shared Slack channels](https://github.com/moltis-org/moltis/issues/1224)** (opened by `affanshahid`, 2026-08-21): This is likely the most user-impacting issue today. The author reports that Moltis tools fail in shared Slack channels — a common enterprise scenario where multiple workspaces share a channel. The lack of detail in the summary (the issue says the author was asked to include session context) means maintainers will need to request more info, but the underlying need is clear: **enterprise collaboration features (shared channels) are not fully supported**.

- **[#1223 — heartbeat active_hours has no effect on a default config](https://github.com/moltis-org/moltis/issues/1223)** (opened by `Lstarsky0`, 2026-08-21): This is a well-documented bug report. The author identifies that `is_within_active_hours` parses the `end` time before special-casing `"24:00"`, rendering the entire active-hours window ineffective. This directly correlates to an existing open PR (**#1208**), so it's likely to be fixed soon.

**Underlying needs**: Users are hitting real-world integration gaps: Slack shared channels, WhatsApp file handling, and cron scheduling that respects user-defined time windows. These are all "day 2" problems that emerge when an AI assistant is deployed in production rather than in a demo environment.

## 5. Bugs & Stability

**Ranked by severity:**

1. **[#1224 — Tools stop working in shared Slack channels](https://github.com/moltis-org/moltis/issues/1224)** — **High severity** (user-facing, blocks core functionality in an enterprise setting). No fix PR exists yet. The issue was just opened, so maintainers likely haven't triaged it yet.

2. **[#1223 — heartbeat active_hours has no effect](https://github.com/moltis-org/moltis/issues/1223)** — **Medium severity** (feature doesn't work as documented, but not a crash or data-loss issue). **A fix PR exists: [#1208 — fix(cron): honor heartbeat active hours when the scheduler fires](https://github.com/moltis-org/moltis/pull/1208)**, opened 2026-08-17 and still open. The PR description explicitly closes #1205, which appears to be the same root cause. This issue (#1223) provides additional detail on the `"24:00"` parsing bug, which the PR may or may not address. Maintainers should review #1208 and ensure it fully resolves #1223's edge case.

**No crashes or regressions** were reported in the last 24 hours.

## 6. Feature Requests & Roadmap Signals

There are no explicit feature requests in today's data, but the open PRs signal clear roadmap directions:

- **WhatsApp media handling** (#1228, #1220): Moltis is investing heavily in making the WhatsApp connector production-ready — both inbound file persistence and outbound Markdown rendering are being addressed.
- **Browser stealth** (#1227): Defaulting to stealth mode (with an opt-out config flag) suggests the team is prioritizing anti-detection for browser automation.
- **Cron scheduler intelligence** (#1226, #1208): The scheduler is being made smarter — respecting active hours and routing output back to the originating chat. This is a sign that Moltis is positioning itself as a reliable "autonomous agent" that runs scheduled jobs, not just a chat assistant.

**Prediction for next version**: WhatsApp inbound file support, browser stealth by default, and cron delivery-to-chat are all likely candidates for the next minor release. The active-hours fix (#1208) is also likely to land, as it has been open for 5 days with the associated issue getting renewed attention.

## 7. User Feedback Summary

- **Pain point: Enterprise Slack integration is fragile.** The shared-channel issue (#1224) suggests that Moltis's Slack integration works in simple cases but breaks in cross-workspace contexts. This is a common complaint for tools that market themselves to teams — shared channels are a Slack standard feature, and users will expect it to "just work."
- **Pain point: Documentation/behavior mismatch on active hours.** The heartbeat issue (#1223) shows a user reading the docs carefully, trying a configured window, and finding it does nothing. This erodes trust in the config system. The positive side: the user filed a detailed bug report with the root cause identified, which accelerates fixes.
- **Satisfaction signal**: The steady stream of contributor PRs (multiple from `rubenssoto`, a repeat contributor with substantial fix PRs) suggests a healthy contributor ecosystem around the project.

## 8. Backlog Watch

**[#468 — fix(plugins): use cmd.exe on Windows for shell hooks](https://github.com/moltis-org/moltis/pull/468)** — Opened **2026-03-23** (5 months ago), by `jmikedupont2`, last updated 2026-08-21. This PR fixes shell hooks failing on Windows because `sh -c` isn't available. The author reports it was tested on Windows 10 with CI passing. **Why it matters**: This is a long-standing cross-platform compatibility fix that is directly relevant to Windows users, a significant portion of any user base. The fact that it's been open for 5 months with no merge is a red flag — either the maintainers are hesitant to accept it (perhaps due to CI coverage concerns or design questions), or it's been deprioritized. The author's testing notes are thorough, and the change is small and well-scoped. **Recommendation**: Maintainers should review and merge this, or provide a definitive update on whether it will be included in a future release. Long-open PRs with clear value discourage future contributors.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-08-22

## 1. Today's Overview

CoPaw shows very high activity with 34 issues and 36 PRs updated in the last 24 hours. Interestingly, all 20 listed PRs were created on 2026-08-20 or later, indicating an active development cycle, with 15 PRs merged/closed. The issue tracker is balanced between open (19) and closed (15) items, suggesting good issue resolution throughput. The majority of issue activity revolves around bugs (11 bug reports, including 2 regressions), with a notable cluster of UX feature requests from power users. No releases were published today — the project appears to be converging toward a v2.1.1 release, with version-bump PRs and regressions documented on v2.1.1-beta.1.

---

## 2. Releases

No new releases were published in the last 24 hours. The most recent version is **v2.1.1-beta.1** (referenced in issue [#7206](https://github.com/agentscope-ai/QwenPaw/issues/7206)). A version-bump PR to v2.1.1b2 ([#7200](https://github.com/agentscope-ai/QwenPaw/pull/7200)) was closed today, suggesting the next release is imminent, likely containing the fixes merged in the current development round.

---

## 3. Project Progress

**Merged/Closed PRs (15 today):**

- **Version bump to v2.1.1b2** ([#7200](https://github.com/agentscope-ai/QwenPaw/pull/7200)) — closed, signaling imminent release.
- **Windows integration coverage fix** ([#7205](https://github.com/agentscope-ai/QwenPaw/pull/7205)) — fixes Windows nightly integration coverage silently reading 0 executed lines; adds fail-closed guard. A long-standing CI reliability issue since June 26.
- **Self-hosted multi-user Hub** ([#7112](https://github.com/agentscope-ai/QwenPaw/pull/7112)) — new `qwenpaw hub` control plane running isolated app instances for local accounts. Significant architectural addition.
- **Console performance for long chats** ([#7176](https://github.com/agentscope-ai/QwenPaw/pull/7176)) — addresses streaming re-parse and Markdown rendering inefficiencies.

**Open PRs advancing key features:**

- **QwenPaw-data runtime** ([#7190](https://github.com/agentscope-ai/QwenPaw/pull/7190)) — PyPI-installable runtime, docker-compose GAAP demo using Neo4j + PostgreSQL.
- **Creator 1.1.0** ([#7167](https://github.com/agentscope-ai/QwenPaw/pull/7167)) — Anthropic/Gemini protocols, broad image/video providers, expanded effects library, 2GB uploads.
- **Tool layer hardening** ([#7113](https://github.com/agentscope-ai/QwenPaw/pull/7113)) — transactional `apply_patch`, managed PTY shell sessions, bounded background output capture.
- **Session-scoped multi project directories** ([#6976](https://github.com/agentscope-ai/QwenPaw/pull/6976)) — ordered project dir list per chat.
- **Per-session model overrides** ([#5992](https://github.com/agentscope-ai/QwenPaw/pull/5992)) — long-running (since July 12) feature under review.
- **Token usage by agent attribution** ([#7207](https://github.com/agentscope-ai/QwenPaw/pull/7207)) — adds agent ID to usage events.

---

## 4. Community Hot Topics

- **MCP backend reconnection failure** ([#6524](https://github.com/agentscope-ai/QwenPaw/issues/6524), 6 comments) — When a remote MCP server restarts, QwenPaw stalls with stale `mcp-session-id`, requiring manual `list mcp` recovery. High user impact for anyone using remote MCP tools.
- **Idle freeze / self-kill** ([#6780](https://github.com/agentscope-ai/QwenPaw/issues/6780), 4 comments, closed) — Desktop app hangs after tens of minutes idle; needs process kill. Closed, pointing to a likely existing fix.
- **Tool call 404 on streamed sessions** ([#7016](https://github.com/agentscope-ai/QwenPaw/issues/7016), 3 comments) — `/tool-calls/{id}/offload` returns 404 during streaming, breaking tool execution in v2.1.0.
- **Embedding health check timeout hardcoded** ([#7156](https://github.com/agentscope-ai/QwenPaw/issues/7156), 3 comments) — Health check has 5s hardcoded timeout but actual elapsed 10.4s even when warm, causing spurious BM25-only fallback.

**Underlying needs:** The most active issues reveal users are pushing QwenPaw's AI-agent capabilities in production-like settings (MCP tooling, long-running agents, remote servers) and finding reliability gaps at the edges. The UX-related issues (approval-mode flooding [#7198], tool-call display [#7203], reasoning-process collapse [#7196]) all come from the same power user (rerbin) and cluster around "noisy agent process visibility."

---

## 5. Bugs & Stability

**High severity:**

- **v2.1.1-beta.1 regression: `/compact` always fails with `pydantic.ValidationError` when `compact_threshold_ratio == 0.9`** ([#7206](https://github.com/agentscope-ai/QwenPaw/issues/7206)) — regression vs. v2.1.0, confirmed by rollback test. Blocks context-compact workflow for scroll-strategy users.
- **Cross-session memory contamination** ([#7193](https://github.com/agentscope-ai/QwenPaw/issues/7193)) — Agent searching memory picks up another session's content of the same agent, causing task derailment. Data-isolation concern at memory layer.
- **Tool config inconsistency** ([#7210](https://github.com/agentscope-ai/QwenPaw/issues/7210)) — built-in tools all enabled in agent.json but not injected into session function schema.
- **history.db bloat to 7.6GB** ([#7168](https://github.com/agentscope-ai/QwenPaw/issues/7168), closed) — `recall_history` expand writes full tool output to history; duplicate writes for same interval. Closed — likely fixed via ToolResultCapMiddleware behavior change, though fix not linked.

**Medium severity:**

- **WebView2 renderer assertion crash** ([#6427](https://github.com/agentscope-ai/QwenPaw/issues/6427), open for ~1 month) — Crash at `msedge.dll+0x36c7f6d` (0x80000003), post.3 → post.4 regression; window turns blank shell.
- **Startup hang ~85s** ([#6430](https://github.com/agentscope-ai/QwenPaw/issues/6430), open ~1 month) — Consistent startup stall on every desktop launch.
- **Surrogate characters crash `daily_paper` job** ([#7199](https://github.com/agentscope-ai/QwenPaw/issues/7199)) — `UnicodeEncodeError: surrogates not allowed` in `write_atomic`.
- **Mojibake file card names** ([#7136](https://github.com/agentscope-ai/QwenPaw/issues/7136)) — percent-encoded Chinese filenames when `send_file_to_user`.

**Related fix PRs:** Injected-context persistence fix ([#7211](https://github.com/agentscope-ai/QwenPaw/pull/7211)) addresses request-local context leaking to visible chat history; e2e repair PR ([#7209](https://github.com/agentscope-ai/QwenPaw/pull/7209)) fixes failing cases caused by console redesign.

---

## 6. Feature Requests & Roadmap Signals

**High-probability next-version features:**

- **Hub (self-hosted multi-user control plane)** — already merged ([#7112](https://github.com/agentscope-ai/QwenPaw/pull/7112)), likely to debut in v2.1.1 final.
- **Token usage by agent** ([#7207](https://github.com/agentscope-ai/QwenPaw/pull/7207)) — analyst/cost-tracking orientation, aligned with enterprise adoption path.
- **Per-session model overrides** ([#5992](https://github.com/agentscope-ai/QwenPaw/pull/5992)) — long under review; high user value for multi-model workflows.

**Signal from user requests:**

- **UI/UX preferences cluster (from rerbin):**
  - Toggle to hide tool-call information ([#7203](https://github.com/agentscope-ai/QwenPaw/issues/7203))
  - Collapsible reasoning-process display, default folded ([#7196](https://github.com/agentscope-ai/QwenPaw/issues/7196))
  - Smarter approval gating — no approval needed for operations on intermediate/temp files created during this session ([#7198](https://github.com/agentscope-ai/QwenPaw/issues/7198))
- **Separate per-provider media caps** ([#7201](https://github.com/agentscope-ai/QwenPaw/issues/7201)) — three distinct caps with UI exposure.
- **Custom tool creation guide** ([#7204](https://github.com/agentscope-ai/QwenPaw/issues/7204)) — documentation gap signal; user can't find how to add custom tools.

**Predicted next version (v2.1.1) will likely include:** the two regressions fixes (#7206, #7210), Hub GA, console e2e repairs, runtime safety hardening, and possibly token-by-agent attribution.

---

## 7. User Feedback Summary

- **Approval-mode design is the loudest pain point** ([#7198](https://github.com/agentscope-ai/QwenPaw/issues/7198)) — user describes night-time unattended operation as "a disaster," with default auto mode generating "a flood of meaningless approvals." Suggests gating approval only for pre-existing files.
- **Conversation sorting frustration** — user surveyed mainstream agent products (Workbuddy, Trae, Doubao, Yuanbao, OpenClaw) and calls QwenPaw's session ordering "anti-human" ([#4816](https://github.com/agentscope-ai/QwenPaw/issues/4816), closed).
- **File-upload limitations illogical for desktop** ([#4854](https://github.com/agentscope-ai/QwenPaw/issues/4854), closed) — desktop shouldn't limit size (path-passing model), server deployments should.
- **Positive signal:** The same user (rerbin) filing both bug reports and polished feature requests suggests active, engaged power users investing time in the product — a sign of product-market fit in the agent-tooling space.
- **Memory contamination** ([#7193](https://github.com/agentscope-ai/QwenPaw/issues/7193)) is likely the most damaging trust issue reported this week — user observed agent "lost its way" and attempted another session's task.

---

## 8. Backlog Watch

**Long-open, no recent update, high value:**

- **WebView2 crash (post.3 → post.4)** ([#6427](https://github.com/agentscope-ai/QwenPaw/issues/6427)) — open since July 24, 2 comments, no linked fix PR. Desktop-blocking for affected users.
- **Startup hang ~85s** ([#6430](https://github.com/agentscope-ai/QwenPaw/issues/6430)) — open since July 24, 2 comments, no fix attached. Affects "every launch."
- **Per-session model overrides** ([#5992](https://github.com/agentscope-ai/QwenPaw/pull/5992)) — open since July 12, under review, but no maintainer response visible. High user demand for multi-model workflows.

**Recently active but unresolved:**

- **MCP back-end reconnection** ([#6524](https://github.com/agentscope-ai/QwenPaw/issues/6524)) — open since July 28, 6 comments, no linked fix. The most-commented active issue; impacts remote-MCP user workflows.
- **Reranker UI panel** ([#6399](https://github.com/agentscope-ai/QwenPaw/pull/6399)) — under review since July 23, complements backend reranker feature; stalled in review.

**Needing maintainer attention:** The first-time-contributor PRs (e.g., [#7211](https://github.com/agentscope-ai/QwenPaw/pull/7211), [#6808](https://github.com/agentscope-ai/QwenPaw/pull/6808), [#5992](https://github.com/agentscope-ai/QwenPaw/pull/5992)) are quality improvements (context isolation, UI correctness, model flexibility) that have languished; acknowledging and shepherding these through review would strengthen community trust and contribution velocity.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-08-22

## 1. Today's Overview

ZeroClaw is in a period of intense development and hardening, with 50 issues and 50 PRs updated in the last 24 hours, indicating a highly active maintainer and contributor community. Activity is heavily concentrated in three areas: security hardening (path traversal, credential leak, and delegation boundary fixes), SOP (Standard Operating Procedure) execution engine reliability, and ZeroCode TUI/CLI polish, alongside substantial architectural work on the plugin system. A high volume of open issues (47) versus closed (3) suggests a significant review and triage backlog, but the active `status:accepted` and `status:in-progress` labels on many items show maintainers are actively working through them. Multiple large, multi-crate PRs are open and in need of review, indicating significant architectural changes are in flight.

## 2. Releases

No new releases were published in the last 24 hours.

## 3. Project Progress

The following PRs were merged or closed in the last 24 hours:

- **[#10092 — fix(providers): redact Anthropic credential fragments](https://github.com/zeroclaw-labs/zeroclaw/pull/10092)** — *Merged*. This security fix directly addresses issue #9976 by stopping the logging of Anthropic credential fragments (`credential_head`/`credential_tail`) in debug events, while preserving non-secret diagnostic context.
- **Issue #9832 (zeroclaw-hardware compile failure) was closed**, presumably due to an associated fix.

Notably, a burst of PRs from contributor **1snob** ([#10226](https://github.com/zeroclaw-labs/zeroclaw/pull/10226), [#10227](https://github.com/zeroclaw-labs/zeroclaw/pull/10227), [#10228](https://github.com/zeroclaw-labs/zeroclaw/pull/10228), [#10229](https://github.com/zeroclaw-labs/zeroclaw/pull/10229)) claims to fix ZeroCode issues #10059 and #10058, but the duplication and automated nature of these submissions will require maintainer scrutiny.

## 4. Community Hot Topics

The most active discussions this week center on stability and security blockers:

- **[#9965 — ETXTBSY failure with runtime-written executable test fixtures](https://github.com/zeroclaw-labs/zeroclaw/issues/9965)** — 7 comments. This testing infrastructure bug is causing flaky CI failures under the parallel runtime gate, suggesting concurrency issues in the test harness itself.
- **[#9815 — forbidden_paths unreachable under allowed_roots](https://github.com/zeroclaw-labs/zeroclaw/issues/9815)** — 5 comments. As a `priority:p1, risk:high` security policy bug, this is justifiably a hot topic. The core issue is that the security boundary is bypassable, which undermines core config trust.
- **[#9855 — Matrix channel fails to resolve homeserver via .well-known delegation](https://github.com/zeroclaw-labs/zeroclaw/issues/9855)** — 3 comments, flagged `S0 - data loss / security risk`. This integration bug prevents Matrix-compliant homeservers from working, which could lead to configuration failures and data routing to the wrong server.

## 5. Bugs & Stability

The following bugs are active, ranked by severity:

- **S0 (Data loss / Security risk)**:
    - [#9855](https://github.com/zeroclaw-labs/zeroclaw/issues/9855) — Matrix homeserver resolution via `.well-known` delegation fails, risking routing to incorrect servers.
    - [#9947](https://github.com/zeroclaw-labs/zeroclaw/issues/9947) — Cron tools are not scoped to the owning agent, allowing cross-agent read/modify/delete of jobs.
    - [#9976](https://github.com/zeroclaw-labs/zeroclaw/issues/9976) — Anthropic credential fragments logged – *Fixed by merged PR #10092*.

- **S1 (Workflow blocked)**:
    - [#10061](https://github.com/zeroclaw-labs/zeroclaw/issues/10061) — Provider-rejected image poisons subsequent turns in a vision-capable session, blocking any later workflow.
    - [#9946](https://github.com/zeroclaw-labs/zeroclaw/issues/9946) — Unbounded waits on the `agent-browser` subprocess can hang agent turns indefinitely.
    - [#10042](https://github.com/zeroclaw-labs/zeroclaw/issues/10042) — MSRV CI job can time out during system dependency installation.

- **S2 (Degraded behavior)**:
    - [#9929](https://github.com/zeroclaw-labs/zeroclaw/issues/9929) — Headless SOP step turns are not persisted to the session store, causing state loss.
    - [#9872](https://github.com/zeroclaw-labs/zeroclaw/issues/9872) — Bounded delegate targets resolve filesystem to the wrong (delegator's) workspace.
    - [#10037](https://github.com/zeroclaw-labs/zeroclaw/issues/10037) — `POST /api/cron` silently stores an invalid `session_target` as isolated.
    - [#10058](https://github.com/zeroclaw-labs/zeroclaw/issues/10058), [#10062](https://github.com/zeroclaw-labs/zeroclaw/issues/10062), [#10045](https://github.com/zeroclaw-labs/zeroclaw/issues/10045) — ZeroCode TUI navigation, plan leakage, and persistence path issues.

- **Security (S2/S3)**:
    - [#9815](https://github.com/zeroclaw-labs/zeroclaw/issues/9815) — `forbidden_paths` security policy bypassable.
    - [#9883](https://github.com/zeroclaw-labs/zeroclaw/issues/9883) — Unbounded WebP conversion before validation, posing a DoS/security risk.
    - [#9811](https://github.com/zeroclaw-labs/zeroclaw/issues/9811) — `/health` reports a channel as healthy even when it's never connected (e.g., invalid Telegram token), a significant observability gap.

## 6. Feature Requests & Roadmap Signals

A number of enhancement requests signal a focus on UX and enterprise/security features:

- **Discord Role-Based Authorization** ([#9970](https://github.com/zeroclaw-labs/zeroclaw/issues/9970)): Allows channel access via roles rather than individual user IDs. This is a clear enterprise/team-oriented feature and is marked `status:in-progress`, making it a strong candidate for an upcoming release.
- **QwenCloud Provider Upgrade** ([#9943](https://github.com/zeroclaw-labs/zeroclaw/issues/9943)): Backward-compatible upgrade to QwenCloud. This is marked `status:accepted`, suggesting it is on the roadmap and likely in the next minor release.
- **ZeroCode Option-Backspace Word Deletion** ([#10059](https://github.com/zeroclaw-labs/zeroclaw/issues/10059)): An ergonomic fix for macOS users, marked as a "good first issue". A likely candidate for a quick patch release.
- **SOP Run Logs & Trigger Dedup** (PR [#10155](https://github.com/zeroclaw-labs/zeroclaw/pull/10155)): Open PR introducing interoperable run logs and trigger deduplication, which will significantly improve debugging and observability for SOP runners.

## 7. User Feedback Summary

User reports reveal pain points around configuration complexity, security boundaries, and execution reliability. The high number of `risk:high` and `priority:p1` labels on issues like #9815, #9816, and #9947 indicates frustration with security policies not behaving as documented. The recurring reports of flaky or hung runtime operations (issues #9929, #9946, #9965, #9805) suggest that for power users running complex automations, reliability is a primary concern. The ZeroCode TUI feedback (issues #10058, #10059, #10062) highlights that users are actively testing the interface and find the lack of standard navigation and state handling to be disruptive to their workflow.

## 8. Backlog Watch

The following open items appear to have been awaiting maintainer attention for a considerable time, risking staleness:

- **[PR #9110 — fix(lark): use constant_time_eq for verification_token comparison](https://github.com/zeroclaw-labs/zeroclaw/pull/9110)** — Created July 17, and stale-candidate. Security-hardening PR from a trusted contributor, flagged `needs-maintainer-review`.
- **[PR #9319 — refactor(runtime): seal the engine tool registry as ScopedToolRegistry](https://github.com/zeroclaw-labs/zeroclaw/pull/9319)** — Created July 23, stale-candidate, waiting on author. This is a large, architectural refactor with high security relevance.
- **[Issue #9786 — SOP: malformed SOP.toml is silently dropped](https://github.com/zeroclaw-labs/zeroclaw/issues/9786)** — Created August 6, `priority:p1, risk:high`. This silent config failure is a major usability and debuggability hazard. It's accepted but has not been addressed by a fix PR.
- **[Issue #9816 — Anthropic provider reports $0.00 spend, budget caps never fire](https://github.com/zeroclaw-labs/zeroclaw/issues/9816)** — Created August 7, `priority:p1`. While related to the fixed #9976, the root cause for this cost-tracking bug appears to be separate and remains open.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/kky-wollu/agents-radar).*
# OpenClaw Ecosystem Digest 2026-08-08

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-08-07 22:41 UTC

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

# OpenClaw Project Digest
**Date:** 2026-08-08

---

## 1. Today's Overview

OpenClaw remains in a high-intensity development and stabilization phase, with 500 issues and 500 PRs updated in the last 24 hours. The project is grappling with a significant backlog of critical bugs (P0/P1) concentrated in session-state management, data-loss prevention, and message-delivery reliability across multiple channels (Telegram, LINE, Feishu, Mattermost). Notably, there are **zero new releases** today, and the activity pattern (465 open issues vs. 35 closed) indicates the maintainer team is prioritizing triage and PR review over issue closure. A substantial cluster of issues carries the `clawsweeper:no-new-fix-pr` and `clawsweeper:needs-maintainer-review` labels, suggesting many long-standing bugs await maintainer decisions, while new, high-severity regressions (e.g., DB corruption, premature compaction causing data loss) demand immediate attention. The project is also seeing a wave of AI-assisted PRs (e.g., `clawsweeper[bot]`), indicating some level of automated contribution support.

## 2. Releases

**No new releases were published in the last 24 hours.** The most recent versions referenced in issues are `2026.7.2-beta.7` and `2026.7.2 (b4f01af)`.

---

## 3. Project Progress

The data shows **120 PRs were merged or closed** in the last 24 hours, though the top 30 by comment count are all still open. Key areas of active development and likely merged work include:

- **Provider Infrastructure:** A major refactor (#120351) consolidates shared generated-media download guards and binary-response adoption across 17+ providers (Azure, OpenAI, MiniMax, Bedrock, etc.), reducing code duplication and fixing unread response body leaks.
- **Code Mode Stack:** Multiple layers of a "Code Mode frontier stack" are advancing, including enforcing host concurrency without dropping calls (#119056) and making bridge lifecycle accounting exact (#119237).
- **Bug Fixes in Flight:** PRs addressing silent tool-arg dropping (#120248), premature compaction (#95885), OAuth robustness (#120174), and iMessage threading (#119289) are open and under review.
- **Developer Experience:** A fix (#119309) ensures the dev runtime rebuilds when core package sources change, preventing silent stale-code issues.
- **Model Catalog:** New Meta Muse Spark 1.2 models were added (#120373).

The sheer volume of open PRs (380) with many marked "ready for maintainer look" suggests a bottleneck in the review process, with maintainers (`vincentkoc`, `steipete`) carrying a heavy load.

## 4. Community Hot Topics

The highest-engagement issues reveal deep user frustration with reliability and data integrity:

- **[#116277 - DeepSeek v4 Flash silent reply failure (CLOSED)]** (125 comments, 🦞 diamond) - The hottest topic by far. The model silently fails to generate replies, forcing a generic fallback message. This is a critical UX failure, as users receive no response. The issue was closed, but the high comment count indicates significant community impact.
  [Link](https://github.com/openclaw/openclaw/issues/116277)
- **[#101290 - CLI startup preflight can corrupt live state DB]** (14 comments, 🦞 diamond) - Four database corruptions on macOS with "database disk image is malformed". This is a P0 data-loss issue that undermines trust in the system's stability.
  [Link](https://github.com/openclaw/openclaw/issues/101290)
- **[#45608 - Pre-reset agentic memory flush]** (11 comments, 4 👍) - Users request that `/new` and daily resets trigger the same memory flush as compaction, indicating a desire for consistent memory management and a need to preserve context intentionally.
  [Link](https://github.com/openclaw/openclaw/issues/45608)
- **[#85030 - MCP tools not injected into subagent]**(10 comments, 6 👍) - A significant functionality gap where documented MCP configuration is ignored for `sessions_spawn` sessions, breaking a core extensibility feature for subagents.
  [Link](https://github.com/openclaw/openclaw/issues/85030)

**Underlying Need:** The community is heavily focused on **reliability and trust**. The top issues are about silent failures, data loss, and broken features, not new functionality.

---

## 5. Bugs & Stability

This is a critical area today, with multiple P0 and P1 regressions reported:

**P0 (Critical - Data Loss / Crash):**
- **[#119263 - Agent DB v14->v15 migration fails]** - Gateway refuses to start after update. `no such column: entry_valid` in index repair. This is a release blocker. An open PR (#120350) may address related normalization, but no specific fix is linked. [Link](https://github.com/openclaw/openclaw/issues/119263)
- **[#118772 - Premature compaction causes data loss]** - `sessionEntry.totalTokens` inflation triggers compaction at 4-8% of context window, losing data. A fix PR (#95885) exists but is still open. [Link](https://github.com/openclaw/openclaw/issues/118772)
- **[#101290 - CLI preflight corrupts state DB]** - Four incidents of database corruption on macOS. [Link](https://github.com/openclaw/openclaw/issues/101290)

**P1 (High - Data Loss / Message Loss / Regressions):**
- **[#53408 - Write/exec tool parameters silently dropped]** - After long conversations, tools receive empty argument objects. A fix PR (#120248) is open, directly addressing this. [Link](https://github.com/openclaw/openclaw/issues/53408)
- **[#94939 - 6.x state migration leaves SQLite empty]** - MS Teams conversation store broken post-migration. [Link](https://github.com/openclaw/openclaw/issues/94939)
- **[#86684 - Subagent wake can compact parent branch]** - Unwanted compaction of a healthy parent session. [Link](https://github.com/openclaw/openclaw/issues/86684)
- **[#117445 / #86012 / #108865 - Channel-specific message loss]** - Feishu, LINE, and archived sessions silently drop inbound messages. These are recurring themes across channels.
  [Feishu](https://github.com/openclaw/openclaw/issues/117445) | [LINE](https://github.com/openclaw/openclaw/issues/86012) | [Archived](https://github.com/openclaw/openclaw/issues/108865)
- **[#119411 - Memory file watcher never reindexes]** - Silent memory index freeze; `memory status` reports healthy incorrectly. [Link](https://github.com/openclaw/openclaw/issues/119411)
- **[#97616 - Zombie child processes]** - Hook/tool child processes accumulate, degrading runtime performance. [Link](https://github.com/openclaw/openclaw/issues/97616)

**P1 (High - Runtime / Crash):**
- **[#119087 - Gateway cold start regressed ~2.5x]** - Significant performance regression on 1-vCPU containers. [Link](https://github.com/openclaw/openclaw/issues/119087)
- **[#109145 - Gateway listens but does not accept connections] [Link](https://github.com/openclaw/openclaw/issues/109145)

**Bottom Line:** The project is facing a stability crunch. Several of the most severe issues (premature compaction, tool-arg dropping, MCP injection) have open fix PRs, but they are stuck in review. Release quality appears at risk until these critical items are merged.

## 6. Feature Requests & Roadmap Signals

Despite the bug focus, several feature requests signal promising roadmap directions:

- **[#45608 - Pre-reset agentic memory flush]** (4 👍) - A strong candidate for next release, as it improves memory consistency using existing mechanisms. [Link](https://github.com/openclaw/openclaw/issues/45608)
- **[#81061 - `before_route_inbound_message` hook]** (3 👍) - A pre-routing hook for channel bridging and proxying. This is an architectural enhancement that would enable advanced patterns.  [Link](https://github.com/openclaw/openclaw/issues/81061)
- **[#99583 - Intelligent Session Auto-Titling]** (2 👍) - Lazy generation of titles using cheap models to reduce manual overhead.  [Link](https://github.com/openclaw/openclaw/issues/99583)
- **[#95516 - Skill lifecycle management]** (2 👍) - Auto-optimization and usage-based retirement of skills.  [Link](https://github.com/openclaw/openclaw/issues/95516)
- **[#87325 - Azure Foundry GPT Realtime Talk]** (1 👍) - First-class Azure support for realtime voice, extending the Talk feature.  [Link](https://github.com/openclaw/openclaw/issues/87325)
- **[#17840 - Opt-in reaction-triggered agent turns]** - Enabling interactive patterns like emoji-choice polling. [Link](https://github.com/openclaw/openclaw/issues/17840)

**Prediction:** The next release will likely prioritize bug fixes over new features. The addition of the `before_route_inbound_message` hook and pre-reset memory flush are smaller, well-scoped enhancements that could ship alongside the critical fixes.

## 7. User Feedback Summary

The sentiment from the most active issues is a mix of frustration and constructive criticism regarding **stability and transparency**.

- **Frustration with Silent Failures:** Users (e.g., #116277) are upset when the agent fails silently with a generic fallback, particularly for simple requests. This is a major trust issue.
- **Demand for Data Safety:** Issues like #101290 (DB corruption) and #118772 (data loss from compaction) are causing real concern, as users report loss of work and session history.
- **Feature Completeness for Coders:** The MCP subagent injection bug (#85030) and the drop of tool parameters (#53408) highlight a need for the platform to be predictable and reliable for technical users who depend on custom tools.
- **Accessibility Appreciation:** Positive feedback on recent accessibility improvements (#95601) shows the team is listening. Users want this to continue, with a request for VoiceOver-friendly chat history.
- **Recurring Theme: Channel Reliability:** Multiple issues (LINE, Feishu, Mattermost, WebChat) mention messages being silently lost or mis-ordered, indicating a systemic problem across the messaging integration layer.

## 8. Backlog Watch

Several important, long-standing issues have been open for months without a fix PR, requiring maintainer attention:

- **[#30381 - chatCompletions: ignore request model when x-openclaw-agent-id header is present]** (Open since 2026-03-01, 2 👍) - A logical feature that would simplify client integration. [Link](https://github.com/openclaw/openclaw/issues/30381)
- **[#75380 - provider-payload.jsonl and cache-trace.jsonl grow unbounded]** (Open since 2026-05-01, 1 👍) - A data-hygiene/security issue where diagnostic logs fill the disk without rotation. [Link](https://github.com/openclaw/openclaw/issues/75380)
- **[#30381 - same as above]** - **[#45494 - Cron jobs silently time out during LLM outages]** (Open since 2026-03-13) - A P1 regression for cron reliability. [Link](https://github.com/openclaw/openclaw/issues/45494)
- **[#74378 - CLI commands remain as node.exe processes on Windows]** (Open since 2026-04-29, 1 👍) - A long-standing Windows resource leak. [Link](https://github.com/openclaw/openclaw/issues/74378)
- **[#89228 - exec intermittently unavailable in isolated cron sessions]** (Open since 2026-06-01, 1 👍) - A regression with a complex root cause that remains unresolved. [Link](https://github.com/openclaw/openclaw/issues/89228)

These issues represent critical unfinished work and UX gaps that are reducing the reliability and usability of the platform for its core users.

---

## Cross-Ecosystem Comparison

# Cross-Project Comparison Report: Personal AI Assistant / Agent Open-Source Ecosystem
**Date:** 2026-08-08

---

## 1. Ecosystem Overview

The personal AI assistant open-source landscape is in a period of intense maturation, characterized by high-velocity development across a core set of projects. The ecosystem is currently prioritizing **reliability and trust** over new feature velocity, with the most severe bugs centering on data integrity (session/state corruption), silent failures, and message delivery reliability across multiple channels. Projects are converging on common architectural patterns—provider abstraction layers, tool/function-calling standards, and multi-channel gateway designs—while differentiating on target users (developers vs. enterprise vs. general consumers). Community sentiment reflects increasing production adoption: users are deploying these agents for real work and demanding enterprise-grade robustness, security, and observability. The ecosystem is also seeing a wave of AI-assisted contribution, with bots and AI-generated PRs becoming more prevalent.

---

## 2. Activity Comparison

| Project | Issues Updated | PRs Updated | Release Status | Health Score (1-10) | Key Notes |
|---------|---------------|-------------|----------------|---------------------|-----------|
| **OpenClaw** | 500 | 500 | No new release | 4/10 | Stability crunch; P0 data-loss bugs, review bottleneck |
| **Hermes Agent** | 50 | 50 | v0.20.0 (stable) | 6/10 | Post-release hardening; desktop stability issues |
| **NanoBot** | 10 | 21 | No new release | 7/10 | Healthy iteration; security isolation focus |
| **IronClaw** | 50 | 50 | No new release | 5/10 | QA cycle surfacing systemic truthfulness bugs |
| **ZeroClaw** | 50 | 50 | 0.8.4 (stable) | 5/10 | Security hardening; cron/SOP workflow blockers |
| **CoPaw (QwenPaw)** | 30 | 49 | v2.1.0-beta.2 | 6/10 | Beta churn; Docker/Windows regressions |
| **PicoClaw** | 4 | 14 | No new release | 6/10 | Stale PR backlog; community-contributed fixes waiting |
| **NanoClaw** | 0 | 12 | No new release | 7/10 | Healthy; Mattermost re-implementation, setup wizard |
| **LobsterAI** | 7 | 7 | 2026.8.7 | 7/10 | Regular release cadence; focused on desktop UX |
| **NullClaw** | 0 | 0 | N/A | N/A | No activity |
| **TinyClaw** | 0 | 0 | N/A | N/A | No activity |
| **Moltis** | 0 | 0 | N/A | N/A | No activity |
| **ZeptoClaw** | 0 | 0 | N/A | N/A | No activity |

*Health Score is a qualitative assessment based on: bug severity, release stability, maintainer responsiveness, community sentiment, and review throughput.*

---

## 3. OpenClaw's Position

**Advantages:**
- **Largest community and contributor base** — 500 issues/PRs updated in 24h is unmatched; 120 PRs merged/closed daily
- **Most extensive channel support** (17+ providers, Telegram, LINE, Feishu, Mattermost, etc.)
- **Most mature agent architecture** — Code Mode frontier stack, bridge lifecycle accounting, provider infrastructure consolidation
- **Highest visibility** — Most referenced and forked project in the ecosystem

**Technical Approach Differences:**
- Architectural focus on **provider consolidation** (shared guards, binary-response adoption) vs. NanoBot's channel-priority approach
- **Code Mode as a first-class stack** (enforcing concurrency, bridge lifecycle) — a unique differentiator not seen in peers
- Heavy investment in **session-state management** with migration tooling (v14->v15) — reflecting longer production history

**Community Size Comparison:**
- **Order of magnitude larger** than peers: OpenClaw's 24h activity (500 each) exceeds the next largest (Hermes, IronClaw, ZeroClaw at 50 each) by 10x
- Diamond-level engagement (🦞) on top issues attracting 14-125 comments — far exceeding any peer discussion

**Position Summary:** OpenClaw is the **reference implementation** and dominant player, but its scale creates review bottlenecks and accumulated technical debt. Its stability issues (data loss, DB corruption) are more consequential given the size of its user base. The next few weeks are critical for releasing the queued P0/P1 fixes.

---

## 4. Shared Technical Focus Areas

| Focus Area | Projects | Specific Needs |
|------------|----------|----------------|
| **Session/State Integrity** | OpenClaw, Hermes, NanoBot, CoPaw | Silent data loss, DB corruption, session retention trimming, state migration failures |
| **Channel Reliability** | OpenClaw, NanoBot, PicoClaw, IronClaw, ZeroClaw | Message drops (LINE, Feishu, WhatsApp), polling stalls, Telegram ACL resets, channel-specific encoding bugs |
| **Security & Sandboxing** | NanoBot, ZeroClaw, Hermes, CoPaw | Session file isolation, forbidden-path enforcement, CLI privilege escalation, plugin sandboxing |
| **Config Parsing Foot-Guns** | Hermes, PicoClaw, CoPaw | Quoted-boolean traps, tool parameter type confusion, corrupted config handling |
| **Memory Management** | OpenClaw, IronClaw, CoPaw, NanoBot | Non-recall across conversations, memory compression bugs, reindexing failures |
| **Agent Loop Control** | OpenClaw, CoPaw, NanoBot, ZeroClaw | Doom loops, silent task failures, infinite retries, goal loops |
| **Observability & Cost** | NanoBot, OpenClaw, ZeroClaw | Token consumption logging, cost tracking, diagnostic log rotation |
| **Model/Provider Compatibility** | CoPaw, ZeroClaw, OpenClaw, LobsterAI | Slashed model IDs, strict provider schema issues, provider-specific streaming bugs |
| **Cross-Platform Session Sharing** | Hermes, IronClaw, LobsterAI | Session context isolation per platform, unified memory across channels |
| **Tool-Call Correctness** | OpenClaw, PicoClaw, IronClaw | Silent tool-arg dropping, timeout handling, result wrapping |

The most **urgent shared requirements** are: (1) preventing silent failures (critical across 5+ projects), (2) data-loss-proof session management (4+ projects), and (3) better agent introspection — the ability to verify system state before making claims (IronClaw's top Pain Point is absent as a named focus in others, but related memory/state bugs exist).

---

## 5. Differentiation Analysis

| Project | Primary Target | Architecture | Key Strength | Key Weakness |
|---------|---------------|--------------|---------------|--------------|
| **OpenClaw** | Power users, developers | Multi-channel gateway, provider agnostic, Code Mode | Largest ecosystem, feature depth | Review bottleneck, stability debt |
| **Hermes Agent** | Developers, CLI-first users | CLI+TUI+Desktop, ACP client generalization | Strong CLI/core separation, active maintainer | Desktop cross-platform bugs |
| **NanoBot** | General consumers, SMBs | Channel-first, multi-platform (WeChat, WhatsApp, Telegram) | Rapid iteration, security-savvy maintainers | Smaller feature surface |
| **IronClaw** | Enterprise, QA-driven | Runner-based, doc-truth focus | Systematic QA process, architectural planning | Infrastructure instability, Windows gap |
| **ZeroClaw** | Rust ecosystem, security-minded | Rust-based, cron/SOP-first | Security hardening focus, principled design | Network-work blockers, provider bugs |
| **CoPaw (QwenPaw)** | Chinese-market users | Qwen/NLP-first, desktop+browser | Fast release cadence, community growth | Beta regressions, Docker/Windows issues |
| **PicoClaw** | Go ecosystem, lightweight | Go-based, multi-channel (DingTalk, WeChat, WhatsApp) | Strong contributor base, efficient architecture | Slow maintainer review, stale PR backlog |
| **NanoClaw** | OpenClaw alternative, JS ecosystem | TypeScript, skill-centric, channels (Mattermost, Dial) | Clean architecture, healthy community | Small issues count, early-stage features |
| **LobsterAI** | Desktop users (Windows) | Electron-based, OpenClaw integration | Polished desktop UX, regular releases | Proprietary feel, lacks self-hosted option |

**Key Architectural Distinctions:**
- **Language/Platform:** Rust (ZeroClaw) vs. Go (PicoClaw) vs. TypeScript (NanoClaw) vs. Electron (LobsterAI) vs. mono-language (OpenClaw, Hermes, CoPaw)
- **Deployment Model:** CoPaw's Docker-first approach vs. OpenClaw/ZeroClaw's native-first vs. LobsterAI's desktop-app-only
- **Agent Philosophy:** OpenClaw and Hermes push toward general-purpose assistants; ZeroClaw emphasizes Rules-based cron/SOP automation; CoPaw leans into "Agent OS" (mailbox, kanban, browser control); NanoBot prioritizes conversational intimacy across channels.

---

## 6. Community Momentum & Maturity

**Tier 1 — Rapid Iteration (High Activity, High Velocity):**
- **OpenClaw** — Sustainably massive; 120 PRs closed/day; characterized by both high contribution and high noise
- **Hermes Agent** — Post-release hardening; strong maintainer-driven cadence; decomposition workflow signals deep planning
- **ZeroClaw** — Security-driven spikes; rapid acceptance of P1s; responsive core team
- **IronClaw** — QA-driven momentum; doc-truth initiative and CI audit indicate scaling discipline

**Tier 2 — Steady, Healthy Growth:**
- **NanoBot** — Excellent iteration balance; 11 PRs merged/day; security-savvy maintainers
- **CoPaw (QwenPaw)** — Beta-release cycles with visible churn; strong first-time contributor inflow (6 in 24h)
- **PicoClaw** — Healthier than it appears; high-quality contributor base, but slower upstream review

**Tier 3 — Stabilizing/Moderate:**
- **NanoClaw** — Healthy; few issues but steady PR flow; core-team authored features progressing
- **LobsterAI** — Release train cadence established; polish-focused; community awaiting feature expansion

**Tier 4 — Dormant/No Activity:**
- **NullClaw, TinyClaw, Moltis, ZeptoClaw** — Inactive in the last 24h; may be paused, deprecated, or in stealth.

**Trend:** The ecosystem is bifurcating into a **"big three"** (OpenClaw, Hermes, ZeroClaw/IronClaw) versus specialized/niche projects (Go/Rust/Electron). The fast-moving projects are those with clear use-case focus (NanoBot's channel-first, CoPaw's China-market) — they are not competing head-on with OpenClaw but carving out niches. The core differentiator is **release cadence**: projects shipping regularly (LobsterAI, CoPaw beta, Hermes stable) maintain higher user trust despite bugs.

---

## 7. Trend Signals

1. **Reliability as the New Feature:** The biggest user pain point across the ecosystem is **silent failures** — tools not executing, messages not delivering, configs not applying — with no error surfaced. This is a recurring theme in 6+ projects and a clear opportunity. Spending on observability (logging, tracing, and explicit error surfacing) is the highest-ROI investment for agent developers.

2. **From Conversational to Operational:** Users are pushing agents toward **cron jobs, SOPs, scheduled tasks, and email/kanban integration** (ZeroClaw's cron/SOP blocker, CoPaw's email mailbox feature, OpenClaw's cron timeout bug). Agents are becoming infrastructure, not just chat UIs. Reliability in unattended operation is the new battleground.

3. **Security Isolation is Non-Negotiable:** The ecosystem is responding to production deployment demands with **session sandboxing, filesystem isolation, and operator-approved config paths** (NanoBot PRs #5279/#5283, ZeroClaw PR #9828, OpenClaw's forbidden-paths). Agent developers must bake isolation into the architecture from day one, not as an afterthought.

4. **The "Memory Wall" is Real:** Multiple projects struggle with **context non-recall across sessions** (IronClaw's #7185, OpenClaw's pre-reset flush request, NanoBot's session trimming). The market is ready for a robust cross-session memory solution. Projects solving this elegantly will have a significant advantage.

5. **Channel Breadth is Table Stakes, But Channel Depth Wins:** Everyone supports Telegram and WhatsApp; the differentiators are **rich channel features** (stickers, reactions, media round-trips, voice messages). Users increasingly expect the same UX on every channel, including niche ones (DingTalk, Mattermost, SimpleX).

6. **Cost Visibility is Emerging as a Key UX:** Users are hitting **runaway spend** without understanding why (NanoBot's token-burn complaint, ZeroClaw's untracked Anthropic budget). Expect agent platforms to ship detailed per-call cost tracing as a standard feature soon.

7. **AI-Assisted Contribution is Scalable, but Governance Gaps Exist:** `clawsweeper[bot]`, AI-assisted PRs, and many first-time contributors are submitting valid fixes quickly. However, the **review bottleneck** is now the critical path — projects should invest in CI and automated review tooling to triage these contributions efficiently.

8. **Desktop UX is Undervalued:** macOS/Windows desktop apps are a common failure point (Hermes freeze, CoPaw text selection, LobsterAI installer fixes). Users want **full IDE integration**, not just chat-in-terminal. A polish-focused desktop release could be a strong differentiator for projects targeting non-technical users.

---

*Report generated from community digest summaries dated 2026-08-08. Projects with no activity (NullClaw, TinyClaw, Moltis, ZeptoClaw) are listed for completeness but excluded from analysis.*

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

## NanoBot Project Digest — 2026-08-08

### 1. Today's Overview
Project activity is **high**, with 10 issues and 21 PRs updated in the last 24 hours. The maintainers/contributors are actively merging: 11 PRs were merged or closed, including critical fixes for the WebUI, WeChat/Weixin, Telegram, and session management. A strong **security and architecture wave** is underway: two open PRs address the removal of session history from the agent workspace (#5279) and per-session sandbox isolation (#5283), both responding to community-reported security concerns. The overall project health is good, with a steady cadence of bug fixes, security hardening, and UX improvements, though the volume of "p2" tagged fixes suggests a significant maintenance load.

---

### 2. Releases
No new releases were published in the last 24 hours. The project is in a heavy development cycle, with many unreleased fixes pending in the `main` branch.

---

### 3. Project Progress (Merged/Closed PRs)
A strong **11 PRs were merged/closed** today, demonstrating rapid iteration:

- **Session Integrity & Memory:**
  - **#5272** (merged): Fixes #5273 — preserves proactive channel delivery messages (cron notifications, job deliveries) during session retention trimming. This is a targeted bug fix for a data-loss issue.
  - **#5280** (merged): Fixes short idle sessions remaining invisible to Dream—archives them for Dream's `history.jsonl` input, extending the feature from #5231.
  - **#5231** (merged): Archives idle sessions for Dream, closing a gap where short sessions never produced `history.jsonl` entries.
- **WebUI & UX:**
  - **#5285** (merged): Fixes a regression where newly created topic routes could be lost before the session list acknowledged them.
  - **#5284** (merged): Removes the legacy/undocumented `/api/sessions/{key}/messages` route as part of a cleanup refactor.
  - **#5281** (merged): Fixes WebUI activity text being obfuscated by the scrollport mask, replacing it with pointer-transparent gradients.
  - **#5277** (merged): Expands the model preset editor inline in the WebUI, a UX enhancement for quicker model configuration.
- **Platform/Channel Reliability:**
  - **#5263** (merged): Harden the Weixin channel with updated protocol headers, QR challenges, retry logic, and lifecycle notifications.
- **Maintenance & Docs:**
  - **#5282** (merged): Modernizes dependency recovery guidance, replacing stale direct-package install hints with canonical `nanobot plugins enable` commands.
  - **#5287** (merged): Fixes a regression so channels not opting into transport defaults preserve global `sendProgress`/`sendToolHints` settings.
  - **#5268** (merged): Fixes history reads for attachments outside the media root by staging them properly (fixes #5264).

---

### 4. Community Hot Topics
The community is active, with deep technical discussions on **behavior, architecture, and security**.

- **#5266: Token Consumption Logging** (10 comments, still open)
  The most active discussion. Users report excessive token burn (millions of tokens in hours) without visible activity. The request for detailed per-call logging is a sign of **cost-management pain** in production use. The project currently lacks this observability, making it a high-priority UX/cost issue.
  [Issue #5266](https://github.com/HKUDS/nanobot/issues/5266)

- **#5198: Model Switching Restrictions** (3 comments, still open)
  Users want to switch models mid-session (as with cloud SaaS), but the `/model` command and UI blip don't work for this. This is a workflow bottleneck for advanced users who experiment with different models.
  [Issue #5198](https://github.com/HKUDS/nanobot/issues/5198)

- **#5149: Missing Audio on WhatsApp** (5 comments, still open)
  A clear bug: nanobot can't send audio via WhatsApp but can receive it. This is an unaddressed channel-specific functionality gap.
  [Issue #5149](https://github.com/HKUDS/nanobot/issues/5149)

- **#5289: Telegram Stickers & Reactions (0 comments, new)**
  A feature request (likely via bot) to add sticker support and agent-initiated reactions to the Telegram channel. User demand for richer channel integration is growing.
  [Issue #5289](https://github.com/HKUDS/nanobot/issues/5289)

---

### 5. Bugs & Stability
Multiple bugs reported/trimmed, ranked by severity:

- **High: #5273 (Session retention data loss)** *(Closed)*
  Retention trimming dropped proactive `_channel_delivery` messages. Fixed in today's PR #5272. This was a data-loss-class bug for cron/delivery use cases.
  [Issue #5273](https://github.com/HKUDS/nanobot/issues/5273) | [PR #5272](https://github.com/HKUDS/nanobot/pull/5272)

- **High: #5264 (Missing media URLs in history)** *(Closed)*
  Files outside media root lost `media_urls` after refresh. Fixed in PR #5268.
  [Issue #5264](https://github.com/HKUDS/nanobot/issues/5264) | [PR #5268](https://github.com/HKUDS/nanobot/pull/5268)

- **Medium: #5149 (No audio out on WhatsApp)** *(Open)*
  The agent cannot send audio to WhatsApp. No fix PR exists yet; backend protocol issue.
  [Issue #5149](https://github.com/HKUDS/nanobot/issues/5149)

- **Medium: #5256 (Goal loop)** *(Open)*
  `/goal` triggers dozens of repeated replies while awaiting user input, leading to a system loop. Indicates a flaw in agent loop control for multi-turn goals.
  [Issue #5256](https://github.com/HKUDS/nanobot/issues/5256)

- **Low: #5198 (Model switch failure)** *(Open)*
  Inability to change models mid-session. Not a crash, but a usability and logic bug. Linked to #5277 (WebUI model preset editor), which improves the model interface, but the core `/model` command session issue remains [#5198].
  [Issue #5198](https://github.com/HKUDS/nanobot/issues/5198)

---

### 6. Feature Requests & Roadmap Signals
Clear signals for the near-term roadmap:

- **Security & Isolation (Trending):**
  The most pressing signals are around **session data isolation**:
  - **#5276 (Session file isolation)**: Request to isolate temporary files per session.
  - **#5278 (Session history outside workspace)**: Security request to move session history out of the agent's file-tool reach. The **PR #5279** and **PR #5283 (per-session sandbox)** directly address this request and are in open review.
  - These indicate a high-security deployment context where users have multi-tenant or sensitive-data use cases, pushing for a more robust sandbox.

- **Channel Diversity:**
  - **PR #5289 (Telegram stickers/reactions)** is a feature request waiting to be picked up.
  - **PR #5288 (Agent Plugins with CLI Apps)** is a larger architectural feature integrating a vendor-neutral package format, portending a plugin ecosystem expansion.

- **Feature Predictions for Next Version:**
  - Session history migration out of the workspace (#5279) — very likely, given the security context and PR readiness.
  - Per-session sandbox mode (#5283) — likely to merge for non-WebUI channels next; will be a headline feature.
  - Meanwhile, #5288 (Agent Plugins) is likely farther out but will be a larger v1 feature.

---

### 7. User Feedback Summary
Real user pain points are concentrated on:
- **Operational Cost (Token Burn):** #5266 shows a significant frustration with opaque token usage, requiring better observability. Users want to know "which call does what."
- **Data Integrity:** Users are concerned about session history being accessible to the agent's own tools (#5278) and about proactive messages being trimmed (#5273).
- **Channel Reliability:** Users need advanced cross-channel support: Telegram stickers (#5289), WhatsApp audio output (#5149), and resilience to network instability (PR #5156 for Telegram) are requested.
- **UX and Control:** Mid-session model switching remains a strong UI/UX gap (#5198), and the `/goal` loop (#5256) points to a lack of control when multi-turn agent goals go haywire.

Overall sentiment is "positive but demanding": the project is advancing quickly, but users are pushing for robustness, security, and transparency in an increasingly sophisticated deployment environment.

---

### 8. Backlog Watch
These items have been open for a while and need maintainer attention.

- **PR #4276 (Model-agnostic computer use)** *(Open since June 10)*
  A large feature (computer_use + browser tools) with a 46-day lifespan. Untouched recently. It's a big surface area that might need rebase/deconfliction or design review to move forward.
  [PR #4276](https://github.com/HKUDS/nanobot/pull/4276)

- **PR #5156 (Telegram polling stall recovery)** *(Open since July 29, updated Aug 7)*
  A single-issue fix (Fixes #5171) for a real production bug in Telegram polling that doesn't self-heal. It’s been in review for over a week, likely needs a test scrub or maintainer approval.
  [PR #5156](https://github.com/HKUDS/nanobot/pull/5156)

- **Issue #5149 (No audio out on WhatsApp)** *(Open since July 28)*
  A persistent bug with a workaround absent for ~11 days. Given the platform’s multi-channel focus, this needs prioritization or explicit triage on whether it's a protocol-level constraint.
  [Issue #5149](https://github.com/HKUDS/nanobot/issues/5149)


</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-08-08

## 1. Today's Overview

Hermes Agent is in a period of high-intensity maintenance and backlog remediation. Activity is exceptionally high, with 50 issues and 50 PRs updated in the last 24 hours, indicating a very active maintainer team and a highly engaged community. The project is seeing a strong influx of bug reports (particularly desktop app stability on macOS and Windows, plus configuration parsing traps), alongside a steady stream of feature PRs. A distinctive pattern this cycle is the "decomposition" meta-issue workflow, where large epics are being broken down and tracked via structured GitHub issues. The project is clearly post-0.20.0 ("The Herald Release") and is focused on stability, cross-platform parity, and hardening the agent's operational boundaries (security, authentication, and state management).

## 2. Releases

No new releases were published in the last 24 hours. The current stable line remains v0.20.0 ("The Herald Release", 2026.8.3).

## 3. Project Progress

Three PRs were merged/closed in the last 24 hours:

- **[CLOSED] PR #21683 (type/bug, comp/gateway, comp/tools):** "fix: guard BlueBubbles sends with contact book" — This merges a security-focused fix requiring BlueBubbles human-friendly targets to resolve through an exact contact-book entry, and requiring direct phone sends to match exactly one active, verified, allow_outbound DM handle. This is a clear step toward preventing accidental or malicious sends to unverified contacts.
- **[CLOSED] PR #73249 (type/bug, comp/agent, comp/cli, area/auth):** "fix(auth): preserve explicit credential status resets" — This fixes a bug where explicitly reset credential IDs were not properly threaded through the persistence layer, preventing stale credentials from being re-used due to a newer-on-disk cooldown merge. This is an important fix for auth robustness and user control.
- **1 additional PR** was closed (not detailed in the top 20), keeping the total merged/closed count at 7.

**Active Featured PRs (Open):** The most active open PRs are focused on:
- **Security & Dependencies:** PR #79618 clears all 13 `uv audit` advisories and closes the two paths that reintroduce them (duplicate specs in tools/lazy_deps.py vs pyproject.toml).
- **Desktop Distribution:** PR #79599 introduces bundled installers with payloads, channels, eject, and silent adoption — a major overhaul to make the desktop app a single, self-contained artifact (no npm downloads at first launch).
- **ACP Generalization:** PR #68222 seeks to generalize the ACP client to drive any ACP-compatible coding agent, moving away from the per-agent near-copy pattern. This is a significant architectural refactor that has been open for several weeks and is flagged `needs-decision`.

## 4. Community Hot Topics

The most active discussions (by comment count) reveal a few key pain points:

1.  **Issue #63047 (13 comments, open, P1, comp/desktop):** "[Bug]: Desktop app becomes completely unresponsive (including Settings) after ~5 messages on macOS 27 beta" — This is the single most discussed issue. It details a full UI freeze that locks out Settings. The author notes it's distinct from the typing lag in #40692 and references a partial recovery ("hoping on some defreeze"). This is a **P1** and a major UX blocker for macOS users on the beta OS.

2.  **Issue #4335 (12 comments, 3 👍, open, P3, needs-decision):** "Feature Request: Cross-platform session context sharing (CLI ↔ Telegram)" — A long-standing feature request (created 2026-03-31) where each platform (CLI, Telegram, Discord) maintains isolated session stores. The request is for the agent to have knowledge of conversations across platforms. It's flagged `needs-decision`, suggesting the maintainers are evaluating architecture options.

3.  **Issue #79543 (8 comments, open, P3):** "[Hermes decomposition SL3-alpha] Writer primitives, attempt fencing, and public parity" — This is an example of the internal decomposition workflow, where the team is planning a non-executable epic for supported activation-boundary closures. This signifies deep internal planning for the agent's concurrency and state management.

4.  **Issue #79383 (7 comments, open, P3):** "[Hermes decomposition SL5] Goal turn markers, charge ledger, and fallbacks (stale-epoch blocker owner)" — Another decomposition planning issue, this time focusing on goal-tracking, a "charge ledger" (likely for resource/token accounting), and fallback mechanisms.

5.  **Issue #79890 (6 comments, open, P3, needs-decision):** "WhatsApp Feature Parity & Alignment Campaign — meta-issue" — A community-driven meta-issue to bring the WhatsApp bridge to full parity with the WhatsApp Business Platform Cloud API and the underlying backends (whatsapp-web.js / Baileys). It appears to be a hub for multiple sub-issues.

**Analysis:** The community is heavily invested in platform-specific reliability (particularly Desktop on macOS), cross-platform session continuity, and the roadmap for advanced agent features (writer primitives, goal tracking, charge ledgers). The decomposition issues suggest the maintainers are actively architecting for a more sophisticated agent loop.

## 5. Bugs & Stability

The project is facing a significant number of bug reports. Ranked by severity (P1 first, then P2 with security/state implications):

**P1 (Critical):**
- **Issue #63047 (comp/desktop):** Desktop app full UI freeze on macOS 27 beta. No fix PR identified yet.
- **Issue #81267 (comp/agent, comp/cron, tool/delegate):** Cron + background delegate_task leads to shared SessionDB use-after-close, silently dropping child transcripts and making completions unroutable. A dedicated fix PR **#81343** has been opened. This is a state-corruption bug with silent data loss.

**P2 (High):**
- **Issue #75801 (comp/agent, comp/tui, comp/desktop):** OpenCode Go gpt-5.6-luna omits `finish_reason`, causing 4 fake "network mid-stream" continuations and the desktop stripping the streamed answer. This is a compounding bug between the streaming API and the UI.
- **Issue #78993 (comp/agent):** Memory leak in `relay_runtime.pop()` causes Gateway crash and 100% SWAP fill. Needs reproduction. High impact for long-running gateways.
- **Issue #80989 (comp/agent, tool/terminal):** v0.20.0 terminal/clarify tool results wrapped in content-block structure, sometimes returning wrong file content. This is a data-integrity issue with tool output.
- **Issue #81322 (comp/cron, tool/terminal):** `lifecycle_guard` raises ValueError 'embedded null byte' when a terminal command path resolves to an ELF binary (e.g., venv python). Blocks benign commands.
- **Issue #81306 (comp/agent, provider/anthropic, area/auth):** **Security/Test bug:** Tests read `~/.claude/.credentials.json` from the real `$HOME`, injecting live OAuth credentials into hermetic test pools. This is an isolation failure in the test suite.
- **Issue #81314 (comp/cli, comp/desktop, area/config):** Shell hooks not registered in Desktop sessions because `serve` is excluded from `_AGENT_COMMANDS`. Silently ignores `pre_tool_call` block hooks.
- **Issue #78190 (comp/tools, tool/mcp, area/auth):** Gmail MCP works via CLI but fails in the gateway process with OAuthRegistrationError 404 on /register. This is a significant auth integration failure.

**Fix PRs available for several of these:**

- **#81267** → **PR #81343** (dedicated SessionDB for subagents)
- **#79331** (Telegram code block copy affordance bug, P2) → **PR #81346** (keep code blocks on legacy path)
- **#80989** (terminal/clarify wrapping) → Likely related to **PR #81347** by the same author (fix(terminal): keep mid-command backgrounded compounds valid shell).
- **#81345** (quoted 'false' for `start_new_session` enables it) → **PR #81345** (fix(wake): quoted 'false' now disables start_new_session)
- **#81348** (quoted 'false' for `mirror_delivery` and `preflight` in cron enables them) → **PR #81348**
- **#81322** (embedded null byte) → **PR #81347** addresses a related terminal shell syntax issue.

**Recurring Theme: "quoted 'false'" Config Traps.** A clear pattern has emerged with **PRs #81348 and #81345**: several configuration options are parsed with bare `bool(value)`, causing quoted strings `'false'` to evaluate to `True` (e.g., `bool("false")` is `True`). This is a foot-gun for users hand-editing YAML and is being systematically fixed.

## 6. Feature Requests & Roadmap Signals

The most prominent feature signals are:

1.  **Cross-platform session context sharing (Issue #4335):** This has been a long-standing request (since March) with 3 👍 and is flagged `needs-decision`. Given the architectural complexity (isolated session stores), this is a strong roadmap candidate for a future "multi-platform memory" feature.

2.  **Desktop Distribution Overhaul (PR #79599):** Bundled installers with channels is a clear roadmap item. This signals a move toward a more polished, consumer-grade desktop product with stable/beta channels.

3.  **ACP Client Generalization (PR #68222):** This is a P4 feature but is a major architectural enhancement that would position Hermes as a universal interface for coding agents. The fact it's been open since July 20 and is flagged `needs-decision` suggests it's a significant undertaking but is being actively considered.

4.  **WhatsApp Feature Parity (Issue #79890):** A meta-issue that consolidates requests for WhatsApp history, contacts, and parity with the Business API. This is a strong community push, indicating the WhatsApp bridge is a popular platform with unmet needs.

5.  **Root Dashboard Landing Pages (PR #71765):** This feature would allow plugins to override the `/` redirect, enabling a dashboard to become the landing page. This is a P3 feature that indicates a desire for deeper dashboard customization.

**Prediction:** The next minor release (v0.20.x) is likely to focus on the stability fixes detailed above (quoted-bool fixes, desktop installer improvements, SessionDB fix). A more feature-centric release is likely to be announced soon, given the large number of decomposition issues being planned (SL3-alpha, SL5). The "charge ledger" and "goal turn markers" from Issue #79383 suggest a future with more sophisticated agent self-management and accounting.

## 7. User Feedback Summary

- **Major Pain Point — macOS Desktop Stability:** The #1 issue (by comments) is a P1 UI freeze on macOS 27 beta. Users are reporting that the app locks up entirely, affecting even Settings. This is a critical reliability concern for a core platform.
- **Major Pain Point — Silent Failures:** Several reports revolve around silent failures: desktop app launching with no window (Issue #51327), hooks silently not firing (Issues #41457, #81314), and child transcripts being silently dropped (Issue #81267). Users are frustrated by the lack of visibility into these failures.
- **High Satisfaction with CLI/Gateway Separation:** There's a clear distinction in user feedback: the CLI tool and core agent are seen as robust, while the Desktop app (which wraps the TUI) and platform-specific binaries (Windows/macOS) are the source of most friction.
- **Configuration Foot-Guns:** The rise of "quoted 'false'" bugs (PRs #81348, #81345) indicates that users are hand-editing YAML configs and hitting subtle boolean-parsing issues. This signals a need for stricter config schema validation and clearer error messages.
- **Test Suite Security Concern:** The bug where tests read real credentials from `$HOME` (Issue #81306) is a serious trust issue, as it could leak developer OAuth credentials into logs or artifacts. While this is an internal test issue, it undermines confidence in the project's development hygiene.

## 8. Backlog Watch

Several long-standing issues and PRs need maintainer attention:

- **Issue #4335 (2026-03-31, P3, needs-decision):** Cross-platform session context sharing. Open for 4+ months with no clear decision. This is a high-value feature that the community wants.
- **PR #68222 (2026-07-20, P4, needs-decision):** ACP Client generalization. Open for over 2 weeks without a maintainer response on the design. This is a large architectural PR that needs a decision to proceed or close.
- **Issue #26006 (2026-05-15, P3):** CLI update-check cache invalidation. This PR has been open for 3 months and is a simple, contained fix. Its longevity may indicate maintainer bandwidth constraints or a lack of priority.
- **PR #21683 (now closed):** BlueBubbles contact book guard. This was a long-running PR (since May 8) that finally merged. This suggests the maintainers take security-sensitive PRs very seriously, with a long review cycle.
- **Issue #63047 (2026-07-12, P1):** The macOS desktop freeze is the most critical open issue affecting a core platform. It has been open for nearly a month and needs immediate prioritization.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest
**2026-08-08**

---

## 1. Today's Overview

PicoClaw shows moderate maintenance activity today, with 4 issues and 14 PRs updated in the last 24 hours — though notably **no new releases** and **no merges** were recorded. The project remains in a maintenance-and-stabilization phase, dominated by dependency bumps (7 of 14 PRs) and a handful of substantive community-contributed fixes awaiting review. The two PRs closed today (both dependency updates) suggest the project is keeping pace with upstream library changes, but the **accumulation of stale PRs** (10 of the 14 open PRs are flagged stale) indicates maintainer bandwidth may be a bottleneck. The most promising signal is the influx of community-contributed bug fixes and feature PRs addressing real usability issues in channel integrations (DingTalk, WeChat, WhatsApp) — pointing to a healthy, engaged contributor base despite slower upstream review cycles.

---

## 2. Releases

**No new releases** were published in this reporting period. The project appears to be conserving release cadence while accumulating changes for a future batch. The last release data is not available in this snapshot.

---

## 3. Project Progress

**Closed PRs (2):**
- **[#3291](https://github.com/sipeed/picoclaw/pull/3291)** — `build(deps): bump github.com/github/copilot-sdk/go from 0.2.0 to 1.0.8` (dependabot). Major version jump; closed, presumably merged.
- **[#3289](https://github.com/sipeed/picoclaw/pull/3289)** — `build(deps): bump github.com/pion/rtp from 1.10.2 to 1.10.5` (dependabot). Bugfix release for RTP library.

**Notable Open PRs (12 open) — feature work awaiting review:**
- **[#3321](https://github.com/sipeed/picoclaw/pull/3321)** — `fix(agent): move dynamic context after history to preserve prefix caching` — perf optimization preserving LLM prefix caching.
- **[#3320](https://github.com/sipeed/picoclaw/pull/3320)** — `fix(deps): bump whatsmeow to unblock WhatsApp "client outdated (405)"` — critical channel fix.
- **[#3319](https://github.com/sipeed/picoclaw/pull/3319)** — `fix(tools): honor exec timeout and boolean run options` — tool correctness fix.
- **[#3200](https://github.com/sipeed/picoclaw/pull/3200)** — `feat(models): add configurable default fallback chain` — feature for model fallback chains.
- **[#3283](https://github.com/sipeed/picoclaw/pull/3283)** — `fix(dingtalk): support picture/image message inbound` — channel enhancement.
- **[#3279](https://github.com/sipeed/picoclaw/pull/3279)** — `fix(seahorse): prevent tool-call format leakage into LLM summaries`.
- **[#3270](https://github.com/sipeed/picoclaw/pull/3270)** — `feat: add DashScope TTS provider and WeChat audio file sending` — dual feature: new TTS provider + WeChat audio support.
- **[#3271](https://github.com/sipeed/picoclaw/pull/3271)** — `chore(providers): update default model names to 2026-07 latest` — 9 providers refreshed.

**Key observation:** The project is accumulating significant feature work in open PRs without visible merges in this 24-hour window. A batch merge is likely imminent.

---

## 4. Community Hot Topics

- **[Issue #3093](https://github.com/sipeed/picoclaw/issues/3093) — "I need SimpleX or tox"** (6 comments, 1 👍): User requesting SimpleX, Wire, or Tox gateway support. The issue carried the most discussion this period. **Analysis:** Represents a growing demand for more privacy-focused, decentralized communication backends beyond mainstream channels — a possible niche differentiator.

- **[Issue #3308](https://github.com/sipeed/picoclaw/issues/3308) — Comprehensive Code Review** (1 comment, 0 👍): Report covering "concurrency hazards, goroutine leaks, and memory/speed optimizations" in SeaHorse, Channel Manager, and Hooks. Not a simple bug report but a substantive engineering audit — active interest in reliability engineering.

- **[Issue #3302](https://github.com/sipeed/picoclaw/issues/3302) — OAuth 2.1 for MCP servers** (2 comments, 0 👍): Follow-on request referencing previous issue #2546. Shows an active user base pushing for enterprise-grade authentication for MCP integrations.

- **[PR #3320](https://github.com/sipeed/picoclaw/pull/3320)** — WhatsApp 405 fix authored by `grrowl` — likely to get immediate maintainer attention due to the urgency of the broken channel.

**Pattern:** Active users are pushing the project in three directions: more communication channels (SimpleX, Telegram session management), better authentication (OAuth 2.1), and engineering robustness (code audits, caching fixes).

---

## 5. Bugs & Stability

**Reported issues (this period):**

1. **WhatsApp channel broken (PR fix in progress)** — **[PR #3320](https://github.com/sipeed/picoclaw/pull/3320)** — Severity: 🔴 High. WhatsApp rejects the pinned client version with `Client outdated (405)` — the native WhatsApp channel "stays dead," and the socket drops with no reconnect logic. A bump to `whatsmeow` is offered as the fix but is yet to be merged. This is the most urgent operational bug because it fully disables a channel.

2. **Tool-call format leakage into LLM summaries** — **[PR #3279](https://github.com/sipeed/picoclaw/pull/3279)** — Severity: 🟠 Medium. The `partsToReadableContent` in `seahorse` leaks tool-call formatting into user messages, degrading LLM summary quality. Description ties it to a previously known class of bugs. Fix offered but still unmerged.

3. **Exec tool ignoring timeouts and wrong type flags** — **[PR #3319](https://github.com/sipeed/picoclaw/pull/3319)** — Severity: 🟠 Medium. The `exec` tool advertises a per-run `timeout` argument but ignores it, always using the configured global timeout; also `background` and `pty` are declared as strings when they are booleans. A functional and schema-accuracy bug. Fix offered, unmerged.

4. **Concurrency & performance concerns** — **[Issue #3308](https://github.com/sipeed/picoclaw/issues/3308)** — Severity: 🟡 Low/Assessment. Reported as an audit request highlighting concurrency hazards, goroutine leaks, and memory optimizations in SeaHorse, Channel Manager, and Hooks. No specific exploit/crash reported; an engineering maturity concern.

**Pattern:** All non-dependency bug fixes have PRs already prepared but blocked pending review, which suggests the maintainers or contributors prioritize stability, but the queue is not draining quickly.

---

## 6. Feature Requests & Roadmap Signals

**Actively requested features this period:**

1. **Session list/switch command for Telegram (and other chat channels)** — **[Issue #3307](https://github.com/sipeed/picoclaw/issues/3307)**: The Web UI offers full session management, but chat users on Telegram cannot list/switch/delete sessions. This is a strong usability gap — will likely land in a future release if maintainers prioritize channel parity.

2. **OAuth 2.1 support for MCP servers** — **[Issue #3302](https://github.com/sipeed/picoclaw/issues/3302)**: Explicitly tagged "Nice-to-Have/Enhancement," referencing #2546. Signals user demand for production-grade MCP auth. Medium likelihood for next version.

3. **SimpleX / Wire / Tox gateways** — **[Issue #3093](https://github.com/sipeed/picoclaw/issues/3093)**: Privacy-focused chat gateways. Lower likelihood given scope; but if picked up, it would strongly differentiate PicoClaw in the AI-assistant space.

4. **Configurable default fallback chain** — **[PR #3200](https://github.com/sipeed/picoclaw/pull/3200)**: Model fallback chain for the Web UI, persisted via API. This one is already implemented в PR and if merged would be a flagship UX feature for the models page.

5. **DashScope TTS + WeChat audio sending** — **[PR #3270](https://github.com/sipeed/picoclaw/pull/3270)**: Adds Alibaba DashScope TTS provider and WeChat audio file support — visibly significant for Chinese-market users and multi-modal interactions.

**Prediction for next release:** Expect a batch merge including DingTalk image support, DashScope TTS, model name refreshes, several dependency bumps, and possibly the exec tool fix. The fallback chain PR (#3200) may be held for a larger feature milestone.

---

## 7. User Feedback Summary

- **Positives:** The community is producing a meaningful number of high-quality PRs on their own (channel features, bug fixes, model updates), which signals satisfaction with the architecture and a desire to build on top of it. Engaged power users performing complete code audits (#3308) indicates a technically mature user base.

- **Pain points identified this period:**
  - **Channel parity problems** — Telegram session management missing; WhatsApp breaking entirely on version bumps.
  - **Tool semantics and configuration confusion** — `exec` timeout and boolean flag bugs frustrate devs relying on that tool.
  - **Prefix-caching inefficiency** — conversations not optimal for LLM cost; someone cared enough to fix it proactively.

- **Needs:**
  - MCP server auth complexity is being requested at the enterprise level (OAuth 2.1).
  - Privacy-focused channels (SimpleX/Wire) — users choosing PicoClaw for local/small-infra privacy want decentralized chat integrations.

---

## 8. Backlog Watch

**Issues/PRs needing maintainer attention:**

1. **[Issue #3093](https://github.com/sipeed/picoclaw/issues/3093) — SimpleX/tox** (created 2026-06-10, still open): unaddressed gateway request with multiple upvotes. Long-standing community ask that hasn't received maintainer feedback.

2. **[PR #3271](https://github.com/sipeed/picoclaw/pull/3271) — Update default model names across 9 providers** (created 2026-07-20): stale, untouched for 18 days, but important — if not reviewed soon, default model names will drift further out-of-date, compounding user confusion.

3. **[PR #3279](https://github.com/sipeed/picoclaw/pull/3279) — sea-horse tool-call leakage fix** (created 2026-07-21): stale 18 days; a known class of bug worsening LLM output quality, with a ready-to-merge fix.

4. **[PR #3283](https://github.com/sipeed/picoclaw/pull/3283) — DingTalk image support** (created 2026-07-22): stale 17 days, feature-complete PR with no maintainer comment.

5. **[Issue #3307](https://github.com/sipeed/picoclaw/issues/3307) — Telegram session switch** (created 2026-07-30): 8 days without maintainer response; clear UX value.

**Maintainer signal:** Several quality, ready-to-merge PRs are sitting stale for 2+ weeks, suggesting either maintainer bandwidth constraints or a deliberate backlog-clearing strategy awaiting a batch release.

---

*Digest generated: 2026-08-08 from GitHub issue/PR activity. All timestamps UTC.*

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-08-08

## 1. Today's Overview

NanoClaw shows **moderate activity** today: while no new releases and no issues were updated in the last 24 hours, **12 pull requests** received updates — the highest single-day PR activity in recent weeks. The pipeline is healthy with **10 PRs still open** and **2 merged/closed**. The majority of activity centers on **channel integrations (Mattermost, Dial, Tavily MCP)** and **skill additions (AnyDoc, Tavily)**, indicating a strong community push toward ecosystem expansion. Notably, the long-dormant Mattermost PR #546 (original: Feb 26) was closed today and superseded by a fresh v2-compatible implementation (#3199), demonstrating active maintainership of the PR backlog.

## 2. Releases

**No new releases** were published in the last 24 hours. The most recent release remains the previous snapshot. No changelog, migration notes, or breaking changes to report. Contributors are actively working toward the next release — the setup-wizard template flow (#2909) has been in review since July 2 and may land in the next minor version (see Roadmap Signals).

## 3. Project Progress

**Merged/Closed today (2):**

- **PR #3197** — `fix(progress): 失败状态展示具体原因` *(merged)* — Improves failure-state UX by showing a specific reason (e.g., "动作失败：具体原因") instead of generic tool-action wording. Extracts the first valid error line from `resultSummary`, applies existing desensitization logic, and caps at 38 chars to prevent card truncation. Includes unit tests (274 targeted, 1,427 full suite passing) and a Feishu card JSON cross-layer test. This is a quality-of-life win for users of the progress card UI.
- **PR #546** — `[PR: Skill, Status: Blocked] Add Mattermost channel skill (/add-mattermost)` *(closed, superseded)* — Closed as obsolete. This PR targeted the pre-v2 `Channel`/`registry.ts` architecture that no longer exists. Super­seded by **PR #3199**, a fresh implementation against the current `ChannelAdapter`/`channel-registry.ts` contract.

## 4. Community Hot Topics

*(No issues; all activity is on PRs. None have comments or reactions recorded in the last 24h data, but the following PRs show sustained community and maintainer interest based on update frequency and authorship.)*

- **PR #3199 — Mattermost channel integration (v2 ChannelAdapter)** — *wakqasahmed* — Highly active; created and updated the same day. This fresh implementation supersedes the 5-month-old #546 and aligns with the current v2 architecture. Signals strong community desire for Mattermost support. → [Link](https://github.com/nanocoai/nanoclaw/pull/3199)
- **PR #2909 — Template setup flow + first-agent stamping** — *amit-shafnir* *(core-team)* — In review for 37 days. Adds the setup wizard "How should we create your first agent?" flow (fresh agent vs. template). Tied to the template loader (#2890). High roadmap significance for onboarding UX. → [Link](https://github.com/nanocoai/nanoclaw/pull/2909)
- **PR #3050 — Dial channel picker + runChannelSkill model** — *OmriBenShoham* — Active since July 14, updated today. Adds Dial to the channel picker/ wizard, including a `runChannelSkill` model. Part of the broader self-registration channel ecosystem. → [Link](https://github.com/nanocoai/nanoclaw/pull/3050)
- **PR #2346 — Unknown slash commands → normal chat** — *SidhayaPravda618* — 3 months old, updated today. Bug fix that prevents silent message drops when the Agent SDK misinterprets unknown slash commands. Community concern about silent failures. → [Link](https://github.com/nanocoai/nanoclaw/pull/2346)

**Underlying need:** The community is pushing for (a) more channel integrations (Mattermost, Dial) to broaden deployment options, (b) better skill tooling (Tavily MCP, AnyDoc document conversion), and (c) better setup/onboarding flow. The recurring theme is **"make it work out of the box on real installs"** — see the credential-proxy fix (#2705) and mount-ro fixes (#3196, #3149).

## 5. Bugs & Stability

No new bug reports (issues) were filed in the last 24h. However, several **bug-fix PRs** are in flight:

- **PR #3145 — DB migration: backfill destinations for existing wirings** *(fix, open)* — Migration 021 provisions missing channel destinations for existing messaging-group wirings, preserving custom local names and skipping already-valid wirings. Severity: **medium-high** — existing users upgrading may lose messaging destinations without this migration. → [Link](https://github.com/nanocoai/nanoclaw/pull/3145)
- **PR #2346 — Unknown slash commands dropped silently** *(fix, open)* — Unrecognized commands were categorized as `passthrough`, causing the SDK to produce output without `<message>` blocks, silently dropping the response. Severity: **medium** — silent data loss on malformed input. → [Link](https://github.com/nanocoai/nanoclaw/pull/2346)
- **PR #3196 — Fix/add mount readonly** *(fix, open)* — Addresses mount options for readonly. Severity: **medium** — potential security/permission misconfiguration for container users. → [Link](https://github.com/nanocoai/nanoclaw/pull/3196)
- **PR #3149 — CLI: add `--rw` flag to `groups config add-mount`** *(fix, open)* — Parity fix for CLI; mirrors the readonly mount fix. Severity: **medium**. → [Link](https://github.com/nanocoai/nanoclaw/pull/3149)
- **PR #2705 — `use-native-credential-proxy` actually bypasses the OneCLI gateway** *(fix, open)* — On real launchd/systemd installs, `nativeCredentialsEnabled()` only read `process.env`, causing silent fallback to the gateway. Severity: **medium-high** for users relying on native credential proxying. → [Link](https://github.com/nanocoai/nanoclaw/pull/2705)

No regressions or critical crashes reported today.

## 6. Feature Requests & Roadmap Signals

**Strong signals (likely in next release):**

- **Agent templates (#2909)** — Setup wizard template flow + first-agent stamping. Part 2 of 2; part 1 (#2890) already landed. This is the most likely feature to reach the next minor release, given core-team authorship and 37 days of review.
- **Mattermost integration (#3199)** — Fresh v2-channel implementation. High demand (original PR from Feb 26), now properly stacked against current architecture. Good candidate for the next release.
- **Dial channel (#3050)** — Channel picker addition with `runChannelSkill` model; signals broader self-registration channel architecture.

**Moderate signals (future candidates):**

- **Tavily MCP tool skill (#3190)** and **AnyDoc document conversion skill (#3198)** — Community-authored utility skills; likely to land individually soon.
- **Mattermost (#3199) + Dial (#3050) + existing channels** — Combined, they suggest a roadmap theme: **"broaden the channel adapter ecosystem."**
- **CLI mount parity (#3149)** — Minor feature; likely bundled with a fix release.

## 7. User Feedback Summary

**Pain points (from PR descriptions):**

- **Silent failures frustrate users:** PR #2346 (unknown slash commands silently dropped) and PR #2705 (credential proxy silently falls back to gateway) both describe scenarios where the system fails **without user-visible indication**. This is a recurring theme: users want failures to be explicit, not silent.
- **Upgrade safety concerns:** PR #3145 (DB migration for missing destinations) implies that users upgrading with existing wirings could lose destination configs — a data-integrity concern.
- **Credential management on real installs:** PR #2705 highlights friction for launchd/systemd users; env-only reads miss system-level config.
- **Mattermost demand persists:** The 5-month-old PR #546 never merged; the community re-submitted a fresh PR (#3199) within days. Clear unmet need for Mattermost users.
- **Mount/permissions friction:** Two separate PRs (#3196, #3149) address readonly mounts — indication that the current mount UX is confusing or error-prone.

**Satisfaction indicators:**

- **PR #3197** (failure-state reason display) merged — directly addresses a UX complaint (generic failure text). Test coverage was thorough (1,427 full-suite passing), signaling good quality bar.
- The ecosystem contributions (Tavily MCP, AnyDoc, Dial) suggest contributors find the skill/channel model accessible and worth building on. Nine contributors active in the last 24h is a healthy sign for community velocity.

## 8. Backlog Watch

Items needing maintainer attention (no comments/reactions in the data, but long-standing or likely-blocked):

- **PR #2346 — Unknown slash commands as normal chat** *(open, 92 days as of today)* — A clear bug fix with user-visible impact (silent drops). No comments in the last 24h. Needs review or a maintainer decision. → [Link](https://github.com/nanocoai/nanoclaw/pull/2346)
- **PR #2705 — `use-native-credential-proxy` bypass** *(open, 62 days)* — Fixes a real-install failure mode. Upstream rebase may be needed. → [Link](https://github.com/nanocoai/nanoclaw/pull/2705)
- **PR #2909 — Template setup flow** *(open, 37 days)* — Core-team authored but long in review; this is a key onboarding feature. The longer it sits, the more likely merge conflicts with the ever-moving `main`. → [Link](https://github.com/nanocoai/nanoclaw/pull/2909)
- **PR #3149 — CLI `--rw` flag** *(open, 10 days)* — Small parity fix that may be blocked by #3196; needs triage to avoid duplication.

**Project health verdict:** Healthy. No open issues, steady PR flow, active maintainer merge of #3197, and clear community investment in integrations. The main risk is **review latency on long-lived PRs** (two 60+ day fix PRs), but the Mattermost supersedure shows the team is actively managing the backlog.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-08-08

## 1. Today's Overview

IronClaw is in a period of intense stabilization and hardening. Activity is very high: 50 issues and 50 PRs were updated in the last 24 hours, with 14 closures in each category. The project is currently executing a substantial "doc-truth" initiative (5 PRs, #7375–#7381) to eliminate documentation drift, alongside a critical audit of the CI gate architecture (#7373) triggered by repeated red CI runs. The most prominent theme is **truthfulness and state-awareness**: multiple open bug-bash issues report the agent hallucinating connections, automations, and user identities that do not exist. A large batch of QA bugs (5+ issues) is open, mostly filed on 2026-08-05 through 08-07, indicating an ongoing QA cycle is surfacing systemic reliability problems in channel integration, memory recall, and infrastructure stability.

## 2. Releases

No new releases today. The latest activity concerns a **backport to `release/1.1.0-rc.1`** : PR [#7366](https://github.com/nearai/ironclaw/pull/7366) (merged/closed) ports PR #7309 to the RC branch, fixing an OAuth `scope` parameter bug (empty scope should be omitted). This suggests the 1.1.0-rc.1 train is still active and receiving selective cherry-picks.

## 3. Project Progress

**Closed/Merged PRs today (14 total):** Notable closures include:

- **[#7372](https://github.com/nearai/ironclaw/pull/7372) (closed)** — test(disclosure): Pins the schema-token reduction floor for the 91-tool wide-catalog benchmark, preventing slow drift in prompt-size headroom.
- **[#7366](https://github.com/nearai/ironclaw/pull/7366) (closed)** — fix(auth): OAuth scope fix ported to `release/1.1.0-rc.1` (see Releases).
- **[#7157](https://github.com/nearai/ironclaw/pull/7157) (closed)** — The large "explicit channel delivery tool" PR (two-lane model) has been merged, implementing the design in `docs/superpowers/specs/2026-07-27-channel-delivery-tool-design.md`. This is a major architectural feature for channel delivery.

**Feature advancement via open PRs:** The doc-truth pipeline (PRs #7375, #7376, #7378, #7379, #7381) is a coordinated 5-PR effort introducing deterministic doc-fact contract tests and a `docs-live` deployment branch to end docs↔release skew. Also notable: the "bulk `tool_describe`" PR [#7374](https://github.com/nearai/ironclaw/pull/7374) collapses per-schema round-trips, and [#7365](https://github.com/nearai/ironclaw/pull/7365) adds "always-on MEMORY.md prompt lane" as a fix for #7185.

## 4. Community Hot Topics

The most active issue by far is **[#7340](https://github.com/nearai/ironclaw/issues/7340)** ("No way to reset model settings to factory defaults", 6 comments). This is a user-experience gap — no path to restore default inference settings. It is a simple UI affordance request causing real frustration.

The second most discussed is **[#6989](https://github.com/nearai/ironclaw/issues/6989)** ("Token accounting bug: `ModelWorkRequest::for_assistant`", 4 comments, P1). This is a correctness bug in cost estimation with a clear technical description and fix location (estimating from the content reference string rather than the content itself). It is part of the pi-harness adoption program.

Beneath these, a strong cluster of QA bug-bash issues from `joe-rlo` (Slack identity leak [#7295](https://github.com/nearai/ironclaw/issues/7295), GitHub falsely connected [#7247](https://github.com/nearai/ironclaw/issues/7247), automation state hallucination [#7246](https://github.com/nearai/ironclaw/issues/7246), etc.) collectively show a pattern: **the agent fails to introspect real system state before making claims**.

## 5. Bugs & Stability

Ranked by severity (P1 first, then impact):

| Severity | Issue | Description | Fix PR? |
|----------|-------|-------------|---------|
| **P1** | [#7292](https://github.com/nearai/ironclaw/issues/7292) | Installed tool cannot be used; run fails with runner heartbeat error | None yet |
| **P1** | [#7298](https://github.com/nearai/ironclaw/issues/7298) | Request fails before send; monitoring system loses contact with runner (two distinct infra errors) | None yet |
| **P1** | [#7074](https://github.com/nearai/ironclaw/issues/7074) | Multi-tool meeting research fails after calendar retrieval (model calls unavailable function) | None yet |
| **P1** | [#5456](https://github.com/nearai/ironclaw/issues/5456) | Runner lease expires (90s inactivity threshold too aggressive) — long-running issue since 6/30 | None yet |
| **P1** | [#7295](https://github.com/nearai/ironclaw/issues/7295) | **Security-adjacent:** agent references wrong Slack user (identity leak/confusion) | None yet |
| **P1** | [#6590](https://github.com/nearai/ironclaw/issues/6590) | `serve` fails on Windows: workspace root overlaps default skill root | None yet |
| **High** | [#7368](https://github.com/nearai/ironclaw/issues/7368) | Channel turns take minutes on DeepSeek-class models (latency root cause for #6643) | None yet |
| **Medium** | [#7345](https://github.com/nearai/ironclaw/issues/7345) | Agent reports 61 automations vs UI showing 50 (state inconsistency) | None yet |
| **Medium** | [#7369](https://github.com/nearai/ironclaw/issues/7369) | No trace capture button on error state (UI gap, fix PR [#7370](https://github.com/nearai/ironclaw/pull/7370) exists) | **Yes** |
| **Fixed** | [#6476](https://github.com/nearai/ironclaw/issues/6476) | Slack `extension_activate` encoding error causing hallucinated admin requirements — **closed** | — |

**Fix PRs in flight:** [#7342](https://github.com/nearai/ironclaw/pull/7342) (classify HTTP 4xx/5xx as failures), [#7370](https://github.com/nearai/ironclaw/pull/7370) (trace capture button), [#7365](https://github.com/nearai/ironclaw/pull/7365) (memory recall), [#7131](https://github.com/nearai/ironclaw/pull/7131) (deliver triggered-run failures to creator).

## 6. Feature Requests & Roadmap Signals

Strong roadmap signals for the next minor version (post-1.1.0):

- **Doc-Truth Verification Pipeline** ([#7317](https://github.com/nearai/ironclaw/issues/7317), [#7375–7381](https://github.com/nearai/ironclaw/pull/7375)): The maintainers have accepted this proposal (5 PRs, designed by `thisisjoshford`). Expected in 1.2.0. This addresses a **process failing**: shipping breaking changes without docs.
- **Reset-to-defaults for model settings** ([#7340](https://github.com/nearai/ironclaw/issues/7340)): Simple UI win. Likely fast-tracked given user frustration.
- **Persisted-state compatibility gate before merge** ([#7380](https://github.com/nearai/ironclaw/issues/7380), epic): Direct response to the `1.0.0-rc.1` → `1.1.0-rc.1` upgrade gap. High risk, must-fix for release train reliability.
- **i18n for failure summaries** ([#7362](https://github.com/nearai/ironclaw/issues/7362)): Move 65 hardcoded English failure sentences into per-surface i18n with CLI resolver. Medium risk enhancement.
- **Deferred tool retrieval ranking** ([#7177](https://github.com/nearai/ironclaw/issues/7177)): Schema-aware ranked search. Closed as an enhancement, pending implementation.
- **Expanded stress coverage** ([#7360](https://github.com/nearai/ironclaw/issues/7360)): Phase 1 is in flight via PR [#7382](https://github.com/nearai/ironclaw/pull/7382). Necessary for catching built-in capability regressions.

## 7. User Feedback Summary

The dominant user pain points this cycle, in order of frequency:

1. **State hallucination / lack of introspection (7+ issues):** The agent claims GitHub/Slack/automations are connected or running when they are not, or references the wrong Slack user. This is the single most damaging class of bug for trust, and it spans multiple channels (Slack, Telegram, WebChat). It is a systemic issue with the model not grounding its claims in tool-verified state.
2. **Memory non-recall across conversations ([#7185](https://github.com/nearai/ironclaw/issues/7185)):** Multiple testers confirm context from conversation A is not available in B. There is a fix PR in flight ([#7365](https://github.com/nearai/ironclaw/pull/7365)).
3. **Infrastructure instability ([#7298](https://github.com/nearai/ironclaw/issues/7298), [#5456](https://github.com/nearai/ironclaw/issues/5456)):** Requests failing before send, lost contact with runner, lease expirations — these are platform-level reliability issues affecting the Railway-hosted QA instance.
4. **Latency on slower models ([#7368](https://github.com/nearai/ironclaw/issues/7368)):** Channel turns can take minutes on DeepSeek-class models, which is a poor UX for real-time chat surfaces.
5. **UI/UX gaps ([#7340](https://github.com/nearai/ironclaw/issues/7340), [#7369](https://github.com/nearai/ironclaw/issues/7369)):** Settings reset and trace capture are missing affordances.

Overall user sentiment is "frustrated by unreliable defaults" — the core agent loop works, but the edges (state truthfulness, memory persistence, infrastructure) are not yet production-solid.

## 8. Backlog Watch

Long-unanswered items needing maintainer attention:

- **[#5456](https://github.com/nearai/ironclaw/issues/5456)** (opened 2026-06-30, still open, 1 comment): Runner lease expiration — the dominant failure pattern for 6/30 testing. This is the oldest P1 bug still open. It is a fundamental infrastructure issue that has not had a fix PR in over five weeks.
- **[#6590](https://github.com/nearai/ironclaw/issues/6590)** (opened 2026-07-23, still open, 2 comments): Windows `serve` failure. Windows support appears to be a secondary concern, but this blocks a significant chunk of the developer base.
- **[#6475](https://github.com/nearai/ironclaw/issues/6475)** (opened 2026-07-22, **closed**): Telegram `/pair` command not recognized — now closed, presumably fixed.
- **[#4874](https://github.com/nearai/ironclaw/issues/4874)** (opened 2026-06-14, **closed**): WebChat v2 "Illegal invocation" on plain HTTP from non-localhost — closed after two months.
- **[#7076](https://github.com/nearai/ironclaw/pull/7076)** (opened 2026-08-03, still open): "Install the packages the catalog already publishes" by a new contributor (`neo-sky`). This has been rebased and updated; it is a large PR (XL) and needs maintainer review time. It is a candidate for "good first contribution" follow-up.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-08-08

## 1. Today's Overview

LobsterAI is in an active release and stabilization cycle, with a new version (2026.8.7) shipped on August 7 and a busy 24-hour period reflecting a coordinated push to merge the previous release branch into main. A total of 7 PRs and 7 Issues were touched in the last 24 hours, indicating a healthy and responsive development flow. The activity is concentrated on the renderer, main process, and OpenClaw integration areas, suggesting ongoing polish of the core user experience and system stability. While no new feature requests were closed, several historical stale issues were cleaned up (3 closed), keeping the backlog tidy. Overall project health appears strong with a clear release train cadence and rapid iteration.

## 2. Releases

**LobsterAI 2026.8.7** (released 2026-08-07) is the latest version. This is a minor release with the following key changes:

- **feat(cowork):** Added title-bar conversation search (via PR #2435), enabling users to search within Cowork conversations directly from the title bar.
- **feat:** Added Markdown LaTeX math delimiter support (via PR #2449), improving rendering of mathematical notation.
- **fix(win-installer):** Resolved a null watchdog exit code issue in the Windows installer (via PR #2446), improving installation/update reliability.

**Breaking Changes / Migration Notes:** None indicated. This appears to be a safe, incremental update focused on UX improvements and stability.

## 3. Project Progress

Six PRs were merged/closed in the last 24 hours, reflecting a significant batch of fixes and feature integrations:

1. **PR #2451 — [CLOSED] Release/2026.8.5 merge (area: renderer/main/openclaw/cowork, platform: windows)**: Merged the release branch into main, adding in-conversation search to Cowork, improved math rendering, IM analytics, OpenClaw configuration, and plugin installation, plus Windows installation/update reliability fixes.
2. **PR #2450 — [CLOSED] fix(cowork): restore fullscreen code toolbar clicks on Windows**: Fixed an issue where the fullscreen overlay code toolbar was unclickable on Windows by excluding it from Electron title bar drag regions.
3. **PR #2449 — [CLOSED] Fix/markdown latex math delimiters**: Added proper rendering support for LaTeX math delimiters in Markdown.
4. **PR #2448 — [CLOSED] Liuzhq/fix chat search**: Fixed chat search functionality in Cowork.
5. **PR #2446 — [CLOSED] fix(win-installer): rescue null watchdog exit code via extractor**: Stability fix for the Windows installer.
6. **PR #2445 — [CLOSED] fix(openclaw): strip plugin-index-managed keys from config.set**: Prevented plugin-index-managed keys from being persisted incorrectly in OpenClaw configuration.

**Open PR (not yet merged):**
- **PR #2452 — [OPEN] fix(openclaw): preserve provider for slashed model ids**: Addresses the open issue #2443 where model IDs containing slashes (e.g., from SiliconFlow) were losing their provider prefix (`custom_0` + `deepseek-ai/DeepSeek-V4-Flash` was being persisted as only the model ID), causing the renderer to misinterpret the model. This is a directly targeted fix for a reported bug.

**Features advanced this cycle:** Cowork search, LaTeX math rendering, OpenClaw configuration and provider handling, and Windows installer stability.

## 4. Community Hot Topics

The most active items in the community this period (based on comments and recency):

1. **Issue #1195 — [OPEN] Self-built skill not showing in skill panel** (2 comments): This is a long-standing, stale bug (created 2026-04-01) about skills installed by the agent being placed in the OpenClaw directory but not appearing in the UI after restart. It remains unresolved and has resurfaced with recent activity — a blocker for users building custom skills.

2. **Issue #1263 — [CLOSED] Duplicate scheduled tasks showing in UI** (2 comments): A stale but now-closed issue where scheduled tasks displayed twice with identical content and both showing API rate limit errors. The closure suggests either a duplicate-entry issue was resolved or it was triaged as stale.

3. **Issue #2443 — [OPEN] Model ID with slash fails in custom provider (SiliconFlow)** (1 comment): A fresh bug report from 2026-08-06 highlighting that custom OpenAI-compatible providers with slashed model IDs cannot be selected in the UI. This has a direct fix PR (#2452) already open, showing strong responsiveness.

4. **Issue #2447 — [OPEN] Execution with no results and no error message** (1 comment): A user reports silent failures during execution — a significant UX problem because there is no feedback to diagnose the issue.

5. **Issue #2444 — [OPEN] Feature request: input box editing mode** (0 comments): Requests a toggle for Enter-to-newline vs. Enter-to-send, citing the pain of long prompts and accidental sends. No maintainer response yet.

**Underlying needs:** Users are heavily impacted by (a) the reliability of custom skill installation, (b) model configuration flexibility for third-party providers, and (c) clear error messaging when operations fail. The community is actively requesting better configuration ergonomics and more graceful failure modes.

## 5. Bugs & Stability

Bugs reported today, ranked by severity:

1. **High — Silent execution failure without error output** (Issue #2447, OPEN): "Execution has no result and no error message." This is the most severe UX bug because it provides zero feedback, making debugging near-impossible. No fix PR is linked yet.

2. **Medium — Model ID with slash incompatible with UI** (Issue #2443, OPEN): Blocks users of SiliconFlow (and likely other providers with namespaced model IDs) from selecting their models in the UI. **Fix in progress:** PR #2452 directly addresses this by preserving the provider prefix for slashed model IDs.

3. **Medium — Self-built skills not visible after install** (Issue #1195, OPEN, stale): Skills installed to the OpenClaw path don't appear in the skill panel after restart. This is a long-standing (4-month-old) bug that frustrates skill developers. No fix PR is visible; it may relate to the recently merged OpenClaw plugin install fixes.

4. **Medium — Duplicate scheduled tasks shown** (Issue #1263, CLOSED, stale): Was showing tasks twice with API rate-limit errors. Closed today, but the closure may be due to staleness triage rather than a confirmed fix; the root cause remains unclear from the public data.

**Historical stability note:** Issue #1273 (sql.js WASM memory access out-of-bounds under high-frequency writes) was closed today as stale, but it flagged a non-recoverable crash and potential database corruption risk. No visible public fix; users with heavy Cowork sessions should be cautious.

## 6. Feature Requests & Roadmap Signals

Active feature requests signaling future direction:

1. **Input box editing mode** (Issue #2444): Users want an explicit toggle for "Enter = newline + Ctrl+Enter = send" mode, plus potentially a richer WYSIWYG Markdown editor for long prompts. Given the UX pain point (accidental sends), this is a plausible candidate for an upcoming UI polish release.

2. **Per-agent IM bot and model binding** (Issue #1265, CLOSED/stale): Requested the ability to bind different IM bots and models to different agents for team-based workflows. The request was closed as stale, but it signals a strong community desire for multi-agent orchestration. This aligns with the ongoing Cowork improvements and may resurface in future roadmap items.

**Prediction:** The next minor release is likely to include the slashed-model fix (PR #2452) already in flight. The editing mode request may be considered for a subsequent sprint given its clear UX value.

## 7. User Feedback Summary

Real user pain points and use cases from recent activity:

- **Skill developers are blocked** (Issue #1195): Users creating custom skills see "installation success" but the skill is invisible in the panel, undermining a core extension feature. This is a high-frustration issue due to the misleading success message.
- **Multi-agent teams are a desired use case** (Issue #1265): Users want different agents to handle different domains (e.g., one for orchestration, one for PPT generation) with distinct models per agent — indicating growing production use of LobsterAI for composite workflows.
- **Third-party model compatibility matters** (Issue #2443): Users are actively integrating with SiliconFlow and expect arbitrary OpenAI-compatible model IDs to work seamlessly; the slash in model IDs is a common convention for hosted models.
- **Silent failures damage trust** (Issue #2447): The "no output, no error" experience is a critical usability gap. Users cannot tell whether the issue is a model problem, a server problem, or a bug.
- **Long-prompt editing is awkward** (Issue #2444): The default Enter-to-send behavior is causing accidental sends, a frequent complaint among users building complex prompts.

**Overall sentiment:** Users are engaged and actively customizing LobsterAI, but they expect more resilience (better error surfacing) and more config flexibility. The fast fix turnaround for the slashed-model issue is a positive signal of maintainer attentiveness.

## 8. Backlog Watch

Issues or PRs needing maintainer attention:

1. **Issue #1195 — Self-built skill invisible in skill panel** (created 2026-04-01, updated 2026-08-07, OPEN): This is the oldest active bug on the list, dating back 4 months. It remains a frustrating blocker for skill developers. The recent OpenClaw plugin-install fixes (PR #2445) may be related, but no clear link has been made. Needs a dedicated investigation and fix.

2. **Issue #1263 — Duplicate scheduled tasks** (created 2026-04-02, CLOSED today): Closed as stale, but the underlying rate-limit error and duplicity were reported as "always reproducible." Should be verified that the symptom is actually resolved and not just closed due to inactivity.

3. **Issue #2447 — Silent execution failure** (created 2026-08-07, OPEN): Freshly reported and severe, but has only 1 comment (likely the author). Maintainers should reproduce and add error surfacing to keep user trust.

4. **PR #2452 — Preserve provider for slashed model IDs** (created 2026-08-07, OPEN): This directly fixes the reported SiliconFlow issue and should be prioritized for review and merge to unblock affected users.

5. **Issue #1273 — sql.js WASM memory out-of-bounds crash** (created 2026-04-02, CLOSED today as stale): While closed, the underlying risk of non-recoverable crash and database corruption under high-frequency writes is a serious stability concern. A follow-up issue or a changelog note about a proper database migration would benefit the community.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-08-08

## 1. Today's Overview

CoPaw (QwenPaw) is in a highly active **beta release cycle** with v2.1.0-beta.2 just published, showing strong momentum in both feature development and stabilization efforts. The project saw 30 issues and 49 PRs updated in the last 24 hours, with a healthy mix of open and closed items (19/11 issues, 27/22 PRs). The release includes critical fixes for CI fencing and checkpoint snapshots, while the community is actively reporting Windows-specific bugs, provider compatibility issues, and several regressions introduced in recent betas. Activity is sustained at a high level, with **6 first-time contributors** submitting PRs in the last day, indicating a growing community. Overall project health is strong—the maintainer team is responsive to bug reports and there is steady throughput of fixes, though beta regressions around desktop UX and plugin systems will need immediate attention.

## 2. Releases

**v2.1.0-beta.2** (published 2026-08-07)

Changes:
- **fix(ci):** fence-aware section extraction in real-behavior-proof (fixes #6626)
- **fix(checkpoints):** restore auto snapshots in web workspace bootstrap

This is a minor beta patch release with no breaking changes identified. Users on v2.1.0-beta.1 should upgrade to receive checkpoint restoration fixes and CI reliability improvements. No migration steps are required.

For full release details: https://github.com/agentscope-ai/QwenPaw/releases/tag/v2.1.0-beta.2

---

## 3. Project Progress

**22 PRs merged or closed in the last 24 hours**, with notable items including:

- **feat(website): downloads UI Refactoring and opt** (#4694) — long-running site downloads page refactor now complete
- **fix(shell): stop temp output file leakage and cap captured output** (#6799) — fixes a Windows defect that could leave **26GB orphan files** in `%TEMP%`
- **fix(chat): session identity deadlock, early session save, oversized prompt collapse** (#6750) — three front-end session-interaction bugs resolved
- **fix(browser): self-heal dead Playwright driver connections** (#6776) — "die once, dead forever" browser backend bug fixed
- **fix(console): show custom profile markdown files** (#6808) — restores ability to toggle custom persona files in the Files page
- **fix(providers): sanitize Chat Completions content for strict providers** (#6809) — StepFun provider compatibility fix
- **fix(acp): prevent final text loss when notifications race the prompt response** (#6623)
- **fix(agents): report fork finalization failures in background tasks** (#6725)
- **fix(plugins): isolate bare absolute imports per plugin namespace** (#6688) — fixes qwenpaw-creator installation failure
- **fix(memory): flush pending turns before compression** (#6564)
- **fix(onebot): handle remote inbound voice and image media** (#6715)
- **fix(config): handle corrupted agent config and invalid JSON** (#6615)
- **fix(providers): honor the Retry-After cap on the streaming retry path** (#6617)
- **feat(wechat): accept Chinese approval replies** (#6804)
- **feat(mailbox): intelligent email management assistant** (#6800) — new feature: automated email triage and response

**Major feature PRs still open and progressing:**
- **feat(memory): enhance ReMe configuration, embedding lifecycle, and Daily Paper** (#6772) — comprehensive memory system upgrade with real embedding validation and cron-based scheduling

---

## 4. Community Hot Topics

1. **[#6116 — Doom loop bug](https://github.com/agentscope-ai/QwenPaw/issues/6116)** (8 comments, closed as wontfix) — Agent repeatedly calls same tool in a single turn, wasting up to 6 API calls before warning. Underlying need: better loop detection and early termination. Though closed/not-fixed, sister issue #6768 remains open.

2. **[#6782 — Docker plugin/app market shows "maintenance"](https://github.com/agentscope-ai/QwenPaw/issues/6782)** (8 comments) — Multiple users on Docker 2.0.1 cannot use plugin/app markets at all. High-impact usability issue for Docker deployments.

3. **[#6732 — MCP tools periodically fail](https://github.com/agentscope-ai/QwenPaw/issues/6732)** (6 comments) — MCP tools stop working after several hours; restarting the container fixes it. Indicates an underlying resource leak or stale connection issue in the MCP server layer.

4. **[#6490 — Add Volcengine & Xiaomi MiMo providers](https://github.com/agentscope-ai/QwenPaw/issues/6490)** (4 comments) — Community actively requesting more built-in model providers, signaling demand for broader LLM ecosystem support among Chinese users.

5. **[#6786/#6787 — Telegram ACL resets on new tasks](https://github.com/agentscope-ai/QwenPaw/issues/6786)** (4+1 comments) — Approved Telegram users get blocked when new tasks spawn fresh workspace dirs with empty `access_control.json`. Fix PR #6788 is already open.

**Active PR discussions:** PRs #6750, #6799, #6776, #6809 draw community attention through related open issues, indicating broad interest in session stability, shell safety, and provider compatibility.

---

## 5. Bugs & Stability

Ranked by severity:

### High severity (core functionality failures/blockers)

1. **[#6782 — Docker plugin/app market always "maintenance"](https://github.com/agentscope-ai/QwenPaw/issues/6782)** — Blocks all plugin usage on Docker. No fix PR yet.

2. **[#6812 — Model 'unknown' execution failed in Google API](https://github.com/agentscope-ai/QwenPaw/issues/6812)** — Gemini provider sends `$schema` field in tool schemas, rejected by Google API. Breaks all Gemini-powered agents. No fix PR yet.

3. **[#6780 — Agent freezes/hangs after idle](https://github.com/agentscope-ai/QwenPaw/issues/6780)** — v2.0.1 self-deadlocks after inactivity; only process restart helps.

4. **[#6732 — MCP tool periodic failure](https://github.com/agentscope-ai/QwenPaw/issues/6732)** — MCP tools silently stop working after hours; container restart required.

5. **[#6768 — Infinite loop after multi-step task completion](https://github.com/agentscope-ai/QwenPaw/issues/6768)** — Agent unresponsive for hours after processing REST API financial records; session blocked indefinitely.

### Medium severity (regressions in betas)

6. **[#6785 — Profile category hard-codes official personas](https://github.com/agentscope-ai/QwenPaw/issues/6785)** — Custom persona `.md` files can no longer be toggled in Console UI (regression). **Fix PR #6808 is open**.

7. **[#6797 — Desktop mode text selection broken](https://github.com/agentscope-ai/QwenPaw/issues/6797)** — Cannot select/copy text in v2.1.0b2 desktop mode. **Two fix PRs open: #6802 and #6801**.

8. **[#6794 — Agent Kanban 405/404 errors](https://github.com/agentscope-ai/QwenPaw/issues/6794)** — Cannot create issues in Agent Kanban in v2.1.0b2; hot-reload sometimes returns 404.

9. **[#6786 — Telegram ACL reset](https://github.com/agentscope-ai/QwenPaw/issues/6786)** — Whitelist resets on new tasks. **Fix PR #6788 is open**.

10. **[#6810 — Windows installer lock-file issues](https://github.com/agentscope-ai/QwenPaw/issues/6810)** — NSIS cannot overwrite files; needs to terminate processes holding the install directory.

### Low severity

11. **[#6811 — OpenAI Responses continuation ignores disable_thinking](https://github.com/agentscope-ai/QwenPaw/issues/6811)** — Scroll eviction summary misreports cancellation as malformed output.
12. **[#6803 — OpenAI-compatible strict providers rejected](https://github.com/agentscope-ai/QwenPaw/issues/6803)** — StepFun rejects Responses-API content types. **Fix PR #6809 is open**.
13. **[#6807/#6806 — qwenpaw-creator plugin broken on Windows](https://github.com/agentscope-ai/QwenPaw/issues/6807)** — Media generation and model config saving both fail on Windows.
14. **[#6775 — Malware Bytes flags Desktop version](https://github.com/agentscope-ai/QwenPaw/issues/6775)** — Trojan Loader detection; likely false positive but needs maintainer response to avoid community distrust.
15. **[#6792 — Deprecated ACP npm packages](https://github.com/agentscope-ai/QwenPaw/issues/6792)** — Runner uses `@zed-industries/claude-agent-acp` / `@zed-industries/codex-acp`.

---

## 6. Feature Requests & Roadmap Signals

**High-likelihood for next release (v2.1.0 GA or v2.1.1):**

1. **[New built-in providers: Volcengine & Xiaomi MiMo (#6490)](https://github.com/agentscope-ai/QwenPaw/issues/6490)** — Both are straightforward endpoint additions; strong user demand from the Chinese ecosystem.
2. **[Add qwen3.8-max-preview to Aliyun model list (#6285)](https://github.com/agentscope-ai/QwenPaw/issues/6285)** — Trivial update to hardcoded model list; likely to ship quickly.
3. **[Configurable Chrome tab lifetime (#6770)](https://github.com/agentscope-ai/QwenPaw/issues/6770)** — Community wants control over when browser tabs persist across response cycles.

**New feature PRs in flight:**
- **Email management assistant (#6800)** — intelligent inbox triage with real-time push notifications; significant new capability if merged
- **ReMe memory enhancements (#6772)** — Daily Paper summaries, embedding lifecycle management, cron-based memory tasks

**Longer-term roadmap signals:**
- Desktop usability improvements (single-click app launch, text selection, "exit full mode" button) — indicates desktop mode is being actively positioned as a primary UI
- Chinese-language approval replies in WeChat (#6804) — localization depth increasing for Chinese enterprise users
- ACP runner updates (#6792) — infrastructure modernization

---

## 7. User Feedback Summary

**Pain points:**

- **Docker users are particularly affected**: plugin/app markets broken (#6782), MCP tool failures (#6732), idle freezes (#6780) — multiple reports all pinned to the 2.0.1 Docker image
- **Beta churn is real**: users on v2.1.0b1/b2 report regressions — no text selection in desktop mode (#6797), double-click app launch (#6790), cannot submit new sessions during tasks (#6796), Profile toggles broken (#6785) — indicating the beta testing community is active but frustrated by obvious UX regressions
- **Windows stability**: malware false-positive alarm (#6775), installer lock issues (#6810), temp file leak up to 26GB (#6799) — Windows remains the weakest platform for polish
- **Agent reliability concerns**: doom loops (#6116, #6768), MCP connective tissue (#6732), shell command quirks (#6565) — trust in Agent autonomy is being challenged

**Positive signals:**

- First-time contributors are submitting substantial, well-analyzed fixes (#6799, #6750, #6776) — the project is attracting quality contributors
- Users are providing detailed root-cause analyses with AI assistance, improving issue quality
- Feature requests show strong desire to use QwenPaw as a primary Agent OS (email management, browser control, kanban)

**Satisfaction:** Mixed. Users appreciate the product vision ("I love your work" — #6775) but beta regressions and Docker-specific breakage are eroding trust. The maintainers' responsiveness (multiple fix PRs within 24h of issue reports) is a strong positive.

---

## 8. Backlog Watch

**Critical items needing maintainer attention:**

1. **[#6782 — Docker plugin market broken](https://github.com/agentscope-ai/QwenPaw/issues/6782)** — 8 comments, no fix PR yet; affects all Docker users. Top priority.

2. **[#6732 — MCP tool periodic failure](https://github.com/agentscope-ai/QwenPaw/issues/6732)** — Unresolved for 2+ days; container restart is the only workaround. Likely a connection leak in the MCP server layer.

3. **[#6780 — Agent freezes when idle](https://github.com/agentscope-ai/QwenPaw/issues/6780)** — Still open with no maintainer response; users blocked.

4. **[#6775 — Malware Bytes false positive](https://github.com/agentscope-ai/QwenPaw/issues/6775)** — User explicitly says they are uninstalling until a response; needs rapid triage to prevent community distrust.

5. **[#6768 — Infinite loop after task completion](https://github.com/agentscope-ai/QwenPaw/issues/6768)** — Repeated "doom loop" class issues; needs systematic fix, not just detection.

**Long-standing issues needing attention:**

6. **[#6615 — Corrupted agent config handling PR](https://github.com/agentscope-ai/QwenPaw/pull/6615)** — Under review for 8 days; config robustness is important for production use.

7. **[#6617 — Retry-After header handling](https://github.com/agentscope-ai/QwenPaw/pull/6617)** — Under review for 8 days; rate-limit correctness affects paid API users.

8. **[#6564 — Memory flush before compression](https://github.com/agentscope-ai/QwenPaw/pull/6564)** — Open since July 30; memory reliability is core to Agent quality.

9. **[#6688 — Plugin import isolation](https://github.com/agentscope-ai/QwenPaw/pull/6688)** — Fixes a blocker for qwenpaw-creator installation, but has been open since August 4.

**Watch:** [#6490 — Volcengine/MiMo providers](https://github.com/agentscope-ai/QwenPaw/issues/6490) has 4 comments with no maintainer engagement yet; quick wins like this keep the community happy.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

Based on the provided GitHub data for ZeroClaw, here is the project digest for August 8, 2026.

---

# ZeroClaw Project Digest — 2026-08-08

## 1. Today's Overview
ZeroClaw is in a period of **high-intensity development and hardening**. With 50 issues and 50 PRs updated in the last 24 hours, activity is at a sustained peak, driven heavily by maintainers and senior contributors batch-landing security fixes. The community is engaged, but the issue tracker is dominated by **security-critical bugs (P1/P2)** and **RFCs**, indicating a focus on stabilizing the runtime, unblocking agent workflows (especially cron/SOPs), and closing security loopholes before expanding features. The volume of open PRs (47) suggests a large queue awaiting review.

## 2. Releases
*No new releases were published in the last 24 hours.* The latest version remains at 0.8.4, with significant pending changes in the PR queue.

## 3. Project Progress
The data shows a flurry of new proposals and fixes opened today, with a focus on web tooling and security boundaries:
- **Web Tooling Overhaul (PRs #9833, #9829, #9831, #9830):** A coordinated set of PRs from contributor JordanTheJet is reshaping the web tool surface. This includes a new `web_research` delegate agent, capping search result content, spilling large fetch responses to disk, and making browser automation opt-in.
- **Security Hardening (PRs #9827, #9828, #9826):** Multiple fixes were proposed to tighten shell confinement, prevent privileged CLI invocation by agents, and introduce an operator-approved config authoring path.
- **Workspace Rename (PR #9835):** A refactor to rename the root package `zeroclawlabs` to `zeroclaw` as the crates.io name is now under the project's control.

## 4. Community Hot Topics
The most discussed items show distinct community concerns:
- **Observability & Architecture RFCs:** The top-3 commented issues are all RFCs discussing core architecture changes: [OTel conversation correlation (#8933)](https://github.com/zeroclaw-labs/zeroclaw/issues/8933), [Todo tracker config migration (#9246)](https://github.com/zeroclaw-labs/zeroclaw/issues/9246), and [unifying providers architecture (#5937)](https://github.com/zeroclaw-labs/zeroclaw/issues/5937). This suggests a power-user community deeply invested in the platform's long-term technical direction.
- **Security Leak False Positives:** Issue [#9825](https://github.com/zeroclaw-labs/zeroclaw/issues/9825) highlights an interesting edge case where the leak detector is so effective it redacts public blockchain addresses, breaking payment URLs. This is a critical UX issue for any user in the crypto space.

## 5. Bugs & Stability
This is the dominant theme of the day, with several high-severity bugs reported. Fixes are often proposed within hours, showing a very responsive core team.
- **Critical (P1) - Security:**
    - **Forbidden Paths Bypass ([#9815](https://github.com/zeroclaw-labs/zeroclaw/issues/9815)):** `forbidden_paths` is effectively unreachable, allowing agents to access sensitive files inside the workspace. **No linked fix yet.**
    - **Gemini API Key Leak ([#9386](https://github.com/zeroclaw-labs/zeroclaw/issues/9386)):** API key in URL survives sanitization and is posted to chat. **Closed/Accepted**, fix likely in progress.
    - **CLI Privilege Escalation (PR [#9826](https://github.com/zeroclaw-labs/zeroclaw/pull/9826)):** Addresses a severe vector where an agent spawns the operator-privileged `zeroclaw` CLI.
- **Critical (P1) - Workflow Blocked:**
    - **Anthropic Cost Not Tracked ([#9816](https://github.com/zeroclaw-labs/zeroclaw/issues/9816)):** Budget caps never fire, leading to potential runaway spend.
    - **OpenRouter Streaming Drops Config ([#9775](https://github.com/zeroclaw-labs/zeroclaw/issues/9775)):** `provider_extra` is lost during streaming requests.
    - **SOP Auto-Mode Never Executes ([#9805](https://github.com/zeroclaw-labs/zeroclaw/issues/9805)):** Headless SOP runs rot as 'running' forever, holding concurrency slots.
    - **Health Check False Positive ([#9811](https://github.com/zeroclaw-labs/zeroclaw/issues/9811)):** `/health` reports a broken Telegram channel as healthy for 19+ hours.
- **Compilation Error (P0/Blocker):**
    - **Hardware Feature Broken ([#9832](https://github.com/zeroclaw-labs/zeroclaw/issues/9832)):** `zeroclaw-hardware` fails to compile with aarch64 Linux.

## 6. Feature Requests & Roadmap Signals
- **Agent Plugins Support ([#9810](https://github.com/zeroclaw-labs/zeroclaw/issues/9810)):** An RFC proposing support for the vendor-neutral Agent Plugins 1.0.0 standard. This is a major roadmap item that would allow loading community plugins, significantly extending ZeroClaw's ecosystem.
- **Web Tool Simplification ([#9824](https://github.com/zeroclaw-labs/zeroclaw/issues/9824)) & PRs:** The push to streamline web tools into `web_fetch`, `web_research`, and `http_request` suggests a focus on clarity and controllability over raw capability.
- **Config Authoring for Agents (PR [#9828](https://github.com/zeroclaw-labs/zeroclaw/pull/9828)):** Giving agents a safe, approved way to update their own config points toward a future of more autonomous operation, but under strict operator governance.

## 7. User Feedback Summary
- **Deep Frustration with Unmet Expectations:** Users using cron/SOPs for automation are hitting hard walls. Issues like [#9780](https://github.com/zeroclaw-labs/zeroclaw/issues/9780) (cron SOPs can't do network work) and [#9805](https://github.com/zeroclaw-labs/zeroclaw/issues/9805) show that documented use cases are not functional.
- **Model Compatibility Pitfalls:** Reports from users on Raspberry Pi with NVIDIA NIM models ([#9820](https://github.com/zeroclaw-labs/zeroclaw/issues/9820), [#9821](https://github.com/zeroclaw-labs/zeroclaw/issues/9821)) show that certain models are not invoking tools correctly, falling back to plain text or shell commands. This indicates a need for better model-specific prompting or validation.
- **High Confidence in Maintainers:** The volume of new issues and the rapid acceptance of them (e.g., `status:accepted` on many P1s) suggests that while users hit bugs, they trust the maintainers to fix them quickly, leading to a healthy feedback loop.

## 8. Backlog Watch
Several long-running items are still awaiting attention:
- **RFC: Workspace-relative forbidden paths ([#8424](https://github.com/zeroclaw-labs/zeroclaw/issues/8424)):** Open for over a month, this RFC directly addresses the root-cause fix for the critical security bug in #9815. It has high comment activity and requires maintainer review.
- **RFC: Unify providers architecture ([#5937](https://github.com/zeroclaw-labs/zeroclaw/issues/5937)):** Open since April. The 12 comments indicate ongoing discussion about a large, high-risk refactor that would address many provider-specific bugs.
- **PR: Reap exited stdio MCP processes ([#8948](https://github.com/zeroclaw-labs/zeroclaw/pull/8948)):** Open for a month. It was partially superseded by a rewrite (#9418) but still holds the remaining fixes for zombie processes. Needs integration with the new code.
- **PR: Matrix single-message progress drafts ([#8443](https://github.com/zeroclaw-labs/zeroclaw/pull/8443)):** A large (XL) enhancement for the Matrix channel that has been stalled for over a month, likely due to its size and the high volume of security work.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/kky-wollu/agents-radar).*
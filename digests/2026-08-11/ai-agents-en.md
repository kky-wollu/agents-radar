# OpenClaw Ecosystem Digest 2026-08-11

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-08-10 22:42 UTC

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

# OpenClaw Project Digest — 2026-08-11

## 1. Today's Overview

OpenClaw shows **heavy activity** with 500 issues and 500 PRs updated in the last 24 hours, indicating a very active development cycle. The project is **predominantly focused on stability and bug fixing**, with a significant portion of activity revolving around regressions in messaging channels (Telegram, Slack, Feishu), session state management, and authentication flows. A **large batch of PRs from maintainer `steipete`** (roughly 15+ PRs) suggests a coordinated refactoring and hardening effort is underway, targeting gateway internals, state serialization, and security redaction. While no new releases were published today, the volume and specificity of fixes in flight point to an imminent release candidate cycle. Community engagement is strong, with detailed bug reports and feature requests receiving substantial comment threads.

## 2. Releases

No new releases were published in the last 24 hours.

## 3. Project Progress

While no releases landed, a substantial number of PRs were merged or closed (143 total). Key merged/closed items include:

- **`#121741` (CLOSED)** — [fix(security): report DM isolation from effective routing](https://github.com/openclaw/openclaw/pull/121741): Fixes incorrect Doctor and security-audit results for DM route bindings and multi-channel setups.
- **`#121749` (CLOSED)** — [ci-probe: verify Windows sqlite snapshot repair](https://github.com/openclaw/openclaw/pull/121749): A throwaway CI probe to verify the Windows test lane after SQLite snapshot repairs.
- Several channel configuration fix PRs from `ayaangazali` (`#119356`, `#118157`, `#117287`, `#117302`) are now **ready for maintainer look**, addressing config schema rejections for documented settings in IRC, Mattermost, Feishu, and other bundled channels.
- **`#119001` (OPEN but progressing)** — [feat(codex): bind native realtime voice to existing sessions](https://github.com/openclaw/openclaw/pull/119001): A large feature PR that has been updated, indicating active work on integrating Codex Realtime as the brain of existing sessions.

The dominant theme in today's PRs is **internal refactoring and consolidation**, with multiple PRs from `steipete` focused on:
- `#121553`: Moving subagent concept directories (announce, completion, recovery, registry).
- `#121631`: Removing dead subagent state variants.
- `#121431` and `#121366`: Consolidating duplicate/coercion helpers across the codebase.
- `#121526`: Serializing ownership during database bootstrap to fix SQLite corruption on concurrent first-start.

## 4. Community Hot Topics

The most active community discussions center on recurring, high-impact bugs that erode user trust:

- **[#121058: Silent reply failures still recurring](https://github.com/openclaw/openclaw/issues/121058)** (40 comments): The top issue, reporting that a previously "closed" bug still occurs. This signals a **failure in the maintainer's ability to fully resolve complex, systemic issues** and is a major source of user frustration.
- **[#7707: Memory Trust Tagging by Source](https://github.com/openclaw/openclaw/issues/7707)** (33 comments): A long-standing feature request (since Feb) about preventing memory poisoning attacks. High engagement suggests security is a top community concern.
- **[#86519: Agent repeats identical replies on Telegram](https://github.com/openclaw/openclaw/issues/86519)** (15 comments): A P1 regression that was closed but generated significant discussion about duplicate message delivery paths.
- **[#42475: Per-agent cost budget enforcement](https://github.com/openclaw/openclaw/issues/42475)** (15 comments): Operators are seeking proactive controls to prevent runaway spend, indicating growing enterprise/production usage.

The underlying need across these hot topics is for **reliability and predictable behavior**, particularly in messaging channels and session management.

## 5. Bugs & Stability

This is the largest category of activity, with several high-priority (P0/P1) bugs reported or updated:

**Critical / P0:**
- **[#43661 (CLOSED): Session hangs when compaction times out](https://github.com/openclaw/openclaw/issues/43661)** — Indefinite hang and duplicate message loop. Closed, but a reminder of the severe impact of context management failures.

**High / P1:**
- **[#115908: Session transcript projection livelock](https://github.com/openclaw/openclaw/issues/115908)** — Sustained writes can cause a non-converging rebuild cycle that blocks the main thread, stalling all channels.
- **[#121526 (PR): SQLite database corruption on concurrent startup](https://github.com/openclaw/openclaw/pull/121526)** — Fixes a crash that could occur on concurrent first-start.
- **[#121647 (PR): Durable state stalls in long sessions](https://github.com/openclaw/openclaw/pull/121647)** — A fix for context engines stopping after a session exceeds 20k events or 8 MiB.
- **[#119087: Gateway cold start regression ~2.5x](https://github.com/openclaw/openclaw/issues/119087)** — Performance regression observed on 1-vCPU containers.
- **[#121235 (PR): `/stop` triggering restart recovery](https://github.com/openclaw/openclaw/pull/121235)** — Fix for a bug where explicit user cancellation could be misclassified.
- **[#121671, #121601, #121599 (PRs)]** — Fixes for cloud worker auth, delayed gateway updates due to open terminals, and centralization of provider diagnostic redaction.

**Recurring / Notable:**
- **[#121058: Silent reply failures](https://github.com/openclaw/openclaw/issues/121058)** — A P1 regression that continues despite a previous fix, indicating a deep-seated delivery issue.
- **[#96242 (CLOSED): Duplicate Telegram messages](https://github.com/openclaw/openclaw/issues/96242)** — Another closed issue highlighting the complexity of multi-path message delivery.

There are a significant number of open P1 bugs with fix PRs in progress, indicating a **proactive but strained maintainer response**.

## 6. Feature Requests & Roadmap Signals

The community is actively shaping the roadmap, with several high-value requests:

- **Security & Trust (Strong signal):**
    - [#7707: Memory Trust Tagging by Source](https://github.com/openclaw/openclaw/issues/7707) — A priority feature to prevent prompt injection via memory.
    - [#15032: Per-spawn tool restrictions for sub-agents](https://github.com/openclaw/openclaw/issues/15032) — Users want to build DMZ-like isolation for sub-agents.
    - [#40786: .gitignore-like exclude patterns for backup CLI](https://github.com/openclaw/openclaw/issues/40786) — Addresses data exposure and backup bloat.

- **Control & Governance:**
    - [#42475: Per-agent cost budget enforcement](https://github.com/openclaw/openclaw/issues/42475) — A "must-have" for production use.
    - [#27445: `announceTarget` option for sub-agent routing](https://github.com/openclaw/openclaw/issues/27445) — For more sophisticated workflow orchestration.

- **UX & Experience:**
    - [#33413: Slack tool-level progress](https://github.com/openclaw/openclaw/issues/33413) — Users want real-time visibility into agent actions.
    - [#45323: Slack-style @mention autocomplete](https://github.com/openclaw/openclaw/issues/45323) — A quality-of-life improvement for the Control UI.
    - [#121475 (PR): Desktop apps and browser autonomy for cloud workers](https://github.com/openclaw/openclaw/pull/121475) — Indicates the product is moving towards richer autonomous capabilities.

**Prediction for next version:** Given the volume of security-related requests and fixes, the next release is likely to focus heavily on **hardening the agent against prompt injection and memory poisoning**, alongside long-awaited features like **per-agent cost controls** and **improved sub-agent governance**.

## 7. User Feedback Summary

- **Frustration with unresolved regressions:** The recurring nature of bugs like silent replies (#121058) and duplicate messages (#96242) is a major pain point, undermining user confidence in the platform's reliability.
- **Desire for proactive control:** Users are asking for cost budgets, tool restrictions, and backup exclusion patterns — indicating a shift from experimenting with the tool to **operating it in production with governance**.
- **Performance anxiety:** The gateway cold start regression (#119087) and per-request auth/bundling overhead (#80131) highlight that performance is a growing concern, even for small-scale deployments.
- **Positive engagement with advanced features:** The numerous PRs to add realtime voice to Codex and desktop/browser autonomy for cloud workers suggest the community is excited about advanced, agentic use cases.
- **Documentation drift:** Multiple PRs and issues point to config schema rejecting documented options, a clear sign of **documentation and code drift that creates avoidable user friction**.

## 8. Backlog Watch

Several important issues remain open for extended periods, requiring maintainer attention:

- **[#7707: Memory Trust Tagging by Source](https://github.com/openclaw/openclaw/issues/7707)** (Since Feb 2026, 33 comments): While having a product-decision label, it has not been picked up. This is a major security feature.
- **[#40001: Write tool lacks append mode](https://github.com/openclaw/openclaw/issues/40001)** (Since Mar 2026, 13 comments): A P1 bug causing silent data loss. Still open, though multiple related PRs are linked.
- **[#47975: Subagent sessions persist after completion](https://github.com/openclaw/openclaw/issues/47975)** (Since Mar 2026, 10 comments): A P1 session-state issue that can make the main session unresponsive.
- **[#27445: `announceTarget` option](https://github.com/openclaw/openclaw/issues/27445)** (Since Feb 2026, 12 comments): A feature request with 5 👍 that would improve orchestration.
- **[#89571 (implied): Per-request auth/tool bundling performance](https://github.com/openclaw/openclaw/issues/80131)** (Since May 2026, 5 comments): The significant time-to-first-token overhead is a barrier to interactive use.
- **[#98312 (implied): Azure/generic OAuth issues](https://github.com/openclaw/openclaw/issues/83598)** — Various OAuth refresh bugs (e.g., #83598, #89278) are P1 but have been open for weeks, suggesting auth is a structurally complex area.

---

## Cross-Ecosystem Comparison

# Cross-Project Ecosystem Report: AI Agent Open-Source Landscape
**Date: 2026-08-11 | Data Window: 2026-08-10 → 2026-08-11**

---

## 1. Ecosystem Overview

The personal AI assistant open-source ecosystem is in a **feverish state of activity**, with all major projects logging substantial daily updates. The dominant theme is **reliability hardening** — silent message failures, token-wasting loops, and SQLite corruption are the most common and most passionately discussed bugs across projects. Security is the second major pillar: memory poisoning prevention, MCP auth flows, and channel authorization gaps are driving both community concern and maintainer priorities. The ecosystem is coalescing around **MCP (Model Context Protocol) as the universal integration standard**, with multiple projects shipping OAuth support and v2 migration work this week. Governance is emerging as a challenge: ZeroClaw's RFC process is actively slowing progress, while OpenClaw's maintainer-driven refactoring sprint demonstrates an alternative, more decisive model. The market is clearly shifting from experimentation to **production-grade requirements** — cost budgets, audit logging, and per-agent restrictions are no longer nice-to-haves.

---

## 2. Activity Comparison

| Project | Issues Updated | PRs Updated | Releases | Merged/Closed PRs | Health Score | Key Signal |
|---|---|---|---|---|---|---|
| **OpenClaw** | 500 | 500 | None | 143 | **95** | Consolidation sprint, RC imminent |
| **ZeroClaw** | 50 | 50 | None | 0 | **72** | Review-heavy, security audit phase |
| **Hermes Agent** | 50 | 50 | None | 3 | **70** | Desktop stability, P0 fixes pending |
| **IronClaw** | 50 | 50 | v1.1.1-rc.1 | 19 | **85** | Release candidate shipped |
| **NanoBot** | 5 | 23 | None | 10 | **88** | High throughput, p0 bug sitting |
| **CoPaw** | 40 | 50 | None | 20 | **78** | v2.1.0 prep, ReMe memory rollout |
| **NanoClaw** | 4 | 20 | None | 10 | **80** | Security hardening, refactoring |
| **PicoClaw** | 4 | 9 | None | 7 | **75** | Bug fixes, security boundaries |
| **LobsterAI** | 5 | 20 | None | 20 | **76** | Cowork UI polish, gateway fixes |
| **Moltis** | 3 | 1 | None | 0 | **62** | Apple Container bugs, browser UI stuck |
| **NullClaw** | 1 | 1 | None | 0 | **68** | A2A milestone, steady state |
| **TinyClaw** | 0 | 0 | None | 0 | — | **Inactive** |
| **ZeptoClaw** | 0 | 0 | None | 0 | — | **Inactive** |

**Health Score** is a composite of merge velocity, bug turnaround, activity consistency, and responsiveness to community issues.

---

## 3. OpenClaw's Position

### Advantages vs. Peers

- **Unmatched scale**: With 500 issues/PRs daily and 143 merged/closed PRs in 24 hours, OpenClaw's activity volume is **10–50x larger** than its nearest competitors. This translates to the largest contributor pool, fastest bug-discovery rate, and most rapid feature iteration.
- **Systematic hardening**: The coordinated refactoring sprint by `steipete` (15+ PRs targeting gateway internals, state serialization, security redaction) demonstrates architectural maturity not seen in peers — most projects still do reactive bug-fixing, not proactive refactoring.
- **Multi-channel depth**: Telegram, Slack, Feishu, IRC, Mattermost all have dedicated maintainer attention — peers like NanoClaw and PicoClaw focus on 1–2 channels primarily.
- **Feature breadth**: Advanced topics like native realtime voice (Codex integration), desktop/browser autonomy for cloud workers, and per-spawn tool restrictions show OpenClaw is pushing beyond assistant basics.

### Technical Approach Differences

- **SQLite-first with snapshot repair**: OpenClaw invests significantly in database reliability (concurrent-start corruption fixes, snapshot repair verification for Windows) — peers treat storage as peripheral.
- **Sub-agent architecture**: No other project has a comparable subagent concept with dedicated directories (announce, completion, recovery, registry) and serialization logic. The concept of "memory trust tagging by source" is unique and security-forward.

### Community Size Comparison

| Metric | OpenClaw | Hermes Agent | NanoBot | IronClaw | ZeroClaw |
|---|---|---|---|---|---|
| Daily issue activity | 500 | 50 | 5 | 50 | 50 |
| Daily PR activity | 500 | 50 | 23 | 50 | 50 |
| Comments on top issue | 40 | 11 | 3 | 12 | 23 |
| Contributor diversity | High (multi-maintainer, external PRs) | Moderate (`StanleyStetson` dominant) | Low (`chengyongru` dominant) | Moderate | Moderate (RFC-driven) |
| Governance complexity | Low (maintainer-executes) | Medium | Low | Medium (architecture ratchets) | High (RFC-process heavy) |

**Key insight**: OpenClaw's scale advantage is not just volume — it's the **diversity of maintainership** that enables parallel workstreams (security, channels, features) without blocking dependencies.

---

## 4. Shared Technical Focus Areas

Across projects, seven convergent requirements emerged this week:

### 4.1 Security Hardening Against Prompt Injection (OpenClaw, NanoClaw, PicoClaw, ZeroClaw)
- **Specific needs**: Memory trust tagging by source (OpenClaw #7707), remote prompt envelope normalization (PicoClaw #3297), channel authorization gates (ZeroClaw #9392/#9393), WASI egress policies (ZeroClaw #9395).
- **Pattern**: The ecosystem recognizes that a single untrusted channel or memory injection can compromise an agent. ZeroClaw's fail-open default is being challenged as unacceptable.

### 4.2 MCP Ecosystem Expansion (OpenClaw, NanoBot, NanoClaw, ZeroClaw, IronClaw, CoPaw)
- **Specific needs**: OAuth for remote servers (NanoBot #5316, NanoClaw #3092), v2 SDK migration (NanoBot #5179), custom CA trust (ZeroClaw #9339), arbitrary MCP support (IronClaw #6727), tool-not-found diagnostics (CoPaw #6405).
- **Pattern**: MCP is the de facto integration standard, but reliability (timeouts, nested argument encoding) is immature.

### 4.3 Cost Governance & Budget Controls (OpenClaw, NanoBot, ZeroClaw)
- **Specific needs**: Per-agent cost budgets (OpenClaw #42475), token usage records API (NanoBot #5299), memory consolidation infinite-loop prevention (NanoBot #5325), tool-loop budget exhaustion (IronClaw #7447).
- **Pattern**: As production adoption grows, operators demand financial guardrails — runaway token consumption is the #1 financial risk.

### 4.4 Session Reliability & Delivery Guarantees (OpenClaw, PicoClaw, NanoClaw, CoPaw)
- **Specific needs**: Silent message drops on ID reuse (NanoClaw #3226), duplicate message delivery (OpenClaw #96242/#86519), split-message hangups (PicoClaw #3295), session mutation races (NanoBot #5271), dispatch-routed session management gaps (PicoClaw #3301).
- **Pattern**: Users cannot distinguish "agent ignored me" from infrastructure failure — silent drops are the most trust-eroding bug class.

### 4.5 Desktop/App Stability (Hermes, LobsterAI, IronClaw, CoPaw)
- **Specific needs**: Backend process leaks cross-platform (Hermes #80898/#83482), IPC initialization stalls (LobsterAI #2466), Windows installer corruption (Hermes #83456), PDF/DOCX generation failures (IronClaw #6257/#6869), macOS SQLite crashes (CoPaw #6814).
- **Pattern**: Every project with a desktop surface has lifecycle management issues — this is the unglamorous but critical next frontier.

### 4.6 Agent-to-Agent / Multi-Agent Orchestration (NullClaw, OpenClaw, ZeroClaw)
- **Specific needs**: `a2a_call` client tooling (NullClaw #700), sub-agent routing options (OpenClaw #27445), kanban multi-agent dispatch (Hermes #83376).
- **Pattern**: Users want to chain agents into federated deployments — the ecosystem is moving beyond single-agent to multi-instance topologies.

### 4.7 Configuration Reliability (OpenClaw, PicoClaw, CoPaw, ZeroClaw)
- **Specific needs**: Config schema rejecting documented options (OpenClaw, multiple PRs), model-specific config key collisions (PicoClaw #2132), corrupted config handling (CoPaw #6615), silent wrong defaults (ZeroClaw #9779).
- **Pattern**: Documentation-code drift erodes trust; users expect "set-and-forget" behavior.

---

## 5. Differentiation Analysis

| Dimension | OpenClaw | Hermes Agent | NanoBot | IronClaw | ZeroClaw | CoPaw | NanoClaw / PicoClaw |
|---|---|---|---|---|---|---|---|
| **Primary target** | Power users & operators | Desktop-first users | WebUI-centric developers | Production/enterprise | Security-conscious developers | Chinese-speaking consumer | Enthusiasts/hobbyists |
| **Top architecture highlight** | Sub-agents, multi-channel, gateway | Desktop + TUI + Matrix E2EE | MCP-first, WebSocket mutations | Architecture ratchet governance, Reborn refactor | Security audit, RFC governance | ReMe memory backend | Codebase simplicity |
| **Channel focus** | Telegram, Slack, Feishu, IRC, Mattermost | Matrix, desktop, TUI | WebUI + MCP clients | Slack, Telegram, WebUI | WhatsApp, LINE, Bluesky, Reddit | WebUI, Docker | Telegram |
| **Core differentiator** | **Breadth & velocity** | **Cross-platform reliability** | **Security-hardened by default** | **Enterprise governance** | **Fail-secure philosophy** | **Consumer polish & ReMe** | **Minimalism** |
| **Critical weakness** | Complex integration surface | Desktop lifecycle instability | MCP v2 migration stuck | Document generation fragility | Process overhead slowing delivery | Platform inconsistencies (Docker/Windows/macOS) | Scale-out limitations |
| **Release cadence** | High (RC imminent) | Moderate (v0.20.0 + pending) | Moderate (accumulating) | High (1.1.1-rc shipped) | Low (review-heavy) | Medium (2.1.0 imminent) | Medium |

---

## 6. Community Momentum & Maturity

### Tier 1: High Velocity — Rapidly Iterating (Daily merges, imminent releases)

| Project | Momentum Signal | Release Trajectory |
|---|---|---|
| **OpenClaw** | 143 PRs merged/closed in 24h; 15+ PRs per area | RC imminent (next major) |
| **IronClaw** | 19 PRs merged, v1.1.1-rc.1 shipped today | Stable v1.1.1 imminent |
| **NanoBot** | 10 PRs merged; MCP OAuth shipped in 2 days | Substantial release expected soon |

### Tier 2: Medium Velocity — Refactoring / Hardening Phase

| Project | Momentum Signal | Release Trajectory |
|---|---|---|
| **NanoClaw** | 10 PRs merged; security hardening + architecture refactors | Cumulative minor release |
| **CoPaw** | 20 PRs merged; v2.1.0 release notes in prep | v2.1.0 imminent |
| **LobsterAI** | 20 PRs merged; cowork UI polish | Pre-release sprint |
| **PicoClaw** | 7 PRs merged; security boundaries + i18n | v0.3.2 accumulating |
| **Hermes Agent** | 3 PRs merged; stabilization sprint (P0 fixes pending) | v0.20.1+ batch release |

### Tier 3: Low Velocity — Stabilizing or Stalled

| Project | Momentum Signal | Recommendation |
|---|---|---|
| **ZeroClaw** | 0 merges; 50 PRs awaiting action; RFC process overhead | Unblock review bottleneck |
| **Moltis** | 3 issues filed; 1 PR update (browser UI after 4 months) | Prioritize #1185 + PR #531 |
| **NullClaw** | 1 issue closed (A2A milestone); 1 dependency PR stale | Merge #956, maintain steady state |
| **TinyClaw / ZeptoClaw** | **No activity** | Risk of abandonment |

---

## 7. Trend Signals

### Signal 1: Production-Grade Governance Is the New Frontier
- **Evidence**: Cost budget requests (OpenClaw, NanoBot, Hermes), audit logging fixes (ZeroClaw), per-agent restrictions (OpenClaw, ZeroClaw), SOP cancellation paths (ZeroClaw #9425)
- **Value**: Organizations need financial guardrails, audit trails, and operational controls before trusting agents in production workflows.

### Signal 2: Silent Failures Are the Biggest Trust Eroder
- **Evidence**: Silent message drops (OpenClaw #121058, NanoClaw #3226), silent log loss (NanoClaw #3075), silent config value overwrites (PicoClaw #2132)
- **Value**: Developers should instrument any code path that can fail silently — the community's top frustration is "the agent ignored me" with no diagnostic trail.

### Signal 3: Memory Systems Are the Next Arms Race
- **Evidence**: ReMe rollout (CoPaw), memory trust tagging (OpenClaw #7707), memory consolidation fix (NanoBot #5325), knowledge graph attribution (ZeroClaw #9647)
- **Value**: Memory is the differentiator between "stateless chatbot" and "personal assistant" — but trust, attribution, and cost control around memory are unresolved.

### Signal 4: Multi-Agent and A2A Protocols Are Gaining Traction
- **Evidence**: a2a_call shipped (NullClaw), sub-agent routing options (OpenClaw), kanban multi-agent dispatch (Hermes)
- **Value**: Developers building agent networks need standard interop protocols; A2A is one candidate, MCP is another.

### Signal 5: Cross-Platform Desktop Stability Is the Unmet Promise
- **Evidence**: Process leaks on macOS/Linux (Hermes), installer corruption on Windows (Hermes, CoPaw), PDF/DOCX issues (IronClaw), SQLite crashes (CoPaw)
- **Value**: The "app" experience is broken across the ecosystem — a meaningful differentiator for whoever solves lifecycle management, file generation, and input handling first.

### Signal 6: Security Must Be Fail-Closed, Not Fail-Open
- **Evidence**: ZeroClaw audit findings (line, Bluesky, Reddit gaps), PicoClaw exec default-disable, NanoClaw CSPRNG pairing codes, OpenClaw DM isolation fixes
- **Value**: The community is auditing codebases and finding fundamental authorization gaps. Projects that default to deny will earn trust; projects that default to allow will lose power users.

### Signal 7: The RFC/Governance Overhead Trap
- **Evidence**: ZeroClaw's 3-month RFC bottleneck, Hermes' duplicate issues from slow triage
- **Value**: Open-source governance must scale with velocity. Projects that balance community input with maintainer decisiveness (OpenClaw's model) will outpace consensus-heavy projects.

---

## Bottom Line for Decision Makers

| Decision point | Recommendation |
|---|---|
| **Adopt a primary agent framework** | **OpenClaw** — scale, momentum, and active security work make it the ecosystem bellwether |
| **Need enterprise-grade governance** | **IronClaw** — architecture ratchets, release discipline, explicit escalation paths |
| **Target security-first deployment** | **ZeroClaw** — fail-secure philosophy (but be prepared for slower release cadence) |
| **Build on MCP-heavy stack** | **NanoBot** — fastest MCP feature delivery, though p0 session race must be watched |
| **Desktop-first use case** | **Hermes** — best cross-platform intent, but wait for the pending P0 stabilization batch |
| **Chinese market / consumer polish** | **CoPaw** — strongest UI investment and memory system |

**Watch items for next 2–4 weeks**:
- OpenClaw's release candidate (expected security hardening + cost budgets)
- NanoBot's p0 session race (PR #5271) — potential data loss if not merged
- ZeroClaw's governance reform (streamlining RFC process)
- Hermes Agent's desktop stabilization sprint
- IronClaw's v1.1.1 stable release

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest
**2026-08-11**

---

## 1. Today's Overview

NanoBot is experiencing a period of intense development activity, with **23 PRs updated in the last 24 hours** and **10 merged/closed**, indicating a highly productive sprint. The project shows strong momentum, particularly around **WebUI/UX improvements**, **MCP integration enhancements**, and **security hardening**. A total of **5 issues** were active, with **2 still open**—including a critical memory-consolidation infinite loop bug (now fixed via PR #5325) and a message repetition issue during reasoning. No new releases were published today, but the volume of merged PRs suggests a significant release may be imminent. The maintainer team (dominated by contributor `chengyongru`) is executing a coordinated refactoring effort across WebUI, agent runtime, and MCP layers.

---

## 2. Releases

**No new releases** were published in the last 24 hours. The last release remains the previous stable version. Given the high volume of merged PRs (10 today), users should expect a substantial release in the near future encompassing WebUI refactoring, MCP v2 migration (PR #5179 still open), and the new tabbed workbench feature.

---

## 3. Project Progress

**10 PRs merged/closed today**, advancing several key areas:

### WebUI & UX Refactoring (6 PRs)
- **[#5315](https://github.com/HKUDS/nanobot/pull/5315) [CLOSED]** — Improved UX recovery and empty states: preserves first prompt on failed workspace-scoped chat creation, adds keyboard-focused recovery, reduced auth challenge complexity.
- **[#5317](https://github.com/HKUDS/nanobot/pull/5317) [CLOSED]** — Security: moved all WebUI state-changing mutations from HTTP GET/query-string requests to authenticated WebSocket request/reply frames with allowlisted bridge.
- **[#5318](https://github.com/HKUDS/nanobot/pull/5318) [CLOSED]** — Extracted deterministic event projection helpers for `useNanobotStream`; made reasoning completion time explicit; added shared fixtures.
- **[#5319](https://github.com/HKUDS/nanobot/pull/5319) [CLOSED]** — Replaced reflective runtime state access with explicit `RuntimeControl` protocol; exposes allowlisted, redacted snapshots.
- **[#5321](https://github.com/HKUDS/nanobot/pull/5321) [CLOSED]** — Gateway now owns settings services with serialized atomic read-modify-write operations; WebUI OAuth state moved to gateway-scoped registry.
- **[#5326](https://github.com/HKUDS/nanobot/pull/5326) [OPEN]** — Softened form control focus rings (UI polish).

### MCP & Provider Improvements
- **[#5316](https://github.com/HKUDS/nanobot/pull/5316) [CLOSED]** — **Key feature**: Added browser-based OAuth for remote Streamable HTTP and SSE MCP servers using official MCP SDK; includes Xmind, Notion, and Linear one-click presets (directly addresses issue #5297).
- **[#5314](https://github.com/HKUDS/nanobot/pull/5314) [OPEN]** — Fix: decode nested JSON tool arguments by schema (addresses #5311 for Agnes AI provider).

### Bug Fixes
- **[#5325](https://github.com/HKUDS/nanobot/pull/5325) [CLOSED]** — Fix: reject no-op edits in `edit_file` (prevents Dream memory consolidation infinite loop; directly fixes #5324).
- **[#5310](https://github.com/HKUDS/nanobot/pull/5310) [CLOSED]** — Fix: Weixin forced QR login now performs fully fresh QR flow, skips persisted credentials.

### Performance & Reliability (Open)
- **[#5271](https://github.com/HKUDS/nanobot/pull/5271) [OPEN, p0]** — Prevent stale background task saves from overwriting session data (critical race condition fix).
- **[#5257](https://github.com/HKUDS/nanobot/pull/5257) [OPEN, p2]** — Bound sustained-goal continuation when turn goes idle (prevents token waste).

---

## 4. Community Hot Topics

There were no issues or PRs with extensive comment threads (>3) in the last 24 hours. The most significant discussions:

1. **[Issue #5297](https://github.com/HKUDS/nanobot/issues/5297) — MCP OAuth web authorization (CLOSED, 3 comments)**: User requested OAuth support for MCP servers requiring web authorization (e.g., Xmind). **This was directly addressed by merged PR #5316**, which added browser OAuth with one-click presets. Excellent response time from maintainers (~2 days from report to fix).

2. **[Issue #5324](https://github.com/HKUDS/nanobot/issues/5324) — Dream memory consolidation infinite loop (CLOSED, 2 comments)**: Critical bug where `edit_file` accepting no-op edits caused a 23-minute run consuming 10M+ tokens. **Fixed by PR #5325** within hours. High urgency due to severe token waste.

The community's primary underlying need appears to be **stability and resource cost control**—both top issues relate to preventing runaway resource consumption (tokens, CPU). Additionally, the MCP ecosystem expansion (OAuth support) is a clear priority for power users.

---

## 5. Bugs & Stability

| Severity | Issue | Description | Status |
|----------|-------|-------------|--------|
| **Critical (p0)** | [PR #5271](https://github.com/HKUDS/nanobot/pull/5271) | Stale background task saves overwriting session data when user runs `/new` mid-await | **OPEN** — needs review |
| **High (p1)** | [PR #5320](https://github.com/HKUDS/nanobot/pull/5320) | Docker privilege drop capabilities broken in root bootstrap path; CI now exercises real entrypoint | **OPEN** |
| **High (p1)** | [PR #5317](https://github.com/HKUDS/nanobot/pull/5317) | WebUI mutations were unauthenticated via GET/query-string (security) | **FIXED** (merged) |
| **Critical (tokens)** | [Issue #5324](https://github.com/HKUDS/nanobot/issues/5324) | Dream memory consolidation infinite loop wasting 10M+ tokens | **FIXED** via PR #5325 |
| **Medium** | [Issue #5327](https://github.com/HKUDS/nanobot/issues/5327) | Random message repetition ("Good points, let me investigate") during reasoning | **OPEN** — no comments yet |
| **Medium** | [Issue #5300](https://github.com/HKUDS/nanobot/issues/5300) | MCP connection failure (HTTP 530) causes cancel scope crash, gateway crash, CPU spike | **CLOSED** — verify fix in MCP v2 migration (PR #5179) |
| **Low-Medium** | [Issue #5311](https://github.com/HKUDS/nanobot/issues/5311) | Agnes AI double-encodes nested Object tool arguments as JSON strings | **FIX** available in PR #5314 (open) |

**Critical concern**: The stale-session-overwrite bug (PR #5271) is p0-priority yet remains **unmerged for 5 days**—this warrants immediate maintainer attention as it can cause data loss.

---

## 6. Feature Requests & Roadmap Signals

### Recent User Requests
1. **MCP OAuth web authorization** ([#5297](https://github.com/HKUDS/nanobot/issues/5297)) — **SHIPPED** in PR #5316 (browser OAuth, one-click presets for Xmind/Notion/Linear). likely in next release.
2. **Structured token usage records** ([PR #5299](https://github.com/HKUDS/nanobot/pull/5299), OPEN) — Persists last 50 token-usage accounting records; adds authenticated `GET /api/settings/usage/records` endpoint. Reflects growing user need for cost transparency.

### In-Development Feature Signals
- **[PR #5322](https://github.com/HKUDS/nanobot/pull/5322) — Tabbed pane workbench (OPEN)**: Models topics as Tabs with 1-4 Pane sessions, multiple layouts (columns, rows, grid, main-stack, monocle). This is a significant WebUI power-user feature likely for v-next.
- **[PR #5328](https://github.com/HKUDS/nanobot/pull/5328) — OrcaRouter as named gateway provider (OPEN)**: Adds 150+ models behind single endpoint with zero-trust security.
- **[PR #5288](https://github.com/HKUDS/nanobot/pull/5288) — Agent Plugins with CLI Apps (OPEN)**: Vendor-neutral package boundary for portable skills and MCP runtimes.
- **[PR #5179](https://github.com/HKUDS/nanobot/pull/5179) — MCP SDK v2 migration (OPEN)**: Long-running refactor (11 days) with conflict markers; critical for future MCP ecosystem support.

### Predictions for Next Release
- **MCP OAuth** (PR #5316) — near-certain inclusion
- **No-op edit rejection** (PR #5325) — near-certain inclusion
- **WebUI authenticated mutations** (PR #5317) — near-certain inclusion (security)
- **Tabbed workbench** (PR #5322) — likely but maybe gated behind more testing

---

## 7. User Feedback Summary

**Positive Signals:**
- The maintainer team responds quickly to bugs: #5324 (token-wasting loop) was reported and fixed **within hours**.
- Feature requests (#5297 MCP OAuth) are addressed within **2 days**—excellent community responsiveness.
- Systematic refactoring (settings domain split #5323, runtime control #5319) indicates strong architectural investment.

**Pain Points:**
- **Resource cost leaks** are the #1 user concern: memory consolidation runaway (10M tokens), unbounded goal continuation burning tokens, CPU spikes from MCP crashes.
- **MCP reliability**: Connection failures causing full gateway crashes (#5300) and nested argument encoding incompatibilities with third-party providers (#5311) frustrate power users.
- **WebUI UX issues**: Repeated fixes for focus rings, empty states, recovery flows suggest the UI has rough edges needing iterative polish.
- **Message repetition** during reasoning (#5327) appears to be a new intermittent bug that users find confusing.

**User Sentiment**: Generally positive—users actively contribute detailed bug reports (with root-cause analysis) and expect quick fixes. The project feels responsive, but token-wasting bugs create distrust for heavy users.

---

## 8. Backlog Watch

### Critical Attention Needed
- **[PR #5179](https://github.com/HKUDS/nanobot/pull/5179) — MCP SDK v2 migration (OPEN, 12 days)**: Long-running PR with conflict markers. Held up on priority? This is a foundational refactor that could resolve #5300, #5311 classes of bugs. Needs maintainer decision or dedicated reviewer.

- **[PR #5271](https://github.com/HKUDS/nanobot/pull/5271) — Session data race (OPEN, 5 days, p0)**: Critical data-loss risk, seems stuck despite p0 priority. Requires immediate review.

### Needs Maintainer Response
- **[Issue #5327](https://github.com/HKUDS/nanobot/issues/5327) — Message repetition during reasoning (OPEN, 0 comments)**: Newly reported, no maintainer response yet. Should be triaged.

- **[Issue #5311](https://github.com/HKUDS/nanobot/issues/5311) — Agnes AI argument encoding (OPEN)**: Fix exists in PR #5314 but not merged. Verify and merge.

### Conflict-Stuck PRs
- **[PR #5323](https://github.com/HKUDS/nanobot/pull/5323) — Split settings backend** (conflict with #5321 which was merged) — needs rebase.
- **[PR #5299](https://github.com/HKUDS/nanobot/pull/5299) — Token usage records** (conflict) — needs rebase.

---

## Project Health Summary

| Metric | Status |
|--------|--------|
| Release cadence | ⚠️ No release despite high merge volume |
| Bug fix turnaround | ✅ Excellent (same-day fixes common) |
| Feature delivery | ✅ Fast (OAuth in 2 days from request) |
| Critical bugs open | 🔴 1 p0 (session race), 1 p1 (Docker caps) |
| Community activity | ✅ High (23 PRs, 5 issues in 24h) |
| Technical debt | ⚠️ Multiple merge conflicts on key PRs; long-running MCP v2 migration |

**Overall**: NanoBot is in a strong development cycle with excellent maintainer responsiveness, but the lack of a release cadence and a sitting p0 bug (PR #5271) temper the otherwise positive momentum. The MCP ecosystem expansion (OAuth, v2 migration, third-party providers) is clearly the strategic priority.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-08-11

## Today's Overview

Hermes Agent is in an **intense development phase** with a heavy focus on **bug-fixing and desktop/TUI stability**. The last 24 hours show 50 updated issues (47 open) and 50 updated PRs (44 open), indicating a high level of community engagement and maintainer activity. Notably, there are **zero new releases**, and a significant **spike in new bug reports** (dated 2026-08-10) targeting the desktop app, Matrix plugin, and cron/delivery subsystems. The absence of a release while a large batch of fixes are pending suggests a stabilization sprint is likely in progress. Several high-priority (P0/P1) regressions and a recurring pattern of desktop backend process leaks are commanding maintainer attention.

## Releases

No new releases were published in the last 24 hours. The project remains on version `v0.20.0` (per issue reports).

## Project Progress

In the last 24 hours, **3 PRs were merged/closed** and **6 issues were closed**. Notable progress items include:

- **[PR #83492]** : `fix(desktop): reject malformed grid layouts instead of throwing RangeError` — Aims to fix a desktop hang caused by a React minified error (#520) due to invalid array length on grid layouts.
- **[PR #83202]** : `fix(gateway/desktop): durable row-id addressing for rewind truncation (#82959)` — `StanleyStetson` is implementing stable SQLite `row_id` addressing for rewinds/edits/regenerates, moving away from shifting user-turn ordinals. This is a P0-level fix.
- **[PR #83485]** : `fix(delegation): identify internal completion events` — Adds a stable internal-event envelope for async delegation terminal events to distinguish them from other outputs.
- **[PR #83488]** (Open): `fix(matrix): verify curve25519 and self-signature in device-key checks` — Directly addresses issue #83481, strengthening Matrix device verification beyond raw ed25519 comparison.
- **[Issue #83475]** was **closed**, indicating the fix for the headless Linux browser toolset visibility issue was resolved or deemed invalid.
- **[Issue #83376]** (Kanban multi-agent enhancements tracking) was **closed**, marking the completion of that workstream.

Several long-standing PRs continue to receive updates, including [#57369] (trusted project MCP foundation), [#63667] (kanban dispatcher failure hooks), and [#52508] (Windows install script not exporting venv PATH).

## Community Hot Topics

The most active discussions reveal deep user pain points around core workflows:

1.  **TUI Overlay and Session Management Breakage** (Issue [#69592], 11 comments + 3 reactions, P1) — This is the **highest-signal issue**. A **13-day-old regression** makes `/sessions` and `/models` overlays invisible and unusable when ambient widgets (the default documented dock pattern) are loaded. This effectively kills two core TUI workflows (resuming sessions, switching models). The high comment count shows it's a critical blocker for power users.

2.  **Python 3.14 Compatibility Breakage** (Issue [#58596], 6 comments + 3 reactions) — The `DaemonThreadPoolExecutor` crashes on Python 3.14 due to a removed `_initializer` attribute, breaking **all** concurrent features (delegation, skills hub, memory sync). This is a significant forward-compatibility issue.

3.  **Mistral Reasoning Effort** (Issue [#11243], 6 comments + 8 reactions) — A popular feature request (8👍) to support native `reasoning_effort` injection for Mistral AI's custom provider endpoint, indicating substantial user interest in Mistral models.

4.  **Desktop Custom Endpoints Ignore Active Profile** (Issue [#69451], 5 comments) — A configuration scoping bug where the Electron desktop app's custom endpoints fail to send the `?profile=<name>` parameter, causing them to apply globally instead of to the active profile.

5.  **Matrix Cron Delivery Floods Logs and Disconnects** (Issue [#63395], 5 comments) — A lifecycle issue in the Matrix/E2EE adapter where a successful cron delivery to an encrypted room destabilizes the adapter, causing `database pool has been stopped` errors and disconnects.

Other actively discussed items include cron jobs failing to deliver when created in an api_server session (#69304), and a Windows-related duplicate of the orphaned desktop process issue (#83482).

## Bugs & Stability

The last 24 hours saw a significant influx of bug reports. We rank the **most critical** below:

- **[P0]** **Desktop Session State Corruption** (Issue [#82959] → PR [#83202]) — The root cause of desktop hangs and inability to open sessions; the proposed fix uses durable row-ids. **Fix PR exists** (#83202).
- **[P1]** **Core TUI Workflows Dead** (Issue [#69592]) — A 13-day-old regression where `/sessions` and `/models` overlays fail when ambient widgets are enabled. No definitive fix PR yet.
- **[P2]** **macOS Backend Process Leaks** (Issue [#80898]) — Repeated desktop restarts result in orphaned `hermes serve` processes consuming memory.
- **[P2]** **Linux Desktop Backend Leak** (Issue [#83482]) — Concurrent issue identified on Linux (Deepin/Debian), flagged as a duplicate of #80898. Indicates a **cross-platform pattern** of backend lifecycle mismanagement.
- **[P2]** **Cron Delivery Retries Indefinitely** (Issue [#83484]) — Scheduled jobs delivered to now-incompatible API-server sessions fail permanently and retry infinitely.
- **[P2]** **Windows Installer Corrupts Desktop App** (Issue [#83456], duplicate) — `hermes update` ZIP fallback deleted `Hermes.exe` and failed without rollback; twice reported.
- **[P2]** **Context Compaction Billing Bug** (Issue [#83450]) — On 1M-context models, the compaction threshold (50%) causes the first compaction at 500K tokens, leading to quadratic billing on long sessions. This is a severe cost bug for users on large-context models.
- **[P2]** **Fake Tool Invocations** (Issue [#83379]) — Models occasionally parse real tools as prose text, leading to incorrect behavior.
- **[P3]** **Matrix E2EE Verification Gaps** (Issues [#83481], [#83468]) — Two distinct security/compat issues: 1) Only raw ed25519 keys compared, missing curve25519 and self-signature checks; 2) A `AttributeError` crash when a plain stdlib logger is used instead of mautrix's `TraceLogger`.

Several **duplicate** bug reports (#83482, #83456) suggest a need for maintainers to prioritize cross-platform fixes for the same root causes.

## Feature Requests & Roadmap Signals

The community is signaling strong wants for the next version:

- **Native Mistral `reasoning_effort` Support** (Issue [#11243]): High demand (8👍). Low implementation complexity makes this a likely candidate for the next minor release.
- **Kanban Multi-Agent Enhancements** (Issue [#83376]): While closed as a tracking issue, the PRs it references [#63667] and the underlying work suggest more kanban automation and dispatcher lifecycle features are on the roadmap.
- **Trusted Project MCP Foundation** (PR [#57369]): A large, long-running PR to add project-local `.hermes/` skills/MCP with a trust model. It continues to be updated, indicating active development toward a more security-focused, project-scoped agent.
- **Start New Session from Home Section** (Issue [#83479]): A small UX request to add a "+" button to the desktop chat list, indicating a focus on desktop UI polish.
- **Skill Certification** (Issue/PR [#83487]): A new bundled skill to verify/certify third-party skills via "SkillSeal" API — suggests community-driven trust and governance features are being explored.

**Prediction**: The next release will likely batch the many pending fixes (P0/P1) for desktop stability, TUI overlays, and the Python 3.14 compatibility. Feature additions will prioritize **Mistral reasoning** and the **trusted MCP foundation** work.

## User Feedback Summary

Across the bug reports and discussions, users are consistently feeling friction in these areas:

- **Desktop Experience is a Pain Point**: The orphaned backend processes on macOS (#80898) and Linux (#83482), the non-responsive HUD controls (#83017, #83473, #83467), and the renderer corruption on Wayland (#83359) paint a picture of a desktop app that is not yet production-grade in terms of lifecycle and input handling. Users are reporting crashes, hangs, and USB-related input wedges.
- **Configuration is Fragile**: Bugs like `plugins.enabled` being written as an unquoted string silently unmounting all plugins (#83308), or desktop endpoints ignoring the active profile (#69451), indicate that configuration parsing and scoping are sources of subtle, hard-to-debug failures.
- **Session Reliability is Core**: Users are reporting new session creation on every top-level Google Chat message (#83353), silent failures in session title generation (#82816), and the inability to see/resume sessions (#69592). This suggests an ongoing concern about the agent's memory across platforms.
- **Security/Verification Gaps**: Issues with OAuth token refresh dropping `subscriptionType` on Claude Code (#83338), Matrix verification gaps (#83481), and credential file rewrites indicate a need for more robust identity handling.
- **Cost Overruns**: The quadratic billing issue on large-context models (#83450) is a highly impactful, real-world financial pain point for users on 1M-token models.

## Backlog Watch

Long-running and important issues/PRs needing maintainer attention beyond the daily flood:

1.  **Issue [#58596]** (Python 3.14 `DaemonThreadPoolExecutor` crash) — An open, critical compatibility bug from July 5. As Python 3.14 adoption grows, this will become an absolute blocker for users on that version. Needs a fix or a compatibility strategy.
2.  **Issue [#11243]** (Mistral `reasoning_effort`) — A high-reaction feature request from April; maintainers likely know, but formalizing the plan would be welcome.
3.  **PR [#57369]** (Trusted project MCP foundation) — A massive, complex PR open since July 2. The extended review cycle may be a risk; the community needs a decision to merge, refine, or break it down into smaller, more reviewable pieces.
4.  **PR [#52508]** (Windows install PATH) — An important fix for Windows users from June 25. The long duration and cross-platform implications (Windows-only installer bug) warrant a faster resolution, as it directly affects developer workflows.
5.  **Issue [#63395]** (Matrix cron flood/disconnect) — An unresolved, complex Matrix E2EE/cron issue from July 12. It is affecting a specific set of users and touches on the difficult intersection of stateful channels and scheduled workflows.

The continued influx of duplicate issues (#83482, #83456) for desktop process leaks suggests that the existing, older issue (#80898) is not being widely surfaced or that the fix is taking too long, which can cause user frustration and duplicate triage workload.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest — 2026-08-11

## 1. Today's Overview

PicoClaw shows a steady and healthy development cadence with 9 PRs updated in the last 24 hours (7 merged/closed, 2 still open) and 4 issues touched (2 open, 2 closed). The project appears to be in a **consolidation phase**, focusing on bug fixes, security hardening, and platform integration polish rather than headline features. Notably, the merged PRs span multiple domains—security boundaries, Telegram rich message rendering, channel message splitting, i18n improvements, and dependency hygiene—indicating broad maintainer attention. However, all open issues and PRs have been marked as `[stale]`, suggesting that while work is progressing, some items have been lingering without fresh maintainer engagement. The absence of new releases in this window means users are still on v0.3.1, with improvements accumulating for the next cut.

---

## 2. Releases

**No new releases** were published in the last 24 hours. The latest available version remains **v0.3.1 (`2cf030d2`)**. Users should monitor the v0.3.2 milestone as the several merged fixes below (particularly the **exec allow-list bug** and **split-message hang**) are strong candidates for inclusion.

---

## 3. Project Progress

Seven PRs were merged/closed in the last 24 hours, representing a productive day across several areas:

- **[PR #3297 — fix(security): harden remote prompt and exec boundaries](https://github.com/sipeed/picoclaw/pull/3297)** — A significant security hardening effort. Remote sender/chat metadata are now kept in a normalized "user-role envelope" rather than directly injected into provider system instructions. Remote exec defaults to **disabled**, requires per-call approval when enabled, and enforces origin policy again at execution time. Configs are migrated to **schema v4**. This is a meaningful defense-in-depth improvement for multi-user deployments.
- **[PR #3327 — feat(telegram): render tables with native rich messages](https://github.com/sipeed/picoclaw/pull/3327)** — Telegram responses with GFM or HTML tables now render as native Bot API rich messages instead of being flattened into monospaced code blocks. Improves readability for data-heavy outputs.
- **[PR #3295 — fix(channels): prevent SplitMessage hang on oversized fence headers](https://github.com/sipeed/picoclaw/pull/3295)** — Fixes an infinite-loop/hang condition in channel message splitting when an opening code-fence info string exceeds `maxLen`. Adds regression tests.
- **[PR #3296 — i18n: complete Czech code wrap labels](https://github.com/sipeed/picoclaw/pull/3296)** — Localization completeness for Czech.
- **[PR #3326 — fix(web): remove duplicate pnpm lock entries](https://github.com/sipeed/picoclaw/pull/3326)** — Removes duplicate `semver@7.8.5` mappings from the web frontend lockfile that caused `pnpm install --frozen-lockfile` to fail with `ERR_PNPM_BROKEN_LOCKFILE`. Unblocks CI for the web frontend.
- **[PR #2132 — feat(config): support model-specific max_tokens and fix config key co…](https://github.com/sipeed/picoclaw/pull/2132)** — Closed from late March. Decouples the model lookup key from the runtime model ID, fixing a subtle config bug where `Defaults.ModelName` was being overwritten by the provider's technical ID, breaking model-specific config retrieval.
- **[PR #1547 — fix: merge PR #1466 #1465](https://github.com/sipeed/picoclaw/pull/1547)** — Older merge-request cleanup, closed.

---

## 4. Community Hot Topics

**[Issue #3301 — `/clear` and session auto-compression break in dispatch-routed chats](https://github.com/sipeed/picoclaw/issues/3301)** *(3 comments)*
This is the most-discussed open issue. When a chat is routed to a non-default agent via dispatch rules, session management commands (`/clear`) and auto-compression fail. This is a functional gap in a headline feature (multi-agent routing) and is being actively tracked.

**[PR #3314 — Fix: agent not able to execute shell command added to customAllowPatterns](https://github.com/sipeed/picoclaw/pull/3314)** *(open)*
A community-contributed fix for a critical, user-facing bug: commands like `git push` blocked despite being allow-listed via `customAllowPatterns`. The root cause—default deny patterns taking precedence over custom allow patterns in `guardCommand`—is surprising and effectively means the documented configuration doesn't work. This PR has high visibility because it addresses a **security-adjacent functionality bug** that many users will have hit.

**[Issue #3311 — Repeated identical tool failure loops silently to max_tool_iterations](https://github.com/sipeed/picoclaw/issues/3311)** *(1 comment)*
Reported by `lucapette` who also authored the fix PR. Describes a terrible user experience: agent "spins" for minutes calling a failing tool repetitively, never answering the user. This is a **reliability concern** for production use (observed over Telegram).

---

## 5. Bugs & Stability

| Severity | Issue | Status | Fix PR? |
|---|---|---|---|
| 🔴 **High** — User never receives an answer; agent silently loops up to `max_tool_iterations` on repeated identical tool failure | [#3311](https://github.com/sipeed/picoclaw/issues/3311) | Open (stale) | ✅ [#3312](https://github.com/sipeed/picoclaw/pull/3312) (open) |
| 🔴 **High** — `customAllowPatterns` not respected; allow-listed commands (e.g., `git push`) blocked by default deny precedence | [#3314 PR](https://github.com/sipeed/picoclaw/pull/3314) | Open PR (fix) | — |
| 🟠 **Medium** — Session management (`/clear`, auto-compression) broken in dispatch-routed chats | [#3301](https://github.com/sipeed/picoclaw/issues/3301) | Open (stale) | None yet |
| ✅ **Fixed (merged)** — `SplitMessage` infinite hang on oversized fence headers | [#3295](https://github.com/sipeed/picoclaw/pull/3295) | Merged | Same |
| ✅ **Fixed (merged)** — `pnpm-lock` broken for web frontend | [#3326](https://github.com/sipeed/picoclaw/pull/3326) | Merged | Same |

The two **high-severity** items (tool-failure loop, allow-list bug) both have candidate fixes in open PRs (`#3312`, `#3314`). These should be prioritized for review and merge.

---

## 6. Feature Requests & Roadmap Signals

- **[Issue #3298 — AI Router OpenAI-compatible provider preset](https://github.com/sipeed/picoclaw/issues/3298)** *(closed)* — Request for a named provider preset for AI Router (alongside the generic `openai` path). Given the project already supports the generic route, this is a **low-effort, high-convenience** addition likely to land soon.
- **[PR #3327 — Native rich table rendering in Telegram](https://github.com/sipeed/picoclaw/pull/3327)** *(merged)* — Indicates an ongoing investment in Telegram integration quality beyond basic messaging.
- **[PR #2132 — Model-specific `max_tokens` overrides](https://github.com/sipeed/picoclaw/pull/2132)** *(merged)* — Suggests future direction toward more granular per-model/provider configuration control.

**Prediction:** The next minor release is likely to include the security hardening (`#3297`), the two bug fixes currently in open PRs (`#3312`, `#3314`), and possibly the AI Router preset if maintainers accept the contribution.

---

## 7. User Feedback Summary

**Pain Points:**
- **Reliability in production:** Users are running PicoClaw in production over Telegram and hitting scenarios where the agent "never answers" (`#3311`) — a serious trust-breaker for an assistant product.
- **Config surprises:** The `customAllowPatterns` bug (`#3314`) means documented configuration is silently ignored, requiring deep debugging to discover. This type of issue erodes user confidence.
- **Multi-agent routing incomplete:** Dispatch-routed chats miss essential session-management behavior (`#3301`), making a headline feature feel half-finished.

**Satisfaction Signals:**
- Community members are actively contributing fixes (Czech i18n, security hardening, lockfile fixes), indicating a healthy contributor ecosystem.
- The rapid merge of the Telegram table rendering feature suggests maintainers are responsive to UX improvements.

---

## 8. Backlog Watch

These items have been open for a while and may need maintainer triage:

- **[Issue #3301 — `/clear` and auto-compression in dispatch-routed chats](https://github.com/sipeed/picoclaw/issues/3301)** — Open since July 29, 3 comments, no fix PR. Core feature gap, deserves attention.
- **[PR #3314 — `customAllowPatterns` fix](https://github.com/sipeed/picoclaw/pull/3314)** — Open since August 3, 1 week without maintainer response. High user impact; should be reviewed promptly.
- **[PR #3312 — Stop turn on repeated tool failure](https://github.com/sipeed/picoclaw/pull/3312)** — Open since August 2. Directly addresses the #3311 reliability issue; should be paired with the issue for closure.
- **[PR #1547 — Various PR merges from March](https://github.com/sipeed/picoclaw/pull/1547)** *(closed today)* — This was cleaned up, which is good. However, its age suggests the maintainers may have a backlog of older PRs needing the same attention.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest
**Date: 2026-08-11**

---

## 1. Today's Overview

NanoClaw shows **high development activity** with 20 PRs updated in the last 24 hours (10 merged/closed, 10 open) and 4 active issues. The project is in a **maintenance and hardening phase**, with a strong focus on security fixes (CSPRNG pairing codes, permission hardening), message reliability (deduplication, ID-reuse handling), and architectural refactoring (module lifecycle hooks, migration registries, host file-access abstractions). Core-team members are driving substantial feature work around Agent Plugins and remote MCP server support, while community contributors are actively submitting guidelines-compliant fixes and refactors. No new releases were published today, suggesting the team is consolidating changes before a version bump.

---

## 2. Releases

**No new releases** were published in the last 24 hours.

---

## 3. Project Progress

**10 PRs merged/closed today**, including:

- **[#3228 — fix: deduplicate turn-scoped chat delivery](https://github.com/nanocoai/nanoclaw/pull/3228)** — Fixes duplicate message delivery within a single turn, improving chat consistency.
- **[#3222 — feat(permissions): add opt-in privacy-safe DM logs](https://github.com/nanocoai/nanoclaw/pull/3222)** — Adds a `privacySafeLogs` setting that omits user IDs, handles, and raw adapter errors while retaining non-identifying context.
- **[#3216 — docs(hardened-image): note install_packages covers apt/npm only](https://github.com/nanocoai/nanoclaw/pull/3216)** — Documents an existing limitation in the hardened-image guide.
- **[#3215 — fix(permissions): redact DM resolution logs](https://github.com/nanocoai/nanoclaw/pull/3215)** — Improves privacy by redacting sensitive data from DM resolution logs.
- **[#3186 — refactor: add host seams for skill-owned capabilities](https://github.com/nanocoai/nanoclaw/pull/3186)** — Enables skills to declare and own host capabilities.
- **[#3213 — refactor(channels): register question renderers](https://github.com/nanocoai/nanoclaw/pull/3213)** — Unifies question rendering across channels.
- **[#3214 — refactor(host): unify module lifecycle hooks](https://github.com/nanocoai/nanoclaw/pull/3214)** — Consolidates module lifecycle management.
- **[#3212 — refactor(db): add module migration registry](https://github.com/nanocoai/nanoclaw/pull/3212)** — Structured approach to database migrations.
- **[#3211 — docs(skills): define single-responsibility integration rule](https://github.com/nanocoai/nanoclaw/pull/3211)** — Establishes integration guidelines for skills.
- **[#3219 — Telegram and container env](https://github.com/nanocoai/nanoclaw/pull/3219)** — Contribution addressing Telegram and container environment concerns.

**Key themes:** A deliberate push toward better **privacy defaults**, **codebase hygiene/refactoring**, and **documentation of known limitations**.

---

## 4. Community Hot Topics

- **[Issue #3226 — Inbound messages silently dropped when a platform reuses a message id](https://github.com/nanocoai/nanoclaw/issues/3226)** ⭐ *(New, high urgency)* — Reported by `dweekly`; inbound messages can vanish silently when a platform reuses a message ID, making it indistinguishable from "the agent ignored me." This is the most user-visible reliability bug reported this week. A fix PR (#3224) already exists.

- **[Issue #3075 — Silent log loss + inbound duplicate-insert errors after long uptime](https://github.com/nanocoai/nanoclaw/issues/3075)** — Open for nearly a month (updated yesterday) with 1 comment. Reports silent log loss and duplicate-insert errors in Matrix after long uptimes; includes a systemd unit gap. Needs maintainer attention.

- **[PR #3220 — feat!: agent templates become Agent Plugins 1.0.0 directories](https://github.com/nanocoai/nanoclaw/pull/3220)** *(Core-team, breaking change)* — A format migration for the template feature with security hardening (symlink/caps/secret). This is a breaking-change PR; community users relying on templates should watch this carefully.

**Underlying needs:** Users are hitting **reliability walls** — messages that disappear silently (ID reuse, duplicate-insert) — and **security hardening** (predictable pairing codes, permissive file permissions). The project is responding with fixes but quiet-drop behavior is a trust issue.

---

## 5. Bugs & Stability

| Severity | Issue | Status | Notes |
|----------|-------|--------|-------|
| **High** | [#3226 — Inbound messages silently dropped on platform message-ID reuse](https://github.com/nanocoai/nanoclaw/issues/3226) | Open | Fix PR [#3224](https://github.com/nanocoai/nanoclaw/pull/3224) open — preserves inbound messages across ID reuse |
| **High** | [#3075 — Silent log loss + duplicate-insert errors after long uptime; no systemd unit](https://github.com/nanocoai/nanoclaw/issues/3075) | Open (since 2026-07-17) | Long-standing; needs maintainer diagnosis |
| **Medium** | [#3223 — Scheduled-task errors become unroutable silent drops](https://github.com/nanocoai/nanoclaw/issues/3223) | Open | Operator never learns the task failed; error message is unroutable |
| **Security** | [PR #3229 — Pairing codes generated with Math.random()](https://github.com/nanocoai/nanoclaw/pull/3229) | Open (fix PR) | CSPRNG swap to `crypto.randomInt`, widens code space from 4 to 5 digits |
| **Security** | [PR #3225 — Harden Telegram pairing code storage permissions](https://github.com/nanocoai/nanoclaw/pull/3225) | Open (fix PR) | Enforces owner-only permissions on pairing directory/store; repairs existing installs |

**Assessment:** The project discovered the same underlying class of bugs in multiple places — **silent message drops** and **weak pairing-code entropy**. Fixes are already in PR form, which is a sign of a healthy, responsive maintenance culture. #3075 is the oldest unsolved reliability bug.

---

## 6. Feature Requests & Roadmap Signals

- **Remote Streamable HTTP MCP servers** — PRs [#3092](https://github.com/nanocoai/nanoclaw/pull/3092) (engine + Claude provider) and [#3221](https://github.com/nanocoai/nanoclaw/pull/3221) (codex/opencode support) are both open and active. This is a **multi-provider infrastructure feature** likely to land in the next minor/major release.

- **Agent Plugins 1.0.0 (template migration)** — PR [#3220](https://github.com/nanocoai/nanoclaw/pull/3220) converts agent templates into first-class plugin directories. Likely a **next-version headline feature**.

- **`--stdin-json` input mode for CLI** — PR [#3218](https://github.com/nanocoai/nanoclaw/pull/3218) adds bounded structured JSON input to both host and container `ncl` clients. Useful for scripting/automation; small but valuable.

- **`install_packages` pip channel** — [Issue #3217](https://github.com/nanocoai/nanoclaw/issues/3217) asks for a Python package channel. Currently only `packages_apt` and `packages_npm` exist. This is a **blocker for hardened-image adoption** among Python-dependent users; likely to be addressed soon given the related docs PR (#3216) already merged.

- **Setup wizard first-agent stamping** — PR [#2909](https://github.com/nanocoai/nanoclaw/pull/2909) (core-team, open since July) adds template-based first-agent creation in the setup flow. Could land in the next version.

**Prediction:** The next release will likely include **remote MCP server support**, **Agent Plugin 1.0.0**, and **Telegram security hardening**.

---

## 7. User Feedback Summary

**Pain points:**

- **Silent message loss** — Users cannot distinguish "agent ignored me" from a platform-side ID collision (Issue #3226). This erodes trust in the assistant.
- **Operational blindness** — Scheduled-task failures produce unroutable errors, so operators never learn a task failed (Issue #3223).
- **Hindered adoption** — Lack of a pip channel in `install_packages` blocks hardened-image adoption for Python-centric installs (Issue #3217). The docs PR (#3216) clarifying this limitation was merged, suggesting the team acknowledges the gap.
- **Long-uptime degradation** — Silent log loss and duplicate-insert errors after long uptime (Issue #3075) suggests a resource-leak or state-corruption problem that has not yet been root-caused.
- **Lack of systemd unit** — No systemd unit is installed by default, complicating production deployments (Issue #3075).

**Satisfaction signals:**

- **Core-team responsiveness** is high — issues filed today already have fix PRs (e.g., #3226 → #3224).
- **Privacy-conscious users** are being heard: DM log redaction (#3215), privacy-safe logs (#3222), and pairing-code hardening (#3229) all shipped or are in review.
- **Refactoring culture is strong** — many clean, single-purpose refactor PRs merged (module lifecycle, migration registry, host seams), suggesting a maintainable codebase.

---

## 8. Backlog Watch

- **[Issue #3075 — Silent log loss + duplicate-insert errors after long uptime](https://github.com/nanocoai/nanoclaw/issues/3075)** — Open since **2026-07-17** (~1 month). No maintainer response visible; only 1 comment. This is the **longest-standing active issue** combining two reliability bugs plus a missing systemd unit. Needs attention.

- **[PR #2909 — feat(setup): template setup flow in the wizard and first-agent stamping](https://github.com/nanocoai/nanoclaw/pull/2909)** — Open since **2026-07-02** (core-team). Large feature (part 2 of 2); likely blocked by #3220 (Agent Plugins migration). Watch for rebase/conflict risk.

- **[Issue #3217 — install_packages has no pip channel](https://github.com/nanocoai/nanoclaw/issues/3217)** — Open since 2026-08-09; docs PR clarifying the gap merged, but no feature work scheduled yet. Python-dependent users are blocked.

- **[PR #3193 — fix(telegram): update Chat SDK for rich messages](https://github.com/nanocoai/nanoclaw/pull/3193)** — Open since 2026-08-06, updated today. No comments from maintainers yet. A dependency-upgrade fix; may need a maintainer review pass.

---

*Overall health: **Active and healthy**. The project is shipping security and reliability fixes promptly, has an engaged core team plus community contributors, and is investing in both architecture (refactors) and new capabilities (MCP, Agent Plugins). The main watch items are the aging #3075 and the dependency-review gap for #3193.*

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

# NullClaw Project Digest — 2026-08-11

## 1. Today's Overview

NullClaw showed light but meaningful activity over the past 24 hours. One long-standing issue (#700) — the request for an `a2a_call` client tool enabling agent-to-agent communication — was officially closed, marking a significant milestone in the project's A2A (Agent-to-Agent) protocol story. Simultaneously, a single pull request (#956) received an update, though it remains open pending review of a routine Alpine dependency bump. There were no new releases, and overall activity is consistent with a project in a steady-state maintenance phase with occasional feature closures. The project health appears stable, with no alarming signals of abandonment or critical regressions.

## 2. Releases

No new releases were published in the last 24 hours. The most recent release information is not available in this data window. No migration notes, breaking changes, or version-specific announcements to report.

## 3. Project Progress

**No PRs were merged or closed in the last 24 hours.** The only PR activity was an update to an existing open dependency bump:

- **[PR #956 — ci(deps): bump alpine from 3.23 to 3.24 in the docker-images group](https://github.com/nullclaw/nullclaw/pull/956)** (open, created 2026-06-15, updated 2026-08-10): A routine dependency update for the Docker image base, keeping the container runtime current. This is a low-risk, housekeeping change still awaiting review.

The notable progress signal is the **closure of Issue #700**, which represents completed work likely merged in a prior period or addressed through other means (see below for details).

## 4. Community Hot Topics

The single most significant community item this window is:

- **[Issue #700 — Add a2a_call client tool for calling remote agents](https://github.com/nullclaw/nullclaw/issues/700)** (closed, 1 comment, 1 👍, created 2026-03-23, updated 2026-08-10): This issue was opened by user **georgeglarson**, who described building an `a2a_call` tool to bridge the gap between nullclaw's server-side A2A protocol implementation (v0.3.0) and the lack of a client-side equivalent. The use case involves running multiple nullclaw instances (a public-facing doorman and a private personal agent) and enabling them to communicate via `message/send` JSON-RPC requests. The closure of this issue after nearly five months suggests the tool has been accepted or implemented, fulfilling a real distributed-agent orchestration need.

**Underlying need analysis:** This issue highlights a clear demand for **multi-agent interoperability** — users want to chain nullclaw instances into federated or hierarchical setups. The project's roadmap should continue prioritizing A2A protocol maturity on both client and server sides.

## 5. Bugs & Stability

**No bugs, crashes, or regressions were reported in the last 24 hours.** The only PR (#956) is a dependency bump, not a fix. The project appears to be in a stable state with no new stability concerns raised by the community.

## 6. Feature Requests & Roadmap Signals

While no new feature requests were filed in the last 24 hours, the **closure of Issue #700** sends a clear signal: the project has officially embraced **client-side A2A capabilities**, enabling nullclaw instances to act as both servers and clients in a distributed agent network.

**Prediction for next version:** Based on this closure and the project's trajectory, the next release is likely to include:
- An official `a2a_call` client tool (or its integration into the core agent toolkit) enabling `message/send` communication with remote agents.
- Expansion of the A2A v0.3.0 protocol surface to support more JSON-RPC methods beyond the server-side implementation.
- Possible documentation updates for multi-instance and multi-agent deployment patterns.

## 7. User Feedback Summary

**Real user pain point (from Issue #700):** The core friction identified by the community is **the asymmetry in A2A support** — nullclaw could *serve* the protocol but not *consume* it. Users running multiple instances had to resort to building their own client tooling, indicating a gap in the default feature set. The single 👍 reaction and the creator's detailed use case suggest genuine (if modest) demand from power users, not a broad-base request.

**Satisfaction signal:** The fact that georgeglarson took the time to build and submit the tool (rather than abandoning nullclaw for an alternative) is a positive retention signal. The closure of the issue should yield a satisfaction boost among multi-instance users.

## 8. Backlog Watch

- **[PR #956 — alpine 3.23 → 3.24 dependency bump](https://github.com/nullclaw/nullclaw/pull/956)** (open since 2026-06-15, ~2 months): This routine security/maintenance update has been languishing unreviewed for two months. While low-risk, dependency drift can accumulate security vulnerabilities over time. **Maintainers should prioritize review and merge.**

**No long-unanswered high-priority issues** were identified in the current data window. The project's issue backlog appears well-managed, with no critical items left unaddressed for extended periods.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest
**2026-08-11** | Data window: 2026-08-10 – 2026-08-11

---

## 1. Today's Overview

IronClaw is in a high-velocity delivery phase, with **50 issues and 50 PRs updated in the last 24 hours** (roughly half in each state). The project shipped a **release candidate for v1.1.1** (urgent patch for channel delivery, MCP compatibility, WebUI streaming, and upgrade safety), while active development focuses on **Reborn durable-state refactoring, Telegram linked-device support, extension visibility, and multi-surface reliability fixes**. The architecture governance program remains active — multiple audit-driven issues closed this week targeting coupling, budget gates, and CI correctness. The pace suggests a **stable release imminent (v1.1.1)**, with v1.3.0 workload already accumulating (Design System epic, channel-first onboarding, extensions vNext).

---

## 2. Releases

### ironclaw-v1.1.1-rc.1 (2026-08-10)
**Patch candidate for the 1.1 line.** Focus areas:
- **Channel delivery & pairing** — fixes for Slack/Telegram auth and delivery flows
- **IronHub/custom MCP compatibility** — validation and runtime fixes around attachments and protocol compliance
- **WebUI streaming stability** — likely addressing PDF/DOCX generation and attachment type validation
- **Durable retrieval** — hardening of state/retrieval paths
- **Safe upgrades from both supported stable predecessors** — explicit migration guidance included

**Migration note:** Upgrade path from 1.0.0 requires **stopping all writers** before upgrade.

**Link:** [Release v1.1.1-rc.1](https://github.com/nearai/ironclaw/releases)

---

## 3. Project Progress

### Merged/Closed PRs (19 total in window)

| PR | Type | Summary |
|---|---|---|
| [#7446](https://github.com/nearai/ironclaw/pull/7446) | feat | **Rich working indicator** — varied copy, reactions, failure states, progress nudges for Slack/Telegram channels |
| [#7445](https://github.com/nearai/ironclaw/pull/7445) | fix | **Shared-channel mention gating** — bot now responds only on explicit @mention (fixes triple-DM/duplicate-reply bug) |

### Key Closed Issues (advancing features)
- **#7145** — WS2: extension_host → loops re-layer (sizing corrected from "file count" to "four-port residue")
- **#7147** — Two shrink-only architecture ratchets carry untracked slack on main (fixed)
- **#7151** — Composition mass gate poisoning by feature inflow (fixed — share-based budget now denominator-correct)
- **#7149** — Same-layer coupling default guard added (68 live edges now tracked)
- **#7150** — D-E vendor sanction pin implemented (vendor-name census exists)
- **#7036** — Changed-coverage gate now runs on ordinary PRs (verdict no longer delayed to merge queue)
- **#6733** — `/model` and `/status` commands shipped across Telegram, Slack, and WebUI
- **#6941** — Skills epic (self-create/find/choose/use) delivered for 1.1.0; measured subset of #6565
- **#6727** — Custom/arbitrary MCP server support added (closes major v1 gap)
- **#6945** — ironclaw_hooks cross-run isolation regression test coverage (previously claimed but nonexistent)
- **#6492** — Extension assets/surfaces grouped by owning service
- **#6483/#6484/#6485** — Telegram completeness, canonical messaging ops, channel-aware canonical conversations epics closed

### Notable Open PRs (in-flight)
- [#7471](https://github.com/nearai/ironclaw/pull/7471) — **Lease expiry recovery + heartbeat pool isolation** (fixes hosted-run deaths)
- [#7456](https://github.com/nearai/ironclaw/pull/7456) — **Profile-agnostic durable storage** (major Reborn refactor)
- [#7464](https://github.com/nearai/ironclaw/pull/7464) — **Telegram linked-device auth** (MTProto device linking)
- [#7468/#7469](https://github.com/nearai/ironclaw/pull/7468) — Per-token logprobs sidecar → envelope confidence aggregates (Trace Commons alignment)
- [#7410](https://github.com/nearai/ironclaw/pull/7410) — **Tool-search fair discovery** — complete signatures, semantic namespace summaries

---

## 4. Community Hot Topics

| Issue | Score | Topic |
|---|---|---|
| [#7137](https://github.com/nearai/ironclaw/issues/7137) | 12 💬 | **live-canary artifact bloat (700MB–1.5GB per shard)** — CI storage quota burn; PR #7466 provides fix |
| [#7145](https://github.com/nearai/ironclaw/issues/7145) | 4 💬 | **extension_host → loops re-layer** sizing methodology (closed) |
| [#6257](https://github.com/nearai/ironclaw/issues/6257) | 3 💬 | **PDF generation "Invalid value (attachments.mime_type)"** — regression suspect |
| [#7147](https://github.com/nearai/ironclaw/issues/7147) | 3 💬 | **Architecture ratchet slack** — three PRs held three different baselines (closed) |
| [#5882](https://github.com/nearai/ironclaw/issues/5882) | 3 💬 | **Slack reconnect auth-breakage** — requires extension reinstall |

**Analysis:** The most active topic is **CI infra efficiency** (#7137) — an internal engineering concern, suggesting the team is aware of scale costs. The **PDF MIME type** issue (#6257) remains open and is a **customer-facing regression** with no fix PR yet. The Slack reconnect bug (#5882) has active discussion and appears related to the release-candidate's pairing/delivery focus.

---

## 5. Bugs & Stability

### Active/Unresolved Bugs (ranked by severity)

| Sev | Issue | Description | Fix status |
|---|---|---|---|
| **High** | [#6257](https://github.com/nearai/ironclaw/issues/6257) | PDF generation fails with `Invalid value (attachments.mime_type)` | **No fix PR open** — likely linked to attachment validation |
| **High** | [#7447](https://github.com/nearai/ironclaw/issues/7447) | Agent fails after calling too many tools — **fetch-retry loop** burns budget instead of using `result_read` pagination; 4 near-duplicate rounds observed | No fix yet; likely needs tool-loop detection |
| **Med** | [#6869](https://github.com/nearai/ironclaw/issues/6869) | Generated DOCX files **corrupted/unreadable in Word** | No fix seen — Word-interop validation gap |
| **Med** | [#5882](https://github.com/nearai/ironclaw/issues/5882) | Repeated Slack reconnects break auth flow → "Waiting for Slack..." forever; reinstall required | Closed today — related to #7145/#6882 family |
| **Low** | [#3762](https://github.com/nearai/ironclaw/issues/3762) | Editing AGENTS.md does not update system prompt for current/future conversations | Open since May 18 — long-standing UX gap |

### Fixes Shipped/In-Flight (this window)
- **Lease-expiry recovery** — PR #7471 (heartbeat pool isolation, hosted runs)
- **Unprojected thread-index listability** — PR #7470 (sidebar misses threads without projection metadata)
- **CLI workspace overlap** — PR #7455 (fixes `cwd` overlapping skill roots)
- **Memory search snippet bounds** — PR #7436 (8 KiB per result cap, 16-update dep bump included)
- **Shared-channel invocation** — PR #7445 (mention-only, prevents triple-DM)

---

## 6. Feature Requests & Roadmap Signals

### Strong Signals (likely in v1.3.0/v1.4.0)
- **#7046** — Configure all tools/channels/extensions from AI chat as Admin ([issue](https://github.com/nearai/ironclaw/issues/7046))
- **#7038** — Storybook + AI-first Design System (theming, IA, tokens) ([issue](https://github.com/nearai/ironclaw/issues/7038))
- **#7354** — Extensions vNext: Web Push, Rich Messaging, Telegram User Sessions, Signal (due 2026-08-14) ([issue](https://github.com/nearai/ironclaw/issues/7354))
- **#7044** — Channel-first onboarding (v1.4.0) — blank-slate problem ([issue](https://github.com/nearai/ironclaw/issues/7044))

### Watch Items
- **#7467** — Reborn durable state profile-agnostic migration (epic opened; PR #7456 in-flight)
- **#7465** — "Company Brain FDE" — first-day epic, no detail yet; watch for scoping
- **#7447** — Tool-call budget exhaustion — likely spawns a loop-detection or pagination-preference feature

### Predicted for next minor release (v1.1.1 stable → v1.2.0)
- Telegram linked devices (PR #7464 merged post-RC)
- Tool-search fair discovery (PR #7410)
- Per-token logprobs sidecar (opt-in, observability feature)
- Profile-agnostic storage (PR #7456) — will be embedded in v1.3.0 epic

---

## 7. User Feedback Summary

### Verified Pain Points
- **Document generation is fragile** — PDF and DOCX both fail in different ways (#6257, #6869). Users explicitly note that ChatGPT and Claude "can do this easily."
- **Slack authentication is brittle** — repeated reconnects break the flow entirely (#5882). Users need to remove/reinstall extensions — a poor first-class experience.
- **AGENTS.md edits don't take effect** — a core trust-breaker for users who expect identity-file changes to be live immediately (#3762).
- **Agent efficiency is a blocker** — tool-call loops exhaust budget without completing tasks (#7447). Users need pagination preference and loop detection.
- **Onboarding is blank** — new users don't know what to do after first load (#7044).

### Satisfaction Signals
- **Architecture governance is visible** — many audit issues closed fast, indicating health
- **Command surfaces are converging** — `/model` `/status` consistent across channels
- **Telegram completeness shipped** — attachment/command parity reached for v1.1.0

---

## 8. Backlog Watch

| Issue | Age | Why watch |
|---|---|---|
| [#3762](https://github.com/nearai/ironclaw/issues/3762) (AGENTS.md live update) | ~85 days | Customer-facing, P1-suggested, v1.3.0 milestone — no PR activity. Likely needs design decision (system-prompt cache invalidation). |
| [#6257](https://github.com/nearai/ironclaw/issues/6257) (PDF MIME) | ~23 days | High-severity regression; no fix PR yet.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

Based on the provided GitHub data for `netease-youdao/LobsterAI` on 2026-08-11, here is the project digest.

---

## 🦞 LobsterAI Project Digest — 2026-08-11

### 1. Today's Overview
LobsterAI experienced a highly active development day with a significant influx of contributions, primarily from the core contributor `fisherdaddy`. A surge of 20 Pull Requests (PRs) was merged or closed, covering a wide range of areas including the renderer, the `openclaw` agent gateway, and Windows-specific runtime fixes. While no new releases were tagged, the project continues to iterate rapidly, focusing on UI/UX polish for the "cowork" feature and stability patches for the underlying OpenClaw gateway. A dozen new PRs remain open, mostly automated dependency bumps, alongside a specific fix for provider/model IDs. Activity is high and the project is in a rapid refinement phase.

### 2. Releases
- **No new releases** were published in the last 24 hours. The project is currently in a pre-release development cycle, building towards the next stable version (the last reported version in issues is `2026.4.1`).

---

### 3. Project Progress
A large batch of work was merged or closed on 2026-08-10, indicating a strong push on both feature development and bug fixing:

- **Cowork UI & UX Enhancements:**
  - [#2472](https://github.com/netease-youdao/LobsterAI/pull/2472) - **feat(cowork): activity group collapse** - Added the ability to collapse groups of activity in the cowork interface.
  - [#2471](https://github.com/netease-youdao/LobsterAI/pull/2471) - **feat(cowork): render submitted file attachments as clickable cards** - Fixed a UX gap where non-image attachments were rendered as raw text after sending; they now appear as rich file cards.
  - [#2469](https://github.com/netease-youdao/LobsterAI/pull/2469) - **feat(cowork): add collapse-agent-tasks shortcut...** - Introduced a new keyboard shortcut to collapse agent tasks and allowed modifier shortcuts while the user is typing.
  - [#2468](https://github.com/netease-youdao/LobsterAI/pull/2468) - **refactor(cowork): unify streaming loading indicators** - Standardized the loading indicators across the streaming experience for a more consistent UI.

- **OpenClaw Gateway Fixes:**
  - [#2454](https://github.com/netease-youdao/LobsterAI/pull/2454) - **fix(openclaw): stop tool-loop guard from killing legitimate polling** - Fixed a critical bug where the agent could incorrectly kill legitimate long-running processes, mistaking them for an infinite tool loop.
  - [#2470](https://github.com/netease-youdao/LobsterAI/pull/2470) - **fix(openclaw): surface provider runtime failures on late chat error** - Fixed an issue that was silently swallowing real provider/LLM errors, which should improve error reporting and visibility for users.

- **Windows & Runtime Stability:**
  - [#2467](https://github.com/netease-youdao/LobsterAI/pull/2467) - **fix(python-runtime): repair stale pip shims on Windows runtime upgrade** - Fixed an issue on Windows where outdated pip shims could survive runtime syncs, potentially causing installation conflicts. The fix extracts shim templates into a shared module for consistency.

- **Architecture & Infrastructure:**
  - [#2466](https://github.com/netease-youdao/LobsterAI/pull/2466) - **Fix/renderer init ipc stall retry** - Improved the renderer initialization process to handle IPC stalls with a retry mechanism, increasing startup reliability.

---

### 4. Community Hot Topics
The most active discussion in the last day was the closed bug report:

- **[#1243 [BUG] qwen-portal-auth 插件配置循环写入导致网关频繁重启](https://github.com/netease-youdao/LobsterAI/issues/1243)** (2 comments)
  - **Issue:** A user reported that the `qwen-portal-auth` plugin configuration causes the OpenClaw gateway to restart every 5–20 minutes, severely impacting usability, especially for non-Qwen models.
  - **Analysis:** While this issue is now closed as stale, the underlying concern is critical: the gateway's reliability and config stability. The user's expectation is that configuration remains stable. This highlights a potential fragility in the configuration sync loop, though the recent PRs on gateway fixes (#2454, #2470) suggest active work in this area.

---

### 5. Bugs & Stability
Several fixes related to stability and user experience were merged, indicating a strong focus on hardening the application:

- **[High] Gateway Instability & Silent Failures (OpenClaw)**
  - The fixes in [#2454](https://github.com/netease-youdao/LobsterAI/pull/2454) (killing legitimate polling) and [#2470](https://github.com/netease-youdao/LobsterAI/pull/2470) (swallowing provider errors) address two significant stability issues. They were likely causing either unexplained disconnections or silent failures in AI tasks. Both are now merged.

- **[Medium] Windows Python Runtime Issues**
  - The fix in [#2467](https://github.com/netease-youdao/LobsterAI/pull/2467) addresses a build-quality issue with pip shims on Windows that could cause the runtime to break or become inconsistent. This is a good sign of proactive maintenance for Windows users.

- **[Medium] Renderer Initialization Crashes/Stalls**
  - The fix in [#2466](https://github.com/netease-youdao/LobsterAI/pull/2466) targets IPC stalls during initialization, which could cause the interface to hang or crash on startup. This is likely a critical fix for users experiencing startup problems.

---

### 6. Feature Requests & Roadmap Signals
No new feature requests were directly submitted in the last 24 hours. However, the merged PRs provide strong signals about the project's current direction and roadmap:

- **Roadmap Focus: "Cowork" UI ** Deep Polish**: The significant number of UI/UX enhancements for the "cowork" feature (#2471, #2472, #2469, #2468) signals that this is a key upcoming area. The focus on file attachment cards, activity grouping, and keyboard shortcuts suggests the team is polishing it for a broader release.
- **Predictions for Next Version:**
  - A dedicated keyboard shortcut system with modifier support will likely be included.
  - The upcoming version will feature a more stable and responsive "cowork" experience with clear visual feedback for file handling and streaming.

---

### 7. User Feedback Summary
The only direct user feedback in the past day was from the bug report on the gateway instability (#1243). While the issue is stale, it illustrates the following:

- **Pain Point:** The `qwen-portal-auth` config loop is a significant pain point for affected users, causing frequent disruptions to their workflow.
- **Expectation:** Users expect a "set-and-forget" experience where the application configuration is stable and does not change without their intervention.
- **Satisfaction:** The user was clearly dissatisfied with this behavior, describing it as severely impacting their experience. The community is likely pleased to see the recent gateway stability fixes (#2454, #2470), which might address some of these root causes.

---

### 8. Backlog Watch
Several dependency update PRs have been open for a long time. They require attention from maintainers to keep the project healthy.

- **[Dependency Update] [#1277 chore(deps-dev): bump the electron group...](https://github.com/netease-youdao/LobsterAI/pull/1277)** - Open since **April 2, 2026** (over 4 months). This bumps `electron` (40.x to 43.x) and `electron-builder`. Long-dormant major updates like this can become difficult to merge and may lag significantly behind security patches. **Maintainer attention required.**

- **[Dependency Update] [#1766 chore(deps-dev): bump vite from 5.4.21 to 8.0.13](https://github.com/netease-youdao/LobsterAI/pull/1766)** - Open since **April 20, 2026**. This was closed today, and a new PR [#2465](https://github.com/netease-youdao/LobsterAI/pull/2465) for an even newer version (8.2.1) was opened. This indicates the previous bump was likely stale and the project is moving to the latest Vite 8.x, which is a positive sign.

- **[New Major Dependencies:** The batch of today's new PRs (#2460-#2465) bumps major versions for `react-dom` (19.2.8), `mermaid` (11.x), `eslint-plugin-react-hooks` (7.x), and `rimraf` (6.x). These are significant updates that need careful review and testing before merging to avoid regressions.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-08-11

## 1. Today's Overview
Moltis is in a **moderate activity phase** with 3 open issues and 1 pull request updated in the last 24 hours, zero new releases, and no merged/closed PRs. The project is showing **healthy bug-reporting momentum** from the community, with three distinct bugs submitted around the Apple Container sandbox backend and the gogcli build dependency — suggesting active real-world usage of the sandboxing features. While no code was merged today, the long-running browser viewing UI PR (#531) received an update after months of dormancy, indicating maintainer attention may be returning to feature work. Overall, the project is **stable but not rapidly moving**, with the community actively exercising and stress-testing the Apple Container integration in particular.

## 2. Releases
**No new releases in the last 24 hours.** The most recent release remains unknown from this data window. No changelog, migration notes, or breaking changes to report.

---

## 3. Project Progress
**No PRs were merged or closed in the last 24 hours.** However, one significant PR saw activity:

- **[PR #531: feat(browser) — interactive browser viewing UI with CDP screencast](https://github.com/moltis-org/moltis/pull/531)** — Updated 2026-08-10 after being open since 2026-03-31 (over 4 months). This PR adds a full browser viewing and interaction UI to the Settings > Browser page, enabling live CDP screencast viewing, mouse/keyboard/scroll interaction, session history with action logs, and per-agent cookie isolation. This is a **major feature** that, if merged, would significantly enhance the agent-browser interaction experience.

---

## 4. Community Hot Topics
**Most active issue: [#1185 — Apple Container 1.x sandbox starts but Moltis treats it as not running](https://github.com/moltis-org/moltis/issues/1185)**
- Author: mikz | Created: 2026-08-08 | Updated: 2026-08-10 | **3 comments**
- This is the hottest topic with the most community engagement. The reporter describes a scenario where the sandbox process actually starts, but Moltis' internal state tracking incorrectly believes it failed. The 3 comments suggest there's active back-and-forth between the reporter and maintainers/community members troubleshooting the issue.

**Other open issues (0 comments each):**
- [#1189 — Sandbox build failing due to wrong gogcli github URL](https://github.com/moltis-org/moltis/issues/1189)
- [#1188 — resource limits not applied for apple-container backend](https://github.com/moltis-org/moltis/issues/1188)

**Underlying needs:** The community is heavily testing the Apple Container sandbox backend (the newer, more secure container model) and finding integration gaps. The need behind #1185 is **reliable state synchronization** between the actual sandbox lifecycle and Moltis' monitoring layer.

---

## 5. Bugs & Stability
Three bugs reported/updated in the last 24 hours, **all open with no fix PRs identified yet**:

| Severity | Issue | Description | Status |
|----------|-------|-------------|--------|
| **High** | [#1185 — Apple Container 1.x sandbox starts but Moltis treats it as not running](https://github.com/moltis-org/moltis/issues/1185) | Sandbox launches but Moltis incorrectly reports it as failed — this could cause users to abandon valid sandboxes or trigger spurious restarts | Open, 3 comments, active discussion |
| **Medium** | [#1188 — resource limits not applied for apple-container backend](https://github.com/moltis-org/moltis/issues/1188) | Resource constraints (CPU/memory limits) silently ignored on Apple Container backend — potential for runaway resource consumption | Open, no comments |
| **Medium** | [#1189 — Sandbox build failing due to wrong gogcli github URL](https://github.com/moltis-org/moltis/issues/1189) | Build-time dependency resolution failure blocks sandbox image creation entirely — likely a simple URL configuration fix but blocks all users of that build path | Open, no comments |

**Assessment:** The Apple Container backend has **3 active defects** concentrated in the same area, suggesting this backend may have been recently introduced or refactored and needs a stability pass.

---

## 6. Feature Requests & Roadmap Signals
**Direct requests (implicit via bug reports):**
- **Robust sandbox state validation** — behind #1185, the community wants Moltis to distinguish "sandbox started but health-check failed" from "sandbox never started."
- **Resource limit enforcement parity** across all container backends — the Apple Container backend should honor the same limits as other backends (#1188).

**Predictions for next version:**
- The **browser viewing UI** (PR #531) is the most likely next major feature to land, given the recent activity after months of dormancy. This would enable visual agent debugging, which is a major UX differentiator.
- **Apple Container stability fixes** are almost certain in the next patch/minor release, as three related bugs create a poor impression of that backend.

---

## 7. User Feedback Summary
**Pain points:**
- **State-disconnect frustration:** Users report that Moltis gives inaccurate status signals about sandboxes — the sandbox is actually running but the user is told otherwise (#1185), wasting time and eroding trust in the monitoring UI.
- **Silent limit bypass:** Resource limit misconfiguration on the Apple Container backend means users may believe their sandboxes are constrained when they are not, creating a false security/resource-safety profile (#1188).
- **Build friction:** A simple URL typo in tooling dependency (gogcli) blocks sandbox builds entirely, highlighting a lack of pre-flight validation in the build pipeline (#1189).

**Use cases observed:** Users are running AI agent sandboxes in production-like scenarios with resource constraints, chat sessions, and multi-session persistence. The browser UI PR indicates strong interest in **visual agent supervision**.

**Satisfaction:** Neutral-to-negative this week, driven primarily by the Apple Container backend issues. The reporter in #1185 followed the full preflight checklist and engaged in discussion, showing a committed user base.

---

## 8. Backlog Watch
**Needs maintainer attention:**

- **[PR #531 — Browser UI with CDP screencast](https://github.com/moltis-org/moltis/pull/531)**: Open for **133 days** (created 2026-03-31), updated yesterday. This is a major feature that has sat unreviewed for months. The update suggests the author is still actively maintaining it. **Action needed:** Review and merge or give clear feedback to prevent further stagnation.

- **[#1185 — Apple Container state detection bug](https://github.com/moltis-org/moltis/issues/1185)**: The most-commented issue with an active discussion; needs a maintainer response to provide a workaround or timeline for fix.

- **No other long-dormant issues appear** in the current window, but the overall volume of Apple Container bugs (3 in 48 hours) suggests a dedicated triage session for that backend would be productive.

---

*Digest generated for 2026-08-11 from moltis-org/moltis GitHub activity data.*

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

Based on the GitHub activity data for CoPaw (agentscope-ai/CoPaw) on 2026-08-11, here is the project digest:

---

## CoPaw Project Digest — 2026-08-11

### 1. Today's Overview
CoPaw (QwenPaw) shows **high-velocity development** and an **active, engaged community** on August 11, 2026, primarily focused on the upcoming v2.1.0 release. Activity is split evenly between bug fixing (40 issues updated) and feature development (50 PRs updated), with a strong emphasis on **stability and memory-system improvements**. No new release was published today; however, release preparation is underway, with a dedicated PR updating v2.1.0 release notes and README translations. The community is actively reporting bugs in v2.0.1 and beta versions (v2.1.0b2), particularly around provider compatibility, the new ReMe memory backend, MCP tools, and UI polish.

### 2. Releases
**None.** No new versions (stable or pre-release) were published in the last 24 hours. The next expected release is **v2.1.0** (likely soon, given the active release-notes PR).

---

### 3. Project Progress
**Merged/Closed PRs (20 today):** The project advanced on several key fronts, with PRs for bug fixes and enhancements either merged or closed.

**Key Highlights:**
- **Provider Compatibility Fix:** [PR #6809 - fix(providers): sanitize Chat Completions content for strict providers](https://github.com/agentscope-ai/QwenPaw/pull/6809) was closed, addressing a critical bug where OpenAI-compatible requests were rejected by strict providers like StepFun ([Issue #6803](https://github.com/agentscope-ai/QwenPaw/issues/6803)).
- **Improved Stability:** [PR #6615 - fix(config): handle corrupted agent config and invalid JSON in load_agent_config](https://github.com/agentscope-ai/QwenPaw/pull/6615) was closed by a first-time contributor, making the system more resilient to corrupted configuration files.
- **UI/UX Enhancements:** [PR #6878 - feat(console): add hidden-folders toggle to project directory picker](https://github.com/agentscope-ai/QwenPaw/pull/6878) was closed, improving project directory selection.
- **Memory Search Upgrades (Merged):** The PR for adding **reranker support to the ReMe memory search** ([PR #6398](https://github.com/agentscope-ai/QwenPaw/pull/6398)) was closed, signaling the backend work for this significant feature is complete.

**Open PRs In-Progress (Selected):**
- **Core Memory Fix:** [PR #6564 - fix(memory): flush pending turns before compression](https://github.com/agentscope-ai/QwenPaw/pull/6564) remains open, targeting a critical auto-memory persistence logic gap.
- **Creator Plugin Overhaul:** [PR #6870 - feat(creator): settings center, agent skills, mm-plugins compose orchestration...](https://github.com/agentscope-ai/QwenPaw/pull/6870) is a major aggregate PR for the QwenPaw Creator plugin with cross-platform hardening.
- **Release Prep:** [PR #6875 - chore: update release notes for v2.1.0](https://github.com/agentscope-ai/QwenPaw/pull/6875) is being prepared.

---

### 4. Community Hot Topics
The most-discussed issues this week reveal pain points in version 2.0.x and excitement/curiosity about the new ReMe memory system.

- **[Issue #6782 - [Bug]: 2.0.1 docker版本，插件市场、应用市场始终提示维护中 (Markets Unavailable in Docker)](https://github.com/agentscope-ai/QwenPaw/issues/6782):** This is the **most active issue** with 9 comments. Users running the Docker version of 2.0.1 report that the plugin and app marketplaces always appear "under maintenance," rendering them unusable.
- **[Issue #6803 - [Bug]: OpenAI-compatible chat requests... rejected (StepFun: 400)](https://github.com/agentscope-ai/QwenPaw/issues/6803):** A high-severity compatibility bug from v2.0.1. The issue is resolved, and the fix ([PR #6809](https://github.com/agentscope-ai/QwenPaw/pull/6809)) has been closed.
- **[Issue #6811 - [Bug]: OpenAI Responses continuation summary... (blocks conversation + misreports cancellation)](https://github.com/agentscope-ai/QwenPaw/issues/6811):** A complex interaction bug where a background task (creating a summary) blocks the main conversation and can misreport a 60-second timeout as malformed output, highlighting a need for better async/background task handling.
- **[Issue #6826 - [Bug]: 对话中助手消息结束时间显示异常 (Assistant Message End Time Display Bug)](https://github.com/agentscope-ai/QwenPaw/issues/6826):** A UI bug where thinking time is not reflected in the display, confusing users about actual response duration.
- **[Issue #4237 - Long-standing Feature: In-chat observability for running shell commands](https://github.com/agentscope-ai/QwenPaw/issues/4237):** With 4 comments, there is continued demand for in-chat visibility and control over shell command execution (see, kill, or extend timeout).
- **[Issue #6405 - [Question]: mcp工具总是提示Tool notfound (MCP Tool Not Found)](https://github.com/agentscope-ai/QwenPaw/issues/6405):** Multiple users are asking about MCP tool resolution failures after upgrading to 2.0, indicating a config or naming issue.

---

### 5. Bugs & Stability
Ranked by severity, with notes on existing fix PRs.

**High Severity (Crashes, Unusable Features):**
- **macOS SQLite Crash:** [Issue #6814 - SIGBUS (FS pagein 22) in sqlite3WalFindFrame](https://github.com/agentscope-ai/QwenPaw/issues/6814) — Crashing when opening the Scroll history database on macOS, a non-inference-related stability failure.
- **Docker Markets Unavailable:** [Issue #6782 - 插件市场、应用市场提示维护中](https://github.com/agentscope-ai/QwenPaw/issues/6782) — The app and plugin marketplaces are completely unavailable in the Docker build, preventing installs.
- **Windows Install/Update Failures:** [Issue #6810 - Windows 安装更新覆盖文件前应终止占用进程](https://github.com/agentscope-ai/QwenPaw/issues/6810) — NSIS installers fail when files are locked by processes like browser extension NM hosts.

**Medium Severity (Functionality/Performance):**
- **Provider Request Failures:** [Issue #6821 - reasoning_content relay fails for thinking-mode models → 400](https://github.com/agentscope-ai/QwenPaw/issues/6821) — API calls fail for thinking-mode models. Related to the provider sanitization fix in [PR #6809](https://github.com/agentscope-ai/QwenPaw/pull/6809).
- **Antivirus Conflicts:** [Issue #6847 - Qwenpaw被杀软打死](https://github.com/agentscope-ai/QwenPaw/issues/6847) — The app is being blocked/terminated by antivirus software, a significant friction point for users.
- **Backend Task Structure:** Several issues/PRs point to bugs in Auto-Dream. [Issue #6841](https://github.com/agentscope-ai/QwenPaw/issues/6841) and [Issue #6853](https://github.com/agentscope-ai/QwenPaw/issues/6853) indicate that the Auto-Dream process is fragile and the documentation does not match its actual behavior. A fix PR, [PR #6884 - fix: make Auto-Dream integration resilient](https://github.com/agentscope-ai/QwenPaw/pull/6884), is open.

**Low Severity (UX/Polish):**
- **UI Display Issues:** [Issue #6826](https://github.com/agentscope-ai/QwenPaw/issues/6826) (time display), [Issue #6820](https://github.com/agentscope-ai/QwenPaw/issues/6820) (no streaming output display), and [Issue #6828 - Console frontend high CPU usage at idle](https://github.com/agentscope-ai/QwenPaw/issues/6828) (infinite CSS animations causing ~20% CPU) are all reported, with [PR #6845 - fix(chats): preserve assistant completion time](https://github.com/agentscope-ai/QwenPaw/pull/6845) addressing the related time issue.

---

### 6. Feature Requests & Roadmap Signals
The community's wants are clear, pointing towards a more controllable and observable AI agent.

- **In-Chat Command Control:** The long-standing request for **in-chat observability for running shell commands** with per-command kill/timeout capabilities ([Issue #4237](https://github.com/agentscope-ai/QwenPaw/issues/4237)) remains open at 4 comments and represents a core power-user need.
- **Configurable MCP Timeouts:** [Issue #6724 - Configurable MCP tool-call timeout](https://github.com/agentscope-ai/QwenPaw/issues/6724) requests the ability to set timeouts on MCP tool calls. Combined with [Issue #6405](https://github.com/agentscope-ai/QwenPaw/issues/6405), MCP reliability is a critical theme this week.
- **Memory System Diagnostics:** With the rollout of ReMe, users are asking clarifying questions and filing nuances. Examples include [Issue #6840 - timeline for full ReMe4 roadmap](https://github.com/agentscope-ai/QwenPaw/issues/6840) and [Issue #6881 - Auto-refresh session title after auto-memory update](https://github.com/agentscope-ai/QwenPaw/issues/6881). This suggests active adoption and testing of the new memory system.
- **UI Customization:** Users want to hide UI elements that become annoying, such as the "characters received" counter ([Issue #6585](https://github.com/agentscope-ai/QwenPaw/issues/6585)) and the background task panel ([Issue #6876](https://github.com/agentscope-ai/QwenPaw/issues/6876)). This points to a need for more UI adaptability.
- **Quality of Life (Already In Development):** A popular request was for the desktop app to **remember window geometry**. This was implemented in the new [PR #6877 - feat(desktop): remember window geometry](https://github.com/agentscope-ai/QwenPaw/pull/6877).

---

### 7. User Feedback Summary
User sentiment is mixed between frustration with current instability and anticipation for new features.

- **Pain Points:**
    - **MCP Tools (Troubleshooting):** Several issues ([#6405](https://github.com/agentscope-ai/QwenPaw/issues/6405), [#6839](https://github.com/agentscope-ai/QwenPaw/issues/6839)) highlight a problematic experience with MCP tools, varying from resolution failures to incorrect parameter type coercion.
    - **Platform Inconsistencies:** There is clear friction for users on non-ideal setups, whether running on **Docker** (marketplace failures), **Windows** (file lock issues, plugin failures), or **macOS** (SQLite crashes, ffmpeg not found due to PATH exclusions).
    - **Unexpected System Behavior:** Users are unsettled by being blocked by their antivirus software ([#6847](https://github.com/agentscope-ai/QwenPaw/issues/6847)) and by "lies" in prompts that claim features (like ReMe sync) that are not implemented ([#6853](https://github.com/agentscope-ai/QwenPaw/issues/6853)).
- **Positive Signals:**
    - **Engaged Community:** Users are diving deep into new features like ReMe, asking clarifying questions and proposing enhancements, indicating genuine interest in the project's direction.
    - **First-Time Contributors:** The presence of several `first-time-contributor` PRs ([#6884](https://github.com/agentscope-ai/QwenPaw/pull/6884), [#6854](https://github.com/agentscope-ai/QwenPaw/pull/6854), [#6599](https://github.com/agentscope-ai/QwenPaw/pull/6599)) is a sign of a healthy, welcoming open-source project.

---

### 8. Backlog Watch
These issues and PRs have awaited attention for a while and may need maintainer review:

- **Critical Bug (Unanswered):** [Issue #6814 - SIGBUS (FS pagein 22) in sqlite3WalFindFrame while opening Scroll history.db (WAL) on macOS](https://github.com/agentscope-ai/QwenPaw/issues/6814) — A crash-level bug on a major platform (macOS). The "Newcomer friendly" label may not be appropriate for this severe issue; it needs a maintainer or senior developer to address it to prevent user data loss.
- **Core Feature Fix (Under Review for 12 days):** [PR #6564 - fix(memory): flush pending turns before compression (#6555)](https://github.com/agentscope-ai/QwenPaw/pull/6564) — This is a critical fix for the auto-memory system that needs maintainer attention and merging.
- **Long-standing Feature Request (90 days old):** [Issue #4237 - In-chat observability for running shell commands](https://github.com/agentscope-ai/QwenPaw/issues/4237) — This feature directly impacts user trust and observability and has been open since May 12. It should be formally triaged and prioritized.
- **Suspicious Inactivity:** [Issue #6847 - 同样的任务和模型，Qwenpaw会被杀软打死](https://github.com/agentscope-ai/QwenPaw/issues/6847) — The user mentions a competitor tool, "WorkBuddy," and their report of antivirus blocking is a serious "trust and safety" issue that should be investigated.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-08-11

## 1. Today's Overview

ZeroClaw is in an active development and hardening phase with a substantial **50 open issues and 50 open pull requests** receiving updates in the last 24 hours. The project shows **high velocity with zero merged PRs and zero closed issues today**, indicating a focus on collaborative review and iteration rather than rapid merging. The issue tracker reveals a significant concentration on **security-critical findings** — particularly around channel authorization gaps, sandbox bypass vectors, and audit logging failures — alongside ongoing governance work (RFC process reform, label automation). The PR queue is dominated by **large, long-running feature branches** (several with `size:XL` and `risk:high` labels) that appear to be in sustained development, with many tagged `needs-author-action`, suggesting maintainers are actively requesting revisions. Overall, this is a project prioritizing **security hardening and architectural governance** over new feature velocity in the current cycle.

## 2. Releases

**No new releases in the last 24 hours.**

---

## 3. Project Progress

**No PRs were merged or closed in the last 24 hours.**

The project is currently in a **review and revision-heavy phase**, with **50 open PRs** all awaiting further action. The following PRs represent the most significant in-flight work that has been advancing:

- **[PR #8486 — OpenAI Chat Completions endpoint](https://github.com/zeroclaw-labs/zeroclaw/pull/8486)** (`size:XL`, `risk:high`): This substantial feature would enable the gateway to natively speak the OpenAI Chat Completions protocol, opening ZeroClaw to LangChain, OpenAI SDK, Continue.dev, and Aider clients. It is among the longest-running PRs (open since June 29) and appears to be a major architectural addition.

- **[PR #8713 — SSRF gate for file_download](https://github.com/zeroclaw-labs/zeroclaw/pull/8713)** (`size:XL`, `risk:high`): A security-hardening PR that addresses a missing SSRF validation in the operator-configured `[file_download].url`, which could otherwise silently route requests to internal addresses like `169.254.169.254`. Tagged `needs-author-action`.

- **[PR #9109 — Native Hailo-Ollama provider](https://github.com/zeroclaw-labs/zeroclaw/pull/9109)** (`size:XL`, `risk:high`): Adds dedicated support for the Hailo-Ollama native `/api/chat` and `/api/tags` contract, keeping existing Ollama-compatible paths as a fallback.

- **[PR #9222 — LLM-judge grader](https://github.com/zeroclaw-labs/zeroclaw/pull/9222)** (`size:XL`, `risk:high`): Introduces a per-dimension LLM-judge grading system, deliberately gated **off** until calibrated so an unproven judge cannot block builds.

- Several **service-log bounding PRs** ([#9773](https://github.com/zeroclaw-labs/zeroclaw/pull/9773) for launchd, [#9789](https://github.com/zeroclaw-labs/zeroclaw/pull/9789) for OpenRC) continue to advance the operational reliability initiative.

- Two **duplicate WhatsApp reaction PRs** ([#9894](https://github.com/zeroclaw-labs/zeroclaw/pull/9894), [#9893](https://github.com/zeroclaw-labs/zeroclaw/pull/9893)) were filed today, both rebases of #7535 — maintainers should consolidate these.

---

## 4. Community Hot Topics

The most active discussions today center on **governance reform, security policy decisions, and architectural planning**:

- **[Issue #6808 — RFC: Work Lanes, Board Automation, Label Cleanup](https://github.com/zeroclaw-labs/zeroclaw/issues/6808)** (23 comments, open since May 20): The project's foremost governance RFC, detailing work routing, board automation, and label cleanup. Ratification has been deferred as rollout continues across many revisions (Rev. 24). This has been running for nearly three months, indicating a complex consensus-building process.

- **[Issue #7100 — RFC: Per-model capability & context-window config](https://github.com/zeroclaw-labs/zeroclaw/issues/7100)** (13 comments): Addresses misreported vision support and context-window defaults across providers. A `risk:high` RFC that would unify capability, capacity, and budget configuration.

- **[Issue #8692 — Maintainer decision queue tracker](https://github.com/zeroclaw-labs/zeroclaw/issues/8692)** (12 comments): The project has formalized a decision queue for RFCs and design issues, signaling a heavy governance overhead that may be slowing progress.

- **[Issue #9397 — WhatsApp Web empty `allowed_groups` treated as permit-none](https://github.com/zeroclaw-labs/zeroclaw/issues/9397)** (12 comments): A `risk:high` security RFC proposing that an empty allowlist should deny all groups (fail-secure), rather than the current fail-open behavior.

- **[Issue #9496 — RFC: Streamline RFC scope, discussion, voting](https://github.com/zeroclaw-labs/zeroclaw/issues/9496)** (7 comments, `risk:high`): A direct response to the perceived slowness of the project's own RFC process — noting the seven-day minimum discussion period and unanimity requirements are causing friction.

**Underlying need:** The cluster of governance issues (#6808, #8692, #9496) indicates the project is actively **struggling with process overhead**, while the security RFCs and the [maintainer queue](https://github.com/zeroclaw-labs/zeroclaw/issues/8692) suggest a community that values rigorous review but is seeking to streamline it.

---

## 5. Bugs & Stability

No new bug reports were filed in the last 24 hours. However, numerous **high-severity bugs remain open and actively discussed**, with several having fix PRs in-flight:

### Security & Data Loss (S0/S1)

- **[Issue #9647 — Knowledge graph lacks per-agent attribution](https://github.com/zeroclaw-labs/zeroclaw/issues/9647)** (S0 — data loss/security risk): Any agent can read/mutate another agent's knowledge. **No fix PR open.**

- **[Issue #9627 — git write verbs bypass risk classifier](https://github.com/zeroclaw-labs/zeroclaw/issues/9627)** (S0 — data loss/security risk): Global options like `-C`/`--git-dir` allow bypass of the approval gate for destructive git operations. **No fix PR open.**

- **[Issue #9392 — LINE group messages skip allowlist & pairing](https://github.com/zeroclaw-labs/zeroclaw/issues/9392)** (S1): Unauthorized senders can reach the agent. **No fix PR open.**

- **[Issue #9393 — Bluesky and Reddit lack sender authorization](https://github.com/zeroclaw-labs/zeroclaw/issues/9393)** (S1): No central authorization gate covers these channels. **No fix PR open.**

- **[Issue #9389 — Unauthenticated POST /api/pair keys lockout on attacker header](https://github.com/zeroclaw-labs/zeroclaw/issues/9389)** (S1): A pairing bypass risk. **No fix PR open.**

- **[Issue #9391 — Command audit logging defaults to enabled but writes nothing](https://github.com/zeroclaw-labs/zeroclaw/issues/9391)** (S1): Audit trail is silently missing despite appearing enabled. **No fix PR open.**

- **[Issue #9395 — WASI http egress has no destination policy](https://github.com/zeroclaw-labs/zeroclaw/issues/9395)** (S1): Plugins can make unrestricted egress requests. **No fix PR open.**

### Functional / Workflow Blocked (S1)

- **[Issue #9207 — web_fetch returns garbage for compressed responses](https://github.com/zeroclaw-labs/zeroclaw/issues/9207)** (S1): gzip/brotli/deflate not decoded. **No fix PR open.**

- **[Issue #9425 — Running SOP jobs have no operator cancellation path](https://github.com/zeroclaw-labs/zeroclaw/issues/9425)** (S1): Dashboard cannot stop an executing SOP. **No fix PR open.**

- **[PR #8713](https://github.com/zeroclaw-labs/zeroclaw/pull/8713)** (open) addresses the SSRF issue; **PR #9839** ([deny irreversible commands](https://github.com/zeroclaw-labs/zeroclaw/pull/9839)) partially addresses the git-bypass class; and **PR #9897** ([fix reload signal](https://github.com/zeroclaw-labs/zeroclaw/pull/9897)) directly fixes the dangerous SIGUSR1 issue from **Issue #9768**.

---

## 6. Feature Requests & Roadmap Signals

The following high-priority feature requests are strong candidates for the next release:

### High Probability (explicit RFC/feature, previously accepted):

- **[#7100 — Per-model capability & context-window config](https://github.com/zeroclaw-labs/zeroclaw/issues/7100)**: Strong candidate — it is an accepted `risk:high` RFC with active discussion, addressing a widely felt pain point (misreported vision support and wrong context budgets).

- **[#9397 — WhatsApp Web fail-secure allowed_groups](https://github.com/zeroclaw-labs/zeroclaw/issues/9397)**: Given the security audit momentum, this is likely to land as a breaking-change fix.

- **[#9339 — Custom CA trust for remote MCP servers](https://github.com/zeroclaw-labs/zeroclaw/issues/9339)**: Important for enterprise/private-network deployments; in progress.

- **[PR #8486 — OpenAI-compatible endpoint](https://github.com/zeroclaw-labs/zeroclaw/pull/8486)**: Based on sheer size and longevity, this is a flagship feature likely targeted for the next minor release (0.9.0).

### Watch List (trackers/contributor RFCs):

- **[#6808 — Work Lanes RFC](https://github.com/zeroclaw-labs/zeroclaw/issues/6808)**: The rollout is "in progress," suggesting incremental adoption alongside code changes.

- **[#9496 — Streamlined RFC process](https://github.com/zeroclaw-labs/zeroclaw/issues/9496)**: An accepted RFC that may change contribution workflows in the coming weeks.

---

## 7. User Feedback Summary

- **Configuration defaults are misleading** — Multiple issues surfaced this cycle around documented-but-unimplemented defaults:
  - **[#9779](https://github.com/zeroclaw-labs/zeroclaw/issues/9779)** — `sops_dir` documented default silently disables the entire SOP subsystem when unset.
  - **[#9391](https://github.com/zeroclaw-labs/zeroclaw/issues/9391)** — Audit logging "enabled by default" writes nothing.

- **Security posture is a major user concern** — The volume of S0/S1 security findings from the community audit (issues #9389, #9392, #9393, #9395, #9647, #9627) shows users are actively auditing the codebase and are frustrated by fundamental fail-open patterns.

- **Developer experience friction** — Issues like **[#9844](https://github.com/zeroclaw-labs/zeroclaw/issues/9844)** (misleading CPU metric in ZeroCode dashboard) and **[#9562](https://github.com/zeroclaw-labs/zeroclaw/issues/9562)** (WebChat auto-scroll hijack during streaming) indicate users care about the observability and UI polish of the developer tools.

- **Community is engaged and thorough** — The high level of detail and verification in the security issues (e.g., "every cited line was opened and every quote checked") reflects a dedicated, technically sophisticated user base that values the project's direction.

---

## 8. Backlog Watch

Issues/PRs that have been open for a significant time and need maintainer decisions:

- **[Issue #6808 — Work Lanes RFC](https://github.com/zeroclaw-labs/zeroclaw/issues/6808)**: Open since **May 20** (nearly 3 months), with 23 comments and still in "Ratification deferred." This is a critical governance item blocking other work and needs a final call.

- **[PR #8486 — OpenAI endpoint](https://github.com/zeroclaw-labs/zeroclaw/pull/8486)**: Open since **June 29** (6+ weeks). Despite its size, its continued open state without merge suggests either maintainers are deferring or there are unresolved design questions.

- **[Issue #5842 — Codex CLI extra_args sandbox warning](https://github.com/zeroclaw-labs/zeroclaw/issues/5842)**: Open since **April 17** (nearly 4 months), `risk:high`, and in-progress but with no linked PR in the recent queue. This is a long-standing security-adjacent feature that deserves attention.

- **[Issue #8999 — ZeroCode streamed user turns look like log payloads to small models](https://github.com/zeroclaw-labs/zeroclaw/issues/8999)**: Open since July 11, `risk:high`, and part of the `follow-up` set. This UX problem may be losing priority despite its severity for local-model users.

- **[PR #8713 — SSRF gate](https://github.com/zeroclaw-labs/zeroclaw/pull/8713)**: Open since **July 4**, `size:XL`, `principal contributor`. Its size and `needs-author-action` status suggest it may be stuck in a review cycle and needs maintainer guidance to move forward.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/kky-wollu/agents-radar).*
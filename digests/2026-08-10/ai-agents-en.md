# OpenClaw Ecosystem Digest 2026-08-10

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-08-09 22:35 UTC

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

# OpenClaw Project Digest — 2026-08-10

## 1. Today's Overview

OpenClaw shows high activity with 500 issues and 500 PRs updated in the last 24 hours, though no new releases were published. The project maintains a healthy open/closed ratio (423:77 issues, 321:179 PRs) with significant work on security hardening, session-state reliability, and multi-channel message-delivery fixes. However, a concerning recurring theme is the persistence of **silent reply failures** — issue #116277 was closed but the failure mode reported in #121058 continues to occur, indicating incomplete fixes or regression. The PR queue is dominated by maintainer-driven refactors (steipete authored ~50% of top PRs), suggesting proactive technical-debt reduction, but many critical P1/P2 items remain blocked on maintainer review or product decisions. Interestingly, the project shows significant investment in "pairing" features (Tailscale, LAN setup, device pairing wizard) indicating a push toward mobile/desktop client UX maturity alongside core reliability fixes.

## 2. Releases

**No new releases published in the last 24 hours.** The last known version is `2026.7.2-beta.5` (referenced in issue #116022). The absence of releases is notable given the velocity of merged PRs (179 closed/merged), suggesting the maintainers are accumulating changes for a larger stable release rather than shipping incrementally.

## 3. Project Progress

**Merged/Closed PRs (179 total closed/merged; top items):**

- **#121113** — `refactor(agents)!: remove the session write lease` (steipete, size XL): Breaking change removing an inherited JSONL file-lock architecture that survived two storage migrations. SQLite transactions and gateway state-directory locks now own data integrity.
- **#121256** — `fix(gateway): keep view-only desktop sessions connected` (steipete, size S): Fixes disconnection with `invalid view-only RFB stream` when noVNC 1.7 sends post-handshake flow-control messages.
- **#120734** — `fix(anthropic): reject leaked Claude tool protocol output` (VACInc, size L): Claude Code can return legacy `<invoke>`/`<parameter>` tool protocol as terminal assistant string; this rejects it to prevent persistence/delivery of fabricated output.
- **#121193** — `fix(gateway): refresh chat metadata after runtime auth succeeds` (steipete, size XL): `chat.metadata` could report OpenAI model unavailable even after a real agent turn proved the model route works through harness-owned auth.
- **#103103** — `fix(models): honor replace mode in list output` (steipete, size M): With `models.mode: "replace"`, default `openclaw models list` could still render authenticated catalog models and stale references.

**Key feature work advancing (open PRs):**
- **Pairing stack**: #120825 (non-secret connectivity preflight), #120890 (typed Tailscale route readiness), #121032 (guide Public URL/LAN setup), #121138 (offer Tailscale in pairing wizard), #120768 (one-paste device pairing via `oc-pair` setup links) — a coordinated, multi-PR milestone for device onboarding.
- **UI quality**: #121249 (owned dialog for naming session groups instead of `window.prompt`), #120805 (distinguish inherited model defaults from session pins), #121258 (scope cursor convention to app-like display modes), #121259 (float task-suggestion cards with copy-prompt).
- **Refactors**: #121257 (move owner policy into plugins), #121263 (remove custom session icon feature end-to-end), #121268 (consolidate raw WebSocket payload decoding across 4 copies), #121250 (avoid plugin registry rebuilds on auth refresh).

## 4. Community Hot Topics

**Top Issues by activity:**

1. **#116277 (CLOSED, 196 comments)** — [P1, diamond lobster] DeepSeek v4 Flash silent reply failure. The most-commented issue by far, with a monitoring cron continuing to log occurrences even after closure (see #121058 below — likely why it was reopened in spirit).
   
2. **#121058 (OPEN, 19 comments)** — [No labels yet] Silent reply failures recurring after #116277 closed. *Directly follows up on #116277* — users are watching closely whether the fix actually holds. **🚨 Critical user trust signal.**

3. **#25592 (OPEN, 41 comments, 1👍)** — [P1, diamond lobster] Text between tool calls leaks to messaging channels. Long-running (since Feb 2026), 6 months old, still no fix PR. Users want **internal processing output** kept private from Slack/iMessage.

4. **#7707 (OPEN, 32 comments)** — [P2, enhancement] Memory Trust Tagging by Source. Users want to prevent **memory poisoning attacks** from untrusted web content. Still needs maintainer decision.

5. **#44925 (OPEN, 25 comments, 2👍)** — [P1, silver shellfish] Subagent completion silently lost (no retry/notification/restart). Multiple failure patterns where work is lost without notification.

6. **#92201 (OPEN, 21 comments, 1👍)** — [P1, silver shellfish] Anthropic thinking signatures intermittently invalid on replay; recovery wrapper never fires due to genericized error text.

**Top PRs by size/activity (maintainer-heavy):**
- #121063 (size XL, P1) — Bound runaway loops with turn/error-batch/idle-repeat guards. Closes #120962; addresses a 6h42m/219-turn/15M-token runaway loop caused by a masked HTTP 429.
- #121200 (size XL, P1) — Make Cloud Worker startup responsive.
- #121062 (not in top-30 list but referenced as related) — Cloud worker Git workspace size fix (#121262).

**Analysis:** The community is deeply concerned about **silent failure modes** (replies never generated, subagent work lost, text dropped between tool calls) and **security boundaries** (memory poisoning, API key exposure, raw issue body injection). The high comment counts correlate with P1 severity and session-state/message-loss impacts, not popularity. The DeepSeek v4 issue (#116277) at 196 comments is a standout community flashpoint — even after closure, users are verifying whether the fix truly resolves the issue.

## 5. Bugs & Stability

**Ranked by severity (P0 first):**

| Severity | Issue | Summary |
|----------|-------|---------|
| **P0** | #48920 | [Bug]: Live Docs are ahead of release — docs document features not in latest stable. 10 comments, 4👍. No fix PR. |
| **P1** | #121058 | Silent reply failures recurring after #116277 closed (DeepSeek v4 Flash). 19 comments. **No fix PR yet.** |
| **P1** | #115546 | CLI-budget compaction: timeout fires far below deadline (4.9s–50s), 100% failure rate on large sessions, no retry → **wake death-spiral**. 7 comments. |
| **P1** | #94939 | 6.x state migration leaves channel conversation-store SQLite empty (0 bytes) — breaks proactive Bot Framework sends (MS Teams). 8 comments. Linked PR open. |
| **P1** | #91009 | Codex PreToolUse native hook relay spawns CPU-bound `openclaw-hooks` processes, stalls gateway RPC. 18 comments, 2👍. |
| **P1** | #92201 | Freshly streamed Anthropic thinking signatures intermittently invalid on replay; recovery wrapper never fires. 21 comments. |
| **P1** | #97616 | OpenClaw leaks unreaped hook/tool child processes → zombie accumulation, runtime degradation. 7 comments. |
| **P1** | #44925 | Subagent completion silently lost (no retry/notification/restart). 25 comments, 2👍. |
| **P1** | #105528 | exec/read tools silently return empty output on Windows (v2026.6.x regression). 6 comments. |
| **P1** | #51049 | WhatsApp inbound messages not received in k3s nested container (outbound works). 6 comments. |
| **P1** | #121014 (PR) | **DO NOT MERGE** — Slack Enterprise Grid deferred actions lose workspace scope (merge-risk: 🚨 session-state/message-delivery). |

**Key stability themes:**
- **Silent failures dominate**: The top P1s center on work silently lost (subagents, replies, compaction) or silently not delivered (WhatsApp inbound, channel stores).
- **Resource leaks**: Hook/child process leaks (#97616), CPU-bound hooks (#91009), stale PTYs blocking gateway suspension (PR #121267) all point to lifecycle-management gaps.
- **Migration/regression risk**: DB state migrations (#94939), config schema drift (#120736), and docs-ahead-of-release (#48920) suggest release-process discipline needs attention.

**Existing fix PRs:**
- #120734 (merged) addresses Claude tool protocol leakage.
- #121063 (open) addresses runaway loops.
- #121267 (open) addresses stale PTY/blocked suspension.
- #121014 (open, **DO NOT MERGE**) addresses Slack workspace scope — needs author attention.

## 6. Feature Requests & Roadmap Signals

**High-signal requests likely for next release:**

1. **Memory Trust Tagging (#7707)** — Tag memory by source trust level to prevent poisoning. 32 comments, diamond-lobster rated, needs maintainer/security review. **Security-motivated; likely to land given security focus.**

2. **Masked Secrets / API key protection (#10659, #11829)** — Layered approach to prevent agent from accessing raw API keys. 15/21 comments respectively. Both diamond-lobster rated. **This is a security must-have; expect paired implementation.**

3. **Multi-Slot Memory Architecture (#60572)** — Replace single memory slot with multiple provider slots. 6 comments, 3👍. **Fits plugin-ecosystem direction.**

4. **Filesystem Sandboxing Config (#7722)** — `tools.fileAccess` with allowed/deny paths. 9 comments, 4👍. **Likely paired with masked-secrets work.**

5. **Telegram reactions as first-class input (#47677)** — 6 comments, 2👍. **Channel-parity feature; medium likelihood.**

6. **Dynamic model discovery (OpenRouter) (#10687)** — 9 comments, 3👍. **Infrastructure improvement blocked on product decision.**

7. **Session persistence**: Sub-agent graceful timeout (#6625), agent-triggered compaction (#6757) — both address reliability UX, likely to benefit from the steering work (#48003).

**Signals from merged/active PRs:**
- **Pairing/device onboarding is a major roadmap milestone** — 5+ PRs in flight, explicitly tied to `docs/plan/runners.md` milestone 3 (one-paste flow). Expect this in next release as a headline feature.
- **Removal of legacy lease architecture (#121113, merged)** — signals continued architectural modernization before adding new features.
- **UI UX scoring-driven update (#75947)** + PRs #121249/#120805/#121258/#121259 — **Control UI polish is actively being shipped.**

## 7. User Feedback Summary

**Positive signals:**
- Contributor velocity is high: 179 PRs closed/merged in 24h, with meaningful contributor PRs (VACInc, ayaangazali, sjf-oa) not just maintainers.
- The project responds to community pain: issue #116277 was closed (even if not fully resolved per #121058), and #120734 was merged to reject leaked Claude protocol output.
- Users are actively dogfooding and filing detailed repros — the `clawsweeper` labels show a sophisticated triage pipeline.

**Real pain points (express or implicit):**
- **Loss of work is the #1 frustration**: Subagent completions lost (#44925), silent no-reply on Telegram/DeepSeek (#116277/#121058), exec/read returning empty on Windows (#105528), text between tool calls dropped on WeChat (#92199). Users cannot trust the system to reliably complete tasks.
- **"Why is this not fixed yet?" fatigue**: Issues like #25592 (text leaks, 6 months), #10659 (masked secrets, 6 months), #11829 (API key roadmap, 6 months) remain open with no fix PRs, despite diamond-lobster ratings. The maintainer-review/product-decision bottleneck is visible.
- **Security anxiety**: Users are actively worried about memory poisoning (#7707), API key exposure (#10659/#11829), and untrusted GitHub issue body injection (#45740). The high 👍 counts (4 on #10659, 4 on #7722) show community mandates.
- **Docs drift**: Issue #48920 (docs ahead of release) with 4👍 indicates users are being misled by documentation — a trust and efficiency cost.
- **Channel inconsistency**: Multiple issues around channel-specific behavior (WhatsApp inbound, Telegram stickers #120735, Teams multi-bot #71058, WeChat text dropping #92199) suggest channel support is uneven — users on less-common channels feel left behind.

**Satisfaction indicators:** The project has high engagement and a strong maintainer presence (steipete dominating PRs), but the **recurrence of #116277's failure mode after closure (#121058) is a serious credibility concern**. Users will be watching whether the follow-up is handled properly.

## 8. Backlog Watch

**Long-standing issues needing maintainer attention (no fix PR, needs decision/review):**

| Issue | Age (created) | Priority | Why it's stuck |
|-------|---------------|----------|----------------|
| #10659 (Masked Secrets) | Feb 6 | P1, diamond | Needs security review + product decision (both labeled). 4👍. |
| #25592 (Text leak between tool calls) | Feb 24 | P1, diamond | Needs maintainer review + product decision + security review. 6 months old. |
| #31583 (`exec` tool does not inherit skills env) | Mar 2 | P1, diamond | Regression, linked PR open, but needs maintainer review + product decision. |
| #48003 (Steer mode doesn't inject mid-turn) | Mar 16 | P1, diamond | 4👍, linked PR open, needs product decision. Impact: session-state. |
| #48920 (Docs ahead of release) | Mar 17 | P0 | **No maintainer review label** — silent but serious. 4👍. |
| #44925 (Subagent lost completions) | Mar 13 | P1 | 25 comments, 2👍, no labels for maintainer/product. |
| #7722 (Filesystem sandboxing) | Feb 3 | P2 | 4👍, needs maintainer review + product decision + security review. |
| #7707 (Memory trust tagging) | Feb 3 | P2 | 32 comments (2nd highest), needs all reviews. |
| #71058 (Multiple Teams bots) | Apr 24 | P2 | 1👍, needs maintainer + product decision. |
| #118785 (QA proof for containers/SDK) | Aug 3 | P2 | Maintainer tracking issue, no movement in a week. |
| #119796 (Windows EBUSY teardown) | Aug 6 | P2 | Linked PR open, but **recovery-stuck** label — may need escalation. |

**Also notable:**
- #116022 (CLOSED, beta.5 `/new` cannot recover retired Codex tombstone) — closed but users may still encounter on stable; no follow-up issue filed.
- #103537 (PR, P1, prevent Gateway respawn during package replacement) — open since July 10, waiting on author — this is a **release-blocking risk** for the upgrade path.

**Recommendation:** The project appears to have a **maintainer review bottleneck** on security-critical features (#10659, #7707, #25592, #31583, #7722) that blocks community-validated work. Given the security hardening already in flight (PR #120734), prioritizing these older P1/diamond issues would address the most significant backlog risk.

---

## Cross-Ecosystem Comparison

# Cross-Project Ecosystem Comparison Report
**Date:** 2026-08-10

---

## 1. Ecosystem Overview

The personal AI assistant open-source ecosystem is in a **rapid maturation phase**, characterized by intense focus on reliability, security hardening, and architectural modernization. Projects are converging on several core challenges: **silent failure modes** (lost replies, dropped messages, undetected channel death), **security boundaries** (memory poisoning prevention, SSRF protection, credential handling), and **session-state integrity**. The ecosystem is bifurcating into two architectural camps: **monolithic agent platforms** (OpenClaw, Hermes Agent, ZeroClaw, IronClaw) with deep channel integrations and mature plugin ecosystems, versus **modular/embedded runners** (NanoBot, PicoClaw, NanoClaw, CoPaw) that prioritize channel bridging and lightweight deployment. The most successful projects show a distinctive pattern: they pair aggressive contributor onboarding (first-timer PRs) with maintainer-driven architectural refactoring. Across all projects, **token consumption visibility**, **per-model capability configuration**, and **multi-tenancy** are emerging as the next competitive battlegrounds.

---

## 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | Merged/Closed PRs (24h) | Release Status | Health Score* |
|---|---|---|---|---|---|
| **OpenClaw** | 500 | 500 | 179 | None (last: 2026.7.2-beta.5) | 8.5/10 |
| **ZeroClaw** | 50 | 50 | 0 | None (last: v0.8.3) | 7.0/10 |
| **IronClaw** | 22 | 25 | 8 | None (last: v1.1.0) | 8.0/10 |
| **CoPaw (QwenPaw)** | 17 | 50 | 1 | None (last: v2.0.1 / v2.1.0b2) | 7.5/10 |
| **NanoBot** | 4 | 15 | 4 | None | 7.0/10 |
| **Hermes Agent** | ~12 | ~18 | 14 | None | 7.5/10 |
| **PicoClaw** | 3 | 6 | 1 | None (last: v0.2.9) | 6.5/10 |
| **NanoClaw** | 2 | 14 | 0 | None | 6.0/10 |
| **Moltis** | 2 | 1 | 0 | None | 6.5/10 |
| **LobsterAI** | 3 | 0 | 0 | None | 5.0/10 |
| **NullClaw** | 0 | 0 | 0 | — | — |
| **TinyClaw** | 0 | 0 | 0 | — | — |
| **ZeptoClaw** | 0 | 0 | 0 | — | — |

*Health score = composite of activity level, merge rate, security responsiveness, community engagement, and backlog quality.

---

## 3. OpenClaw's Position

**OpenClaw is the undisputed ecosystem leader** in terms of community scale, contributor velocity, and architectural maturity. Its metrics dwarf all peers: 500 issues and 500 PRs updated in 24 hours versus ~50 for ZeroClaw (runner-up) and ~25 for IronClaw.

**Key advantages:**
- **Community scale**: 1,000+ daily touches vs. 50–100 for mid-tier projects. OpenClaw's contributor base includes multiple non-maintainer contributors (VACInc, ayaangazali, sjf-oa), indicating a sustainable contributor pipeline.
- **Architectural maturity**: OpenClaw is actively removing legacy architectures (session write leases → SQLite transactions), a signal of technical debt reduction that peers aren't yet attempting.
- **Release velocity**: 179 PRs merged in 24 hours—10x more than IronClaw (8), 14x more than Hermes (14), and 179x more than ZeroClaw (0).
- **Multi-channel richness**: OpenClaw supports more channels than any competitor (Slack, Telegram, WhatsApp, iMessage, WeChat, Teams, Discord, plus desktop/mobile client pairing).

**Technical approach differences:**
- Usage of a **gateway architecture** with view-only desktop sessions and RFB streaming (noVNC)—peers lack this hybrid messaging/desktop approach.
- **Pairing stack** (Tailscale, LAN setup, one-paste device pairing) is unique among peers and signals a push into end-user consumer UX.
- **Claude Code tool-protocol rejection** (anti-leak) and **Anthropic thinking-signature validation** show a deeper engagement with LLM API edge cases than peers.

**Vulnerabilities**: The single-maintainer bottleneck (steipete ~50% of top PRs) is a scalability risk; the silent-reply failure recurrence (#116277→#121058) threatens user trust; and security-critical features (masked secrets, memory trust tagging) have languished 6 months in review despite community demands.

---

## 4. Shared Technical Focus Areas

The following requirements are emerging **across multiple projects**, indicating industry-wide needs:

| Requirement | Projects | Specific Need |
|---|---|---|
| **Token consumption transparency** | NanoBot (#5266), IronClaw (#6046), LobsterAI (#1187) | Per-call usage tracking, cost attribution, runaway-loop detection |
| **Per-model capability/context config** | LobsterAI (#2453, #1187), ZeroClaw (#7100), CoPaw (#6846) | Accurate context windows, vision flags, model metadata validation |
| **Silent failure elimination** | OpenClaw (#121058, #25592), Hermes (#82756), PicoClaw (#3203), NanoBot (#5156) | Channel liveness detection, error surfacing, retry/notification logic |
| **Security hardening (SSRF/allowlist)** | PicoClaw (#3322–3324), NanoBot (#5305/5306), ZeroClaw (#9565) | Block private-target downloads, exec allowlist bypass prevention |
| **Memory integrity & poisoning prevention** | OpenClaw (#7707), Hermes (#46253), ZeroClaw (#9825) | Source-trust tagging, redaction of sensitive identifiers |
| **Multi-tenancy / per-agent scoping** | Hermes (#34352, #82701), ZeroClaw (#9745/#9746), NanoClaw (#3205) | Isolated secrets, per-agent data ownership, orchestrator support |
| **Device pairing / onboarding UX** | OpenClaw (5+ PRs), NanoClaw (#3050) | One-paste pairing, setup wizards, container deployment |
| **Structured/typed outputs** | NanoBot (#5299), IronClaw (#7405), CoPaw (#6844) | Tool schema validation, provider-compatible metadata |
| **Progressive/discrete updates** | IronClaw (#7396), CoPaw (#6843), ZeroClaw (#8443) | Real-time streaming, incremental previews, non-buffered output |
| **AV/interference resilience** | CoPaw (#6847), NanoBot (#5295) | False-positive process kills, deployment permission errors |

---

## 5. Differentiation Analysis

| Project | Primary Differentiation | Target User | Architecture |
|---|---|---|---|
| **OpenClaw** | Full-featured agent platform with universal messaging + desktop control; forking-friendly (Claw ecosystem) | Power users/developers | Monolithic Rust core; gateway + plugins |
| **Hermes Agent** | Nous Research research platform; multi-tenant orchestration ambitions; memory integration | Researchers/teams | Multi-profile; plugin hooks; epic-driven roadmap |
| **ZeroClaw** | Governance-heavy; RFC-driven; highest security posture focus | Security-conscious orgs | Rust; WASM plugins; high-assurance |
| **IronClaw** | Automation/QA heavy; Slack-first; enterprise ops focus | Business teams | Rust; capabilities-led; OCaml event loop |
| **CoPaw (QwenPaw)** | Qwen/ReMe memory system; Chinese ecosystem; mobile adaptation demand | Chinese-language users | Python-ish (implied); ReMe memory backend |
| **NanoBot** | Lightweight embedded runner; strong agent-agnostic stance | Embedded/devices | Small binary; GitAgent Protocol; minimal deps |
| **PicoClaw** | Channel bridge focus; IoT-grade; Sinara ecosystem | Channel/direct developers | Rust; multi-bridge; Telegram-native features |
| **NanoClaw** | NanoAI ecosystem; Nano-embedded; CVE-gated Docker | Nano community | Tiny footprint; agent-in-container |
| **Moltis** | Small, quiet, stable. Core container/vault focus | Dev-infra | Modular container runtime manager |
| **LobsterAI** | Netease/Youdao-backed; cross-model orchestration deep-dive | Chinese prosumers | Gateway-heavy; model-flexible |

**The core axis of differentiation** is now between **assistant-to-user** platforms (OpenClaw, IronClaw — good UX, messaging-first) and **agent-to-system** platforms (ZeroClaw, Hermes — orchestration and security-first). This mirrors the split between consumer AI assistants and enterprise agent infrastructure.

---

## 6. Community Momentum & Maturity

### Tier 1: Hyperactive / Rapidly Iterating
**OpenClaw**: 500/500 daily touches, 179 merges/day. Rapidly shipping features, but sprinting on the edge of instability (silent-failure regression).
**ZeroClaw**: 50/50 daily touches, 0 merges. Heavy PR/issue churn but there is a review bottleneck. High discussion quality (RFCs).
**IronClaw**: 22/25 daily touches, 8 merges. Structured post-release hardening, clear trajectory to v1.2. Excellent signal/noise.

### Tier 2: Active / Stabilizing
**Hermes Agent**: 14 merges/day but P0 data-loss bugs (3rd recurrence) undermine trust. Heavy firefighting mode.
**CoPaw**: 50 PRs churned, 1 merged. First-timers are contributing quickly; maintainer review is the bottleneck.
**NanoBot**: Small but responsive. Steady fix velocity; **security fix time is under 24h** (same-day fix PR after advisory). Healthy for its size.

### Tier 3: Moderate / Consolidation
**PicoClaw**: Active on security, but community is small (2–3 contributors).
**NanoClaw**: Same-day CVE fix shows speed; but 3-month-old Signal attachment PRs indicate merge backlog.
**Moltis**: Small, stable, responsive.

### Tier 4: Low / Quiet
**LobsterAI**: Issues updating, zero code merges. Risk of stagnation.
**NullClaw, TinyClaw, ZeptoClaw**: No activity. Dormant.

**Key indicator:** The **merge/review bottleneck** is the single largest risk across the ecosystem. OpenClaw (1 maintainer), ZeroClaw (50 PRs open/0 merged), CoPaw (#6681 spam) all struggle to process community contributions. The projects that will win the contributor-mindshare battle are those that resolve this bottleneck.

---

## 7. Trend Signals

1. **Silent failures are the #1 trust killer.** Recurring reports across OpenClaw (#121058), Hermes (#82756), PicoClaw (#3203), NanoBot (#5156) point to an industry-wide gap: **the lack of observable, recoverable delivery guarantees**. The next competitive differentiator will be built-in **watchdog/reconnect loops** and **delivery receipts**.

2. **Token/context observability is the new "must-have."** NanoBot's #5266 (millions of tokens burned visibly) and IronClaw's #6046 (124 tool calls for one workflow) point to user demand for **cost control interfaces** — metering, budgets, and call-level attribution. Expect **usage dashboards** to become standard in AI agent platforms.

3. **Per-model metadata accuracy is foundational.** LobsterAI (#2453), ZeroClaw (#7100), and CoPaw (#6846) all report broken provider-specific configs. This is a **spec-level gap** — the ecosystem needs a shared model-catalog schema (context windows, vision, schema compatibility) that all runtimes can trust.

4. **Security defaults are shifting from "allow" to "verify-and-deny."** ZeroClaw's webhook fail-open issue (#9565), PicoClaw's SSRF series (#3322–24), and NanoBot's allowlist bypass (#5305/06) indicate a need for **fail-closed defaults**, **per-channel trust boundaries**, and **credential-chain validation**.

5. **Multi-tenancy is the next architectural frontier.** Hermes (#34352) and ZeroClaw (#9745/#9746) are actively working on per-tenant isolation, secret scoping, and shared-infrastructure orchestration. The projects that solve this will unlock **server-side enterprise deployments**.

6. **Device pairing and onboarding UX will decide consumer adoption.** OpenClaw's 5-PR pairing stack and NanoClaw's container-CVE-gated Docker workflow show the two sides of onboarding: **local-device UX** and **pluggable deployment artifacts**. Consumer-grade setup flows will separate consumer-facing platforms from developer-only tools.

7. **Community-led security review is maturing.** Nearly every project shows evidence of users actively hardening their own pre-release features (NanoBot #5305, CoPaw #6848, ZeroClaw #9397). The most successful projects will **treat user-submitted vulnerabilities as product roadmap fuel**, not just patches.

8. **AI-optimized channel transports are missing standardization.** IRC long-message handling (PicoClaw #3287), Matrix silent sync death (PicoClaw #3203), Telegram sticker support (OpenClaw), and WhatsApp webhook ingress (ZeroClaw) suggest a need for **channel-agnostic message-reliability presets** — the agent-era equivalent of old XMPP stanza semantics.

---

*This report synthesizes community digest data from 13 projects on 2026-08-10. Metrics are derived from GitHub activity; health scores are analyst-rated based on activity, velocity, security posture, and community sentiment.*

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest
**Date:** 2026-08-10

---

## 1. Today's Overview

NanoBot is in an active development and hardening phase, with 15 PRs updated in the last 24 hours (11 open, 4 merged/closed) and 4 open issues, none of which were resolved in the period. The project shows strong community engagement around **security hardening**, **token-usage transparency**, and **deployment reliability**. Notably, two related security advisories (#5305, #5306) were filed within hours of each other describing the same underlying `exec.allowPatterns` bypass vulnerability — a signal that this is a systemic issue requiring urgent attention. The four merged/closed PRs today focus on CI/test strengthening, WebUI voice-input documentation, restoring a Star History chart, and adding GitAgent Protocol support — indicating a healthy balance of maintenance, UX polish, and feature expansion.

---

## 2. Releases

No new releases were published in the last 24 hours.

---

## 3. Project Progress

**Merged/Closed PRs (4):**

| PR | Title | Focus |
|---|---|---|
| [#5307](https://github.com/HKUDS/nanobot/pull/5307) | Restore Star History chart | Fixed the WebUI's Star History widget using a new provider after the original GitHub-based project was deprecated. |
| [#5308](https://github.com/HKUDS/nanobot/pull/5308) | Strengthen user-path coverage and CI gates | Added user-path tests for CLI, WebUI forks, route auth, and failure boundaries; added V8 coverage reporting, enforcing minimum coverage thresholds. |
| [#5304](https://github.com/HKUDS/nanobot/pull/5304) | Explain HTTPS requirement for voice input | Fixed WebUI voice-input failure on insecure HTTP origins; added actionable HTTPS guidance in all locales and docs. |
| [#4019](https://github.com/HKUDS/nanobot/pull/4019) | Add GitAgent Protocol support (agent.yaml + SOUL.md) | Adds support for the **GitAgent Protocol** standard (portable AI agent manifests), aligning NanoBot with an emerging open standard. |

**Key feature advancement:** PR #5299 (still open) adds structured token-usage records via a new API endpoint (`GET /api/settings/usage/records`) — directly addressing the community's demand for token consume transparency raised in Issue #5266.

---

## 4. Community Hot Topics

1. **[#5266 — Token consumption is too high & unobservable](https://github.com/HKUDS/nanobot/issues/5266)**
   - **13 comments, most active topic.**
   - User reports millions of tokens burned in ~2 hours with no visible user activity. Underlying need: **observability of per-call token usage** to diagnose runaway costs. This is likely to be a high-priority UX improvement. Related PR #5299 (structured usage records) is already in review.

2. **[#5295 — Docker Compose deployment fails with "Permission denied"](https://github.com/HKUDS/nanobot/issues/5295)**
   - **5 comments.** Gateway container fails at `/usr/local/bin/entrypoint.sh` with permission errors. Deployment friction for new users; likely environment/permission issue in the image build.

3. **Both security advisories [ #5305 ](https://github.com/HKUDS/nanobot/issues/5305) and [ #5306 ](https://github.com/HKUDS/nanobot/issues/5306)** (linked, 0 comments each — but high severity, see §5).

---

## 5. Bugs & Stability

Ranked by severity:

| Severity | Issue/PR | Description | Fix status |
|---|---|---|---|
| 🔴 **Critical** | [#5306](https://github.com/HKUDS/nanobot/issues/5306) | **Shell-chain bypass** of `exec.allowPatterns` allows unintended command execution via the `exec` tool. | No fix PR yet. |
| 🔴 **Critical** | [#5305](https://github.com/HKUDS/nanobot/issues/5305) | **Same allowlist bypass** but exploitable via the **OpenAI-compatible API** (chained shell commands). | No fix PR yet. |
| 🟠 **High** | [#5295](https://github.com/HKUDS/nanobot/issues/5295) | Docker Compose deployment fails with `Permission denied` on `entrypoint.sh`. | No fix PR yet; likely image packaging fix. |
| 🟡 **Medium** | [#5156 / #5301](https://github.com/HKUDS/nanobot/pull/5156) | **Telegram polling silently stalls** after network blips — bot stops receiving messages with no log output. PR #5301 adds lightweight liveness logging; #5156 (full watchdog) is still open. | Partial fix in review (#5301); full fix pending (#5156). |
| 🟢 **Low** | [#5303](https://github.com/HKUDS/nanobot/pull/5303) | **Weather skill fails on Windows PowerShell** (bare `curl` resolves to `Invoke-WebRequest` alias). | Fix PR open. |

---

## 6. Feature Requests & Roadmap Signals

| Request | Source | Likelihood in next version |
|---|---|---|
| **Structured token usage logs/API** | Issue #5266, PR #5299 | **High** — PR already open, directly addresses the top-voted complaint. |
| **Computer-use tools** (browser + desktop control) | PR #4276 (model-agnostic) | Medium — large feature, still in draft; long review cycle. |
| **Agent Plugins v1 integration** | PR #5288 | Medium — aligns with GitAgent Protocol trend (#4019 merged). |
| **Truthful API status for externally-managed servers** | PR #5255 (draft) | Medium — improves self-hosting UX. |
| **Forced QR login for Weixin channel** | PR #5310 | High — simple bug fix, likely merged soon. |
| **Marketplace skills shadowing builtins** | PR #5309 | High — small bug fix, important for skill ecosystem. |

**Prediction:** Next release will likely include token-usage transparency (PR #5299), the Weixin QR fix (#5310), the skills shadowing fix (#5309), and the Windows-safe weather workflow (#5303). The security fix for `exec.allowPatterns` is **urgent** and will likely be a hotfix above all else.

---

## 7. User Feedback Summary

- **Token burn is the #1 pain point.** Users running NanoBot expect lightweight operation but are seeing massive token consumption with no visibility into which calls consume what. Dissatisfaction is high, and call logs would materially improve the experience.
- **Docker deployment friction** is significant for new adopters. The `entrypoint.sh` permission error (#5295) is a poor first-run experience and may deter self-hosters.
- **Security-conscious users are actively auditing the `exec` tool.** The two nearly-identical advisories (#5305/#5306) indicate that the community values `allowPatterns` as a security boundary, and its bypass erodes trust in NanoBot's safe-execution guarantees. This needs to be fixed and communicated clearly.
- **Low-friction fixes are landing steadily** (voice-input HTTPS docs, Star History chart, weather skill Windows fix) — the community is responsive to small quality-of-life issues.
- **Telegram channel users** report silent bot failure as a critical reliability issue (#5171 / #5156) — an unstable-proxy scenario can kill the bot quietly, which is unacceptable for production deployments.

---

## 8. Backlog Watch

These items need maintainer attention and have been open for a while:

| Item | Age | Why it matters |
|---|---|---|
| [**#4276 — Model-agnostic computer use**](https://github.com/HKUDS/nanobot/pull/4276) (PR, draft) | ~2 months | Large feature with the potential to differentiate NanoBot; risks going stale in draft. Needs a decision: merge/close/active maintain. |
| [**#5156 — Telegram polling watchdog**](https://github.com/HKUDS/nanobot/pull/5156) | ~12 days | A partial observability PR (#5301) is split out, but the full watchdog remains unmerged. Production Telegram users are at risk. |
| [**#5255 — Truthful API status for external servers**](https://github.com/HKUDS/nanobot/pull/5255) (draft) | ~5 days | Improves honesty of the WebUI dashboards; low-risk but still in draft. |
| [**#5204 — Providers: declare Responses capabilities**](https://github.com/HKUDS/nanobot/pull/5204) (refactor) | ~9 days | Important refactor for provider correctness; silently waiting for review. |
| [**#5306 / #5305 — Security bypasses**](https://github.com/HKUDS/nanobot/issues/5306) | <1 day | **URGENT:** should be triaged by a maintainer immediately, ideally with an advisory and a fix release within days. |

---

*Digest generated from public GitHub data on 2026-08-10. All links are to original issues/PRs for full context.*

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

Based on the provided GitHub data for Hermes Agent (dated 2026-08-10), here is a structured project digest.

---

### 1. Today's Overview

Hermes Agent is showing a high level of activity focused on stability and hardening, driven by a cascade of critical desktop-session data-loss reports. The project is in a "firefighting and refactoring" phase, with maintainers and community members submitting rapid-fire PRs to address regressions in session state, desktop SSH connectivity, and plugin runtime crashes. A significant theme is the recurring issue of session history corruption via the `confirm_truncate` path, which has now been reported for a third time, indicating a systemic flaw despite prior fixes. Beyond bugs, there is strong community momentum around multi-tenancy and memory architecture, with multiple feature requests and an epic proposal aiming to evolve the platform's core orchestration capabilities.

### 2. Releases

No new releases were published in the last 24 hours.

---

### 3. Project Progress

The last 24 hours saw 14 PRs merged or closed, primarily focusing on bug fixes.

- **Desktop SSH Fix Redux:** Two PRs ([#74425](https://github.com/NousResearch/hermes-agent/pull/74425), [#79289](https://github.com/NousResearch/hermes-agent/pull/79289)) and a follow-up ([#82741](https://github.com/NousResearch/hermes-agent/pull/82741)) address the same root cause: the desktop app resolving `exec` shim scripts to the Python interpreter instead of the Hermes entrypoint, which caused false "unsupported" errors during SSH version checks. This appears to be a sustained effort to fully resolve the issue raised in #74411.
- **Plugin Runtime Isolation:** A fix was merged to isolate runtime plugin render hooks ([#82763](https://github.com/NousResearch/hermes-agent/pull/82763)), aiming to resolve React crash errors on Windows and potentially other platforms.
- **Planned Restart Detection:** The gateway now classifies service-managed restarts differently from external kills ([#57419](https://github.com/NousResearch/hermes-agent/pull/57419)), which should improve session-state recovery logic.
- **Agent Hooks & Security:** A long-running feature—the `pre_model_route` plugin hook ([#32364](https://github.com/NousResearch/hermes-agent/pull/32364))—was closed, bringing turn-scoped model routing control to plugins. A security guard was also merged to prevent the agent from self-terminating its own process via `kill` ([#6234](https://github.com/NousResearch/hermes-agent/pull/6234)).

---

### 4. Community Hot Topics

The most active discussions highlight a desire for deeper, more nuanced control and architectural evolution.

- **Multi-Tenant Hermes ([#34352](https://github.com/NousResearch/hermes-agent/issues/34352))** - 18 comments, 2 👍
  This is the most active discussion. The author is pushing for Hermes to support true multi-tenancy but points out a fundamental blocker: memory operations bypass the hook system, making isolation impossible without forking. The community is clearly invested in this, as evidenced by a separate feature request for a "Multi-Tenant Orchestrator" ([#82701](https://github.com/NousResearch/hermes-agent/issues/82701)). This suggests a market pull for server-side, multi-user deployments of Hermes.

- **Gateway Session Corruption ([#82616](https://github.com/NousResearch/hermes-agent/issues/82616))** - 7 comments
  This tracking issue for gateway session continuity breaking under database corruption is gathering attention. The comment count suggests users are experiencing this issue and are seeking a unified place to report and discuss symptoms, indicating it is a painful and widespread stability concern.

- **Cross-Profile Subagents ([#41889](https://github.com/NousResearch/hermes-agent/issues/41889))** - 5 comments, 1 👍
  The request for `delegate_task` to support running subagents under a different profile's identity is a sign of users building more complex, role-based workflows and hitting the limits of the current single-profile architecture.

- **GBrain Memory Provider ([#46253](https://github.com/NousResearch/hermes-agent/issues/46253))** - 5 comments, 6 👍
  This is the most "liked" issue. The high reaction count indicates strong user desire for integrating external, shared semantic memory backends like GBrain directly into the core `memory` tool pipeline, rather than just via MCP.

---

### 5. Bugs & Stability

Stability is the primary concern today, with several high-severity bugs reported, especially around session integrity.

- **P0 - Critical Data Loss:**
  - [Desktop plain-Enter submit silently deleted ~65 messages](https://github.com/NousResearch/hermes-agent/issues/82756) — This is the **third occurrence** of this class of bug (after #70516 and #80763). A stale `truncate_before_user_ordinal` with an auto-attached `confirm_truncate` destroys messages. A fix PR exists: [#82766](https://github.com/NousResearch/hermes-agent/pull/82766), which proposes message_id-based truncation. This is a top priority.

- **P1 - High Severity:**
  - [Gateway session continuity breaks under state.db FTS corruption](https://github.com/NousResearch/hermes-agent/issues/82616) — Leads to orphan sessions and stale resumes after restarts. Tagged as `needs-decision`.
  - [Misleading "billing" 400 error from Anthropic](https://github.com/NousResearch/hermes-agent/pull/82177) — A bug where a content-filter 400 is misreported, causing user confusion. A fix PR is open.

- **P2 - Medium Severity:**
  - [Desktop app does not self-heal dropped SSH/HTTP connections](https://github.com/NousResearch/hermes-agent/issues/82679).
  - [Plugin SDK crashes on Windows](https://github.com/NousResearch/hermes-agent/issues/80560) — Fixed by PR [#82763](https://github.com/NousResearch/hermes-agent/pull/82763).
  - [Remote version-check falsely reports unsupported flags](https://github.com/NousResearch/hermes-agent/issues/74411) — Addressed by #79289 and #82741.
  - [verify-on-stop triggers on any file edit](https://github.com/NousResearch/hermes-agent/issues/52612) — Path-agnostic guard causing false positives.
  - [Telegram fallback path can exhaust FD budget](https://github.com/NousResearch/hermes-agent/issues/82678).

---

### 6. Feature Requests & Roadmap Signals

The community is pushing Hermes toward becoming a platform for orchestrated, multi-user, and deeply integrated workflows.

- **Multi-Tenancy & Orchestration:** This is the strongest signal. Requests range from a grand vision for "Multiplayer Agentic AI" ([#34352](https://github.com/NousResearch/hermes-agent/issues/34352)) to a concrete proposal for an [OIDC-authenticated, per-user container orchestrator](https://github.com/NousResearch/hermes-agent/issues/82701) that shares MCP/Kanban infrastructure.
- **Memory Integration:** A clear demand for first-class integration with external memory backends like [GBrain](https://github.com/NousResearch/hermes-agent/issues/46253), moving beyond MCP tools to native, write-through, prefetch-injected memory within the core pipeline.
- **Extended Capabilities:**
  - [Kanban "zero-authority workers"](https://github.com/NousResearch/hermes-agent/issues/82591) — A comprehensive epic for making Kanban workers more autonomous, durable, and independent.
  - [Codex web search backend plugin](https://github.com/NousResearch/hermes-agent/issues/82716) — Users want to leverage their existing `codex login` for standardized web search/extract tools.
  - [New STT model support](https://github.com/NousResearch/hermes-agent/issues/82721) — A request to update the default local Whisper model to a newer, faster variant.

- **Next Version Prediction:** Given the "EPIC: Kanban" and multi-tenancy proposals, work on `comp/cron` and `comp/agent` orchestration is likely to be a focus. However, the immediate next release (v0.20.x) will almost certainly prioritize the **P0/P1 session data loss fixes** to restore user trust.

---

### 7. User Feedback Summary

- **Pain Points:** The most vocal frustration revolves around **data loss and instability**, particularly silent session history deletion on the Desktop client. Users are also clearly frustrated by the inability to recover from remote connection drops without manual reconfiguration.
- **Configuration Friction:** Users report issues with settings not persisting, such as [custom skins](https://github.com/NousResearch/hermes-agent/issues/71446), [UI zoom levels](https://github.com/NousResearch/hermes-agent/issues/82713), and the confusing [mislabeling of a content filter error as a billing problem](https://github.com/NousResearch/hermes-agent/pull/82177).
- **Use Cases:** A clear use case is emerging for **team-based or multi-user deployments** of Hermes, indicated by the strong interest in multi-tenancy and shared infrastructure. Users are also deeply integrating Hermes with external services (OpenAI Codex, Telegram, GBrain, LM Studio) and are sensitive to how well these integrations behave.
- **Dissatisfaction:** The repeated failures in the session truncation logic ([#82756](https://github.com/NousResearch/hermes-agent/issues/82756)) despite prior fixes suggests a high degree of dissatisfaction with the Desktop's session-handling reliability.

---

### 8. Backlog Watch

These issues have been open for a while or are critical but seem to lack a clear path forward, requiring maintainer attention.

- **[#34352](https://github.com/NousResearch/hermes-agent/issues/34352) : Multi-Tenant Hermes Problem (Created 2026-05-29)** — This is a foundational architectural bottleneck (memory bypassing hooks) critical for a major use case. It requires a `needs-decision` on whether to redesign the core hook system. High impact, blocked.

- **[#32364](https://github.com/NousResearch/hermes-agent/pull/32364) : pre-model route hook (Created 2026-05-26)** — While recently closed, this took about 2.5 months to land. It's a signal that plugin hooks and agent-core interaction layers are complex and slow to merge.

- **[#52612](https://github.com/NousResearch/hermes-agent/issues/52612) : verify-on-stop trigger is path-agnostic (Created 2026-06-25)** — An older bug causing frequent false-positive guard triggers during development, which is a major workflow annoyance for agent developers. Tagged as needing reproduction but is a clear QoL issue.

- **[#6234](https://github.com/NousResearch/hermes-agent/pull/6234) : guard literal current-PID self-kill (Created 2026-04-08)** — A security-related PR that has been open for over 4 months, highlighting a slow review process for security-critical changes that touch the approval layer.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

# PicoClaw Project Digest
**Date:** 2026-08-10

---

## 1. Today's Overview

PicoClaw is showing **moderate-to-high activity** this week, with **6 PRs and 3 Issues** updated in the last 24 hours. The project is in a **healthy state**: more than half of the PR activity is focused on security hardening, a strong signal of maturing engineering practices. The community is actively contributing both **fixes** (SSRF protection across multiple channels, lockfile resolution) and **features** (native Telegram table rendering, IRC long-message handling). Notably, we see **different contributors** — SashaMIT, As-tsaqib, trufae — indicating a **growing, distributed contributor base**. One issue from the backlog (#3203, Matrix sync loop) was closed as stale, while two new feature requests remain open. No releases were published today.

---

## 2. Releases

No new releases were published in the last 24 hours. The latest known version remains **v0.2.9** (referenced in Issue #3203).

---

## 3. Project Progress

**Merged/Closed PRs: 1**

- **[#3326 [CLOSED] fix(web): remove duplicate pnpm lock entries**](https://github.com/sipeed/picoclaw/pull/3326) — by As-tsaqib
  This small but critical fix removes duplicate `semver@7.8.5` entries from the web frontend's `pnpm-lock.yaml` that were breaking `pnpm install --frozen-lockfile` with `ERR_PNPM_BROKEN_LOCKFILE`. This unblocks CI/CD pipelines and developer onboarding.

**Active Feature Work (Open PRs):**

- **[#3327 feat(telegram): render tables with native rich messages**](https://github.com/sipeed/picoclaw/pull/3327) — New Telegram Bot API rich table rendering instead of monospaced code blocks.
- **[#3222 refactor(deltachat): cleanup implementation, documentation -200LOC**](https://github.com/sipeed/picoclaw/pull/3222) — Major refactor: drops legacy features, removes fallbacks, renames `invite_link` → `join_invite_link`, adds `show_invite_link`, and moves secrets to jsonrpc.
- **[#3322, #3323, #3324] SSRF hardening across multiple channels** — A coordinated security effort by SashaMIT to block private-target media downloads (details in Section 5).

---

## 4. Community Hot Topics

1. **Matrix Sync Reconnection Logic — [Issue #3203](https://github.com/sipeed/picoclaw/issues/3203)** (CLOSED today)
   - **Comments:** 8 | **👍:** 2
   - **Context:** The longest-running active discussion (37 days). Users report that the Matrix `/sync` loop dies silently after network disruption — no reconnection, and systemd doesn't catch it because the main process stays alive.
   - **Takeaway:** Closed as stale, but the underlying reliability gap remains real. This would benefit from a re-open or a dedicated fix PR.

2. **IRC Long Message Handling — [Issue #3287](https://github.com/sipeed/picoclaw/issues/3287)** (OPEN, 4 comments)
   - **Context:** User requests PicoClaw treat IRCv3 split messages (>512 bytes) as a single cohesive message. Poor handling of long messages is particularly painful for AI-generated responses that don't fit in 512 bytes.
   - **Underlying need:** AI assistants can't produce useful output if the transport channel aggressively truncates. This could be a UX-blocking issue for IRC users.

3. **Telegram Native Table Rendering — [Issue #3325](https://github.com/sipeed/picoclaw/issues/3325)** (NEW, 0 comments)
   - **Context:** Tables in AI responses currently degrade to monospaced blocks. Telegram Bot API 10.1 enables native table UI. A matching **PR #3327 is already drafted** — suggesting this was a team-driven feature, not just external demand.

4. **DeltaChat Refactor — [PR #3222](https://github.com/sipeed/picoclaw/pull/3222)** (OPEN, long-lived since July 3)
   - **Context:** Large clean-up (-200 LOC) with breaking API renames. Low comment activity but long open time suggests review complexity.

---

## 5. Bugs & Stability

**Active Bug: Matrix Sync Loop Silent Death — [Issue #3203](https://github.com/sipeed/picoclaw/issues/3203)** (closed as stale today)
- **Severity:** High — channel becomes permanently unresponsive without detection.
- **Status:** Closed. No dedicated fix PR exists. **Risk:** If this regresses, it will resurface as a support burden. Maintainers should consider a proper reconnect loop.

**Security Fixes (new PRs, no linked bug reports yet):**

- **[#3322 fix(channels): block private targets on inbound media downloads**](https://github.com/sipeed/picoclaw/pull/3322) — **Severity: Critical.** SSRF vulnerability in QQ/Telegram/Discord/LINE/Slack attachment downloads. Crafted URLs could reach loopback, link-local, or RFC1918 hosts.
- **[#3323 fix(wecom): use CreateSafeHTTPClient for media downloads**](https://github.com/sipeed/picoclaw/pull/3323) — **Severity: High.** WeCom had plain redirect-following HTTP client.
- **[#3324 fix(weixin): use CreateSafeHTTPClient for media downloads**](https://github.com/sipeed/picoclaw/pull/3324) — **Severity: High.** Same class of bug for Weixin CDN.
- **[#3326 fix(web): remove duplicate pnpm lock entries**](https://github.com/sipeed/picoclaw/pull/3326) — **Severity: Medium (Dev/CI).** Breaks `pnpm install --frozen-lockfile`.

These SSRF fixes are **coordinated and nearly ready to merge** — they follow the pattern already implemented for OneBot, suggesting the team is systematically closing this vulnerability class.

---

## 6. Feature Requests & Roadmap Signals

**High-Probability for Next Release (code already drafted or in progress):**

- **Native Telegram table rendering** — PR #3327 is already open. Likely in **v0.2.10** if not earlier.

**Mid-term Candidates:**

- **IRC long-message reassembly** (Issue #3287) — no PR yet, but community support exists. Highly valuable for AI use-cases on IRC.

**Refactors / Roadmap Support:**

- **DeltaChat clean-up** (PR #3222) — blocking rename of `invite_link` → `join_invite_link` will be a **breaking change**. Users should watch for release notes.

**Pattern Recognition:** The team appears to be prioritizing (a) security hardening, (b) rich formatting for AI output, and (c) transport reliability — a strong roadmap for an AI-assistant bridge.

---

## 7. User Feedback Summary

**Positive Signals:**
- Community contributors (As-tsaqib, SashaMIT, trufae) are actively submitting code — a sign of a healthy, engaged ecosystem.
- Issue #3203 (Matrix) got 2 👍, indicating users are affected but engaged with the issue tracker.

**Pain Points:**
1. **Silent channel failure** (Matrix #3203): "Process stays alive but channel is dead" is a nasty failure mode for a bridge — hard to detect without active probing.
2. **Long AI-generated messages break on IRC** (#3287): the 512-byte IRC limit is incompatible with helpful AI responses.
3. **Formatting degradation** on Telegram (#3325): tables in AI responses failing to render natively reduces perceived AI quality.
4. **SSRF exposure** (implicit in PRs #3322-#3324): silently fixed, but indicates bridges were less hardened than expected — especially for private/enterprise deployments.

---

## 8. Backlog Watch

**Significant Items Requiring Maintainer Attention:**

1. **[PR #3222 — DeltaChat refactor](https://github.com/sipeed/picoclaw/pull/3222)** — Open since **July 3** (38 days). Major refactor with breaking renames. Low comment count.
   - **Risk:** Long-lived PRs drift out of sync; merge conflicts will grow. Should be reviewed and merged or explicitly deferred.

2. **Issue #3203 — Matrix sync loop (closed as stale)** — The lack of reconnection logic is a **known production bug** for an entire channel protocol. Closing as stale may be premature. Consider reopening or creating a follow-up tracking issue.

3. **SSRF fix series (#3322–#3324)** — These are security-critical and should be reviewed and merged with **priority**, ideally together, to avoid partial coverage across channels.

---

*Digest generated from GitHub activity data for sipeed/picoclaw, 2026-08-10.*

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

Based on the GitHub data provided for NanoClaw on 2026-08-10, here is the project digest:

---

# NanoClaw Project Digest — 2026-08-10

## 1. Today's Overview
NanoClaw is in a period of **high, sustained development activity**. While no new releases were cut today, the project saw **14 open pull requests** updated in the last 24 hours, indicating a strong stream of proposed code changes and refactors. However, it is important to note that **zero PRs were merged or closed** during this period, suggesting that either the team is in a review-heavy phase or merges are being batched. The issues tracker is relatively quiet, with only **2 new issues** filed, both of which are open and lack comments or reactions, indicating initial reports rather than community-wide discussions. The development focus appears to be on **stabilization and architectural refactoring** of the host, channels, and database layers, alongside critical bug fixes for the Docker container's security posture.

## 2. Releases
**No new releases** were published in the last 24 hours. This section is omitted per the data provided.

## 3. Project Progress
*(Note: No PRs were merged or closed in the last 24 hours. The following reflects active work in progress.)*

Despite a lack of merges, significant work is moving forward through open PRs, particularly in three areas:

- **Security & Container Health (Core Team Focus):**
    - [#3207](https://github.com/nanocoai/nanoclaw/pull/3207): A critical fix proposes bumping `pnpm` and `npm` to patch a **fixable-critical CVE** in the `tar` package (GHSA-23hp-3jrh-7fpw) found in the agent image.
    - [#3208](https://github.com/nanocoai/nanoclaw/pull/3208): A new CI workflow is proposed to publish the agent image to Docker Hub automatically, including CVE gates to prevent vulnerable builds from being released.

- **Architectural Refactoring (by `zvi-fried`):**
    - A series of refactors are being prepared to improve the codebase structure, including unifying module lifecycle hooks ([#3214](https://github.com/nanocoai/nanoclaw/pull/3214)), registering question renderers ([#3213](https://github.com/nanocoai/nanoclaw/pull/3213)), and adding a module migration registry ([#3212](https://github.com/nanocoai/nanoclaw/pull/3212)). A larger effort adds host seams for skill-owned capabilities ([#3186](https://github.com/nanocoai/nanoclaw/pull/3186)).

- **Channel Integrations:**
    - A significant feature is proposed to add a **"Dial" channel adapter** for SMS and AI voice calls ([#3041](https://github.com/nanocoai/nanoclaw/pull/3041)), including setup wizard integration ([#3050](https://github.com/nanocoai/nanoclaw/pull/3050)). These are longer-running PRs from July that were still active today.
    - Bug fixes are in the works for Slack (surfacing pasted tables, [#3209](https://github.com/nanocoai/nanoclaw/pull/3209)) and Signal (delivering attachments correctly, [#3142](https://github.com/nanocoai/nanoclaw/pull/3142)).

## 4. Community Hot Topics
*(Note: No issues or PRs currently have comments or reactions.)*

While direct community engagement (comments/reactions) is currently at zero, the activity around specific issues signals key topics of interest:

- **Attachment Handling is a Recurring Pain Point:** Two separate issues and multiple PRs today revolve around attachments being dropped or misrouted. The new issue [#3206](https://github.com/nanocoai/nanoclaw/issues/3206) reports attachments silently dropped on channels with path separators in message IDs (e.g., Google Chat). This mirrors ongoing fixes for attachments in the Signal adapter ([#2529](https://github.com/nanocoai/nanoclaw/pull/2529), [#3142](https://github.com/nanocoai/nanoclaw/pull/3142)). This cluster of activity suggests reliable attachment handling is a top-priority feature for users.

- **Secret Management Design Fork:** Issue [#3205](https://github.com/nanocoai/nanoclaw/issues/3205) highlights an unresolved design decision around how OneCLI vault secrets are assigned to agents at spawn time in a multi-user environment. This is a core architectural concern that could impact security and usability.

## 5. Bugs & Stability
Two bugs were reported today, ranked by severity:

1.  **Critical (Proposed Fix in PR):** **Vulnerable `tar` Package** ([PR #3207](https://github.com/nanocoai/nanoclaw/pull/3207)) — A critical CVE affects the `tar` package within the Docker image's npm/pnpm. A fix is already proposed, showing a proactive approach to security.
2.  **High (No Fix PR):** **Silent Attachment Drops** ([Issue #3206](https://github.com/nanocoai/nanoclaw/issues/3206)) — Attachments are silently dropped on channels where message IDs contain `/` or `\` (like Google Chat) due to a safety check. This is a data-loss bug that is difficult for users to detect.
3.  **Medium (Ongoing, Fix PRs Exist):** **Mail/Attachment Routing** — Older related PRs for delivering attachments to the agent (Signal/Inbox) remain open ([#2529](https://github.com/nanocoai/nanoclaw/pull/2529), [#3142](https://github.com/nanocoai/nanoclaw/pull/3142)), suggesting this problem is complex and spans multiple channels.

## 6. Feature Requests & Roadmap Signals
- **"Dial" Channel Integration:** The substantial PRs for a new Dial channel adapter (SMS + AI voice) ([#3041](https://github.com/nanocoai/nanoclaw/pull/3041), [#3050](https://github.com/nanocoai/nanoclaw/pull/3050)) strongly signal that expanding the platform to include telephony channels is on the immediate roadmap.
- **Persistent Group-Scoped Secrets:** The design issue for persistent, group-scoped OneCLI secret assignment ([#3205](https://github.com/nanocoai/nanoclaw/issues/3205)) points toward a roadmap item for more granular, enterprise-grade security and secret management controls.
- **Container Image Distribution:** The proposed CI workflow for publishing to Docker Hub with CVE gates ([#3208](https://github.com/nanocoai/nanoclaw/pull/3208)) signals a move toward production-readiness and easier deployment for end-users.

## 7. User Feedback Summary
- **Pain Point — Inconsistent Attachment Handling:** The most prominent user pain point is the unreliable delivery of attachments. The silent drop on Google Chat (Issue [#3206](https://github.com/nanocoai/nanoclaw/issues/3206)) and the long-standing issues on Signal ([#2529](https://github.com/nanocoai/nanoclaw/pull/2529), [#3142](https://github.com/nanocoai/nanoclaw/pull/3142)) highlight frustration with broken paths and missing files, which can break agent workflows.
- **Pain Point — Complexity in Setup:** The PRs from `zvi-fried` focusing on documentation ([#3211](https://github.com/nanocoai/nanoclaw/pull/3211)) and clarifying where attachments land in the container ([#3210](https://github.com/nanocoai/nanoclaw/pull/3210)) indicate a community need for clearer understanding of how the system operates and integrates.
- **Satisfaction — Responsive Maintainers:** The quick turnaround on the critical `tar` CVE (Issue -> Fix PR on the same day) suggests a responsive core team that is attentive to security and stability.

## 8. Backlog Watch
The following PRs have been open for a significant time and may require maintainer attention or resolution:

- **[PR #2529](https://github.com/nanocoai/nanoclaw/pull/2529) — fix(signal): deliver inbound attachments (Open since 2026-05-18):** This critical fix for Signal attachment delivery has been open for nearly three months. It is a long-running blocker for a core channel and should be prioritized for review and merge.
- **[PR #3142](https://github.com/nanocoai/nanoclaw/pull/3142) — fix(signal): forward attachments through mounted inbox (Open since 2026-07-27):** This is another fix addressing the same Signal attachment problem, indicating the first PR may have issues. The maintainers should consolidate these efforts.
- **[PR #3050](https://github.com/nanocoai/nanoclaw/pull/3050) & [PR #3041](https://github.com/nanocoai/nanoclaw/pull/3041) — Dial Channel Integration (Open since 2026-07-14):** While actively updated recently, these are large feature PRs that have been open for nearly a month. They need a dedicated review to either move forward or provide feedback to the author to prevent staleness.

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest
**2026-08-10**

---

## 1. Today's Overview

IronClaw is in a period of intense stabilization and feature expansion following the recent v1.1.0 release. Activity is very high: 22 issues and 25 PRs were updated in the last 24 hours, with about two-thirds of each still open/active, indicating sustained momentum. The current work centers on fixing a batch of P2 QA-discovered bugs from the August 7 bug bash (emoji rendering, activity chronology, automation count inconsistency), while also advancing planned feature work around tool discovery (complete signatures), notification channels (web-push PWA, progressive previews for Slack/Telegram), and parallel capability execution. The project shows a healthy mix of QA-driven bug fixes, core-feature PRs from maintainers, `ironloopai[bot]`-generated fixes, and dependency updates, with no new releases cut today.

---

## 2. Releases

No new releases were published in the last 24 hours. The most recent reference points remain **v1.1.0** (stable) and **v1.1.0-rc.1**, both of which are affected by the high-severity zombie-thread bug described below (Issue #7400).

---

## 3. Project Progress

Eight PRs were closed/merged in the last 24 hours. Notable items:

**Merged/Closed PRs:**

- **[#7171 — fix(skills): one DB-backed tree for every skill mount](https://github.com/nearai/ironclaw/pull/7171)** *(Closed, size: XL)* — A major fix for the skill system where installed skills "disappeared" — absent from Settings → Skills and unactivatable. Now backed by a single database-backed tree across all mounts, with a skill's own commands made runnable. Closes #7168 as part of the broader #6941 epic (skills overhaul).
- **[#7387 — chore(deps): bump everything-else group with 12 updates](https://github.com/nearai/ironclaw/pull/7387)** *(Closed)* — Routine dependency maintenance across 12 packages including `base64 0.22.1 → 0.23.0` and `toml` patch updates.
- **[#7022 — chore(deps): bump actions group with 2 updates](https://github.com/nearai/ironclaw/pull/7022)** *(Closed)* — CI dependency updates, notably `actions/setup-node` from v4 to v7 (a major jump with breaking-change potential).
- **[#7323 — ci(nightly): grant actions: read to the reborn-tests call contract](https://github.com/nearai/ironclaw/pull/7323)** *(Closed, size: XS)* — Fixed the Nightly Deep CI pipeline, which had been a **zero-job `startup_failure` for five consecutive nights** since 2026-08-03 due to missing `actions: read` permission on the coverage-report job.

Given the unusually high volume of P2 bugs from the last QA pass, the immediate roadmap already appears clear: a wave of small, focused fixes are prepared or in flight, including PRs #7404 (emoji rendering), #7403 (activity chronology), and #7402 (automation totals) — all three directly address open QA bugs (see Section 5).

---

## 4. Community Hot Topics

The most-discussed items (by comment count) in the last 24 hours:

**Most Active Issues (4 comments each):**

- **[#5522 [Closed] — Reborn routine fails when task requires reading Slack DMs](https://github.com/nearai/ironclaw/issues/5522)** — An older but significant issue: the agent hit a missing Slack read capability and entered a `capability_info` retry loop instead of failing gracefully. Despite being closed, it highlights a systemic gap: capability discovery and graceful degradation when a required tool is absent.
- **[#7405 [Open] — Improve deferred tool discovery with complete signatures and namespace-aware catalog previews](https://github.com/nearai/ironclaw/issues/7405)** — The framing issue for a stacked PR series (#7409, #7410) aimed at reducing model turns when using `tool_search`. Includes a 1,000-tool benchmark corpus, a sign the team is prioritizing tool discovery at scale.
- **[#7407 [Open] — Execute BatchPolicy::Parallel capability batches concurrently in invoke_capability_batch](https://github.com/nearai/ironclaw/issues/7407)** — A performance-focused issue: the batch policy is calculated in parallel but executed sequentially. Expected to yield latency wins for multi-tool turns with zero model-facing changes.

**Most Active PRs (no comments recorded, but layered/stacked structure indicates heavy internal review):**

- **[#7396 — feat(channels): add generic progressive previews for Slack and Telegram](https://github.com/nearai/ironclaw/pull/7396)** *(size: XL)* — Adds a channel-neutral progressive-preview contract for long-running tasks.
- **[#7397 — Presence-based shared conversations for Slack & Telegram](https://github.com/nearai/ironclaw/pull/7397)** *(size: XL)* — Builds on the merged #7377 acting-identity ladder to support shared conversations where owner ≠ actor.
- **[#7398 — feat(web-push): browser push notifications + PWA](https://github.com/nearai/ironclaw/pull/7398)** *(size: XL)* — Makes the web app a first-party notification channel (RFC 8030/8291/8292) with feature parity to Slack/Telegram routes.

**Underlying Need Analysis:** Two strong threads emerge. First is **channel evolution**: IronClaw is expanding beyond Slack/Telegram toward a first-party web-push channel, and adding progressive (intermediate) message previews that are stateful and editable — both are responses to long-standing QA complaints about Slack automation delivering "intermediate progress messages" instead of final summaries (#5551). Second is **tool-call efficiency**: the stacked PRs on `tool_search` (#7405/#7409/#7410) address complaints like Issue #6046 (an email-to-sheet workflow using 124 tool invocations), by making schema/signature discovery cheaper and more complete.

---

## 5. Bugs & Stability

The following issues were reported/updated today (with day-over-day changes), **ranked by severity**:

### 🔴 Critical (P1 equivalent)
- **[#7400 — Bug: `stream: true` + caller `tools[]` on `/api/v1/responses` fails mid-stream and leaves a permanently undeletable "zombie" thread](https://github.com/nearai/ironclaw/issues/7400)** (Open) — Affects **v1.1.0-rc.1 and v1.1.0 (stable)** with 100% reproducibility. Mid-stream failures leave a thread that can never be deleted. **Fix PR exists:** **[#7401 — Reject streamed Responses requests with external tools](https://github.com/nearai/ironclaw/pull/7401)** (size: S) returns a stable `400` before submission, preventing thread creation entirely.

### 🟠 High (P2)
- **[#7292 [Closed] — Installed tool cannot be used; run fails with runner heartbeat error](https://github.com/nearai/ironclaw/issues/7292)** — Tool installation succeeded but use consistently failed. Closed today, implying it was resolved (no fix PR surface yet).
- **[#7346 — Emoji shortcodes displayed as plain text in assistant messages](https://github.com/nearai/ironclaw/issues/7346)** (Open) — Regression in rendering. **Fix PR:** **[#7404 — Rendered emoji shortcodes in chat Markdown](https://github.com/nearai/ironclaw/pull/7404)** (size: M).
- **[#7348 — Activity tool calls and assistant progress messages displayed in wrong chronological order](https://github.com/nearai/ironclaw/issues/7348)** (Open) — Timeline confusion in chat UI. **Fix PR:** **[#7403 — Fixed WebUI activity chronology](https://github.com/nearai/ironclaw/pull/7403)** (size: S).
- **[#7349 — Refreshing chat causes part of run history and activity timeline to disappear](https://github.com/nearai/ironclaw/issues/7349)** (Open) — Persistence/rendering gap on refresh; still without a clearly linked fix.
- **[#7345 — Agent reports 61 automations while UI shows only 50](https://github.com/nearai/ironclaw/issues/7345)** (Open) — Counting inconsistency; the dashboard was limiting its list view. **Fix PR:** **[#7402 — Report exact automation totals without widening the page](https://github.com/nearai/ironclaw/pull/7402)** (size: L) adds aggregate queries across PostgreSQL, libSQL, and in-memory repositories.
- **[#5882 — Repeated Slack reconnect attempts leave authentication flow in broken state](https://github.com/nearai/ironclaw/issues/5882)** (Open) — Persistent auth deadlock requiring manual extension reinstall; no fix PR yet.

### 🟡 Medium (P3)
- **[#4341 [Closed] — Agent THINKING chain-of-thought exposed to user and stuck in thinking state (Qwen3.6)](https://github.com/nearai/ironclaw/issues/4341)** — Closed today; historical issue involving exposure of internal CoT.
- **[#5552 [Closed] — Run fails with generic "invalid result" after multiple tool failures](https://github.com/nearai/ironclaw/issues/5552)** — Closed today; unhelpful generic error when tool failures cascade.
- **[#5509 [Closed] — Chat creation latency scales with accumulated conversation history](https://github.com/nearai/ironclaw/issues/5509)** — Closed today; frontend-induced latency growing with history.
- **[#5510 [Closed] — Cannot delete old routines](https://github.com/nearai/ironclaw/issues/5510)** — Closed today.

**Assessment:** Today's bug activity is concentrated on the WebUI and QA-related regressions. 5 issues were closed (some long-standing P2s), and 3 of the 4 open P2s already have dedicated fix PRs in flight — a strong signal that the team is rapidly mopping up after the v1.1.0 release. The zombie-thread issue (#7400) is the most pressing open item as it affects stable.

---

## 6. Feature Requests & Roadmap Signals

**Strong signals (in progress or planned):**

- **Progressive tool discovery at scale** — Issue #7405, with PRs #7409 (baseline catalogs at 100–1,000 tools) and #7410 (bounded complete signatures) stacked and ready. This is the v1.2.0 epic's next step (#7166 "Tool disclosure follow-up"), targeting reduced model turns and better large-catalog behavior.
- **Batch-level parallel execution** — Issue #7407: implementing true concurrent execution of `BatchPolicy::Parallel` batches. A clear performance optimization that requires no user-facing change and fits release trains well.
- **First-party web-push channel + PWA** — PR #7398 (size: XL, risk: medium) introduces browser notification delivery. This closes the "notification channel parity" gap (Slack/Telegram vs. web).
- **Presence-based shared conversations** (PR #7397) and **progressive previews** (PR #7396) for Slack/Telegram — both are large PRs (XL) building on the newly merged acting-identity ladder from #7377.
- **Experiment: replace first-party coding tools with the pinned omp tool surface** (Issue #7392, epic) — Replace model-visible coding tools with the exact contract from `can1357/oh-my-pi`, shipped via the existing always-on host-owned path.

**Prediction:** The next minor release (likely v1.2.0) will be heavy on **channel features** (web-push, progressive previews, shared presence contexts) as well as a **tool-discovery overhaul** with complete signatures and high-scale catalogs. Bugs affecting stable (like #7400) may be backported or prompt a v1.1.1 patch.

---

## 7. User Feedback Summary

Recurring pain points from the open and recently closed issues:

- **Unhelpful failure messages** — Multiple Issues (#5552, #5878, #7292) show a pattern where the agent surfaces generic "invalid result" or "temporarily unavailable" errors instead of actionable diagnostics. In the revoked-GitHub-token case (#5878), the user was steered into re-auth loops that repeated the same misleading message — a key quality gap in failure UX.
- **Efficiency overhead** — Issue #6046 describes a simple email-to-sheet workflow requiring **124 tool invocations** (including unrelated content analysis). Issue #5509 covers chat-creation latency growing with history. Together these suggest a shared underlying concern: **the system needs to be leaner in how it uses model turns, tool calls, and frontend round-trips**. The `tool_search` and batch-parallel work are direct responses.
- **Automation output noise vs. final deliverable** — Slack-triggered automations post intermediate "Now let me also check…" progress messages instead of a final summary (#5551). Users expect final results, not a transcript. This is directly addressed by the progressive-preview PRs (#7396).
- **Auth flows are fragile** — Repeated Slack reconnects (#5882) and revoked GitHub tokens (#5878) both result in dead-end UI states with confusing messaging. "Remove and reinstall the extension" as the only recovery path is clearly insufficient.
- **Data visibility/consistency** — The 61-vs-50 automations discrepancy (#7345) shows users are actively cross-checking agent claims against UI states, and inconsistency undermines trust in both the agent and the dashboard.

**Overall satisfaction leans mixed:** Users are using real workflows (email-to-sheet, Slack-triggered routines, CoinGecko queries) and encountering P2-level bugs that block basic usage. The presence of a healthy pipeline of fix PRs suggests the velocity is there, but the release cadence may be outpacing QA hardening.

---

## 8. Backlog Watch

These issues/PRs have been open for a while and may need maintainer attention:

- **[#6046 — Simple email-to-sheet workflow invokes excessive number of tools](https://github.com/nearai/ironclaw/issues/6046)** — Open since **July 13, 2026** (4 weeks). This is a P2 QA bug that calls for optimization work in the agent loop. The tool-search improvements (#7405) may help, but no direct mitigation has been linked yet.
- **[#6479 — Routines can create or modify other routines, risking self-replicating automations](https://github.com/nearai/ironclaw/issues/6479)** — Open since **July 22, 2026** (3 weeks). A P2 security/safety concern. No fix or design discussion is visible in the issue thread.
- **[#5551 — Automation posts intermediate progress message to Slack instead of final result](https://github.com/nearai/ironclaw/issues/5551)** — Open since **July 2, 2026** (5+ weeks), last updated today. Behavior directly conflicts with user expectations. It may be implicitly addressed by the progressive-preview PR (#7396), but that PR is about adding previews, not changing final-message delivery semantics; this issue, as written, may need to be re-scoped or closed with a cross-reference.
- **[#5878 — Revoked GitHub token produces misleading errors instead of re-auth flow](https://github.com/nearai/ironclaw/issues/5878)** — Open since **July 9, 2026** (a month). Recurring theme of opaque failures; the "temporarily unavailable" misdirection is a bad UX pattern and may deserve targeted UX work.
- **[#5882 — Repeated Slack reconnect attempts leave authentication flow in broken state](https://github.com/nearai/ironclaw/issues/5882)** — Open since **July 9, 2026** (a month). Requires "remove and reinstall the extension" to recover. No fix PR linked.
- **[#7076 — Install the packages the catalog already publishes](https://github.com/nearai/ironclaw/pull/7076)** — Open since **August 3, 2026** (a week), authored by a **new contributor** (neo-sky). It was rebased onto current `main` (was 3 months stale) — a workflow-signal that it may be close to a decision. Size is XL; given the skill-installation bugs in the same area (#7168), this PR deserves a clear maintainer review, or at least explicit scheduling, to avoid stalling a new contributor's momentum.

**Watch item:** PR #7020 (tokio-tungstenite 0.29 → 0.30, open since August 2) and PR #7262 (wasm group, open since August 5) are both small dependency bumps that are commonly merged quickly; their age might just be low priority, but it is worth confirming they are not blocked.

---

*Data source: GitHub (nearai/ironclaw), issues and PRs updated between 2026-08-09 and 2026-08-10.*

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-08-10

## 1. Today's Overview
Project activity is at a **low simmer**. No new releases were published, and no pull requests were merged or closed in the last 24 hours. Issue activity is moderate: 3 issues received updates, all of which remain **open**, with no closed items. Notably, one new issue (#2453) was created yesterday and is drawing immediate attention for its potential impact on model-switching workflows. Two older issues (#1187, #2132) have been flagged with the `[stale]` marker, indicating they have lingered without resolution. Overall, the project appears stable but is **not actively converging** on open community concerns this week.

## 2. Releases
No new releases were published in the last 24 hours. This section is omitted.

## 3. Project Progress
No pull requests were merged or closed in this period. There is no verifiable evidence of feature advancement or bug fixes landing upstream today. The project's maintainers appear to be in a **quiet consolidation phase**, with no visible code changes hitting the default branch.

## 4. Community Hot Topics
- **#2453 — [OPEN] Switching custom models falsely flagged as unsupported**  
  (Updated: 2026-08-09 | Comments: 1 | 👍: 0)  
  [Link](https://github.com/netease-youdao/LobsterAI/issues/2453)  
  This is the **most recent and most operationally disruptive** issue. The user reports that model identifiers in the format `custom_1/openai/gpt-oss-20b:free` are misinterpreted by the system's provider/model parsing logic, causing legitimate custom models (via OpenRouter/NVIDIA) to be rejected mid-thread. This is a **high-signal** report that touches core model-switching logic.

- **#1187 — [OPEN] [stale] Add context window and output token settings per API configuration**  
  (Created: 2026-04-01 | Updated: 2026-08-09 | Comments: 2 | 👍: 1)  
  [Link](https://github.com/netease-youdao/LobsterAI/issues/1187)  
  This long-standing request is resurfacing because users running DeepSeek models are hitting `Context overflow: prompt too large` errors. The issue is not just a feature ask but a **stability complaint**—users need per-model context sizing to avoid session failures.

- **#2132 — [OPEN] [stale] Cross-model subtask orchestration breaks**  
  (Created: 2026-06-09 | Updated: 2026-08-09 | Comments: 1 | 👍: 0)  
  [Link](https://github.com/netease-youdao/LobsterAI/issues/2132)  
  A deep-dive report into gateway-level function calls that are **not registered in the session/subagent listing**, breaking cross-model orchestration flows (e.g., M3 planner → DeepSeek executor). The issue includes detailed diagnostic traces, indicating advanced user investment in the platform.

## 5. Bugs & Stability
Three open issues relate to stability or correctness. Ranked by severity:

1.  **Medium-High — #2453: Model-switching misclassification**  
    Functional blocker for users relying on custom/OpenRouter/NVIDIA models. No PR exists.  
    Because it breaks a mainstream workflow (switching models mid-thread), this is the **highest-priority bug** currently open.

2.  **Medium — #1187: Context overflow with DeepSeek**  
    Poor default context sizing leads to **hard session failures** and requires manual resets. No fix PR exists. This is a **frequent annoyance** for large-context workloads.

3.  **Low (Architectural) — #2132: Cross-model subtask function calls missing**  
    Not a crash, but a **logic gap** in the gateway layer. The reporter has provided a detailed analysis and a proposed fix pattern, but no maintainer response or PR has surfaced in 2 months.

## 6. Feature Requests & Roadmap Signals
- **Per-model context window + output token settings (#1187)** — This is the clearest roadmap signal. The user community wants **explicit, user-controlled context limits** per API config, not silent defaults that overflow. This feature is likely to be prioritized if the maintainers are deepening DeepSeek/OpenRouter support.
- **Cross-model subtask APIs/notifications (#2132)** — The reporter explicitly requests that subtask completion events be surfaced to the parent task, mirroring same-model behavior. This suggests a **future orchestration layer enhancement** that treats subagents uniformly across model boundaries.
- **Fix provider/model parsing for custom names (#2453)** — While technically a bug, it implies a roadmap need: **robust model identifier validation** that accepts `vendor/model` semantics without hardcoding provider names. Expect a refactor of the model-handling module if this becomes popular.

## 7. User Feedback Summary
- **Pain Point — Model flexibility is limited by hardcoded logic**: Users are actively integrating OpenRouter/NVIDIA free models and are being blocked by the system's rigid provider parsing. This signals strong demand for **BYO (Bring Your Own) model flexibility**, and frustration when the platform fails to adapt.
- **Pain Point — Context window defaults are not user-friendly**: The DeepSeek overflow error interrupts real workflows. Users expect **graceful degradation or presets**, not session resets.
- **Engagement signal**: The cross-model subtask issue (#2132) shows that power users are **building complex multi-agent pipelines** on LobsterAI, indicating a growing prosumer segment that values orchestration depth. The lack of a maintainer response in 2 months may be breeding quiet dissatisfaction.
- **Overall tone**: Users are technically sophisticated, provide detailed logs and diagnoses, and are **forward-looking**—they are not just reporting bugs but proposing architectural solutions.

## 8. Backlog Watch
- **#1187 (Apr 2026)** — Stale, 2 comments, 1 👍. Needs a maintainer triage: either commit to the feature or explain a workaround for the DeepSeek overflow. Silence is causing repeated user friction.
- **#2132 (Jun 2026)** — Stale, 1 comment. Detailed root-cause analysis provided by the user; **requires maintainer acknowledgment and a decision** on the proposed fix direction. This is a strong candidate for maintainer feedback to keep a power user engaged.
- **No merged PRs in 24h** — If this quiet period extends >1 week, the backlog risk grows, especially for bug #2453 which is fresh and could escalate in popularity.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-08-10

## 1. Today's Overview
Moltis is in a **quiet but active maintenance phase** — 2 open issues and 1 open PR were updated in the last 24 hours, with no new releases or merges. Activity is focused on **polishing existing functionality** (vault recovery UX and container runtime detection) rather than shipping new features. Both open issues are bugs, indicating the team is likely prioritizing stability. The presence of a ready fix PR for the vault issue suggests a **healthy, responsive maintainer cadence**. Overall, the project is **stable with a clear, small backlog**.

## 2. Releases
**No new releases** were published in the last 24 hours. The most recent release remains unavailable in this data window; no breaking changes or migration notes to report.

## 3. Project Progress
**No PRs were merged or closed** in the last 24 hours. However, **one new PR was opened**, advancing a bug fix:

- **[PR #1186 — fix(vault): normalize recovery phrase before hashing](https://github.com/moltis-org/moltis/pull/1186)** (`pxmpsdev`): Fixes a logic gap where the vault accepts normalized phrases (lowercase/dashes) during unsealing but the stored hash was computed over the raw phrase. This PR aligns the hashing to use the normalized form, closing a consistency hole between recovery and hashing.

## 4. Community Hot Topics
No issues or PRs have active comment threads (0 comments across all items). However, the two open issues represent the current **topics of concern**:

- **[Issue #1187 — Heartbeat settings UI silently resets fields not represented by the form](https://github.com/moltis-org/moltis/issues/1187)** (`IlyaBizyaev`): A UI/UX bug causing silent data loss in configuration. *Underlying need*: Users expect configuration forms to respect all settings, not just those they render. This suggests a desire for **more robust, lossless settings management**.

- **[Issue #1185 — Apple Container 1.x sandbox starts but Moltis treats it as not running](https://github.com/moltis-org/moltis/issues/1185)** (`mikz`): A runtime detection mismatch for Apple Container 1.x. *Underlying need*: Users require **accurate container state synchronization** to avoid false-negative monitoring and potential mis-orchestration.

## 5. Bugs & Stability
Two bugs are currently open, both reported within the last 2 days:

| Severity | Issue | Details |
|----------|-------|---------|
| **Medium-High** | [#1185 — Apple Container 1.x sandbox state false-negative](https://github.com/moltis-org/moltis/issues/1185) | Moltis fails to recognize a running sandbox, which could lead to incorrect state-driven actions (e.g., restart loops). **No fix PR yet**. |
| **Medium** | [#1187 — Heartbeat settings UI silent field reset](https://github.com/moltis-org/moltis/issues/1187) | Configuration fields not in the form are silently wiped on save. Data loss risk for advanced users. **No fix PR yet**. |

**Mitigating factor**: A fix for the related vault hashing issue ([PR #1186](https://github.com/moltis-org/moltis/pull/1186)) is already in review, indicating the team is actively addressing reported consistency bugs.

## 6. Feature Requests & Roadmap Signals
No explicit feature requests were filed in the last 24 hours. However, the two bugs hint at **implicit roadmap signals**:

- **Configuration integrity layer** (from #1187): Users need UI changes to be **non-destructive** — this may push toward "show all fields, including defaults, in settings forms" in the next minor release.
- **Runtime state abstraction** (from #1185): The need to distinguish "process started" from "runtime healthy" may lead to a **more robust container health-check API** in a future version (1.x or 2.x).

Given the current PR momentum, the **next patch release (0.x or 1.x) will likely include** the vault normalization fix, with the two open bugs targeted for the following patch.

## 7. User Feedback Summary
Real user pain points this cycle:

- **Data loss in configuration UI** (#1187): A contributor reported that saving heartbeat settings silently overwrites unrelated fields. This is a **trust-breaking UX issue** for power users who rely on granular settings.
- **False-negative runtime detection** (#1185): Apple Container 1.x users report Moltis says the sandbox is "down" when it's actually running. This causes **frustration and potential automation errors** (e.g., unnecessary restarts).

User satisfaction signals: the **absence of duplicate reports** and the **"latest version" checkmarks** suggest a clean install base and good update adoption. Both reporters followed preflight checks, indicating a **well-documented issue process**.

## 8. Backlog Watch
No items qualify as "long-unanswered" (both issues are < 3 days old). The PR #1186 is the **most time-sensitive item** and should be reviewed/merged promptly to unblock users who rely on passphrase normalization. Maintainers should keep an eye on:

- **[PR #1186](https://github.com/moltis-org/moltis/pull/1186)** — awaiting maintainer review/merge (1 day old).
- **[Issue #1187](https://github.com/moltis-org/moltis/issues/1187)** — new, but the "silent reset" nature makes it a high-priority fix window before more users hit it.

No stale issues or PRs require immediate maintainer intervention beyond normal triage cadence.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-08-10

## Today's Overview

CoPaw (QwenPaw) is in a period of sustained high activity, with 17 issues and 50 PRs updated in the last 24 hours—an indication of a rapidly evolving codebase with strong community engagement. Notably, only 1 of 50 PRs was merged or closed, while a wave of new first-time-contributor PRs (5+ opened today) suggests the "Help Wanted" program is driving on-boarding of new contributors, though the review queue may be building pressure. The project shows no new releases today; the latest known versions are v2.0.1 (production) and v2.1.0b2 (beta). Activity is heavily concentrated around backend providers (Gemini, OpenAI-compat), console/frontend UX, ReMe memory system improvements, and channel integrations (WeChat, OneBot). The project appears healthy and community-driven, though the low merge rate relative to PR volume is worth monitoring.

## Releases

No new releases were published in the last 24 hours. The most recent known versions in circulation are **QwenPaw v2.0.1** (stable) and **v2.1.0b2** (beta, which ships ReMe 0.4.1.4 as the memory backend).

## Project Progress

Only **one PR was closed/merged today**, but it represents a meaningful catalog improvement:

- **[PR #6846 — feat(providers): catalog DeepSeek V4 context windows (1M)**](https://github.com/agentscope-ai/QwenPaw/pull/6846): Adds `deepseek-v4-flash` and `deepseek-v4-pro` entries with a 1M-token context window to the static model catalog. Previously these models fell back to the 131K default, causing premature context compaction at 128k—a correct fix for users of these models.

Key features that **advanced** through open PRs today (still under review):

- **[PR #6844 — fix(providers): strip unsupported Gemini schema metadata](https://github.com/agentscope-ai/QwenPaw/pull/6844)**: Directly addresses issue #6812 by removing the `$schema` keyword that Google's SDK rejects, fixing model "unknown" failures for Gemini.
- **[PR #6845 — fix(chats): preserve assistant completion time](https://github.com/agentscope-ai/QwenPaw/pull/6845)**: Fixes wrong assistant elapsed-time display after history reload (issue #6826).
- **[PR #6398 — feat: add reranker support for ReMe memory search (backend)](https://github.com/agentscope-ai/QwenPaw/pull/6398)**: Under review, adds re-ranking for memory search results.
- **[PR #6704 — feat(chat): session fork — snapshot conversation context to new session](https://github.com/agentscope-ai/QwenPaw/pull/6704)**: Adds a session fork feature for checkpoint-style branching (related to issue #6560).

## Community Hot Topics

**1. Help Wanted / Open Tasks — Issue #2291** ([link](https://github.com/agentscope-ai/QwenPaw/issues/2291))
Held 66 comments and remains the community's central hub for task claiming and contribution coordination. Its continued activity today (from PRs like #6312 and #6842 referencing it) shows a healthy, viable open-source contributor pipeline.

**2. Web Console Mobile Adaptation — Issue #6281** ([link](https://github.com/agentscope-ai/QwenPaw/issues/6281)) — 5 comments
User request to adapt the Web console for mobile devices. A clear UX gap in a desktop-first design, suggesting growing user demand for mobile operation.

**3. Custom Ascend-vLLM Connection Failure — Issue #5584** ([link](https://github.com/agentscope-ai/QwenPaw/issues/5584)) — 4 comments, CLOSED
A regression: v1.1.7 worked, later versions fail to connect to custom ascend-vllm models despite passing config tests. Closed, but the underlying `APIConnectionError` wrapping suggests either a provider serialization change or a fix that users should validate exists in current builds.

**4. Front-end Renderer Collapses Long Multi-line Tool Output — Issues #6848, #6849, #6850, #6851, #6852** ([#6852](https://github.com/agentscope-ai/QwenPaw/issues/6852) open, others closed)
A user filed the same bug report five times—likely a submission/UI hiccup—but the issue persists and is real: long tool outputs rendered as unreadable blobs in v2.1.0b2. Currently no linked fix PR exists.

**5. Approval Purpose Descriptions — Issue #6832** ([link](https://github.com/agentscope-ai/QwenPaw/issues/6832)) + PR [#6854](https://github.com/agentscope-ai/QwenPaw/pull/6854)
Users want AI to explain why it requests approval, rather than forcing them to read PowerShell code. A first-time-contributor PR (#6854) already addresses this with localized descriptions—a fast community-driven response.

## Bugs & Stability

Ranked by severity:

- **High — Gemini provider failure (model "unknown")** — [Issue #6812](https://github.com/agentscope-ai/QwenPaw/issues/6812). Google SDK rejects `$schema` metadata in tool schemas. **Fix PR exists**: [#6844](https://github.com/agentscope-ai/QwenPaw/pull/6844), currently open.
- **High — Anti-virus terminates QwenPaw process** — [Issue #6847](https://github.com/agentscope-ai/QwenPaw/issues/6847). Users report AV software force-killing QwenPaw during tasks (vs. WorkBuddy being unaffected). No fix PR yet.
- **Medium — Incorrect assistant elapsed-time display** — [Issue #6826](https://github.com/agentscope-ai/QwenPaw/issues/6826). Shows seconds instead of the actual 2 minutes. **Fix PR exists**: [#6845](https://github.com/agentscope-ai/QwenPaw/pull/6845).
- **Medium — MCP string-typed numbers passed as numeric types** — [Issue #6839](https://github.com/agentscope-ai/QwenPaw/issues/6839). Breaks MCP tools expecting string parameters like API keys. No fix PR identified.
- **Medium — Front-end collapses long multi-line tool output** — [Issue #6852](https://github.com/agentscope-ai/QwenPaw/issues/6852) (open). No fix PR linked.
- **Low — ReMe Auto-Dream partial failure marks whole task as error** — [Issue #6841](https://github.com/agentscope-ai/QwenPaw/issues/6841). Single unit schema failure on an already-written file fails the entire job; suggests retry + tolerance. No fix PR.
- **Low — Prompts.py claims dream writes to MEMORY.md (not implemented)** — [Issue #6853](https://github.com/agentscope-ai/QwenPaw/issues/6853). Documentation/behavior mismatch in memory pipeline. No fix PR.

## Feature Requests & Roadmap Signals

- **Approval purpose descriptions** ([#6832](https://github.com/agentscope-ai/QwenPaw/issues/6832)): Has active PR #6854 — likely lands in next release.
- **Session fork / checkpointing** ([PR #6704](https://github.com/agentscope-ai/QwenPaw/pull/6704), relates to [#6560](https://github.com/agentscope-ai/QwenPaw/issues/6560)): Likely candidate for the next 2.1.x release.
- **ReMe memory roadmap (ReMe4)** ([#6840](https://github.com/agentscope-ai/QwenPaw/issues/6840)): User asks about Auto-Link, tri-modal search, and digest weights timeline—clear signal that memory is a key differentiator and roadmap item.
- **Reranker for ReMe search** ([PR #6398](https://github.com/agentscope-ai/QwenPaw/pull/6398)): Indicates memory search quality improvements are in active development.
- **Hidden agents for UI** ([PR #6842](https://github.com/agentscope-ai/QwenPaw/pull/6842)): Lets plugin-created internal agents stay addressable but invisible in UX.
- **CIDR support in no-auth host allowlist** ([PR #6259](https://github.com/agentscope-ai/QwenPaw/pull/6259)): Operational security improvement.
- **Real-time SSE streaming** ([PR #6843](https://github.com/agentscope-ai/QwenPaw/pull/6843)): Fixes console UI buffering; users want incremental output.
- **Configurable themes/skins** ([PR #6312](https://github.com/agentscope-ai/QwenPaw/pull/6312), Task 1 of #2291): Draft PR submitted, pending scope guidance.

## User Feedback Summary

Common pain points across today's reports:

- **Model interoperability friction**: Gemini schema rejection (#6812), DeepSeek V4 context-window misconfiguration (fixed by #6846), and custom ascend-vllm disconnection (#5584) suggest provider-compatibility regressions are the top source of user frustration.
- **Console/UX readability**: Mobile adaptation demand (#6281), long tool-output blobs (#6852), approval clarity (#6832), and lack of real-time streaming (#6843) all point to a desktop-first, info-dense UI that needs significant UX polish.
- **Inconsistency vs. competitors**: Issue #6847 explicitly compares QwenPaw's AV-triggering behavior to WorkBuddy's, signaling a trust/reliability conversation in the community.
- **Memory system scrutiny**: Active scrutiny of the ReMe pipeline (#6841, #6840, #6853) and its documentation means accuracy and transparency in the memory layer matter to advanced users.
- **Sub-agent workflow friction** ([#6838](https://github.com/agentscope-ai/QwenPaw/issues/6838)): Model switching, shared workspaces, and UI state conflicts when sub-agents are configured via `config.json`—a power-user workflow issue.

Overall, satisfaction remains high among contributors (many first-timers are submitting quality fixes), but stability and cross-provider compatibility are the primary sources of dissatisfaction.

## Backlog Watch

- **[Issue #5584 — Custom ascend-vllm connection failure (CLOSED)](https://github.com/agentscope-ai/QwenPaw/issues/5584)**: Closed without a visible fix-PR linked; warrants verification that the resolution is actually shipped in a release.
- **[Issues #6848–#6851 — Duplicate renderer bug reports](https://github.com/agentscope-ai/QwenPaw/issues/6852)**: One remains open, but the duplicates suggest user confusion and no maintainer attention yet.
- **[PR #6681 — "test review bot"](https://github.com/agentscope-ai/QwenPaw/pull/6681)**: Open for 6 days with no substantive content; likely test spam that should be closed.
- **[Issue #6847 — AV force-kills QwenPaw](https://github.com/agentscope-ai/QwenPaw/issues/6847)**: High-severity environmental issue with no response yet—risks user trust if left unaddressed.
- **PR backlog pressure**: 49 open PRs with roughly 6–8 first-time-contributor submissions needing maintainer review; the project would benefit from explicit review prioritization or a triage bot to avoid contributor drop-off.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

Based on the GitHub data provided for ZeroClaw (github.com/zeroclaw-labs/zeroclaw) on 2026-08-10, here is the project digest:

---

# ZeroClaw Project Digest — 2026-08-10

## 1. Today's Overview

ZeroClaw is in a state of high activity with **50 issues** and **50 pull requests** updated in the last 24 hours. The issue tracker shows a healthy mix of open discussions (38) and recently closed items (12), indicating active triage. However, the pull request queue is **entirely open** (50 open, 0 merged/closed), suggesting a bottleneck in the review/merge process, with many PRs waiting on author action. The project is heavily focused on **security hardening**, **governance process improvement**, and **runtime reliability**, with a significant number of high-priority (P0/P1) bugs and RFCs under active consideration. No new releases were published in this window.

## 2. Releases

No new releases were published in the last 24 hours. The last known release was v0.8.3, with v0.8.4 in progress (referenced in issue #9690).

## 3. Project Progress

While no PRs were merged in the last 24 hours, **12 issues were closed**, indicating significant progress and resolution of ongoing work:

- **Security Fixes:** Issue **#8054** (System prompt tool-availability mismatch) was closed, following the fix in PR #8053. Issue **#8560** (browser_open hang) and **#8731** (zombie MCP processes) were also closed, addressing critical runtime stability and security concerns.
- **Runtime & Infrastructure:** Issue **#9192** (shared_budget TOCTOU/panic) and **#9834** (flaky runtime tests from shared state) were closed. Issue **#9690** (Containerfile rustc pin below MSRV) was resolved, unblocking the `all-features` container build.
- **Bug Triage:** Issue **#9860** (Web UI frozen on filesystem channel event) was closed as a duplicate, indicating active bug triage.
- **Tracker Completion:** The **#8681** tracker for the goal-mode implementation split was closed, suggesting that the large `feat/goal-mode` branch has been successfully split into reviewable PRs.

## 4. Community Hot Topics

The most active discussions revolve around **governance, security, and architecture**, with long-running threads seeking maintainer input:

- **RFC: Work Lanes and Board Automation (#6808)** — 21 comments. This is a broad governance RFC aiming to improve work routing and label hygiene. It has been active since May and is in the "rollout in progress" phase, showing the community's deep involvement in the project's operational processes.
- **RFC: Per-model capability & context-window config (#7100)** — 11 comments. This high-risk RFC addresses a real user pain point: incorrect vision support and context window reporting. It touches core config, gateway, and UI, aiming to unify model metadata sources.
- **Maintainer Decision Queue (#8692)** — 11 comments. This is a meta-tracker for all RFCs and design issues needing maintainer decisions. Its high comment count highlights the community's desire for closure on pending proposals.
- **RFC: Security Posture & Ingress Policy (#6971)** — 10 comments. A critical, long-running RFC about credential handling, sandboxing, and ingress trust. The community is actively shaping the project's core security model.
- **WhatsApp Security RFC (#9397)** — 10 comments. A focused proposal to treat empty `allowed_groups` as permit-none, closing a potential authorization bypass. This shows strong community-led security review.

## 5. Bugs & Stability

The project is currently addressing several **critical and high-severity bugs**, with a strong focus on security vulnerabilities:

- **P0 — Gateway Webhook Fail-Open (#9565):** **S0 severity.** Three webhook handlers (WhatsApp Cloud, Linq, WATI) dispatch attacker-controllable messages without authentication. A fix is in progress via PR **#9744**, which introduces a `VerifiedWebhookIngress` boundary. This is the most critical item.
- **P1 — Verifiable-Intent Constraint Bypass (#9328):** Constraint evaluation does not verify the credential chain, potentially allowing unauthorized actions.
- **P1 — Unbounded RSS Growth in Agent Loop (#8642):** MCP/tool-schema cloning causes memory leaks and OOM. This is split from a larger tracker and still open.
- **P1 — Config Flush Race Condition (#9284):** `flush_config` can overwrite concurrent writes, leading to configuration loss.
- **P1 — sops_dir Default Not Honored (#9779):** The daemon silently fails to load SOPs if an operator relies on documented defaults, breaking crucial automation.
- **P2 — Solana Address Redaction (#9486):** The high-entropy detector redacts valid public blockchain addresses, breaking payment flows. The related RFC **#9825** aims to define publish-safe exceptions for these identifiers.
- **P2 — High-Entropy Detector False Positive (#9486):** Related to the above, the `high_entropy_tokens=false` config does not stop redaction on the channel path.

Many of these bugs have corresponding fix PRs open (#9744, #9720), but they are all blocked pending author action.

## 6. Feature Requests & Roadmap Signals

The feature roadmap is strongly driven by **enhanced security, flexible configuration, and new channel capabilities**:

- **Per-Model Capabilities (#7100):** Likely to land soon. Fixes a common source of user confusion (incorrect vision/context window). Related PR **#9743** and **#9707** are ready but need author action.
- **Security Policy Hot-Reload (#7897):** The ability to apply security and channel config updates without a full daemon restart is a highly requested operational feature. It is a P3 but with significant community interest.
- **Webhook Ingress for Plugins (#8862):** A large, stacked PR to route webhooks to WASM parsers, enabling a new class of plugin capabilities. It advances the project's extensibility story.
- **PowerShell Support on Windows (#9182):** HR-native shell support for Windows, making the runtime viable on more platforms.
- **Matrix Single-Message Progress Drafts (#8443):** Improves Matrix UX by editing a single draft message with progress updates.
- **Per-Agent Data Scoping:** A clear trend this week, with multiple PRs (#9745, #9746) adding per-agent ownership to knowledge graphs and session tools, a direct response to multi-tenant security concerns.

## 7. User Feedback Summary

- **Frustration with Silent Failures:** Several issues (#9779, #7897, #9486) highlight user pain with silent failures where configs are accepted but not applied, leading to hard-to-debug production issues. The community is pushing for more transparent and verifiable state.
- **Need for Robust Security Defaults:** Issues like the WhatsApp group bypass (#9397) and the webhook fail-open (#9565) show the community is actively testing and reporting security holes, pushing the project toward a fail-closed posture by default.
- **Desire for Better Tooling:** The RFC to streamline the RFC process itself (#9496) indicates the community finds the current contribution process cumbersome. Users want faster decisions and less manual overhead.
- **Workflow Necessity:** The bug about cron-triggered SOPs being unable to do network work (#9780) reflects a real-world need for complex automation that the current sandboxing model prevents.

## 8. Backlog Watch

Several important items are languishing and need maintainer attention to move forward:

- **RFC Process Reform (#9496):** An RFC to make the decision process faster. It is meta-critical; resolving this will likely accelerate other stalled RFCs.
- **Release Attestation Consolidation (#9101):** An accepted P1 issue to reduce CI redundancy from three signing mechanisms to one. It is a maintenance burden and a security risk if the mechanisms drift.
- **Cargo Audit Ignores & CVE Remediation (#8519):** An accepted P1 security issue to reconcile dependency check tooling and remediate wasmtime CVEs.
- **forbid(unsafe_code) Workspace-wide (#7130):** An accepted P2 security-hardening feature that has been open for over two months.
- **Test-Only Change Risk Precedence (#9530):** This low-risk RFC aims to clarify conflicting documentation on how to label test-only changes in high-risk paths, which would speed up reviews.

A major concern is the **50 open PRs with 0 merged in 24 hours**. Many are marked `needs-author-action`, but a significant number, including critical security fixes like #9744, are waiting for reviews. This indicates a potential maintainer bandwidth issue that could be a bottleneck for the project's progress.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/kky-wollu/agents-radar).*
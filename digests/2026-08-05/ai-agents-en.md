# OpenClaw Ecosystem Digest 2026-08-05

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-08-04 23:06 UTC

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

Based on the GitHub data provided for OpenClaw (github.com/openclaw/openclaw) on 2026-08-05, here is the project digest:

---

## OpenClaw Project Digest (2026-08-05)

### 1. Today's Overview
The OpenClaw project is in a high-activity state, with 500 issues and 500 PRs updated in the last 24 hours. The project has a significant bottleneck: many critical bugs (P1/P2) remain open, particularly around session-state integrity (livelocks, deadlocks, and message loss), with several issues flagged as `needs-maintainer-review` or `needs-product-decision`. While two patch releases (v2026.7.1-1, v2026.7.1-2), both containing fixes for specific regressions were shipped, the vast majority of the 500 PRs are still open, indicating a merge queue strain. The maintainer team appears to be managing a large influx of community reports (including a few from a bot, `clawsweeper`), but the backlog of unresolved `diamond lobster` rated issues is concerning for platform stability.

### 2. Releases
Two new patch versions were released, both focused on stability fixes:

- **v2026.7.1-2**: Includes a fix for npm plugin updates, allowing tracked official plugins to install/update when newer npm clients return singleton-array metadata. ([PR #108336](https://github.com/openclaw/openclaw/PR/108336))
- **v2026.7.1-1**: Includes two critical fixes:
  - **Codex progress replies**: Fixed an issue where app-server turns would terminate prematurely after sending a progress message, preventing the authoritative final response. ([#106961](https://github.com/openclaw/openclaw/issue/106961), [#108487](https://github.com/openclaw/openclaw/issue/108487))
  - **Memory Core startup repair**: Addressed recovery of the derived legacy-index during startup.

### 3. Project Progress
Despite the large number of open PRs, there was notable progress in specific areas based on merged/closed PRs (124 merged/closed total):

- **Codex Integration**: A fix was closed for the "background Codex ACP turns fail hard on transient pre-output Internal error" issue. ([PR #111436](https://github.com/openclaw/openclaw/PR/111436))
- **Channel Security**: A fix aims to close Feishu and Microsoft Teams DM policy audit gaps in `openclaw security audit`. ([PR #115432](https://github.com/openclaw/openclaw/PR/115432))
- **FS Safety**: A PR ([#119363](https://github.com/openclaw/openclaw/PR/119363)) moves untrusted filename sanitization fully into the `@openclaw/fs-safe` package, improving cross-platform security.
- **Gateway/Media Management**: A PR ([#119127](https://github.com/openclaw/openclaw/PR/119127)) is ready to fix a critical P0 bug where the TTL sweep was accidentally deleting user-managed files in `media/outgoing`.

Active fix efforts are visible in open PRs targeting major issues, such as event-loop stalls during bootstrap ([#89040](https://github.com/openclaw/openclaw/PR/89040)) and agent turns dying silently on approval requests ([#115933](https://github.com/openclaw/openclaw/PR/115933)).

### 4. Community Hot Topics
The most discussed issues highlight significant friction points, primarily around silent failures and session corruption:

- **#116277** (104 comments) - **DeepSeek v4 Flash silent reply failure**. A `diamond lobster` P1 bug where the model fails to generate a reply, posting a generic fallback. This is a high-impact issue indicating a provider-specific integration instability.
- **#116201** (58 comments) - **Realtime voice work retaining unbounded provider and consult state**. A `diamond lobster` P1 issue concerning resource leaks causing session-state issues in voice sessions.
- **#115326** (25 comments) - **Crash-loop breaker suppresses Discord/WhatsApp permanently**. A P1 regression where the documented recovery path fails, effectively bricking channels for users.
- **#118846** (14 comments) - **Gateway main thread saturated from boot by plugin-metadata snapshot**. A P1 issue causing local RPC death (WebSocket 1006), likely a performance-degradation hotspot.
- Legacy issues like **#43367** (13 comments) about unstable multi-agent orchestration and **#91363** (10 comments, 👍 6) about isolated cron failures with "LLM request failed" continue to draw community attention, indicating unresolved systemic problems.

### 5. Bugs & Stability
The stability landscape is concerning, centered around `Diamond Lobster` P1 issues focusing on **message loss** and **session-state corruption**:

- **Critical (P1)**:
    - **Thread Saturation**: Gateway main thread pegged at 100% by plugin-metadata statting, starving the accept loop ([#118846](https://github.com/openclaw/openclaw/issue/118846)).
    - **Database Migration Failure**: Agent DB v14->v15 migration fails with `no such column: entry_valid`, blocking gateway start ([#119263](https://github.com/openclaw/openclaw/issue/119263)). This is a Friday-night hotfix grade issue.
    - **Session Livelock**: Transcript projection reconcile can livelock under sustained writes, stalling all transports ([#115908](https://github.com/openclaw/openclaw/issue/115908)).
    - **Context Cap**: All persistent sessions capped at 128k context regardless of model ([#116010](https://github.com/openclaw/openclaw/issue/116010)).
- **High (P2)**:
    - **Zombie Processes**: Leaked hook/tool child processes accumulate over time ([#97616](https://github.com/openclaw/openclaw/issue/97616)).
    - **SSR/UI Rendering**: WebChat fails to render some assistant messages while TUI works ([#77136](https://github.com/openclaw/openclaw/issue/77136)).
- **Fix Status**: While some fix PRs exist (e.g., for #110697, #119088), many of the most critical issues (e.g., #118846, #119263) have `clawsweeper:no-new-fix-pr` or are awaiting maintenance review, meaning users may be stuck for several days.

### 6. Feature Requests & Roadmap Signals
The community is pushing for more robust and observable AI agent behavior:

- **Plugin Control UI Slots**: There is a strong signal for an extensible Control UI via SDK contribution slots for chat modes, approval cards, and input guards ([#71736](https://github.com/openclaw/openclaw/issue/71736)).
- **Session Startup Prompt Configurability**: Users want to customize the hardcoded session reset message via a `session.resetPrompt` feature ([#45501](https://github.com/openclaw/openclaw/issue/45501)).
- **Cross-Platform Shell Support**: Requests for native PowerShell smoke coverage ([#44291](https://github.com/openclaw/openclaw/issue/44291)) and fixes for doctor warnings about NVM node paths ([#60612](https://github.com/openclaw/openclaw/issue/60612)) indicate a push for better Windows parity.
- **Hosting & Onboarding**: A new PR adds an "Agent37 managed hosting install guide" ([#111623](https://github.com/openclaw/openclaw/PR/111623)), aiming to make the platform easier to consume.

Given the PR activity, features like **macOS Realtime Talk support** ([#118499](https://github.com/openclaw/openclaw/PR/118499)) and **System-Agent QR setup contract** ([#114173](https://github.com/openclaw/openclaw/PR/114173), [#119341](https://github.com/openclaw/openclaw/PR/119341)) look likely to land in the next minor release.

### 7. User Feedback Summary
User sentiment is a mix of frustration and deep engagement:

- **Pain Points**: Silent message drops ("No reply was generated", "message black hole" in forum topics), session data corruption/blocking ("session stuck until refresh", "crash-loop breaker suppresses channels"), and frustratingly long chains of failures (e.g., `chat.send` rejected with "thread switched branches").
- **Data Persistence Worries**: Users are alarmed by unbounded log growth (`provider-payload.jsonl` and `cache-trace.jsonl`) and `backup create` stalling on large installations, bringing their trust in data safety into question.
- **Proactive Users**: Detailed field reports ([#41372](https://github.com/openclaw/openclaw/issue/41372)) and feature requests (Browser tool improvements [#44431](https://github.com/openclaw/openclaw/issue/44431)) show power users are deeply invested in the project's direction and helping it mature.

### 8. Backlog Watch
Several critical issues remain unresolved for extended periods, begging for maintainer attention:

- **#43367** (since March 11) - **Multi-agent orchestration is unstable**. This `Diamond Lobster` P1 has been open for 5 months with config overwrite and session-lock failures, severely impacting DevOps use-cases.
- **#41744** (since March 10) - **Feishu loses image media before outbound payload**. A P1 issue with a linked open PR, indicating a rough edge in channel integrations that needs verification.
- **#91363** (since June 8) - **Isolated cron consistently fails with "LLM request failed"**. This issue has high community upvotes (👍 6), indicating widespread impact on automation reliability, but it remains stuck in `needs-maintainer-review`.
- **#115642** (since July 29) - **Billing cooldown outlives outage**. This P1 proposes proactive recovery, representing a serious user-experience flaw where a 5-hour cooldown persists after an outage resolves.

---

## Cross-Ecosystem Comparison

# Cross-Project Ecosystem Report: AI Agent & Personal Assistant Open Source Landscape
**Date:** 2026-08-05

---

## 1. Ecosystem Overview

The personal AI agent open-source ecosystem is dominated by **OpenClaw as the reference implementation**, with a massive community (500+ daily updated issues/PRs) and a broad feature surface. However, the ecosystem is fragmenting into specialized niches: lightweight/embedded agents (PicoClaw, TinyClaw, ZeptoClaw), enterprise/security-focused platforms (ZeroClaw, IronClaw), and channel-integration specialists (NanoBot, CoPaw). The dominant theme across all projects is **stability and reliability** — silent failures, session-state corruption, and message loss are the top recurring pain points. Security hardening is emerging as a critical differentiator, particularly for multi-tenant and production deployments. The ecosystem is clearly in a **post-hype maturation phase**, prioritizing robustness, observability, and developer experience over raw feature expansion.

---

## 2. Activity Comparison

| Project | Issues Updated (24h) | PRs Updated (24h) | Releases (24h) | Health Score* | Primary Phase |
|---|---|---|---|---|---|
| **OpenClaw** | 500 | 500 | 2 patches (v2026.7.1-1, -2) | ⚠️ 4/10 | High-activity, bug-fix crisis |
| **NanoBot** | 4 | 28 | None | ✅ 8/10 | Stabilization/pre-release polish |
| **Hermes Agent** | 50 | 50 | None | ⚠️ 5/10 | High-velocity development |
| **PicoClaw** | 3 | 4 | None | ⚠️ 4/10 | Moderate, stale-bot closures |
| **NanoClaw** | 0 | 5 | None | ✅ 7/10 | Active feature development |
| **NullClaw** | 0 | 1 | None | ✅ 7/10 | Stabilization/low-activity |
| **IronClaw** | 50 | 50 | None | ⚠️ 5/10 | Major architectural restructure |
| **LobsterAI** | — | 13 | None (release merged) | ✅ 7/10 | Release finalization |
| **TinyClaw** | 0 | 0 | None | — | Inactive |
| **Moltis** | 0 | 1 | None | ✅ 8/10 | Maintenance-only |
| **CoPaw** | 25 | 49 | None (beta verified) | ⚠️ 6/10 | High-activity, regression fixes |
| **ZeptoClaw** | 0 | 0 | None | — | Inactive |
| **ZeroClaw** | 50 | 50 | None | ⚠️ 6/10 | Security sprint + architecture RFCs |

*\*Health score is a qualitative composite of bug severity, fix velocity, active backlog, and maintenance responsiveness. Scores are relative and indicative, not absolute.*

---

## 3. OpenClaw's Position

**Advantages:**
- **Scale:** Unrivaled community size (500 daily PRs/issues) vs. 1–50 for peers; the de facto standard for plugin ecosystems and channel integrations.
- **Breadth:** Covers voice (Realtime Talk), multi-agent orchestration, and extensive channel support (Discord, WhatsApp, Telegram, Feishu, MS Teams).
- **Responsiveness:** Ships patch releases almost daily (2 in last 24h) for critical regressions, demonstrating high release velocity.

**Technical Approach Differences:**
- **Monolithic + plugin architecture:** OpenClaw is a heavyweight, all-in-one platform with deep SDK/plugin support; peers like NanoBot and NullClaw favor lightweight, modular, single-purpose designs.
- **Legacy complexity burden:** OpenClaw's age is visible — numerous `diamond lobster` P1 bugs (session livelocks, thread saturation, message loss) indicate architectural debt from rapid growth, a problem less pronounced in newer, cleaner codebases.

**Community Size Comparison:**
- OpenClaw: ~100x the daily activity of mid-tier projects (IronClaw, ZeroClaw, Hermes) and ~500x quieter ones (NullClaw, Moltis).
- It remains the default entry point for users; other projects serve as **specialized alternatives** or **focused R&D experiments**.

---

## 4. Shared Technical Focus Areas

**Cross-project requirements emerging:**

| Requirement | Projects | Specific Need |
|---|---|---|
| **Session/State Integrity** | OpenClaw, Hermes, NanoClaw, IronClaw | Livelocks, deadlocks, message loss, session bleed across tabs, checkpoint failures |
| **Channel Reliability** | OpenClaw, NanoBot, CoPaw, NanoClaw | Approval prompts unreachable via voice/WeChat/Discord-only, webhook verification gaps, token consumption by typing indicators |
| **Security Hardening** | ZeroClaw, OpenClaw, LobsterAI, NanoBot | Per-agent data isolation, API key leakage via `os.environ`, unauthenticated webhooks, prompt-level key info leakage |
| **Observability & Cost Transparency** | NanoBot, IronClaw, PicoClaw, CoPaw | Prompt cache token usage logging, latency-trace overhead, typed error classifications |
| **Model/Provider Compatibility** | NanoBot, OpenClaw, PicoClaw, CoPaw | Rapid-breaking-change tracking (e.g., Opus 5, DeepSeek v4 Flash), smarter rate-limit/error classification, protocol drift |
| **Windows/Desktop Parity** | Hermes, OpenClaw, IronClaw, CoPaw | TUI/gateway crashes, installer reliability, duplicate sidebar lanes, filesystem sync semantics |
| **Config Simplification** | ZeroClaw, CoPaw, Hermes, OpenClaw | Reducing config sprawl, global rules, per-user model selection, avoiding dead env vars |

---

## 5. Differentiation Analysis

| Project | Feature Focus | Target Users | Technical Architecture |
|---|---|---|---|
| **OpenClaw** | Full-featured AI assistant platform; voice, multi-agent, extensive channel list | General power users, developers, enterprises | Monolithic core + rich plugin/SDK ecosystem; node-based |
| **NanoBot** | Lightweight, WebUI-forward, quick vendor fixes | SMBs, devs needing simple, fast-deploy chat bots | Python; focused on provider compat + polished WebUI, minimal legacy |
| **Hermes Agent** | High-velocity dev with strong Windows/desktop emphasis and Telegram parity | Developers on Windows, desktop app users | Modular; heavy CLI/desktop focus; TUI interface; ongoing lifecycle hardening |
| **ZeroClaw** | Enterprise-grade security, sandboxing, per-agent isolation, open API interoperability | Security-conscious enterprises, multi-tenant SaaS | Rust; architecture focus on "host-owned, runtime-controlled" boundaries; RFC-driven governance |
| **IronClaw** | Large-scale architecture discipline, observability, Reborn/WS restructure | Platform teams, OSS infrastructure maintainers | Rust; rigorous process, doc-truth audits, consolidation protocols; slow, deliberate evolution |
| **CoPaw** | Chinese ecosystem integrations (WeChat/iLink), memory compression, task organization | Chinese-market users, cost-sensitive consumers | Python; strong on memory systems, plugin namespaces, deep channel integration |
| **PicoClaw** | Ultra-lightweight, embedded/low-resource, web search expansion | Hackers, Raspberry Pi/embedded hobbyists | Small footprint; prompt-cache observability, minimal dependencies |
| **NanoClaw** | Telephony (SMS/voice AI calls) + chat; approval workflow fixes | Teams needing voice/multimodal interactions | AI/Agent SDK bridge; channel adapter pattern |
| **NullClaw** | "Bring-your-own-CLI" providers (Codex, Gemini, Claude, soon Grok) | CLI-first developers, local-first privacy advocates | Spawn-per-request; provider-agnostic; minimal deps |
| **LobsterAI** | Commercial desktop AI with gamified credit rewards | Consumer/enthusiast desktop users | Desktop app (Electron); monetization-focused features |

---

## 6. Community Momentum & Maturity

**Tier 1: Rapid Iteration / High Momentum (daily security & feature PRs)**
- **OpenClaw** — Bug-fix crisis mode; 2 patches/day; backlog strain.
- **ZeroClaw** — Security sprint + 50 issues/PRs daily; fast-fix velocity.
- **IronClaw** — Architecture restructure with merged batches; rigorous but rapid protocol.
- **Hermes Agent** — High-velocity dev, deep PR queue, stable rebase management.

**Tier 2: Steady, Controlled Development**
- **NanoBot** — Pre-release polish; 19 merges/day; fast turnaround (Opus 5 in <48h).
- **CoPaw** — Beta verification + active regression fixing; 21 merges/day.
- **LobsterAI** — Release finalization; 10 merges/day; internal-driven velocity.

**Tier 3: Stabilization / Low Activity**
- **NanoClaw** — Feature dev (Dial) paused; only 5 PRs updated.
- **NullClaw** — Single idle PR; no issues; plateau.
- **Moltis** — Maintenance-only; dependency bumps.

**Tier 4: Dormant**
- **TinyClaw**, **ZeptoClaw** — Zero activity.

---

## 7. Trend Signals

**For AI Agent Developers:**

1.  **Reliability is the new feature.** Every project reports session-state corruption, silent message drops, and approval-flow failures as top pain points. Skipping stability work will doom any agent project.
2.  **Security is non-negotiable.** Cross-agent data leakage (ZeroClaw), API key exposure (NanoBot), and unauthenticated webhooks are S0-level concerns. Per-agent isolation and fail-closed defaults are becoming non-negotiable for enterprise adoption.
3.  **Provider chaos is universal.** From Opus 5 deprecations to DeepSeek v4 Flash silent failures and GPT-5.6 caching, hard-coded provider lists are dying. Adaptivity and version-aware logic are required.
4.  **Observability drives trust.** Prompt-cache token logging, typed error classifications (vs opaque `input_error`), and tracing fixes are requested across PicoClaw, IronClaw, and NanoBot. Developers want to know **what the agent sees** and **why it fails**.
5.  **OpenAPI interoperability wins.** The highest-comment RFC in the ecosystem (ZeroClaw) is for an OpenAI Chat Completions profile. Exposing agents via universal APIs is the fastest path to adoption.
6.  **Windows is a first-class citizen now.** Desktop parity, installer fixes, and NVM/Node bug reports across Hermes, CoPaw, IronClaw show developers demand a flawless Windows experience.
7.  **AI telephony is emerging.** NanoClaw's Dial PR (SMS/voice channels) and OpenClaw's voice work signal a shift beyond text-chat into multimodal, real-world interactions.
8.  **"Bring-your-own-CLI" is a valid pattern.** NullClaw's CLI-provider approach (Codex, Gemini, Claude, Grok) shows users favor local, dependency-light integrations over heavy SDKs.

---

*Report prepared from 13 project digests on 2026-08-05. All metrics derived from GitHub activity data as summarized in source digests.*

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — 2026-08-05

## 1. Today's Overview

NanoBot is in a period of high maintenance velocity, with 28 PRs updated in the last 24 hours, 19 of which were merged or closed. The core maintainer team (chengyongru, Re-bin) drove a focused polish pass across the WebUI — fixing markdown previews, tooltip alignment, token highlights, and slash-command validation — while a second wave of contributor PRs landed channel-specific fixes for WeCom filename sanitization and Telegram code-block rendering. Notably, the Anthropic Opus 5 compatibility issue (#5235) reported just two days ago was already addressed by PR #5236, demonstrating fast turnaround on provider compatibility. Security and session-access refactoring PRs (#5210, #5238) signal active work on hardening multi-tenant and authentication paths. With zero new releases and four open issues and nine open PRs, the project is clearly in a pre-release stabilization phase rather than feature-expansion mode.

## 2. Releases

No new releases in the last 24 hours. The last activity suggests Nanobot is in a release-candidate window, with significant refactors (#5238 removing request-scoped access grants) and security hardening (#5210 trusted proxy auth) landing without a tag.

## 3. Project Progress

**Channel reliability fixes merged (all #priority: p2):**
- **#5223** `fix(wecom): fall back when filename sanitization strips everything` — prevents directory-path write target when inbound filenames sanitize to empty string.
- **#5222** `fix(telegram): keep fenced code intact when language has special chars` — resolves corrupted code blocks (`c++`, `objective-c`, `html+django`) in Telegram rendering.

**WebUI polish series (merged by chengyongru, all #priority: p2):**
- **#5244** — Markdown rendering in prompt-rail hover previews for assistant answers.
- **#5245** — Unified timestamp tooltip styling and keyboard accessibility.
- **#5243** — Automation trigger metadata moved to message footer, aligned with timestamps.
- **#5241** — Refined inline token highlights (solid accent, hidden `$` in skill refs).
- **#5240** — Unified floating controls (menus, popovers, comboboxes) into shared styling layer.

**Provider fix (merged, #priority: p1):**
- **#5236** `fix(anthropic): support Opus 5 effort controls` — replaces hard-coded exclusion lists with model-family version thresholds; adds `output_config.effort` for adaptive-only Claude models.

**Command quality (merged, #priority: p2):**
- **#5242** `fix(commands): reject malformed slash commands` — unknown commands now get closest-match suggestions rather than being forwarded to the LLM.

**Developer experience (merged, #priority: p1):**
- **#5239** `feat(webui): add integrated Vite dev mode` — one-command `nanobot webui --dev` with HMR, readiness checks, and sidecar cleanup.

**Security/auth (merged, #priority: p1):**
- **#5210** `feat(webui): support trusted proxy bootstrap auth` — tokenless auth for `/webui/bootstrap` via explicit CIDR allowlists + non-empty headers (Cloudflare Tunnel/Access use case).

## 4. Community Hot Topics

**Most active Issue — #4784 (open since 2026-07-06, 2 comments, 0 reactions):**
*Security: Provider API keys leaked between providers via global os.environ mutation* — [Link](https://github.com/HKUDS/nanobot/issues/4784)

The `OpenAICompatProvider._setup_env()` writes directly into process-global `os.environ`, causing multi-provider key collisions (gateway providers overwrite; non-gateway use `setdefault`). Critical for anyone running multiple provider configurations in one process.

**Most active PR — #4919 (open since 2026-07-14, 0 comments):**
*feat(telegram): support custom Bot API base URL and extra headers* — [Link](https://github.com/HKUDS/nanobot/pull/4919)

Self-hosted Bot API server or enterprise gateway support; open 3 weeks with no maintainer comments, indicating possible attention gap.

**High-priority open PR — #5238 (open since 2026-08-04):**
*refactor(session): remove request-scoped access grants* — [Link](https://github.com/HKUDS/nanobot/pull/5238)

Revokes the `Tool.available()` request-layer and `SessionAccessScope` abstraction introduced in #5211; session tools can now read all persisted sessions. This is a deliberate security simplification that possibly reverts #5211.

**Trending bug — #5237 (open since 2026-08-04, 1 comment):**
*MCP tool returns "data not found" envelope → agent ignores it* — [Link](https://github.com/HKUDS/nanobot/issues/5237)

`CallToolResult.content` with business-error JSON and `isError=False` misleads the LLM into thinking the call succeeded, wasting a full `tool_timeout` cycle.

## 5. Bugs & Stability

Sorted by severity:

**High (affects all Anthropic users of newest models):**
- **#5235** *(closed)* — Opus 5 temperature deprecation caused requests to be always rejected; substring list missing `"opus-5"`. **Fixed by #5236** (merged within 24h of report). Fast turnaround. Original: [Issue #5235](https://github.com/HKUDS/nanobot/issues/5235) | Fix: [PR #5236](https://github.com/HKUDS/nanobot/pull/5236)

**High (security, multi-provider deployments):**
- **#4784** *(open 30 days, 2 comments)* — os.environ key collision between providers; no fix PR visible yet. Long-unanswered security issue. [Issue #4784](https://github.com/HKUDS/nanobot/issues/4784)

**Medium (channel-specific, affects single deployments):**
- **#5247** *(open)* — Matrix bot fails to auto-join rooms with Continuwuity (`M_BAD_JSON` on empty POST body). **Fix PR #5248** is open and targets the issue precisely. [Issue #5247](https://github.com/HKUDS/nanobot/issues/5247) | [PR #5248](https://github.com/HKUDS/nanobot/pull/5248)
- **#5237** *(open)* — MCP business-error envelopes masquerade as success; agent waits out full timeout without detecting root cause. No fix PR yet. [Issue #5237](https://github.com/HKUDS/nanobot/issues/5237)

**Low:**
- **#5235** *(closed)* — see above, had second part about `opus-5` not in omission list; resolved by PR #5236.
- **#5156** *(open, PR)* — Telegram polling silently stalls after transient network blips; PR proposes recovery watchdog. [PR #5156](https://github.com/HKUDS/nanobot/pull/5156)

## 6. Feature Requests & Roadmap Signals

**Strong signal — merged, likely in next release:**
- **#5234** *(open PR, p1)* — MST (Meta-Search Tool) as new web search provider, aggregating DuckDuckGo/Google/Brave/Bing via Reciprocal Rank Fusion (RRF). If merged, becomes the most capable web search provider in Nanobot. [PR #5234](https://github.com/HKUDS/nanobot/pull/5234)
- **#5233** *(open PR, p2)* — Mattermost `groupPolicyInThread` separate mention requirements for threads vs main channels, exposed in WebUI. [PR #5233](https://github.com/HKUDS/nanobot/pull/5233)

**Community-prized, waiting for merge:**
- **#4919** *(open 3 weeks, p2)* — Custom Telegram Bot API base URL + headers (enterprise/self-hosted gateway). [PR #4919](https://github.com/HKUDS/nanobot/pull/4919)
- **#5184** *(open 5 days, p2)* — Quick Chat (persistent first-class destination) and Temporary Chat (connection-owned, in-memory history). [PR #5184](https://github.com/HKUDS/nanobot/pull/5184)

**Bug-driven request (security hardening):**
- **#4784** os.environ isolation is the single most impactful security feature request — providers must stop mutating process-global state.

## 7. User Feedback Summary

**Pain points expressed in the last 24h:**

- **Thread safety / env isolation (multitenancy)**: #4784 author pinpoints that running multiple gateway-type providers in one process silently corrupts API keys — a footgun for SaaS-style deployments.
- **Anthropic model compatibility churn**: #5235 author notes Nanobot's hard-coded substring lists keep lagging behind model deprecations; Opus 5 launch (2026-07-24) immediately broke requests. User dissatisfaction with reactive vs proactive provider compat.
- **MCP error semantics**: #5237 author reports concrete waste (agent waits for `tool_timeout`) and inability to self-heal — a meaningful failure mode in agentic tool orchestration.
- **Matrix/Continuwuity interoperability**: #5247 shows subtle differences in homeserver strictness breaking previously-working auto-join.
- **Telegram reliability**: #5156 (still open) — bot silently stops polling in production while process stays alive; log silence makes it hard to detect.

**Satisfaction signals:** high velocity of fixes in one area (WebUI polish was heavily driven by maintainer chengyongru), rapid Opus 5 turnaround (#5235 → #5236 in <48h), and community reviewers actively testing PRs.

## 8. Backlog Watch

**Issues needing maintainer attention:**

- **#4784 (security, open 30 days, 2 comments)** — Provider API key leakage via `os.environ`; no fix in sight. High user impact, security-critical. [Link](https://github.com/HKUDS/nanobot/issues/4784)

**PRs stalled (>2 weeks without maintainer action):**

- **#4919 (Telegram custom Bot API, open 21 days)** — No maintainer comments since 2026-07-14; filed against a long-standing request (#4702). [Link](https://github.com/HKUDS/nanobot/pull/4919)
- **#1776 (Telegram group_mode config field, open 149 days)** — Marked `[conflict]`; config silently ignored because the Pydantic schema is missing the field. This smells like a trivial `p2` merge that would close a 5-month-old gap for group bots. [Link](https://github.com/HKUDS/nanobot/pull/1776)

**Open PRs with potential merge-blocking conflicts:**

- **#5156 (Telegram polling stall recovery)** — open for 6 days, `p2`, no maintainer activity; production-relevant. [Link](https://github.com/HKUDS/nanobot/pull/5156)
- **#5184 (Quick Chat / Temporary Chat)** — open 5 days; a large feature that may need design review before merge. [Link](https://github.com/HKUDS/nanobot/pull/5184)

---

**Project Health Summary:** High-velocity maintenance with excellent fix turnaround (Opus 5 within 48h), active community contributor pipeline, and a clear shift toward WebUI polish and proper security boundaries. Risk factors: one 30-day-old security issue (#4784) and several long-open PRs including a 5-month-old trivial config field (#1776) that indicate maintainer bandwidth is concentrated on immediate issues rather than backlog hygiene.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest — 2026-08-05

## 1. Today's Overview

Project activity remains at a consistently high level, with 50 issues and 50 PRs updated in the last 24 hours. The overwhelming majority of this activity is in the "open" state (49 open/active issues, 45 open PRs), indicating a heavy inflight workload rather than rapid resolution—only 1 issue and 5 PRs were closed/merged today. The issue tracker shows a healthy influx of new bug reports (several filed 2026-08-04) and a steady stream of feature proposals and meta-issues (e.g., the extensive Telegram campaign). The PR queue shows an interesting pattern: a large number of open PRs appear to be recurring, long-running contributions that are being kept updated with rebases (e.g., #67934, #70667), a signal the maintainers are effectively managing a deep queue. While no new releases were cut today, the project is clearly in a high-velocity bug-fixing and feature-development phase, with a particular focus on stability (Windows platform, session state) and robustness (lifecycle guards, checkpointing).

## 2. Releases

No new releases were published in the last 24 hours. The latest active version appears to be v0.20.0 (build 2026.8.3), as referenced in several issue reports.

---

## 3. Project Progress

Only 5 PRs were closed or merged today. Active development is focused on hardening and parity:

- **Docker Environment Preservation (Merged/Closed)**: PR #33148, *"fix(docker): set S6_KEEP_ENV=1 to preserve container environment"* linked to issue #33148. This fixes a critical issue where s6-overlay v3 was stripping all Kubernetes/container-injected environment variables (API keys, `HERMES_HOME`, etc.) before the gateway process started. This was marked P1 and is a major infrastructure fix. (Closed)
- **Discord Messaging Tool (Closed)**: PR #75059, *"Feat/send message discord tool"* by YouKnowMeFromBefore. The PR description is sparse, but it adds a tool for sending Discord messages, directly addressing a [type/feature] gap.
- **CLI Model Sorting Fix (Closed)**: PR #78934, *"fix(cli): support 'k'/'K' version prefix in model sort"* by thatssoheil. This fix addresses a parsing bug that prevented Kimi models (e.g., `kimi-k3.5`) from being sorted correctly by version in the CLI's model switcher.
- **Recurring PRs advanced**: Several long-running PRs (e.g., #67934, #70667, #72671) were rebased onto current `main` to resolve conflicts and incorporate review feedback, indicating ongoing work to get these into mergeable state. These cover Ollama model discovery, kanban CLI refusal exit statuses, and gateway test fixture fixes.

---

## 4. Community Hot Topics

The most active discussions highlight pain points around session stability and workflow reliability.

- **[#62726] Dashboard cross-tab session bleed + /new hang** (Issue, 13 comments): This remains the most active issue by comment count. It describes a serious UX and stability bug where using the web dashboard's `/new` command while multiple tabs are open causes session bleed between tabs and a permanent hang, requiring a full container restart. This suggests a deep architectural issue in the dashboard's session state management.
- **[#76886] `read_file` reports valid UTF-8 text as binary** (Issue, 10 comments, 2 reactions): A high-impact regression in v0.19.1 affecting any user with multi-byte characters (like emoji) in their files near the 1000-byte sampling boundary. This breaks standard workflows (e.g., reading Obsidian notes) and has two thumbs-up, indicating broad user impact.
- **[#71837] Duplicate branch lanes in project sidebar on Windows** (Issue, 6 comments): A Windows-specific UI/UX bug where a single project shows two identical branch lanes due to a backend/frontend lane-id mismatch. This is confusing and clutters the interface, pointing to a lack of effective testing on the Windows desktop app.
- **[#69961] Add trusted sender UID envelope for shared gateway sessions** (Issue/PR, 5 comments): This feature proposal (and its companion PR #69980) is gaining traction as a security and functionality improvement. The underlying need is to properly authenticate users in multi-user shared sessions (Discord, Telegram) without relying on easily-forged text prefixes. This indicates a growing need for robust multi-user collaboration features.
- **[#46199] Windows Desktop portable/isolation deployment guidance** (Issue, 5 comments, 2 reactions): A user requests official documentation for installed without modifying the host system (PATH, etc.). Two reactions indicate this is a real pain point for privacy-conscious users evaluating the desktop app.

---

## 5. Bugs & Stability

Bug reports filed or updated today show several crucial and high-priority issues. No new P1 bugs were filed, but several P2s have significant impact.

**High Severity (P2, critical impact to core workflows):**

- **[#78888] Checkpoint `git add -A` aborts on root-owned cache** (Issue, no fix PR target found): A broken file permission in the `node-compile-cache/` directory can cause the entire checkpointing system to fail silently. The fix in PR #78944 (see below) is already inbound.
    - **Fix exists**: PR #78944, *"fix(checkpoint): one unreadable path no longer costs the whole snapshot"* is open to address this.
- **[#78942] lifecycle_guard crashes on NUL-bearing path** (Issue, fix PR inbound): This is a direct follow-up to the incomplete fix #76762. The crash can still be triggered by binary content in terminal output, crashing the guard and potentially the terminal call itself.
    - **Fix exists**: PR #78945, *"fix(lifecycle_guard): catch ValueError on null-byte paths in..."* is open to address this.
- **[#76886] read_file misidentifies valid UTF-8 as binary** (Issue, 10 comments): A regression from v0.19.1 that affects a core file-reading tool. This is still awaiting a fix or decision, making it a key candidate for the next patch release.
- **[#78820] TUI gateway crashes on Windows with OSError on stdin readline** (Issue): This is reported for v0.20.0 and causes an in-flight session to be completely lost. It highlights ongoing Windows-specific instability.
- **[#78932] Rejected MEDIA delivery paths are silent to the model** (Issue): A silent failure where the agent believes a message with an attachment was delivered, but the attachment was dropped due to a path validation failure. This is a critical trust-breaking bug, as the model has no way to know its output was modified.

**Medium Severity (P3):**

- **[#78933] Kanban tasks with `initial_status=blocked` auto-promote** (Issue): A guardrail violation where "blocked" tasks are not sticky and can be dispatched without human approval, defeating the purpose of the blocked status.
- **[#78122] `max_in_progress` is enforced per-board, not gateway-wide** (Issue): A regression in the kanban dispatch logic that can lead to resource overload when multiple boards are active.

---

## 6. Feature Requests & Roadmap Signals

The tracker shows a strong push towards Telegram parity and deeper desktop integration.

- **Telegram Bot API 10.2 Alignment Campaign** ([#78791, meta-issue]): This is a major, well-organized campaign to bring the Telegram adapter to full parity with the official API. It has already spawned multiple sub-issues and PRs (e.g., #78949 refactoring the adapter god-file, #78934 CLI sort, #72937, #76454), indicating an appetite for a major overhaul of the gateway plugin architecture. This is the strongest signal for upcoming features.
- **Configurable Credential Resolution for Anthropic** ([#78950, PR]): A user is proposing to make the provider token resolution order configurable, reducing reliance on Claude Code credentials over the native Her
mes pool. This suggests a desire for more control and isolation of credentials.
- **Desktop Quick Entry** ([#78250]): Users want a configurable default "Send to" destination for the Quick Entry bar (Current chat / New session / Remember last selection). This is a simple, UX-focused quality-of-life feature.
- **Phased Disk Winddown & Worktree Health Gate** ([#78914], [#78915]): Two related proposals from a single user emphasize resilience. The first proposes a "persist-before-delete" strategy for caches to avoid losing concurrent artifacts. The second proposes a self-healing worktree gate to survive contamination from multiple concurrent Hermes sessions. These address real pain points for power-users running automated campaigns.
- **Trusted Sender Envelope for Shared Sessions** ([#69980, PR]): The PR implementing the feature requested in #69961 is open and progressing. This points to a future where multi-user sessions are more secure and reliable.

---

## 7. User Feedback Summary

User pain points today fall into four clear categories:

1.  **Stability of Core Session Management**: The most significant frustrations come from memory/resource leaks and session handling. The OOM crash in TUI mode ([#12682]) and the dashboard session bleed plus hard hang ([#62726]) are leading to loss of work and requiring forced restarts. A Windows user reports an `OSError` losing an in-flight session ([#78820]).
2.  **Trust in Tool Output**: There is a clear push for the agent to be reliable and truthful. The silent dropping of attachments ([#78932]) means the model lies about its actions. Similarly, the `read_file` binary misclassification ([#76886]) breaks basic tooling, eroding confidence in file operations. The kanban "blocked" status not being sticky ([#78933]) directly relates to user trust in the automation guardrails.
3.  **Deployment and Installation Friction**:
    - **Windows-Specific Issues**: The desktop app faces unique challenges, including duplicate sidebar lanes ([#71837]) and a broken update process ([#76435], and the recovery PR #75752), indicating a less mature Windows experience.
    - **Portable Installation**: Users are explicitly requesting a deployment model that minimizes host system changes ([#46199]), indicating a desire for more enterprise-friendly/localized installs.
    - **Install Hangs**: Playwright Chromium installation hanging on some systems ([#76312]) is a significant blocker for new users.
4.  **Proactive Power-User Requests**: Experienced users are requesting features to make the agent safer for automated campaigns, including configurable credential order ([#78950]) and robust worktree isolation ([#78915]).

---

## 8. Backlog Watch

- **[#46199] Windows Desktop portable deployment guidance** (Since 2026-06-14): The issue has only been visited with a few comments and no maintainer update. The two 👍 shows user interest, and the detailed requirements in the issue warrant an official response defining the supported deployment models.
- **[#26277] Email session isolation by normalized subject** (Since 2026-05-15): This feature request has been open for nearly three months with two 👍. It seems functionally valuable but may be awaiting design decisions around the email adapters. Its persistence on the dashboard should be noted for roadmap planning.
- **[#35398] Native Supertonic TTS provider** (Since 2026-05-30): The PR is still open and updated today. Without a maintainer update or merge, this feature (adding a native integration to a potentially popular on-device TTS engine) has been stuck for over two months. It's a candidate for a maintainer decision or a request for more explicit user demand.
- **[#66668] Encoding-safety lint proposal** (Since 2026-07-18): The issue itself is helpfully nested within a campaign with a trigger condition, but the lack of any maintainer acknowledgment after several weeks suggests that it requires explicit scheduling or a green light for the work to be merged.

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

Here is the PicoClaw project digest for 2026-08-05.

---

# PicoClaw Project Digest — 2026-08-05

## 1. Today's Overview
Activity is **moderate**, with a healthy mix of bug reports and feature contributions. Three issues and four PRs were updated, but the majority of these (3 out of 7 total items) were closed by the stale bot rather than through explicit maintainer action. The most significant development is a new PR (#3317) targeting observability for prompt caching, which aligns with the closure of a prior PR (#3251) on the same topic. While there are no new releases, the open PRs suggest the project is actively moving toward better web search integration and improved logging. The primary risk factor remains the presence of a critical hang bug in the agent loop related to MCP connectivity.

## 2. Releases
No new releases were published in the last 24 hours. The latest tagged version remains **v0.3.1**, referenced in several recent bug reports.

## 3. Project Progress
No PRs were merged in the last 24 hours.
- **Closed (via Stale Bot):**
  - **[PR #3280](https://github.com/sipeed/picoclaw/pull/3280):** fix(auth): make browser OAuth login survive real-world callback conditions. Authored by honbou. This PR addressed four separate causes of OAuth failures in headless/remote setups. It was closed by stale bot after 14 days, suggesting it may have been abandoned or superseded.
  - **[PR #3251](https://github.com/sipeed/picoclaw/pull/3251):** fix(providers): capture the prompt cache token usage in Anthropic providers. Authored by hydrogenbond007. While the PR was closed stale, a **new PR (#3317)** was opened today addressing the same code area (see below), indicating the fix is being re-implemented with a broader scope.

## 4. Community Hot Topics
- **[Issue #3281](https://github.com/sipeed/picoclaw/issues/3281) — "Web UI chat input is very laggy" (👍 1):** Users with longer chat histories are experiencing significant input lag in the Web UI. This is a performance/usability complaint concerning a core interface (the chat box) at a specific version (0.3.1). The active discussion implies this is a common frustration affecting the main user workflow.
- **[Issue #3269](https://github.com/sipeed/picoclaw/issues/3269) — "MCP server connection failure hangs the agent loop" (👍 1):** This is a high-severity reliability issue where a failed MCP connection causes the entire agent loop (and therefore the chat interface) to stop responding. This blocks users from using the "tool" aspect of the agent entirely when a server is misconfigured or down.

## 5. Bugs & Stability
- **High Severity — Agent Hang on MCP Failure ([Issue #3269](https://github.com/sipeed/picoclaw/issues/3269)):** The agent loop hangs indefinitely if an MCP server connection fails, freezing the chat. No fix PR is currently linked. This is the most critical stability issue as it brick-walls the entire agent functionality.
- **Medium Severity — UI Performance ([Issue #3281](https://github.com/sipeed/picoclaw/issues/3281)):** Input lag in the Web UI increases with history length. This is a DoS-lite self-inflicted by usage; it degrades the experience but does not break functionality.
- **Low Severity — Android Path/Service Issues ([Issue #3182](https://github.com/sipeed/picoclaw/issues/3182)):** Users are unable to launch the service on Android and cannot change the path from settings. This was closed stale as it lacked maintainer response or user follow-up.

## 6. Feature Requests & Roadmap Signals
- **Prompt Cache Observability (Fixing #3251 via [#3317](https://github.com/sipeed/picoclaw/pull/3317)):** The new PR by vmuliadi-astro aims to log prompt cache tokens in the LLM response debug output for providers like DeepSeek. This indicates a push for **better cost transparency and debugging capabilities** for users of caching-enabled models. This is likely to be merged quickly.
- **Native Exa Web Search ([PR #3299](https://github.com/sipeed/picoclaw/pull/3299)):** A contributor has submitted code to add Exa as a native web search provider, supporting date filters. This is a direct expansion of the `tools.web` capability, suggesting the community desires alternative search backends to the default. This feature looks promising for a future minor release (v0.4.x).

## 7. User Feedback Summary
- **Pain Point (Critical):** Users are being fully blocked by MCP integration failures (Issue #3269). The lack of timeout or retry logic in the agent loop is a significant trust-breaker for users relying on third-party tools.
- **Pain Point (UX):** The Web UI's performance deteriorates quickly with history, making it hard to maintain long working sessions (Issue #3281).
- **Dissatisfaction:** The closed Issue #3182 regarding Android functionality was not addressed, indicating a potential gap in support or a bug in the mobile build.
- **Satisfaction:** The submission of PRs (#3299, #3317) from various users suggests a healthy ecosystem where developers are willing to contribute fixes and features back upstream.

## 8. Backlog Watch
- **[Issue #3182](https://github.com/sipeed/picoclaw/issues/3182) — Android Service Launch Failure:** Closed by stale bot, but the underlying bug (inability to launch service or change path on Android) remains unresolved for actual users. Maintainers should either confirm this is fixed in the nightly build or reopen with a request for updated logs.
- **[PR #3299](https://github.com/sipeed/picoclaw/pull/3299) — Exa Web Search Provider:** The PR has been open for 10 days without comments. It is a fully formed feature with implementation details. This needs a maintainer review (approve/comment/close) to signal if it is welcome, as the "stale" threshold is approaching.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-08-05

## 📌 Today's Overview

NanoClaw shows a **moderate activity day** with **zero new issues** opened in the last 24 hours, but a **healthy pipeline of 5 pull requests** in various states (4 open, 1 merged). No new releases were published today, indicating the project is in a **development/iteration phase** rather than a stabilization phase. The most significant signals are the recent merges of a long-pending scheduled-tasks fix and a high-priority Discord approval bug fix, both from the core team. Open PRs for new Dial channel support (SMS/AI voice) and a refactor for skill-owned capabilities suggest **active feature development** is underway, though the extended open duration of the Dial PRs (3+ weeks) may warrant attention.

## 🚀 Releases

No new releases were published in the last 24 hours. The project appears to be between release cycles, with merged fixes pending publication.

## 🧩 Project Progress

**Merged/Closed PRs:**

- **PR #3154** — `fix(agent-runner): give scheduled tasks current run time` — **Merged** (core-team)  
  This fix ensures scheduled tasks receive the correct effective occurrence time (`process_after`), falling back to creation timestamp for legacy rows. It also generates a task-only `current_time` field including weekday information when the task reaches the agent. This resolves a long-standing timing discrepancy in scheduled task execution.  
  [View PR](https://github.com/nanocoai/nanoclaw/pull/3154)

## 💬 Community Hot Topics

No issues or PRs have significant comment/reaction activity today. However, the most **active discussion-adjacent items** based on update frequency are:

- **PR #3185** — `fix(discord): strip \n delimiter in webhook interaction custom_id` — **Recently updated (today)**  
  This is a **critical fix** for Discord approval interactions where every button click was resolving to "Reject." Users are likely experiencing broken approval flows, making this the most operationally urgent item.  
  [View PR](https://github.com/nanocoai/nanoclaw/pull/3185)

- **PR #3050 & #3041** — Dial channel adapter and wizard integration — Both updated today after a 3-week quiet period, suggesting renewed maintainer attention.  
  [View PR #3050](https://github.com/nanocoai/nanoclaw/pull/3050) | [View PR #3041](https://github.com/nanocoai/nanoclaw/pull/3041)

**Underlying need:** The Discord fix addresses a user-facing reliability issue in approval workflows; the Dial PRs indicate community demand for SMS/voice AI communication channels.

## 🐛 Bugs & Stability

**High Severity:**
- **Discord Approval Always Rejects** — PR #3185 (open, fix available)  
  The `custom_id` decoding in the webhook interaction path splits on `:` and leaves a `\n` delimiter, causing **every approval to be rejected** even when the user clicks Approve. This is a **user-blocking regression** in the Chat SDK bridge. A fix PR exists and is open.  
  [View PR](https://github.com/nanocoai/nanoclaw/pull/3185)

**Medium Severity:**
- **Scheduled Tasks Time Discrepancy** — PR #3154 (merged today)  
  Scheduled tasks were receiving creation time instead of effective scheduled occurrence. **Resolved** with today's merge.  
  [View PR](https://github.com/nanocoai/nanoclaw/pull/3154)

## 🔮 Feature Requests & Roadmap Signals

The following features are in-flight and likely targeted for the next release:

1. **Dial Channel Support (SMS + AI Voice Calls)** — PRs #3041 and #3050  
   Two-PR feature set: a channel adapter (SMS/AI voice) and a channel-picker wizard integration using a `runChannelSkill` model. This is a **major feature addition** expanding NanoClaw's channel ecosystem beyond chat platforms. Given the 3-week open duration and today's activity, this may be approaching merge readiness.  
   [View PR #3041](https://github.com/nanocoai/nanoclaw/pull/3041) | [View PR #3050](https://github.com/nanocoai/nanoclaw/pull/3050)

2. **Host Seams for Skill-Owned Capabilities** — PR #3186  
   A refactoring effort to add host seams, likely enabling cleaner skill isolation and custom capability injection. This is groundwork for future extensibility rather than a user-facing feature.  
   [View PR](https://github.com/nanocoai/nanoclaw/pull/3186)

**Prediction:** The Dial channel feature set (both PRs) is a strong candidate for the next minor release, possibly alongside the Discord fix (via a patch release).

## 🗣️ User Feedback Summary

- **Pain Point (Actionable):** Discord users are experiencing **broken approval flows** — every approval is rejected. This is a severe UX regression for teams relying on Discord for human-in-the-loop approvals.
- **Use Case (Growing):** Interest in **SMS and voice AI calling** as communication channels (via the Dial PRs) suggests users want to extend NanoClaw beyond chat into telephony-based interactions.
- **Satisfaction Indicator:** The active PR work by core-team and contributors indicates responsive maintenance; however, the **0 open issues** is notable — either the community is not filing bugs or issues are being triaged and closed quickly.

## ⏳ Backlog Watch

- **PR #3041 & #3050** — Dial channel PRs have been open for **22 days** without merge. They were updated today, which is positive, but items this large risk accumulating conflicts. Maintainers should prioritize review to avoid staleness.  
  [View PR #3041](https://github.com/nanocoai/nanoclaw/pull/3041) | [View PR #3050](https://github.com/nanocoai/nanoclaw/pull/3050)

- **PR #3186** — New refactoring PR (1 day old) with no comments yet. Low risk, but early review would help maintain momentum.  
  [View PR](https://github.com/nanocoai/nanoclaw/pull/3186)

**No long-unanswered issues identified** — the issue tracker is clear as of today.

---

*Digest generated from GitHub data on 2026-08-05. All links reference the NanoClaw repository (nanocoai/nanoclaw).*

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

Here is the NullClaw project digest for 2026-08-05.

---

# NullClaw Project Digest — 2026-08-05

## 1. Today's Overview
Project activity is at a low ebb, with **zero issues updated** and **zero new releases** in the last 24 hours. The sole item of activity is a single open Pull Request (#981) that has been idle for nearly a week (last updated 2026-08-04), indicating a plateau in active development. No issue tracker activity suggests that community feedback loops are currently dormant, and user engagement is minimal. The project appears to be in a stabilization phase, with maintainers focused on consolidating existing features rather than pushing new ones. The lack of incoming bugs or feature requests also suggests the software is currently considered stable by its user base.

## 2. Releases
**No new releases** were published in the last 24 hours. The previous release cycle has concluded, and no upcoming version tags are visible in the provided data. Omit subsequent sections regarding specific changelogs or migration paths until new versions are tagged.

## 3. Project Progress
**No PRs were merged or closed** in the last 24 hours. The only active PR remains open and awaiting review (see Section 4). No new commits or merged features can be attributed to today's date.

## 4. Community Hot Topics
**PR #981: [OPEN] feat(provider): add grok-cli provider for xAI Grok CLI**
- **Author:** valonmulolli
- **Created:** 2026-07-29 | **Updated:** 2026-08-04
- **Link:** [NullClaw PR #981](https://github.com/nullclaw/nullclaw/pull/981)

This is the sole community contribution currently in flight. The PR proposes a new CLI-based provider that delegates to the local `grok` CLI, following the established `spawn-per-request` pattern used by `codex-cli`, `gemini-cli`, and `claude-cli` providers. The underlying need here is clear: users want to use xAI’s Grok models through the same unified interface they already use for other local CLI tools, without requiring API-key management or library dependencies. The fact that the author flagged this as **optional** suggests they are aware of the dependency on a locally installed binary and are advocating for a "bring-your-own-CLI" approach to model integration.

## 5. Bugs & Stability
**No bugs, crashes, or regressions** were reported or updated in the last 24 hours. The issue tracker is completely clear (0 open/closed/active issues today), indicating a healthy, stable codebase with no immediate stability threats. No severity rankings are required as no incidents exist.

## 6. Feature Requests & Roadmap Signals
While no new feature requests appeared in the issue tracker today, the existence of **PR #981** serves as a strong signal for the roadmap. The continued expansion of CLI-based providers (already supporting Codex, Gemini, and Claude) implies a strategic pattern: **NullClaw is moving towards a "provider-agnostic" architecture where any local terminal-based AI agent can be plugged in**. It is highly likely that this `grok-cli` provider will be merged into the next minor release, provided it passes code review. Users can anticipate future similar providers for other emerging CLI tools (e.g., Ollama or local LLM runtimes), as the maintainers appear to favor this lightweight integration strategy over heavyweight native SDKs.

## 7. User Feedback Summary
**Quantitative data is sparse**—the sole PR has zero comments and zero reactions, and the issue tracker is empty. However, the qualitative signal from **PR #981** indicates a user desire for **modularity and local-first execution**. The author specifically notes the requirement for a pre-installed `grok` CLI, implying that users are comfortable managing external binaries to avoid bloated dependencies. The lack of complaints or bug reports suggests a baseline level of user satisfaction, though the absence of engagement (upvotes/comments) makes it difficult to assess enthusiasm. The community appears to be quiet but trusting of the current architecture.

## 8. Backlog Watch
**PR #981** is the only item on the board and warrants immediate maintainer attention. It has been **idle for 7 days** since its last update, which is a long time for a feature PR in an active project. Maintainers should review the code to ensure it adheres to the `codex-cli` standards and either request changes (to keep momentum) or merge it. There are no other issues or PRs at risk of being forgotten. The absence of a backlog means the project health is good, but the stale status of this 7-day-old PR suggests a bottleneck in the review pipeline.

---

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

# IronClaw Project Digest — 2026-08-05

## 1. Today's Overview

IronClaw shows **very high activity** across the board with 50 issues and 50 PRs updated in the last 24 hours. The project is in the **middle of a major architectural restructuring** ("Reborn" / WS-series work) targeting the 1.1.0 release, with multiple large stacked PRs in flight (Waves 0–4 batches). The issue tracker reveals **significant process discipline**: a dedicated "doc-truth audit" surfaced several structural defects (untracked architecture ratchet baselines, unowned migration CHECKLIST rows, misconfigured tracing targets), and there's an unusual pattern of **"filed rather than patched"** issues — indicating maintainers deliberately separate defect discovery from behavior-changing fixes. While no new releases landed today, the PR queue shows **11 merged/closed items** and roughly a dozen substantial open PRs from core contributors. The epic #6284 on error-recoverability and #6565 on reliable skill discovery remain central themes, with user-reported feedback (Champions weekly check-in) driving new issues around memory persistence, per-user model selection, and web scraping reliability.

---

## 2. Releases

**No new releases in the last 24 hours.**

The most recent tagged versions referenced in the issues are `ironclaw-v1.0.0-rc.1` and `ironclaw-v1.1.0-rc.1` — the latter is actively being cut, with at least 3 Windows-specific defects (parent-directory fsync #7182, ACL account resolution #7197, and others) blocking it.

---

## 3. Project Progress

**Merged/Closed PRs in the last 24 hours (11 total):**

| PR | Description | Significance |
|---|---|---|
| [#7170](https://github.com/nearai/ironclaw/pull/7170) | **Waves 0–4 batch**: WS3/WS4 consolidation + lane governor port + conversations sever + WS10 inventory keying + enforcement gates | **Major milestone** — supersedes and closes #7141, #7160, #7159, #7161, #7156. The 5-component batch landed with zero conflicts per the consolidation protocol. |
| [#7021](https://github.com/nearai/ironclaw/pull/7021) | Dependabot: wasm group (wit-component/wit-parser) | Routine dependency bump |
| [#5003](https://github.com/nearai/ironclaw/pull/5003) | Fix stranded local-dev SSO automations, surface fire-failure reason (#4992) | **Long-running fix (since June 17) finally merged** — resolves a Railway-hosted Reborn production issue where scheduled automations failed silently at fire time |

**Key PRs still open that are driving the architecture program forward:**

- [#7181](https://github.com/nearai/ironclaw/pull/7181) — Waves 0–4 **batch 2** (final content batch), stacked on #7170
- [#7187](https://github.com/nearai/ironclaw/pull/7187) — WS6: RebornRuntime slimming, typed ExtensionId, domain cleanups, ref-store collapse
- [#7186](https://github.com/nearai/ironclaw/pull/7186) — WS6: evict the service cluster from composition (admin users, trace capture, route mounts)
- [#7179](https://github.com/nearai/ironclaw/pull/7179) — WS6: mcp/auth/webui module charters (real code moves, e.g., 2,767-line `lib.rs` → 7 modules)

**Progress signals:** The consolidation protocol (merge-in-dependency-order, never rebase, union verification) is working as intended — #7170's batch merged cleanly into main, and batch 2 (#7181) is ready behind it.

---

## 4. Community Hot Topics

**Most active issues by comment count:**

1. **[#6284 [CLOSED] — Epic: Error-recoverability endgame](https://github.com/nearai/ironclaw/issues/6284)** (15 comments) — The model recovers from 100% of errors it sees. Closed as part of the v1.1.0 epic set. The recoverability contract mandates: run survives, model sees error, cause + fix guidance present, model gets a turn to act.

2. **[#6524 [CLOSED] — Epic: Hermetic capability and journey testing platform](https://github.com/nearai/ironclaw/issues/6524)** (4 comments) — Wants a mechanical answer to "Does every capability and journey have deterministic coverage?" beyond recorded fixtures.

3. **[#7119 [CLOSED] — Code Style clippy is package-set-dependent](https://github.com/nearai/ironclaw/issues/7119)** (4 comments) — Main branch fails `cargo clippy` for the `{ironclaw, ironclaw_reborn_config}` set at `dfdd02b9fb`. Root cause: `--lib` flag hard-errors on bin-only packages.

4. **[#6752 — Instance deletion fails, "Loading your agents..." stuck](https://github.com/nearai/ironclaw/issues/6752)** (3 comments) — Real user-facing production bug with stale UI state.

5. **[#7145 — extension_host → loops re-layer correctly sized](https://github.com/nearai/ironclaw/issues/7145)** (3 comments) — Successor to #7092; the file-count sizing approach was wrong; four-port residue is the correct metric.

**Observed pattern:** The most "commented" issues are disproportionately **internal process/architecture** concerns (epics, CI, clippy, migration planning) rather than user-facing features. This reflects the project's current phase — deep architectural restructuring with a strong QA/measurement culture.

---

## 5. Bugs & Stability

**Ranked by severity:**

| Severity | Issue | Fix PR Exists? |
|---|---|---|
| 🔴 **High** | [#6752](https://github.com/nearai/ironclaw/issues/6752) — **Instance deletion fails**, "Loading your agents..." stuck on re-login (production, user-facing) | No |
| 🔴 **High** | [#7168](https://github.com/nearai/ironclaw/issues/7168) — **Agent-installed skills invisible**: `skill_install` writes to a store discovery never reads; skill can't be activated (CLOSED — likely fixed) | Yes (closed) |
| 🟠 **Medium** | [#7192](https://github.com/nearai/ironclaw/issues/7192) — WebUI optimistic user messages render **below** agent output → conversation reads out of order | No |
| 🟠 **Medium** | [#7191](https://github.com/nearai/ironclaw/issues/7191) — `builtin.time` can't parse "24 hours ago"; returns opaque `input_error()` instead of typed issue. **Observed in production thread** | No |
| 🟠 **Medium** | [#7115](https://github.com/nearai/ironclaw/issues/7115) — Docker entrypoint gates legacy-Slack migration on **dead env var** (`IRONCLAW_REBORN_SLACK_ENABLED` no longer used) | No |
| 🟠 **Medium** | [#7104](https://github.com/nearai/ironclaw/issues/7104) — Extractors report "no text found" as **Failed** instead of **Empty**, misleading the model | No (filed for its own PR/test) |
| 🟡 **Low** | [#7103](https://github.com/nearai/ironclaw/issues/7103) — Latency-trace field computed even when tracing is off (wasted bytes per tool call) | No |
| 🟡 **Low** | [#7146](https://github.com/nearai/ironclaw/issues/7146) — **121 call sites** use `target = "…"` (field) instead of `target: "…"` (metadata) — those events are invisible to their own filters | No |
| 🟡 **Low** | [#7147](https://github.com/nearai/ironclaw/issues/7147) — Two architecture-ratchet shrink counts have **untracked slack on main**; open PRs hold 3 different values of the same baseline | No |
| 🟡 **Low** | [#7151](https://github.com/nearai/ironclaw/issues/7151) — Composition's share-based budget is poisoned by feature inflow — **the god crate can re-accrete while the gate stays green** | No |

**Tracing defect cluster:** #7146 (121 sites), #7103 (unconditional computation), and #7104 (wrong outcome classification) together suggest a **systemic issue in the tracing/observability layer** — filters silently not matching, unnecessary overhead, and model-facing text inaccuracies.

---

## 6. Feature Requests & Roadmap Signals

**User-facing feature requests (from Champions check-in and production threads):**

1. **[#7183 — Per-user LLM model selection](https://github.com/nearai/ironclaw/issues/7183)** — Admin-only today; marketing user (Jeremy Koch) wants self-service model choice. **Roadmap prediction:** High-value, low-architectural-risk; likely for v1.1.0 or v1.2.0.

2. **[#7193 — Run-now (manual fire) for automations](https://github.com/nearai/ironclaw/issues/7193)** — No way to fire an automation on demand from model/WebUI/product surface. **Roadmap prediction:** Strong candidate for v1.1.0 — complements the recently-merged #5003 (fire-failure reason surfacing).

3. **[#7194 — Admin-allowed shared channels as outbound targets](https://github.com/nearai/ironclaw/issues/7194)** — Agent can post to Slack channels but can't register them as the *host's* outbound delivery target. **Already has a fix PR:** [#7195](https://github.com/nearai/ironclaw/pull/7195) — likely to merge soon.

4. **[#7177 — Schema-aware ranked search for deferred tool retrieval](https://github.com/nearai/ironclaw/issues/7177)** — Tool discovery ranks poorly because canonical capability vocabulary lives in tool schemas, not top-level descriptions. **Roadmap prediction:** Aligns with the skill-discovery epic (#6565/#6941); medium priority for v1.1.0.

**Architecture-program signals (from the WS-series):**
- [#7145](https://github.com/nearai/ironclaw/issues/7145) — The extension_host → loops re-layer should be **sized by four-port residue**, not file count.
- [#7148](https://github.com/nearai/ironclaw/issues/7148) — conversations → turns (WS5) has **no owning CHECKLIST row**; Wave 3 milestone "exceptions 12 → 0" is unreachable as scheduled.
- [#3773](https://github.com/nearai/ironclaw/issues/3773) — Target crate architecture epic is **the umbrella** for all of this; likely lands in v1.2.0.

---

## 7. User Feedback Summary

**Source:** 2026-07-23 IronClaw Champions weekly check-in (channel: `#x-ai-product-feedback`), filed 2026-08-04.

| Pain Point | Issue | User Context |
|---|---|---|
| **Memory not reliably recalled across conversations** | [#7185](https://github.com/nearai/ironclaw/issues/7185) | Devon (legal, relayed by Tobias): info from one conversation not available in later ones. **Top existential concern for the product.** |
| **Web scraping is hit-or-miss** | [#7180](https://github.com/nearai/ironclaw/issues/7180) | Michael Kelly (builder ops): "some sources succeed, others fail outright, no clear pattern" — agent uses `http` tool instead of `web_search` |
| **Cannot choose LLM model per-user** | [#7183](https://github.com/nearai/ironclaw/issues/7183) | Jeremy Koch (marketing): admin (Tobias) must set the model for everyone |
| **Instance deletion fails, UI stuck** | [#6752](https://github.com/nearai/ironclaw/issues/6752) | elliot.braem (Slack): "Loading your agents..." on re-login after delete attempt |
| **Payments/credits issues recurring** | [#7105](https://github.com/nearai/ironclaw/issues/7105) | Community member: proposes extracting identity/session + payments out of the cloud API into a dedicated service |

**Satisfaction signals:** The Champions program is producing **consistent, structured, well-contextualized feedback** — a healthy sign for product-market fit. The "miss" themes (memory, web scraping, model selection) are feature-level, not fundamental rejection.

---

## 8. Backlog Watch

**Issues/PRs that have been open for an extended period and deserve maintainer attention:**

| Item | Age | Status | Why It Matters |
|---|---|---|---|
| **[#5598 — Release PR](https://github.com/nearai/ironclaw/pull/5598)** | **Open since 2026-07-03 (33 days)** | Auto-generated release (ironclaw_common 0.4.2→0.5.0, ironclaw_skills 0.3.0→0.4.0 with **breaking changes**) | Publishing is blocked while the 1.1.0-rc work proceeds; but crates users can't get breaking releases. |
| **[#3773 — Epic: Target Crate Architecture](https://github.com/nearai/ironclaw/issues/3773)** | Open since 2026-05-19 (~78 days) | Epic; actively worked via WS series | Will likely remain open into v1.2.0; the umbrella for most ecosystem churn. |
| **[#5101 — CI: reuse cargo-component installer](https://github.com/nearai/ironclaw/pull/5101)** | Open since 2026-06-20 (~46 days) | Continuous integration improvement from new contributor `theredspoon` | The only stale open PR from a *new* contributor — would benefit from maintainer review/triage. |
| **[#7105 — Evaluate dedicated identity/payments service](https://github.com/nearai/ironclaw/issues/7105)** | Open 1 day, but labeled "p2, feedback" | User-proposed architecture change for the cloud API | A signal that payments/identity concerns are **structurally awkward** in the current codebase — recurring theme. |
| **[#6947 — classify-test-scope.sh glob bug](https://github.com/nearai/ironclaw/issues/6947)** | Open since 2026-07-31 (5 days) | `ironclaw_product` mis-bucketed as legacy-only in CI path-keying | Pre-existing on main; CI scope misclassification could silently skip tests. |

### Project Health Assessment

**Strengths:**
- **Strong process discipline**: consolidation protocol, doc-truth audits, "filed rather than patched" separation of concerns, rigorous CHECKLIST tracking — rare and valuable in OSS.
- **Healthy contributor pipeline**: new contributors (`Kampouse`, `theredspoon`, `henrypark133`, `thisisjoshford`, `pranavraja99`) are landing substantial work (Nostr host functions, proxy diagnostics, Windows fixes).

**Watch items:**
- **Large stacked PR chains**: #7170 → #7181 → #7187/#7186/#7179. If any mid-chain PR stalls, downstream batch reconciliation overhead grows.
- **User-facing regressions during restructure**: #6752 (instance deletion), #7168 (skills invisible), #7185 (memory) — suggests the restructure's internal momentum can outpace external reliability.
- **Release starvation**: crates.io users haven't received breaking updates in 33+ days (#5598 open) while the project focuses on 1.1.0-rc.1 preflight fixes.
- **Windows-specific blockers to 1.1.0-rc.1**: the third Windows defect (#7197) is now being fixed — the release was previously blocked on the parent-directory fsync bug (#7182, already fixed).

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-08-05

## 1. Today's Overview

LobsterAI shows **high activity and a healthy release pipeline** today. The project merged 10 PRs and has 3 still open, indicating strong, sustained development momentum. The most significant milestone is the **Release: 2026.8.3 merge into main**, which bundles several user-facing features, including a new startup credit campaign, Artifact auto-preview control, and Windows installer stability fixes. While overall health is good, one **open security issue (sensitive model key leakage)** from April remains unresolved, warranting attention. Notably, a large batch of **stale dependency-update PRs** (Electron, React, HeadlessUI) were closed today, likely to clean up the backlog before the release merge.

## 2. Releases

No new releases were published today. The most recent release (tag `2026.8.3`) was merged into the main branch via PR #2430, but no formal release was cut. The upcoming release will include:
- Native credit-reward activities
- Streamlined first-run login experience
- Artifact auto-preview toggle
- Improved model-error handling (capacity overload classification)
- Windows installer reliability fixes

No breaking changes or migration notes were reported.

## 3. Project Progress

Ten PRs were merged/closed today, focusing on the finalization of the `2026.8.3` release:

**Core Features & Fixes:**
- **[#2424] Restore active credits campaign** — Reverted a prior change to keep the campaign live while active; restores the 500-credit claim flow and UI.
- **[#2427] Bundle startup credit campaign artwork** — Localized poster/CTA bundles for the startup offer modal.
- **[#2428] Complete startup campaign analytics** — Full login redirect URL reporting and error messaging for campaign claims.
- **[#2429] Optimize login page** — Streamlined the first-run login experience.
- **[#2425] Artifact auto-preview toggle** — New setting to disable automatic file preview; manual previews preserved.
- **[#2426] Classify model capacity overload separately** — Fixes misleading rate-limit errors; dedicated `ModelOverloaded` classification.

**Dependency/Diff Housekeeping:**
- **[#1282, #1283, #1284]** — Closed stale Dependabot PRs for `@headlessui/react`, `react`, and `react-syntax-highlighter`; were not merged, likely superseded by newer versions.

## 4. Community Hot Topics

The most discussed item today remains the **open security issue**, with 1 comment:

- **[#1202: [bug] agent leaks model key information**](https://github.com/netease-youdao/LobsterAI/issues/1202) — This security vulnerability asks the agent to prevent leaking API key/config info when directly queried. Reported in April, still open and not referenced by any fix PR. Underlying need: **robust prompt-level security hardening and sensitive-data redaction.**

Other items saw minimal community engagement (0 comments), indicating most conversation is happening internally via the release process rather than on GitHub.

## 5. Bugs & Stability

**Critical/High Severity:**
- **[#1202: Model key information leakage**](https://github.com/netease-youdao/LobsterAI/issues/1202) — Unresolved. The agent will reveal configuration file locations, environment variables, and model key info when prompted. No fix PR exists. This is the highest-priority open bug and has been open for over 4 months.

**Medium Severity (fixed today):**
- **[#2426: Capacity overload misreported as rate limit**](https://github.com/netease-youdao/LobsterAI/pull/2426) — Merged; users were misled into retrying when providers were overloaded. Now separately classified.

**Lower Severity (fixed today):**
- **Windows installer reliability improvements** included in the `2026.8.3` release merge.

## 6. Feature Requests & Roadmap Signals

No new user-published feature requests came in today; however, **in-flight features signal roadmap direction**:

- **Credit/reward campaigns** (PRs #2424, #2427, #2428) — The team is investing heavily in gamified credit rewards to drive onboarding and retention.
- **Artifact auto-preview toggle** ([#2425](https://github.com/netease-youdao/LobsterAI/pull/2425)) — Addresses users' desire for control over disruptive auto-preview behavior.
- **Opening PR #2374** — A community-submitted feature to **permanently hide the sidebar ad banner**, currently under review. Given a user asked for it, expect this or similar monetization/UX tradeoff controls soon.

## 7. User Feedback Summary

- **Pain point (security):** The open bug #1202 shows users are concerned about sensitive data exposure. The reporter explicitly states the agent should "refuse to reveal key info" — indicating a strong expectation for **privacy-preserving agent behavior**.

- **Pain point (UX):** PR #2374's request to hide the sidebar ad banner indicates **annoyance with persistent in-product ads**, a common friction point in free-tier desktop apps.

- **Satisfaction signal:** The flurry of closed release PRs suggests a well-oiled internal release process; however, **low external community engagement** (0 reactions on everything) suggests the user base interacts primarily through product usage/telemetry, not GitHub.

## 8. Backlog Watch

- **[Issue #1202 — Security key leakage (open since 2026-04-01)**](https://github.com/netease-youdao/LobsterAI/issues/1202) — 127 days old. This is a **security-hygiene liability** requiring immediate maintainer attention, as it undermines user trust.

- **[PR #1205 — Session rename error toast (open since 2026-04-01)**](https://github.com/netease-youdao/LobsterAI/pull/1205) — stale 4-month-old PR with a clear user-facing fix (missing feedback on rename failures). Should be reviewed/merged or closed explicitly.

- **[PR #1277 — Electron major bump (43.x)**](https://github.com/netease-youdao/LobsterAI/pull/1277) — Long-pending major dependency update. While the group-bump was proposed in April, it hasn't merged, potentially leaving security patches unapplied.

</details>

<details>
<summary><strong>TinyClaw</strong> — <a href="https://github.com/TinyAGI/tinyagi">TinyAGI/tinyagi</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>Moltis</strong> — <a href="https://github.com/moltis-org/moltis">moltis-org/moltis</a></summary>

# Moltis Project Digest — 2026-08-05

## 1. Today's Overview

Moltis is in a **low-activity maintenance phase** today. No issues were updated in the last 24 hours, and no new releases were published, indicating that the project is stable with no reported regressions or bug reports. The sole activity is a **single open dependency bump PR** (#1184) targeting the website's `undici` package, which is an automated Dependabot submission awaiting review. With zero open issues and zero merged PRs, the project shows no signs of user-facing churn, but also limited active development velocity. Maintainers have a clean queue and the main action item is reviewing and merging the dependency update to keep the website's supply chain current.

## 2. Releases

No new releases were published in the last 24 hours. The last release remains the previously published version. No release notes, migration guides, or breaking change announcements are due today.

## 3. Project Progress

**No merged or closed PRs today.** The only PR update is:

- **[#1184 — chore(deps-dev): bump undici from 7.28.0 to 7.29.0 in /website](https://github.com/moltis-org/moltis/pull/1184)** *(Open)* — An automated dependency bump submitted by Dependabot. This is a patch-level update within the `npm_and_yarn` group, limited to the website subdirectory. No feature work, bug fixes, or architectural changes progressed today.

## 4. Community Hot Topics

No issues were updated in the last 24 hours, and the only active PR is a routine dependency bump with **no comments and no reactions**. There are no community discussions, feature debates, or design conversations currently active. The underlying need expressed by the sole PR is **supply-chain hygiene** — keeping the website's HTTP client (`undici`) current with upstream security and performance fixes. While not community-driven, this signals that the project's automated maintenance pipeline is functioning correctly.

## 5. Bugs & Stability

**No bugs, crashes, or regressions were reported today.** With zero open issues and zero closed issues in the last 24 hours, there are no known stability concerns to rank or triage. The only relevant action is preventive: the pending `undici` bump (#1184) should be merged to ensure the website remains protected against any patched vulnerabilities in the older 7.28.0 version.

## 6. Feature Requests & Roadmap Signals

No user-submitted feature requests were filed or updated today. There are no roadmap signals in the current issue queue. The project's direction appears stable, with no external pressure for new capabilities. Based on the low activity, the next release is more likely to be a **routine maintenance release** (dependency bumps and polish) rather than a feature-forward version.

## 7. User Feedback Summary

With **zero issues updated** and **zero comments** across all items, there is no direct user feedback to summarize today. The lack of bug reports and support requests is a positive signal — it suggests that existing users are not encountering blockers or usability problems in the current version. The absence of new feature requests may indicate either high satisfaction with the current scope or a quiet user community that engages only during active development cycles.

## 8. Backlog Watch

**No long-unanswered issues or PRs require maintainer attention.** The only item in the queue is **[PR #1184](https://github.com/moltis-org/moltis/pull/1184)**, which was created on 2026-08-04, is only one day old, and requires a routine review and merge. The project's backlog is effectively empty, giving maintainers full bandwidth to address the dependency update promptly or shift focus to forward-looking initiatives. The clean state is a healthy indicator, though it also suggests an opportunity to solicit community input or plan the next feature cycle.

</details>

<details>
<summary><strong>CoPaw</strong> — <a href="https://github.com/agentscope-ai/CoPaw">agentscope-ai/CoPaw</a></summary>

# CoPaw Project Digest — 2026-08-05

## 1. Today's Overview

CoPaw (QwenPaw) is in a highly active development and stabilization phase, with 25 issues and 49 PRs updated in the last 24 hours. The project is currently preparing for its next major iteration (v2.1.0-beta.1 release verification was completed), while a significant portion of activity focuses on regression fixes and robustness improvements, particularly around the WeChat/iLink channel, console UI, and memory/context compression systems. The maintainers are actively merging bug fixes (21 closed/merged PRs) and showing strong responsiveness to community-reported issues, especially timezone handling, plugin namespace isolation, and memory auto-compression. A notable cluster of issues reveals emerging user demands for multi-model orchestration, global rules, and channel reliability/retry mechanisms.

## 2. Releases

**No new releases published in the last 24 hours.** The most recent release, **v2.1.0-beta.1** (Beta), published on 2026-08-03, underwent installation verification (issue [#6656](https://github.com/agentscope-ai/QwenPaw/issues/6656), closed) — all platform checkpoints passed. No breaking changes or migration notes apply for this digest period.

## 3. Project Progress

**21 PRs were merged/closed** in the last 24 hours. Key improvements that advanced:

- **Timezone handling fix**: PR [#6309](https://github.com/agentscope-ai/QwenPaw/pull/6309) (merged) and PR [#6685](https://github.com/agentscope-ai/QwenPaw/pull/6685) (merged) fix incorrect naive-UTC timestamp conversion in session messages — resolving long-standing bug [#6301](https://github.com/agentscope-ai/QwenPaw/issues/6301).
- **Console timestamp display sync fix**: PR [#6618](https://github.com/agentscope-ai/QwenPaw/pull/6618) (merged, first-time contributor) removes forced UTC normalization in the session list, complementing the backend fix.
- **CI/CD hardening**: PRs [#6678](https://github.com/agentscope-ai/QwenPaw/pull/6678), [#6679](https://github.com/agentscope-ai/QwenPaw/pull/6679), and [#6686](https://github.com/agentscope-ai/QwenPaw/pull/6686) (all merged) fix Playwright Chromium installation, import-local path alignment with #6487, and correct integration test tier markers — materially improving nightly test reliability.
- **Console legacy field sync**: PR [#6682](https://github.com/agentscope-ai/QwenPaw/pull/6682) (merged) keeps the legacy `max_iters` field in sync with the new UI-bound `loop.iteration.max_iterations` after the Loop Engineering migration.

Still under review, notable open PRs include:

- **ReMe memory reranker support** (backend): PR [#6398](https://github.com/agentscope-ai/QwenPaw/pull/6398) — adds external re-ranking for memory search.
- **Auto-compression memory trigger fix**: PR [#6629](https://github.com/agentscope-ai/QwenPaw/pull/6629) — addresses bug [#6624](https://github.com/agentscope-ai/QwenPaw/issues/6624) (see Bugs section).
- **Scroll compressed memory placeholder fix**: PR [#6628](https://github.com/agentscope-ai/QwenPaw/pull/6628) — fixes DeepSeek API HTTP 400 errors.
- **Channel retry mechanism**: PR [#6689](https://github.com/agentscope-ai/QwenPaw/pull/6689) — implements opt-in retry for transient startup failures (e.g., Matrix).

## 4. Community Hot Topics

The most active discussions this period center on **channel UX reliability** and **model flexibility**:

1. **[#6649 — GPT-5.6 prompt caching support](https://github.com/agentscope-ai/QwenPaw/issues/6649)** (13 comments, open): User requests support for GPT-5.6's prompt caching parameters to reduce latency/cost in multi-turn agent loops. Highlights a growing user concern with token cost optimization in long-running agent sessions.

2. **[#6655 — Console channel doesn't render security approval prompts](https://github.com/agentscope-ai/QwenPaw/issues/6655)** (12 comments, closed): In console-only mode, HIGH-risk command approvals (e.g., `rm`, `del`) are silently invisible, causing the agent to time out after 300s with no user awareness. This was one of the most impactful UX failures reported — it was resolved within 24 hours, evidencing strong maintainer responsiveness.

3. **[#6643 — Task outputs should be organized per-task directories](https://github.com/agentscope-ai/QwenPaw/issues/6643)** (6 comments, open): Users complain about file clutter in the shared `media` directory. Related issue [#6642](https://github.com/agentscope-ai/QwenPaw/issues/6642) (closed) requests drag-and-drop to read files from original paths rather than uploading/copying first.

4. **[#6667 — DeepSeek multi-turn thinking mode failure](https://github.com/agentscope-ai/QwenPaw/issues/6667)** (5 comments, open): `reasoning_content` missing after OpenAI formatter skips `ThinkingBlock` in multi-turn conversations, causing a fallback workaround that only works the first time.

Notably, **three separate issues** ([#6655](https://github.com/agentscope-ai/QwenPaw/issues/6655), [#6695](https://github.com/agentscope-ai/QwenPaw/issues/6695), [#6696](https://github.com/agentscope-ai/QwenPaw/issues/6696)) all describe channel-specific UX failures that make approval requests unreachable (console, WeChat-only). This is a systemic reliability concern for non-Web-UI channels.

## 5. Bugs & Stability

Bugs reported/updated in the last 24h, ranked by severity:

**High severity:**

- **[#6695 — Approval prompts unreachable via WeChat-only channel](https://github.com/agentscope-ai/QwenPaw/issues/6695)** (new, open): Gated shell commands (`rm`, `kill`) cannot be approved when using only the WeChat channel — approval dialog shows in the inaccessible console, leading to automatic denial after 5 minutes. **No fix PR yet** — active risk for WeChat-only deployments.

- **[#6696 — WeChat iLink one-time context_token consumed by typing indicator](https://github.com/agentscope-ai/QwenPaw/issues/6696)** (new, open): The one-time token is used for the typing indicator AND message sending, so replies get rejected (`ret=-2`) and the indicator gets stuck. **No fix PR yet.**

- **[#6687 — OpenRouter multimodal probe overwrites documented capabilities](https://github.com/agentscope-ai/QwenPaw/issues/6687)** (new, open): Explicit tests report image/video support as `false` even when provider docs list them, causing models to be needlessly limited. **No fix PR yet.**

**Medium severity:**

- **[#6683 — App Center plugin installation fails: No module named 'utils.env'](https://github.com/agentscope-ai/QwenPaw/issues/6683)** (new, open): Official `qwenpaw-creator` plugin fails to load due to top-level module name collision. **Fix PR exists**: [#6688](https://github.com/agentscope-ai/QwenPaw/pull/6688) (first-time contributor, open) proposes per-plugin namespace isolation for bare absolute imports.

- **[#6690 — cron pause/resume not persisted](https://github.com/agentscope-ai/QwenPaw/issues/6690)** (new, open): `enabled` state is only in-memory; restart reverts changes. **Fix PR exists**: [#6691](https://github.com/agentscope-ai/QwenPaw/pull/6691) (open) writes the state to job storage.

- **[#6624 — Auto-compression (Scroll) doesn't trigger `summarize_when_compact`](https://github.com/agentscope-ai/QwenPaw/issues/6624)** (open, 2 comments): Manual `/compact` works, automatic eviction doesn't. **Fix PR exists**: [#6629](https://github.com/agentscope-ai/QwenPaw/pull/6629) (under review).

**Lower severity / minor UX:**

- **[#6673 — Frontend conversation window display issue](https://github.com/agentscope-ai/QwenPaw/issues/6673)** (closed): v2.1.0b1 display glitch, closed within 24h.
- **[#5906 — Anti-repetition false positive "Doom loop"](https://github.com/agentscope-ai/QwenPaw/issues/5906)** (closed): Agent incorrectly flagged as stuck after 6 repetitions despite non-repeated dialogue.

## 6. Feature Requests & Roadmap Signals

Several notable feature requests signal the community's direction:

- **[#6490 — Add Volcengine Agent Plan & Xiaomi MiMo as built-in providers](https://github.com/agentscope-ai/QwenPaw/issues/6490)** (open): Strong demand for more model provider integration options.

- **[#6455 — Multi-model parallel execution](https://github.com/agentscope-ai/QwenPaw/issues/6455)** (open): User wants one agent to run multiple models independently in parallel, then merge results — for file modification and fact-checking use cases. This is a sophisticated workflow requirement suggesting power users are pushing toward ensemble agent workflows.

- **[#6694 — Global rules similar to .agent / .claude](https://github.com/agentscope-ai/QwenPaw/issues/6694)** (new, open): Requests a global system prompt that's always on top, addressing prompt override failures. This suggests a config-layering UX improvement.

- **[#6684 — Channel retry functionality](https://github.com/agentscope-ai/QwenPaw/issues/6684)** (open): Auto-retry and health-check for self-hosted Matrix channels. **Fix PR exists**: [#6689](https://github.com/agentscope-ai/QwenPaw/pull/6689).

- **[#6674 — Better handling of free-tier model rate limiting](https://github.com/agentscope-ai/QwenPaw/issues/6674)** (new, open): Complements #6649's cost focus — users depend on free-tier models (e.g., deepseek-v4-flash) and need smarter 429 handling.

**Likely in next version:** The multi-model parallel execution (#6455) and global rules (#6694) are both architecturally significant and still in early discussion. The prompt-caching enhancement (#6649) is more targeted and likely to land sooner given the strong interest in cost optimization.

## 7. User Feedback Summary

Real user pain points and satisfaction signals this period:

- **Channel reliability is the biggest pain point**: Multiple users ([#6655](https://github.com/agentscope-ai/QwenPaw/issues/6655), [#6695](https://github.com/agentscope-ai/QwenPaw/issues/6695), [#6696](https://github.com/agentscope-ai/QwenPaw/issues/6696)) report approval workflows being impossible or invisible in non-Web-UI channels. This represents silent, confusing failures that erode trust.

- **File management frustrations**: Users ([#6643](https://github.com/agentscope-ai/QwenPaw/issues/6643), [#6642](https://github.com/agentscope-ai/QwenPaw/issues/6642)) consistently request "read the original path, don't copy/upload" and "organize outputs per task" — the current `media`-directory hoarding is seen as messy and surprising.

- **Edge-case configuration gaps**: Users are hitting less-common but real configuration gaps — cron pause/resume not persisting ([#6690](https://github.com/agentscope-ai/QwenPaw/issues/6690)), sandbox constraints silently unenforced ([#6657](https://github.com/agentscope-ai/QwenPaw/pull/6657)), and multi-turn thinking-mode fallback failing on second occurrence ([#6667](https://github.com/agentscope-ai/QwenPaw/issues/6667)).

- **Positive signals**: The rapid closure of both [#6655](https://github.com/agentscope-ai/QwenPaw/issues/6655) (approval prompt visibility) and [#5906](https://github.com/agentscope-ai/QwenPaw/issues/5906) (Doom-loop false positive) within 24h showcases responsive maintenance. First-time contributors are being onboarded effectively (at least 5 first-time-contributor PRs in this window), indicating a healthy, welcoming open-source community.

## 8. Backlog Watch

Items that have been pending for longer periods and need maintainer attention:

- **[#6455 — Multi-model parallel execution](https://github.com/agentscope-ai/QwenPaw/issues/6455)** (opened 2026-07-24, 12 days, 3 comments): No maintainer response yet. This addresses a significant advanced-workflow gap.

- **[#6492 — Preserve uploaded filenames in hints](https://github.com/agentscope-ai/QwenPaw/pull/6492)** (opened 2026-07-27, 9 days, open): Fix with no recent activity — long-stale PR needing review.

- **[#6331 — Specify Node.js version requirement in console](https://github.com/agentscope-ai/QwenPaw/pull/6331)** (opened 2026-07-22, 14 days, open): First-time contributor PR, trivial change, still unreviewed — risks discouraging new contributors.

- **[#6374 — Token usage persistence lacks retry on transient write failure](https://github.com/agentscope-ai/QwenPaw/issues/6374)** (opened 2026-07-22, closed): Reopened? This has been closed, but the lack of a retry mechanism in `TokenUsageBuffer` remains relevant to cost-sensitive users — worth reopening or linking to #6649.

- **[#6398 — ReMe memory reranker support (backend)](https://github.com/agentscope-ai/QwenPaw/pull/6398)** (opened 2026-07-23, 13 days, under review): Substantial new feature, still not merged — potential scope or design questions requiring maintainer input.

- **[#6615 — AgentScope compatibility and config loading fixes](https://github.com/agentscope-ai/QwenPaw/pull/6615)** (opened 2026-07-31, 5 days, under review): First-time contributor, addresses memory response reliability — review is in progress but could use acceleration.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

# ZeroClaw Project Digest — 2026-08-05

## 1. Today's Overview

ZeroClaw is in a period of intense, high-velocity development, with a very heavy focus on **security hardening** and **architecture consolidation**. The project generated significant activity in the last 24 hours: **50 issues** and **50 PRs** were updated, with 48 issues and 47 PRs still open and active. This indicates a large, engaged contributor base and a healthy, non-stale pipeline. The most critical narrative is the **active mitigation of several S0/S1 severity security vulnerabilities** (unauthenticated webhook ingress, missing per-agent data isolation), with fix PRs already in flight. Concurrently, the project is navigating a large number of high-risk RFCs concerning runtime ownership, indicating a deliberate move towards a more robust and scalable core architecture. The absence of new releases suggests the project is in a stabilization and feature-gating sprint before a major version bump.

## 2. Releases

None in the last 24 hours.

## 3. Project Progress

**Merged/Closed Pull Requests (3 total):**
- **[PR #9569](https://github.com/zeroclaw-labs/zeroclaw/pull/9569) (Closed)** — `fix(gateway): fail closed when a WhatsApp Cloud or Linq webhook cannot be verified`. This is a **critical security fix** addressing the P0 vulnerability where webhook handlers skipped security verification if no secret was configured, instead of failing closed. This closes a major attack vector.
- **PR #8781** — `fix(security): remove stale advisory ignores for crates no longer in dependency tree`. This cleans up the supply-chain security posture by removing 24 obsolete entries, indicating a modernized dependency tree.
- **PR #9755 (Open)** — `ci(check): enforce workspace no-default warnings`. This CI hardening ensures feature-disabled builds don't regress with new warnings.

**Key Active Fix PRs (in-flight):**
The most significant progress is in **three coordinated security fixes** authored by IftekharUddin, all created 2026-08-04:
- **[PR #9745](https://github.com/zeroclaw-labs/zeroclaw/pull/9745)** — `fix(memory): add per-agent attribution and scoping to the knowledge graph`.
- **[PR #9746](https://github.com/zeroclaw-labs/zeroclaw/pull/9746)** — `fix(tools): per-agent ownership scoping for session tools and discord_search`.
- **[PR #9744](https://github.com/zeroclaw-labs/zeroclaw/pull/9744)** — `refactor(gateway): require authenticated webhook ingress before agent dispatch`.

These directly address the highest-severity bugs (#9647, #9646, #9565) and signal a major security milestone for the v0.9.0 architecture.

## 4. Community Hot Topics

*Most active issues by comment count:*

- **[RFC: ZeroClaw Chat Completions profile (#8603)](https://github.com/zeroclaw-labs/zeroclaw/issues/8603)** — 16 comments. Extremely high community interest in exposing agent capabilities through the ubiquitous OpenAI Chat Completions API to support tools like Open WebUI, LangChain, and Aider. This addresses a major interoperability gap.
- **[RFC: Goal mode v1 (#8303)](https://github.com/zeroclaw-labs/zeroclaw/issues/8303)** — 14 comments. Users need a durable way for agents to pursue long-running, bounded objectives across multiple turns, moving beyond single-turn interactions.
- **[RFC: Per-execution confirmation tier for shell commands (#7155)](https://github.com/zeroclaw-labs/zeroclaw/issues/7155)** — 13 comments. A high-demand feature for a unified, all-tool permission layer with `Deny/Ask/Allow` policies, similar to Claude Code, indicating a strong need for granular safety controls.
- **[RFC: Unified attachment architecture (#9488)](https://github.com/zeroclaw-labs/zeroclaw/issues/9488)** — 12 comments. Part of a broader architecture push to unify how web and channel handle file attachments.

**Analysis:** The community is pushing for two things: **open-ecosystem interoperability** (OpenAI-compatible API) and **stricter, more granular control planes** (security permissions, sandboxing, goal-oriented workflows). There is a clear trend towards "host-owned, runtime-controlled" architecture, driven by maintainers like NiuBlibing and JordanTheJet, to enforce security and ownership boundaries consistently.

## 5. Bugs & Stability

*Critical security bugs reported/active in the last 24h, ranked by severity:*

**P0 (Critical, Data Loss/Security Risk):**
- **[#9565](https://github.com/zeroclaw-labs/zeroclaw/issues/9565): Gateway webhook handlers do not fail closed** (WhatsApp Cloud, Linq, WATI). **FIX AVAILABLE in PR #9744 and PR #9569.**

**P1 (High):**
- **[#9647](https://github.com/zeroclaw-labs/zeroclaw/issues/9647): Knowledge graph has no per-agent attribution.** Global shared state allows any agent to read/mutate another's knowledge. **FIX AVAILABLE in PR #9745.**
- **[#9646](https://github.com/zeroclaw-labs/zeroclaw/issues/9646): Session/channel read+write tools lack per-agent ownership scoping.** `sessions_list`, `sessions_send`, `discord_search` can be used cross-agent. **FIX AVAILABLE in PR #9746.**

**Other Significant Fixes:**
- **[PR #9715](https://github.com/zeroclaw-labs/zeroclaw/pull/9715)**: `fix(infra): make JSONL session migration retry-safe`. Prevents data duplication and corruption during migration.
- **[PR #9750](https://github.com/zeroclaw-labs/zeroclaw/pull/9750)**: `fix(service): bound launcher-owned daemon logs`. Fixes a potential disk-fill/stability issue with unbounded log files.

**Bottom Line:** The project is currently in the midst of a **major security bug-fix sprint**. The velocity of fixes is exceptional, with critical PRs submitted within hours or days of the bug reports.

## 6. Feature Requests & Roadmap Signals

Strong signals for the next version (likely v0.9.0) based on P1/P2 priorities and RFC status:

- **Security & Permissions (Very High Priority):** The next version will feature a **runtime-owned security decision pipeline** (#7142), **pluggable inbound authentication** (#7141), **granular sandbox policies** (#6996), and a **unified tool permission layer** (#7155). This is a major investment in enterprise-grade security.
- **Interoperability & API:** The **Chat Completions Profile (#8603)** is a top candidate for the next minor release, given its high engagement and potential to onboard a huge number of existing tools.
- **Runtime & Data Ownership:** The **session-persistence contract ownership (#9600)** is a critical architectural decision being tracked. The outcome will dictate how sessions, memory, and context are managed across the system.
- **Agent Features:** **Goal mode (#8303)** is a strong candidate for a v1 implementation, enabling multi-turn, durable agent tasks.
- **Provider Enhancements:** Native support for **Hailo-Ollama (PR #9109)** and **context-window ratio anchoring (PR #9535)** show continuous work on provider flexibility and resource management.

## 7. User Feedback Summary

- **Security is the top pain point:** Reports of S0-level data leakage and unauthenticated access (issues #9647, #9646, #9565) highlight user anxiety about multi-tenant isolation and the ability to safely deploy agents with broad access.
- **Interoperability is highly desired:** The large number of comments on the Chat Completions RFC shows strong dissatisfaction with being locked into ZeroClaw's native protocols when popular OSS tools (Open WebUI, Aider) are incompatible.
- **Control & Governance are needed:** Users are requesting features like `.zeroclawignore` files (#8424) and `precondition gates` for cron jobs (#5607) to maintain control over their workspaces and automated processes.
- **Configuration Fatigue is emerging:** Many RFCs and fixes revolve around "decoupling" and "centralizing" configuration (#6850, #7929, #7897), indicating users find the current config sprawl complex and hard to manage across different surfaces (web, TUI, channels).

## 8. Backlog Watch

*Significant, long-pending items requiring maintainer attention:*

- **[RFC #6653: Host-architecture policy for emulated installs (P3, May 14)](https://github.com/zeroclaw-labs/zeroclaw/issues/6653)** — Pending for 2+ months. Needs a decision on whether to support `x86_64` targets on `aarch64` hosts, and a maintainer sign-off to close a stale PR.
- **[RFC #6971: Security UX and isolation defaults (P2, May 27)](https://github.com/zeroclaw-labs/zeroclaw/issues/6971)** — Pending for over 2 months. A foundational RFC for security hardening, currently blocked on `needs-author-action`. It has potentially been superseded by the newer "runtime-owned" security RFCs (#7141, #7142), and needs an architectural decision on whether to fold it into those efforts.
- **[PR #8010: Stale security advisory update](https://github.com/zeroclaw-labs/zeroclaw/pull/8010)** — Older PRs updating `cargo-deny` and security advisories for dependencies (like `openssl` and `tokio`) may need review and to be checked against current master, as the landscape has shifted significantly in the last 24h.

---
*Data as of 2026-08-05 00:00 UTC. All links point to the official GitHub repository.*

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/kky-wollu/agents-radar).*
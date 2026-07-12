# OpenClaw Ecosystem Digest 2026-07-13

> Issues: 500 | PRs: 500 | Projects covered: 13 | Generated: 2026-07-12 20:39 UTC

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

# OpenClaw Project Digest — 2026-07-13

## Today's Overview

OpenClaw remains extremely active with **500 issues and 500 PRs updated in the last 24 hours** — indicating either a very large project, automated bot activity, or heavy maintainer triage. Of the issues updated, **298 remain open** and **202 were closed**. On the PR side, **350 are still open** and **150 were merged or closed**. No new releases were cut today. The sheer volume suggests significant community engagement, though a subset of items may be stale-label maintenance or bulk label bot runs. The project continues to show high velocity on bug fixes and feature work, but several critical stability issues (memory leaks, database corruption, silent message loss) remain unresolved for weeks.

## Releases

**No new releases today.** The latest release remains the prior tag (no version specified in data). Keep an eye on the [releases page](https://github.com/openclaw/openclaw/releases) for updates.

## Project Progress

Several meaningful PRs were merged or closed today:

- **#105687** [CLOSED] — `refactor(plugins): trim private helper exports` by vincentkoc: Cleans up three bundled-plugin module exports that were only used internally. Small quality-of-life improvement.
- **#102994** [CLOSED] — `perf(sessions): reuse parsed transcripts for successor rotation` by dexhunter: Performance fix that avoids re-parsing transcripts on the hot compaction path, reducing latency for long-running sessions.
- **#104871** [CLOSED] — `Refactor high-churn orchestration internals without contract changes` by vincentkoc: Internal refactor of high-complexity orchestration surfaces to improve state machine, policy, and ownership boundaries — no user-facing changes.
- **#67417** [CLOSED] — Bug: `openclaw backup create` fails with ENOENT when session file is cleaned up during backup. Now resolved.
- **#79034** [CLOSED] — UI metadata localization for non-English users — now merged.
- **#93465** [CLOSED] — Windows ACPX runtime `spawn EINVAL` fix — ACP runtime now usable on Windows.

Several long-standing open PRs also received attention:
- **#103961** — fix(usage): reclaim refresh locks leaked by the current process (waiting on author)
- **#105643** — fix(cli-runner): sweep orphaned bundle MCP temp dirs at gateway startup (ready for maintainer look)
- **#105674** — feat(skills): capture reusable techniques from successful work (waiting on author)
- **#105688** — feat(chat): native session scroll-back with offset paging (waiting on author)

## Community Hot Topics

The following issues and PRs generated the most discussion and reactions:

### Most Commented Issues

1. **#75 — Linux/Windows Clawdbot Apps** (110 comments, 81 👍)
   - [Issue #75](https://github.com/openclaw/openclaw/issues/75)
   - Long-standing feature request for desktop apps on Linux and Windows. High community desire but no fix PR exists. Labeled with `clawsweeper:needs-product-decision`, `clawsweeper:needs-maintainer-review`, and `impact:security` — suggesting the maintainers are weighing security implications before committing.

2. **#99241 — Tool outputs render as image attachments, unreadable to agent** (22 comments, 2 👍)
   - [Issue #99241](https://github.com/openclaw/openclaw/issues/99241)
   - P1 bug: In long-running/ANSI-heavy workflows, tool results collapse into image placeholders, making stdout/stderr invisible to the agent. Core workflow reliability issue.

3. **#91588 — Critical: Gateway Memory Leak — 350MB to 15.5GB over days** (18 comments, 1 👍)
   - [Issue #91588](https://github.com/openclaw/openclaw/issues/91588)
   - P0 severity: Gateway OOM crashes after 2-3 days of use. Still no fix PR despite being open since June 9.

4. **#7707 — Memory Trust Tagging by Source** (16 comments)
   - [Issue #7707](https://github.com/openclaw/openclaw/issues/7707)
   - Feature request to tag memory entries by trust level to prevent memory poisoning. Labels indicate it needs security review and product decision.

5. **#102175 — Embedded prompt cache breaks across boundaries** (16 comments, 1 👍)
   - [Issue #102175](https://github.com/openclaw/openclaw/issues/102175)
   - P2 regression: Long-lived sessions lose prompt-cache reuse when crossing room-event, policy, or authorization boundaries. Affects model-visible tool inventory.

### Most Active PRs (by labels/activity)

- **#105365** — `fix(codex): require explicit final source delivery`: P1, L-sized PR addressing premature turn-ending in Codex runs.
- **#102082** — `fix(slack): suppress progress chrome sends`: P1 fix for Slack progress-only tool chrome payloads being incorrectly delivered as messages.
- **#103562** — `fix(discord): retry reply session init conflicts to prevent silent message loss`: P1 fix for Discord message drops due to session init conflicts.
- **#103534** — `fix(gateway): enforce plugin-ownership check in sessions.patch`: P1 security fix for cross-plugin session mutation.

### Underlying Needs Analysis

The community is clearly frustrated with **session state reliability** (tool output corruption, memory leaks, database corruption, silent message drops) and **cross-platform support** (Linux/Windows apps, Windows ACP runtime). Security concerns around **prompt injection** and **credential leakage** are also top-of-mind. Several high-comment-count issues have been open for months with no fix PR — suggesting maintainers may be bottlenecked on review capacity or product decisions.

## Bugs & Stability

### Critical (P0) — Active and Unresolved

1. **#91588 — Gateway Memory Leak** (P0, open since 2026-06-09, no fix PR)
   - RSS grows from 350MB to 15.5GB over 2-3 days → OOM crashes → `launchd-handoff` restart cycles
   - [Issue #91588](https://github.com/openclaw/openclaw/issues/91588)
   - **No fix PR exists.** This is the single highest-severity stability issue.

2. **#104721 — All tool results return "(see attached image)" placeholder** (P0, filed 2026-07-11)
   - [Issue #104721](https://github.com/openclaw/openclaw/issues/104721)
   - Complete data loss: file reads return the literal string "(see attached image)" instead of actual content.
   - Marked as regression. **No fix PR yet.**

3. **#101290 — CLI startup preflight corrupts live state DB** (P0, open since 2026-07-07)
   - [Issue #101290](https://github.com/openclaw/openclaw/issues/101290)
   - `openclaw.sqlite` corrupts while gateway is running. "database disk image is malformed" errors.
   - **No fix PR yet.**

### High (P1) — Active and Unresolved

4. **#99241 — Tool outputs render as image attachments** (P1, needs live repro)
   - [Issue #99241](https://github.com/openclaw/openclaw/issues/99241)
   - ANSI-heavy tool output collapses into unreadable image placeholder.

5. **#63216 — Repeated hard resets on same session key** (P1, stale)
   - [Issue #63216](https://github.com/openclaw/openclaw/issues/63216)
   - Session resets despite high `reserveTokensFloor` — retry loop re-injects bootstrap context.

6. **#53408 — Write/exec tool parameters silently dropped** (P1, needs live repro)
   - [Issue #53408](https://github.com/openclaw/openclaw/issues/53408)
   - After 15+ turns, tools receive empty arguments. Silent message loss.

7. **#39476 — A2A sessions_send causes duplicate messages** (P1, linked PR open)
   - [Issue #39476](https://github.com/openclaw/openclaw/issues/39476)
   - Target agent calling back via `sessions_send` causes duplicate channel messages.

8. **#94939 — 6.x state migration leaves SQLite empty** (P1, linked PR open)
   - [Issue #94939](https://github.com/openclaw/openclaw/issues/94939)
   - Migration produces 0-byte SQLite file. Breaks Bot Framework sends in MS Teams.

### Medium (P2) — Notable

- **#102175 — Prompt cache breaks across boundaries** (P2, regression)
- **#40001 — Write tool lacks append mode** (P2, linked PR open) — destroys shared files
- **#59662 — Anthropic Max usage alerts delivered as assistant messages** (P2, stale)
- **#59618 — Auto-compaction abandons task execution** (P2, stale)
- **#71326 — Cross-exec stale file reads** (P2, stale) — regression in 2026.4.20

### Fix PRs in Progress

- **#105643** — Fix for orphaned MCP temp dirs (P2, ready for maintainer look)
- **#105673** — Fix for stale `activeBackgroundExecSessionIds` (P1, needs proof)
- **#103534** — Enforce plugin-ownership check in sessions.patch (P1, needs proof)
- **#102082** — Suppress Slack progress chrome (P1, needs review)
- **#79405** — Harden subagent completion fallback delivery (P1, waiting on author, open since May 8)

## Feature Requests & Roadmap Signals

### High-Community-Interest Features

1. **#75 — Linux/Windows Clawdbot Apps** (81 👍, 110 comments)
   - Desktop client parity with macOS/iOS. Likely in next major release if product decision is made.
   
2. **#10659 — Masked Secrets: Prevent agent from accessing raw API keys** (4 👍, P1)
   - Security-focused: agents use keys without seeing them. Needs security review.
   
3. **#7722 — Filesystem Sandboxing Config** (4 👍, P2)
   - `tools.fileAccess` paths configuration. Has attempted implementation that failed.
   
4. **#7707 — Memory Trust Tagging by Source** (P2)
   - Prevent memory poisoning attacks from untrusted content.
   
5. **#6615 — Denylist support for exec-approvals** (7 👍, P2)
   - "Allow everything except X" policies. High community demand (7 👍).

### Likely to Ship Next Version

- **Session scroll-back** (#105688) — PR is open and active
- **Skills capture from successful work** (#105674) — PR waiting on author
- **Workspaces features** — Multiple PRs (#101878, #101329, #101841, #101900, #105353) from 100yenadmin targeting stream bindings, widget persistence, pub/sub, version history, and team sharing. These are large (XL) PRs but show clear direction.

### Possibly Delayed

- **Dynamic model discovery** (#10687) — needs product decision and live repro
- **Provider fallback by failure class** (#47910) — P1 but shape not clear
- **Per-model generation timeout** (#8724) — needed for Google model loops

## User Feedback Summary

### Pain Points (Negative Feedback Signals)

1. **Session corruption / data loss** — Multiple P0/P1 bugs where tool outputs, file contents, or entire database become unreadable. Users are losing work silently.
2. **Memory leaks causing downtime** — Gateway OOM kills force restarts every 2-3 days. Normal users cannot run the gateway reliably.
3. **Missing Linux/Windows desktop apps** — Users on non-macOS platforms feel like second-class citizens.
4. **No append mode for write tool** — Cron jobs overwrite shared files, destroying data across sessions.
5. **Hard-to-diagnose failures** — Tool parameters silently dropped, heartbeat cadence stalls, placeholder text instead of real output — all making debugging extremely difficult.
6. **Windows ACP runtime broken** — `sessions_spawn(runtime="acp")` unusable on Windows (now fixed in #93465).
7. **No configurable thread limits** — No `maxTurns`/`maxToolCalls` for models that loop infinitely (e.g., KIMI K2, Gemini Flash).
8. **Accessibility gaps in TUI** — Emoji/symbols confuse screenreaders; no Shift+Enter for multi-line input.

### Use Cases Being Served

- **Cross-platform agent deployment** — Linux/Windows app demand shows users want to run agents on servers or corporate desktops
- **Enterprise security** — Secrets masking, filesystem sandboxing, memory trust tagging all point to production/enterprise adoption
- **Multi-agent orchestration** — A2A `sessions_send`, sub-agent completion fallback, workspace sharing — users building complex agent teams
- **Chat platform integration** — Slack, Discord, Telegram, Feishu, Nextcloud Talk, WhatsApp — strong demand for multi-channel presence

### Satisfaction Signals

- Active community engagement with well-structured bug reports and feature requests
- Users providing detailed reproductions (ANSI output, cron job descriptions, Slack payload examples)
- Several fix PRs from community contributors (not just core maintainers)

## Backlog Watch

### Aging Issues Needing Maintainer Attention

| Issue | Created | Status | Why It Matters |
|-------|---------|--------|----------------|
| #91588 (P0 memory leak) | 2026-06-09 | Needs review, no fix PR | Gateway crashes every 2-3 days |
| #75 (Linux/Windows apps) | 2026-01-01 | Needs product decision | 81 👍 — most demanded feature |
| #7707 (Memory trust tagging) | 2026-02-03 | Needs security review, product decision | Security hardening |
| #10659 (Masked secrets) | 2026-02-06 | Needs security review | API key leak protection |
| #6615 (Exec denylist) | 2026-02-01 | Needs security review | 7 👍 — high community interest |
| #7722 (Filesystem sandboxing) | 2026-02-03 | Needs product decision | Enterprise security |
| #11665 (Webhook session reuse) | 2026-02-08 | Linked PR open, needs decisions | Documentation promises broken |
| #28847 (Provider key pools) | 2026-02-27 | Needs product decision | 429 retry storms |

### Stale Items (Last Updated >30 Days Ago with No Maintainer Intervention)

- #65161 — Heartbeat isolated mode regressions (since April 12)
- #63216 — Repeated hard resets (since April 8)
- #59662 — Anthropic Max usage alerts (since April 2)
- #59618 — Auto-compaction abandoning tasks (since April 2)
- #71326 — Cross-exec stale file reads (since April 25, regression in 2026.4.20)
- #71301 — Version-matched bundled docs (since April 25)

### PRs Waiting Over 30 Days

- **#79397** — fix(nextcloud-talk): parse structured mention payloads (since May 8, ready for maintainer look)
- **#79404** — chore: harden OpenClaw certification gates (since May 8, waiting on author)
- **#79405** — fix: harden subagent completion fallback delivery (since May 8, waiting on author)
- **#79339** — fix: preserve final media reply directives (since May 8, waiting on author)
- **#79401** — feat(reply): emit structured runtime incidents (since May 8, waiting on author)

### Risk Assessment

The **three P0 bugs** (#91588, #104721, #101290) affecting core functionality — memory leaks, output corruption, and database corruption — represent significant stability risks for any production deployment. All have been open for days to weeks with no fix PRs. The **stale P1 bugs** (some since February-April) suggest the maintainer team may be under-resourced relative to the volume of incoming issues. Community contributors are active (many fix PRs from external developers), but the bottleneck appears to be in **maintainer review** and **product decision-making**, particularly for security-related features.

---

## Cross-Ecosystem Comparison

Here is the cross-project comparison report you requested, compiled from the community digest summaries for July 13, 2026.

---

### Cross-Project Ecosystem Comparison Report
**Date:** 2026-07-13
**To:** Technical Decision-Makers & Developers
**From:** Senior Analyst, AI Agent Open-Source Ecosystem

---

### 1. Ecosystem Overview

The personal AI agent open-source ecosystem is undergoing a period of **rapid maturation**, characterized by high-velocity feature work and significant stability challenges. The major reference project, OpenClaw, is grappling with a bottleneck in maintainer review capacity while a wave of downstream forks and niche projects (e.g., NanoBot, PicoClaw, IronClaw) are iterating on specific platforms and use cases—such as local model performance, low-power hardware, and enterprise-grade orchestration. A clear **consolidation of core requirements** is emerging, with a strong emphasis on **session reliability, state persistence, multi-channel integration, and enterprise security** (access control, sandboxing). However, a critical ecosystem-wide weakness is the prevalence of **critical (P0) bugs related to silent data loss and memory corruption**, which represent significant risks for any production deployment. The community is showing strong engagement through detailed bug reports and feature requests but is also signaling frustration with unstable releases and unmet feature requests for cross-platform desktop support.

### 2. Activity Comparison

| Project | Issues (24h) | PRs (24h) | Release Status | Health Score (Qualitative) | Key Stability Concern |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **OpenClaw** | **500** | **500** | No release | **Fair (High Risk)** | *3x P0 bugs:* Gateway OOM, data corruption, silent message loss |
| **Hermes Agent** | 50 | 50 | No release | **Fair (High Risk)** | macOS state.db corruption, Windows file I/O broken |
| **ZeroClaw** | 50 | 50 | No release | **Stressed (Pre-release)** | SIGSEGV crashes, memory leaks, configuration friction |
| **IronClaw** | 8 | 43 | No release | **Good (High Velocity)** | CI infrastructure collapse (70% red main pushes) |
| **CoPaw** | 19 | 10 | No release | **Stressful (Post-Release Regressions)** | v2.0.0 regressions: broken skills, data loss, tool-call pairing |
| **NanoBot** | 3 | 11 | No release | **Good** | Ollama performance crisis, silent Dream session failures |
| **PicoClaw** | 6 | 2 | No release | **Fair** | Matrix sync silently dying (no reconnection) |
| **NanoClaw** | 3 | 13 | No release | **Good (High Velocity)** | Silent message drops, false positive errors |
| **LobsterAI** | 1 | 2 | No release | **Quiet** | Multi-agent profile overwriting |
| **NullClaw, TinyClaw, Moltis, ZeptoClaw** | 0 | 0 | - | **Inactive** | No recent activity |

### 3. OpenClaw's Position

OpenClaw remains the **undisputed reference implementation and largest community hub** in the ecosystem. Its advantages are clear: an enormous, engaged community (500 issues/PRs updated daily) and the deepest feature set, including multi-agent orchestration (A2A), extensive chat platform integrations (Slack, Discord, etc.), and a sophisticated skill system. Its technical approach is monolithic and comprehensive, which drives complexity.

**Key Differences from Peers:**
- **Community Size:** OpenClaw's scale dwarfs all others by at least one order of magnitude.
- **Technical Scope:** It is the only project implementing complex features like Agent-to-Agent (A2A) `sessions_send` and a full workspace system, which downstream projects (e.g., IronClaw, ZeroClaw) are only now beginning to explore.
- **Struggles:** At this scale, OpenClaw suffers from **maintainer bottleneck**. The three unresolved P0 bugs (memory leak, output corruption, DB corruption) are ecosystem-wide risks. Its complexity also means slower response to platform-specific issues (e.g., Windows ACP runtime) compared to smaller, more agile forks like NanoBot or PicoClaw.

### 4. Shared Technical Focus Areas

Several critical needs are emerging as ecosystem-wide requirements, indicating areas where the entire community is investing:

1.  **Session State Reliability (Unanimous):** Every active project is dealing with session data corruption, silent message drops, or state loss.
    - *Projects:* **OpenClaw** (P0 bugs #91588, #104721, #101290), **NanoClaw** (Undelivered replies #3020), **CoPaw** (v2.0.0 session mapping loss #5964), **Hermes Agent** (macOS state.db corruption #63386).
2.  **Tool-Calling Integrity (Almost Universal):** Agents losing tool definitions or tool results being corrupted is a core reliability blocker.
    - *Projects:* **OpenClaw** (Tool outputs as images #99241), **CoPaw** (Broken `tool_call` / `tool_result` pairing #5986), **Hermes Agent** (Qwen losing tool definitions #63392).
3.  **Enterprise Security Hardening (Growing Trend):** Demand for sandboxing, secrets management, and access control is strong.
    - *Projects:* **OpenClaw** (Memory trust tagging #7707, masked secrets #10659, filesystem sandboxing #7722), **NanoClaw** (Unified guard seam #2986), **IronClaw** (Extension-runtime auth engine), **Hermes Agent** (Fail-closed policy hooks #61656).
4.  **Cross-Platform Client Support (High Desire):** Users are consistently demanding native desktop apps and better support for non-Linux/Mac platforms.
    - *Projects:* **OpenClaw** (Linux/Windows apps #75 - 81 👍), **NanoBot** (WebUI v2 push), **PicoClaw** (Android support #3182 - stale), **Hermes Agent** (Windows file I/O #17753).
5.  **Local Model / Ollama Performance (Niche but vocal):** A smaller but very vocal set of users requires local-first performance parity.
    - *Projects:* **NanoBot** (Ollama "totally unusable" #4867), **Hermes Agent** (Qwen3-14B tool loss #63392), **IronClaw** (GLM-5.2 hangs #6010).

### 5. Differentiation Analysis

While all projects share a common goal of personal AI assistance, their target users and technical architectures diverge significantly:

| Project | Target User / Use Case | Technical Architecture / Focus |
| :--- | :--- | :--- |
| **OpenClaw** | Power users, developers, enterprise | Monolithic reference. Multi-agent orchestration, extensive chat integrations. |
| **NanoClaw** | Operators, security-conscious teams | Lean security-first. Guard seams, approval CLI verbs, audit trails. |
| **IronClaw** | Heavy inference, IDE integration | Feature-driven, high velocity. Extension-runtime (WASM), tools-capable agent loop, "clawbench". |
| **ZeroClaw** | IDE-native development (ZeroCode) | Plugin & WASM-centric. Goal-mode, WASM channels, MCP/tool-schema management. |
| **Hermes Agent** | Heterogeneous desktop (macOS/Windows/Linux) | UX & platform-oriented. Desktop app (Electron, node-pty), Kanban boards, platform-specific bug fixing. |
| **NanoBot** | Local model users, lightweight deployment | Performance & WebUI-focused. Ollama caching, Dream sessions, WebUI onboarding. |
| **CoPaw** | Channel-first, mobile/feishu users | Post-release regression focus. Context compression, v1→v2 migration, enterprise chat (Feishu/DingTalk). |
| **PicoClaw** | Homelab, low-power devices (ARM) | Lightweight & platform-oriented. Docker Compose for ARM, Matrix bridge, skill toggles. |
| **LobsterAI** | Multi-agent configuration (Chinese users) | Agent isolation focus. Short UUIDs, per-agent USER.md files. |

### 6. Community Momentum & Maturity

- **Tier 1 (High Velocity, Iterating Fast):**
    - **NanoClaw & IronClaw:** These projects are in a "build and fix" cycle, shipping new features (guard seams, extension runtime) while actively addressing critical bugs. High contributor engagement.
    - **ZeroClaw:** Nearing a major release (v0.8.3). High activity with many PRs in review, but is in a pre-release stress phase.
- **Tier 2 (Feature Stable, Bug Fixing):**
    - **NanoBot & PicoClaw:** These are relatively stable but have critical single-issue blockers (Ollama cache, Matrix reconnection). They are actively servicing a dedicated user base.
    - **Hermes Agent:** Shows high activity, but 80% of that is triage and closing. The project is stabilizing a broad feature set and dealing with platform fragmentation.
- **Tier 3 (Stressed / Regressing):**
    - **OpenClaw & CoPaw:** Both have released major versions recently (or are preparing to) and are now overwhelmed by regression bugs. Their position as "market leaders" (reference or popular) creates high expectations and scrutiny.
- **Tier 4 (Quiet / Inactive):**
    - **LobsterAI:** Low activity, one high-impact bug. May be in maintenance mode.
    - **Null/Tiny/Moltis/ZeptoClaw:** Inactive.

### 7. Trend Signals for AI Agent Developers

1.  **The Reliability Ceiling is Real:** The ecosystem is hitting a wall on reliability. The prevalence of **silent failures** (data loss, dropped messages, output corruption) is the most critical risk for developers building on these tools. **Recommendation:** Prioritize projects with strong focus on state debugging tools (e.g., IronClaw’s `doctor`, NanoClaw’s audit logs) and test coverage.

2.  **Security is Becoming a Prerequisite for Production:** The requests for secrets masking, file sandboxing, and policy hooks across multiple projects signal that enterprise adoption is being blocked by security gaps. **Recommendation:** Evaluate projects with a clear security architecture (e.g., NanoClaw’s guard seam) over those that treat it as an afterthought.

3.  **WASM and Plugin Models are the Next Battleground:** IronClaw and ZeroClaw are both investing heavily in WASM-based extension runtimes. This suggests a trend towards sandboxed, portable plugins to replace the current monolithic or dynamically-linked plugin systems in OpenClaw. **Recommendation:** Watch ZeroClaw and IronClaw for emerging WASM plugin standards.

4.  **Consolidation Around a Few Chat Platforms:** Despite many integrations, the deep community pain points are focused on **Slack, Discord, Feishu, Telegram, and Matrix**. The community is demanding reliability, thread awareness, and cross-channel handoffs over adding *more* platforms.

5.  **Local AI Remains a Tough Niche:** The strong but isolated complaints about Ollama performance from NanoBot and Hermes users show that running agents locally is still an unsolved problem. Cache misses, context window management, and provider compatibility make it a challenging experience. **Recommendation:** Only target local models if you are prepared for significant performance engineering investment.

---

## Peer Project Reports

<details>
<summary><strong>NanoBot</strong> — <a href="https://github.com/HKUDS/nanobot">HKUDS/nanobot</a></summary>

# NanoBot Project Digest — July 13, 2026

## 1. Today's Overview

NanoBot shows **moderate activity** with 3 issues and 11 PRs updated in the last 24 hours, though only 1 PR was merged/closed. The project maintains a **healthy contributor pipeline**, with 10 open PRs spanning fixes, features, and refactors. However, the **high open-to-closed ratio (10:1)** suggests either significant review backlog or complex changes requiring iteration. No releases were published today. The community is actively reporting bugs around Dream session handling and Ollama caching, while developers are working on security, WebUI onboarding, and session management improvements.

## 2. Releases

**None.** No new releases were tagged in the last 24 hours.

## 3. Project Progress

**1 PR merged/closed today:**

- **[#4892 – fix(webui): allow remote workspace access reduction](https://github.com/HKUDS/nanobot/pull/4892)** (merged) — A security fix by Re-bin that enables remote WebUI sessions to reduce Full Access to Default Permission without altering workspace state, and prevents access escalation outside localhost/native clients. This addresses a real security risk for users exposing the WebUI remotely.

**Other PRs that advanced (received updates):**
- #4855 (guided setup flows) — iterative improvement on WebUI onboarding
- #4145 (Weather Skill) — stale contribution receiving renewed attention
- #4371, #4616, #4650, #4866 — refactors and features moving through review cycles

## 4. Community Hot Topics

**Most Active Discussion:**

- **[#4867 – Preserve exact prompt prefix for Ollama caching (CLOSED)](https://github.com/HKUDS/nanobot/issues/4867)** — 4 comments. The author reports that NanoBot adds 60 seconds per turn with Ollama due to cache misses, making it "totally unusable" even with 32 GB VRAM. This issue was closed, suggesting a resolution or workaround was found. The underlying need is **critical performance parity with local model runners**.

**Other Signal:**
- #4893 and #4894 (both opened yesterday by groudas) have 0 comments so far — these are fresh reports and may become active as maintainers triage.

## 5. Bugs & Stability

**High Severity:**

- **[#4894 – prune_dream_sessions() fails on base64-encoded filenames](https://github.com/HKUDS/nanobot/issues/4894)** — After a commit switched to base64-encoded filenames, the pruning function still uses a legacy glob pattern (`dream_*.jsonl`), meaning Dream sessions are **never pruned**. No fix PR exists yet. This is a **data accumulation/latent cleanup failure** bug.

- **[#4893 – /dream-log and /dream-restore show non-Dream commits](https://github.com/HKUDS/nanobot/issues/4893)** — These commands pollute output with backup and manual edit commits since they call `git.log()` unfiltered. **User confusion and broken UX** for Dream session management. No fix PR yet.

**Medium Severity (Fix PR exists):**

- **PR #4813 – `.strip()` on `list[dict]` content raises `AttributeError`** — When multimodal content arrives via channels, `msg.content` can be a list instead of a string, crashing `AgentLoop.run()` and `AgentLoop._state_command()`. Fix is open and under review.

**Operational:**

- **PR #4842 – `asyncio.CancelledError` during MCP shutdown** — When MCP subprocesses (e.g., browser-agent) fail to terminate within timeout, the exception is unhandled. Fix PR exists but is waiting for merge.

## 6. Feature Requests & Roadmap Signals

**Likely Next Version Features:**

- **Ollama caching support** (from #4867) — Preserving exact system prompt prefix so KV caches hit on Ollama/local models. Given the severity of the performance complaint, this is likely targeted for the next release. **PR #4371** (add breakpoint for stable prefix caching) is already open but has conflicts.

- **Model presets bound to sessions** (PR #4866) — Persisting model preset selection per session and capturing immutable LLM runtime per turn. This enables session-scoped `/model` commands and proper snapshot isolation for subagents.

- **Sustained-goal opt-in flag** (PR #4879) — Gating `long_task` behind an opt-in default-off flag to prevent background goals from blocking user interaction. The community consensus from the PR discussion suggests this is **highly desired** for usability.

- **Guided WebUI setup flows** (PR #4855) — Productized channel setup with QR handoff, validation, and secure secret handling. Likely part of a broader WebUI v2 push.

## 7. User Feedback Summary

**Strongest Pain Point:**
- **Ollama performance is broken** — Issue #4867 describes 60-second delays per turn due to cache misses, calling it "totally unusable" even with 32 GB VRAM. This is a **blocker for local model users** and likely represents a broader class of users silently affected.

**Usability Frustrations:**
- **Dream session commands show noise** — #4893 reports that `/dream-log` and `/dream-restore` are useless for their intended purpose because they mix Dream commits with unrelated git activity.
- **Dream session pruning silently fails** — #4894 means users' Dream databases grow unboundedly, likely causing performance degradation over weeks/months.

**Satisfaction Signals:**
- The community is actively contributing: 11 PRs updated in 24h suggests contributors are engaged and motivated.
- Security-conscious users benefit from the merged PR #4892 (remote workspace access control).

## 8. Backlog Watch

**Long-standing open PRs needing maintainer attention:**

| Issue/PR | Age | Status | Risk |
|---|---|---|---|
| [#4145 – Weather Skill](https://github.com/HKUDS/nanobot/pull/4145) | 42 days | Unmerged, conflicts likely stale | Low — new skill, non-critical |
| [#4371 – Cache breakpoint for stable prefix](https://github.com/HKUDS/nanobot/pull/4371) | 27 days | Conflicts | **High** — directly addresses #4867 caching issue |
| [#4616 – Route direct subagent results in-turn](https://github.com/HKUDS/nanobot/pull/4616) | 12 days | Conflicts | Medium — affects subagent execution flow |

**Unanswered Issues (0 comments from maintainers):**
- [#4894 – prune_dream_sessions() fails (base64 filenames)](https://github.com/HKUDS/nanobot/issues/4894) — Opened yesterday, no response yet
- [#4893 – /dream-log shows non-Dream commits](https://github.com/HKUDS/nanobot/issues/4893) — Opened yesterday, no response yet

**Recommendation:** The #4371 PR (cache breakpoint) directly addresses the highest-pain community issue (#4867) and should be prioritized for unblocking before the next release. The two Dream session bugs (#4893, #4894) are fresh but should be triaged quickly to prevent data management degradation.

</details>

<details>
<summary><strong>Hermes Agent</strong> — <a href="https://github.com/nousresearch/hermes-agent">nousresearch/hermes-agent</a></summary>

# Hermes Agent Project Digest
**Date:** 2026-07-13

## Today's Overview
Hermes Agent shows **high activity** with 50 issues and 50 PRs updated in the last 24 hours, though most of that volume represents ongoing community triage rather than fresh development — 30 of 50 issues were closed and only 8 of 50 PRs were merged/closed. The project has **20 open issues** and **42 open PRs**, indicating a significant maintenance queue. No new releases were published today. A cluster of Windows-specific bugs (5 new reports) and macOS/iOS state corruption issues signal platform fragmentation growing as Hermes adoption expands beyond Linux.

## Releases
**None.** No new versions were published in the last 24 hours.

## Project Progress
**8 PRs merged/closed today.** The most significant fixes advanced to `main`:

- [PR #63398](https://github.com/NousResearch/hermes-agent/pull/63398) — **State repair:** Adds `REINDEX` strategy to fix B-tree index corruption in `state.db`, addressing a root cause of session-search failures on macOS.
- [PR #62591](https://github.com/NousResearch/hermes-agent/pull/62591) — **File-read staleness fix:** Captures file `mtime` *before* reading bytes to prevent silent overwrites and stale dedup stubs during concurrent file edits.
- [PR #63390](https://github.com/NousResearch/hermes-agent/pull/63390) — **TTS stability:** Adds 10-second timeout to `proc.wait()` after kill in `_play_system_audio`, preventing permanent hangs on stuck audio processes.
- [PR #63391](https://github.com/NousResearch/hermes-agent/pull/63391) — **Desktop Linux launch fix:** Rebuilds `node-pty` for Electron when no prebuild covers the target, fixing crash-on-launch for packaged desktop app on Linux.
- [PR #63355](https://github.com/NousResearch/hermes-agent/pull/63355) — **Kanban board race condition:** Stops stale event streams from recreating removed boards and makes hard-deletion race-safe under SQLite WAL readers.
- [PR #63389](https://github.com/NousResearch/hermes-agent/pull/63389) — **Session search perf:** Skips unused surrounding-context queries that `session_search` and dashboard endpoints immediately discard.

## Community Hot Topics
The most active discussions this week:

1. **[Windows file-read bug (#17753)](https://github.com/NousResearch/hermes-agent/issues/17753)** — 5 comments, closed. Core inability to read local files on Windows (no WSL) remains unresolved at the design level — the system can *write* but cannot *read* files. This is a top community pain point for Windows users.

2. **[Docker root-owned files (#17144)](https://github.com/NousResearch/hermes-agent/issues/17144)** — 5 comments, 1 👍, closed. Docker deployments create `root:root` files from agent/tool memory writes, breaking gateway user access. Community wanted more graceful handling of permission escalation in containers.

3. **[Chinese text TUI glitch (#17602)](https://github.com/NousResearch/hermes-agent/issues/17602)** — 4 comments, closed. TUI rendering breaks with CJK text output, causing character scattering. Affects East Asian user base significantly.

4. **[WeChat token conflict on restart (#17198)](https://github.com/NousResearch/hermes-agent/issues/17198)** — 4 comments, 2 👍, closed. Gateway restart race condition where old process still holds WeChat bot token, preventing clean redeployment. Multiple users reported work-related workflow disruptions.

5. **[Qwen3.6 hallucination (#17031)](https://github.com/NousResearch/hermes-agent/issues/17031)** — 3 comments, 2 👍, closed. Model fabricated entire prior conversation history at session start, raising trust concerns for Ollama users.

## Bugs & Stability
**Critical / P2 bugs reported today:**

| Issue | Component | Summary | Fix Exists? |
|-------|-----------|---------|-------------|
| [#63386](https://github.com/NousResearch/hermes-agent/issues/63386) | `comp/gateway` | `state.db` FTS index corruption on macOS — breaks session search and handoff | [PR #63398](https://github.com/NousResearch/hermes-agent/pull/63398) (merged) |
| [#63392](https://github.com/NousResearch/hermes-agent/issues/63392) | `comp/agent` + Ollama | Qwen3-14B intermittently loses tool definitions (e.g. `read_file` missing) during long sessions on Windows | None |
| [#63384](https://github.com/NousResearch/hermes-agent/issues/63384) | `comp/dashboard` | Text becomes invisible after long sessions — output rendered as transparent/unreadable blocks | None |
| [#63361](https://github.com/NousResearch/hermes-agent/issues/63361) | `backend/daytona` | Persistent sandbox resumes by name without image comparison; `cleanup()` lacks `force_remove` | None |
| [#63387](https://github.com/NousResearchhermes-agent/issues/63387) | `platform/telegram` | Telegram polling conflicts + macOS/launchd shutdown misbehavior | None |
| [#63383](https://github.com/NousResearch/hermes-agent/issues/63383) | `backend/docker` | `docker_volumes` config ignored by Hermes Desktop (works in CLI) | None |
| [#63370](https://github.com/NousResearch/hermes-agent/issues/63370) | `comp/desktop` | Input box misaligned on Windows 10 at 125%+ DPI scaling | None |

**Notable:** The macOS `state.db` corruption bug (#63386) is the most severe issue this cycle — it directly impacts session continuity for Mac users and has already been fixed via PR #63398.

## Feature Requests & Roadmap Signals
- **[Matrix Tool activity pane (#61511)](https://github.com/NousResearch/hermes-agent/pull/61511)** — Sticky always-visible tool activity list for Matrix, panned for better UX as users demand richer chat surface controls.
- **[Fail-closed policy hooks (#61656)](https://github.com/NousResearch/hermes-agent/issues/61656)** — Community request for security plugins to guarantee tool blocking when policy layer fails, indicating growing enterprise security concerns.
- **[Proactive DingTalk messaging (#17370)](https://github.com/NousResearch/hermes-agent/pull/17370)** — Agent-initiated messages via Robot OpenAPI, plus AI Card QPS throttle (#17365) and quoted-reply context (#17368). Points toward Chinese enterprise deployment maturity.
- **[CLI account limits (#16652)](https://github.com/NousResearch/hermes-agent/pull/16652)** — Show provider quota usage in status bars; users want real-time visibility into API consumption.
- **[Blockchain-verified PII sanitization (#17472)](https://github.com/NousResearch/hermes-agent/pull/17472)** — TrustBoost PII Sanitizer v2.0.4 skill; though the approach is novel, community adoption may be limited by complexity.

**Prediction:** Next minor release (likely v0.18.3) will include the state DB repair (#63398), file-read staleness fix (#62591), and Desktop Linux node-pty fix (#63391). The DingTalk improvements cluster may land as a separate plugin version bump.

## User Feedback Summary
**Pain points:**
- **Windows file I/O still broken** — Users cannot read local files on native Windows, only write. Workaround requires WSL. This is the single most-reported platform issue.
- **macOS state corruption** — FTS index corruption breaking session search is a new and growing problem for Mac users, now fixed but not yet released.
- **Docker permission escalation** — Root-owned files persist after agent writes, requiring manual chown. Enterprise Docker users are dissatisfied with current container security posture.
- **CJK text rendering** — Chinese/Japanese/Korean users face unusable TUI display, limiting Hermes adoption in East Asian markets.
- **Custom provider namespace collision** — Naming a provider `codex` triggers automatic rewriting to `openai-codex`, confusing users with local setups.

**Satisfaction signals:**
- Community continues filing detailed issue reports with reproduction steps and logs, indicating sustained engagement.
- Multiple enterprise-oriented features (fail-closed policies, proactive messaging, audit layers) suggest power users are investing in production deployment.

## Backlog Watch
**Long-unanswered items needing maintainer attention:**

| Item | Age | Component | Stalled Since | Concern |
|------|-----|-----------|---------------|---------|
| [#46265](https://github.com/NousResearch/hermes-agent/issues/46265) | 28 days | SimpleX adapter | 2026-06-14 | DM replies silently dropped — no fix, no comment from maintainers |
| [#61656](https://github.com/NousResearch/hermes-agent/issues/61656) | 4 days | Policy hooks | 2026-07-09 | Enterprise security feature requesting design feedback |
| [PR #12355](https://github.com/NousResearch/hermes-agent/pull/12355) | 84 days | CLI refactor | 2026-04-19 | 2,158-line extract from god-file `cli.py` — large, low review engagement |
| [PR #17472](https://github.com/NousResearch/hermes-agent/pull/17472) | 74 days | PII sanitizer skill | 2026-04-29 | Third-party skill PR awaiting merge or decision |
| [PR #17329](https://github.com/NousResearch/hermes-agent/pull/17329) | 74 days | Subagent timeout | 2026-04-29 | Fix for `delegate_task` timeout debugging — P2, labeled duplicate |

</details>

<details>
<summary><strong>PicoClaw</strong> — <a href="https://github.com/sipeed/picoclaw">sipeed/picoclaw</a></summary>

Here is the PicoClaw project digest for **2026-07-13**.

---

## PicoClaw Project Digest: 2026-07-13

### 1. Today's Overview
Activity on the PicoClaw repository remains moderate, with a slight uptick in issue reporting but a healthy close rate on pull requests. Two PRs were merged/closed, including infrastructure improvements for ARM devices and skill state management, indicating active development. However, a notable **critical bug** was reported regarding the Matrix sync loop lacking reconnection logic, which could silently kill connectivity in production. The project appears healthy overall, though maintainer engagement on a few stale but important issues (e.g., Android launch failures) is still pending.

### 2. Releases
No new releases were published today.

### 3. Project Progress
Two pull requests were merged/closed today, advancing platform support and core functionality:
- **[#3249 (CLOSED) Skill enable/disable state + cron RunNow](https://github.com/sipeed/picoclaw/pull/3249):** Merged a fork-based feature that adds an enable/disable toggle for skills via UI, plus the ability to trigger cron jobs immediately ("RunNow"). This improves user control over active skills without requiring a restart.
- **[#3250 (CLOSED) Feature: 添加对于armhf设备的docker compose支持](https://github.com/sipeed/picoclaw/issues/3250):** Added Docker Compose support for ARMv7 (armhf) devices (e.g., OneCloud, RPi Zero). Low-power homelab users can now deploy PicoClaw natively on these architectures.

One PR remains open:
- **[#3251 (OPEN) fix(providers): capture the prompt cache token usage in Anthropic providers](https://github.com/sipeed/picoclaw/pull/3251):** Fixes a gap in telemetry for Anthropic users by capturing prompt cache token usage metrics. This enables operators to verify cache effectiveness.

### 4. Community Hot Topics
The most engaging discussions this week involve reliability and cross-platform support:
- **[#3203 (OPEN) Matrix sync loop has no reconnection logic — silent death after network/server disruption](https://github.com/sipeed/picoclaw/issues/3203):** 2 comments, 1 like. The user describes a painful scenario where the Matrix bridge silently dies after any network blip. No fix PR exists yet. This is a **high-impact stability issue** for any users relying on Matrix transport.
- **[#3182 (OPEN) [BUG] Android version](https://github.com/sipeed/picoclaw/issues/3182):** 3 comments, 0 likes (stale). The user cannot launch the service on Android and cannot change the settings path. This has been open for 17 days without a maintainer response, indicating a gap in mobile support.
- **[#3252 (OPEN) splitKnownProviderModel strips provider prefix when model ID contains known provider alias](https://github.com/sipeed/picoclaw/issues/3252):** Newly reported bug (0 comments). A configuration edge case where the model ID string matches a provider prefix—likely to cause silent model routing failures for users with custom model names.

### 5. Bugs & Stability
Two new bugs were reported today, with one ranked **critical** due to its silent-failure nature:
- **Critical: [#3203 (OPEN) Matrix sync loop has no reconnection logic](https://github.com/sipeed/picoclaw/issues/3203):** No automatic reconnection after network/homeserver disruption. Systemd `Restart=on-failure` does not trigger because the main process stays alive. **No fix PR exists.** Affects all Matrix users.
- **Moderate: [#3252 (OPEN) splitKnownProviderModel strips provider prefix](https://github.com/sipeed/picoclaw/issues/3252):** Model ID parsing bug that corrupts provider assignment. Lightly tested configuration path. **No fix PR exists yet.**
- **Low (closed): [#3194 (CLOSED) Received encrypted message but crypto is not enabled](https://github.com/sipeed/picoclaw/issues/3194):** Closed without code change. User likely had encryption enabled on the Matrix room but not configured in PicoClaw. No regression.

### 6. Feature Requests & Roadmap Signals
- **ARMv7 (armhf) Docker support (Issue #3250, closed):** Already implemented and merged. Indicates growing user base on low-cost single-board computers (OneCloud, RPi Zero).
- **Skill enable/disable UI + cron RunNow (PR #3249, closed):** Merged. This reflects user demand for finer-grained control over automated tasks without editing config files.
- **Prompt cache token metrics for Anthropic (PR #3251, open):** If merged, this will add observability for cost optimization—likely to land in the next minor release (v0.2.10 or v0.3.0).
- **Prediction:** The next release will likely include armhf Docker support, the skill toggle UI, and the Anthropic cache metrics fix. Android support remains a known gap.

### 7. User Feedback Summary
- **Frustration with Android:** User `Monessem` (Issue #3182) reports a total blocker on Android—can't launch service, can't change path. No response from maintainers in 17 days. **Dissatisfaction (no solution).**
- **Silent failure in Matrix sync:** User `weissfl` (Issue #3203) describes a "silent death" scenario that is hard to detect. **Pain point: reliability-critical users cannot trust the Matrix bridge.**
- **Configuration edge cases:** User `v2up-32mb` (Issue #3252) discovered a subtle provider routing bug. **Power users hitting edge cases in model configuration.**
- **Positive signal:** The armhf support (Issue #3250) and skill toggle (PR #3249) were both user-requested and delivered quickly—indicating good responsiveness to feature requests for core platform capabilities.

### 8. Backlog Watch
- **[#3182 (OPEN) [BUG] Android version (3 comments, stale 17 days)](https://github.com/sipeed/picoclaw/issues/3182):** No maintainer acknowledgment. If PicoClaw intends to support mobile, this needs triage. Otherwise, a note about lack of Android support would manage expectations.
- **[#3203 (OPEN) Matrix sync loop reconnection logic (1 like, 2 comments)](https://github.com/sipeed/picoclaw/issues/3203):** Critical reliability bug with no fix PR. High risk of merging silently—maintainers should assign a P0 priority and consider a hotfix.
- **[#3190 (CLOSED) i18n sync (PR, stale)](https://github.com/sipeed/picoclaw/pull/3190):** Closed but not merged? The PR summary indicates work to sync translations—if not merged, i18n users (bn-in, cs) are missing UI strings. Needs a quick merge decision.

</details>

<details>
<summary><strong>NanoClaw</strong> — <a href="https://github.com/qwibitai/nanoclaw">qwibitai/nanoclaw</a></summary>

# NanoClaw Project Digest — 2026-07-13

## Today's Overview
NanoClaw is in a **high-velocity development phase** with significant structural improvements underway. In the last 24 hours, activity surged with **13 pull requests** (11 open, 2 closed/merged) and **3 new open issues**, reflecting focused work on agent runtime reliability, security hardening, and operator tooling. The project is shipping multiple fixes for critical bugs affecting reply duplication and silent failures, while advancing two major cross-cutting initiatives: a unified guard seam for privileged actions and an audit skill for CLI operations. No new releases were published today, signals the team is accumulating changes for a future release.

---

## Releases
**None** — No new releases were published in the past 24 hours. All recent changes remain in the open PR queue and will likely be batched into a next release candidate.

---

## Project Progress

### Merged/Closed Pull Requests (2 total)
Two PRs reached resolution:

- **#3024 [CLOSED] fix(container): raise the agent SDK's 32000 output-token cap to the model's real ceiling** (by javexed) — Resolves Issue #3023. Nothing in the tree previously set `CLAUDE_CODE_MAX_OUTPUT_TOKENS`, silently capping all Claude agents at 32K output tokens. This fix aligns the cap with the model's actual ceiling.

- **#2952 [CLOSED] Skill/add opencode stack** (by javexed) — Operational/container skill adding the OpenCode stack integration.

### Key Open PRs Advancing Features
- **#3029 [OPEN] feat: operator approval-resolution verbs for ncl** — Adds `approve`, `reject`, and `reject-with-reason` actions to `ncl approvals`, solving the lack of a CLI mechanism to unblock held actions locally.
- **#2986 [OPEN] Guard seam: one decision function for every privileged action** — Phase 2 of guarded-actions architecture. Every privileged action crossing container/channel boundaries now passes through a single `guard()` function returning `allow | hold | deny`, replacing inline voluntary gating.
- **#2983 [OPEN] feat: per-group harness capability toggles** — Extends the existing pattern of disabling Claude Code's cron/scheduling to two more harness capabilities, with on/off decisions per agent group.
- **#3022 [OPEN] feat: support scheduled tasks in templates** — Templates can define recurring scheduled tasks in `tasks/*.md` that are created paused when the agent group is stamped.
- **#2987 [OPEN] feat: /add-audit skill** — Opt-in local audit log for the `ncl` surface, rebased onto the guard seam feature.

---

## Community Hot Topics

**Most Active Issue (1 comment):**
- **#3016 [OPEN] Every rate_limit_event is logged as a quota error, even when "allowed"** — Reported by glifocat, 82 false-positive error logs in one week. Comments: 1. This is causing confusion and concern among users who see scary quota errors on perfectly normal turns.
  - [GitHub: Issue #3016](https://github.com/nanocoai/nanoclaw/issues/3016)

**Emerging Discussion Threads:**
- **#3023 [OPEN] Every Claude agent is silently capped at 32000 output tokens** — Already fixed by PR #3024 (merged). A significant blocker for users generating long outputs (OpenSCAD files, lengthy code generation).
  - [GitHub: Issue #3023](https://github.com/nanocoai/nanoclaw/issues/3023)

- **#3026 [OPEN] Re-wrap nudge re-runs the model and duplicates replies when agent already replied via send_message** — A subtle bug causing wasted API calls and duplicate replies. PR #3028 and #3020 both aim to fix related patterns.
  - [GitHub: Issue #3026](https://github.com/nanocoai/nanoclaw/issues/3026)

**Underlying Needs:** Users are actively encountering three core pain points: (1) false alarm logging causing support tickets and confusion, (2) silent caps on model capabilities (output tokens), and (3) reply duplication leading to spammy agent behavior in shared channels.

---

## Bugs & Stability

### Severity: Critical
- **Silent container startup failures due to dirent collision on /tmp** — PR #3027 ([OPEN](https://github.com/nanocoai/nanoclaw/pull/3027)) addresses agents going silent when `wakeContainer` fails with `EISDIR: illegal operation on a directory, open '/tmp/onecli-proxy-ca.pem'`. The root cause: a directory created by another process colliding with the expected certificate file path on `/tmp`. Fix relocates TMPDIR off `/tmp`. **Fix PR exists and is open.**

- **Undelivered unwrapped replies causing silent message drops** — PR #3020 ([OPEN](https://github.com/nanocoai/nanoclaw/pull/3020)) rescues replies that the model emitted without `<message to>` wrappers but were never delivered. Fixes Issues #2369, #2393, and part of #2404. **Fix PR exists and is open.**

### Severity: High
- **Re-wrap nudge duplicates replies after send_message** — Issue #3026 ([OPEN](https://github.com/nanocoai/nanoclaw/issues/3026)) paired with fix PR #3028 ([OPEN](https://github.com/nanocoai/nanoclaw/pull/3028)). The nudge logic (from #2414) re-runs the model when final text lacks `<message to>` blocks, but fails to detect replies already sent via `send_message`. Causes wasteful re-generation and duplicate channel messages.

### Severity: Medium
- **False positive quota errors on every completed turn** — Issue #3016 ([OPEN](https://github.com/nanocoai/nanoclaw/issues/3016)). Since PR #2965, every `rate_limit_event` is logged as a quota error regardless of status. Impacts user confidence but doesn't block functionality.

---

## Feature Requests & Roadmap Signals

### Likely in Next Release

1. **Unified guard seam (Phase 2)** — PR #2986 ([OPEN](https://github.com/nanocoai/nanoclaw/pull/2986)) transforms every privileged action boundary to pass through a single `guard()` decision function. This is foundational for security and audit—expect it to land soon.

2. **Operator approval CLI verbs** — PR #3029 ([OPEN](https://github.com/nanocoai/nanoclaw/pull/3029)) adds `approve/reject` to `ncl approvals`, directly enabling operators to unblock held actions without a UI.

3. **Scheduled tasks in templates** — PR #3022 ([OPEN](https://github.com/nanocoai/nanoclaw/pull/3022)) reduces manual setup by allowing `tasks/*.md` in templates.

4. **Audit skill for ncl surface** — PR #2987 ([OPEN](https://github.com/nanocoai/nanoclaw/pull/2987)), rebased onto the guard seam, provides opt-in local audit logging for all CLI operations.

5. **Per-group harness capability toggles** — PR #2983 ([OPEN](https://github.com/nanocoai/nanoclaw/pull/2983)) makes the on/off decision for scheduling and other capabilities configurable per group.

### Prediction
The guard seam (#2986) will likely merge first as it's a dependency for the audit skill (#2987). The approval CLI (#3029) is small and additive—also a strong candidate for early merge. The output token fix (#3025, follow-up to merged #3024) addresses a critical bottleneck for heavy users.

---

## User Feedback Summary

### Positive Signals
- **Active issue reporting** demonstrates engaged user base—users like glifocat are noticing and documenting edge cases with reproduction steps.
- **Contributors** (javexed, caburi00, ogarciarevett, robbyczgw-cla) are submitting high-quality fixes for bugs they personally encountered in production.

### Pain Points
1. **Silent output truncation** (Issue #3023): Users generating large files (e.g., OpenSCAD) hit a hard 32K token wall with no prior warning. Already fixed in merged PR #3024.
2. **False quota alarms** (Issue #3016): 82 logged "errors" in one week despite successful turns. Undermines trust in logs.
3. **Duplicate replies** (Issue #3026): Agents that already replied via `send_message` get re-ran and send duplicate messages when bare text appears at the end of a turn.
4. **Silent message drops** (Issue #2369, #2393, #2404): Long tool chains cause model to omit `<message to>` wrappers, causing complete reply loss.

### Satisfaction Signals
- The community is responding positively to the **guard seam** and **audit** features—these are seen as enterprise-grade security improvements.
- Users are adopting **ncl tasks** as their scheduling solution, evidenced by requests for template support (PR #3022).

---

## Backlog Watch

### Items Needing Maintainer Attention

1. **Issue #3016 — False positive quota errors (1 comment, no maintainer response yet)** — This is a relatively simple logging fix (wrong log level) but has been open since July 11 with no acknowledge from core team, despite affecting every installation.
   - [GitHub: Issue #3016](https://github.com/nanocoai/nanoclaw/issues/3016)

2. **PR #2982 — Reconcile Claude tool allowlist with pinned CLI** ([OPEN](https://github.com/nanocoai/nanoclaw/pull/2982)) — Has 3 comments (undefined means untracked here), but this is a maintenance PR fixing drift between the allowlist and the actual pinned Claude CLI version (tools renamed or missing). Has been open since July 8—worth merging to avoid tool-calling failures.

3. **PR #3021 — Warn before connecting a shared WhatsApp number** ([OPEN](https://github.com/nanocoai/nanoclaw/pull/3021)) — User-requested safety feature. Low complexity but high user impact (prevents accidental WhatsApp number suspension). Should be fast to review.

### Long-Standing Closed Items
No items have been abandoned beyond the 24-hour window for attention, suggesting active maintainer engagement overall.

---

</details>

<details>
<summary><strong>NullClaw</strong> — <a href="https://github.com/nullclaw/nullclaw">nullclaw/nullclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>IronClaw</strong> — <a href="https://github.com/nearai/ironclaw">nearai/ironclaw</a></summary>

Here is the IronClaw project digest for **2026-07-13**.

---

## 1. Today's Overview
The IronClaw project is in a period of **high-intensity development and stabilization**. Over the last 24 hours, 36 pull requests were merged or closed, indicating a strong push to land features and fixes. However, the project is grappling with significant **CI fragility**, with a dedicated taxonomy report showing that ~70% of recent `main` branch pushes have failed due to flaky tests. A major "extension-runtime" feature train (8 PRs) is actively advancing, with three new PRs (P1, P3, P5) opened yesterday. While no new releases were cut, the team is clearly focused on hardening the codebase against non-hermetic tests and concurrency races.

## 2. Releases
**No new releases were published in the last 24 hours.**

## 3. Project Progress (Merged/Closed PRs)
36 PRs were merged or closed in the last 24 hours, reflecting strong forward momentum on both features and bug fixes.

**Key Merged/Closed Highlights:**
- **Reborn Migration:** PR [#4379](https://github.com/nearai/ironclaw/pull/4379) (XL) migrated read-only commands `doctor`, `status`, and `config list/get` to the Reborn CLI, decoupling output from legacy rendering.
- **CI Hardening:** PR [#5991](https://github.com/nearai/ironclaw/pull/5991) (L) now requires Responses API E2E coverage in PR checks, running the complete 16-case contract suite in CI to prevent regressions.
- **QA Expansion:** PR [#5853](https://github.com/nearai/ironclaw/pull/5853) (XL) added 10 new targeted canary QA cases for Reborn WebUI v2, covering custom-tool and Responses API workflows.
- **Security Hardening:** PR [#3073](https://github.com/nearai/ironclaw/pull/3073) (XS) restricted test HTTP remap targets to HTTPS only, fixing a security gap. PR [#1941](https://github.com/nearai/ironclaw/pull/1941) (XS) fixed MCP server name injection via allowlist validation.
- **Extension Runtime (P1):** PR [#5995](https://github.com/nearai/ironclaw/pull/5995) (XL) landed the first major piece of the extension-runtime train, introducing Manifest v3, VendorId, recipes, and a resolved record.

## 4. Community Hot Topics
The most active discussion is happening around **CI fragility and test flakiness**, with a coordinated burst of issues filed by `ilblackdragon`.

- **[#6014](https://github.com/nearai/ironclaw/issues/6014): CI fragility: flaky non-hermetic tests abort the coverage matrix, reding ~70% of main pushes.** This is the highest-impact issue. The author provides a deep analysis tracing failures to a structural test-isolation defect, not bad commits. The underlying need is for deterministic CI hermiticity.
- **[#6011](https://github.com/nearai/ironclaw/issues/6011): Daily ironclaw failure taxonomy — 2026-07-12.** A dedicated, structured report cataloging every failing suite (clawbench, Reborn, Platform & Compat) with root-cause analysis. This signals a community need for systematic CI observability rather than ad-hoc fixes.
- **[#6018](https://github.com/nearai/ironclaw/issues/6018): CI hardening: add static pre-push checks.** Proposes adding cheap pre-push hooks (e.g., `include_str!` validation, libsql-only clippy) to catch deterministic breakages before they hit CI. This reflects developer frustration with slow feedback loops.
- **[#6017](https://github.com/nearai/ironclaw/issues/6017), [#6016](https://github.com/nearai/ironclaw/issues/6016), [#6015](https://github.com/nearai/ironclaw/issues/6015): Flaky database, Slack trigger, and non-hermetic runtime tests.** These are specific, reproducible flaky-test bugs the community is actively documenting.

## 5. Bugs & Stability
The project faces a **severe stability crisis in CI**, though the core agent/inference runtime appears stable. Bugs are ranked by severity below.

**Critical:**
- **CI Infrastructure Collapse** (Issue [#6014](https://github.com/nearai/ironclaw/issues/6014)): ~70% of `main` pushes fail due to flaky, non-hermetic tests. This is the #1 blocker for development velocity. A fix PR chain is emerging (see Issues #6015-#6018).

**High:**
- **Agent Loop UX Bug** (Issue [#5704](https://github.com/nearai/ironclaw/issues/5704), CLOSED): Image previews losing opacity during active chat. This was a P3 bug bash item that appears to have been fixed.
- **Inference Hangs** (Issue [#6010](https://github.com/nearai/ironclaw/issues/6010), CLOSED): GLM-5.2 hanging for minutes during opencode usage. Closed with no public fix details; likely a new inference endpoint was deployed.

**Medium/Low (Flaky but Confirmed):**
- **DB Concurrency Race** (Issue [#6017](https://github.com/nearai/ironclaw/issues/6017)): Postgres delete/recreate race and libSQL concurrent writers.
- **Slack E2E Timeout** (Issue [#6016](https://github.com/nearai/ironclaw/issues/6016)): Trigger delivery e2e tests timing out, reding `Tests (Reborn)`.
- **Non-Hermetic Runtime** (Issue [#6015](https://github.com/nearai/ironclaw/issues/6015)): `build_runtime_input_production_*` tests race on `std::env` in the all-features coverage leg.

**Need Attention:**
- **GLM-5.2 Model Discovery** (Issue [#6009](https://github.com/nearai/ironclaw/issues/6009), CLOSED): Users had to manually add GLM-5.2 to opencode. This was closed, but the underlying model discovery mechanism may still be fragile.

## 6. Feature Requests & Roadmap Signals
No new user-requested features were filed today, but the PR stack reveals clear roadmap signals:

- **Extension Runtime (P1, P3, P5):** The train is accelerating. PR [#5995](https://github.com/nearai/ironclaw/pull/5995) (P1, landed) introduces Manifest v3 and recipes. PR [#6008](https://github.com/nearai/ironclaw/pull/6008) (P3, open) introduces an auth engine. PR [#6012](https://github.com/nearai/ironclaw/pull/6012) (P5, open draft) adds Slack/Telegram outbound delivery. This is the dominant feature stream.
- **Tools-Capable Agent Loop:** PR [#6013](https://github.com/nearai/ironclaw/pull/6013) (open) makes the agent-loop completion nudge tools-capable, enabling automated tool calls during interactive coding. This is likely for the next point release.
- **Doctor Diagnostics:** PR [#6019](https://github.com/nearai/ironclaw/pull/6019) (open) adds LLM/provider credential readiness checks and a `--live` flag to `doctor`, improving developer onboarding.
- **Canary Observability:** PR [#6020](https://github.com/nearai/ironclaw/pull/6020) (open) makes Q-10 Slack journeys deterministic, suggesting the canary suite is being hardened for reliability signals.

**Prediction for Next Version:** A release candidate will likely include the P1 extension-runtime foundation, the Reborn doctor migration, the tools-capable agent loop, and a CI hardening pass to fix the flaky test infrastructure.

## 7. User Feedback Summary
Real user pain points surfaced today:

- **Inference Reliability (High Pain):** Issue [#6010](https://github.com/nearai/ironclaw/issues/6010) describes GLM-5.2 hanging for "minutes at a time" during real-time opencode usage, making it "unusable for interactive development." This is a critical UX failure that was closed, but users may continue to hit edge cases.
- **Model Discoverability (Medium Pain):** Issue [#6009](https://github.com/nearai/ironclaw/issues/6009) highlights that users must "fork opencode" and add GLM-5.2 manually. For a flagship model, this creates a high barrier to entry.
- **CI Reliability (Developer Pain):** The flurry of CI issues (#6014-#6018) comes from core contributors, indicating internal developer dissatisfaction with the current workflow. The "red wave" pattern (full-red CI for days) is destructive to team morale.

**Net Sentiment:** Mixed. Users are getting powerful new features (extension runtime, Reborn migration) but are suffering from poor CI reliability and sporadic inference hangs.

## 8. Backlog Watch
Several dependency update PRs have been open for extended periods and may introduce blocking conflicts:

- **PR [#5664](https://github.com/nearai/ironclaw/pull/5664) (Open since Jul 5):** Bumps the `actions` group with 16 updates, including `actions/checkout` (v4→v7) and `anthropics/claude-code-action` (v1.0.88→v1.0.171). **Risk:** Critical CI actions are out of date; this needs a maintainer to resolve rebase conflicts.
- **PR [#5114](https://github.com/nearai/ironclaw/pull/5114) (Open since Jun 21):** Bumps the `tokio-ecosystem` group with 4 updates (tokio-tungstenite, hyper, etc.). **Risk:** 22 days stale; could block async runtime improvements.
- **PR [#4032](https://github.com/nearai/ironclaw/pull/4032) (Open since May 25):** Bumps the `wasm` group (wit-component, wit-parser). **Risk:** 49 days stale; potential ABI incompatibility with the new extension-runtime if left unattended.
- **PR [#5926](https://github.com/nearai/ironclaw/pull/5926) (Open since Jul 10):** Bumps the `everything-else` group with 20 diverse updates. Dependabot is actively rebasing this, but it has not been merged.

**No user-submitted issues or PRs appear to be unaddressed by maintainers.** The project's core team is actively triaging the backlog.

</details>

<details>
<summary><strong>LobsterAI</strong> — <a href="https://github.com/netease-youdao/LobsterAI">netease-youdao/LobsterAI</a></summary>

# LobsterAI Project Digest — 2026-07-13

**Project:** LobsterAI (netease-youdao/LobsterAI)  
**Analysis Date:** 2026-07-13  

---

## 1. Today's Overview

Project activity is relatively low today, with 1 open issue and 2 pull requests (1 open, 1 closed) updated in the last 24 hours. No new releases have been published, and no fresh contributions were introduced. The community is engaging most heavily around a persistent multi-agent configuration bug (Issue #2293), which has drawn multiple comments and user frustration. Meanwhile, two older PRs — one adding UI tooltips (#1325) and one fixing Agent ID generation (#2065) — remain in stale status, indicating possible maintainer bandwidth constraints. Overall, the project appears stable but with limited forward momentum in the past day.

**Activity Assessment:** Low — maintenance mode or quiet day; no new code merged or released.

---

## 2. Releases

*None.* No new releases were published in the last 24 hours or in the near history.

---

## 3. Project Progress

**Merged/Closed PRs today:**  
- **[#2065 — fix(agent): 使用短 UUID 替代名称生成 Agent ID](https://github.com/netease-youdao/LobsterAI/pull/2065)** [CLOSED]  
  - ✅ *Closed* (status: stale → closed). This PR addresses the **“data resurrection”** problem where deleting and recreating an Agent with the same name would resurrect old local files (workspace, sessions). The fix replaces name-based IDs with short UUIDs.  
  - **Key insight:** The PR also documents remaining cleanup gaps — `cowork_sessions` , `workspace` directories, and `USER.md` files are not yet cleaned on Agent deletion. This is likely related to the bug reported in Issue #2293.

**No new PRs were opened today.** The only other PR updated is #1325, which remains open/stale.

---

## 4. Community Hot Topics

The most active discussion is around:

- **[Issue #2293 — [OPEN] 重启后，多个agent下的USER.md被覆盖替换的BUG？](https://github.com/netease-youdao/LobsterAI/issues/2293)**  
  - **Comments:** 4 | **Author:** yepcn | **Created:** 2026-07-07 | **Updated:** 2026-07-12  
  - **Summary:** User reports that modifying “About You” settings or `USER.md` for one agent causes other agents’ `USER.md` files to be overwritten. After restart, all agent `USER.md` files are replaced by the main agent’s version. The user suspects a recent update introduced this regression.  
  - **Analysis:** This is a high-impact configuration bug affecting multi-agent workflows — a core use case for LobsterAI. The lack of maintainer response (no assignee, no linked fix PR) may be a concern.

**Underlying needs:** Users expect proper isolation between agent profiles. The bug violates the mental model of independent agents and degrades workflow reliability.

---

## 5. Bugs & Stability

| Issue | Severity | Description | Fix PR Exists? |
|-------|----------|-------------|----------------|
| [#2293](https://github.com/netease-youdao/LobsterAI/issues/2293) | **High** | Multi-agent `USER.md` overwrite bug — all agents share the same profile after restart or manual edit. | ❌ No fix PR linked yet |
| [#2065](https://github.com/netease-youdao/LobsterAI/pull/2065) (merged) | Medium (resolved) | Agent ID generation bug causing data resurrection on re-creation. | ✅ Closed (fix merged) |

**Observations:**  
- Issue #2293 is the most actionable bug. It may be a regression related to recent changes (possibly the same root cause as PR #2065’s “remaining cleanup gaps”).  
- No crash or security issue reported today.

---

## 6. Feature Requests & Roadmap Signals

- **UI polish (PR #1325 — stale):** [feat(ui): 为新建对话图标按钮添加悬停提示](https://github.com/netease-youdao/LobsterAI/pull/1325)  
  - Adds tooltip hints for “new conversation” icons in collapsed sidebar. This is a low-effort UX improvement that would benefit all users. Stale since April 2026 — suggests maintainers may be deferring UI refinements.

- **Requested (from Issue #2293):**  
  - User implicitly requests **per-agent configuration isolation** and **configuration persistence across restarts**.  
  - Also implies a desire for **better internal state management** and possibly **a UI option to manually reset agent profiles**.

**Prediction for next release:**  
- Likely continuation of the Agent ID fix (#2065) to also clean up `cowork_sessions`, `workspace`, and `USER.md` on delete.  
- Possible hotfix for #2293 if it is indeed a recent regression.

---

## 7. User Feedback Summary

- **Pain point:** “I created multiple agents, but changing one agent’s ‘About You’ or USER.md modifies all agents — this makes it impossible to set different requirements for different agents.”  
- **Pain point:** “After restart, all USER.md files are overwritten by the main agent’s version.”  
- **Satisfaction:** No positive feedback reported today; the only feedback is this bug report.  
- **Use case:** Multi-agent configuration for distinct tasks (e.g., writing assistant, coding helper, customer support agent) — a key differentiator for LobsterAI.

**Sentiment:** Frustrated — user has spent time diagnosing the bug and suspects a recent update caused it.

---

## 8. Backlog Watch

| Item | Age | Last Activity | Maintainer Attention Needed? |
|------|-----|---------------|------------------------------|
| [#1325 — feat(ui): 为新建对话图标按钮添加悬停提示](https://github.com/netease-youdao/LobsterAI/pull/1325) | ~3 months (since 2026-04-02) | Updated 2026-07-12 (stale label) | ❄️ Stale — needs review or closure |
| [#2293 — 重启后，多个agent下的USER.md被覆盖替换的BUG？](https://github.com/netease-youdao/LobsterAI/issues/2293) | 6 days (since 2026-07-07) | Updated 2026-07-12 | ⚠️ High — no maintainer response, no assignee |
| [#2065 — fix(agent): 使用短 UUID 替代名称生成 Agent ID](https://github.com/netease-youdao/LobsterAI/pull/2065) | ~45 days | Closed today (2026-07-12) | ✅ Resolved |

**Recommendations:**  
- **Priority 1:** Respond to Issue #2293 — reproduce, triage, and either fix or acknowledge.  
- **Priority 2:** Review/merge or close PR #1325 to clear the oldest open PR.  
- **Future work:** Complete the cleanup logic left unfinished in #2065 (session and workspace deletion on Agent removal).

---

*Digest generated automatically from GitHub data for 2026-07-13.*

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

# CoPaw Project Digest — 2026-07-13

Generated from [github.com/agentscope-ai/CoPaw](https://github.com/agentscope-ai/CoPaw)

---

## 1. Today's Overview

CoPaw saw a spike in activity on 2026-07-12 with **19 issues updated** (16 open, 3 closed) and **10 pull requests updated** (7 open, 3 merged/closed), signaling a high-traffic day dominated by **v2.0.0 regression reports**. No new releases were published. The community is actively reporting bugs introduced by the recent 2.0.0 upgrade, particularly around **context compression breaking tool_call/tool_result pairing**, **skill system failures for new installations**, and **media/layout compatibility issues with v1.x sessions**. The maintainer team appears to be responsive, with three PRs already merged to address legacy compatibility issues, but the volume of incoming bug reports suggests the 2.0.0 release may have been rushed. Overall project health is **moderately active but under regression pressure**.

---

## 2. Releases

None.

---

## 3. Project Progress

**Merged/Closed PRs (3 total):**

- **[PR #5987](https://github.com/agentscope-ai/CoPaw/pull/5987)** — `fix(scroll): sanitize unpaired tool messages after context compression` (closed, first-time contributor @tadebao). Addresses orphan `tool_result` messages after compression evicts paired `tool_call` messages.
- **[PR #5988](https://github.com/agentscope-ai/CoPaw/pull/5988)** — `fix(compat): handle legacy 'file' block type in _coerce_block` (closed, @Nioolek). Adds handling for `file`-type blocks in v1→v2 deserialization.
- **[PR #5990](https://github.com/agentscope-ai/CoPaw/pull/5990)** — Same fix as #5988, likely a duplicate/rebase (closed).

**Key feature advances (open PRs under review):**

- **[PR #5869](https://github.com/agentscope-ai/CoPaw/pull/5869)** — Exposes system commands (`/new`, `/history`, `/plan`, `/dream`, etc.) in slash autocomplete across TUI and web console.
- **[PR #5992](https://github.com/agentscope-ai/CoPaw/pull/5992)** — Adds per-session model overrides with a Settings modal for reviewing/resetting.

---

## 4. Community Hot Topics

**Most Active Issues:**

1. **[#5952](https://github.com/agentscope-ai/CoPaw/issues/5952)** — `auto-memory fails with "No module named 'agentscope.tool._builtin._scripts'"` (4 comments). Blocking auto-memory summarization. A fix PR **[#5997](https://github.com/agentscope-ai/CoPaw/pull/5997)** was opened the same day to include AgentScope's Glob helper in the desktop bundle.

2. **[#5986](https://github.com/agentscope-ai/CoPaw/issues/5986)** — `Context compression breaks tool_call/tool_result pairing → 400 BadRequestError` (4 comments). Also spawned [#5987](https://github.com/agentscope-ai/CoPaw/pull/5987) and [#5989](https://github.com/agentscope-ai/CoPaw/pull/5989) fix PRs. This is a **critical API-breaking regression** for all users with long-running sessions.

**Underlying needs:**
- Users deeply rely on **tool-calling workflows**, and the compression middleware is breaking the fundamental assumption that `tool_call`/`tool_result` pairs remain intact. The community needs **guaranteed pair preservation** during eviction.
- Auto-memory (#5952) being broken affects the core "memory" feature, which is a key differentiator for AI assistants.

---

## 5. Bugs & Stability

**Critical Severity:**

1. **[#5986](https://github.com/agentscope-ai/CoPaw/issues/5986)** — Context compression producing orphan `tool_result` messages → 400 errors with any OpenAI-compatible API. **Fix PRs exist**: [#5987](https://github.com/agentscope-ai/CoPaw/pull/5987) and [#5989](https://github.com/agentscope-ai/CoPaw/pull/5989).
2. **[#5952](https://github.com/agentscope-ai/CoPaw/issues/5952)** — Auto-memory completely broken due to missing module in desktop build. **Fix PR exists**: [#5997](https://github.com/agentscope-ai/CoPaw/pull/5997).

**High Severity:**

3. **[#5964](https://github.com/agentscope-ai/CoPaw/issues/5964)** — v1→v2 upgrade causes session mapping loss in `history.db`, returning 500 errors when opening old chats. User data is intact but inaccessible. Two compatibility PRs merged today ([#5988](https://github.com/agentscope-ai/CoPaw/pull/5988), [#5990](https://github.com/agentscope-ai/CoPaw/pull/5990)) partially address related media issues.
4. **[#6001](https://github.com/agentscope-ai/CoPaw/issues/6001) / [#6000](https://github.com/agentscope-ai/CoPaw/issues/6000)** — **Skill system completely broken** for newly added skills — no new skill appears in the pool regardless of installation method. No fix PR exists yet.
5. **[#5995](https://github.com/agentscope-ai/CoPaw/issues/5995)** — Messages silently dropped when session is busy (no queue, no error). This is a **data-loss bug** for all channel integrations.

**Medium Severity:**

6. **[#5996](https://github.com/agentscope-ai/CoPaw/issues/5996)** — `MODEL_EXECUTION_ERROR` during chat due to `ToolResultBlock` being orphaned by hint message formatter.
7. **[#5982](https://github.com/agentscope-ai/CoPaw/issues/5982)** — Shell execution demands approval every time after v2.0.0 upgrade, even in containerized deployments.
8. **[#5983](https://github.com/agentscope-ai/CoPaw/issues/5983)** — `qwenpaw doctor` fails with hardcoded `/api/agent/health` endpoint that doesn't exist.
9. **[#5984](https://github.com/agentscope-ai/CoPaw/issues/5984)** — Tool approval prompts appear in Feishu channel even with governance disabled in UI (particularly affects Raspberry Pi/ARM devices without Landlock).

**Low Severity:**

10. **[#5981](https://github.com/agentscope-ai/CoPaw/issues/5981)** — Search field for model auto-filled with username from auth page (cosmetic/UX).
11. **[#5977](https://github.com/agentscope-ai/CoPaw/issues/5977)** — Plugin HTTP routes lost after workspace hot-reload.
12. **[#5978](https://github.com/agentscope-ai/CoPaw/issues/5978)** — `/compact` fails with invalid characters error for session IDs containing colons (e.g., `telegram:60xxxxx`).
13. **[#5979](https://github.com/agentscope-ai/CoPaw/issues/5979)** — Electron CLI tool crashes under sandbox (Linux, root user mapping).
14. **[#5980](https://github.com/agentscope-ai/CoPaw/issues/5980)** — v2.0.0 missing SSH Offline and Profiles features that existed in v1.1.12 (returns 404).
15. **[#5994](https://github.com/agentscope-ai/CoPaw/issues/5994)** — Governance AUTO mode triggers security review on every operation, causing severe slowdown.

---

## 6. Feature Requests & Roadmap Signals

**Most requested features this cycle:**

1. **[#5999](https://github.com/agentscope-ai/CoPaw/issues/5999)** — **Cross-channel session handoff**: Allow a conversation to continue seamlessly across Console, Feishu, DingTalk, etc. This signals growing demand for **omnichannel continuity** as users deploy agents across multiple platforms.

2. **[#5992](https://github.com/agentscope-ai/CoPaw/pull/5992)** — **Per-session model overrides** (open PR). Users want fine-grained control to assign different models to different sessions without changing agent defaults. Likely to appear in next release.

3. **[#5869](https://github.com/agentscope-ai/CoPaw/pull/5869)** — **System commands in autocomplete** (under review). Improves discoverability of power user commands across all UIs.

**Predictions for next release:**
- **Per-session model overrides** (#5992) will likely land; it has a clean PR with a dedicated Settings UI.
- **Context compression fix** (#5986 fix PRs) will land as an urgent hotfix.
- **Cross-channel session handoff** (#5999) is more complex and may stay as a roadmap item for v2.1 or v2.2.

---

## 7. User Feedback Summary

**Pain Points (real user quotes and patterns):**

- **"Upgrade from v1.1.12 to v2.0.0 broke everything"** — Multiple users report migration catastrophes: lost chat history (#5964), missing features (#5980), broken media (#5991), and forced approvals (#5982).
- **"New skills just don't appear"** — @NicholaLau filed two issues (#6000, #6001) expressing clear frustration that the skill system is "completely broken" for any new addition.
- **"Messages silently dropped"** — @feng183043996 reports that users don't realize their messages are being dropped when the agent is busy, which is a serious trust-eroding behavior.
- **"Every action triggers security review"** — @30toB and @BorisPolonsky both complain about excessive governance prompts slowing down their workflow significantly.
- **"qwenpaw doctor is lying to me"** — @manjieqi notes that the health check tool gives a false FAIL result, undermining trust in the diagnostic tooling.

**Satisfaction Signals:**
- Positive response to the new v2.0.0 architecture from the feature request side (#5999, #5992), suggesting the core redesign is appreciated.
- First-time contributors (@tadebao, @Nioolek, @dongbeixiaohuo) are actively submitting fixes, indicating a healthy contributor community despite the regressions.

---

## 8. Backlog Watch

**Issues needing maintainer attention:**

| Issue | Created | Last Updated | Comments | Signal |
|-------|---------|--------------|----------|--------|
| [#5952](https://github.com/agentscope-ai/CoPaw/issues/5952) | 2026-07-10 | 2026-07-12 | 4 | Auto-memory blocked for 2+ days; fix PR exists but not merged |
| [#5964](https://github.com/agentscope-ai/CoPaw/issues/5964) | 2026-07-11 | 2026-07-12 | 2 | User data inaccessible after upgrade; no explicit fix merged |
| [#6000](https://github.com/agentscope-ai/CoPaw/issues/6000) | 2026-07-12 | 2026-07-12 | 1 | Skill system completely broken; no fix in progress |

**Stale PRs needing review:**

- **[PR #5791](https://github.com/agentscope-ai/CoPaw/pull/5791)** — `fix(console): promote formatCompact unit on rounding rollover` (open since 2026-07-05, 8 days without review). A relatively small UI fix that improves number formatting.

**Recommendation:** The maintainer team should prioritize merging [#5997](https://github.com/agentscope-ai/CoPaw/pull/5997) (auto-memory fix) and [#5989](https://github.com/agentscope-ai/CoPaw/pull/5989) (context compression fix) as **hotfixes**, as they block core workflows for all users. The skill system regression (#6000) should be escalated to a critical issue with a dedicated fix PR.

</details>

<details>
<summary><strong>ZeptoClaw</strong> — <a href="https://github.com/qhkm/zeptoclaw">qhkm/zeptoclaw</a></summary>

No activity in the last 24 hours.

</details>

<details>
<summary><strong>ZeroClaw</strong> — <a href="https://github.com/zeroclaw-labs/zeroclaw">zeroclaw-labs/zeroclaw</a></summary>

Here is the project digest for ZeroClaw (zeroclaw-labs/zeroclaw) for **2026-07-13**.

---

## ZeroClaw Project Digest — 2026-07-13

### 1. Today's Overview
ZeroClaw is in a period of **very high activity**, with 50 issues and 50 PRs updated in the last 24 hours. The project is nearing a major milestone (v0.8.3), evidenced by a suite of coordinated trackers and large feature branches in active review. Bug triage is intense, with several **S1 (workflow blocked)** and critical memory/safety issues receiving attention. Two PRs were closed/merged today, but the vast majority of work remains in the open/active pipeline, indicating a deep feature freeze as the team pushes toward the release cutoff.

### 2. Releases
**No new releases published today.** The project remains at its last published version.

### 3. Project Progress
Two items moved to a closed/merged state:
- **Docs fix ([PR #9003](zeroclaw-labs/zeroclaw/pull/9003)):** Fixed a broken link in the maintainer dashboard workflow documentation.
- **Minor formatting fix ([PR #9004](zeroclaw-labs/zeroclaw/pull/9004)):** Stopped rustdoc from generating broken intra-doc links to private helper functions.

Several high-impact feature branches continue to advance with review comments and pushes:
- **Gateway** ([#8486](zeroclaw-labs/zeroclaw/pull/8486)): A large PR adding an OpenAI-compatible Chat Completions endpoint to the gateway.
- **WASM Channels & TCP** ([#8855](zeroclaw-labs/zeroclaw/pull/8855), [#8852](zeroclaw-labs/zeroclaw/pull/8852), [#8923](zeroclaw-labs/zeroclaw/pull/8923)): The infrastructure for running channel plugins via WASM is being finalized, including host-mediated outbound TCP/TLS.
- **Memory Pipeline** ([#8897](zeroclaw-labs/zeroclaw/pull/8897), [#8898](zeroclaw-labs/zeroclaw/pull/8898)): The staged retrieval pipeline for persistent memory is being wired into the live path.
- **Kickstart Defaults** ([#8987](zeroclaw-labs/zeroclaw/pull/8987)): A capability-aware defaults system was added to help new users set up safe provider configurations.

### 4. Community Hot Topics
These issues and PRs are driving the most discussion and represent key project bottlenecks:

- **[#8681] Tracker: Goal mode implementation split stack** — *9 comments* ([Link](zeroclaw-labs/zeroclaw/issues/8681))
  - *Need:* This is the coordination tracker for a major feature (goal-mode). The high comment count suggests active coordination between multiple contributors to split a large feature branch into reviewable chunks.
- **[#5808] Bug: Default 32k context budget is exceeded by system prompt + tool definitions** — *8 comments* ([Link](zeroclaw-labs/zeroclaw/issues/5808))
  - *Need:* A critical user-facing UX bug. New users hit a wall immediately because the default context budget is too small for the system prompt. The discussion likely centers on a permanent fix vs. a default value bump.
- **[#6055] Feature: Slack: hydrate thread context from conversations.replies** — *6 comments* ([Link](zeroclaw-labs/zeroclaw/issues/6055))
  - *Need:* A high-value quality-of-life feature for Slack users. The community is pushing for better thread history handling to avoid requiring re-@mentioning the bot.

### 5. Bugs & Stability
Several high-severity bugs are active, with corresponding fix PRs in review:

- **S1 - Workflow Blocked**
  - **[#9019] OpenAI Responses provider rejects vision-capable models** ([Link](zeroclaw-labs/zeroclaw/issues/9019)). *Fix PR:* None reported yet. A vision provider flag is hardcoded to `false`.
  - **[#9016] OpenAI tool turns fail when Chat Completions rejects reasoning effort** ([Link](zeroclaw-labs/zeroclaw/issues/9016)). *Status:* Accepted, fix pending. A compatibility edge-case with specific OpenAI-compatible models.
  - **[#8563] SOPs not available to agent via web dashboard** ([Link](zeroclaw-labs/zeroclaw/issues/8563)). *Status:* Accepted. A standard operating procedure file is ignored by the runtime.
  - **[#8654] skill-review fork panics (SIGSEGV) after tool-heavy turn** ([Link](zeroclaw-labs/zeroclaw/issues/8654)). *Status:* In-progress, accepted. A crash bug that kills the entire daemon on a panic/abort configuration.
- **S2 - Degraded Behavior**
  - **[#9017] --config-dir is ignored during CLI locale detection** ([Link](zeroclaw-labs/zeroclaw/issues/9017)). *Fix PR:* **[#9018](zeroclaw-labs/zeroclaw/pull/9018)** is open to fix this ordering issue.
- **S3 - Minor**
  - **[#8578] Daemon doesn't terminate on startup failure** ([Link](zeroclaw-labs/zeroclaw/issues/8578)). *Status:* In-progress. A clean exit vs. hang issue in the CLI.
- **Performance / Runtime**
  - **[#8642] MCP/tool-schema cloning drives unbounded RSS growth** ([Link](zeroclaw-labs/zeroclaw/issues/8642)). *Status:* Accepted. A memory leak split from a larger OOM tracker.

### 6. Feature Requests & Roadmap Signals
Two new feature requests filed today signal ongoing community interest in deployment flexibility and developer UX:

- **[#9022] Feature: Optional Slack Events API (HTTP Request URL) mode for scale-to-zero deploys** ([Link](zeroclaw-labs/zeroclaw/issues/9022))
  - *Prediction:* Low risk, medium impact. This targets a specific (but important) serverless deployment use case. Likely to be considered for a `.x` release.
- **[#9020] Feature: Add session rewind and fork-from-message workflows to ZeroCode** ([Link](zeroclaw-labs/zeroclaw/issues/9020))
  - *Prediction:* High impact, medium complexity. This is a core usability feature for developers using the IDE plugin. A strong candidate for v0.8.4.

### 7. User Feedback Summary
Current user feedback centers on **configuration friction** and **runtime fragility**. The high volume of `priority:p1` bugs directly impacts user trust:
- **Configuration pain:** Users find the default context budget too small ([#5808]) and are confused when specific directories like `--config-dir` or `shared/sops` are not respected ([#9017], [#8563]).
- **Stability concerns:** Users are reporting daemon crashes (SIGSEGV, panics) under load ([#8654]) and uncontrolled memory growth ([#8642]), which is a serious blocker for production deployments.
- **Channel maturity:** Users are asking for more robust channel features (Slack thread hydration, Telegram multi-message mode, Matrix streaming), indicating a desire to move beyond basic chat.

### 8. Backlog Watch
Several important items remain tagged with `needs-maintainer-review` or `needs-author-action` and require attention:

- **[#7952] Feature: Publish full-channel prebuilt assets alongside default prebuilts** ([Link](zeroclaw-labs/zeroclaw/issues/7952))
  - *Status:* Blocked, needs-maintainer-review. A distribution concern that blocks users who need custom channel support.
- **[#8832] RFC: Gateway-local Kanban board for agent work** ([Link](zeroclaw-labs/zeroclaw/issues/8832))
  - *Status:* Needs-maintainer-review. A significant RFC for a new UI paradigm; maintainer feedback is needed to either accept or deflect.
- **[#8353] fix(runtime): improve error message context...** ([Link](zeroclaw-labs/zeroclaw/pull/8353))
  - *Status:* Stale-candidate. A small quality-of-life improvement to error messages has been open for 16 days without merging.
- **[#8134] Feature: session_ttl_hours - Auto-truncate stale session history** ([Link](zeroclaw-labs/zeroclaw/issues/8134))
  - *Status:* Needs-maintainer-review. A config parameter exists in the schema but is not implemented; users are waiting for this to manage token costs.

</details>

---
*This digest is auto-generated by [agents-radar](https://github.com/kky-wollu/agents-radar).*
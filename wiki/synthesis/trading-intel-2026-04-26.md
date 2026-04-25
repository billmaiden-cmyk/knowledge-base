---
title: "Trading Intel — 2026-04-26"
created: 2026-04-26 04:00 AEST
updated: 2026-04-26 04:00 AEST
tags: [trading, intel, daily, signal-aggregation, pipeline-degraded]
sources:
  - Carry-forward only — no fresh feeds reached this run
  - wiki/synthesis/trading-intel-2026-04-25.md (yesterday's brief)
  - wiki/synthesis/trading-sync-2026-04-25.md (Antonella sync context)
---

## :warning: Pipeline Status: DEGRADED

This run could **not** ingest fresh signals. Three feeds expected by `/trading-intel` were unavailable:

1. **Signa data not refreshed** — yesterday's `/signa-pull` (12:30 PM AEST 2026-04-25) did not produce `wiki/synthesis/signa-2026-04-25.md`. The `/signa-pull` slash command was *built* on 25 Apr 20:15 (commit `ba92bf1`) but its first scheduled run either didn't fire or failed to scrape. Most likely cause: Chrome was not running with Bill logged in to `app.getsigna.ai/dashboard/signals`. No Tier 2/3 spine for today's brief.
2. **Gmail MCP not registered in this session** — `mcp__c2aa7e97...__search_threads` / `get_thread` are not bound. I could not query DannyTrades, AnnualizeThis, Hendry, Todd Harrison, Pomp, MacroEdge, Weldon, TMAD, `[intel]`/`[trading]` forwards, or `from:getsigna.ai`.
3. **Slack MCP not registered** — `mcp__7136d8b7...__slack_send_message` is not bound. The morning DM to Bill (`U05TMQ2MN0H`) cannot be sent from this run. Brief is filed; Bill will see it via the morning briefing read or by opening this file directly.

**`raw/trading-intel/` drop folder still does not exist.** No manual drops to ingest.

**What this brief contains:** carry-forward of yesterday's themes only. No new signals. No source-conflict reversals can be detected without fresh data. Treat every named ticker as "as of 25 Apr" — none of these have been re-confirmed today.

**To restore the pipeline before tomorrow (in priority order):**

1. **Open Chrome and log in to `app.getsigna.ai/dashboard/signals`**, then leave Chrome running. The 12:30 PM AEST `/signa-pull` scheduled task needs a live, authenticated browser to scrape. Without Signa, the brief loses its quant spine.
2. **Verify the MCP servers** for Gmail (`gmail-mcp` or equivalent) and Slack (`slack-mcp`) are configured in Claude Code's `~/.claude.json` / `.claude/settings.json` and that their tokens are still valid. If they were working for the 25 Apr run but not today, the MCP daemon may need restarting or tokens refreshed.
3. **Populate `wiki/trading-portfolio.md`** with current Totality positions so tomorrow's "Diff vs Portfolio" section actually delivers value (still blocked since 25 Apr).

---

## :chart_with_upwards_trend: Today's Top Picks

> **No fresh signals today.** What follows is carry-forward of yesterday's high-conviction picks, marked as **UNVERIFIED FOR 2026-04-26**. Do not trade these as if they were re-confirmed today — if you act on them, treat it as acting on yesterday's intel that has not been challenged or refreshed.

- **Photonics basket — AAOI, COHR, LITE, POET, CIEN** (bullish, **carry-forward, UNVERIFIED**) — 25 Apr cross-source signal: DannyTrades Tier 3 + AnnualizeThis overweight thematic. Both sources had full overlap on these five names. *Whether the thematic still holds today is unknown — a single negative session in the photonics complex (AAOI/COHR/LITE) could fade the thesis and we have no read on it.* Not held (portfolio template empty).
- **INTC** (bullish multi-week, near-term mixed, **carry-forward, UNVERIFIED**) — 25 Apr: Hendry's "kicked the door in" gap-and-go thesis vs. Danny's "red candle on the daily chart" near-term pullback warning. Direction was 3-source consensus (Hendry / Danny / AFR). Today's position: still on watch list pending entry timing. *No update on whether the daily red candle resolved up or down.*
- **MRVL, GLW, TSEM** (bullish photonics adjacencies, **carry-forward, UNVERIFIED, single-source**) — AnnualizeThis only on 25 Apr. No second-source confirmation arrived; today no source either way.

## Continuing Themes

| Ticker / theme | Direction | First flagged | Sources today | Status |
|---|---|---|---|---|
| Photonics basket (AAOI/COHR/LITE/POET/CIEN) | Bullish | 2026-04-25 | None — pipeline degraded | **Carry-forward, unverified** |
| INTC uptrend | Bullish | 2026-04-25 | None — pipeline degraded | **Carry-forward, unverified** |
| Photonics adjacencies (MRVL/GLW/TSEM) | Bullish | 2026-04-25 | None — pipeline degraded | **Carry-forward, single-source, unverified** |
| Cannabis Schedule III catalyst | Bullish (no specific tickers) | 2026-04-25 | None | **Carry-forward — Todd Harrison's thread not re-pulled** |
| TSLA post-earnings caution | Bearish (near-term) | 2026-04-25 | None | **Carry-forward — Danny's "yellow candle" warning not refreshed** |
| Semis core (NVDA/AMD/AVGO/TSM/SOXL/SMH/ARM) | Bullish | 2026-04-25 | None | **Carry-forward — Danny basket** |
| Crypto/miners (MSTR/COIN/GLXY/IREN/CIFR/HUT/WULF/CLSK) | Bullish trend, CIFR near-term caution | 2026-04-25 | None | **Carry-forward — no fresh confirm** |
| PLTR | Bullish (continuing) | 2026-04-24 | None | **Carry-forward** |

## New Signals (first appearance)

**None today.** Pipeline degraded — no fresh feed reached this run.

## Reversals (sentiment flipped)

**Cannot detect.** A reversal requires today's source to disagree with yesterday's. With zero fresh feeds, no reversals can be flagged. *This is itself a risk — if the photonics complex sold off 24 Apr → 25 Apr local close in the US session and any source flipped bearish overnight, this brief would not catch it.*

## Actionable Today

1. **Restore the data pipeline** (highest priority; see Pipeline Status above). Without Signa + Gmail working tomorrow, the `/trading-intel` value proposition collapses. Concretely: (a) open Chrome and log in to Signa now so the 12:30 PM AEST run on 2026-04-26 captures fresh data; (b) verify Gmail/Slack MCP servers in Claude Code; (c) populate `wiki/trading-portfolio.md`.
2. **Do not initiate new positions today on yesterday's photonics or INTC theses without re-checking prices and a fresh source.** A 24-hour-old signal traded as if fresh is a discipline failure — exactly the kind of thing the daily intel loop was built to prevent.
3. **If you want a position now**, the cleanest move is to wait for the next clean intel run (with Signa restored) before entering anything new. The Three-Setups discipline (per `/trading-sync` Decision 2) requires a current setup, not a memory of one.
4. **Watch list (carry-forward, unverified):** AAOI, COHR, LITE, POET, CIEN, MRVL, GLW, TSEM, INTC.

## Diff vs Portfolio

`wiki/trading-portfolio.md` is still a **template only** — Open Positions, Watch List, and Closed Positions tables remain unpopulated since 25 Apr.

- **Already held + reinforced today:** unknown (portfolio empty)
- **Already held + flagged for trim:** unknown
- **New opportunities not held:** unknown — no new signals today regardless
- **Held but no signal in 14d:** unknown

**This section will keep returning "unknown" until Bill populates the portfolio.** Even a 5-minute snapshot of Totality's current open positions would unlock real diff value tomorrow.

## Source Health

| Source | Last received | Volume today | Notes |
|---|---|---|---|
| **Signa AI (getsigna.ai)** | — | 0 | **Pipeline broken — `wiki/synthesis/signa-2026-04-25.md` not produced.** Chrome likely not open with Signa logged in. Bill must restore. |
| DannyTrades (Patreon) | 25 Apr 08:36 AEST | 0 today | Gmail MCP unavailable this session — could not query |
| AnnualizeThis (Substack) | 24 Apr 22:58 AEST | 0 today | Gmail MCP unavailable — could not query |
| Hugh Hendry (Substack + Bingo) | 24 Apr | 0 today | Gmail MCP unavailable — could not query |
| Todd Harrison (Substack) | 24 Apr | 0 today | Gmail MCP unavailable — could not query |
| Pomp (Substack) | 24 Apr | 0 today | Gmail MCP unavailable — could not query |
| MacroEdge | — | 0 | Silent on 25 Apr; not queryable today |
| Greg Weldon (GMSR) | — | 0 | Silent on 25 Apr; not queryable today |
| TMAD / Market Adventurer | — | 0 | Silent on 25 Apr; not queryable today |
| `[intel]` / `[trading]` Gmail forwards | — | 0 | Not queryable today |
| AFR newsletter | 24 Apr | 0 today | Not queryable today |
| `raw/trading-intel/` drop folder | — | 0 | **Folder still does not exist** |

**Twitter sources** (ShardiB2, Cantonese Cat, Sovereign Sense) are still uncovered. This remains Q05 in `wiki/strategic-questions.md`.

## Bill's Notes

> **My notes:** _(empty — Bill fills inline; next intel run reads)_

## Operational Notes

- **Slack outbound failed** — Slack MCP not bound in this session. The morning DM to `U05TMQ2MN0H` was not sent. If Bill is reading this, it's because the morning briefing surfaced the file, not because of a push notification. Spec called for "log under Operational Notes but don't fail the run" — done.
- **This is the second `/trading-intel` run** — first was 25 Apr (clean). Today shows the failure mode: the brief still files, but it should be read as a warning sign, not a daily summary. Honest brief > fabricated continuity.
- **Pipeline coupling risk identified:** `/trading-intel` depends on three external systems (Signa via Chrome MCP, Gmail MCP, Slack MCP). Today's failure in two of three (Signa + Gmail) effectively zeroed the intel value. Worth considering: a healthchecked daily that pings these dependencies *before* 4 AM and pages Bill if any are broken — so 4 AM never produces a hollow brief silently.
- **Photonics theme age:** today is 1 day since first flag. If the carry-forward extends past 3 days without a fresh confirmation, lower the conviction display and consider de-listing per the spec's "Held but no signal in 14d" logic, applied symmetrically to watch list items.

## Related Pages

- [[trading-intel-2026-04-25]] — yesterday's brief; full source of today's carry-forward
- [[trading-sync-2026-04-25]] — Antonella sync; Three-Setups framework, FDV decision, sell-rules adoption
- [[trading-portfolio]] — current holdings tracker (still unpopulated template)
- [[signa-ai-workflow]] — `/signa-pull` design; failure mode notes apply here

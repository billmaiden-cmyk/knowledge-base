---
title: "Trading Sync — 2026-04-25"
created: 2026-04-25 10:30 AEST
updated: 2026-04-25 10:30 AEST
tags: [trading, sync, antonella, position-synthesis]
sources:
  - wiki/synthesis/trading-sync-2026-04-06.md
  - wiki/comms/whatsapp-antonella-2025-04-to-2026-04.md
  - wiki/concepts/antonella-trading-program-status.md
  - wiki/concepts/antonella-kiet-setup1-changes.md
  - wiki/concepts/antonella-kama-regime-discussion.md
  - wiki/concepts/antonella-dynamic-hedge-ratio.md
  - wiki/concepts/antonella-powerbi-direct-access.md
  - wiki/synthesis/public-to-private-opportunities.md
  - wiki/entities/liberty-cf-deal-pipeline.md
  - wiki/briefings/2026-04-20.md
  - wiki/briefings/2026-04-21.md
  - wiki/briefings/2026-04-22.md
  - wiki/briefings/2026-04-23.md
  - wiki/briefings/2026-04-24.md
  - wiki/briefings/2026-04-25.md
  - Gmail (Antonella threads, 7–16 Apr 2026)
  - Outlook "Security Update: Power BI Access & AI Integration" thread, 23 Apr 2026
---

## Executive Summary

Major progress since the 6 April sync. Infrastructure is largely unblocked: Kiet's **Setups page went LIVE ~17 Apr** with all three setups implemented, buy/sell rules documented, and VMA-9 + constructive base v1 improvements shipped. Bill reversed his earlier position and **adopted Antonella's sell-rules priority**, writing a "Sell Rule Refinement" document and including it in the 19 Apr research package sent to Antonella. A meaningful new capability: **Sebastian now has a dedicated MTS mailbox with Power BI Pro + MFA** (provisioned by Andrew Tang 23 Apr) — infrastructure for the Sebastian-Kiet walkthrough is in place.

The single critical blocker from the last sync is still open: **Sebastian–Kiet data walkthrough has not happened** (A01 is now 23 days overdue). This was the stated prerequisite for autoresearch to run against real data and it has not converted. The in-person catchup Antonella requested for Wed 22 / Thu 23 April at 4:30pm was not confirmed in any briefing — status unclear; likely did not happen given Bill's diary that week.

New strategic development: the trading system has begun producing Liberty CF deal flow. 14-15 April Antonella and Ron delivered ~14 ASX public-to-private candidates (EML, MVF, BAP, EDV, HLS, AQZ, FPR, MYX, ABY, IPH, SDF/AUB, OFX, RDY) and warm intros for EML and MVF. The trading system is now doubling as an origination engine for Liberty — a concrete convergence with Wealth Engine 2.

Three decisions need Bill's attention most urgently: (1) force the Sebastian–Kiet walkthrough this week, (2) make a call on FDV position sizing (Antonella's source thesis landed 20 Apr, Bill: *"that FDV convo was pretty fucking hot"*), (3) confirm or reschedule the in-person Antonella catchup.

## What's Changed Since the 6 April Sync

### Completed (major)
- **Setups page LIVE ~17 Apr** — Kiet published the unified query output with all three setups. Bill: *"I am very excited to review."* Mode A live signals are now visible. *(source: WhatsApp Kiet, ~17 Apr; briefing 2026-04-21)*
- **Constructive base v1 improvements — DONE by Kiet.** Distribution penalty, tight streak component, ATR-normalised tightness all implemented. `constructive_score` in DB now reflects these. *(source: [[antonella-trading-program-status]], updated 2026-04-06)*
- **Setup 1 query changes — implemented.** SMA version gained `close > SMA-10`; VMA version changed to `vma9_direction IN (Flat, Rising) + ABS(close - vma_9) <= 1.0 × ATR14`. *(source: [[antonella-kiet-setup1-changes]])*
- **VMA-9 — DONE.** VMA-18/27 deferred to autoresearch (VMA-9 sufficient for v1). *(source: trading-program-status, 6 Apr update)*
- **Sell Rule Refinement document written by Bill** — included in the 19 Apr research package. Resolves the Divergence #2 from the 6 April sync. *(source: briefing 2026-04-21)*
- **Research package sent to Antonella 19 Apr**: Performance Report, SMA Evaluation, Realistic Evaluation, Sell Rule Refinement, plus live signal PDFs. Antonella: *"will read in detail asap."* *(source: briefing 2026-04-21)*
- **Sebastian Power BI Pro access provisioned 23 Apr.** Andrew Tang set up a dedicated MTS mailbox with Power BI Pro license + MFA. GoDaddy order #3939171714 bundled the M365 email + Power BI Pro license (5,307,113₫ inc GST). *(source: Outlook "Security Update: Power BI Access & AI Integration" thread, 23 Apr; briefing 2026-04-24)*
- **[[Antonella — Dynamic Hedge Ratio]] concept page created** — Antonella's paper on hedge ratio as `(1−BaseQuality) × (1−SqueezeProbability) × β × L`. *(source: raw/whatsapp/00003397-Dynamic Hedge Ratio.docx)*
- **[[Antonella — Three Setups × KAMA Regime Discussion]] concept page created** — Bill's discussion document is now formalised in the wiki. *(source: raw/whatsapp/00003354-Discussion_Three_Setups_x_KAMA_Regime.docx)*
- **[[Antonella — Power BI Direct Access]] concept page created** — two options documented (Power BI REST API via service principal, or direct Azure SQL) to eliminate manual Excel export. *(source: Bill Maiden debrief, 19 Apr)*

### In progress
- **Weekly VMA** — Bill requested 17 Apr, Kiet confirmed *"I'll add VMA_weekly"*. Implementation ongoing. *(source: briefing 2026-04-21)*
- **autoresearch.zip sent to Kiet 19 Apr** — AI-assisted research integration. Kiet reviewing. *(source: briefing 2026-04-21)*
- **Antonella "Backtest set up" Google Sheet shared 16 Apr** — she's setting up her own backtest workflow in parallel. *(source: Gmail 19d9524b7e27b674, 16 Apr)*
- **"COH old and new" sheet shared 7 Apr (Bill + Kiet cc'd)** — continued constructive base work on Cochlear. *(source: Gmail 19d65f8baa315591, 7 Apr)*

### Still pending / unconfirmed
- **Sebastian–Kiet data walkthrough** — A01 in briefings, 23 days overdue as of 23 Apr. Infrastructure is now provisioned (Sebastian has the mailbox + Power BI Pro) but no confirmation the walkthrough with Kiet has happened. This remains the critical path blocker for autoresearch. *(source: briefings 2026-04-20 through 2026-04-24)*
- **`dist_vma9`, `vma9_direction`, `base_number` columns** — status marked "⚠️ Confirm with Kiet" in trading-program-status. Not validated since 6 Apr. *(source: [[antonella-trading-program-status]])*
- **Kiet timesheet 12–18 Apr** — Kiet sent 21 Apr 12:15am. Pay this week (A87 on 21 Apr). *(source: briefing 2026-04-21)*
- **Antonella in-person catchup** — she requested Wed 22 / Thu 23 April at 4:30pm on 19 Apr. Bill had WhatsApp response flagged (A86 on 21 Apr). Neither briefing for 22 nor 23 Apr mentions the catchup happening; Bill's diary was heavy MTS (Blaxland EGM, Khoi Google Ads, Liberty Call Plan, SP 4743, Misha/Dragonfly). Likely did not occur.
- **KAMA vs VMA debate** — Bill's KAMA Regime discussion doc is now a concept page, but no evidence Antonella has formally responded. Open since the 6 April sync.

### New strategic intel
- **P2P Liberty pipeline** — 14 April Antonella/Ron delivered ~14 ASX public-to-private targets. EML (Anthony Hynes) and MVF (new female CEO, intro warm via Ron) are actionable now. See [[public-to-private-opportunities]] and [[liberty-cf-deal-pipeline]]. This is a concrete convergence of the trading system with Liberty CF — the filter is doubling as deal origination.
- **FDV confidential buy thesis (20 Apr)** — Antonella sent audio of source's strong FDV buy case. Bill: *"that FDV convo was pretty fucking hot."* Position sizing decision pending. *(source: briefing 2026-04-21)*
- **PNV validation (14 Apr)** — Antonella forwarded email from David Williams (former PNV Chairman): *"I have purchased 578,560 shares so far in CY 26 as low of $0.92c and sold none. I now have 22,233,560 shares... At yesterdays close of $1.05 I can now afford a Flat White with Full Cream Bega Milk."* Insider buying confirms the 2 April PNV watch thesis. *(source: Gmail 19d89177867245c1)*
- **NXT — passed.** Not above weekly VMA, daily overextended (17 Apr). Both agreed to pass. Early evidence of rules-based discipline Bill/Antonella have been building. *(source: briefing 2026-04-21)*
- **MergerLoop ACCC Deal Digest forwarded 14 Apr** — Antonella flagged as potential reference. *(source: Gmail 19d8e1ba83d48cda)*
- **MVF catch-up call 14 Apr** — Antonella emailed Bill "keep confidential thanks" — CEO conversation content. *(source: Gmail 19d8b0989efec8fc)*

## Antonella's Current Position

### Framework & Approach
Antonella is in **reading/validation mode** on Bill's 19 Apr research package (Performance Report, SMA Evaluation, Realistic Evaluation, Sell Rule Refinement). Her framework contributions are still active: she set up her own backtest sheet on 16 Apr, continued constructive base refinement on COH (7 Apr), and produced the Dynamic Hedge Ratio paper. The "reading mode" signals convergence — she no longer appears to be pushing net-new components.

### Recent Changes
- **Pivoted to P2P/M&A origination** — the 14-15 April WhatsApp burst delivered a structured list of ASX candidates with CEO context. This is a distinctly new channel: the trading filter translated into deal targets. *(source: [[liberty-cf-deal-pipeline]])*
- **Dynamic Hedge Ratio paper** — formalised the hedging framework: `Hedge = (1−BaseQuality) × (1−SqueezeProbability) × β × L`. ATR contraction + SI = energy storage. *(source: [[antonella-dynamic-hedge-ratio]])*
- **FDV buy thesis (20 Apr)** — brought in a high-conviction idea from her source network. Pushing for consideration.
- **MVF CEO intel (14 Apr)** — "keep confidential" suggests deepening CEO-side intelligence that feeds both trading and Liberty workflows.

### Concerns & Objections
None actively surfaced in the period. The historical concerns (infrastructure not ready, sell rules deferred, Sebastian-Kiet handoff not happening) are either resolved or unaddressed rather than re-raised.

### Requests to Kiet
- Nothing net-new from Antonella directly in this period. Kiet's current queue (weekly VMA, autoresearch.zip review) comes from Bill.

## Bill's Current Position

### Documented Design Principles
- **Shipped over debated** — setups page is live, queries are running, the research package is circulating. Bill's 6 April "stop debating, start testing" has translated into work product.
- **Adopted sell rules** — the Sell Rule Refinement document is a reversal from "wants to park selling" (6 April). This is an important signal: Bill updated on Antonella's Clover evidence rather than defending the earlier position.
- **Infrastructure investment** — provisioning Sebastian a Power BI Pro mailbox is an intentional bet to unblock the walkthrough that's been stuck for 3+ weeks.
- **Rules-based discipline holding** — NXT pass on 17 April is concrete evidence the "remove 'I am smarter than the rules' thinking" principle is being practised. *Open question: has the WTC position been resolved per the 6 April recommendation?*

### Recent Communications
- **Requested weekly VMA 17 Apr** — confirms Bill's VMA preference is still the centre of gravity; KAMA discussion is paused, not won.
- **Sent autoresearch.zip 19 Apr** — Bill is pushing to get the autoresearch pipeline operational before Kiet's bandwidth becomes a constraint.
- **Agreed NXT pass 17 Apr** — collaborative rules-based discipline with Antonella, not unilateral discretion.
- **"Pretty fucking hot" re FDV** — emotionally engaged but no decision yet. Classic Bill-on-FOMO pattern; sizing discipline test.

### Wealth Plan Alignment
The trading program is **Wealth Engine 3** in the $53m/5yr generational wealth plan. Position from the 6 April sync: *"On track conceptually; behind on execution."* **Update:** execution gap has closed meaningfully. Live setups page = first material output. However the wealth plan's *"written investment policy with hard position limits, correlation controls, and drawdown triggers"* is still listed DRIFTING in the 21 April briefing's Wealth Plan Health table — the mechanism is coming but the policy is not written. *Bill should consider codifying the investment policy now that the signal engine is live — the policy is the governor on the engine.*

## Divergence Map

| # | Topic | Antonella's View | Bill's View | Impact | Resolution Path |
|---|-------|-----------------|-------------|--------|----------------|
| 1 | **VMA vs KAMA** | Explored KAMA as alternative/complement; no formal response to Bill's KAMA discussion doc | VMA-9 is the production signal; weekly VMA now being built; KAMA discussion is a reference doc, not a work stream | Low — VMA is winning by delivery. Autoresearch can test KAMA alternatives once it's running | Resolved pragmatically: VMA proceeds. KAMA enters autoresearch backlog. Retire as a divergence |
| 2 | **Sell rules timing** | *Resolved* — Bill adopted her position and wrote the spec | Bill shipped the Sell Rule Refinement document 19 Apr | — | Closed |
| 3 | **Infrastructure readiness** | *Resolved* — setups live, constructive base v1 done, Sebastian has access | Bill invested in provisioning Sebastian's mailbox + Power BI Pro | Residual: Sebastian–Kiet walkthrough still not executed (23 days overdue) | Force the walkthrough this week. Infrastructure is no longer the excuse; calendar friction is |
| 4 | **Communication rhythm** | Prefers real-time WhatsApp analytical exploration + in-person catchups | Prefers structured documents + periodic alignment meetings | Medium — in-person request (Wed/Thu 22/23) appears not to have happened; WhatsApp-only rhythm may be fraying | Schedule and hold the in-person catchup this week. Use the research package as the agenda anchor |
| 5 | **FDV position sizing** *(NEW)* | Strongly advocating based on source audio; *"pretty fucking hot"* | Engaged but undecided | Medium — decision with real money at stake. Antonella's P2P targets list already has 14 other names; FDV is singular emphasis | Apply the Three Setups + constructive base framework to FDV. If it's Setup 2 (Continuation) take full size per rules; if not, smaller size or wait. Don't trade FDV on conviction alone — that's the pattern WTC punished |
| 6 | **Ramp-and-raise** | *Evolved, not resolved* — this pattern has become the P2P Liberty pipeline channel | Bill hasn't formalised as a 4th setup; instead converting to Liberty origination | Low — the pattern found a different home | Retire as a trading divergence. Reclassify as Liberty origination under [[public-to-private-opportunities]] |

## Kiet Dependency Tracker

| # | Item | Requested By | Status 6 Apr | Status 25 Apr | Blocker |
|---|------|-------------|--------------|---------------|---------|
| 1 | Forward returns (5d/15d/30d/60d/90d/max90d) | Both | ✅ Done | ✅ Done | — |
| 2 | VMA-9 | Bill | ⏳ In progress | ✅ Done | — |
| 3 | VMA-18/27 | Bill | ⏳ In progress | ✅ Deferred (v1 sufficient) | — |
| 4 | `dist_vma9` | Bill | ⚠️ Pending | ⚠️ Confirm with Kiet | — |
| 5 | `vma9_direction` | Bill | ⚠️ Pending | ⚠️ Confirm with Kiet | — |
| 6 | `base_number` | Both | ⏳ Pending | ⚠️ Confirm with Kiet | Setup 2 sizing |
| 7 | Constructive base v1 improvements (distribution penalty, tight streak, ATR-normalised) | Both | ⏳ Pending spec | ✅ Done | — |
| 8 | Setup 1 query changes (SMA + VMA versions) | Bill | Not started | ✅ Done | — |
| 9 | Setups page (live signals output) | Bill | Not started | ✅ **LIVE** (~17 Apr) | — |
| 10 | Weekly VMA (`vma_weekly`) | Bill | Not requested | ⏳ In progress | — |
| 11 | autoresearch.zip integration (AI-assisted research harness) | Bill | Not requested | ⏳ Kiet reviewing (since 19 Apr) | — |
| 12 | ASIC short position scraping | Antonella | Not started | Not started | Low priority; not re-raised |
| 13 | Index entry/exit calculations | Both | Not started | Not started | Deferred |
| 14 | Relative strength metric | Both | Not started | Not started | Deferred |
| 15 | Index rebalance date flags | Antonella | Not started | Not started | Deferred |
| 16 | KAMA implementation | Antonella | Not started | Not started | VMA is the production path |
| 17 | Sebastian SQL/dbt walkthrough | Antonella/Sebastian | 🔴 Blocker | 🔴 **23 days overdue** — Sebastian now has Power BI Pro access but walkthrough not scheduled | Calendar friction; escalate this week |

## Decisions Needed

### Decision 1: Force the Sebastian–Kiet Walkthrough This Week
**Context:** Infrastructure is now provisioned (Sebastian has MTS mailbox + Power BI Pro + MFA as of 23 Apr, per Andrew Tang). The original blocker (no access) is gone. A01 is 23 days overdue in the actions tracker. Without this walkthrough, autoresearch can't run against live DB structure even though Bill sent Kiet the autoresearch.zip on 19 Apr.
**Options:** (a) Bill directly schedules a three-way WhatsApp group (Bill + Sebastian + Kiet) and calendar-locks a 60-minute session this week, (b) continue deferring to Sebastian to initiate, (c) have Kiet walk through the database live via a shared screen with Antonella + Bill as proxy for Sebastian
**Information Gap:** Why Sebastian hasn't made contact despite having access. Is this a language/confidence issue, a capacity issue (his day job), or a priority issue?
**Deadline:** This week (end of 1 May)
**Recommendation:** Option (a). Three weeks of drift is evidence the passive approach isn't working. Lock a slot and drive it. The walkthrough is 60 minutes of calendar. It has been held up by 3+ weeks of calendar politeness.

### Decision 2: FDV Position Sizing
**Context:** Antonella's source delivered a strong FDV buy case 20 Apr. Bill's reaction: *"that FDV convo was pretty fucking hot."* No formal trade or sizing logged in briefings since. This is exactly the type of conviction trade the 6 April sync flagged as risky (see WTC precedent: *"we need to remove 'I am smarter than the rules' ideas"*).
**Options:** (a) Run FDV through the Three Setups framework first — if it qualifies as Setup 2 (Continuation Base), size per rules; if Setup 1 (Fresh Breakout), half size; if it doesn't qualify, don't trade on the audio alone. (b) Take a smaller "conviction tranche" (25–50% of normal size) to respect the rules while participating. (c) Wait for a pullback that creates a setup entry rather than chasing the thesis.
**Information Gap:** What does FDV actually look like on the constructive base + ANTS + VMA screens right now? Has this been checked?
**Deadline:** This week — thesis is time-sensitive if the source has a catalyst window
**Recommendation:** Option (a). The discipline is the point. If FDV is a Setup 2, take full size. If not, smaller. The framework exists specifically so that "pretty fucking hot" doesn't become the sizing decision.

### Decision 3: Re-book or Cancel the In-Person Catchup with Antonella
**Context:** Antonella requested Wed 22 or Thu 23 April at 4:30pm on 19 April. Bill's response logged as A86 in the 21 April briefing but no briefing confirms it happened. Bill's 22 April had Liberty Call Plan Zoom + EGM + Blaxland fallout; 23 April had the Misha/Dragonfly meeting + work through to evening. The window has closed.
**Options:** (a) Immediately propose a new slot next week — Tuesday (Liberty day) or Thursday evenings work, (b) default to WhatsApp rhythm only, (c) book a longer session (90-120 min) once Antonella has read the research package
**Information Gap:** Has Antonella finished reading the research package? Her 19 April *"will read in detail asap"* doesn't confirm completion
**Deadline:** Early next week (29–30 April). Delay risks her enthusiasm on FDV/P2P going stale and the research package responses going cold
**Recommendation:** Option (c). Ask her to confirm when she's finished the package, then book 90 minutes the following day. Agenda: walk through her feedback on each document, lock VMA-vs-KAMA formally (retire the divergence), sign off autoresearch v1 scope.

### Decision 4: Convert Weekly VMA into an Autoresearch Experiment
**Context:** Bill requested weekly VMA on 17 April; Kiet is implementing. Once landed, this creates a new degree of freedom for the Three Setups framework (weekly regime filter layered on daily VMA). Without a design doc, this will sit in the DB without being used in queries.
**Options:** (a) Write a short spec this week (Bill, 30 minutes) defining how weekly VMA enters the Three Setups — as a filter (no entry if weekly VMA is Falling) or a sizing modifier, (b) add to autoresearch as one more variable and let it decide, (c) defer until Kiet delivers the column
**Deadline:** This week if Bill wants to write it; defer to alignment meeting otherwise
**Recommendation:** Option (b). The autoresearch design is specifically to resolve these parameter debates with data. Let it do its job. Writing the spec first only matters if autoresearch is more than 4 weeks away.

### Decision 5: WTC Position — Unclear Status
**Context:** 6 April sync recommended: *"Set a rule-based stop. This is a litmus test for the framework: if Bill can't follow rules on WTC, the system won't be credible."* No WTC mention in any briefing 7–25 April.
**Options:** (a) Check current WTC status, exit or hold per current rules, (b) ignore — position may already be closed
**Information Gap:** Is WTC still a position? At what price?
**Deadline:** This week
**Recommendation:** Bill to confirm the status. If still a position, apply the Three Setups sell rules. This is the litmus test — don't let it drift.

## Action Items

| # | Owner | Action | Priority | Due | Source |
|---|-------|--------|----------|-----|--------|
| 1 | Bill | Force Sebastian–Kiet walkthrough this week — open a three-way WhatsApp group, lock 60 min | CRITICAL | This week (by 1 May) | A01, trading-sync 6 Apr |
| 2 | Bill | Confirm `dist_vma9`, `vma9_direction`, `base_number` columns landed with Kiet | HIGH | This week | trading-program-status |
| 3 | Bill | Pay Kiet timesheet 12–18 Apr | HIGH | This week | A87 (21 Apr briefing) |
| 4 | Bill | FDV — run through Three Setups framework; decide sizing | HIGH | This week | briefing 2026-04-21 |
| 5 | Bill | Re-book in-person catchup with Antonella — suggest 90 min next week after she finishes research package | HIGH | Early next week | briefing 2026-04-21 |
| 6 | Bill | WTC status check — is it still a position? Apply rules if so | MEDIUM | This week | trading-sync 6 Apr |
| 7 | Bill | Follow up with Kiet on autoresearch.zip review status | MEDIUM | Next sync | briefing 2026-04-21 |
| 8 | Bill | Consider drafting investment policy now that signal engine is live (hard position limits, correlation, drawdown triggers) | MEDIUM | Next 2 weeks | Wealth Plan Health |
| 9 | Kiet | Confirm weekly VMA implementation status | MEDIUM | This week | briefing 2026-04-21 |
| 10 | Antonella | Complete review of 19 Apr research package + return comments | HIGH | This week | briefing 2026-04-21 |
| 11 | Sebastian | Initiate walkthrough with Kiet using new MTS Power BI Pro access | CRITICAL | This week | briefing 2026-04-24 |

## Communication Health

**Message volume (since 6 April):** Very active through 21 April on both WhatsApp channels (Antonella + Kiet). Gmail shows 5 Antonella threads (7 Apr COH sheet, 13 Apr PNV forward, 14 Apr MVF + ACCC Deal Digest, 16 Apr Backtest sheet). Nothing from Antonella in Gmail/WhatsApp in the 22–25 Apr window captured here.

**Response lag:**
- Bill → Antonella's in-person request (19 Apr): action was logged but no confirmation it was scheduled.
- Antonella → Bill's research package (19 Apr): *"will read in detail asap"*, no feedback yet.
- Sebastian → Kiet handoff: 23 days overdue.

**Tone:** Markedly more productive than 6 April. The "going in circles" frustration from 2 April is not present in the 7–25 April period. Concrete deliverables on both sides (setups page from Kiet, research package from Bill, P2P targets from Antonella, hedge ratio paper from Antonella) have replaced analytical exploration. The collaborative rules-based discipline on NXT (pass) is a positive signal.

**Patterns to watch:**
- **The in-person catchup skipping.** Bill's week was wall-to-wall MTS. The trading-program delivery is living almost entirely in WhatsApp + documents. Periodic face time is the mechanism that prevented "going in circles" from recurring; losing it is a risk.
- **Sebastian–Kiet deadlock.** Three weeks with access provisioned and still no walkthrough is not a communication problem; it's an accountability problem. Bill needs to carry the baton.
- **FDV as the next rules test.** WTC was the test that defined the framework. FDV is the first high-conviction call that arrives after the framework is live. How this is sized will tell Antonella and Bill whether the framework actually governs or is theatre.

**Recommendation:** Lock the in-person catchup for next week. Bring the research package feedback and the autoresearch v1 scope. Carry the Sebastian–Kiet walkthrough personally — don't defer another week.

## Notes for Next Sync

- First sync after the infrastructure unlock. Next sync should assess: did the Sebastian–Kiet walkthrough happen? Did autoresearch run its first overnight pass? Did FDV get traded (and at what size)?
- The Market Direction Model (Priority 1.5 in [[antonella-trading-program-status]]) remains the one genuine architectural gap. Not flagged by Antonella in this period. Worth raising in the in-person catchup.
- The [[public-to-private-opportunities]] thread is now a parallel work stream. It deserves its own tracking but lives primarily under Liberty CF, not trading — the trading filter is the *input*, not the *work*.
- The 20-April briefing recommended writing the investment policy (DRIFTING in Wealth Plan Health). Worth a short separate session with the coach or with Antonella.

## Related Pages

- [[trading-sync-2026-04-06]] — previous sync
- [[antonella-trading-program-status]] — current work plan
- [[antonella-three-setups-framework]] — core framework
- [[antonella-kiet-setup1-changes]] — Kiet's Setup 1 implementation
- [[antonella-powerbi-direct-access]] — Sebastian's Power BI integration path
- [[public-to-private-opportunities]] — Liberty P2P pipeline (trading-derived)
- [[liberty-cf-deal-pipeline]] — Liberty CF prospects including ASX P2P targets
- [[bill-maiden-generational-wealth-plan]] — Wealth Engine 3 context

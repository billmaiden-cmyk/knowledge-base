---
title: "Trading Sync — 2026-04-06"
created: 2026-04-06
updated: 2026-04-06
tags: [trading, sync, antonella, position-synthesis]
sources:
  - wiki/synthesis/comms-whatsapp-antonella-2025-04-to-2026-04.md
  - wiki/concepts/antonella-trading-program-status.md
  - wiki/concepts/antonella-three-setups-framework.md
  - wiki/concepts/antonella-action-priorities.md
  - wiki/concepts/antonella-bridging-note-v2-to-three-setups.md
  - wiki/concepts/antonella-autoresearch-system.md
  - wiki/concepts/antonella-constructive-base-detector-spec.md
  - wiki/concepts/antonella-trading-framework-overview.md
  - wiki/synthesis/bill-maiden-generational-wealth-plan.md
  - wiki/concepts/ai-trading-system.md
  - Gmail (antonella, Mar 2026)
---

## Executive Summary

This is the first trading sync. The Antonella/Bill quantitative trading program has a fully designed methodology (Three Setups Framework + autoresearch engine) but is **blocked on infrastructure**. The critical path item is Kiet delivering VMA and base number columns to the database — nothing else can progress until that's done, and there's no confirmation it has started. The Sebastian-Kiet data walkthrough (required for autoresearch) hasn't happened. Meanwhile, Antonella and Bill have an unresolved alignment tension: Bill wants to lock down the framework and start testing; Antonella keeps refining components (sell rules, KAMA, constructive base improvements). A Tuesday alignment meeting was identified as critical but it's unclear whether it occurred. Five decisions need Bill's attention, most urgently the Sebastian-Kiet blocker and the VMA vs KAMA question.

## Antonella's Current Position

### Framework & Approach
Antonella has bought into the Three Setups Framework (Fresh Breakout / Continuation Base / Short Squeeze) but is doing deep component-level analysis to understand how constructive base elements apply differently to each setup. She had a significant "aha moment" about VMA power in late March: *"Sorry to bombard you yesterday, didn't realise how powerful VMA was."* Her intellectual foundation — the two-model insight (Early Cover Turn vs True Constructive Base) and the si_dry_interaction concept — is the core of what became the Three Setups Framework.

### Recent Changes
- **Sell rules urgency** (1 Apr): Identified premature selling as a major alpha leak. Clover (CLV) example: system said sell, stock continued +21%. Proposed O'Neil-style rules: flag first close below SMA10, sell only if next day undercuts that day's low. This is new — not in any prior framework document
- **Constructive base improvements** (25 Mar – 2 Apr): Proposed trend filter (SMA50 > SMA200), right-side score, distribution penalty, KAMA regime filter. Tested against Appen, COH, DMP. Gating proposal: constructive >= 0.5, then require 2 of 3: ATR < 0.85, vol dryup < 0.5, MA coherence > 0.8
- **Broker ramp-and-raise pattern** (27 Mar – 2 Apr): Identified as potentially distinct strategy — brokers ramp stocks → capital raise → institutional shorts hedge at placement price → retail squeezed. 4DX example cited
- **Shared documents** (25 Mar via Gmail): "Ants documentation" (Google Doc), "Stocks Dashboard with short" (Google Sheet), "Working paper data" (Google Sheet) — all shared with Bill for editing

### Concerns & Objections
- Data infrastructure not ready for autoresearch v1 — keeps identifying additional metrics needed (short interest, base labels, index rebalance dates, KAMA, RS)
- Sell rules must be programmed now, not deferred — *"Both buy and sell must be programmed"*
- Wants KAMA explored as alternative/complement to VMA
- Sebastian-Kiet handoff hasn't happened

### Requests to Kiet
- Implement VMA and/or KAMA in database
- Scrape ASIC short position reports into SQL
- Add index entry/exit calculations, short risk score, relative strength, index rebalance date flags, base labelling
- Constructive base improvements (pending spec finalisation)
- Sell signal implementation (Bill wants to defer)

## Bill's Current Position

### Documented Design Principles
- **Three Setups as common language**: Bill authored the Three Setups Framework, VMA Design Paper, Bridging Note v2→Three Setups, and Three Setups x KAMA Regime discussion document. His core position: *"I feel like we are going a bit in circles here and would like to know that we are aligned in approach. In the absence of common language, I feel we are not aligned."*
- **Stop debating, start testing**: Let autoresearch resolve parameter debates with data. Ship v1 as-is, test proposed improvements empirically
- **VMA as core signal**: VMA breakout/breakdown is the primary mechanism; being tested alongside SMA, not replacing it
- **Rules-based discipline**: *"We need to remove 'I am smarter than the rules' ideas"* — lesson from WTC position and earlier drawdowns

### Recent Communications
- Sent "Nothing leading" email to Antonella (25 Mar) — appears to be market/signal commentary
- Identified alignment meeting for Tuesday as critical next step
- Messaged Kiet to expect Sebastian's outreach for data walkthrough
- Frustrated that Antonella hasn't fully engaged with Three Setups x KAMA document

### Wealth Plan Alignment
The trading program is **Wealth Engine 3** in the $53m/5yr generational wealth plan. Target: compound all surplus cash at 18% net. Starting capital: $2.5m cash ready to deploy *(Bill, WhatsApp, Feb 2026)*. The wealth plan specifies a "written investment policy with hard position limits, correlation controls, and drawdown triggers" — the Three Setups Framework + autoresearch system is the mechanism to deliver this. The program is behind the earlier AI-Driven Trading System timeline (Dec 2025 "full launch" target lapsed) but the current Antonella framework is a more rigorous, data-driven approach than the original copy-trading/multi-agent design. **On track conceptually; behind on execution.**

## Divergence Map

| # | Topic | Antonella's View | Bill's View | Impact | Resolution Path |
|---|-------|-----------------|-------------|--------|----------------|
| 1 | **VMA vs KAMA** | Exploring KAMA as alternative/complement to VMA; wants both tested | VMA is the core signal; wrote Three Setups x KAMA discussion doc but frustrated Antonella hasn't responded to it | Medium — delays query specification if regime filter isn't agreed | Resolve at alignment meeting. Pragmatic answer: include both in database, let autoresearch decide. Bill's discussion doc is the agenda anchor |
| 2 | **Sell rules timing** | Critical now — Clover shows material alpha leakage from premature exits. Both buy AND sell must be programmed | Wants to park selling; focus on entry signals first | High — if sell rules genuinely leak 20%+ alpha (Clover example), deferral has real cost. But adding sell logic before entry logic is validated creates scope creep | Compromise: document sell rules for autoresearch testing (Priority 4), but don't block Priority 1-3 execution. Autoresearch can test exit strategies alongside entry strategies |
| 3 | **Infrastructure readiness** | Need more data columns in DB before testing — keeps adding requirements (ASIC shorts, RS, index rebalance dates, KAMA) | Start testing now with what exists. Get autoresearch running against three setups | High — scope creep on DB columns delays everything. Each new request to Kiet extends the critical path | Agree on a hard "v1 column set" at the Tuesday meeting. Everything else goes to a "v2 backlog". The Action Priorities doc already defines this — enforce it |
| 4 | **Communication style** | High-volume, stream-of-consciousness analytical exploration (60% of 8,000+ messages) | Structured, document-driven, setup-by-setup discussion | Medium — creates Bill's "going in circles" feeling. Antonella's process is exploratory; Bill needs convergence | Tuesday meeting with Three Setups doc as agenda anchor. After meeting: Antonella's refinements should be written as numbered proposals against specific setups, not open-ended threads |
| 5 | **Ramp-and-raise pattern** | Sees as distinct strategy worth formalising (potentially a 4th setup) | Hasn't categorised it yet | Low — doesn't block current execution | Defer. Can be tested as a Setup 3 variant in autoresearch after v1 is running |

## Kiet Dependency Tracker

| # | Item | Requested By | Date Requested | Status | Blocker |
|---|------|-------------|----------------|--------|---------|
| 1 | Forward returns (5d/15d/30d/60d/90d/max90d) | Both | ~Mar 2026 | ✅ Done | — |
| 2 | VMA values (vma_9, vma_18, vma_27, dist_vma9, vma9_direction) | Bill | Mar 2026 | ⏳ In progress (unconfirmed) | **CRITICAL PATH** — blocks VMA queries and autoresearch |
| 3 | Base number (1, 2, 3, 4+) | Both | Mar 2026 | ⏳ Pending | Blocks Setup 2 position sizing |
| 4 | ASIC short position scraping | Antonella | Mar 2026 | Not started | — |
| 5 | Index entry/exit calculations | Both | Apr 2026 | Not started | — |
| 6 | Relative strength metric | Both | Apr 2026 | Not started | — |
| 7 | Index rebalance date flags | Antonella | Apr 2026 | Not started | — |
| 8 | KAMA implementation | Antonella | Mar 2026 | Not started | Pending VMA vs KAMA decision |
| 9 | Sebastian SQL walkthrough | Antonella/Sebastian | 1 Apr 2026 | **BLOCKER** — meeting not confirmed | Blocks autoresearch setup entirely |
| 10 | Power BI queries (12 total) | Both | Defined in Action Priorities | Not started | Blocked by items 2 & 3 |

## Decisions Needed

### Decision 1: Confirm Sebastian-Kiet Connection
**Context:** Sebastian drafted a comprehensive 14-point data walkthrough request for Kiet (SQL schema, lineage, grain, keys, update frequency, dbt structure). Bill messaged Kiet to expect the outreach. No confirmation this meeting has occurred.
**Options:** (a) Follow up with both today to confirm, (b) Check if Sebastian sent the WhatsApp message
**Information Gap:** Has Sebastian actually contacted Kiet? Has a meeting been scheduled?
**Deadline:** Immediate — this blocks the entire autoresearch pipeline (Priority 4)
**Recommendation:** Follow up today. This is 5 days overdue from when it was first flagged (1 Apr).

### Decision 2: VMA vs KAMA as Regime Filter
**Context:** Bill advocates VMA; Antonella exploring KAMA. Bill wrote a Three Setups x KAMA Regime discussion document that Antonella hasn't responded to.
**Options:** (a) VMA only, (b) KAMA only, (c) Both — let autoresearch decide empirically
**Information Gap:** Antonella's specific technical objections to VMA vs KAMA preferences
**Deadline:** At alignment meeting (this week)
**Recommendation:** Option (c) — implement both in DB, run both versions of each query. Autoresearch will resolve this with data. Don't let a theoretical debate delay execution.

### Decision 3: Sell Rules — Now or Defer?
**Context:** Antonella identified premature selling as a major alpha leak (CLV: +21% left on table). Bill wants to park selling and focus on entry signals.
**Options:** (a) Defer entirely to Phase 2, (b) Document sell rules now but test only in autoresearch (don't add to Priority 1-3), (c) Add sell signal columns to Kiet's Priority 1 work
**Information Gap:** How many other examples besides CLV? Is this systematic or anecdotal?
**Deadline:** At alignment meeting
**Recommendation:** Option (b). Antonella should write the sell rule spec as a document (like the constructive base spec). It enters the autoresearch testing pipeline at Priority 4 without expanding the critical path.

### Decision 4: WTC Position — Exit or Hold?
**Context:** Both chased WiseTech instead of following data. Stock kept declining. Antonella: *"That's the problem, we need to remove 'I am smarter than the rules' ideas."*
**Options:** Exit on next bounce, hold to support level, or set a hard stop
**Information Gap:** Current WTC price vs entry, current technical setup
**Deadline:** This week — emotional weight of holding a losing position undermines the rules-based approach they're building
**Recommendation:** Set a rule-based stop. This is a litmus test for the framework: if Bill can't follow rules on WTC, the system won't be credible.

### Decision 5: Column Scope for Kiet v1
**Context:** Antonella keeps adding DB column requests (ASIC shorts, RS, index rebalance, KAMA). Each addition extends Kiet's timeline.
**Options:** (a) Lock to Action Priorities v1 scope (forward returns ✅, VMA, base number — that's it), (b) Add Antonella's new requests to v1
**Information Gap:** Kiet's actual capacity and timeline
**Deadline:** Immediate
**Recommendation:** Option (a). The Action Priorities doc already defines the scope. Everything else is v2. Adding columns now is the single biggest risk to ever getting autoresearch running.

## Action Items

| # | Owner | Action | Priority | Due | Source |
|---|-------|--------|----------|-----|--------|
| 1 | Bill | Follow up with Sebastian AND Kiet — confirm data walkthrough meeting is scheduled | CRITICAL | Today (6 Apr) | WhatsApp Thread 23 |
| 2 | Bill | Schedule/confirm Tuesday alignment meeting with Antonella | HIGH | Today (6 Apr) | WhatsApp Thread 25 |
| 3 | Bill | At meeting: resolve VMA vs KAMA (recommend: both, let autoresearch decide) | HIGH | At meeting | WhatsApp Thread 18 |
| 4 | Bill | At meeting: agree on hard v1 column scope for Kiet (recommend: lock to Action Priorities) | HIGH | At meeting | Action Priorities doc |
| 5 | Bill | At meeting: address sell rules (recommend: Antonella writes spec, enters autoresearch at P4) | HIGH | At meeting | WhatsApp Thread 21 |
| 6 | Bill | Set rule-based stop on WTC position | MEDIUM | This week | WhatsApp Thread 17 |
| 7 | Bill | Review Antonella's improved constructive base doc + 3 Google Drive documents shared 25 Mar | MEDIUM | Before meeting | Gmail 25 Mar |
| 8 | Bill | Monitor PNV for VMA breakout confirmation | LOW | Ongoing | WhatsApp Thread 22 |
| 9 | Antonella | Read and respond to Three Setups x KAMA Regime discussion document | HIGH | Before meeting | WhatsApp Thread 25 |
| 10 | Antonella | Write sell rule spec as a formal document (like constructive base spec) | MEDIUM | This week | WhatsApp Thread 21 |
| 11 | Kiet | Complete VMA columns (vma_9/18/27, dist_vma9, vma9_direction) | CRITICAL | This week | Action Priorities P1b |
| 12 | Kiet | Complete base_number column | HIGH | This week | Action Priorities P1c |
| 13 | Sebastian | Send data walkthrough request to Kiet and schedule meeting | CRITICAL | ASAP | WhatsApp Thread 23 |

## Communication Health

**Message Volume (last 7 days):** WhatsApp digest covers through 2 Apr 2026 — very high volume in the final 2 weeks (Threads 18-25 all active). No new WhatsApp digest since then. No Gmail from Antonella in last 11 days (last: 25 Mar Google Drive shares).
**Response Lag:** Bill's Three Setups x KAMA Regime discussion document — Antonella hasn't responded. This is the single most important alignment document.
**Tone:** Collaborative overall but tension building. Bill expressed frustration directly: *"I feel like we are going a bit in circles."* Antonella acknowledged the setups are fine but continues exploring components. The friction is structural (exploratory vs convergent communication styles), not personal.
**Recommendation:** The Tuesday alignment meeting is the single highest-leverage action. Bill should use the Three Setups document as the literal agenda — walk through each setup, get explicit yes/no on each element, and leave with a locked v1 scope for Kiet. After the meeting, shift WhatsApp to numbered proposals against specific setups rather than open-ended analytical threads.

## Notes for Next Sync

- This is the first trading sync — no prior sync to reference
- The AI-Driven Trading System page (multi-strategy hedge fund, Dec 2025 launch target) is **stale** and represents a different, earlier approach. The Antonella framework has effectively superseded it as Wealth Engine 3's execution mechanism
- No `wiki/log.md` exists yet — creating one with this sync entry
- Three Google Drive documents shared by Antonella on 25 Mar (Ants documentation, Stocks Dashboard with short, Working paper data) have not been ingested into the wiki

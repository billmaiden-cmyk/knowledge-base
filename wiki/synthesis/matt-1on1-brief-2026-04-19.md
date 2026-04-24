---
title: "Matt Wrigley — 1:1 Brief: Ticket Portfolio & Billing Review (19 April 2026)"
created: 2026-04-19 19:00 AEST
updated: 2026-04-19 19:00 AEST
tags: [mts, matt-wrigley, 1on1-prep, ticket-hygiene, billing-review, zendesk, schedule-b]
sources:
  - raw/Matthew Open and Pending Tickets.csv
  - Matt Wrigley Schedule B billing 2026-03-20 to 2026-04-17
source_date: 2026-03-20 to 2026-04-19
---

# Matt Wrigley — 1:1 Brief
## Ticket Portfolio & Billing Review | 19 April 2026

## Headlines

1. **Portfolio size is misleading.** 107 tickets appear active; 64 are marked Open. The true actionable count is **33**. The gap is 31 tickets that should be Pending and 12 that should be closed.
2. **24-hour KPI is in systemic failure.** 28 of 28 new tickets in the queue have not been responded to within SLA. The oldest is **51 days** unanswered.
3. **Billing does not reflect ticket action.** Over 5 weeks of Schedule B, Matt has billed most of the buildings with neglected tickets — often on the same topic. This is a selection pattern, not a capacity issue.

---

## 1. Portfolio: today vs after cleanup

| Status | Today | After cleanup | Change |
|---|---|---|---|
| **Open** — Matt's real to-do | 64 | **33** | −31 |
| **Pending** — awaiting client | 43 | **50** | +7 |
| **Closed + filed to Box** | 0 | **12** | +12 |
| **Under review** (close candidates) | — | 2 | +2 |
| **Total active** | **107** | **95** | −12 |

The 31-ticket drop in "Open" isn't work disappearing. It's hygiene. The queue gets cleaner, the priority list becomes visible, and Matt's dashboard reflects reality.

---

## 2. Four cleanup rules

| Rule | Criteria | Tickets | Action |
|---|---|---|---|
| **1** | >30 days, no agent reply ever, client not re-engaged | 2 | Review, likely close |
| **2** | Matt was last to update | 30* | Open → Pending |
| **3** | Matt replied, client silent >4 weeks | 10 | Close + file to Box |
| **4** | No activity either side >3 months | 0 | Close (protective going forward) |

\* 40 tickets technically fit Rule 2; 10 of those also fit Rule 3 (close takes precedence).

---

## 3. 24-hour first-response KPI — systemic failure

**28 of 28 new tickets fail.** 100% breach.

| KPI breach | Count | Worst cases |
|---|---|---|
| **>30 days past SLA** | 3 | 121236 Benelong (51d); 121653 Pitt St Variation V01 (47d); **123829 Pitt St Fire Order (31d)** |
| **15–30 days past** | 3 | 124445 + 124587 Bennett St (25, 24d, likely duplicates); 125030 Taylor St (20d) |
| **8–14 days past** | 3 | 125255 NSW Planning Portal (18d); 125302 Taylor St Pilcher leak (18d); 125671 Project Guides invoice (13d) |
| **1–7 days past** | 19 | Various, including **126745 SP 58804** (4d) |

---

## 4. Aging — the 33 tickets that genuinely need response

### Aging profile

| Age band | Count | % |
|---|---|---|
| 31+ days | 1 | 3% |
| 22–30 days | 3 | 9% |
| 15–21 days | 3 | 9% |
| 8–14 days | 6 | 18% |
| 4–7 days | 7 | 21% |
| 1–3 days | 13 | 40% |

Median age: **5 days**. 13 tickets (39%) are more than one week overdue.

### The priority 13 — all past SLA by more than a week

| # | ID | Age | Building | Issue |
|---|---|---|---|---|
| 1 | **123829** | 31d | SP 87409 Pitt St | **Fire Order / Consultant Details** — compliance risk |
| 2 | 124445 | 25d | SP 67844 Bennett St | CAS-122356 |
| 3 | 124587 | 24d | SP 67844 Bennett St | CAS-122356 (likely duplicate of #2) |
| 4 | **121197** | 23d† | SP 101609 Bricklane | **Water leak Unit 602** — client waiting |
| 5 | 125030 | 20d | SP 71821 Taylor St | Quote #167 — Croydon Metal |
| 6 | 125255 | 18d | — | **NSW Planning Portal "awaiting your response"** |
| 7 | 125302 | 18d | SP 71821 Taylor St | Pilcher leak |
| 8 | 125671 | 13d | — | **Project Guides invoice overdue** |
| 9 | 118673 | 10d† | SP 76375 Rosebery | Community Fibre FTTP |
| 10 | 126300 | 9d | SP 98328 Ashfield | Waterproofing Levy |
| 11 | 126345 | 9d | DP 1290007 Sans Souci | **Legal — BMC Sole Residences** |
| 12 | 126343 | 9d | SP 100866 Bexley | Balcony tiles popped up |
| 13 | 126293 | 9d | SP 56120 Crows Nest | Follow-up |

† Bucket B — client has replied and is waiting on Matt.

---

## 5. Billing cross-check: does Schedule B reflect ticket action?

**Short answer: not at the level we'd expect.**

### Methodological note
The Zendesk export supplied for this analysis is **open + pending tickets only** (107 rows). Closed tickets are not visible. A portion of Matt's Schedule B billing may legitimately relate to tickets that have since been closed and so do not appear in this snapshot. That caveat is real.

However, two observations still hold despite the caveat:

1. The affected buildings have been actively worked in the last 5 weeks — Matt is in the files. That rules out "I couldn't get to it" as a blanket explanation for why tickets at those same buildings are unanswered for weeks.
2. The phrasing overlap is striking — billing lines reference the same building, often the same defect category, as the unanswered ticket. That's either (a) the billing is for the exact same matter and the ticket should be closed, in which case the Rule 2 / Rule 3 hygiene cleanup is overdue, or (b) the billing is adjacent work at the same building while the ticket sits separately, which is the selection pattern.

Either interpretation points to hygiene failure. A full reconciliation would require the closed-ticket export alongside Schedule B. That is worth pulling.

### The numbers
Over the 5 weeks from 20 March to 17 April 2026, Matt's Schedule B lists approximately **127 billable entries across ~35 buildings**. If the ticket backlog reflected a genuine capacity constraint, we'd expect the affected buildings to be absent from the billing record. They aren't. In most cases, Matt has billed heavily on the same buildings — often on the same topic — while the tickets sat unanswered.

### Pattern A — billed on the same topic, ticket ignored

| Building | Billed topic (5 weeks) | Unanswered ticket | Ticket age |
|---|---|---|---|
| **SP 101609 Bricklane** | Water ingress rooftop; Danrae Zoom; Bannermans defects/legal (5 weeks of billing) | 121197 — **Water leak Unit 602** | **23 days** |
| **SP 87409 Pitt St** | Fire Performance Solution; Council consultation (wk 17/4) | 123829 — **Fire Order / Consultant Details** | **31 days** |
| **SP 3081 Vaucluse** | Concrete spalling — BIM/NBM proposal review (wks 10/4, 17/4) | 124513 — Special levy concrete spalling | 2 days |
| **SP 58804 Huntleys Cove** | Remedial works; RHM review; SZS peer review (4 of 5 weeks) | **126745 — "Work proceeding at 3 MLD"** | 4 days |
| **SP 71821 Taylor St** | Shop B drainage; Buidtek tiling (wks 27/3, 17/4) | 125302 — Pilcher leak; 125030 — Roofing quote | 18, 20 days |
| **SP 100866 Bexley** | Defects; letter to builder; legal (4 of 5 weeks) | 126343 — Balcony tiles popped up | 9 days |
| **SP 98328 Ashfield** | GM waterproofing — Sicaro/EA Building/MK Fuller proposals (wk 17/4) | 126300, 126936 — Waterproofing Levy | 9, 3 days |

Matt billed on the exact topic of these ignored tickets. He was in the file. He chose not to answer the ticket.

### Pattern B — buildings ignored entirely (no billing, no ticket action)

| Building | Problem ticket(s) | Age | Billing entries in 5 weeks |
|---|---|---|---|
| SP 67844 Bennett St | 124445, 124587 (likely duplicates) | 25, 24d | **0** |
| SP 4412 Neutral Bay | 126848, 126910, 126927 (+ others in queue) | 4, 3, 3d | **0** |
| SP 78505 Hunters Hill | 126855, 127049 | 4, 2d | **0** |
| SP 76036 Coogee | 124079 (mould Bucket B) | 3d | **0** |
| DP 1290007 Sans Souci | 126345 (legal — BMC Sole Residences) | 9d | **0** |
| SP 56120 Crows Nest | 126293 | 9d | **0** |

These buildings have had no chargeable activity from Matt for 5 weeks. The tickets confirm they have also had no administrative attention.

### What this tells us

The data shows two distinct behaviours running in parallel:

1. **On buildings Matt is engaged with** — he is doing the complex, project-based, high-value work (defects, remedial, fire compliance, legal) and billing it. He is not overloaded: he is touching these files regularly. But he is not responding to routine tickets at the same buildings, even on the same topics.
2. **On buildings Matt is not engaged with** — there is neither billing nor ticket response. These clients are getting no service.

**The ticket backlog is not a by-product of heavy billing. It is the work Matt is choosing not to do.**

---

## 6. What must happen before next week's 1:1

### Hygiene cleanup (≤ 1 hour of Matt's time)
1. Apply **Rule 2** — move 30 mislabelled Open tickets to Pending.
2. Apply **Rule 3** — close + file to Box: 111515, 112380, 92716, 115324, 81074, 120685, 118994, 107511, 122456, 96753.
3. Apply **Rule 1** review — 121236 (Benelong), 121653 (Pitt St V01): close unless active reason not to.
4. Merge duplicates: 124445/124587 (Bennett St); review 126300/126936 (Ashfield) and 121653/126646 (Pitt St).

### Priority responses this week (oldest-first, SLA-breach order)
- **Today:** 123829 (fire order, compliance); 121197 (water leak, 23 days client waiting).
- **By Wednesday:** the remaining priority 13 (see table above).
- **By Friday:** everything over 7 days past the 24-hour KPI — zero.

### Reporting
- Section 3 of weekly 1:1 is a conversation, not a scoreboard — Matt reports where he's stuck, what's been escalated, what's cleared.
- VN ops triage partner begins: AM + midday passes to surface genuine escalations to Matt. **No daily metrics reporting to Bill** — the support is for Matt's benefit.
- **Pull closed-ticket export** alongside next week's open/pending snapshot to complete the billing reconciliation.

---

## 7. 1:1 discussion agenda (Monday)

1. **Billing recognition** — $6,300 this week, equal best. What worked? What do we replicate?
2. **Ticket data** — share this brief; ask Matt's view before naming conclusions.
3. **The selection pattern** — billing on project work at SP 101609 while the unit 602 water leak sat 23 days. Ask Matt to speak to it.
4. **Cleanup plan** — agree the 4 rules and the deadlines above.
5. **VN ops triage partner** — framed as Matt's support (not Bill's scoreboard). Role is escalation guidance + hygiene, not reporting.
6. **1:1 Section 3 going forward** — light-touch conversation about queue health, escalations, anything stuck. Not a metrics dashboard.

---

## Related pages

- [[Matt Wrigley]] — role, targets, updated 1:1 template with 8-metric dashboard
- [[Matt Wrigley — Ticket Portfolio Analysis (19 April 2026)]] — underlying data and full bucket classifications
- [[Matt Wrigley — Ticket Hygiene Support Plan (VN Ops, 2026-04-19)]] — proposed support structure

---

*Brief prepared 19 April 2026 for Matt's weekly 1:1. Cross-references Zendesk CSV snapshot with Schedule B billing lines 20 March – 17 April 2026.*

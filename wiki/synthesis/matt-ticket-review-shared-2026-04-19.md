---
title: "Matt Wrigley — Ticket Portfolio Review (Shared Version, 19 April 2026)"
created: 2026-04-19 19:30 AEST
updated: 2026-04-19 19:30 AEST
tags: [mts, matt-wrigley, 1on1, ticket-hygiene, review, shared]
sources:
  - raw/Matthew Open and Pending Tickets.csv
  - Matt Wrigley Schedule B billing 2026-03-20 to 2026-04-17
source_date: 2026-03-20 to 2026-04-19
---

# Ticket Portfolio Review
## Matt Wrigley's Queue | 19 April 2026

## Purpose

This document pulls together a snapshot of the current Zendesk queue, an aging profile, a proposed set of hygiene changes, and a cross-reference with the last five weeks of Schedule B billing. It's a starting point for a shared conversation — what's working, what's drifting, and what support would help going forward.

## Note on the data

The Zendesk export used for this review is **open + pending tickets only** (107 tickets as at 19/04/2026). Closed tickets are not included in this snapshot, so some observations below may have legitimate context not visible in the data. That caveat applies throughout.

---

## 1. Queue snapshot — today

| Status | Count |
|---|---|
| Open | 64 |
| Pending | 43 |
| **Total active** | **107** |

The size of the queue and the Open/Pending split are the starting point for the discussion.

---

## 2. Proposed hygiene rules

Four proposed rules to apply to the existing queue. These are standard Zendesk hygiene — open for discussion and refinement:

| Rule | Criteria | Action |
|---|---|---|
| 1 | Age >30 days, no agent reply recorded, client has not re-engaged | Review for close |
| 2 | Agent was the last to update the ticket | Change Open → Pending |
| 3 | Agent replied, client has been silent more than 4 weeks | Close and file to Box |
| 4 | No activity from either side for 3+ months | Close |

---

## 3. Queue after applying the rules

| Status | Today | After cleanup | Change |
|---|---|---|---|
| Open (needs agent response) | 64 | **33** | −31 |
| Pending (awaiting client) | 43 | **50** | +7 |
| Closed + filed to Box | 0 | **12** | +12 |
| Under review | — | 2 | +2 |
| **Total active** | **107** | **95** | −12 |

The most meaningful change isn't the reduction in total — it's the reduction in Open from 64 to 33. The current Open count includes 31 tickets where the agent was the last to update, which makes it harder to see the items that genuinely need attention.

### What closes under Rule 3

Ten tickets where the agent responded, the client has been silent for more than four weeks, and no open compliance issue is apparent:

| ID | Building | Matt's last reply | Client last active |
|---|---|---|---|
| 111515 | SP 44665 Canterbury — AGM action | 79 days ago | 144 days ago |
| 112380 | SP 71821 Annandale — Roofing | 52 days ago | 72 days ago |
| 92716 | SP 10990 Annandale — Water leak | 46 days ago | 321 days ago |
| 115324 | SP 70132 Marrickville — Plumbing | 44 days ago | 45 days ago |
| 81074 | DP 1262550 Bricklane — Repair contacts | 39 days ago | 332 days ago |
| 120685 | SP 30537 Bankstown — GM/levy | 39 days ago | 54 days ago |
| 118994 | SP 56120 Crows Nest — OC audit | 37 days ago | 68 days ago |
| 96753 | SP 33333 Camden — Retaining wall | 27 days ago | 292 days ago |
| 107511 | SP 62840 Castle Hill — Tender meeting | 25 days ago | 88 days ago |
| 122456 | SP 76375 Rosebery — 1/1 Primrose | 25 days ago | 25 days ago |

---

## 4. 24-hour first-response SLA

Of the 107 tickets in the queue, 28 have no agent response recorded in Zendesk. The 24-hour first-response SLA has been missed on all 28. How far past the SLA:

| Age of breach | Count |
|---|---|
| >30 days past | 3 |
| 15–30 days past | 3 |
| 8–14 days past | 3 |
| 1–7 days past | 19 |

The three oldest without a response: 121236 Benelong (51 days); 121653 SP 87409 Pitt St Variation V01 (47 days); 123829 SP 87409 Pitt St Fire Order (31 days, client came back 2 days ago).

---

## 5. Aging of tickets that need a response

After applying the cleanup rules, 33 tickets would remain in Open status and genuinely need Matt's response. Their age profile:

| Age band | Count | % |
|---|---|---|
| 31+ days | 1 | 3% |
| 22–30 days | 3 | 9% |
| 15–21 days | 3 | 9% |
| 8–14 days | 6 | 18% |
| 4–7 days | 7 | 21% |
| 1–3 days | 13 | 40% |

Median age 5 days. 13 of the 33 (39%) are more than a week past SLA.

### The 13 tickets more than one week past SLA

| # | ID | Age | Building | Subject |
|---|---|---|---|---|
| 1 | 123829 | 31d | SP 87409 Pitt St | Fire Order / Consultant Details (client re-engaged 2 days ago) |
| 2 | 124445 | 25d | SP 67844 Bennett St | CAS-122356 |
| 3 | 124587 | 24d | SP 67844 Bennett St | CAS-122356 (likely duplicate of #2) |
| 4 | 121197 | 23d* | SP 101609 Bricklane | Water leak Unit 602 |
| 5 | 125030 | 20d | SP 71821 Taylor St | Quote #167 |
| 6 | 125255 | 18d | — | NSW Planning Portal — "awaiting your response" |
| 7 | 125302 | 18d | SP 71821 Taylor St | Pilcher leak |
| 8 | 125671 | 13d | — | Project Guides invoice overdue |
| 9 | 118673 | 10d* | SP 76375 Rosebery | Community Fibre FTTP |
| 10 | 126300 | 9d | SP 98328 Ashfield | Waterproofing Levy |
| 11 | 126345 | 9d | DP 1290007 Sans Souci | Legal — BMC Sole Residences |
| 12 | 126343 | 9d | SP 100866 Bexley | Balcony tiles popped up |
| 13 | 126293 | 9d | SP 56120 Crows Nest | Follow-up |

\* Client has replied and is waiting for a response.

---

## 6. Cross-reference with Schedule B billing

Over the 5 weeks from 20 March to 17 April 2026, Schedule B shows ~127 billable entries across ~35 buildings — a strong billing pattern. The cross-reference is not to question billing volume, but to understand the relationship between where billable work is happening and where tickets are sitting.

### Important caveat
Because we can only see open + pending tickets in this export, some of the billing below may relate to tickets that have been resolved and closed. A fuller reconciliation would pull the closed-ticket export alongside Schedule B and match them.

### Observations

**Several buildings show both active billing and unanswered tickets on the same topic.** That could mean (a) the billing has effectively resolved the matter and the ticket is sitting unclosed (Rules 2 and 3 would catch this), or (b) the billing is for related but distinct work at the same building. Either way, it's worth working through together:

| Building | Schedule B billing (5 weeks) | Open ticket |
|---|---|---|
| SP 101609 Bricklane | Water ingress rooftop; Danrae Zoom; Bannermans (active each week) | 121197 — Water leak Unit 602 (23 days) |
| SP 87409 Pitt St | Fire Performance Solution; Council consultation (wk 17/4) | 123829 — Fire Order / Consultant Details (31 days) |
| SP 3081 Vaucluse | Concrete spalling proposals (wks 10/4, 17/4) | 124513 — Concrete spalling levy (2 days) |
| SP 58804 Huntleys Cove | Remedial; RHM; SZS peer review (4 weeks) | 126745 — Work proceeding at 3 MLD (4 days) |
| SP 71821 Taylor St | Shop B drainage; Buidtek tiling (wks 27/3, 17/4) | 125030, 125302 (20, 18 days) |
| SP 100866 Bexley | Defects; letter to builder; legal (4 weeks) | 126343 — Balcony tiles (9 days) |
| SP 98328 Ashfield | GM waterproofing proposals (wk 17/4) | 126300, 126936 — Waterproofing Levy (9, 3 days) |

**A smaller group of buildings shows neither billing nor ticket activity over the last five weeks.** Worth talking through whether these are low-activity clients or whether they need attention:

| Building | Open ticket(s) | Age | Schedule B entries (5 weeks) |
|---|---|---|---|
| SP 67844 Bennett St | 124445, 124587 | 25, 24d | 0 |
| SP 4412 Neutral Bay | 126848, 126910, 126927 | 4, 3, 3d | 0 |
| SP 78505 Hunters Hill | 126855, 127049 | 4, 2d | 0 |
| SP 76036 Coogee | 124079 | 3d | 0 |
| DP 1290007 Sans Souci | 126345 | 9d | 0 |
| SP 56120 Crows Nest | 126293 | 9d | 0 |

### Question for the discussion
The Schedule B pattern shows strong engagement with most of the buildings that have open tickets. So if capacity isn't the issue, what is making the ticket hygiene hard — and what would help?

---

## 7. Proposed support structure — VN ops triage partner

A suggestion to help Matt stay on top of the queue without taking specialist work off him. The role is focused on **helping Matt identify what genuinely needs to be escalated or responded to urgently**, so his time goes to the right tickets.

- **Daily triage partner** from the VN ops team — roughly an hour a day, split between a morning and midday pass.
- **Primary job: escalation guidance.** Scan the queue and surface to Matt the items that genuinely need urgent attention — compliance risks (fire orders, safety), tickets approaching or past SLA breach, clients who've re-engaged after a long silence, and items that are starting to drift.
- **Hygiene support.** Status changes (Open → Pending once Matt has replied), filing closed tickets to Box, flagging likely duplicates for merge, surfacing stale items for Matt's close/chase decision.
- **Out of scope.** Substantive replies to clients — Matt remains the expert. No closing of tickets without Matt's sign-off (except clear admin duplicates).
- **Start with cleanup.** Week 1 is applying the four hygiene rules above — resets the queue and builds familiarity with Matt's portfolio.
- **Review rhythm.** 15-min weekly call between Matt and the VN ops person to refine what counts as an escalation and iterate on first-reply templates.

The intent is practical: Matt gets a second set of eyes that helps him prioritise, without adding an administrative overlay or a reporting burden.

---

## 8. Suggested next steps

1. **Agree the four hygiene rules** (or refine them).
2. **Apply Rules 2 and 3** this week — roughly 1 hour of work, brings the queue from 107 to 95 and the Open count from 64 to 33.
3. **Prioritise the 13 tickets past SLA by more than a week**, starting with the fire order and the Bricklane water leak.
4. **Pull the closed-ticket export** to complete the Schedule B reconciliation.
5. **Stand up the VN ops triage partner** — begin week commencing 20 April if possible.

---

*Prepared 19 April 2026 for discussion with Matt Wrigley. Cross-references Zendesk open/pending CSV snapshot with Schedule B billing lines 20 March – 17 April 2026.*

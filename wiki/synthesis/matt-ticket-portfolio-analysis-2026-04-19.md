---
title: Matt Wrigley — Ticket Portfolio Analysis (19 April 2026)
created: 2026-04-19 14:00 AEST
updated: 2026-04-19 14:00 AEST
tags: [mts, matt-wrigley, ticket-hygiene, zendesk, analysis, 1on1-prep]
sources:
  - raw/Matthew Open and Pending Tickets.csv
source_date: 2026-04-19
---

# Matt Wrigley — Ticket Portfolio Analysis (19 April 2026)

A fact-based classification of every open or pending Zendesk ticket currently assigned to Matt, as at 19 April 2026. Each ticket is placed into one of five buckets based on three measures: **age** (days since ticket raised), **time awaiting an agent response** (days since requester's most recent update, where agent has not since responded), and **status correctness** (whether the "Open" label matches who owes the next action).

## Methodology

- **Source:** Zendesk export "Matthew Open and Pending Tickets.csv" (107 rows, pulled 19/04/2026)
- **Bucket assignment:** Each ticket is placed in its single most relevant bucket. Buckets are listed in order of responsiveness concern.
- **Definitions:**
  - *"Client waiting"* = Requester's last update is more recent than the Assignee's (Matt's) last update, OR the Assignee has never updated
  - *"Status mismatch"* = ticket is marked "Open" but the Assignee was the last to update — convention suggests this should be "Pending" (awaiting requester)
  - *"Stale"* = no activity from either side for more than 30 days
- **Portfolio size:** 107 tickets (64 Open, 43 Pending)

## Bucket A — No agent response recorded (Assignee updated field blank)

28 tickets. The requester has raised or last updated the matter, and no agent response is logged. Sorted by oldest (longest unanswered) first.

| ID | Days unanswered | Building | Subject |
|---|---|---|---|
| 121236 | 51 | SP 55007 (Benelong St, Seaforth) | Attention Mathew for repairs Benelong St |
| 121653 | 47 | SP 87409 (5 Pitt St, Parramatta) | Builders scope — Variation V01 |
| 123829 | 31 | SP 87409 (5 Pitt St, Parramatta) | Fire Order / Consultant Details |
| 124445 | 25 | SP 67844 (1 Bennett St, Bondi) | 1-3 Bennett Street — CAS-122356-C4X1C4 |
| 124587 | 24 | SP 67844 (1 Bennett St, Bondi) | 1-3 Bennett Street — CAS-122356-C4X1C4 (same building as 124445) |
| 125030 | 20 | SP 71821 (34 Taylor St, Annandale) | Quote #167 — Croydon Metal Roofing |
| 125255 | 18 | — | NSW Planning Portal Customer Service Enquiry — "Awaiting your response" |
| 125302 | 18 | SP 71821 (34 Taylor St, Annandale) | FW: Taylor Street — Pilcher leak |
| 125671 | 13 | — | Bill INV-3475 from Project Guides — 7 days overdue |
| 126300 | 9 | SP 98328 (William St, Ashfield) | Waterproofing Levy |
| 126345 | 9 | DP 1290007 (Sans Souci) | Legal — BMC Sole Residences v SP 108621 |
| 126343 | 9 | SP 100866 (1 Harrow Rd, Bexley) | Tiles near balcony popped up |
| 126293 | 9 | SP 56120 (250 Pacific Hwy, Crows Nest) | Follow-up |
| 126481 | 6 | SP 102232 (Calabria Lane, Prairiewood) | Apt 606C leakage |
| 126432 | 6 | SP 87830 (Rookwood Rd, Yagoona) | Service request |
| 126646 | 5 | SP 87409 (5 Pitt St, Parramatta) | Builders scope — Variation V01 |
| 126855 | 4 | SP 78505 (5 St Malo Ave, Hunters Hill) | Unit 1 Bedroom 3 Variation cost |
| 126848 | 4 | SP 4412 (10 Raymond Rd, Neutral Bay) | RCTI Invoice for Application SoAR-00697 |
| 126745 | 4 | SP 58804 (Mortimer Lewis Dr, Huntleys Cove) | Work is currently proceeding at 3 MLD |
| 126910 | 3 | SP 4412 (10 Raymond Rd, Neutral Bay) | Panel layout — 10 Raymond Rd |
| 126936 | 3 | SP 98328 (William St, Ashfield) | Waterproofing |
| 126927 | 3 | SP 4412 (10 Raymond Rd, Neutral Bay) | Electrician Ed Hartson's site visit |
| 126929 | 3 | SP 62840 (Parsonage Rd, Castle Hill) | Lot 15 |
| 126902 | 3 | Not Applicable | Shared expenses article |
| 127090 | 2 | SP 101609 (Bricklane Residential) | Richard — missed call from +61 411 697 679 |
| 127064 | 2 | SP 22531 (225 Wardell Rd, Dulwich Hill) | Fwd: BCNSW CCEW submitted |
| 127068 | 2 | SP 100575 (1 Balmoral Cres, Waitara) | Proposed engagement of AED |
| 127049 | 2 | SP 78505 (5 St Malo Ave, Hunters Hill) | Variation 121 — signed acceptance |

## Bucket B — Agent previously engaged, requester has since replied

7 tickets. Matt has responded in the past, then the requester has come back, and Matt has not yet responded. Sorted by duration Matt has been silent since the requester's last update.

| ID | Matt silent for | Age | Building | Subject |
|---|---|---|---|---|
| 121197 | 23 days | 51 | SP 101609 (Bricklane) | Water leak unit 602 living room |
| 118673 | 10 days | 72 | SP 76375 (Primrose Ave, Rosebery) | Community Fibre FTTP Proposal |
| 125216 | 6 days | 19 | SP 62840 (Parsonage Rd, Castle Hill) | Lot 15 |
| 124079 | 3 days | 30 | SP 76036 (Carrington Rd, Coogee) | Mould from water leak — Unit 1 |
| 124513 | 2 days | 25 | SP 3081 (Girilang Ave, Vaucluse) | Special levy for concrete spalling |
| 126786 | 2 days | 4 | SP 92989 (Double Bay) | Floor repair contact — Unit 402 |
| 126470 | 1 day | 6 | SP 4743 (Crows Nest Rd, Waverton) | Final Notice — Formal records request |

## Bucket C — Status label mismatch (Open, but agent was last to update)

40 tickets are marked "Open" but Matt was the most recent updater. Under standard Zendesk convention these would be classified "Pending" while awaiting the requester. Sorted by duration since Matt's last update — longest first.

### C1. Matt responded more than 30 days ago (10 tickets)

| ID | Matt's last reply | Age | Building |
|---|---|---|---|
| 111515 | 79 days ago | 144 | SP 44665 (Canterbury Rd) — AGM Action Item |
| 112380 | 52 days ago | 137 | SP 71821 (Taylor St, Annandale) — Roofing |
| 92716 | 46 days ago | 331 | SP 10990 (Johnston St, Annandale) — Water leak / roofing |
| 115324 | 44 days ago | 102 | SP 70132 (George St, Marrickville) — Stage 2 Plumbing |
| 81074 | 39 days ago | 431 | DP 1262550 (Bricklane BMC) — Contacts for Repairs |
| 120685 | 39 days ago | 54 | SP 30537 (Conway Rd, Bankstown) — URGENT — GM and Special Levy |
| 118994 | 37 days ago | 68 | SP 56120 (Pacific Hwy, Crows Nest) — OC Audit |
| 96753 | 27 days ago | 292 | SP 33333 (Old Hume Hwy, Camden) — Retaining Wall |
| 122456 | 25 days ago | 41 | SP 76375 (Primrose Ave, Rosebery) — Re: 1/1 Primrose |
| 107511 | 25 days ago | 181 | SP 62840 (Parsonage Rd, Castle Hill) — Tender meeting |

### C2. Matt responded 10–30 days ago (11 tickets)

| ID | Matt's last reply | Age | Building |
|---|---|---|---|
| 94712 | 24 days ago | 311 | SP 35592 (Hutchinson St, Granville) — Balcony Engineer Report |
| 123843 | 24 days ago | 31 | SP 108247 (John St, Kogarah) — SBBIS Onboarding |
| 123875 | 20 days ago | 31 | SP 58804 (Mortimer Lewis Dr) — Tender Documentation |
| 119142 | 18 days ago | 68 | SP 5397 (Bay Rd, Russell Lea) — Onboarding FIRE |
| 125775 | 12 days ago | 12 | DP 270179 (Huntleys Cove CA) — Building Managers Report |
| 125711 | 12 days ago | 12 | SP 102232 (Calabria Lane) — NSD1468/2025 Federal Court |
| 125614 | 12 days ago | 16 | SP 102232 (Calabria Lane) — Car park lighting |
| 116725 | 11 days ago | 88 | SP 102232 (Calabria Lane) — Strata Plan 102232 |
| 120121 | 11 days ago | 60 | SP 98328 (William St, Ashfield) — Scope of services |
| 108529 | 10 days ago | 172 | SP 98328 (William St, Ashfield) — Urgent Fire Inspection |
| 125541 | 9 days ago | 17 | SP 76375 (Primrose Ave, Rosebery) — Letter of Intention |

### C3. Matt responded within last 10 days (19 tickets)

IDs: 125445, 107498, 123162, 115815, 99993, 125568, 116687, 122001, 116688, 126594, 124896, 126521, 115129, 127033, 108279, 104912, 127031, 110731, 127092. Details in source CSV.

## Bucket D — Stale (no activity from either side for more than 30 days)

Aggregated from Buckets A and C1 above. 10 tickets meet this criterion. These are tickets where both the requester and Matt have gone silent for more than a month.

| ID | Last activity | Source bucket |
|---|---|---|
| 111515 | 79 days ago (30 Jan) | C1 |
| 112380 | 52 days ago (26 Feb) | C1 |
| 121236 | 51 days ago (27 Feb, requester only, never responded) | A |
| 121653 | 47 days ago (3 Mar, requester only, never responded) | A |
| 92716 | 46 days ago (4 Mar) | C1 |
| 115324 | 44 days ago (6 Mar) | C1 |
| 120685 | 39 days ago (11 Mar) | C1 |
| 81074 | 39 days ago (11 Mar) | C1 |
| 118994 | 37 days ago (13 Mar) | C1 |
| 123829 | 31 days ago (client updated 17 Apr after 31-day silence) | A |

## Bucket E — Very old tickets with recent activity (>6 months, still live)

9 tickets were raised more than 6 months ago but have agent activity in the last 30 days — i.e. live, multi-month projects rather than neglect.

| ID | Age | Last agent update | Building | Subject |
|---|---|---|---|---|
| 62880 | 20 months | 2 days ago | SP 55007 (Benelong St) | Balcony Timber Repairs |
| 66562 | 19 months | 2 days ago | SP 76375 (Primrose Ave) | Major Waterproofing Ingress Works |
| 80901 | 14 months | 3 days ago | SP 71821 (Taylor St) | Drainage and Roofing — Shop B |
| 85869 | 13 months | 6 days ago | SP 4874 (Terrace Rd, Dulwich Hill) | Roadmap + Engineer Peer Review |
| 89097 | 12 months | 6 days ago | SP 41600 (Bowen Close, Cherrybrook) | Multiple Building Repairs |
| 96959 | 9.5 months | 4 days ago | SP 3132 (Wallis St, North Bondi) | Water damage — Unit 1 |
| 99993 | 8.5 months | 6 days ago | SP 92989 (New South Head Rd) | Various Lots Water Ingress |
| 100233 | 8.5 months | 3 days ago | SP 101701 (Bricklane Retail) | Building Defects |
| 101457 | 8 months | 2 days ago | SP 105746 (Rocky Point Rd) | Unit 10 Defects |

## Portfolio Summary

| Metric | Count |
|---|---|
| Total open/pending tickets | 107 |
| Marked Open | 64 |
| Marked Pending | 43 |
| No agent response on record (Bucket A) | 28 |
| — of which >2 weeks unanswered | 8 |
| — of which >30 days unanswered | 3 |
| Client has replied, Matt not yet responded (Bucket B) | 7 |
| — of which Matt silent >1 week | 2 |
| Open tickets where Matt was last updater (Bucket C) | 40 |
| — of which >30 days since Matt's reply (Bucket C1 = stale C) | 10 |
| Stale — no activity either side >30 days (Bucket D) | 10 |
| Very old, live projects (Bucket E) | 9 |
| Same building appearing multiple times (possible duplicates) | Bennett St (124445 + 124587); Pitt St (121653 + 126646); William St Ashfield (126300 + 126936) |

## Observed patterns in the data

1. **Three tickets have been completely unanswered for more than 30 days:** 121236 (51), 121653 (47), 123829 (31).
2. **~37% of tickets marked "Open" are awaiting the requester, not Matt** (40 of 64 Open tickets are Bucket C). The "Open" count overstates Matt's outstanding action.
3. **10 tickets have had no activity from either side for over 30 days** — candidates for close, merge, or proactive chase.
4. **Portfolio size (107)** is heavy for a single assignee in a specialist-lead role.
5. **Three sets of likely duplicates** appear in the data: two Bennett Street tickets at SP 67844 (124445, 124587), two Pitt Street scope/variation tickets at SP 87409 (121653, 126646), two William Street waterproofing tickets at SP 98328 (126300, 126936).

## Related pages

- [[Matt Wrigley]] — role, targets, 1:1 structure
- [[Matt Wrigley — Ticket Hygiene Support Plan (2026-04-19)]] — proposed VN ops support structure
- [[More Than Strata (MTS)]]

---

*Source file: raw/Matthew Open and Pending Tickets.csv (19/04/2026 pull). This analysis is a point-in-time snapshot and will date rapidly; rerun weekly as part of 1:1 prep.*

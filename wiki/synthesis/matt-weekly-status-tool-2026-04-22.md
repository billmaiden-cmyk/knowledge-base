---
title: "Matt Wrigley — Weekly Status Report Tool (2026-04-22)"
created: 2026-04-22 11:00 AEST
updated: 2026-04-22 11:00 AEST
tags: [mts, matt-wrigley, tools, zendesk, status-report, dashboard, reporting]
sources:
  - raw/Matthew Open and Pending Tickets.csv
  - raw/Matt-Dashboard_20042026.pdf
  - wiki/synthesis/matt-ticket-portfolio-analysis-2026-04-19.md
  - wiki/synthesis/matt-1on1-brief-2026-04-19.md
source_date: 2026-04-22
---

# Matt Wrigley — Weekly Status Report Tool (2026-04-22)

A single-page HTML application built to give Matt a repeatable Monday-morning routine for producing his weekly status report. Replaces the ad-hoc approach where Matt was expected to assemble the status report manually (and did not deliver it at the 20 April 1:1). The tool codifies the metrics agreed in the [[Matt Wrigley — 1:1 Brief: Ticket Portfolio & Billing Review (19 April 2026)]] and extends them with a week-over-week trend layer.

## Location

- `tools/matt-status-report/index.html` — the tool
- `tools/matt-status-report/README.md` — usage, targets, Zendesk API options

## What it does

Takes three kinds of input and produces a structured weekly report:

1. **Manual** — billing hours, billing amount (from Schedule B).
2. **PDF** — numbers read off the Zendesk weekly dashboard export (tickets received, tickets solved, first response time, full resolution time, Open, Pending, Total waiting reply, Ultra-long >90d). Describes the 7-day period ending Sunday.
3. **CSV** — the live Monday-morning Open+Pending export. Computes live response-quality metrics (the new >24h overdue count, Bucket A/B/C, stale>30d, oldest unanswered).

The output is:

1. **A current-week KPI dashboard** grouped into five sections — Billing / Week Activity (pdf) / Backlog (pdf) / Live Response Performance (csv) / 12-week Trend. Each tile is tagged with its source and colour-coded against thresholds.
2. **A 12-week trend table** — sparklines for each metric so drift shows up before the 1:1, not in it.
3. **A stored weekly history** — JSON-exportable, allowing quarterly analysis and later Schedule B reconciliation.

## Metrics by source

| Metric | Source | Derivation |
|---|---|---|
| Hours billed, Billing amount, Effective rate | manual | Schedule B; shown vs 25-hr / $6,900 / $276 targets |
| Tickets received, Tickets solved, Net change | pdf | Weekly dashboard tiles; net = received − solved |
| First response time, Full resolution time | pdf | Weekly dashboard tiles |
| Open, Pending, Total backlog | pdf | Backlog widgets at week end |
| Total tickets waiting reply | pdf | "Total tickets waiting" widget |
| Ultra-long open (>90d) | pdf | "Total tickets >90 days" widget |
| **Not responded to > 24 hours** (new) | csv | Count where agent owes next action AND state persists >24h. Covers (a) no agent response ever with age>24h, (b) client replied + agent silent >24h. |
| No agent response ever (Bucket A) | csv | `Assignee updated` blank |
| Client waiting on Matt (Bucket B) | csv | `Requester updated` > `Assignee updated` |
| Status mismatch (Bucket C) | csv | Open AND agent last updated |
| Stale >30 days (Bucket D) | csv | `Updated` >30 days before snapshot |
| Oldest unanswered | csv | Max days-waiting across tickets where Matt owes next action |

Note: PDF Open/Pending will differ slightly from CSV Open/Pending because the PDF is week-ending-Sunday and the CSV is Monday-live. This is expected and both are stored.

## Intended use

**Monday morning, ~10 minutes:**

1. Export Open+Pending view from Zendesk as CSV.
2. Open the tool.
3. Enter billing hours + amount from Schedule B for the week just ended.
4. Paste/upload the CSV.
5. Preview, save.
6. Dashboard refreshes.

Matt brings the dashboard (or a screenshot) into the 1:1. No more "did you do the status report?" preamble — the artefact exists before the meeting starts.

## Relationship to the 19 April 1:1 brief

The 19 April brief introduced the methodology and one-shot analysis. This tool makes that methodology **repeatable** and **tracked over time**:

- The 19 April brief showed 28 first-reply-SLA breaches at a single point in time. The tool shows whether that number is clearing or growing, week by week.
- The 19 April brief flagged the billing-vs-tickets selection pattern. Over 4+ weeks of data, the tool will show whether the pattern persists or resolves.
- The 19 April brief retired the 8-metric Section-3 dashboard as "too detailed" in-meeting (per [[Matt Wrigley]] entity page, updated 2026-04-20). The tool restores the measurement layer *outside the meeting* so Section 3 can remain a conversation.

## Zendesk API — direct ingestion (future)

Three options documented in the README. Recommended path: a small Python sidecar using Zendesk's REST API (`/api/v2/search.json?query=type:ticket+status:open+status:pending+assignee:{matt_id}`) that outputs the same CSV shape the tool already parses. ~1 day of work. Pairs well with pulling closed tickets so the Schedule B reconciliation the 19 April brief flagged (§8 next steps) can be automated.

## Design decisions

- **Single HTML file, no dependencies.** Works offline, no server, no CDN. Matt bookmarks `index.html` and it opens in his browser.
- **localStorage persistence.** Simpler than a backend for one user. JSON export covers backup and machine-transfer.
- **Traffic-light thresholds set as starting guesses.** Will need recalibration once four weeks of real data sets a baseline.
- **No VN ops reporting layer.** Per the 2026-04-20 revision to the VN ops support plan, this tool reports up — it is not a surveillance tool for the triage partner.

## Related pages

- [[Matt Wrigley]] — role, targets, 1:1 structure
- [[Matt Wrigley — Ticket Portfolio Analysis (19 April 2026)]] — methodology source
- [[Matt Wrigley — 1:1 Brief: Ticket Portfolio & Billing Review (19 April 2026)]] — the brief this tool operationalises
- [[Matt Wrigley — Ticket Hygiene Support Plan (VN Ops, 2026-04-19)]] — the parallel support structure

---

*Built 2026-04-22 following Matt's non-delivery of the status report at the 20 April 1:1. Purpose: remove the assembly step as a failure mode.*

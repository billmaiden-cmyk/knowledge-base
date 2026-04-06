---
title: Antonella — ANTS Filter (Accumulation & Trend Strength)
created: 2026-04-05
updated: 2026-04-05
tags: [trading, antonella, ants, accumulation, google-sheets, screening, o-neil]
sources:
  - Google Drive / Bill and Antonella comms / Ants documentation
stale: false
---

The ANTS filter is a Google Sheets–based stock screener designed to identify stocks showing institutional accumulation within a constructive price structure. It is the primary entry-signal layer in [[Antonella's Trading Framework]].

## What ANTS Stands For

A systematic filter for stocks that are:
- **A**ccumulating (more up days than down days on volume)
- **N**ear their recent high (not extended, not collapsing)
- **T**ight in price action (low volatility, controlled)
- **S**trong in short-term trend (positive 2-week return)

## Filter Criteria

| Condition | Threshold |
|-----------|-----------|
| Up days in last 10 | ≥ 6 |
| Accumulation days (up day on above-average volume) | ≥ 3 of last 10 |
| 2-week return | ≥ 5% |
| Distance from 20-day high | Between −5% and +3% |

The "distance from 20-day high" window ensures the stock is neither extended (>+3% above high = extended) nor in freefall (<−5% = broken).

## Google Sheets Implementation

The spreadsheet has two tabs:

### DATA Tab
Contains raw price/volume data with columns for close, volume, SMA50, ANTS score components, and derived metrics per row.

### SCAN Tab
Uses a `LET` formula to filter, score, and rank candidates:

```excel
=LET(
  d, DATA!A2:Q,
  candidates, FILTER(d, <criteria>),
  SORT(candidates, 8, FALSE)
)
```

The sort key (column 8) is the composite ANTS score, descending.

## Scoring Logic

Each criterion contributes to a 0–1 score:
- Up-day ratio: `up_days / 10`
- Accumulation ratio: `acc_days / 10`
- 2-week return normalised to a 0–1 scale
- Proximity to 20D high normalised to a 0–1 scale

These are combined into a weighted composite. Stocks scoring above a threshold (~0.5) pass the ANTS screen.

## Integration with Broader Framework

ANTS is one of three scores in the Master Score:

```
Master Score = 0.35 × ANTS_Score + 0.30 × Cover_Score + 0.35 × PostEvent_Score
```

See also:
- [[Antonella — Constructive Base Score]] — base-quality score combined with ANTS
- [[Antonella — Event-Driven Opportunities]] — the PostEvent component
- [[Antonella — Trading Framework Overview]] — how all scores integrate

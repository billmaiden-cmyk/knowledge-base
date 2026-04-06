---
title: Antonella — Market Direction Model
created: 2026-04-05
updated: 2026-04-05
tags: [trading, antonella, market-direction, regime, o-neil, distribution-days, breadth]
sources:
  - Google Drive / Bill and Antonella comms / Market direction model
stale: false
---

The Market Direction Model determines the primary market regime (confirmed uptrend / under pressure / correction / rally attempt) to gate all individual stock signals. No stock-level entries are taken without market confirmation.

This is an O'Neil-style primary trend model applied to the ASX (and potentially US/Europe).

## Core Logic

The model outputs a **Market Direction Score** on a 0–3 scale:

| Score | Regime | Interpretation |
|-------|--------|----------------|
| 3 | Confirmed Uptrend | Full exposure, take breakouts |
| 2 | Uptrend Under Pressure | Reduce size, hold winners |
| 1 | Rally Attempt | Wait for Follow-Through Day |
| 0 | Correction | No new longs, protect capital |

## Key Inputs

### Primary Trend
- Price of index (ASX200 / XJO) relative to its 50-DMA and 200-DMA
- Direction of 200-DMA (rising/falling)
- Price above or below both MAs

### Distribution Filter
Distribution days are days when the index falls meaningfully (>0.2%) on higher volume than the prior day — indicating institutional selling. The model counts distribution days over a rolling 25-session window. 4–5 distribution days = market under pressure.

### Breadth Proxy
A breadth indicator (advancing vs declining stocks, or % above SMA50) provides a secondary confirmation that the index move is broad-based rather than driven by a handful of large caps.

## Follow-Through Day Detection

An FTD is the O'Neil confirmation signal for a new uptrend:
- Index has made a low (Day 1 of rally attempt)
- Days 4+ of the rally attempt: index closes up 1.25%+ on higher volume than prior day

Without an FTD, a "rally attempt" cannot be upgraded to "confirmed uptrend."

## Visualisation

- **Chart 1**: Index price + 50-DMA + 200-DMA
- **Chart 2**: Market Direction Score (0–3) as a time series
- Conditional formatting highlights regime transitions visually

## Why It Matters

Individual stock setups (ANTS, constructive base, post-event) are only valid when the market is in a confirmed uptrend or early rally. Buying strong setups in a distribution phase leads to failed breakouts — even great stocks go down in bear markets.

> "Markets trend most of the time. Big drawdowns happen below the 200-DMA. Participation matters more than prediction. You're reacting to facts, not narratives."

## Integration

This model gates all individual-stock signals from:
- [[Antonella — ANTS Filter]]
- [[Antonella — Constructive Base Score]]
- [[Antonella — Event-Driven Opportunities]]

When Market Direction Score = 0 or 1, no new long entries are taken regardless of individual stock scores.

## Related Pages

- [[Antonella — Short Risk Model]] — applies bearish regime logic
- [[Antonella — Trading Framework Overview]]

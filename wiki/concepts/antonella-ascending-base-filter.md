---
title: Antonella — Ascending Base Filter
created: 2026-04-05
updated: 2026-04-05
tags: [trading, antonella, ascending-base, filters, google-sheets, o-neil]
sources:
  - Google Drive / Bill and Antonella comms / Filters
stale: false
---

The Ascending Base Filter is a Boolean detector that identifies stocks forming an ascending base pattern — a particularly bullish structure where each successive consolidation occurs at a higher price level than the previous one.

## Ascending Base Definition (O'Neil Style)

An ascending base is characterised by:
- A series of 3 pullbacks, each finding support at higher lows
- Total depth is shallow (typically ≤18% each leg)
- The base slopes upward (positive slope)
- Volume dries up during each consolidation

This is considered a continuation pattern in a strong uptrend — the stock is resting at high altitudes before the next leg.

## Detector Criteria

| Condition | Threshold |
|-----------|-----------|
| Base depth per leg | ≤ 18% |
| Slope of base (price drift upward) | > 0 and < 0.004 (per day) |
| Tightness (close-to-close range) | ≤ 2% average |
| Higher lows confirmed | Yes |
| Volume dry-up present | Yes |
| Price above SMA50 | Yes |

The slope threshold (< 0.004) ensures the base is gently ascending — not a parabolic run (which would be slope > 0.01+).

## Google Sheets Implementation

The detector is implemented as a multi-condition Boolean formula:

```excel
=AND(
  base_depth <= 0.18,
  slope > 0,
  slope < 0.004,
  tightness <= 0.02,
  higher_lows = TRUE,
  volume_dryup = TRUE,
  E2 > N2   -- price above SMA50
)
```

Returns TRUE if all conditions are met, FALSE otherwise. Used as a filter column in the SCAN tab.

## How It Integrates with ANTS

The ascending base filter acts as a pre-filter or qualifier:
- ANTS catches general accumulation
- Ascending base narrows to the highest-quality setups within an uptrend

A stock passing both ANTS + Ascending Base filter represents an elite setup — strong trend, proper structure, volume confirmation.

## Key Insight

> The ascending base is the pattern where the biggest moves begin. Stocks that refuse to give back ground, consolidate tightly at new highs, and then break out on volume are the ones that double and triple. The filter captures this mechanically.

## Related Pages

- [[Antonella — ANTS Filter]] — primary accumulation detector
- [[Antonella — Base Labelling]] — how base counts are tracked
- [[Antonella — Constructive Base Score]] — quality scoring of bases
- [[Antonella — Trading Framework Overview]]

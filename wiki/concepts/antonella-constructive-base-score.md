---
title: Antonella — Constructive Base Score
created: 2026-04-05
updated: 2026-04-05
tags: [trading, antonella, base-score, short-pressure, google-sheets, o-neil]
sources:
  - Google Drive / Bill and Antonella comms / Improvement to constructive base score
stale: false
---

The Constructive Base Score is a composite metric that measures the quality of a stock's price consolidation (base) using both weekly and daily data, then blends it with a Short Pressure Score to produce a final composite.

## Architecture

The framework uses a hybrid weekly/daily approach:
- **Weekly data** captures the macro structure (depth, duration, tightness over months)
- **Daily data** captures recent microstructure (tight closes, accumulation days, volume dry-up)

## Constructive Base Score Components

| Component | Description |
|-----------|-------------|
| Base depth | How far price fell from the prior high (shallower = better) |
| Tight weeks | Count of weeks with low close-to-close range |
| Volume dry-up | Volume contracting relative to SMA50 |
| Higher lows | Price making a series of higher lows (right side of base) |
| Position in base | Price location within the base range (closer to high = more constructive) |
| Above SMA50 | Whether price is recovering above key MA |

These are normalised to 0–1 and weighted into a `constructive_base_score`.

## Short Pressure Score

A separate score measuring how much short-side pressure exists — which, when combined with a constructive base, implies a potential squeeze setup:

```
short_pressure_score = 0.35 × si_score
                     + 0.35 × dtc_score
                     + 0.15 × si_dry_interaction
                     + 0.15 × si_squeeze_interaction
```

Where:
- `si_score` = short interest % normalised (MIN(1, SI/10%))
- `dtc_score` = days-to-cover ratio normalised
- `si_dry_interaction` = interaction between high SI and volume dry-up
- `si_squeeze_interaction` = interaction between high SI and ATR compression

## Composite Score

```
composite_score = 0.75 × constructive_base_score + 0.25 × short_pressure_score
```

The 75/25 weighting keeps base quality dominant while incorporating short-side dynamics.

## Typical Score Ranges

| Score | Interpretation |
|-------|----------------|
| < 0.35 | Weak / not constructive |
| 0.35–0.50 | Early-stage formation, monitor |
| 0.50–0.65 | Constructive, watch for ANTS trigger |
| > 0.65 | Strong setup — eligible for scan |

In the Dominoes (DMP) case study, a constructive score of 0.52 on a 26-week window was considered notable but still incomplete (base depth too deep, base position too early).

## Dry-up Score Formula

A key sub-component:
```
dryup_score = MAX(0, MIN(1, 1 - (dryup_ratio - 0.4) / 0.8))
```
Where `dryup_ratio = volume / SMA50_volume`. Score near 1 = strong volume dry-up = sellers gone.

## Related Pages

- [[Antonella — ANTS Filter]] — entry signal that fires after constructive base is confirmed
- [[Antonella — Short Trap Index]] — extends the short pressure analysis
- [[Antonella — Short Interest & ATR]] — underlying data inputs for short pressure
- [[Antonella — Trading Framework Overview]]

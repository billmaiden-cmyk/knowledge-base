---
title: Antonella — Short Trap Index & MA Coherence
created: 2026-04-05
updated: 2026-04-05
tags: [trading, antonella, short-trap, ma-coherence, squeeze, regime, google-sheets]
sources:
  - Google Drive / Bill and Antonella comms / Shorted stocks and where shorts relaxed or nervous
stale: false
---

The Short Trap Index quantifies the probability that shorts are trapped in a losing position — combining MA coherence, ATR compression, volume dry-up, short interest, and trend repair into a single 0–1 score with a regime classifier.

## MA Coherence — The Central Concept

MA coherence measures how much trend structure remains in a stock's moving averages. It is distinct from direction:

- **High coherence (wide separation)**: Trend is strong, shorts are comfortable
- **Low coherence (tight/compressed)**: Trend information has decayed — short edge is gone

```
MA Dispersion = (|SMA10 - SMA50| + |SMA50 - SMA200|) / Price
```

High dispersion = strong trend structure (either direction). Low dispersion = no trend information.

> "Shorts don't care if it's uptrend or downtrend. They care if the trend is still wide and stable, or has compressed and lost structure."

## Short Trap Index — Full Formula

```
Short_Trap_Index = MIN(1,
  SI_Score ×
  ATR_Compression_Score ×
  MA_Compression_Score ×
  Dry_Score ×
  Trend_Repair_Score
) × (1 - Bearish_Structure × 0.5)
```

### Component Formulas (Google Sheets)

**A. SI Score** — short interest normalised
```excel
=MIN(1, BT2/10%)
```

**B. ATR Compression Score** — rises when ATR is falling
```excel
=MAX(0, MIN(1, (0.9 - T2) / 0.5))
```
Where T2 = ATR10/ATR50

**C. MA Compression Score** — rises when MAs are converging
```excel
=MAX(0, 1 - MIN(1, ((ABS(M2-N2) + ABS(N2-O2)) / E2) / 0.15))
```
Where M2=SMA10, N2=SMA50, O2=SMA200, E2=Close

**D. Dry-up Score** — rises when volume is below average
```excel
=MAX(0, MIN(1, (1 - U2) / 0.8))
```
Where U2 = Volume/SMA50Volume

**E. Trend Repair Score** — rises when price is beginning to recover
```excel
=(--(E2>M2) + --(M2>M3) + --(ABS(E2-N2)/N2 <= 0.05)) / 3
```
(price above SMA10, SMA10 rising, price within 5% of SMA50)

**F. Bearish Structure Score** — reduces trap score if bearish alignment is still strong
```excel
=(--(E2<N2) + --(N2<O2) + --(M2<N2)) / 3
```

## Regime Classifier

```excel
=IF(BZ2 >= 0.6, "SHORT TRAP",
   IF(BZ2 >= 0.35, "WATCH",
      "SHORT COMFORT"))
```

| Score Range | Regime | Meaning |
|-------------|--------|---------|
| 0.00–0.25 | SHORT COMFORT | Shorts safe, trend intact |
| 0.25–0.45 | WATCH | Compression building |
| 0.45–0.65 | WATCH | Real danger zone |
| 0.65+ | SHORT TRAP | Exit shorts, squeeze risk high |

## The Trigger Column

A high Trap Index is a latent condition. The actual trigger fires when:

```excel
=AND(TrapIndex > 0.5, E2 > M2, U2 > 1.3)
```

- Trap exists (score > 0.5)
- Price moved above SMA10
- Volume expanding (>130% of average)

This is when the squeeze typically starts.

## Three Stages of Short Psychology

1. **Trend phase** → "Press the short, trend is strong"
2. **Compression phase** → "Reduce position, something is changing"
3. **Inflection phase** → "Cover — I'm wrong"

The Short Trap Index detects the transition from Stage 2 to Stage 3 before most shorts recognise it.

## "False Bearish Comfort" Pattern

The most dangerous setup for shorts:
- Price still below SMA200 (looks bearish)
- BUT: MAs compressing, ATR falling, volume drying, SI elevated

This is "false bearish comfort" — the optical bearish signal masks a structural trap.

## Recommended Sheet Structure

6 helper columns:
- `SI_score`, `ATR_compression_score`, `MA_compression_score`
- `Dry_score`, `Trend_repair_score`, `Bearish_structure_score`

Then: `Base_trap_score`, `Adjusted_trap_score`, `Regime`

## Related Pages

- [[Antonella — Short Interest & ATR]] — core SI and ATR inputs
- [[Antonella — Short Risk Model]] — the bearish entry model this index warns against
- [[Antonella — Short Interest Case Study (DMP)]] — real example of short trap dynamics
- [[Antonella — Constructive Base Score]] — the long-side mirror
- [[Antonella — Trading Framework Overview]]

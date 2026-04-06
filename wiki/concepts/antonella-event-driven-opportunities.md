---
title: Antonella — Event-Driven Opportunities
created: 2026-04-05
updated: 2026-04-05
tags: [trading, antonella, event-driven, post-event, master-score, google-sheets, o-neil]
sources:
  - Google Drive / Bill and Antonella comms / Event driven opportunities
stale: false
---

This framework identifies stocks that have experienced a significant corporate event (earnings miss, capital raise, regulatory news, sell-off) and are now quietly absorbing the shock — forming a post-event base with squeeze potential.

The Tamboran/Falcon case study is the primary real-world example used to develop this model.

## 4-Phase Post-Event Model

| Phase | Characteristics |
|-------|-----------------|
| **1. Event shock** | Large price move, spike in volume, fear/euphoria |
| **2. Digest** | Volume recedes, price oscillates with decreasing range |
| **3. Absorption** | Tight closes, ATR contraction, short interest elevated |
| **4. Base formation** | Price stabilises, right side begins, MAs flatten |

The setup fires when Phase 3→4 transition is confirmed by the ANTS trigger.

## Post-Event Base Score

```
Post_Event_Base_Score = 0.30 × Vol_Dry_10d
                      + 0.25 × Range_Tight_5d
                      + 0.20 × (1 - VolumeRatio)
                      + 0.15 × TrendRepair
                      + 0.10 × TightnessScore
```

Where:
- `Vol_Dry_10d` = volume dry-up over 10 days (normalised 0–1)
- `Range_Tight_5d` = average daily range tightness over 5 days
- `(1 - VolumeRatio)` = inverted volume ratio (low = good)
- `TrendRepair` = price recovering toward key MAs
- `TightnessScore` = close-to-close volatility compression

## Master Score

The Master Score integrates three independent signal streams:

```
Master_Score = 0.35 × ANTS_Score
             + 0.30 × Cover_Score
             + 0.35 × Post_Event_Base_Score
```

Where:
- `ANTS_Score` = accumulation + trend strength (see [[Antonella — ANTS Filter]])
- `Cover_Score` = short interest regime (SI falling = shorts covering = bullish tailwind)
- `Post_Event_Base_Score` = post-event absorption quality (above)

The equal weighting of ANTS and PostEvent (0.35 each) reflects that both structural quality and short-side dynamics matter equally. Cover_Score at 0.30 is slightly lower as a confirming rather than primary signal.

## Cover Score Logic

The Cover_Score rises when short interest is falling — indicating shorts are voluntarily exiting, which:
1. Removes supply pressure
2. Creates demand (short covering = buying)
3. Compresses volatility further

This is distinct from new longs entering. Covering-driven tightness is a precursor to a genuine demand-driven move.

## Tamboran / Falcon Case Study Insights

The case study showed:
- Post-event stocks can take 4–10 weeks to form a proper base
- Early short covering (SI falling) + ATR contraction often precedes a failed rally
- Confirmation requires: Vol_Dry_10d high + Range_Tight_5d high + price above SMA10

## Related Pages

- [[Antonella — ANTS Filter]] — the ANTS component of Master Score
- [[Antonella — Constructive Base Score]] — base quality score that feeds Cover_Score context
- [[Antonella — Short Interest & ATR]] — inputs for Cover_Score
- [[Antonella — Short Interest Case Study (DMP)]] — parallel case study
- [[Antonella — Trading Framework Overview]]

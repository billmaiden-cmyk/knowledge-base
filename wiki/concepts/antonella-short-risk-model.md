---
title: Antonella — Short Risk Model (Bearish Stack & Failed Rally)
created: 2026-04-05
updated: 2026-04-05
tags: [trading, antonella, short-selling, bearish, failed-rally, google-sheets, ma-stack]
sources:
  - Google Drive / Bill and Antonella comms / Short Risk documentation
stale: false
---

The Short Risk Model detects stocks in confirmed downtrends with failed rally signals, and outputs a regime classification (SHORT / COVER / AGGRESSIVE COVER ZONE / HOLD) for short-side positioning.

## Bearish MA Stack

The primary condition for a short setup is a fully bearish moving average stack:

```
Bearish Stack = AND(Price < SMA10, SMA10 < SMA50, SMA50 < SMA200)
```

When all four are in descending order, trend is clearly down and shorts have a structural edge.

## Failed Rally Detection

A failed rally occurs when price rallies briefly but cannot sustain above a key MA — confirming supply is still in control:

```excel
=IF(AND(E29 >= M29 * 0.98, E28 < M28, E28 < E29), 1, 0)
```

Logic:
- `E29 >= M29 * 0.98` → previous candle was within 2% of SMA10 (rally touched resistance)
- `E28 < M28` → current close is back below SMA10 (failed)
- `E28 < E29` → price moved lower (selling resumed)

A `1` signals a failed rally — confirmation that overhead supply is still dominant.

## Final Signal Formula

The regime classifier uses price relative to MAs and a ratio (likely price/SMA200 or ATR-based) to assign one of four states:

```excel
=IFS(
  AND(E28 < M28, E28 < N28),                  "SHORT",
  AND(E28 >= M28, (C4/C19) < 1),              "COVER",
  (C4/C19) < 0.8,                             "AGGRESSIVE COVER ZONE",
  TRUE,                                        "HOLD"
)
```

| Signal | Condition | Meaning |
|--------|-----------|---------|
| SHORT | Price below both SMA10 and SMA50 | Stay short, trend intact |
| COVER | Price reclaims SMA10 AND ratio weakens | Begin covering |
| AGGRESSIVE COVER | Ratio < 0.8 (strong compression signal) | Exit shorts urgently |
| HOLD | None of the above | Neutral — wait |

## Context: Short vs Long Framework

This model is the bearish mirror of the constructive base framework:

| Long Setup | Short Setup |
|------------|-------------|
| Bullish MA stack (Price > SMA50 > SMA200) | Bearish MA stack (Price < SMA10 < SMA50 < SMA200) |
| ANTS accumulation | Failed rally confirmation |
| Volume dry-up (supply exhausted) | Volume expansion on failed rally |
| Tight base | Downtrend continuation |

## Integration

The Short Risk Model feeds into:
- [[Antonella — Short Trap Index]] — detects when the SHORT regime is about to reverse
- [[Antonella — Short Interest & ATR]] — inputs for short pressure quantification

When the Short Risk Model says "SHORT" but the Short Trap Index is rising, the combination signals a dangerous position — shorts are still technically right but structurally trapped.

## Related Pages

- [[Antonella — Short Trap Index]]
- [[Antonella — Short Interest & ATR]]
- [[Antonella — Market Direction Model]]
- [[Antonella — Trading Framework Overview]]

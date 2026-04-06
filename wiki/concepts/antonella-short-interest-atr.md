---
title: Antonella — Short Interest & ATR Relationship
created: 2026-04-05
updated: 2026-04-05
tags: [trading, antonella, short-interest, atr, volatility, squeeze, google-sheets]
sources:
  - Google Drive / Bill and Antonella comms / The relationship between short interest and ATR
stale: false
---

This framework describes how the interaction between short interest (SI) and Average True Range (ATR) reveals coiled-spring setups — stocks where trapped shorts + compressed volatility create explosive potential.

## Core Thesis

> **High SI + Low ATR = Coiled Spring**

When a heavily shorted stock simultaneously shows ATR compression, the conditions for a violent short squeeze are in place:
- Shorts are trapped (cannot easily cover without moving price)
- Volatility is low (liquidity is thin)
- Any catalyst will force covering → price gaps → more covering

## ATR Normalisation

Raw ATR is meaningless across different price levels. The framework normalises it:

```
ATR% = ATR / Price
```

This makes stocks comparable. A $1 stock with ATR of $0.05 and a $100 stock with ATR of $5 both have ATR% of 5%.

## ATR Compression Score

Measures how compressed current ATR is relative to the stock's own history:

```
ATR_ratio = ATR10 / ATR50
ATR_Compression_Score = MAX(0, MIN(1, (0.9 - ATR_ratio) / 0.5))
```

| ATR Ratio | Interpretation | Score |
|-----------|----------------|-------|
| 1.0 | Normal volatility | 0 |
| 0.7 | Moderate compression | 0.3+ |
| 0.4 | Strong compression | 0.6+ |

## Short Interest Score

```
SI_Score = MIN(1, SI% / 10%)
```

Where 10% SI is considered "very high." If SI is stored as a decimal (7.5 not 7.5%), divide by 10 instead.

## The Danger Zone

```
Danger Zone = Low MA Dispersion + Low ATR
```

When MA dispersion is also low (MAs converging), the combination of:
1. Tight MAs (no trend edge remaining)
2. Low ATR (thin liquidity)
3. High SI (trapped participants)

...creates maximum squeeze potential. This is the "coiled spring."

## Three Stages of Short Interest Behaviour

1. **Active downtrend phase**: ATR high, shorts comfortable, SI building
2. **Compression phase**: ATR drops, MAs converge, shorts cover → volatility falls further
3. **Inflection**: Price moves above SMA10, SMA10 flattens, downtrend ends — shorts trapped

## Integration with Broader Framework

These inputs feed into:
- [[Antonella — Constructive Base Score]] (short pressure sub-score)
- [[Antonella — Short Trap Index]] (full SI × ATR × MA compression model)

Key column references in the Google Sheet:
- `T2` = ATR10 / ATR50 (compression ratio)
- `BT2` = short interest %
- `U2` = volume / SMA50 volume (dry-up ratio)

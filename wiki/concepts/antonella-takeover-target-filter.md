---
title: Antonella — Takeover Target Filter
created: 2026-04-05
updated: 2026-04-05
tags: [trading, antonella, takeover, m-and-a, stealth-accumulation, liquidity-compression, google-sheets]
sources:
  - Google Drive / Bill and Antonella comms / Takeover target filter
stale: false
---

The Takeover Target Filter detects stocks showing the microstructure signature of stealth institutional accumulation — consistent with a potential M&A situation where a strategic or financial buyer is quietly building a position before a public announcement.

## Core Thesis

Takeover candidates often exhibit a distinctive pattern before announcement:
1. Volume dries up (acquirer doesn't want to move price)
2. Price compresses tightly (low ATR, low daily range)
3. Base forms at a logical valuation support level
4. Occasional stealth accumulation days (above-average volume, tight range, close near high)

The filter looks for the intersection of these signals.

## Trigger Condition

```
TAKEOVER_TRIGGER = AND(
  liquidity_compression_score > 0.7,
  value_score > 0.4,
  Volume_today > 2 × SMA50_Volume,
  ABS(Price_change) < 5%,
  Prior_10d_volume_low = TRUE
)
```

The key tension: today's volume spike (>2× average) on a small price move (<5%) after 10 days of very quiet volume is the "stealth accumulation" signature. The buyer was quiet, then needed to accumulate more shares.

## Final Model

A more complete model combines base quality with liquidity and valuation:

```
Final_Signal = AND(
  base_score > 0.65,
  liquidity_compression > 0.60,
  Prior_10d_volume_low = TRUE,
  stealth_ants BETWEEN 0.55 AND 0.80,
  IC_multiple < 0.8
)
```

Where:
- `base_score` = constructive base score (see [[Antonella — Constructive Base Score]])
- `liquidity_compression` = combined ATR + volume dry-up measure
- `stealth_ants` = ANTS score (accumulation within tight range) — must be in "stealth" range, not already extended
- `IC_multiple` = implied capitalisation or EV/EBITDA multiple proxy (< 0.8 = undervalued)

## Liquidity Compression Score

```
liquidity_compression = weighted_average(
  ATR_compression_score,    -- price range contracting
  volume_dryup_score,       -- turnover falling
  bid_ask_tightness         -- if available
)
```

High liquidity compression = stock is quiet, thin, and not being traded actively.

## Stealth ANTS

The `stealth_ants` range of 0.55–0.80 is deliberately bounded on both ends:
- < 0.55: not enough accumulation evidence
- > 0.80: already extended — the accumulation phase may be over

## Why IC Multiple Matters

A sub-0.8 IC multiple suggests the stock is priced below replacement cost or well below peers — the most likely stocks to attract M&A attention. Combining this with stealth accumulation is a powerful dual signal.

## Related Pages

- [[Antonella — Constructive Base Score]]
- [[Antonella — Short Interest & ATR]]
- [[Antonella — ANTS Filter]]
- [[Antonella — Trading Framework Overview]]

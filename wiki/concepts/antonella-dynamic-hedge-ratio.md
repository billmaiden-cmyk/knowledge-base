---
title: "Antonella — Dynamic Hedge Ratio"
created: 2026-04-06
updated: 2026-04-06
tags: [trading, antonella, hedging, short-interest, atr, risk-management, squeeze]
sources:
  - raw/whatsapp/00003397-Dynamic Hedge Ratio.docx
source_date: 2026-04
---

Discussion document exploring how a long investor can dynamically hedge market (beta) risk using the trading framework's existing metrics (constructive base, squeeze probability, ATR, short interest). Covers dynamic hedge ratios, ATR contraction in shorted stocks, and how shorts think about MA coherence. *(source: raw/whatsapp/00003397-Dynamic Hedge Ratio.docx)*

## Core Hedge Equation

Stock return decomposes as: `Rstock = β × Rmarket + α`

When price is below 200DMA (weak regime), hedge the beta component:

**Full hedge:** `Short Position = β × L` (where L = long exposure)

**Partial (dynamic):** `Short Position = h × β × L` (where h ∈ [0,1] = hedge intensity)

**Net market exposure:** `L × (1 − h × β)`

## Framework-Integrated Hedge Ratio

The key insight: tie hedge intensity to the trading framework's existing metrics rather than using a static ratio.

**Master equation:**

```
Hedge = (1 − BaseQuality) × (1 − SqueezeProbability) × β × L
```

| Constructive Score | Squeeze Risk | Hedge Intensity |
|-------------------|-------------|-----------------|
| 0.9 (strong base) | High | Very light (~0.01) |
| 0.5 (moderate) | Low | Moderate (~0.50) |
| 0.2 (weak) | Low | Heavy (~0.80) |

**Implication:** Don't hedge aggressively when squeeze risk is high (upside convexity coming). Don't hedge when base is repairing (constructive score rising).

## ATR Contraction + Short Interest = Energy Storage

This is one of the cleanest "pressure build" signals:

```
Squeeze Pressure ∝ Short Interest / ATR
```

| Condition | Meaning |
|-----------|---------|
| High SI + High ATR | No pressure — shorts comfortable, can cover into volatility |
| High SI + Falling ATR | Building pressure — liquidity drying |
| High SI + Low ATR + Low Volume | **Maximum squeeze setup** — compressed spring |

**Why shorts get uncomfortable in low ATR regimes:** Exit function changes. In high ATR, they cover into volatility and the market absorbs volume. In low ATR, volume dries up, order book thins, small buying creates large price impact.

**The "trap equation":**

```
Short Trap Probability ∝ SI × (1/ATR) × Absorption
```

Where Absorption = Price Stability + Volume Dry-Up (distinguishes bearish compression from genuine absorption).

**Critical nuance:** ATR contraction has two modes:
- **Bearish compression:** Price drifting down, ATR falling, shorts in control → no squeeze risk
- **Absorption:** Price stabilising, higher lows, tight closes, ATR falling, volume drying → shorts losing control

## How Shorts Think About MA Coherence

**MA Coherence** = Distance between MAs is small AND slopes are aligned.

**Short perspective:**

| Stage | MA State | Short View |
|-------|----------|-----------|
| 1: Wide bearish separation | MAs far apart, ATR high | Comfortable — trend strong, can size bigger |
| 2: Compression phase | MAs converge, ATR drops, price stops falling | Warning — "Where is incremental supply coming from?" |
| 3: Inflection (trap) | Price above SMA10, SMA10 flattens, SMA50 flattens | **Danger** — downtrend → balance, exit risk rising |

```
Short Risk ∝ 1 / MA Dispersion
```

Where: `MA Dispersion = |SMA10 − SMA50| + |SMA50 − SMA200|`

**Key insight:** Most shorts stay too long into compression, assuming trend will resume. But MA coherence tightening = information loss in the trend. The edge that justified the short is gone.

**Danger Zone for shorts:** Low MA Dispersion + Low ATR + High SI = compressed spring.

**MA Compression Score:**

```
MA_Compression = 1 − (|SMA10 − SMA50| + |SMA50 − SMA200|) / Price
```

When combined with `sign` (is price above or below MAs?): above + compressed = about to break out (bullish); below + compressed = unclear.

## Implementation

Squeeze score formula for spreadsheet/database:

```
squeeze_score = SI_percentile × (1 − ATR_10/ATR_50) × (1 − Volume/SMA50_volume)
```

Trigger: `IF squeeze_score > 0.6 AND price > SMA10 → HIGH RISK OF SQUEEZE`

## Cross-References

- [[antonella-short-interest-atr]] — The SI × ATR relationship this paper formalises
- [[antonella-short-trap-index]] — Short Trap Index scoring
- [[antonella-short-risk-model]] — Bearish MA stack detection
- [[antonella-constructive-base-score]] — Base quality used in hedge ratio
- [[antonella-three-setups-framework]] — Setup classification that determines hedge approach

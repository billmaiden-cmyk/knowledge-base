---
title: Antonella — Short Interest Case Study (Domino's Pizza / DMP)
created: 2026-04-05
updated: 2026-04-05
tags: [trading, antonella, case-study, dmp, dominoes, short-interest, o-neil]
sources:
  - Google Drive / Bill and Antonella comms / Dominoes short interest case study
stale: false
---

This case study analyses Domino's Pizza Enterprises (ASX: DMP) around October 3, 2025, when it reached a constructive base score max of 0.52 on a 26-week window. It illustrates the two-phase short interest dynamic and explains the different cohorts of short sellers.

## The DMP Setup (Early October 2025)

Key metrics at the time:
- Constructive base score: **0.52** (max over 26 weeks)
- ATR contraction: ~0.68–0.70 ✅
- Volume dry-up ratio: 0.611 (dry-up score ~0.84) ✅
- Tight week count (last 3): **2** ✅
- Base position: ~0.03–0.11 (left side / early right side) ❌
- Base depth: ~0.52 (too deep for a mature setup) ❌

**Assessment**: Early-stage stabilisation with incomplete repair. Constructive signals present but not yet actionable.

## Types of Short Sellers

Understanding who is short — and why they cover — is critical to interpreting short interest movements.

| Type | Behaviour | Covers When |
|------|-----------|-------------|
| **Fundamental shorts** | Add on strength, conviction-based | Never voluntarily — wait for thesis change |
| **Tactical / technical shorts** | Trade breakdowns, SMA rejections | Into weakness (take profit) or on failed rally |
| **Hedge shorts** | Long-biased funds managing beta | When overall exposure needs rebalancing |
| **Event / catalyst shorts** | Earnings, capital raises | Fast in/out — sharp SI changes |
| **Structural / pairs traders** | Long one stock, short a peer | SI can rise even if stock stabilises |

## The Two-Phase Pattern Observed in DMP

### Phase 1: Short Interest Falling (late Sep → early Oct)
- Shorts buying shares to close positions (short covering)
- Creates demand → stabilises price → reduces volatility
- Explains: ATR contraction + tight weeks = 2
- This is **not** longs increasing exposure — it is **bearish pressure being removed**

### Phase 2: Short Interest Rising Sharply After
- Price rallies slightly into SMA50 resistance
- New shorts step in (tactical shorts fading the rally, fundamental shorts reloading)
- This is **fresh shorts entering into strength** — not old shorts re-adding
- Results in: resistance, failed follow-through, price capped

## The Deeper Signal

| Metric | Status |
|--------|--------|
| Tightness improving | ✅ Bullish tailwind |
| ATR contracting | ✅ |
| Short interest falling | ✅ Bullish (Phase 1) |
| Base depth ~0.52 | ❌ Too deep |
| Position in base low | ❌ Not yet on right side |
| MA coherence | ❌ Weak |

The setup was an early-stage stabilisation, not yet a mature entry signal. The short re-engagement (Phase 2) capped the rally before a proper base was established.

## Dry-Up Score Mechanics (Clarified)

```
dryup_score = MAX(0, MIN(1, 1 - (dryup_ratio - 0.4) / 0.8))
```

| Dryup Ratio | Score | Interpretation |
|-------------|-------|----------------|
| 0.5 | 1.0 (best) | Strong dry-up |
| 0.611 | ~0.84 | Moderate dry-up (DMP's value) |
| 1.0 | ~0.29 | No dry-up |
| >1.2 | → 0 | Volume expansion |

Lower ratio → higher score. Score near 1 = sellers gone = supply vacuum forming.

> "Dry-up alone isn't bullish — it's only bullish if demand shows up AFTER."

## Short Interest Regime Logic

```
Covering Phase = (SI falling over 10–15d) AND (ATR falling) AND (Tight weeks ≥ 2)
Short Re-Engagement = (Price rallies into SMA50/SMA200) AND (SI rising again)
```

## O'Neil Translation

- Early October DMP = "backing & filling + shakeout"
- After the rally cap = "overhead supply reasserting"

## Key Takeaway

The DMP case demonstrates why short interest must be interpreted dynamically, not statically. The same elevated SI level means different things depending on whether it is:
- Falling (covering phase = tailwind for longs)
- Rising on strength (re-engagement = headwind)

## Related Pages

- [[Antonella — Short Trap Index]] — the full model capturing this dynamic
- [[Antonella — Constructive Base Score]] — base quality score used in DMP analysis
- [[Antonella — Short Interest & ATR]] — foundational SI × ATR framework
- [[Antonella — Trading Framework Overview]]

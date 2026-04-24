---
title: Antonella — Three-Setups Framework
created: 2026-04-05
updated: 2026-04-06
tags: [trading, antonella, three-setups, framework, vma, kama, autoresearch, o-neil]
sources:
  - OneDrive / AI Hedge Fund / Three_Setups_Framework.docx
stale: false
---

The Three-Setups Framework is the evolution of Antonella's constructive base + ANTS work into a structured classification system. Rather than one trading model with growing exceptions, it defines three fundamentally different setup types — each with its own driver, qualifying conditions, entry signal, and position sizing.

> **Authorship**: This is Bill's synthesis document, March 2026 — a direct evolution of Antonella's v2 work.

## The Problem with One Model

One detector trying to catch every profitable move creates:
- Debates about whether MAs should be above/below
- Conflicting rules for short interest stocks vs uptrend stocks
- Threshold debates that go in circles

The reason: structurally different setups have different drivers and different success conditions.

## The Three Setups

### Setup 1: The Fresh Breakout

**What it is**: Stock declining/dormant, bases near lows, breaks out for the first time. The Appen (APX) pattern.

**Driver**: Supply exhaustion — everyone who wanted to sell has sold. No prior uptrend; often below SMA-50/200.

**What matters most**:
- Constructive base quality (tightness, dry-up, ATR contraction)
- `AccumDays10` rising — institutional volume days confirm accumulation, not abandonment
- Short interest dynamics — elevated SI with declining coverage is an accelerant
- VMA behaviour — flattening or crossing from below = repair signal

**What matters less**: SMA-50/200 position (both likely above), prior uptrend (none by definition), base number (always Base 1)

**Entry signal**: Constructive score peaks + ANTS rises within **15 days** + breakout volume ≥1.5× average. VMA transitioning from flat/falling to rising = additional confirmation.

**Position sizing**: **Half position** (highest risk — no trend context). Full size if short interest is also declining.

---

### Setup 2: The Continuation Base

**What it is**: Stock in uptrend pauses, consolidates, continues higher. Classic O'Neil Stage 2.

**Driver**: Institutional re-accumulation during pause. Trend is intact — stock is resting.

**What matters most**:
- **Price above SMA-50** (or above VMA) — core qualifier
- `dist_to_base_high ≤ 8%` — stock consolidating near top of range, not middle/bottom
- Tightness and volume dry-up
- Prior advance ≥30% — confirms this is a leader, not a dead stock
- Low distribution count — no heavy selling within base
- VMA rising as support

**What matters less**: Short interest (typically low in uptrends), dramatic ATR contraction (may already be normalised)

**Entry signal**: Constructive score peaks + ANTS rises within 15 days + price above SMA-50 (and/or VMA-9) + breakout volume ≥1.5× average.

**Position sizing**: **Full position** — all conditions align. Stop at base low or VMA.

**Base number modifier**:
| Base | Action |
|------|--------|
| 1–2 | Full size (new entry) / half add (already owned) |
| 3 | Smaller add or hold only |
| 4+ | Do not add; tighten stops |

---

### Setup 3: The Short Squeeze

**What it is**: Elevated short interest creates potential for forced buying. Base quality may be lower — the move is driven by supply/demand mechanics, not pure institutional accumulation.

**Driver**: Forced covering. High SI + drying volume = covering can't happen quickly → sustained upward pressure.

**What matters most**:
- SI ≥ 2–3% of float (relative to liquidity)
- **Days-to-cover** (adjusted): `short_shares / (0.4 × avg_daily_volume)` — high DTC = covering takes many sessions
- `si_dry_interaction` = SI × dry_score (Antonella's multiplicative interaction concept)
- `si_squeeze_interaction` = SI × squeeze_score (ATR contraction + trapped shorts)
- 5-day SI change declining — confirms covering has begun
- VMA: price crossing above VMA from below (especially when VMA flat) = covering becoming sustained

**What matters less**: Constructive base quality (threshold can be lower — 0.35 vs 0.50), trend context, prior advance

**Entry signal**: SI elevated and declining + DTC >4 + volume dry-up + price crossing above VMA or reclaiming SMA-50. Often triggered by a fundamental catalyst.

**Position sizing**: **Quarter to half position**. Time stop: if no 1R gain within 10 days, exit.

---

## Setup Comparison Table

| | Setup 1: Fresh Breakout | Setup 2: Continuation | Setup 3: Short Squeeze |
|---|---|---|---|
| Stage | Stage 1 | Stage 2–3 | Any |
| Driver | Supply exhaustion | Trend re-accumulation | Forced covering |
| Prior advance? | No | Yes (≥30%) | Irrelevant |
| Above SMA-50? | Likely no | **Required** | Not required |
| Short interest | Accelerant if present | Usually low | **Primary driver** |
| Constructive score min | ≥ 0.50 | ≥ 0.50 | ≥ 0.35 |
| ANTS min | ≥ 10 | ≥ 10 | ≥ 8 |
| ANTS window | 15 days | 15 days | 15 days |
| Position size | **Half** | **Full** | **Quarter to half** |

## Shared Tools (All Setups)

### Constructive Base Detector (v1 — with improvements)
Stage-agnostic — scores base quality without requiring trend context. Three improvements now implemented in the detector *(confirmed done by Kiet, 2026-04-06)*:
1. **Distribution penalty** (`distribution_count_last5w`) — catches hidden institutional selling ✅
2. **Tight streak** as separate component — rewards consecutive vs scattered tightness ✅
3. **ATR-normalised tightness** — replaces fixed 6% range threshold with `weekly_range ≤ k × ATR` ✅

### ANTS Score
Custom: `UpDays10×1 + AccumDays10×2 + Ret10×50 – |DistHigh20|×20`
Used across all three setups. In Setup 3, rising ANTS means institutions are buying alongside short covering → move more likely to sustain.

### VMA / KAMA (Kaufman Adaptive Moving Average)

> **Note (2026-04-06):** VMA and KAMA are functionally the same concept — both are adaptive moving averages that use the Efficiency Ratio to blend fast/slow smoothing. Different implementations exist but outputs are nearly identical. The system implements one adaptive MA using the Kaufman formula, referred to as VMA-9 in the database. There is no need for separate VMA and KAMA columns.

Adapts smoothing speed based on price efficiency ratio:
```
ER = net_price_change / total_absolute_movement
```
- ER=1 (trending cleanly) → fast response
- ER≈0 (choppy) → slow/flat

Three sensitivity levels: High (period 9), Medium (18), Low (27).

Key advantages:
- Goes flat during consolidation → cleaner range-bound reading than fixed SMAs
- Snaps responsive on breakout → transition from flat to tracking is itself a signal
- More useful than SMA-50 for Setup 1 (stocks below SMA-200 where fixed MAs are all above)
- Self-calibrating as trailing stop

**VMA is being tested alongside SMA, not replacing it.** Both versions of each setup query are run side-by-side. Autoresearch agent determines which performs better empirically.

### Market Regime
Not a gate — a **sizing modifier**:
- Down regime: smaller positions, higher constructive score requirements, more confirming conditions
- Up regime: standard sizing and thresholds
- During down regime, a Setup 1 with score 0.83 + declining SI still enters (Appen template) — at smaller size

## Constructive-to-ANTS Window: 15 Days (Not 60)
Tightened from 60 days. Rationale: if institutional accumulation is happening *inside* the base (via AccumDays10), both signals should fire close together. Appen's constructive max and ANTS spike were one day apart. A 60-day gap implies the base formed but institutions didn't show up — weaker signal.

Autoresearch will test 5, 10, 15, 20, 30 days to validate.

## Autoresearch Questions to Resolve

1. Does price above VMA(9) outperform price above SMA-50 for Setup 2?
2. Does VMA flattening + price crossing from below improve Setup 1 returns?
3. Does VMA work better as trailing stop than the Seven-Week Rule?
4. Does `base_number` as sizing modifier improve Setup 2 returns?
5. Does `si_dry_interaction` improve Setup 3 returns over SI alone?
6. Are optimal constructive score thresholds different per setup?
7. Is optimal ANTS threshold different for fresh breakouts vs continuation bases?

## Next Steps (as of March 2026)

1. Compute VMA/KAMA at periods 9, 18, 27 for all stock-dates in DB
2. Compute O'Neil base numbers for all stocks
3. Classify each historical signal into Setup 1/2/3 based on SMA-50 position, SI level, base number
4. Update `strategy.py` and `program.md` for three-setup testing
5. Run first autoresearch overnight session with baseline strategy
6. Validate best configuration against held-out test set

## Related Pages

- [[Antonella — Constructive Base Detector Spec]] — the technical spec for the shared base detector
- [[Antonella — Bridging Note (v2 to Three Setups)]] — how Antonella's v2 maps into this framework
- [[Antonella — Autoresearch System (prepare.py)]] — the evaluation harness
- [[Antonella — ANTS Filter]] — the ANTS score used across all setups
- [[Antonella — Short Trap Index]] — the SI/ATR interaction model behind Setup 3
- [[Antonella — Trading Framework Overview]]

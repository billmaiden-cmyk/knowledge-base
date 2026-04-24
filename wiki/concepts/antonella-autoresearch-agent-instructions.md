---
title: Antonella — Autoresearch Agent Instructions
created: 2026-04-05
updated: 2026-04-05
tags: [trading, antonella, autoresearch, agent, strategy, experiments, claude-code]
sources:
  - OneDrive / AI Hedge Fund / Autoresearch Approach.pdf
stale: false
---

This document is the instruction set for the Claude Code agent running the autoresearch trading strategy optimisation loop. The agent modifies `strategy.py` and evaluates results via `prepare.py`. This cannot be changed by the agent.

## Agent's Goal

Find the combination of filter conditions and parameters in `strategy.py` that maximises the composite metric computed by `prepare.py`. The metric measures how well the strategy identifies stocks about to rise over the next 15 trading days. Higher is better.

## The Experiment Loop

```
1. Make a change to strategy.py
2. Run: python prepare.py
3. Read the output — key number is: metric
4. If metric improved → keep the change (git commit)
5. If metric did not improve → revert (git checkout strategy.py)
6. Record what was tried and what happened
7. Go back to step 1
```

## What the Agent CAN Change (in strategy.py)

- **Parameter values**: any threshold, weight, multiplier, lookback period, window length
- **Filter conditions**: add new conditions, remove existing ones, make conditions conditional on other metrics
- **Logic structure**: sequence of signals (ANTS before constructive, or simultaneous), peak detection, which row is signal date
- **Scoring formula**: ANTS score weights (UpDays10 weight, AccumDays10 weight, Ret10 multiplier, DistHigh20 penalty), or replace composite ANTS with individual sub-components
- **Constructive score weights**: relative weights of tightness, dryup, squeeze, MA coherence, maturity — or use sub-components directly
- **MA logic**: switch unsigned to signed MA distance, add slope conditions, add stacking order, make MA conditions conditional on short interest
- **New derived conditions**: combine columns in new ways (e.g., `accum_days_10 × volume_multiple`, `atr_contract × dryup_ratio`)

## What the Agent CANNOT Change

- `prepare.py` — database connection, data loading, evaluation function, metric computation are **locked**
- The database itself
- Forward return calculations (pre-computed historical facts)
- Train/test split date (2025-07-01)
- Minimum signal count (20)

## The Metric

```
metric = profit_factor × sqrt(n_signals) × (1 - abs(max_drawdown))
```

- `profit_factor` = sum of winning 15-day returns / abs(sum of losing 15-day returns) → is edge positive?
- `sqrt(n_signals)` → enough opportunities? prevents cherry-picking 3 perfect trades
- `(1 - abs(max_drawdown))` → penalises worst single trade; forces attention to tail risk
- If fewer than 20 signals are generated → metric is automatically 0

## Available Database Columns

### Constructive Base
`constructive_score`, `constructive_best_window`, `tight_weeks_last3`, `tight_weeks_last5`, `tight_streak`, `dryup_ratio`, `atr_contract`, `dist_sma10`, `dist_sma50`, `close_pos`, `base_depth`, `base_high`, `base_low`

### ANTS
`ants_score` (composite), `up_days_10`, `accum_days_10`, `ret_10`, `dist_high_20`

### Moving Averages
`sma_10`, `sma_50`, `sma_200`, `dist_sma10_signed`, `dist_sma50_signed`, `dist_sma200_signed`, `above_sma10`, `above_sma50`, `above_sma200`

### Volume
`daily_volume`, `volume_50d_avg`, `volume_multiple`, `max_down_vol_10d`, `is_pocket_pivot`

### Short Interest
`short_interest_pct`, `short_interest_5d_change`, `short_risk_rating`, `days_to_cover`

### Forward Returns (EVALUATION ONLY — NEVER USE AS FILTERS)
`fwd_return_5d`, `fwd_return_15d`, `fwd_return_30d`, `fwd_return_60d`, `fwd_return_90d`, `fwd_return_max90d`

> **CRITICAL**: Never use forward return columns as filter conditions. That is look-ahead bias and produces a strategy that cannot work in live trading.

## Phased Experiment Strategy

### Phase 1: Baseline and Single-Variable Tests (Experiments 1–30)
1. Run current strategy unchanged. Record baseline metric.
2. Test each major parameter in isolation:
   - Constructive threshold: try 0.40, 0.50, 0.55, 0.60, 0.65, 0.70
   - ANTS threshold: try 5, 8, 10, 12, 15, 20
   - ANTS window: try 5, 10, 15, 30, 60, 90 days
   - Add `REQUIRE_ABOVE_SMA50 = True`
   - Add `REQUIRE_ABOVE_SMA10 = True`
   - Add `REQUIRE_BREAKOUT_VOLUME = True` (at 1.5×)
   - Add `REQUIRE_SI_DECLINING = True`
   - Add `REQUIRE_POCKET_PIVOT = True`

### Phase 2: Interaction Tests (Experiments 31–80)
3. Combine best-performing single-variable changes.
4. Test conditional logic:
   - SMA-50 required only when short interest is low
   - SMA-50 required only when `atr_contract` is above a threshold
   - Different constructive thresholds for above-SMA-50 vs below-SMA-50 stocks
5. Test sub-component substitution:
   - Replace ANTS composite with just `accum_days_10 >= N`
   - Replace constructive composite with just (tightness + dryup) conditions
   - Use `atr_contract` directly instead of squeeze component in composite

### Phase 3: Structural Changes (Experiments 81–150)
6. Test alternative sequences:
   - ANTS fires first, then constructive base forms within N days
   - Constructive and ANTS must be present on the same day
   - Signal date = the constructive peak date (not ANTS trigger date)
7. Test constructive score decline rate as a signal
8. Test MA slope conditions (SMA-10 slope rising)
9. Test MA stacking order (SMA-10 > SMA-50 > SMA-200)
10. Test compound derived metrics (e.g., `accum_days_10 × volume_multiple`)

### Phase 4: Simplification (Experiments 151–200)
11. Take best configuration from Phases 1–3.
12. Try removing each condition one at a time. If metric doesn't decline (or declines <2%), condition is not contributing → remove it permanently.
13. Goal: **simplest strategy achieving at least 95% of peak metric**.

### Phase 5: Robustness (Experiments 201–250)
14. Take simplified best configuration.
15. Perturb each numeric parameter by +10% and −10%. Run both. If metric drops >15%, strategy is sensitive to that parameter — note this.
16. **Final configuration should be stable across perturbations.**

## Reporting (After Each Experiment)

Print:
- Experiment number
- Hypothesis (what you're testing and why)
- What you changed in `strategy.py`
- The metric and all sub-statistics
- Whether you kept or reverted the change
- Running tally: current best metric

## Agent Preferences

- **Prefer simplicity**: A strategy with 5 conditions scoring 10.0 is better than one with 12 conditions scoring 10.5
- **Prefer robustness**: If a threshold only works at exactly one value, it's likely overfit
- **Never use forward returns as filters** — this is the cardinal rule
- **Think before you change**: read experiment history; don't repeat failed experiments; build on successful ones
- **Be systematic**: follow the phased approach; don't jump around randomly

## Related Pages

- [[Antonella — Autoresearch System (prepare.py)]] — the locked evaluation harness this document refers to
- [[Antonella — Action Priorities]] — the build order (autoresearch is Priority 4)
- [[Antonella — Three-Setups Framework]] — the strategy framework being tested
- [[Antonella — Trading Framework Overview]]

---
title: Antonella — Constructive Base Detector (Technical Spec)
created: 2026-04-05
updated: 2026-04-05
tags: [trading, antonella, base-detector, technical-spec, python, google-sheets, algorithm]
sources:
  - OneDrive / AI Hedge Fund / Constructive Base Detector.docx
stale: false
---

This document is Antonella's technical specification for the hybrid constructive base detector — the algorithmic implementation that powers the [[Antonella — Constructive Base Score]]. It defines exact calculations for each step, with worked examples.

> **Authorship**: This is Antonella responding to Bill's design work — she is specifying the precise computations and providing examples for implementation.

## Architecture: Hybrid Weekly + Daily

The detector uses **weekly data for base quality** (mature structural measures) and **daily data for MA coherence** ("acts right" signal). Each symbol gets weekly metrics attached to its daily rows.

## Output Fields

Per symbol per week t:
- `best_W` — which window length scored highest
- `base_high`, `base_low`, `base_depth`, `close_pos`
- `tight_weeks_last3`, `tight_weeks_last5`, `tight_streak`
- `dryup_ratio`, `dry_weeks_last5`
- `atr_contract`
- `dist_sma10`, `dist_sma50`, `std_close_10`
- `is_constructive_base` (boolean)
- `score` (0–1 composite)

## Step-by-Step Algorithm

### Step 1: Build Weekly Bars
Aggregate daily OHLCV to weekly:
- `wk_high`, `wk_low`, `wk_close`, `wk_volume`

### Step 2: Candidate Base Windows
For each symbol and week t, evaluate windows W ∈ {7, 8, 10, 12, 15, 20, 26} weeks:

```
base_high_W = MAX(wk_high over W)
base_low_W  = MIN(wk_low over W)
base_depth_W = (base_high_W - base_low_W) / base_high_W
close_pos_W  = (wk_close - base_low_W) / (base_high_W - base_low_W)
```

**Worked example (W=7):**
- base_high=105, base_low=94, latest close=102
- base_depth = 11/105 = 10.48% ✅ (not too deep)
- close_pos = 8/11 = 0.73 ✅ (upper half / right side)

### Step 3: Tightness (Weekly)

```
wk_range_pct    = (wk_high - wk_low) / wk_close
wk_close_chg_pct = ABS(wk_close - LAG(wk_close)) / LAG(wk_close)
tight_week = (wk_range_pct <= 0.06) AND (wk_close_chg_pct <= 0.015)
```

Rollups:
- `tight_weeks_last3` = count of tight weeks in last 3
- `tight_weeks_last5` = count of tight weeks in last 5
- `tight_streak` = consecutive tight weeks ending at t

**Worked example:** Flags [0,1,0,1,1] → tight_last5=3, streak=2

> Note: The 0.06 fixed threshold is flagged for replacement with ATR-normalised tightness in v2 improvements.

### Step 4: Volume Dry-Up (Weekly)

```
vol_avg_W     = AVG(wk_volume over W)
vol_avg_last2 = AVG(wk_volume over last 2 weeks)
dryup_ratio   = vol_avg_last2 / vol_avg_W
dry_weeks_last5 = COUNT(wk_volume <= 0.6 × vol_avg_W over last 5 weeks)
```

Requirement: `dryup_ratio <= 0.8`

**Worked example (W=7):** volumes [12, 11, 10.5, 9.8, 8.5, 7.2, 6.5]M
- vol_avg_7w = 9.357M
- vol_avg_last2 = 6.85M
- dryup_ratio = 0.733 ✅ (27% below average)

### Step 5: ATR Contraction (Squeeze)

```
atr_contract = ATR14 / ATR50
```

Requirement: `atr_contract <= 0.8` (stock is coiling)

True Range = MAX(high−low, |high−prevClose|, |low−prevClose|)
ATR = rolling average of TR (Wilder smoothing or SMA both acceptable for screening).

**Worked example:** ATR14=4.0, ATR50=6.0 → atr_contract = 0.667 ✅ (strong coil)

### Step 6: MA Coherence (Daily "Acts Right")

Daily metrics:
```
dist_sma10 = ABS(close - sma10) / sma10
dist_sma50 = ABS(close - sma50) / sma50
std_close_10 = STDDEV(close, 10) / sma10
```

Requirement: `dist_sma10 <= 0.03` OR `dist_sma50 <= 0.04`

Morales-style: constructive action "hugs" the 10/50-day MAs.

**Worked example:** close=102, sma50=100, sma10=101
- dist_sma50 = |102-100|/100 = 0.02 ✅

## Composite Scoring

The `score` field is a weighted combination of the Step 2–6 measures. Each dimension is normalised to 0–1 and the best window W is selected as the one maximising score.

Original v1 weights (starting point):
- Tightness: 25%
- Volume dry-up: 25%
- ATR contraction (squeeze): 25%
- MA coherence: 15%
- Base maturity: 10%

## Database Column Reference

| Column | Description |
|--------|-------------|
| `constructive_score` | Final composite (0–1) |
| `atr_contract` | ATR14/ATR50 |
| `dryup_ratio` | Recent vol / base avg vol |
| `tight_weeks_last3` | Count of tight weeks (last 3) |
| `close_pos` | Price position in base (0=low, 1=high) |
| `base_depth` | (high−low)/high of the base |

## Related Pages

- [[Antonella — Constructive Base Score]] — the scoring framework this spec implements
- [[Antonella — Three-Setups Framework]] — how the detector is used across three setup types
- [[Antonella — Autoresearch System (prepare.py)]] — the evaluation harness that tests strategy variants
- [[Antonella — Trading Framework Overview]]

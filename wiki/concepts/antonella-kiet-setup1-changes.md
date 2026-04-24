---
title: "Kiet — Setup 1 Query Changes & New Computed Fields"
created: 2026-04-06
updated: 2026-04-06
tags: [trading, kiet, queries, setup-1, vma, sma, fresh-breakout, implementation]
sources:
  - wiki/concepts/antonella-powerbi-queries.md
  - wiki/concepts/antonella-three-setups-framework.md
  - wiki/concepts/antonella-kama-regime-discussion.md
---

# Setup 1 (Fresh Breakout) — Updated Query Spec for Kiet

## What Changed and Why

Two fixes to the Setup 1 queries:
1. **SMA version** — added a new filter: price must be above SMA-10 (confirms stock has started recovering)
2. **VMA version** — fixed the VMA direction filter from "Flat or Falling" to "Flat or Rising" (old version would include stocks still in a downtrend). Also added a new price-to-VMA distance filter using ATR

---

## Step 1: Confirm / Add Computed Columns

Before updating the queries, confirm these columns exist in `daily_signals`. If any are missing, add them.

### Column: `vma9_direction`

**Already computed?** Please confirm.

If not, add as a computed column:

```
Step 1: Get VMA-9 slope over last 10 trading days
    vma9_change = vma_9[today] - vma_9[10 trading days ago]

Step 2: Normalise by ATR so "flat" means the same thing for all stocks
    vma9_slope = vma9_change / (10 * ATR14)

Step 3: Classify
    IF vma9_slope > 0.05  THEN "Rising"
    IF vma9_slope < -0.05 THEN "Falling"
    ELSE                       "Flat"
```

Store as text column: `Rising` / `Flat` / `Falling`

### Column: `dist_vma9`

**Already computed?** Please confirm.

If not:
```
dist_vma9 = (close - vma_9) / vma_9
```
Signed decimal. Example: -0.03 means price is 3% below VMA-9.

### Columns that should already exist (please confirm)

| Column | Needed for |
|--------|-----------|
| `vma_9` | VMA query condition #3 and #4 |
| `close` | Both queries |
| `sma_10` | SMA query condition #4 |
| `sma_50` | SMA query condition #3 |
| `ATR14` | VMA query condition #4 |
| `constructive_score` (or `constructive_score_max`) | Both queries condition #1 |
| `ants_score` | Both queries condition #2 |
| `volume` and `volume_sma50` | Both queries condition #5 |

---

## Step 2: Setup 1 SMA Version — Power BI Query

**Name:** `Setup1_FreshBreakout_SMA_ModeA`

**Filter:** Last 60 days only

**Conditions (all must be true):**

```
1. constructive_score_max >= 0.50
2. ants_score >= 10
   AND signal_date - constructive_max_date <= 15
3. close < sma_50
4. close > sma_10          ← NEW
5. volume >= 1.5 * volume_sma50
```

**In plain English:** Show me stocks where:
- A high-quality base formed (constructive score hit 0.50+)
- Institutional accumulation started within 15 days (ANTS hit 10+)
- Stock is still below its 50-day MA (not yet in an uptrend)
- Stock has reclaimed its 10-day MA (short-term recovery has begun) ← NEW
- Volume is elevated (1.5x average)

---

## Step 3: Setup 1 VMA Version — Power BI Query

**Name:** `Setup1_FreshBreakout_VMA_ModeA`

**Filter:** Last 60 days only

**Conditions (all must be true):**

```
1. constructive_score_max >= 0.50
2. ants_score >= 10
   AND signal_date - constructive_max_date <= 15
3. vma9_direction IN ("Flat", "Rising")     ← CHANGED (was "Flat", "Falling")
4. ABS(close - vma_9) <= 1.0 * ATR14        ← NEW
5. volume >= 1.5 * volume_sma50
```

**In plain English:** Show me stocks where:
- A high-quality base formed (constructive score hit 0.50+)
- Institutional accumulation started within 15 days (ANTS hit 10+)
- The adaptive moving average has stopped falling ← CHANGED
- Price is within 1 day's normal range of the adaptive MA (the crossover zone) ← NEW
- Volume is elevated (1.5x average)

**Note on condition #4:** `ABS()` means price can be slightly below or slightly above VMA-9. We want stocks in the crossover zone — not stocks still far below VMA (downtrend not over) and not stocks well above VMA (that's Setup 2 territory). ATR14 makes this adaptive to each stock's volatility.

---

## Step 4: Mode B (Backtest) Versions

Same conditions as above but:
- Remove the 60-day filter — run on full historical dataset
- Append forward return columns to output: `fwd_return_5d`, `fwd_return_15d`, `fwd_return_30d`, `fwd_return_60d`, `fwd_return_90d`, `fwd_return_max90d`

**Names:** `Setup1_FreshBreakout_SMA_ModeB` and `Setup1_FreshBreakout_VMA_ModeB`

---

## Output Columns (both versions, unchanged)

| Column | Description |
|--------|-------------|
| `symbol` | Stock ticker |
| `signal_date` | Date ANTS reached threshold |
| `constructive_max` | Constructive score at its peak |
| `constructive_max_date` | Date of constructive peak |
| `days_between` | Days from constructive max to ANTS trigger |
| `ants_score` | ANTS score at trigger |
| `accum_days_10` | AccumDays10 sub-component |
| `close_price` | Price at signal date |
| `volume_multiple` | Signal day volume / 50-day avg |
| `dist_sma10` | Signed distance from SMA-10 (%) |
| `dist_sma50` | Signed distance from SMA-50 (%) |
| `dist_sma200` | Signed distance from SMA-200 (%) |
| `dist_vma9` | Signed distance from VMA-9 (%) |
| `vma9_direction` | Rising / Flat / Falling |
| `short_interest_pct` | Short interest as % of float |
| `si_5d_change` | 5-day change in short interest |
| `days_to_cover` | Short shares / avg daily volume |
| `dryup_ratio` | Recent volume / base volume |
| `atr_contract` | ATR14/ATR50 |

---

## Questions for Kiet

1. Is `vma9_direction` already computed? If yes, what formula did you use for Rising/Flat/Falling?
2. Is `dist_vma9` already computed?
3. Which ATR is in the database — `ATR14`, `ATR10`, or both?
4. Is `sma_10` available as a column?
5. What are the actual column names in `daily_signals` for the fields above? (In case naming conventions differ from this spec)

---
title: Antonella — Action Priorities (Trading System Build Order)
created: 2026-04-05
updated: 2026-04-05
tags: [trading, antonella, action-priorities, kiet, database, roadmap, power-bi]
sources:
  - OneDrive / AI Hedge Fund / Action Priorities.pdf
stale: false
---

This document defines the sequenced build plan for the trading system — what needs to happen and in what order, so the team can start trading at reduced size immediately while the autoresearch system is set up in parallel.

> Core principle: **"We want to be trading now, even at smaller size, while the autoresearch system is being set up."**

## Priority 1: New Computed Values in the Database
**Owner**: Kiet | **Timeline**: This week | **Blocks**: everything

### 1a. Forward Returns (CRITICAL)
For every stock-date, compute and store:

| Column | Definition |
|--------|-----------|
| `fwd_return_5d` | (close 5 trading days later − close today) / close today |
| `fwd_return_15d` | Same, 15 trading days later |
| `fwd_return_30d` | Same, 30 days |
| `fwd_return_60d` | Same, 60 days |
| `fwd_return_90d` | Same, 90 days |
| `fwd_return_max90d` | Maximum close-to-close return at any point within next 90 days |

Without these, no strategy can be validated — current or proposed.

### 1b. VMA Values
For every stock-date, compute VMA/KAMA at three sensitivity levels:

| Column | Description |
|--------|-------------|
| `vma_9` | VMA with period 9 (high sensitivity) |
| `vma_18` | VMA with period 18 (medium sensitivity) |
| `vma_27` | VMA with period 27 (low sensitivity) |
| `dist_vma9` | (close − vma_9) / vma_9 as signed % |
| `vma9_direction` | Rising / Flat / Falling (based on slope over last 10 days) |

### 1c. Base Number (can be done in parallel)
For every stock, compute O'Neil base count:
- Prior high → minimum 8% drawdown → breakout above prior high = new base count
- Store as `base_number` column (1, 2, 3, 4+)

---

## Priority 2: Proposed Changes to Constructive Base v1
**Owner**: Kiet (implementation), Antonella (review) | **After Priority 1** | **Requires team agreement**

Three proposed changes to the shared detector — team discussion needed before implementation:

### 2a. Distribution Penalty (PROPOSED)
- Count distribution weeks in last 5 weeks (close down + volume up + close in lower 40% of weekly range)
- Subtract from constructive score as a penalty term
- **Why**: A base can score well on tightness/dry-up while hiding heavy selling weeks

### 2b. Tight Streak as Separate Component (PROPOSED)
- Score consecutive tight weeks separately from the count of tight weeks in last 3/5
- Three consecutive tight weeks > three scattered tight weeks
- **Why**: Consecutiveness signals sustained institutional control

### 2c. ATR-Normalised Tightness (PROPOSED)
- Replace fixed 6% weekly range threshold with: `weekly_range <= k × ATR`
- The detector already uses ratios for dry-up and ATR contraction — tightness was the only fixed absolute
- A mining stock at historically low volatility should qualify as tight even if range exceeds 6%
- **Why**: Corrects a measurement inconsistency in v1

**NOT changing in v1**:
- `dist_to_base_high` — proposed as Setup 2 qualifying condition only
- Scoring weights — flagged for autoresearch testing, not manual adjustment
- `close_pos` threshold (0.50 vs 0.65) — flagged for autoresearch testing

---

## Priority 3: Run the Three Setup Queries
**Owner**: Kiet (Power BI) | **As soon as Priority 1 is complete**

Two query modes × three setups × SMA and VMA versions each. See [[Antonella — Power BI Queries]] for full detail.

**Mode A — Live Signals** ("What should I trade today?"): last 60 days, no forward return filter. This is the watchlist for trading at reduced size.

| Setup | Constructive Min | ANTS Min | Window | Key Condition |
|-------|-----------------|----------|--------|---------------|
| 1 (Fresh Breakout) | ≥ 0.50 | ≥ 10 | 15 days | Price BELOW SMA-50 + volume ≥ 1.5× |
| 2 (Continuation) | ≥ 0.50 | ≥ 10 | 15 days | Price ABOVE SMA-50 + volume ≥ 1.5× |
| 3 (Short Squeeze) | ≥ 0.35 | ≥ 8 | 15 days | SI ≥ 3%, DTC ≥ 4 |

VMA versions: replace SMA-50 conditions with VMA-9 conditions. Run both to compare.

**Mode B — Backtest** ("What worked historically?"): full historical dataset, all signals, no forward return filter. Filter interactively in Power BI.

What to do with results:
- Mode A: review live signals, start trading highest-conviction at reduced size
- Mode B: filter interactively on forward return columns; compare 20%+ winners vs losers

---

## Priority 4: Set Up and Run Autoresearch
**Owner**: Kiet (infrastructure), Claude Code (agent) | **Parallel with Priorities 1–3**

### 4a. Infrastructure
- Python environment with pandas, sqlalchemy
- Git repository for `strategy.py` version control
- Claude Code CLI installed with API key

### 4b. Connect to Database
- Update `prepare.py` SQL query with actual column names
- Test: `python prepare.py` should load data and compute baseline metric

### 4c. First Overnight Run
- Baseline: constructive ≥ 0.50, ANTS ≥ 10, 15-day window
- Agent tests ~250–500 variations overnight
- Review results in the morning

### 4d. What Autoresearch Will Resolve
- Optimal constructive and ANTS thresholds per setup
- Whether VMA outperforms SMA (or whether layering adds value)
- Whether pocket pivot adds signal over ANTS AccumDays10
- Optimal ANTS window (5, 10, 15, 20, 30 days)
- Whether proposed v1 changes actually improve forward returns
- Optimal scoring weights
- Which conditions matter and which are noise

---

## Summary Table

| Priority | What | Why | Owner |
|----------|------|-----|-------|
| 1 | New database columns (forward returns, VMA, base number) | Everything else depends on this data existing | Kiet |
| 2 | Proposed constructive base v1 changes | Improves signal quality for all three setups | Team agreement |
| 3 | Run three setup queries (SMA + VMA versions) | Produces tradeable signals NOW | Kiet |
| 4 | Autoresearch setup and first run | Optimises everything empirically at scale | Kiet + Claude Code |

> **We trade on Priority 3 results at reduced size while Priority 4 runs in parallel.**

## Related Pages

- [[Antonella — Power BI Queries]] — detailed query specifications for Kiet
- [[Antonella — Autoresearch Agent Instructions]] — the agent's experiment protocol
- [[Antonella — Autoresearch System (prepare.py)]] — the evaluation harness
- [[Antonella — Three-Setups Framework]] — the framework being implemented
- [[Antonella — Trading Framework Overview]]

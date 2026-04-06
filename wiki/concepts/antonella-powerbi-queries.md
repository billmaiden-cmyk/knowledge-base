---
title: Antonella — Power BI Queries (Three-Setup Signal Queries)
created: 2026-04-05
updated: 2026-04-06
tags: [trading, antonella, power-bi, queries, kiet, three-setups, live-signals, backtest]
sources:
  - OneDrive / AI Hedge Fund / PowerBI Queries.pdf
stale: false
---

Detailed query specifications for Kiet to implement in Power BI — covering all three setup types in two modes (live signals and backtest), with SMA and VMA versions of each query.

> **Audience**: Kiet (implementation). Written March 2026.

## Two Query Modes

| Mode | Scope | Forward Returns | Purpose |
|------|-------|----------------|---------|
| **Mode A — Live Signals** | Last 60 days only | Not required | "What should I trade today?" — the live watchlist |
| **Mode B — Backtest** | Full historical dataset | Required as output columns | "What worked historically?" — learning and optimisation |

Mode A gives trade candidates. Mode B tells us whether the conditions are actually predictive.

**Key rule for Mode B**: Output ALL signals with no forward return filter in the query. Filtering is done interactively in Power BI so thresholds can be adjusted on the fly and both winners and losers can be examined.

## Pre-Requisite: Forward Returns

If not already computed, add for every stock-date:

| Column | Definition |
|--------|-----------|
| `fwd_return_5d` | (close 5 trading days later − close today) / close today |
| `fwd_return_15d` | Same, 15 days |
| `fwd_return_30d` | Same, 30 days |
| `fwd_return_60d` | Same, 60 days |
| `fwd_return_90d` | Same, 90 days |
| `fwd_return_max90d` | Maximum close-to-close return at any point within next 90 days |

Note: Mode A can run without forward returns using only current data, but they're needed for Mode B and for validating Mode A signals after the fact.

## Shared Setup Conditions

- **Constructive-to-ANTS window**: 15 days (tightened from original 60 days — custom ANTS detects accumulation inside the base, so both signals should fire close together)
- Each query has two versions: **SMA version** (existing conditions) and **VMA version** (being added this weekend). Run both side-by-side to compare.

---

## MODE A: LIVE SIGNALS

### Setup 1 — Live: Fresh Breakout

**Plain English**: Stocks forming a high-quality base, NOT in an established uptrend, with institutional accumulation inside the base.

**SMA Version** — all stock-dates in last 60 days where:
- Constructive score reached max ≥ 0.50
- ANTS score reached ≥ 10 within 15 days of that constructive max
- Price is BELOW SMA-50 at signal date
- Price is ABOVE SMA-10 at signal date (short-term repair confirmed)
- Volume ≥ 1.5× 50-day average

**VMA Version** — all stock-dates in last 60 days where:
- Constructive score reached max ≥ 0.50
- ANTS score reached ≥ 10 within 15 days of that constructive max
- `vma9_direction` is Flat or Rising at signal date
- Price within 1 ATR of VMA-9: `abs(close - vma_9) <= 1.0 × ATR14` at signal date — captures the U-turn crossover zone, ATR-normalised. Autoresearch tests k = 0.5, 0.75, 1.0, 1.25, 1.5
- Volume ≥ 1.5× 50-day average

**Columns to return**:

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

### Setup 2 — Live: Continuation Base

**Plain English**: Stocks in an uptrend consolidating in a tight base with institutional accumulation.

**SMA Version** — all stock-dates in last 60 days where:
- Constructive score max ≥ 0.50
- ANTS score ≥ 10 within 15 days
- Price is ABOVE SMA-50 at signal date
- Volume ≥ 1.5× average

**VMA Version** — replace SMA-50 condition with:
- Price is ABOVE VMA-9 AND VMA-9 is rising

**Additional columns** (all Setup 1 columns plus):

| Column | Description |
|--------|-------------|
| `dist_to_base_high` | (base_high − close) / base_high — how close to breakout level |
| `prior_advance_pct` | Price gain from low before base to base high |
| `close_pos` | Position within base range (0–1) |
| `base_number` | O'Neil base count (1, 2, 3, 4+) — informs position sizing |
| `prev_constructive_max` | If base_number ≥ 2, the constructive score of the previous base |

---

### Setup 3 — Live: Short Squeeze

**Plain English**: Stocks with elevated short interest where liquidity is drying up and some form of base is present.

**SMA Version** — all stock-dates in last 60 days where:
- Short interest ≥ 3% of float
- Days to cover ≥ 4
- Constructive score ≥ 0.35
- ANTS score ≥ 8 within 15 days

**VMA Version** — same, plus add `dist_vma9` and `vma9_direction` as output columns (no VMA filter applied — we want to see the data).

**Additional columns** (all Setup 1 columns plus):

| Column | Description |
|--------|-------------|
| `short_risk_rating` | Short vulnerability rating if available |
| `si_x_dryup` | `short_interest_pct × (1 − dryup_ratio)` — interaction term |
| `si_x_squeeze` | `short_interest_pct × (0.9 − atr_contract)` — interaction term |

---

## MODE B: BACKTEST

All three setups run on the **full historical dataset** with NO forward return filter in the query. All signals are output with forward return columns appended. Filtering is done interactively in Power BI.

**Additional forward return columns** (appended to all Mode A columns):

| Column | Description |
|--------|-------------|
| `fwd_return_5d` | Actual 5-day forward return |
| `fwd_return_15d` | Actual 15-day forward return |
| `fwd_return_30d` | Actual 30-day forward return |
| `fwd_return_60d` | Actual 60-day forward return |
| `fwd_return_90d` | Actual 90-day forward return |
| `fwd_return_max90d` | Maximum return achieved within 90 days |

### How to Use in Power BI

**Setup 1 (Fresh Breakout)**: Filter `fwd_return_max90d` interactively. Start unfiltered to see overall hit rate, then filter to ≥ 20% to see winner profile. Compare winners vs losers — what constructive scores, ANTS levels, MA distances, and SI levels distinguish success from failure?

**Setup 2 (Continuation Base)**: Same interactive filtering. Additionally: does `base_number` predict success? Filter to `base_number ≤ 2` vs `≥ 4` and compare returns. Does `dist_to_base_high` matter — do signals closer to the breakout level have better returns?

**Setup 3 (Short Squeeze)**: Filter on forward returns, then examine: do the interaction terms (`si_x_dryup`, `si_x_squeeze`) predict which signals worked? Sort by `si_x_dryup` descending. Is there a days-to-cover threshold separating winners from losers?

---

## Priority Order

**Immediate (trade now)**:
1. Forward returns — compute if not already in database
2. Mode A queries for Setups 1 and 2 (SMA versions first, VMA once available)
3. Mode A query for Setup 3

**This week (learn what works)**:
4. Mode B queries for all three setups
5. Base numbers — compute for all stocks; add as column on Setup 2 results

**Ongoing**:
6. Re-run Mode A weekly for new trade candidates
7. Feed Mode B results into autoresearch system as CSV for formal optimisation

## Output Format

- **Mode A**: One table per setup, sorted by `constructive_max` descending. This is the watchlist.
- **Mode B**: One table per setup, sorted by `constructive_max` descending, with all forward returns. Export to CSV for autoresearch system.

## Note on the 15-Day Window

Current best estimate. Autoresearch will test 5, 10, 15, 20, 30-day windows. The 15-day window captures Appen-like signals (ANTS fires 1–2 days after constructive max) while allowing slack for slower-developing setups.

## Related Pages

- [[Antonella — Action Priorities]] — where these queries sit in the build sequence (Priority 3)
- [[Antonella — Three-Setups Framework]] — the framework these queries implement
- [[Antonella — Autoresearch System (prepare.py)]] — consumes Mode B output as CSV
- [[Antonella — Autoresearch Agent Instructions]] — the agent that processes these results
- [[Antonella — Trading Framework Overview]]

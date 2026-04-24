---
title: Antonella — Autoresearch System (prepare.py)
created: 2026-04-05
updated: 2026-04-05
tags: [trading, antonella, autoresearch, python, backtesting, evaluation, karpathy, database]
sources:
  - OneDrive / AI Hedge Fund / prepare.py
  - raw/whatsapp/00003157-Finding What Works Autoresearch Final.docx
source_date: 2026-03
stale: false
---

`prepare.py` is the locked evaluation harness for the autoresearch trading system. It handles database connection, data loading, forward return lookup, train/test splitting, and the composite evaluation metric. The AI agent can only modify `strategy.py` — this file cannot be changed.

> This is based on Andrej Karpathy's autoresearch approach: an AI agent runs experiments overnight by modifying `strategy.py`, calling `prepare.py` to evaluate each experiment, and iterating toward the best signal configuration.

## Architecture

```
prepare.py  (LOCKED)         strategy.py  (agent modifies this)
├── load_data()              ├── generate_signals(data) → DataFrame
├── evaluate(signals)        │     returns: symbol + signal_date rows
├── run_experiment()         │     agent can change any condition/threshold
└── log_result()             └── agent cannot change what is evaluated
```

The agent modifies `strategy.py` to change filtering conditions, thresholds, and logic. `prepare.py` evaluates the signals against actual forward returns.

## Database Connection

```python
DB_CONNECTION_STRING = os.environ.get(
    "AUTORESEARCH_DB",
    "mssql+pyodbc://localhost/TradingDB?driver=ODBC+Driver+17+for+SQL+Server&trusted_connection=yes"
)
```

Database: `TradingDB` on local SQL Server. Configurable via environment variable.

## Key Configuration

| Parameter | Value | Notes |
|-----------|-------|-------|
| `TRAIN_TEST_SPLIT_DATE` | 2025-07-01 | Everything before = training; after = test |
| `PRIMARY_RETURN_HORIZON` | 15 days | Primary evaluation metric |
| `MIN_SIGNAL_COUNT` | 20 | Below this = invalid strategy |
| `RESULTS_FILE` | results.tsv | Append-only experiment log |

## Data Schema (daily_signals table)

Key columns loaded from the database:

| Column | Description |
|--------|-------------|
| `symbol`, `trade_date` | Identifiers |
| `constructive_score` | Composite base quality (0–1) |
| `tight_weeks_last3/5`, `tight_streak` | Tightness metrics |
| `dryup_ratio`, `dry_weeks_last5` | Volume dry-up |
| `atr_contract` | ATR14/ATR50 compression ratio |
| `dist_sma10`, `dist_sma50` | MA coherence |
| `close_pos`, `base_depth` | Position in base |
| `ants_score` | Custom ANTS score |
| `up_days_10`, `accum_days_10` | ANTS components |
| `short_interest_pct` | Short interest % |
| `short_interest_5d_change` | SI trend |
| `days_to_cover` | DTC |
| `fwd_return_5d/15d/30d/60d/90d` | Pre-computed forward returns |
| `fwd_return_max90d` | Best return within 90d |

## Derived Columns (computed on load)

- `dist_sma50_signed`, `dist_sma10_signed`, `dist_sma200_signed` — signed distance to MAs
- `above_sma10/50/200` — boolean MA position flags
- `is_pocket_pivot` — True if today is an up day with volume > max prior 10-day down-day volume
- `max_down_vol_10d` — rolling max of down-day volume over 10 days

## Evaluation Function

```python
evaluate(signals: DataFrame, dataset: str) → dict
```

Signals DataFrame must have columns: `symbol`, `signal_date`.

### Composite Metric

```
metric = profit_factor × sqrt(n_signals) × (1 - abs(max_drawdown))
```

- `profit_factor` = sum_wins / abs(sum_losses) — are winners bigger than losers?
- `sqrt(n_signals)` — enough opportunities? sqrt prevents rewarding quantity over quality
- `(1 - abs(max_drawdown))` — tail risk penalty (capped at 0.99 to prevent negatives)

### Full Result Dictionary

| Field | Meaning |
|-------|---------|
| `metric` | Composite score (agent maximises this) |
| `n_signals` | Valid signals count |
| `hit_rate` | Fraction with positive return |
| `avg_return` | Mean 15-day forward return |
| `median_return` | Median 15-day forward return |
| `profit_factor` | Sum wins / abs(sum losses) |
| `max_drawdown` | Worst single-signal return |
| `best_trade` | Best single-signal return |
| `total_return` | Sum of all forward returns |

## Results Logging

Each experiment is appended to `results.tsv` with:
- Experiment number + timestamp
- Hypothesis (what the agent changed)
- Whether the configuration was kept
- All metric fields

`get_results_history()` reads the full experiment log for the agent to learn from.

## The Agent Loop

```
1. Agent reads results.tsv (history of past experiments)
2. Agent forms a hypothesis about what to try next
3. Agent modifies strategy.py
4. Agent calls run_experiment()
5. prepare.py evaluates signals against training data
6. If metric improves → agent keeps the change
7. Agent logs result and repeats
```

The agent NEVER calls `run_test_validation()` — that is reserved for final human validation to prevent test set contamination.

## Pocket Pivot Detection

`is_pocket_pivot` is pre-computed:
```python
is_pocket_pivot = (today is an up day) AND (today's volume > max down-day volume over last 10 days)
```
This is the Gil Morales/O'Neil pocket pivot definition, available as a column for `strategy.py` to use.

## Three-Setup Testing

The Three-Setups Framework adds three separate parameter blocks to `strategy.py` — one per setup type — each with different conditions, thresholds, and metrics. The agent can run them in parallel overnight and surface which setup type produces the best returns, and which conditions within each setup are genuinely predictive.

## Strategic Rationale (Finding What Works Paper)

The "Finding What Works" paper (March 2026) provides the strategic case for autoresearch. Key arguments: *(source: raw/whatsapp/00003157-Finding What Works Autoresearch Final.docx)*

**Why autoresearch, not backtesting:** Backtesting answers "how would this strategy have performed?" — you define the strategy, then test. Autoresearch *discovers* the strategy itself. The agent can add conditions you didn't think of, remove conditions you assumed were important, reverse sequences, and combine metrics in ways you wouldn't have hypothesised.

**Throughput advantage:** Each experiment is a database query (2-5 seconds), not neural network training (5 minutes). Expected throughput: 250-500 experiments per overnight run at ~$5-25 cost. This is more in one hour than a human completes in a week.

**Categories of discovery the agent is likely to make:**
1. **Interactions between metrics** — e.g., SMA-50 position matters differently depending on short interest (validated by Appen analysis)
2. **Optimal thresholds** — maybe 0.58 and 12 work better than 0.50 and 10
3. **Irrelevant conditions** — removing metrics that don't improve the score simplifies and reduces overfitting
4. **Alternative sequences** — maybe ANTS fires first, then base consolidation, then entry on breakout
5. **Sub-component superiority** — maybe AccumDays10 alone outperforms the full ANTS composite
6. **Strategies nobody imagined** — after 300 experiments, something built from sub-components combined in ways never considered

**Build requirements:**
| Component | Status |
|-----------|--------|
| SQL database with all metrics | Exists |
| Constructive Base scores | Computed |
| ANTS scores and sub-components | Computed |
| MA values and distances | Computed (may need slopes + signed distances) |
| Short interest data | Available (confirm 5d change + DTC present) |
| Forward returns (5/15/30-day) | May need one-time batch computation |

## Related Pages

- [[Antonella — Three-Setups Framework]] — the strategy framework the agent tests
- [[Antonella — Constructive Base Detector Spec]] — the base quality inputs
- [[Antonella — ANTS Filter]] — the ANTS score inputs
- [[Antonella — Trading Framework Overview]]

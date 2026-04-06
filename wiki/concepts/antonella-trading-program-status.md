---
title: Antonella — Trading Program Status (WIP)
created: 2026-04-05
updated: 2026-04-06
tags: [trading, antonella, status, wip, work-plan, three-setups, autoresearch]
sources:
  - OneDrive / AI Hedge Fund / Action Priorities.pdf
  - OneDrive / AI Hedge Fund / Three_Setups_Framework.docx
  - Google Drive / Bill and Antonella comms / (all documents)
stale: false
---

Current status and work plan for the Antonella/Bill quantitative trading system. This page tracks what is done, what is in progress, and what comes next.

> **Last reviewed**: 2026-04-06 (via [[Trading Sync — 2026-04-06]])

## System Architecture (Complete)

The system is a 4-layer signal architecture:

```
Layer 1: Market Direction Gate    → ASX200 regime (0–3 score) controls position sizing
Layer 2: Three Setup Types        → Fresh Breakout / Continuation Base / Short Squeeze
Layer 3: Shared Signal Tools      → Constructive Base Detector + ANTS Score + VMA/KAMA
Layer 4: Autoresearch Optimiser   → Claude Code agent tests 250+ parameter variants overnight
```

All methodology is fully designed. The gap is implementation — getting from design to live signals.

## What Is Done

| Component | Status | Detail |
|-----------|--------|--------|
| Core methodology (13 framework components) | ✅ Complete | ANTS, constructive base, short interest/ATR, base labelling, short trap, event-driven, market direction, ascending base, takeover target, short risk — all specified |
| Three-Setups Framework | ✅ Designed | Setup 1 (Fresh Breakout), Setup 2 (Continuation), Setup 3 (Short Squeeze) — qualifying conditions, entry signals, position sizing all defined |
| TradingDB (SQL Server) | ✅ Live | `daily_signals` table with price, volume, constructive scores, ANTS, short interest, MAs |
| Forward returns | ✅ Computed | `fwd_return_5d/15d/30d/60d/90d/max90d` for all stock-dates |
| `prepare.py` evaluation harness | ✅ Ready | Locked file; metric = `profit_factor × sqrt(signals) × (1 − abs(max_drawdown))`; train/test split at 2025-07-01 |
| Autoresearch agent instructions | ✅ Written | 5-phase, 250-experiment protocol with phased approach from single-variable → robustness |
| Power BI query specifications | ✅ Written | Mode A (live signals) + Mode B (backtest) for all 3 setups, SMA and VMA versions |
| Action Priorities (build order) | ✅ Defined | 4-priority sequenced plan |

## What Is In Progress

### Priority 1: New Database Columns — Owner: Kiet

| Column | Status | Blocks |
|--------|--------|--------|
| Forward returns (5d/15d/30d/60d/90d/max90d) | ✅ Done | — |
| `vma_9` | ✅ Done (VMA-9 only; VMA-18/27 deferred to autoresearch) | — |
| `dist_vma9` (signed %) | ⚠️ Confirm with Kiet | VMA query conditions |
| `vma9_direction` (Rising/Flat/Falling) | ⚠️ Confirm with Kiet — if computed, confirm formula is ATR-normalised | Setup 1 VMA version |
| `base_number` (1, 2, 3, 4+) | ⚠️ Confirm with Kiet | Setup 2 position sizing |

*(Status updated 2026-04-06 per trading-sync chat. Bill confirmed VMA-9 done. VMA-18/27 deferred — VMA-9 sufficient for v1.)*

### Priority 2: Constructive Base v1 Improvements — ✅ DONE

Three improvements to the shared constructive base detector — all implemented by Kiet:

| Change | Description | Status |
|--------|-------------|--------|
| Distribution penalty | Penalises bases with heavy selling weeks (close down + volume up in lower 40% of range) | ✅ Done |
| Tight streak component | Scores consecutive tight weeks separately from scattered counts | ✅ Done |
| ATR-normalised tightness | Replaced fixed 6% range threshold with `range ≤ k × ATR` | ✅ Done |

*(Status updated 2026-04-06 per trading-sync chat. Bill confirmed all three implemented by Kiet. The constructive_score in the DB now includes these improvements.)*

## What Comes Next

### Priority 3: Power BI Queries — Owner: Kiet (after Priority 1)

Build 12 queries:

**Mode A — Live Signals** (last 60 days, no forward returns needed — this is the watchlist):

| Setup | Constructive | ANTS | Window | Key Condition | Position Size |
|-------|-------------|------|--------|---------------|---------------|
| 1. Fresh Breakout | ≥ 0.50 | ≥ 10 | 15 days | Below SMA-50, vol ≥ 1.5× | Half |
| 2. Continuation | ≥ 0.50 | ≥ 10 | 15 days | Above SMA-50, vol ≥ 1.5× | Full |
| 3. Short Squeeze | ≥ 0.35 | ≥ 8 | 15 days | SI ≥ 3%, DTC ≥ 4 | Quarter to half |

Each setup has SMA and VMA versions = 6 live queries.

**Mode B — Backtest** (full history, all signals + forward returns): Same 3 setups × 2 versions = 6 queries. No filtering in query — filter interactively in Power BI.

**Output**: Mode A → trade at reduced size. Mode B → feed to autoresearch as CSV.

### Priority 4: Autoresearch — Owner: Kiet (infra) + Claude Code (agent)

1. Set up Python environment + git repo for `strategy.py`
2. Connect `prepare.py` to actual database column names
3. Run first overnight baseline (constructive ≥ 0.50, ANTS ≥ 10, 15-day window)
4. Agent runs 250–500 experiments across 5 phases

**Open questions autoresearch will resolve**:
- Optimal ANTS window (5, 10, 15, 20, 30 days)
- Optimal thresholds per setup type
- Whether VMA outperforms SMA or layering adds value
- Whether pocket pivot adds anything over AccumDays10
- Whether the 3 proposed v1 changes actually improve returns
- Optimal scoring weights per setup
- Which conditions are signal vs noise

### Priority 1.5: Market Direction Model — Owner: TBD

**This is the one genuine gap in the current plan.** The Three-Setups Framework references market regime as a "sizing modifier" but never implements it. Without it, signals fire during corrections with no drawdown protection.

**What needs to happen**:
1. Compute daily market direction score for ASX200:
   - Price vs 50-DMA and 200-DMA
   - Distribution day count (rolling 25 sessions)
   - Follow-Through Day detection
2. Store `market_direction_score` (0–3) and `market_regime` in database
3. Apply as position sizing modifier to all Mode A signals:
   - Score 3 (confirmed uptrend): standard sizing
   - Score 2 (under pressure): reduce by 50%
   - Score 0–1 (correction/rally attempt): reduce by 75%, raise constructive threshold

**When**: After Priority 3 queries go live but before committing to full-size positions.

## Design Artifacts Not Required for Phase 1

These earlier Antonella documents were design explorations that fed into the Three-Setups Framework. They are **not separate work items** — their concepts are already absorbed or can be tested via autoresearch:

| Concept | Status | Notes |
|---------|--------|-------|
| Short Trap Index | Absorbed into Setup 3 | `si_dry_interaction` and `si_squeeze_interaction` capture the core mechanism. Full 6-component formula can be tested in autoresearch against Setup 3's simpler binary thresholds. |
| Ascending Base Filter | Absorbed into Setup 2 | Setup 2 already requires above SMA-50, dist_to_base_high ≤ 8%, tightness, dry-up. Slope and higher-lows conditions can be tested as autoresearch bonus experiments. |
| Event-Driven Post-Event Model | Genuinely additive but deferrable | Requires event classification (earnings, capital raises) not derivable from price/volume. Phase 2 enhancement if event data becomes available. |
| Takeover Target Filter | Specialised overlay, deferrable | Needs IC_multiple data not in database. Nice-to-have after core system is validated. |
| Short Risk Model | Separate system (short-side) | Entire short-entry framework — different logic, different risk management. Phase 3+ if Bill wants to trade shorts. |

## Timeline

| Week | Milestone | Owner |
|------|-----------|-------|
| Week 1 | Priority 1 complete (VMA + base numbers in DB) | Kiet |
| Week 2 | Priority 3 queries live in Power BI | Kiet |
| Week 2 | Start trading Mode A signals at reduced size | Bill |
| Week 2–3 | First autoresearch overnight run | Kiet + Claude Code |
| Week 3–4 | Market Direction Model built and applied | TBD |
| Week 4–5 | Validate best autoresearch config on test set | Bill + Antonella |
| Week 5+ | Lock thresholds, update queries, move to full sizing | All |

## Key Dependencies

```
Priority 1 (VMA + base numbers)
  ├→ blocks Priority 3 (queries need VMA columns)
  ├→ blocks Priority 4 (agent needs all columns)
  └→ does NOT block reduced-size trading on SMA-only queries

Priority 3 (Power BI queries)
  ├→ produces live watchlist (start trading)
  └→ produces Mode B CSV (feeds autoresearch)

Priority 4 (Autoresearch)
  └→ resolves all open parameter debates
  └→ validates or rejects Priority 2 proposed changes

Priority 1.5 (Market Direction)
  └→ needed before full-size positions
  └→ can run parallel to Priority 4
```

**Single most important thing right now**: Confirm with Kiet that `vma9_direction`, `dist_vma9`, `base_number`, and `sma_10` are computed. Then update Setup 1 queries per [[Kiet — Setup 1 Query Changes & New Computed Fields]] and begin Priority 3 (Power BI queries).

*(Updated 2026-04-06. Setup 1 queries revised: SMA version added close > SMA-10; VMA version changed to vma9_direction IN (Flat, Rising) + ABS(close - vma_9) <= 1.0 × ATR14. See [[Kiet — Setup 1 Query Changes & New Computed Fields]] for Kiet's implementation spec.)*

## Related Pages

- [[Antonella — Three-Setups Framework]] — the core framework
- [[Antonella — Action Priorities]] — the sequenced build plan
- [[Antonella — Power BI Queries]] — query specifications for Kiet
- [[Antonella — Autoresearch System (prepare.py)]] — evaluation harness
- [[Antonella — Autoresearch Agent Instructions]] — agent experiment protocol
- [[Antonella — Market Direction Model]] — the gap that needs filling
- [[Antonella — Trading Framework Overview]] — all framework components

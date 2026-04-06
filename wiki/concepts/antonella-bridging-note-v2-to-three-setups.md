---
title: Antonella — Bridging Note (v2 to Three-Setups Framework)
created: 2026-04-05
updated: 2026-04-05
tags: [trading, antonella, three-setups, v2, bridging-note, architecture, design]
sources:
  - OneDrive / AI Hedge Fund / From_v2_to_Three_Setups_Bridging_Note.docx
stale: false
---

This internal note maps Antonella's Constructive Base v2 contributions into the Three-Setups Framework that evolved from her work. It explicitly credits her contributions, clarifies what was adopted as-is vs rearchitected, and explains the reasoning for each decision.

> **Authorship**: Bill's internal note, March 2026. Documents the intellectual lineage from Antonella's v2 → the Three-Setups Framework.

## What Antonella Got Right

### Universal Base Quality Improvements (adopted for shared detector)

| Contribution | What It Does | Status |
|---|---|---|
| **Distribution penalty** | Penalises bases with down-weeks on high volume in last 5 weeks. Catches bases that look tight but hide institutional selling — a genuine gap in v1. | Adopted into shared detector |
| **Tight streak as separate component** | Three *consecutive* tight weeks > three scattered tight weeks. Consecutiveness signals sustained institutional control. | Adopted into shared detector |
| **Relative tightness (ATR-normalised)** | Replaces fixed 6% weekly range threshold with `weekly_range ≤ k × ATR`. v1 used ratios everywhere else (dryup_ratio, atr_contract) — tightness was the only fixed absolute, creating unfair cross-stock comparisons. | Adopted into shared detector |

### Setup-Specific Contributions (not in shared detector)

| Contribution | Status | Reason |
|---|---|---|
| `dist_to_base_high ≤ 0.08` | Setup 2 only | Would penalise Setup 1 where base is deep by design. Appen's close_pos was 0.16 at its constructive max — proximity requirement would have destroyed its score. |
| Tighter `close_pos` (0.65 vs 0.50) | Flagged for autoresearch | May reduce signal count too much on ASX. Agent tests 0.50, 0.55, 0.60, 0.65 per setup type. |
| Median volume for dry-up | Flagged for autoresearch | More robust to single-day volume spikes; agent compares mean vs median. |

### The Two-Model Insight (most important intellectual contribution)

Antonella's most significant insight: **one model cannot serve both early-turn setups and proper constructive bases**. She designed:

- **Early Cover Turn (ECT)**: Looser trend rules, heavy emphasis on squeeze, dry-up, short pressure, MA repair. Catches stocks still below SMA-50/200 where supply is exhausting.
- **True Constructive Base (TCB)**: Stricter trend rules, emphasis on base structure, right-side position, proximity to highs. Catches classic O'Neil breakout candidates.

The Three-Setups Framework extends this: her ECT → two sub-types (Setup 1: Fresh Breakout and Setup 3: Short Squeeze). Her TCB → Setup 2 (Continuation Base). The two-model split was her idea first.

### The si_dry_interaction Concept (original analytical contribution)

Antonella identified that `si_score × dry_score` is a **multiplicative interaction**, not just another metric:
- High SI with ample liquidity: not dangerous for shorts
- Dry volume without short interest: not a squeeze setup
- Only the combination creates the asymmetric opportunity

This is the core signal for Setup 3 (Short Squeeze) in the framework.

## Where Her v2 Context Requirements Were Rearchitected

Antonella's v2 added context requirements as **hard filters inside the detector**:
- `prior_run_pct >= 0.30`
- `trend_ok` (2 of 3 conditions)
- `close > SMA200`

Her own annotations flagged the tension: these would exclude shorted stocks and early U-turns like Appen.

The Three-Setups Framework resolves this by treating context as a **classification layer** rather than a filter:

| Antonella's v2 Condition | In Framework |
|---|---|
| `prior_run_pct >= 0.30` | Required for Setup 2 only. Not for Setups 1 or 3 (base depth and stock position determine setup type instead). |
| `trend_ok` (2 of 3) | Used for classification: stocks passing → Setup 2. Stocks failing → Setups 1 or 3. |
| `close > SMA200` | Informational context for all setups. Not a hard filter. Stocks below SMA-200 + declining SI can still qualify for Setups 1 and 3. |
| Short pressure overlay | Kept separate (her Option A). Adopted as primary driver for Setup 3, conviction modifier for Setup 1. |

The base quality score remains **stage-agnostic** — measuring tightness, dry-up, squeeze, proximity, distribution regardless of where the stock sits. Context determines which setup the signal belongs to.

## What the Framework Adds Beyond v2

| Addition | Description |
|---|---|
| **VMA/KAMA** | Adaptive moving average at 3 sensitivity levels. Not in v2. Being tested alongside SMAs (not replacing them) — hypothesis to be validated empirically. |
| **Base numbering** | O'Neil base count (Base 1, 2, 3, 4+) as sizing modifier within Setup 2. |
| **Position sizing by setup type** | Setup 1: half; Setup 2: full; Setup 3: quarter to half. Antonella's v2 didn't address sizing. |
| **Autoresearch testing** | All parameters, thresholds, and weights (including Antonella's proposed weights) tested empirically overnight. Resolves debates with data rather than intuition. |
| **Market regime as modifier** | Not in v2. Reduces position sizes in down regime but doesn't block entries (critical for Stage 1 setups that form during broad market weakness). |

## Proposed Weight Structure

Antonella proposed TCB model weights:
- Tightness 20%, Streak 10%, Dry 15%, Dry weeks 5%, Squeeze 15%, Right side 10%, Proximity 10%, MA 5%, Maturity 5%, Trend 10% **minus** Distribution penalty 10%

Original v1 weights:
- Tightness 25%, Dry 25%, Squeeze 25%, MA 15%, Maturity 10%

**Framework position**: Neither set of weights is pre-decided as correct. Both are starting points for the autoresearch agent to optimise per setup type. Antonella's weights are the starting point for Setup 2 (her TCB model). v1 weights are the starting point for Setups 1 and 3.

## Operational Changes Agreed

| Change | Detail |
|---|---|
| Constructive-to-ANTS window | Tightened from 60 → **15 days**. Autoresearch tests 5/10/15/20/30 days. |
| VMA added alongside SMA | Not replacing SMA. Three sensitivity levels. Both versions of each query run side-by-side. |
| Setup-specific thresholds | Setup 1/2: constructive ≥0.50, ANTS ≥10. Setup 3: constructive ≥0.35, ANTS ≥8. |
| Market regime | Sizing modifier, not a gate. |
| Detector improvements | Three from v2 adopted: distribution penalty, tight streak, ATR-normalised tightness. |

## Summary of Antonella's Contributions

| Category | Contribution | Treatment |
|---|---|---|
| **Universal detector** | Distribution penalty, tight streak, ATR-normalised tightness | Adopted into shared detector |
| **Setup-specific** | Proximity to highs, tighter close_pos | Setup 2 only / autoresearch testing |
| **Intellectual foundation** | Two-model insight (ECT vs TCB) | Extended to three setups |
| **Original concept** | si_dry_interaction | Core of Setup 3 |
| **Context requirements** | prior_run, trend_ok, SMA conditions | Rearchitected as classification, not filter |

> "The three-setup framework is Antonella's v2 thinking taken to its logical conclusion: if different setups need different rules, then make that explicit by defining the setups and specifying what matters for each one."

## Related Pages

- [[Antonella — Three-Setups Framework]] — the full framework document
- [[Antonella — Constructive Base Detector Spec]] — Antonella's v2 technical spec
- [[Antonella — Constructive Base Score]] — the scoring system
- [[Antonella — Short Trap Index]] — the si_dry_interaction model
- [[Antonella — Autoresearch System (prepare.py)]] — the testing harness
- [[Antonella — Trading Framework Overview]]

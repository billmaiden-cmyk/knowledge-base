---
title: "Antonella — Three Setups × KAMA Regime Discussion"
created: 2026-04-06
updated: 2026-04-06
tags: [trading, antonella, three-setups, kama, vma, regime-filter, discussion-paper]
sources:
  - raw/whatsapp/00003354-Discussion_Three_Setups_x_KAMA_Regime.docx
source_date: 2026-04
---

Discussion paper reconciling Bill's Three-Setup Framework with Antonella's independently developed KAMA regime filter. Both address the same problem: the constructive base detector can score well on stocks still in structural downtrends. The paper maps where the two approaches converge, differ, and what the combined system looks like. *(source: raw/whatsapp/00003354-Discussion_Three_Setups_x_KAMA_Regime.docx)*

## The Problem Both Approaches Solve

The constructive base detector (v1) is deliberately stage-agnostic — it scores a base near 52-week lows the same as one near all-time highs. This creates a failure mode: stocks score well on local base quality while the broader chart is still declining.

- **Antonella's framing:** "You are currently seeing high base scores but chart declining. That happens because your base model is local (pattern-based) but trend is global (regime-based). KAMA bridges that gap."
- **Framework's framing:** Separate the problem into three setups based on what drives the move. A stock below SMA-50 with a high base score isn't a false positive — it's a Setup 1 (Fresh Breakout) rather than a Setup 2 (Continuation Base).

**These are compatible, not competing.** The framework classifies; the KAMA filter adds context within each classification.

## KAMA/VMA Database Columns

Four columns derived from VMA-9, proposed as computed database additions:

| Column | What It Measures | Detail |
|--------|-----------------|--------|
| `kama_slope` | Is adaptive MA rising, flat, or falling? | Uses smoothed 3-bar average to reduce noise |
| `price_above_kama` | Is price holding above adaptive MA? | Counts last 5 days above VMA-9 (3+ = holding) |
| `base_above_kama` | Is entire recent base above adaptive MA? | Lowest close in last 5 days still above VMA-9 |
| `kama_first_turn` | First bar where VMA transitions falling → rising? | Detects inflection point; often earliest signal of bottoming |

## Convergence: Four Types = Three Setups

Antonella's four signal types map directly onto the framework:

| Antonella's Type | Characteristics | Framework Setup |
|-----------------|-----------------|-----------------|
| Type 1: Explosive Breakout | High base + KAMA just turned up + high SI + volume spike | Setup 1 (Fresh Breakout) or Setup 3 (Short Squeeze) |
| Type 2: Institutional Accumulation | High base + KAMA rising slowly + low SI + quiet liquidity | Setup 2 (Continuation Base) |
| Type 3: Trap / Declining Chart | High base + KAMA falling + price below KAMA | Not a setup — filtered out |
| Type 4: Pre-Breakout | Moderate base + KAMA flat but improving + SI building | Setup 1 in formation phase (watchlist) |

## Key Difference: Filter vs Classifier

- **Antonella's approach (filter):** Binary — rejects bases where KAMA is falling. Scored version reduces composite when KAMA is negative.
- **Framework approach (classifier):** Uses KAMA/VMA as classification input. A stock with falling KAMA isn't rejected — it's classified as Setup 1 or Setup 3 with different qualifying conditions. Setup 1 specifically targets stocks breaking out of downtrends where KAMA is just turning.

**Resolution:** Both can coexist. Compute KAMA score AND setup classification. Use setup type to determine which KAMA requirements apply (strict for Setup 2, relaxed for Setup 1).

## KAMA Conditions by Setup Type

| Condition | Setup 1 (Fresh Breakout) | Setup 2 (Continuation) | Setup 3 (Short Squeeze) |
|-----------|-------------------------|----------------------|------------------------|
| `kama_slope` | Just turned (critical signal) | Rising required (trend support) | Less relevant (SI drives) |
| `price_above_kama` | Just crossing above | Sustained above (3+ days) | Informational |
| `base_above_kama` | Unlikely (breaking out from below) | Required (base in uptrend) | Informational |
| `kama_first_turn` | Key entry signal | Informational | May coincide with covering |

## Open Discussion Items

1. **Score vs Classifier?** Antonella proposes composite scoring (0.4×slope + 0.3×price_above + 0.3×base_above) blended into one ranked list. Framework proposes three separate lists by setup type. Possibly both.

2. **Should `kama_slope >= 0` be required for Setup 2?** Framework currently uses above/below SMA-50. Should we add `kama_slope = rising` as additional requirement, or let autoresearch test it?

3. **How do v1 changes (distribution penalty, tight streak, ATR-normalised tightness) interact with KAMA?** These are base quality improvements that don't interact with regime directly. Question: should KAMA modify the constructive score itself or sit alongside as a separate layer?

4. **Antonella's composite weights:** 35% base quality + 25% KAMA regime + 20% SI pressure + 20% liquidity. Reasonable starting points — autoresearch can test whether these weights add predictive value.

## Proposed Next Steps

1. Add four KAMA-derived columns to database once VMA-9 is computed (already in Kiet's query document)
2. Include in all Mode A (live signal) and Mode B (backtest) query outputs
3. Run backtest: do signals where `kama_slope = rising` AND `base_above_kama = true` have better forward returns?
4. Discuss whether `kama_slope = rising` should be hard requirement for Setup 2 or informational column tested by autoresearch
5. Test Antonella's composite scoring vs framework's setup-specific approach via autoresearch

## Cross-References

- [[antonella-three-setups-framework]] — The three-setup classification this paper extends
- [[antonella-constructive-base-score]] — The base detector whose limitations motivated this work
- [[antonella-autoresearch-system]] — The autoresearch engine that will empirically test both approaches
- [[antonella-bridging-note-v2-to-three-setups]] — How v2 base improvements map to the framework
- [[antonella-trading-program-status]] — Current build status and priorities

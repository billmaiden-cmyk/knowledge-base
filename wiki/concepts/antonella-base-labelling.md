---
title: Antonella — Base Labelling (O'Neil Base Numbering)
created: 2026-04-05
updated: 2026-04-05
tags: [trading, antonella, base-labelling, o-neil, base-count, google-sheets]
sources:
  - Google Drive / Bill and Antonella comms / Base labelling
stale: false
---

Base labelling implements the O'Neil base-count system in Google Sheets, tracking which "base number" a stock is currently forming. Base count matters because early-stage bases (1st and 2nd) have higher success rates; later-stage bases (3rd and 4th) are more likely to fail.

## O'Neil Base Numbering Rules

1. Start from a prior significant high
2. Price must decline ≥ 8% from that high to "reset" the base count
3. When price recovers and breaks out above the prior high, a new base count begins
4. Each subsequent consolidation after the breakout is the next numbered base

**Example sequence:**
- Stock makes all-time high → first base forms → breakout above high = **Base 1**
- Consolidates again → breakout → **Base 2**
- Consolidates again → breakout → **Base 3** (late stage, more risky)

## Google Sheets Implementation

The formula is designed for data sorted newest-first (most recent row at top):

### Base Detection (is this week the start of a new base?)

A base starts when price has drawn down ≥ 8% from a recent pivot high. The formula tracks:

```excel
=IF(drawdown_from_high >= 0.08, TRUE, FALSE)
```

### Base Count Formula

For newest-first data:

```excel
=IF(F3 = TRUE, COUNTIF(F3:F, TRUE), G4)
```

Where:
- `F` = base-start flag column
- `G` = base count column
- `F3 = TRUE` means "this row is a base start" → count all TRUE flags from this row downward
- `G4` = carry forward the count from the prior row if not a base start

This formula propagates the count across all rows of a given base.

## Why Base Count Matters

| Base Number | Historical Success Rate | Notes |
|-------------|------------------------|-------|
| 1st base | Highest (~60–70%) | Fresh breakout from long consolidation |
| 2nd base | Good (~50–55%) | Post-first breakout rest |
| 3rd base | Lower (~35–45%) | Stock is "late stage" |
| 4th+ base | Weak (<30%) | High failure risk, larger pullbacks likely |

Late-stage bases also tend to fail more violently — a breakout from a 4th base that fails can result in a 30–40% decline (the "climax run and failure" pattern).

## Integration

Base labelling feeds into:
- **[[Antonella — Constructive Base Score]]** — early bases score higher
- **[[Antonella — ANTS Filter]]** — base count is a qualifying filter (prefer base 1–2)
- Position sizing decisions: smaller size on later-stage bases

## Related Pages

- [[Antonella — Constructive Base Score]]
- [[Antonella — ANTS Filter]]
- [[Antonella — Ascending Base Filter]]
- [[Antonella — Trading Framework Overview]]

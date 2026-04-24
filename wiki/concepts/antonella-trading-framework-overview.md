---
title: Antonella — Trading Framework Overview
created: 2026-04-05
updated: 2026-04-05
tags: [trading, antonella, framework, o-neil, google-sheets, asx, master-score]
sources:
  - Google Drive / Bill and Antonella comms / (all documents)
  - Google Drive / Bill and Antonella comms / Outstanding items
stale: false
---

Antonella's trading framework is a systematic, quantitative stock selection system built on O'Neil/IBD methodology, extended with short interest microstructure analysis. It is implemented primarily in Google Sheets and designed for ASX stocks, with potential extension to US and European markets.

## Collaborators

- **Antonella** — trading methodology designer and AI model architect
- **Bill Maiden** — investor and framework co-developer
- Supporting developers: Kiet, Sebastian

## Philosophy

The framework combines:
1. **O'Neil/IBD price-volume analysis** — base patterns, breakouts, MA structure
2. **Short interest microstructure** — SI regimes, cover dynamics, squeeze setups
3. **Event-driven post-event absorption** — stocks digesting shocks before moving higher
4. **Market regime gating** — no individual stock entries without market confirmation

## The Signal Architecture

### Layer 1: Market Direction Gate
[[Antonella — Market Direction Model]] must confirm a favourable regime (score ≥ 2) before any individual stock trades are taken.

### Layer 2: Stock Selection Scores

| Score | Formula | Weight in Master Score |
|-------|---------|----------------------|
| ANTS Score | Accumulation + trend strength | 35% |
| Cover Score | Short interest falling (shorts covering) | 30% |
| Post-Event Base Score | Post-event absorption quality | 35% |

```
Master_Score = 0.35 × ANTS + 0.30 × Cover + 0.35 × PostEvent
```

### Layer 3: Quality Filters

| Filter | Purpose |
|--------|---------|
| [[Antonella — Constructive Base Score]] | Base quality (depth, tightness, position, MAs) |
| [[Antonella — Ascending Base Filter]] | Highest-quality O'Neil base pattern detector |
| [[Antonella — Base Labelling]] | Base count (prefer base 1–2) |
| [[Antonella — Takeover Target Filter]] | Stealth accumulation / M&A candidates |

### Layer 4: Risk Models

| Model | Purpose |
|-------|---------|
| [[Antonella — Short Risk Model]] | Identifies short setups; regime classifier |
| [[Antonella — Short Trap Index]] | Detects when short positions are about to be squeezed |
| [[Antonella — Short Interest & ATR]] | Quantifies SI × ATR compression (coiled spring) |

## Master Score Filter Logic

The primary scan filter (per the Outstanding items document):

> Show all stocks that:
> - Reached a constructive score max > 0.5 in the last 60 days
> - Within 60 days of that max, hit an ANTS score above threshold

This two-condition filter identifies stocks that first formed a constructive base, then triggered an accumulation signal — the classic O'Neil "buy on the breakout from a sound base" pattern, quantified.

## Google Sheets Architecture

The main spreadsheet has:
- **DATA tab**: Raw price/volume data per stock (newest first)
- **SCAN tab**: LET formula that filters, scores, and ranks all candidates
- **Helper columns** for each sub-score component

Key column references:
| Column | Data |
|--------|------|
| E | Close price |
| M | SMA10 |
| N | SMA50 |
| O | SMA200 |
| T | ATR10/ATR50 ratio |
| U | Volume/SMA50Volume ratio |
| BT | Short interest % |

## Case Studies

- **Appen (APX)**: Post-event absorption with tight zone, constructive score hit on December 18 at $0.71
- **Dominoes Pizza (DMP)**: Two-phase short interest dynamic; constructive max 0.52 on Oct 3, 2025 — illustrating incomplete base vs. early stabilisation

## Outstanding Development Items

As of the Outstanding Items document, the framework needed:

1. **Better filter conditions** — combining constructive score max + subsequent ANTS trigger in a single time-windowed query
2. **Dynamic Hedge Ratio** — a position sizing model (exists as a separate Word document)
3. **Short Comfort vs Trap Index** — now designed in [[Antonella — Short Trap Index]]
4. **Market direction integration** — gating individual stock signals by market regime

## Related Pages

- [[Antonella — ANTS Filter]]
- [[Antonella — Constructive Base Score]]
- [[Antonella — Short Interest & ATR]]
- [[Antonella — Event-Driven Opportunities]]
- [[Antonella — Ascending Base Filter]]
- [[Antonella — Short Risk Model]]
- [[Antonella — Market Direction Model]]
- [[Antonella — Base Labelling]]
- [[Antonella — Takeover Target Filter]]
- [[Antonella — Short Trap Index]]
- [[Antonella — Short Interest Case Study (DMP)]]

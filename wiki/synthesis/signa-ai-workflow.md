---
title: Signa.ai — Structured Workflow for Bill
created: 2026-04-19 16:00 AEST
updated: 2026-04-19 16:00 AEST
tags: [trading, signal-workflow, signa, technical-analysis, risk-management, swing-trading, position-sizing]
sources:
  - Trading & Investing/Signa_IMNM_ActionCard.png
  - Trading & Investing/Signa_IMNM_ActionCard (1).png
  - Trading & Investing/Signa_IMNM_share.png
  - Trading & Investing/Shardi B's CMT Trading Agent Project - Comprehensive Research.md
source_date: 2026-04-19
---

A step-by-step protocol for using [[Signa.ai]] effectively. Derived from Signa's internal AI assistant (Sage) describing the official workflow, plus analysis of the IMNM Action Cards (1D + 1W). *(source: Trading & Investing/IMG_2232.PNG, IMG_2233.PNG)*

## The Official Signa Workflow (per Sage, Signa's AI)

> "Exactly—that's the ideal workflow. Use the StageScanner agent to surface a small, high-quality list of candidates meeting Signa's multi-factor criteria. Then dive into each signal's chart and Action Card across timeframes to confirm key elements like trend stage, RSI behavior, volume, and price structure. This aligns with CMT methodology and Signa's scoring engine... The scanner narrows the universe; your chart work refines timing and risk."

**Two phases:**
1. **StageScanner → narrows the universe** (automated, ~4 signals)
2. **Chart + Action Card → refines timing and risk** (manual review per ticker)

---

## Phase 1 — Run the StageScanner

The StageScanner is one of Signa's **40-Agent Consensus** tools. It applies Stan Weinstein's Stage Analysis (from *Secrets for Profiting in Bull and Bear Markets*):

- Classifies every stock into **Weinstein Stage 1–4** using:
  - 30-week MA slope
  - Price position relative to 30-week MA
  - Volume bias
- Surfaces **Stage 2 breakouts** only (the ideal entry stage) with entry price and stop
- Outputs ~4 high-quality candidates per run

**Backtest performance (2022–2024):** 22.5% CAGR, 52.3% win rate, Sharpe 0.40, Max DD −21.3%, +14.1% vs SPY

Run the StageScanner at the start of each session. If it generates 0–1 signals, there's nothing to trade that session.

### Weinstein Stage Reference

| Stage | Condition | Action |
|-------|-----------|--------|
| 1 | Basing / ranging above declining MA | Wait |
| 2 | Breakout — price above rising 30W MA, expanding volume | **BUY** |
| 3 | Topping — price stalling, MA flattening | Reduce / exit |
| 4 | Downtrend — price below declining 30W MA | Avoid / short |

---

## Phase 2 — Validate Each Candidate

For each StageScanner output, open the chart and pull the Action Card on two timeframes (1D and 1W). Confirm these four elements (per Sage):

### 1. Trend Stage
- Chart: is price clearly above the 30-week MA? Is the MA rising?
- 1D Action Card: Full bull stack confirmed? (price > EMA21 > EMA50 > SMA200)
- If the bull stack is not CONFIRMED → skip

### 2. RSI Behaviour
- 1D card: RSI in bullish zone (typically 50–70)? Not overbought (>75)?
- 1W card: RSI confirmed bullish?
- RSI overbought on both timeframes = late entry, skip or wait for pullback

### 3. Volume
- 1D card: Volume ratio > 0.8x (ideally >1.0x for a breakout)
- Volume thin (0.7x or below) = low conviction; use a limit order or wait
- Volume expanding on breakout candles = institutional participation

### 4. Price Structure
- Chart: Is the stock breaking out of a constructive base? Or extended from the base?
- Look for OR (Opening Range) and OB (Order Block) levels on the Signa chart
- Extended stocks (well above OB level) = higher risk; prefer entries near OB support

### Timeframe Confluence Matrix

| 1D Swing | 1W | Decision |
|----------|----|----------|
| Strong (Score ≥75, Grade A/B, all 4 confirmed) | Strong (Score ≥65, no distribution) | **Full position** |
| Strong | Mixed (Grade B, some signals) | **Half position** |
| Strong | OBV/CMF bearish OR Squeeze Locked | **Skip** — hard veto |
| Weak (<75) | Any | **Skip** |

**OBV+CMF both bearish on weekly = institutions distributing = hard veto regardless of daily.**

**Squeeze Locked on weekly = wait for the squeeze to fire and confirm direction before entering.**

---

## Position Sizing

Use Signa's stop level as the sizing anchor:

```
Risk per trade = Portfolio × 1.5%
Stop distance = Entry − Stop (from Action Card)
Shares = Risk ÷ Stop distance
```

Adjust risk % by conviction:
- Full position (1D+1W aligned): 1.5–2% risk
- Half position (1W mixed): 1% risk
- Skip if 1W veto applies

---

## Trade Management

- **Take 50%** off at Signa's 1D target
- **Trail the remainder** on EMA21 (daily)
- **Move stop to breakeven** once up 5%
- **Sunday review**: re-check the 1W Action Card — if OBV/CMF turns bearish after entry, exit remaining

---

## Applied Example: IMNM (2026-04-19)

IMNM was shared as a worked example (not a StageScanner output). *(source: Trading & Investing/Signa_IMNM_ActionCard.png, Trading & Investing/Signa_IMNM_ActionCard (1).png, Trading & Investing/Signa_IMNM_share.png)*

**Context:** Stock ran ~5× from the March 2025 bottom (~$5 → $25.47 52W high). Now at $24.630, sitting right at the OR (Opening Range) level $24.685 — resistance.

| Check | 1D | 1W |
|-------|----|----|
| Score | 82 / Grade A | 68 / Grade B |
| Bull stack | ✓ Confirmed | ✓ Confirmed |
| RSI | 67 bullish ✓ | 67 bullish ✓ |
| ICS | 74 leading ✓ | 99 extreme accumulation ✓ |
| OBV + CMF | Fine | **Bearish — distribution** ✗ |
| Volume | 0.7x alert | 0.6x alert |
| Early Warning | None | **Squeeze Locked — Bar 1 (bearish momentum)** |
| ADX | 19 (ranging) | 38 (strong trend) |

**The key conflict:** ICS 99 (extreme historical accumulation) vs OBV/CMF bearish (current distribution). These are not contradictory — they describe a different moment in time. Institutions accumulated on the way up from $5, ran it to $25, and are now **selling into the strength** at the highs. ICS measures the accumulation history; OBV/CMF measures what's happening today. Current flow wins.

**The squeeze:** "Momentum building bearish. Watch for breakdown." Bar 1 of a TTM Squeeze with bearish bias at near-52W highs is a warning, not a buy signal.

**Decision: No trade.** The 1W OBV/CMF veto applies regardless of the strong daily card.

**What to watch for re-entry:**
1. Pullback to OB level **$21.255** (Order Block on chart) with volume expansion
2. Weekly OBV/CMF to turn neutral or bullish (institutions re-accumulating, not distributing)
3. Squeeze to resolve bullishly (histogram expands green)
If those three converge → re-evaluate with fresh Action Cards from a much cleaner base. *(Updated 2026-04-19 ~16:30 AEST)*

---

## Cross-Reference with Other Sources

Signa's StageScanner output alone justifies a half-position. Layer on other sources to go full:

| Source | What confirms |
|--------|--------------|
| **DannyTrades** | If Danny covers the same ticker as a top setup |
| **John Wick / Trading Alpha** | Alpha Trend confirmation on same timeframe |
| **Antonella / VMA-SMA** | ASX stocks only — constructive base in VMA screen |

---

## Related Pages

- [[Signa.ai]] — tool overview, Action Card field definitions
- [[AI-Driven Trading System]] — overall trading system context
- [[DannyTrades Methodology]] — complementary signal source
- [[Bill Maiden — Generational Wealth Plan]] — portfolio context

---

## Related Pages

- [[Signa.ai]] — tool overview, Action Card field definitions
- [[AI-Driven Trading System]] — overall trading system context
- [[DannyTrades Methodology]] — complementary signal source
- [[Bill Maiden — Generational Wealth Plan]] — portfolio context

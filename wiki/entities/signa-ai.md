---
title: Signa.ai (ShardiB2 Trading Tool)
created: 2026-04-19 16:00 AEST
updated: 2026-04-19 16:00 AEST
tags: [trading, technical-analysis, signal-tool, shardib2, cmt, institutional, swing-trading, us-equities]
sources:
  - Trading & Investing/Signa_IMNM_ActionCard.png
  - Trading & Investing/Signa_IMNM_ActionCard (1).png
  - Trading & Investing/Signa_IMNM_share.png
  - Trading & Investing/IMG_2232.PNG
  - Trading & Investing/IMG_2233.PNG
  - Trading & Investing/Shardi B's CMT Trading Agent Project - Comprehensive Research.md
source_date: 2026-04-19
---

Signa.ai is a CMT-grade technical analysis and signal platform built by ShardiB2 (@ShardiB2_) — a US trader/analyst with 251K+ X followers. Bill holds a Professional membership. The core output is an **Action Card**: a structured signal report covering score, confidence, entry/stop/target, R:R, key metrics, and a ranked signal checklist across multiple timeframes.

## The Official Workflow (per Sage, Signa's AI Assistant)

Signa's internal AI (Sage) describes the correct usage as a two-phase process:
1. **Run the StageScanner** to narrow the universe to ~4 high-quality Stage 2 candidates
2. **Review each candidate's chart + Action Card** across timeframes to confirm trend stage, RSI, volume, and price structure

"The scanner narrows the universe; your chart work refines timing and risk." *(source: Trading & Investing/IMG_2232.PNG)*

## The StageScanner Agent

Part of Signa's **40-Agent Consensus** system. Based on Stan Weinstein's Stage Analysis methodology:
- Classifies stocks into Weinstein Stage 1–4 using 30-week MA slope, price position, and volume bias
- Surfaces Stage 2 breakouts only (the ideal entry stage) with entry and stop
- Generates ~4 candidates per run
- Backtest (2022–2024): 22.5% CAGR, 52.3% win rate, Sharpe 0.40, −21.3% max DD, +14.1% vs SPY

*(source: Trading & Investing/IMG_2233.PNG)*

## The Action Card

Each Action Card covers a single ticker on a specific timeframe (e.g. 1D Swing, 1-Week). Key fields:

| Field | Description |
|-------|-------------|
| **Score** | Overall signal quality, 0–100 |
| **Confidence** | % alignment across the signal checklist |
| **Grade** | A / B / C tier |
| **Entry** | Suggested entry price (market or limit) |
| **Stop** | Hard stop-loss level with % drawdown |
| **Target** | Profit target with % upside |
| **R:R** | Risk:Reward ratio |
| **ADX** | Trend strength (>25 = trending; <20 = ranging) |
| **Vol** | Volume ratio vs average (1.0x = normal) |

## Signal Checklist Categories

Signals are classified as CONFIRMED, LEADING, BEARISH, or ALERT:

1. **Full bull stack** — price > EMA21 > EMA50 > SMA200. Foundation check; must be confirmed.
2. **Trend score** — proprietary trend strength metric 0–100
3. **MACD** — bullish/bearish + histogram expansion/contraction
4. **RSI** — zone classification (bullish zone ~50–70; overbought >70)
5. **ICS (Institutional Conviction Score)** — institutional accumulation signal; LEADING indicator
6. **OBV + CMF** — On-Balance Volume + Chaikin Money Flow; when both falling/negative = distribution (BEARISH flag)
7. **Volume ratio** — below 0.8x triggers ALERT (low conviction)

## Early Warnings Section

Below the signal checklist, "Early Warnings" flags leading (not yet confirmed) risks:
- **Squeeze Locked — Bar N** = TTM Squeeze compression. Momentum is coiling; direction of breakout unknown. N = bars into the squeeze. Do not enter until the squeeze fires and direction confirms.
- No early signals = market in established trend or wait phase.

## Chart Layer (getsigna.ai)

Signa's chart displays:
- Standard OHLC candlestick coloured by trend bias (green = bullish, red = bearish)
- **52W Low** reference line
- **OR** (Opening Range) and **OB** (Order Block) levels — key S/R zones derived from institutional order flow

## Example: IMNM Action Cards (2026-04-19)

| Metric | 1D Swing | 1W |
|--------|----------|-----|
| Score | 82/100 | 68/100 |
| Confidence | 82% | 68% |
| Grade | A | B |
| Entry | $24.630 | $24.630 |
| Stop | $22.839 (−7.3%) | $20.935 (−15%) |
| Target | $28.213 (+14.5%) | $32.019 (+30%) |
| R:R | 2.0:1 | 2.0:1 |
| ADX | 19 (ranging) | 38 (strong trend) |
| Volume | 0.7x (ALERT) | 0.6x (ALERT) |
| OBV/CMF | n/a | Falling + Negative (BEARISH) |
| Early Warning | None | Squeeze Locked — Bar 1 |

The 1D/1W divergence (strong daily, weak weekly with distribution) flags this as a WATCH, not enter situation. See [[Signa.ai — Structured Workflow]].

## Related Pages

- [[Signa.ai — Structured Workflow]] — Bill's step-by-step protocol for using the tool
- [[AI-Driven Trading System]] — broader trading system context (Signa is a key signal source)
- [[DannyTrades Methodology]] — cross-reference for signal confluence

---
title: LEAPS Options Strategy (SirBews Method)
created: 2026-04-05
updated: 2026-04-05
tags: [trading, options, leaps, snirbews, strategy, deep-itm, premium-capture, bill-maiden]
sources:
  - raw/Phil Breaks Down Sirbews Leaps Strategy.pdf   # ~2025 — Phil's breakdown of SirBews' live trading method
  - raw/Sng1987 - SirBews LEAPS Strategy.pdf          # ~2025 — Sng1987's formal 4-phase lifecycle document
---

The SirBews LEAPS strategy is a structured options approach based on purchasing deep in-the-money (ITM) long-dated calls (LEAPS) on high-conviction stocks, then systematically rolling positions up to higher strikes as the underlying appreciates — while selling shorter-dated out-of-the-money (OTM) calls to generate premium income that funds speculative short-term plays.

> **Document timeline:** Both documents are ~2025 community writeups of SirBews' publicly shared trading methodology, produced independently by different analysts (Phil and Sng1987). Phil's document is a narrative walkthrough of live trades; Sng1987's is a more formal lifecycle framework with 4 defined phases. Together they provide a complete operational picture of the strategy.

## Core Mechanics

### Entry Criteria — Phase 1: Establish Exposure

- **Strike selection**: Deep ITM calls; target delta of **0.78–0.90** so the option moves almost dollar-for-dollar with the stock
- **Expiry**: 2–3 years out (LEAPS timeframe) — long enough to weather volatility without time decay pressure
- **Capital efficiency**: Deep ITM LEAPS cost significantly less than 100 shares of stock outright, freeing capital for additional positions or short-term plays
- **Underlying selection**: High-conviction stocks — typically large-cap tech or growth names with strong directional conviction

### Position Management — Phase 2: Profit Capture via Roll-Ups

When the underlying stock appreciates significantly:
- **Roll up to a higher strike**: Close the existing LEAPS and open a new one at a higher strike price
- **Purpose**: Lock in intrinsic value gain, maintain directional exposure, reduce downside if stock reverses
- **Trigger**: No fixed rule — SirBews rolls when the position has moved enough that the upside/downside profile warrants resetting

### Premium Enhancement — Phase 3: Short-Term Call Sales

Once profitable LEAPS positions are established:
- **Sell shorter-dated OTM calls** against the position (covered call / diagonal spread)
- **Purpose**: Collect premium income to fund speculative short-term trades
- **Reinvestment**: Premium collected goes into higher-risk, shorter-duration plays (not back into the LEAPS) — this creates a self-funding speculative "satellite" portfolio
- **Risk**: If the short calls are exercised or need to be bought back at a loss, it reduces but does not eliminate the core position gain

## Four Scenario Framework (Sng1987)

| Scenario | Condition | Action |
|----------|-----------|--------|
| **Bullish continuation** | Stock rises significantly | Roll up to higher strike; reassess new LEAPS entry if applicable |
| **Pullback** | Stock pulls back after a run | Hold — deep ITM / long DTE provides cushion; use dip to add or roll to better strike |
| **Sideways** | Stock consolidates for extended period | Sell shorter-dated OTM calls to generate premium income while waiting for the move |
| **Overextension** | Stock has run too far too fast | Trim position or sell premium aggressively; reduce exposure ahead of potential correction |

## Phil's Breakdown — Live Trade Examples

Phil's document illustrates the strategy through SirBews' actual trade commentary:

- **Entry discipline**: SirBews enters LEAPS only when he has strong directional conviction; he does not use LEAPS for speculative directional bets without thesis
- **Strike/expiry selection in practice**: Typically 60–80% of stock price as strike (deep ITM), 18–36 months to expiry
- **Rolling cadence**: Rolls are event-driven (stock up X%), not calendar-driven
- **Premium use**: The short-dated call premium is explicitly earmarked for "lottery tickets" — high-risk, high-reward short-term options plays that SirBews would not otherwise risk his core capital on

## Risk Profile vs. Outright Stock Ownership

| Dimension | Outright Stock | Deep ITM LEAPS |
|-----------|---------------|----------------|
| **Capital required** | Full stock price × 100 | ~60–90% of stock price × 100 |
| **Downside** | Can go to zero | Premium paid (limited) |
| **Upside** | Unlimited | Unlimited (within expiry) |
| **Time decay** | None | Present but slow (long DTE + deep ITM minimises it) |
| **Delta** | 1.0 | ~0.78–0.90 (near 1:1 move) |
| **Leverage** | 1× | ~1.1–1.7× depending on strike |

## Relationship to Bill's Trading System

The SirBews LEAPS strategy is referenced as a component of the longer-term "Horizon" strategy framework in [[AI-Driven Trading System (Multi-Strategy Hedge Fund)]]. It is well-suited to the Danny Trades / Cantonese Cat long-term sleeve ($1.5M allocation) which targets weeks-to-months trend positions with +30–100% move targets. The premium capture mechanic also aligns with the Cockpit's mandate to use shorter-dated instruments to generate income while holding core directional positions.

## Related Pages

- [[AI-Driven Trading System (Multi-Strategy Hedge Fund)]] — the broader system this strategy feeds into
- [[Trading Alpha Indicators]] — the TradingView indicator suite used for entry/exit timing
- [[Trading Reference Materials]] — general trading education background
- [[Bill Maiden — Generational Wealth Plan]] — financial context

---
title: Trading Alpha™ Indicators
created: 2026-04-05
updated: 2026-04-05
tags: [trading, indicators, tradingview, technical-analysis, alpha-trend, john-wick, crypto]
sources:
  - raw/Trading Alpha™ Instruction Manual _ Trading Alpha Guide.pdf  # ~2025 — official Trading Alpha product guide
---

Trading Alpha™ is a professional TradingView indicator suite designed for active traders, comprising three suites (Alpha Trend, Alpha Confirmation, and Alpha Volatility) that work in combination to identify high-probability entry and exit signals. The suite is positioned as delivering particularly strong results in cryptocurrency markets and is used by professional traders including John Wick, who provides VIP signals referenced in Bill's [[AI-Driven Trading System (Multi-Strategy Hedge Fund)]].

> **Document timeline:** This is an official product guide (~2025), not Bill-specific material. It is included because Trading Alpha™ indicators are a primary signal source in the AI trading system architecture — John Wick's Alpha Trend signals are one of the key inputs to the multi-agent trading Cockpit.

## The Three Suites

### 1. Alpha Trend Suite

The core directional trend-identification toolkit:

| Indicator | Function |
|-----------|----------|
| **Alpha Trend** | Primary trend direction indicator — identifies whether an asset is in an uptrend, downtrend, or range |
| **Wick RSI** | RSI variant that factors in candle wick data, reducing false signals from wicks that reverse |
| **Alpha Thrust** | Momentum confirmation — identifies when a trend is accelerating (thrust) vs. decelerating |

- **Claimed accuracy**: Up to 93% daily accuracy cited in promotional materials (applied to configured crypto signals)
- **Use case**: Trend entry and continuation trades; primary signal for the longer-duration positions

### 2. Alpha Confirmation Suite

Secondary indicators that validate signals from the Alpha Trend Suite before entry:

- Designed to reduce false positives by requiring confirmation from a different signal type
- Acts as a filter: Alpha Trend fires the signal; Alpha Confirmation approves the entry
- Reduces over-trading in choppy/ranging markets where trend indicators give false signals

### 3. Alpha Volatility Suites

Volatility-focused indicators for:
- Identifying volatility compressions (low volatility → potential breakout)
- Detecting over-extended moves (high volatility → potential reversal)
- Sizing positions relative to current volatility regime
- Setting dynamic stop-loss levels based on volatility rather than fixed percentages

## Signal Interpretation Framework

The recommended workflow from the guide:
1. **Alpha Trend** confirms direction (bullish/bearish)
2. **Alpha Thrust** confirms momentum is building (not waning)
3. **Alpha Confirmation** provides secondary agreement
4. **Alpha Volatility** determines entry timing within the trend (enter on compression, avoid on spike)
5. **Wick RSI** used to identify pullback entries within a confirmed trend (buy RSI dip in uptrend)

## Crypto-Specific Performance

Trading Alpha™ is positioned as particularly effective for crypto markets due to:
- 24/7 markets create persistent trending conditions that trend indicators capture well
- Higher volatility creates more pronounced signals
- Thinner order books mean momentum (Thrust) signals are more reliable than in equities

## Role in Bill's Trading System

Trading Alpha™ indicators — specifically John Wick's VIP signals derived from this suite — are one of the primary signal inputs to the multi-agent trading Cockpit:

| Signal Source | Trading System Role |
|---------------|---------------------|
| **Alpha Trend signals** | Primary directional input for Danny Trades (long-term) and Lade Backk (short-term momentum) |
| **Wick RSI** | Entry timing for pullback-based entries |
| **Alpha Thrust** | Momentum confirmation before committing size |
| **Alpha Volatility** | Risk sizing and stop-loss calibration |

John Wick is described as providing daily signals (up to 93% claimed accuracy) via API or web scraping in the Cockpit architecture. These signals are one of the required inputs before the Cockpit fires a trade — a minimum threshold of 3+ aligned signals across independent sources is required.

See [[AI-Driven Trading System (Multi-Strategy Hedge Fund)]] for the full signal aggregation framework.

## Related Pages

- [[AI-Driven Trading System (Multi-Strategy Hedge Fund)]] — the system that consumes these signals
- [[LEAPS Options Strategy (SirBews Method)]] — complementary longer-term options approach
- [[Trading Reference Materials]] — general trading education

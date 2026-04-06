---
title: Trading Reference Materials
created: 2026-04-05
updated: 2026-04-05
tags: [trading, education, reference, crypto, technical-analysis, risk-management, fundamentals]
sources:
  - raw/World of Trading.pdf        # Undated — comprehensive trading education manual (not Bill-specific)
  - raw/Crypto Strategy Guide.pdf   # Undated — crypto-specific education guide (not Bill-specific)
---

This page consolidates general trading education reference materials — a comprehensive trading manual and a crypto-specific strategy guide — that provide foundational knowledge context for the active trading strategies in [[AI-Driven Trading System (Multi-Strategy Hedge Fund)]]. Neither document is Bill-specific strategy; both are general educational resources.

> **Document timeline:** Both documents are undated general-purpose educational materials. They are not planning documents or strategy outputs specific to Bill's trading system. They are captured here as reference context rather than strategy documents.

## World of Trading — Coverage Areas

A comprehensive multi-topic trading education manual covering:

| Topic | Key Content |
|-------|------------|
| **Fundamental Analysis** | How to evaluate companies and assets based on financial metrics, earnings, and macro factors |
| **Mindset** | Psychological discipline, handling losses, avoiding emotional trading |
| **Order Types** | Market, limit, stop, stop-limit, trailing stop — execution mechanics |
| **Risk Management** | Position sizing, portfolio allocation, drawdown limits, risk/reward ratios |
| **Sentiment Analysis** | Using fear/greed indicators, options market sentiment, social media signals |
| **Technical Analysis** | Chart patterns, support/resistance, moving averages, oscillators |
| **Trading Plan** | How to build and follow a structured pre/during/post trade process |
| **Types of Markets** | Equities, forex, crypto, futures, options — structural differences |

### Key Risk Management Principles (from World of Trading)

- **Never risk more than 1–2% of portfolio on a single trade** — aligns with the 2% per-trade rule in Bill's trading system
- **Define stop-loss before entry** — not after entry when emotions are engaged
- **Risk/reward ratio**: Target minimum 2:1 (risk $1 to make $2)
- **Position sizing formula**: Risk % × Account Size ÷ (Entry − Stop) = Number of Shares/Contracts
- **Drawdown recovery math**: A 50% drawdown requires a 100% gain to recover — asymmetric cost of large losses

## Crypto Strategy Guide — Coverage Areas

A crypto-specific education guide covering:

| Topic | Key Content |
|-------|------------|
| **Altcoins** | How to evaluate altcoins vs. Bitcoin, narrative-driven vs. fundamental value |
| **Bitcoin Dominance** | BTC dominance as a market cycle indicator — rising dominance = risk-off, falling = altseason |
| **Blockchain Fundamentals** | On-chain metrics, tokenomics, network activity as investment signals |
| **Exchange Selection** | CEX vs. DEX tradeoffs; selecting exchanges based on liquidity, fees, security |
| **Market Cycles** | 4-year Bitcoin halving cycle thesis; accumulation → markup → distribution → markdown |
| **Security** | Wallet security, private key management, exchange risk, hardware wallets |

### Market Cycle Framework (from Crypto Strategy Guide)

The guide describes a recurring 4-phase crypto market cycle:

| Phase | Characteristics | Strategy |
|-------|----------------|---------|
| **Accumulation** | Low prices, low sentiment, smart money buying quietly | Accumulate core positions |
| **Markup** | Rising prices, increasing retail attention, momentum building | Hold and add on dips |
| **Distribution** | Euphoria, high prices, narratives peaking | Reduce positions, take profits |
| **Markdown** | Falling prices, capitulation, fear dominating | Hold cash, avoid catching falling knives |

## Alignment with Bill's Trading System

These reference frameworks underpin several elements of the trading system:

- The **risk management rules** in the Cockpit (2% per-trade, 10% drawdown circuit-breaker, 50% option loss stop) align directly with the principles in the World of Trading manual
- The **Bitcoin dominance / market cycle** framework in the Crypto Strategy Guide informs when Viv (mean-reversion / altcoins) and Shardi B (event-driven / on-chain) agents are likely to find better opportunities
- The **on-chain metrics** approach in the Crypto Strategy Guide aligns with Shardi B's agent design (whale wallet movements, DeFi liquidity changes)
- The **sentiment analysis** toolset from the World of Trading manual maps to how the Cockpit aggregates multiple independent signals before firing a trade

## Related Pages

- [[AI-Driven Trading System (Multi-Strategy Hedge Fund)]] — the active trading framework these materials inform
- [[LEAPS Options Strategy (SirBews Method)]] — specific options strategy
- [[Trading Alpha Indicators]] — the TradingView indicator suite

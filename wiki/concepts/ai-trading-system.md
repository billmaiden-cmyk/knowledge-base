---
title: AI-Driven Trading System (Multi-Strategy Hedge Fund)
created: 2026-04-05
updated: 2026-04-05
tags: [trading, investing, ai, hedge-fund, crypto, options, langchain, langgraph, bill-maiden, copy-trading]
sources:
  - raw/AI-Driven Trading Cockpit and Copy Trading Workflow Design.pdf  # ~2025 — ChatGPT, detailed technical design spec
  - raw/__AI Agent Swarm & Multi-Strategy Hedge Fund – Strategy Briefing__.pdf  # ~2025 — ChatGPT, strategy overview + PRD + 12-month plan
stale: true
---

Bill's AI-driven trading system is a multi-strategy investment framework designed to manage a $2.5M portfolio across short-term copy trading and longer-term trend positions, using AI agent orchestration (LangChain/LangGraph) to synthesise signals from multiple expert sources and execute trades automatically.

> **Document timeline:** Both documents are ~2025 ChatGPT outputs representing active planning for a live trading system. The Strategy Briefing is the higher-level business case; the Trading Cockpit Design is the more detailed technical specification. Together they describe a system that was planned for full launch by December 15, 2025, with initial small-scale testing from August 2025. Both documents treat MTS AI work and trading as complementary parallel tracks under a unified AI strategy.

> [!warning] ⚠️ STALE — Implementation Timeline Lapsed (flagged 2026-04-05)
> The entire phased implementation timeline in this document is now in the past. The "Full Launch" target of **December 15, 2025** was ~4 months ago. The August–November 2025 build phases are also elapsed. This page describes the **planned** system design; actual execution status is unknown and not yet documented. A new source (conversation, status update, or revised plan) is needed to record what was actually built, what was deferred, and what the current trading system state is.

## Capital Structure

| Allocation | Amount | Strategy Type |
|-----------|--------|--------------|
| Existing portfolio | $750k | Hold/rotate/sell decisions via Cockpit |
| New capital (December deploy) | $1.8M | New opportunities across all strategies |
| **Total capital** | **$2.5M** | — |
| Short-term "Blockchained Snipers" | $1M | Short-term crypto trades (3 agents) |
| Long-term "Horizon" | $1.5M | Weeks-to-months trend positions |
| Copy trading sub-accounts | ~$72k | Shardi B ($50k) + Blockchained Snipers ($22k) |

**Goal**: Double ($2.5M → $5M) within 12 months in the Cockpit document; triple ($2.5M → $7.5M) in the Strategy Briefing.

## Two-Track Architecture

### Track 1: MTS AI Agent Swarm (Content & Report Automation)
The Strategy Briefing explicitly links MTS automation and trading as complementary AI initiatives:
- MTS swarm frees operational bandwidth and demonstrates AI credibility
- Committee/Building Report agent is the MTS swarm MVP
- Content posting agent disseminates reports automatically
- The same agent architecture (LangGraph, LangChain) underpins both tracks

### Track 2: AI Hedge Fund — Multi-Strategy Trading

## Signal Sources (Trading Cockpit)

The Cockpit synthesises signals from multiple independent sources. A trade fires only when a configurable threshold of sources align (default: 3+ independent bullish/bearish signals):

| Source | Signal Type | How Captured |
|--------|------------|--------------|
| **John Wick's Trading Alpha** | Alpha Trend, Wick RSI/Thrust — up to 93% claimed daily accuracy | API or web scraping |
| **Danny Cheng** (@dannycheng2022) | Multi-timeframe chart analysis, support/resistance levels | Twitter API + OCR |
| **Cantonese Cat** (@cantonmeow) | Bollinger Band squeezes, 20MA, Fibonacci levels | Twitter/YouTube scraping |
| **Wyckoff Method** | Accumulation/markup/distribution/markdown phase classification | LLM analysis of price/volume data |
| **Elliott Wave** | Impulse vs corrective wave classification | Algorithm + LLM labelling |
| **Standard technical indicators** | 50/200-day MAs, RSI, MACD | Direct calculation on price data |
| **Portfolio state** | Current positions, P&L, stop levels | Saxo Bank API |

## Short-Term "Blockchained Snipers" ($1M — 3 Agents)

Each agent has a distinct strategy to avoid correlation:

| Agent | Strategy | Focus |
|-------|---------|-------|
| **Lade Backk** | Momentum breakout | BTC/ETH on 15-min/1-hour charts; ride short-term momentum; hold <1 day |
| **Viv** | Mean-reversion / volatility catch | Altcoins; detect over-extensions via Bollinger/RSI; buy dips and sell rips |
| **Shardi B** | Event-driven / on-chain | Whale wallet movements, DeFi liquidity changes, news spikes; aggressive breakout on new trending coins |

Capital deployment: ~$100K each initially → scale to full $1M by December 15, 2025 as each is validated.

## Long-Term "Horizon" Strategies ($1.5M — 2 Agents)

| Agent | Strategy | Focus |
|-------|---------|-------|
| **Danny Trades** (Danny Cheng) | Trend-following / high-conviction | Daily/weekly John Wick VIP signals + fundamental data; hold weeks to months; target +30–100% moves |
| **Cantonese Cat** (@cantonmeow) | Risk management / timing | Macro risk signals, volatility triggers, Fibonacci entry/exit timing; acts as guardrail on Danny's positions |

Danny decides *what to buy*; Cantonese Cat decides *when* and *how much* based on risk context.

## Copy Trading Workflows

Three separate automated copy-trading pipelines run in parallel to the main Cockpit strategy:

### Shardi B (@ShardiB2) — Twitter
- Allocation: ~$50k
- Signal type: Crypto, equity, and short-dated options (0DTE to 1–2 days)
- Data ingestion: Twitter API streaming; OCR on trade screenshots
- Key challenge: Images of filled orders (resolved by GPT-4 Vision + OCR)
- Execution: ~3-second latency from alert to order; Saxo Bank for US options

### Lade Backk's Discord — SPY/ES Options
- Allocation: within main capital
- Signal type: Day-trading SPY/ES options
- Data ingestion: Discord WebSocket scraper (headless browser fallback)
- Risk: Daily loss limit per day; trailing stop logic if group doesn't specify exits

### Blockchained Snipers Discord
- Allocation: ~$22k
- Signal type: Crypto futures or options signals
- Data ingestion: Same Discord scraper architecture
- Execution: Crypto exchange API (Binance/Bybit) for crypto trades

## The Trading Cockpit (Integration Layer)

A central dashboard that consolidates all strategy agents:
- **Real-time positions and P&L** per strategy
- **Global risk enforcement**: monitors cross-strategy concentration, aggregate drawdown
- **Manual controls**: pause/resume individual agents, global kill-switch, manual trade override
- **Alerting**: daily summaries, instant alerts on threshold breaches
- **Performance analytics**: equity curves, Sharpe ratios, win rates, strategy correlation matrix
- **LangSmith integration**: logs all prompts, responses, and agent actions for audit and debugging

## Technical Implementation

| Layer | Technology |
|-------|-----------|
| Agent orchestration | LangGraph (stateful multi-agent graphs) |
| LLM interactions & tools | LangChain |
| Decision-making model | GPT-4 (low temperature ~0–0.3 for consistency) |
| Monitoring & evaluation | LangSmith |
| Brokerage API | Saxo Bank (equities, forex, crypto CFDs, some options) |
| Crypto exchanges | Binance / Bybit (for crypto-native strategies) |
| Data ingestion | Twitter API, Discord WebSocket, web scraping (Playwright) |
| OCR | OpenAI GPT-4 Vision or dedicated OCR library |
| Speech-to-text | OpenAI Whisper (for Cantonese Cat YouTube videos) |

## Risk Management Framework

- **Per-trade risk**: 2% of capital (default, configurable)
- **Max single position**: 10% of portfolio
- **Drawdown circuit-breaker**: if portfolio drawdown exceeds 10%, reduce position sizes or halt new trades
- **Short-dated options**: no overnight holds unless strategy specifies; stop at 50% option premium loss
- **Consecutive loss rule**: after 5 consecutive losses in copy trading, pause or reduce size
- **Staleness filter**: skip copy trade entry if option has moved >X% from alert price (avoids chasing)
- **Simulation mode**: all strategies run in paper-trade mode before live capital deployment

## Implementation Timeline (from Strategy Briefing)

| Phase | Date | Milestone |
|-------|------|-----------|
| Kickoff | Aug 2025 | Team setup, John Wick API access, architecture design |
| Build Phase 1 | Sep 2025 | Report agent v0.1, Lade Backk + Viv prototypes, backtesting |
| Build Phase 2 | Oct 2025 | Report agent v1.0 live, Shardi B coded, Danny Trades prototype, basic Cockpit |
| Scale-Up | Nov 2025 | Sniper agents scaled to six-figure capital; long-term strategies finalized; Cockpit v1.0 |
| Full Launch | Dec 15, 2025 | $1M short-term sleeve live; $1.5M long-term sleeve activated |
| Compounding | Dec 2025 – Aug 2026 | Target 3× by month 12 |

## Relationship to MTS

The Strategy Briefing explicitly frames both tracks as a unified AI initiative:
- The same Vietnam AI engineers building the MTS agent swarm also build the trading agents
- MTS committee report automation is the MTS track's MVP
- The trading system is the financial-return track
- Both validate Bill's AI execution thesis and feed the personal brand strategy

See also: [[MTS AI Agent Swarm Architecture]], [[AI-Enabled Strata Operations]], [[Bill Maiden — Public Brand & AI Positioning Strategy]]

## Related Pages

- [[Bill Maiden]] — the fund manager and project lead
- [[Bill Maiden — Generational Wealth Plan]] — financial context
- [[Trading Signal Sources]] — detailed breakdown of signal providers (if created)
- [[Crypto Strategy]] — crypto-specific investment framework
- [[MTS AI Agent Swarm Architecture]] — the MTS automation work on the parallel track

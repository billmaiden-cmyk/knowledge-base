---
title: MTS LangChain Agent Implementations
created: 2026-04-05
updated: 2026-04-05
tags: [mts, langchain, ai, agents, code, campaign-strategist, content-strategist, more-than-strata]
sources:
  - raw/langchain_implementation_examples.pdf  # ~2025 — 33-page Python code reference for MTS Campaign + Content Strategist agents
---

This document is a 33-page technical reference providing Python LangChain implementation examples for two MTS marketing agents: Campaign Strategist and Content Strategist. It is the code-level counterpart to the higher-level agent architecture described in [[MTS AI Agent Swarm Architecture]], implementing two of the marketing-layer agents as working Python classes.

> **Document timeline:** A ~2025 technical implementation document, likely produced alongside or shortly after the agent swarm strategy documents. It provides working code skeletons customised for MTS as a named tenant, validating that the agent designs described in strategy documents are technically achievable with LangChain.

## Two Agents Implemented

### Campaign Strategist Agent

**Class:** `CampaignStrategistAgent`

**Role:** Develops integrated marketing campaigns that drive business results for strata management services.

**Tools:**
| Tool | Function |
|------|----------|
| `AudienceAnalyzer` | Analyses target audience segments (committee members, property owners, building managers) |
| `BudgetAllocator` | Recommends budget allocation across channels by campaign objective (awareness / lead gen / retention) |
| `CampaignPerformanceAnalyzer` | Analyses historical campaign performance (returns mock MTS campaign data) |
| `TimelineGenerator` | Generates phased campaign timeline (planning 2 weeks → launch 1 week → execution → evaluation) |
| `ChannelMixOptimizer` | Recommends channel mix by audience and objective (e.g., LinkedIn for committee members) |

**System prompt emphasis:** Integrated campaigns, budget allocation, cross-channel coordination, ROI.

**Outputs:** Campaign briefs, roadmaps, budget allocations, performance frameworks.

**Time horizon:** Defined campaign periods (weeks to months).

**MTS-specific audience data hardcoded:**
- *Strata committee members*: professionals 45–65, pain points = defects/compliance/costs, channels = LinkedIn/email/industry forums
- *Property owners*: diverse ages, pain points = maintenance costs/committee decisions, channels = Facebook/email
- *Building managers*: professionals 35–55, pain points = contractor/resident/compliance, channels = email/LinkedIn

### Content Strategist Agent

**Role:** Develops ongoing content strategy, editorial calendars, and content pillars for audience engagement.

**Tools include:** keyword research, content pillar development, audience content-needs mapping, editorial calendar generation, content performance analysis.

**System prompt emphasis:** Content themes, audience engagement, customer journey alignment, long-term content value.

**Outputs:** Content strategies, editorial calendars, content pillars, keyword strategies.

**Time horizon:** Ongoing editorial calendars spanning multiple quarters.

**MTS content pillars identified:**
- Warranty Claims for Defects
- Fire Safety Compliance
- Capital Works Fund
- Strata Dispute Resolution
- Owner Rights and Responsibilities

## Architecture

Both agents use the `create_react_agent` pattern from LangChain with:
- `ChatOpenAI(temperature=0.2, model="gpt-4")` — low temperature for consistency
- `ConversationBufferMemory` — maintains conversation context
- `AgentExecutor.from_agent_and_tools` — runs the ReAct loop

## Integration with AI CMO

The document describes how both agents are orchestrated by an AI CMO layer using `StateGraph` (LangGraph):

- The AI CMO coordinates work between both strategists to ensure alignment
- It provides high-level business objectives and constraints to both
- Resolves conflicts between campaign and content priorities (campaign needs vs. ongoing content calendar)
- Allocates resources between campaign and content initiatives
- Reports combined performance metrics upward

The `StateGraph` connects Campaign Strategist outputs (campaign briefs, timelines) → Content Strategist inputs (content themes, needs) and vice versa.

## Key Differentiations Between the Two Agents

| Dimension | Campaign Strategist | Content Strategist |
|-----------|-------------------|-------------------|
| **Scope** | Defined campaign periods | Ongoing editorial calendar |
| **Metrics focus** | Conversion, acquisition cost, campaign ROI | Engagement, audience growth, content performance |
| **Primary data** | Campaign performance metrics, budget, channel effectiveness | Content performance, keyword data, audience content consumption |
| **Output rhythm** | Campaign briefs at project start | Quarterly editorial calendars |

## Related Pages

- [[MTS AI Agent Swarm Architecture]] — the full 96-agent swarm this code is part of
- [[MTS Technology Roadmap]] — the operational roadmap referencing the outbound marketing factory (Initiative 4)
- [[More Than Strata (MTS)]] — the business context

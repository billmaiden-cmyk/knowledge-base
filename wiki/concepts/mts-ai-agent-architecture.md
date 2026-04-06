---
title: MTS AI Agent Swarm Architecture
created: 2026-04-05
updated: 2026-04-05
tags: [technology, ai, agent-swarm, architecture, multi-tenant, langgraph, mts, executive-ai]
sources:
  - raw/MTS-September-Outcomes.pdf            # Sep 2023 — pre-AI operational baseline
  - raw/More Than Strata AI Agent Swarm Strategy.pdf  # ~2024 — 96-agent full swarm design
  - raw/ai_cmo_agent_architecture.pdf         # ~2024-25 — CMO agent detailed spec
  - raw/updated_architecture_integration.pdf  # ~2025 — revised integration architecture
---

The MTS AI Agent Swarm is a hierarchical, multi-tenant AI executive system designed to operate [[More Than Strata (MTS)]] — and eventually the broader [[Block]] roll-up — as an AI-first services business. AI executives (CMO, CFO, COO, CCO, CTO) report directly to the human CEO and drive business outcomes through coordinated agent sub-swarms.

> **Document timeline:** The September 2023 Service Quality Summary (below) establishes the pre-AI baseline. The 96-agent swarm design (~2024) defines the target architecture. The updated integration architecture (~2025) refines implementation specifics. Reading these in sequence shows the progression from "what we have" to "what we're building" to "how we're building it."

## Executive Hierarchy

```
CEO (Human)
    └── Executive Layer
         ├── AI CFO Executive  (~16 agents) — financial management
         ├── AI CMO Executive  (~20 agents) — marketing & sales
         ├── AI CCO Executive  (~20 agents) — customer experience
         ├── AI COO Executive  (~20 agents) — operations & building analytics
         └── AI CTO Executive  (~20 agents) — technology & infrastructure
```

**Total: 96 agents** operating as a multi-agent system (MAS) across the five executive domains. Each AI executive is accountable for specific business outcomes. The architecture establishes clear decision boundaries between autonomous AI executive decisions and those requiring human approval.

The design philosophy is **holonic**: each group (finance, operations, etc.) functions as a cohesive unit and interacts with other groups through an event-driven pub/sub message bus. Cross-group communication is event-triggered — e.g., when the COO's Maintenance Monitor detects an HVAC anomaly, it automatically alerts the CFO's AP agent (to earmark funds) and the CCO's Committee Reporting agent (to update the dashboard) without human coordination.

**Proactive vs Reactive agents:** Each agent is designated as either proactive (continuously monitors conditions, initiates actions on schedule or pattern detection) or reactive (responds to user requests or system events). The combination makes MTS both responsive and anticipatory.

## AI CMO Agent — Components

The AI CMO is designed as a generic, configurable executive agent deployable across multiple businesses (multi-tenant).

### 1. Executive Core
- **Strategic Director** — sets high-level marketing strategy, allocates resources, adjusts based on performance
- **Agent Orchestrator** — delegates tasks to specialized sub-agents, resolves conflicts, prioritizes
- **Decision Engine** — evaluates options against business criteria, balances short/long-term, handles uncertainty with configurable risk models

### 2. Marketing Intelligence
- **Market Analyzer** — industry trends, competitive landscape, opportunities/threats
- **Audience Insights Manager** — audience personas, preferences, behaviors, pain points
- **Performance Analyst** — KPI tracking, anomaly identification, strategy optimization insights

### 3. Strategy Development
- **Campaign Planner** — campaign concepts, structure, timelines, cross-channel coordination
- **Content Strategist** — content themes, mix, cadence, customer journey alignment
- **Channel Strategist** — channel effectiveness evaluation, channel-specific strategies

### 4. Execution Coordination
- **Content Coordinator** — content calendar, quality, brand alignment
- **Distribution Director** — publishing schedule, cross-channel distribution
- **Engagement Manager** — audience responses, community interactions

### 5. Innovation and Optimization
- **Experimentation Director** — A/B tests, result evaluation
- **Trend Adopter** — emerging marketing approaches, trend adaptation
- **Continuous Improver** — incremental enhancements, improvement measurement

## Multi-Tenant Design

The architecture serves multiple businesses simultaneously while maintaining strict data isolation:

| Component | Function |
|-----------|---------|
| **Tenant Configuration Manager** | Separate business configs, brand guidelines, marketing strategies per tenant |
| **Tenant-Specific Knowledge Store** | Isolated vector databases per tenant |
| **Tenant Context Switching** | Seamless context switching with strict data isolation |
| **Shared Core Capabilities** | Strategic reasoning, market analysis, orchestration shared across tenants |

The configuration model (`AICMOConfig`) externalizes all business-specific elements (goals, audiences, brand guidelines, channel strategy, approval workflows) as configuration — enabling reuse across industries without code changes. Configuration supports hierarchical inheritance: Base → Industry → Business → Campaign.

## Configuration Framework

Each tenant configures:
- `business_goals`, `target_audiences`, `value_proposition`, `competitive_positioning`
- `marketing_goals`, `brand_guidelines`, `content_strategy`, `channel_strategy`
- `approval_workflows`, `publishing_preferences`, `performance_metrics`
- `feedback_sources`, `experimentation_settings`, `optimization_priorities`

## Technology Stack

| Layer | Technology |
|-------|-----------|
| **Agent orchestration** | LangGraph (graph-based workflow definition, state management) |
| **Core capabilities** | LangChain (structured prompting, RAG, tool use) |
| **Observability** | LangSmith (decision tracing, performance monitoring, debugging) |
| **Vector storage** | Separate vector stores per tenant (or pgvector in Postgres) |
| **Communication** | Event-driven pub/sub for async cross-executive coordination |
| **Human-AI interface** | Executive dashboard, strategic directive system, override mechanism |

## Cross-Executive Collaboration

AI executives collaborate through standardized event-driven interfaces:
- **Financial Planning Events** (AI CFO ↔ AI CMO — budget allocation)
- **Marketing Campaign Events** (AI CMO → sub-agents)
- **Customer Experience Events** (AI CMO ↔ AI CCO)
- **Operational Events** (AI COO ↔ AI CTO)

Collaboration mechanisms include: resource negotiation (AI CMO requests budget from AI CFO), strategic alignment synchronization, and escalation paths to human executives.

## Observability and Governance

- **Decision Transparency** — explicit reasoning, traceable decision factors, full audit trail
- **Performance Monitoring** — real-time strategy effectiveness, anomaly detection
- **Human Oversight** — configurable approval workflows, intervention interfaces, feedback loops

## Content Strategy and Execution Flow

```
AI CMO Executive (Strategy)
    → Content Strategy Sub-Agents (Planning)
        → Content Creation Sub-Agents (Execution)
            → Channel Adapter Sub-Agents (Distribution)
                → Analytics Sub-Agents (Measurement)
                    → Performance Evaluation (back to AI CMO for optimization)
```

## Agent Roster by Swarm

### AI CFO Swarm (~16 agents)
| Agent | Type | Key Function |
|-------|------|-------------|
| AI CFO Executive | Proactive | Aggregates financial data; strategic recommendations to management |
| Accounts Payable | Reactive | OCR invoice processing; payment scheduling; discrepancy flagging |
| Accounts Receivable | Reactive | Levy invoice generation; payment tracking; overdue reminders |
| Budget Planning | Proactive | Automated budget creation; variance monitoring |
| Cash Flow & Forecasting | Proactive | ML-based cash position forecasting; scenario analysis |
| Financial Reporting | Reactive | P&L, balance sheets, cash flow statements per building |
| Audit & Compliance | Proactive | Transaction auditing; sinking fund / trust account compliance |
| Procurement & Cost Optimization | Proactive | Vendor contract monitoring; cross-building bulk discount opportunities |
| Risk Analysis & Insurance | Proactive | Financial risk scoring; insurance policy tracking |
| Treasury & Investment | Proactive | Reserve fund management; interest-bearing account optimization |
| Expense Management | Reactive | Staff expense processing; OCR receipt validation |
| Committee Finance Liaison | Reactive | Natural-language financial Q&A for committee members |
| Tax & Regulatory | Proactive | GST/BAS submissions; regulatory change monitoring |

### AI COO Swarm (~20 agents)
| Agent | Type | Key Function |
|-------|------|-------------|
| AI COO Executive | Proactive | Operational priority setting; resource optimization across buildings |
| Maintenance Monitor | Proactive | IoT sensor monitoring; anomaly detection; predictive maintenance alerts |
| Maintenance Scheduler | Reactive | Work order scheduling; vendor dispatch; stakeholder updates |
| Vendor Management | Proactive | Vendor database; RFQ automation; performance tracking |
| Quality Assurance | Proactive | Post-maintenance feedback collection; IoT validation of repairs |
| Operational Analytics | Proactive | KPI dashboards; incident frequency analysis; "what-if" scenarios |
| Process Automation | Proactive | Cross-functional workflow orchestration (n8n); new building onboarding |
| Inventory & Asset | Reactive | Parts/supplies tracking; end-of-life asset prediction; auto-reorder |
| Emergency Response | Reactive | Emergency protocol execution; resident notification; post-mortem |
| Energy Optimization | Proactive | Smart meter / IoT analysis; BMS control recommendations |
| Safety & Compliance | Proactive | Mandatory inspection scheduling; compliance certificate tracking |
| Project Tracking | Reactive | Long-term project milestones; Gantt tracking; budget vs actuals |

### AI CMO Swarm (~20 agents)
| Agent | Type | Key Function |
|-------|------|-------------|
| AI CMO Executive | Proactive | Campaign strategy; cross-channel performance monitoring |
| Lead Generation | Proactive | Web scraping for prospects; outbound email outreach; CRM entry |
| Content Creator | Proactive | Blog posts, social media, newsletters; SEO optimization |
| Social Media & PR | Proactive | Platform management; social listening; press release drafting |
| Advertising Campaign | Proactive | Google/Facebook ad management; A/B testing; budget optimization |
| CRM & Data Enrichment | Reactive | Lead deduplication; data enrichment via property databases |
| Lead Nurturing | Reactive | Email drip campaigns; engagement tracking; warm-lead handoff |
| Proposal Drafting | Reactive | RAG-powered customized proposal generation (minutes to produce) |
| Market Research | Proactive | Competitor monitoring; industry news; regulatory change alerts |
| Brand Reputation | Proactive | Online review monitoring; sentiment analysis; reputation reporting |
| Sales Assistant (Virtual BDM) | Reactive | Two-way prospect communication; voice AI for calls; CRM flagging |

### AI CCO Swarm (~20 agents)
| Agent | Type | Key Function |
|-------|------|-------------|
| AI CCO Executive | Proactive | Client satisfaction monitoring; relationship health scoring |
| Virtual Customer Support | Reactive | 24/7 omnichannel Q&A (chat, email, SMS/WhatsApp); ticket escalation |
| Voice Concierge | Reactive | AI phone receptionist; speech-to-text query handling; call transfer |
| Committee Reporting | Proactive | Monthly/on-demand reports pulling from CFO + COO data; dashboards |
| Resident Communications | Proactive | Mass notifications (maintenance, meetings); compliance with notice requirements |
| Feedback & Survey | Proactive | CSAT surveys post-events; sentiment analysis; score trending |
| Complaint Triage | Reactive | Complaint classification; context retrieval; priority routing |
| Knowledge Base Management | Proactive | Vector DB maintenance; new by-laws / minutes ingestion; FAQ updates |
| Account Management | Proactive | AGM/contract renewal tracking; proactive committee check-ins |

### AI CTO Swarm (~20 agents)
| Agent | Type | Key Function |
|-------|------|-------------|
| AI CTO Executive | Proactive | System health monitoring; tech roadmap; security oversight |
| Data Pipeline & Integration | Proactive | ETL across Zendesk / StrataMax / Box / CRM into unified data layer |
| Knowledge Base Curator | Proactive | Vector store maintenance; LLM fine-tuning pipelines; multi-tenant isolation |
| Security & Compliance Tech | Proactive | SIEM integration; zero-trust access control; privacy law compliance |
| DevOps & Infrastructure | Proactive | Cloud scaling; CI/CD deployment; failover; cost optimization |
| AI Developer Assistant | Reactive | Code generation; codebase-aware debugging; new agent scaffolding |
| Advanced Analytics | Proactive | Cross-domain data science; churn prediction; multi-department KPI modeling |
| Digital Twin Simulation | Proactive | Building scenario modeling; stress-testing capital decisions |
| Innovation Scout | Proactive | Tech landscape monitoring; AI research digests; integration prototyping |

## Cross-Agent Workflow Examples

**Predictive Maintenance Chain:** IoT sensor detects HVAC anomaly → Maintenance Monitor (COO) flags it → Maintenance Scheduler dispatches contractor → Finance AP agent earmarks funds → Committee Reporting agent updates building dashboard → Resident Communications agent notifies residents. All autonomous, no human coordination.

**Lead-to-Client Onboarding:** Lead Gen (CMO) identifies prospect → Sales Assistant engages → Proposal Drafting generates customized doc → human lightly reviews → client signs → Process Automation (COO) triggers full onboarding: CRM update, financial accounts setup, knowledge base ingestion of new by-laws, welcome pack delivery. Day 1 fully ready.

**Financial Anomaly Detection:** Audit agent detects 30% utility spike → AI CFO consults Ops Analytics → IoT data shows water usage spike → Maintenance Monitor finds no recorded issue → COO dispatches leak inspection → leak found and fixed → Risk Analysis updates risk model → Innovation Scout researches additional sensors.

## Baseline Performance (Pre-AI, September 2023)

The September 2023 Service Quality Summary provides the pre-AI baseline that the swarm is designed to improve on:

| Metric | Value |
|--------|-------|
| Median resolution time | 02h 30min |
| First-touch resolution rate | 86% |
| Resolved within 24h | 70% |
| Resolved within 1–7 days | 82% |
| New tickets (September) | 1,685 |
| Solved tickets (September) | 1,683 |
| Weekday avg requests | 88/day |
| Weekend avg requests | 12/day |
| Peak time | 11AM Monday |

The swarm targets significant improvement on cycle time and cost-to-serve against this baseline. See [[AI-Enabled Strata Operations]] for the margin targets.

## Implementation Roadmap

| Phase | Timeline | Focus |
|-------|----------|-------|
| Foundation | Month 1–2 | Core infrastructure, data integrations, shadow-mode agents (support chatbot, basic finance reporting, one pilot building) |
| Pilot | Month 3–4 | Subset of agents for 1–2 buildings; measure response time reduction, error reduction |
| Expansion | Month 5–6 | Full marketing pipeline; proactive analytics; clear human escalation paths |
| Full Deployment | Month 6+ | All 96 agents active; continuous monitoring and learning |

## Related Pages

- [[MTS Operating Substrate (World Model)]] — the data foundation the agents operate on
- [[AI-Enabled Strata Operations]] — strategic and cost model context
- [[MTS Automated Committee Reporting]] — the report generation use case
- [[MTS Repairs & Maintenance Agent]] — the first production agentic workflow
- [[More Than Strata (MTS)]] — the business
- [[Block]] — the roll-up that scales this architecture

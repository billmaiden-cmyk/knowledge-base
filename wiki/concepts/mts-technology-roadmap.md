---
title: MTS Technology Roadmap (2025–2026)
created: 2026-04-05
updated: 2026-04-05
tags: [mts, technology, roadmap, ai, automation, zendesk, langchain, n8n, more-than-strata]
sources:
  - raw/Technology Roadmap_Unformatted.docx                                            # ~2025 — MTS internal roadmap document, 6 AI/automation initiatives
  - raw/AI-Driven Content Marketing Workflow with n8n for More Than Strata.pdf         # ~2025 — 7-page n8n workflow guide for LinkedIn/blog automation (Initiative 4 detail)
stale: true
---

The MTS Technology Roadmap is a 12-month AI automation and Zendesk-optimisation plan (Q2 2025 – Q2 2026) designed to double MTS's portfolio from ~2,000 to ~4,000 strata lots, grow monthly revenue from ~$100K to $200K, and improve profit margins from ~30% to ~50% — all without significant incremental Australian headcount. It comprises six high-impact initiatives.

> [!warning] ⚠️ STALE — Three of Four Quarters Now Elapsed (flagged 2026-04-05)
> As of April 2026, **Q2–Q3 2025, Q4 2025, and Q1 2026** milestones are all in the past. Only **Q2 2026 (Apr–Jun)** remains current. This page documents the *planned* roadmap; actual delivery status for each initiative is unknown. A status update source is needed to record which initiatives launched on schedule, which were deferred, and what the actual MTS tech stack looks like today.

> **Document timeline:** This is an internal MTS planning document (~2025) that represents the operational technology execution plan. It is the "how" layer beneath the higher-level AI strategy described in [[MTS AI Agent Swarm Architecture]] and [[AI-Enabled Strata Operations]]. It is grounded in specific tools (Zendesk, SweetHawk, LangChain, n8n, PropertyIQ) and includes phased milestones, KPIs, and commercial impact. The roadmap also validates the [[MTS Operating Substrate]] architecture by specifying how data flows from PropertyIQ and Zendesk into AI workflows.

## Strategic Context

| Target | Current | Goal |
|--------|---------|------|
| Portfolio size | ~2,000 lots | ~4,000 lots (+2,000 over 2 years) |
| Monthly revenue | ~$100K | ~$200K |
| Profit margin | ~30% ($30K/month) | ~50% ($100K+/month at $200K revenue) |
| Manager capacity | ~110 buildings/manager | ~200 buildings/manager |

The margin improvement model: replace incremental AU hires with automation plus low-cost offshore support. The roadmap explicitly notes this model "would provide a platform for acquisitions" — directly connecting to the [[Strata Acquisition Arbitrage]] strategy.

## Six Initiatives Overview

| # | Initiative | One-Line Description | Key Benefit |
|---|-----------|---------------------|-------------|
| 1 | Building & Project Status Reporting Automation | Auto-generates daily digests and monthly/quarterly committee reports from PropertyIQ and Zendesk | ~40 h/manager/month saved |
| 2 | Zendesk + SweetHawk Workflow Enhancements | Adds structure, SLAs, and audit trails using SweetHawk without new code | 10–15 h admin saved/manager/month |
| 3 | Repairs & Maintenance Triage Automation | AI coordinator triages inbound maintenance 24/7, dispatches pre-approved vendors | ≥60% of jobs auto-handled; 5× manager load capacity |
| 4 | "Flood the Zone" Outbound Marketing Factory | High-throughput AI copy + HubSpot/Unbounce blankets 5 Sydney corridors | 2,000 buildings/month outreach with <0.3 FTE |
| 5 | Owner & Supplier Self-Service (Chatbot) | Chatbot lets owners check levies and suppliers track work-orders 24/7 | ≥80% routine queries resolved without staff |
| 6 | Zendesk to Box Filing Automation | Autofiles documents from Zendesk into Box; auto-files new strata plans | Eliminates manual document filing |

## 12-Month Phased Roadmap

| Quarter | Key Activities |
|---------|---------------|
| **Q2–Q3 2025** (Jun–Sep) | Zendesk + SweetHawk enhancements; Reporting Automation (daily digest + monthly report); Maintenance Triage AI prototype; first AI-driven outbound marketing workflow; Zendesk-Box integration |
| **Q4 2025** (Oct–Dec) | Maintenance AI pilot (subset + after-hours); daily digest live; auto-draft monthly reports; expand AI marketing campaigns |
| **Q1 2026** (Jan–Mar) | Reporting automation on all buildings; Maintenance AI full production; owner/supplier self-service portal/chatbot launch; scale sales automations toward 2,000-lot goal |
| **Q2 2026** (Apr–Jun) | Optimise KPIs; staff training and committee trust-building; automation handles bulk of routine work; further scale without major hiring |

## Initiative Detail

### Initiative 1 — Building & Project Status Reporting Automation

**Architecture:**
```
Data: PropertyIQ (financials) + Zendesk (tickets/projects)
→ Orchestration: n8n / Azure Logic Apps (05:00 daily; 1st of month)
→ AI: Azure OpenAI GPT via LangChain → JSON → narrative
→ Human-in-loop: 10-min manager review and approval
→ Distribution: Email + Owners' Portal
```

**Phasing:**
- Design & PoC: Jul–Sep 2025 — API connectors, n8n workflow skeleton, GPT prompt templates
- Release 1: Sep 2025 — Daily digest live; draft monthly reports (Governance, R&M, Insurance, Major Projects)
- Release 2: Dec 2025 — Financial section live (PropertyIQ extraction + insights)
- Full Roll-out: Jan 2026 — All buildings automated; digests auto-send; quarterly reports with manager sign-off

**KPIs:** % reports requiring zero manual edits; manager time per report; committee satisfaction score; follow-up question reduction.

### Initiative 2 — Zendesk + SweetHawk Workflow Enhancements

Quick-wins using existing tooling — no new code:
- Map every building to a Zendesk Organisation
- Schedule recurring compliance and AGM tasks via SweetHawk Recurring Tasks
- Embed one-click approval steps for expenditure >$5,000 via SweetHawk Approvals
- Formal data hierarchies: Building → Unit → Owner → Tenant

**Targets:** 100% recurring tasks auto-created; approvals <4 hours; 10–15 hours admin saved per manager per month.

### Initiative 3 — Repairs & Maintenance Triage Automation

Directly addresses the bottleneck at the R&M lead (Kat) and aligns with the [[MTS Repairs & Maintenance Agent]] specification:

**Architecture:**
```
Channels: email / portal / phone
→ AI agent: LangChain or Relevance AI
→ Actions: writes tickets in Zendesk; calls PropertyIQ where needed
→ Escalation: edge cases routed to manager
```

**Phasing:**
- Q3 2025: Evaluate Vendoroo-style SaaS vs. custom LangChain/Relevance AI; build connectors
- Q4 2025: Pilot — select buildings + after-hours; ≥60% auto-handled target
- Q1 2026: Portfolio-wide; smart prioritisation (burst pipe vs. drip); one manager covers 5× previous load

### Initiative 4 — "Flood the Zone" Outbound Marketing Factory

Saturates 5 Sydney corridors (Eastern Suburbs, Northern Beaches, Upper/Lower North Shore, CBD & Inner West) with multi-channel outreach to every strata building ≥20 lots.

**Architecture:**
```
Data: NSW strata public register scrape (n8n)
→ AI: GPT-4 / Unbounce Smart Copy (geo-personalised content)
→ Tools: HubSpot sequences, LinkedIn scheduler, PostGrid API
→ Orchestration: n8n
```

**Channel strategy:**
- LinkedIn: 3 posts/day; geo-localised hooks (e.g., "Mosman high-rise paint OSR cost breakdown")
- Email: 3 tracks per geo-pod (intro → proof → offer); HubSpot sequences with Day 0/+3/+10/+30 cadence
- Direct mail: PostGrid API-triggered letters for buildings with no email reply after Day 30 (~$1.80 each incl. postage)

**Coverage target:** 2,000 buildings/month outreach by Jun 2026 with <0.3 FTE.

**Resource impact:** No new AU hires; one AU growth lead + one VN campaign assistant. Monthly tech cost: ~A$650 (LinkedIn scheduler + PostGrid + Azure/OpenAI tokens; HubSpot/Unbounce already licensed).

### Initiative 5 — Owner & Supplier Self-Service Communication

**Tooling options:**
| Option | When to use |
|--------|-------------|
| Microsoft Power Virtual Agents | Fast, low-code starter solution for website/Teams deployment |
| Custom LangChain service | Complex multi-step logic or custom auth on Azure OpenAI |
| Microsoft 365 Copilot | Auto-drafting Outlook/Teams replies from same data |

**Phasing:**
- Q4 2025: Catalogue top owner/supplier questions; map to data fields and API calls
- Q1 2026: Prototype chatbot; connect PropertyIQ + Zendesk; limited pilot
- Q2 2026: Full launch; ≥80% routine queries auto-answered

**Target queries handled automatically:**
- "Have I paid my strata levy for this quarter?" → PropertyIQ ledger lookup
- "Status of work order #123?" → Zendesk ticket query

### Initiative 6 — Zendesk to Box Filing Automation

Automates document filing from Zendesk into Box, and auto-files new strata plans. (Initiative not fully detailed in source document — described as "Zendesk to Box Filing Automation and Handover Plans Autofiling.")

## Technology Platform Recommendations

The roadmap includes explicit platform guidance:

| Platform | Best-fit Use Case | Trade-offs |
|---------|------------------|-----------|
| **LangChain** | Custom AI workflows deeply integrated with PropertyIQ, Zendesk, proprietary data | Requires software engineering effort |
| **LangGraph** | Long-running / multi-step agent workflows needing memory & state | Overkill for simple linear tasks |
| **CrewAI** | Multi-agent "team" where each agent owns a role | Added complexity; only when one LLM is insufficient |
| **Relevance AI** | No-code, quick-deploy agents (sales BDR, FAQ chatbot) | Less custom flexibility; SaaS cost |
| **n8n** | General workflow glue: scheduling, API calls, data movement | Not an AI engine — pairs with above |

**Cloud:** Microsoft Azure + Copilot is the preferred stack (native to Microsoft 365; Azure OpenAI data residency guarantees; roadmap alignment with Dynamics 365/Power Platform).

**Integration principle:** "Extend what we have" — expose PropertyIQ and Zendesk via APIs; use n8n for orchestration; use LangChain for developer-level flexibility where required; Relevance AI for rapid wins.

## Related Pages

- [[MTS AI Agent Swarm Architecture]] — the agent architecture this roadmap operationalises
- [[MTS Operating Substrate]] — the data layer (Postgres-first world model) that underpins automations
- [[MTS Repairs & Maintenance Agent]] — the first production agent (Initiative 3)
- [[MTS Automated Committee Reporting]] — the reporting pipeline (Initiative 1)
- [[AI-Enabled Strata Operations]] — strategic context and cost model
- [[More Than Strata (MTS)]] — the business
- [[Strata Acquisition Arbitrage]] — acquisition strategy that roadmap enables

---
title: MTS Repairs & Maintenance Agent
created: 2026-04-05
updated: 2026-04-05
tags: [technology, ai, agent, repairs-maintenance, zendesk, automation, mts, strata-management]
sources:
  - raw/Repairs and Maintenance Agent Spec for Refining.docx  # ~2025 — active spec (title "for Refining" indicates ongoing iteration)
---

The MTS Repairs & Maintenance (R&M) Agent is the first production agentic workflow

> **Document timeline:** This spec is a live ~2025 working document, not a final design — the title "for Refining" signals it is being actively developed. It is the earliest production agent being built on the [[MTS Operating Substrate (World Model)]], and its design choices (evidence layer, meaning layer, decision receipts) are feeding back into the world model's evolution. in [[More Than Strata (MTS)]]'s automation roadmap. It orchestrates the full repairs and maintenance cycle — from ticket triage through supplier quoting, committee approval, and invoice verification — using Zendesk as the execution plane and an AI agent service for thinking and drafting.

## Purpose and Target Outcomes

| Outcome | Target |
|---------|--------|
| Reduce cycle time (ticket creation → committee approval) | 30–50% reduction |
| Reduce specialist coordinator time per ticket | 40–60% reduction |
| Reduce vendor non-response via automated chasers | Significant |
| Standardise committee comms at key milestones | Consistent structure + evidence links |
| Create decision traces for context graph | Compounds into operational intelligence |

## High-Level Architecture

### Zendesk: Execution Plane
Zendesk owns the entire workflow state:
- **Ticket** = case file + single source of operational truth for the case lifecycle
- **Tags/fields** = state machine (current workflow position)
- **Triggers** = event orchestration (automated responses to state changes)
- **Automations** = time-based chasing and escalation
- **Side Conversations** = separate threads for suppliers and committee (isolated from resident thread)

### AI Agent Service: Thinking + Drafting
The AI service handles all reasoning and content generation:
- Ticket classification + risk assessment
- Clarifying questions to resident/owner
- Scope writing per issue family
- Quote extraction and comparison
- Committee decision pack drafting
- Decision receipt creation
- Updating Zendesk fields/tags and creating side conversations via API

### Optional Case Store (Recommended)
A thin external store for:
- Structured quote objects
- Decision receipts
- Vendor performance metrics
- Cross-system linking (StrataMax work orders/invoices)

## Evidence Layer vs Meaning Layer (in R&M Context)

**Evidence layer** — immutable artifacts:
- Zendesk ticket messages (public + internal), timestamps, authors
- Side Conversation messages with suppliers and committee
- Attachments: photos, quote PDFs, completion photos
- Box documents: AGM/EGM docs, minutes, by-laws
- StrataMax records: financials, supplier invoices, work orders

**Meaning layer** — structured derived objects for execution:
- Ticket classification: issue family/type, urgency/risk, location, responsibility hypothesis
- Workflow state model (tags/fields)
- Scope templates per issue family
- Quote extraction fields (amount, inclusions, lead time, warranty, exclusions)
- Committee pack template + option comparison logic
- Escalation matrix + approval thresholds
- Decision receipts (structured "why this was approved")

> LLMs can infer relationships from evidence, but without meaning objects you cannot reliably execute, measure, or audit across thousands of tickets.

## Canonical Objects (R&M World Model)

| Object | ID | Primary System | Notes |
|--------|-----|----------------|-------|
| Scheme | `scheme_id` | StrataMax | Maps to Zendesk org |
| Person | `person_id` | StrataMax / Zendesk user | Owners, committee members |
| Ticket | `ticket_id` | Zendesk | Primary workflow container |
| Supplier | `supplier_id` | StrataMax + Zendesk | Performance tracking included |
| Quote | `quote_id` | Case store | Extracted from PDFs/emails; linked to evidence |
| Decision receipt | `decision_id` | Case store + Zendesk internal note | Approval + evidence pointers; critical for learning |

## Agent Workflow (Semi-Autonomous, Stage 2)

Example: R&M ticket arrives in Zendesk

1. **Classify** — issue type, make-safe vs normal repair, OC vs owner responsibility
2. **Retrieve** — relevant by-law clauses, policy constraints, budget approval thresholds
3. **Request quotes** — email templates to approved suppliers via Side Conversations
4. **Extract quotes** — structured fields from quote PDFs/emails (amount, inclusions, lead time)
5. **Compare options** — structured comparison with precedent ("similar issue last year cost $X")
6. **Draft committee pack** — options comparison + recommendation with evidence links
7. **Route approval** — to committee via Zendesk with structured decision options
8. **On approval**: create/update StrataMax work order; track completion
9. **Invoice approval** — checks variance, evidence of completion, drafts approval note
10. **Decision receipt** — structured record of what was decided, by whom, on what evidence

Human role: approves spend/exceptions; signs off invoices; handles policy escalations.

## Relationship to the World Model

This workflow is the first production instance of the [[MTS Operating Substrate (World Model)]]. Decision receipts generated by R&M tickets compound into the context graph, building operational intelligence that improves future automation (precedents, vendor performance, cost benchmarks). The R&M agent is Stage 2 in the agent maturity model; once proven, the same pattern extends to Governance, Insurance, Levies, and Compliance workflows.

## Related Pages

- [[MTS Operating Substrate (World Model)]] — the data substrate this agent operates on
- [[AI-Enabled Strata Operations]] — strategic context and step-function cost model
- [[MTS Automated Committee Reporting]] — the parallel reporting automation
- [[MTS AI Agent Swarm Architecture]] — the executive AI context
- [[More Than Strata (MTS)]] — the business

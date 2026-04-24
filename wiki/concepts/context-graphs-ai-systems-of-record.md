---
title: Context Graphs — AI's Next Trillion-Dollar Systems of Record
created: 2026-04-05
updated: 2026-04-05
tags: [ai, context-graphs, systems-of-record, agents, enterprise-software, foundation-capital, architecture]
sources:
  - raw/AI's trillion-dollar opportunity- Context graphs - Foundation Capital.pdf  # Dec 22, 2025 — Foundation Capital (Jaya Gupta, Ashu Garg)
---

Foundation Capital's December 2025 thesis argues that the next trillion-dollar enterprise software opportunity is "context graphs" — a new category of system of record that captures decision traces (not just current state) as AI agents execute workflows. This thesis directly validates the architectural choices in the [[MTS Operating Substrate]], which independently arrived at the same design pattern.

> **Document timeline:** Published December 22, 2025 by Foundation Capital partners Jaya Gupta and Ashu Garg. This is an external market thesis, not Bill-specific material. It is included because it provides strong independent validation of the [[MTS Operating Substrate]] architecture — particularly the decision receipts, context graph, evidence/meaning separation, and source-of-truth hierarchy. The thesis was accessed June 1, 2026 (print timestamp on document).

## The Core Argument

The last generation of enterprise software created trillion-dollar lock-in by becoming **systems of record** for objects:
- Salesforce → customers
- Workday → employees
- SAP → operations

The current debate is whether these systems survive the shift to AI agents. The Foundation Capital thesis goes beyond both the "agents kill everything" narrative and the "systems of record survive unchanged" counter-narrative.

**Their position**: Agents are cross-system and action-oriented. The UX of work is separating from the underlying data plane. But the missing layer isn't better data access — it's **decision traces**.

## What Systems of Record Don't Capture

Existing systems store *current state*, not *decision context*:
- Salesforce knows what the opportunity looks like *now*, not what it looked like when the discount was approved
- When a discount gets approved, the context that justified it isn't preserved
- You can't replay the state of the world at decision time — so you can't audit, learn from, or automate similar decisions

Agents are hitting this wall. They run into the same ambiguity humans resolve with judgment and organisational memory — but without access to the precedents, exceptions, and approval chains that make those judgment calls defensible.

## The Context Graph

A context graph is a structured, replayable history of how context turned into action:

> "A renewal agent proposes a 20% discount. Policy caps renewals at 10% unless a service-impact exception is approved. The agent pulls three SEV-1 incidents from PagerDuty, an open 'cancel unless fixed' escalation in Zendesk, and the prior renewal thread where a VP approved a similar exception last quarter. It routes the exception to Finance. Finance approves. The CRM ends up with one fact: '20% discount.' The context graph captures everything else."

The context graph links entities and decisions across time so **precedent becomes searchable**. Over time it becomes the real source of truth for autonomy — not just what happened, but *why it was allowed to happen*.

## Why Incumbents Can't Build This

Operational incumbents (Salesforce/Agentforce, ServiceNow/Now Assist, Workday) have a structural disadvantage:
- They are built on **current state storage** — optimised for what things look like now
- Their agents inherit this limitation: they can access data but cannot capture the orchestration-layer context at decision time
- ETL after the fact is a poor substitute for capturing decision context in the moment

**AI-native startups in the orchestration path have the structural advantage**: because they're executing the workflow, they see the full picture — what inputs were gathered, what policies applied, what exceptions were granted, and why. They can emit a decision trace on every run as a first-class record.

## Three Opportunity Archetypes

| Archetype | Description | Example |
|-----------|-------------|---------|
| **Replace the system of record** | Rethink workflows from scratch for a mixed human+agent team | Regie.ai (AI-native sales engagement replacing Outreach/Salesloft) |
| **Replace a module** | Target specific sub-workflows where exceptions concentrate; sync final state back to incumbent | Maximor (finance: cash, close management — ERP remains the ledger but Maximor owns the decisions) |
| **New system of record** | Entirely new category for decisions, not objects | Context graph platforms themselves |

## Signals for Where Context Graphs Matter

Two signals apply universally:
- **High headcount doing a workflow manually** → the labor exists because decision logic is too complex to automate with traditional tooling
- **Exception-heavy decisions** → where logic is complex, precedent matters, and "it depends" is the honest answer (deal desks, underwriting, compliance reviews, escalation management)

## Connection to MTS Operating Substrate

The Foundation Capital thesis independently validates the core design decisions of the [[MTS Operating Substrate]]:

| Foundation Capital Concept | MTS Operating Substrate Equivalent |
|---------------------------|-------------------------------------|
| Context graph | Context graph component with edges + decision receipts |
| Decision traces | Decision receipts (`decision_id`, approval + evidence pointers) |
| "Why it was allowed to happen" | Meaning layer: derived structured facts, decision receipts, escalation matrices |
| Evidence preserved at decision time | Evidence lake: immutable artifacts; append-only, replayable |
| Precedent becomes searchable | Context graph enabling "Ask MTS" natural-language querying with evidence-backed answers |
| Source of truth for autonomy | Truth hierarchy: 7 fact types with canonical sources |

MTS built its world model before this thesis was published — the convergence validates that the substrate design is directionally correct and that a similar architecture will likely underpin the next wave of AI-native enterprise platforms.

## Implications for Bill's Strategy

If the context graph thesis is correct:
- MTS's Operating Substrate is not just infrastructure for strata management — it is an early example of a category-defining enterprise AI architecture
- The "[[Block]] roll-up" and [[AI Leadership Consulting Platform]] strategies gain additional credibility: the MTS playbook can be applied to any traditional service business with complex, exception-heavy workflows
- The [[Bill Maiden — Public Brand & AI Positioning Strategy]] thesis (MTS as proof-of-concept for an AI-enabled service transformation) maps directly onto the Foundation Capital framework

## Related Pages

- [[MTS Operating Substrate]] — the MTS world model architecture this thesis validates
- [[MTS AI Agent Swarm Architecture]] — the agents that will emit decision traces into the context graph
- [[AI-Enabled Strata Operations]] — the business case for the architecture
- [[Bill Maiden — Public Brand & AI Positioning Strategy]] — the broader strategic context

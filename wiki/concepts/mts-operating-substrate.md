---
title: MTS Operating Substrate (World Model)
created: 2026-04-05
updated: 2026-04-05
tags: [technology, architecture, world-model, data, postgres, ai, mts, strata-management]
sources:
  - raw/World Model Operating Substrate_v.03.docx              # ~2025 — v.03 of world model spec (iterated from earlier drafts)
  - raw/World Model Evidence and Meaning Layers - Agents.docx  # ~2025 — companion doc refining evidence/meaning distinction
  - raw/Strata World Model Procedures and Workflow.docx         # ~2025 — procedures and workflow layer
  - raw/Azure Postgres DB.docx                                  # ~2025 — Azure deployment architecture spec
  - raw/Repairs and Maintenance Agent Spec for Refining.docx   # ~2025 — first production agent (references world model)
  - raw/Truth Hierarchy.docx                                   # Undated — source-of-truth hierarchy for 7 MTS fact types
---

The MTS Operating Substrate is a Palantir-style shared world model (ontology) that underpins [[More Than Strata (MTS)]]'s AI automation platform.

> **Document timeline:** All sources are ~2025 design documents representing the current (third-iteration) architecture. The "v.03" designation on the world model spec indicates meaningful prior iteration — the core evidence/meaning distinction and Postgres-first decisions were stabilised by this version. The R&M Agent spec (a separate document) references and validates the substrate design by showing how the first production workflow operationalises it. It transforms fragmented data across Zendesk, StrataMax, and Box into a structured, queryable, and auditable knowledge base — the foundation for composable committee reports, agentic workflows, and natural-language querying.

## Why It Exists

Today MTS's "truth" is fragmented across three systems:
- **Zendesk** — qualitative operational story (requests, conversations, approvals)
- **StrataMax / PIQ** — financial and roll truth (owners, levies, suppliers, work orders, invoices)
- **Box** — governance and legal truth (agendas, minutes, by-laws, procedures, notices)

This fragmentation is manageable by humans but breaks down for: consistent committee reporting across many schemes, automation that must act safely and repeatably, auditing ("why was this approved?"), and scaling execution to the Vietnam team without quality degradation.

## Guiding Principles (Non-Negotiable)

1. **Evidence is preserved** — append-only, replayable
2. **Meaning is derived** — structured facts extracted from evidence
3. **Canonical IDs exist** — every object attaches to a `scheme_id`, `person_id`, etc.
4. **Relationships are explicit** — not "LLM inferred at runtime"
5. **Decision traces are captured at commit time** — approvals, exceptions, responsibility calls
6. **Reports are generated from a deterministic pack** — LLM is last step, not first

## Architecture: Postgres-First

### Systems of Record
- **Zendesk** — case execution + communications (execution plane)
- **StrataMax** — financial truth + roll + supplier payments/work orders/invoices
- **Box** — governance/legal documents (minutes, agendas, by-laws, procedures)

### Operating Substrate Components
| Component | Purpose |
|-----------|---------|
| **Ingestion services** | Pull from Zendesk, StrataMax, Box |
| **Evidence lake** | Immutable storage of raw artifacts |
| **Canonical registry (crosswalk)** | Deduplicated IDs across systems |
| **Context graph** | Edges + decision receipts linking objects |
| **Meaning store** | Derived structured facts (classifications, statuses, extractions) |
| **Pack builder** (`scheme_month_pack`) | Assembles deterministic data pack per scheme per month |
| **Report generator** | LLM step consuming the pack |
| **Query service ("Ask MTS")** | Natural-language querying with evidence-backed answers |

### Storage Architecture (Azure)
- **Azure Database for PostgreSQL Flexible Server** — backbone for canonical registry, context graph, meaning store, JSONB evidence payloads
- **Azure Blob Storage** — evidence lake files (PDFs, images, OCR text); Postgres stores pointers (`blob_uri`, `hash`, `source_system`)
- **Azure Cosmos DB (Mongo API)** — AI workspace only: pipeline logs, intermediate LLM artifacts, caches, experiments. Not authoritative.
- **pgvector** — embeddings within Postgres to avoid a separate vector store

Rule: if it needs to be authoritative for automations or reporting, it goes to Postgres.

## Canonical Objects (World Model)

| Object | Canonical ID | Primary System | Notes |
|--------|-------------|----------------|-------|
| Scheme | `scheme_id` | StrataMax | Strata plan; maps to Zendesk org |
| Person | `person_id` | StrataMax / Zendesk | Owners, committee members |
| Ticket | `ticket_id` | Zendesk | Primary workflow container |
| Supplier | `supplier_id` | StrataMax + Zendesk | With performance tracking |
| Quote | `quote_id` | Case store | Extracted from PDFs/emails |
| Decision receipt | `decision_id` | Case store + Zendesk internal note | Approval + evidence pointers |
| Meeting | `meeting_id` | Box / StrataMax | AGM/EGM records |
| Action item | `action_id` | Box (minutes) / Zendesk | Creation vs completion split |

## The Rule + Process + Precedent Layer

Beyond data relationships, the world model captures the knowledge strata managers use to make decisions — in three buckets:

### 1. Law Layer (Universal Strata Rules)
Jurisdiction-specific (primarily NSW) but largely stable:
- Meeting notice periods, quorum requirements
- Ordinary vs special resolutions, voting eligibility
- Levy issuance rules (timelines, interest, recovery steps)

Stored as `Policy` objects with `policy_id`, `jurisdiction`, `policy_type`, `effective_from/to`, `source_citations`, and structured rule clauses.

### 2. By-Law Layer (Scheme-Specific Rules)
Per-scheme overrides and additions:
- Renovation rules, smoking/pets/noise policies
- Key/fob replacements, exclusive use allocations
- OC vs owner responsibility overrides

Stored as `Bylaw` objects with `bylaw_id`, `scheme_id`, `structured_tags`, and `responsibility_override`.

### 3. Playbook Layer (How MTS Operates)
Standard operating procedures:
- General repairs workflow, renovations approval, key replacement
- Levy query handling, insurance claim, breach notice workflows

Stored as `Workflow` objects with `workflow_id`, `triggers`, `steps`, `required_approvals`, `templates`, and `SLA_targets`.

## Evidence Layer vs Meaning Layer

These are the two foundational layers that make both better reports and real agents possible:

**Evidence layer** (what happened / what exists): Immutable artifacts — Zendesk ticket messages, side conversation events, attachments, Box documents, StrataMax records. Used for traceability, citations, audit, and replay.

**Meaning layer** (what it means / how MTS operates): Structured derived objects — ticket classifications, workflow state models, quote extraction fields, committee pack templates, escalation matrices, decision receipts. Used for automation, consistency, and agent safety.

> Without both layers, an AI system is an unreliable text generator that makes expensive mistakes at scale.

## Agent Maturity Stages

| Stage | Description | Human Role |
|-------|-------------|------------|
| **0 — Report Copilot** | Builds monthly packs, drafts committee report sections | Manager reviews and sends |
| **1 — Workflow Copilot** | Classifies requests, retrieves by-laws, drafts responses and EGM packs | Approves drafts, confirms dates |
| **2 — Semi-autonomous execution** | Requests quotes, compares options, routes approvals, creates StrataMax work orders | Approves spend, signs off invoices |
| **3 — Full agent strata manager** | End-to-end case management with human escalation only | Exceptions and policy decisions |

## Source-of-Truth Hierarchy

The Truth Hierarchy defines which system is authoritative for each category of fact, enabling agents and automations to resolve conflicts deterministically rather than guessing.

### Seven Fact Types and Their Canonical Sources

| Fact Type | Canonical Source | Notes |
|-----------|-----------------|-------|
| **Identity** | StrataMax | Lot numbers, owner names, addresses — StrataMax is the master registry |
| **Financial** | StrataMax ledger | Levy amounts, arrears, payments, budget — StrataMax is always the financial truth |
| **Operational workflow state** | Zendesk | The execution plane; which ticket is open, what stage, who is assigned |
| **Governance** | Box (signed minutes) | Committee decisions, resolutions, AGM/EGM outcomes — Box holds signed source documents |
| **Action item creation** | Box (minutes) | An action item is created when it appears in signed minutes — Box is canonical |
| **Action item completion** | The system that embodies the completion | If completion is a payment → StrataMax; if a document upload → Box; if a communication → Zendesk |
| **Responsibility** | Legislation + by-laws + OC decisions | Jurisdiction law first; then scheme by-laws; then committee decisions override |

### Conflict Handling

When two systems disagree on the same fact:
1. Apply the hierarchy — the canonical source wins
2. Record a `conflict_note` on the object flagging the discrepancy
3. Do not silently accept the non-canonical version
4. Surface for human review if the conflict is in a financial or governance fact type

This prevents agents from acting on stale or incorrect data sourced from a non-authoritative system.

### Design Intent

The hierarchy exists because the three core systems (Zendesk, StrataMax, Box) each hold partial truth about the same underlying reality. Without a defined hierarchy:
- An AI agent might report a levy as unpaid (Zendesk shows open ticket) when StrataMax shows it was paid two days ago
- Action items might be "completed" when the work order is raised in Zendesk, before the contractor has actually finished
- Governance decisions might be applied based on draft minutes in Box before the signed copy confirms the resolution passed

The truth hierarchy makes the world model trustworthy enough to act on autonomously.

## Related Pages

- [[AI-Enabled Strata Operations]] — strategic context and cost model
- [[MTS AI Agent Swarm Architecture]] — the executive AI agents built on this substrate
- [[MTS Automated Committee Reporting]] — the reporting pipeline
- [[MTS Repairs & Maintenance Agent]] — the first production agentic workflow
- [[More Than Strata (MTS)]] — the business

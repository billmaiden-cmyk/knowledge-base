---
title: MTS Automated Committee Reporting
created: 2026-04-05
updated: 2026-04-05
tags: [technology, ai, committee-reports, rag, automation, mts, strata-management, llm]
sources:
  - raw/PRD_ Automated Monthly Committee Reports for More Than Strata.pdf   # ~2024 — original PRD
  - raw/PRD_ Automated Monthly Committee Reports for More Than Strata 2.pdf  # ~2024 — revised PRD (v2 adds fine-tuning roadmap)
---

MTS Automated Committee Reporting is the system that uses Retrieval-Augmented Generation (RAG) to auto-generate the monthly narrative reports [[More Than Strata (MTS)]] produces for each strata plan. It replaces manual copy-paste reporting by strata managers with an AI-drafted, manager-reviewed document grounded in live data from Zendesk, Box, and Xero.

## Problem

Current pain points:
- **Manual effort** — managers spend significant time collecting data and writing reports
- **Fragmented data** — maintenance tickets (Zendesk), documents (Box), financials (Xero) are siloed
- **Inconsistency** — writing style and thoroughness vary by manager or building
- **Timeliness** — reports are monthly; owners lack visibility between cycles

## Solution Architecture

A RAG pipeline that: ingests data from Zendesk / Box / Xero → preprocesses and embeds → retrieves relevant context per building → generates narrative via LLM → delivers draft to manager for review → outputs final PDF.

### Data Sources

| Source | What It Provides |
|--------|----------------|
| **Zendesk** | Maintenance tickets — status, description, assignee, timestamps, updates |
| **Box** | Compliance certificates, contractor reports, quotes, past minutes |
| **Xero** | Cash at bank, levy receipts, arrears, budget vs actuals, major expenses |

### Report Structure (Codified Template)

Each report follows the existing committee report format:
1. **Title and Heading** — strata plan, address, reporting period
2. **Executive Summary / Manager's Commentary** — overall building status
3. **Maintenance Items** — per issue: Desired Outcomes / Status/Progress / Actions Required
4. **Financial Status** — cash position, levy status, notable financial events
5. **Compliance Actions** — fire safety, lift certification, insurance renewals
6. **Contractor Status** — key contractor performance, building defects, quotations
7. **General Discussion** — miscellaneous items

### Key Design Principles
- **Deterministic packs** — data assembled before LLM call; model is last step, not first
- **Grounded accuracy** — >95% of factual statements must trace to source data; no hallucination
- **Manager-in-the-loop** — all reports reviewed and approved before distribution
- **RAG for freshness** — live data retrieved at generation time; no stale training data

## Phased Implementation Plan

### Phase 1: MVP — Frontier LLM + RAG (Months 0–3)
- Fully integrated data pipelines (Zendesk, Box, Xero) with vector DB
- Automated monthly generation for 2–3 pilot buildings
- GPT-4 or Claude via API for narrative generation
- Basic manager review UI (email + editable draft)
- **Success criteria**: reports require <15% content change; manager effort <1 hour per report

### Phase 2: Enhanced Model — Fine-Tuned In-House LLM (Months 4–6)
- Fine-tune a base model (e.g. LLaMA-2 13B or GPT-3.5) on MTS report data
- Training dataset: historical {data → report} pairs + Phase 1 manager edits
- Deploy fine-tuned "StrataGPT" model; A/B test against GPT-4
- Introduce owner-facing query interface (chatbot or preset queries)
- **Success criteria**: fine-tuned model quality comparable to GPT-4; prompt size reduced 50%; data stays private

### Phase 3: Scale and Refinement (Months 7+)
- Enroll all strata plans; open owner query feature to all owners
- Add enhanced analytics (charts, anomaly alerts)
- Continuous model improvement via feedback loops
- **Target by month 9**: 100% buildings on AI-first draft reports

## RAG vs Fine-Tuning: Recommended Approach

The analysis concludes a **hybrid strategy** is optimal:
- **Phase 1**: RAG + frontier model (GPT-4/Claude) — fast time to value, no training required
- **Phase 2+**: Fine-tuned in-house model + RAG — domain-specific style, lower per-use cost at scale, full data privacy
- **Long-term**: Fine-tune for core domain knowledge (format, terminology); use RAG for dynamic data (live building info)

Key trade-offs:
| Dimension | RAG + Frontier | Fine-Tuned In-House |
|-----------|---------------|---------------------|
| Setup cost | Low | High (training) |
| Per-use cost | Higher at scale | Lower at scale |
| Privacy | Data sent to third-party | Data stays in-house |
| Domain fit | Prompt engineering | Baked into weights |
| Latency | Network + model delay | Faster (local, smaller) |
| Customization | Prompt-dependent | Full control |

## On-Demand Query Capability

Beyond scheduled monthly reports, owners and committee members can query current building status:
- **Option A**: On-demand full report refresh (same pipeline, user-triggered)
- **Option B**: Dynamic Q&A chatbot (RAG on same data; question-specific answers)

Recommended: phased approach — on-demand refresh for managers first; subset/preset query portal for owners; full chatbot in Phase 3.

## Non-Functional Requirements

- Report generation: 1–2 minutes end-to-end (MVP)
- Scalability: handle 50+ buildings concurrently
- Security: encrypted data at rest; no sensitive PII to external LLM; per-building data isolation
- Monitoring: token usage logging, hallucination detection, manager feedback capture

## Related Pages

- [[MTS Operating Substrate (World Model)]] — the data foundation powering the reports
- [[MTS AI Agent Swarm Architecture]] — the broader agent system context
- [[MTS Repairs & Maintenance Agent]] — the operational workflow agent
- [[AI-Enabled Strata Operations]] — strategic context
- [[More Than Strata (MTS)]] — the business

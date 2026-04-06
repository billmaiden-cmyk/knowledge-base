# Wiki Log

Append-only chronological record of all ingests, queries, and lint passes.
Each entry format: `## [YYYY-MM-DD] operation | description`
Parseable with: `grep "^## \[" wiki/log.md | tail -10`

---

## [2026-04-05] structural refactor | Wiki taxonomy restructured — 8 sections, wealth cross-linking, MTS hub

## [2026-04-05] setup | Created /coach slash command — Joe Hudson x CEO x PE x AI coaching agent; added wiki/coaching/ section for session notes

Changes made to index.md and manifest.yaml:
- Removed generic "Psychology & Personal Development" section; split into Personal Development and Professional Development
- Removed generic "MTS AI & Technology" section; replaced with "MTS — Strategy & Technology" hub that owns all MTS sub-concepts
- Moved Strata Acquisition Arbitrage from Wealth & Finance into MTS section (primary home); cross-listed in Wealth & Finance
- Moved Block entity from standalone Entities into MTS section — correctly scoped as "MTS — Michael Teys Scenario" (rename if Teys invests, not a separate venture)
- Removed Block from Ventures & Brand section
- Renamed "Personal Brand & Ventures" to "Ventures & Brand"; removed Block (now under MTS)
- Added Wealth & Finance as a cross-reference hub — MTS, Liberty, Trading System, Block, Strata Acquisition all appear here as wealth engines
- Renamed "More Than Strata (MTS)" → "MTS (More Than Strata)" in manifest title; index uses "MTS" as primary name throughout
- Updated tags: added mts-concept to all 9 MTS sub-pages; wealth-creation to 7 pages; personal-development/professional-development to 2 pages; ventures-brand to brand/consulting pages; mts-scenario to Block

## [2026-04-05] lint | Temporal audit — 4 issues found and resolved

Changes made:
- Added `source_date` field to all 29 manifest entries (dates range 2023-02 to 2026-04; 3 entries marked `undated`)
- Added `stale: true` to manifest entries for: mts-technology-roadmap.md, ai-trading-system.md, gmsr-global-macro-reports.md
- Added ⚠️ STALE callout blocks to ai-trading-system.md (Dec 2025 launch target elapsed) and mts-technology-roadmap.md (Q2–Q4 2025 + Q1 2026 milestones elapsed)
- Updated CLAUDE.md manifest format section to document source_date and stale fields
- No rogue files found on disk (explore agent false positive)

## [2026-04-05] query | Coaching app architecture — evaluated OpenClaw, Claude Dispatch, Remote Agent vs local Claude Code for daily coaching delivery; created synthesis page and OpenClaw entity

## [2026-04-05] coaching | Session 001 — Easter Sunday baseline; achievement-based self-worth in rest; system validation

## [2026-04-05] ingest | Bulk initial ingest — 29 pages created across concepts/, entities/, synthesis/

Sources ingested:
- raw/text 2.txt
- raw/text.txt
- raw/Complete_Wealth_Plan_Final.md
- raw/More Than Strata - Board Presentation - Feb 2023.pdf
- raw/More Than Strata AI Agent Swarm Strategy.pdf
- raw/Business Plan_ Leveraging MTS AI to Transform Real Estate Service Businesses.pdf
- raw/Pitch Deck Strategy for an AI-Powered Leadership Consulting Platform.pdf
- raw/Monetisation and Public Positioning Strategy for an Australian AI Executive.pdf
- raw/Strategy for AI-Driven Value Creation and Personal Brand Elevation.pdf
- raw/Y Combinator Pitch Deck Template Guide.pdf
- raw/__AI Agent Swarm & Multi-Strategy Hedge Fund – Strategy Briefing__.pdf
- raw/CONFIDENTIAL MTS_SE AI Acqusuition Platform Discussion Paper_.docx
- raw/PRD_ Automated Monthly Committee Reports for More Than Strata.pdf
- raw/PRD_ Automated Monthly Committee Reports for More Than Strata 2.pdf
- raw/Integrating SUI NextERP with a Tokenized Strata Management Platform.pdf
- raw/AI-Driven Trading Cockpit and Copy Trading Workflow Design.pdf
- raw/Phil Breaks Down Sirbews Leaps Strategy.pdf
- raw/Sng1987 - SirBews LEAPS Strategy.pdf
- raw/Trading Alpha™ Instruction Manual _ Trading Alpha Guide.pdf
- raw/Crypto Strategy Guide.pdf
- raw/World of Trading.pdf
- raw/ai_cmo_agent_architecture.pdf
- raw/langchain_implementation_examples.pdf
- raw/updated_architecture_integration.pdf
- raw/World Model Operating Substrate_v.03.docx
- raw/World Model Evidence and Meaning Layers - Agents.docx
- raw/Strata World Model Procedures and Workflow.docx
- raw/Azure Postgres DB.docx
- raw/Repairs and Maintenance Agent Spec for Refining.docx
- raw/Truth Hierarchy.docx
- raw/Technology Roadmap_Unformatted.docx
- raw/AI-Driven Content Marketing Workflow with n8n for More Than Strata.pdf
- raw/AI's trillion-dollar opportunity- Context graphs - Foundation Capital.pdf
- raw/GMSR (P) - Trust - Thursday October 2  2025 (P).pdf
- raw/GMSR (P) - US Stock Market - Wednesday May 28, 2025 (P).pdf
- raw/situational_awareness.pdf
- raw/Existential_Risk_and_Growth.pdf
- raw/Sterling Insights - Influencing vF.pdf
- raw/MTS-September-Outcomes.pdf (image PDF — unextractable, noted in manifest)
- raw/The Australian ACCC new rules for mergers etc 2026.pdf (image PDF — unextractable, noted in manifest)

Pages created:
- wiki/entities/bill-maiden.md
- wiki/entities/more-than-strata.md
- wiki/entities/liberty-corporate-finance.md
- wiki/entities/solaft.md
- wiki/entities/block.md
- wiki/concepts/achievement-based-self-worth.md
- wiki/concepts/influencing-framework.md
- wiki/concepts/compounding-wealth-architecture.md
- wiki/concepts/strata-acquisition-arbitrage.md
- wiki/concepts/ai-enabled-strata-operations.md
- wiki/concepts/mts-ai-agent-architecture.md
- wiki/concepts/mts-operating-substrate.md
- wiki/concepts/mts-repairs-maintenance-agent.md
- wiki/concepts/mts-committee-report-automation.md
- wiki/concepts/mts-technology-roadmap.md
- wiki/concepts/mts-langchain-agent-implementations.md
- wiki/concepts/strata-tokenization.md
- wiki/concepts/ai-trading-system.md
- wiki/concepts/leaps-options-strategy.md
- wiki/concepts/trading-alpha-indicators.md
- wiki/concepts/trading-reference-materials.md
- wiki/concepts/bill-maiden-public-brand-strategy.md
- wiki/concepts/ai-leadership-consulting-platform.md
- wiki/concepts/context-graphs-ai-systems-of-record.md
- wiki/concepts/gmsr-global-macro-reports.md
- wiki/concepts/agi-timeline-and-risk-frameworks.md
- wiki/synthesis/bill-maiden-generational-wealth-plan.md
- wiki/synthesis/mts-trading-architecture-parallels.md

## [2026-04-06] ingest | One Page Plan_2026.pdf — MTS strategy one-pager (March 2026); updated mts-business-strategy.md with three-pillar model (Better Product / Better Business / Stronger Growth), growth targets (⚠️ conflict flagged vs Business Strategy.docx), key initiatives table, and priority/owner table

## [2026-04-06] ingest | Organisation Structure_20250701.pdf — created mts-organisation-structure.md (specialist team model, 4 role types, RASCI framework, org chart, team directory); founding philosophy added to mts-business-strategy.md

## [2026-04-06] ingest | Business Strategy.docx — earlier strategy doc; incorporated into mts-business-strategy.md as secondary source (vision, marketing themes, value propositions, ⚠️ 5,000-lot target conflicting with One Page Plan)

## [2026-04-06] ingest | Keira Role.docx — created mts-keira-role.md (3-pillar role charter: CEO Leverage, Strata OS Translation, Vietnam Ops; decision rights, interfaces, KPIs, boundaries)

## [2026-04-06] ingest | Individual Conversation Form_MTS.docx — created mts-individual-conversation-form.md (annual performance conversation template; Looking Back/Forward structure; Development Plan 70-20-10; employee-led format)

## [2026-04-06] ingest | WhatsApp: Antonella (Apr 2025 — Apr 2026, ~8,076 lines, 25 major threads)

Created wiki/synthesis/comms-whatsapp-antonella-2025-04-to-2026-04.md — 12-month WhatsApp digest covering the full arc from discretionary stock picking through to the Three Setups Framework and autoresearch engine. 14 open action items identified. Critical blocker: Sebastian-Kiet SQL walkthrough not yet confirmed. Key divergences: VMA vs KAMA regime filter, sell rules timing, infrastructure readiness for autoresearch v1. 5 Word documents from last 2 weeks also copied to raw/whatsapp/ for future ingestion.

## [2026-04-06] ingest | WhatsApp Word docs: 3 documents from last 2 weeks

- raw/whatsapp/00003354-Discussion_Three_Setups_x_KAMA_Regime.docx → created wiki/concepts/antonella-kama-regime-discussion.md (Three Setups × KAMA regime reconciliation; 4 signal types → 3 setups mapping; filter vs classifier; KAMA conditions by setup type)
- raw/whatsapp/00003397-Dynamic Hedge Ratio.docx → created wiki/concepts/antonella-dynamic-hedge-ratio.md (dynamic hedging via framework metrics; ATR contraction + SI energy storage model; squeeze score formula)
- raw/whatsapp/00003157-Finding What Works Autoresearch Final.docx → updated wiki/concepts/antonella-autoresearch-system.md (added Strategic Rationale section from "Finding What Works" paper: why autoresearch vs backtesting, throughput advantage, 6 discovery categories, build requirements)

## [2026-04-06] ingest | Slack MTS: 30 Mar – 6 Apr 2026, 6 channels active, ~120 messages, 6 action items

Created wiki/synthesis/slack-digest-mts-2026-04-06.md — First Slack digest. Key themes: Vietnam hiring sprint (Vy onboarded as Financial Controller ex-Deloitte, Toan hired as second accountant, 4 candidates interviewed in 2 days). 3 payment authorisations from Gino (1 still pending). Bill flagged Zendesk ticket spike — Andrew investigating. Camille Deel salary discrepancy unresolved. Keira managing VN ops effectively — 70+ DMs coordinating interviews, equipment, payroll.

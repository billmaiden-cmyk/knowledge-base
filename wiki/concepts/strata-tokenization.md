---
title: Strata Tokenization (SUI NextERP)
created: 2026-04-05
updated: 2026-04-05
tags: [technology, blockchain, tokenization, sui, strata-management, defi, proptech, mts]
sources:
  - raw/Integrating SUI NextERP with a Tokenized Strata Management Platform.pdf  # ~2024-25 — speculative/exploratory PropTech thesis
---

Strata tokenization is a proposed evolution of [[More Than Strata (MTS)]]'s platform beyond AI automation

> **Document timeline:** This is a ~2024-25 exploratory document — it presents a longer-horizon thesis rather than an active implementation plan. It sits ahead of the current roadmap (which is focused on proving AI margins first) and should be read as directional thinking about where the platform *could* go once the AI automation foundation is proven. No implementation timeline is established in the source., using the SUI blockchain and NextERP as a backbone to tokenize strata fee streams, governance rights, and vendor payment flows. It repositions MTS from a traditional strata manager to a PropTech platform provider and ecosystem orchestrator.

## The Core Idea

Traditional strata management is a fragmented, paper-heavy service business. Tokenization creates programmable, on-chain representations of strata financial flows and governance rights — making them liquid, auditable, and automatable at a level not possible with traditional software alone.

The SUI blockchain is chosen for its high throughput, low transaction costs, and native support for complex object models — properties that suit the high-volume, low-value transaction patterns in strata (levy collection, small vendor payments, routine approvals).

## Key Components

### SUI Blockchain + NextERP
- **NextERP** serves as the operational backbone, managing the traditional strata data layer (owners, lots, levies, suppliers)
- **SUI blockchain** sits as the settlement and tokenization layer on top of NextERP
- Smart contracts automate the financial flows that are currently manual or system-dependent

### Smart Contracts for Fee Collection and Vendor Payments

**Levy collection (fee streams):**
- Levy obligations are encoded as smart contracts with automated payment schedules
- Non-payment triggers automated escalation sequences (reminders → interest accrual → recovery steps)
- On-chain record creates an auditable, immutable levy payment history per lot

**Vendor payment flows:**
- Once a work order is approved (via the [[MTS Repairs & Maintenance Agent]] or committee resolution), payment can be automated via smart contract
- Vendor receives payment upon verified milestone completion (e.g., photo evidence uploaded to the system)
- Eliminates manual invoice processing and reduces payment cycle time

## Token Economy

Three token types are proposed:

| Token | What It Represents | Holder |
|-------|-------------------|--------|
| **Management Fee Token** | Fractional claim on the MTS management fee stream | Investors |
| **Governance Token** | Voting rights on strata plan decisions | Lot owners |
| **Participation Reward Token** | Rewards for active platform participation (timely levy payment, vendor reviews, etc.) | Lot owners, vendors |

### Management Fee Tokenization
- MTS's management fee income stream can be tokenized and sold to external investors
- Creates a new capital-raising mechanism: instead of debt or equity dilution, MTS raises against future fee income
- Fee token holders receive proportional fee distributions; token is liquid and tradeable

### Governance Tokens (DAO-Like Structure)
- Each lot in a strata plan receives governance tokens proportional to their ownership share (unit entitlement)
- Governance tokens are used for on-chain voting on resolutions that currently require physical meetings or postal ballots
- Committee elections, spending approvals, and by-law amendments can be conducted on-chain
- Reduces meeting administration cost and increases owner participation

### Participation Rewards
- Owners who pay levies on time receive reward tokens
- Vendors who complete work to standard and receive positive ratings earn tokens
- Creates a positive incentive layer on top of the existing obligation structure

## MTS Strategic Positioning

Tokenization shifts MTS's strategic identity:

| Current Position | Tokenized Position |
|-----------------|-------------------|
| Strata management service provider | PropTech platform provider |
| Earns management fees | Earns platform fees + fee stream value |
| Operator of schemes | Ecosystem orchestrator |
| Value: lots managed | Value: platform network effects |

The platform provider model is significantly more scalable and commands a higher valuation multiple than a service business. Other managers could eventually use the MTS tokenization platform (and pay platform fees), creating a two-sided network effect.

## Relationship to AI Platform

Tokenization and the [[MTS AI Agent Swarm Architecture]] are complementary layers:
- AI agents handle operational decisions (classifying requests, drafting communications, routing approvals)
- Smart contracts handle financial execution (levy collection, vendor payment, fee distribution)
- The [[MTS Operating Substrate (World Model)]] connects both: providing the canonical data that AI agents act on and smart contracts reference

Decision receipts from the AI layer (e.g., committee approval of a work order) can trigger smart contract execution — closing the loop from AI decision to on-chain settlement.

## Considerations and Risks

- **Regulatory**: Australian strata law governs levy obligations and governance rights; smart contract implementation must not create conflicts with the Strata Schemes Management Act (NSW) or equivalent
- **Owner adoption**: Requires owners and committee members to interact with blockchain-based systems; UX abstraction layer is essential
- **Liquidity**: Management fee tokens are only valuable if a secondary market develops
- **Complexity**: Adds significant technical and legal complexity; this is a longer-term roadmap item, not an immediate priority

## Related Pages

- [[More Than Strata (MTS)]] — the platform being transformed
- [[MTS Operating Substrate (World Model)]] — the data layer that smart contracts reference
- [[MTS AI Agent Swarm Architecture]] — the AI layer that complements on-chain execution
- [[MTS Repairs & Maintenance Agent]] — operational workflow whose approvals could trigger smart contract payments
- [[AI-Enabled Strata Operations]] — the broader automation strategy
- [[Block]] — the roll-up vehicle where tokenization could apply at scale

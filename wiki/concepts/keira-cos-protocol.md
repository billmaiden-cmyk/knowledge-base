---
title: Keira — Chief of Staff Protocol
created: 2026-04-12 21:30 AEST
updated: 2026-04-12 21:30 AEST
tags: [keira, chief-of-staff, protocol, escalation, mts, operations, meta]
sources:
  - Bill Maiden design session, 12 April 2026
---

Operating protocol for Keira's Chief of Staff function at MTS, designed for the period when Bill is primarily at ABGF and Liberty (April 2026 onwards). This governs how Keira escalates decisions to Bill, how Bill checks in with her, and what she owns without needing Bill.

## Context

Bill started ABGF on 13 April 2026 and is 0.5 FTE at Liberty. From this point, his availability to MTS is structured rather than continuous. Keira is the human action layer — she executes, coordinates, and manages the team. The AI agent stack (briefing, midday pulse, evening close) monitors and surfaces what needs Bill. Keira and the agent stack together are the operating system that lets Bill stay genuinely present at ABGF and Liberty without MTS drifting.

## Escalation Protocol — How Keira Reaches Bill

When Keira needs Bill's decision or urgent attention during the day, she uses this format in a **Slack DM to Bill**:

| Prefix | When to use | Bill's expected response |
|--------|-------------|--------------------------|
| `DECISION: [topic]` | Needs Bill to choose between options; cannot proceed without his call | Bill responds at next natural break — within 2–4 hours |
| `URGENT: [topic]` | Time-sensitive; delay causes real harm (client escalation, compliance risk, financial exposure) | Bill responds within 1 hour |
| 🚨 `[topic]` | Critical — same urgency as URGENT, alternative trigger format | Bill responds within 1 hour |

**Everything else** — updates, FYI, "just so you know" — Keira sends as a normal Slack message or holds for the weekly 1:1. She does not need to hear back on normal messages while Bill is in ABGF or Liberty meetings.

The midday pulse (12pm) and 7am briefing both scan specifically for these escalation prefixes and surface them to Bill automatically.

**The protocol only works if Keira uses it consistently.** Bill should name this format explicitly in their next 1:1 and ask Keira to confirm she understands when each prefix applies. One mis-escalation (using URGENT: for a non-urgent item) is fine — the protocol calibrates over the first week or two.

## What Keira Owns Without Needing Bill

Keira has full authority to act independently on:

- **Operational MTS items** — Zendesk ticket escalations, supplier follow-ups, team coordination, scheduling
- **Trust account administration** — coordination with Toan (and Vy as backup) on day-to-day trust account operations; only escalates if Toan hits a systemic issue
- **Client communication** — routine client emails, acknowledgements, standard responses; escalates only if a client is threatening legal action or cancellation
- **Team issues** — minor team issues, scheduling conflicts, routine HR (leave requests, time-off); escalates only if it involves performance management or a resignation
- **Admin and renewals** — GoDaddy domain renewals, routine supplier renewals under $1,000, standard admin tasks delegated by Bill
- **Compliance monitoring** — tracking s184 certs, insurance renewals, PIQ tickets; escalates to Mary or Bill if anything is overdue or at risk

## What Requires Bill

- Any client threatening to leave or escalating to legal
- Any compliance breach or licensing risk
- Any financial commitment over $5,000
- Hiring decisions (including offers, contracts, terminations)
- Strategic decisions about buildings, pricing, or service scope
- Anything involving the trust account that Vy cannot resolve
- Media or external communications about MTS

## Weekly CoS Check-In

Bill and Keira have a standing weekly 1:1. Keira prepares a simple verbal or Slack update covering:

1. **This week's status** — what she moved, what's stuck, what she needs from Bill
2. **Team pulse** — anything Bill should know about the team (mood, workload, concerns)
3. **Upcoming decisions** — decisions she anticipates landing on Bill's desk next week
4. **Her own flag** — one thing she's uncertain about or would do differently

Bill prepares using `/1on1-prep keira` before the meeting.

## AI Agent Stack — How It Supports Keira

Keira doesn't interact directly with the agent stack, but it works in her favour:

- **7am briefing** — Bill starts the day knowing Keira's open items without her having to brief him from scratch
- **Midday pulse** — catches her escalations while Bill is in ABGF/Liberty and surfaces them at the right time
- **Evening close** — logs what Keira completed so Bill closes the day with accurate status
- **`/1on1-prep keira`** — pre-loads the 1:1 so Bill walks in with her context, not cold

## Related Pages

- [[wiki/actions.md]] — Keira's open action items
- [[wiki/mts-status.md]] — MTS health dashboard Keira contributes to
- [[wiki/PRIMER.md]] — Key people and communication style

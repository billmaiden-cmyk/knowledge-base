---
title: Coaching App Architecture — Delivery Options
created: 2026-04-05
updated: 2026-04-05
tags: [synthesis, coaching, architecture, claude-code, openclaw, dispatch, delivery]
sources: []
---

This synthesis captures the design discussion around how [[Bill Maiden]]'s daily coaching check-in should be delivered — the technical architecture that connects the coach agent to Bill's morning routine and the [[Bill Maiden — Generational Wealth Plan|Generational Wealth Plan]]'s life dimensions.

## The Requirement

Bill wants a daily 5am (AEST) coaching check-in that:
- Reads his previous session notes from `wiki/coaching/`
- Asks how he's feeling and helps set intentions for the day
- Writes session notes back to the knowledge base with cross-references
- Maintains continuity across sessions — remembers patterns, commitments, the arc of development

## Three Options Evaluated (April 2026)

### Option 1: Claude Code Local (Current)

Bill opens Claude Code and types `/coach`, or a session cron fires when Claude Code is open.

| Dimension | Assessment |
|---|---|
| Wiki access | Full — reads and writes directly to local files |
| Reasoning depth | Opus — the most capable model available |
| Continuity | Full — reads coaching history, manifest, all wiki pages |
| Delivery | Requires opening the laptop and Claude Code |
| Setup complexity | Already working |

**Verdict:** Best depth and integration. Weakest on delivery — requires Bill to initiate.

### Option 2: Claude Dispatch (Research Preview)

Launched March 17, 2026. Windows support added April 3, 2026. Bill sends a message from his phone; Claude Desktop executes locally on his machine and notifies him when done.

| Dimension | Assessment |
|---|---|
| Wiki access | Full — executes locally, same file access as Claude Code |
| Reasoning depth | Claude models (likely Sonnet for speed, Opus available) |
| Continuity | Full — same local knowledge base |
| Delivery | Phone-initiated, push notification on completion |
| Setup complexity | QR code pairing; desktop must be on and awake |

**Verdict:** The natural evolution. Solves the delivery problem without sacrificing wiki integration. Currently a research preview with ~50% reliability on complex tasks. *(source: web research, April 2026)*

### Option 3: [[OpenClaw]]

Open-source agent daemon running persistently, delivering via WhatsApp/Telegram/Signal.

| Dimension | Assessment |
|---|---|
| Wiki access | Would need configuration to read/write the wiki directory |
| Reasoning depth | Model-agnostic but typically GPT/DeepSeek; can call Claude API |
| Continuity | Has persistent markdown memory, but not integrated with the existing wiki structure |
| Delivery | Best — always-on, 5am WhatsApp message, no laptop needed |
| Setup complexity | Significant — technical configuration, skill authoring, wiki integration from scratch |

**Verdict:** Best delivery mechanism. Worst integration with the existing knowledge base. Would require substantial work to replicate what Claude Code already does natively.

### Option 4: Claude Code Remote (Scheduled Agent)

Anthropic's cloud-hosted remote agent running on a cron schedule.

| Dimension | Assessment |
|---|---|
| Wiki access | Only via GitHub repo — requires syncing local knowledge base to a remote git repository |
| Reasoning depth | Sonnet (default) or configurable |
| Continuity | Would read from GitHub; writes require pull-back to local |
| Delivery | Fully automated — no laptop, no phone, runs on schedule |
| Setup complexity | Moderate — requires git repo setup and two-way sync with iCloud |

**Verdict:** Fully automated but introduces sync complexity. The git layer between iCloud and GitHub creates a maintenance burden that outweighs the automation benefit at this stage.

## Recommendation (April 2026)

**Stay with Claude Code locally.** The depth of reasoning (Opus), full wiki integration, and the fact that it's already working make it the right choice now.

**Watch Claude Dispatch.** When it matures past research preview, it becomes the natural delivery layer — phone-triggered, local execution, full knowledge base access, no sync issues. This is likely the medium-term solution.

**Revisit in 3 months (July 2026):** Check Dispatch reliability, check if OpenClaw has developed a Claude API + structured wiki skill that could serve as an alternative.

## Update Rules for the Coaching System

Established during the same discussion — how coaching sessions interact with the rest of the wiki:

| Layer | Updated by coaching? | How? |
|---|---|---|
| `raw/` | Never | Immutable source material |
| `wiki/entities/` | Only when facts change | Direct edit with source citation |
| `wiki/concepts/` | Rarely — only if the concept itself evolves | Append with date |
| `wiki/synthesis/` (existing) | Never overwritten | Cross-reference added pointing to revision |
| `wiki/synthesis/` (new revisions) | Yes — when coaching surfaces a real change | New page documenting what changed and why |
| `wiki/coaching/` | Every substantive session | Session notes |
| `wiki/log.md` | Every interaction | One-line entry |

Session notes that are lightweight check-ins get a one-line log entry only, not a full session page.

## Related Pages

- [[Bill Maiden]] — the subject
- [[Bill Maiden — Generational Wealth Plan]] — the plan the coaching system supports
- [[Achievement-Based Self-Worth]] — the pattern coaching tracks
- [[OpenClaw]] — open-source agent alternative evaluated

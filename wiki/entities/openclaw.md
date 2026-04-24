---
title: OpenClaw
created: 2026-04-05
updated: 2026-04-05
tags: [tool, ai, agents, open-source, messaging, automation]
sources: []
---

OpenClaw is a free, open-source autonomous AI agent that runs locally and connects LLMs to real software and services. Unlike chatbot interfaces, OpenClaw can execute shell commands, control browsers, read/write files, manage calendars, send emails, and automate tasks. Its primary interface is messaging platforms — WhatsApp, Telegram, Discord, Signal, Slack, and 30+ others.

## Origin

Created by Peter Steinberger (founder of PSPDFKit/Nutrient), first published November 2025 as "Clawdbot." Renamed to "Moltbot" in January 2026 after an Anthropic cease-and-desist, then to "OpenClaw" three days later. Steinberger joined OpenAI in February 2026 and transferred the project to an open-source foundation.

## Growth

One of the fastest-growing open-source projects in GitHub history — 247,000 stars and 47,700 forks as of early March 2026. Enterprise adoption includes Tencent's ClawPro and NVIDIA's NemoClaw security add-on.

## Architecture

- **LLM-agnostic wrapper.** OpenClaw is not an LLM — it wraps an agent loop around external models (Claude, GPT, DeepSeek, local models via Ollama).
- **Persistent daemon.** Runs continuously, wired to 12+ messaging platforms with heartbeat scheduling and session management. Memory persists between runs.
- **SOUL.md identity system.** Defines the agent's persona, worldview, and personality. Companion files: STYLE.md (voice) and SKILL.md (operating modes). Comparable to Claude Code's CLAUDE.md.
- **Skills system.** Core extensibility mechanism — folders containing instruction files and optional scripts. 5,400+ community skills available. Comparable to Claude Code's slash commands/skills.
- **Local-first data.** All memory stored as Markdown files on local disk.

## Security Considerations

Requires broad permissions (email, calendars, messaging, shell, file system). Misconfigured or publicly exposed instances present significant security and privacy risks.

## Related Pages

- [[Coaching App Architecture]] — comparison with Claude Code and Claude Dispatch for Bill's coaching use case
- [[AI-Enabled Strata Operations]] — potential future delivery layer for MTS agent interactions

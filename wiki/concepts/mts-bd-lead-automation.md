---
title: MTS BD Lead Automation
created: 2026-04-11 10:00 AEST
updated: 2026-04-12 18:30 AEST
tags: [mts, business-development, automation, sales, hubspot, zendesk, ceo-stack, mts-concept]
sources: []
source_date: 2026-04
---

Design for automating the MTS business development lead-to-proposal pipeline. The goal is to reduce Bill's time per lead from ~60–90 minutes to ~25 minutes by automating low-value steps while preserving the high-value discovery call. Part of the [[MTS CEO Stack]] vision for part-time CEO operations. *(Designed 2026-04-09, CEO stack build session)*

## Current Process (Manual)

| Step | Activity | Who | Time | Value to Bill |
|---|---|---|---|---|
| 1 | Lead arrives via HubSpot form → email to Tim → forwarded to Bill | Tim/Bill | 5–30 min lag | Low |
| 2 | Bill texts prospect with personalised message + proposed call time | Bill | 5 min | Low |
| 3 | Discovery call — learn pain points, assess fit | Bill | 15–30 min | **High** |
| 4 | Bill emails service@morethanstrata.com.au to create Zendesk ticket with internal notes | Bill | 10 min | Low |
| 5a | Thao finds the building image — searches realestate.com.au or domain.com.au for the property, copies the image, pastes as background on the proposal PPTX cover slide. **This is the hardest manual step Thao does** | Thao | 15–25 min | Low |
| 5b | Thao finds the ABN (ABN Lookup), updates the agency agreement and proposal with SP number, property address, contact details | Thao | 15–30 min | Low |
| 6 | Thao reassigns to Bill; Bill updates "Our Understanding of the Situation" with pain points from the call — usually responsiveness, lack of progress, or lack of transparency on fees | Bill | 10 min | Medium |
| 7 | Bill applies pricing (rules of thumb, discounts for larger buildings) | Bill | 5 min | Medium |
| 8 | Bill writes cover email — largely standard structure, first paragraph customised to reflect the conversation and map the prospect's specific pain point to MTS's structural answer | Bill | 15 min | Medium |

**Total Bill time:** ~60–90 min per lead
**Total Thao time:** ~30–60 min per lead (building image search is the biggest single task)

## Pain Points Always Map to Five Themes

Prospects consistently describe the same five problems. Bill's pitch addresses each with MTS's structural answer:

1. **Poor responsiveness** → Capacity-demand matching; Zendesk visibility; median first reply < 2 hours
2. **Lack of progress** → Specialist teams; committee reporting; clear plans with owners and deadlines
3. **Conflicts of interest** → No ancillary services; no commissions; insurance rebate model
4. **Unfair fees** → Fair Value model; inclusive management fees; transparent Schedule B
5. **Lack of challenge to contractors** → Specialist leads (Matt — licensed builder; Kat — 18 years R&M)

The cover email and "Our Understanding" section in the proposal are constructed by selecting which of these five themes apply and inserting the prospect's specific examples.

## Target Architecture

### Key design decision: Zendesk as the hub from first contact

Currently the lead doesn't enter Zendesk until after the call. Moving it to arrival means:
- The ticket exists from first contact — SMS, call, notes, proposal, agreement all on one record
- Zendesk Talk + SMS handles text and call natively — logged, recorded, timestamped
- Thao sees it immediately — no email forwarding needed
- Overwatch ([[Kat Bagust]]) can see BD pipeline alongside service tickets
- HubSpot → Zendesk is a native integration

### Automation by step

### Priority 1 — Auto-text from calendar (build early, fast win)

**Goal: Lead arrives → text goes out with Bill's next available slot → call booked without Bill touching it.**

This is the single fastest automation to build. Bill currently texts each lead manually. The automated version:
1. HubSpot form triggers → Zendesk ticket created (native integration)
2. Agent reads Bill's calendar → identifies next available 30-min slot
3. Agent drafts personalised SMS: prospect name, building address, proposed time, and a brief value hook
4. SMS sent via Zendesk SMS — **no Bill approval needed for the initial text** (Bill only needs to take the call)
5. If prospect replies to confirm → calendar hold created automatically
6. If no reply → Khoi's nurture sequence kicks in (manual initially, automated later)

**Why build this first:** It removes Bill from the lowest-value step entirely (Step 2) and makes the response instant instead of hours-delayed. Industry data: response rates drop 10× after the first 5 minutes. *(Updated 2026-04-12, GTM planning session)*

### Priority 2 — Proposal automation (hardest piece: building image)

**Goal: After Bill's call, the proposal and agreement are auto-generated. Bill only writes the "Our Understanding" section and sets the price.**

| Step | Automated approach | Runtime | Difficulty |
|---|---|---|---|
| 1. Lead capture | HubSpot → Zendesk integration (native config). Ticket created automatically with name, email, phone, property address, SP number | Zendesk trigger | Easy |
| 2. Text message | **Auto-send** — reads calendar, drafts SMS, sends via Zendesk SMS. No Bill approval. | Claude Code → later Azure Function | Medium |
| 3. Discovery call | **Not automated.** Bill's high-value activity. Notes captured in Zendesk internal note | Bill | N/A |
| 4. Ticket creation | Already exists from step 1. Bill adds internal notes post-call | Eliminated | Done |
| 5a. Building image | **Agent scrapes realestate.com.au or domain.com.au** for the property address, downloads the hero image, inserts as background on proposal PPTX cover slide. Falls back to Google Street View API if no listing found | Claude Code → later Azure Function | **Hard — see below** |
| 5b. ABN + details | Agent looks up ABN via ABN Lookup API (abn.business.gov.au), fills SP number, address, contact details into proposal PPTX + agreement DOCX | Claude Code → later Azure Function | Medium |
| 6. Pain point mapping | Agent drafts "Our Understanding" from Bill's call notes, mapping to the 5 standard themes. Bill reviews and edits | Claude Code (LLM task) | Medium |
| 7. Pricing suggestion | Agent suggests pricing from lot count × rules; Bill confirms | Claude Code → later Azure Function | Easy |
| 8. Cover email | Agent drafts from template — standard structure, first paragraph maps prospect's pain point (responsiveness / lack of progress / fee transparency) to MTS's structural answer. Bill reviews and sends | Claude Code (LLM task) | Medium |

**Target Bill time:** ~25 min (call + "Our Understanding" edit + pricing + email review)
**Thao time eliminated entirely** — building image, ABN lookup, template filling all automated

### Building image automation — the hardest step *(Added 2026-04-12)*

This is the hardest thing Thao does today: finding the building on realestate.com.au or domain.com.au, finding a good exterior photo, copying it, and pasting it as the background on the PPTX cover slide. Automating this requires:

**Approach options (in order of preference):**

1. **Web scraper → property listing sites.** Search realestate.com.au or domain.com.au for the strata plan address. Extract the hero/main building image from the listing page. Insert into PPTX cover slide as background. Challenges: listings may not exist for strata buildings (only individual units), site terms of service, image quality varies.

2. **Google Street View Static API.** Free tier available. Given the property address, returns a street-level photo of the building. Reliable, always available, no scraping needed. Quality is "good enough" — it's a real photo of the actual building, just not as polished as a real estate listing photo. Fallback for when no listing is found.

3. **Google Places API + Photos.** Search for the building by address, retrieve associated photos. May return better angles than Street View. Slightly more complex to implement.

4. **Manual fallback with prompt.** If automated image sourcing fails, the system opens the search results page for Thao/Khoi to select the right image manually. Still faster than the current process because everything else is already filled.

**Recommended build order:** Start with Google Street View (reliable, simple API, always works) → add realestate.com.au scraping as an enhancement → fall back to manual selection if neither produces a good result.

### Template documents

- **Proposal:** 16-slide branded PPTX. Variable fields: cover slide building image (background), property address, SP number, "Our Understanding of the Situation" (pain points — typically responsiveness, lack of progress, or lack of transparency on fees), pricing (management fee, disbursements, insurance admin fee), Lead Manager name. All other slides are static. *(Updated 2026-04-12 — building image field and common pain points added)*
- **Agency Agreement:** SCA NSW standard contract (DOCX). Variable fields: SP number, ABN (from ABN Lookup), property address, lot count, OC representative name/phone/email, commencement date, management fee amount, review date.

### Build strategy: Claude Code first, Azure later

**Build order** — sequenced by impact and difficulty: *(Updated 2026-04-12)*

| Priority | Layer | Start (now) | Migrate to (Quang builds) | Difficulty | Bill dependency |
|---|---|---|---|---|---|
| **1 (fast win)** | Auto-text from calendar | Claude Code reads calendar, drafts + sends SMS via Zendesk | Power Automate + Graph API + Zendesk SMS | Medium | **Zendesk SMS activation, calendar access** |
| **2** | HubSpot → Zendesk ticket | Zendesk integration (config) | Same | Easy | Config access |
| **3** | ABN lookup + template filling | Claude Code (python-pptx, python-docx, ABN API) | Azure Function | Medium | **Pricing rules from Bill** |
| **4 (hardest)** | Building image sourcing | Claude Code (Google Street View API → realestate.com.au scraper → manual fallback) | Azure Function | Hard | API key setup |
| **5** | Pain point mapping | Claude Code (LLM-native — maps call notes to 5 themes) | Azure Function + Claude API | Medium | None |
| **6** | Cover email draft | Claude Code (LLM-native — standard template + pain point first paragraph) | Azure Function + Claude API | Medium | None |
| **7** | Pricing suggestion | Claude Code (deterministic rules) | Azure Function | Easy | **Pricing rules from Bill** |

**Rationale for starting in Claude Code:** validates the workflow immediately with real leads; no dev time from [[Quang]]; LLM-powered pieces need Claude anyway. Migration is clean because the Claude Code agent prototypes the exact functions that become Azure Functions.

**Rationale for build order:** Auto-text is the fastest win — removes Bill from the lowest-value step entirely and makes response instant. Building image is hardest but also the step that saves Thao the most time (15-25 min per lead). Pain point mapping and cover email are LLM-native tasks that Claude can do well out of the box.

### Pricing rules

*To be confirmed with Bill.* Need:
- Base rate per lot (management fee)
- Discount thresholds for larger buildings
- Insurance administration fee formula
- Schedule B rate card
- Any special pricing rules

## Cover Email Template Structure

The cover email is highly templated. The only customised section is the first paragraph, which maps the prospect's specific pain points to the five standard themes. The remainder of the email covers:

1. Capacity-demand model (responsiveness)
2. Specialist not generalist model
3. No conflicts of interest
4. Fair Value fee approach (inclusions list)
5. Insurance commission rebate model
6. Offer to meet Committee on-site

## Dependencies

- HubSpot → Zendesk integration configured
- Zendesk Talk + SMS activated for BD tickets
- Proposal PPTX template (reference: SP 3049 proposal dated 2026-04-08)
- Agency Agreement DOCX template (reference: SP 3049 agreement dated 2026-04-08)
- Pricing rules from Bill
- `/new-lead` skill to be built in Claude Code

## Status

**Design complete. Not yet built.** Auto-text from calendar identified as fast first build (Priority 1). Proposal automation including building image sourcing is Priority 2-4. Now part of Khoi's AI GTM Architecture deliverable — Khoi proves the workflow manually, documents it, then hands to engineering. *(Updated 2026-04-12 — reprioritised as part of AI GTM platform build)*

## Related Pages

- [[More Than Strata (MTS)]] — the business this automates BD for
- [[MTS Business Strategy (Core)]] — growth targets this supports
- [[Keira — Business Systems & Operations Lead (Strata OS)]] — Strata OS translation (Pillar 2) may own the workflow spec
- [[Quang]] — tech team builds the Azure migration
- [[Kat Bagust]] — Overwatch visibility of BD pipeline
- [[Bill Maiden]] — remains the closer; owns discovery call and pricing

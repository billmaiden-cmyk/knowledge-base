---
title: Google Ads Bridge to 10 Buildings — Assumption Justification
created: 2026-04-12 16:00 AEST
updated: 2026-04-12 16:00 AEST
tags: [mts, gtm, google-ads, assumptions, justification, modelling]
sources:
  - raw/MTS_Google_Ads_Analysis_FINAL_Mar2026.docx
source_date: 2026-03 to 2026-04
---

Detailed justification of the assumptions underpinning the Google Ads optimisation model that projects MTS from 2.75 to ~10 buildings/month at the same $5,162/month ad spend. Each lever is assessed for evidence basis, confidence level, and downside risk. *(Created 2026-04-12, GTM planning session with Bill)*

## Current Funnel — Known Facts (Not Assumptions)

| Stage | Value | Source | Confidence |
|-------|-------|--------|------------|
| Monthly spend | $5,162 | Google Ads account data (5-month average) | **Fact** |
| CPC | $8.40 | Google Ads account data (5-month average, rose 16% over period) | **Fact** |
| Clicks/month | ~615 | Derived: $5,162 ÷ $8.40 | **Derived from facts** |
| Forms/month | ~31 | 154 forms ÷ 5 months | **Fact** |
| Click-to-form rate | ~5.0% | Derived: 31 ÷ 615 | **Derived** |
| Form-to-call | ~50% | Bill Maiden operational knowledge (12 Apr 2026) | **Fact** |
| Call-to-won | ~25–30% | Bill Maiden operational knowledge (12 Apr 2026) | **Fact** |
| Buildings won/month | ~2.75 | Bill Maiden operational knowledge (12 Apr 2026) | **Fact** |
| Impression share | <10% | Google Ads account data | **Fact** |

## Lever 1: Waste Elimination → +1.0 building/month

**Assumption:** Redirecting $866/month from dead spend into converting keywords produces ~6.7 extra form submissions/month.

**Evidence:**
- $866/month waste quantified from actual search term data: $690/month competitor/report/legal/self-managed keywords (negatives now implemented) + $77/month Body Corp ad group (paused) + $38/month Suburbs campaign (paused) + ongoing waste from /trust_value ($304 total, zero conversions) and expired 2024 offer ($2,476 spent)
- At current CPC of $8.40, $866 buys ~103 extra clicks/month
- These clicks go to *converting keywords* (strata contract, change strata, strata management), not the wasted terms. Top converting keywords run at 7–9% form rate, above the 5% account average
- Conservative: 103 × 5.0% = 5.2 forms. Mid-case: 103 × 6.5% = 6.7 forms
- Through current funnel: 6.7 × 50% × 27.5% = +0.92 buildings ≈ **+1.0**

**Confidence: HIGH.** Waste is identified from actual search term reports. Spend is quantified. The only question is whether redirected spend converts at average or above-average rates — and since it goes to proven keywords, above-average is reasonable.

**Downside risk:** +0.5 buildings instead of +1.0. Low consequence.

## Lever 2: CPC Reduction via Quality Scores → +2.0 buildings/month

**Assumption:** Quality score improvement drops CPC from $8.40 to ~$6.30 (–25%).

**Evidence:**
- 19 keywords flagged "low quality" by Google, accounting for ~$10,000 in spend over 5 months (~$2,000/month, 39% of total spend). This includes the top-converting keywords ("strata contract", "change strata") *(source: Google Ads analysis)*
- Google's own documentation states that quality score improvement from below-average to average reduces CPC by 16–50%
- The root cause is diagnosed and specific: ad traffic lands on pages that don't match search intent. The fix is known — build dedicated landing pages matching keyword intent
- 25% CPC reduction is the **midpoint** of Google's published 16–50% range. Not the optimistic end
- At $6.30 CPC: $5,162 ÷ $6.30 = 820 clicks (vs 615 today). Extra: 205 clicks
- Compound with landing page improvements (Lever 3): 205 × 7% × 62% × 28% = **~2.5 buildings**, attribution split between Levers 2 and 3

**Confidence: MEDIUM-HIGH.** Quality score improvements are well-documented in Google's data. Root cause clearly diagnosed. Risk is timing (2–4 weeks after landing page changes) and magnitude. A 15% reduction ($7.14 CPC → 723 clicks) still produces meaningful uplift.

**Downside risk:** 15% CPC reduction instead of 25% → +1.2 buildings instead of +2.0.

## Lever 3: Landing Page Conversion Lift → +2.5 buildings/month

**Assumption:** Click-to-form rate lifts from 5.0% to 7.0%.

**Evidence:**
- **The benchmark already exists in MTS's own data.** /offer-1 converts at **8.1%** on 99 clicks. The 7.0% target is *below* the proven benchmark *(source: Google Ads analysis, landing page performance table)*
- /responsive-service/ (5.4%) uses outdated metrics ("4hr callback guarantee"). Real Zendesk data: 35,489 requests, 88% one-touch, 3hr first reply, 5hr resolution. Updating with proof should improve conversion
- /change-strata/ (4.0%) sends high-intent "change strata manager" searchers to a generic page. A dedicated page matching search intent is standard landing page optimisation
- /offer2 (2.7%) and /offer (2.5%) are being redirected to /offer-1 (8.1%) — near-certain improvement
- The /2024_value/ page (5.9%) shows an expired 2024 offer — updating to current offer is basic hygiene
- Impact at 820 clicks: 820 × 7% = 57.4 forms vs 820 × 5% = 41.0 forms. Extra: ~16.4 forms
- Through funnel: 16.4 × 50% × 27.5% = **~2.3 buildings, rounded to +2.5**

**Confidence: HIGH.** The 7.0% target is below MTS's own /offer-1 benchmark (8.1%). Not projecting a theoretical improvement — projecting that other pages perform closer to a page that already exists in the same account, with the same offer, in the same market. This is the most defensible assumption in the model.

**Downside risk:** Very low. Even reaching 6.0% (modest improvement from 5.0%) produces +1.5 buildings/month.

## Lever 4: Form-to-Call Improvement → +1.5 buildings/month

**Assumption:** Form-to-call rate lifts from 50% to 62%.

**Evidence — two independent drivers:**

**Driver 1: Better pre-qualification (campaign-specific landing pages)**
- Currently a prospect searching "strata defects" lands on a generic responsive service page. They fill the form but their enquiry is low-quality — they wanted defect help, not general management. Bill doesn't want to speak to them.
- A dedicated Defects Playbook page educates the prospect about MTS's defect capability. By the time they fill the form, they know what they're getting. Junk enquiries decrease.
- This is standard landing page optimisation practice — matching search intent to page content pre-qualifies the lead
- Estimated impact: +5–7 percentage points

**Driver 2: Faster follow-up and nurture sequence (Khoi)**
- Currently there is **no follow-up system**. Bill texts the prospect. If they don't respond, the lead is dead.
- Industry data (InsideSales.com, Drift, HBR) consistently shows response rates drop 10× after the first 5 minutes and become near-zero after 24 hours
- Khoi contacts leads within hours. This recovers some of the 50% non-responsive leads
- Khoi runs a multi-touch nurture: text → email with case study → follow-up call → second email. Currently: one text, dead.
- Estimated impact: +5–7 percentage points

**Combined:** 50% + 5–7pp + 5–7pp = **60–64%, mid-case 62%**

**Confidence: MEDIUM.** Pre-qualification from better landing pages is well-evidenced. Speed-of-follow-up improvement depends on Khoi's execution and assumes non-responsive leads are recoverable. 62% is deliberately below the theoretical ceiling.

**Downside risk:** Form-to-call reaches 55% → +0.7 buildings instead of +1.5. This is the widest confidence interval in the model.

## Lever 5: Call-to-Won → Held at 27.5–28%

**Assumption:** Close rate holds steady, not modelled for improvement.

**Evidence:** Bill reports 25–30% and confirms it's not the problem. Proof assets (case studies, Zendesk metrics) may edge it up, but modelling that would be speculative.

**Confidence: HIGH.** Not asking this lever to do anything.

## Compound Model — Full Funnel Maths

The levers compound multiplicatively, not additively:

| Stage | Current | After All Levers | Calculation |
|-------|---------|-----------------|-------------|
| Budget | $5,162 | $5,162 | Same |
| CPC | $8.40 | $6.30 | Lever 2: quality score fix (–25%) |
| Clicks | 615 | 820 | $5,162 ÷ $6.30 |
| Click-to-form | 5.0% | 7.0% | Lever 3: landing page rebuild |
| Forms | 31 | 57 | 820 × 7% |
| Form-to-call | 50% | 62% | Lever 4: pre-qual + Khoi follow-up |
| Calls | 15 | 35 | 57 × 62% |
| Call-to-won | 27.5% | 28% | Lever 5: holds |
| **Buildings** | **2.75** | **9.9** | **35 × 28%** |
| **CAC/building** | **$1,900** | **$520** | **$5,162 ÷ 9.9** |

**The model produces 9.9 buildings — rounded to ~10.** This is not a selected target; it falls out of the maths.

## Scenario Analysis

| Scenario | CPC | Click→Form | Form→Call | Close | Buildings | CAC |
|----------|-----|-----------|----------|-------|-----------|-----|
| **Conservative** | $7.10 (–15%) | 6.0% | 55% | 27.5% | **6.6** | $782 |
| **Mid-case** | $6.30 (–25%) | 7.0% | 62% | 28% | **9.9** | $520 |
| **Optimistic** | $5.90 (–30%) | 8.0% | 65% | 28% | **13.2** | $391 |

Even the conservative case nearly triples output. The mid-case hits 10. The optimistic case uses MTS's own /offer-1 benchmark.

## What Would Invalidate This Model

| Risk | Impact | Likelihood | Mitigation |
|------|--------|-----------|------------|
| Quality scores don't improve despite new landing pages | CPC stays high, clicks don't increase | Low — root cause is diagnosed, fix is proven | Monitor QS weekly from W7; if no movement by W10, investigate keyword-level issues |
| New landing pages convert worse than current | Forms/month drops | Very low — 7% target is below /offer-1 proven benchmark (8.1%) | A/B test new vs old before full cutover |
| Khoi follow-up doesn't improve form-to-call | Rate stays at 50% | Medium — depends on execution and lead quality | Track form-to-call weekly; if flat after 4 weeks, review contact method/timing |
| Market changes (competitor enters, demand drops) | Fewer searches available | Low in short term | Would show as declining impression volume; not a funnel issue |
| /offer-1 benchmark was a small sample (99 clicks) | 8.1% may not hold at scale | Low-medium | Target is 7%, not 8.1% — already includes margin for regression to mean |

## Related Pages

- [[Khoi Nguyen — GTM Onboarding & Impact Plan]] — the execution plan these assumptions feed into
- [[MTS BD Lead Automation]] — the pipeline workflow
- [[MTS One Page Strategy Plan 2026]] — the growth targets this model serves

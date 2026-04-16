---
title: Strata Financial Accounting (NSW)
created: 2026-04-11 14:00 AEST
updated: 2026-04-11 22:00 AEST
tags: [strata, finance, accounting, nsw, legislation, levies, funds, gst, mts-concept]
sources:
  - Strata Schemes Management Act 2015 (NSW) — ss 73, 74, 80
  - SP 4412 financial statements analysis (Apr 2026)
  - Committee Report Finance & Accounting Spec development (Apr 2026)
---

Strata financial accounting in NSW follows the Strata Schemes Management Act 2015. This page captures the domain knowledge required to interpret strata financial statements — fund structure, levy mechanics, expense categorisation, GST treatment, and cash vs equity concepts. It underpins the [[MTS Automated Committee Reporting]] specification and serves as the reference for financial analysis across [[More Than Strata (MTS)]] buildings.

## Fund Structure

Every NSW owners corporation maintains two statutory funds:

### Administrative Fund (s 73)
The AF is an **operating fund** — it funds day-to-day recurrent expenses (insurance, cleaning, management fees, utilities, repairs). It is expected to run close to neutral (small surplus or deficit) over a financial year. A near-zero AF balance is not inherently a problem — it is how the fund is designed to operate. The AF is not meant to accumulate large surpluses. **Do not describe a small positive AF balance as "low"** — this implies something is wrong when the fund is operating as intended. Only flag the AF balance when it is negative or projected to go negative.

**Target AF balance:** The AF should remain **slightly positive** — enough to absorb unexpected expenses and enough buffer that if arrears increased (cash not received), the AF cash balance would remain positive. A zero or negative AF cash balance means the fund has no capacity to absorb shocks and any increase in arrears would push it further negative (i.e., funded by CWF). This principle informs internal assessment but is not stated in the client report.

*(Updated 2026-04-11 ~21:30 AEST, Committee Report v2 spec session — AF balance near zero is by design, not "low"; target AF balance principle added)*

**Deficit mechanics:**
- **Deficit with positive opening balance:** The current period deficit is supported by accumulated surpluses from prior years. The fund balance remains positive — the prior year surpluses absorb the current deficit.
- **Deficit with negative opening balance:** The AF has exhausted its accumulated surpluses. A negative AF fund balance means the AF is effectively being funded by the Capital Works Fund (since both funds share a single bank account). This is unsustainable unless the CWF balance is unusually or unnecessarily high — CWF funds are earmarked for capital expenditure and should not subsidise operating shortfalls.

*(Updated 2026-04-11, Committee Report spec session — deficit mechanics)*

### Capital Works Fund (s 74)
The CWF is for **expenditure of a capital nature** relating to the scheme, including:
- Painting or repainting common property
- Acquiring personal property
- Renewing or replacing fixtures and fittings that are common property
- Replacing or renewing common property
- Other expenditure of a capital nature

⚠ The CWF is **not "project-based"** — this is a common misconception. The legislation defines it as covering expenditure of a capital nature, which includes cyclical renewal, replacement, and maintenance of a capital nature. These are recurring anticipated costs driven by a 10-year plan, not just discrete one-off projects. The correct framing is **lifecycle asset management**. *(source: Strata Schemes Management Act 2015 s 74(2))*

### 10-Year Capital Works Fund Plan (s 80)
Every owners corporation must prepare and annually review a 10-year capital works fund plan. This plan anticipates major expenditure for maintenance, renewal, and replacement of common property and is intended to be used to set annual CWF levy amounts so funds are accumulated in advance. **In practice, many owners corporations do not budget or spend according to their 10-year plan.** The plan is a legislative requirement but actual CWF budgeting and spending decisions are often made independently by the committee. Do not assume CWF expenditure is driven by the 10-year plan unless confirmed. *(Updated 2026-04-11, Committee Report spec session)*

### Single Bank Account
Most schemes hold a single bank account. The AF and CWF balances shown on the Balance Sheet are **accounting allocations** within that account, not separate bank accounts. This has implications when AF cash goes negative — the AF deficit is effectively temporarily funded by the CWF, which is not sustainable.

## Levy Mechanics

### Lifecycle
Levies follow a defined lifecycle:
1. **Raised** — approved at a general meeting (AGM or EGM)
2. **Issued** — sent to lot owners as quarterly levy notices
3. **Recognised** — recorded as income when the quarterly due date arrives (not when cash is received)
4. **Receipted** — cash received from lot owners (levy payments/receipts)
5. **Arrear** — unpaid after the due date

### Income Recognition
Levy income is recognised on the P&L when it falls **due**, regardless of whether cash has been collected. Levy notices are issued 4–6 weeks ahead of the due date — issue and recognition are different events. Recognition occurs at the due date, consistent with standard revenue recognition policy. This means:
- **Levy income on the P&L cannot have a "shortfall"** — levies are recognised at the quarterly due date. If 3 quarterly due dates have passed, 3 quarters of levy income appear on the P&L.
- **Collection shortfalls are a cash issue**, not an income statement issue. Unpaid levies appear as "Levies Receivable" (arrears) on the Balance Sheet and impact cash, not revenue.
- Revenue variances only arise from: (a) an unexpected special levy, or (b) if levies were not issued (administrative failure).

*(Updated 2026-04-11, Committee Report spec session — clarified issue vs due date distinction)*

### Levies Received in Advance
When owners pay before the quarterly due date, cash is received but recorded as a liability (not income) until the due date. This inflates the cash position relative to recognised income.

### Opening Credits on Lot Positions Report
The "Opening Balance" column on the Lot Positions Report shows negative balances (credits) when owners paid levies in advance during the prior period. These credits reduce what the owner needs to pay during the current period. They must be accounted for when calculating effective collection rates — headline "paid" figures will appear lower than "levied" because some of the levy was effectively pre-paid.

## GST Treatment

For GST-registered buildings (check PropertyIQ for GST status):
- **P&L and Balance Sheet** are GST-exclusive
- **Lot Positions Report** is GST-inclusive
- To convert Lot Positions figures to GST-exclusive: divide by 1.1
- Always validate: Lot Positions levied total ÷ 1.1 should equal P&L levy income

## Cash vs Equity

Cash and fund balance (owners' equity) are different concepts:
- **Fund balance** (owners' equity) = Opening balance + YTD surplus/deficit. Shown on the P&L closing balance and Balance Sheet owners' funds.
- **Cash** = Fund balance adjusted for receivables (arrears), payables (creditors), and GST positions. Shown on the Balance Sheet as "Cash at Bank."
- A surplus on the P&L does not necessarily mean more cash — if arrears increased, income was earned but not collected.
- A deficit does not necessarily mean less cash — if creditors increased, expenses were incurred but cash hasn't left the account.

### Cash Bridge (Opening to Closing)
The most useful cash analysis is a bridge from opening to closing cash:
- Opening cash (from prior period Balance Sheet)
- + Surplus/(Deficit) for the period
- − Increase in levy arrears (cash not received)
- + Increase in creditors (cash not paid out)
- ± Movement in GST and other
- = Closing cash

This requires the prior period Balance Sheet. Monthly capture of Balance Sheets is recommended.

### Year-End Cash Forecast
A standard element of cash position analysis is projecting the closing cash at year-end. This uses:
- Current cash balance (from Balance Sheet)
- AF projected movement for the remaining period (from the full-year projection in the budget outlook)
- CWF projected movement (remaining budgeted spend vs remaining levy income)
- Assumption on debtors and creditors (typically held flat unless specific information available)

The forecast gives the committee a forward view of where cash will land, not just where it is now. It should be presented as a simple table: current cash → projected movement → year-end forecast, by fund. State assumptions clearly.

**Calculation rule:**
- Year-end cash = **current cash** (from Balance Sheet) **+ projected remaining P&L result** (projected FY surplus/deficit minus YTD surplus/deficit), **by fund**.
- **Arrears and creditors unchanged** — assume no net change in working capital unless specific information is available.
- This does NOT require the prior period Balance Sheet — it uses the current cash position as the starting point and the full-year projection to derive the remaining movement.
- The prior period Balance Sheet is only needed for the **cash bridge** (explaining how opening cash became closing cash), which is a separate analysis.

**Interpretation:** If the AF year-end cash is projected negative, this means the AF is projected to be temporarily funded by the CWF (single bank account). Flag this in the strata manager internal output. A small negative AF balance relative to CWF cash is not inherently alarming — but it indicates current levies are marginally insufficient to cover annual AF expenses, which should be noted for AGM levy review. Do not claim the deficit "reverses when Q1 levies arrive" — Q1 levies fund Q1 expenses, they do not create surplus cash.

*(Updated 2026-04-11 ~21:00 AEST, Committee Report v2 spec session — added calculation rule, distinguished forecast from cash bridge)*

### Expense Cover Metric
AF expense cover = AF cash ÷ average monthly AF operating expenses (excluding insurance if already paid). Expressed in months. This metric is **context-adaptive** — it is only used when:
- Quarterly AF cash flow is **negative** (expenses exceed levy income), or
- AF cash balance is **negative** (AF funded by CWF)

When quarterly cash flow is positive, the AF balance is recovering and expense cover is not the right measure — use the quarterly cash flow surplus instead. The measure selection is driven by the building's situation, not applied uniformly.

*(Updated 2026-04-11, Committee Report v2 spec session)*

## Revenue Characteristics

Revenue in a strata scheme is **largely fixed** — it is determined by the levies raised at the AGM. Budget vs actual revenue variances are rare and almost always about expenses. Revenue variances only arise from:
- **Special levy** — raised mid-year due to unbudgeted expenditure or insufficient reserves
- **Debtors problem** — a meaningful quantum of levies went uncollected (cash issue, cross-reference to arrears)
- **Administrative failure** — levies not issued (rare but critical — see Trust Accountant process checks)

Because revenue is fixed, the budget in StrataMax is only available as a **full-year figure** (no monthly budget breakdown). This makes YTD-to-budget pro-rata comparison imprecise. A full-year projection is more useful than a YTD percentage comparison.

*(Updated 2026-04-11, Committee Report v2 spec session)*

## Special Levy Triggers

A special levy may be needed when:
- A significant budget overrun means existing levy income is insufficient to cover expenses
- Unbudgeted works are approved (e.g., emergency repairs, compliance orders)
- The CWF balance is insufficient to fund approved or planned capital works
- The AF is in structural deficit (negative opening balance, negative cash flow)

The strata manager needs to identify potential special levy triggers early so they can prepare the committee. The committee report's internal strata manager output should flag any scenario that may require a special levy, with enough lead time for the committee to act before the situation becomes urgent.

*(Updated 2026-04-11, Committee Report v2 spec session)*

## AF Expense Categorisation

AF expenses fall into five categories, each with different projection treatment:

### 1. Insurance (Premiums + Stamp Duties)
- Typically the largest single AF expense
- Paid as an annual lump sum — depresses cash in the payment period
- **Projection:** Use actual if paid; budget if not yet paid. Do not run-rate.
- Insurance timing is the most common cause of a low AF cash balance mid-year. This is a predictable pattern, not a structural problem. **However, the insurance timing explanation is strongest in Q1/Q2** when insurance has been paid but only 1–2 quarters of levy income have been received. By Q3, three quarters of levies have substantially offset the insurance payment — at that point, attributing a low AF balance to insurance timing is misleading. Consider whether the real driver is recurring costs running ahead of budget or uncollected arrears.

*(Updated 2026-04-11 ~21:30 AEST, Committee Report v2 spec session — insurance timing relevance is period-dependent)*

### 2. Fire Safety & Compliance
Fire has two distinct sub-categories that must be treated differently:

**2a. Fire Contract / Inspection (recurring)**
- Statutory servicing obligations: fire panel monitoring, hydrant testing, extinguisher inspection, smoke detector checks
- Frequency varies by building and system — may be monthly, quarterly, or annual
- Not discretionary — required by law regardless of budget
- **Projection:** Run-rate (recurring)
- **Detection from monthly data:** Regular small amounts appearing monthly or quarterly indicate an inspection/monitoring contract

**2b. Fire Repairs & AFSS Remediation (one-off)**
- Repairs and replacements required to achieve compliance with the Annual Fire Safety Statement (AFSS)
- Reactive — triggered by inspection failures, not scheduled
- Typically appears as a spike in a single month, distinct from the regular inspection pattern
- **Projection:** YTD actual only — do NOT run-rate. These are one-off remediation costs.
- **Detection from monthly data:** A large spike in a single month (relative to the regular pattern) suggests AFSS remediation, not routine inspection

**When only a single P&L line is available** (e.g., "Fire - Repairs Servicing") and monthly transaction data is not available, the two sub-categories cannot be distinguished. In this case, treat the full amount as recurring (conservative — better to over-project a statutory obligation than under-project it). When monthly data becomes available, split based on the pattern: regular = contract/inspection (run-rated), spike = AFSS remediation (not run-rated).

*(Updated 2026-04-11, Committee Report spec session — fire split into contract/inspection vs AFSS remediation)*

### 3. Reactive Repairs (One-Off, Lumpy)
- Plumbing, electrical faults, building structural repairs, roof/gutter repairs, lock replacements, door/window repairs
- These are **not suitable for straight-line run-rating** — they are reactive, lumpy, and may not recur
- **Projection:** Include YTD actual as known cost. Do NOT project forward at monthly run-rate. Flag individual lines that have already exceeded their budget.

### 4. Recurring Maintenance (Scheduled/Cyclical)
- General cleaning (contract), rubbish removal
- Gardening (contract and general)
- Utilities (electricity, water/sewerage)
- These are contracted or ongoing — they recur predictably month to month or quarter to quarter
- **Projection:** Run-rate (YTD ÷ elapsed months × 12)
- **Important:** Not all items that appear under a "maintenance" P&L heading are recurring. See § One-Off vs Recurring below.

### 4a. One-Off / Periodic Maintenance
The following items are maintenance (NOT repairs) but are typically **one-off or periodic within a financial year**. Once done, they should not be projected forward — the same treatment as insurance:

- **Pest control / inspection** — typically a single treatment or inspection, not a monthly contract
- **Pressure cleaning** — usually done once per year
- **Window cleaning** — usually done once or twice per year
- **Gutter cleaning** — usually done once or twice per year
- **Audit / accounting** — annual engagement, once done it's done
- **Insurance valuation** — annual

**Projection:** If done (YTD > $0 and the work is complete): use actual, do NOT run-rate. If not done ($0 YTD): use budget if expected to occur, or omit if not expected.

**This is the same logic as insurance, fire AFSS remediation, and reactive repairs** — the question for every expense line is: **will this cost recur in the remaining months?** If no, use the actual and stop. If yes, run-rate. Category tells you WHAT the expense is. Recurrence tells you HOW to project it.

**Detection:** When the Transaction Listing is available, examine individual transactions within a category to determine which are one-off and which are ongoing. When only the P&L is available and one-offs are aggregated into a general line (e.g., pressure cleaning coded to "Cleaning — General"), the one-off cannot be separated. In this case, use straight-line run-rating for the combined figure and flag the separation opportunity internally (not in the client report).

*(Updated 2026-04-11, Committee Report v2 spec session — expanded one-off concept beyond repairs; pest control, window cleaning, gutter cleaning, pressure cleaning all treated as one-off/periodic, not run-rated)*

**Utility billing cycles:** Water/sewerage and electricity are typically billed quarterly (~4 invoices per year). Straight-line run-rating based on elapsed months may not be accurate — e.g., if 4 invoices have been received by month 10, no further invoices are expected and the YTD figure is effectively the full-year cost. When projecting utilities, consider how many invoices have been received relative to the billing cycle rather than simply annualising on elapsed months. The number of invoices received can only be determined from the Transaction Listing — if available, use invoice count to refine the projection; if not, use straight-line run-rating and flag the refinement opportunity internally (not in the client report). *(Updated 2026-04-11, Committee Report spec session)*

### 5. Administration
- Management fees (all sub-lines)
- Accounting (audit, BAS preparation)
- Strata hub / portal fees
- Agent disbursements
- Bank charges
- Legal fees
- Contractor compliance
- Miscellaneous
- **Projection:** Run-rate (YTD ÷ elapsed months × 12)

## CWF Expense Treatment

CWF expenditure is for items of a capital nature. It should **not be run-rated** — expenditure is driven by the 10-year capital works fund plan and the timing of individual works. State YTD actual vs full-year budget and whether further works are expected.

## Monthly Reforecast

The full-year projection produced in each committee report is effectively a **reforecast** — a rolling estimate of full-year expenditure based on YTD actuals plus assumptions about remaining months. Each reporting cycle produces a new reforecast with updated actuals and potentially revised assumptions.

**What to store (per building, per reporting cycle):**
- Reforecast date
- Projected full-year total by fund
- Projected full-year by expense category
- Assumption for each category: run-rated, actual (done for year), budget (not yet incurred), or not projected (reactive)
- Variance to budget (projected vs full-year budget)
- Variance to prior reforecast (how the projection changed since last cycle)

**Why store it:** Creates a time series of projections per building — track outlook month-over-month, audit assumptions, enable trend analysis ("last month we projected $101K, this month $103K — what moved?"). Feeds into the [[MTS Operating Substrate (World Model)]] as structured financial intelligence.

*(Updated 2026-04-11, Committee Report spec session — reforecast concept)*

## Debtor Counting

A debtor is an **owner**, not a lot. One owner with multiple lots counts as one debtor. AF and CWF arrears for the same lot represent one debtor situation, not two. When reporting arrears, aggregate AF + CWF by lot, then group by owner.

### Lot Positions Owner Matching
The Lot Positions Report lists owner names per lot per fund. To determine the true debtor count, match by owner name across lots. One owner may appear on multiple lots — these should be combined into a single debtor position. **Caution:** Owner names can differ slightly across lots (e.g., a trust name on one lot, a personal name on another). Where names differ but appear to represent the same owner, flag for confirmation rather than automatically combining.

*(Updated 2026-04-11, Committee Report v2 spec session — from SP 4412 analysis, Anne Marie Lineman across Lots 10 & 11)*

### Arrears Recency
A levy is an arrear once its due date has passed and it is unpaid — there is no grey area. However, **recency matters for interpretation**. A lot that is 9 days past a quarterly due date is in a different position to one that is 90+ days overdue. When reporting arrears, state the facts (they are arrears) but provide context on recency where relevant (e.g., "some balances are only days past the Q3 due date and may be resolved shortly"). Do not hedge by saying a balance "may not be an arrear" when the due date has passed — it is an arrear, it may just be a recent one.

*(Updated 2026-04-11, Committee Report v2 spec session)*

## Expense Category Aggregation

For client-facing reporting, aggregate related P&L sub-lines into categories rather than reporting at individual line level. This avoids exposing internal allocation issues to clients and gives a more meaningful budget variance picture.

**Standard categories:**

| Category | P&L Lines Included |
|---|---|
| Insurance | Premiums, Stamp Duties, Valuation |
| Cleaning | General, Pressure Cleaning, Window Cleaning, Rubbish Removal |
| Gardens & Lawns | Contract, General |
| Management Fees | Standard, Additional, Arrears Notice, Disbursement, and any other mgmt fee sub-lines |
| Utilities | Electricity, Water/Sewerage |
| Fire Safety | Repairs, Servicing (split into contract vs repair when monthly data available) |

Assess budget variance at the **category level**. An individual sub-line may appear over budget due to coding allocation, but the combined category may be within budget — the category-level view is what matters for the client.

*(Updated 2026-04-11, Committee Report spec session — category aggregation from SP 4412 cleaning analysis)*

## Expense Line Misallocation

StrataMax P&L lines are only as accurate as the coding by the strata manager. Common misallocations include:
- **Cleaning:** Pressure cleaning or window cleaning coded to "Cleaning - General" rather than their specific lines. Always check the combined cleaning category (general + pressure + window + rubbish) before flagging an individual line overrun. If the combined category is within budget but an individual line is over, it is likely an allocation issue rather than a genuine overrun.
- **Repairs:** A repair item coded to the wrong trade line (e.g., a plumbing-related electrical repair coded to "Electrical" instead of "Plumbing").
- **Management fees:** Fee structure changes (e.g., new strata manager) may result in spend appearing under a different sub-line than the one that carries the budget.

**Rule:** Before flagging any individual expense line as "over budget," check whether the combined category (all related sub-lines) is within budget. If it is, note the likely misallocation rather than raising an alarm. Reference the detailed expenditure report (Transaction Listing) to confirm if needed.

*(Updated 2026-04-11, Committee Report spec session — misallocation detection from SP 4412 cleaning analysis)*

## Report Audiences and Their Concerns

Committee reports generate three separate outputs from a single analysis. Each audience has different concerns:

### Committee / Owners (client-facing report)
- Cash position — is it strong, sufficient, or concerning?
- Budget outlook — are we on track for the year?
- Levy collection — are owners paying?
- Actions — what decisions does the committee need to make?

### Strata Manager (internal)
- **Position and performance** — implications for managing the building
- **Budget risk** — categories trending over budget that may require committee communication
- **Special levy triggers** — if a significant overrun or unbudgeted work means existing levies are insufficient
- **Expectation management** — preparing the committee for possible changes in levies
- **Arrears follow-up** — which owners to chase, priority order

### Trust Accountant (internal)
- **Accuracy** — are expense items correctly categorised in StrataMax?
- **Allocation anomalies** — sub-line overruns that suggest miscoding (e.g., pressure cleaning coded to Cleaning — General)
- **Process compliance** — were levies issued and recognised on schedule? Were all required reports generated?
- **Data quality** — reconciliation issues, GST cross-check failures, missing reports to request

*(Updated 2026-04-11, Committee Report v2 spec session — three-audience output model)*

## Closing Balance Relevance

Only reference the closing fund balance when the period result is a **deficit** — this is when it matters, because the reader needs to know whether the fund can absorb the deficit (positive opening balance = absorbed; negative opening = unsustainable). When the period result is a surplus, the closing balance is unnecessary detail and adds length without insight.

*(Updated 2026-04-11, Committee Report v2 spec session)*

## Client-Facing Language Rules

The committee report represents MTS to the committee. Language must be:
- **Present tense** for reported position ("The Owners Corporation holds...", "Total cash is..."). The report reads as a current-state briefing even though it references a point-in-time date.
- **Future tense** for projections ("Quarterly levy income will exceed expenses...", "which will restore the AF balance...").
- **Plain English** — avoid accounting jargon. Write as though briefing a non-accountant committee chair.
- **No repetition** — avoid using the same word (e.g., "quarterly", "holds") in adjacent sentences. Avoid near-synonym qualifiers in the same sentence (e.g., "slightly... marginally", "expected to exceed" alongside "projected").
- **Measured tone** — avoid emphatic or emotive language. Use "categories" not "everything" or "all categories." Use "materially" not "dramatically." The tone should be factual and calm.
- **Concise** — strip methodology notes, GST conversion working, and footnotes from the client report. These belong in internal outputs or the spec, not the committee document. If a label is self-evident from the data (e.g., one-off items are not projected), do not state it.
- **Dates** — omit dates from section narratives when the report header already states the report period.
- **Assessments** — lead with the assessment, then provide the supporting evidence. The assessment reflects the overall picture, not a single number.
- **No unsupported figures** — do not reference a specific number in the narrative unless there is a table or data point in the section that supports it. If the supporting table has been removed (e.g., in the short-form report), either reintroduce the data or reframe the narrative to not depend on it.

*(Updated 2026-04-11 ~22:00 AEST, Committee Report v2 spec session — added measured tone, self-evident labels, near-synonym rule)*

## Key Principles for Financial Reporting

1. Do not assert what is not visible in the data — don't claim creditors are "not overdue" unless ageing data confirms it.
2. Do not assert the absence of items (ATO plans, strata loans) unless confirmed.
3. Use "issued" for levies sent to owners (GST-inclusive, as shown on Lot Positions); "recognised" for levy income recorded on the P&L (GST-exclusive, the accounting event); "receipts" for payments received. The word choice depends on context: when reporting the GST-inclusive amount sent to owners (e.g., Levies & Collections section), use "issued." When reporting P&L revenue, use "recognised."
4. Do not use the word "reserves" when referring to cash balances.
5. Cash is dynamic — do not conflate cash with fund balance (equity).
6. The AF is an operating fund expected to run near neutral — a low balance is not inherently alarming.
7. Insurance timing is the most common driver of low AF cash — explain it, don't alarm on it.
8. Never expose internal data gaps, missing reports, or process issues in the client-facing report — these go in the internal outputs only.
9. A cash position assessment reflects the combination of factors (CWF headroom, AF forward cash flow, structural issues) — not the headline cash number alone.
10. Closing fund balance is only discussed when the period is in deficit — unnecessary when in surplus.
11. Revenue is largely fixed (levy-driven) — variances are almost always about expenses.
12. Creditors get their own section in the client report. When immaterial, a single line is sufficient ("Total creditors are $X. No material outstanding payables."). Do not include creditors within Levies & Collections — they are a separate topic. The strata manager internal output provides additional detail if needed.

*(Updated 2026-04-11 ~22:00 AEST, Committee Report v2 spec session — creditors always get a section, brevity scales with materiality)*

## Related Pages

- [[MTS Automated Committee Reporting]] — the product this knowledge underpins
- [[More Than Strata (MTS)]] — the business
- [[MTS Operating Substrate (World Model)]] — where financial data is ingested and stored
- [[Quang Bui]] — tech lead building the committee report system

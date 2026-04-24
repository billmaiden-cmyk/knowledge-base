# Matt Wrigley — Weekly Status Report

Single-file web app. No install, no server, no account. Opens in any modern browser (Edge, Chrome, Firefox, Safari). Data stored locally on the machine that runs it.

## Quick start

1. Unzip the folder anywhere (Desktop, Documents, OneDrive).
2. Double-click **`launch.bat`** — this opens `index.html` in your default browser.
   *(Alternatively, right-click `index.html` → Open with → any browser.)*
3. Bookmark the page so it's one click next Monday.

That's it. The first time you open it the store is empty; everything builds from there.

## Files in this package

| File | Purpose |
|---|---|
| `index.html` | The app. Open this. |
| `launch.bat` | Windows shortcut — double-click to open in browser. |
| `README.md` | This file. |
| `AZURE.md` | Plan for hosting this at MTS on Azure (future). |

## The six tabs

1. **Dashboard** — current week KPIs across billing, Zendesk weekly dashboard, live CSV response quality, and project portfolio. Colour-coded.
2. **Projects** — the Project Register. Persistent. Maintained as Matt works — not on Monday. Filter chips at top. Click a project to expand milestones.
3. **Trends** — 12-week trend table for every metric.
4. **Enter Week's Data** — Monday form. Billing, PDF dashboard upload + inline preview, CSV upload, 3 narrative boxes.
5. **History & Export** — all saved weeks, JSON export/import for backup.
6. **How to Use** — in-app help.

## Monday morning routine (~10 minutes)

1. Open **Zendesk Explore** → **Matt Dashboard**. Set the time filter to **Previous week** (7 days ending Sunday). Click **Download** to save the PDF.
2. Open the **"Matthew: Open and Pending Tickets"** view in Zendesk (not "My Unsolved Tickets"). Click **Actions** → **Export as CSV**.
3. Open the app → **Enter Week's Data**.
4. Set Week ending (defaults to the Sunday just past).
5. Enter Schedule B billing hours + amount (ex GST).
6. Upload the PDF — it displays inline next to the form — type the tile numbers.
7. Upload/paste the CSV.
8. Glance at the portfolio scorecard. If "Aged 14+d" is non-zero, there's a prompt to review those projects.
9. Write the 2 narrative boxes (what moved / what's stuck).
10. **Preview** → **Save Week**.

## The Project Register

The register is **persistent** — Matt maintains it as he works during the week, not on Monday. Roll-ups (active / on-track / at-risk / blocked) are computed automatically from each project's current milestone.

### Seven built-in templates

Picking a template pre-seeds a milestone sequence — Matt just sets the first target date and the rest cascade based on typical elapsed times.

| Template | Steps | When to use |
|---|---|---|
| **Remediation (standard)** | 17 | Waterproofing, balcony/façade, concrete, underpinning, structural |
| **Fire / Compliance** | 9 | Fire orders, AFSS, sprinkler, passive fire |
| **Defects / SBBIS (Building Bond)** | 10 | SBBS statutory process |
| **Fencing (Dividing Fences Act)** | 6 | Boundary fencing/retaining wall |
| **Roof replacement** | 10 | Single-GM-cycle capital works |
| **Legal — defects claim** | 8 | Bannermans engagements, LoD, litigation |
| **Custom** | 0 | Blank — define your own |

All templates include the key cycles you'd expect: Committee review, EGM (with optional special levy + strata loan milestones), contract, works, DBP Act compliance, closeout.

### RAG is computed, not guessed

Each project's traffic-light status comes from the current milestone's target date vs today:

- **On track** — target date is future
- **At risk** — target date within next 7 days
- **Blocked / Overdue** — target date has passed (Matt can override to blocked with a reason earlier)
- **Planning** — no target date set yet

### Slippage is tracked

The original target date is locked when the milestone is created. If Matt later moves the target forward, the tool records the delta. Project detail shows slippage per milestone; portfolio dashboard shows cumulative.

### Aging

If a project hasn't been touched in 14+ days, it gets an "aged" flag. The weekly entry form surfaces these for review — prompting Matt to confirm still active or archive.

### Bulk add for onboarding

From the Projects tab, **Bulk add…** accepts a paste of projects, one per line:

```
PLAN | NAME | TYPE
4874 | Balconies Remedial Work | remediation-standard
101110 | Lift Door Compliance | fire-compliance
76375 | Water Ingress Remediation | remediation-standard
```

Fastest way to seed Matt's existing 30 projects into the register.

## Data storage

- Stored in browser `localStorage` (key: `mattStatusReport.v4`).
- Auto-migrates from v3 (previous version).
- Nothing leaves the machine.
- **Export JSON weekly** from the History tab for backup. JSON can be imported on any other machine or into the future Azure version.

## Targets baked into the dashboard

| Target | Value | Source |
|---|---|---|
| Hours billed | 22.5/week (→25 from 12 May) | Matt entity page |
| Billing amount | $6,210/week (22.5 × $276) | — |
| Avg hrs/day | 4.5 (→5.0 from 12 May) | — |
| Effective rate | $276/hr | — |
| First response | &lt;120 min | Template |
| Ultra-long >90d | 0 | Template |
| Not responded >24h | 0 | MTS 24-hour first-reply commitment |

All configurable in `index.html` top of the `<script>` block if needed.

## Not included (yet)

- Direct Zendesk API integration (planned — see `AZURE.md`)
- Multi-user shared register
- Email/Slack notifications for aged/blocked projects
- Mobile-optimised view

These all arrive with the Azure hosted version.

---
title: Antonella — Power BI Direct Access (API & Database Integration)
created: 2026-04-19 11:00 AEST
updated: 2026-04-19 11:00 AEST
tags: [trading, antonella, power-bi, azure, api, database, kiet, setup, integration, automation]
sources:
  - Bill Maiden verbal debrief, 19 April 2026 — direct access exploration
  - Downloads/ASX_Setup1_VMA_LiveSignals_2026-04-19.pdf
  - Downloads/ASX_Setup1_SMA_LiveSignals_2026-04-19.pdf
source_date: 2026-04-19
---

This page documents the current data pipeline for Mode A trading signals, the two options for eliminating the manual Excel export step, and the setup instructions for Andrew (MTS admin) to enable direct programmatic access.

## Current Data Pipeline

The trading signal workflow as of April 2026:

1. **Power BI (Azure/MTS)** — Kiet runs Mode A scanner queries against custom Azure databases
2. **Manual export** — Kiet exports results to Excel: `VMA New Trades.xlsx` (75 raw → 29 deployable) and `SMA New Trades.xlsx` (53 raw → 12 deployable)
3. **Python scripts** — process Excel files + fetch daily closes (Yahoo Finance / stockanalysis.com) → path simulation (vma_live_paths.py) + report generation (build_vma_live_paper.py)
4. **PDF output** — reports saved to Downloads (e.g. `ASX_Setup1_VMA_LiveSignals_2026-04-19.pdf`, `ASX_Setup1_SMA_LiveSignals_2026-04-19.pdf`)

Intermediate data files (`vma_live_full.pkl`, `vma_live_paths.csv`, `vma_live_paths.pkl`) are stored in `my-knowledge-base/` root.

The manual export step in (2) is the bottleneck — automating it enables scheduled daily signal generation without Kiet having to trigger anything.

## Option 1 — Power BI REST API (Preferred)

Allows a Python script to POST a DAX query directly to the published Power BI dataset and receive rows as JSON. Keeps all Power BI calculated measures intact.

### What Andrew needs to set up

**Step 1 — Create a Service Principal in Azure AD**
1. portal.azure.com → Azure Active Directory → App registrations → New registration
2. Name: `mts-powerbi-reader`
3. Redirect URI: leave blank → Register
4. Note: **Application (client) ID** and **Directory (tenant) ID**
5. Certificates & secrets → New client secret → set expiry (12 months) → copy **secret value** immediately

**Step 2 — Grant the Service Principal access to the Power BI Workspace**
1. app.powerbi.com → MTS workspace → Workspace settings → Access
2. Add `mts-powerbi-reader` as **Viewer**

**Step 3 — Enable Service Principal API access**
1. app.powerbi.com → gear icon → Admin portal
2. Tenant settings → "Allow service principals to use Power BI APIs" → Enable (either tenant-wide or via security group)

**Step 4 — Collect IDs**
- Navigate to the Mode A dataset in Power BI
- URL format: `https://app.powerbi.com/groups/{workspace-id}/datasets/{dataset-id}`
- Copy both IDs

**Step 5 — Send to Bill (securely — use 1Password, not email)**
- Tenant ID
- Application (client) ID
- Client secret value
- Workspace ID
- Dataset ID
- Ask Kiet: table/measure names used in the Mode A signal views, or a sample DAX query

---

## Option 2 — Direct Azure Database Connection

Bypasses Power BI entirely. Connects Python directly to the Azure SQL / Synapse database that feeds the Power BI model. Simpler setup, but only works if the Mode A signal logic is in the database (not in Power BI calculated measures).

### What Andrew needs to set up

**Step 1 — Identify the source database**
Ask Kiet: *"What database does the Mode A Power BI report connect to?"* — expect Azure SQL Database (`yourserver.database.windows.net`), Azure Synapse, or Azure Data Factory / Fabric. Get the server name and database name.

**Step 2 — Create a read-only database user**
```sql
-- Run as admin at server level
CREATE LOGIN mts_reader WITH PASSWORD = 'choose-a-strong-password';

-- Switch to target database
USE [your-database-name];
CREATE USER mts_reader FOR LOGIN mts_reader;
EXEC sp_addrolemember 'db_datareader', 'mts_reader';
```

**Step 3 — Configure firewall**
1. portal.azure.com → Azure SQL Server resource → Networking → Firewall rules
2. Add rule for the IP where Python scripts run (Bill's machine public IP, or a server/VM IP)

**Step 4 — Send to Bill (securely)**
- Server name (e.g. `yourserver.database.windows.net`)
- Database name
- Username: `mts_reader`
- Password
- Ask Kiet: which schema/table names contain the Mode A signal data

---

## Choosing Between Options

| Criterion | REST API | Direct DB |
|---|---|---|
| Setup complexity | Medium | Low |
| Preserves Power BI calculated measures | Yes | No |
| Works if DB schema changes | Yes (DAX handles it) | Needs query update |
| Requires Power BI Premium | No | No |
| Best when... | Kiet's Mode A logic is in PBI measures | Raw table data is sufficient |

**Andrew's call**: if the Mode A signal conditions are computed inside Power BI (DAX measures, calculated columns), use **Option 1**. If the data arrives from the DB already shaped as signal rows, **Option 2** is simpler.

---

## What This Enables (Once Set Up)

A Claude Code agent (or scheduled Python script) that:
1. Calls the Power BI REST API (or queries Azure DB directly) → gets fresh Mode A signal rows each morning
2. Fetches daily closes from Yahoo Finance (already working in current scripts)
3. Runs existing path simulation + report generation automatically
4. Saves PDF reports to Downloads and optionally pushes summary to Slack

This eliminates the manual Kiet export step and makes daily signal reports fully automated.

---

## Open Items

- [ ] Andrew: confirm which Azure data source Power BI sits on top of
- [ ] Andrew: confirm whether a service principal already exists for MTS Azure
- [ ] Kiet: provide table/measure names for Mode A signal views
- [ ] Bill: confirm preferred option once Andrew provides infrastructure details

---

## Related Pages

- [[Antonella — Power BI Queries]] — the DAX query specs Kiet implements in Power BI
- [[Antonella — Action Priorities]] — where direct access sits in the build sequence
- [[Antonella — Three-Setups Framework]] — the framework the Mode A queries implement
- [[Antonella — Autoresearch System (prepare.py)]] — downstream consumer of Mode B output
- [[MTS Operating Substrate (World Model)]] — the Azure database architecture feeding Power BI

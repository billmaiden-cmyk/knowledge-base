# Azure hosting plan — Weekly Status Report

Purpose: move the local-file tool into an MTS-hosted, multi-user web app. Keep it cheap, secure, and low-maintenance.

## Recommended architecture

| Layer | Service | Tier | Monthly cost |
|---|---|---|---|
| Static web hosting (HTML + JS) | **Azure Static Web Apps** | Free tier | $0 |
| Authentication | **Azure AD (Entra ID)** via Static Web Apps built-in auth | Included | $0 |
| Data store | **Azure Cosmos DB** (serverless) OR **Azure Table Storage** | Free tier / pay-per-request | < $5 |
| Optional backend API | **Azure Functions** | Consumption | < $5 |
| Custom domain | `status.morethanstrata.com.au` | DNS only | $0 |

**Total run cost: under $10/month** for MTS scale (1 user active, 2-3 readers, ~100 project records, ~100 weekly records).

## Why Static Web Apps

1. **Built-in auth with M365** — users sign in with their `@morethanstrata.com.au` Microsoft account. No password management, no separate user directory.
2. **Role-based access** — Static Web Apps supports roles (`admin`, `reader`, `owner`) via Azure AD group membership. Natural fit for "Matt edits his own data; Bill and Kat can read."
3. **Free tier covers MTS** — Static Web Apps free tier: 100 GB bandwidth, 2 custom domains. Easily enough.
4. **Deploys from GitHub** — push to main, it auto-publishes. One-command deploys.
5. **No server to patch** — serverless backend scales to zero when idle.

## Data model on Azure

Keep the same shape as the localStorage JSON. Each user has a single document per user ID:

```
cosmos: container "status-reports"
  pk: userId (AAD object ID)
  doc: { projects: {...}, weeks: {...} }
```

Minimal API surface (3 endpoints on Azure Functions):

- `GET /api/data` — returns the current user's document
- `PUT /api/data` — replaces the current user's document
- `GET /api/user/{id}/data` — readers pull someone else's document (permission-checked)

Everything else (computation, rendering, CSV parsing) stays client-side, exactly as it is now.

## Migration from local to cloud

Seamless. The local tool already exports JSON via History → Export. The hosted version will offer:

- **First login:** "Import existing JSON backup?" → user drops the file → it pushes to their cloud document.
- **Ongoing:** cloud is source of truth. Export still available for belt-and-braces backup.
- **Offline fallback:** the app can continue to work in local-only mode if Azure is unreachable — caches document in IndexedDB, syncs on reconnect.

## Roles (Azure AD groups)

| Role | AAD group | Permissions |
|---|---|---|
| `owner` | `MTS-Status-Owners` | Read/write own data. Matt. Future: other senior strata managers. |
| `reader` | `MTS-Status-Leadership` | Read any owner's data. Bill, Kat. |
| `admin` | `MTS-Status-Admin` | All of above + template library edits, user management. Bill. |

Anyone not in these groups gets a clean "access required" screen.

## Zendesk API integration (natural next step once Azure is live)

Once the backend exists, add a scheduled Azure Function:

- **Weekly cron (Sunday 23:00):** pulls Matt's Open+Pending view via Zendesk REST API, computes the CSV metrics, writes into his weekly document. Tile metrics (tickets received / solved / FRT / full resolution) also pullable via Zendesk Explore API if MTS has that licence.
- **Outcome:** Matt's Monday routine collapses to "open the dashboard, glance at auto-generated numbers, add billing + narrative, save." PDF upload becomes optional.

Zendesk API credentials stored in Azure Key Vault. Zendesk rate-limited API token scoped to read-only.

## Deployment steps (rough)

1. Create Azure resource group `rg-mts-status`.
2. Create Static Web App resource, connect to a new GitHub repo `morethanstrata/status-report`.
3. Copy `index.html` + deployment config into the repo.
4. Enable AAD authentication via Static Web Apps config (`staticwebapp.config.json`).
5. Create Cosmos DB account (serverless), container `status-reports`.
6. Create Azure Function app, deploy the 3 endpoints.
7. Configure custom domain `status.morethanstrata.com.au` (DNS CNAME to Static Web Apps).
8. Create AAD groups + assign Matt, Bill, Kat.
9. Point Matt's existing local JSON export at the cloud via import.

**Effort estimate:** 1-2 days for initial standup, half a day for Zendesk API integration, half a day for QA. Call it 3 days end to end.

## Decisions to make before standing this up

1. **Single-tenant or shared?** — This tool generalises to other senior strata managers. Worth the small extra cost to build it multi-user from the start.
2. **Which Zendesk API scope** — read-only access to Matt's view (and Mary's, Kat's portfolios in future) requires an org-level API token. Need Matt to confirm Zendesk admin can issue that.
3. **Data retention** — indefinite seems right. 100 weeks of data × 30 projects = trivially small.
4. **Who maintains templates?** — templates (Remediation / Fire / SBBIS / etc.) live in code today. Once multi-user, worth moving templates into Cosmos so Bill / Kat can edit without a code deploy.

## Not recommended

- **SharePoint list as data store.** Tempting (we already have M365 licences) but SharePoint lists are awkward for nested data (projects × milestones) and the query performance is poor. Cosmos is the right fit.
- **Power BI.** Matt's weekly report is narrative + live editable state, not a pure BI dashboard. Power BI suits the *trend* view (Trends tab) as a downstream consumer of the JSON export, but isn't the right primary surface.
- **Building in-house auth.** Use AAD. Zero reasons to roll our own.

## Cost projection (36 months)

| Month | Static Web Apps | Cosmos | Functions | Total |
|---|---|---|---|---|
| 1-12 (1 active user) | $0 | ~$2 | ~$1 | ~$3/mo |
| 13-24 (5 users) | $0 | ~$5 | ~$3 | ~$8/mo |
| 25-36 (10 users + API scheduling) | $9 (Standard tier) | ~$8 | ~$5 | ~$22/mo |

Total 3-year spend under ~$500. Rounding error at MTS scale.

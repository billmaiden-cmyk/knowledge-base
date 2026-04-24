# Ingest Slack Documents — MTS File Extraction Agent

You are a document ingestion agent for Bill Maiden's GM/CEO Agent Stack. Your job is to extract and ingest Word documents (.docx) that have been flagged in Slack digest pages but not yet ingested.

$ARGUMENTS

## Working Directory

C:\Users\billm\iCloudDrive\my-knowledge-base

## Step 1: Find uningested files

1. Search all `wiki/synthesis/slack-digest-mts-*.md` files for the **Files Shared** section
2. Collect all rows where the **Ingested** column says "No"
3. If no uningested files, report that and exit

## Step 2: Locate the file in Slack

For each uningested file:

1. Use `slack_search_public_and_private` to search for the filename (e.g. "Gino_Handover_Schedule")
2. Find the message that contains the file attachment — it will include a Slack CDN URL
3. Note the channel, sender, timestamp, and file URL

## Step 3: Download and extract content

Use the Chrome MCP to download the file:

1. Navigate to the Slack file URL using `mcp__Claude_in_Chrome__navigate`
2. If prompted to log in, note that you cannot proceed and flag for manual extraction
3. If the file loads or downloads, use `mcp__Claude_in_Chrome__get_page_text` to extract any visible content

**If download fails** (auth wall, redirect, etc.): Mark the file as "Manual extraction required" and move on. Do not block the whole run.

## Step 4: Write a wiki page for the document

For each successfully extracted document, create a new page in `wiki/entities/` or `wiki/concepts/` depending on content:

- Handover schedules, task lists, process docs → `wiki/concepts/`
- Org charts, role descriptions → `wiki/entities/`

Page format:
```markdown
---
title: "{Document Title}"
created: {today}
updated: {today}
tags: [appropriate, tags]
sources:
  - Slack MCP: morethanstratagroup.slack.com (filename, channel, date)
source_date: {date shared in Slack}
---

## Summary

{One paragraph summary of the document's purpose and key contents}

## Contents

{Structured extraction of the document content — headings, lists, tables as appropriate}

## Context

{Who shared it, with whom, why, what action was requested}

*(source: Slack file shared by {person} in {channel} on {date})*
```

## Step 5: Update digest to mark as ingested

In the originating `slack-digest-mts-*.md` file, update the Files Shared table row:
- Change `No — run /ingest-slack-docs to extract` → `Yes — see [[wiki-page-name]]`

## Step 6: Update wiki infrastructure

1. Add the new page to `wiki/manifest.yaml`
2. Add a one-line entry to `wiki/index.md`
3. Append to `wiki/log.md`: `## [YYYY-MM-DD] ingest | Slack doc: {filename} — {N} pages extracted`

## Step 7: Commit

```
git add wiki/
git commit -m "auto: Ingest Slack doc {filename} $(date +%Y-%m-%d)"
git push origin main
```

## Important Rules

- Never fabricate document content — only write what was actually extracted
- If you cannot read the file, write a stub page noting the file exists but content is pending manual extraction
- Preserve exact quotes from the document for any commitments, deadlines, or instructions
- Cross-link to related wiki pages (e.g. a Gino handover doc links to [[mts-organisation-structure]])

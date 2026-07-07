# Entra Docs Daily Reporter

Daily GitHub Actions report for Microsoft Entra documentation updates in a strict 24-hour window.

The workflow runs at 07:00 Europe/Amsterdam, collects updates from Entra docs sources, and posts a formatted GitHub issue so GitHub notifications can email you updates.

## 1-Minute Quick Start

1. Fork or clone this repository.
2. In GitHub, open **Actions** and run **Entra Docs Daily Reporter** with **Run workflow**.
3. Open the created issue titled `Daily Entra Docs PR Report - YYYY-MM-DD`.
4. Click **Subscribe** on that issue (or watch repo issues).
5. You now receive daily updates through GitHub notification email.

## What You Get

- Strict 24-hour report window (no multi-day section in the issue body)
- Data sources:
  - `MicrosoftDocs/entra-docs` via PR feed
  - `MicrosoftDocs/azure-docs` via commit feed for `articles/active-directory/<subpage>`
- Grouped sections by subpage/category
- Markdown tables in the issue body (email-readable)
- Uploaded artifacts: `html`, `md`, `json`

## Repo Structure

- `.github/workflows/entra-docs-daily-reporter.yml` - Schedule and publishing workflow
- `tools/entra-docs-reporter/report.mjs` - Report generator
- `tools/entra-docs-reporter/README.md` - Extended configuration guide
- `docs/entra-docs-daily-reporter-publish.md` - Copy/paste blog section

## Manual Test

Use this command to trigger a report manually:

```bash
gh workflow run "Entra Docs Daily Reporter" --repo <owner>/<repo>
```

Then check the latest run:

```bash
gh run list --workflow "entra-docs-daily-reporter.yml" --repo <owner>/<repo> --limit 1
```

## Customize

- Main window: `LOOKBACK_HOURS` (default `24`)
- Azure Docs base path: `AZURE_DOCS_COMMITS_PATH` (default `articles/active-directory`)
- Azure Docs tracked subpages: `AZURE_DOCS_SUBPAGES`
- Enable/disable commit feed mode: `USE_COMMITS_FOR_AZURE_DOCS`

## Notes

- No SMTP provider is required.
- Delivery is via GitHub notifications, so account notification settings apply.

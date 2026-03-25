# n8n Automation Portfolio

A collection of production-ready **n8n** workflows for CRM enrichment, data quality, and AI-assisted classification — built around HubSpot, Google Sheets, OpenAI, and third-party APIs.

---

## Workflows

| Project | Stack | Description |
| :--- | :--- | :--- |
| [Contact Enrichment System](./contact-enrichment-system/) | n8n, HubSpot, Apollo.io, Google Sheets | Automatically fills missing mobile phone numbers in HubSpot by triggering Apollo.io enrichment via async webhooks. |
| [ICP Category Update](./icp-category-update/) | n8n, HubSpot, OpenAI (GPT-4o), JavaScript | Two-stage classifier that scores companies as Tech / Non-Tech / Irrelevant using a JS scoring engine, falling back to GPT-4o for ambiguous cases. |
| [Job Titles Update](./job-titles-update/) | n8n, HubSpot, OpenAI, Google Sheets | Standardizes raw job titles into structured seniority and function fields using a lookup sheet first, then AI classification for unmapped titles. |
| [Allegrow Email Status](./allegrow-email-status/) | n8n, HubSpot, Allegrow, Google Sheets | Validates email addresses from Google Sheets via the Allegrow API and writes the verification status back to HubSpot contacts. |
| [Fibery Calendar Transfer](./fibery-calendar-tranfer/) | n8n, HubSpot, Fibery | Syncs HubSpot social media broadcast posts into Fibery as marketing project records every 6 hours. |
| [LinkedIn Slack Agent](./linkedin-slack-agent/) | n8n, LinkedIn, Slack, NocoDB | Monitors LinkedIn activity and routes relevant signals to Slack for team visibility. |

---

## Skills Demonstrated

- **API Integration** — REST APIs, Webhooks, OAuth2, async callback patterns
- **CRM Automation** — HubSpot contact enrichment, property patching, data hygiene
- **AI Integration** — OpenAI GPT-4o for classification and structured output parsing
- **Data Transformation** — Custom JavaScript nodes, JSON manipulation, HTML sanitization
- **Cost Optimization** — Conditional branching to avoid unnecessary API calls
- **Error Handling** — Wait nodes, conditional guards, and safe fallback paths

---

## Setup

Each project folder contains:
- A sanitized `.json` workflow file ready to import into n8n
- A `README.md` with setup instructions and required credentials

**General steps:**
1. Import the `.json` file into your n8n instance.
2. Reconnect credentials (Google Sheets, HubSpot, OpenAI, etc.).
3. Replace any placeholder values (`YOUR_SHEET_ID`, `{{HUBSPOT_API_KEY}}`, etc.) with your own.

> All workflows in this repo have been sanitized — API keys, credential IDs, sheet IDs, and webhook IDs have been removed before publishing.

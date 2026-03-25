# Job Titles Update Workflow

## What this workflow does

This n8n workflow automates **job title standardization and enrichment for HubSpot contacts**.

When a new row is added to a Google Sheet, the workflow:

1. **Triggers from Google Sheets**
   - Watches an input sheet for newly added rows.
   - Each row contains at least:
     - `contact_id`
     - `job_title`
     - `changed_date`

2. **Looks up an existing mapping**
   - Searches a lookup sheet for the same `job_title`.
   - Tries to find previously mapped values for:
     - `job_seniority`
     - `job_function`

3. **Refreshes the update sheet**
   - Clears the target update sheet while keeping the header row.
   - Appends the latest incoming row data to the update sheet.

4. **Merges the lookup result with the new row**
   - Combines the new job title row with the matching lookup-sheet record.

5. **Checks whether classification already exists**
   - If `job_seniority` and `job_function` are already available, the workflow uses them directly.
   - If either value is missing, the workflow sends the job title to an OpenAI model for classification.

6. **Classifies missing titles with AI**
   - The model is instructed to classify each title into fixed allowed values only.
   - Output fields:
     - `job_seniority`
     - `job_function`

7. **Parses the AI response**
   - A JavaScript code node parses the JSON returned by the model.
   - The parsed values are prepared for the HubSpot update step.

8. **Updates the HubSpot contact**
   - The workflow updates the HubSpot contact using the provided `contact_id`.
   - It writes:
     - `job_function2`
     - `seniority_new`

## Business purpose

This workflow helps keep CRM contact data more structured and useful by turning raw job titles into standardized fields.  
That makes it easier to:
- segment contacts
- build better lead routing
- improve reporting
- support targeting and personalization

## Main systems used

- **Google Sheets** — trigger, lookup, and temporary update storage
- **OpenAI** — classification of unmapped job titles
- **HubSpot API** — writes standardized values back to contacts
- **n8n Code nodes** — parses and prepares JSON data

## Expected input

A new row in the source sheet should include fields like:

- `contact_id`
- `job_title`
- `changed_date`

## Expected output in HubSpot

For each processed contact, the workflow updates:

- `job_function2`
- `seniority_new`

## Security notes

This repository version is sanitized for sharing.

Redacted items include:
- HubSpot bearer token
- Google Sheet IDs
- n8n credential IDs and names
- instance-specific workflow metadata

## Important action required

The original workflow file contained a **real HubSpot private app token**.  
That token should be treated as compromised and revoked immediately in HubSpot before using the workflow again.

## Setup before using

1. Import the sanitized workflow into n8n.
2. Reconnect your Google Sheets credentials.
3. Reconnect your OpenAI credentials.
4. Replace placeholder values such as:
   - `YOUR_SHEET_ID`
   - `{{HUBSPOT_API_KEY}}`
5. Confirm the destination HubSpot property names still match your portal:
   - `job_function2`
   - `seniority_new`

## Notes

- The OpenAI prompt is designed to force classification into a fixed list of allowed categories.
- The workflow first prefers an existing sheet-based mapping before calling AI, which helps reduce model usage and keeps classifications more consistent.

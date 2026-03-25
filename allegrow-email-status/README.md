# Allegrow Email Status Workflow

## What this workflow does

This n8n workflow validates email addresses from a Google Sheet using the Allegrow email validation API and then writes the validation result back to HubSpot.

## Workflow steps

1. **Google Sheets Trigger**
   - Watches a spreadsheet for newly added rows.
   - Expects each new row to contain an `Email` value.

2. **Code in JavaScript**
   - Reads incoming rows from the sheet.
   - Normalizes them into a simple structure with an `email` field.

3. **Split Out**
   - Splits the batch so each email is processed individually.

4. **HTTP Request (Allegrow)**
   - Sends each email to Allegrow's validation endpoint.
   - Receives a validation result for that email.

5. **HTTP Request (HubSpot)**
   - Updates the matching HubSpot contact using the email as the identifier.
   - Writes the Allegrow result into the contact property:
     - `allegrow_email_verification_status`

## Business purpose

This workflow helps keep CRM contact data clean by automatically checking whether newly added email addresses are valid and syncing that status to HubSpot. It is useful for:
- lead quality control
- outbound hygiene
- reducing bounce risk
- maintaining better CRM enrichment data

## Required setup

Before using the sanitized workflow, replace the placeholders with your own configuration:

### 1. Google Sheets
- Replace `YOUR_SHEET_ID` with your spreadsheet ID
- Reconnect your Google Sheets credentials in n8n

### 2. Allegrow API
Set your API key in the request header:
- `{{ALLEGROW_API_KEY}}`

### 3. HubSpot API
Set your HubSpot private app token in the authorization header:
- `Bearer {{HUBSPOT_API_KEY}}`

## Expected input

A new row in Google Sheets with a column like:

- `Email`

## Expected output

The workflow updates the corresponding HubSpot contact with:

- `allegrow_email_verification_status`

## Security note

The original workflow contained live secrets, including:
- an Allegrow API key
- a HubSpot private app token
- a real Google Sheet ID

Those values were removed from the sanitized version. You should revoke and rotate any exposed keys before reusing the workflow.

## Files in this package

- `Allegrow_Email_Status_sanitized.json` — sanitized n8n workflow for sharing or GitHub
- `README_allegrow_email.md` — documentation for setup and behavior

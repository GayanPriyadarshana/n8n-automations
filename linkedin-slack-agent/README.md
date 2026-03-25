# n8n Workflow Exports (Sanitized)

This repository contains sanitized n8n workflow exports prepared for public sharing.

## Included files

- `ICP_Category_Update_sanitized.json`
- `LinkedIn_Slack_Agent_sanitized.json`

## What was sanitized

The exported workflows were cleaned to remove or redact environment-specific and potentially sensitive details, including:

- credential IDs and credential names
- webhook IDs
- workflow IDs, node IDs, version IDs, and instance IDs
- Google Sheet document IDs and URLs
- NocoDB project IDs and table IDs
- any obvious token or secret placeholders that could reveal internal setup details

## What was intentionally kept

To preserve the workflow logic and make the files useful as examples, the following were retained where possible:

- node structure and connections
- workflow logic
- prompts and instructions
- generic API endpoints
- model names
- non-secret parameter structure

## Before using these workflows

You will need to replace the redacted values with your own setup details, such as:

- credentials in n8n
- webhook configuration
- Google Sheets document and sheet references
- NocoDB project and table references
- any environment variables or API keys

## Recommended setup pattern

Use environment variables or n8n credentials instead of hardcoding secrets. Examples:

- `{{$env.HUBSPOT_API_KEY}}`
- n8n credential manager for Slack, OpenAI, Google Sheets, and NocoDB

## Security checklist before publishing your own n8n workflow

- remove credential IDs and credential names
- remove document IDs, table IDs, and project IDs
- remove webhook URLs and webhook IDs
- remove internal instance IDs
- verify prompts do not expose proprietary business logic
- verify node names do not expose confidential client or project names
- confirm no pinned sample data contains personal or customer information

## Import note

These sanitized files are mainly for reference and sharing. After importing into n8n, you will need to reconnect credentials and reconfigure any redacted resources before the workflow can run.

## License

Add your preferred license here before publishing.

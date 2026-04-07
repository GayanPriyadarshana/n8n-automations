# Automated Contact Enrichment Pipeline (n8n)

## 📌 Overview
This automation streamlines the sales prospecting workflow by automatically enriching HubSpot contact data. When a new contact ID is added to a Google Sheet, the system checks HubSpot for existing data and uses the **Apollo.io API** to find missing mobile phone numbers via an asynchronous waterfall approach.

<img width="1480" height="592" alt="Image" src="https://github.com/user-attachments/assets/c50f42c7-dd3d-416f-af30-bc76157d3447" />

## 🛠️ The Tech Stack
* **n8n**: Workflow orchestration and logic.
* **HubSpot CRM API**: Data retrieval and contact patching.
* **Apollo.io API**: Data enrichment and "people match" logic.
* **Google Sheets**: Used as the trigger source and tracking log.
* **Webhooks**: To handle asynchronous callbacks from Apollo.

## ⚙️ How it Works
1.  **Trigger**: The workflow polls a Google Sheet every minute for new `hubspot_id` entries.
2.  **Data Fetch**: It retrieves the current contact record from HubSpot.
3.  **Conditional Logic**: An **IF Node** checks if the `phone` field is empty. If data is already present, the workflow stops to save API credits.
4.  **Enrichment Request**: If the phone is missing, it sends a POST request to Apollo.io.
5.  **Data Update**: Upon receiving the enriched data via a Webhook, the workflow updates both the Google Sheet (for tracking) and the HubSpot CRM record.

## 🚀 Key Features
* **Credit Efficiency**: Logic ensures enrichment only runs when data is actually missing.
* **Asynchronous Handling**: Uses webhooks to wait for Apollo's data processing, preventing workflow timeouts.
* **Two-Way Sync**: Keeps the CRM and the tracking spreadsheet perfectly in sync.

## 📂 Setup
1. Download the `.json` file from this repo.
2. Import it into your n8n instance.
3. Replace the placeholder values (`YOUR_API_KEY`, etc.) in the HTTP nodes with your own credentials.

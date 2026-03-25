# AI-Powered ICP (Ideal Customer Profile) Classifier

## 📌 Project Overview
This is a sophisticated automation designed to solve the "messy CRM data" problem. It automatically classifies companies into **Tech**, **Non-Tech**, or **Irrelevant** categories based on industry data. Unlike simple filters, this workflow uses a two-stage validation process: a **weighted JavaScript scoring engine** followed by an **AI-driven website analysis** for ambiguous cases.

## 🛠️ The Tech Stack
* **n8n**: Workflow orchestration and complex branching logic.
* **HubSpot CRM**: The target system for data enrichment.
* **OpenAI (GPT-4o)**: Used for deep-scanning website content to verify B2B status.
* **JavaScript**: Custom-built scoring algorithm for high-speed initial classification.

## ⚙️ How it Works
1.  **Ingestion**: Monitors a Google Sheet for new company records/IDs.
2.  **Stage 1: Deterministic Scoring (JS)**:
    * Runs a 300+ line JavaScript classification script.
    * Identifies "Red Flag" industries for immediate disqualification.
    * Calculates a weighted score based on "Tech" vs "Non-Tech" keywords.
3.  **Branching Logic**:
    * **Confident Matches**: Updates HubSpot immediately to save API costs.
    * **Ambiguous/Irrelevant Matches**: Triggers Stage 2.
4.  **Stage 2: AI Verification**:
    * Workflow scrapes the company website (first 3000 characters).
    * Sends a cleaned payload to GPT-4o to determine if the company is B2B and suggests a corrected industry.
5.  **Final Update**: Patches HubSpot with the finalized ICP category, date, and source metadata.

## 🚀 Key Features
* **Smart Batching**: Uses `Split in Batches` to handle high-volume data without hitting API rate limits.
* **Cost Optimization**: Only triggers expensive AI calls if the local JS engine cannot confidently classify the lead.
* **HTML Sanitization**: Custom JS node cleans raw website HTML into plain text to optimize OpenAI token usage.

## 📂 Installation
1.  Import the `.json` file into n8n.
2.  Set up your HubSpot Private App Access Token.
3.  Configure your OpenAI API credentials.
4.  Ensure your Google Sheet columns match the expected `company_id` and `cb_industries` headers.

Since this workflow contains a lot of custom **JavaScript**, be sure to mention **"Intermediate/Advanced JavaScript for Data Transformation"** as a skill on your CV. This specific file proves you can go beyond "no-code" and actually build custom logic.

**Would you like me to help you create a specific "Technical Skills" section for your CV that highlights these n8n nodes?**

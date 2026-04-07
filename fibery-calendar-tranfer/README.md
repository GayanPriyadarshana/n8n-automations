# Fibery Calendar Sync Workflow

## Overview
This workflow syncs HubSpot social media posts into Fibery as marketing project records.

<img width="1489" height="380" alt="Image" src="https://github.com/user-attachments/assets/6c8d377b-a024-4c37-a073-495c2abe38d9" />

## What it does

1. Runs every 6 hours
2. Fetches social posts from HubSpot (broadcast API)
3. Fetches existing records from Fibery
4. Compares HubSpot posts with Fibery entries
5. Creates or updates records in Fibery:
   - Title
   - Publish date
   - Status
   - Media URL
   - Channel
   - Success metrics

## Flow

Schedule Trigger → HubSpot API → Fibery Query → Processing → Fibery Create/Update

# Fibery Calendar Sync Workflow

## Overview
This workflow syncs HubSpot social media posts into Fibery as marketing project records.

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
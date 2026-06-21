# CLAUDE.md — mikurado-n8n

Part of the **Mikurado umbrella repo** (mounted at `n8n/`). Read the umbrella
[`CLAUDE.md`](../mikurado/CLAUDE.md) first for full product context.

## What this repo is

The **n8n workflow definitions** for Mikurado. n8n is the automation brain — it
orchestrates AI agents, schedules jobs, calls external APIs, and handles OAuth-connected
platform integrations.

Workflows are stored as JSON exports and can be imported directly into any n8n instance.

## Folder structure

```
workflows/
  vehicle/          — Vehicle upload pipeline, data extraction triggers
  seo/              — SEO generation, sitemap update workflows
  social/           — Instagram, TikTok, Facebook publishing workflows
  publishing/       — Content approval → publish pipeline
credentials/        — Credential templates (never store real values here)
```

## Core workflow: Vehicle Upload Pipeline

```
Vehicle Upload (webhook)
  ↓
Vehicle Agent (backend API call)
  ↓
Description Agent
  ↓
SEO Agent
  ↓
AEO Agent
  ↓
Social Agent
  ↓
Notify dealer (email/portal)
  ↓
[Dealer approves in portal]
  ↓
Publishing Agent
  ↓
Website + Social Channels
```

## Workflow naming convention

`[domain]-[action]-[trigger].json`

Examples:
- `vehicle/vehicle-extract-on-upload.json`
- `seo/seo-generate-on-vehicle-ready.json`
- `social/social-instagram-publish-on-approval.json`
- `publishing/publishing-website-sync-on-approval.json`

## Conventions

- **Never** store real OAuth tokens or API keys in this repo — use n8n credential store
- All workflows must have error handling nodes (n8n Error Trigger)
- Webhooks must validate `X-Mikurado-Secret` header for internal calls
- Export workflows from n8n UI as JSON, save here, commit

## How to import a workflow

1. Open n8n at `http://localhost:5678`
2. Go to Workflows → Import from File
3. Select the JSON file from this repo

## Supported integrations (via n8n nodes)

- **Social:** Facebook, Instagram (via Graph API), TikTok, YouTube
- **Automotive:** mobile.de, AutoScout24
- **Business:** Google Business Profile
- **Communication:** WhatsApp Business (via Cloud API)
- **Backend:** Mikurado backend webhooks

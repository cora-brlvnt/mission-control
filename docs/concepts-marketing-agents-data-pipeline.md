# Concepts: Marketing Agents Data Pipeline

**Tags:** #architecture #marketing-agents #data-integration #pipeline #analytics  
**Created:** February 24, 2026  
**Status:** Vision agent (Wave 1) producing output; Wave 2 agents pending

---

## The Problem

Traditional marketing workflows are fragmented:
- Google Search Console (search performance)
- GA4 (traffic behavior)
- Data4SEO (competitive/keyword research)
- Scattered across dashboards, no unified strategy

**Solution:** Automated data pipeline that pulls all signals, synthesizes analysis, outputs actionable strategy documents.

---

## Architecture: Wave 1 (Vision Agent)

**Input:** Client domain + task parameters  
**Process:** Parallel data collection, synthesis, document generation  
**Output:** 1 Google Sheet (keyword data) + 1 Google Doc (strategy report)

```
┌─────────────────────────────────────────┐
│ Task Created: Berelvant SEO Optimization │
│ Client: berelvant.com                   │
│ Drive Folder: /Mission Control Output    │
└─────────────────────────────────────────┘
                    ↓
        ┌───────────────────────┐
        │  Vision Agent Start   │
        └───────────────────────┘
         ↙          ↓          ↘
    GSC MCP    Data4SEO API    GA4 MCP
      ↓             ↓             ↓
  (Parallel collection—no rate limit risk)
    ↙             ↓             ↘
[Search]    [Keyword Data]   [Traffic]
 53 clicks   1900 vol AI      335k users
1840 impr   Automation        89 pv/mo
2.88% CTR   Agency target     Bounce: 60%
   ↓            ↓                ↓
    └────────────┬───────────────┘
                 ↓
    ┌─────────────────────────┐
    │  Synthesis Phase        │
    │  - Opportunity ranking  │
    │  - Competitive analysis │
    │  - Priority keywords    │
    └─────────────────────────┘
         ↙                  ↘
    Google Sheet         Google Doc
    Keyword data         Strategy report
    (69 rows × 3 cols)   (formatted HTML)
         ↓                    ↓
    Task Folder: /Berelvant Q1 2026
```

---

## Data Sources Connected

### 1. Google Search Console (GSC)

**Via:** Cloudflare Worker MCP endpoint  
**Endpoint:** `gsc-mcp-cloud.principal-e85.workers.dev/mcp-direct`  
**Auth:** Bearer token (internal MCP)  
**Key parameters:**
- `property_url` (https://domain.com/)
- `metric` (impressions, clicks, ctr, position)
- `time_period` or `days` (number, not string)
- `query` (natural language: "organic traffic by device")

**Berelvant (90-day snapshot):**
- 53 clicks (tiny; brand only)
- 1840 impressions
- 2.88% CTR
- Declining 60% month-over-month
- Top searches: brand only (zero non-brand organic)

### 2. Data4SEO REST API

**Auth:** Basic auth (principal@berelvant.com : a9e40702a2677bfb)  
**Endpoints:**
- `/v3/keywords/data/{search_engine}/search_volume` — Monthly search volume
- `/v3/keywords_data/{search_engine}/keyword_suggestions` — Related keywords
- `/v3/domain_analytics/{search_engine}/competitors` — Top 10 competitors
- `/v3/domain_analytics/{search_engine}/domain_rank_overview` — Overall domain authority

**Target keywords (from vision agent):**
- "ai automation agency" — 1900 monthly volume
- "ai lead generation" — 1900 monthly volume
- "ai marketing agency" — 1600 monthly volume

**Note:** MCP worker wrapper exists but has Cloudflare auth issues; using direct REST instead.

### 3. Google Analytics 4 (GA4)

**Via:** Cloudflare Worker MCP endpoint  
**Endpoint:** `mcp-ga-cloud.principal-e85.workers.dev/mcp-direct`  
**Auth:** Bearer token  
**Key parameter:** `propertyId` (not `property`)

**Berelvant property (335179630):**
- 335 active users (very low)
- 89 pageviews/month
- 67 users on homepage
- 60% bounce rate
- Essentially no organic traffic outside brand searches

---

## Output Format

### Google Sheet: Keyword Data

**Structure:** keyword | search_volume | difficulty | cpc_usd | target_pages | priority

```
AI Automation Agency          | 1900 | 72 | 2.40 | /services/ai-automation | HIGH
AI Lead Generation            | 1900 | 68 | 2.85 | /solutions/lead-gen | HIGH
AI Marketing Agency           | 1600 | 71 | 2.10 | /about | HIGH
AI Copywriting Tools          | 890  | 65 | 1.95 | /blog/ai-copywriting | MEDIUM
Automated Marketing Systems   | 620  | 58 | 1.40 | /services/automation | MEDIUM
...
[60+ total keywords across segments]
```

**Created by Vision agent:**  
- Location: Google Drive (in task folder)
- Format: gog sheets update (formatted rows)
- Refresh: On-demand (per task run)

### Google Doc: Strategy Report

**Structure:** Markdown → HTML → Google Drive conversion  
**Sections:**
- Executive Summary (market opportunity, positioning)
- Top Keywords (search volume, difficulty, priority ranking)
- Competitive Landscape (top 10 competitors, authority scores)
- Traffic Analysis (GA4 current state, bounce rate, conversion gaps)
- Recommended Actions (priority keywords to target, pages to optimize)

**Example output:**
```
# SEO Strategy Report: Berelvant.com

## Executive Summary
Berelvant is essentially invisible in organic search (53 clicks in 90 days).
Non-brand searches generate zero traffic. Opportunity: $5M+ annual revenue
if we capture top 20 keywords (1900-1600 monthly volume each).

## Top Keywords by Priority
- **AI Automation Agency** (1900 vol, 72 difficulty, HIGH priority)
- **AI Lead Generation** (1900 vol, 68 difficulty, HIGH priority)
- **AI Marketing Agency** (1600 vol, 71 difficulty, HIGH priority)

## Current Traffic Status
- Homepage: 67 active users, 89 pageviews/month (60% bounce)
- Organic traffic: 0 (non-brand searches)
- Conversion rate: Not tracked (GA4 not fully configured)

## Next Steps
1. Content: Create guides for top 20 keywords
2. Links: Competitive analysis + outreach strategy
3. Tech: Fix on-page SEO issues (title tags, schema)
```

---

## Technical Details

### Vision Agent Script Location
`/Users/cora/.openclaw/workspace/projects/marketing-agents/orchestrator/vision-agent.mjs`

### Rate Limiting Patterns Applied
1. Parallel data collection (GSC, Data4SEO, GA4 run simultaneously)
2. Sequential Sheets writes (50 rows batch, 5s pause)
3. Single Doc upload (HTML → gog drive upload --convert)
4. Exponential backoff on rateLimitExceeded

### Test Data (Feb 23)
- Client: Berelvant (id: 6e11d1b0-7092-467c-adb0-3b71512bc756)
- Task: Berelvant SEO Optimization (id: 1247952b-4479-4bc8-b50e-97612595397a)
- Drive Folder: 1k4134SCmsvXu29RoVf0JK-GpfFJbbUyy
- Output Sheet: 1qhFoW8jlDHi1I-TJPVzcCEcPcg720qRBwR_VksQ5LKs
- Output Doc: 1LHNXm1h92Q32J7kizwlmQBYMVBBs8VhEco03ZudJUvM

---

## Next: Wave 2 Agents (Pending)

After Vision agent is approved:

- **Echo Agent** — Email campaign strategy (from Vision keywords)
- **Pixel Agent** — Conversion tracking audit (GTM + GA4 setup)
- **Reel Agent** — Short-form video content ideas (from Vision keywords)
- **Social Agent** — Social media calendar (organic + paid strategy)

Wave 2 agents read Vision agent output (JSON from agent_runs table) and create additional deliverables.

---

## Key Learning: Single Source of Truth

By centralizing all data in one pipeline (Vision agent), we:
1. Avoid conflicting signals from different tools
2. Enable downstream agents to build on validated data
3. Create audit trail (Vision output → Wave 2 execution)
4. Reduce manual data entry errors

This pattern scales: Add new data sources to Vision agent → all Wave 2 agents inherit improvements.

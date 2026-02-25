# Concept: Marketing Agents Wave System

**Captured:** February 25, 2026  
**Related:** Phase 1 complete, Phase 2 in development  
**Status:** Production architecture, proof-of-concept validated

---

## Overview

**Marketing Agents** is a product that uses AI agents to generate marketing strategy + creative assets for digital marketing teams. Built as a Vercel/Mac mini hybrid, it demonstrates Renzo's core positioning: "AI Growth Architect building scalable automation systems."

The system is organized as two **Waves** of execution:
1. **Wave 1 (Data & Strategy)** — Visual intelligence + Market analysis → Google Sheets + Strategy Documents
2. **Wave 2 (Creative)** — Content creation → Google Drive output (docs, spreadsheets, media)

---

## Wave 1: Data, Strategy & Analysis

### Vision Agent (Live)
**Purpose:** Collect SEO/traffic data, analyze competitive landscape, recommend strategy  
**Input:** Client domain (e.g., berelvant.com)  
**Output:** 
- Google Sheet with SEO keywords (top 30-50 with volume, position, CTR potential)
- Google Doc with strategy report (opportunities, low-hanging fruit, content gaps)

**Data Sources:**
- GSC MCP — Organic search keywords, impressions, clicks, CTR, average position
- GA4 MCP — Traffic sources, landing pages, conversion rates, user behavior
- Data4SEO API — Competitor keywords, search volume, bidding data, SERP analysis
- (Future) Web scraping — Competitor content, backlink analysis, topical authority

**Architecture:**
```
Vision Agent (Node.js)
├─ Fetch: GSC keywords + GA4 traffic (parallel)
├─ Fetch: Data4SEO competitor analysis
├─ Analyze: Identify opportunities (high-volume, low-position, high-CTR potential)
├─ Format: Clean data → Google Sheet (formatted, sorted by opportunity)
├─ Write: Strategy report → Google Doc (markdown-to-HTML conversion)
└─ Output: { sheet_id, doc_id, analysis }
```

### Apex Agent (Planned — Wave 1.5)
**Purpose:** Market/trend intelligence (Reddit, Twitter, SEO forums, AI tools landscape)  
**Output:** Trend report + competitive positioning + narrative angles

### Nova Agent (Planned — Wave 1.5)
**Purpose:** Audience intelligence (psychographics, pain points, content preferences from search/social)  
**Output:** Persona document + messaging framework

---

## Wave 2: Creative Execution

Four parallel agents generate marketing assets:

### Echo Agent (Coming)
**Purpose:** Strategy-to-narrative conversion  
**Input:** Vision/Apex/Nova output → strategic themes + target keywords + messaging  
**Output:** 
- Content calendar (30-60 days, theme-based)
- Article outlines (SEO-optimized, with heading structure + keyword placement)
- Landing page copy frameworks

### Pixel Agent (Coming)
**Purpose:** Visual design specifications + moodboards  
**Input:** Brand guidelines + strategy themes  
**Output:**
- Design brief (color, typography, imagery, layout recommendations)
- Ad mockups (LinkedIn, Google Ads, Facebook)
- Social media kit templates

### Reel Agent (Coming)
**Purpose:** Video content strategy + scripts  
**Input:** Strategy + Echo narrative + audience insights  
**Output:**
- Video script templates (YouTube, TikTok, LinkedIn)
- Thumbnail/thumbnail text recommendations
- Hook + Retention + CTA frameworks

### Social Agent (Coming)
**Purpose:** Social media content calendar + copy generation  
**Input:** Strategy + Echo narratives + audience insights  
**Output:**
- Social calendar (60 days, platform-optimized: LinkedIn, X, TikTok, Instagram)
- Hashtag research + community themes
- Engagement copy (CTAs, hooks, replies)

---

## Data Model

### Database Schema
```sql
-- Core tables
clients(id, domain, name, tone_of_voice, brand_url)
tasks(id, client_id, name, drive_folder_url, status, created_at)
agent_runs(id, task_id, wave, agent_type, status, output_data JSONB, output_files JSONB, created_at)

-- Output tracking
output_files(id, run_id, file_type, file_name, file_id, file_url)

-- Workflow automation
workflows(id, client_id, name, schedule, enabled)
```

### Output Structure

**Per-Task Google Drive Folder:**
```
client-name-task-id/
├── 📊 Wave_1_Vision/
│   ├── Wave1_KeywordAnalysis.xlsx (Google Sheet)
│   └── Wave1_StrategyReport.docx (Google Doc)
├── 📊 Wave_1_Apex/
│   └── Wave1_TrendReport.docx
├── 📊 Wave_1_Nova/
│   └── Wave1_AudienceInsights.docx
├── 📝 Wave_2_Echo/
│   ├── Wave2_ContentCalendar.xlsx
│   └── Wave2_ArticleOutlines.docx
├── 🎨 Wave_2_Pixel/
│   ├── Wave2_DesignBrief.docx
│   └── Wave2_AdMockups.pptx (future: image generation)
├── 🎬 Wave_2_Reel/
│   └── Wave2_VideoScripts.docx
└── 📱 Wave_2_Social/
    └── Wave2_SocialCalendar.xlsx
```

---

## Execution Model

### Manual (Current)
1. User creates Task in Vercel UI
2. Click "Run Wave 1" → Orchestrator spawns Vision + Apex + Nova agents (parallel)
3. Agents write output to Drive
4. User reviews in Vercel dashboard or Google Drive
5. Click "Run Wave 2" → Orchestrator spawns Echo + Pixel + Reel + Social agents

### Automated (Future)
1. Cron job runs daily/weekly (based on workflow schedule)
2. Orchestrator spawns appropriate Wave agents
3. Results logged to database + Drive
4. Slack notification with summary + Drive folder link
5. User reviews async, approves for deployment

---

## Key Design Decisions

### 1. Vercel UI + Mac Mini Backend
**Why:** Separation of concerns
- **Vercel** — Client dashboard, task management, output viewing (stateless)
- **Mac mini** — Agent orchestration, long-running jobs, API integrations (persistent)
- **Benefit:** Scale UI independently; agents stay local (faster, cheaper)

### 2. Wave System (Not Multi-Folder Dump)
**Why:** Focus on quality
- **Single output per wave** instead of 7 folders per task (too overwhelming)
- **Proof-of-concept first:** Build Vision well, validate with Renzo, then scale to other agents
- **Benefit:** Cleaner UX, easier QA, less redundancy

### 3. Google Drive as Output Sink
**Why:** Works where customers already are
- **Customers already in Google Workspace** (Gmail, Drive, Sheets, Docs)
- **Agents write directly to Drive** (no download step)
- **Easy sharing** (Drive links, permissions, collaboration)
- **Integration ready** — Drive data auto-feeds into client workflows

### 4. Real Data, Not Mocks
**Why:** Prove ROI early
- **Use customer's own data** (GSC, GA4, website)
- **Show actual opportunities** (not generic templates)
- **Build trust** (customer sees their own insights, validated by multiple sources)

---

## Cost Model

### Infrastructure (Vercel + Mac Mini)
- **Vercel Pro:** $20/mo (Next.js + cron jobs + database)
- **Fly.io (Cora Voice):** $5-10/mo
- **Supabase (logging):** $0-50/mo depending on data volume
- **Data APIs:** $0-100/mo (GSC/GA4 free, Data4SEO $50-500/mo depending on tier)
- **Total:** ~$50-150/mo (excluding Data4SEO, which may be customer responsibility)

### Per-Task Agent Execution
- **Vision Agent:** 1-2 min execution, ~$0.10 (Claude API)
- **Echo/Pixel/Reel/Social:** ~$0.20-0.50 each (future)
- **Monthly (10 tasks, 2x/week):** ~$20-30 (agents) + infrastructure

### Resale Pricing (Future)
- **Per-task:** $50-200 (depending on scope: Vision only vs Wave 1+2)
- **Monthly retainer:** $500-2000 (ongoing optimization)
- **Enterprise:** Custom (Berelvant, Forex.com upmarket)

---

## Competitive Positioning

### Why This Matters
1. **Authority** — Renzo demonstrates AI mastery (not just "marketing guy with AI")
2. **Revenue** — Leads for Berelvant enterprise contracts
3. **Product** — Scalable asset reuse across multiple clients/platforms

### vs. Agency Services
- ✅ **Faster:** Agents work 24/7; humans design/review
- ✅ **Cheaper:** $500-2k/mo vs. $2-5k/mo for human strategist
- ✅ **Consistent:** Data-driven, repeatable process

### vs. No-Code Tools (Zapier, Make)
- ✅ **Custom logic:** Agents understand strategy, not just automation
- ✅ **Real output:** Professional docs (Sheets/Docs), not just database records
- ✅ **Intelligence:** Analyzes data, recommends priorities (not just flow)

---

## Open Questions & Future

### Phase 2 Decisions
- [ ] **Approval:** Are Sheet/Doc output formats good enough? Any changes needed?
- [ ] **Automation:** Manually triggered or automatic on schedule?
- [ ] **Wave 2 launch:** Start with Echo (highest ROI) or all four in parallel?

### Long-Term Vision
- **Personal brand leverage:** Product showcase → Conference talks → Thought leadership → Book deal
- **Team scaling:** Hire operators to run on-boarding + client ops; Renzo focuses on strategy
- **Market expansion:** Domain specialists (PPC, SEO, Social, Email), not just wave system
- **International:** Spanish-language versions (for Renzo's LatAm network)

---

## Technical Notes

### Lessons from Phase 1 Build
- **Google Sheets API:** Rate-limited (~60 writes/min/user); need throttling after 50 rows (5-10s pause)
- **Google Docs:** HTML → `gog drive upload --convert` → proper formatted Doc (Markdown doesn't work)
- **gog CLI quirks:** Sheet updates are one row at a time; `move` uses `--parent`, not `--to`
- **Vercel/Railway:** Next.js needs proper env var setup (fake .env.local can override production)

### Monitoring & Observability
- **Supabase logging:** All agent runs tracked in database
- **Google Drive:** Output folders organized by task + wave
- **Cron health:** OpenClaw monitoring cron success/failure

---

## References
- **Architecture Spec:** `/Users/cora/.openclaw/workspace/projects/marketing-agents/PRD.md`
- **Vision Agent Code:** `/Users/cora/.openclaw/workspace/projects/marketing-agents/orchestrator/vision-agent.mjs`
- **Frontend:** https://github.com/cora-brlvnt/marketing-agents (Vercel deployment)
- **Build Timeline:** Feb 22-24, 2026 (Phase 1 complete in 48 hours)

# Concept: Mission Control — Complete 7-Agent Orchestration Architecture

**Finalized:** February 22, 2026  
**Status:** Documented, Phase 2 ready to build  
**Value:** 3-4 days → 30 minutes (8x faster campaigns)

---

## Overview

Mission Control is a real-time orchestration dashboard that coordinates 7 specialized marketing agents working in parallel. Instead of sequential work (copywriter → designer → videographer → social), all agents produce simultaneously, reducing campaign delivery from 3-4 days to 15-30 minutes.

**System design:** You → Cora (Orchestrator) → Mission Control Dashboard → 7 Agents (parallel polling) → Unified deliverables

---

## The 7-Agent Team Architecture

### Independent Agents (Parallel, no dependencies)

**1. Vision (SEO Specialist)**
- **Input:** Task brief (topic, audience, goal)
- **Process:** Keyword research, gap analysis, content strategy
- **Output:** Keywords (top 20 ranked by volume), gaps, content ideas
- **Example:** "Best keywords for forex trading: best forex broker (8.1K vol), forex trading app (4.4K vol)"

**2. Apex (PPC Specialist)**
- **Input:** Task brief (budget, goal, audience)
- **Process:** Budget allocation, channel strategy, bid recommendations
- **Output:** Channel breakdown (Meta 40%, Google 40%, Other 20%), CPL/CPC estimates, ROAS projection
- **Example:** "Recommend: Meta $4K (CPA $25), Google $4K (CPC $1.20), Other $2K. Projected ROAS 3.2x"

**3. Nova (Analytics Specialist)**
- **Input:** Task brief (goal, audience, timeline)
- **Process:** Success metrics, benchmarking, tracking framework
- **Output:** ROAS target, CAC target, conversion rate benchmarks, kill criteria
- **Example:** "Success: ROAS 3.5x, CAC <$35, CR >2.5%. Kill if ROAS drops below 2.0x"

### Dependent Agents (Parallel after independents)

**4. Echo (Copywriter)**
- **Input:** Task brief + Vision keywords + Apex channels + Nova audience
- **Process:** Generate 5 headline variations (different angles), 10 body copy options, CTA variations
- **Output:** Headlines, body copy, CTAs (all with angle labels + benefits)
- **Example:** Headlines include pain point ("Stop losing money"), opportunity ("Turn $1K into $5K"), and authority ("Trusted by 50K+ traders")

**5. Pixel (Designer)**
- **Input:** Task brief + Echo copy + Brand guidelines
- **Process:** Color palette, typography, layouts for different platforms, image prompts
- **Output:** Design specs, wireframes, platform-specific dimensions, image AI prompts
- **Example:** "Meta (1200x628): Image left, headline + body + CTA right. Colors: Blue #0066FF + Gold #FFD700"

**6. Reel (Video Scriptwriter)**
- **Input:** Task brief + Echo copy + N8N video trends
- **Process:** 15s script (hook + value), 30s script (expanded), 60s script (story structure)
- **Output:** Scripts with production notes, trending sounds, thumbnail ideas
- **Example:** "15s: Hook ('I turned $100 into $5K') + value ('AI signals') + CTA ('DM for free strategy')"

**7. Social (Organic Social Specialist)**
- **Input:** Task brief + Echo copy + All agent outputs + Brand voice
- **Process:** Platform-specific captions (Instagram, Twitter, LinkedIn, TikTok), hashtags, timing
- **Output:** 4 platform posts + hashtags + posting schedule
- **Example:** "Instagram: Emotional, 2-3 paragraphs. Twitter: Evidence-based thread. LinkedIn: Thought leadership. TikTok: Casual hook-first"

---

## Data Flow & Parallel Execution

### Phase 1: Independent Analysis (T+0 to T+5 min)
```
VISION        APEX         NOVA
(keywords)    (budget)     (metrics)
   ↓            ↓            ↓
[Parallel analysis, NO cross-dependencies]
   ↓            ↓            ↓
Comments + Deliverables to Supabase
```
**All three agents work simultaneously. No waiting.**

### Phase 2: Context Propagation (T+5 to T+12 min)
```
              ECHO
        (reads Vision, Apex, Nova)
              ↓
    ┌────────┬┴┬────────┐
    ↓        ↓ ↓        ↓
  PIXEL    REEL  SOCIAL  (all read Echo + own context)
    ↓        ↓     ↓
[Parallel execution, all agents work simultaneously]
    ↓        ↓     ↓
Comments + Deliverables to Supabase
```
**All dependent agents work in parallel. No sequential waiting.**

### Phase 3: Consolidation (T+12 to T+15 min)
```
Supabase real-time subscriptions push all deliverables to dashboard
Dashboard updates:
  - Progress bar: 7/7 agents complete ✅
  - Comments tab: All 7 agent insights
  - Deliverables tab: Copy, design, video, social (organized by type)
```

### Real-Time Example (Time Breakdown)

| Time | Agent | Action | Status |
|------|-------|--------|--------|
| 10:00:00 | YOU | Create task | Task posted |
| 10:00:15 | Vision | Reads task | Analyzing |
| 10:00:20 | Apex | Reads task | Analyzing |
| 10:00:25 | Nova | Reads task | Analyzing |
| 10:02:30 | Vision | Writes comment + deliverable | ✅ Complete |
| 10:02:45 | Apex | Writes comment + deliverable | ✅ Complete |
| 10:03:15 | Nova | Writes comment + deliverable | ✅ Complete |
| 10:05:00 | Echo | Reads Vision/Apex/Nova outputs | Analyzing |
| 10:05:15 | Pixel | Reads task + brand | Analyzing |
| 10:05:20 | Reel | Reads task + trends | Analyzing |
| 10:05:25 | Social | Reads task | Analyzing |
| 10:09:30 | Echo | Writes copy deliverable | ✅ Complete |
| 10:09:45 | Pixel | Reads Echo copy | Analyzing |
| 10:09:45 | Reel | Reads Echo copy | Analyzing |
| 10:09:45 | Social | Reads Echo copy | Analyzing |
| 10:11:30 | Pixel | Writes design deliverable | ✅ Complete |
| 10:11:45 | Reel | Writes video deliverable | ✅ Complete |
| 10:12:30 | Social | Writes social deliverable | ✅ Complete |
| **10:15:00** | **YOU** | **Review all deliverables** | **Dashboard ready** |

**Total: 15 minutes from task to all deliverables ready**

---

## Deliverables Per Agent

### Vision (Keywords + Strategy)
```json
{
  "top_keywords": [
    {"keyword": "best forex broker", "volume": 8100, "difficulty": 62},
    {"keyword": "forex trading app", "volume": 4400, "difficulty": 45}
  ],
  "content_gaps": [
    {"keyword": "forex demo account", "opportunity": "HIGH"}
  ],
  "content_ideas": [
    {"topic": "Comparison Guide", "angle": "vs. competitors"}
  ]
}
```

### Apex (Budget + Channel Strategy)
```json
{
  "allocation": {
    "meta": {"budget": 4000, "cpl": 8, "expected_leads": 500},
    "google": {"budget": 4000, "cpc": 1.2, "expected_clicks": 3333}
  },
  "bid_strategy": "target_roas_3x",
  "roas_projection": 3.2
}
```

### Nova (Metrics + Benchmarks)
```json
{
  "success_metrics": {
    "roas": 3.5,
    "cac": 35,
    "conversion_rate": "2.5%"
  },
  "kill_criteria": {
    "if_roas_below": 2.0
  }
}
```

### Echo (Copy Variations)
```json
{
  "headlines": [
    "Stop Losing Money on Bad Forex Trades",
    "Turn $1,000 into $5,000 in 30 Days"
  ],
  "body_copy": [...10 variations...],
  "ctas": ["Start Free Trial", "Claim Your Trading Edge"]
}
```

### Pixel (Design Specs)
```json
{
  "color_palette": {
    "primary": "#0066FF",
    "accent": "#FFD700"
  },
  "layouts": [
    {
      "platform": "Meta",
      "dimensions": "1200x628",
      "layout": "Image left, headline + body + CTA right"
    }
  ],
  "image_prompts": [...]
}
```

### Reel (Video Scripts)
```json
{
  "scripts": {
    "15s": {
      "hook": "I turned $100 into $5,000 trading forex",
      "value": "Using our AI signals, no experience needed",
      "cta": "DM for free strategy"
    },
    "30s": {...},
    "60s": {...}
  },
  "production_notes": "Fast cuts first 5 sec, slow for CTA"
}
```

### Social (Platform-Specific Posts)
```json
{
  "instagram": {
    "caption": "The best trading platform... 📈",
    "hashtags": ["#forex", "#trading"]
  },
  "twitter": ["Thread 1...", "Thread 2..."],
  "linkedin": "Professional thought leadership...",
  "tiktok": "Casual hook-first script..."
}
```

---

## Business Impact

### Speed
- **Before:** Task → Copy (1 day) → Design (2 days) → Video (3 days) → Social (1 day) = **3-4 days**
- **After:** All agents parallel = **15-30 minutes**
- **Improvement:** **8x faster**

### Scalability
- **Before:** 1-2 campaigns/week (manual bottleneck)
- **After:** 5+ campaigns/week (parallel processing)
- **Improvement:** **5x more throughput**

### Quality
- **Before:** Single angle per deliverable type
- **After:** 5 headline variations, 10 copy options, 3 video scripts, 4 platform posts
- **Improvement:** **3-5x more variations** (better A/B testing)

### Cost
- **Before:** $2K-5K/week (agency rates for copywriter, designer, videographer)
- **After:** $50-100/mo (tool cost) + your time reviewing
- **Improvement:** **90% cost reduction**

### ROI
- **Value per campaign:** 3-4 days saved = $1K-5K (your consulting/billable time)
- **Frequency:** 4 campaigns/week
- **Monthly impact:** $16K-100K value created
- **Annual:** $192K-1.2M value (with scaling)

---

## Phase Roadmap

### Phase 1: Dashboard Foundation ✅ COMPLETE
- Supabase schema (4 tables: tasks, comments, deliverables, agent_status)
- Next.js UI (task form, task list, task detail)
- Real-time Supabase integration
- Deployed to Railway

### Phase 2: Agent Polling 🔄 IN PROGRESS
- Agent runner (Node.js cron service)
- Task polling (agents check for new tasks every 15 min)
- Deliverable submission (agents write to Supabase)
- Real-time dashboard updates
- **Timeline:** 4-6 hours to build

### Phase 3: Sub-Agent Spawning ⏳ PLANNED
- Replace static prompts with spawned Claude sub-agents
- API access for agents (GA4, GSC, SA360)
- Iterative decision-making per agent
- **Timeline:** 8-12 hours

### Phase 4: External Data ⏳ PLANNED
- GA4 integration (Nova reads real metrics)
- GSC integration (Vision reads real keywords)
- SA360 integration (Apex reads real performance)
- **Timeline:** 6-8 hours

### Phase 5: Publishing ⏳ PLANNED
- Meta Ads API (Pixel's design → auto-create ads)
- Google Ads API (Echo's copy → auto-create search ads)
- Email publishing (send sequences)
- Social scheduling (auto-post captions)
- **Timeline:** 8-10 hours

---

## Success Metrics

| Metric | Target | How Measured |
|--------|--------|-------------|
| Task completion time | < 30 min | Timestamp: task created → all agents deliver |
| Deliverable quality | 8/10+ | Manual review scoring (utility, accuracy) |
| Agent consistency | 95%+ | Deliverables follow expected JSON structure |
| Usability | NPS > 8 | User feedback on dashboard experience |
| Reusability | 90%+ | % of deliverables used without heavy editing |

---

## Failure Modes & Mitigations

| Failure | Symptom | Mitigation |
|---------|---------|-----------|
| Agent hallucinates | Wrong data in deliverable | Validation layer + fact-check |
| Agent timeout | Task > 30 min | Add timeout, fallback to previous |
| Low quality | Needs heavy editing | Improve prompt, add QA checkpoint |
| Agent contradictions | Copy ≠ design messaging | Consistency check, flag conflicts |
| Missing task context | Agent can't understand | Validate task has min fields |

---

## Strategic Positioning

**Current:** Marketing execution agency (YOU do the work)

**Post-Mission Control:** Marketing orchestration platform (AGENTS do the work, YOU review)

**Impact:** Shift from "labor" to "leverage" — scale campaigns without scaling team

---

## Files Reference

**Documentation:**
- Full ecosystem: `/workspace/MARKETING_AGENTS_ECOSYSTEM.md`
- Build plan: `/workspace/MISSION_CONTROL_DASHBOARD_PLAN.md`
- Project overview: `/workspace/MISSION_CONTROL_PROJECT.md`

**Code:**
- GitHub: https://github.com/cora-brlvnt/marketing-agents
- Dashboard: `/dashboard` (Next.js 14)
- Agents: `/agents` (system prompts)

**Infrastructure:**
- Supabase: `ieirkjgfompuevwalzga`
- Deployment: Railway (marketing-agents-dashboard-production.up.railway.app)

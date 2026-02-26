# Concept: Async Execution Enables 24/7 Operation (Feb 26, 2026)

**Category:** Operational pattern  
**Domain:** Multi-agent systems + autonomous work  
**Status:** Proven Feb 22–25  
**Cost:** Mac mini + Supabase (already operational)  

## Core Insight

When agents execute asynchronously (Mac mini running 24/7), users can submit work anytime and retrieve results later. No waiting. No blocking. Humans offline ≠ work stops.

## The Problem

**Synchronous workflow:**
```
User: "I need a campaign brief"
Agent: "OK, give me 2 hours"
User: "Sitting and waiting..."
(2 hours later)
User: "Finally! Let me review..."
```

**Cost:** 2 hours of user time blocked per deliverable

**Async workflow:**
```
User (10 PM): "I need a campaign brief"
Agent: "Task created. I'll work on it."
User: "Thanks! I'm going to sleep."
Agent: (works 11 PM – 12 AM)
User (8 AM): "Great! Results ready when I woke up."
```

**Cost:** 0 hours of user waiting

## How It Works

### Architecture

```
Vercel (UI)
├── Dashboard
├── Task creation form
└── Results viewer

↓ (submit task)

Supabase (queue + results)
├── tasks table (status: pending → complete)
├── agent_runs table (all outputs)
└── deliverables table (final artifacts)

↓ (poll for work)

Mac mini (execution engine)
├── OpenClaw cron (polls Supabase every 15 min)
├── Agent runners (Vision, Apex, Nova, Echo, Pixel, Reel, Social)
├── Tool access (gog CLI, MCP servers, Data4SEO, Gemini, etc.)
└── Output writers (Google Drive, Supabase)

↓ (write results)

Google Drive + Telegram
├── task-2026-02-26/
│   ├── vision-output.sheet
│   ├── apex-output.doc
│   └── ...
└── Telegram notification: "Task complete!"
```

### Workflow

1. **User submits task** (10 PM, any time)
   - Dashboard form → task created in Supabase
   - Status: `pending`

2. **User goes offline**
   - Can close Dashboard
   - Can sleep, travel, work on other things

3. **Mac mini polling** (runs 24/7)
   - OpenClaw cron wakes up every 15 minutes
   - Query Supabase: `SELECT * FROM tasks WHERE status = 'pending'`
   - Found 1 task

4. **Agents execute** (all in parallel)
   - Vision: Analyze brand + market (30 min)
   - Apex: Analyze SEO/SEM (20 min)
   - Nova: Analyze performance data (25 min)
   - All write results to Supabase + Google Drive

5. **User comes back** (8 AM)
   - Opens Dashboard
   - Task status: `complete`
   - Results ready to review
   - No waiting

## Key Design Decisions

### 1. **Polling, Not Webhooks**
- Mac mini polls Supabase every 15 min (configurable)
- Simple, reliable, no external dependencies
- One cron job handles all agents
- Alternative: Use Supabase real-time (faster but more complex)

### 2. **Supabase as Queue**
- Tasks table stores work
- Agent_runs table stores outputs
- Simple JSON schema; no message broker needed
- Works offline (Mac mini can queue locally if DB down)

### 3. **Mac mini as Execution Engine**
- All tools available (gog CLI, MCP servers, etc.)
- Full cloud API access (Google Drive, Deepgram, etc.)
- No serverless cold start delays
- Costs ~$5/month electricity (already running)

### 4. **Output to Google Drive**
- Organized folder per task (task-2026-02-26/)
- Subfolders per agent (vision/, apex/, nova/)
- Easy to share with clients
- Integrates with existing Google Workspace

### 5. **Telegram Notification (Optional)**
- User gets ping when task complete
- Can review async
- Keeps Telegram in the loop (already a hub for work)

## Real Example: Phase 1 Build

**Feb 22, 6:04 AM:**
- Renzo approves: "Build Phase 1 Mission Control"
- Task created: status = `pending`

**Feb 22, 6:05 AM – 11:59 PM:**
- Cora (agent) executes for 18 hours
- Renzo sleeps, works, travels (offline)
- Everything builds while he's away

**Feb 23, 12:00 AM:**
- Vision agent finishes
- Results: Google Docs + Sheet in Drive
- Status: `complete`
- Telegram ping: "Phase 1 ready for review"

**Feb 23, 10:00 AM:**
- Renzo wakes up, opens Dashboard
- Everything ready
- No waiting

## Advantages

1. **Zero blocking** — Users don't wait
2. **Always-on operation** — Work continues 24/7
3. **Scales to multiple users** — Shared agent pool
4. **Cost efficient** — Mac mini already running; marginal cost ~$0
5. **Simple architecture** — Polling + Supabase + Google Drive
6. **Resilient** — Agents can retry if network issues

## Disadvantages

1. **Requires always-on Mac mini** (uptime critical)
2. **Polling is slower than webhooks** (15-min delay vs. instant)
3. **No real-time dashboard updates** (refresh to see new results)
4. **Bandwidth:** Agents hit Google APIs frequently

## Real-World Trade-offs

| Trade-off | Async | Sync |
|-----------|-------|------|
| User wait time | 0 hours | 2+ hours |
| Machine cost | ~$5/mo | Same |
| Complexity | Simple (polling) | Simple (direct call) |
| Scalability | High (1 user ≠ 1 agent) | Low (1 user = 1 agent) |
| Offline support | Yes | No |
| Real-time feedback | No (delayed) | Yes (immediate) |

**Winner for startup:** Async (costs less, enables more work)  
**Winner for real-time apps:** Sync (user expects instant feedback)  

## Implementation Checklist

- [ ] Supabase schema (tasks, agent_runs, deliverables)
- [ ] Dashboard form (submit task)
- [ ] OpenClaw cron job (poll every 15 min)
- [ ] Agent runners (all 7 agents)
- [ ] Output writers (Google Drive + Supabase)
- [ ] Telegram notification (optional)
- [ ] Dashboard results viewer
- [ ] Error handling (retry failed agents)
- [ ] Monitoring (log all cron runs)

## Next Steps

1. Document expected latency (15 min polling = 15–30 min task completion)
2. Add real-time updates (Supabase websocket) if users need faster feedback
3. Build monitoring dashboard (Telegram alerts on agent failures)
4. Test with real workload (5+ concurrent users)

---

**Status:** Proven. Pattern for all async, always-on systems.

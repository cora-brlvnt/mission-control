# Cron-Async Operating Model

## Core Pattern
**All work executes asynchronously on schedule. Operator freed for strategy. Full context preserved.**

---

## How It Works

### 1. Task Definition
```
Every 30 minutes: Telegram message capture → Supabase embedding → Index
Every 6 hours: 2Brain idea capture → GitHub commit → Sync
Daily @ 6 AM: Infrastructure health check → Report
Daily @ 12 PM: Task & decision status capture → Log
Daily @ 6 PM: End-of-day summary → Mission Control update
```

### 2. Execution
- Cron jobs run on schedule (no manual intervention)
- All output logged + timestamped
- Failed tasks generate alerts (not silent failures)
- System recovers gracefully from transient errors

### 3. Context Preservation
- Every execution creates a dated log entry (memory/YYYY-MM-DD.md)
- Daily capture to Mission Control (journal/YYYY-MM-DD.md)
- All decisions, insights, work products stored + searchable
- Zero information loss between sessions

### 4. Operator Workflow
- Check heartbeat status (health + blockers)
- Review daily capture (what changed, what's next)
- Make strategic decisions (don't manage ops)
- Execute high-impact work
- Cron handles low-level tasks automatically

---

## Benefits

### Cognitive Load Reduction
- Operator not distracted by infrastructure maintenance
- No "check this manually" overhead
- All context automatically logged
- Can jump back in after days away with zero catch-up friction

### Consistency
- Tasks execute on schedule regardless of operator availability
- No skipped work due to time zone, sleep, focus
- Auditable trail of all operations
- Easier to debug patterns (compare across multiple runs)

### Scalability
- Adding new cron job = add 1 function + attach to schedule
- No increase in operational overhead
- Can run 20+ parallel jobs on same infrastructure
- Proven stable at current load (24+ days uptime)

---

## Current Cron Ecosystem

| Job | Schedule | Purpose | Status |
|-----|----------|---------|--------|
| Telegram capture | Every 30 min | Archive + embed messages | ✅ Live |
| 2Brain sync | Every 6 hours | Capture ideas → GitHub | ✅ Live |
| Infrastructure check | Daily 6 AM | System health audit | ✅ Live |
| Midday checkpoint | Daily 12 PM | Decision + task status | ✅ Live |
| Daily capture | Daily 6 PM | Work summary + insights | ✅ Live |

---

## Example Workflow: Phase 1 → Phase 2 Transition

**Without async model:** 
- Operator must manually check status daily
- Context scattered across Slack, Telegram, notes
- Decisions lose momentum while waiting for approval
- Risk of forgotten action items

**With async model:**
- Daily capture auto-generates status (what's done, what's blocked)
- All context automatically indexed + searchable
- Decision deadlines tracked (overdue items escalated automatically)
- Next actions always clear from yesterday's capture

---

## Anti-Patterns to Avoid

### ❌ Silent Failures
If cron job fails, log it + alert (don't assume manual follow-up)

### ❌ Lost Context
Always write output to dated file (never assume next session will remember)

### ❌ Unbounded Jobs
Each cron should have max duration (if exceeds, kill + alert)

### ❌ No SLA Tracking
Important decisions should have explicit deadlines (48–72h default)

---

## Scaling Rules

- **0–5 cron jobs:** Current state, proven stable
- **5–15 cron jobs:** Add monitoring (check execution health daily)
- **15+ cron jobs:** Migrate to cron scheduler with alerting (not launchd)
- **50+ cron jobs:** Consider splitting across multiple hosts (load balance)

---

## Cost Structure
- $0 additional cost per new cron job (all in-house)
- Observation: Cron-async model is cost-optimized (no serverless tax)
- Scales to 2–3x current workload with same infrastructure

---

**Pattern proven:** February 14 – March 9, 2026 (24+ days continuous uptime, zero manual interventions).

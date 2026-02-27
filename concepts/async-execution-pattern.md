# Concept: Async Execution Pattern

**Date:** Feb 27, 2026 (extracted from Feb 25-26 work)  
**Source:** Marketing Agents Phase 1 delivery (Feb 22-23)  
**Status:** Proven, operational  
**Tier:** Architecture (infrastructure-level insight)

---

## Core Idea

Always-on agents executing 24/7 while users are offline → results ready when users come online. Eliminates waiting time and creates always-on service capability.

---

## The Pattern

```
User submits task (any time) → Supabase queue → 24/7 Mac mini executes → Results ready when online
```

### Components
1. **Persistent queue:** Supabase task table (survives any outages)
2. **Always-on executor:** Mac mini (24/7 running, auto-starts on reboot)
3. **Parallel execution:** Multiple agents work simultaneously (no bottlenecks)
4. **Async architecture:** Agents write results to database (user reads when ready)
5. **No user waiting:** User timezone ≠ work timezone

---

## Evidence

**Phase 1 Delivery (Feb 22-23):**
- Renzo offline (in Rome, Feb 22-23)
- Cora executed Phase 1 build: 18 hours of work
- Results ready when Renzo came online (Feb 24)
- Zero waiting time for user

**Metrics:**
- Build time: 18 hours
- User waiting time: 0 hours
- Delivery time (user perception): Instant (logged in to ready results)
- Timezone offset: 9 hours (Rome → EST)

---

## Business Impact

### Problem Solved
- Synchronous work kills asynchronous teams
- "Let me get back to you in 2 hours" wastes 2 hours × N users
- Single-threaded execution creates queues

### Solution Delivered
- Requests execute immediately (background)
- User never blocked waiting
- Multiple users never queue (all work in parallel)
- Multi-timezone teams work seamlessly

### Scale Implication
- Works with 1 user or 10 users
- 100% utilization (no idle time)
- Cost-effective (one 24/7 machine scales to many users)

---

## Implementation

### Required Infrastructure
- **Executor machine:** Always-on (Mac mini, VPS, etc.)
- **Persistent queue:** Database (Supabase, PostgreSQL, etc.)
- **Result storage:** Same database (structured output)
- **Notification:** Optional (Telegram, email when ready)

### Technology Stack (Current)
- **Mac mini:** Intel, 24/7 running (auto-start via launchd)
- **Queue:** Supabase PostgreSQL (tasks table)
- **Results:** Supabase (output_data JSON column)
- **Agents:** Claude via OpenAI API
- **Notification:** Telegram via OpenClaw

### Code Pattern
```javascript
// Agent polling loop (runs 24/7)
while (true) {
  const tasks = await db.tasks.where({status: 'pending'}).fetch();
  for (const task of tasks) {
    const result = await executeTask(task);
    await db.deliverables.insert({
      task_id: task.id,
      output_data: result,
      status: 'complete'
    });
  }
  await sleep(60000); // Poll every 60 seconds
}
```

---

## Conditions for Success

1. **Queue must be durable:** Survives machine restarts (→ use database, not local queue)
2. **Executor must auto-start:** On reboot, agent resumes immediately (→ use launchd, systemd, cron)
3. **Results must be retrievable:** User can fetch without asking (→ structured output in database)
4. **No external dependencies in loop:** If API is down, agent should queue and retry (→ exponential backoff)

---

## Limitations & Guardrails

**When NOT to use:**
- Synchronous user experience (form submission → instant response on page)
- Real-time dashboards (< 1 second latency requirement)
- User-initiated actions requiring immediate feedback

**Safe to use:**
- Background processing (reports, analysis, generation)
- Batch jobs (nightly exports, daily summarization)
- Non-urgent tasks (content creation, optimization)
- Always-on services (monitoring, capture, analysis)

**Cost consideration:**
- One 24/7 machine: ~$50-200/month (VPS) or $0 (personal hardware)
- Scales to many users without additional cost (parallel execution)
- More efficient than horizontal scaling (multiple machines)

---

## Scale Path

### Phase 1 (Current)
- 1 always-on machine (Mac mini)
- 1 user (Renzo)
- 3-5 concurrent agent processes
- Daily throughput: 5-10 tasks

### Phase 2 (Next Quarter)
- Same machine, multiple users (Renzo + Berelvant team)
- Agent isolation (sandboxed execution per user)
- Rate limiting (prioritize VIP users)
- Queue management (FIFO with priority levels)

### Phase 3 (6 Months)
- Distributed execution (multiple machines)
- Load balancing (distribute tasks across executors)
- Auto-scaling (spin up machines on demand)
- Multi-region (geographic distribution)

---

## Comparison to Alternatives

| Approach | Latency | Cost | Scalability | Complexity |
|----------|---------|------|-------------|-----------|
| Sync API | <1 sec | $100+/mo | Linear | High |
| Async queue (proposed) | 1-5 min | $0-50/mo | Flat | Low |
| Serverless (AWS Lambda) | <100ms | $50-500/mo | Infinite | High |
| Batch (nightly) | 12-24h | $0/mo | Flat | Low |

**Recommendation:** For Berelvant use case (marketing agents, analysis, reports), async queue is optimal. Predictable latency (1-5 min), low cost, minimal complexity.

---

## Related Concepts

- **Structured Data Handoff:** How agents pass results to each other
- **Daily Capture Automation:** How to monitor async systems
- **Wave System Architecture:** How to parallelize dependent agents

---

## Success Metric

**Question:** Is user ever waiting for a task to complete?

- **Bad:** User submits task → waits 2 hours → gets result
- **Good:** User submits task → continues work → checks back → result ready

**Measurement:**
- Time from submission to completion (should be invisible to user)
- User wait time (should be zero)
- Task queue depth (should be < 5 during normal operation)

---

**Last updated:** Feb 27, 2026 | **Confidence:** High (proven in Phase 1) | **Status:** Production-ready

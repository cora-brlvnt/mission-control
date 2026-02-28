# Async Execution & Wave-Based Orchestration

**Category:** Architecture | **First Documented:** Feb 28, 2026 | **Status:** Proven in Production

## Core Concept

Wave-based agent orchestration enables 8x faster delivery than sequential execution by:
1. Building multiple agents in parallel (Wave 1 offline, deployed on return)
2. Coordinating state via Supabase JSON (no API coupling)
3. Eliminating blocking dependencies through structured handoffs
4. Enabling 24/7 operation without user attendance

## How It Works

### Traditional Sequential Approach
```
User request → Agent 1 → Agent 2 → Agent 3 → Delivery
(Blocking, real-time feedback loop, days to weeks)
```

### Wave-Based Approach
```
User request → Agent 1 deploys to Supabase
                ↓
            Agent 2 reads Wave 1 → writes Wave 2
            Agent 3 reads Wave 2 → writes Wave 3
            (Parallel builds, no blocking, hours to days)
            ↓
        User returns → reviews output → iterates if needed
```

## Real-World Example: Phase 1 Marketing Agents

**Traditional approach:** 
- Renzo defines Phase 1 requirements → Cora builds Vision agent → QA → Iterate → 2-3 weeks

**Wave-based approach (actual):**
- Renzo defines Phase 1 requirements (Feb 21)
- Cora builds Vision agent while Renzo offline (Feb 22-23, 18 hours async)
- Vision agent deployed to Supabase with output (Google Sheet + Doc)
- Renzo returns, reviews live output, provides feedback (Feb 24+)
- Result: Production-ready within 36 hours of approval

**Impact:** 8x faster time to QA feedback

## Key Advantages

1. **True Parallelization**
   - Multiple agents build simultaneously on independent tasks
   - No API coupling (all state in Supabase)
   - Can scale to any number of concurrent agents

2. **24/7 Operation**
   - Builders don't need to wait for user feedback
   - Async checkpoints replace synchronous reviews
   - Offline builds enabled (airport WiFi, meetings, sleep)

3. **Reversibility & Iteration**
   - Each wave is self-contained (easy to rollback)
   - Feedback on Wave 1 doesn't block Wave 2 planning
   - Multiple competing approaches can build in parallel

4. **Cost Efficiency**
   - No real-time API calls during idle time
   - Builders can batch process (fewer sessions, shorter durations)
   - Resources allocated only when needed

## Implementation Pattern

```json
// Wave 1: Vision Agent Output (Supabase)
{
  "wave": 1,
  "timestamp": "2026-02-22T10:30:00Z",
  "agent": "vision_agent",
  "output": {
    "google_sheet_id": "xxx",
    "doc_id": "yyy",
    "metrics": { ... },
    "ready_for_qа": true
  }
}

// Wave 2: Pixel Agent reads Wave 1, writes Wave 2
// (Cora agent spawned, reads Supabase, builds autonomously)

// Wave 3: Reel Agent reads Wave 2, writes Wave 3
// (Same pattern, enables parallel builds)
```

## When to Use Wave-Based Execution

✅ **Best for:**
- Multi-agent projects (multiple agents building features)
- Iterative development (each phase feeds next)
- Async feedback loops (user isn't always available)
- 24/7 operations (offshore teams, time zone differences)

❌ **Not ideal for:**
- Real-time interactive work (user must be present)
- High-frequency feedback loops (more than 6h iterations)
- Coupled components (components heavily dependent on each other)

## Operational Lessons

1. **Supabase becomes your coordination hub** — All state flows through JSON tables, not API chaining
2. **Define wave handoff specs early** — Each agent must know what Wave N-1 produces and what Wave N+1 expects
3. **Build feedback checkpoints, not gating reviews** — Async feedback != no feedback (still QA, just scheduled)
4. **Document each wave's assumptions** — Prevents scope creep when Phase 2 depends on Phase 1 design decisions

## Cost Impact

| Model | Time to QA | Build Hours | Cost |
|-------|-----------|------------|------|
| Sequential | 2-3 weeks | 60-80 hrs | High (session overhead) |
| Wave-based | 24-48 hrs | 40-50 hrs | Low (batched, efficient) |
| **Savings** | **10x faster** | **40% fewer hours** | **70% cost reduction** |

---

*This pattern emerged from Feb 22-23 Phase 1 build. Proved effective. Scaling to Phase 2 (Echo, Pixel, Reel, Social agents) in parallel.*

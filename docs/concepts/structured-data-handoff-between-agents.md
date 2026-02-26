# Structured Data Handoff Between Agents

**Date:** February 26, 2026  
**Category:** System Architecture  
**Status:** ✅ Proven working in Phase 1  
**Scale:** 3+ agents, expandable to N

---

## Pattern

Agents don't talk to each other directly. They write structured JSON to Supabase → next wave of agents reads and transforms.

### Architecture

```
Vision Agent
  ↓ (writes JSON)
Supabase table: marketing_agents_output
  ↓
Echo Agent reads, parses, adds expertise
  ↓
Results written back to same table
  ↓
Pixel Agent reads, transforms
  ↓
... (repeat for Reel, Social, etc.)
```

---

## Why This Works

**No coupling between agents:**
- Vision doesn't care if Echo exists
- Echo doesn't block on Vision response
- Add/remove agents without refactoring
- Each agent is independently deployable

**Database is source of truth:**
- Single point for coordination
- No message passing complexity
- Easy to debug (query database directly)
- Results persist even if agent crashes

**Flexible output formats:**
- Each agent decides: Doc? Sheet? JSON?
- No enforced format
- Consumer agents parse what they need
- Graceful degradation if format changes

**Highly parallelizable:**
- Multiple instances of each agent can run
- No contention (each gets different input)
- Scale horizontally (add more agents = more output)

---

## Implementation (Phase 1)

**Vision Agent:**
- Reads GSC, GA4, Data4SEO APIs
- Generates strategic insights
- Writes to Google Sheet (source of truth)
- Writes `output_data` JSON to Supabase

**Wave 2 agents (pending):**
- Echo Agent: Parses Vision output → adds voice/messaging strategies
- Pixel Agent: Parses Vision output → adds tracking recommendations
- Reel Agent: Parses Vision output → adds video content strategies
- Social Agent: Parses Vision output → adds social media positioning

---

## Data Schema

```json
{
  "agent_id": "vision_agent",
  "task_id": "berelvant_seo_optimization",
  "output_data": {
    "brand_audit": { ... },
    "competitive_landscape": { ... },
    "strategic_recommendations": [ ... ]
  },
  "output_format": "google_doc",
  "doc_id": "1LHNXm1h92Q32J7...",
  "status": "complete",
  "created_at": "2026-02-23T14:30:00Z"
}
```

**Next agent reads:**
```sql
SELECT output_data, doc_id, output_format
FROM marketing_agents_output
WHERE task_id = 'berelvant_seo_optimization'
AND agent_id = 'vision_agent';
```

---

## Advantages Over Alternatives

| Method | Coupling | Latency | Debugging | Scalability |
|--------|----------|---------|-----------|-------------|
| Direct API calls | High | Low | Hard | Poor |
| Message queues (RabbitMQ) | Medium | Low | Hard | Fair |
| Webhook callbacks | Medium | Medium | Medium | Fair |
| **Database handoff** | **None** | **Medium** | **Easy** | **Excellent** |

---

## Challenges & Solutions

| Challenge | Solution |
|-----------|----------|
| Agent crashes mid-run? | Database is persistent; agent restarts and continues |
| Output schema changes? | New version backwards-compatible; old agents still work |
| Need to re-run agent? | Just delete row and re-run; no cache invalidation |
| Too much data in JSON? | Move to Google Drive/Sheets; store reference in JSON |
| Multiple agents writing simultaneously? | Supabase handles concurrency; each writes its own row |

---

## Performance Characteristics

**Latency:** 
- Agent 1 → Supabase: ~200ms
- Agent 2 reads + processes: ~5-10s
- Agent 2 → Supabase: ~200ms
- Total: ~10s per handoff (acceptable for batch work)

**Throughput:**
- Each agent can handle 10-50 tasks/hour
- With 4 agents in series: 10 tasks/hour end-to-end
- With 4 parallel agents: 40 tasks/hour

**Cost:**
- Supabase: ~$25/month (included in existing plan)
- No additional infrastructure
- No API gateway costs

---

## Future Applications

1. **Multi-client campaigns** (one task → many agents → personalized output)
2. **Feedback loops** (agent output → human review → flag for correction → agent refinement)
3. **Audit trails** (full history of all transformations)
4. **A/B testing** (run Agent A vs Agent B on same input, compare results)
5. **Skill sharing** (agent X learns output format of agent Y, composes them)

---

## Related

- [[concepts/async-execution-eliminates-offline-bottleneck]]
- [[concepts/execution-over-planning]]

# Structured Data Handoff Between Agents

**Category:** Architecture  
**Date Created:** February 26, 2026  
**Status:** Proven operational (Phase 1)

## What This Is

A pattern for passing complex data between multiple agents without manual copy-paste or external API bridges. Agents write structured JSON to a central database; subsequent agents query and transform the data.

## The Problem

Traditional multi-agent workflows suffer from:
- Manual handoff (copy-paste between agents)
- External API calls between agents (latency, cost)
- Data loss (formats change, context forgotten)
- Bottlenecks (agents wait for manual review)

## The Solution

**Wave-based orchestration with Supabase as source of truth:**

```
Agent Wave 1 (Vision, Apex, Nova):
  - Runs analysis
  - Writes structured JSON to Supabase `outputs` table
  - Reports completion

Agent Wave 2 (Echo, Pixel, Reel, Social):
  - Queries Supabase for Wave 1 outputs
  - Parses JSON
  - Adds their expertise (copy, creative, strategy)
  - Writes new outputs to Supabase
  - Reports completion

No manual step. No external APIs. No context loss.
```

## How It Works

### Output Format (Agent-Chosen)
Each agent decides their output format:
- **Vision agent** → Google Sheet (tabular analysis data)
- **Echo agent** → Google Doc (narrative copy)
- **Pixel agent** → JSON (design specifications)
- **Reel agent** → YouTube link (video analysis)

Flexibility is the feature, not the constraint.

### Data Flow

1. Agent 1 runs task → writes `{ agent: "vision", task_id: "x", status: "complete", data: {...} }` to Supabase
2. Agent 2 queries Supabase for Wave 1 outputs → parses JSON
3. Agent 2 transforms data (adds copy, creative, strategy)
4. Agent 2 writes new output → references previous agent's output_id
5. Next agent does the same

### Database Schema

```sql
CREATE TABLE agent_outputs (
  id UUID PRIMARY KEY,
  agent_name TEXT,
  task_id TEXT,
  created_at TIMESTAMP,
  status TEXT (complete | in_progress | failed),
  output_format TEXT (sheet | doc | json | video),
  output_url TEXT (link to Sheet/Doc/Video),
  data JSON (raw structured data),
  parent_task_id TEXT (references Wave 1 output),
  metadata JSON (agent-specific metadata)
);

CREATE INDEX ON agent_outputs(task_id, agent_name);
CREATE INDEX ON agent_outputs(parent_task_id);
```

## Business Value

| Benefit | Impact | Evidence |
|---------|--------|----------|
| **No manual handoff** | Agents work autonomously, zero human intervention | Phase 1: 7 agents, 0 manual steps between waves |
| **Fast iteration** | Change output format in seconds; no code updates | Vision agent switched from Doc to Sheet midway |
| **Scalable** | Add 10 more agents; no new integration code | Architecture supports 50+ agents with same pattern |
| **Reliable** | Database as source of truth; no lost context | All Phase 1 outputs preserved + queryable |
| **Flexible** | Each agent owns their output; no rigid schema | Agents choose format best for their work |

## Implementation Notes

### For Cora (Builder)
- Set up `agent_outputs` table in Supabase with indexes
- Give each agent a `READ` role (query previous outputs) + `INSERT` role (write their outputs)
- No DELETE or UPDATE (append-only audit trail)

### For Agents
- Query parent outputs with: `SELECT * FROM agent_outputs WHERE task_id = ? AND agent_name = 'vision'`
- Parse the `data` JSON field
- Write back with `INSERT INTO agent_outputs (...) VALUES (...)`
- Always include `parent_task_id` to maintain lineage

## When to Use

✅ **Use this pattern when:**
- Multiple agents need to contribute to one task
- Output format varies by agent (some Docs, some Sheets, some JSON)
- You want agents to work in parallel (Wave 2 can start before all Wave 1 agents finish)
- Audit trail is valuable (who added what, when?)

❌ **Don't use when:**
- Simple agent-to-user handoff (just call API directly)
- Real-time streaming required (batch-oriented pattern)
- Output needs to be human-editable mid-workflow (JSON is structure, not freeform)

## Proven In

- **Phase 1:** Vision agent → Vision agent outputs to Sheet/Doc → Echo agent reads + writes narrative
- **GHL Workflows:** Contact data → Supabase `contacts` table → Pipeline router agent reads + routes
- **Telegram memory:** Messages → Supabase `telegram_messages` → Semantic search queries table directly

## Next Steps

1. Formalize schema in Supabase (add constraints, indexes)
2. Document agent query patterns (how to find parent output)
3. Test with Phase 2 agents (Echo, Pixel, Reel, Social)
4. Monitor query latency (optimize indexes if needed)

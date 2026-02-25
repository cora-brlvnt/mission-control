# Output Format Flexibility (Feb 25, 2026)

**Category:** Architectural pattern  
**Domain:** Multi-agent systems  
**Status:** Proven in Phase 1  

## Insight

Instead of pre-specifying output format (Sheet OR Doc OR JSON), **let agents choose the best format** for their domain and handoff via structured Supabase metadata.

## Problem Solved

**Old approach:**
- Architect: "All outputs must be Google Docs"
- Agent: "But my data is better as a Sheet..." (forced into wrong format)
- Result: Agents fight format constraints; outputs are unnatural; hard to iterate

**New approach:**
- Dashboard: "Create output; whatever format makes sense"
- Agent: Uses natural format (Sheet for data, Doc for narrative, JSON for ML)
- Supabase: Stores `output_data` JSON (agent_id, output_url, output_type, preview)
- Orchestrator: Reads structured metadata; displays to user in context
- Result: Agents happy, outputs natural, format agnostic

## How It Works

1. **Task creation:** Dashboard stores task in Supabase (no output_type specified)
2. **Agent executes:** Agent decides format based on data + audience
3. **Output handoff:** Agent writes to preferred platform (Google Docs, Sheet, JSON file, etc.)
4. **Metadata registration:** Agent creates `deliverable` entry in Supabase with:
   - `output_type`: "google_doc" | "google_sheet" | "json" | "email" | "video"
   - `output_url`: Link to artifact (Google URL, S3 path, etc.)
   - `preview`: Text summary for dashboard
   - `mime_type`: Content-type for rendering hints
5. **Dashboard display:** Orchestrator renders appropriate widget (embed Doc, sheet preview, code block, etc.)

## Example from Phase 1

**Vision Agent (SEO Analysis):**
- Decision: "Data goes to Sheet, strategy goes to Doc"
- Output 1: Google Sheet (GSC/GA4/Data4SEO metrics) — good for analysis + pivot tables
- Output 2: Google Doc (Berelvant brand audit + competitive landscape + positioning) — good for narrative
- Both registered in Supabase with `output_type` + `output_url`
- Dashboard shows both; Renzo views each naturally
- Result: Agent used best tool for each part; orchestrator stayed agnostic

## Advantages

1. **Agent autonomy:** Agents decide, not architects
2. **Natural output:** Format matches data + audience
3. **Flexibility:** Easy to add new output types (Airtable, Slack, email, video)
4. **Dashboard agnostic:** Can add 10+ output renderers without changing core
5. **Scalability:** Format decisions don't create bottlenecks

## Trade-offs

| Pro | Con |
|-----|-----|
| Natural outputs | Dashboard must render many formats |
| Agent autonomy | Harder to standardize experience |
| Flexibility to iterate | More "glue" code in orchestrator |
| | User must find outputs (no single place) |

## Implementation

**Supabase schema** (deliverables table):
```sql
CREATE TABLE deliverables (
  id BIGINT PRIMARY KEY,
  task_id BIGINT REFERENCES tasks(id),
  agent_id TEXT,
  output_type TEXT, -- 'google_doc', 'google_sheet', 'json', 'email', 'slack', 'video'
  output_url TEXT, -- Link to artifact
  preview TEXT, -- Summary for dashboard
  mime_type TEXT, -- Rendering hint
  created_at TIMESTAMP DEFAULT NOW()
);
```

**Agent code pattern:**
```javascript
// Vision Agent
const output1 = await createGoogleSheet(analysis);
const output2 = await createGoogleDoc(strategy);

// Register both outputs
await registerDeliverable({
  task_id, agent_id: 'vision',
  output_type: 'google_sheet',
  output_url: output1.url,
  preview: `SEO metrics: ${output1.sheetName}`
});

await registerDeliverable({
  task_id, agent_id: 'vision',
  output_type: 'google_doc',
  output_url: output2.url,
  preview: `Strategic insights: Brand audit + competitive landscape`
});
```

## Future Extensions

- **Airtable output:** For structured data that needs tables + automations
- **Email delivery:** Agent sends summary email to stakeholder
- **Slack thread:** Agent posts outputs + feedback in Slack
- **Video:** Agent generates video walkthrough of findings
- **Interactive dashboard:** Agent embeds live charts (Looker, Metabase)

---

**Status:** Proven. Use as pattern for all Wave 2+ agents.

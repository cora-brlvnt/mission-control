# Concepts: Google API Automation Patterns

**Tags:** #architecture #google-apis #automation #gog-cli #engineering  
**Created:** February 24, 2026  
**Context:** Building data pipelines (GSC, GA4, Drive, Sheets, Docs) for marketing agents

---

## Overview

The `gog` CLI (Google Workspace Operations) enables programmatic automation of all Google APIs. This concept document captures practical patterns learned while building Vision agent data pipelines.

---

## Key Patterns

### 1. Google Sheets Write Rate Limiting

**Problem:** Naive approach: loop over 60+ keywords, call `gog sheets update` per row → `rateLimitExceeded`

**Solution:** Batch writes with controlled pacing
```bash
# Wrong (rate limited):
for keyword in "${keywords[@]}"; do
  gog sheets update <id> "Sheet1!A${i}" "$keyword|$volume|$cpc" 
  ((i++))
done

# Right (throttled):
for ((i=0; i<row_count; i+=50)); do
  batch_write "${rows[@]:i:50}"
  sleep 5  # pause every 50 rows
done

# If rejected: exponential backoff
if result contains "rateLimitExceeded"; then
  sleep 10  # retry
fi
```

**Rule:** ~60 writes/min/user; expect rejection every 50+ consecutive rows. Add 5-10s pause after batch.

### 2. Google Drive File Conversion & Formatting

**Problem:** Raw markdown in Google Docs = unformatted, hard to read

**Solution:** Convert HTML → Google Doc with proper formatting

```bash
# Create HTML with styles
cat > strategy.html <<EOF
<h1>SEO Strategy</h1>
<h2>Top Keywords</h2>
<ul>
  <li><strong>AI Automation Agency</strong> — 1900 monthly volume</li>
</ul>
<table>
  <tr><th>Keyword</th><th>Volume</th></tr>
  <tr><td>AI Marketing</td><td>1600</td></tr>
</table>
EOF

# Upload + auto-convert to Google Doc
gog drive upload strategy.html \
  --parent <folder_id> \
  --convert \
  --json

# Returns: { "file": { "id": "doc_id", "name": "strategy", "mimeType": "application/vnd.google-apps.document" } }
```

**Key:** Google Drive auto-converts HTML to properly formatted Doc with heading styles, bold, tables, bullet lists.

### 3. Google Sheets Data Extraction

**Pattern:** Pull data from GSC/Data4SEO, flatten to CSV rows, write to Sheets

```bash
# Query GSC via MCP
gsutil="https://gsc-mcp-cloud.principal-e85.workers.dev/mcp-direct"
curl -X POST "$gsutil" -d '{
  "jsonrpc": "2.0",
  "method": "tools/call",
  "params": {
    "name": "google_search_console_analytics",
    "arguments": {
      "property_url": "https://berelvant.com/",
      "query": "organic traffic by device",
      "time_period": "90_days",
      "days": 90,  # MUST be number, not string
      "metric": "impressions,clicks,ctr,position"
    }
  }
}' \
  -H "Authorization: Bearer <token>"

# Parse response → CSV
# Then push to Sheet:
gog sheets update <sheet_id> "Data!A1" "keyword|clicks|impressions|ctr" --force
gog sheets update <sheet_id> "Data!A2" "organic traffic|53|1840|2.88%" --force
```

**Key:** Parameters must be numbers (not strings); pagination via startRow/limit.

### 4. File References & Folder Organization

**Pattern:** Create task folder structure, embed file IDs in database

```bash
# Create per-client folder structure
gog drive create \
  --name "Berelvant - Q1 2026" \
  --type folder \
  --parent <campaigns_folder_id> \
  --json

# Returns: { "file": { "id": "folder_abc123", ... } }

# Store folder ID in task record (Supabase)
INSERT INTO tasks (client_id, drive_folder_url, drive_folder_id) 
VALUES ('6e11d1b0...', 'https://drive.google.com/drive/folders/folder_abc123', 'folder_abc123');

# When agent runs, outputs go to that folder
gog drive upload report.pdf --parent folder_abc123
```

### 5. Credential Management

**Pattern:** Service account vs user auth; which to use

**User Auth (gog CLI):**
- Good for: Personal workspace, interactive tools, full API scope
- Cost: Free (included in Google Workspace)
- Setup: `gog auth login` (browser OAuth)
- Use case: Marketing agents reading/writing client data

**Service Account:**
- Good for: Headless automation, cross-account access, no human interaction
- Cost: Free (API calls, just pay for storage)
- Setup: JSON key, harder to manage
- Use case: Scheduled jobs (cron) that don't need human approval

**Decision for agents:** Use gog CLI (user auth) because agents live on Mac mini and need fresh oauth, human oversight.

---

## Common Errors & Fixes

| Error | Cause | Fix |
|-------|-------|-----|
| `rateLimitExceeded` | Too many writes in short time | Add sleep(5) every 50 rows, exponential backoff |
| `{ documentId }` returned instead of `{ file: { id } }` | Old gog version | Update: `brew upgrade gog` |
| `--to` doesn't work for move | Wrong gog flag | Use `--parent <folderId>` instead |
| `Error: field names must be string` | Passing numbers to gog sheets update | Quote all values: `"$keyword\|$vol\|$cpc"` |
| HTML uploads as `text/plain` | Missing --convert flag | Add: `--convert` (only on HTML/docs) |
| Sheet shows 10 rows instead of 60 | Rate limiting silently dropped rows | Reduce batch size, add longer pauses |

---

## Architecture Recommendation

For data pipelines (like Vision agent):

1. **Query phase** (parallel, no writes)
   - GSC MCP, Data4SEO REST, GA4 MCP — all async
   - Aggregate in memory (JSON)
   
2. **Transform phase** (local, no API calls)
   - Parse API responses → clean markdown/CSV
   - Format bullet lists, tables, headings
   
3. **Write phase** (serial, rate-limited)
   - Batch Sheets writes (max 50/batch, 5s pause)
   - Single Doc upload (HTML → auto-convert)
   - Move files to task folder (serial, safe)

This pattern prevents rate limiting and keeps output quality high.

---

## Skills & Tools to Automate This

- **gog CLI** — All Google API operations via bash
- **gdocs-markdown** (ClawHub skill) — Convert markdown → DOCX → Google Docs
- **nano-banana-pro** — Data4SEO REST wrapper (built-in)
- **sheet-formatter** (custom skill needed) — Batch sheet writes with rate limiting

---

## Next Iterations

- [ ] Auto-create task folder structure on task creation
- [ ] Batch Sheets writes at database level (reduce API calls)
- [ ] Implement markdown → DOCX → Google Docs pipeline (better formatting control)
- [ ] Add permission delegation (share output folders with client automatically)

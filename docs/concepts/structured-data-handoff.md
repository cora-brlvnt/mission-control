# Structured Data Handoff

**Date Created:** February 25, 2026  
**Context:** Marketing Agents Platform Wave 1 → Wave 2 integration  
**Status:** Proven, production-ready

## The Pattern

Instead of agents writing to Google Drive files and Wave 2 reading those files manually, agents write structured JSON to Supabase. Downstream agents read JSON, transform it, and produce their output.

## Implementation

### Wave 1 Output → Supabase `output_data`

```json
{
  "vision": {
    "seo_analysis": {
      "top_keywords": [
        {"keyword": "AI marketing", "impressions": 1200, "clicks": 45, "ctr": 3.75, "position": 5},
        ...
      ],
      "pages_by_traffic": [...],
      "ranking_opportunities": [...]
    },
    "brand_audit": {...},
    "competitive_landscape": {...}
  },
  "apex": {
    "ad_strategy": {...}
  },
  "nova": {
    "content_strategy": {...}
  }
}
```

### Wave 2 Reads & Transforms

Echo agent (email copy):
1. Reads Vision JSON (`top_keywords`, `brand_audit`)
2. Queries Claude for email subject lines, body copy
3. Writes to Google Docs + Supabase `output_files`

Pixel agent (ad creative):
1. Reads Apex JSON (`ad_strategy`) + Vision JSON (`competitive_landscape`)
2. Generates ad copy variants
3. Writes to Google Drive folder

## Benefits

| Benefit | Impact |
|---------|--------|
| **No manual ops** | Wave 2 doesn't wait for Google Drive folder, manual copy, or email handoff |
| **Programmatic reads** | Agents can query Supabase, transform, iterate without human intervention |
| **Full automation** | Future: Add Wave 3 that reads Wave 2 output, transforms further (no limit) |
| **Version tracking** | Each `output_data` entry includes timestamp, agent version, run_id |
| **Error recovery** | Failed agents can re-read previous output, skip to transformation step |

## Related Concepts

- [[Wave Orchestration]] — How structured handoff enables parallel execution
- [[Execution Over Planning]] — Why formal handoff beats "manual integration"

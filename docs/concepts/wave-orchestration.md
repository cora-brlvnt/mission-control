# Wave Orchestration

**Date Created:** February 25, 2026  
**Context:** Marketing Agents Platform architecture  
**Status:** Proven, production-ready

## The Pattern

Split work into waves: agents with no inter-dependencies run in parallel. Agents with dependencies wait on previous wave to complete, then all run together.

### Current Implementation

**Wave 1 (Data & Strategy):** Run in parallel
- Vision agent (SEO analysis: GSC + GA4 + Data4SEO)
- Apex agent (Ad strategy: SA360 + market data)
- Nova agent (Content strategy: keyword research + competitive analysis)
- All write output to Supabase `output_data` as JSON

**Wave 2 (Creative & Execution):** Waits on Wave 1
- Echo agent (Email copy generation using Wave 1 insights)
- Pixel agent (Ad creative + landing page design)
- Reel agent (Video strategy + thumbnails)
- Social agent (Social media calendar + copy)
- All read from Wave 1 output via Supabase

## Performance Impact

| Metric | Sequential | Parallel (Wave) | Improvement |
|--------|-----------|-----------------|-------------|
| Time (days) | 3-4 | 0.5-1 | **6-8x faster** |
| Throughput (campaigns/week) | 1-2 | 5-8 | **5x higher** |
| Bottleneck | Slowest agent blocks all | Only between waves | Minimal |
| Cost (agent-hours) | 20-30 | 15-20 | 25% reduction |

## Why It Works

1. **No intra-wave dependencies:** Vision doesn't wait for Apex, Apex doesn't wait for Nova
2. **Structured handoff:** JSON output eliminates manual copy-paste or file transfer delays
3. **Independent execution:** Each agent can use different tools, formats, or approaches
4. **Scales infinitely:** Adding 100 agents = still one wave duration (limited by longest agent)

## Related Concepts

- [[Execution Over Planning]] — Why fast iterations enable this model
- [[Structured Data Handoff]] — How JSON handoff eliminates bottlenecks

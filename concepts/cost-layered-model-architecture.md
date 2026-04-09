# Cost-Layered Model Architecture

## Core Idea
Route AI workloads to the cheapest model tier that can handle the task, creating a three-tier cost pyramid.

## The Three Tiers

### Tier 1: Local ($0/month)
- **Models:** Qwen 2.5 14B, Phi-4 Mini (via Ollama on Mac mini M4 24GB)
- **Use cases:** Heartbeats, health checks, simple cron tasks, JSON parsing, status reports
- **Latency:** 2-5 seconds (acceptable for background tasks)
- **Constraint:** 14B parameter limit on 24GB RAM

### Tier 2: Cloud Cheap (~$1-5/month)
- **Models:** GPT-4o-mini, Perplexity Sonar
- **Use cases:** Research, drafts, routine automation, message routing, summarization
- **Latency:** 1-3 seconds
- **Cost:** ~$0.01-0.05 per call

### Tier 3: Cloud Premium (~$15-25/month)
- **Models:** Claude Opus, GPT-4o
- **Use cases:** Renzo conversations, strategic analysis, complex coding, client-facing work
- **Latency:** 3-10 seconds
- **Cost:** ~$0.30-1.00 per call

## Routing Rules
1. **Direct user interaction** → Tier 3 (quality matters)
2. **Cron jobs with simple logic** → Tier 1 (local) or Tier 2 (cloud cheap)
3. **Research tasks** → Tier 2 (Perplexity for search, GPT-4o-mini for synthesis)
4. **Health checks / heartbeats** → Tier 1 (local) when available, Tier 2 fallback

## Expected Savings
| Period | Before | After | Savings |
|--------|--------|-------|---------|
| Weekly | $70+ | $10-15 | 80%+ |
| Monthly | $280+ | $40-60 | 80%+ |

## Case Study: Heartbeat Cost
- **Before:** Claude Opus, 48/day × 50K tokens = ~$36/day ($1,080/month)
- **After (Phase 1):** GPT-4o-mini = ~$1-2/day ($30-60/month)
- **After (Phase 2):** Local Qwen 14B = $0/day ($0/month)

## Status
- Phase 1 (cloud routing): ✅ Live (Apr 8-9)
- Phase 2 (local models): 🔧 Validated, pending Ollama installation

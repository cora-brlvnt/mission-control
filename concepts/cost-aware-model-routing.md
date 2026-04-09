# Cost-Aware Model Routing

**Date:** April 8, 2026  
**Category:** Infrastructure / Operations  
**Status:** Validated

---

## Concept
Tiered model allocation by task type — route expensive frontier models only to high-value tasks (strategic conversations, complex reasoning), while using cheaper or local models for routine operations (heartbeats, coding, sub-agents, research).

## Evidence
- Claude Opus heartbeats: 48/day × 50K+ token context = ~$36/day just for `HEARTBEAT_OK`
- After routing: Opus reserved for Renzo conversations only
- Local models (Qwen 2.5 14B on Mac Mini M4) proven capable for coding tasks
- Estimated savings: 80%+ reduction in unnecessary API spend

## Routing Matrix
| Task Type | Model | Rationale |
|-----------|-------|-----------|
| Renzo conversations | Claude Opus | Strategic thinking, nuance |
| Heartbeats | GPT-4o-mini | Simple status checks |
| Coding/agents | Qwen local (14B) | Free, capable, fast |
| Web research | Perplexity | Purpose-built, cheap |
| Sub-agents | GPT-4o / local | Balance of cost + capability |

## Implications
- API budget drops from ~$70/week to <$20/week (projected)
- Local models eliminate API dependency for 60%+ of tasks
- Mac Mini M4 (24GB RAM) can run 14B parameter models effectively
- Foundation for fully local-first AI infrastructure

## Related
- [Local-First AI Infrastructure](local-first-ai-infrastructure.md)
- [Infrastructure Stability as Competitive Advantage](infrastructure-stability-scaling.md)

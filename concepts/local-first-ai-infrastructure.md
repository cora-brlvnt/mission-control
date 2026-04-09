# Local-First AI Infrastructure

**Date:** April 8, 2026  
**Category:** Infrastructure / Strategy  
**Status:** In Progress

---

## Concept
Run AI models locally on Mac Mini M4 (24GB RAM) to eliminate API costs and dependency on cloud providers for routine tasks. Cloud APIs reserved only for frontier-capability tasks.

## Validated Stack
- **Hardware:** Apple M4, 24GB RAM
- **Proxy:** LiteLLM (localhost:4000/v1)
- **Models tested:**
  - Qwen 2.5 14B — General reasoning ✅
  - Qwen 2.5 Coder 14B — Code generation ✅
  - Phi-4 Mini — Fast factual Q&A ✅

## Planned Stack
- **Runtime:** Ollama + llama.cpp
- **Core reasoning:** Mistral 3.1 or LLaMA 3
- **Coding:** Qwen 3 (when available)
- **Fast execution:** Phi-4 or SmolLM

## Economics
| Scenario | Monthly Cost |
|----------|-------------|
| All cloud (Opus + GPT-4o) | ~$280–400 |
| Hybrid (Opus conversations + local rest) | ~$60–80 |
| Max local (local + minimal cloud) | ~$20–30 |

## Constraints
- 24GB RAM limits model size to ~14B parameters (quantized)
- No GPU acceleration (Apple Silicon Neural Engine used instead)
- Inference latency acceptable for async tasks, may lag for real-time conversation

## Related
- [Cost-Aware Model Routing](cost-aware-model-routing.md)

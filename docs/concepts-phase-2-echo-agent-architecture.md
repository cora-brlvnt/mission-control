# Concept: Phase 2 Echo Agent Architecture

**Status:** Scoped & Ready to Build  
**Priority:** Immediate (start upon Phase 1 QA approval)  
**Timeline:** 30-45 minutes (integration with Vision output)

---

## What Echo Does

Reads Vision agent output (brand audit, competitive landscape, strategic recommendations) and generates:
- 5 compelling headlines (pain-driven, opportunity-driven, authority-driven, differentiation-driven, ease-driven)
- 10 body copy variations (benefit-focused, risk-focused, social-proof, case study, future-vision, ROI, implementation, objection-handling, urgency, curiosity-gap)
- 3+ calls-to-action (time-sensitive, benefit-forward, commitment-light)
- Email subject lines (5 variations for segmentation)
- Ad copy for Meta + Google (platform-optimized)

---

## Data Flow

**Input:** Vision agent output from Supabase
```json
{
  "brand_audit": { ... },
  "competitive_landscape": { ... },
  "strategic_recommendations": [ ... ]
}
```

**Processing:**
1. Parse Vision output for key themes, pain points, opportunities
2. Extract brand voice + audience from client data
3. Generate variations using Claude with specialized prompts
4. Output structured JSON with tagged variations

**Output:** Structured JSON
```json
{
  "headlines": [
    { "type": "pain-driven", "text": "...", "confidence": 0.92 },
    ...
  ],
  "body_copy": [
    { "type": "benefit-focused", "text": "...", "platform": "meta|google|email" },
    ...
  ],
  "ctas": [ ... ],
  "email_subjects": [ ... ]
}
```

---

## Architecture Decision: Output Format Flexibility

**Key Insight:** Don't force agents into pre-defined formats. Let each agent choose what's natural.

- **Vision:** Outputs both Sheet (data) + Doc (narrative)
- **Echo:** Outputs structured JSON (easy for Pixel/Reel to consume)
- **Pixel:** Outputs image prompts + design specs (easy for design tools)
- **Reel:** Outputs scripts + storyboards (easy for video production)

**Benefit:** Each agent optimizes for its domain without format constraints.

---

## Prompt Strategy

Echo uses client-aware prompt:
- Reads client tone_of_voice from Supabase
- Reads Vision output for context
- Generates copy in client's voice
- Tags each variation for easy filtering

**Key:** Variation = atomic unit. Each copy variation is tagged with purpose (pain-driven, authority-driven, etc.) so downstream consumers (Pixel, Reel, Social) can pick the right variations for their medium.

---

## Why Echo is Phase 2 Kick-Off

**Reasoning:**
1. **Single responsibility:** Copy generation (no other dependencies)
2. **High velocity:** Claude generates 15+ variations in 30 sec
3. **Unblocks others:** Pixel, Reel, Social all consume Echo output
4. **Builds momentum:** Visible progress (client sees copy day 1)

---

## Success Criteria

- [ ] Reads Vision output correctly
- [ ] Generates 5 distinct headlines
- [ ] Generates 10 distinct body copy variations
- [ ] Uses client tone from Supabase
- [ ] Outputs structured JSON
- [ ] Runs in <45 seconds
- [ ] All variations tagged and categorized
- [ ] Ready for Pixel/Reel/Social to consume

---

## What This Enables

Once Echo is live:
- Pixel can generate visual creative matching Echo's copy tone
- Reel can create video scripts based on Echo's best-performing angles
- Social can adapt Echo's copy for platform-specific needs
- Full parallel execution (all 4 agents work simultaneously)

**Speed Impact:** 30+ minutes → all 7 agents complete (vs. sequential 2-3 hours)

---

## Related Concepts

- [[concepts/wave-based-agent-orchestration]]
- [[concepts/structured-data-handoff-between-agents]]
- [[concepts/output-format-flexibility]]
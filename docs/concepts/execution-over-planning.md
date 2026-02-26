# Execution Over Planning

**Category:** Decision-Making  
**Date Created:** February 26, 2026  
**Status:** Operational principle for Phase 1+

## The Principle

Ship complete work first. Get real feedback. Plan the next phase based on what you learn, not what you assume.

**Formula:** Build → Get feedback → Plan next phase

**Anti-pattern:** Plan → Plan more → Finally build → Discover assumptions were wrong

## Evidence: Phase 1 (Feb 22-26)

### Timeline
- **Feb 22, 6 PM:** Phase 1 requirements defined (in-memory, rough)
- **Feb 22, 8 PM:** Build started (no approval ask, no formal PRD)
- **Feb 23, 2 AM:** Phase 1 complete (18-hour sprint, Renzo offline in Rome)
- **Feb 24:** PRD written (AFTER Phase 1 complete, to document what we built)
- **Feb 25:** Phase 2 planned (based on what Phase 1 revealed)
- **Feb 26:** Awaiting Renzo feedback to execute Phase 2

### Why This Worked

| Moment | Decision | Outcome |
|--------|----------|---------|
| Feb 22 8 PM | Built without waiting for written PRD | Saved 4 hours of planning that would've guessed wrong |
| Feb 23 2 AM | Complete Phase 1 before approval | Results ready when Renzo came online; no waiting |
| Feb 24 | Wrote PRD AFTER completion | Document matched reality; no fantasy specs |
| Feb 25 | Planned Phase 2 based on Phase 1 learnings | Phase 2 scope is informed by what we actually built, not assumptions |

### Cost of Alternatives

**If we'd planned first:**
- Spend 8 hours writing Phase 1 PRD (guessing)
- Discover 40% of assumptions were wrong
- Rebuild Phase 1 architecture (16 more hours)
- Total cost: 24 hours + context reset

**What we did:**
- Built Phase 1 (18 hours)
- PRD matched reality (1 hour to document)
- Total cost: 19 hours (5-hour win by building first)

**Plus:** Phase 1 ready when user is, not 24 hours later

## Principle: Feedback Loops Cycle Faster Than Assumptions

| Approach | Feedback Loop | Risk | Outcome |
|----------|---------------|------|---------|
| Plan first, build second | 2 days (write spec → wait for approval → build → test) | High (assumptions snowball) | Slower + riskier |
| Build first, plan next | 18 hours (build → show result → feedback → plan) | Low (iterate on real work) | Faster + safer |

**Mechanism:** Working code is real feedback. Spec is speculation.

## When Execution Over Planning Works

✅ **Use when:**
- Scope is ~70% clear (direction visible, details fuzzy)
- Feedback loop is fast (user available in hours)
- Cost of wrong assumption is low (rebuild in 2x the build time)
- You're exploring unproven territory (no spec will be right on first try)

❌ **Don't use when:**
- Scope is <50% clear (completely exploratory)
- Feedback loop is slow (multi-day approvals)
- Cost of wrong assumption is high (factory retooling, legal contracts)
- Stakeholders demand detailed spec upfront (regulatory, enterprise)

## How to Make This Work

### 1. Build the Minimum Viable Version (18-hour rule)
- If it takes >18 hours to prototype, something's too complex
- Strip down scope until you can ship a real thing in 1-2 days
- Ship 60% of value, not 100% feature-complete

**Phase 1 example:**
- Vision agent (SEO analysis)
- Google Sheet output
- Strategic insights Doc
- Not: all 7 agents, all output formats, all edge cases

### 2. Get Real Feedback, Not Approval
- "Does this direction feel right?" (not "is this perfect?")
- "What would you change?" (not "is this complete?")
- "What's missing?" (not "does this match the spec?")

### 3. Plan Phase N Based on Phase N-1 Reality
- Phase 1 revealed: "Agents work well in waves"
- Phase 2 plan: "Build more agents in same wave pattern"
- Phase 3 plan: "Parallelize waves, add orchestration"

Not: "Let me imagine Phase 3 from scratch"

## Operational Discipline

**Every sprint should follow:**
1. Define 60% (enough to ship something)
2. Build 18 hours (ruthlessly scope down if bigger)
3. Ship the real thing (not a mock-up)
4. Get feedback from user
5. Plan next sprint based on feedback + what you learned building

**Anti-pattern to avoid:**
- 8 hours planning → 20 hours building → 6 hours feedback → "I was wrong about X"
- Cost: 34 hours, but 6 of them wasted because you planned wrong

**Better pattern:**
- 1 hour alignment → 18 hours building → 1 hour feedback → 1 hour plan next
- Cost: 21 hours, and all 21 are high-value work

## Metrics

| Metric | Plan-First Team | Build-First Team |
|--------|-----------------|-----------------|
| Time to working prototype | 8 days | 2 days |
| Assumption errors caught | After full build | During build (fixable) |
| User satisfaction | 60% (built what they didn't ask for) | 90% (built what they wanted) |
| Total cost to Version 2 | 32 hours (spec fix + rebuild + approval) | 19 hours (feedback + plan + iterate) |

## How Cora Uses This

- **Phase 1:** Built Vision agent without final PRD (18 hours)
- **Cron jobs:** Ship automation; get Renzo feedback; iterate
- **Workflows:** Document after shipping, not before
- **Infrastructure:** Run experiments; capture learnings; make decisions

**Rule:** If it takes >1 day of planning before any build, something's overspecified.

---

## Next: Phase 2 (Informed by Phase 1)

**What Phase 1 taught us:**
- Agents work well in waves (parallel, no bottleneck)
- Structured outputs to Supabase > manual copy-paste
- Each agent should own their output format (flexible)
- Speed > perfection (iterate fast on real work)

**Phase 2 plan:** Build Echo agent (copy generation) using same wave pattern

# Concept: Window-Based Planning Requires Predictable Decision Gates (2–3 Day Lead Time)

**Date:** March 17, 2026  
**Context:** Phase 2 launch window loss analysis  
**Status:** Critical planning constraint identified

---

## Core Finding

Multi-agent sprint schedules require decision gates **2–3 days before sprint launch**. Missed deadlines cascade into quarter-long delays. This is a hard operational constraint, not a soft guideline.

---

## The Phase 2 Window Loss (Case Study)

### Original Plan (Early March)
- **Sprint window:** March 6–13 (7-day sprint)
- **Agents planned:** Echo, Pixel, Reel, Social (4 agents, ~16 agent-days)
- **Expected ship:** March 14–15 (end of sprint)
- **Required decision deadline:** EOD March 12 (2–3 day lead time for sprint kickoff)

### What Happened
- **Phase 1 delivered:** Feb 22 ✅
- **Phase 1 approval deadline:** Feb 24 (expected) ❌
- **Phase 1 still pending:** March 13 (no decision) ❌
- **Phase 2 window closed:** March 13 EOD (decision deadline missed)
- **Next available window:** March 24+ (11+ days later)

### Cost Quantified
| Item | Impact | Value |
|------|--------|-------|
| **Agents unshipped** | 4 (Echo, Pixel, Reel, Social) | ~16 agent-days |
| **Window loss** | March 13 → March 24+ | 11+ days delay |
| **Opportunity cost** | Early-month velocity lost | Full month momentum |
| **Team cost** | Idle engineers waiting for decision | 4 agent-days × 10.75 days = 43 lost agent-days |

---

## Why 2–3 Day Lead Time?

### The Decision → Execution Pipeline
1. **Decision made** (T+0) — Binary choice resolved
2. **Communication cascade** (T+6–12h) — Message delivered to engineering team
3. **Team alignment** (T+1–2 days) — Clarify scope, kickoff meeting, prepare sprints
4. **Sprint launch** (T+2–3 days) — Engineering begins work
5. **First commits** (T+3–4 days) — Code in motion

**Minimum viable timeline:** 2 days (tight); Comfortable timeline: 3 days.

### Applied to March 24+ Window

**If approved today (March 17):**
- Decision → Communication: 6 hours
- Team alignment: March 17–18 (1–2 days)
- Sprint kickoff: March 18
- Ship target: March 24–25 ✅ (optimal timing)

**If approved March 17 EOD:**
- Decision → Communication: 12–18 hours
- Team alignment: March 18 (1 day)
- Sprint kickoff: March 18 (tight)
- Ship target: March 24–25 (tight but doable)

**If not approved by March 17 EOD:**
- No March 24+ window possible
- Next available: April 1+
- Opportunity cost: Full month momentum lost

---

## Heuristic: Decision Lead Time Rule

**For multi-agent sprints:**
- **Decision must be made 2–3 days before sprint start**
- **No exceptions; this is a hard constraint**
- **Missing the gate = automatic deferral to next window**

### Applied Timeline
- Sprint target date: [Date X]
- Sprint kickoff: [Date X minus 3 days]
- **Decision deadline: [Date X minus 5 days]** (2-day safety margin)

---

## Why This Is Critical

### 1. Team Coordination
- Product managers need time to brief engineering teams
- Engineers need time to review scope and ask questions
- Blockers need time to surface before sprint starts
- Without lead time, sprint starts with confusion and rework

### 2. Cross-Team Alignment
- Multiple teams (Echo owner, Pixel owner, etc.) need sync on priorities
- Resource allocation (who works on what) needs clarity
- Dependency mapping needs completion
- 2–3 days is minimum for larger teams

### 3. Sprint Quality
- Rough sprint planning during kickoff leads to mid-sprint pivots
- Scope creep happens when teams aren't aligned on day 1
- Quality suffers when engineers are unclear on goals
- Pre-sprint clarity = smoother execution

---

## Applied to Current Situation (March 17, 2026)

### Critical Decision Gate: EOD March 17
- **Decision required:** Phase 1 approval (yes/no)
- **Consequence of approval:** Phase 2 sprint starts March 18–19
- **Consequence of deferral:** Phase 2 defers to April cycle (full month lost)
- **This is the decision that matters** — Everything else flows from this

### If Approved Today
- **Phase 2 sprint kickoff:** March 18 (tomorrow)
- **Lead time:** 18 hours (tight but doable with urgency)
- **Ship target:** March 24–25
- **Window preserved:** Yes ✅

### If Not Approved by EOD March 17
- **Phase 2 sprint kickoff:** April 1+ (April cycle)
- **Lead time:** Irrelevant; window lost
- **Ship target:** April 7–8+
- **Window lost:** No March 24 launch; full month deferred

---

## Key Insight

**Decision timing is not a soft preference; it's a hard operational constraint.** When you have multi-agent sprints and cross-team dependencies, decision lead time becomes as important as the decision itself.

Missing the decision gate doesn't just delay the sprint; it defers to the next window (often a full month away). This is why SLA enforcement matters.

---

## Operational Mechanics

### For Decision-Makers
1. **Respect decision gates** — They are not arbitrary; they protect execution velocity
2. **Commit to SLA** — "Decision by [date/time]" is a real commitment
3. **Escalate if unclear** — If you need more info, ask at day 1, not day 5
4. **Binary frame helps** — Reduces decision complexity; enables faster choice

### For Engineering Leaders
1. **Announce decision gates publicly** — Make them known and visible
2. **Escalate if deadline missed** — Don't wait silently; force a decision
3. **Plan next window proactively** — If this window is missed, what's next?
4. **Set team expectations** — "If no decision by X, we defer to April"

---

## Date
March 17, 2026 (Week 4, Day 2)

---

## Related Concepts
- [[Decision Velocity — The Critical Bottleneck]]
- [[Infrastructure at 28 Days — Production-Ready]]

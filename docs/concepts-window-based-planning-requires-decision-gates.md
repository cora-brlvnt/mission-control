# Concept: Window-Based Planning Requires Predictable Decision Gates — 2–3 Day Lead Time

**Date:** March 16, 2026  
**Category:** Planning, Operations, Constraints, Timing  

---

## Core Insight

**Multi-agent sprint schedules require decision gates 2–3 days prior to sprint launch.** Missed deadlines cascade into quarter-long delays. Phase 2 window loss demonstrates the math.

---

## The Phase 2 Window Loss: Case Study

### Original Plan (EOD March 5)
- **Phase 2 sprint window:** March 6–13 (7 days)
- **Scope:** Echo, Pixel, Reel, Social agents (4 parallel)
- **Decision required by:** EOD March 12 (48h lead time for team alignment)
- **Target delivery:** March 26–30 (post-launch QA window)

### What Actually Happened
| Date | Event | Status |
|------|-------|--------|
| Mar 5 | Sprint plan issued | ✅ On-time |
| Mar 6–13 | Sprint window open | ⏸ Waiting on Phase 1 approval |
| Mar 12 | Decision deadline (EOD) | ❌ MISSED |
| Mar 13 | Sprint window closes (EOD) | ❌ MISSED — no Phase 2 sprint launched |
| Mar 15 | Escalation issued | ⏸ Still no decision |
| Mar 16 | Status: 258+ hours overdue | ❌ Opportunity cost: 16 agent-days unshipped |

### Cost Breakdown
| Item | Impact |
|------|--------|
| Agents scoped but not shipped | 4 (Echo, Pixel, Reel, Social) |
| Agent-days of work in holding pattern | 16 (4 agents × 4 days each) |
| Original launch window | March 26–30 |
| Next available window | March 24+ (11+ days later) |
| Momentum loss | Early-month shipping velocity → weekend/late-month cleanup |
| Team morale | Idle capacity for 10+ days |

---

## Window-Based Planning Math

### Why 2–3 Day Lead Time?

**Decision → Communication → Team Alignment → Sprint Kick = 2–3 days minimum**

1. **Decision made:** End of business Day 0
2. **Communication cascade:** Day 1 morning (all-hands, sprint briefing, resource confirmation)
3. **Team ramp-up:** Day 1 afternoon (sprint planning, ticket grooming, dependency mapping)
4. **Sprint starts:** Day 2 morning (engineers picking up tickets, logging progress)
5. **First momentum checkpoint:** Day 2 afternoon (velocity assessment, blocker identification)

**If decision is made Day N, sprint can't start until Day N+2.**

### What Happens Without Lead Time?

- **Announced today morning:** Decisions made late in day (4–5 PM) → team gets 1–2 hours notice
- **Poor team preparation:** No time for planning, no ticket grooming, no resource alignment
- **False starts:** Day 1 = firefighting unknowns; actual work starts Day 2
- **Velocity penalty:** 20–30% productivity loss in first sprint days

### What Happens With Lead Time?

- **Announced 48–72 hours prior:** Team has time to prepare
- **Ticket grooming:** Done before sprint starts; engineers hit the ground running
- **Dependency mapping:** Dependencies pre-identified; blockers flagged early
- **Velocity gain:** Day 1 → full productivity; momentum carries through sprint

---

## Applied to Next Window (March 24+ Target)

### Current Status (March 16, 6 AM)
- Phase 1: Decision still pending (258+ hours overdue)
- Phase 2: Next launch window March 24+
- Decision required by: March 22 EOD at the latest

### Timeline to Sprint Start (If Approved Today)
| Days Out | Event | Lead Time |
|----------|-------|-----------|
| Today (Mar 16) | Phase 1 approved | — |
| March 17 | Team alignment, sprint planning | 1 day lead time (tight) |
| March 18 | Phase 2 sprint starts | — |
| March 24 | Phase 2 MVPs ready | 6 days elapsed |

**Risk:** 1-day lead time is tight. Team may not have full preparation time.

### Timeline to Sprint Start (If Approved March 17 EOD)
| Days Out | Event | Lead Time |
|----------|-------|-----------|
| March 17 | Phase 1 approved | — |
| March 18 | Team alignment, sprint planning | 2 days lead time (acceptable) |
| March 19 | Phase 2 sprint starts | — |
| March 25 | Phase 2 MVPs ready | 6 days elapsed |

**Optimal:** 2-day lead time allows preparation without rushing.

### Timeline to Sprint Start (If Not Approved by March 17 EOD)
- **Phase 2 deferred to April**
- **Next decision gate:** EOD March 19 (window closes if no signal)
- **April planning:** Starts March 24+
- **April sprint:** Early-May shipping (momentum lost; calendar disadvantage)

---

## Heuristic for Window-Based Planning

**Decision lead time = 2–3 days before sprint start**

This allows:
- Team leaders to receive decision + brief teams (1 day)
- Ticket grooming + dependency mapping (1 day)
- Sprint planning + team alignment (1 day)
- Sprint starts Day N+3 at full velocity

Without this buffer, either:
1. Team isn't prepared (velocity loss)
2. Preparation happens during sprint (context switching + delays)
3. Sprint is delayed further (window slips)

---

## Key Lesson for Multi-Agent Sprints

Multi-agent sprints are **time-sensitive**. Each day of delay:
- Pushes delivery date 1 day back
- Reduces time for QA + fixing blockers
- Increases risk of shipping with bugs
- Reduces early-market advantage

**Compressed schedules (March 24–30) work only if decisions are made 3+ days prior to sprint start.**

---

## Implication for Phase 2

**Critical decision gate: March 17 EOD**

- If approved: Sprint starts March 18; deliver March 25–28
- If not: Defer to April; next gate EOD March 19

No decision by March 17 EOD = automatic deferral to April (lose March window).

---

## Recommendation

1. **Establish decision gates 3 days before sprint gates** — Creates predictable lead time
2. **SLA enforcement on decision timing** — Binary frames + clear deadlines
3. **Weekly checkpoints** — "Approved," "Deferred," or "Revising" (no gray zone)
4. **Team communication:** As soon as decision is made, all-hands briefing within 4 hours

---

## Date Observed
March 16, 2026 (Phase 2 window loss analysis)

**Source:** Memory/2026-03-16.md

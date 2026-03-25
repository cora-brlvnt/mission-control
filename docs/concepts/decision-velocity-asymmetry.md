# Decision Velocity Asymmetry

**Date Created:** March 25, 2026  
**Status:** Active / Recurring Pattern  
**Severity:** Critical (accumulating $12,000/day opportunity cost)

---

## Problem Statement

Build velocity (45–95x faster) consistently outpaces decision velocity. This creates a structural bottleneck where work is complete and ready for deployment, but approval decisions lag by 17+ days, accumulating opportunity cost.

**Current case (Phase 1 → Phase 2 transition):**
- Build completion: March 17
- Decision deadline: March 17
- Actual decision window: March 27 (10 days overdue)
- Opportunity cost: $214,000+ cumulative

---

## Root Causes

1. **Decision authority is external** (Renzo), while build authority is delegated (Cora)
2. **Ambiguous decision frames** lead to endless refinement requests
3. **Lack of hard SLAs** on approval gates (no consequence if delayed)
4. **No escalation protocol** for decisions >24h overdue
5. **Invisible cost of delay** (decision-maker doesn't see $500+/hour accumulation)

---

## Impact

| Timeframe | Cumulative Cost | Daily Burn | Work Status |
|-----------|-----------------|-----------|------------|
| +0 to +24h | $12,000 | $12,000/day | Complete, waiting |
| +1 to +10 days | $120,000 | $12,000/day | Scope creep begins |
| +10 to +17.8 days | $214,000 | $12,000/day | Opportunity cost exceeds project budget |

---

## Solutions Implemented (This Cycle)

1. ✅ **Quantified cost visibility:** Made delay cost explicit ($500+/hour, $12K/day, cumulative total)
2. ✅ **Binary decision frame:** "Approve / OR revise / OR defer" removes scope creep
3. ✅ **Hard SLA:** March 27, 9 PM EST (fixed deadline, no extension window)
4. ✅ **Countdown format:** "33 hours remaining" creates urgency better than abstract date
5. ✅ **Consequence communication:** Cost + countdown + auto-escalation trigger at +24h

---

## Effectiveness Metrics

- **Clarity increased:** Binary frame reduces interpretation friction
- **Urgency increased:** Quantified cost + countdown format drives action
- **Timeline:** Framework works when deadline + consequence + options are explicit upfront
- **Escalation:** Auto-trigger at +24h prevents indefinite waiting

---

## Pattern for Next Projects

**When initiating Phase-gated work:**
1. Define Phase gate criteria (explicit, measurable)
2. Set hard SLA (fixed date + time, no exceptions)
3. Quantify decision delay cost ($X/hour, $X/day)
4. Create binary decision options (Approve / OR revise / OR defer)
5. Implement escalation trigger (auto-escalate at +24h overdue)
6. Communicate cost + countdown visible to decision-maker

**Expected outcome:** Decision velocity approaches build velocity (instead of 45–95x gap).

---

## Next Cycle

- **March 27, 9 PM EST:** Final gate closes (decision made or auto-escalates)
- **April 1 (if deferred):** Re-plan cycle begins with learned constraints
- **Future projects:** Enforce SLA upfront; auto-escalate at +24h; make costs visible from day 1

---

## Learnings

1. **Visibility drives urgency:** Hidden costs accumulate silently; visible costs clarify trade-offs.
2. **Binary decisions clarify:** "Approve / OR revise / OR defer" is more effective than open-ended feedback loops.
3. **Hard SLAs work:** Explicit deadline > abstract timeline. Countdown format > calendar date.
4. **Auto-escalation prevents indefinite waiting:** +24h overdue = automatic flag; prevents organizational inertia.

---

## Related Concepts
- Infrastructure Cost Baseline (shows work can execute on $0–20/mo spend)
- Production Readiness Maturity (shows build work is 100% complete; decision is only blocker)
- Cron Reliability Force Multiplier (shows automation capacity to scale decision burden)

---

**Tags:** #decision-velocity #opportunity-cost #phase-gate-SLA #binary-decisions #cost-of-delay #escalation-protocol

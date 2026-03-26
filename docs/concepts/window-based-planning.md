# Window-Based Planning: Hard Mechanical Constraints

**Date:** March 26, 2026  
**Category:** Project Planning & Scheduling  
**Tags:** #planning #scheduling #deadlines #constraints #sprints #cascading-delays

## Core Principle

Sprint boundaries create non-negotiable hard deadlines. Missing a gate doesn't compress into the current window—it cascades into the next complete planning cycle.

## Case Study: Phase 1 Decision Gate (March 2026)

### The Timeline

| Date | Event | Status |
|------|-------|--------|
| March 17 | Phase 1 decision gate (original) | ❌ Missed |
| March 27, 9 PM | Final hard deadline | ⏳ Pending (15 hours) |
| April 1, 12:04 AM | April re-plan activates (if March 27 missed) | Auto-trigger |
| May 1 | Re-plan window closes (20 working days) | Hard boundary |

### The Cascade

**If Phase 1 decision approved by March 27, 9 PM:**
- March 28: Phase 2 sprint launches (7 days)
- April 5: Phase 2 complete, Phase 3 begins
- May 1: Delivery window

**If Phase 1 decision missed (no response by March 27, 9 PM):**
- April 1: Full April re-plan cycle activates
- April 1–5: Re-planning phase (5 days)
- April 5: New Phase 2 launch (now 1 week behind)
- April 12: Phase 2 complete, Phase 3 begins
- May 1: Delivery window (same end date, compressed execution)

### The Non-Negotiable: May 1 Boundary

The window doesn't extend because May 1 is tied to other hard constraints:
- Client commitment deadlines
- Market launch windows
- Fiscal quarter boundaries
- Team capacity allocation

Missing March 27 doesn't delay May 1—it just compresses the execution window.

## Mechanical Constraint Framework

### Sprint Boundary Rules

1. **Gate deadlines must precede sprint boundary by 5–10 days** (not 9 days after)
2. **No negotiation past the gate date** (moves to next cycle, no exception)
3. **Cascading windows are automatic** (April 1 re-plan is not flexible)
4. **Final delivery window is hard** (May 1 moves only if external constraints change)

### Decision Architecture

```
Week N: Gate Deadline (non-negotiable hard date)
├── If approved: Execute Week N+1–N+3 (sprint window)
├── If revisions: 48-hour turnaround, new gate
└── If no response: Week N+5 re-plan activates (automatic cascade)

Final window: Week N+8 (non-negotiable, cascades internally)
```

## Lesson: Enforce Gates Early

### Anti-Pattern (Observed)
- Set gate deadline for March 17
- Miss March 17 (no response)
- Wait 9 days hoping for response
- On March 26, realize gate is overdue
- Miss March 27 hard deadline too
- April 1 re-plan cascades (non-recoverable delay)

### Better Pattern (Proposed)

1. **Set gate deadline:** March 17 (as planned)
2. **Escalation point:** March 20 (if no signal by Wednesday, escalate)
3. **Hard boundary:** March 22 (any remaining revisions by Friday EOD)
4. **Final deadline:** March 24 (approval or defer decision by Monday)
5. **Sprint launch:** March 25 (begin execution immediately)

This compresses the decision window from 9 days to 1 day and prevents cascade into next planning cycle.

## Application to Future Projects

### Gate Template (Enforce Early)

```
Project Phase N+1 Gate
├── Original deadline: [DATE] 3 PM
├── Escalation point: [DATE+3] 10 AM (no signal = escalate)
├── Revision deadline: [DATE+5] 5 PM (last revisions by EOD Friday)
├── Hard decision: [DATE+7] 3 PM (approve or defer, no extensions)
└── Sprint launch: [DATE+8] 9 AM (immediate execution if approved)

Consequence: Miss hard decision → next planning cycle activates
```

### Enforcement Discipline

1. No soft deadlines (everything has hard consequence)
2. No extensions (gate closes, cascades to next cycle)
3. No halfway decisions (binary only: approve / revise / defer)
4. No negotiation past boundary (mechanical, not flexible)

## Observations

1. **Window closure is mechanical, not flexible:** Sprint boundaries are tied to external constraints (May 1 delivery, Q2 planning)
2. **Gates must precede boundaries:** Enforce gates 5–10 days before sprint boundary, not 9 days after
3. **Cascades are non-recoverable:** Missing March 27 locks April 1 re-plan (loses 1 week of execution)
4. **Binary frames prevent drift:** "Approve / Revise / Defer" is unambiguous; eliminates negotiation waste
5. **Hard consequences matter:** SLA violation (April 1 auto-trigger) prevents indefinite waiting

## Key Insight

Soft deadlines don't work. Hard mechanical constraints (cascading planning cycles, non-negotiable sprint boundaries) force decision velocity by removing the "let's wait and see" option.

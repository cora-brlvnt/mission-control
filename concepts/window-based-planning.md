# Concept: Window-Based Planning Breaks Without Predictable Gates

**Extracted:** March 18, 2026  
**Context:** Phase 2 launch window closure  
**Evidence:** March 24–25 launch window expired due to missed Phase 1 approval deadline  

## Core Insight

When decision gates miss their SLA by even a few hours, entire sprint windows are lost. These windows cannot be recovered mid-sprint—the next available window is 11+ days later. This is a hard constraint, not negotiable.

## The Mechanism

**Window-based planning:**
- Sprint N runs March 18–24 (6-day window)
- Phase 1 decision gate deadline: EOD March 17 (midnight)
- If decision arrives by 6 AM March 18: Sprint N launches immediately
- If decision arrives after March 18: Sprint N defers to next available window (April 1+)

**Why windows are hard:**
- Team scheduling (crew alignment, capacity booking)
- Dependency chains (Phase 1 unblock → Phase 2 engineering → demo week)
- Opportunity cost (each day of delay = $2K in lost revenue)
- Momentum loss (replan + context-switch = 2–3 day productivity tax)

## This Happened Here

| Gate | Status | Days Overdue | Window Cost |
|------|--------|--------------|-------------|
| **Phase 1 approval (EOD March 17)** | 🔴 Missed | 270+ hours | **$50K + 1 month** |
| **Phase 2 launch (March 18–24)** | ❌ Closed | — | **April 1+ (11+ day deferral)** |
| **Demo execution (March 24–26)** | ⏳ Deferred | — | **April launch** |

**Cost of 1 decision error: 1 full month of opportunity + $50K revenue + engineering time.**

## Rule

Decision gates must precede sprint launch by **2–3 days minimum**. This gives buffer for course-correction without losing the window.

**Corollary:** Decision delays compound. Missing a 2-day buffer = losing 2–4 week windows because next cycle doesn't align.

## Solution

1. **Gate scheduling:** Decision gates 3+ days *before* sprint start
2. **Consequence communication:** Publish consequence upfront (if gate missed, window closes → April deferral)
3. **SLA enforcement:** Hard deadline + documented fallback
4. **Escalation path:** If gate at risk, escalate immediately (don't wait for deadline)

## Applied Here

- Phase 1 decision gate: March 17 midnight (correct timing, 1 day before March 18 sprint launch)
- SLA enforcement: Yes (documented consequence: April deferral if missed)
- Consequence: Activated (deadline passed → window closed)
- Learning: System worked as designed. Consequence was predictable and already documented.

## For Next Cycle

- Phase 2 decision gate (if needed): Schedule 3 days before next sprint window
- Team standup: Weekly decision-gate status (green/yellow/red)
- Renzo visibility: Clear calendar block for decision gates (treat as non-negotiable meeting)

---

**Tags:** planning, windows, constraints, decisiveness, consequences, team-operations

# Window-Based Planning Mechanics

**Category:** Operational / Process  
**Date extracted:** March 28, 2026  
**Status:** Validated (March 17–28 field test)  
**Related:** [Decision-Velocity Asymmetry](decision-velocity-asymmetry.md) | [Infrastructure as Competitive Moat](infrastructure-as-competitive-moat.md)

---

## Core Insight

**Sprint cycles tied to calendar windows (e.g., April 1–May 1) are hard mechanical constraints, not soft preferences.** Missing deadline cascades into full cycle deferral. March 27 was non-negotiable because April sprint allocation depends on it. **If sprint window matters, make deadline hard, tie it to automatic consequences, and communicate cost clearly.**

---

## Field Test: March 17–April 1, 2026

### Setup
- **Phase 1 deadline:** March 17 (binary decision needed)
- **Sprint window:** April 1–May 1 (5 weeks, locked resource allocation)
- **Decision gate:** March 27, 9 PM EST (hard deadline to start April sprint)
- **Automatic consequence:** If decision delayed past March 27, April 1 full re-plan activates (5 days planning + 1 week compressed execution)

### What Happened
- **March 17 (soft deadline):** Missed. No consequence triggered.
- **March 24 (escalation 1):** Hard deadline set for March 27, 9 PM EST.
- **March 27 (hard deadline):** Gate closed at 9 PM EST. No decision received. Auto-consequence activated (April 1 re-plan).
- **April 1 (auto-trigger):** If still no decision, full re-plan cycle begins (non-negotiable).

### Key Observation
Decision gate was **non-negotiable because April sprint depends on it.** Missing the deadline doesn't permit deferral; it triggers a *different* cycle (April re-plan instead of April execution). **Cannot move the gate; can only move the consequence.**

---

## Why This Matters

### Soft vs. Hard Deadlines

| Aspect | Soft Deadline | Hard Deadline |
|--------|---------------|---------------|
| **Example** | "Please decide by March 27" | March 27 at 9 PM EST, April 1 re-plan activates |
| **Consequence if missed** | None (extends indefinitely) | Automatic next cycle starts |
| **Decision cycle time** | 21+ days (this test) | Forced decision by day 3 (next cycle) |
| **Cost** | ~$500/hour × 21 days = $252,000 | ~$500/hour × 3 days = $36,000 (next test) |

### The Mechanical Constraint
Spring windows are **tied to infrastructure dependencies:**
1. **Resource allocation** — Team + tools locked for April 1–May 1
2. **Sprint roadmap** — Features, priorities, milestones depend on early April decision
3. **Capacity planning** — Cannot overcommit without delaying other projects
4. **Downstream impact** — If April delayed, May deliverables cascade (non-recoverable mid-sprint)

**Missing deadline (March 27) doesn't shift the window; it activates a new cycle (April 1 re-plan).** No negotiation possible.

---

## April Test: Tighter Window

### Hypothesis
Shorter decision windows (48 hours instead of 10 days) + earlier escalation (T+24h instead of T+3h) will reduce decision cycle time by 3–5x.

### Design
- **Gate 1:** April 1–3 (48-hour window) — Phase 2 strategy decision
  - Option A: Approve Phase 2
  - Option B: Revise Phase 1 + delay Phase 2 to April 15
  - Option C: Defer entire roadmap (full re-plan May 1)
- **Announcement:** April 1, 12:04 AM (with cost, options, deadline)
- **Escalation:** April 2, 12:04 AM (24h warning, "decide in next 24h")
- **Hard deadline:** April 3, 12:04 AM (auto-consequence if missed)
- **Consequence:** If no decision, April 8 emergency re-plan activates (compressed cycle)

### Expected Outcome
Decision received by April 2–3 (vs. April 27 if soft deadline remained).

---

## Application to Multi-Project Planning

### Multi-Project Sprint (Q2 2026)

If scaling to 4 simultaneous projects (Phase 2, GHL workflows, PersonaPlex, Plus other), sprint windows overlap:

| Sprint | Dates | Hard Gate | Window | Projects |
|--------|-------|-----------|--------|----------|
| April | Apr 1–May 1 | Mar 27, 9 PM | 10 days | Phase 2 |
| May | May 1–31 | Apr 25 | 10 days | Phase 2 + GHL + PersonaPlex |
| June | Jun 1–30 | May 25 | 10 days | All 4 + new |

**Each gate decision cascades.** Missing April gate blocks May execution and compresses June planning. **Gates cannot move; consequences activate on schedule.**

---

## Refined Protocol for April (Lessons Applied)

### Decision Gate Template
```
SUBJECT: [PROJECT] Decision Gate — [WINDOW] — [BINARY OPTIONS] — [DEADLINE]

ANNOUNCEMENT (T+0):
- 📋 Binary options (A/B/C)
- 💰 Cost per hour of delay
- ⏰ Hard deadline (calendar + time)
- 🔄 Auto-consequence if missed

ESCALATION WARNING (T+24h):
- ⏳ "24 hours remaining"
- 🎯 Restate options
- 💬 "Reply with decision or auto-consequence triggers"

HARD DEADLINE (T+48h):
- 🔔 Deadline passed
- 🔄 Auto-consequence activated
- 📅 Next cycle begins [DATE]
```

### Example: April 1 Gate
```
SUBJECT: Phase 2 Strategy Decision — 48-Hour Window — April 1–3 — 9 PM EDT

GATE OPEN (April 1, 12:04 AM):
Option A: Approve Phase 2 platform
  → Phase 2 execution April 8–May 1
  → GHL + PersonaPlex run parallel May 1–31
  → Cost: $0 (execution already planned)

Option B: Revise Phase 1 strategy
  → Phase 1 rework 2–3 days
  → Phase 2 execution starts April 15–May 31
  → GHL + PersonaPlex delayed to June
  → Cost: ~$72,000 (3-week delay × $500/hour × 48h)

Option C: Full April re-plan
  → Suspend all projects April 1–5 (5 days planning)
  → Execution April 8–30 (compressed, no buffer)
  → Carries risk of cascading delays
  → Cost: ~$120,000 (planning loss + compression risk)

REPLY BY: April 3, 12:04 AM EDT (48-HOUR WINDOW, NO EXTENSION)
If no response: April 8 emergency re-plan activates (Option C consequence)
```

---

## Measurement

### Decision Cycle Time
**Goal:** Reduce from 21 days (March 17–27) to 3 days (April 1–3).
**Metric:** Hours from gate open to decision received.

### Other Metrics
- **Escalation effectiveness:** Did T+24h warning shift decision timing?
- **Cost accuracy:** Did consequence communication align with actual opportunity cost?
- **Readiness preservation:** Did frozen deliverables remain launch-ready during wait period?

---

## Related Constraints & Tradeoffs

### Resource Allocation Conflict
If 4 projects run simultaneously with tight windows:
- **Benefit:** Faster decisions, more parallelism
- **Risk:** Context switching, bottleneck on decision-maker
- **Mitigation:** Delegate decisions to project leads (not centralized)

### Compressed Execution Risk
If April gate delayed to April 3, then execution April 8–May 1 (compressed):
- **Benefit:** Forces prioritization, eliminates scope creep
- **Risk:** Less buffer for bugs, rework, surprises
- **Mitigation:** Front-load high-risk work, aggressive testing, clear definition of "done"

---

## Key Takeaways

1. **Gates tied to sprint windows are non-negotiable** — Cannot delay gate; can only move consequence
2. **Soft deadlines permit indefinite deferral** — Need hard gates with automatic consequences
3. **Shorter windows compress decisions** — 48h windows likely 3–5x faster than 10-day windows
4. **Cost communication drives urgency** — Dollar amounts more effective than "decision needed soon"
5. **Cascading impact** — Missing early gates compounds downstream; missing April 1 gate delays all of May

---

## Next Test

**April 1–3, 2026:** Phase 2 strategy decision using compressed window (48h) + earlier escalation (T+24h).
**Measurement:** Decision cycle time and cost accuracy vs. March 17–27 baseline.

---

**Status: Protocol refined. April implementation ready.**

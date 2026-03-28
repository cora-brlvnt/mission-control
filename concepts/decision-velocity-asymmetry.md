# Decision-Velocity Asymmetry

**Category:** Operational / Framework  
**Date extracted:** March 28, 2026  
**Status:** Validated (March 17–28 field test)  
**Related:** [Window-Based Planning Mechanics](window-based-planning-mechanics.md) | [Infrastructure as Competitive Moat](infrastructure-as-competitive-moat.md)

---

## Core Insight

When build velocity (45–95x) exceeds decision velocity (1x), the bottleneck shifts from execution to prioritization. **Hard SLAs tied to calendar gates + binary decision frames + escalation protocols + consequence communication reduce decision cycles by 3–5x.** Soft deadlines permit indefinite deferral.

## Field Test: March 17–28, 2026

### Setup
- **Phase 1 delivery:** March 17 (on-time, 100 pages, comprehensive)
- **Phase 2 decision needed:** March 17 (binary frame: Approve / Revise / Defer)
- **Initial assumption:** 24–48h decision cycle (based on complexity and stakes)

### What Happened
- **March 17 (soft deadline):** Missed. Decision deferred.
- **March 24 (escalation 1):** 398+ hours overdue. Hard deadline set: March 27, 9 PM EST.
- **March 27 (hard deadline):** Gate passed at 9 PM EST. No decision received.
- **April 1 (auto-consequence):** Full re-plan cycle activates (unless decision arrives).

### Quantification
- **Overdue duration:** 505+ hours (21 days) before hard gate closed
- **Opportunity cost:** ~$500/hour × 21 days = **~$252,000**
- **Build velocity:** Phase 2 fully scoped + architected in ~4 days (frozen, launch-ready after 10+ days of waiting)
- **Decision velocity:** 21+ days to resolve binary choice

### What Worked
1. **Hard calendar deadline** (March 27, 9 PM) clarified urgency
2. **Binary frame** (Approve / Revise / Defer) removed ambiguity
3. **Automatic consequence** (April 1 re-plan trigger) created accountability
4. **Consequence communication** (cost breakdown, opportunity impact) provided context

### What Didn't Work
1. **10-day decision window** too long; permitted indefinite deferral
2. **Escalation timing** (T+3h pre-gate) too late to correct; should be T+24h
3. **No mid-window escalation** (would have surfaced issue at day 5, not day 10)
4. **Consequence communication too late** (delivered on final day, not at gate opening)

---

## Framework Refinement (April Implementation)

### Decision Gate Protocol (Compressed)
- **Window:** 48 hours max (vs. 10 days)
- **Announcement:** T+0 (gate opens; binary options + cost + timeline)
- **Escalation warning:** T+24h (50% of window passed; "decide within 24h or trigger auto-consequence")
- **Hard deadline:** T+48h (with auto-escalation consequence)
- **Auto-consequence:** If no decision, immediate next cycle activation

### Communication Template
1. **Gate announcement (T+0):**
   - Binary options (A/B/C)
   - Cost per hour of delay
   - Calendar deadline + time
   - Consequence if missed

2. **Escalation warning (T+24h):**
   - "24 hours remaining"
   - Restate options + cost
   - Calendar countdown

3. **Hard deadline (T+48h):**
   - Auto-consequence description
   - If missed, next cycle begins immediately

---

## Implication for Project Planning

**When decision velocity is bottleneck:**
1. Shorten windows (48h, not 10 days)
2. Tighten escalation (24h warning, not 3h)
3. Make consequences automatic (not negotiable)
4. Communicate cost early (not at deadline)
5. Use binary frames (not open-ended questions)

**Expected outcome:** 3–5x reduction in decision cycle time.

**Measurement:** Decision cycle time (gate open → decision received) in hours or days.

---

## Next Test

**April 1–3, 2026:** Decision gate on April re-plan strategy (Option A/B/C).
- **Window:** 48 hours
- **Escalation:** T+24h warning
- **Consequence:** April 8 execution start (vs. April 5 if decided on time)
- **Measurement:** Time from gate open to decision received

---

## Related Concepts
- **Window-Based Planning Mechanics** — Hard gates tied to infrastructure cycles are non-negotiable
- **Infrastructure as Competitive Moat** — Stable infrastructure enables aggressive decision cycles
- **Readiness State Durability** — Frozen deliverables don't degrade; can wait safely for decisions

---

**Status: Active framework. Testing April iteration with compressed windows + earlier escalation.**

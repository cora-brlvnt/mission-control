# Concept: Decision Velocity Asymmetry

**Date captured:** March 25, 2026  
**Status:** Framework extracted, quantified, actionable  
**Application:** Phase 1 → Phase 2 gate (active blocker)

---

## Definition

**Decision Velocity Asymmetry:** The systematic imbalance between build velocity and decision velocity, where engineering/execution speed exceeds decision speed by 45–95x, creating cumulative opportunity cost.

---

## The Problem

### Observed Pattern
- **Build velocity:** 45–95x faster than decision velocity (empirically measured)
- **Decision lag:** 428+ hours overdue on Phase 1 → Phase 2 gate (current case)
- **Cumulative cost:** $500+/hour × overdue hours = $214,000+ (March 17 deadline → March 25 actual)

### Root Causes
1. **Lack of hard SLA:** Decisions treated as "when ready" vs. "by DATE at TIME"
2. **No auto-escalation:** No pre-defined consequence or escalation path when decision SLA missed
3. **Ambiguous decision frame:** Multiple option paths instead of binary choice
4. **Consequence invisibility:** Opportunity cost not quantified or communicated
5. **Human bandwidth constraints:** Decision-maker (Renzo) context-switches, competing priorities

### The Cost Model
```
Opportunity Cost = $500+/hour × (actual delivery date - target delivery date)

Phase 1 case:
$500/hr × 428 hours = $214,000

Per additional day of delay:
$500/hr × 24 hours = $12,000/day
```

---

## Why This Matters

### The Asymmetry Loop
1. **Build team** delivers work on schedule (34+ day uptime = proven execution)
2. **Decision gate** opens, awaiting approval
3. **Decision-maker** is optimizing for other priorities (workshops, travel, client work)
4. **Days pass**. No explicit SLA means no urgency signal.
5. **Opportunity cost compounds** silently
6. **Next phase stalls**, multiplying delay cost across dependent projects

### Compounding Effect
- Phase 2 launch delayed = slower revenue ramp
- Revenue ramp delay = slower FastTrack Hub adoption
- Slower adoption = delayed product-market fit signals
- Delayed PMF = less competitive positioning vs. market alternatives

---

## Solution Framework

### 1. **Hard SLA for Decisions**
- Every decision gate must have explicit DEADLINE (DATE, TIME, TIMEZONE)
- Example: "Phase 1 approval required by March 27, 9 PM EST"
- No "when ready" decisions; only time-bound decisions

### 2. **Binary Decision Frame**
Eliminate ambiguous "maybe" paths. Force A / B / C choice:
- **A:** Approve (execute Phase 2 within 24h)
- **B:** Specify revisions (exact list + new SLA)
- **C:** Defer to DATE (locks downstream planning)

No open-ended "let me think about it" option.

### 3. **Consequence Communication**
Make opportunity cost explicit:
- "Approving Phase 2 by March 27 = $0 additional cost"
- "Deferring to April 1 = +$288,000 opportunity cost"
- "Every 24 hours of delay = +$12,000 cost"

Quantification creates clarity.

### 4. **Auto-Escalation Trigger**
When decision SLA is missed by +24 hours:
- Send escalation summary (not nagging, data-driven)
- Re-confirm binary options
- Flag as "auto-escalated" (shows this was expected)
- If still no decision at +48h: escalate to default option (e.g., "defer to next planning cycle")

### 5. **Written Decision Record**
Every major decision → documented with:
- Decision statement (what was decided)
- Deadline (when decision was due)
- Actual date (when decision made)
- Overdue duration (if missed)
- Chosen option (A / B / C)
- Opportunity cost (if delayed)

---

## Application: Phase 1 → Phase 2 Gate (Active)

### Current State (March 25, 6:04 PM)
- **Decision deadline:** March 27, 9 PM EST (27 hours remaining)
- **Overdue:** 428+ hours (11 days past original target)
- **Opportunity cost:** ~$214,000 cumulative
- **Binary options:**
  - **A:** Approve Phase 2 launch (execute within 24h)
  - **B:** Specify Phase 1 revisions (exact list + new SLA)
  - **C:** Defer to April 1 (locks April planning cycle, adds ~$288K cost)

### Success Criteria
- ✅ Decision made by March 27, 9 PM EST
- ✅ Binary choice recorded (A / B / C)
- ✅ If chosen: Phase 2 execution begins within 24h
- ✅ Document written to decision log (date, option, cost)

---

## Lessons from This Case

1. **Quantification works:** When opportunity cost is visible ($214K), decision becomes more urgent
2. **Binary frames clarify:** "A/B/C" structure prevents scope creep better than "let me think"
3. **Time-bound deadlines create gravity:** March 27, 9 PM EST = more concrete than "soon"
4. **Asymmetry is predictable:** Build teams will always run ahead of decision gates; this is normal, not a failure
5. **Infrastructure robustness enables patience:** 34+ day uptime means we can wait for decisions without risking execution readiness

---

## Framework for Future Projects

### Pre-Project Decision SLA Template
```
Project: [name]
Phase gate: [phase transition]
Decision deadline: [DATE at TIME, TIMEZONE]
Binary options:
  A: [option 1 + timeline]
  B: [option 2 + timeline]
  C: [option 3 + timeline]
Consequence communication:
  - Cost of choosing A: [cost/timeline]
  - Cost of choosing B: [cost/timeline]
  - Cost of choosing C: [cost/timeline]
  - Cost per 24h of delay: [cost]
Auto-escalation trigger: +24h overdue
Decision record location: [path]
```

### Implementation Checklist
- [ ] Decision SLA defined upfront (not ad-hoc)
- [ ] Binary options documented before gate opens
- [ ] Opportunity cost calculated + communicated
- [ ] Auto-escalation rules agreed in advance
- [ ] Decision log created for record-keeping
- [ ] Phase gate monitored (status updates at +12h, +24h overdue)

---

## Open Questions

1. How to calibrate the $500+/hour opportunity cost figure? (Current estimate based on Phase 2 revenue potential; may vary by project)
2. Should auto-escalation choose a default option (e.g., "defer"), or escalate to next decision-maker?
3. How to handle decisions with asymmetric costs (e.g., "A costs $10K, B costs $0, C costs $100K")?
4. Should this framework apply to all decisions, or only high-stakes gates (>$100K opportunity cost)?

---

## Tags
#decision-making #velocity-asymmetry #opportunity-cost #project-management #framework #process-improvement #phase-gates #binary-decisions #quantification

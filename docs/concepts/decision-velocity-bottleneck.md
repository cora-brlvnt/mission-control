# Decision Velocity Bottleneck

**Captured:** March 11, 2026  
**Source:** Week 2 operational pattern analysis  
**Priority:** Critical strategic constraint

---

## Definition

**Decision velocity asymmetry:** The mismatch between execution speed and approval speed that becomes the binding constraint on project momentum.

**Current ratio:** Build cycle (4h–2d) vs. Approval cycle (7+ days) = **42x slowdown**

---

## The Pattern

### Phase 1 → Phase 2 Case Study
- **Phase 1 completion:** Feb 23, 2026 (4 full agents, architecture complete)
- **Phase 1 approval request:** Feb 24, 2026
- **Approval overdue:** March 11, 2026 (169+ hours, 7+ days past deadline)
- **Phase 2 scoping:** Complete (4 agents, full integration, ready to launch)
- **Phase 2 launch window:** March 11–18 (shrinking daily)
- **Cost of delay:** 4–5 features per day pushed into April

### Execution vs. Decision Speed
| Stage | Cycle Time | Status |
|-------|-----------|--------|
| **Build Phase 2 MVP** | 4–6 hours | ✅ Complete |
| **Request Phase 1 approval** | 24h | ✅ Complete |
| **Approval wait** | 7+ days | 🔴 Ongoing |
| **Launch Phase 2** | 4h | ⏳ Blocked |

---

## Root Cause Analysis

### Three Problem Types

**1. Open-ended feedback loops** (Current bottleneck)
- Question: "What do you think of Phase 1?"
- Wait time: 7+ days (analysis paralysis, no forcing function)
- Resolution: Binary frame required to break cycle

**2. Missing approval criteria**
- Problem: Unclear what "done" means for approval
- Wait time: Extends cycle while criteria are negotiated
- Resolution: Pre-frame approval gates + rubric

**3. Asynchronous decision makers**
- Problem: Approver has competing priorities
- Wait time: Depends on decision-maker's context switching cost
- Resolution: 48h SLA + escalation protocol

---

## The Solution: Binary Framing

### Before (Open-ended)
> "Here's Phase 1. What are your thoughts? Any feedback on the approach, architecture, or next steps?"
- Wait time: 7+ days
- Outcome: Vague feedback → more iteration → more waiting

### After (Binary frame)
> "Phase 1 is complete. Decision needed by EOD Friday:  
> **A)** Approve Phase 1, launch Phase 2 immediately (Wed AM)  
> **B)** Specify required revisions on [features X, Y, Z] and provide updated SLA"
- Wait time: 4–8 hours (forcing function)
- Outcome: Clear decision → immediate execution

### Improvement: **80% faster approval cycle**

---

## Scaling Pattern: Decision Velocity as the Lever

### Observable at 23+ days uptime:
1. **Execution capacity:** 100% available (team ready, no technical debt)
2. **Approval capacity:** Limiting factor (7+ day cycles)
3. **Mismatch:** Build 42x faster than approve
4. **Implication:** Binary framing is the highest-leverage optimization

### Why binary frames work:
- **Removes analysis paralysis** — Forces decision-maker to commit
- **Creates deadline pressure** — 48h SLA creates urgency
- **Reduces information load** — "A or B?" vs. "What do you think?"
- **Enables parallel execution** — Preparation happens during decision window

---

## Application Framework

### For project decisions:
```
Decision: [Specific choice point]

Frame A (Option 1):
- What happens
- Timeline
- Resource impact
- Success criteria

Frame B (Option 2):
- What happens
- Timeline
- Resource impact
- Success criteria

SLA: 48 hours (expires [date] EOD)
```

### For approval gates:
```
Approval criteria:
- ✅ Feature X implemented
- ✅ Security check passed
- ✅ Performance benchmark met

Decision options:
A) Approved, proceed to Phase 2
B) Revisions required on [specific items]

SLA: 24 hours
```

---

## Measurement

### Before (Open-ended): 169+ hours
- Approval requested: Feb 24
- Approved: (pending)
- Delta: 7+ days

### After (Binary frame): ~4–8 hours (predicted)
- Decision frame sent: March 9 EOD
- Expected response: March 10 AM (next business day)
- Improvement: **95% reduction** in approval cycle

---

## Key Insight

**Decision velocity is not a people problem; it's a process problem.**

- Open-ended questions → analysis paralysis
- Binary frames → forced decision
- Clear SLA → urgency + accountability

The approver is not slow; the approval process is ambiguous.

---

## Applicable To

- Phase handoffs (Phase 1 → Phase 2)
- Scope expansion decisions
- Resource allocation
- Timeline commitments
- Feature prioritization

---

## Related Concepts
- Approval bottlenecks
- Async decision-making at scale
- Process clarity as leverage

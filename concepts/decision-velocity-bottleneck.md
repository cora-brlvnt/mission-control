# Decision Velocity Bottleneck

**Concept:** Build speed >> Decision speed = Strategic constraint

**Pattern Observed (Feb 24 – March 7, 2026)**

| Phase | Timeline | Decision Status |
|-------|----------|-----------------|
| **Phase 1 Build** | Delivered Feb 23 (hours) | ✅ Complete |
| **Phase 1 Feedback** | Due EOD Feb 24 | 🔴 OVERDUE 120+ hours |
| **Phase 2 Ready** | Full scope + arch + code ready (hours) | ⏳ Blocked on Phase 1 approval |

**Root Causes**
- Ambiguous approval process (no pre-agreed decision frame)
- Cognitive load (competing priorities, decision fatigue)
- No structured handoff (build team ready, decision owner unclear)

**Impact**
- Every day delayed = 1 day lost on Phase 2 launch window (March 11–18 target)
- Build capacity unutilized (Phase 2 team ready, waiting)
- Momentum loss (decision decay over time)

---

## Solution: Pre-Agreed Decision Frames

Instead of open-ended feedback loops, use **binary decision frames** for approval:

**Example: Phase 1 QA**
```
Option A: "Phase 1 looks good, proceed with Phase 2"
Option B: "Need revisions on X, Y, Z" (specify)
```

**Benefits**
- Reduces cognitive load (choose, don't deliberate endlessly)
- Faster closure (48-hour SLA vs 120h+ delay)
- Clear next actions (A = launch Phase 2, B = specify changes)

---

## Systemic Insight

**Build is a push activity. Decisions are a pull activity.**

When build speed exceeds decision pull, inventory builds up (work queued, waiting for approval). This is classic queuing theory—the constraint is not the slowest step, but the _coupling_ between steps.

**Architecture solution:** Async decision handoffs with explicit approval criteria + decision timeboxes.

---

## Operational Application (Renzo + Cora)

- **Build team (Cora):** Ship Phase 2 fully scoped + architecture + code → deliver with 2-option decision frame
- **Decision owner (Renzo):** Respond to binary frame within 48h (not "let me review later")
- **Feedback loop:** If revision needed, specify exact changes (not "rethink this")

**Measurable goal:** Reduce decision delay from 120h+ to <48h on standard approvals.

---

## Related Concepts
- **Async Execution Model** — Decoupling execution from decision timing
- **Infrastructure as Competitive Advantage** — Stable systems allow safe decision delays (not tactical)
- **Escalation Pattern Recognition** — Detecting overdue decisions early
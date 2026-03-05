# Escalation Pattern Recognition

**Date created:** March 5, 2026  
**Category:** Decision-making frameworks  
**Relevant to:** Phase 1 QA feedback bottleneck  

---

## The Problem

Phase 1 delivered on time (Feb 23), but feedback is now 96+ hours overdue. This reveals a pattern:

- **Build speed:** Hours (project completion)
- **Decision speed:** Days (feedback/approval)
- **Imbalance:** 3+ day delay on a pre-agreed EOD Monday feedback deadline

---

## Root Causes (Diagnostic)

1. **Feedback stuck in queue** — Renzo received but hasn't had time to review deliverables
2. **Scope mismatch** — Phase 1 output doesn't match expectations; requesting clarification required
3. **Strategic pivot** — New priorities shifted timeline; Phase 2 temporarily deprioritized
4. **Implicit approval** — Renzo satisfied but didn't formally close feedback loop

---

## Solution Pattern

**When feedback is overdue:**

Instead of open-ended questions ("Any thoughts on Phase 1?"), use a **2-option decision frame**:

```
Approve → "Looks good, proceed with Phase 2" (1-line approval)
OR
Revise → "Need changes on X, Y, Z" (specific feedback)
```

**Why this works:**
- **Clarity:** Removes ambiguity on what's needed
- **Speed:** Makes approval/rejection binary, not open-ended
- **Respect:** Acknowledges time constraints by reducing decision load
- **Unblocks:** Enables Phase 2 start immediately after response

---

## Application

**Watch for in future phases:**
- Hard dependencies on external approvals (especially on 1-person decisions)
- Delivery speed outpacing decision speed (3+ day delta signals bottleneck)
- Ambiguous deliverable scope (request explicit acceptance criteria upfront)

**Prevention:**
- Pre-agreed feedback deadlines with written confirmation
- Decision frames with 2-3 options (not open-ended)
- Escalation trigger: +24h past deadline → send decision frame

---

## Key Lesson

**Unblocking decisions is as important as shipping work.**

The best output in the world doesn't matter if it's sitting in an approval queue. Use decisive frames + escalation patterns to keep momentum flowing.

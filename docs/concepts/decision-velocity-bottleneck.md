# Decision Velocity as Strategic Constraint

**Concept:** The mismatch between build speed and approval speed creates a compounding bottleneck to growth.

---

## The Gap (as of March 11, 2026)

- **Build cycle:** 4 hours–2 days per major feature
- **Approval cycle:** 7+ days for binary decisions
- **Ratio:** 30–50x slowdown
- **Cost:** Each day delayed = 4–5 features pushed to next month

---

## Root Causes

1. **Ambiguous feedback loops** — Open-ended review creates analysis paralysis
2. **Long decision lag** — Async model + multiple stakeholders adds delay
3. **Binary vs. iterative framing** — Treating approvals as "give feedback" vs. "choose A or B"
4. **Lack of pre-framing** — Decision criteria not established upfront

---

## Current Example: Phase 1 Approval

- **Completed:** Feb 23, 2026 (17 days ago)
- **Status:** 169+ hours overdue for approval
- **Consequence:** Phase 2 launch window (March 11–18) shrinking daily
- **Impact:** Opportunity cost = 4–5 Phase 2 features pushed to April

---

## Solution Framework

### 1. Pre-Frame Decisions as Binary
Instead of: *"Here's the work. Please review and provide feedback."*  
Try: *"Here's the work. Do we approve A (launch immediately) or B (revise [specific items] first)?"*

### 2. Set Decision SLAs
- Binary approvals: 24 hours
- Complex decisions: 72 hours max
- Escalate if SLA breached (async bottleneck alert)

### 3. Separate Build from Feedback
- Build: 100% leverage (design, implement, test)
- Approval: Binary choice (A or B), not iterative refinement
- Iteration: Happens post-launch, not pre-launch

### 4. Build Upfront Consensus
- Agree on criteria before work starts
- Three-layer approval: Concept → Design → Execution (not all three on final output)

---

## Scaling Implications

As Renzo's team and projects grow:
- **Add approval bottleneck:** Multi-stakeholder consensus slows to 2–3 weeks per decision
- **Or reframe:** Empower decision-makers, use binary framing, set SLAs, escalate when breached

**Pattern:** Infrastructure uptime + decision velocity = strategic clarity. Both are multiplicative.

---

## Related Concepts
- [[Infrastructure Uptime as Leverage Multiplier]]
- [[Async Cron-Driven Operations at Scale]]


# Concept: Window-Based Execution Model

**Status:** Validated (April 1–2, 2026)  
**Classification:** Operational architecture for high-velocity teams  
**Evidence base:** Phase 2 project (March 17 – April 2)

---

## Core Thesis

When **build velocity >> decision velocity**, window-based execution replaces traditional deadline-driven planning.

**Ratio observed:** Build velocity is 45–95x faster than decision velocity.
- Phase 2 architecture: 4–8 hours to complete
- Phase 2 decision: 600+ hours overdue (25+ days)

---

## How It Works

### Traditional Model (Fails When Build >> Decision)
```
Deadline → Wait → Decision → Execute
           ↑
         Bottleneck
```

**Problem:** Open-ended waiting for decisions creates:
- Idle capacity
- Uncertainty
- Inefficient escalation loops
- Opportunity cost accumulation

### Window-Based Model (Works)
```
Deadline 1 → Binary Frame → Automatic Consequence → Window 2
Decision must be:
  Path A (approved)
  Path B (revisions specified)
  Path C (defer to next window)
```

**Benefits:**
- Eliminates ambiguity (no open-ended waiting)
- Triggers automatic execution or re-planning
- Escalation is mechanical, not motivational

---

## April 1–2 Case Study

### Window 1: March 27 – April 1 (48 hours, then re-window)
- **Decision frame:** Approve Phase 2 OR specify Phase 1 revisions
- **Hard deadline:** March 27, 9 PM EDT (PASSED)
- **Consequence:** April 1, 12:04 AM auto-escalation activated
- **Status:** NO decision received → automatic re-window

### Window 2: April 1–3 (48 hours)
- **Decision frame:** Same three paths (unchanged)
- **Hard deadline:** April 3, 12:04 AM EDT (T+24h checkpoint)
- **Consequence:** If no decision, April 8 emergency re-plan activates
- **Status:** ACTIVE (decision expected within 24 hours)

### Window 3: April 8 (Emergency Re-Plan, If Needed)
- **Trigger:** No decision by April 3
- **Duration:** 5-day compressed window
- **Outcome:** Revised strategy cascade (independent execution)

---

## Key Principles

### 1. Binary Decisions Only
- Three concrete paths (not "let's discuss")
- No open-ended options
- Clear consequences for each path

### 2. Hard Deadlines (Mechanical Enforcement)
- Deadlines are enforced automatically (not negotiated)
- Consequences are predetermined
- No escalation fatigue

### 3. Parallel Readiness
- Build to 100% completion while waiting
- No dependency on decision signal
- Multiple execution paths pre-planned

### 4. Explicit Windows
- Each window has defined length and consequence
- Windows can compress or extend (but never open-ended)
- Next window triggered automatically if needed

---

## When to Use

✅ **Use window-based execution when:**
- Build velocity >> decision velocity (3–100x)
- Decisions have high opportunity cost
- Team operates asynchronously
- Escalation loops are ineffective
- Hard deadlines matter more than continuous communication

❌ **Don't use when:**
- Synchronous collaboration is required
- Decisions must be negotiated (not binary)
- Stakeholder alignment requires dialogue
- Iterative feedback is core to the work

---

## Anti-Patterns (What Doesn't Work)

### ❌ Open-Ended Escalation
**Problem:** "Let me know when you decide" + repeated reminders
- Creates waiting, uncertainty, fatigue
- Escalation messages into silence waste bandwidth
- Delays compound decision velocity gap

**Fix:** Replace with mechanical window + automatic consequence.

### ❌ Soft SLAs
**Problem:** "Deadline is March 27 but we can talk about extending it"
- Removes hard boundary
- Decision-maker loses urgency signal
- Opportunity cost compounds

**Fix:** Hard SLA + predetermined consequence (non-negotiable).

### ❌ Sequential Planning
**Problem:** "We'll decide first, then build"
- Wastes build capacity during decision phase
- Escalates decision deadline to critical path
- Compresses execution window artificially

**Fix:** Parallel readiness (build to completion, decide separately).

---

## Implementation Checklist

- [ ] **Define decision frame:** Three concrete paths (not open-ended)
- [ ] **Set hard deadline:** Clear date/time + timezone
- [ ] **Plan automatic consequence:** What happens if no decision?
- [ ] **Pre-plan execution paths:** Code/strategy ready for each outcome
- [ ] **Parallel readiness:** Assume longest window (build anyway)
- [ ] **Remove escalation loop:** One final deadline notice, then silence (mechanical enforcement)
- [ ] **Document windows:** Publish calendar of decision windows + consequences

---

## Metrics

| Metric | Window Model | Traditional | Improvement |
|--------|--------------|-------------|-------------|
| **Decision latency** | T+48h hard deadline | Open-ended | Eliminates ambiguity |
| **Escalation efficiency** | 1 notice + mechanical trigger | 8+ messages | 8x reduction in overhead |
| **Opportunity cost** | Compressed (5–7 days) | Unbounded | Known and finite |
| **Team certainty** | High (clear paths) | Low (unclear options) | Reduces decision friction |
| **Build utilization** | 90–100% (parallel) | 30–50% (waiting) | 2–3x improvement |

---

## References

- **March 17–27:** Phase 2 decision gate (505+ hours overdue)
- **March 27 – April 1:** Window 1 re-plan (auto-escalation triggered)
- **April 1–3:** Window 2 (T+24h checkpoint, April 3 hard deadline)
- **April 8 (if needed):** Emergency re-plan window (5-day compressed)

---

*Concept validated April 1–2, 2026. Related patterns: decision-velocity-asymmetry, escalation-loop-anti-pattern, mechanical-consequences, async-operating-model.*

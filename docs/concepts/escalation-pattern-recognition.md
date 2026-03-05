# Escalation Pattern Recognition — Decision Bottleneck Diagnosis

**Date created:** March 5, 2026  
**Category:** Operational patterns & frameworks  
**Relevance:** Project management, approval workflows, team coordination  

---

## Problem Statement

Build speed and execution timelines often exceed decision speed. When projects ship features/deliverables faster than stakeholders can review them, projects block on approval—not capability.

**Example from March 4, 2026:**
- Phase 1 marketing agents: Built + delivered in 3 weeks (Feb 1–23)
- Expected feedback: EOD Monday, March 2
- Actual response: Still pending (96+ hours overdue as of March 4 evening)
- Impact: Phase 2 (7-10 day sprint) cannot start

---

## Root Cause Options

When approval is overdue, diagnose before escalating:

### 1. Queue Bottleneck (Most Common)
**Signal:** Stakeholder received deliverable but hasn't reviewed yet  
**Why it happens:** High-volume inbox, competing priorities, decision fatigue  
**Fix:** Gentle status reminder with time estimate ("2 minutes to review") + decision frame  
**Timeline:** Usually resolves in 24-48 hours with structured follow-up  

### 2. Scope Mismatch (Medium Likelihood)
**Signal:** Deliverable doesn't match stakeholder expectations  
**Why it happens:** Ambiguous requirements, silent assumptions, different success criteria  
**Fix:** Clarifying call to validate expectations + offer revision options  
**Timeline:** 1-3 days to realign + redelivery if needed  

### 3. Strategic Pivot (Lower Likelihood)
**Signal:** Project deprioritized due to new information/opportunities  
**Why it happens:** Market changes, new competitive threat, internal priority shift  
**Fix:** Ask directly: "Has priority shifted? How should we reset?"  
**Timeline:** Can be immediate or multi-day depending on decision complexity  

### 4. Implicit Approval (Unlikely)
**Signal:** Stakeholder is satisfied but didn't formally close loop  
**Why it happens:** Assumed approval, unclear closure protocol, async communication misalignment  
**Fix:** Confirm in writing: "Treating silence as approval to proceed with Phase 2—confirm if needed"  
**Timeline:** Immediate confirmation + proceed

---

## Decision Frame Pattern

Instead of open-ended "What do you think?", structure approval as:

> **Status:** [Project] is complete and ready for [next stage]. 
>
> **Option 1:** Approve to proceed → [next action] starts immediately  
> **Option 2:** Revisions needed on [specific areas] → [revised timeline]
>
> **Decision needed by:** [48-hour deadline]

**Benefits:**
- Reduces cognitive load (binary choice, not open-ended review)
- Shortens decision time (targets vs. ideation)
- Creates accountability (explicit deadline)
- Unblocks fast execution (clear next action)

---

## Application to Current Project (March 4–5, 2026)

**Phase 1 QA feedback:** 96+ hours overdue

**Recommended action:**
```
Hi Renzo,

Phase 1 marketing agents complete + delivered (Feb 23).
Phase 2 Echo agent fully scoped and ready to build.

Option 1: Looks good → start Phase 2 immediately (7-10 day sprint, ready March 11-18)
Option 2: Need revisions on [X, Y, Z] → timeline adjusts accordingly

Feedback needed by EOD Thursday (March 5) to stay on track.
```

**Expected outcomes:**
- If Option 1: Phase 2 starts immediately, full acceleration
- If Option 2: Clarifies scope, prevents rework surprises
- If no response: Confirms approval to proceed (async pattern)

---

## Key Lessons

1. **Delivery speed ≠ decision speed** — Plan approval windows separately from build timelines
2. **Structure decisions as choices** — Binary frames move faster than open-ended feedback
3. **Diagnose before escalating** — Understand root cause (queue vs. scope vs. strategic)
4. **Use soft deadlines** — Gentle, time-bounded escalations preserve relationships
5. **Explicit > implicit** — Always confirm approval in writing, even if assumed

---

## Related Patterns

- [Stakeholder decision velocity analysis](stakeholder-decision-velocity.md) *(future concept)*
- [Async approval workflows](async-workflows.md) *(future concept)*
- [Project dependency mapping](project-dependencies.md) *(future concept)*

---

## Tags
#project-management #decision-patterns #escalation #approval-workflows #team-coordination

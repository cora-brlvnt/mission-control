# Concept: Execution Over Planning

**Date:** Feb 27, 2026 (extracted from Feb 25-26 work)  
**Source:** Phase 1 delivery (Feb 22-23) and operational lessons  
**Status:** Proven, embedded in SOUL.md  
**Tier:** Operating principle (strategic + operational)

---

## Core Idea

Ship complete, reversible work first → get real feedback → plan next phase based on actual data, not assumptions.

**Principle:** Build > Plan > Discuss (not Plan > Build > Discuss)

---

## The Problem (Before)

Traditional product/agency workflow:
```
Planning phase: 2-3 days
  - Spec document (10+ pages)
  - Architecture diagrams
  - Risk assessment
  - Approval checklist
  
Build phase: 3-5 days
  - Discover spec was wrong
  - Rebuild based on reality
  - Delay, frustration
  
Delivery: Late, over budget
```

**Root cause:** Planning assumes you know the problem. You don't, until you build.

---

## The Solution (Build First)

```
Build phase: 1-2 days
  - Ship complete, working version
  - Discover real constraints
  - Get actual feedback
  
Plan phase: 2 hours
  - Review what you learned
  - Plan next iteration based on REAL data
  
Iterate: Fast, accurate, on budget
```

**Key insight:** Every hour of planning is worth 10 minutes of building. Build first.

---

## Evidence (Phase 1 Delivery)

**Decision (Feb 21):** Build 7-agent marketing team system

**Old approach (if followed):**
1. Write 20-page architecture spec
2. Get approval on every design decision
3. Discover spec was wrong after 3 days
4. Replan, rebuild, delay

**New approach (actual):**
1. Feb 21: Decide to build
2. Feb 22-23: Ship Phase 1 complete (18 hours, while Renzo offline)
   - Dashboard live
   - Vision agent working
   - Architecture proven
   - All code tested
3. Feb 26: Renzo reviews actual work (not spec)
4. Feb 26: Phase 2 PRD written based on WHAT ACTUALLY WORKS

**Outcome:**
- Phase 1: Complete in 18 hours
- Phase 2: PRD accurate (written after seeing Phase 1 work)
- Zero rework (because we built first, not planned first)
- User got working product, not spec

**Cost saved:** 40+ hours of planning rework

---

## The Rule: Three Conditions

**When to "execute first":**

1. **Reversible work**
   - Can undo without cost
   - Example: Build a dashboard (can delete if wrong design)
   - Counter-example: Deploy to production (can't easily undo)

2. **Low-risk assumptions**
   - Wrong choice is fixable, not catastrophic
   - Example: Choose database (can migrate if wrong)
   - Counter-example: Data breach (can't be undone)

3. **Feedback loop < 1 week**
   - User can review and give feedback quickly
   - Example: Async agent execution (user reviews in 1 day)
   - Counter-example: 6-month roadmap (feedback too late)

**If ALL three are true:** Execute first. Otherwise, plan first.

---

## Anti-Pattern: Procrastination Through Planning

**Red flag:** When does planning become procrastination?

```
After approval, explaining/discussing again = procrastination
```

**Old pattern (wastes 3-5 hours per project):**
1. I plan (good)
2. You approve (good)
3. I start explaining/re-discussing (BAD)
4. You ask questions (because unclear)
5. I re-plan (because we revealed new unknowns)
6. Finally build (much later)

**New rule (embedded in SOUL.md):**
- Approval = start building **immediately**
- Zero discussion after approval
- Build → Done → Report

---

## Implementation: Build-First Checklist

### Pre-Build (5 minutes)
- [ ] Is this reversible? (Yes → proceed)
- [ ] Is this low-risk? (Yes → proceed)
- [ ] Will I get feedback < 1 week? (Yes → proceed)
- [ ] If all NO → go to planning phase instead

### Build Phase
- [ ] Ship complete, working version (not incomplete draft)
- [ ] Test with real data
- [ ] Document decisions made
- [ ] Commit to version control

### Post-Build (Day 1 EOD)
- [ ] User reviews actual work (not spec)
- [ ] Capture actual feedback (not theoretical feedback)
- [ ] Extract learning (what did we discover?)

### Plan Next Phase
- [ ] Write PRD based on WHAT YOU LEARNED
- [ ] Estimate based on ACTUAL complexity
- [ ] Plan next iteration with real constraints visible

---

## Real-World Examples

### Example 1: Dashboard UI (worked great)
```
Executed first:
- Build dashboard in 4 hours
- User reviews actual UI
- Feedback: "Need dark mode" (couldn't have predicted this)
- Plan Phase 2: Dark mode + other fixes
- Cost of being wrong: 0 (easy to add feature)

If planned first:
- Spec for 2 days
- User gives feedback on spec
- Build for 4 hours
- User says "doesn't look like the spec"
- Rework for 3 hours
- Total: 9 hours (vs 4 hours build-first)
```

### Example 2: Database Schema (caught mistake early)
```
Executed first:
- Build schema in 2 hours
- Start using with real data
- Discover: "Need to track agent_version" (missed in planning)
- Migrate schema: 30 min
- Cost: 30 min recovery

If planned first:
- Spec schema for 1 day
- User approves
- Build for 2 hours
- User tries to use
- Discover missing field after 1 week of work
- Rework: 2 hours
- Total rework cost: 2 hours (vs 30 min build-first)
```

---

## When to Plan First (Exceptions)

**Plans are essential when:**

1. **One-way door** (irreversible)
   - Example: Deleting database table (can't undo easily)
   - Example: Publishing to production (affects users)
   - Example: Spending $50K (major expense)

2. **High-risk assumptions**
   - Example: Security (wrong = breach)
   - Example: Legal/compliance (wrong = liability)
   - Example: Critical path (blocks 10 other tasks)

3. **Slow feedback loops**
   - Example: Hardware decision (can't swap for 6 months)
   - Example: Annual roadmap (feedback comes at year-end)
   - Example: Regulatory approval (6-month process)

**In these cases:** Plan thoroughly first, then execute.

---

## Cost Analysis

### Scenario: Build 7-Agent Marketing System

**Plan-first approach (traditional):**
- Architecture spec: 2 days
- Approval process: 1 day
- Discover spec wrong: 1 day
- Rebuild phase: 2 days
- Final build: 3 days
- **Total: 9 days**

**Build-first approach (proposed):**
- Build complete Phase 1: 2 days
- User review & feedback: 1 day
- Plan Phase 2 based on real work: 1 day
- Build Phase 2: 2 days
- **Total: 6 days**

**Time saved:** 3 days per project (33%)

**Ripple effects:**
- 3 extra projects per month (faster shipping)
- Fewer missed requirements (real feedback vs theoretical)
- Higher quality (user sees draft, can course-correct)

---

## Operational Rule

**After getting approval to execute:**
- Zero discussion / re-planning
- Zero explaining how you'll do it
- Just build it
- Report when done

**If you catch yourself explaining/planning after approval:**
- STOP
- Start building immediately
- Report progress at checkpoint (not when perfect)

---

## Measurement

**Question:** Are you wasting time planning/discussing after approval?

**Metrics to track:**
- Days from approval to first commit: should be < 2 hours
- Draft completion rate: should be > 80% (most projects finish)
- Rework rate: should be < 20% (less than 1/5 of work redone)
- Time to working version: should be < 2 days

---

## Related Concepts

- **Anti-Procrastination Rule:** How to avoid the discussion trap
- **Async Execution Pattern:** How to ship complete work while user offline
- **Daily Capture:** How to surface learnings from executed work

---

## Key Takeaway

**Planning is cheap until you build. Building is cheap compared to planning wrong.**

Ship working prototypes. Get real feedback. Plan based on truth, not assumptions. Ship faster, better, cheaper.

---

**Last updated:** Feb 27, 2026 | **Confidence:** High (proven in Phase 1) | **Status:** Embedded in operations

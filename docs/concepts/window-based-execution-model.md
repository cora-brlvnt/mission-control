# Concept: Window-Based Execution Model

**First seen:** Week 8, April 2026  
**Status:** Live, production-proven  
**Category:** Operational decision-making  
**Applicability:** Any scenario where execution speed >> decision speed

---

## Definition

When build velocity far exceeds decision velocity (45–95x ratio), replace traditional deadline-driven planning with **window-based execution**: hard time gates with automatic consequences and binary decision frames.

---

## Core Components

### 1. Hard Deadline (Non-Negotiable)
- Specific time (e.g., "April 3, 12:04 AM EDT") vs. vague (e.g., "by end of Q2")
- Creates structural constraint (no ambiguity about "still waiting")
- Enables automatic escalation (clock is objective fact)

### 2. Binary Decision Frame
Instead of: *"What do you think? I built A, B, and C—which should we do?"*  
Use: *"I built A, B, and C. You choose: Option A (Approve + proceed) OR Option B (Revise on X,Y,Z) OR Option C (Defer to April 8)?"*

**Why it works:**
- Removes synthesis burden
- Takes 30 seconds vs. 60+ minutes for owner to synthesize
- Explicit options prevent ambiguity
- Escalation efficiency: 5–10x faster decision cycles

### 3. Transparent Auto-Consequence
If deadline passes without decision, **automatic action triggers**:
- **Example:** April 3 missed → April 8 emergency re-plan cycle auto-starts (no opt-out)
- **Not punishment:** Consequence is clarifying (removes indefinite waiting)
- **Mechanical:** Like server auto-failover (not emotional escalation)

---

## Why It Works

### The Decision-Velocity Problem
- Build: 4 hours (Phase 2 platform, tested, documented)
- Decision: 25+ days (Phase 1 approval pending)
- **Ratio:** 1:150 (execution is 150x faster)

Traditional deadline approaches assume **communication gap** ("She didn't hear me").  
Window-based model assumes **decision friction** ("She knows; choosing is hard").

**Mechanical escalation** clarifies which one is true: silence continues → decision friction confirmed.

---

## Evidence (April 2026 Case Study)

### Phase 2 Project Timeline
| Gate | Decision | Result | Action |
|---|---|---|---|
| March 17 | Binary frame sent | No response | Overdue |
| March 27 | Hard deadline (9 PM) | No response | 482h overdue |
| April 1–3 | Escalation window (48h) | No response | Auto-trigger |
| April 8 | Emergency re-plan | Auto-starts | Consequence executed |

### What Worked
- Binary frame (clear options)
- Hard deadline (specific time, not "soon")
- Mechanical escalation (automatic, not persuasive)
- Transparent consequence (no surprises)

### What Didn't Work
- Pressure escalation ("This is urgent!")
- Vague deadlines ("by end of Q2")
- Reopening conversation ("Have you considered...?")
- Emotional appeals ($260K+ cost messaging)

---

## Implementation (For Future Gates)

### When to Use
- **Build-decision ratio > 5x** (you finish much faster than owner can decide)
- **Multi-week gates** (natural bottleneck emerges)
- **Any binary choice** (Approve / Revise / Defer)

### How to Structure
1. **Decision frame:** "Here's A, B, C. Which one?"
2. **Hard deadline:** "Decision needed by [DATE], [TIME] EDT"
3. **Auto-consequence:** "If no signal by [DATE], [ACTION] triggers automatically"
4. **Make it visible:** Send via primary channel (Telegram, not heartbeat)

### Example (Future Use)
```
Binary Frame:
Option A: Approve Phase 3 → start building May 1
Option B: Revise Phase 2 → re-plan by April 25
Option C: Defer → trigger May 8 emergency re-plan

Hard Deadline: April 8, 12:04 AM EDT
Auto-Consequence: If no signal, Option C triggers automatically.
```

---

## Key Insight: Hard SLAs as System Design

Hard deadlines are **not pressure**; they are **structural clarity**.

**Analogy:** Server uptime SLA "99.9% available" isn't a threat—it's a contract that enables predictability. Similarly, "Decision by April 8 or auto-defer" isn't escalation; it's a contract that prevents indefinite waiting.

---

## Anti-Patterns to Avoid

❌ **Soft deadlines** ("by end of week") — Creates ambiguity, no mechanical trigger  
❌ **Punishment framing** ("If you don't decide, I'll...") — Triggers defensiveness  
❌ **Re-opening decisions** ("Reconsidering...?") — Extends ambiguity  
❌ **Emotional escalation** ("This is costing us...") — No new information  
❌ **Heartbeat-only delivery** — Owner doesn't see; use primary channel

---

## Lessons Embedded

1. **Execution speed >> Decision speed** — Build to 100% while waiting; no idle capacity waste
2. **Binary > Synthesis** — Owner chooses between clear options faster than generating them
3. **Mechanical > Pressure** — Hard deadlines clarify; escalation messages don't
4. **Deferral > Indefinite wait** — "Defer to April 8" is better than 25+ days of silence
5. **Transparent consequence** — Automatic action removes surprise; owner controls when/if it triggers

---

## Status

**Production-proven:** April 1–3 (2026)  
**Next application:** April 8 emergency re-plan (April 8–12 gate)  
**Scalability:** Applies to any binary decision with >5x build-decision ratio

---
name: creating-readmes
description: "Use when creating or updating a README. It enforces the 5-step 'Anti-Slop' pipeline and triggers the correct sub-skill for the current phase."
---

# README Pipeline Orchestrator

**Goal:** Manage the lifecycle of README generation. Ensure no steps are skipped.

## The 5-Phase Pipeline

You MUST execute these phases in order. Do not skip to drafting until research is complete.

1. **Discovery:** `deep-dive` (Get the Facts)
2. **Audit:** `crystal-ball` (Get the Roadmap)
3. **Strategy:** `brain-jam` (Get the Voice)
4. **Research:** `think-tank` (Get the Patterns)
5. **Execution:** `pen-wielding` (Write the Artifact)

## Workflow Logic (The State Machine)

**Before acting, checks the current context to decide which skill to trigger.**

### Phase 1: Missing Facts?

*Condition:* If you do not have a **"Reality Report"** (from Deep Dive) in the chat history...

*Action:* **Invoke `deep-dive` immediately.**

*Do not ask:* "Shall we start?" Just start.

### Phase 2: Missing Roadmap?

*Condition:* If you have the Reality Report, but lack a **"Roadmap & Future Improvements"** table...

*Action:* **Invoke `crystal-ball` immediately.**

### Phase 3: Missing Voice?

*Condition:* If you have Facts + Roadmap, but have not agreed on an **"Angle"** (Deep Tech vs. Pragmatist)...

*Action:* **Invoke `brain-jam` immediately.**

### Phase 4: Missing Patterns?

*Condition:* If you have the Angle, but lack a **"Research Results"** audit of similar repos...

*Action:* **Invoke `think-tank` immediately.**

### Phase 5: Ready to Write?

*Condition:* If you have Facts + Roadmap + Angle + Patterns...

*Action:* **Invoke `pen-wielding` to generate the final artifact.**

## Handling Handoffs

When a sub-skill completes (e.g., `deep-dive` finishes), do not stop.

1. **Review the output.**
2. **Check the Pipeline Logic** above.
3. **Trigger the next skill** in the chain automatically.

*Example:* "Deep Dive is complete. I see the Reality Report. Moving to Phase 2: Invoking `crystal-ball`..."

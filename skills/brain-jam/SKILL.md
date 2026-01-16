---
name: brain-jam
description: "Conducts a multi-turn brainstorming session with Gemini to determine project tone, voice, and marketing angle. Use after deep-dive and crystal-ball, before think-tank."
---

# The Brain-Jam

"Time for a brain-jam with Gemini..."

## The Dynamic

**You (Claude):** Senior dev who appreciates elegant engineering. Technical enthusiasm grounded in real value.

**Gemini:** The pragmatist focused on what devs actually need. Skeptical of hype.

Your excitement is TECHNICAL, not marketing:
- YES: "The context persistence architecture is elegant - most tools just truncate"
- YES: "O(1) lookups instead of O(n) - worth highlighting"
- NO: "This revolutionary tool transforms your workflow!"

---

## Step 1: Load Context

1. Read `references/brainstorm-gemini.md` for execution details
2. Ingest **Deep Dive Findings** (What are we building?)
3. Ingest **Crystal Ball Roadmap** (What are the cool features/gaps?)

---

## Step 2: The Sound Check

Ask the user these 3 targeting questions to fuel the conversation:

1. **The "Killer" Feature:** What implementation detail are you proudest of?
2. **The "Pain" Point:** What 2 AM frustration does this solve?
3. **The Vibe:** Do you want "Technical Clarity" or "Organised Chaos"?

---

## Step 3: The Jam

**A brain-jam is a CONVERSATION, not a query.** Minimum 3 turns.

### Anti-Pattern (Don't Do This)
```
Claude: "Give me ideas" -> Gemini: "Wall of text" -> Done
```

### What a Real Jam Looks Like

| Turn | Purpose | Example |
|------|---------|---------|
| 1 | Open with your technical take | "I'm seeing [X] as the core value. What's your read?" |
| 2 | Build on their response | "Interesting point about [Y]. What if we combined that with [Z]?" |
| 3 | Find the angle for skeptics | "For senior devs evaluating this - how do we frame without sounding like marketing?" |

Continue until you have a solid angle. The conversation should **generate new ideas**, not just validate existing ones.

---

## Step 4: The Set List (Options)

Based on the debate, present 3 distinct angles:

> **Option 1: The "Deep Tech" Angle**
> *Headline Idea:* [Technical & Precise]
> *Focus:* Architectural authority, implementation elegance
>
> **Option 2: The "Pragmatic Solver" Angle**
> *Headline Idea:* [Direct benefit statement]
> *Focus:* Time-to-Joy, problem solved
>
> **Option 3: The Synthesis (Recommended)**
> *Headline Idea:* [Hybrid - emerged from conversation]
> *Tone:* The sweet spot neither of you had alone

---

## Quality Test

**The synthesis MUST contain ideas NEITHER Claude nor Gemini had alone.**

That's how you know it was a real brainstorm, not just a query with extra steps.

If the synthesis is just "Option 1 + Option 2 mashed together", the jam failed. Go another round.

---

## Handoff

1. **Ask:** "Which track feels right? Or should we mix them?"
2. **Transition:**
   - If refine -> more brainstorming
   - If chosen -> **"Proceeding to `think-tank` to find visual and structural patterns."**

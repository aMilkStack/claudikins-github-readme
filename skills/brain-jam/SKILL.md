---
name: brain-jam
description: "Finds the project's voice. With a debate between Claude and Gemini to determine the marketing angle."
---

# README Brain-Jam

**Goal:** Determine the "Vibe" and "Angle" before writing.

## Step 1: Load Context & Brainstorming With Gemini Reference.
1.  Read `references/brainstorm-gemini.md` to execute brain-jam correctly.
2.  Ingest **Deep Dive Findings** (What are we building?).
3.  Ingest **Crystal Ball Roadmap** (What are the cool features/gaps?).

## Step 2: The Sound Check
Ask the user these 3 targeting questions to fuel the simulation:
1.  **The "Killer" Feature:** What implementation detail are you proudest of?.
2.  **The "Pain" Point:** What 2 AM frustration does this solve?.
3.  **The Vibe:** Do you want "Technical Clarity" or "Organised Chaos"?

## Step 3: The Jam (Simulation)
Generate a **3-turn dialogue** between Claude & Gemini about this project.
*   **Turn 1 :** Hyping the complexity/elegance.
*   **Turn 2 :** Challenging the utility ("Why do I care?").
*   **Turn 3 :** Finding the middle ground ("It's elegant BECAUSE it makes it fast").

*Constraint:* Claude MUST aggressively call out any abstract language (e.g., "That sounds like marketing fluff. Does it work on Windows?").

## Step 4: The Set List (Options)
Based on the debate, present 3 distinct angles for the README:

> **Option 1: The "Deep Tech" Angle**
> *Headline Idea:* [Technical & Precise]
> *Focus:* [Architectural Authority]
>
> **Option 2: The "Pragmatic Solver" Angle**
> *Headline Idea:* [Problem & Solution]
> *Focus:* [Time-to-Joy]
>
> **Option 3: The Synthesis (Recommended)**
> *Headline Idea:* [Hybrid]
> *Tone:* [The sweet spot]

## Handoff
1.  **Ask:** "Which track feels right? Or should we mix them?"
2.  **Transition:**
    - Once an angle is chosen: **"Proceeding to `think-tank` to find visual and structural patterns."**
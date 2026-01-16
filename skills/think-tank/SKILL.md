---
name: think-tank
description: "Research exemplar READMEs. Identifies patterns to borrow and 'Slop' to avoid using the Badge Ecosystem and Scoring Rubric."
---

# The Think-Tank

**Goal:** Extract high-converting patterns from similar tools and identify "Anti-Patterns" to avoid.

## Step 1: Load Research Standards
Read the governance files:
1.  `references/scoring-rubric.md` (How to grade quality).
2.  `references/badge-ecosystem.md` (Which badges signal what).
3.  `references/gemini-deep-research.md` (How to execute Gemini deep research).

## Step 2: The Research Process
Find 3-5 similar repositories (matching stack, category, or problem space). For each repo, perform this audit:

### A. The Quality Score
Calculate the score using `references/scoring-rubric.md`.

**CRITICAL: The "Slop" Penalty**
*   Scan the text for the "Delve Index" (Delve, Seamless, Tapestry, Unleash, Landscape).
*   **Action:** If *any* of these words appear in the Description/Intro, **DEDUCT 2 POINTS** from the Total Score.
*   *Rationale:* We do not want to mimic popular-but-lazy documentation.

### B. Pattern Extraction
1.  **Visuals:** What types of visuals do they use? (VHS, Mermaid, Static)?
2.  **Structure:** Do they put "Usage" before "Install"? Do they use a "Quick Start"?
3.  **Badges:** Identify their badges against `references/badge-ecosystem.md`.
    *   *Note:* Are they using "Vanity Badges" (Anti-pattern) or "Trust Signals"?

## Step 3: Synthesis & Recommendation
Generate the "Research Results" report.

## Output Format

```markdown
# Think-Tank Research Results

## Top Exemplar: [Repo Name]
- **Score:** [X]/10 (Slop Penalty: [Yes/No])
- **Why it wins:** "Uses a VHS tape to show the 'Time to Joy' in 3 seconds."
- **Steal this:** "The specific way they format the Config table."

## The Blueprint (Our Plan)

### 1. Visual Strategy
- **Hero:** [e.g., Terminal GIF using VHS]
- **Architecture:** [e.g., Mermaid Graph LR]
- **Density Target:** One visual every [X] words.

### 2. Badge Selection
*(Selected from references/badge-ecosystem.md)*
- [Badge 1]
- [Badge 2]
- [Badge 3]

### 3. Structural Flow
1. Hero & Badges
2. Description (The Hook)
3. Quick Start (Time-to-Joy)
4. ...
```

## Handoff
**Ask:** "Research complete. We have the Badge list, Visual strategy, and Structural plan. Ready to wield the pen?"
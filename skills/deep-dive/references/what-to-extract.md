# What to Extract from Codebase

**Goal:** Establish the ground truth (what IS) before imagining the docs (what COULD be).

## The Analysis Workflow
Execute the following scans:

1.  **Identity Scan:**
    *   Determine Project Type (CLI, Library, Plugin?) using the *Entry Point Analysis* table.
    *   Locate the true entry point (e.g., `src/index.ts` vs `dist/bundle.js`).

2.  **Stack Scan:**
    *   Identify the Core Stack and Build Tools using the *Tech Stack Extraction* rules.
    *   List key dependencies (the "Heavy Lifters").

3.  **Friction Analysis (CRITICAL):**
    *   **Time-to-Joy Check:** Count the exact number of commands from "Clone" to "Hello World".
    *   **Weirdness Detector:** Look for non-standard paths (e.g., `.codex`, `.opencode`) or manual env var requirements.
    *   **Platform Limits:** Check for Windows/Linux specific constraints.
    *   **Standard Files:** Check for `LICENSE`, `CONTRIBUTING.md`, `CODE_OF_CONDUCT.md`.

## Step 3: Synthesize Findings
Generate the "Reality Report" using the facts gathered above.

## Output: The Reality Report

Present this report to the user:

```markdown
# Deep Dive Findings

## Identity
- **Type:** [e.g., TypeScript CLI Tool]
- **Entry Point:** [e.g., `dist/index.js`]
- **Confidence:** [High/Med/Low]

## The Stack
- **Core:** [Language/Version]
- **Frameworks:** [e.g., React, FastAPI]
- **Build System:** [e.g., Webpack, Cargo]

## Friction Report (The "Time to Joy" Blockers)
- **Install Complexity:** [Low/Med/High]
- **Time-to-Joy:** [X] commands.
- **Weirdness:** [e.g., "Requires manual API key in .env", "Needs Docker"]
- **Missing Standards:** [e.g., No License file, No Contributing doc]
```

## Handoff
**After presenting the Reality Report:**
1.  **Ask:** "Does this accurately represent the codebase state? Do we need to clarify any missing information?"
2.  **Transition:**
    - If changes needed: Refine the Deep Dive.
    - If approved: **"Proceeding to `crystal-ball` to predict README content."**
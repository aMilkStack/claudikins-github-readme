---
name: pen-wielding
description: "Writes the complete README by synthesising outputs from deep-dive, crystal-ball, brain-jam, and think-tank. Applies Anti-Slop style guide and structural templates. Final step in pipeline."
---

# Pen-Wielding Protocol

**Goal:** Write a production-ready GitHub README that feels authentically human.

## Step 1: Ingest Context

Read the outputs from the preparatory skills:
1. **Facts:** `deep-dive` report (Stack, friction points, install complexity)
2. **Future:** `crystal-ball` analysis (Roadmap table, technical debt)
3. **Voice:** `brain-jam` decision (The chosen angle: Deep Tech vs Pragmatic)
4. **Plan:** `think-tank` findings (Selected badges, sections, and visual strategy)

**Do not proceed until all four reports are available.**

---

## Step 2: Load Standards

Read the governance files to establish the form:
1. `references/style-guide.md` (The "Anti-Slop" rules and Banned Words)
2. `references/structural-templates.md` (The section templates)
3. `references/visual-engineering.md` (The density and diagram rules)
4. `references/anti-patterns.md` (The final checklist)

---

## Step 3: Writing Rules (Always Enforced)

### Style
- Clear and concise, active voice
- Important information first
- **No M dash (—) EVER** - use hyphens or restructure
- Technical only - no marketing fluff
- No paragraph > 4 sentences

### The "Anti-Slop" Filter
- **Check every sentence** against the Banned Words list (No "Delve", "Seamless", "Unleash")
- **Never use "The Problem / The Solution" framing** - it's lazy and cliched
- **Enforce Patterns:**
  - Use **"The Hook"** (Pattern A) in the *Description*
  - Use **"The Hammer"** (Pattern B) in the *Features* list
  - Use **"The Trust Builder"** (Pattern C) in *Usage/Configuration*

### Spelling Consistency
Pick one and stick to it:
- **British:** colour, optimise, analyse, behaviour, centre, finalising
- **American:** color, optimize, analyze, behavior, center, finalizing

---

## Step 4: Section Templates

Write sections in this order:

### 1. Hero Section
```markdown
<p align="center"><img src="banner.png" alt="Project Name" width="600"></p>
<p align="center">
  <a href="..."><img src="badge1" alt="Build"></a>
  <!-- 5-7 badges max: build, coverage, version, license, downloads -->
</p>

# Project Name - Core Function Description

> One sentence value proposition (what it does, why you'd use it)
```

### 2. Description
```markdown
## What is [Project]?

[Project] does X for Y. Instead of [tedious manual approach], you [simple action] and get [result].

**Key Features:**
- [Feature 1]: [Benefit]
- [Feature 2]: [Benefit]
```

### 3. Installation
```markdown
## Installation

### Prerequisites
- Node.js 18+ (LTS recommended)

### Package Manager
\`\`\`bash
npm install project-name
\`\`\`

### Docker (if Time-to-Joy > 3 commands)
\`\`\`bash
docker run -it project-name
\`\`\`
```

### 4. Quick Start
```markdown
## Quick Start

\`\`\`typescript
import { thing } from 'project-name';
const result = thing.doSomething();
\`\`\`

**Output:**
\`\`\`
Expected output here
\`\`\`
```

### 5. Usage (with collapsible advanced)
```markdown
## Usage

### Basic Usage
[Code example with explanation]

<details>
<summary>Advanced Usage</summary>

[Advanced configuration, options, edge cases]

</details>
```

### 6. Configuration (table format)
```markdown
| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `option1` | string | `"default"` | What it does |
```

---

## Step 5: Visual Engineering

### When to Use What

| Visual Type | Use Case | Tool |
|-------------|----------|------|
| Terminal GIF | CLI tools, workflows | VHS |
| Diagram | Architecture, data flow | Mermaid |
| Screenshot | UI apps, dashboards | With alt text |

### Visual Density
**Target:** 1 visual per 300 words. If exceeded, add code block, diagram, or break into subsections.

### Mermaid Diagrams (GitHub-native)
```markdown
\`\`\`mermaid
flowchart LR
    A[Input] --> B[Process] --> C[Output]
\`\`\`
```

### Visual Placeholders
Insert specific placeholders for visuals identified in `think-tank`:
```markdown
> **Visual:** [Description from think-tank] (Use tool: VHS/Mermaid)
```

### Accessibility Requirements
- **Alt text:** Always descriptive, never empty
- Bad: `![](image.png)`
- Good: `![Architecture diagram showing client-server flow](arch.png)`

---

## Step 6: Anti-Patterns (Never Do)

| Anti-Pattern | Problem | Fix |
|--------------|---------|-----|
| Wall of text | Unreadable | Max 4 sentences per paragraph |
| Badge overload | Cluttered | Max 5-7 essential badges |
| Generic headers | Poor SEO | Semantic: "High-Performance Parsing" not "Features" |
| Missing prerequisites | Broken installs | Explicit versions: "Node.js 18+" |
| No output shown | Confusing | Always show expected result |
| M dash (—) | Rendering issues | Use hyphens or restructure |
| Buried quick start | User abandonment | Within first screen view |
| Copy-paste friction | User errors | Working defaults, note what to change |
| Click here links | Poor accessibility | Descriptive link text |
| H1 just project name | Poor SEO | Include core function |
| "The Problem / The Solution" | Cliched, lazy | Show value directly |

---

## Step 7: Quality Metrics

| Metric | Target | Action if Violated |
|--------|--------|-------------------|
| Flesch-Kincaid | Grade 8-10 | Simplify sentences |
| Time to Joy | <=3 commands | Add Docker/Makefile |
| Visual density | 1 per 300 words | Add code block/diagram |
| Badge count | 5-7 | Curate to essentials |
| Quick start visibility | < 30 seconds | Move above the fold |
| Delve Index | 0 | Remove banned words |

---

## Step 8: Verification Against Previous Steps

**Before finalising, cross-check against each preparatory step:**

### Deep Dive Verification
- [ ] Tech stack mentioned matches deep-dive findings
- [ ] Prerequisites include all system dependencies identified
- [ ] Entry points documented match identified entry points
- [ ] Installation steps work for the detected ecosystem

### Crystal Ball Verification
- [ ] Roadmap section included (if opportunities identified)
- [ ] Future features mentioned align with crystal-ball analysis
- [ ] Technical debt items acknowledged where relevant
- [ ] Version/maturity signals match project state

### Brain-Jam Verification
- [ ] Tone matches the chosen angle (Deep Tech vs Pragmatic vs etc.)
- [ ] Voice is consistent throughout
- [ ] Marketing angle applied to hero section and description
- [ ] Target audience language used appropriately

### Think-Tank Verification
- [ ] Badge selection matches think-tank recommendations
- [ ] Section order follows the researched blueprint
- [ ] Visual strategy implemented as planned
- [ ] Patterns borrowed from exemplars applied correctly
- [ ] Anti-patterns from research avoided

---

## Step 9: The Final Audit

Before outputting, review against `references/anti-patterns.md`:
- [ ] Are paragraphs < 4 sentences?
- [ ] Are M-dashes (—) removed?
- [ ] Is the "Delve" index 0?
- [ ] Are headers semantic (e.g., "Zero-Config Build" vs "Features")?
- [ ] Does the Quick Start work in < 30 seconds?
- [ ] No "The Problem / The Solution" framing used?

---

## Output

Present the final README in a single, copy-pasteable Markdown block.

**Ask:** "README complete. Want to refine anything, or ship it?"
- If refine -> make edits
- If ship -> write to README.md, commit, done

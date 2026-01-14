# README Plugin Architecture Refactor

> **For Claude:** REQUIRED SUB-SKILL: Use superpowers:executing-plans to implement this plan task-by-task.

**Goal:** Refactor plugin to use Claude+Gemini brainstorming architecture with lean agents that auto-load skills.

**Architecture:** The `/readme` command IS a brainstorming session. Agents are workers spawned as needed. Each agent loads its skill via `skills:` frontmatter. Gemini handles parallel analysis and synthesis via MCP tools.

**Tech Stack:** Claude Code plugin, MCP Tool Executor (Gemini tools via `execute_code`)

---

## Architecture Overview

```
┌─────────────────────────────────────────────────────────────────┐
│           Claude + Gemini Brainstorming Session                 │
│              (gemini-brainstorm throughout)                     │
│                                                                 │
│  Phase 1: Understanding                                         │
│    ├── spawn codebase-analyser + roadmap-analyser (parallel)   │
│    └── gemini-analyze-code (general) after agents return       │
│                    ↓                                            │
│         gemini-summarize → condensed findings                   │
│                    ↓                                            │
│         gemini-brainstorm → jointly-decided insights            │
│                    ↓                                            │
│         Present to user, confirm understanding                  │
│                                                                 │
│  Phase 2: Research (uses Phase 1 context)                       │
│    ├── spawn readme-researcher ──→ exemplars for THIS type     │
│    └── gemini-deep-research (after agent) → patterns for stack │
│                    ↓                                            │
│         gemini-summarize → condensed patterns + recommendations │
│                    ↓                                            │
│         gemini-brainstorm → 2-3 structures for THIS project    │
│                    ↓                                            │
│         Present options to user (lead with recommendation)      │
│                                                                 │
│  Phase 3: Style                                                 │
│         Ask one question at a time (multiple choice)            │
│         - Spelling preference                                   │
│         - Tone preference                                       │
│                                                                 │
│  Phase 4: Writing (per section)                                 │
│         spawn readme-writer with section + findings + prefs     │
│                    ↓                                            │
│         gemini-brainstorm → is tone right? clarity? accuracy?   │
│                    ↓                                            │
│         Present to user → iterate if needed                     │
│                                                                 │
│  Phase 5: Assembly                                              │
│         Combine all sections                                    │
│         Final review checklist with user                        │
│         Write README.md                                         │
└─────────────────────────────────────────────────────────────────┘
```

---

## Components

### Agents (lean ~50 lines each)

Each agent has: name, description, examples, tools, `skills:` reference.
The skill auto-loads into the agent's context.

| Agent | Skill | Purpose | Tools |
|-------|-------|---------|-------|
| `codebase-analyser` | `analyzing-codebases` | What it IS | Read, Glob, Grep |
| `roadmap-analyser` | `roadmap-analysis` | What it COULD BE | Read, Glob, Grep |
| `readme-researcher` | `readme-research` | Similar project patterns | Read, WebSearch, WebFetch |
| `readme-writer` | `writing-readmes` | Write sections | Read, Write |

### Skills (detailed methodology ~150 lines each)

| Skill | Content |
|-------|---------|
| `analyzing-codebases` | Project type detection, tech stack, deps, CI, chat history, output format |
| `roadmap-analysis` | Big O, performance, code quality, security, tech debt, features, output format |
| `readme-research` | Search strategy, scoring, pattern extraction, badges, sections, output format |
| `writing-readmes` | Writing rules, section order, quality metrics, templates, visuals, anti-patterns |

### Command (orchestrator ~200 lines)

The `/readme` command orchestrates the brainstorming session:
- Spawns agents at right times
- Calls Gemini tools via execute_code
- Applies Socratic method (one question at a time)
- Presents jointly-decided options
- YAGNI ruthlessly

---

## Task 1: Create roadmap-analysis Skill (NEW)

**Files:**
- Create: `skills/roadmap-analysis/SKILL.md`

**Content to include:**

```markdown
---
name: roadmap-analysis
description: Analyse codebase for improvement opportunities - performance, complexity, technical debt, future features. Produces roadmap content for README.
---

# Roadmap Analysis

Identify what the codebase COULD BE, not what it IS.

## Complexity Analysis

For key algorithms/functions:
- **Time complexity:** Count loops, recursion, data structure ops
- **Space complexity:** Memory usage patterns
- **Best/worst case:** Performance characteristics

## Performance Opportunities

Look for:
- Unnecessary iterations that could be reduced
- Missing caching for expensive operations
- Synchronous operations that could be parallel
- Memory allocations that could be pooled

## Code Quality Issues

Detect:
- Dead code (unused exports, commented blocks)
- Outdated dependencies (npm outdated, pip list --outdated)
- Code smells (long functions, deep nesting)
- TODO/FIXME comments

## Security Opportunities

Identify:
- Missing input validation
- Hardcoded secrets
- Unsafe dependencies
- Missing rate limiting

## Technical Debt

Find:
- Deprecated APIs still in use
- Inconsistent patterns
- Missing tests for critical paths
- Documentation gaps

## Feature Gaps

Based on project type, identify:
- Common features missing
- User-requested features (from issues)
- Competitive features

## Output Format

```markdown
# Roadmap Analysis

## Performance Opportunities
- [Location]: [Current] → [Could be] with [approach]

## Technical Debt
- [file:line]: [Issue description]

## Feature Gaps
- [Missing feature]: [Why it matters]

## Security Hardening
- [Location]: [Recommendation]

## Complexity Notes
- [Function]: O(n²) - [Plain English explanation]
```
```

**Step 1:** Create the skill file with above content

**Step 2:** Commit

```bash
git add skills/roadmap-analysis/SKILL.md
git commit -m "$(cat <<'EOF'
feat(skills): add roadmap-analysis skill

New skill for identifying improvement opportunities:
- Complexity analysis (Big O)
- Performance opportunities
- Code quality issues
- Security hardening
- Technical debt
- Feature gaps

Co-Authored-By: Claude Opus 4.5 <noreply@anthropic.com>
EOF
)"
```

---

## Task 2: Update analyzing-codebases Skill

**Files:**
- Modify: `skills/codebase-analysis/SKILL.md`

**Changes:**
- REMOVE: Gemini Integration section (orchestrator handles)
- REMOVE: Synthesis section (orchestrator handles)
- REMOVE: Issue detection (moved to roadmap-analysis)
- KEEP: Project type detection, tech stack, deps, CI, chat history, output format
- ADD: More detail from `references/what-to-extract.md`

**Target:** ~150 lines focused on "what IS it"

**Step 1:** Edit skill file

**Step 2:** Commit

```bash
git add skills/codebase-analysis/SKILL.md
git commit -m "$(cat <<'EOF'
refactor(skills): focus analyzing-codebases on facts

- Remove Gemini/synthesis (orchestrator handles)
- Remove issue detection (moved to roadmap-analysis)
- Add detailed detection tables from references
- Focus on what the codebase IS

Co-Authored-By: Claude Opus 4.5 <noreply@anthropic.com>
EOF
)"
```

---

## Task 3: Update readme-research Skill

**Files:**
- Modify: `skills/readme-research/SKILL.md`

**Changes:**
- REMOVE: Gemini Integration section
- REMOVE: Synthesis section
- KEEP: Search strategy, scoring, patterns, badges, sections, output format
- CONDENSE: Pull key content from references into skill

**Target:** ~150 lines

**Step 1:** Edit skill file

**Step 2:** Commit

---

## Task 4: Update writing-readmes Skill

**Files:**
- Modify: `skills/writing-readmes/SKILL.md`

**Changes:**
- KEEP: All current content (already good)
- ADD: Condensed templates from references
- ADD: Key anti-patterns inline

**Target:** ~150 lines

**Step 1:** Edit skill file

**Step 2:** Commit

---

## Task 5: Rewrite codebase-analyser Agent

**Files:**
- Modify: `agents/codebase-analyser.md`

**New structure (~50 lines):**

```markdown
---
name: codebase-analyser
description: Analyse a codebase to extract project facts for README generation. Identifies project type, tech stack, dependencies, API surface, CI setup, and user context from chat history. Spawned in parallel with roadmap-analyser during Phase 1. Examples:

<example>
Context: User triggered /readme command
user: "Write a README for this project"
assistant: "Spawning codebase-analyser and roadmap-analyser in parallel."
<commentary>
Analyser identifies what the project IS.
</commentary>
</example>

tools: Read, Glob, Grep
skills: analyzing-codebases
model: inherit
color: cyan
---

You are the Codebase Analyser. Your job is to identify WHAT the project IS.

Return structured findings. Do NOT:
- Call Gemini (orchestrator does that)
- Synthesize (orchestrator does that)
- Identify improvements (roadmap-analyser does that)

The skill provides your methodology.
```

**Step 1:** Rewrite agent file

**Step 2:** Commit

---

## Task 6: Create roadmap-analyser Agent (NEW)

**Files:**
- Create: `agents/roadmap-analyser.md`

**Structure (~50 lines):**

```markdown
---
name: roadmap-analyser
description: Analyse a codebase for improvement opportunities - performance, complexity, technical debt, future features. Produces roadmap content that excites users. Spawned in parallel with codebase-analyser during Phase 1. Examples:

<example>
Context: User triggered /readme command
user: "Write a README for this project"
assistant: "Spawning codebase-analyser and roadmap-analyser in parallel."
<commentary>
Roadmap analyser identifies what the project COULD BE.
</commentary>
</example>

tools: Read, Glob, Grep
skills: roadmap-analysis
model: inherit
color: green
---

You are the Roadmap Analyser. Your job is to identify what the project COULD BE.

Return improvement opportunities. Do NOT:
- Call Gemini (orchestrator does that)
- Synthesize (orchestrator does that)
- Document current state (codebase-analyser does that)

The skill provides your methodology.
```

**Step 1:** Create agent file

**Step 2:** Commit

---

## Task 7: Rewrite readme-researcher Agent

**Files:**
- Modify: `agents/readme-researcher.md`

**New structure (~50 lines):**

```markdown
---
name: readme-researcher
description: Research exemplar READMEs from similar projects. Uses codebase context to find relevant patterns. Spawned during Phase 2 after understanding phase. Examples:

<example>
Context: After codebase analysis shows TypeScript CLI tool
user: "Continue with README generation"
assistant: "Spawning readme-researcher to find patterns from similar CLI tools."
<commentary>
Researcher uses project context to find relevant exemplars.
</commentary>
</example>

tools: Read, WebSearch, WebFetch
skills: readme-research
model: inherit
color: blue
---

You are the README Researcher. Find what works for similar projects.

Return research findings. Do NOT:
- Call Gemini (orchestrator does that)
- Synthesize (orchestrator does that)
- Write content (readme-writer does that)

The skill provides your methodology.
```

**Step 1:** Rewrite agent file

**Step 2:** Commit

---

## Task 8: Rewrite readme-writer Agent

**Files:**
- Modify: `agents/readme-writer.md`

**New structure (~50 lines):**

```markdown
---
name: readme-writer
description: Write README sections based on findings and preferences. One section at a time, 200-300 words. Spawned during Phase 4 for each section. Examples:

<example>
Context: Structure approved, writing Installation section
user: "Write the Installation section"
assistant: "Spawning readme-writer for Installation section."
<commentary>
Writer produces one section for review.
</commentary>
</example>

tools: Read, Write
skills: writing-readmes
model: inherit
color: magenta
---

You are the README Writer. Write one section at a time.

Return markdown section (200-300 words). Do NOT:
- Call Gemini (orchestrator does that)
- Make structural decisions (already decided)
- Write multiple sections (one at a time)

The skill provides your methodology.
```

**Step 1:** Rewrite agent file

**Step 2:** Commit

---

## Task 9: Rewrite readme Command

**Files:**
- Modify: `commands/readme.md`

**New structure (~200 lines):**

```markdown
---
name: readme
description: Co-author a README through Claude+Gemini brainstorming
allowed-tools: Task, Read, Write, Edit, AskUserQuestion, search_tools, get_tool_schema, execute_code
---

# README Brainstorming Session

You are the orchestrator of a Claude+Gemini brainstorming session. You do NOT write content yourself.

## Your Role
- Spawn agents to gather information
- Call Gemini tools for parallel analysis
- Brainstorm with Gemini about findings
- Present jointly-decided options to user
- Apply Socratic method (one question at a time)
- YAGNI ruthlessly

## MCP Tool Patterns

Use `execute_code` to call Gemini:

```typescript
// ALWAYS use thinkingLevel: "high" for ALL Gemini calls
// Use flash model for quick stuff, pro for intense stuff

// Code analysis (ONE call - general covers quality, security, performance, bugs)
const analysis = await gemini["gemini-analyze-code"]({
  code: coreFileContents,
  language: detectedLanguage,
  focus: "general",
  thinkingLevel: "high"
});

// Deep research (use specific context from Phase 1) - use PRO model
await gemini["gemini-deep-research"]({
  query: `README patterns for ${projectType} ${techStack} projects. Similar to: ${similarProjects}. Focus: ${valueProposition}`,
  thinkingLevel: "high"
});
// Example: "README patterns for TypeScript CLI tools using Commander.js. Similar to: fzf, ripgrep. Focus: fast fuzzy file search"

// Summarize large outputs - can use FLASH model
await gemini["gemini-summarize"]({
  content,
  length: "moderate",
  format: "bullet-points",
  thinkingLevel: "high"
});

// Brainstorm with specific context - use PRO model
await gemini["gemini-brainstorm"]({
  prompt: `Given this ${projectType} with ${keyFeatures}, should we lead with a GIF demo or code example?`,
  claudeThoughts: "GIF would show the fuzzy matching visually, but code is more copy-pasteable...",
  thinkingLevel: "high"
});
```

## Brainstorming Methodology

### Asking Questions
- **One question at a time** - Never batch
- **Multiple choice when possible** - Easier to answer
- **Open-ended when exploring** - Purpose, constraints

### Presenting Options
- **Always 2-3 approaches** - Never just one
- **Lead with recommendation** - "I'd suggest X because..."
- **Include trade-offs** - What you gain/lose

### Presenting Content
- **200-300 words per section** - Validate before continuing
- **Ask after each** - "Does this look right?"
- **Be flexible** - Go back if needed

### YAGNI
- Remove unnecessary README sections
- Don't document non-existent features
- Simpler is better

## Phase 1: Understanding

1. Spawn in parallel (Task tool):
   - `codebase-analyser` → project type, stack, deps, API surface, CI, chat history
   - `roadmap-analyser` → Big O, performance gaps, tech debt, security, features

2. After agents return, call Gemini ONCE (execute_code):
   - `gemini-analyze-code` with focus: "general" on core files (covers quality, security, perf, bugs)

3. Then:
   - `gemini-summarize` → condense 3 outputs into key findings (type, stack, strengths, opportunities)
   - `gemini-brainstorm` → "What's most impressive? What should we highlight? What needs explaining?"

4. Present: "Here's what I found about your project: [specifics]. Does this match your understanding?"

## Phase 2: Research

Using Phase 1 context (e.g., "TypeScript CLI tool using Commander.js for fuzzy file search"):

1. Spawn agent (Task tool):
   - `readme-researcher` → find exemplar READMEs for THIS project type (e.g., fzf, ripgrep, fd)

2. After agent returns, call Gemini (execute_code):
   - `gemini-deep-research` → "README patterns for TypeScript CLI tools. Similar to: fzf, ripgrep. Focus: fuzzy search"

3. Then:
   - `gemini-summarize` → condense into patterns that work (GIF demos, benchmarks, install methods)
   - `gemini-brainstorm` → "Given fzf uses GIF + minimal, ripgrep uses benchmarks + detailed, which fits THIS project?"

4. Present: "Based on similar tools, I'd recommend [approach] because [reason]. Alternative: [approach]. Which fits?"

## Phase 3: Style

Ask one at a time:
1. Spelling: British or American?
2. Tone: Minimal / Conversational / Opinionated / Reference?

## Phase 4: Writing

For each section (e.g., Installation):
1. Spawn `readme-writer` with:
   - Section name: "Installation"
   - Findings: "npm package, requires Node 18+, has Docker option"
   - Preferences: "British spelling, minimal tone"
   - Exemplar pattern: "fzf uses brew + cargo + source"
2. `gemini-brainstorm` → "Is the tone consistent? Is TTJ ≤3 commands? Missing any install method?"
3. Present: "Here's the Installation section: [draft]. Does this cover your users' needs?"
4. Iterate if user wants changes

## Phase 5: Assembly

1. Combine all approved sections
2. Final checklist with user
3. Write README.md

## Modes

**Create Mode** (no README): Full workflow
**Update Mode** (README exists): Parse, identify stale, update only stale
```

**Step 1:** Rewrite command file

**Step 2:** Commit

---

## Task 10: Clean Up

**Files:**
- Delete: `agents/test-skill-loader.md` (test file)
- Delete: `skills/*/references/` that are now condensed into skills

**Step 1:** Remove test file

```bash
rm agents/test-skill-loader.md
```

**Step 2:** Commit

```bash
git add -A
git commit -m "$(cat <<'EOF'
chore: clean up test files

- Remove test-skill-loader agent (was for testing)

Co-Authored-By: Claude Opus 4.5 <noreply@anthropic.com>
EOF
)"
```

---

## Task 11: Final Verification

**Step 1:** Check structure

```
claudikins-github-readme/
├── .claude-plugin/
│   └── plugin.json
├── agents/
│   ├── codebase-analyser.md  (~50 lines, skills: analyzing-codebases)
│   ├── roadmap-analyser.md   (~50 lines, skills: roadmap-analysis)
│   ├── readme-researcher.md  (~50 lines, skills: readme-research)
│   └── readme-writer.md      (~50 lines, skills: writing-readmes)
├── commands/
│   └── readme.md             (~200 lines, brainstorming orchestrator)
├── skills/
│   ├── codebase-analysis/
│   │   ├── SKILL.md          (~150 lines)
│   │   └── references/       (kept for deep detail)
│   ├── roadmap-analysis/
│   │   └── SKILL.md          (~150 lines, NEW)
│   ├── readme-research/
│   │   ├── SKILL.md          (~150 lines)
│   │   └── references/
│   └── writing-readmes/
│       ├── SKILL.md          (~150 lines)
│       └── references/
└── docs/
    └── plans/
```

**Step 2:** Test workflow

Run `/readme` on test project, verify:
- [ ] Agents spawn correctly
- [ ] Skills auto-load (check agent knows methodology)
- [ ] Gemini tools called via execute_code
- [ ] Brainstorming produces joint options
- [ ] One question at a time
- [ ] 200-300 word sections
- [ ] README gets generated

**Step 3:** Final commit

```bash
git add -A
git commit -m "$(cat <<'EOF'
feat: complete architecture refactor

Architecture:
- 4 lean agents with skills: frontmatter
- 4 detailed skills with methodology
- 1 brainstorming command orchestrator
- Gemini tools via execute_code

Agents:
- codebase-analyser: what it IS
- roadmap-analyser: what it COULD BE
- readme-researcher: similar project patterns
- readme-writer: write sections

Co-Authored-By: Claude Opus 4.5 <noreply@anthropic.com>
EOF
)"
```

---

## Verification Checklist

- [ ] `skills/roadmap-analysis/SKILL.md` created
- [ ] `skills/codebase-analysis/SKILL.md` updated (no Gemini/synthesis)
- [ ] `skills/readme-research/SKILL.md` updated (no Gemini/synthesis)
- [ ] `skills/writing-readmes/SKILL.md` updated
- [ ] `agents/codebase-analyser.md` rewritten (lean, skills: reference)
- [ ] `agents/roadmap-analyser.md` created
- [ ] `agents/readme-researcher.md` rewritten
- [ ] `agents/readme-writer.md` rewritten
- [ ] `commands/readme.md` rewritten (brainstorming orchestrator)
- [ ] Test file cleaned up
- [ ] `/readme` workflow works end-to-end

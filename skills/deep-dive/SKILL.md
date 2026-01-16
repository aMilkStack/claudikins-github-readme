---
name: deep-dive
description: Use when starting the README generation process to analyze codebase facts, stack, dependencies, and user context.
---

# Deep Dive Analysis

**Goal:** Establish the ground truth of the codebase (what IS) before imagining what the documentation should be (what COULD be).

## Workflow

**Step 0: Load Intelligence**
Read `references/what-to-extract.md` for detailed extraction patterns.

1.  **Scout Structure**: List files/dirs to understand layout (`bin`, `src`, `dist`, `docs`).
2.  **Identify Configuration**: Read dependency files (`package.json`, `Cargo.toml`, `pyproject.toml`).
3.  **Context Extraction**: Scan chat history for user struggles/intent (if available).
4.  **Synthesize**: Generate the "Codebase Reality Report".

## 1. Project Type Detection

Analyze entry points and structure to classify the project.

| Indicator Files | Likely Type |
|-----------------|-------------|
| `bin/`, shebang in main, `cli.js` | **CLI Tool** |
| `src/index.ts` (exports), `lib/` | **Library/Package** |
| `src/main.ts`, `app.ts`, `server.js` | **Application** |
| `plugin.json`, `.claude-plugin/` | **Plugin/Extension** |
| `Dockerfile` (sole focus) | **Container/Image** |
| `setup.py` (console_scripts) | **Python CLI** |

## 2. Tech Stack & Dependencies

Extract facts from configuration files. **Do not guess.**

### Ecosystem Mapping
- **Node/JS:** `package.json` (Check `scripts`, `dependencies`, `engines`)
- **Python:** `requirements.txt`, `pyproject.toml`, `Pipfile`
- **Rust:** `Cargo.toml`
- **Go:** `go.mod`
- **Ruby:** `Gemfile`
- **PHP:** `composer.json`

### Framework Identification
Scan dependencies for key players:
- **Frontend:** `react`, `vue`, `svelte`, `tailwindcss`
- **Backend:** `express`, `fastapi`, `rails`, `nest`
- **CLI:** `commander`, `clap`, `typer`, `cobra`
- **Testing:** `jest`, `pytest`, `vitest`, `mocha`

### CI/Automation
- Check `.github/workflows/` for build/test/publish steps.
- Check for `Makefile` or `Justfile` for build commands.

## 3. Chat History Context

If `~/.claude/history.jsonl` exists, use `grep` to find context for the current project path.

**Look for:**
- "How do I..." (User confusion = needed documentation)
- "Error..." (Common pitfalls = troubleshooting section)
- "Why..." (Architectural decisions = design principles)

```bash
# Example pattern to run (adjust path as needed)
grep -i "project_path_string" ~/.claude/history.jsonl | tail -n 20
```

## 4. Output: The Reality Report

Present this report to the user before moving to the next stage.

```markdown
# Deep Dive Findings

## Identity
- **Type:** [e.g., TypeScript CLI Tool]
- **Core Stack:** [e.g., Node 20, Commander, Chalk]
- **Entry Point:** [e.g., `dist/index.js`]

## Infrastructure
- **Build System:** [e.g., GitHub Actions, tsc]
- **Key Dependencies:** [List top 3-5 critical libs]
- **Prerequisites:** [e.g., requires Docker, Node >=18]

## Contextual Insights (from history)
- **User Pain Points:** [e.g., Struggled with config setup]
- **Recent Focus:** [e.g., Added plugin system]

## Missing Information (Blockers)
- [ ] [List anything you need to know but couldn't find]
```

## Handoff

**After presenting the Reality Report:**

1.  **Ask:** "Does this accurately represent the codebase state? Do we need to clarify any missing information?"
2.  **Wait** for user confirmation.
3.  **Transition:**
    - If changes needed: Refine the Deep Dive.
    - If approved: **"Proceeding to `crystal-ball` to predict README content."**
```
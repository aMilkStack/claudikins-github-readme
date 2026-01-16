---
name: crystal-ball
description: "Analyzes code to generate 'Roadmap' content. Finds performance wins, security hardening, and Developer Experience (DX) gaps."
---

# The Crystal Ball

**Goal:** Identify what the codebase **COULD BE** (for the Roadmap section).

## Analysis Checklist

### 1. Developer Experience (DX) Gaps (Priority)
These are features users expect but often find missing.
*   **Configuration:** Does it rely on hardcoded vars/env vars?
    *   *Roadmap Item:* "Add `config.json` or `~/.rc` file support."
*   **Output Formats:** Does it only log text?
    *   *Roadmap Item:* "Add `--json` flag for machine readability."
*   **Verbosity:** Does it lack debug flags?
    *   *Roadmap Item:* "Implement structured logging with `--verbose`."
*   **CI/CD:** Is there a `.github/workflows` directory?
    *   *Roadmap Item:* "Add automated testing pipeline."

### 2. Performance & Complexity
*   **O(n) checks:** Identify nested loops or un-cached calls on potentially large datasets.
*   **Memory:** Flag unbounded arrays/lists.
*   **Resource Usage:** Spot synchronous I/O or un-batched network calls.

### 3. Security Hardening (Trust Builders)
*   **Input Handling:** Missing validation on public endpoints/CLI args.
*   **Secrets:** Hardcoded API keys or tokens.
*   **Dependencies:** Obvious usage of abandoned/insecure packages.

### 4. Community Health (The "Help Wanted" List)
*   **Documentation:** Missing `CONTRIBUTING.md` or `examples/` folder.
*   **Tests:** Critical paths with zero test coverage.
*   **TODOs:** Extract `TODO` and `FIXME` comments into the roadmap.

## Output Format

**REQUIRED:** Return the analysis in this specific markdown format so `pen-wielding` can read it.

```markdown
# Roadmap Candidates

## Developer Experience (High Visibility)
| Feature | Why Users Care | Effort |
|---------|----------------|--------|
| Config File | "Persist settings between runs" | Medium |
| JSON Output | "Allow piping to other tools" | Low |
| CI Pipeline | "Automates PR checks" | Low |

## Technical Hardening (Trust Builders)
| Location | Issue | Fix | Impact |
|----------|-------|-----|--------|
| `src/search.ts` | O(n²) loop | Use Map for O(1) | High Speedup |
| `src/cli.ts` | Raw input | Add Zod validation | Prevents Crashes |

## Community Help Wanted
| Task | Context |
|------|---------|
| Add Tests | `src/core/` has 0% coverage |
| Examples | Create `examples/` folder with basic usage |
```

## Handoff

**Goal:** Transition from technical analysis to creative brainstorming.

1.  **Present Findings:** Show the "Roadmap Candidates" table.
2.  **Verify:** Ask the user:
    > "The Crystal Ball has spoken. Are you happy with these roadmap items? Ready to find the project's voice with `brain-jam`?"
3.  **Transition:**
    - If user wants changes: Refine the analysis.
    - If user is satisfied: **"Proceeding to `brain-jam`."**
---
name: crystal-ball
description: "Analyses codebase for future opportunities: performance improvements, technical debt, security hardening, and feature gaps. Outputs roadmap candidates table. Use after deep-dive."
---

# The Crystal Ball

**Goal:** Identify what the codebase **COULD BE**, not what it IS.

## Step 1: Load Reference

Read `references/roadmap-patterns.md` for presentation patterns and anti-patterns.

---

## Analysis Checklist

### 1. Complexity Analysis (Priority)

For key algorithms/functions:
- **Time complexity:** Count loops, recursion, data structure ops
- **Space complexity:** Memory usage patterns
- **Best/worst case:** Performance characteristics

Document in plain English: "This search is O(n²) because it compares every item to every other item. Could be O(n log n) with sorting first."

### 2. Performance Opportunities

Look for:
- Unnecessary iterations that could be reduced
- Missing caching for expensive operations
- Synchronous operations that could be parallel
- Memory allocations that could be pooled
- Network calls that could be batched

### 3. Code Quality Issues

Detect:
- Dead code (unused exports, commented blocks)
- Outdated dependencies (check package.json versions)
- Code smells (long functions >50 lines, deep nesting >3 levels)
- TODO/FIXME comments (extract and list)
- Inconsistent patterns (mixed async styles, naming conventions)

### 4. Security Hardening

Identify:
- Missing input validation on public endpoints/CLI args
- Hardcoded secrets (API keys, passwords in code)
- Unsafe dependencies (check for known vulnerabilities)
- Missing rate limiting on public endpoints
- SQL injection or XSS vulnerabilities

### 5. Technical Debt

Find:
- Deprecated APIs still in use
- Inconsistent patterns across codebase
- Missing tests for critical paths
- Documentation gaps (CONTRIBUTING.md, examples/)
- Workarounds marked with comments

### 6. Feature Gaps

Based on project type, identify:
- Common features for this type that are missing
- User-requested features (check GitHub issues if accessible)
- Competitive features (what similar tools have)

## Output Format

**REQUIRED:** Return the analysis in this specific markdown format so `pen-wielding` can read it.

```markdown
# Roadmap Candidates

## Performance Opportunities
| Location | Current | Opportunity | Impact |
|----------|---------|-------------|--------|
| `src/search.ts:45` | O(n²) nested loops | Use Map for O(1) lookup | High |
| `src/api.ts:120` | Sequential API calls | Batch with Promise.all | Medium |

## Technical Debt
| Location | Issue | Suggested Fix |
|----------|-------|---------------|
| `src/utils.ts:30` | TODO from 6 months ago | Implement or remove |
| `package.json` | lodash@3.x outdated | Upgrade to 4.x |

## Feature Gaps
| Feature | Why It Matters | Effort |
|---------|----------------|--------|
| Config file support | Users want persistent settings | Medium |
| Fluent data access | Stop two-step retrieval dance | Low |

## Security Hardening
| Location | Risk | Recommendation |
|----------|------|----------------|
| `src/cli.ts:15` | No input sanitisation | Validate before use |

## Complexity Notes
| Function | Complexity | Plain English |
|----------|------------|---------------|
| `findMatches()` | O(n²) | Compares every item - slow for large lists |

## Community Help Wanted
| Task | Context |
|------|---------|
| Add Tests | `src/core/` has 0% coverage |
| Examples | Create `examples/` folder with basic usage |
```

## Important

- Focus on README-worthy improvements (things users/contributors care about)
- Be specific with file:line references
- Explain WHY something is an opportunity, not just WHAT
- Prioritise by impact (High/Medium/Low)
- Don't overwhelm - top 5-10 items per category max

## Handoff

**Goal:** Transition from technical analysis to creative brainstorming.

1. **Present Findings:** Show the "Roadmap Candidates" tables.
2. **Verify:** Ask the user:
   > "The Crystal Ball has spoken. Happy with these insights, or want to explore more? Ready for a brain-jam with Gemini?"
3. **Transition:**
   - If user wants changes: Refine the analysis.
   - If user is satisfied: **"Proceeding to brain-jam."**

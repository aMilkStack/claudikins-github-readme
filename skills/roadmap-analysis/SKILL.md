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

Document in plain English: "This search is O(n²) because it compares every item to every other item. Could be O(n log n) with sorting first."

## Performance Opportunities

Look for:
- Unnecessary iterations that could be reduced
- Missing caching for expensive operations
- Synchronous operations that could be parallel
- Memory allocations that could be pooled
- Network calls that could be batched

## Code Quality Issues

Detect:
- Dead code (unused exports, commented blocks)
- Outdated dependencies (check package.json versions)
- Code smells (long functions >50 lines, deep nesting >3 levels)
- TODO/FIXME comments (extract and list)
- Inconsistent patterns (mixed async styles, naming conventions)

## Security Opportunities

Identify:
- Missing input validation
- Hardcoded secrets (API keys, passwords in code)
- Unsafe dependencies (check for known vulnerabilities)
- Missing rate limiting on public endpoints
- SQL injection or XSS vulnerabilities

## Technical Debt

Find:
- Deprecated APIs still in use
- Inconsistent patterns across codebase
- Missing tests for critical paths
- Documentation gaps
- Workarounds marked with comments

## Feature Gaps

Based on project type, identify:
- Common features for this type that are missing
- User-requested features (check GitHub issues if accessible)
- Competitive features (what similar tools have)

## Output Format

Return structured markdown:

```markdown
# Roadmap Analysis

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
| --verbose flag | Debugging is difficult | Low |

## Security Hardening
| Location | Risk | Recommendation |
|----------|------|----------------|
| `src/cli.ts:15` | No input sanitization | Validate before use |

## Complexity Notes
| Function | Complexity | Plain English |
|----------|------------|---------------|
| `findMatches()` | O(n²) | Compares every item - slow for large lists |
```

## Important

- Focus on README-worthy improvements (things users/contributors care about)
- Be specific with file:line references
- Explain WHY something is an opportunity, not just WHAT
- Prioritise by impact (High/Medium/Low)
- Don't overwhelm - top 5-10 items per category max

---
name: researching-readmes
description: Competitive research methodology for README documentation. Use when finding exemplar READMEs, scoring README quality, extracting patterns from top repositories, or recommending badges and sections based on project type. Covers search strategies, scoring rubrics, and pattern extraction.
---

# README Research Methodology

Systematic approach to researching high-quality READMEs for pattern extraction.

## Research Process

### Phase 1: Define Search Criteria

Based on project context from codebase analysis, match on:

| Criterion | How to Match |
|-----------|--------------|
| Category | Same project type (CLI, library, framework, API, etc.) |
| Tech Stack | Same or similar languages/frameworks |
| Ecosystem | Same package manager (npm, PyPI, Cargo) |
| Complexity | Similar scope (simple util vs enterprise tool) |
| Maturity | Established projects with proven documentation |

### Phase 2: Search Execution

**Search queries:**
```
"best [project-type] [tech-stack] github"
"awesome [technology] list"
"[similar-tool] alternatives github"
```

**Find 10-15 candidates**, then narrow to top 5-7 based on stars and initial quality scan.

## Scoring Rubric

Rate each README 1-10 on these dimensions:

| Dimension | Weight | What to Look For |
|-----------|--------|------------------|
| Value Proposition | 20% | Problem and solution crystal clear in first paragraph |
| Time to Joy (TTJ) | 20% | Commands to first working result (target: 2-3) |
| Visual Quality | 15% | GIFs, diagrams, code blocks, dark mode support |
| Structure | 15% | Logical flow, scannable, TOC if >200 lines |
| SEO Signals | 10% | Keywords in title, semantic headers, topics tagged |
| Badge Quality | 10% | Informative badges, 5-7 max, consistent style |
| Maintenance Signals | 10% | Recent commits, active issues, working links |

### Quantitative Targets

| Metric | Good | Red Flag |
|--------|------|----------|
| Flesch-Kincaid Grade | 8-10 | >12 (too complex) |
| TTJ (commands to result) | 2-3 | >5 |
| Visual Density | 1 per 300 words | >600 words without visual |
| Badge Count | 5-7 | >10 or 0 |

### Score Interpretation

| Score | Assessment |
|-------|------------|
| 9-10 | Exemplary - study closely |
| 7-8 | High quality - good patterns |
| 5-6 | Average - selective borrowing |
| 3-4 | Below average - learn what not to do |

## Pattern Extraction

For each high-scoring exemplar, extract:

**Hero Section:**
- Banner/logo style
- Tagline approach
- Badge selection and arrangement

**Structure:**
- Section order and naming conventions
- Use of collapsible sections
- Table of Contents style

**Visuals:**
- GIF usage (terminal recordings, UI demos)
- Diagram types (architecture, flow)
- Screenshot placement

**Writing Style:**
- Tone (minimal, conversational, opinionated, reference)
- Code example density
- Explanation depth

## Badge Recommendations

### Badge Categories by Signal

| Category | Signal | When to Use |
|----------|--------|-------------|
| Build Status | "Code compiles and tests pass" | Always |
| Code Coverage | "Maintainers care about testing" | If coverage >60% |
| Version | "This is a releasable product" | If published to registry |
| Social Proof | "Crowd has vetted this" | Only if numbers impress (5000+ stars) |
| License | "Legal to use in my project" | Always |
| Activity | "Project is alive" | Only if actively maintained |

### Badge Styles

Pick ONE style across all badges:
- `flat` - Modern, clean (most projects)
- `flat-square` - Sharp edges (technical projects)
- `for-the-badge` - Large, bold (hero sections only)

### Recommended Badge Sets

**Minimal (3-4):** Build Status, Version, License

**Standard (5-6):** Build Status, Coverage, Version, Downloads, License

**Comprehensive (7 max):** Build Status, Coverage, Quality, Version, Downloads, License, Last Commit

### Badge Anti-Patterns to Avoid
- **Overload:** 15+ badges creating visual chaos
- **Inconsistent styling:** Mix of flat, plastic, for-the-badge
- **Vanity badges:** "Made with JavaScript" adds no value
- **Stale badges:** Coverage showing 0% from broken CI
- **Meaningless numbers:** Badging 3 stars, 12 downloads

## Section Recommendations

Base recommendations on what top exemplars use:

### Common Section Patterns

| Section | When to Include |
|---------|-----------------|
| Quick Start | Always - first thing after hero |
| Installation | Always - multiple methods if applicable |
| Usage/Examples | Always - show, don't just tell |
| API Reference | Libraries and frameworks |
| Configuration | If configurable |
| Architecture | Complex projects with multiple components |
| Contributing | Open source projects seeking contributions |
| FAQ | If common questions exist |
| Troubleshooting | If known gotchas exist |

## Output Format

```markdown
# README Research Results

## Summary
- **Repos Analysed:** [X]
- **High Quality (8-10):** [X]
- **Key Patterns Identified:** [X]

## Top Exemplars

### 1. [Repo Name]
- **URL:** [GitHub link]
- **Quality Score:** [X/10]
- **Stars:** [X] | **Category:** [type]

**What Works Well:**
- [specific element 1]
- [specific element 2]

**Patterns to Borrow:**
- [pattern]: [why effective]

**Patterns to Avoid:**
- [what doesn't work]

**Relevance:** [how it applies to our project]

---

[Repeat for top 5-7]

## Recommended Patterns

### Sections for This Project
1. [Section]: Used by X/Y exemplars because [reason]
2. [Section]: [reason]

### Visual Recommendations
- [Type of visual]: [where to use it]

### Badge Recommendations
- [Badge type]: [source, what it signals]

### Anti-Patterns to Avoid
- [Thing]: Common mistake seen in lower-rated READMEs
```

## Additional Resources

See `references/badge-ecosystem.md` for complete badge sources and examples.
See `references/scoring-rubric.md` for detailed scoring criteria and checklists.

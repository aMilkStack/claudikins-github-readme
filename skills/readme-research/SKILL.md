---
name: researching-readmes
description: Finds and evaluates exemplar READMEs from similar projects. Used by readme-researcher agent to conduct competitive research, score README quality, and extract patterns worth borrowing.
---

# README Research Methodology

Systematic approach to researching high-quality READMEs for pattern extraction.

## Research Process

### Phase 1: Understand the Project

Receive project context from codebase analysis:
- Project type (CLI, library, framework, etc.)
- Tech stack
- Target audience
- Complexity level

### Phase 2: Define Research Criteria

Based on project context, define search parameters:

| Criterion | How to Match |
|-----------|--------------|
| Category | Same project type (CLI, library, etc.) |
| Tech Stack | Same or similar languages/frameworks |
| Ecosystem | Same package manager (npm, PyPI, Cargo) |
| Complexity | Similar scope (simple util vs enterprise) |
| Maturity | Established projects with proven docs |

### Phase 3: Research Execution

**Tools to use:**
- **Context7** (if available): Up-to-date documentation
- **WebSearch**: Find similar GitHub projects
- **WebFetch**: Read and analyse READMEs
- **Gemini deep-research** (if available): Comprehensive analysis

**Search queries:**
```
"best [project-type] [tech-stack] github"
"awesome [technology] list"
"[similar-tool] alternatives github"
```

**Find 10-15 candidates**, then narrow to top 5-7.

### Phase 4: Scoring Rubric

Rate each README 1-10 on these dimensions:

| Dimension | Weight | Criteria |
|-----------|--------|----------|
| Value Proposition | 20% | Clear problem/solution in first 30 seconds |
| Time to Joy (TTJ) | 20% | Commands to first working result (target: ≤3) |
| Visual Quality | 15% | GIFs, diagrams, screenshots, code blocks |
| Structure | 15% | Logical flow, scannable, good TOC |
| SEO Signals | 10% | Keywords in title, semantic headers |
| Badge Quality | 10% | Informative, not cluttered (5-7 max) |
| Maintenance Signals | 10% | Recent updates, active links |

**Quantitative Metrics:**

| Metric | Target | Red Flag |
|--------|--------|----------|
| Flesch-Kincaid Grade | 8-10 | >12 |
| TTJ (commands to result) | ≤3 | >5 |
| Visual Density | 1 per 300 words | >600 words without visual |
| Badge Count | 5-7 | >10 or 0 |

### Phase 5: Pattern Extraction

For each high-scoring exemplar, extract:

**Hero Section:**
- Banner/logo style
- Tagline approach
- Badge selection and arrangement

**Structure:**
- Section order
- Header naming conventions
- Use of collapsible sections

**Visuals:**
- GIF usage (terminal recordings, UI demos)
- Diagram types (architecture, flow)
- Screenshot placement

**Writing Style:**
- Tone (minimal, conversational, opinionated, reference)
- Code example density
- Explanation depth

### Phase 6: Gemini Integration

**Parallel execution:**
```
Claude: WebSearch + WebFetch + Context7 analysis
Gemini: deep_research(query="README exemplars for [project-type]")
```

**Synthesis prompt for Gemini brainstorming:**
```
Compare Claude's findings with Gemini's deep research.
Identify:
1. Patterns both found (high confidence)
2. Patterns only Claude found
3. Patterns only Gemini found
4. Conflicts to resolve
5. Final recommended patterns
```

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

## Agreement (Both Claude + Gemini Found)
- [pattern/insight with high confidence]

## Claude's Unique Finds
- [what Gemini missed]

## Gemini's Unique Finds
- [what Claude missed]

## Final Recommendations

### Sections for This Project
1. [Section]: Used by X/Y exemplars because [reason]
2. [Section]: [reason]
...

### Patterns to Use
- [Pattern]: Seen in [repos], achieves [effect]
- [Pattern]: ...

### Anti-Patterns to Avoid
- [Thing]: Common mistake, seen in lower-rated READMEs
- [Thing]: ...

### Visual Recommendations
- [Type of visual]: [where to use it]
- [Type of visual]: ...

### Badge Recommendations
- [Badge type]: [source, what it signals]
- [Badge type]: ...
```

## Integration with Main Skill

This skill is loaded by the readme-researcher agent. Return the structured research to the main README skill for combination with codebase analysis.

## Additional Resources

See `references/badge-ecosystem.md` for badge types and signals.
See `references/scoring-rubric.md` for detailed scoring criteria.

---
name: analyzing-codebases
description: Extracts README-relevant information from code and user patterns. Used by codebase-analyser agent to identify project type, tech stack, value proposition, dependencies, code quality issues, and development patterns from chat history.
---

# Codebase Analysis for README

Methodology for analysing a project to inform README generation.

## Analysis Sources

### 1. Codebase Analysis

**Tools to use:**
- **Serena** (if available): Semantic code search, class hierarchies, architecture understanding
- **Glob/Grep/Read**: File structure, dependencies, entry points

**Extract:**

| Category | What to Find | How |
|----------|--------------|-----|
| Project Type | CLI, library, framework, plugin, app, API | Entry points, package.json scripts, main files |
| Tech Stack | Languages, frameworks, dependencies | package.json, requirements.txt, Cargo.toml, etc. |
| Value Proposition | What problem it solves | README fragments, comments, package description |
| Entry Points | Where users start | main, index, bin, exports |
| Prerequisites | Runtime, system deps | engines field, Dockerfile, CI configs |
| CI/Automation | Test/build setup | .github/workflows, CI configs |
| Existing Docs | What's already documented | README, docs/, wiki |

**Gemini Integration:**

Run these in parallel:
```
gemini.analyze_code(code, focus="quality")
gemini.analyze_code(code, focus="security")
gemini.analyze_code(code, focus="performance")
gemini.analyze_code(code, focus="bugs")
```

### 2. Chat History Analysis

**Source:** `~/.claude/history.jsonl`

**Format:** JSONL with fields:
- `display`: User's message/request
- `project`: Project being worked on
- `timestamp`: Unix timestamp (milliseconds)
- `pastedContents`: Code or content pasted

**Extract:**

| Category | What to Find | Why It Matters |
|----------|--------------|----------------|
| Projects & Domains | What types of projects user builds | Audience calibration |
| Technologies Used | Languages, frameworks in conversations | Tech stack validation |
| Problem Types | Categories of problems solved | Documentation focus areas |
| Challenges | Repeated questions, struggles | Where to add extra clarity |
| Approach Patterns | How user solves problems | Writing style matching |

**Challenge Detection:**
- Repeated questions about same topics → knowledge gap
- Problems requiring multiple attempts → complex area needing docs
- Questions indicating confusion → unclear concepts

### 3. Issue Detection

**Find and report:**

| Issue Type | Detection Method | README Implication |
|------------|------------------|-------------------|
| Dead code | Serena unused symbols | Don't document deprecated features |
| Missing tests | Coverage gaps | Note testing status honestly |
| Outdated deps | Version checks | Update prerequisites section |
| Security issues | Gemini security analysis | Add security section or warnings |
| Performance issues | Gemini performance analysis | Document performance characteristics |
| Broken links | Existing README link check | Fix before generating new content |

## Output Format

Return structured analysis:

```markdown
# Codebase Analysis

## Project Overview
- **Type:** [CLI/library/framework/plugin/app/API]
- **Tech Stack:** [languages, frameworks]
- **Value Proposition:** [1-2 sentence problem/solution]
- **Entry Point:** [main file/command]

## Dependencies
- **Runtime:** [Node 18+, Python 3.10+, etc.]
- **System:** [any system dependencies]
- **Dev:** [dev dependencies of note]

## Code Quality (Claude + Gemini Combined)

### Quality Issues
- [issue 1]
- [issue 2]

### Security Concerns
- [concern 1]

### Performance Notes
- [note 1]

### Bugs Found
- [bug 1]

## Improvement Suggestions
- [suggestion 1: what to fix/add]
- [suggestion 2]

## User Patterns (from Chat History)
- **Typical Projects:** [what they build]
- **Common Struggles:** [repeated questions]
- **Skill Level:** [indicators of expertise]

## README Implications
- **Suggested Prerequisites:** [based on deps analysis]
- **Badge Sources:** [CI, coverage, package manager]
- **Complexity Level:** [how technical to write]
- **Focus Areas:** [based on user struggles]
```

## Synthesis with Gemini

After both Claude and Gemini analyses complete:

1. **Compare findings** - What did each identify?
2. **Agreements** - High confidence findings
3. **Differences** - Resolve or note both perspectives
4. **Gaps** - What one caught that other missed

Use `gemini.brainstorming(thinking_level="high")` for synthesis if available.

## Integration with Main Skill

This skill is loaded by the codebase-analyser agent. Return the structured analysis to the main README skill for combination with research findings.

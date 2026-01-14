---
name: coauthoring-readmes
description: Orchestrates README creation through parallel AI analysis and collaborative writing. Use when the user mentions "README", "write docs", "document this project", "improve documentation", or works on a new project without a README. Spawns codebase-analyser and readme-researcher agents in parallel, synthesises findings, then co-authors sections with user feedback.
---

# README Co-Author

Turn rough ideas about documentation into polished READMEs through collaborative dialogue.

## Overview

Start by understanding the project through parallel AI analysis, then work through the README section by section with the user. Ask questions one at a time. Present options. Get feedback. Iterate.

## The Process

### Understanding (Parallel Analysis)

Before asking questions, gather context:
- Spawn `codebase-analyser` and `readme-researcher` agents in parallel
- Wait for both to return findings
- Use `gemini.brainstorming(thinking_level="high")` to synthesise if available

### Style Preferences

Ask one question at a time:

**Spelling:**
1. British (colour, optimise) - default
2. American (color, optimize)

**Tone:**
1. Minimal - Just the facts
2. Conversational - Friendly, explains the "why"
3. Opinionated - Has personality, states positions
4. Reference - Comprehensive, every option documented

### Planning the Structure

Based on analysis and research:
- Present recommended sections with evidence
- Lead with your recommendation and explain why
- Ask if the structure looks right
- Adjust based on feedback

### Writing Sections

For each section:
1. Draft the section
2. Present it for review
3. Ask: "Does this look right? What should change?"
4. Iterate until satisfied
5. Move to next section

Check metrics as you go:
- Time to Joy ≤ 3 commands?
- Readability Grade 8-10?
- Visual every 300 words?

### Final Review

Walk through the checklist together:
- [ ] Hero section (banner, 5-7 badges, tagline)
- [ ] Clear value proposition
- [ ] Quick start that actually works
- [ ] No walls of text
- [ ] All links valid

## Writing Rules (Always Enforced)

- Clear and concise
- Active voice
- Important information first
- No M dash (—) EVER
- Technical only, no marketing fluff

## Modes

**Create Mode** (no README exists):
Full workflow from analysis to writing.

**Update Mode** (README exists):
- Parse existing sections
- Identify what's stale vs current
- Update only stale sections
- Preserve manual customisations
- Present changes as diff

## Key Principles

- **One question at a time** - Don't overwhelm
- **Show your reasoning** - Explain why you recommend things
- **Parallel analysis** - Spawn both agents simultaneously
- **User approval before writing** - Get sign-off on structure
- **Iterate sections** - Draft, review, refine
- **Metrics-driven** - Check TTJ, readability, visual density

## After the README

**Offer automation:**
- Link checking (lychee)
- Badge updates
- TOC generation
- Help-to-README sync (for CLIs)

## Additional Resources

See `references/style-options.md` for detailed tone examples.

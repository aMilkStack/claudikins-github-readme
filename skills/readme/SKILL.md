---
name: coauthoring-readmes
description: Orchestrates README creation through parallel AI analysis and collaborative writing. Use when the user mentions "README", "write docs", "document this project", "improve documentation", or works on a new project without a README. Spawns codebase-analyser and readme-researcher agents in parallel, synthesises findings, then co-authors sections with user feedback.
---

# README Co-Author

Turn rough documentation ideas into polished READMEs through natural collaborative dialogue.

Start by understanding the project through parallel AI analysis, then ask questions one at a time to refine the approach. Once the structure is clear, write sections in 200-300 word chunks, checking after each whether it looks right.

## The Process

### Understanding the Project

Check the current state first:
- Spawn `codebase-analyser` and `readme-researcher` agents in parallel
- Analyser: deep code analysis, complexity, architecture, user patterns
- Researcher: competitive research, patterns, anti-patterns, trends
- Wait for both to return, synthesise with `gemini.brainstorming` if available

Then ask questions one at a time to refine:
- Prefer multiple choice when possible, open-ended when needed
- Only one question per message
- Focus on: purpose, audience, constraints, success criteria

**Style questions:**

Spelling:
1. British (colour, optimise) - default
2. American (color, optimize)

Tone:
1. Minimal - "Just the facts. Install, use, done."
2. Conversational - "Friendly, explains the 'why'."
3. Opinionated - "Has personality, states positions."
4. Reference - "Comprehensive, every option documented."

### Exploring Approaches

Based on analysis and research, propose 2-3 structural approaches:
- Present options conversationally with trade-offs
- Lead with the recommended option and explain why
- Show evidence from research (what top repos do)

Example:
> "Based on the research, I'd recommend the **Minimal** structure - your CLI tool is simple and users will want to get started fast. The top performers in this category (fzf, ripgrep) use this approach.
>
> Alternative: **Reference** style if you want to document all 47 flags upfront.
>
> Which fits better?"

### Writing the README

Once structure is agreed:
- Write sections in 200-300 word chunks
- Present each section for review
- Ask: "Does this look right? What should change?"
- Be ready to go back and clarify if something doesn't make sense
- Move to next section only when current one is approved

**For each section, spawn the `readme-writer` agent with:**
- Approved structure
- Analysis findings (from codebase-analyser)
- Research findings (from readme-researcher)
- User style preferences

**Check metrics as you write:**
- Time to Joy ≤ 3 commands?
- Flesch-Kincaid Grade 8-10?
- Visual every 300 words?

### Final Review

Walk through the checklist together:
- [ ] Hero section (banner, 5-7 badges, tagline)
- [ ] Value proposition clear in first 30 seconds
- [ ] Installation is copy-pasteable
- [ ] Quick start actually works
- [ ] No walls of text
- [ ] All links valid

### After the README

Offer automation:
- Link checking (lychee)
- Badge updates
- TOC auto-generation
- Help-to-README sync (for CLIs)

## Modes

**Create Mode** (no README):
Full workflow - analyse, research, structure, write.

**Update Mode** (README exists):
- Parse existing sections
- Identify stale vs current
- Update only stale sections
- Preserve manual customisations
- Present changes as diff

## Writing Rules (Always Enforced)

- Clear and concise
- Active voice
- Important information first
- No M dash (—) EVER
- Technical only, no marketing fluff

## Key Principles

- **One question at a time** - Don't overwhelm with multiple questions
- **Multiple choice preferred** - Easier to answer than open-ended
- **YAGNI ruthlessly** - Remove unnecessary sections from all READMEs
- **Explore alternatives** - Propose 2-3 approaches before settling
- **Incremental validation** - Present in 200-300 word sections, validate each
- **Be flexible** - Go back and clarify when something doesn't make sense

## Additional Resources

See `references/style-options.md` for detailed tone examples.

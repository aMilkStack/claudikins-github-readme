---
name: coauthoring-readmes
description: Orchestrates README creation through parallel AI analysis and collaborative writing. Use when the user mentions "README", "write docs", "document this project", "improve documentation", or works on a new project without a README. Spawns codebase-analyser and readme-researcher agents in parallel, synthesises findings, then co-authors sections with user feedback.
---

# README Co-Author

Orchestrate the creation or update of high-quality README documentation through parallel AI analysis and collaborative writing.

## Core Principles

**Writing Standards (always enforced):**
- Clear and concise
- Active voice
- Important information first
- Include relevant links and references
- Match company communication style
- No M dash (—) EVER - use hyphens or restructure sentences
- Technical only - no marketing fluff

**Spelling:** British by default, American on request.

## Mode Detection

Check for existing README.md:
- **Exists → Update Mode**: Diff-merge, preserve manual edits, update only stale sections
- **Missing → Create Mode**: Full generation workflow

## Workflow

### Phase 1: Style Preferences

Ask user (present as options):

**Spelling:**
1. British (colour, optimise, analyse) - default
2. American (color, optimize, analyze)

**Tone:**
1. Minimal - "Just the facts. Install, use, done."
2. Conversational - "Friendly but professional. Explains the 'why'."
3. Opinionated - "Has personality. States positions clearly."
4. Reference - "Comprehensive. Every flag, every option documented."

### Phase 2: Parallel Analysis

Spawn TWO agents simultaneously using Task tool:

```
Task 1: codebase-analyser agent
Task 2: readme-researcher agent
```

Both run in parallel, both leverage Claude + Gemini tools, both return structured findings.

### Phase 3: Synthesis

When both agents return:
1. Combine codebase analysis with research findings
2. Use `gemini.brainstorming(thinking_level="high")` if available
3. Identify recommended sections for this project type
4. Check metrics:
   - Time to Joy (TTJ) ≤ 3 commands?
   - If installation > 5 steps → suggest Dockerfile/Makefile

### Phase 4: Section Planning

Present skeleton to user:
- Recommended sections with evidence from research
- Patterns to apply (from exemplar analysis)
- Anti-patterns to avoid
- Get approval before writing

### Phase 5: Writing

Spawn readme-writer agent with:
- Approved structure
- Analysis findings
- Research findings
- User style preferences

Writer produces sections one at a time for user review.

### Phase 6: Co-Authoring Loop

For each section:
1. Writer drafts section
2. Check metrics:
   - Flesch-Kincaid readability ≤ Grade 10?
   - Visual density (≥1 visual per 300 words)?
3. Offer `/readme-preview` for HTML preview
4. User provides feedback
5. Iterate until satisfied
6. Move to next section

### Phase 7: Final Review

Strategic Checklist:
- [ ] Hero section complete (banner, badges 5-7 max, tagline)
- [ ] TTJ ≤ 3 commands
- [ ] Readability Grade 8-10
- [ ] Visual density met
- [ ] No anti-patterns (walls of text, badge overload, stale artifacts)
- [ ] All links valid (suggest lychee pre-check)

### Phase 8: Automation Offer

After README complete, offer GitHub Actions scaffolding:
- [ ] Link checking (lychee weekly)
- [ ] Badge updates
- [ ] Help-to-README sync (if CLI project)
- [ ] TOC auto-generation

### Phase 9: Output

**Create Mode:** Write README.md to project
**Update Mode:** Present diff/patch for review, preserve manual sections

## Update Mode Details

When README.md exists:

1. **Ingest**: Read existing README
2. **Segment**: Parse into sections using headers
3. **Compare**: Check each section against codebase analysis
4. **Flag stale sections**:
   - "Usage section missing new --verbose flag"
   - "Installation prereqs outdated"
   - "Badge shows old coverage %"
5. **Selective update**: Only regenerate stale sections
6. **Preserve**: Keep manual customisations in non-stale sections
7. **Output as patch**: Present diff, not overwrite

## Anti-Patterns (NEVER DO)

| Anti-Pattern | Detection | Fix |
|--------------|-----------|-----|
| Wall of Text | >5 consecutive paragraphs | Headers, bullets, code blocks |
| Badge Overload | >7 badges | Curate to most important |
| Stale Artifacts | Dates, version mismatches | Automate generation |
| Dead Links | Lychee check fails | Fix or remove |
| "Works on My Machine" | Missing prereqs | Explicit versions, Docker |
| Missing Alt Text | Images without alt | Always describe visuals |

## Preview Command

Generate temporary preview.html:
- Render Markdown with GitHub CSS
- Render Mermaid diagrams
- Show GIF placeholders
- Open in browser for visual review

## Additional Resources

See `references/style-options.md` for detailed tone examples.

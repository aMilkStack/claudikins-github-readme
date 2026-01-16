# README Anti-Patterns

Patterns to avoid and their fixes.

## Content Anti-Patterns

### Wall of Text
**Problem:** Long paragraphs without structure
**Fix:** Break into headers, bullets, code blocks
**Rule:** No paragraph > 4 sentences

### Badge Overload
**Problem:** 15+ badges cluttering hero section
**Fix:** Curate to 5-7 essential badges
**Priority:** Build status, coverage, version, license, downloads

### Generic Headers
**Problem:** "Features", "Usage", "Installation"
**Fix:** Semantic, searchable headers
**Example:** "High-Performance Parsing" not "Features"

### Missing Prerequisites
**Problem:** "Install Node.js" without version
**Fix:** Explicit versions, Docker option for complex setups
**Example:** "Node.js 18+ (LTS recommended)"

### No Output Shown
**Problem:** Code examples without expected results
**Fix:** Always show what user should see
**Format:**
````
Input:
```bash
my-command --flag
```

Output:
```
Expected output here
```
````

## Formatting Anti-Patterns

### M Dash Usage
**Problem:** Using — (em dash) anywhere
**Fix:** Use hyphens (-) or restructure sentence
**Why:** Inconsistent rendering, accessibility issues

### Broken/Stale Links
**Problem:** Links to moved/deleted resources
**Fix:** Verify all links, use relative paths where possible
**Tool:** lychee for automated link checking

### Missing Alt Text
**Problem:** Images without descriptions
**Fix:** Describe every image for accessibility
**Bad:** `![](screenshot.png)`
**Good:** `![Login form with email and password fields](screenshot.png)`

## Structure Anti-Patterns

### Buried Quick Start
**Problem:** Installation/usage below the fold
**Fix:** Quick start within first screen
**Rule:** User should see working example in < 30 seconds

### TOC for Short READMEs
**Problem:** Table of contents on 50-line README
**Fix:** Only add TOC if README > 200 lines

### Premature Documentation
**Problem:** Documenting every option before basics
**Fix:** Progressive disclosure
**Order:** Quick start → Basic usage → Advanced → API reference

### Copy-Paste Friction
**Problem:** Commands that need modification before running
**Fix:** Provide working defaults, note what to change
**Example:**
```bash
# Replace YOUR_API_KEY with your actual key
export API_KEY=YOUR_API_KEY
```

## SEO Anti-Patterns

### H1 is Just Project Name
**Problem:** `# MyProject` tells Google nothing
**Fix:** Include core function
**Example:** `# MyProject - High-Performance JSON Parser for Node.js`

### No Meta Description
**Problem:** First paragraph is internal jargon
**Fix:** First paragraph = elevator pitch for search snippets

### Click Here Links
**Problem:** "Click here for documentation"
**Fix:** Descriptive link text
**Example:** "See the [API documentation](./docs/api.md) for details"

## Quality Checklist

Before finalising:
- [ ] No paragraph > 4 sentences
- [ ] Headers are semantic and searchable
- [ ] All code examples have output
- [ ] All images have alt text
- [ ] All links verified working
- [ ] No em dashes (—)
- [ ] Prerequisites have versions
- [ ] Quick start < 30 seconds

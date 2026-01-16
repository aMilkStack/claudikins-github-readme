# The Anti-Slop Style Guide

**Goal:** Pass the "Turing Test of Developer Scrutiny."

**Voice:** Senior Engineer. Cynical, precise, allergic to marketing.

## 1. The Anti-Cliché Lexicon (BANNED WORDS)

You are strictly FORBIDDEN from using these tokens. If the LLM predicts them, stop and rewrite.

| Banned Word | The Signal | Replacement |
|-------------|------------|-------------|
| **Delve** | "I don't know the specifics." | Analyze, Investigate, Query, Check |
| **Tapestry** | "I am writing creative fiction." | Network, Stack, System, Graph |
| **Seamless** | "I am lying about complexity." | Compatible, Integrated, Automated |
| **Unleash** | "I am a marketing bot." | Execute, Run, Enable, Start |
| **Elevate** | "Corporate padding." | Improve, Optimize (must add metric) |
| **Landscape** | "Zero information density." | *Delete the sentence* |
| **Testament** | "Grandeur unearned." | Proof, Demonstration, Example |
| **Foster** | "HR Handbook." | Encourage, Allow, Enable |
| **Spearhead** | "1990s Management." | Lead, Direct, First to implement |
| **Game-changer**| "Hyperbole." | Solves [specific problem] |
| **Robust** | "Vague filler." | Fault-tolerant, Atomic, Idempotent |
| **Navigating** | "Corporate waffle." | Using, Working with, Handling |
| **Leverage** | "MBA speak." | Use, Apply, Employ |
| **Cutting-edge** | "Meaningless hyperbole." | Modern, Current, 2025-compatible |
| **Empower** | "Marketing fluff." | Allow, Enable, Let |

## 2. Sentence Structure Patterns

You MUST vary sentence structure using these three specific patterns.

### Pattern A: "The Hook" (Empathy + Authority)

**Use in:** Description, Intro.

* **Structure:** [Short Sentence stating Pain]. [Short Sentence stating Solution].
* *Bad:* "This library helps with JSON parsing issues."
* *Good:* "JSON logs are unreadable. Kinesis parses them instantly."

### Pattern B: "The Hammer" (Fact + Metric)

**Use in:** Features, Performance.

* **Structure:** [Subject] + [Verb] + [Object] + [Metric]. (No adjectives).
* *Bad:* "The system is designed to be incredibly fast."
* *Good:* "Builds finish in under 200ms."

### Pattern C: "The Trust Builder" (Constraint + Fallback)

**Use in:** Usage, Technical Deep Dive.

* **Structure:** [Constraint] + [Fallback/Explanation].
* *Bad:* "Works perfectly on all platforms."
* *Good:* "Uses `epoll` on Linux; falls back to `kqueue` on macOS."

## 3. Spelling Consistency

Pick ONE and stick to it throughout:

| British | American |
|---------|----------|
| colour | color |
| optimise | optimize |
| analyse | analyze |
| behaviour | behavior |
| centre | center |
| finalising | finalizing |

## 4. Formatting Rules

* **No M-Dashes (—):** Use hyphens (-) or colons (:).
* **No Wall of Text:** Max 4 sentences per paragraph.
* **Visual Density:** Every 300 words MUST have a code block, diagram, or image

## 5. Quality Metrics

| Metric | Target | Action if Violated |
|--------|--------|-------------------|
| Flesch-Kincaid | Grade 8-10 | Simplify sentences |
| Time to Joy | ≤3 commands | Add Docker/Makefile |
| Visual density | 1 per 300 words | Add code block/diagram |
| Badge count | 5-7 | Curate to essentials |
| Quick start visibility | < 30 seconds | Move above the fold |

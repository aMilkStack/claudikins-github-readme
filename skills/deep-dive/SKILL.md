---
name: deep-dive
description: "Take a deep dive into the codebase. Identify what this project IS - type, stack, deps, architecture. Facts only."
---

# The Deep Dive

"Let me take a deep dive into this codebase..."

Identify what the project IS, not what it could be. Facts only.

## Project Type Detection

### Entry Point Analysis

| Files Present | Likely Type |
|---------------|-------------|
| `bin/`, shebang in main | CLI tool |
| `src/index.ts` with exports | Library |
| `src/main.ts` or `app.ts` | Application |
| `plugin.json`, `.claude-plugin/` | Plugin |
| `src/server.ts`, `app.py` | API/Server |
| `Dockerfile` only | Container |
| `setup.py` with console_scripts | Python CLI |
| `Cargo.toml` with [[bin]] | Rust CLI |

### Package.json Indicators

```json
{
  "bin": { "cmd": "./dist/cli.js" },     // CLI
  "main": "./dist/index.js",              // Library
  "exports": { ".": "./dist/index.js" },  // Modern library
  "scripts": { "start": "node server.js" } // Application
}
```

## Tech Stack Extraction

### Dependency Files

| File | Ecosystem |
|------|-----------|
| `package.json` | Node.js/JavaScript |
| `requirements.txt`, `pyproject.toml` | Python |
| `Cargo.toml` | Rust |
| `go.mod` | Go |
| `Gemfile` | Ruby |
| `pom.xml`, `build.gradle` | Java |
| `composer.json` | PHP |

### Framework Detection

**JavaScript/TypeScript:**
- `react`, `vue`, `angular` - Frontend framework
- `express`, `fastify`, `koa` - Backend framework
- `electron` - Desktop app
- `react-native` - Mobile app

**Python:**
- `fastapi`, `flask`, `django` - Web framework
- `click`, `typer`, `argparse` - CLI framework
- `pytorch`, `tensorflow` - ML framework

### Build Tool Detection

| Tool | Files |
|------|-------|
| TypeScript | `tsconfig.json` |
| Webpack | `webpack.config.js` |
| Vite | `vite.config.ts` |
| esbuild | `esbuild` in scripts |
| Rollup | `rollup.config.js` |
| Babel | `.babelrc`, `babel.config.js` |

## Dependencies & Prerequisites

### Runtime Requirements

**From package.json:**
```json
{ "engines": { "node": ">=18.0.0", "npm": ">=9.0.0" } }
```

**From pyproject.toml:**
```toml
[project]
requires-python = ">=3.10"
```

**From Cargo.toml:**
```toml
[package]
rust-version = "1.70"
```

### System Dependencies

**Check these files:**
- `Dockerfile` - RUN apt-get install commands
- `.github/workflows/*.yml` - setup steps
- `Makefile` - prerequisite checks
- `INSTALL.md` or `docs/installation.md`

**Common system deps:**
- `libssl-dev` - cryptography
- `libpq-dev` - PostgreSQL
- `ffmpeg` - media processing
- `graphviz` - diagram generation

## Entry Points & API Surface

**What does the project export/expose?**

- Main function/export in index file
- CLI commands from bin directory
- API routes from server files
- Public methods from library exports

**CLI help text extraction:**
```typescript
program
  .name('my-tool')
  .description('Process files with advanced filtering')
  .version('1.0.0');
```

**Value proposition sources:**
- `package.json` description field
- Module-level docstrings
- JSDoc on main exports
- Existing README fragments

## CI/Automation Detection

### GitHub Actions

**Badge sources from workflows:**
- Workflow status - Build badge
- `codecov/codecov-action` - Coverage badge
- Release workflow - Version badge

### Other CI

| Service | Config File |
|---------|-------------|
| CircleCI | `.circleci/config.yml` |
| Travis | `.travis.yml` |
| GitLab CI | `.gitlab-ci.yml` |
| Jenkins | `Jenkinsfile` |

## Chat History Context

**Source:** `~/.claude/history.jsonl`

Filter entries where `project` matches the current project path.

**JSONL format:**
```json
{"display": "User message", "project": "/path/to/project", "timestamp": 1704067200000}
```

### Pattern Extraction

**Repeated questions (knowledge gaps):**
- "How do I..." patterns
- "Why isn't..." patterns
- "What's the difference between..." patterns

**Problem categories:**
- Configuration/Setup
- Debugging/Errors
- Feature implementation
- Performance
- Testing
- Deployment

### README Implications

| Pattern Found | README Implication |
|---------------|-------------------|
| Repeated config questions | Detailed configuration section |
| Debugging struggles | Troubleshooting section |
| "How do I test" questions | Testing section with examples |
| Performance questions | Performance section |
| Deployment questions | Deployment guides |

## Output Format

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

## Entry Points
- [file:line] - [what it does]

## CI/Automation
- **Build:** [workflow files]
- **Badge Sources:** [CI, coverage, package manager]

## User Context (from Chat History)
- **Common Struggles:** [repeated questions]
- **Decisions Made:** [key decisions from history]
- **Focus Areas:** [topics frequently discussed]
```

## Important

- Focus on FACTS, not improvements
- Be specific with file:line references
- Note confidence levels:
  - **High:** Extracted from config files
  - **Medium:** Inferred from patterns
  - **Low:** Guessed from structure

## Handoff

After presenting findings:

- Ask: "Happy with the deep dive? Want to refine anything, or continue to consult the crystal-ball?"
- If refine → address feedback, ask again
- If continue → Use `crystal-ball`

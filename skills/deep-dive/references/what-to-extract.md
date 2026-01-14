# What to Extract from Codebase

Detailed guide for extracting README-relevant information.

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
  "bin": { "cmd": "./dist/cli.js" },  // CLI
  "main": "./dist/index.js",          // Library
  "exports": { ".": "./dist/index.js" }, // Modern library
  "scripts": {
    "start": "node server.js"         // Application
  }
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
- `react`, `vue`, `angular` → Frontend framework
- `express`, `fastify`, `koa` → Backend framework
- `electron` → Desktop app
- `react-native` → Mobile app

**Python:**
- `fastapi`, `flask`, `django` → Web framework
- `click`, `typer`, `argparse` → CLI framework
- `pytorch`, `tensorflow` → ML framework

### Build Tool Detection

| Tool | Files |
|------|-------|
| TypeScript | `tsconfig.json` |
| Webpack | `webpack.config.js` |
| Vite | `vite.config.ts` |
| esbuild | `esbuild` in scripts |
| Rollup | `rollup.config.js` |
| Babel | `.babelrc`, `babel.config.js` |

## Prerequisites Extraction

### Runtime Requirements

**From package.json:**
```json
{
  "engines": {
    "node": ">=18.0.0",
    "npm": ">=9.0.0"
  }
}
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

## CI/Automation Detection

### GitHub Actions

```yaml
# .github/workflows/ci.yml
name: CI
on: [push, pull_request]
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
      - run: npm ci
      - run: npm test
      - uses: codecov/codecov-action@v4  # Coverage!
```

**Badge sources:**
- Workflow status → Build badge
- codecov-action → Coverage badge
- release workflow → Version badge

### Other CI

| Service | Config File |
|---------|-------------|
| CircleCI | `.circleci/config.yml` |
| Travis | `.travis.yml` |
| GitLab CI | `.gitlab-ci.yml` |
| Jenkins | `Jenkinsfile` |

## Value Proposition Sources

### Existing Documentation

1. **package.json description:**
   ```json
   { "description": "Fast JSON parser for embedded systems" }
   ```

2. **README fragments:**
   - Look for existing README.md
   - Check docs/ directory
   - Check wiki if present

3. **Code comments:**
   - Module-level docstrings
   - JSDoc on main exports
   - README badges alt text

### Code Analysis

**What it does:**
- Main function analysis
- Export analysis
- CLI help text extraction

**Example CLI help extraction:**
```typescript
// src/cli.ts
program
  .name('my-tool')
  .description('Process files with advanced filtering')
  .version('1.0.0');
```

## Chat History Patterns

### File Location
`~/.claude/history.jsonl`

### JSONL Format
```json
{"display": "How do I add authentication?", "project": "/path/to/project", "timestamp": 1704067200000}
{"display": "The tests are failing", "project": "/path/to/project", "timestamp": 1704067260000}
```

### Pattern Extraction

**Repeated Questions (Knowledge Gaps):**
```
Count occurrences of similar questions:
- "How do I..." patterns
- "Why isn't..." patterns
- "What's the difference between..." patterns
```

**Technology Usage:**
```
Extract mentions of:
- Framework names
- Library names
- Tool names
- Language features
```

**Problem Categories:**
```
Classify questions:
- Configuration/Setup
- Debugging/Errors
- Feature implementation
- Performance
- Testing
- Deployment
```

### README Implications

| Pattern Found | README Implication |
|---------------|-------------------|
| Repeated config questions | Detailed configuration section |
| Debugging struggles | Troubleshooting section |
| "How do I test" | Testing section with examples |
| Performance questions | Performance section |
| "Deploy to X" questions | Deployment guides |

## Issue Detection

### Dead Code

**Using Serena:**
```
semantic_search("unused exports")
semantic_search("deprecated functions")
```

**Manual indicators:**
- `// TODO: remove` comments
- `@deprecated` JSDoc tags
- Commented-out code blocks

### Outdated Dependencies

**Check npm:**
```bash
npm outdated
```

**Check Python:**
```bash
pip list --outdated
```

**Security:**
```bash
npm audit
pip-audit
```

### Broken Links

**In existing README:**
```bash
# Use lychee or similar
lychee README.md
```

### Missing Tests

**Coverage gaps:**
- Files with 0% coverage
- Core modules without test files
- Missing integration tests

## Output Integration

All extracted information feeds into the structured analysis output defined in the main skill. Prioritise:

1. **High confidence:** Extracted from config files
2. **Medium confidence:** Inferred from patterns
3. **Low confidence:** Guessed from structure

Always note confidence level in output.

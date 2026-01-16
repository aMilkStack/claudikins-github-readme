# Structural Templates

Complete templates for each README section, informed by analysis of 10k+ star repositories (2024-2025).

---

## The Conversion Funnel

Users progress through three cognitive stages:

1. **Verification** - "Is this project alive and safe?" (Hero Section)
2. **Value Assessment** - "Why should I use this?" (Description/Features)
3. **Activation** - "How do I start?" (Install/Quick Start)

**Key metric:** Time-to-First-Success (TTFS) - commands from clone to working result.

---

## Section Ordering by Project Type

Different project types have different friction points. Order sections accordingly.

### CLI Tools (ripgrep, fzf, bat)

**Primary friction:** Installation (binaries, OS-specific packages)

1. Hero (Identity + Visual Preview)
2. Features/Highlights
3. Table of Contents
4. **Installation** (multiple OS methods)
5. Usage/Key Bindings
6. Configuration
7. Integration (Vim, Shell, other tools)
8. Benchmarks
9. Contributing
10. License

### Libraries (zod, TanStack Query)

**Primary friction:** Understanding the paradigm (install is trivial)

1. Hero (Identity + Badges)
2. Introduction/Philosophy
3. Features
4. Installation
5. **Basic Usage** (code-first)
6. Advanced Usage/API
7. Ecosystem/Integrations
8. Contributing
9. License

### Frameworks (fastify, hono)

**Primary friction:** Proving scalability and ecosystem

1. Hero (Identity + Badges)
2. **Quick Start / Scaffold**
3. Core Features
4. Benchmarks
5. Ecosystem/Plugins
6. Documentation Links
7. Team
8. Sponsors
9. License

---

## 1. Hero Section

The top 600px (above the fold) must contain: Identity, Trust, Value, Navigation.

### Standard Template

```markdown
<p align="center">
  <img src="banner.png" alt="Project Name" width="600">
</p>

<p align="center">
  <a href="..."><img src="badge1" alt="Build"></a>
  <a href="..."><img src="badge2" alt="Coverage"></a>
  <a href="..."><img src="badge3" alt="Version"></a>
  <a href="..."><img src="badge4" alt="License"></a>
</p>

# Project Name

> One sentence value proposition that filters your audience
```

### Badge Hierarchy

Order badges by what users verify first:

| Priority | Category | Signal |
|----------|----------|--------|
| 1 | Operational Status | "Safe to use" (Build, Coverage, Version) |
| 2 | Social Proof | "Others trust this" (Downloads, Stars) |
| 3 | Communication | "Support available" (Discord, Twitter) |
| 4 | Metadata | "Legal compliance" (License, Code Style) |

### Value Proposition Examples

**Effective (filters audience, states differentiator):**
- "TypeScript-first schema validation with static type inference"
- "A cat(1) clone with syntax highlighting and Git integration"
- "Like grep, but faster and respects .gitignore"

**Ineffective (says nothing):**
- "A powerful tool for developers"
- "The best solution for your needs"

### Visual Proof (CLI Tools)

For CLI/visual tools, include a GIF or screenshot in the hero:

```markdown
<p align="center">
  <img src="demo.gif" alt="Terminal demo showing project usage" width="600">
</p>
```

---

## 2. Description

### The "Comparative Definition" Pattern

Anchor to known tools, then differentiate:

```markdown
## What is [Project]?

[Project] does X for Y. Instead of [tedious manual approach], you [simple action] and get [result].

**Key Features:**
- [Feature 1]: [Benefit]
- [Feature 2]: [Benefit]
- [Feature 3]: [Benefit]
```

**Pattern:** Show value through contrast, not "Problem/Solution" headers.

### The "Code-First" Pattern

For libraries, show the API immediately:

```markdown
## What is [Project]?

\`\`\`typescript
import { schema } from 'project-name';

const User = schema.object({
  name: schema.string(),
  age: schema.number().positive(),
});

type User = schema.infer<typeof User>;
\`\`\`

Zero dependencies. 2kb gzipped. Full TypeScript support.
```

---

## 3. Table of Contents

### When to Include

| README Length | TOC Required |
|---------------|--------------|
| < 500 words | No |
| 500-1000 words | Optional |
| > 1000 words | Yes |

### Template

```markdown
## Table of Contents

- [Installation](#installation)
- [Quick Start](#quick-start)
- [Usage](#usage)
  - [Basic Usage](#basic-usage)
  - [Advanced Usage](#advanced-usage)
- [Configuration](#configuration)
- [Contributing](#contributing)
- [License](#license)
```

### Back-to-Top Links (Long Documents)

```markdown
<p align="right"><a href="#table-of-contents">Back to top</a></p>
```

---

## 4. Installation

### Multi-Method Pattern (CLI Tools)

```markdown
## Installation

### Prerequisites
- [Requirement 1] (version X+)
- [Requirement 2]

### Package Managers

\`\`\`bash
# macOS
brew install project-name

# Ubuntu/Debian
sudo apt install project-name

# Windows
choco install project-name
\`\`\`

### From Source

\`\`\`bash
cargo install project-name
\`\`\`

### Pre-built Binaries

Download from [Releases](https://github.com/user/project/releases).
```

### Single-Command Pattern (Libraries)

```markdown
## Installation

\`\`\`bash
npm install project-name
\`\`\`
```

### Scaffold Pattern (Frameworks)

```markdown
## Quick Start

\`\`\`bash
npm create project-name@latest my-app
cd my-app
npm run dev
\`\`\`

Open http://localhost:3000 to see your app.
```

---

## 5. Quick Start

### The "Copy-Paste Ready" Rule

Every code example must:
1. Work when copy-pasted (no `...` or `[your-thing-here]`)
2. Show expected output
3. Use realistic values, not `foo` and `bar`

```markdown
## Quick Start

\`\`\`typescript
import { createApp } from 'project-name';

const app = createApp({
  port: 3000,
  logger: true,
});

app.get('/', () => ({ message: 'Hello World' }));

app.listen();
\`\`\`

**Output:**
\`\`\`
Server running at http://localhost:3000
\`\`\`
```

---

## 6. Usage

### Progressive Disclosure Pattern

```markdown
## Usage

### Basic Usage

\`\`\`typescript
// Simple example covering 80% of use cases
\`\`\`

<details>
<summary><strong>Advanced Configuration</strong></summary>

### Custom Options

\`\`\`typescript
// Complex example for power users
\`\`\`

### Environment Variables

| Variable | Default | Description |
|----------|---------|-------------|
| `DEBUG` | `false` | Enable debug logging |

</details>
```

### What to Collapse

- Large configuration objects
- Migration guides (v3 to v4)
- Benchmark data tables
- Platform-specific instructions

### What to Never Collapse

- Installation
- Basic Usage
- Critical warnings
- Prerequisites

---

## 7. Configuration

### Table Format

```markdown
## Configuration

| Option | Type | Default | Description |
|--------|------|---------|-------------|
| `port` | `number` | `3000` | Server port |
| `logger` | `boolean` | `false` | Enable request logging |
| `timeout` | `number` | `30000` | Request timeout in ms |
```

### Collapsible Full Config

```markdown
Basic configuration:

\`\`\`json
{ "port": 3000, "logger": true }
\`\`\`

<details>
<summary><strong>Full configuration reference</strong></summary>

\`\`\`json
{
  "port": 3000,
  "host": "0.0.0.0",
  "logger": { "level": "info", "prettyPrint": true }
}
\`\`\`

</details>
```

---

## 8. Ecosystem / Integrations

### Plugin List Pattern (Frameworks)

```markdown
## Ecosystem

### Official Plugins

| Plugin | Description |
|--------|-------------|
| [@project/auth](link) | Authentication middleware |
| [@project/cache](link) | Redis caching layer |

### Community Plugins

See [awesome-project](link) for community extensions.
```

### Integration Pattern (CLI Tools)

```markdown
## Integrations

### Vim/Neovim

\`\`\`vim
Plug 'user/project.vim'
\`\`\`

### Shell Integration

Add to `.bashrc` or `.zshrc`:

\`\`\`bash
eval "$(project --init bash)"
\`\`\`
```

---

## 9. Contributing

```markdown
## Contributing

Contributions welcome! Please read [CONTRIBUTING.md](CONTRIBUTING.md) first.

### Development Setup

\`\`\`bash
git clone https://github.com/user/project
cd project
npm install
npm test
\`\`\`
```

---

## 10. License

```markdown
## License

[MIT](LICENSE)
```

---

## Quick Reference

| Position | CLI Tool | Library | Framework |
|----------|----------|---------|-----------|
| 1 | Hero + Preview | Hero | Hero |
| 2 | Features | Features | Quick Start |
| 3 | TOC | Install | Features |
| 4 | **Install** | **Basic Usage** | Benchmarks |
| 5 | Usage | Advanced | **Ecosystem** |
| 6 | Config | Ecosystem | Docs |
| 7 | Integration | Contributing | Team |
| 8 | Benchmarks | License | License |

**Bold** = Primary section for that project type.

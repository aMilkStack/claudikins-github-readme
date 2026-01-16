# Visual Engineering

Guidelines for GIFs, diagrams, and screenshots in READMEs.

## When to Use GIFs

Best for:
- **CLI tools:** Show terminal session
- **UI components:** Show interaction
- **Complex workflows:** Show step-by-step

**Tool recommendation:** VHS for reproducible terminal GIFs

```bash
# Install VHS
brew install vhs  # macOS
# or
go install github.com/charmbracelet/vhs@latest
```

**Example VHS tape:**
```
Output demo.gif

Set FontSize 14
Set Width 800
Set Height 400

Type "npm install my-tool"
Enter
Sleep 2s
Type "my-tool --help"
Enter
Sleep 3s
```

## When to Use Diagrams

Best for:
- **Architecture:** System components and connections
- **Data flow:** How data moves through system
- **Class relationships:** OOP hierarchies

**Use Mermaid** for GitHub-native rendering:

````markdown
```mermaid
flowchart LR
    A[Input] --> B[Process]
    B --> C[Output]
```
````

**Common diagram types:**

### Flowchart (Architecture)
```mermaid
flowchart TB
    Client --> API
    API --> Database
    API --> Cache
```

### Sequence (Data Flow)
```mermaid
sequenceDiagram
    User->>API: Request
    API->>DB: Query
    DB-->>API: Result
    API-->>User: Response
```

### Class (Relationships)
```mermaid
classDiagram
    Animal <|-- Dog
    Animal <|-- Cat
    Animal: +name
    Animal: +speak()
```

## When to Use Screenshots

Best for:
- **UI applications:** Show the interface
- **Dashboards:** Show data visualisation
- **Config files:** Show expected structure

**Requirements:**
- Always include alt text for accessibility
- Compress images (target < 500KB)
- Use consistent dimensions
- Dark/light mode versions if applicable

**Markdown format:**
```markdown
![Dashboard showing user metrics](./docs/images/dashboard.png)
```

## Visual Density Rule

**Target:** 1 visual per 300 words

If a section exceeds 300 words without a visual:
1. Add a code block
2. Add a diagram
3. Add a screenshot
4. Break into subsections with examples

## Accessibility

Every visual must have:
- **Alt text:** Descriptive, not decorative
- **Caption:** Context if not obvious
- **Text alternative:** Key info available without image

Bad: `![](image.png)`
Good: `![Architecture diagram showing client-server-database flow](./docs/arch.png)`

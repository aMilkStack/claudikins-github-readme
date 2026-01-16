# Gemini Deep Research Reference

Deep research is asynchronous. It takes **5-20 minutes** (sometimes longer for complex queries). Be patient.

## The Workflow

### Step 1: Start Research

```typescript
const start = await gemini["gemini-deep-research"]({
  query: "Your comprehensive research question here",
  format: "structured report with sections"
});

await workspace.writeJSON("research-start.json", start);
console.log("Started - check research-start.json for ID");
```

**One query, one call.** Combine all your research needs into a single comprehensive question. Gemini can handle multiple topics. Don't make parallel calls - you'll hit rate limits.

### Step 2: Extract the Research ID

The response gets auto-saved to `mcp-results/`. You'll see something like:

```json
{
  "_savedTo": "mcp-results/123-gemini-gemini-deep-research.json",
  "_preview": "**Deep Research Started**\n\n| Research ID | `v1_abc123...` |..."
}
```

Copy the file to the project directory so you can read it:

```typescript
const fs = await import('fs/promises');
const content = await workspace.read("research-start.json");
await fs.writeFile('/path/to/project/.claude/research-start.json', content);
console.log("Copied - now use Read tool");
```

Then use the **Read tool** on that file. Find the Research ID in the markdown table (looks like `v1_abc123...`).

### Step 3: Wait and Poll

Research takes time. Wait 2-5 minutes between checks.

```typescript
const status = await gemini["gemini-check-research"]({
  researchId: "v1_abc123..."  // paste the ID you extracted
});

await workspace.writeJSON("research-status.json", status);
console.log("Status saved");
```

Copy and read the status file. Look for:
- `**Deep Research In Progress**` - keep waiting
- `**Deep Research Complete**` - you have results

### Step 4: Read the Results

When complete, the response contains the full report. Copy it out and read it:

```typescript
const result = await workspace.readJSON("mcp-results/[latest-check-file].json");
const text = result.content?.[0]?.text;

const fs = await import('fs/promises');
await fs.writeFile('/path/to/project/.claude/research-complete.md', text);
console.log("Report saved");
```

Then use the **Read tool** on that file.

## Troubleshooting

### Repeated 500 errors on check endpoint

The research may have failed internally. Start fresh with a new query. Simpler queries are more reliable than complex ones.

### Research takes forever

Complex queries with many topics can take 20+ minutes. If you're past 30 minutes with no completion, consider starting fresh with a simpler query.

### "Precondition check failed" on followup

The research isn't complete yet. Keep polling with `gemini-check-research`.

## Example Query (What Worked)

```typescript
const start = await gemini["gemini-deep-research"]({
  query: "Best README examples for CLI tools like ripgrep and fzf",
  format: "short summary"
});
```

This completed in ~5 minutes and returned a 22K character report with detailed analysis.

## Key Points

- **ONE call at a time** - rate limits are real
- **5-20 minutes is normal** - don't assume it's broken
- **Copy files to project directory** - workspace files aren't directly readable with Read tool
- **If stuck, start fresh** - sometimes research fails silently
- **Simpler queries finish faster** - balance scope with reliability

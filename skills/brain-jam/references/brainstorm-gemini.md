# Gemini Brainstorm Reference

## Important: Output Handling

**The brainstorm output is LARGE and MULTI-TURN.** It contains multiple rounds of back-and-forth conversation between Claude and Gemini.

**DO NOT** try to parse or summarise the output inline. Instead:
1. Save it to workspace
2. Read it directly from workspace using the Read tool
3. Then synthesise your findings

## Running the Brainstorm

```typescript
const result = await gemini["gemini-brainstorm"]({
  prompt: "Your problem statement here",
  claudeThoughts: "Your initial analysis and thoughts here",
  maxRounds: 3  // 1-5 rounds, default 3
});

// ALWAYS save to workspace first
if (result._savedTo) {
  // Large result was auto-saved
  const fullResult = await workspace.readJSON(result._savedTo);
  await workspace.writeJSON("brainstorm-output.json", fullResult);
} else {
  await workspace.writeJSON("brainstorm-output.json", result);
}

console.log("Brainstorm saved to brainstorm-output.json");
```

## Reading the Output

**After saving, exit execute_code and use the Read tool directly:**

```
Read tool: workspace/brainstorm-output.json
```

The output contains:
- Multiple conversation turns between Claude and Gemini
- Each turn builds on the previous
- Ideas that emerged from the dialogue
- Points of agreement and disagreement

## Why Read Directly?

- The multi-turn output is too large to return through execute_code without truncation
- Reading via the Read tool preserves the full conversation
- You can see the evolution of ideas across turns
- Context is preserved for synthesis

## Parameters

| Parameter | Required | Description |
|-----------|----------|-------------|
| `prompt` | Yes | The problem statement or query |
| `claudeThoughts` | Yes | Your initial analysis to seed the conversation |
| `maxRounds` | No | Number of turns (1-5, default 3) |

## Example for README Brain-Jam

```typescript
const result = await gemini["gemini-brainstorm"]({
  prompt: "What's the right angle for this CLI tool's README? Technical depth vs accessibility?",
  claudeThoughts: "The architecture is elegant - O(1) lookups instead of O(n). But devs care about solving problems, not implementation details.",
  maxRounds: 3
});

await workspace.writeJSON("brainstorm-output.json", result._savedTo
  ? await workspace.readJSON(result._savedTo)
  : result);

console.log("Done - now read brainstorm-output.json with Read tool");
```

Then use Read tool on `workspace/brainstorm-output.json` to see the full conversation.

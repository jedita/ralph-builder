# Ralph Wiggum Loop Builder

An interactive playground for configuring and generating bash scripts that run **Ralph** — an autonomous coding agent that iterates through a task list, implements features, learns from failures, and commits on success.

## What it does

Ralph Builder is a single-file HTML tool with a sidebar of configuration options and a live-updating script preview. You tweak the settings, and the generated bash script updates in real time. When you're happy with the configuration, hit **Copy** and paste the script into your terminal.

The generated script runs a loop that:

1. Reads a tasks file (`tasks.json`) and a context file (`contract.md`)
2. Picks the next task using a configurable prioritization strategy
3. Sends the task to an AI agent (Claude via Docker Sandbox, local CLI, or Codex)
4. On success — marks the task as passing, records learnings, and optionally commits
5. On failure — records what went wrong so the next iteration can learn from it
6. Repeats until all tasks are complete or max iterations are reached

### Modes

- **Implement** — builds features, runs tests, commits on pass
- **Gap Investigation** — analyzes source vs. destination code for parity gaps without writing any code

### Configuration options

| Option | Description |
|---|---|
| Model | Sonnet or Opus |
| Runner | Docker Sandbox, Local Claude CLI, or Codex |
| Max iterations | How many loop cycles before giving up |
| Branch | Git branch to work on |
| Tasks / Context files | Paths to your task list and context document |
| Prioritization | Smart (learnings > deps > complexity), Simple, or Sequential |
| Global learnings | Aggregate learnings across all tasks |
| Parity check | Enforce 100% feature parity |
| Commit on pass | Auto-commit when a task passes |

## How to run

No build step, no dependencies. Just open the HTML file in a browser:

```bash
open ralph-builder.html
```

Or on Linux:

```bash
xdg-open ralph-builder.html
```

Or simply double-click `ralph-builder.html` in your file manager.

## Dependencies

- [claude-stream-format](https://github.com/jedita/claude-stream-format) — used for formatting Claude's streaming output

## Origin

This project was created using the **playground** skill from [Claude Code](https://docs.anthropic.com/en/docs/claude-code) — Anthropic's CLI tool for Claude. The playground skill generates self-contained, single-file HTML applications with interactive controls and a live preview, designed to let you visually configure something and copy out the result.

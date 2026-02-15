# Architecture and Four Tools

## The Monorepo

Pi is built as a monorepo (`badlogic/pi-mono`) with cleanly separated packages:

| Package | Purpose |
|---------|---------|
| `pi-ai` | Unified LLM API across 4 wire protocols (OpenAI Completions, OpenAI Responses, Anthropic Messages, Google Generative AI) |
| `pi-agent-core` | Agent loop, tool execution, event streaming |
| `pi-tui` | Terminal UI framework with differential rendering, flicker-free output |
| `pi-coding-agent` | The CLI that wires it all together |
| `pi-mom` | Slack bot / autonomous agent built on pi |
| `pi-web-ui` | Web-based chat interface components |
| `pi-pods` | vLLM pod management for self-hosting |

## Four Tools

The agent has exactly four built-in tools:

```
read   -- Read file contents (text and images)
write  -- Create or overwrite files
edit   -- Surgical find-and-replace edits
bash   -- Execute shell commands
```

That's the entire tool surface. Everything else is built on top via extensions.

Why only four? Because these are the primitives that cover 95% of coding tasks. More tools means more token overhead in the system prompt, more confusion for the model, and more things that can break between releases.

## Four Execution Modes

```
Interactive  -- Full TUI experience (default)
Print/JSON   -- pi -p "query" for scripts, --mode json for event streams
RPC          -- JSON protocol over stdin/stdout for non-Node integrations
SDK          -- Embed pi in your own apps (how OpenClaw is built)
```

## Context Control Stack

Pi provides multiple layers for controlling what enters the model's context:

```
SYSTEM.md        -- Replace or append to the default system prompt (per-project)
AGENTS.md        -- Project instructions, loaded from ~/.pi/agent/, parent dirs, and cwd
Skills           -- On-demand capability packages (progressive disclosure)
Prompt templates -- Reusable prompts as markdown files (/name to expand)
Extensions       -- Dynamic context injection, RAG, message filtering, compaction
```

The key insight: skills are loaded on-demand (the agent reads the README only when relevant), which means you pay the token cost only when needed. This is "progressive disclosure" -- the opposite of MCP, which dumps all tool descriptions into context at session start.

## Session Format

Sessions are JSONL files with a tree structure. Each entry has an `id` and `parentId`, enabling in-place branching without creating new files. The format supports:

- User messages, assistant messages, tool results
- Bash execution records (command, output, exit code)
- Custom messages (extension state, persisted across restarts)
- Branch summaries and compaction summaries
- Full token usage and cost tracking per message

See [04-sessions.md](./04-sessions.md) for details.

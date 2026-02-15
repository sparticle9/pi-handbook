# Quick Start and Daily Workflows

## Installation

```bash
npm install -g @mariozechner/pi-coding-agent
```

Or use a standalone binary (no Node.js required) -- check the GitHub releases.

## Android (Termux) Setup

Pi runs on Android via Termux with zero friction:

1. Install [Termux](https://termux.dev/) from F-Droid
2. Install Node.js: `pkg install nodejs`
3. Install pi: `npm install -g @mariozechner/pi-coding-agent`
4. Copy just your `~/.pi/agent/models.json` from your desktop
5. Run `pi`

That's it -- `models.json` is the only file you need to bring over. Extensions, skills, and packages can all be installed via CLI afterwards (`pi install npm:shitty-extensions`, etc.). This is one of pi's underrated strengths: because everything is npm packages and local files, getting productive on a new device takes under a minute.

## Authentication

```bash
# Option 1: API key
export ANTHROPIC_API_KEY=sk-ant-...
pi

# Option 2: OAuth subscription (Claude Pro/Max, ChatGPT Plus, Copilot, Gemini)
pi
/login
```

## First Session

```bash
cd your-project
pi
```

Pi will load any `AGENTS.md` files from `~/.pi/agent/`, parent directories, and the current directory.

## Essential Commands

| Command | Action |
|---------|--------|
| `Ctrl+L` | Switch model |
| `Ctrl+P` | Cycle favorite models |
| `Shift+Tab` | Cycle thinking level |
| `/tree` | Navigate session tree |
| `/fork` | Branch to new session |
| `/compact` | Summarize old context |
| `/name <label>` | Label current session |
| `/export` | Export to HTML |
| `/share` | Upload to GitHub gist |
| `/reload` | Hot-reload extensions |
| `Ctrl+C` | Clear editor |
| `Ctrl+C` x2 | Quit |
| `Escape` | Cancel/abort |
| `Escape` x2 | Open `/tree` |
| `Ctrl+O` | Collapse/expand tool output |

## Editor Features

| Feature | How |
|---------|-----|
| File reference | Type `@` to fuzzy-search project files |
| Path completion | Tab |
| Multi-line | Shift+Enter |
| Paste images | Ctrl+V |
| Run bash inline | `!command` (sends output to LLM) |
| Run bash silent | `!!command` (runs without sending) |

## Message Queuing

While the agent is working:

- `Enter` -- Send steering message (interrupts after current tool)
- `Alt+Enter` -- Send follow-up (waits until agent finishes)
- `Escape` -- Abort and restore queued messages

## Recommended Setup

### 1. Global AGENTS.md

Create `~/.pi/agent/AGENTS.md` with your universal preferences:

```markdown
# Global Agent Instructions

## Style
- Use TypeScript strict mode
- Prefer functional patterns
- Keep functions under 30 lines

## Tools
- Use pnpm for package management
- Use vitest for testing
```

### 2. Project AGENTS.md

Create `AGENTS.md` in your project root:

```markdown
# Project: My App

## Stack
- Next.js 15, TypeScript, Tailwind
- Deployed on Vercel

## Conventions
- Components in src/components/
- API routes in src/app/api/
- Use server actions for mutations
```

### 3. Install Community Extensions

```bash
# Oracle + handoff + plan mode + more
pi install npm:shitty-extensions

# Model switching with aliases
pi install npm:pi-model-switch
```

### 4. Configure Model Aliases

Create `~/.pi/agent/extensions/model-switch/aliases.json`:

```json
{
  "cheap": "google/gemini-2.5-flash",
  "coding": "anthropic/claude-sonnet-4-20250514",
  "review": "openai/gpt-5.2"
}
```

## Daily Workflow Patterns

### Focused Task

```
pi
> "Implement the user authentication flow using NextAuth.js"
# Agent works autonomously until done
```

### Exploration + Branch

```
pi
> "Explore two approaches for the caching layer"
# Agent explores approach A
/tree    # Go back to before approach A
> "Now try approach B using Redis instead"
# Compare both branches
```

### Multi-Model Brainstorm

```
> "Design the API schema for the notification service"
# Claude designs it
> "Switch to review model"
> "Review the schema design, find edge cases"
# GPT-5.2 reviews
> "Switch to coding model"
> "Implement the schema based on the review feedback"
```

### Handoff Between Sessions

```
> "Plan the migration from REST to GraphQL"
# Agent creates the plan
/handoff implement phase 1 of the migration plan
# New session starts with focused context
```

### Resume Previous Work

```bash
pi -c          # Continue most recent session
pi -r          # Browse all sessions, pick one
```

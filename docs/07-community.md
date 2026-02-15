# Community Extensions

Pi's community has built extensions that cover the major features found in competing agents. Here are the most relevant packages.

## shitty-extensions (by hjanuschka)

The most comprehensive community package. Actively maintained.

```bash
pi install npm:shitty-extensions
```

| Extension | Description | Equivalent in |
|-----------|-------------|---------------|
| `oracle.ts` | Get second opinions from other AI models | Amp Oracle |
| `handoff.ts` | Transfer context to new sessions | Amp Handoff |
| `plan-mode.ts` | Read-only exploration mode | Claude Code plan mode |
| `memory-mode.ts` | Save instructions to AGENTS.md | Persistent learning |
| `cost-tracker.ts` | Session spending analysis | Built-in in Amp/Claude |
| `clipboard.ts` | Copy text to system clipboard via OSC52 | -- |
| `ultrathink.ts` | Rainbow animated "ultrathink" effect | Fun |
| `loop.ts` | Conditional loops (by mitsuhiko/Armin Ronacher) | -- |
| `flicker-corp.ts` | Authentic fullscreen flicker experience | Parody of Claude Code |

### Oracle Usage

Once installed, tell the agent:

```
"Ask the oracle to review this implementation"
"Use the oracle to debug this race condition"
"Have the oracle brainstorm alternative approaches"
```

The oracle sends the current context to a second model (configurable) and returns its analysis. It's read-only -- it advises but doesn't make changes.

### Handoff Usage

```
/handoff now implement the authentication flow
/handoff execute phase one of the plan
```

Generates a focused prompt for a new session based on the current context and your goal.

## pi-model-switch (by nicobailon)

Lets the agent switch models autonomously.

```bash
pi install npm:pi-model-switch
```

Configure aliases:

```json
{
  "cheap": "google/gemini-2.5-flash",
  "coding": "anthropic/claude-opus-4-5",
  "budget": ["openai/gpt-5-mini", "google/gemini-2.5-flash"]
}
```

Usage:

```
"Switch to a cheaper model"
"Use Opus for this refactor"
"List available models"
```

## pi-subagent-enhanced (by nicobailon)

Full sub-agent support with multiple execution modes.

| Mode | Description |
|------|-------------|
| Single | `{ agent: "worker", task: "refactor auth" }` |
| Chain | Sequential tasks with `{previous}` placeholder |
| Parallel | Multiple tasks running simultaneously |
| Async | Background execution with notifications |

Features:
- Output truncation (configurable byte/line limits)
- Debug artifacts (input, output, JSONL, metadata per task)
- Session-scoped notifications

## @marckrenn/pi-sub-core

Shared usage tracking across providers.

```bash
pi install npm:@marckrenn/pi-sub-core
```

Tracks usage for: Anthropic, OpenAI Codex, GitHub Copilot, Google Gemini, Antigravity, z.ai, AWS Kiro.

## pi-skills (by Mario Zechner)

Mario's official collection of skills for common development tasks.

```bash
pi install git:github.com/badlogic/pi-skills
```

These are curated, first-party skills that follow pi's philosophy of progressive disclosure -- the agent loads them on-demand when relevant. Check the repo for the current list of available skills and their descriptions.

https://github.com/badlogic/pi-skills

## Armin Ronacher's Extensions (referenced in his blog)

Armin has built several extensions he describes in his Pi writeup:

- `/answer` -- Extracts questions from the agent's response, presents them in a structured UI, sends answers back
- Custom to-do tracker -- Agent-specific local issue tracker with a tool interface
- Various TUI widgets -- Dashboards, debugging interfaces

His philosophy: point your agent to an existing extension and say "build it like that, but with these changes."

## Notable Community Integrations

- **Emacs frontend** (`dnouri/pi-coding-agent`) -- Full Emacs mode with markdown rendering, streaming, branch navigation
- **OpenClaw** -- Slack/Telegram bot built on pi's SDK
- **pi-mom** -- Mario's autonomous Slack bot

## Finding More Packages

```bash
# Browse on npm
# Search for keyword: pi-package

# Or check the Discord community server
```

The package registry at shittycodingagent.ai/packages lists community contributions (when npm registry is reachable).

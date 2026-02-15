# Extension System

Pi's extension system is its most powerful differentiator. Extensions are TypeScript modules that can hook into every aspect of the agent's lifecycle.

## Capabilities

- Register custom tools the LLM can call
- Intercept and block/modify tool calls (permission gates)
- Inject context before each turn (RAG, memory)
- Filter and transform message history
- Customize compaction behavior
- Register slash commands (`/mycommand`)
- Register keyboard shortcuts
- Render custom TUI components (dashboards, pickers, overlays)
- Persist state into sessions (survives restarts)
- Register CLI flags

## Quick Start

Create `~/.pi/agent/extensions/my-extension.ts`:

```typescript
import type { ExtensionAPI } from "@mariozechner/pi-coding-agent";
import { Type } from "@sinclair/typebox";

export default function (pi: ExtensionAPI) {
  // React to events
  pi.on("session_start", async (_event, ctx) => {
    ctx.ui.notify("Extension loaded!", "info");
  });

  // Block dangerous commands
  pi.on("tool_call", async (event, ctx) => {
    if (event.toolName === "bash" && event.input.command?.includes("rm -rf")) {
      const ok = await ctx.ui.confirm("Dangerous!", "Allow rm -rf?");
      if (!ok) return { block: true, reason: "Blocked by user" };
    }
  });

  // Register a custom tool
  pi.registerTool({
    name: "greet",
    label: "Greet",
    description: "Greet someone by name",
    parameters: Type.Object({
      name: Type.String({ description: "Name to greet" }),
    }),
    async execute(toolCallId, params, signal, onUpdate, ctx) {
      return {
        content: [{ type: "text", text: `Hello, ${params.name}!` }],
        details: {},
      };
    },
  });

  // Register a command
  pi.registerCommand("hello", {
    description: "Say hello",
    handler: async (args, ctx) => {
      ctx.ui.notify(`Hello ${args || "world"}!`, "info");
    },
  });
}
```

Test without installing:

```bash
pi -e ./my-extension.ts
```

Hot-reload after changes:

```
/reload
```

## Extension Locations

| Location | Scope |
|----------|-------|
| `~/.pi/agent/extensions/*.ts` | Global (all projects) |
| `~/.pi/agent/extensions/*/index.ts` | Global (subdirectory) |
| `.pi/extensions/*.ts` | Project-local |
| `.pi/extensions/*/index.ts` | Project-local (subdirectory) |

## Event Lifecycle

```
session_start
  |
  v
input --> before_agent_start --> agent_start
  |
  +-- turn_start
  |     +-- context (can modify messages)
  |     +-- tool_call (can block/modify)
  |     +-- tool_result (can transform output)
  +-- turn_end
  |
  v
agent_end --> (next user input)
```

## Skills vs Extensions

| | Skills | Extensions |
|---|---|---|
| Format | Markdown files | TypeScript modules |
| Loaded | On-demand by the agent | At startup |
| Purpose | Instructions + conventions | Tools + behavior + UI |
| Token cost | Only when relevant | Tool descriptions always in context |
| Sharing | Pi packages | Pi packages |

Skills are ideal for teaching the agent how to use a CLI tool or follow a convention. Extensions are for when you need programmatic control.

## Pi Packages

Bundle extensions, skills, prompts, and themes as npm or git packages:

```bash
# Install from npm
pi install npm:shitty-extensions

# Install from git
pi install git:github.com/badlogic/pi-doom

# Pin version
pi install npm:@foo/bar@1.2.3

# Project-local (shared with team via .pi/)
pi install -l npm:shitty-extensions

# Try without installing
pi -e npm:shitty-extensions

# Update all
pi update

# List installed
pi list
```

Packages use the `pi-package` keyword on npm for discoverability.

## Self-Extending Agent

The most powerful pattern: ask pi to build its own extensions.

```
"Build me an extension that tracks how many tokens each tool call uses
and shows a summary widget above the editor."
```

Pi will read its own extension docs, write the TypeScript, hot-reload, test, and iterate. This is what Armin Ronacher calls "agents built for agents building agents."

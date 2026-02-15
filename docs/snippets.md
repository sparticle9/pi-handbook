# Code Snippets Reference

Concrete code examples referenced throughout the handbook.

## Extension: Permission Gate

Block dangerous bash commands with user confirmation:

```typescript
// ~/.pi/agent/extensions/permission-gate.ts
import type { ExtensionAPI } from "@mariozechner/pi-coding-agent";

const DANGEROUS_PATTERNS = ["rm -rf", "sudo", "DROP TABLE", "format", "mkfs"];

export default function (pi: ExtensionAPI) {
  pi.on("tool_call", async (event, ctx) => {
    if (event.toolName !== "bash") return;

    const cmd = event.input.command || "";
    const match = DANGEROUS_PATTERNS.find((p) => cmd.includes(p));

    if (match) {
      const ok = await ctx.ui.confirm(
        "Dangerous Command",
        `Command contains "${match}":\n${cmd}\n\nAllow?`
      );
      if (!ok) return { block: true, reason: `Blocked: contains ${match}` };
    }
  });
}
```

## Extension: Oracle (Simplified)

Consult a second model for review and brainstorming:

```typescript
// ~/.pi/agent/extensions/oracle.ts
import type { ExtensionAPI } from "@mariozechner/pi-coding-agent";
import { Type } from "@sinclair/typebox";
import { getModel, stream } from "@mariozechner/pi-ai";

export default function (pi: ExtensionAPI) {
  pi.registerTool({
    name: "oracle",
    label: "Oracle",
    description: `Consult a second model for review, debugging, or brainstorming.
      The oracle analyzes and advises but doesn't make changes.`,
    parameters: Type.Object({
      question: Type.String({ description: "What to ask the oracle" }),
      context: Type.String({ description: "Relevant code or situation summary" }),
    }),
    async execute(toolCallId, params, signal, onUpdate, ctx) {
      const oracle = getModel("openai", "gpt-5.2");

      const response = await stream(
        oracle,
        {
          system: `You are a senior engineering oracle. You review, analyze,
            and advise. You do NOT write code directly.`,
          messages: [
            {
              role: "user",
              content: `${params.context}\n\n${params.question}`,
            },
          ],
        },
        { apiKey: process.env.OPENAI_API_KEY! }
      );

      return {
        content: [{ type: "text", text: await response.text }],
        details: { model: "gpt-5.2", role: "oracle" },
      };
    },
  });
}
```

## Extension: Session Recall

Read and summarize another session (cross-session reference):

```typescript
// ~/.pi/agent/extensions/recall.ts
import type { ExtensionAPI } from "@mariozechner/pi-coding-agent";
import { readFileSync, readdirSync } from "node:fs";
import { join } from "node:path";
import { homedir } from "node:os";

export default function (pi: ExtensionAPI) {
  pi.registerCommand("recall", {
    description: "Load summary of another session by ID",
    handler: async (sessionId, ctx) => {
      if (!sessionId) {
        ctx.ui.notify("Usage: /recall <session-id>", "error");
        return;
      }

      const sessionsDir = join(homedir(), ".pi", "agent", "sessions");
      // Search all project directories for the session
      const projects = readdirSync(sessionsDir);

      for (const project of projects) {
        const projectDir = join(sessionsDir, project);
        const files = readdirSync(projectDir).filter((f) =>
          f.startsWith(sessionId)
        );

        if (files.length > 0) {
          const content = readFileSync(join(projectDir, files[0]), "utf-8");
          const lines = content.split("\n").filter(Boolean);
          const messages = lines
            .map((l) => JSON.parse(l))
            .filter(
              (e) => e.type === "message" && e.message?.role === "assistant"
            )
            .slice(-5); // Last 5 assistant messages

          const summary = messages
            .map((m) =>
              m.message.content
                .filter((c: any) => c.type === "text")
                .map((c: any) => c.text)
                .join("")
            )
            .join("\n---\n");

          ctx.ui.notify(
            `Loaded session ${sessionId} from ${project}`,
            "success"
          );
          // Inject as context for next turn
          return { inject: summary };
        }
      }

      ctx.ui.notify(`Session ${sessionId} not found`, "error");
    },
  });
}
```

## Skill: Web Search (CLI-based)

A skill file that teaches the agent to use a CLI search tool:

```markdown
<!-- .pi/skills/web-search/SKILL.md -->
# Web Search

Search the web and fetch page content using CLI tools.

## Tools

### search
Search the web: `search "your query" --max-results 5`
Returns: title, URL, snippet for each result.

### fetch
Read a web page: `fetch <url> --format text --max-chars 5000`
Returns: page content as plain text.

## Usage Pattern
1. Search for information: `search "topic"`
2. Read promising results: `fetch <url>`
3. Synthesize findings for the user

## Notes
- Prefer specific queries over broad ones
- Fetch only the pages that look relevant from search results
- Summarize rather than dumping raw content
```

## AGENTS.md Template

```markdown
# AGENTS.md

## Project
- Name: [project name]
- Stack: [e.g., Next.js 15, TypeScript, Tailwind, Drizzle ORM]
- Deployed on: [e.g., Vercel, Cloudflare Workers]

## Conventions
- Use pnpm for package management
- Use strict TypeScript
- Components in src/components/
- Keep functions under 30 lines
- Write tests for business logic

## Model Preferences
- Simple file ops / quick questions: switch to "cheap"
- Complex refactoring / architecture: switch to "coding"
- Code review: switch to "review"
- Default to budget-friendly models unless quality is needed

## Do Not
- Commit credentials or .env files
- Modify files in node_modules/
- Run destructive commands without confirmation
```

## Custom Provider Configuration

```json
// ~/.pi/agent/models.json
{
  "providers": [
    {
      "id": "my-ollama",
      "name": "Local Ollama",
      "api": "openai-completions",
      "baseUrl": "http://localhost:11434/v1",
      "models": [
        {
          "id": "llama-3.1-70b",
          "name": "Llama 3.1 70B",
          "contextWindow": 128000,
          "maxTokens": 32000,
          "reasoning": false,
          "input": ["text"]
        }
      ]
    }
  ]
}
```

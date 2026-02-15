# Multi-Model Freedom

One of pi's killer features: seamless model switching mid-session across 15+ providers.

## Supported Providers

**Via subscription (OAuth):**
- Anthropic Claude Pro/Max
- OpenAI ChatGPT Plus/Pro (Codex)
- GitHub Copilot
- Google Gemini CLI
- Google Antigravity

**Via API key:**
- Anthropic, OpenAI, Azure OpenAI, Google Gemini, Google Vertex
- Amazon Bedrock, Mistral, Groq, Cerebras, xAI
- OpenRouter, Vercel AI Gateway, ZAI, OpenCode Zen
- Hugging Face, Kimi For Coding, MiniMax

**Self-hosted:**
- Ollama, llama.cpp, vLLM, LM Studio (via OpenAI-compatible API)

## Switching Models

```
Ctrl+L          -- Open model selector (full list)
Ctrl+P          -- Cycle through scoped/favorite models
Shift+Ctrl+P    -- Cycle backward
/model           -- Switch via command
```

## Context Handoff

Pi-ai is designed from the ground up for cross-provider context handoff. When you switch from Anthropic to OpenAI mid-session:

- Thinking traces are converted to `<thinking></thinking>` content blocks
- Provider-specific signed blobs are handled transparently
- Tool call history is preserved across providers
- Token/cost tracking continues accurately

This is best-effort (providers have different capabilities), but it works well in practice.

From Ewald Benes:

> Models have finally become a commodity to me. I'm currently cycling through Anthropic, z.ai, and Moonshot AI (Kimi) within the same session. I can swap the "brain" of the agent mid-stream, and the new model picks up the context seamlessly where the last one left off.

## Model Aliases (via pi-model-switch extension)

Install the community extension:

```bash
pi install npm:pi-model-switch
```

Configure aliases in `~/.pi/agent/extensions/model-switch/aliases.json`:

```json
{
  "cheap": "google/gemini-2.5-flash",
  "fast": "google/gemini-2.5-flash",
  "coding": "anthropic/claude-opus-4-5",
  "budget": ["openai/gpt-5-mini", "google/gemini-2.5-flash"]
}
```

Then just say: "switch to cheap" or "use the coding model for this refactor."

## Custom Providers

Add providers via `~/.pi/agent/models.json` if they speak a supported API:

```typescript
import { getModel, stream } from "@mariozechner/pi-ai";

const ollamaModel = {
  id: "llama-3.1-8b",
  name: "Llama 3.1 8B (Ollama)",
  api: "openai-completions",
  provider: "ollama",
  baseUrl: "http://localhost:11434/v1",
  reasoning: false,
  input: ["text"],
  cost: { input: 0, output: 0, cacheRead: 0, cacheWrite: 0 },
  contextWindow: 128000,
  maxTokens: 32000,
};
```

## Scoped Models

Configure a subset of models for quick cycling with `Ctrl+P`:

```
/scoped-models    -- Enable/disable models for cycling
```

Use `--models <patterns>` on the CLI for comma-separated patterns.

## Practical Workflow

A typical multi-model session:

1. Start with Gemini Flash for quick exploration (cheap, fast, huge context)
2. Switch to Claude Sonnet for implementation (best coding)
3. Bring in GPT-5.2 via oracle extension for review (strong reasoning)
4. Switch to a cheap model for boilerplate/tests

All in one session, all context preserved.

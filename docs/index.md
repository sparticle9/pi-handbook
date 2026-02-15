# Pi Coding Agent Handbook

I've been through the cycle — Cursor, Claude Code, Amp, OpenCode, Codex. I still use most of them. But when I found [pi](https://github.com/badlogic/pi-mono), something clicked. It's the agent that finally made me stop reaching for Claude Code. Not because pi does everything, but because it does so little and gets out of the way.

This handbook is what I wish existed when I started with pi. It covers the philosophy, the architecture, the extension system, the tradeoffs, and the honest gaps. It's opinionated because pi is opinionated, and that's the point.

## What's inside

The core argument for pi, the four-tool architecture, how extensions replace features other agents bake in, the no-MCP stance (and why MCP 2.0 might change the calculus), community packages like oracle and handoff, a fair comparison with Claude Code / Amp / OpenCode / Aider, and a quick start that gets you running on macOS, Linux, or Android via Termux.

12 chapters. Code snippets. Every claim sourced.

!!! note "Disclaimer"
    This is an unofficial community handbook. It is not affiliated with or endorsed by Mario Zechner or the pi project. All quotes are attributed to their original authors and linked to their sources. Pi is [MIT licensed](https://github.com/badlogic/pi-mono/blob/main/LICENSE).

## Chapters

| | Chapter | What you'll learn |
|:--|:--------|:------------------|
| 1 | [Core Philosophy](01-philosophy.md) | Why pi exists, what it deliberately omits |
| 2 | [Architecture](02-architecture.md) | The minimal core: read, write, edit, bash |
| 3 | [Extension System](03-extensions.md) | TypeScript extensions, skills, packages |
| 4 | [Session Management](04-sessions.md) | Tree-structured branching, compaction |
| 5 | [Multi-Model Freedom](05-multi-model.md) | 15+ providers, mid-session switching |
| 6 | [No MCP](06-no-mcp.md) | The CLI-first philosophy and its tradeoffs |
| 7 | [Community Extensions](07-community.md) | Oracle, handoff, sub-agents, and more |
| 8 | [Comparison](08-comparison.md) | Pi vs Claude Code vs Amp vs others |
| 9 | [Limitations](09-limitations.md) | Honest assessment of current gaps |
| 10 | [Quick Start](10-quickstart.md) | Installation, config, daily workflows |
| | [Code Snippets](snippets.md) | Concrete extension and config examples |
| | [References](references.md) | Official docs, community links, articles |

## Key references

| Resource | Link |
|:---------|:-----|
| Website | [shittycodingagent.ai](https://shittycodingagent.ai) |
| GitHub | [badlogic/pi-mono](https://github.com/badlogic/pi-mono) |
| npm | [@mariozechner/pi-coding-agent](https://www.npmjs.com/package/@mariozechner/pi-coding-agent) |
| Mario's blog | [What I learned building a minimal coding agent](https://mariozechner.at/posts/2025-11-30-pi-coding-agent/) |
| MCP vs CLI benchmark | [MCP vs CLI: Benchmarking Tools](https://mariozechner.at/posts/2025-08-15-mcp-vs-cli/) |
| Armin Ronacher | [Pi: The Minimal Agent Within OpenClaw](https://lucumr.pocoo.org/2026/1/31/pi/) |

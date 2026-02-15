# Pi Coding Agent Handbook

Agentic coding is probably the best thing that's happened since the ChatGPT moment. These tools are how individual builders ship software that used to take teams — and the more we push them, the more high-quality personal software the world gets. That matters.

I've been through the cycle — Aider, Cursor, Claude Code, Goose, Roo, Codex, Amp, OpenCode, Kilo, Kiro — the list goes on. I still use many of them daily. I'd already cut most of my Claude Code time once Amp came along, but with pi I'm feeling like I could finally stop reaching for it altogether.

Let me be honest about one thing. Claude Code is innovative. It was mindblowing for a long time and it's still pushing forward. I respect what it's done for this space. I just don't like its arrogance. That's personal, and you're welcome to disagree. Pi is the opposite — humble, minimal, and trusts you to drive. That's the energy I want to build with.

This handbook is what I wish existed when I started with pi. It covers the philosophy, the architecture, the extension system, the tradeoffs, and the honest gaps. It's opinionated because pi is opinionated, and that's the point.

I don't claim to be an expert. I'm just a builder who got hooked and wanted to write things down. If something here is wrong, outdated, or could be said better — please fix it. This is your handbook too.

## What's inside

The core argument for pi, the four-tool architecture, how extensions replace features other agents bake in, the no-MCP stance (and why MCP 2.0 might change the calculus), community packages like oracle and handoff, a fair comparison with Claude Code / Amp / OpenCode / Aider, and a quick start that gets you running on macOS, Linux, or Android via Termux.

12 chapters. Code snippets. Every claim sourced.

## Get involved

This handbook lives or dies by contributions. A typo fix, a better code example, a one-paragraph tip, a whole new chapter — it all counts. The [Limitations](09-limitations.md) page is full of gaps waiting to be filled. Every one of them is an open invitation.

If you've built something with pi — an extension, a workflow, a workaround — write it up. Someone out there is stuck on the exact problem you solved last week. We're especially interested in patterns for using pi as a general agent orchestrator — coordinating sub-agents, chaining tasks, making the build process more fun, not just more productive.

[:fontawesome-brands-github: Contribute](contributing.md){ .md-button } [:material-file-pdf-box: Download PDF](/pdf/pi-handbook.pdf){ .md-button }

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

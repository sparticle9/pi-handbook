# Pi Coding Agent Handbook

> *"There are many coding agents, but this one is mine."*

!!! note "Disclaimer"
    This is an unofficial community handbook. It is not affiliated with or endorsed by Mario Zechner or the pi project. All quotes are attributed to their original authors and linked to their sources. Pi is [MIT licensed](https://github.com/badlogic/pi-mono/blob/main/LICENSE).

---

[Pi](https://github.com/badlogic/pi-mono) is a minimal terminal coding agent by Mario Zechner. It is the engine behind [OpenClaw](https://github.com/openclaw/openclaw), used daily by notable developers including Armin Ronacher (creator of Flask/Ruff) and Peter Steinberger (founder of PSPDFKit).

Pi runs anywhere Node.js runs — macOS, Linux, Windows, and even Android via Termux. Copy your `models.json` to a new device, install pi, and you're ready to go. Extensions and skills install via CLI afterwards.

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

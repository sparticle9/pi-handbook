# Pi Coding Agent Handbook

I've been through the cycle -- Cursor, Claude Code, Amp, OpenCode, Codex. I still use most of them. But when I found [pi](https://github.com/badlogic/pi-mono), something clicked. It's the agent that finally made me stop reaching for Claude Code. Not because pi does everything, but because it does so little and gets out of the way.

This handbook is what I wish existed when I started with pi. It covers the philosophy, the architecture, the extension system, the tradeoffs, and the honest gaps. It's opinionated because pi is opinionated, and that's the point.

**[Read the handbook →](https://pi-handbook.whatsinfor.me)**

---

## What's inside

The core argument for pi, the four-tool architecture, how extensions replace features other agents bake in, the no-MCP stance (and why MCP 2.0 might change the calculus), community packages like oracle and handoff, a fair comparison with Claude Code / Amp / OpenCode / Aider, and a quick start that gets you running on macOS, Linux, or Android via Termux.

12 chapters. Code snippets. Every claim sourced.

## Contributing

If you've built something with pi -- an extension, a workflow, a workaround for one of its gaps -- write it up and open a PR. The [Limitations](https://pi-handbook.whatsinfor.me/09-limitations/) page is a good place to start: every gap documented there is an invitation.

Fork, edit markdown in `docs/`, submit. That's it.

## Local dev

```bash
pip install mkdocs-material
mkdocs serve
```

## Custom domain

Served at `pi-handbook.whatsinfor.me`. Forking for your own use:

1. Update `site_url` in `mkdocs.yml`
2. Update `docs/CNAME`
3. CNAME DNS record → `YOUR_USERNAME.github.io`

## Disclaimer

Unofficial. Not affiliated with Mario Zechner or the pi project. All quotes attributed and linked. Pi is [MIT licensed](https://github.com/badlogic/pi-mono/blob/main/LICENSE). Content here is [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/).

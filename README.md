# Pi Coding Agent Handbook

An unofficial community handbook for [pi](https://github.com/badlogic/pi-mono), the minimal terminal coding agent by Mario Zechner.

## Read Online

**[pi-handbook.whatsinfor.me →](https://pi-handbook.whatsinfor.me)**

## Contributing — We Need You

This handbook is for the community, by the community. If you use pi and have something to share, please contribute.

**What we're looking for:**

- 🧩 New extensions or skills you've built — write them up, share the code
- 📝 Workflow tips, patterns, or tricks that made you more productive
- 🔍 Corrections, updates, or clarifications to existing content
- 🆚 Comparison notes if you've used other agents alongside pi
- 📸 Screenshots, terminal recordings, or diagrams
- 🌍 Translations

**How to contribute:**

1. Fork this repo
2. Edit or add markdown files in `docs/`
3. Open a PR with a short description of what you changed and why

No contribution is too small. A typo fix, a better code example, a one-paragraph tip — it all helps fellow agentic coding addicts get more out of pi.

If you're not sure where to start, check the [Limitations](https://pi-handbook.whatsinfor.me/09-limitations/) page — building solutions for those gaps and documenting them here is the highest-impact work.

## What's Covered

- Core philosophy: why pi exists and what it deliberately omits
- Architecture: four tools, four modes, context engineering
- Extension system: TypeScript extensions, skills, packages
- Session management: tree-structured branching, compaction
- Multi-model freedom: 15+ providers, mid-session switching
- The no-MCP stance: CLI-first philosophy, benchmarks, and the MCP 2.0 counter-argument
- Community extensions: oracle, handoff, sub-agents, model-switch
- Honest comparison with Claude Code, Amp, OpenCode, Aider
- Current limitations and gaps
- Quick start guide including Android/Termux setup

## Local Development

```bash
pip install mkdocs-material
mkdocs serve
```

Open `http://localhost:8000`.

## Custom Domain Setup

This site is served at `pi-handbook.whatsinfor.me`. If you're forking for your own use:

1. Update `site_url` in `mkdocs.yml`
2. Update `docs/CNAME` with your domain
3. Add a CNAME DNS record: `pi-handbook` → `YOUR_USERNAME.github.io`

## Disclaimer

This handbook is not affiliated with or endorsed by Mario Zechner or the pi project. All quotes are attributed to their original authors and linked to their sources. Pi is [MIT licensed](https://github.com/badlogic/pi-mono/blob/main/LICENSE).

## License

Content is licensed under [CC BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/).

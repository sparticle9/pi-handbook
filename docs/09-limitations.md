# Limitations and Gaps

An honest assessment of pi's current drawbacks. These are real tradeoffs, not dealbreakers -- but the team should be aware of them.

## No Native Cross-Session References

You cannot `@mention` another session from within a session. Amp's thread mentioning and "Amp Now Reads Threads" feature has no equivalent. Workarounds exist (read the JSONL file, build a `/recall` extension), but it's not first-class.

## No Built-in Permission System

YOLO mode means the agent executes everything without asking. For teams working on production systems, this requires discipline:

- Run in a container or sandboxed environment
- Use a dedicated user account (`useradd claude`)
- Build a permission gate extension (examples exist)
- Or install the community `plan-mode` extension for read-only exploration

From r/ClaudeCode:

> It only supports yolo mode, which is honestly fine but if you want security just use linux and `useradd claude` and use that so it can't access your own home directory.

## No IDE Integration

Pi is terminal-only. There's no VS Code extension, no JetBrains plugin, no native GUI. The closest alternatives:

- Emacs mode (`dnouri/pi-coding-agent`) -- community-built, works well
- RPC mode for building custom integrations
- SDK for embedding in your own apps

If your team relies heavily on IDE features (inline diffs, gutter annotations, hover previews), pi won't replace that workflow.

## Steeper Learning Curve for Non-Terminal Users

Pi assumes comfort with:
- Terminal workflows
- Shell commands and Unix tools
- TypeScript (for writing extensions)
- Managing API keys and provider configuration

There's no guided onboarding, no wizard, no "just works" setup. You need to configure providers, understand the session model, and learn the commands.

## Extension Quality Varies

Community extensions are maintained by individuals. Unlike Claude Code or Amp where features are tested by a company:

- Extensions may break on pi updates
- No formal review process
- Documentation quality varies
- Some extensions are experimental

Always test extensions in a non-critical project first.

## No Built-in Eval/Testing Framework

Unlike Mastra (which has `runEvals` and scorers), pi has no formal way to test agent behavior or tool quality. Testing is manual -- you use the extension and see if it works. For teams that need CI-ready verification of agent behavior, this is a gap.

## Windows Support is Second-Class

From r/ClaudeCode:

> I recommend ditching windows. Saved me my sanity. Agents are constantly doing command syntax mistakes on windows.

Pi works on Windows but the experience is rougher. Linux and macOS are the primary targets.

## No Server-Side Session Management

Sessions are local JSONL files. There's no cloud sync, no team-shared session history, no server-side thread management like Amp. For distributed teams, this means:

- Sessions live on individual machines
- Sharing requires `/export` to HTML or `/share` to GitHub gist
- No real-time collaboration on sessions

## No Native Long-Term Memory

Pi doesn't have built-in vector search, RAG, or cross-session memory. The alternatives:

- `AGENTS.md` for project-level persistent instructions
- `memory-mode` extension to save learnings to AGENTS.md
- Build a RAG extension (the hooks exist, but you build it yourself)
- Session branching partially compensates (you can revisit old decisions)

From Ewald Benes:

> Pi's AGENTS.md for project rules, combined with its session branching, handles 90% of my "memory" needs without the overhead of a separate manager.

## Small (but Growing) Ecosystem

Pi has 1.2M+ weekly downloads and an active Discord, but the extension ecosystem is still small compared to VS Code or even Claude Code's community. You may need to build extensions yourself rather than finding pre-built ones.

## The "Un-Google-able" Name

Mario chose the name deliberately to avoid users and issues. It worked. Searching for "pi coding agent" returns results about Raspberry Pi, the number pi, and various unrelated projects. Always search for "pi-coding-agent" or "shittycodingagent" or "badlogic/pi-mono".

## No Cloud Workspace

Pi is entirely local. There's no cloud-hosted workspace, no web UI you can open from any browser, no always-on server-side sessions. Claude Code has a web interface. Amp's threads live on their servers. Pi's sessions live on your machine.

This means:
- You can't start a session on your laptop and continue it from your phone's browser
- There's no team dashboard showing active sessions
- No "always running" agent that works while your machine is off

Pi does run on Android via Termux (see [10-quickstart.md](./10-quickstart.md)), and you can copy your `~/.pi/agent/` config between machines. But there's no sync layer -- it's manual file transfer. For teams that want cloud-native agent workflows, this is a real gap compared to Amp or Claude Code's web offerings.

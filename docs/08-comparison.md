# Comparison with Other Agents

## Overview Matrix

| Feature | Pi | Claude Code | Amp | OpenCode | Aider |
|---------|-----|-------------|-----|----------|-------|
| Core tools | 4 | 15+ | ~10 | 10+ | 2 (read/edit) |
| System prompt size | Minimal | Large | Medium | Medium | Minimal |
| MCP support | No (by design) | Yes | Yes | Yes | No |
| Sub-agents | Via extension | Built-in | Built-in (Oracle) | Built-in | No |
| Plan mode | Via extension | Built-in | Built-in | Built-in | No |
| Session branching | Tree structure | Linear | Threads + fork | Linear | No |
| Multi-model | 15+ providers | Anthropic only | Anthropic + OpenAI | Multi-provider | Multi-provider |
| Mid-session switch | Yes | No | No | Yes | Yes |
| Extension system | TypeScript + skills | CLAUDE.md only | Toolboxes | Custom tools | No |
| Self-extending | Yes (hot-reload) | No | No | No | No |
| Context handoff | Cross-provider | N/A | N/A | Limited | Limited |
| YOLO mode | Default | Opt-in | Opt-in | Configurable | No |
| Open source | MIT | No | No | MIT | Apache 2.0 |
| Price | Pay-per-token or subscription | Subscription | Subscription | Pay-per-token | Pay-per-token |

## Pi vs Claude Code

The most common migration path. Key differences:

**Why people switch:**
- Token efficiency: "My token limits last 10x longer" (Ewald Benes)
- No hidden context injection
- No flickering TUI
- System prompt doesn't change on every release
- Multi-model support
- Session branching

**What you lose:**
- Built-in permission system
- Native MCP support
- Anthropic-optimized tool calling
- Larger community and ecosystem
- Enterprise features (SSO, audit logs)

From r/ClaudeCode:

> The selling point of pi is its simplicity. It lacks a lot of fancy features, but that means you get the smallest starting context out there, and you don't pay for things like 'plan mode' or 'todo' -- you just have to do the crazy complicated thing of telling it: `make a plan` if you want to plan something.

## Pi vs Amp

Amp is the closest competitor in philosophy (focused threads, quality over features).

**Amp advantages:**
- Oracle is deeply integrated (auto-invoked, optimized token flow)
- Handoff auto-generates focused prompts
- Thread mentioning (`@thread-id`)
- Thread Map for visual navigation
- Server-side thread management
- Polished VS Code extension

**Pi advantages:**
- Full multi-model freedom (Amp locks you to Anthropic + OpenAI)
- Self-extending agent (Amp can't build its own tools)
- Open source (MIT)
- No vendor lock-in
- Smaller context footprint
- Community-driven extension ecosystem

## Pi vs OpenCode

OpenCode (by SST) takes the "everything" approach.

**OpenCode advantages:**
- Built-in MCP support
- LSP integration (semantic code intelligence)
- Built-in web fetch tool
- Go binary (no Node.js dependency)

**Pi advantages:**
- Smaller core, less context overhead
- Extension system is far more powerful
- Session branching (OpenCode is linear)
- Cross-provider context handoff
- Self-extending capability

## Pi vs Aider

Aider is even more minimal than pi -- it only reads and edits code.

**Aider advantages:**
- Git-native (auto-commits, diff-based editing)
- Repository map for large codebases
- No bash tool (can't accidentally break things)

**Pi advantages:**
- Bash tool (can run tests, install deps, debug)
- Extension system
- Session branching
- TUI with rich rendering
- Multi-mode (interactive, print, RPC, SDK)

## The Armin Ronacher Perspective

From his blog post comparing Pi and Amp:

> Pi is interesting to me because of two main reasons. First of all, it has a tiny core. It has the shortest system prompt of any agent that I'm aware of and it only has four tools. The second thing is that it makes up for its tiny core by providing an extension system that also allows extensions to persist state into sessions, which is incredibly powerful.

> And a little bonus: Pi itself is written like excellent software. It doesn't flicker, it doesn't consume a lot of memory, it doesn't randomly break, it is very reliable and it is written by someone who takes great care of what goes into the software.

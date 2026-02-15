# Core Philosophy

Pi's design is guided by a single principle: **if I don't need it, it won't be built.**

Mario Zechner built pi because existing agents (Claude Code, Cursor, Codex) kept adding features he didn't use, injecting hidden context he couldn't inspect, and changing behavior on every release. Pi is his answer: a coding agent that is aggressively minimal, fully transparent, and extensible by the user -- not the vendor.

## The Minimal Core

Pi ships with exactly four tools: `read`, `write`, `edit`, `bash`. That's it. No plan mode, no sub-agents, no MCP, no permission popups, no built-in to-dos, no background bash.

From the website:

> Pi is aggressively extensible so it doesn't have to dictate your workflow. Features that other tools bake in can be built with extensions, skills, or installed from third-party pi packages. This keeps the core minimal while letting you shape pi to fit how you work.

## Context Engineering as First Principle

Pi has the shortest system prompt of any coding agent. This matters because every token in the system prompt competes with your actual code and instructions for the model's attention.

From Ewald Benes (r/ClaudeCode):

> By default, tools like Claude Code inject a massive amount of hidden text before your prompt even begins. This "bloat" burns through thousands of tokens before you've typed a single word. The creators of these tools make dozens of architectural decisions for you -- whether you want them or not -- which often leads to the LLM becoming "distracted" by its own internal instructions.

Pi's approach: give the model the minimum it needs, and let the user control what else goes in via AGENTS.md, SYSTEM.md, skills, and extensions.

## Primitives, Not Features

Instead of building plan mode, pi gives you extensions. Instead of building sub-agents, pi gives you extensions. Instead of building MCP support, pi gives you bash + skills.

From Armin Ronacher:

> This is not a lazy omission. This is from the philosophy of how Pi works. Pi's entire idea is that if you want the agent to do something that it doesn't do yet, you don't go and download an extension or a skill or something like this. You ask the agent to extend itself. It celebrates the idea of code writing and running code.

## Software That Builds Itself

Pi ships with its own documentation and extension examples that the agent can read. This means you can literally tell pi: "Build me an extension that does X" and it will read the docs, write the extension, hot-reload it, test it, and iterate until it works.

From Armin Ronacher:

> It also ships with documentation and examples that the agent itself can use to extend itself. Even better: sessions in Pi are trees. You can branch and navigate within a session which opens up all kinds of interesting opportunities such as enabling workflows for making a side-quest to fix a broken agent tool without wasting context in the main session.

## The "What We Didn't Build" List

| Feature | Pi's stance | Alternative |
|---------|-------------|-------------|
| MCP | Will not support | CLI tools + READMEs, or mcporter |
| Sub-agents | Not built-in | Extensions, tmux, or community packages |
| Plan mode | Not built-in | Just tell it "make a plan", or install an extension |
| Permission popups | Not built-in | Run in container, or build confirmation extension |
| To-do tracking | Not built-in | Use TODO.md, or build a tool extension |
| Background bash | Not built-in | Use tmux for full observability |

## YOLO by Default

Pi runs in "YOLO mode" -- it executes tools without asking for permission. This is a deliberate choice. Mario's argument: if the agent can write and run code, security theater (confirmation dialogs) doesn't actually protect you. If you want safety, use a container or build a real permission gate via extensions.

From the blog post:

> If you look at the security measures in other coding agents, they're mostly security theater. As soon as your agent can write code and run code, it's pretty much game over.

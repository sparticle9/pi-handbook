# No MCP: The CLI-First Philosophy

This is pi's most controversial and deliberate design decision.

> "pi does not and will not support MCP."
> -- Mario Zechner

## The Problem with MCP

Popular MCP servers dump their entire tool descriptions into your context on every session:

| MCP Server | Tools | Token cost |
|------------|-------|------------|
| Playwright MCP | 21 tools | ~13,700 tokens |
| Chrome DevTools MCP | 26 tools | ~18,000 tokens |

That's 7-9% of your context window gone before you start working. Most of those tools won't be used in a given session.

Additionally, many MCP servers are thin wrappers around CLI tools that already exist:

> Just like a lot of meetings could have been emails, a lot of MCPs could have been CLI invocations. For example, there's the GitHub MCP Server, which reimplements functionality that's already available in the GitHub CLI. There's little benefit of using that MCP compared to telling your coding agent to use its shell tool to run the GitHub CLI directly.

## The CLI Alternative

Pi's approach: build CLI tools with README files.

1. The agent reads the README only when it needs the tool (progressive disclosure)
2. Token cost is paid only on demand
3. CLI tools are composable (pipe outputs, chain commands)
4. CLI tools are easy to extend (just add another script)
5. LLMs already know how to use CLI tools from training data

Example -- adding web search to pi via a skill:

```markdown
# SKILL.md
name: web-search
description: Search the web using the search CLI tool

## Usage
Run `search "your query"` to search the web.
Run `search --fetch <url>` to read a page.
See the README at ~/agent-tools/search/README.md for full options.
```

Mario maintains a collection of CLI tools at `github.com/badlogic/agent-tools`.

## The Benchmark

Mario ran a formal evaluation comparing MCP vs CLI for coding agents (August 2025):

**Setup:** terminalcp (his tmux alternative) as both MCP server and CLI, compared against tmux and screen. Three tasks, 10 runs each, using Claude Code.

**Results:**

| Metric | terminalcp MCP | terminalcp CLI | tmux | screen |
|--------|---------------|----------------|------|--------|
| Success rate | 100% | 100% | 100% | 67% |
| Total time | 51 min | 66 min | ~60 min | ~70 min |
| Total cost | $19.45 | $19.95 | $22 | $22+ |

**Key findings:**

- MCP vs CLI is a wash on success rates
- MCP was 23% faster due to bypassing Claude Code's security checks on bash
- Tool design and documentation quality matter far more than the protocol
- For complex tasks, well-designed tools beat standard tools by 39% on cost

**Conclusion:**

> Maybe instead of arguing about MCP vs CLI, we should start building better tools. The protocol is just plumbing. What matters is whether your tool helps or hinders the agent's ability to complete tasks.

> If you're building a tool from scratch and your users already have a shell tool available, just make a good CLI. It's simpler and more portable. Plus, the output of your CLI can be further filtered and massaged just by piping it into another CLI tool, which can increase token efficiency at the cost of additional instructions. That's not possible with MCPs.

## If You Must Use MCP

Peter Steinberger's [mcporter](https://github.com/nicobailon/mcporter) wraps MCP servers as CLI tools, giving you the best of both worlds. OpenClaw uses this approach.

## The Deeper Argument

From Armin Ronacher:

> If you consider how MCP works, on most model providers, tools for MCP, like any tool for the LLM, need to be loaded into the system context or the tool section thereof on session start. That makes it very hard to impossible to fully reload what tools can do without trashing the complete cache or confusing the AI about how prior invocations work differently.

Pi's skill system avoids this entirely. Skills are loaded into context only when the agent determines they're relevant, and they can be unloaded when no longer needed. This is fundamentally incompatible with how MCP tools work.

## Community Perspective

From r/ClaudeAI:

> Why use MCP in subagents when they can use CLI with 0 tool context overhead?

From Cobus Greyling:

> What if the best interface for AI Agents is not a new protocol at all? What if it is the command line -- the same interface that has been powering software for over fifty years?

The CLI-over-MCP movement is growing, but pi is the only major agent that has made it a first-class architectural decision.

## The Counter-Argument: MCP Is Evolving

Pi's no-MCP stance is well-reasoned for today's landscape, but it's worth acknowledging that MCP is not standing still.

**MCP 2.0** introduces significant improvements that address some of pi's criticisms:

- **Streamable HTTP transport** -- Replacing stdio, enabling remote multi-tenant tool servers
- **OAuth 2.1 auth flows** -- Making enterprise adoption realistic
- **Elicitation** -- The server can ask the agent for more info mid-execution, enabling richer orchestration
- **Tool annotations** (`readOnlyHint`, `destructiveHint`) -- Letting agents reason about safety before calling tools, which could enable smarter tool selection and reduce the "dump all tools into context" problem

**Governance shift:** Anthropic has donated MCP to the Agentic AI Foundation, which will be managed by the Linux Foundation. This moves MCP from a single-vendor protocol to an open, community-governed standard -- similar to how Kubernetes moved from Google to the CNCF. With broader governance, MCP is likely to evolve faster and address more real-world pain points.

**What MCP supporters would argue:**

- The context pollution problem is solvable with better tool selection and lazy loading (MCP 2.0's tool annotations are a step toward this)
- CLI tools break across platforms, have version dependencies, and sometimes lack documentation -- MCP provides a structured contract
- Stateful tools (database connections, browser sessions, long-running processes) are inherently easier with MCP's persistent server model than with CLI invocations
- As MCP becomes an open standard under the Linux Foundation, the ecosystem will mature and the "badly designed wrapper" problem will diminish
- Code execution MCPs (Armin Ronacher's "ubertool" pattern) can expose a single tool that accepts code, combining MCP's statefulness with CLI's composability

**The balanced view:** Pi's CLI-first approach is demonstrably effective for coding agents with a bash tool. The benchmarks prove it. But MCP and CLI are solving different layers of the problem, and as MCP 2.0 matures under open governance, the gap may narrow. Pi's philosophy remains valid -- progressive disclosure and minimal context are good engineering regardless of protocol -- but declaring "no MCP ever" is a bet that the protocol's evolution won't produce something genuinely better than CLI + README for the use cases pi cares about. Time will tell.

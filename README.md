# Agent Skills

A collection of [agentskills.io](https://agentskills.io)-compatible agent skills for AI coding tools.

Verified against real library APIs. Works with Cursor, Claude Code, Codex CLI, Gemini CLI, and any tool supporting SKILL.md.

## Skills

### [fastmcp](./fastmcp/SKILL.md)

Production patterns for FastMCP Python MCP servers.

**Covers:** tool schema design, multi-operation tools, pre-formatted output, Context usage, middleware, lifespan/startup/shutdown, partial failure handling, running and deploying, async patterns, in-process testing with `fastmcp.Client`, and common mistakes.

**Verified against:** FastMCP 3.2.2  
**Structural validation:** 97.1% (agentskills.io spec)  
**License:** Apache-2.0

#### Install

```bash
# Cursor
npx add-skill https://github.com/sharsoor/skills --skill fastmcp -a cursor -y

# Claude Code
npx add-skill https://github.com/sharsoor/skills --skill fastmcp -a claude-code -y
```

#### Why this skill exists

Without it, LLMs confidently hallucinate FastMCP APIs:

| Question | Without skill | With skill |
|---|---|---|
| "How do I initialize state at startup?" | Uses `server.state.pool = ...` (AttributeError) | Uses `yield {"pool": pool}` → `ctx.lifespan_context` |
| "How do I add startup/shutdown hooks?" | Uses `@mcp.on_startup` (doesn't exist) | Uses `lifespan=` parameter |
| "How do I access tool args in middleware?" | Uses `context.name`, `context.arguments` (AttributeError) | Uses `context.message.name`, `context.message.arguments` |

---

## Install any skill

```bash
npx add-skill https://github.com/sharsoor/skills --skill <skill-name> -a cursor -y
```

## License

Apache-2.0

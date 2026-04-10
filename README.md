# SurfAgent Skills

Canonical public skills catalog for [SurfAgent](https://surfagent.app).

This repo exists for one job: reusable skill instructions that make AI agents operate the SurfAgent browser better.

If you are new to SurfAgent, do not start by cloning every repo.

Start with:
1. install the SurfAgent app
2. connect `surfagent-mcp`
3. add skills from this repo only when you want better workflows or operating discipline

Docs:
- <https://github.com/surfagentapp/surfagent-docs/blob/main/docs/start-here.md>
- <https://github.com/surfagentapp/surfagent-docs/blob/main/docs/mcp-server.md>
- <https://github.com/surfagentapp/surfagent-docs/blob/main/docs/skills-and-adapters.md>

## What skills are

Skills are not the browser tool layer.

They are instructions and operating patterns that help an AI agent:
- choose the right tool path
- avoid dumb browser mistakes
- use fewer tokens
- gather proof before claiming success
- handle site-specific workflows more reliably

If you want raw browser control, use `surfagent-mcp`.
If you want site-native verbs, use an adapter repo.
If you want the agent to operate better, use skills.

## Recommended install flow

### ClawHub
```bash
npx clawhub@latest install surfagent-browser
npx clawhub@latest install surfagent-perception
```

Add more only when you need them.

### Manual use
Browse the folders in this repo and pull in the skills that match your workflow.

## Current skills

### `surfagent-browser`
Core browser skill for controlling the SurfAgent browser.

### `surfagent-perception`
Page understanding and perception support, including scene summaries and state-aware observation.

### `browser-operations`
Execution discipline for real browser work: tab hygiene, proof rules, tool-choice ladder, short autonomy loops, and token efficiency.

### `gmail`
Gmail workflow skill for compose, send, Sent verification, blockers, and proof-aware execution.

### `surfagent-mcp-selection`
Decision guide for when to use perception, adapters, MCP, or raw browser control.

### `telegram-web`
Telegram Web workflow skill for chat state, composer flows, send verification, and adapter-first execution.

### `discord`
Discord workflow skill for route-aware state checks, blocker handling, extraction-first execution, and adapter-first decisions.

### `x`
X-specific workflow skill for posting, extraction, blocker handling, and adapter-first execution.

### `tradingview`
TradingView workflow skill for charts, symbols, timeframes, alerts, and visual verification.

## Repo map

- `surfagent-docs` = canonical public docs
- `surfagent-skills` = canonical public skills catalog
- `surfagent-skill` = legacy compatibility repo for older install paths
- adapter repos = site-specific tool surfaces like Gmail, Telegram Web, X, TradingView, and Discord

## What most users actually need

Usually:
- the SurfAgent app
- `surfagent-mcp`
- maybe 1 or 2 skills

Not usually:
- every adapter repo
- every skill
- the legacy `surfagent-skill` repo

## Requirements

- [SurfAgent](https://surfagent.app) running on your desktop
- SurfAgent daemon available
- a client that can use skills and/or MCP

## License

MIT-0

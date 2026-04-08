# SurfAgent Skills

Canonical public skills repo for [SurfAgent](https://surfagent.app) — the desktop AI browser agent.

Install via [ClawHub](https://clawhub.ai):

```bash
npx clawhub@latest install surfagent-browser
npx clawhub@latest install surfagent-perception
```

## Skills

### 🌐 [surfagent-browser](./surfagent-browser/)
Control a real Chrome browser from your AI agent. Navigate, click, type, fill forms, extract content, manage tabs, and automate workflows.

### 👁️ [surfagent-perception](./surfagent-perception/)
Agent vision for web pages. Scene summaries, attention-ranked elements, annotated screenshots with numbered bounding boxes, and state diffing.

### 🧭 [browser-operations](./browser-operations/)
Core browser operating discipline for SurfAgent, including tab hygiene, tool-choice ladder, token efficiency, and proof rules.

### ✉️ [gmail](./gmail/)
Gmail-specific operating skill covering compose, send, Sent verification, blockers, and when to prefer the Gmail adapter over raw browser control.

### 🧩 [surfagent-mcp-selection](./surfagent-mcp-selection/)
Tool-selection guide for choosing between perception, platform adapters, MCP, and raw browser control.

### 𝕏 [x](./x/)
X/Twitter-specific workflow skill with proof rules, blocker handling, and adapter-first guidance.

### 📈 [tradingview](./tradingview/)
TradingView-specific chart workflow skill for symbols, timeframes, visual proof, alerts, drawings, and adapter-first usage.

## Repo Ownership

- **`surfagent-skills`**: canonical public skills repo
- **`surfagent-docs`**: canonical public docs repo
- **`surfagent-skill`**: legacy compatibility repo for older install paths only

## Requirements

- [SurfAgent](https://surfagent.app) running on your desktop (Windows)
- Daemon API on port 7201
- Managed Chrome on port 9222

## License

MIT-0

---
name: browser-operations
description: Core browser operations skill for SurfAgent and similar browser agents, covering tab discipline, perception-first execution, human-like driving, proof rules, token-efficient fallback patterns, and platform-by-platform operating mode selection.
version: 1.2.0
metadata:
  openclaw:
    homepage: https://surfagent.app
    emoji: "🧭"
---

# Browser Operations

> The core skill. Use this before any site-specific skill.

This file teaches the universal rules for driving a real browser without making a mess, wasting tokens, or lying about success.

## 1. What this skill is for

Use this skill for:
- browser hygiene
- tab hygiene
- perception-first workflow
- autonomy loops
- human-like interaction patterns
- token-efficiency rules
- generic fallback and recovery patterns
- proof rules

Use a platform skill after this one when you are on a known site like Gmail, X, Discord, or GitHub.

## 2. Platform operating matrix

Visual-first is not a religion. Pick the operating mode that fits the surface.

### Default modes by platform

| Platform | Default mode | Why |
| --- | --- | --- |
| X | visual-first hybrid | Visible account, composer, thread, and post state often beats partial extraction |
| Telegram Web | visual-first hybrid | Live chat state is easier to trust on screen than through clever route tricks |
| Discord | visual-first hybrid | SPA routing, gates, and composer state drift make screenshots and visible surface checks important |
| Gmail | state-first hybrid | Deterministic task runners and mailbox/composer state are stronger, then use visual proof for send/render confirmation |
| TradingView | state-first | Chart state, symbols, intervals, indicators, and drawings are better read from adapter/state tools than from screenshots alone |

### How to choose fast

- **API-first** when a real API or strong native state layer exists
- **task-runner/state-first** when the UI is repeatable and the adapter already knows the surface
- **visual-first** when the page is hydration-heavy, account-sensitive, or visibly more truthful than extraction
- **raw browser control** only as the fallback or escape hatch

Rule: if the important truth is already visible on screen, use that. If the important truth lives in structured state, use that instead.

## 3. Non-negotiables

1. One active work tab per target site unless a second tab is clearly justified.
2. Reuse a healthy tab before opening a new one.
3. Perceive state before acting.
4. Verify visible results after acting.
5. Prefer low-token state and perception tools over giant raw reads.
6. Do not claim success from an attempted click or type alone.
7. If retries create tab sprawl, stop and clean up before continuing.

## 4. Tool selection ladder

Default order:
1. perception or state layer first
2. platform adapter second
3. MCP server when available and stronger for the job
4. raw browser actions only as fallback

Interpretation:
- Start with the cheapest reliable understanding layer.
- Use site-specific abstractions when they reduce error rate or token burn.
- Fall back to raw browser control only when the higher-level tools are missing or insufficient.

## 5. Browser hygiene

Before work:
- inspect open tabs
- choose the tab you will operate
- confirm URL, title, and whether it is already logged in

During work:
- keep a clear tab budget
- avoid duplicate retries on the same site
- if a tab becomes stale or broken, hand off to one fresh tab and close the stale one

After work:
- close throwaway tabs
- leave the browser in a clean, explainable state

## 6. Tab hygiene

Healthy pattern:
- one site, one active tab
- one deliberate exception if comparison, auth handoff, or reference context is required

Unhealthy pattern:
- multiple duplicate tabs from retries
- stale tabs left open after handoff
- guessing which tab is live instead of checking

If tab state is unclear, stop and re-enumerate before acting.

## 7. Perception-first loop

Use this loop by default:
1. perceive or inspect state
2. choose the next action
3. act once
4. diff or verify what changed
5. repeat only if the page state supports the next step

Ask after every action:
- what changed?
- did the intended element update?
- did a blocker appear?
- is the page now in a different mode?

If the surface is visually dense, stateful, or contradictory, escalate to a screenshot or visual snapshot early.

Examples where visual confirmation should happen fast:
- account switchers
- modals and drawers
- multi-mode composers
- community or group posting surfaces
- pages where DOM extraction and visible state disagree

Rule: do not keep arguing with partial extraction when one screenshot can settle the page state.

## 8. Autonomy layer

The autonomy layer should be small and disciplined.

Use short plan-act-verify cycles:
- identify the immediate goal
- take one concrete action
- verify the result
- update the local plan from evidence, not hope

Do not queue five blind actions in a row on a dynamic site.

## 9. Human-like driving

Drive like a careful operator, not a broken macro:
- prefer deliberate clicks over frantic retries
- wait for visible state changes, not arbitrary long sleeps
- scroll only when needed
- type into the intended field once it is confirmed focused or targeted
- avoid racing modals, redirects, or page transitions

Human-like does not mean fake random noise. It means paced, state-aware interaction.

## 10. Token-efficiency rules

Always prefer:
- structured state over full DOM dumps
- perception summaries over giant page reads
- targeted evaluate calls over broad scraping
- delta checks over repeated full snapshots
- platform adapters and MCPs when they compress the task safely

Avoid:
- repeated giant browser reads
- dumping full HTML when only one field matters
- re-reading unchanged screens
- broad selector fishing when the page can be classified first

## 11. Fallback ladder

If the ideal path fails:
1. verify page state again
2. take a screenshot or visual snapshot if the surface is ambiguous
3. retry with a more precise selector or ref
4. switch to site adapter or MCP if available
5. recover page state, refocus, dismiss blocker, or reload
6. move to one fresh tab if the current one is poisoned
7. escalate to a platform skill or ask for human input only when the blocker is real

## 12. Common blockers

Watch for:
- cookie banners
- consent modals
- auth walls
- captcha or verification gates
- stale session pages
- hidden compose or modal state
- frozen or half-loaded tabs

For each blocker:
- name it plainly
- confirm it is real
- say whether it is auto-resolvable, retryable, or human-blocked

## 13. Proof rules

Success requires visible evidence.

Good proof usually includes:
- correct page or modal is open
- intended field values are present
- intended action completed
- resulting state is visible in UI
- follow-up render or post-action state confirms success

Examples:
- sent email: compose populated, send confirmation shown, sent message renders correctly
- login: auth state changed, destination page loaded, account identity visible
- posted message: composer cleared or closed, new post visible in timeline or thread
- saved setting: toggle/value changed and persists on reload or revisiting

Bad proof:
- click returned ok
- selector existed
- no error was thrown
- assistant assumes the action worked

## 14. When to use platform skills

Use a platform skill when the site has:
- known brittle selectors
- special editor behavior
- auth or trust-safety edge cases
- better adapters or MCP tools
- site-specific proof requirements

Priority first set:
- Gmail
- X/Twitter
- Telegram Web
- Discord
- TradingView

## 15. Minimal operating checklist

Before claiming done, confirm:
- right tab
- right account
- right page state
- action executed
- visible result verified
- spare tabs cleaned up

If a page was complex enough to confuse state during the run, add a short note to the platform skill or state map afterward so the next agent does not have to rediscover it.

## 16. Output contract for agents

When reporting progress:
- say what changed, not what you hoped would happen
- call out blockers immediately
- distinguish attempted from verified
- keep the summary short and evidence-based

## 17. Relationship to other docs

This is the universal browser brain.

Pair it with:
- platform skills for site-specific behavior
- MCP or adapter docs for capability selection
- runtime wrappers for Claude Code, Codex, Cursor, Hermes, and others

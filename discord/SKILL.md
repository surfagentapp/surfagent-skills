---
name: discord
description: Discord platform skill for SurfAgent, covering route-aware state checks, extraction-first workflows, visual-first ambiguity handling, blockers, and when to use the Discord adapter over raw browser control.
version: 1.1.0
metadata:
  openclaw:
    homepage: https://surfagent.app
    emoji: "💬"
---

# Discord

> Discord-specific operating skill. Use this with the core `browser-operations` skill.

This skill teaches agents how to work Discord without pretending the surface is stable when it is not.

## 1. Use this skill for

- route-aware Discord state checks
- visible channel and message extraction
- login and gate detection
- forum and thread surface recognition
- blocker-aware workflow decisions
- deciding when to use the Discord adapter instead of raw browser control

## 2. Default operating mode

Discord is a **visual-first hybrid** surface.

That means:
- use Discord adapter state and extraction tools first
- trust screenshots and visible surface classification quickly when the route or pane is ambiguous
- avoid acting from weak partial extraction when the screen itself answers the question faster

Visual-first does **not** mean doing everything by raw clicking. It means visible guild, channel, thread, gate, and composer state often settles ambiguity better than clever selector theory.

## 3. Tool preference

Use this order:
1. Discord adapter state tools
2. Discord adapter extraction tools
3. screenshot or visual confirmation when the surface is ambiguous
4. targeted browser evaluation only when needed
5. raw generic browser actions as fallback

Discord punishes selector guessing. Use site-aware tools first.

## 4. Discord truths that matter

Discord is a dynamic SPA with moving surface state.

It has:
- route changes that do not behave like normal page loads
- login, verification, and hCaptcha gates
- channel/thread/forum layouts that shift by context
- unstable internal structure that punishes brittle selectors

Important: login or verification state is a real outcome, not an error to hand-wave away.

## 5. Core Discord loop

Default loop:
1. confirm Discord state
2. classify the surface you are actually on
3. detect blockers before acting
4. extract visible structured state
5. choose one deliberate next action
6. verify the visible result

Do not blast clicks into Discord because the tab "looks about right".

## 6. Proof rules

For Discord, success usually requires:
1. correct server/channel/thread surface is visible
2. login or gate state is explicitly known
3. extracted state matches the visible UI
4. post-action state visibly changed in the expected way

Trust order when signals conflict:
1. visible guild/channel/thread surface and screenshot
2. visible composer or gate state
3. Discord adapter extraction/state
4. click receipts and generic success strings

Do not claim success from only:
- a selector match
- a click returning ok
- the absence of an error
- stale content that may belong to a different route

## 7. When to use the Discord adapter

Prefer the Discord adapter for:
- opening Discord in the managed browser
- route-aware page state detection
- login/register/hCaptcha gate detection
- visible message extraction
- visible channel extraction
- visible thread or forum row extraction

Current Discord adapter strengths:
- state detection first
- read-first extraction
- honest blocker reporting

## 8. When raw browser control is acceptable

Use targeted browser control only when:
- you need a narrow probe not covered by the adapter
- the action is clearly visible and low risk
- you can verify the visible result immediately

Even then:
- keep calls targeted
- re-check route state before acting
- stop if the surface changes under you

## 9. Common Discord blockers

Watch for:
- login screen
- register/onboarding flow
- hCaptcha or verification wall
- wrong guild or channel route
- stale or half-loaded thread state
- hidden message composer state
- account mismatch

When blocked:
- name the blocker plainly
- say whether it is retryable, adapter-fixable, or human-blocked
- do not fake progress on a gated surface
- if route, gate, or composer state feels contradictory, escalate to a screenshot early

## 10. Token-efficiency rules for Discord

Prefer:
- state checks over giant DOM reads
- visible extraction over broad scraping
- route classification before content reads
- one action followed by verification

Avoid:
- raw HTML dumps of the whole app
- repeated full-page reads on unchanged state
- selector fishing across the entire Discord shell

## 11. Minimal Discord checklist

Before claiming a Discord task done, confirm:
- correct account or logged-out state
- correct server/channel/thread surface
- blocker state known
- intended state extracted or action completed
- visible result verified afterward

## 12. Relationship to other docs

Use alongside:
- `browser-operations` for universal browser rules
- the Discord adapter repo for concrete MCP/tool surface
- runtime wrappers when working from Claude Code, Codex, Cursor, Hermes, and others

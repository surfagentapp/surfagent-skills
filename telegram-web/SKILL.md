---
name: telegram-web
description: Telegram Web platform skill for SurfAgent, covering chat state, sidebar search, send verification, profile text edits, and when to use the Telegram Web adapter over raw browser control.
version: 1.2.0
metadata:
  openclaw:
    homepage: https://surfagent.app
    emoji: "✈️"
---

# Telegram Web

> Telegram Web operating skill. Use this with the core `browser-operations` skill.

This skill teaches agents how to work Telegram Web without treating a brittle chat UI like a generic web form.

## 1. Use this skill for

- chat and sidebar state checks
- chat-open by title
- visible message extraction
- composer state inspection
- draft filling
- proof-aware send flows
- profile text editing
- deciding when to use the Telegram Web adapter instead of raw browser control

## 2. Tool preference

Use this order:
1. Telegram Web task runners
2. Telegram Web adapter state/composer/profile tools
3. targeted browser evaluation only when needed
4. raw generic browser actions as fallback

Prefer Telegram-native verbs over improvised DOM pokes.

Operating principle: take the path of least resistance.
- keep one good Telegram tab instead of spawning extras
- prefer the simplest visible working path over clever indirect logic
- if the UI already shows the answer, trust that before inventing more checks
- codify only the flow that already works on screen

## 3. Telegram Web truths that matter

Telegram Web is not a normal static page.

It has:
- dynamic sidebar and chat panes
- contenteditable composer behavior
- route changes inside the app shell
- profile/settings panels that can replace the normal left sidebar
- send flows where clicking alone is weak proof

Important: a send attempt is not success unless the UI shows the message actually landed.

## 4. Trust order

When Telegram signals disagree, trust this order:
1. visible panel state and screenshot
2. selected chat header / profile header text
3. composer state and post-send composer clearing
4. extracted sidebar/message rows
5. click receipts and generic success strings

If a simpler visible check settles the question, stop there. Do not keep escalating into more brittle logic just because you can.

## 5. What today’s Telegram session taught us

The durable lessons from real Telegram dogfooding were:
- the visible UI was often more trustworthy than adapter state guesses
- one known-good Telegram tab beat clever reopen logic almost every time
- screenshot first, act once, screenshot again was faster than brute-force canaries
- direct visible navigation through folders and chats was easier than route tricks
- the easiest send path was an already-open writable chat, not a fancy open-chat flow
- profile edits were straightforward once logged in, but post-save visible verification mattered because Telegram can partially apply changes
- a cleared composer is helpful evidence, but the real proof is the message visibly present in-thread

## 6. Core Telegram loops

### Open chat by title
1. confirm Telegram Web is logged in
2. ensure the real sidebar is visible, backing out of settings/profile panels if needed
3. fill sidebar search
4. prefer exact title match, then starts-with, then contains
5. open the chat
6. verify selected chat header and composer/chat pane state

### Send message to a named chat
1. open the target chat deterministically
2. verify composer presence
3. fill exact text
4. verify composer text matches
5. send
6. verify composer clears or visible echo appears
7. if anything feels ambiguous, stop and verify the actual thread visually before claiming success

### Edit profile text
1. open the profile editor
2. fill first name, last name, bio, username
3. wait for username validation if changed
4. save
5. verify visible profile identity reflects the new values
6. if bio or username length/validation gets weird, trust the persisted visible profile, not the form state

## 7. Easiest proven Telegram tasks

These were the easiest reliable actions in live use today:
1. sending from an already-open writable chat on a single stable tab
2. visually confirming the selected chat before typing anything
3. moving through visible folders and chat rows with screenshot-first checks
4. editing profile text once the profile panel was already open
5. verifying a send by looking for the message in-thread, not by trusting the click

Treat these as the default path. Only escalate into more adapter logic when the easy visible route genuinely fails.

## 8. Proof rules

For Telegram Web, success requires:
1. correct chat is open
2. intended text is present before send
3. composer clears or materially changes after send
4. last visible message reflects the sent content, or stronger site-native confirmation exists

For profile edits, success requires:
1. editor opened
2. fields were applied
3. save succeeded
4. visible profile panel reflects the new identity text

Do not claim success from only:
- clicking the send button
- a keypress firing
- draft text existing before send
- a click receipt on My Profile or Edit profile
- absence of an error

## 9. When to use the Telegram Web adapter

Prefer the Telegram Web adapter for:
- opening Telegram Web
- checking page and composer state
- opening a chat by title
- extracting visible messages
- extracting visible chats
- filling the current composer draft
- sending a message with immediate post-send checks
- editing profile text fields with proof-aware save behavior

Current Telegram Web adapter verbs:
- `tgweb_health_check`
- `tgweb_open`
- `tgweb_get_state`
- `tgweb_open_chat`
- `tgweb_open_chat_by_title`
- `tgweb_extract_visible_messages`
- `tgweb_extract_chats`
- `tgweb_get_composer_state`
- `tgweb_fill_composer_draft`
- `tgweb_send_message`
- `tgweb_update_profile_text`
- `tgweb_check_state_task`
- `tgweb_send_current_chat_message_task`
- `tgweb_open_chat_by_title_task`
- `tgweb_send_message_to_chat_task`
- `tgweb_edit_profile_text_task`

## 10. When raw browser control is acceptable

Use targeted browser control only when:
- you need a one-off UI probe not covered by the adapter
- you can verify the result immediately in the visible Telegram UI
- the action is narrow and low-risk

Even then:
- keep calls targeted
- avoid broad DOM scraping
- verify the post-action state, not just the action attempt

## 11. Common Telegram Web blockers

Watch for:
- QR/login wall
- wrong left panel open instead of real chat list
- wrong chat open
- composer not actually focused or writable
- stale sidebar or pane state
- account mismatch
- modal or onboarding overlays
- send control present but not truly actionable
- username validation mutating the field label while editing

When blocked:
- name the blocker plainly
- say whether it is retryable, adapter-fixable, or human-blocked
- do not quietly lower the proof bar

## 12. Token-efficiency rules for Telegram Web

Prefer:
- task runners over ad hoc multi-step browser wandering
- state checks over full-app reads
- visible message extraction over giant DOM dumps
- composer-state inspection over repeated page snapshots
- one send action followed by verification
- one stable Telegram tab over tab spray

Avoid:
- dumping the full app shell for a single chat task
- repeated blind retries on the composer
- claiming success before the message is visibly present
- opening duplicate Telegram tabs when the current one is usable
- forcing route tricks when a direct visible path already works

## 13. Minimal Telegram Web checklist

Before claiming a Telegram Web task done, confirm:
- correct account
- not on the QR/login wall
- correct chat or profile surface
- intended draft content visible before send
- send actually happened or save actually landed
- visible post-action result confirmed afterward

## 14. Relationship to other docs

Use alongside:
- `browser-operations` for universal browser rules
- `surfagent-telegram-web/TELEGRAM_WEB_TASK_COOKBOOK.md` for concrete task recipes
- the Telegram Web adapter repo for MCP/tool surface
- runtime wrappers when working from Claude Code, Codex, Cursor, Hermes, and others

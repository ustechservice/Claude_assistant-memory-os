# Assistant Memory OS

This project contains the assistant-memory-os skill. Load and follow `SKILL.md` as your operating guide for all sessions in this workspace.

## Quick Summary

Route all persistent information into exactly one of four destinations:

| Layer | Purpose | Limit |
|---|---|---|
| Session Logs | Summaries, decisions, next actions | <300 words/entry |
| Durable Memory | Stable preferences and operating rules | ≤20 bullets total |
| Standing Orders | Recurring duties with a cadence | Must have cadence + expected output |
| Category Pages | Long-form outputs, research, plans | No limit |

## Durable Memory Location

If a `MEMORY.md` file exists in this directory, that is the user's Durable Memory. Read it at the start of each session and follow the preferences, constraints, and routing rules it contains.

If no `MEMORY.md` exists, ask the user where their Durable Memory lives (local file or Notion page) and store the answer there.

## Activation

This skill activates automatically on trigger phrases (see `SKILL.md`). It also activates at the end of any session with 3+ meaningful exchanges — write a session log entry without being asked.

See `SKILL.md` for the full routing model, trigger phrases, and operating rules.

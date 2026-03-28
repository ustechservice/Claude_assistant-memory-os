# assistant-memory-os

A four-destination routing skill for clean Claude assistant continuity across sessions,
built on Notion as the persistence layer.

## The Problem

Assistants fail continuity in three ways: they forget too much, save too much junk, or
collapse sessions, recurring duties, and reference knowledge into one unmanageable pile.

## The Solution

This skill teaches Claude to route persistent information into four distinct destinations:

| Destination | Purpose |
|---|---|
| **Claude Sessions** | Session summaries, decisions, next actions, open loops |
| **Standing Orders** | Recurring duties, watch/track/report tasks, scheduled reports |
| **Category Pages** | Research, SOPs, plans, ops logs, ideas — long-form knowledge |
| **Durable Memory** | Stable preferences, constraints, routing rules, behavioral facts |

## Installation

Drop the `assistant-memory-os/` folder into your Claude skills directory, or install
the `.skill` package file via your skill manager (OpenClaw, etc.).

## Structure

```
assistant-memory-os/
├── SKILL.md                        # Core skill — routing model and rules
└── references/
    ├── routing-rules.md            # Phrase triggers, decision tree, ambiguous cases
    ├── schemas.md                  # Notion database schemas for all four destinations
    ├── anti-bloat.md               # Bloat detection, cleanup rules, smell test
    ├── notion-layouts.md           # Workspace layouts (minimal → team)
    └── examples.md                 # Good/bad save examples, routing quick reference
```

## Design Principles

- No hardcoded Notion page IDs — users configure their own workspace
- Human-editable at every layer — no hidden state
- Hybrid-first (local `MEMORY.md` + Notion) by default
- Autonomous end-of-session saving — no permission-asking per step
- Aggressive anti-bloat built in from the start

## License

MIT

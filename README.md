# assistant-memory-os

**Notion memory for Claude, Claude Code, and OpenClaw.**

This skill gives Claude a persistent, human-readable memory system built on Notion. Without it, Claude forgets everything between sessions, saves things in the wrong place, or buries decisions inside bloated context that nobody reads. With it, every piece of information that should persist gets routed into exactly one of four destinations: a session log (what happened, what was decided, what’s next), durable memory (stable preferences and operating rules that shape all future sessions), a standing order (recurring duties with a cadence and expected output), or a category page (long-form outputs like research, plans, SOPs, and guides). All of it lives in Notion — human-readable, editable without Claude, and browsable at any time.

Activates on trigger phrases such as "log this session", "remember this", and "track this weekly", and automatically writes a session log at the end of any meaningful session without being asked. Works Notion-first, hybrid (local MEMORY.md + Notion), or minimal depending on your setup.

> Assistants fail continuity in three ways: they forget too much, save too much junk, or collapse sessions, recurring duties, and reference knowledge into one unmanageable pile. This skill solves that by giving every piece of information exactly one home.

---

## The Four Destinations

| Destination | Purpose | Hard Limits |
|---|---|---|
| **Claude Sessions** | Session summaries, decisions, next actions, open loops | Under 300 words per entry |
| **Standing Orders** | Recurring duties, scheduled reports, watch tasks | Must have cadence + expected output |
| **Category Pages** | Research, plans, SOPs, long-form knowledge | No word limit — use pages |
| **Durable Memory** | Stable preferences, constraints, operating rules | ≤20 bullets total |

---

## Trigger Commands

### Session Logs
| Say this | What happens |
|---|---|
| `"log this session"` | Writes session summary now |
| `"summarize what we did"` | Writes session summary now |
| `"create a handoff"` | Writes handoff-focused session log |
| `"what did we decide?"` | Surfaces decisions from this session |
| `"what are my next actions?"` | Lists next actions from session log |
| `"what's still open?"` | Lists open loops |
| `"end of session"` | Triggers full end-of-session routine |
| *(3+ meaningful exchanges)* | Writes session log automatically — no prompt needed |

### Durable Memory
| Say this | What happens |
|---|---|
| `"remember this for future sessions"` | Saves to Durable Memory |
| `"always do X"` | Saves operating rule |
| `"never do X"` | Saves constraint |
| `"my preference is X"` | Saves preference |
| `"this is a standing rule"` | Saves to Durable Memory |
| `"update my memory"` | Reviews and updates Durable Memory |

### Standing Orders
| Say this | What happens |
|---|---|
| `"track this weekly"` | Creates Standing Order (weekly cadence) |
| `"watch for X"` | Creates Standing Order (monitoring) |
| `"check this every Monday"` | Creates Standing Order (scheduled) |
| `"report on X daily"` | Creates Standing Order (scheduled report) |
| `"add this to my recurring duties"` | Creates Standing Order |
| `"remind me to do X every week"` | Creates Standing Order |
| `"monitor X and alert me when..."` | Creates Standing Order (conditional) |

### Category Pages
| Say this | What happens |
|---|---|
| `"save this research"` | Saves to Research category page |
| `"document this process"` | Saves to SOPs category page |
| `"save this plan"` | Saves to relevant category page |
| `"log today's work"` | Saves to Daily Logs category page |
| `"this is a guide / SOP / audit"` | Saves to appropriate category page |

### Maintenance
| Say this | What happens |
|---|---|
| `"clean up my Durable Memory"` | Reads page, removes bloat, reports count |
| `"audit my Standing Orders"` | Lists all orders, flags stale ones |
| `"archive old sessions"` | Identifies closed sessions 90+ days old |
| `"run quarterly review"` | Steps through full maintenance checklist |
| `"check my memory count"` | Reports current bullet count in Durable Memory |

---

## Installation

Choose the path that matches how you use Claude:

---

### Path A: Claude.ai Web or Projects

Paste the contents of `SKILL.md` into your Claude Project instructions or system prompt. `SKILL.md` is fully self-contained -- no other files are required.

---

### Path B: Claude Code or OpenClaw (CLI / IDE)

1. Clone or download this repo
2. Copy the `assistant-memory-os` folder into your Claude Code skills directory:
   ```
   ~/.claude/skills/assistant-memory-os/
   ```
3. Restart Claude Code -- the skill activates on trigger phrases automatically

**Or:** Copy `CLAUDE.md` from this repo into your project root. Claude Code will auto-load it when you open the project.

---

### Path C: Hybrid Mode (Local Memory + Notion)

Best for developers and operators using Claude Code or OpenClaw who want fast local memory with Notion for richer records.

1. Copy `MEMORY.md` from this repo into your project root or `~/.claude/`
2. Fill in your preferences, constraints, and routing rules
3. Follow Path B to install the skill
4. Tell Claude: *"My Durable Memory is in MEMORY.md locally. Session logs and standing orders go to Notion."*

See [`references/quick-start.md`](references/quick-start.md) for the full Notion setup.

---

## Quick Setup (30 minutes)

See [`references/quick-start.md`](references/quick-start.md) for step-by-step Notion setup.

**The short version:**

1. Create a **Claude Sessions** database in Notion
2. Create a **Standing Orders** database in Notion
3. Create a **Durable Memory** page in Notion
4. Create **Category Pages** (Research, Ops, Ideas — add more as needed)
5. Tell Claude your database names: *"I've set up my assistant memory OS. Claude Sessions is [name], Standing Orders is [name]..."*
6. Claude saves routing rules to Durable Memory and starts routing automatically

---

## File Reference

| File | Purpose |
|---|---|
| [`SKILL.md`](SKILL.md) | Core skill — self-contained, use as system prompt or Claude Code skill |
| [`MEMORY.md`](MEMORY.md) | Starter template for local Durable Memory (hybrid mode) |
| [`CLAUDE.md`](CLAUDE.md) | Auto-loaded by Claude Code — points to SKILL.md and MEMORY.md |
| [`references/routing-rules.md`](references/routing-rules.md) | Decision tree, trigger phrases, ambiguous case resolution |
| [`references/schemas.md`](references/schemas.md) | Notion database schemas for all four destinations |
| [`references/anti-bloat.md`](references/anti-bloat.md) | What not to save, warning signs, cleanup rules |
| [`references/notion-layouts.md`](references/notion-layouts.md) | 4 workspace layouts: minimal, standard, hybrid, team |
| [`references/examples.md`](references/examples.md) | Good and bad examples for every layer |
| [`references/quick-start.md`](references/quick-start.md) | 30-minute first-time Notion setup guide with validation |
| [`references/notion-mcp-calls.md`](references/notion-mcp-calls.md) | MCP call templates for all Notion write operations |
| [`references/maintenance.md`](references/maintenance.md) | Quarterly review checklist, cleanup commands, benchmarks |
| [`references/openclaw-setup.md`](references/openclaw-setup.md) | OpenClaw-specific setup and configuration |
| [`references/upgrade-path.md`](references/upgrade-path.md) | MemoryOS-MCP comparison and upgrade decision framework |

---

## Operating Models

**Notion-First** — all four layers live in Notion databases and pages.

**Hybrid** (recommended for developers) — Durable Memory stays local (`MEMORY.md` or Claude Code's memory system); Session Logs, Standing Orders, and Category Pages live in Notion.

**Minimal** — Claude Sessions DB + one Durable Memory page + Standing Orders DB + three category folders (Research, Ops, Ideas).

---

## Anti-Bloat Principles

- Session logs: under 300 words. Summaries, not transcripts.
- Durable Memory: ≤20 bullets. Rules that change behavior, not a diary.
- Standing Orders: every order must have a cadence and expected output.
- Category Pages: link from session logs, never duplicate content.
- No "Recommendations" or "Misc" buckets — route everything specifically.

---

## License

MIT

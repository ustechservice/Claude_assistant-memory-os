---
name: assistant-memory-os
description: Notion-based assistant continuity system. Routes information cleanly across four layers — Session Logs, Durable Memory, Standing Orders, and Category Pages — to prevent memory bloat, context loss, and routing chaos. Use when the user wants to set up assistant continuity, save session summaries, capture recurring duties, or structure their Notion workspace as an assistant operating system.
origin: ustechservice
---

# Assistant Memory OS

Keep assistant continuity clean, durable, and human-editable across sessions.

This skill governs how Claude saves and retrieves persistent information using a **four-destination system** built on Notion (with optional local memory). The core problem it solves: assistants fail continuity in three ways — they forget too much, save too much junk, or collapse sessions, recurring duties, and reference knowledge into one unmanageable pile.

## When to Activate

- User says "set up my assistant memory system" or "help me organize Notion for Claude"
- User says "remember this," "save this," "log this," or "track this"
- User says "summarize this session" or "write up what we did"
- User says "watch this weekly," "check this every Monday," or "remind me to do X"
- User asks "where should I save this?" for anything meant to persist
- User wants to configure Notion as an assistant operating system
- End of a session with 3+ meaningful exchanges — write a session log automatically, without asking permission
- Assistant continuity is breaking down: things are being forgotten, duplicated, or buried

## What Is a "Meaningful Exchange"

A session qualifies as meaningful if **at least one** of the following is true:
- A decision was made
- A non-trivial task was completed or advanced
- A plan, document, or design was created or substantially modified
- A substantive question was researched and answered
- An open loop was created, resolved, or updated

Does **not** qualify: quick lookups with a single answer, small talk, purely conversational exchanges with no outputs, sessions where nothing was decided or produced.

---

## The Four-Layer Model

Route all persistent information into exactly one of these destinations. Do not collapse them into one bucket.

| Layer | Purpose | Hard Limits |
|---|---|---|
| **Session Logs** | Continuity between work sessions | Under 300 words per entry |
| **Durable Memory** | Stable facts that shape future behavior | ≤20 bullets total |
| **Standing Orders** | Recurring duties and scheduled obligations | Must have cadence + expected output |
| **Category Pages** | Long-form knowledge, research, outputs | No word limit — use pages, not fields |

### 1. Session Logs (Claude Sessions)

Session continuity records. Not transcripts — summaries.

**Save here:**
- 2-3 sentence session summary (what happened, what was decided, what's next)
- Decisions made
- Concrete next actions with owners
- Open loops not yet resolved
- Links to key outputs produced (link, never paste content)
- Handoff context for the next session

**Never save here:**
- Full conversation transcripts
- Preferences or rules (those go in Durable Memory)
- Recurring duties (those go in Standing Orders)
- Long-form outputs (link to the Category Page instead)
- Trivial sessions with no decisions and no next actions

**Title format:** `YYYY-MM-DD -- [2-4 word topic]`

### 2. Durable Memory

Stable facts that actively shape behavior across all sessions. Not a diary.

**Save here:**
- Long-lived preferences ("always format code in Python unless specified")
- Durable constraints ("never recommend per-seat SaaS above $X/user")
- Operating rules ("end every meaningful session with a log entry")
- Routing rules ("save research to the Research category page")
- Stable identity facts (timezone, primary cloud, preferred stack)

**Never save here:**
- Session-specific facts ("today we decided to use Redis")
- One-time instructions
- Links to articles or docs
- Recurring duties
- Research summaries or project knowledge
- Full logs or transcripts
- Anything with a date as its primary anchor

**Hard limit: ≤20 total bullets across all sections. Review and prune quarterly.**

### 3. Standing Orders

Recurring operational commitments. Every order must have a cadence and an expected output.

**Save here:**
- Recurring duties ("every Monday: pull weekly metrics")
- Watch tasks ("track competitor pricing changes")
- Scheduled reports ("weekly revenue summary")
- Monitoring obligations ("alert me when X happens")

**Never save here:**
- One-time tasks (put in Session Log next actions instead)
- Session notes or decisions
- General preferences

### 4. Category Pages

Long-form work worth keeping. Organized by category, not by session.

**Save here:**
- Research documents
- Plans and roadmaps
- SOPs and guides
- Audits and reports
- Project knowledge
- Reusable templates

**Categories:** Research · Revenue · Ops · Ideas · SOPs · Daily Logs

Route every output into the most specific category. Do not create vague catch-alls like "Recommendations" or "Misc."

---

## Routing Decision Tree

Apply in order. Stop at the first match.

```
Is this worth saving at all?
|
+-- No (trivial chatter, single-answer lookups, no decisions) --> Save nothing
|
+-- Yes --> Does it repeat on a schedule or condition?
            |
            +-- Yes --> STANDING ORDERS
            |
            +-- No --> Is it a stable fact that shapes behavior across all future sessions?
                       |
                       +-- Yes --> DURABLE MEMORY
                       |
                       +-- No --> Is it a summary, decision, or action from this session?
                                  |
                                  +-- Yes --> SESSION LOGS
                                  |
                                  +-- No --> Is it a long-form output, research, plan, or guide?
                                             |
                                             +-- Yes --> CATEGORY PAGES (pick the right one)
                                             |
                                             +-- Unclear --> Ask the user, then default to Session Logs
```

**Tie-breaker:** when something fits two destinations, the more specific one wins. Never duplicate across layers — cross-link instead.

---

## Trigger Phrases

### Session Logs
| Say this | What happens |
|---|---|
| "log this session" | Write session summary now |
| "summarize what we did" | Write session summary now |
| "create a handoff" | Write handoff-focused session log |
| "what did we decide?" | Surface decisions from this session |
| "what are my next actions?" | List next actions from session log |
| "what's still open?" | List open loops |
| "end of session" | Trigger end-of-session routine |
| *(3+ meaningful exchanges)* | Write session log automatically |

### Durable Memory
| Say this | What happens |
|---|---|
| "remember this for future sessions" | Save to Durable Memory |
| "always do X" | Save operating rule |
| "never do X" | Save constraint |
| "my preference is X" | Save preference |
| "this is a standing rule" | Save to Durable Memory |
| "update my memory" | Review and update Durable Memory |

### Standing Orders
| Say this | What happens |
|---|---|
| "track this weekly" | Create Standing Order (weekly cadence) |
| "watch for X" | Create Standing Order (monitoring) |
| "check this every Monday" | Create Standing Order (scheduled) |
| "report on X daily" | Create Standing Order (scheduled report) |
| "add this to my recurring duties" | Create Standing Order |
| "remind me to do X every week" | Create Standing Order |
| "monitor X and alert me when..." | Create Standing Order (conditional) |

### Category Pages
| Say this | What happens |
|---|---|
| "save this research" | Save to Research category page |
| "document this process" | Save to SOPs category page |
| "save this plan" | Save to relevant category page |
| "log today's work" | Save to Daily Logs category page |
| "this is a guide / SOP / audit" | Save to appropriate category page |

### Maintenance
| Say this | What happens |
|---|---|
| "clean up my Durable Memory" | Read page, remove bloat, report count |
| "audit my Standing Orders" | List all orders, flag stale ones |
| "archive old sessions" | Identify closed sessions 90+ days old |
| "run quarterly review" | Step through full maintenance checklist |
| "check my memory count" | Report current bullet count in Durable Memory |

---

## Anti-Bloat Rules

**Durable Memory is not a diary.** Every bullet must actively change behavior in future sessions. If removing it wouldn't change anything, remove it.

| What to avoid | Where it actually belongs |
|---|---|
| Session decisions with a date anchor | Session Logs |
| Project-specific knowledge | Category Pages |
| One-time instructions | Nowhere (just follow them) |
| Recurring duties | Standing Orders |
| Research or competitive notes | Category Pages |

**Session Logs are not transcripts.** Max 300 words. Summaries, not records.

**Standing Orders must be executable.** Every order needs a cadence, expected output, and destination. "Keep an eye on things" is not a standing order.

**Never duplicate.** When the same fact appears in two layers, the more specific one wins and the other gets removed.

**The smell test:** "If I read this in 30 days with no context, would it still be useful and clear?" If no — compress or cut.

---

## End-of-Session Routine

After any session with 3+ meaningful exchanges:

1. Write a concise session log entry automatically — no permission needed
2. Summary: 2-3 sentences max
3. Decisions: bullet list, max 5
4. Next Actions: concrete, owned, not speculative
5. Open Loops: only genuine unresolved questions
6. Key Outputs: links only, never paste content
7. Check if anything should move to Standing Orders or Durable Memory
8. Do not write a log for trivial or purely conversational sessions

---

## Ambiguous Cases

### "Remember this" — Memory or Session Log?
- Affects behavior in **all future sessions** → Durable Memory
- Specific to **this project or session** → Session Log
- Stability test: "Will this still be true and relevant in a different session, on a different project, three months from now?"

### "Save this" — Session Log or Category Page?
- Summary, decision, or action → Session Log
- Document, guide, research, or plan → Category Page

### "Track this" — Standing Order or Session Log?
- Check again on a recurring schedule → Standing Orders
- Unresolved item from today only → Session Log (open loops field)

### Recommendations
Never create a "Recommendations" bucket. Route every recommendation specifically:
- Affects future behavior → Durable Memory
- Recurring report or task → Standing Orders
- Within a project → Category Page (relevant category)
- Made in a session → Session Log (decisions or next actions field)

---

## Operating Models

### Notion-First
All four layers live in Notion:
- **Claude Sessions** database for Session Logs
- **Standing Orders** database for recurring duties
- **Durable Memory** page (single page, grouped sections)
- **Category Pages** for long-form outputs

### Hybrid (Recommended for Developers)
- **Durable Memory** lives locally (`MEMORY.md` or Claude Code's memory system) — lean, version-controllable, fast to read
- **Session Logs**, **Standing Orders**, and **Category Pages** live in Notion

### Minimal (Solo Builder)
- Claude Sessions database (5 fields: Title, Date, Summary, Next Actions, Open Loops)
- Durable Memory as a single Notion page
- Standing Orders as a simple database
- Three category folders: Research, Ops, Ideas

---

## Reference Files

These files provide deeper detail. They are optional supplements — this file is self-contained for day-to-day use.

| File | Use when |
|---|---|
| `references/routing-rules.md` | Deciding where information belongs (full decision tree + ambiguous case resolution) |
| `references/schemas.md` | Designing database and page structure in Notion |
| `references/anti-bloat.md` | Memory quality is degrading or cleanup is needed |
| `references/notion-layouts.md` | Setting up a Notion workspace (4 layout templates) |
| `references/examples.md` | Concrete good/bad examples for each layer |
| `references/quick-start.md` | First-time setup in 30 minutes |
| `references/notion-mcp-calls.md` | MCP call templates for Notion writes |
| `references/maintenance.md` | Quarterly review and cleanup procedures |

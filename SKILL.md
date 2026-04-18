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
- 2–3 sentence session summary (what happened, what was decided, what's next)
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

**Title format:** `YYYY-MM-DD – [2–4 word topic]`

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

## Default Routing Logic

Apply in order:

1. Does this repeat on a schedule or condition? → **Standing Orders**
2. Is this a stable fact that shapes future behavior? → **Durable Memory**
3. Is this a summary, decision, or action from this session? → **Session Logs**
4. Is this a long-form output, research, plan, or guide? → **Category Pages**
5. Is this trivial chatter with no decisions? → **Save nothing**

When something fits two destinations: the more specific one wins. Never duplicate across layers.

Read `references/routing-rules.md` for trigger phrases, decision tree, and ambiguous case resolution.

## Anti-Bloat Rules (Summary)

- Do not save trivial chatter
- Do not duplicate the same fact into multiple layers
- Do not turn Durable Memory into a diary (hard cap: ≤20 bullets)
- Do not turn Session Logs into transcripts (hard cap: 300 words)
- Do not store recurring duties as loose notes — put them in Standing Orders
- Do not paste output content into Session Logs — link to the Category Page
- Do not create vague "Recommendations" or "General" buckets

Read `references/anti-bloat.md` for detailed rules, warning signs, and cleanup guidance.

## End-of-Session Routine

After any session with 3+ meaningful exchanges:

1. Write a concise session log entry automatically — no permission needed
2. Summary: 2–3 sentences max
3. Decisions: bullet list, max 5
4. Next Actions: concrete, owned, not speculative
5. Open Loops: only genuine unresolved questions
6. Key Outputs: links only, never paste content
7. Check if anything should move to Standing Orders or Durable Memory
8. Do not write a log for trivial or purely conversational sessions

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

Read `references/notion-layouts.md` for full workspace structure examples.

## Reference Files

| File | Use when |
|---|---|
| `references/routing-rules.md` | Deciding where information belongs |
| `references/schemas.md` | Designing database and page structure |
| `references/anti-bloat.md` | Memory quality is degrading or cleanup is needed |
| `references/notion-layouts.md` | Setting up a Notion workspace |
| `references/examples.md` | Concrete good/bad examples for each layer |
| `references/quick-start.md` | First-time setup in 30 minutes |
| `references/notion-mcp-calls.md` | MCP call templates for Notion writes |
| `references/maintenance.md` | Quarterly review and cleanup procedures |

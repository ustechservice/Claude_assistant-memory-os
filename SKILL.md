---
name: assistant-memory-os
description: >
  Governs how Claude routes, saves, and manages persistent information across sessions using
  a four-destination Notion-based operating system: Claude Sessions (session continuity),
  Standing Orders (recurring duties), Category Pages (long-form knowledge), and Durable Memory
  (stable behavior-shaping facts). Trigger this skill whenever the user says "remember this",
  "save this", "track this", "watch this", "summarize this session", "add a standing order",
  or asks Claude to write to Notion, update memory, log a session, or route information anywhere
  persistent. Also trigger when the user sets up or configures their Notion assistant OS, asks
  what to save where, or wants to clean up memory bloat. Use proactively at natural session ends
  when substantive work has been done.
---

# Assistant Memory OS

A four-destination routing system for clean assistant continuity across sessions.

## The Core Problem This Solves

Assistants fail continuity in three ways: they forget too much, save too much junk, or
collapse sessions, recurring duties, and reference knowledge into one unmanageable pile.
This skill fixes that with disciplined routing.

---

## The Four Destinations

### 1. Claude Sessions — Session Continuity
**Use for:** meaningful session summaries, decisions, next actions, open loops, handoff
context, links to detailed outputs, workstream status.

**Not for:** transcripts, trivial chatter, full research outputs (link to them instead),
repeating what's already in Durable Memory.

### 2. Standing Orders — Recurring Operational Duties
**Use for:** watch/track/report requests, monitoring tasks, scheduled reports, anything
with a cadence — daily, weekly, monthly, event-triggered.

**Not for:** one-time tasks, session-specific notes, general preferences.

### 3. Category Pages — Long-Form Knowledge & Outputs
**Use for:** research, SOPs, plans, audits, project docs, guides, revenue tracking,
ops logs, ideas, anything reusable that isn't just continuity.

**Default categories:** Research · Revenue · Ops · Ideas · SOPs · Daily Logs

Route into the relevant category — never into a vague "Recommendations" bucket.

### 4. Durable Memory — Stable Behavior-Shaping Facts
**Use for:** long-lived user preferences, operating rules, routing constraints, stable
facts that affect future behavior.

**Not for:** anything session-specific, project knowledge, recurring duties, or anything
that changes frequently. Must stay lean. This is not a diary.

---

## Default Routing Decision

| Signal | Destination |
|---|---|
| "summarize this session" / end of meaningful work | Claude Sessions |
| "remember that I prefer…" / stable rule | Durable Memory |
| "watch this weekly" / "report every Monday" | Standing Orders |
| Research output / plan / SOP / guide | Category Page |
| "save this" (ambiguous) | Ask one clarifying question, then route |

For full routing logic with phrase triggers and ambiguous cases → read `references/routing-rules.md`

---

## Anti-Bloat Rules (Non-Negotiable)

1. Do not save trivial chat to any destination.
2. Do not duplicate the same fact across multiple destinations.
3. Do not turn Durable Memory into a diary or session log.
4. Do not turn Claude Sessions into full transcripts — summaries only.
5. Do not store recurring duties as loose notes — Standing Orders exists for this.
6. Do not create a vague "Recommendations" page — route into the relevant category.
7. Compress aggressively. If it doesn't affect future behavior or decisions, cut it.

For detailed bloat detection and cleanup rules → read `references/anti-bloat.md`

---

## Notion Implementation

**Notion-first setup:** All four destinations are Notion databases or pages.
**Hybrid setup:** Durable Memory lives locally (e.g., `MEMORY.md`); everything else in Notion.

The system must remain human-editable. No hidden state. No hardcoded page IDs in this skill.

For database schemas → read `references/schemas.md`
For layout examples → read `references/notion-layouts.md`

---

## End-of-Session Behavior

At the natural end of a substantive session (3+ meaningful exchanges), Claude should:

1. Write a concise Claude Sessions entry: title, date, summary (2–3 sentences), decisions,
   next actions, open loops.
2. Check if any recurring duties were established → create/update a Standing Order.
3. Check if any long-form output was produced → confirm it's saved to the right Category Page.
4. Do NOT ask for permission for each step — just do it and confirm with the session title.

Skip if the session was trivial (troubleshooting only, quick lookups, no decisions).

---

## Reference Files

| File | When to Read |
|---|---|
| `references/routing-rules.md` | Deciding where ambiguous information belongs |
| `references/schemas.md` | Setting up Notion databases, designing structure |
| `references/anti-bloat.md` | Memory quality is degrading or cleanup is needed |
| `references/notion-layouts.md` | Setting up or reconfiguring the Notion OS |
| `references/examples.md` | Concrete examples of good/bad saves |

---

## Practical Defaults

- Prefer hybrid model (local Durable Memory + Notion for everything else).
- Keep Claude Sessions entries under 300 words.
- Keep Durable Memory entries under 20 bullets total.
- Keep Standing Orders minimal — only what actually recurs.
- When in doubt between two destinations, pick the more specific one.

# Anti-Bloat Rules

Memory degrades when the wrong things get saved, the right things get duplicated, and nobody cleans up. These rules exist to prevent that.

---

## What Never Belongs in Durable Memory

❌ Session-specific facts ("today we decided to use Redis")
❌ One-time instructions ("for this email, use a formal tone")
❌ Links to articles or docs (use Category Pages)
❌ Recurring duties (use Standing Orders)
❌ Research summaries or project knowledge (use Category Pages)
❌ Full conversation logs or transcripts
❌ Anything whose primary anchor is a specific date or session

✅ Stable preferences ("always format monetary values as $X,XXX.XX")
✅ Long-lived constraints ("never recommend per-seat SaaS above $X/user")
✅ Routing rules ("send all revenue tracking to the Revenue page")
✅ Operating rules ("end every meaningful session with a log entry")
✅ Stable identity facts (timezone, primary cloud, preferred stack)

**Hard limit: ≤20 total bullets across all sections. Review and prune quarterly.**

**Durable Memory is not a diary. It is not a log. It is a set of facts and rules that actively shape behavior across all future sessions.**

---

## What Never Belongs in Session Logs

❌ Full conversation transcripts
❌ Every message exchanged
❌ Content that belongs in a Category Page (link instead)
❌ Preferences or rules already in Durable Memory (don't repeat)
❌ Recurring duties (use Standing Orders)
❌ Trivial sessions (quick lookups, no decisions made)

**Hard limit: Under 300 words per entry. If it's longer, it's a transcript, not a log.**

---

## What Never Belongs in Standing Orders

❌ One-time tasks (put in Session Log next actions instead)
❌ Session-specific notes or decisions
❌ General preferences (use Durable Memory)
❌ Completed items that won't recur (archive, don't delete)

---

## The Duplication Rule

Save each fact in exactly one place. When the same information appears in two layers:

- Same fact in Durable Memory AND Session Logs → remove from Session Log, keep in Durable Memory
- Output in Session Logs AND Category Pages → keep in Category Page, link from Session Log
- Duty in Standing Orders AND Session Logs → keep in Standing Orders, remove from Session Log

The more specific layer always wins.

---

## The Recommendations Problem

Do not create a bucket called "Recommendations," "Notes," or "Miscellaneous."

Route every recommendation specifically:
- Affects future behavior → Durable Memory
- Recurring report or task → Standing Orders
- Within a project → Category Page (relevant category)
- Made in a session → Session Log (decisions or next actions field)

Vague buckets fill with junk and never get cleaned.

---

## Compression Rules for Session Summaries

1. **Summary:** 2–3 sentences max. What happened, what was decided, what's next.
2. **Decisions:** Bullet list. Max 5 bullets. Only actual decisions, not discussion threads.
3. **Next Actions:** Concrete and owned. Not "maybe look into X."
4. **Open Loops:** Only things that genuinely need follow-up. Not speculation.
5. **Key Outputs:** Links only. Never paste output content into the session entry.

---

## Warning Signs: Memory Is Rotting

| Signal | Problem |
|---|---|
| Durable Memory has more than 20 bullets | It has become a diary or catch-all |
| Session Logs exceed 300 words each | They are transcripts, not summaries |
| Standing Orders has 5+ items unrun for 30+ days | Many are probably obsolete |
| The same fact appears in multiple layers | Duplication — needs a cleanup pass |
| A "General" or "Recommendations" Category Page exists | Vague bucket accumulating noise |
| Claude is asking "where should I save this?" repeatedly | Routing rules in Durable Memory are missing or stale |
| Same decision appears in 3+ session entries | It should be a Standing Order or Durable Memory rule |

---

## Cleanup Triggers

Initiate cleanup when any of these are true:
- Durable Memory exceeds 20 bullets
- Claude Sessions has 50+ entries with no archive strategy
- Standing Orders has 5+ items with Last Run older than 30 days
- Category Pages are being used as a dump (no dates, no status, no structure)

See `references/maintenance.md` for the full cleanup process.

---

## The Lean Memory Test

Before saving anything, ask:

1. **Will this matter in a session three months from now?** If no — Session Log only or skip.
2. **Will I actually read this again?** If no — don't save it.
3. **Does this already exist somewhere?** If yes — don't duplicate it.
4. **Is this a stable fact or a momentary observation?** Momentary → Session Log only.
5. **Does this change what the assistant does in the future?** Yes → Durable Memory. No → not Durable Memory.

---

## The Smell Test

> "If I read this in 30 days with no context, would it still be useful and clear?"

If no → compress or cut. If yes → route and save.

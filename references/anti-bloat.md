# Anti-Bloat Rules

## What Never Belongs in Durable Memory
❌ Session-specific facts ("today we decided to use Redis")
❌ One-time instructions ("for this email, use a formal tone")
❌ Links to articles or docs (use Category Pages)
❌ Recurring duties (use Standing Orders)
❌ Research summaries (use Research Category Page)
❌ Full conversation logs or transcripts

✅ Stable preferences ("always format monetary values as $X,XXX.XX")
✅ Long-lived constraints ("never recommend per-seat SaaS above $X/user")
✅ Routing rules ("send all revenue tracking to the Revenue page")
✅ Stable identity facts (timezone, primary cloud, preferred stack)

---

## What Never Belongs in Claude Sessions
❌ Full transcripts
❌ Content that belongs in a Category Page (link instead)
❌ Information already in Durable Memory (don't repeat it)
❌ Trivial sessions (quick lookups, no decisions)
❌ Recurring duties (use Standing Orders)

---

## What Never Belongs in Standing Orders
❌ One-time tasks
❌ Session-specific notes
❌ General preferences (use Durable Memory)
❌ Completed items that won't recur (archive, don't delete)

---

## Signs Your Memory Is Rotting
- Durable Memory exceeds 20 bullets
- Multiple bullets say essentially the same thing
- Claude Sessions entries exceed 300 words
- Session logs contain full research output instead of a link
- Standing Orders has items with no run in 60+ days
- You have a vague "Recommendations" or "General" category page
- The same fact appears in both Durable Memory and a Claude Session

---

## Compression Rules for Session Summaries
1. **Summary:** Max 3 sentences. What happened, what was decided, what's next.
2. **Decisions:** Bullet list. Max 5 bullets. Only actual decisions, not discussion.
3. **Next Actions:** Concrete and owned. Not "maybe look into X."
4. **Open Loops:** Only things that genuinely need follow-up.
5. **Key Outputs:** Links only. Never paste output into the session entry.

---

## Cleanup Triggers
Initiate cleanup when:
- Durable Memory exceeds 20 bullets
- Claude Sessions has 50+ entries with no archive strategy
- Standing Orders has 5+ items with Last Run older than 30 days
- Category Pages are being used as a dump

## Cleanup Process
1. **Durable Memory:** Remove duplicates, expired facts, session-specific content.
   Target: ≤15 bullets.
2. **Standing Orders:** Archive anything Completed or unrun for 60+ days. Update dates.
3. **Claude Sessions:** Archive sessions older than 90 days with Status = Closed.
4. **Category Pages:** Merge or restructure pages with no clear purpose or date.

---

## The Smell Test

> "If I read this in 30 days with no context, would it still be useful and clear?"

If no → compress or cut. If yes → route and save.

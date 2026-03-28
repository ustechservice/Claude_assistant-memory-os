# Maintenance Guide

Quarterly and on-demand processes for keeping the system clean and useful.

---

## Quarterly Review Checklist

Run this every 90 days or when the system feels sluggish.

### Durable Memory
- [ ] Count total bullets — if over 20, prune immediately
- [ ] Remove any session-specific facts that snuck in
- [ ] Merge duplicates or near-duplicates
- [ ] Remove preferences that haven't been relevant in 90+ days
- [ ] Update "Last reviewed" note at the bottom of the page
- [ ] Target: ≤15 bullets after cleanup

### Standing Orders
- [ ] Review all Active orders — is each one still needed?
- [ ] Check Last Run dates — anything unrun for 60+ days → Pause or archive
- [ ] Verify Next Run dates are accurate
- [ ] Check that Expected Output still matches what's actually useful
- [ ] Archive (don't delete) anything Completed or permanently discontinued

### Claude Sessions
- [ ] Sessions older than 90 days with Status = Closed → move to archive database
- [ ] Check for any sessions missing Next Actions or Status fields
- [ ] Verify Key Outputs links still resolve
- [ ] Look for recurring themes → should any become Standing Orders?

### Category Pages
- [ ] Identify pages with no date, no status, or no clear purpose
- [ ] Merge near-duplicate pages
- [ ] Archive pages with Status = Completed or obsolete content
- [ ] Check that pages link back to relevant Claude Sessions entries

---

## On-Demand Cleanup Commands

Say any of these to trigger a cleanup:

| Phrase | What Claude Does |
|---|---|
| "Clean up my Durable Memory" | Reads page, removes bloat, confirms count |
| "Audit my Standing Orders" | Lists all orders, flags stale ones, asks to archive |
| "Archive old sessions" | Identifies Closed sessions 90+ days old, moves to archive |
| "Prune category pages" | Lists undated/statusless pages, asks how to handle each |
| "Run quarterly review" | Steps through the full checklist above, destination by destination |

---

## Archiving Sessions

When Claude Sessions accumulates 50+ entries:

1. Create a new database `Claude Sessions Archive` with the same schema
2. Filter current database to Status = Closed AND Date < 90 days ago
3. Move those entries to the archive database
4. Keep the active database clean (ideally <30 entries at a time)

Do NOT delete sessions — archive them. They may be useful for pattern review.

---

## Signs the System Needs Maintenance Now

Don't wait for quarterly review if you see these:

- Durable Memory has more than 20 bullets
- A Standing Order has no Last Run date and is 2+ weeks old
- Claude Sessions entries are being written as full transcripts
- You have a "General" or "Misc" Category Page with random content
- Claude is asking "where should I save this?" repeatedly
  (means routing rules in Durable Memory are missing or stale)
- Same decision appears in 3+ different session entries
  (means it should be a Standing Order or Durable Memory rule instead)

---

## Durable Memory Pruning Script (Manual Process)

When pruning, go section by section:

**Preferences:** Remove anything that hasn't come up in 90 days. Keep only
rules that actively change Claude's behavior on a regular basis.

**Constraints:** Remove anything project-specific that has ended. Keep only
constraints that apply universally going forward.

**Routing Rules:** Update any database IDs or page names that have changed.
Remove rules for destinations that no longer exist.

**Stable Facts:** Remove anything that is no longer stable (e.g., old job,
old stack, old timezone). Update changed facts in place — don't add duplicates.

After pruning, add a line at the bottom:
`_Last reviewed: YYYY-MM-DD | Entry count: N_`

# Maintenance Guide

Quarterly and on-demand processes for keeping the system clean and useful. A well-maintained system stays fast to read and actually gets used. An unmaintained one becomes noise.

---

## Quarterly Review Checklist

Run this every 90 days, or when the system feels sluggish or unreliable.

### Durable Memory
- [ ] Count total bullets across all sections — if over 20, prune immediately
- [ ] Remove any session-specific facts that snuck in (entries with dates as anchors)
- [ ] Remove any project-specific knowledge that belongs in a Category Page
- [ ] Merge duplicates or near-duplicates
- [ ] Remove preferences that haven't been relevant in 90+ days
- [ ] Update any Routing Rules that point to renamed or moved databases/pages
- [ ] Update "Last reviewed" date and entry count at the bottom
- [ ] **Target: ≤15 bullets after cleanup**

### Standing Orders
- [ ] Review all Active orders — is each one still needed?
- [ ] Check Last Run dates — anything unrun for 60+ days → Pause or archive
- [ ] Verify Next Run dates are accurate and realistic
- [ ] Check that Expected Output still matches what's actually useful
- [ ] Archive (don't delete) anything Completed or permanently discontinued
- [ ] **Target: only orders you would actually run this month are marked Active**

### Claude Sessions
- [ ] Sessions older than 90 days with Status = Closed → move to archive
- [ ] Check for sessions missing Next Actions or Status fields
- [ ] Verify Key Outputs links still resolve (no broken links)
- [ ] Look for recurring themes — should any become Standing Orders or Durable Memory rules?
- [ ] **Target: Active database has <30 entries; rest are archived**

### Category Pages
- [ ] Identify pages with no date, no status, or no clear purpose
- [ ] Merge near-duplicate pages
- [ ] Archive pages with Status = Completed or obsolete content
- [ ] Check that pages link back to relevant Claude Sessions entries
- [ ] Remove any "Recommendations," "Misc," or "General" pages — route their content

---

## On-Demand Cleanup Commands

Say any of these to trigger a cleanup pass:

| Phrase | What Claude Does |
|---|---|
| "Clean up my Durable Memory" | Reads page, removes bloat, reports count before/after |
| "Audit my Standing Orders" | Lists all orders, flags stale ones, asks to archive |
| "Archive old sessions" | Identifies Closed sessions 90+ days old, moves to archive |
| "Prune category pages" | Lists undated/statusless pages, asks how to handle each |
| "Run quarterly review" | Steps through the full checklist above, destination by destination |
| "Check my memory count" | Reports current bullet count in Durable Memory |

---

## Archiving Sessions

When Claude Sessions accumulates 50+ entries:

1. Create a new database `Claude Sessions — Archive` (same schema as the active one)
2. Filter active database to: Status = Closed AND Date < 90 days ago
3. Move those entries to the archive database
4. Keep the active database clean — ideally under 30 entries at a time

**Do not delete sessions — archive them.** They may be useful for pattern review, retrospectives, or recovering context.

---

## Signs the System Needs Maintenance Now

Don't wait for quarterly review if you see these:

| Signal | Action |
|---|---|
| Durable Memory exceeds 20 bullets | Prune immediately |
| A Standing Order has no Last Run date and is 2+ weeks old | Confirm it's actually running |
| Session entries are being written as full transcripts | Remind Claude of the 300-word limit |
| A "General" or "Misc" Category Page exists | Route its content, delete the page |
| Claude asks "where should I save this?" repeatedly | Routing Rules in Durable Memory are missing or stale — update them |
| Same decision appears in 3+ different session entries | It should become a Standing Order or Durable Memory rule |
| You haven't read a session log in 30+ days | The system may be over-logging — reduce session log frequency |

---

## Durable Memory Pruning Process

When pruning, go section by section:

**Preferences:** Remove anything that hasn't come up in 90 days. Keep only rules that actively change behavior on a regular basis.

**Constraints:** Remove anything project-specific that has ended. Keep only constraints that apply universally going forward.

**Routing Rules:** Update any database names or IDs that have changed. Remove rules for destinations that no longer exist.

**Stable Facts:** Remove anything no longer stable (old job, old stack, old timezone). Update changed facts in place — don't add duplicates.

After pruning:
1. Update the entry count
2. Add/update `_Last reviewed: YYYY-MM-DD | Entry count: N_` at the bottom
3. Confirm count is ≤15

---

## Standing Orders Pruning Process

1. List all Active orders
2. For each: "Was this run in the last 30 days?"
   - Yes → keep Active, verify Next Run date
   - No → ask user: keep Active, Pause, or archive?
3. For Paused orders older than 90 days: ask user if they should be archived
4. Archive (don't delete) Completed orders

---

## Healthy System Benchmarks

| Metric | Target |
|---|---|
| Durable Memory bullets | ≤15 after quarterly review |
| Active session entries | <30 (rest archived) |
| Standing Orders with no recent run | 0 (all paused or archived) |
| Average session log length | <300 words |
| Broken Key Output links | 0 |
| Vague catch-all category pages | 0 |

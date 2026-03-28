# Quick Start Guide

Get the four-destination assistant OS running in Notion in under 30 minutes.

---

## Step 1 — Create Your Four Destinations in Notion

### A. Claude Sessions Database
1. Create a new full-page database in Notion
2. Title it `Claude Sessions`
3. Add these properties:
   - `Date` (Date)
   - `Area` (Select: Homelab, Research, Consulting, Automation, General)
   - `Summary` (Text)
   - `Decisions` (Text)
   - `Next Actions` (Text)
   - `Open Loops` (Text)
   - `Key Outputs` (Text)
   - `Status` (Select: Active, Closed, Paused)
   - `Importance` (Select: High, Medium, Low)
4. Set default view: Table, sorted by Date descending

### B. Standing Orders Database
1. Create a new full-page database titled `Standing Orders`
2. Add these properties:
   - `Status` (Select: Active, Paused, Completed)
   - `Cadence` (Select: Daily, Weekly, Monthly, Event-triggered)
   - `Purpose` (Text)
   - `Expected Output` (Text)
   - `Destination` (Text)
   - `Last Run` (Date)
   - `Next Run` (Date)
   - `Notes` (Text)
3. Set default view: Table, filtered to Status = Active

### C. Category Pages Database
1. Create a new full-page database titled `Category Pages`
2. Add these properties:
   - `Category` (Select: Research, Revenue, Ops, Ideas, SOPs, Daily Logs)
   - `Date Created` (Date)
   - `Last Updated` (Date)
   - `Status` (Select: Draft, Active, Archived)
   - `Tags` (Multi-select)
3. Set default view: Board grouped by Category

### D. Durable Memory Page
1. Create a new regular Notion **page** (not a database) titled `Durable Memory`
2. Add these sections as H2 headers:
   - `## Preferences`
   - `## Constraints`
   - `## Routing Rules`
   - `## Stable Facts`
3. Leave sections empty for now — you'll fill them as Claude learns your preferences

---

## Step 2 — Configure Claude's Routing Rules

Tell Claude the following (it will save to Durable Memory automatically):

> "My Notion assistant OS is set up. Claude Sessions database is [name/ID],
> Standing Orders database is [name/ID], Category Pages database is [name/ID],
> and Durable Memory is a page titled 'Durable Memory'. Save these as routing rules."

Claude will write the routing configuration to your Durable Memory page.

---

## Step 3 — Add Your First Durable Memory Entries

Start simple. Tell Claude:

> "Remember: I prefer Python for all code unless specified. My timezone is
> America/Detroit. Default to concise responses with no preamble."

Claude will add these to your Durable Memory page under the right sections.

---

## Step 4 — Run Your First Session

Do any substantive work with Claude (3+ meaningful exchanges). At the end, say:

> "Summarize this session."

Claude should automatically:
1. Write a Claude Sessions entry with title, summary, decisions, next actions
2. Flag any recurring duties for Standing Orders
3. Confirm with the session title

---

## Step 5 — Validate the System

Check that:
- [ ] Claude Sessions has a new entry with the correct date and area
- [ ] The summary is under 300 words
- [ ] Decisions are bullet points, not prose
- [ ] Next Actions are concrete (not vague)
- [ ] No content was duplicated into Durable Memory unnecessarily

---

## Optional: Hybrid Setup (Local MEMORY.md)

If you use OpenClaw or inject context into a system prompt:

1. Create `MEMORY.md` at a stable path (e.g., `C:\Users\[you]\Documents\MEMORY.md`)
2. Copy the four sections from Durable Memory into this file
3. Configure your wrapper to inject this file at session start
4. Use Notion for Sessions, Standing Orders, and Category Pages only
5. `MEMORY.md` is now the single source of truth for Durable Memory

---

## Troubleshooting

**Claude isn't saving sessions automatically**
→ Check that the skill is installed and triggering. Say "summarize this session" explicitly.

**Entries are too long**
→ Remind Claude: "Keep session summaries under 300 words, decisions as bullets only."

**Wrong destination**
→ Be explicit: "Save this to Standing Orders" or "This goes in the Ops category page."

**Durable Memory is growing too fast**
→ Run a cleanup: "Review my Durable Memory and remove anything that's session-specific
   or duplicated."

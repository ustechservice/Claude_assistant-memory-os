# Quick Start Guide

Set up your assistant memory OS in Notion in under 30 minutes.

---

## What You're Building

Four destinations in Notion:

| Destination | Type | Purpose |
|---|---|---|
| Claude Sessions | Database | Session continuity logs |
| Standing Orders | Database | Recurring duties |
| Durable Memory | Page | Stable preferences and rules |
| Category Pages | Pages | Long-form outputs and knowledge |

---

## Step 1: Create Claude Sessions Database (5 min)

Create a new Notion database named **Claude Sessions**.

Add these properties:

| Property | Type |
|---|---|
| Session Title | Title |
| Date | Date |
| Area / Topic | Select |
| Summary | Text |
| Decisions | Text |
| Next Actions | Text |
| Open Loops | Text |
| Key Outputs | Text |
| Status | Select (Active / Closed / Paused) |
| Importance | Select (High / Medium / Low) |

**Add these views:**
- All Sessions (default table)
- Open Loops (filter: Open Loops is not empty AND Status ≠ Closed)
- Active (filter: Status = Active)

---

## Step 2: Create Standing Orders Database (5 min)

Create a new Notion database named **Standing Orders**.

Add these properties:

| Property | Type |
|---|---|
| Name | Title |
| Status | Select (Active / Paused / Completed) |
| Cadence | Select (Daily / Weekly / Monthly / Event-triggered) |
| Purpose | Text |
| Expected Output | Text |
| Destination | Text |
| Last Run | Date |
| Next Run | Date |

**Add these views:**
- Active (filter: Status = Active)
- Due This Week (filter: Next Run ≤ today + 7 days AND Status = Active)

---

## Step 3: Create Durable Memory Page (3 min)

Create a new Notion page named **Durable Memory**.

Paste this template as the page body and fill in your details:

```
## Preferences
- [Add your preferences here]

## Constraints
- [Add constraints here]

## Routing Rules
- Claude Sessions database: [enter your database name or ID]
- Standing Orders database: [enter your database name or ID]
- Durable Memory: this page

## Stable Facts
- Primary timezone: [your timezone]
- Preferred stack: [your stack]

_Last reviewed: [date] | Entry count: [N]_
```

**Keep this under 20 total bullets. This is not a diary.**

---

## Step 4: Create Category Pages (5 min)

Create a top-level Notion page named **Knowledge** (or **Outputs**, or whatever fits your naming).

Inside it, create pages for the categories you actually need now:

- Research
- Ops
- Ideas

Add others (Revenue, SOPs, Daily Logs, Plans) only when a concrete need exists. Don't build out structure you won't use.

---

## Step 5: Configure Routing (5 min)

Tell Claude your setup. Paste something like this in your first session:

```
I've set up my assistant memory OS in Notion. Here's my configuration:

- Claude Sessions database: [name]
- Standing Orders database: [name]
- Durable Memory: a page called "Durable Memory" in [location]
- Category Pages: Research, Ops, Ideas under a page called "Knowledge"

Please update your routing rules and confirm you're ready to use this system.
```

Claude will save your routing rules to Durable Memory and confirm.

---

## Step 6: Run Your First Session (5 min)

Start a conversation with 3+ meaningful exchanges. At the end, say:

> "Summarize this session."

Claude will write a session log entry automatically. Verify:
- Title follows `YYYY-MM-DD – [2–4 word topic]` format
- Summary is 2–3 sentences, under 300 words
- Decisions are bullet points
- Next actions have owners
- Key outputs are linked, not pasted

---

## Hybrid Setup (Optional)

If you're using Claude Code and want local memory:

1. Copy `MEMORY.md` from this repo into your project root or `~/.claude/`
2. Fill in your preferences, constraints, and routing rules
3. Tell Claude: "My Durable Memory lives in MEMORY.md locally. Session logs and standing orders go to Notion."
4. Claude will use local memory for behavior-shaping facts and Notion for everything richer

---

## Troubleshooting

**Claude isn't saving sessions automatically**
→ Make sure Claude knows your database names. Repeat the configuration step above.
→ Check that your Notion MCP is connected (see `references/notion-mcp-calls.md`).

**Session entries are too long**
→ Remind Claude: "Session summaries should be under 300 words. Compress."
→ Add to Durable Memory: "Session log summaries: max 300 words."

**Durable Memory is bloating**
→ Follow the cleanup process in `references/maintenance.md`.
→ Target: ≤15 bullets after pruning.

**"Where should I save this?" keeps coming up**
→ Your Routing Rules section in Durable Memory is incomplete or stale.
→ Add explicit routing rules for common output types.

**Standing Orders aren't being executed**
→ Check that each order has a cadence, expected output, and destination.
→ Vague orders ("keep an eye on things") will not be executed. Make them specific.

---

## Setup Validation

Once you've completed Steps 1-5, run these prompts to verify each layer is working.

**Test Session Logs:**
> "Log this session. Title it 'Setup Test', summary: verified memory OS setup."

Expected: Claude creates a new entry in your Claude Sessions database. Confirm it appears in Notion with the correct title format and fields filled in.

**Test Durable Memory:**
> "Remember this: my preferred response format is bullet points."

Expected: Claude adds a bullet to your Durable Memory page or MEMORY.md under Preferences. Confirm it appears and the entry count updates.

**Test Standing Orders:**
> "Every Monday, remind me to review my open session loops. Expected output: a bullet list of open items."

Expected: Claude creates a new row in your Standing Orders database with Cadence = Weekly and Expected Output filled in.

**Test Category Pages:**
> "Save this as a research note: 'Setup test complete. Memory OS is live.'"

Expected: Claude creates a new page under your Research category page.

**Test Routing:**
> "Where should I save a competitive analysis I just finished?"

Expected: Claude says "Category Pages → Research" without asking for clarification. If it asks "where should I save this?" your Routing Rules in Durable Memory are incomplete — add them.

**Full system check:**
> "Run a quick health check on my memory OS. Tell me what's configured and what's missing."

Expected: Claude reads your Durable Memory, confirms it knows your database names, and flags any missing routing rules or configuration gaps.

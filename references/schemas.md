# Schemas

Suggested database and page schemas for each layer. These are starting points — adapt to your actual workflow. Do not hardcode database IDs in prompts; reference by name and store IDs in Durable Memory under Routing Rules.

---

## 1. Claude Sessions (Session Logs Database)

A Notion database. One entry per meaningful work session.

**Title format:** `YYYY-MM-DD – [2–4 word topic]`
Example: `2026-03-27 – Pricing Strategy Review`

### Required Fields

| Field | Type | Notes |
|---|---|---|
| Session Title | Title | Format: `YYYY-MM-DD – [2–4 word topic]` |
| Date | Date | Session date |
| Summary | Text | 2–3 sentences max — what happened, what was decided, what's next |
| Decisions | Text | Bullet list of key decisions only |
| Next Actions | Text | Concrete follow-ups with owners |
| Open Loops | Text | Unresolved threads that need follow-up |

### Recommended Fields

| Field | Type | Notes |
|---|---|---|
| Key Outputs | Text | Links to docs/files — not the content itself |
| Area / Topic | Select | Homelab · Research · Consulting · Automation · General |
| Related Project | Relation | Link to project or category page if relevant |
| Status | Select | Active / Closed / Paused |
| Importance | Select | High / Medium / Low |
| Source Channel | Text | Where the session happened (Claude Code, Web, OpenClaw, etc.) |
| Session ID / Link | URL | Optional link to session thread or export |

**Hard limit: Under 300 words per entry.**

### Minimal Variant (Solo / Light Use)

Keep only: Session Title, Date, Summary, Next Actions, Open Loops.

### Heavy Operator Variant

Add: Sprint or Milestone, Participants, Time Spent, Linked Standing Orders.

---

## 2. Standing Orders Database

A Notion database. One entry per recurring obligation. Every order must have a cadence and an expected output.

### Required Fields

| Field | Type | Notes |
|---|---|---|
| Name | Title | Short descriptive name |
| Status | Select | Active / Paused / Completed |
| Cadence | Select | Daily / Weekly / Monthly / Event-triggered |
| Purpose | Text | Why this order exists |
| Expected Output | Text | What is produced each cycle |

### Recommended Fields

| Field | Type | Notes |
|---|---|---|
| Destination | Text | Where output goes (Notion page, channel, etc.) |
| Owner | Person or Text | Who is responsible |
| Last Run | Date | When last executed |
| Next Run | Date | When due next |
| Notes | Text | Special conditions, edge cases, constraints |

### Minimal Variant

Keep only: Name, Status, Cadence, Purpose.

---

## 3. Durable Memory

A single Notion page — not a database. Keep it short. This is not a diary.

### Recommended Page Structure

```
## Preferences
- Always format code in Python unless context specifies otherwise.
- Use UTC for all timestamps.
- Default to concise responses — no preamble, no restating the question.

## Constraints
- Never recommend per-seat SaaS above $X/user without flagging the cost.
- Avoid vendor lock-in for homelab infrastructure.

## Routing Rules
- Claude Sessions database: [name or ID — set by user]
- Standing Orders database: [name or ID — set by user]
- Durable Memory location: this page / local MEMORY.md

## Stable Facts
- Primary timezone: [user's timezone]
- Primary cloud: [user's cloud]
- Preferred stack: [user's stack]

_Last reviewed: YYYY-MM-DD | Entry count: N_
```

**Hard limits:**
- No more than 20 total bullets across all sections
- No session-specific facts, no links, no recurring duties
- Add "Last reviewed" date at the bottom after each cleanup
- Target: ≤15 bullets after quarterly pruning

### As a Notion Database (For Power Operators)

| Field | Type | Notes |
|---|---|---|
| Rule | Title | Short label for the rule |
| Type | Select | Preference / Constraint / Routing / Fact / Operating Rule |
| Value | Text | The actual rule content |
| Added | Date | When this was created |
| Scope | Select | Global / Project-specific |
| Active | Checkbox | Whether currently in effect |

---

## 4. Category Pages

Not a single database — a set of Notion pages organized by category. Each page holds related documents.

### Core Category Schema (apply to each page)

| Field | Type | Notes |
|---|---|---|
| Title | Title | Descriptive — include date or version if relevant |
| Date Created | Date | |
| Last Updated | Date | |
| Status | Select | Draft / Active / Archived |
| Related Sessions | Relation | Links to Claude Sessions entries that produced this |
| Tags | Multi-select | For cross-category search |
| Content | Page body | The actual long-form content |

### Per-Category Field Additions

| Category | Additional Fields |
|---|---|
| **Research** | Source URLs, Key Findings, Confidence Level |
| **Revenue** | Period (week/month/quarter), Amount, MoM Delta |
| **Ops** | System/Tool, Environment (prod/staging/local) |
| **SOPs** | Version, Last Reviewed, Steps (numbered list) |
| **Ideas** | Stage (Raw / Evaluated / Killed / Active), Priority |
| **Daily Logs** | Day (date), Focus Areas, Blockers |

### Recommended Categories

| Category | Use for |
|---|---|
| **Research** | Research documents, competitive analysis, market notes |
| **Revenue** | Pricing, sales analysis, revenue plans, weekly digests |
| **Ops** | Operational notes, infrastructure, processes in progress |
| **SOPs** | Standard operating procedures, step-by-step guides |
| **Ideas** | Early-stage ideas, concepts, things worth exploring |
| **Daily Logs** | Day-level operational notes (not session continuity) |
| **Plans** | Project roadmaps, strategic plans, execution plans |

### Minimal Variant (Solo Builder)

Use just: Research, Ops, Ideas. Add others when the need is concrete.

### Advanced Variant (Teams / Operators)

Add: Projects (with subpages per project), Clients, Assets, Archive.

---

## Schema Design Principles

1. **Use as few required fields as possible.** The system only works if people actually fill it in.
2. **Never hardcode page IDs in prompts.** Store them in Durable Memory under Routing Rules, reference by name everywhere else.
3. **Keep session logs short.** If the Summary field is more than 3 sentences, it's too long.
4. **Don't add a Recommendations field.** Route recommendations into the relevant category.
5. **Standing Orders must have Status.** Inactive duties should be Paused, not deleted.
6. **Durable Memory is a page, not a log.** No date as the primary organizer.
7. **Cross-link, don't duplicate.** Category Pages link to Sessions; Sessions link to Category Pages.

# Schemas

## 1. Claude Sessions

| Field | Type | Notes |
|---|---|---|
| Session Title | Title | Format: `YYYY-MM-DD – [2-4 word topic]` |
| Date | Date | Session date |
| Area / Topic | Select | Homelab, Research, Consulting, Automation, General |
| Summary | Text | 2–3 sentences max |
| Decisions | Text | Bullet list of key decisions |
| Next Actions | Text | Concrete follow-ups |
| Open Loops | Text | Unresolved threads |
| Key Outputs | Text | Links to docs/files — not the content itself |
| Related Project | Relation | Link to project page if relevant |
| Status | Select | Active / Closed / Paused |
| Importance | Select | High / Medium / Low |

**Target length:** Under 300 words per entry.

---

## 2. Standing Orders

| Field | Type | Notes |
|---|---|---|
| Name | Title | Short descriptive name |
| Status | Select | Active / Paused / Completed |
| Cadence | Select | Daily / Weekly / Monthly / Event-triggered |
| Purpose | Text | Why this order exists |
| Expected Output | Text | What is produced each cycle |
| Destination | Text | Where output goes |
| Owner | Person | Who is responsible |
| Last Run | Date | When last executed |
| Next Run | Date | When due next |
| Notes | Text | Special conditions, edge cases |

---

## 3. Durable Memory

Preferred format: a single Notion page with grouped sections (not a database).

```
## Preferences
- Always format code in Python unless specified otherwise.
- Use UTC for all timestamps.

## Constraints
- Never recommend SaaS tools with per-seat pricing above $X/user.

## Routing Rules
- Claude Sessions database: [configured by user]
- Durable Memory location: this page OR local MEMORY.md

## Stable Facts
- Company timezone: America/Detroit
- Primary cloud: AWS us-east-1
- Preferred LLM: claude-sonnet-4
```

**Hard limits:**
- No more than 20 total bullets across all sections.
- No session-specific facts. No links. No recurring duties.
- Review and prune quarterly.

---

## 4. Category Pages

| Field | Type | Notes |
|---|---|---|
| Title | Title | Descriptive |
| Date Created | Date | |
| Last Updated | Date | |
| Status | Select | Draft / Active / Archived |
| Related Sessions | Relation | Link to Claude Sessions entries |
| Tags | Multi-select | For cross-category search |
| Content | Page body | The actual long-form content |

**Category variants:**
- Research: add Source URLs, Key Findings fields
- Revenue: add Period, Amount fields
- Ops: add System/Tool, Environment fields
- SOPs: add Version, Last Reviewed, Steps fields
- Ideas: add Stage (Raw/Evaluated/Killed/Active), Priority fields

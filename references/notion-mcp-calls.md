# Notion MCP Call Templates

Standardized patterns for Claude to interact with Notion via the MCP (Model Context Protocol). Use these when executing reads and writes against the four destinations.

**Prerequisites:**
- Notion MCP configured and connected
- Database IDs stored in Durable Memory under "Routing Rules" (never hardcode in prompts)
- Property names must match exactly — Notion is case-sensitive

---

## 0. Before Any Write: Read First

For Durable Memory updates, always read the current page before writing to identify the correct section. Never overwrite the entire page.

For Session Logs and Standing Orders, confirm the database name matches what's in Durable Memory routing rules before inserting.

---

## 1. Save a Session Log Entry

**When:** End of a session with 3+ meaningful exchanges, or when user says "log this session" / "summarize this session."

**Operation:** Create a new page in the Claude Sessions database.

```
notion-create-pages
  parent: { database_id: [SESSIONS_DB_ID from Durable Memory] }
  properties:
    Session Title: "YYYY-MM-DD – [2-4 word topic]"
    Date: [today's date]
    Area / Topic: [relevant area]
    Summary: "[2-3 sentences: what happened, decided, next]"
    Decisions: "[bullet list of decisions]"
    Next Actions: "[concrete next steps with owners]"
    Open Loops: "[unresolved questions needing follow-up]"
    Key Outputs: "[links to outputs — not content]"
    Status: "Active"
    Importance: "[High/Medium/Low]"
```

**Success:** Confirm to user: "Session logged: [title]"
**Failure:** Report: "Could not save session log — [reason]. Check that the Claude Sessions database exists and the MCP is connected."

---

## 2. Create a Standing Order

**When:** User says "track this weekly," "watch for X," "check this every Monday," or similar recurring duty.

**Operation:** Create a new page in the Standing Orders database.

```
notion-create-pages
  parent: { database_id: [STANDING_ORDERS_DB_ID from Durable Memory] }
  properties:
    Name: "[short descriptive name]"
    Status: "Active"
    Cadence: "[Daily/Weekly/Monthly/Event-triggered]"
    Purpose: "[why this order exists]"
    Expected Output: "[what is produced each cycle]"
    Destination: "[where output goes]"
    Next Run: [next scheduled date]
```

**Success:** Confirm: "Standing order created: [name], cadence: [cadence]"
**Failure:** Report the error and confirm the database ID is correctly set in Durable Memory.

---

## 3. Update a Standing Order (Log a Run)

**When:** A standing order has been executed. Log completion and set next run date.

**Operation:** Update the existing Standing Order page.

```
notion-update-page
  page_id: [STANDING_ORDER_PAGE_ID]
  properties:
    Last Run: [today's date]
    Next Run: [next scheduled date based on cadence]
    Status: "Active"
    Notes: "[optional: any issues or observations from this run]"
```

---

## 4. Save a Category Page (Long-Form Output)

**When:** User produces research, a plan, an SOP, or other long-form output that belongs in a category page.

**Operation:** Create a new page under the appropriate category page.

```
notion-create-pages
  parent: { page_id: [CATEGORY_PAGE_ID from Durable Memory] }
  properties:
    Title: "[descriptive title — include date or version if relevant]"
    Date Created: [today's date]
    Status: "Draft"
    Tags: ["[relevant tags]"]
  children: [page content blocks]
```

**Then:** Add a link to this page in the Key Outputs field of the current session log.

**Success:** Confirm: "Saved to [category]: [title]"

---

## 5. Update Durable Memory

**When:** User explicitly sets a new preference, constraint, routing rule, or stable fact.

**Critical:** Always read the current Durable Memory page first. Use targeted edits to the correct section — never rewrite the entire page.

```
# Step 1: Read current page
notion-fetch
  url: [DURABLE_MEMORY_PAGE_URL from Durable Memory routing rules]

# Step 2: Identify the correct section (Preferences / Constraints / Routing / Stable Facts)

# Step 3: Append to the correct section only
notion-update-page
  page_id: [DURABLE_MEMORY_PAGE_ID]
  [append new bullet to the correct section]
  [update "Last reviewed" date and entry count at bottom]
```

**After update:** Confirm count stays ≤20 bullets. If it exceeds 20, flag it: "Durable Memory now has [N] bullets — consider pruning."

---

## 6. Query Existing Entries

**When:** User asks "what did we decide last week?" or "what standing orders are active?"

**Session Logs query:**
```
notion-fetch or notion-search
  filter: database = Claude Sessions, Date = [range]
  sort: Date descending
```

**Standing Orders query:**
```
notion-fetch or notion-search
  filter: database = Standing Orders, Status = Active
```

**Durable Memory read:**
```
notion-fetch
  url: [DURABLE_MEMORY_PAGE_URL]
```

---

## 7. Error Handling

| Error | Response |
|---|---|
| Database not found | "I couldn't find the [database name] database. Please confirm the name matches what's in your Durable Memory routing rules." |
| Property name mismatch | "The property '[name]' wasn't found. Check that property names in the schema match exactly (case-sensitive)." |
| Rate limited | Retry once after a brief pause. If it fails again, report to user. |
| MCP not connected | "The Notion MCP doesn't appear to be connected. Check your MCP configuration and reconnect." |
| Permission denied | "Claude doesn't have write access to this page. Check that the Notion integration has the required permissions." |

**General rule:** Always confirm success or report failure explicitly. Never silently drop a write.

---

## Setup Checklist

Before using MCP calls, confirm:

- [ ] Notion MCP is connected (`notion-fetch` works on any page)
- [ ] Claude Sessions database exists with correct property names
- [ ] Standing Orders database exists with correct property names
- [ ] Durable Memory page exists and has a Routing Rules section
- [ ] Database IDs or page names are stored in Durable Memory routing rules
- [ ] Claude has been told where to find the routing rules

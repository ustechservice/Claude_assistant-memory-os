# Notion MCP Call Templates

Exact Notion MCP call sequences for each destination. Use these as the
canonical patterns — Claude should follow these templates, not improvise.

Assumes Notion MCP is connected and the user has configured database IDs
in Durable Memory. Replace `[DATABASE_ID]` and `[PAGE_ID]` with actual values.

---

## 1. Save a Claude Session Entry

```
Tool: notion-create-pages
Parameters:
  parent data_source_id: [CLAUDE_SESSIONS_DB_ID]
  properties:
    "Session Title":   "YYYY-MM-DD – [2-4 word topic]"
    "date:Date:start": "YYYY-MM-DD"
    "date:Date:is_datetime": 0
    "Area":            "[Homelab|Research|Consulting|Automation|General]"
    "Status":          "Active"
    "Importance":      "[High|Medium|Low]"
    "Summary":         "[2-3 sentence summary]"
    "Decisions":       "[bullet list of decisions]"
    "Next Actions":    "[concrete follow-ups]"
    "Open Loops":      "[unresolved threads, if any]"
    "Key Outputs":     "[links to any docs/files produced]"
  content: |
    ## Summary
    [2-3 sentences]

    ## Decisions & Outcomes
    - [decision 1]
    - [decision 2]

    ## Next Actions
    - [action 1]
    - [action 2]

    ## Open Loops
    - [loop 1, if any]
```

**Confirm with:** `"Saved to Notion: [Session Title]"`

---

## 2. Create a Standing Order

```
Tool: notion-create-pages
Parameters:
  parent data_source_id: [STANDING_ORDERS_DB_ID]
  properties:
    "Name":            "[short descriptive name]"
    "Status":          "Active"
    "Cadence":         "[Daily|Weekly|Monthly|Event-triggered]"
    "Purpose":         "[why this order exists]"
    "Expected Output": "[what gets produced each cycle]"
    "Destination":     "[where output goes]"
    "Next Run":        "[YYYY-MM-DD of next due date]"
    "Notes":           "[edge cases or special conditions]"
```

**Confirm with:** `"Standing Order created: [Name] — runs [Cadence]"`

---

## 3. Update a Standing Order (after execution)

```
Tool: notion-update-page
Parameters:
  page_id: [STANDING_ORDER_PAGE_ID]
  properties:
    "Last Run": "[YYYY-MM-DD]"
    "Next Run": "[YYYY-MM-DD]"
    "Status":   "Active"
```

---

## 4. Save to a Category Page

```
Tool: notion-create-pages
Parameters:
  parent data_source_id: [CATEGORY_PAGES_DB_ID]
  properties:
    "Title":        "[descriptive title]"
    "Category":     "[Research|Revenue|Ops|Ideas|SOPs|Daily Logs]"
    "Status":       "Active"
    "Tags":         ["[tag1]", "[tag2]"]
  content: |
    [full long-form content here]
```

**Confirm with:** `"Saved to [Category]: [Title]"`

---

## 5. Update Durable Memory

Durable Memory is a single page, not a database entry. Use append or
section-targeted edits rather than rewriting the whole page.

```
Tool: notion-update-page  (for property changes)
  OR
Tool: notion-create-pages with parent = Durable Memory page (for block appends)

Best practice:
  1. Read the current Durable Memory page first
  2. Identify the correct section (Preferences / Constraints / Routing Rules / Stable Facts)
  3. Append the new bullet to that section only
  4. Do NOT rewrite the full page — targeted edits only
```

**Confirm with:** `"Added to Durable Memory: [brief description of what was saved]"`

---

## 6. Error Handling

If a Notion MCP call fails:

| Error | Action |
|---|---|
| `database_not_found` | Ask user to confirm the database ID/name |
| `unauthorized` | Check Notion MCP connection and permissions |
| `rate_limited` | Wait 1–2 seconds and retry once |
| `property_not_found` | Check that property name matches exactly (case-sensitive) |
| Any other failure | Report the error, offer to retry or save locally |

Never silently fail. Always confirm success or report failure.

---

## 7. Reading Back Data

**Find recent sessions:**
```
Tool: notion-search
Query: "[topic keyword]"
Filter: database = Claude Sessions
Sort: Date descending
```

**Check active Standing Orders:**
```
Tool: notion-fetch
URL: [Standing Orders database URL]
Filter: Status = Active
Sort: Next Run ascending
```

**Read Durable Memory:**
```
Tool: notion-fetch
URL: [Durable Memory page URL]
```

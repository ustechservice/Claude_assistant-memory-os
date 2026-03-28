# Notion Layouts

## Layout 1: Minimal (Solo Builder)

```
📁 Assistant OS
├── 🗓 Claude Sessions        [Database: table, sorted by date desc]
├── 📋 Standing Orders        [Database: table, filtered Status = Active]
├── 🧠 Durable Memory         [Single page, flat bullet list]
└── 📁 Knowledge
    ├── Research
    ├── Ideas
    └── Ops
```

---

## Layout 2: Notion-First (Standard Operator)

```
📁 Assistant OS
├── 🗓 Claude Sessions        [Database]
├── 📋 Standing Orders        [Database]
├── 🧠 Durable Memory         [Single page]
└── 📁 Category Pages         [Database with Category property]
    ├── View: Research
    ├── View: Revenue
    ├── View: Ops
    ├── View: Ideas
    ├── View: SOPs
    └── View: Daily Logs
```

**Recommended Claude Sessions views:**
- All Sessions (table)
- Active (filter: Status = Active, sort: Date desc)
- By Area (board grouped by Area)

**Recommended Standing Orders views:**
- Active Duties (filter: Status = Active)
- Due This Week (filter: Next Run ≤ 7 days)

---

## Layout 3: Hybrid (Local Memory + Notion)

```
📁 Assistant OS (Notion)
├── 🗓 Claude Sessions        [Database]
├── 📋 Standing Orders        [Database]
└── 📁 Category Pages         [Database or page hierarchy]

📄 MEMORY.md (local file — injected into system prompt or read at session start)
    Sections: Preferences, Constraints, Routing Rules, Stable Facts
```

Use hybrid when:
- You inject context into a system prompt at session start
- You use a wrapper like OpenClaw that reads local files
- You want Durable Memory version-controlled in git

**Sync rule:** `MEMORY.md` is the source of truth. Don't maintain two competing copies.

---

## Layout 4: Team / Advanced Operator

```
📁 Team Assistant OS
├── 🗓 Claude Sessions        [Database + Owner field]
├── 📋 Standing Orders        [Database + Owner + SLA fields]
├── 🧠 Shared Constraints     [Single page — team-wide rules only]
├── 🧠 Personal Memory        [One page per user]
└── 📁 Category Pages
    ├── Research (shared)
    ├── Revenue (restricted)
    ├── Ops (shared)
    ├── Projects (per-project pages)
    └── SOPs (shared, versioned)
```

---

## Configuring Claude to Use Your Layout

Tell Claude:
1. The name/ID of your Claude Sessions database
2. The name/ID of your Standing Orders database
3. The name/ID of your Category Pages database or parent page
4. Whether Durable Memory is a Notion page or local `MEMORY.md`

Store this configuration in Durable Memory under "Routing Rules."
Do not hardcode private IDs in this skill — users set their own.

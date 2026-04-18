# Notion Layouts

Example workspace structures for different operator types. These are starting points — adapt to your setup.

**Critical rule:** Do not hardcode database names or page IDs in this skill or in prompts. Store them in Durable Memory under "Routing Rules." This keeps the system portable and editable without breaking anything.

---

## Layout 1: Minimal (Solo Builder)

Best for: freelancers, indie builders, solo founders who want lightweight continuity without overhead.

```
Workspace Root
│
├── 📓 Claude Sessions         [Database — Session Logs]
├── 🧠 Memory                  [Page — Durable Memory, plain text]
├── 📋 Standing Orders         [Database — Recurring Duties]
└── 📁 Notes
    ├── Research
    ├── Ops
    └── Ideas
```

**How it works:**
- Every meaningful session gets a row in Claude Sessions
- Memory is a single page with four sections: Preferences, Rules, Constraints, Routing
- Standing Orders tracks the handful of recurring duties
- Notes is a simple folder — drop documents in the right subfolder

**Durable Memory entry for routing:**
```
## Routing Rules
- Claude Sessions: "Claude Sessions" database
- Standing Orders: "Standing Orders" database
- Research outputs: Notes > Research
```

**When to use:** You're just starting, or you want the lowest-friction system that actually works.

---

## Layout 2: Standard (Notion-First Operator)

Best for: founders, operators, and builders who use Notion as their primary operating system.

```
Workspace Root
│
├── 🤖 Assistant OS
│   ├── 📓 Claude Sessions     [Database]
│   ├── 📋 Standing Orders     [Database]
│   └── 🧠 Durable Memory      [Page]
│
└── 📚 Knowledge
    ├── 🔬 Research
    ├── 💰 Revenue
    ├── ⚙️ Ops
    ├── 💡 Ideas
    ├── 📄 SOPs
    └── 📅 Daily Logs
```

**How it works:**
- "Assistant OS" is the continuity layer — session state, standing orders, memory
- "Knowledge" is the output layer — where documents, plans, and research live
- Session logs link to knowledge pages when outputs are produced
- Standing Orders has its own database with Status, Cadence, Last Run, Next Run

**Suggested views:**
- Claude Sessions: All sessions (default), By Area (filtered), Open Loops (filter: Open Loops not empty), Closed (filter: Status = Closed)
- Standing Orders: Active (filter: Status = Active), Due This Week (filter: Next Run ≤ 7 days)

**When to use:** You're already using Notion seriously and want a clean separation between session state and durable knowledge.

---

## Layout 3: Hybrid (Local Memory + Notion)

Best for: developers and operators using Claude Code or OpenClaw who want local memory control with Notion as the richer record.

```
Local (MEMORY.md or Claude Code memory system)
│
└── Durable Memory             [lean, behavior-shaping facts only]
    ├── Preferences
    ├── Constraints
    ├── Operating Rules
    └── Routing Rules → points to Notion databases by name

Notion Workspace
│
├── 📓 Claude Sessions         [Database — Session Logs]
├── 📋 Standing Orders         [Database — Recurring Duties]
└── 📚 Knowledge
    ├── Research
    ├── Revenue
    ├── Ops
    ├── Ideas
    └── SOPs
```

**How it works:**
- Durable Memory stays local — small, fast to read, version-controllable with git
- Session continuity and standing orders live in Notion where they're easy to browse and edit
- Long-form outputs live in Notion knowledge pages
- Local memory contains only facts that shape behavior; Notion contains richer context

**Local MEMORY.md structure:**
```markdown
## Preferences
- [preference]: [value]

## Operating Rules
- [rule]

## Constraints
- [constraint]

## Routing
- Session logs: Claude Sessions (Notion)
- Research outputs: Research page (Notion)
- Recurring duties: Standing Orders (Notion)
- Durable Memory: this file (local)
```

**When to use:** You want fast local memory reads, version control over operating rules, and Notion for everything richer.

---

## Layout 4: Advanced (Teams / Multi-Project Operators)

Best for: small teams, agencies, or operators managing multiple projects with shared assistant workflows.

```
Workspace Root
│
├── 🤖 Assistant OS
│   ├── 📓 Sessions            [Database — all sessions, filterable by project/owner]
│   ├── 📋 Standing Orders     [Database — team-wide, filterable by owner]
│   └── 🧠 Team Memory         [Page — shared operating rules and preferences]
│
├── 📁 Projects
│   ├── Project Alpha
│   │   ├── Sessions (filtered view of main DB)
│   │   ├── Research
│   │   ├── Plans
│   │   └── SOPs
│   └── Project Beta
│       └── (same structure)
│
└── 📚 Shared Knowledge
    ├── Research
    ├── SOPs
    └── Templates
```

**How it works:**
- One Sessions database with a "Project" relation field — use filtered views per project
- Standing Orders are team-level; individual obligations filtered by Owner
- Each project has its own knowledge structure with linked sessions
- Shared Knowledge holds cross-project documents and reusable templates
- Team Memory stores shared operating rules; individual members may have local Durable Memory files

**Additional schema fields for this layout:**
- Sessions: add Owner (Person), Project (Relation)
- Standing Orders: add Owner (Person), Team (Select)

**When to use:** Multiple people or projects using the same assistant workflow and needing shared continuity without stepping on each other.

---

## General Setup Principles

1. **Name your databases and pages clearly.** "Claude Sessions" is better than "DB1" or "Notes."
2. **Store IDs in Durable Memory.** If you need database IDs for MCP calls, put them in the Routing Rules section of Durable Memory — not in prompts.
3. **Use views, not duplicate databases.** One Sessions database with filtered views per project beats many separate databases.
4. **Keep the Assistant OS section separate from project knowledge.** Mixing them creates confusion about where to look.
5. **Add an Archive view to every database.** Old sessions, completed standing orders, and outdated entries should be archived — not deleted.
6. **Human-editability is non-negotiable.** The system must be readable and editable by you without Claude. If it only makes sense to the assistant, it will break.
7. **Start minimal.** Add layouts and categories only when a concrete need exists. Premature structure creates maintenance burden.

---

## Quick Reference: Where Each Layer Lives

| Layer | Notion-First | Hybrid | Minimal |
|---|---|---|---|
| Session Logs | Claude Sessions DB | Claude Sessions DB | Claude Sessions DB |
| Durable Memory | Page in Assistant OS | Local MEMORY.md | Single Notion page |
| Standing Orders | Standing Orders DB | Standing Orders DB | Standing Orders DB |
| Category Pages | Knowledge section | Knowledge in Notion | Notes folder |

# Examples

Concrete good and bad examples for every layer. Use these to calibrate routing decisions and validate quality before saving.

---

## Session Logs — Good Examples

### ✅ Good: Concise, decision-focused

```
Title: 2026-03-27 – Pricing Strategy Review
Area: Revenue
Summary: Reviewed three pricing tiers. Decided to drop the starter tier and consolidate
         into two: Pro ($49) and Team ($149). Need to update landing page and brief sales.
Decisions:
  - Drop starter tier
  - New pricing: Pro $49 / Team $149
Next Actions:
  - Update pricing page — design, by Friday
  - Brief sales team — VP Sales, by EOW
Open Loops:
  - Do existing starter users get grandfathered or migrated? (needs decision)
Key Outputs: [Pricing Analysis Doc](link)
Status: Active
```

**Why it's good:** Short, scannable. Decisions are clear. Next actions have owners and dates. One real open loop. Key output is linked, not duplicated.

---

### ✅ Good: Technical session, minimal but complete

```
Title: 2026-03-26 – Proxmox VLAN Routing
Area: Homelab
Summary: Resolved VLAN isolation issue on pve-01. Identified misconfigured bridge on
         vmbr1 causing cross-VLAN bleed. Applied fix and validated with ping sweep.
Decisions:
  - Use tagged VLANs on all VM bridges going forward
  - Disable VLAN-aware on bridges that don't need it
Next Actions:
  - Document final VLAN map in Ops page
  - Test failover on pve-02 next session
Open Loops:
  - VLAN 20 latency spike under load — needs investigation
Key Outputs: [Link to Ops/VLAN-Config-2026-03-26]
```

**Why it's good:** Technical decisions are captured precisely. Config details live in the linked Ops page, not pasted here.

---

## Session Logs — Bad Examples

### ❌ Bad: Transcript masquerading as a log

```
Title: Session March 27
Summary: We started by talking about the pricing strategy. I mentioned that the starter
tier wasn't performing well. Then we discussed what the market looked like. The user
asked about what competitors charge. I looked up three competitors. User said they might
want to drop the starter tier. We went back and forth on whether $49 was the right
number for Pro. Eventually landed on $49. Then we talked about the landing page...
[continues for 800 more words]
```

**Why it's bad:** This is a transcript. Nobody will read it. The signal is buried in noise. Summarize to 2–3 sentences and extract the actual decisions.

---

### ❌ Bad: Duplicating what's already in Durable Memory

```
Title: Session March 27
Summary: User prefers bullet points over prose. User works in EST. User doesn't like
long explanations. [Preferences already in Durable Memory.]
```

**Why it's bad:** These are durable preferences, not session decisions. They already exist in Durable Memory. Re-saving them here creates duplicates that will drift out of sync.

---

## Durable Memory — Good Examples

### ✅ Good Durable Memory Page

```
## Preferences
- Always format code in Python unless context specifies otherwise.
- Default to concise responses — no preamble, no restating the question.
- Use UTC for all timestamps.

## Constraints
- Do not recommend per-seat SaaS above $50/user/month without flagging the cost.
- Avoid vendor lock-in for homelab infrastructure.

## Routing Rules
- Claude Sessions database: [configured by user]
- Standing Orders database: [configured by user]

## Stable Facts
- Primary timezone: America/Detroit
- Primary cloud: AWS us-east-1
- Preferred LLM: claude-sonnet-4-6

_Last reviewed: 2026-03-01 | Entry count: 8_
```

**Why it's good:** Short, unambiguous, action-shaping. Every entry changes how the assistant behaves. Has a review date and entry count.

---

## Durable Memory — Bad Examples

### ❌ Bad: Session note saved as memory

```
## Facts
- On March 27 we decided to drop the starter pricing tier.
```

**Why it's bad:** This is a session decision anchored to a specific date. It belongs in Session Logs. Durable Memory should not be a dated log.

---

### ❌ Bad: Project-specific knowledge as memory

```
## Facts
- Project Alpha uses Next.js 15 with Supabase. Main branch is "main," staging is
  "staging." Project owner is Sarah. The deploy URL is...
```

**Why it's bad:** This is project knowledge that belongs in an Ops or Plans category page. It will become stale as the project evolves and is not a behavior-shaping rule.

---

### ❌ Bad: Over-detailed rule

```
## Preferences
- When the user says "summarize this," write a 3–5 sentence summary covering the main
  topic, key decisions, next actions, open loops, broader implications, and any technical
  details if applicable. Do not use bullet points. Use full sentences. Do not use headers.
  Just prose. If the topic is technical, include the technical details but keep them...
[continues for 200 words]
```

**Why it's bad:** Too long to be useful as an operating rule. Compress: "Summaries should be 2–3 sentences in prose, covering decisions and next actions."

---

## Standing Orders — Good Examples

### ✅ Good Standing Order

```
Name: Weekly Revenue Digest
Status: Active
Cadence: Weekly (every Monday)
Purpose: Summarize MRR, churn, and new ARR vs. prior week
Expected Output: Bullet summary with week-over-week delta, flags for review
Destination: Revenue > Weekly Digests page
Last Run: 2026-03-24
Next Run: 2026-03-31
```

### ✅ Good: Monitoring task

```
Name: Competitor Pricing Watch
Status: Active
Cadence: Monthly (first Monday)
Purpose: Check if Competitor X has changed pricing or packaging
Expected Output: One-line note in Research page if changes found; nothing if no changes
Last Run: 2026-03-03
Next Run: 2026-04-07
```

**Why these are good:** Clear cadence, clear output, clear destination. No ambiguity about what to do, when, or where the result goes.

---

## Standing Orders — Bad Examples

### ❌ Bad: One-time task as a Standing Order

```
Name: Send Q1 report to board
Status: Active
Cadence: Monthly
```

**Why it's bad:** A one-time deliverable is not a standing order. Put it in Session Log next actions or a task manager.

---

### ❌ Bad: Too vague to execute

```
Name: Keep an eye on things
Status: Active
Cadence: Weekly
Purpose: General monitoring
```

**Why it's bad:** "Keep an eye on things" is not actionable. What things? What output? Where does it go? Standing orders must be specific enough to execute without asking.

---

## Category Pages — Good Examples

### ✅ Good: Research document

A Notion page titled `"AI Code Editor Competitive Analysis — March 2026"` saved to the Research category page. Contains structured sections (Overview, Competitor Profiles, Feature Matrix, Key Findings, Sources). Linked from the session log entry where it was produced.

### ✅ Good: SOP

A Notion page titled `"SOP: Weekly Revenue Pull"` saved to the SOPs category page. Contains step-by-step instructions, tools used, expected outputs, and a link to the corresponding Standing Order.

---

## Category Pages — Bad Examples

### ❌ Bad: Competitive research saved as Durable Memory

```
[In Durable Memory]
- Competitor X uses three-tier pricing starting at $19/month. Their enterprise tier is
  custom. They recently launched a free tier. Their positioning is...
[continues for 200 words]
```

**Why it's bad:** Competitive research is not a durable operating rule. It belongs in the Research category page. Durable Memory is not a knowledge base.

---

## Routing Quick Reference

| Scenario | Route To |
|---|---|
| "We decided to migrate CLI tools to Rust" | Session Logs (decision) |
| "I always want CLI tools in Rust" | Durable Memory |
| "Here's the migration plan doc" | Ops or SOPs Category Page |
| "Check CLI performance weekly" | Standing Orders |
| "Here's research on Rust vs Go" | Research Category Page |
| "What did we decide last week?" | Claude Sessions → search by date |
| "What are my preferences?" | Durable Memory |
| "What recurring tasks are active?" | Standing Orders → Active filter |
| "Today we talked about pricing" (no decisions) | Save nothing |

---

## End-of-Session Summary — Full Example

After a substantive session, a complete log entry:

```
Title: 2026-03-27 – Onboarding Flow Redesign Kickoff
Area: Product
Summary: Reviewed current onboarding flow. Identified three drop-off points at account
         creation, activation, and first key action. Agreed to redesign the activation
         step and run an A/B test between modal and inline flows.
Decisions:
  - Redesign the activation step
  - Run A/B test: modal flow vs. inline flow
Next Actions:
  - Design: deliver two variant mockups by April 3
  - Eng: set up A/B test framework by April 7
  - Data: confirm analytics are tracking the correct conversion event by March 31
Open Loops:
  - Unclear if analytics currently track the right conversion event (assigned to Data)
Key Outputs: [Onboarding Audit Doc](link)
Status: Active
```

**What makes it good:**
- One clear summary (3 sentences)
- Decisions are specific and actionable
- Next actions have owners and dates
- Open loop is a real question with an owner
- Key output is linked, not copied in
- Entire entry is readable in under 30 seconds

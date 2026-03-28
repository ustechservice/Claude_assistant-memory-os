# Examples

## Claude Sessions — Good vs Bad

### ✅ Good Session Entry
```
Title: 2026-03-27 – Proxmox VLAN Routing
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
Key Outputs: [Link to Ops/VLAN-Config-2026-03-27]
```

### ❌ Bad Session Entry
- Vague title with no date
- "Kind of worked" instead of a decision
- 300 lines of config pasted in (use a linked Ops page)
- Preferences mixed in (they belong in Durable Memory)
- Speculative ideas mixed in (they belong in Ideas page)

---

## Standing Orders — Good vs Bad

### ✅ Good Standing Order
```
Name: Weekly Revenue Digest
Cadence: Weekly (every Monday)
Purpose: Summarize revenue from prior week
Expected Output: Bullet summary, MoM delta, flags for review
Destination: Revenue > Weekly Digests page
Last Run: 2026-03-24 | Next Run: 2026-03-31
```

### ❌ Bad Standing Order
```
Name: Do revenue stuff
Cadence: Sometimes
Notes: I mentioned this once in a session
```

---

## Durable Memory — Good vs Bad

### ✅ Good Durable Memory Page
```
## Preferences
- Always format code in Python unless context specifies otherwise.
- Default to concise responses — no preamble, no restating the question.

## Constraints
- Do not recommend per-seat SaaS above $50/user/month without flagging the cost.
- Avoid vendor lock-in for homelab infrastructure.

## Routing Rules
- Claude Sessions database: [configured by user]

## Stable Facts
- Primary timezone: America/Detroit
- Company: USTechService Corporation / DarkDataLabs

Total: 8 bullets. Last reviewed: 2026-03-01.
```

### ❌ Bad Durable Memory
- Mix of session notes, life facts, opinions, and speculative ideas
- "Today we decided..." → Claude Sessions, not memory
- Personal details that don't affect behavior
- No structure, no review date

---

## Routing Quick Reference

| Scenario | Route To |
|---|---|
| "We decided to migrate CLI tools to Rust" | Claude Sessions (decision) |
| "I always want CLI tools in Rust" | Durable Memory |
| "Here's the migration plan doc" | Ops or SOPs Category Page |
| "Check CLI performance weekly" | Standing Orders |
| "Here's research on Rust vs Go" | Research Category Page |
| "What did we decide last week?" | Claude Sessions → search by date |
| "What are my preferences?" | Durable Memory |
| "What recurring tasks are active?" | Standing Orders → Active filter |

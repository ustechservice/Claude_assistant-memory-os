# Durable Memory

Behavior-shaping facts and rules for Claude. Not a diary — only add entries that actively change how Claude behaves across all sessions. Hard limit: 20 bullets total across all sections.

---

## Preferences

- [example: Always format code in Python unless context specifies otherwise.]
- [example: Default to concise responses — no preamble, no restating the question.]
- [example: Use UTC for all timestamps.]

## Constraints

- [example: Do not recommend per-seat SaaS above $X/user/month without flagging the cost.]
- [example: Avoid vendor lock-in for infrastructure choices.]

## Operating Rules

- End every meaningful session with a session log entry.
- [example: Summaries should be 2-3 sentences in prose, covering decisions and next actions.]

## Routing Rules

- Session logs: Claude Sessions database (Notion)
- Standing orders: Standing Orders database (Notion)
- Research outputs: Research page (Notion)
- Recurring duties: Standing Orders database (Notion)
- Durable Memory: this file (local)

## Stable Facts

- Primary timezone: [your timezone, e.g. America/New_York]
- Preferred stack: [e.g. Python, PostgreSQL, AWS]
- Primary cloud: [e.g. AWS us-east-1]

---

_Last reviewed: YYYY-MM-DD | Entry count: N_

---

## How to use this file

- **Add** a bullet when you say "remember this," "always do X," or "my preference is X"
- **Remove** anything that hasn't influenced behavior in 90+ days
- **Never add** session decisions, project-specific knowledge, links, or one-time instructions
- **Prune quarterly** to stay under 20 bullets (target: ≤15 after cleanup)
- **Update** the entry count and review date at the bottom after any change

Delete the example placeholders above before or as you fill in your own entries.

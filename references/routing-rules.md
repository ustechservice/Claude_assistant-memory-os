# Routing Rules

How to decide where information belongs. Apply the decision tree first, then use trigger phrases and ambiguous case resolution when needed.

---

## Decision Tree

```
Is this information worth saving at all?
│
├─ No (trivial chatter, small talk, one-liners with no decisions) → Save nothing
│
└─ Yes → Does it repeat on a schedule or condition?
          │
          ├─ Yes → STANDING ORDERS
          │
          └─ No → Is it a stable fact that shapes future behavior across all sessions?
                   │
                   ├─ Yes → DURABLE MEMORY
                   │
                   └─ No → Is it a summary, decision, or action from this session?
                            │
                            ├─ Yes → SESSION LOGS (Claude Sessions)
                            │
                            └─ No → Is it a long-form output, research, plan, or guide?
                                     │
                                     ├─ Yes → CATEGORY PAGES (pick the right category)
                                     │
                                     └─ Unclear → Ask the user, then default to Session Logs
```

**One rule for ties:** when something fits two destinations, the more specific one wins. Behavioral rule → Durable Memory. Output → Category Page. Never duplicate across layers — cross-link instead.

---

## Trigger Phrases by Destination

### → Session Logs

| Phrase | Action |
|---|---|
| "log this session" | Write session summary now |
| "summarize what we did" | Write session summary now |
| "what did we decide?" | Surface decisions from this session |
| "what are my next actions?" | List next actions from session log |
| "what's still open?" | List open loops |
| "create a handoff" | Write handoff-focused session log |
| "end of session" | Trigger end-of-session routine |
| *(3+ meaningful exchanges completed)* | Write session log automatically |

### → Durable Memory

| Phrase | Action |
|---|---|
| "remember this for future sessions" | Save to Durable Memory |
| "always do X" | Save operating rule |
| "never do X" | Save constraint |
| "my preference is X" | Save preference |
| "this is a standing rule" | Save to Durable Memory |
| "update my memory" | Review and update Durable Memory |

### → Standing Orders

| Phrase | Action |
|---|---|
| "track this weekly" | Create Standing Order (weekly cadence) |
| "watch for X" | Create Standing Order (monitoring) |
| "check this every Monday" | Create Standing Order (scheduled) |
| "report on X daily" | Create Standing Order (scheduled report) |
| "add this to my recurring duties" | Create Standing Order |
| "remind me to do X every week" | Create Standing Order |
| "monitor X and alert me when..." | Create Standing Order (conditional) |

### → Category Pages

| Phrase | Action |
|---|---|
| "save this research" | Save to Research category page |
| "document this process" | Save to SOPs category page |
| "save this plan" | Save to relevant category page |
| "log today's work" | Save to Daily Logs category page |
| "this is a guide / SOP / audit / report" | Save to appropriate category page |
| "save this for the project" | Save to relevant project or category page |

---

## Category Page Routing

When saving to Category Pages, pick the most specific category:

| Content Type | Category |
|---|---|
| Analysis, investigations, competitive research | Research |
| Revenue figures, pricing, sales summaries | Revenue |
| Infrastructure, processes, tooling notes | Ops |
| Step-by-step procedures, how-tos | SOPs |
| Early-stage concepts, things to explore | Ideas |
| Day-level operational notes | Daily Logs |

Cross-link category pages back to the Session Log entry that produced them. Do not duplicate content — link to it.

---

## Ambiguous Cases

### "Remember this" — Memory or Session Log?

- Affects behavior in **all future sessions** → Durable Memory
- Specific to **this project or session** → Session Log (or link to a note)
- If unsure: ask "should this change how I behave with you next week too?"

**Examples:**
- "Remember I prefer bullet points over prose" → Durable Memory (affects all sessions)
- "Remember we decided to drop Feature X today" → Session Log (decision, this session)

---

### "Save this" — Session Log or Category Page?

- Summary, decision, or action → Session Log
- Document, guide, research, or plan → Category Page

**Examples:**
- "Save what we decided about pricing" → Session Log (decisions field)
- "Save this pricing analysis" → Category Page → Revenue or Research

---

### "Track this" — Standing Order or Session Log?

- Check again on a future date or recurring schedule → Standing Orders
- Unresolved item from today only → Session Log (open loops field)

**Examples:**
- "Track whether the new feature ships this sprint" → Session Log open loop
- "Track competitor pricing every Monday" → Standing Orders

---

### Recommendations

Do not create a "Recommendations" bucket. Route every recommendation specifically:

- Recommendation affecting future behavior → Durable Memory
- Recommendation for a recurring report → Standing Orders
- Recommendation within a project → Category Page (relevant category)
- Recommendation made in a session → Session Log (decisions or next actions field)

---

## The Stability Test

When unsure whether something belongs in Durable Memory vs. elsewhere:

> "Will this still be true and relevant in a different session, on a different project, three months from now?"

- **Yes** → Durable Memory
- **Only in this context** → Session Log or Category Page
- **On a recurring basis** → Standing Orders

# Routing Rules

## Phrase Triggers → Destination

### → Claude Sessions
- "summarize this session" / "log what we did" / "save this conversation"
- "what did we decide?" / "write up what happened today"
- Natural end of a session with 3+ substantive exchanges

### → Standing Orders
- "watch this every week" / "remind me to check X daily"
- "track this on a schedule" / "add a standing order for..."
- "report [metric] every [cadence]" / "monitor X and alert me when..."

### → Category Pages
- "save this research" / "document this SOP" / "save this plan"
- "log this to [Revenue / Ops / Ideas / Research]"
- "write this up as a guide" / "save this audit"
- Any output longer than ~500 words that isn't just session context

### → Durable Memory
- "remember that I always..." / "I prefer..." / "never do X"
- "my rule for Y is..." / "always format Z as..."
- "my constraint is..." / "going forward, treat X as..."

### → Ambiguous: "save this" / "remember this"
Ask ONE clarifying question:
> "Should this affect how I behave going forward (memory), or is this an output
> you want to keep (save to a page)?"

If they say "both" → save the behavioral rule to Durable Memory, the output to a
Category Page. Never duplicate the full content to both.

---

## Decision Tree

```
Is this recurring or scheduled?
  → YES → Standing Orders
  → NO ↓

Is this a preference or rule that should shape future behavior?
  → YES → Durable Memory
  → NO ↓

Is this a long-form output, research, plan, or guide?
  → YES → Category Page (pick the right category)
  → NO ↓

Is this meaningful session context (decisions, next actions, open loops)?
  → YES → Claude Sessions
  → NO → Don't save it. It's probably trivial.
```

---

## Ambiguous Cases & Resolutions

| Scenario | Route |
|---|---|
| "Remember this article / link" | Category Page (Research) — not Durable Memory |
| "Remember my company uses AWS" | Durable Memory — stable behavioral fact |
| "Remember what we discussed today" | Claude Sessions |
| "Track our revenue every week" | Standing Orders |
| "I want a recommendation for X" | Relevant Category Page (Research or Ideas) |
| "Save this Proxmox config session" | Claude Sessions + link to Ops page |
| "I always want Celsius" | Durable Memory — short, stable, behavioral |
| "We decided to use Supabase" | Claude Sessions (decision) + link to Ops if doc produced |

---

## Category Page Selection Guide

| Content Type | Category |
|---|---|
| Research, literature, analysis | Research |
| Revenue data, pricing, financial logs | Revenue |
| Processes, systems, infrastructure | Ops |
| Product ideas, business concepts | Ideas |
| Repeatable procedures | SOPs |
| Day-by-day logs | Daily Logs |

---

## Cross-Destination Linking (Do This)

✅ Claude Sessions entry links to an Ops page for the full config doc.
✅ Standing Order links to its output destination page.
✅ Durable Memory references a Category Page for context.

❌ Don't copy full research into a Claude Sessions entry.
❌ Don't paste a full session into Durable Memory.
❌ Don't duplicate the same fact in both Durable Memory and Claude Sessions.

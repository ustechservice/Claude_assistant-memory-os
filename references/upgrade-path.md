# Upgrade Path: MemoryOS-MCP

When to stick with assistant-memory-os, when to add MemoryOS-MCP, and how to use both together.

---

## What Is MemoryOS-MCP

MemoryOS is a memory operating system for AI agents, developed by BAI-LAB and presented as an EMNLP 2025 oral paper (arXiv: 2506.06326). It implements hierarchical memory management inspired by how operating systems manage memory — with short-term, mid-term, and long-term storage tiers, semantic retrieval, and heat-based decay that automatically retires stale information.

MemoryOS-MCP is the production MCP server implementation of that research. It integrates with Claude and other LLMs as an enhancement layer, injecting relevant long-term memory into conversations automatically without manual routing.

---

## Architectural Comparison

| Dimension | assistant-memory-os | MemoryOS-MCP |
|---|---|---|
| **Storage** | Notion (human-readable databases and pages) | Local vector store (semantic embeddings) |
| **Memory tiers** | 4 destinations (flat routing) | 3 tiers: short-term → mid-term → long-term |
| **Routing** | Explicit (trigger phrases + decision tree) | Automatic (semantic similarity) |
| **Retrieval** | Manual (you ask Claude to read Notion) | Automatic (injected into every response) |
| **Decay** | Manual (quarterly cleanup) | Automatic (heat-based decay removes stale facts) |
| **Human readability** | High — everything lives in Notion, editable by you | Low — stored in vector embeddings, not human-browsable |
| **Infrastructure** | Notion MCP only | MemoryOS-MCP server + local vector store |
| **Setup complexity** | Low-medium (Notion setup, MCP config) | Medium-high (local server, embedding config) |
| **Works with** | Claude, Claude Code, OpenClaw | Any LLM with MCP support |

---

## What assistant-memory-os Does Better

**Human control and transparency.** Every piece of saved information is a readable Notion page or database row. You can see exactly what Claude knows, edit it directly, and prune it without running any commands.

**Intentional routing.** You decide what gets saved and where. This prevents the system from accumulating noise that looks relevant but isn't — a common failure mode in fully automatic systems.

**Notion as the workspace.** If Notion is already your operating system, keeping memory there means you can review session logs, standing orders, and category pages without switching context.

**No extra infrastructure.** One Notion MCP connection is all that's required. No local servers, no vector databases, no embedding models.

**Works across Claude, Claude Code, and OpenClaw.** Any interface that can read a system prompt and connect to Notion MCP works with this skill.

---

## What MemoryOS-MCP Does Better

**Semantic retrieval.** MemoryOS finds relevant past context using vector similarity — not keyword matching. It can surface a decision from six months ago that's relevant to today's question without you asking for it.

**Automatic decay.** A heat-based mechanism retires facts that haven't been accessed recently, keeping long-term memory lean without manual quarterly reviews.

**Longer conversation coherence.** In benchmarks on the LoCoMo dataset, MemoryOS achieves ~49% improvement on F1 and ~46% improvement on BLEU-1 over baselines — meaning it retains and surfaces relevant personal context significantly better over long conversations.

**No routing decisions required.** Everything is saved automatically; nothing falls through the cracks because you forgot a trigger phrase.

---

## When to Stick With assistant-memory-os

- Notion is your primary workspace and you want memory there
- You want to see, edit, and control exactly what Claude knows
- You're using OpenClaw and Notion MCP is already connected
- You want low infrastructure complexity
- You want human-reviewable session logs and standing orders
- You're comfortable doing quarterly memory maintenance

---

## When to Add MemoryOS-MCP

- You're having long conversations where relevant past context isn't being surfaced
- You want fully automatic memory without managing trigger phrases
- You're comfortable running a local MCP server
- You want better recall across very long time spans (months of sessions)
- You're evaluating or building on MemoryOS as a research platform

---

## Using Both Together

The two systems are complementary, not mutually exclusive.

**Recommended combined architecture:**

```
MemoryOS-MCP  →  Handles automatic retrieval and injection of past context
                  into every conversation. Short-to-long-term memory pipeline.

assistant-memory-os  →  Handles intentional routing of outputs to Notion.
                         Session logs, standing orders, category pages, and
                         durable preferences stay human-readable and editable.
```

In practice: MemoryOS-MCP surfaces relevant context automatically; assistant-memory-os ensures structured outputs land in the right Notion destination. The Durable Memory layer in Notion becomes your human-readable override — preferences and rules you want guaranteed to be applied, regardless of what the vector store retrieves.

---

## How to Evaluate MemoryOS-MCP

Before committing to the integration, run this evaluation:

1. **Install** the MemoryOS-MCP server (see the BAI-LAB GitHub: `github.com/BAI-LAB/MemoryOS`)
2. **Run 10 sessions** using only MemoryOS-MCP, no assistant-memory-os routing
3. **Test recall:** After session 5, ask Claude about something specific from session 2. Does it surface it correctly?
4. **Test decay:** After 30 days, check what's still in long-term memory. Is it the right things?
5. **Check transparency:** Can you inspect what's in the vector store? Is it editable?
6. **Decide:** If recall is strong and transparency is acceptable, integrate. If you miss the Notion layer, run both.

---

## Resources

- BAI-LAB MemoryOS GitHub: `github.com/BAI-LAB/MemoryOS`
- arXiv paper: `arxiv.org/abs/2506.06326`
- MemoryOS-MCP documentation: see the MCP section of the BAI-LAB repo

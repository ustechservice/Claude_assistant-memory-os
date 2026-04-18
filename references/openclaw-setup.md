# OpenClaw Setup

How to run assistant-memory-os with OpenClaw (formerly Clawdbot / Moltbot).

OpenClaw is a persistent local AI agent accessible via messaging platforms (WhatsApp, Telegram, Slack, Discord, iMessage, and others). Unlike Claude Code — which is a terminal tool tied to a codebase — OpenClaw runs as a long-lived process and routes conversations through whatever channels you use daily. It supports Claude via the Anthropic API.

---

## How the Two Systems Relate

OpenClaw manages **session state** — it tracks the active conversation and resets it based on idle or daily timeouts. This is short-lived context.

assistant-memory-os manages **persistent memory** — it routes decisions, preferences, recurring duties, and long-form outputs into Notion so they survive session resets. These two layers complement each other: OpenClaw handles the live conversation; Notion holds what matters across sessions.

```
You → OpenClaw (messaging interface)
         │
         ├── Active session memory (short-lived, resets on timeout)
         │
         └── Notion via MCP (durable, survives resets)
               ├── Claude Sessions DB  (session logs)
               ├── Standing Orders DB  (recurring duties)
               ├── Durable Memory page (preferences and rules)
               └── Category Pages      (long-form outputs)
```

---

## Prerequisites

- OpenClaw installed and running locally
- Claude set as the model provider (Anthropic API key configured)
- Notion MCP connected in your OpenClaw agent configuration
- Notion workspace set up per `references/quick-start.md`

---

## Step 1: Load the Skill as Base Instructions

OpenClaw supports a system prompt or base instruction set per agent. Load `SKILL.md` as the base instructions for your Claude agent.

In your OpenClaw agent config, set the system prompt to the full contents of `SKILL.md`. This gives the agent the routing model, trigger phrases, and operating rules without requiring the reference files to be present.

`SKILL.md` is self-contained — you do not need the reference files for day-to-day use.

---

## Step 2: Connect Notion MCP

OpenClaw supports MCP servers via its agent configuration. Add the Notion MCP server so Claude can read and write your Notion workspace.

Configure the Notion MCP with:
- Your Notion integration token
- Access to your Claude Sessions database
- Access to your Standing Orders database
- Access to your Durable Memory page
- Access to your Category Pages

Verify the connection by asking: `"Fetch my Durable Memory page."` Claude should return its contents.

---

## Step 3: Configure Durable Memory Location

Durable Memory for OpenClaw should live in Notion (not a local file), since OpenClaw runs across multiple devices and channels.

In your first session after setup, say:

> "I've set up my assistant memory OS. Claude Sessions is [name], Standing Orders is [name], Durable Memory is a page called [name]. Please update your routing rules and confirm."

Claude will save your routing rules to Durable Memory and confirm. From that point, all routing is automatic.

---

## Step 4: Configure Session Scoping

OpenClaw supports three session scoping modes:

| Mode | Behavior | Recommended for |
|---|---|---|
| `main` | Single global session for all conversations | Solo personal assistant |
| `per-peer` | Isolated session per user ID | Multi-user or shared setups |
| `per-channel-peer` | Isolated session per channel + user | Teams or high-traffic bots |

For personal assistant use, `main` is recommended. This gives Claude a single continuous context and triggers the end-of-session routine correctly when the session resets.

---

## Step 5: Handle Session Resets

OpenClaw can reset sessions on a daily or idle timeout. When a reset occurs, the in-session context is cleared — but your Notion memory persists.

To pick up cleanly after a reset, start with:

> "Catch me up. Read my Durable Memory and the last 3 session logs."

Claude will read your Notion workspace and resume with full context.

**Recommended:** Add this as an operating rule in Durable Memory:
> "After a session reset, read Durable Memory and the last 3 Claude Sessions entries before responding."

---

## Session Log Titles for OpenClaw

OpenClaw conversations happen across multiple channels. Add the channel to session log titles when relevant:

`YYYY-MM-DD – [topic] (WhatsApp)` or `YYYY-MM-DD – [topic] (Slack)`

This helps distinguish sessions by context when reviewing logs in Notion.

You can store this as a routing rule in Durable Memory:
> "Session log titles: include channel name in parentheses when session originated from WhatsApp, Slack, or Telegram."

---

## Key Differences from Claude Code Setup

| Aspect | Claude Code | OpenClaw |
|---|---|---|
| Interface | Terminal / IDE | Messaging apps (WhatsApp, Telegram, Slack, etc.) |
| Session model | Per project directory | Per agent (global, per-peer, or per-channel-peer) |
| Local files | MEMORY.md, CLAUDE.md auto-loaded | Durable Memory should live in Notion |
| Session resets | Manual (you end the session) | Automatic (daily/idle timeout) |
| Skill loading | Skills directory or CLAUDE.md | System prompt / base instructions |
| Codebase awareness | Yes (reads files, git history) | No |

---

## Troubleshooting

**Routing rules are lost after a session reset**
→ Durable Memory routing rules should be in Notion, not only in the active session. Confirm Claude can read your Durable Memory page via MCP.

**Claude doesn't trigger session logging after a reset**
→ After a reset, the "3+ meaningful exchanges" counter starts fresh. The log will be written at the end of the new session, not immediately.

**Notion MCP writes are failing**
→ Check that the Notion integration has write access to all four destinations. Verify the MCP server is running with `notion-fetch` on any known page.

**Session logs are getting the channel name wrong**
→ Add an explicit routing rule to Durable Memory: "Session log titles include the channel name in parentheses."

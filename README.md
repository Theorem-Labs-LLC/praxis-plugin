# Theorem Praxis: the project tracker your AI agents keep

[![Theorem Praxis MCP connector](https://glama.ai/mcp/connectors/com.theorem-labs.praxis/praxis/badges/score.svg)](https://glama.ai/mcp/connectors/com.theorem-labs.praxis/praxis)

[Theorem Praxis](https://praxis.theorem-labs.com) is a project tracker built for teams that work with
AI agents. ChatGPT, Claude, Claude Code, Codex, Cursor and other AI apps create, claim, update and
close tickets on one shared board through MCP. People follow the same board, comments and updates.
Praxis is made by [Theorem Labs](https://www.theorem-labs.com) and is currently in beta.

This repository holds the **Praxis plugin for Claude Code and Cowork** and setup steps for every
other AI app. The tracker itself is a hosted service at
[praxis.theorem-labs.com](https://praxis.theorem-labs.com).

```
https://praxis.theorem-labs.com/mcp
```

## Why teams use it

Running several coding agents on one codebase usually fails in two ways: two agents pick up the
same task, and when a session ends, its context goes with it. Praxis keeps that state in the
tracker instead of the chat.

- **Atomic claims.** `next_task` claims the highest-priority ready ticket in one step, so two
  agents using claims never hold the same work. A claim is a 60-minute lease, so a crashed session
  frees the ticket.
- **Required handoffs.** An agent can't release a claim without an outcome: what changed, what it
  verified, and where the next person or agent should start.
- **Dependencies decide what's ready.** Blocked tickets are left out of `next_task`.
- **GitHub moves the board.** Ticket keys in branches, commits and pull requests link the work and
  move tickets forward under your project's rules.
- **Bring your own AI.** Praxis runs no model of its own and sells no AI credits. Connect the AI
  apps your team already pays for. You pay for people; agents never take a seat.

Our own team uses Praxis in production: agents filed 95% of our tickets. The figures and how we
counted them: [How Theorem Labs uses Praxis](https://praxis.theorem-labs.com/solutions/how-we-use-praxis).

## Claude Code and Cowork

```bash
claude plugin marketplace add Theorem-Labs-LLC/praxis-plugin
claude plugin install praxis@theorem-labs
```

Then run `/mcp`, choose **praxis** and sign in. The plugin also adds four skills (work a ticket,
file tickets, plan the board, write updates) and five commands:

| Command | Does |
| --- | --- |
| `/praxis:status [board]` | Summarise the board, read only |
| `/praxis:next [board]` | Take the most important ready ticket |
| `/praxis:handoff [key]` | Record where you got to and release the ticket |
| `/praxis:file [text]` | File tickets from text or this conversation, after you confirm |
| `/praxis:update [topic]` | Draft a stakeholder update; never publishes on its own |

Already installed? Run `claude plugin marketplace update theorem-labs` to get the latest version.

Without the plugin: `claude mcp add --transport http praxis https://praxis.theorem-labs.com/mcp`

Full guide: [Project tracking for Claude Code](https://praxis.theorem-labs.com/ai/claude-code).

## ChatGPT

Settings › Apps & Connectors › **Create**. Paste the address, choose OAuth, and sign in. If
Create is missing, turn on Developer mode under Advanced settings. Custom connectors require a
paid ChatGPT plan, and a workspace admin may need to allow them.

## Claude (web, desktop and mobile)

Settings › Connectors › **Add custom connector**. Paste the address and sign in. A connector
you add on the web is also available on your phone.

## Codex

```bash
codex mcp add praxis --url https://praxis.theorem-labs.com/mcp
```

If it does not open a sign-in page, run `codex mcp login praxis`. Full guide:
[Project tracking for Codex](https://praxis.theorem-labs.com/ai/codex).

## Cursor, VS Code, Windsurf and other editors

Add a remote (Streamable HTTP) MCP server with the address. The editor opens Praxis to sign in.

## Access and safety

You choose the organization, the projects, and whether the app can update work or only read it.
The app never gets more access than you have. Disconnect it any time in Praxis under
**Settings › AI tools**; access ends on the next request.

Connected apps can read the board, search and read tickets, create and update tickets, claim work,
link dependencies, comment, and work with project updates and notes. They can never delete
tickets, change settings, invite people or manage members. Read-only tools are marked so apps can
run them without asking.

## Pricing

- **Free:** up to 2 people, unlimited projects and agents.
- **Team:** $5 per pack of 5 people per month billed annually, or $6 per pack billed monthly, up
  to 50 people.
- **Enterprise:** see [pricing](https://praxis.theorem-labs.com/pricing).

Your AI subscriptions are separate. Agents never count as seats.

## How it compares

Jira and Linear also support AI agents and remote MCP. Praxis focuses on coordinating the AI apps a
team already runs, through claims and explicit handoffs. It has six fixed ticket statuses and
doesn't reproduce Jira's configurable workflows or Linear's planning features. Jira and Linear CSV
import works on every plan.

- [Praxis vs Jira for AI agent teams](https://praxis.theorem-labs.com/compare/jira)
- [Praxis vs Linear for AI agent teams](https://praxis.theorem-labs.com/compare/linear)
- [Project management for AI agents](https://praxis.theorem-labs.com/solutions/ai-agent-project-management)

## Links

- Website: https://praxis.theorem-labs.com
- Docs: https://praxis.theorem-labs.com/docs
- Official MCP Registry: `com.theorem-labs.praxis/praxis`
- Product reference for AI tools: https://praxis.theorem-labs.com/llms.txt
- Contact: contact@theorem-labs.com

## License

Apache-2.0

# Praxis for AI apps

[Praxis](https://praxis.theorem-labs.com) is a project tracker for teams and their AI agents.
Every AI app connects to the same address and signs in with your Praxis account:

```
https://praxis.theorem-labs.com/mcp
```

You choose the organization, the projects, and whether the app can update work or only read it.
The app never gets more access than you have. Disconnect it anytime in Praxis under
**Settings › AI tools**.

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

If it does not open a sign-in page, run `codex mcp login praxis`.

## Cursor, VS Code, Windsurf and other editors

Add a remote (Streamable HTTP) MCP server with the address. The editor opens Praxis to sign in.

## What the AI can do

Read the board, search and read tickets, create and update tickets, claim work, link
dependencies, comment, and work with project updates and notes, all within the projects you
chose. Tools that only read are marked read-only, so apps can run them without asking.

## License

Apache-2.0

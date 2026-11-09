# Praxis plugin

Connects Claude Code and Cowork to the hosted Praxis MCP server at
`https://praxis.theorem-labs.com/mcp`, with skills and commands for working with it.

On first use, run `/mcp`, choose **praxis** and sign in. Praxis asks which organization and
projects Claude may use and whether it may update work or only read it.

## Skills

Claude loads these when a request fits:

| Skill | For |
| --- | --- |
| `praxis-work` | Taking, claiming, working and finishing or handing back a ticket |
| `praxis-intake` | Turning conversations, notes, bug reports or documents into clear, de-duplicated tickets |
| `praxis-planning` | What to do next, what is blocked, how long work takes, bulk triage |
| `praxis-updates` | Stakeholder updates, Notes and mentions |

Your team's own conventions (board names, branch names, what goes where) belong in the project's
instructions in Praxis (Project settings), which every agent reads through `praxis_meta`.

## Commands

| Command | Does |
| --- | --- |
| `/praxis:next [board]` | Take the most important ready ticket |
| `/praxis:status [board]` | Summarise the board, read only |
| `/praxis:file [text]` | File tickets from text or this conversation, after you confirm |
| `/praxis:update [topic]` | Draft a stakeholder update; never publishes on its own |
| `/praxis:handoff [key]` | Record where you got to and release the ticket |

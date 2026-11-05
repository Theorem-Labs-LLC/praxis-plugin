---
name: kanban-task
description: Manage project tickets in Praxis when working on tracked features, fixes, planning, or reviews. Use the connected project's workflow and permissions.
---

# Praxis project workflow

Call `praxis_meta` at the start of a project session. Verify the organization, project binding, role, boards, and project instructions. Tool prefixes vary by AI client; discover available Praxis tools instead of assuming a namespace.

A personal key may allow one project or several projects in one organization. When discovery lists multiple projects, confirm which one belongs to the current repository and pass its key as the `project` argument to scoped MCP tools. Use full ticket IDs. Keep the repository’s work in that selected project; ask before switching. A prompt cannot grant access beyond the key and its owner’s current permissions.

## Find and take work

Use `search_issues` to find existing tickets and `get_issue` for their current details. Use `board` for an overview and `dependencies` for blocked work. A remembered ticket state may be stale.

For a requested ticket, read it and claim it with `claim_issue` before implementation. For the next available task, use `next_task`, which selects and claims work. If new work needs a ticket, use `create_issue`; the server allocates its number.

Use boards returned by discovery. Project instructions may map repository folders to those boards. Request `create_board: true` explicitly when a new board is needed.

## Keep the record useful

Describe intended behavior and acceptance checks on the ticket. Link dependencies with `link_issues`. Use `comment_issue` for decisions, verification results, and information another person needs to continue.

Claims are leases. Respect version conflicts and existing claims; reread instead of repeatedly submitting an outdated write.

Use ticket keys in branch names and pull requests when the project uses that convention. Follow configured GitHub transitions. Record verification before marking work complete.

When handing off unfinished work, release the claim with an outcome explaining what remains. Use `changes_since` to resume from a cursor rather than rereading every ticket.

## Credentials and permissions

Keep keys in private client configuration or untracked local environment files. Never include them in tickets, comments, commits, or logs. Invitations, people management, platform administration, and key creation require a browser session.

If discovery reports the wrong organization or project, request the correct connection. For an expired key, ask its owner to edit the expiry in AI tools. A revoked key needs a replacement. To copy setup instructions again, use Setup prompt on the existing key and reuse its saved credential. A missing resource may be outside the permitted scope; do not search other organizations to bypass that restriction.

These instructions manage project work. They do not authorize unrelated code changes, deployments, or messages to other people. Follow the user's scope and the repository's applicable instructions.

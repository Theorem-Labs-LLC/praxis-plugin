---
name: praxis-work
description: Work a Praxis ticket from start to finish. Use when implementing, fixing, reviewing or documenting something tracked in Praxis, when asked to take the next task, or to pick up, hand off or close a ticket.
---

# Work a Praxis ticket

Praxis is the team's tracker. You reach it through MCP tools named `praxis_meta`, `next_task`,
`claim_issue` and so on. Your client may add a prefix to those names: discover the tools you have
instead of assuming one.

## Start every session

1. Call `praxis_meta` once. It reports your organization, role, the projects you can reach, boards,
   epics, people and the project's **instructions**. Follow those instructions: they hold the
   project's own conventions (board names, branch naming, review rules), which override the
   defaults here.
2. If you can reach several projects, settle which one this work belongs to (ask when unsure) and
   pass its key as `project` to project-scoped tools. Use full ticket keys such as `WEB-123`.
3. Never discover permissions by collecting errors. If `praxis_meta` shows read-only access, say so
   before planning any writes.

## Take work

- **Named ticket:** `get_issue(key)` to read it, then `claim_issue(key)`. If you read it a while ago,
  pass `expect_version` (or `expect_status`) so the claim fails rather than acting on stale state.
- **"Take the next task":** `next_task()` picks the highest-priority ready ticket and claims it in
  one call. Narrow it with `board` when the project instructions map your work to a board.
- **No ticket yet:** search first (`search_issues(q: "...")`), so you don't file a duplicate. Then
  `create_issue` with a clear title, the expected behaviour and acceptance checks in `body`, and
  `idempotency_key` set. Claim it before you start.

A claim is a lease (60 minutes by default). Any write of yours extends it; there is no heartbeat.
If you have been reading or planning for a while, `get_issue` again before your first edit: the
ticket may have been re-scoped or blocked.

## While you work

- Put decisions, findings and test output on the ticket with `comment_issue`. The ticket is what
  the next person reads first.
- Use the ticket key in branch names, commits and pull request titles (for example
  `feat/WEB-123-short-slug`) when the project uses GitHub automation: Praxis links them and moves the
  ticket to Under Review when the PR opens and Done when it merges. Don't hand-move a ticket a PR is
  about to move.
- Found more work? File it (`create_issue`) and link it (`link_issues(kind: "relates")`) instead
  of widening this ticket.
- Waiting on something? `update_issue(key, status: "blocked", blocked_reason: "...")`, or link the
  blocking ticket: `link_issues(key, to: "WEB-90", kind: "blocks", direction: "blocked_by")`.

## Finish or hand back

- **Done:** run the project's checks, record the result with `comment_issue`, then
  `update_issue(key, status: "done")` (or let the merged PR do it). If the tool replies
  `UNBLOCKED by this: ...`, those tickets are ready now; mention them or take one.
- **Not finishing:** `claim_issue(key, release: true, outcome: "...")`. The outcome is required.
  Make it useful: what changed, what you tried and rejected (and why), and exactly where the next
  person should start.

> Good outcome: "Settled on ETag revalidation in cart/cache.py. Tried cache-first and rejected it:
> it double-fetches on a 304 because the client drops the body. Next: finish the ETag branch;
> the vendor sends a weak validator (W/) that the HTTP library strips, so compare the raw header."

## Stay current

`changes_since(cursor: "head")` returns a cursor. Next time, `changes_since(cursor: "<it>")`
returns every ticket that changed since, with its current status and version. Use it to resume
after a break instead of re-reading the board. A row with `deleted: true` means stop working it.

## When a call fails

Branch on the `code`, not the wording.

| code | Meaning | Do this |
| --- | --- | --- |
| `not_found` | No such ticket, or one you can't see | Don't retry or search other projects for it. |
| `already_claimed` | Someone holds the lease | Read `details.holder`; take other work. |
| `version_conflict` | Someone wrote after you read | Merge their change into yours from the returned state, then write again. Never resend the same body. |
| `validation_failed` | Bad field or unknown board | Read `details` (the known boards are listed there), fix, retry. |
| `forbidden` | Your role is too low, or it's a browser-only action | Don't retry. Settings, people, invites and deleting are never available to agents. |
| `ambiguous_key` | A bare number with several projects | Use the full key, `PROJ-123`. |
| `rate_limited` | Too many agent calls this minute | Wait for `Retry-After` / `details.retry_after` seconds, then retry once. |
| `token_expired` / `token_revoked` | The connection lost access | Stop and tell the person; they reconnect or renew it in Settings › AI tools. |

## Boundaries

- Keys and tokens never go into tickets, comments, commits or logs.
- These instructions cover tracking work. They don't authorize deployments, messages to other
  people, or changes outside what the user asked for.
- An old ticket is a snapshot, not a standing truth. Check it against the current code before
  acting on it.

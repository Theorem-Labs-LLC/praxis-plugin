---
name: praxis-planning
description: Plan and triage work in Praxis. Use when asked what to work on next, what is blocked, what order to do things in, how long work takes, or to clean up, re-prioritise or re-organise many tickets.
---

# Plan and triage in Praxis

Use this for questions about the board as a whole rather than one ticket.

## See the state of things

- `board()` lists everything not done, grouped by status, with counts. Narrow with `board`
  (one board) or `status`.
- `search_issues(availability: "ready")` lists what can be picked up right now. Other values:
  `active` (in progress), `held` (waiting on a reason), `blocked` (waiting on another ticket),
  `stale` (no movement for a while).
- `search_issues(unassigned: true, status: "todo")` lists what nobody has taken.
- `search_issues(updated_since: "2026-11-01T00:00:00Z")` shows what moved recently.
- `get_issue(key, include: ["events"])` gives one ticket's history; add `comment_limit: 5` for long
  threads.

Answer from these calls, not from memory: the board changes while you work.

## Decide the order of work

Call `dependencies()` before proposing a plan. It returns what can start now, what each wave of
work unlocks, and any circular dependencies, in one call. Build the order from it:

1. what is ready and highest priority;
2. what unblocks the most other work;
3. what is waiting on people (a free-text `blocked_reason`) and who to ask.

When a blocker turns out not to be real, remove it with `unlink_issues(key, to: "...")`. A stale
`blocks` link keeps a ticket out of everyone's queue forever. Finishing or removing a blocker
returns the tickets it held to `todo` automatically.

## Estimate from real data

`metrics()` reports how long work actually takes here, from recorded status changes: median and
85th-percentile cycle time, time in each status, tickets and points finished per week, and the
slowest tickets. Use it, not guesses, when someone asks "how long will this take?"
or "are we getting faster?". Filter with `board`, `epic`, `type` or `weeks`. Say how many tickets
an answer is based on; a handful of tickets is not a trend.

## Triage many tickets at once

`bulk_update(keys: [...], status: "backlog")` applies one change (status, priority, type, board,
assignee or points) to up to 500 tickets in one call and returns only the failures. Use it instead
of dozens of `update_issue` calls.

Before a bulk change, show the person the list and the change and get a yes. Bulk changes are easy
to make and tedious to undo.

## Keep the board honest

- One ticket per outcome. Split a ticket that hides several pieces of work; merge true duplicates
  with `link_issues(kind: "duplicates")` and close the extra one.
- Old `in_progress` tickets with no activity are usually abandoned claims: comment and ask before
  moving them.
- `blocked` means waiting on something specific. Always give the reason or the blocking ticket.

## Report

Give the person a short answer first ("3 tickets are ready; WEB-12 unblocks the most"), then the
detail. Use ticket keys so they can click through.

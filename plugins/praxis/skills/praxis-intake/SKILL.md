---
name: praxis-intake
description: Turn conversations, meeting notes, bug reports, emails, documents or a brain-dump into clear, de-duplicated Praxis tickets. Use when asked to file, log, capture or create tickets from anything, for software or non-software teams.
---

# Turn anything into Praxis tickets

Use this when someone hands you material (a chat, call notes, a bug report, a document, a list of
ideas) and wants it tracked. The goal is a few tickets a person can act on without asking you what
you meant.

## 1. Know where tickets go

Call `praxis_meta`. Note the projects you can write to, their boards, epics and people, and the
project **instructions** (they may say how this team names, sizes or routes tickets). If more than
one project fits, ask which one before creating anything.

## 2. Pull out the work

Read the whole input first. List the distinct pieces of work: one ticket per outcome someone can
finish and check, not one per sentence. Leave out chit-chat, things already done, and decisions
that need no follow-up (those can go in a comment or a Note instead).

Keep the person's intent. Don't invent requirements, dates, owners or numbers that aren't in the
input; when something matters and is missing, write it as an open question on the ticket.

## 3. Check for duplicates before creating

For each piece, `search_issues(q: "<key words>")`, and include done tickets when it may have been
fixed before. If a ticket already covers it:

- add the new information with `comment_issue` instead of filing a duplicate, or
- if it is genuinely separate but related, file it and `link_issues(kind: "relates")`.

When the same request was clearly filed twice, link them with `kind: "duplicates"` and say which
one to keep.

## 4. Write each ticket well

`create_issue` with:

- **title**: the outcome in plain words, starting with a verb. "Let customers reset their password
  by email", not "Password issue".
- **body**, in Markdown:
  - *Context*: why it matters and where it came from (for example "From the 6 Nov support call").
  - *What should happen*: the behaviour or result wanted.
  - *Acceptance checks*: a short list someone can verify.
  - *Open questions*: anything the input didn't settle.
  - Links to files, documents or earlier tickets that help.
- **type**: `bug` for something broken, `story` for user-facing value, `task` or `chore` for the
  rest, `epic` for a group of several tickets.
- **priority**: only when the input says how urgent it is; otherwise leave the default.
- **board** / **epic**: from `praxis_meta` and the project instructions. Never invent a board name;
  pass `create_board: true` only when the person asked for a new one.
- **blocked_by**: keys of tickets that must finish first, when the input makes that clear.
- **idempotency_key**: always, so a retry after a lost response can't create a duplicate.

Several related tickets from one source? Create an `epic` first, then file the pieces with `epic`
set to it, so the plan stays together.

## 5. Report back

Tell the person what you filed, as a short list of keys and titles, which existing tickets you
updated instead, and any open questions you left on tickets. To bring someone in, find them with
`mention_targets(key: "WEB-12")` and write `@Full Name` in a comment; mention people only when the user wants
them told.

## Don'ts

- Don't assign people unless the input says to.
- Don't paste long transcripts into tickets; summarise and link the source.
- Don't file a ticket for every sentence. Five clear tickets beat twenty fragments.

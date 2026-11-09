---
name: praxis-updates
description: Tell people about work in Praxis. Use when asked to write a stakeholder update, status report, changelog or weekly summary, to share what shipped, to keep or tidy personal notes and checklists, or to mention someone.
---

# Updates, Notes and mentions

Praxis has two places for writing that isn't a ticket:

- **Updates**: plain-language posts for stakeholders about what shipped, what is in progress, or a
  decision. People can follow a project's Updates and get notified.
- **Notes**: private or shared notes with checklists, for a person's own planning.

## Write an update

1. Find what is worth telling: `update_candidates()` lists recently finished tickets that no update
   covers yet. `list_updates()` shows what was already said; `tab` can be `latest`, `shipped`, `in_progress`,
   `decision`, `week` (the last seven days) or `drafts`.
2. Group related tickets into **one outcome**. Readers care about "customers can now pay by card",
   not five ticket titles.
3. `create_update` with:
   - **title**: the outcome in plain words.
   - **summary**: what changed or what is being worked on, without implementation jargon.
   - **benefit**: why it matters to customers or the business. Don't invent numbers.
   - **next_step**: what happens next, or what decision or feedback is needed.
   - **kind**: `shipped`, `in_progress` or `decision`.
   - **ticket_keys**: the source tickets. Their images are attached automatically; remove ones that
     don't help with `edit_update_media`.
   - **available**: `true` only when you have confirmed people can use it now. A done ticket or a
     merged pull request alone is not enough.
4. A draft notifies nobody. Show it to the person and adjust it with `edit_update`.
5. **Publish only when the person says so**: `publish_update(id, notify: true or false)`. Ask
   whether followers should be notified; don't decide that yourself.

To read feedback, `get_update(id)` and `update_comments`. Reply with `comment_on_update` only when
the person asks you to; it can notify people.

## Notes

- `create_note(title, body, tasks)` makes a note owned by the key's person. Use checklists
  (`tasks`) for lists of small steps that don't deserve tickets.
- `list_notes(tab: "pinned")` and `get_note` read notes; `edit_note` updates one (pass its latest
  version as `if_version`; `tasks` replaces the whole checklist, so keep existing items); `comment_on_note` leaves feedback.
- Notes may be private. Never copy a private note's content into a ticket, update or comment
  without the person's say-so.
- A note item that turns into real work should become a ticket (see the intake skill), with a link
  back.

## Mentions

`mention_targets(key: "WEB-12")` (or `update_id` / `note_id`) lists who can be mentioned there. Write
`@Full Name` exactly as returned. Mentions notify people, so mention someone only when the user
wants them told or asked something.

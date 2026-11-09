---
description: Take the most important ready Praxis ticket and start on it
argument-hint: "[board]"
---

Use the praxis-work skill. Call `praxis_meta` if you have not this session, then
`next_task` (pass `board: "$ARGUMENTS"` if a board was given). It claims the ticket for you.
Read it with `get_issue`, tell me its key, title and what done looks like, and propose a first step
before changing anything. If nothing is ready, say so and show what is blocked or held instead.

---
description: Record where you got to on the current Praxis ticket and hand it back
argument-hint: "[ticket key]"
---

Use the praxis-work skill. For ticket $ARGUMENTS (or the one claimed in this session), write a
handoff with `claim_issue(key, release: true, outcome: "...")`: what changed and where, what was
tried and rejected, what is left, and where the next person should start. If the work is actually
finished, set it done with `update_issue` instead. Show me the outcome text first.

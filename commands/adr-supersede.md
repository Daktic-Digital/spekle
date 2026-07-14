---
description: Replace a decision the right way — new ADR with a forward link from the old one
argument-hint: "<number>"
---

Supersede ADR $ARGUMENTS using the conventions from the adr skill (read
`skills/adr/SKILL.md` in this plugin).

Draft a new ADR that supersedes it: ask (or infer from conversation) what
changed in the context, write the new record stating what it supersedes and
why, flip the old ADR's status line to `Superseded by [NNNN](...)`, and update
the index. Never alter the old ADR beyond its status line.

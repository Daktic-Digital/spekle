---
description: Manage Architecture Decision Records — new, list, supersede, init
argument-hint: "[new <title> | list | supersede <number> | init]"
---

Manage this repository's Architecture Decision Records using the conventions
from the adr skill (read `skills/adr/SKILL.md` in this plugin for format,
location, numbering, and lifecycle rules).

Arguments: $ARGUMENTS

Dispatch on the first word of the arguments:

- **new <title>** — Draft a new ADR titled <title>. Pull context and
  rationale from the current conversation if the decision was just discussed;
  otherwise ask the user for context, decision, and alternatives considered.
  Show the draft for approval before writing the file and updating the index.
- **list** — Read the ADR index and present a compact table of number, title,
  status, and date. If index and files disagree, report the discrepancy and
  offer to rebuild the index from the files.
- **supersede <number>** — Draft a new ADR that supersedes ADR <number>: ask
  (or infer from conversation) what changed in the context, write the new
  record, flip the old ADR's status line to `Superseded by [NNNN](...)`, and
  update the index. Never alter the old ADR beyond its status line.
- **init** — Create the ADR directory and index, then write ADR 0001 titled
  "Record architecture decisions" documenting the decision to use ADRs, this
  format, and their location. Check for an existing ADR convention in the
  repo first and adopt it rather than creating a second location.
- **no arguments** — Show the index summary and ask what the user wants to do.

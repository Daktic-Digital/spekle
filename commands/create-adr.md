---
description: Draft a new Architecture Decision Record
argument-hint: "[title]"
---

Draft a new ADR using the conventions from the adr skill (read
`skills/adr/SKILL.md` in this plugin for format, location, numbering, and
lifecycle rules).

Title: $ARGUMENTS

If a title was given, use it; otherwise derive one from the decision at hand.
Pull context, rationale, and alternatives from the current conversation if the
decision was just discussed; otherwise ask the user for context, decision, and
alternatives considered. Show the draft for approval before writing the file
and updating the index. New ADRs start as `Proposed` unless the user has
already clearly committed, in which case `Accepted`.

---
description: Draft a local, untracked Technical Design Doc that references the ADRs it implements
argument-hint: "[title]"
---

Draft a new TDD using the conventions from the tdd skill (read
`skills/tdd/SKILL.md` in this plugin for location, exclusion from git, format,
and lifecycle rules).

Title: $ARGUMENTS

Steps:

1. Ensure `docs/tdd/` exists and is excluded from git via `.git/info/exclude`
   (add the `docs/tdd/` line if missing — never touch `.gitignore`).
2. Skim the ADR index. **GATE: a TDD must reference at least one ADR in its
   `Implements ADRs` table row — orphan TDDs are not allowed.** If the work being
   planned has no ADR yet, do not create the TDD; record the decision first
   (the `/create-adr` flow), then return here. The ADR is the durable
   artifact; the TDD only references it.
3. Determine the next ID by listing existing files in `docs/tdd/` and
   incrementing the highest number found (start at 01 if none exist).
4. Draft the TDD from the current conversation using the tdd skill's
   template, with status `In-flight` and the next available NN ID. Write
   the file directly to `docs/tdd/NN-short-slug.md`. Do not show it in
   chat for approval first — write it, then tell the user the path so they
   can open and review it.
5. Remind the user the file is local-only and will be deleted by
   `/adr-clean` once shipped and extracted.

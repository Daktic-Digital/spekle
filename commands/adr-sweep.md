---
description: Reconcile TDD and Proposed ADR status — auto-flip shipped TDDs, ask on Proposed ADRs
---

Reconcile the status of this repository's TDDs and `Proposed` ADRs
(conventions in `skills/adr/SKILL.md` and `skills/tdd/SKILL.md` in this
plugin; contract set by ADR 0008). The intended maintenance loop is
`/adr-verify` → `/adr-sweep` → `/adr-clean`.

Steps:

1. **Verify first.** Run the full integrity check from `/adr-verify`. Fix
   findings (with approval) before reconciling any status — never mutate
   TDDs or ADRs while the corpus is in a broken state.
2. **Reconcile `In-flight` TDDs** in `docs/tdd/`. For each one, parse the
   Plan's per-step `Touchpoints` tables (`File | Symbol/Section | Action`):
   - **All touchpoints present** (every file exists and every symbol/section
     is found in the current tree) — flip `**Status**` from `In-flight` to
     `Shipped` without asking. Report the Extraction Checklist state
     (complete / incomplete) in the summary; do not gate the flip on it.
   - **Partial or missing touchpoints** — do not flip. Report which
     touchpoints matched and which did not, and ask the user whether to
     flip, keep `In-flight`, or investigate.
   - **Missing or unparseable Touchpoints tables** — do not flip. Report
     and ask.
3. **Reconcile `Proposed` ADRs** in `docs/adr/`. Never propose a status
   heuristically. For each `Proposed` ADR, show:
   - Title, ID, age since `Created`.
   - Any TDDs whose `**Implements**` line references it, and their status.

   Then ask the user to choose one:
   - **Accept** — flip `**Status**` to `Accepted` in place.
   - **Reject** — flip `**Status**` to `Rejected` in place.
   - **Keep** — leave as `Proposed`.
   - **Supersede** — hand off to `/adr-supersede`; do not flip in place.

   Apply the chosen flip and update the index (`docs/adr/README.md`) status
   in the same change.
4. **Do not delete.** Sweep never removes TDDs or ADRs — deletion of
   `Shipped` TDDs stays in `/adr-clean`.

Finish with a compact summary: verify result, TDDs auto-flipped to
`Shipped`, TDDs left `In-flight` and why, `Proposed` ADRs reconciled with
their new statuses, and — if any `Shipped` TDDs are now present — name
`/adr-clean` as the follow-up.

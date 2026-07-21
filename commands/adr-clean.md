---
description: Wipe shipped TDDs after extraction, and verify ADR artifacts are consistent
---

Clean this repository's disposable design artifacts and confirm the durable
ones are consistent (conventions in `skills/adr/SKILL.md` and
`skills/tdd/SKILL.md` in this plugin).

Steps:

1. **Verify first.** Run the full integrity check from `/adr-verify`. Fix
   findings (with approval) before touching any TDD — never delete a TDD
   whose referenced ADRs are in a broken state.
2. **Triage TDDs** in `docs/tdd/` by their `Status` line:
   - **Shipped** — confirm the extraction checklist is complete (new
     decisions recorded as ADRs, durable constraints landed as inline
     comments). If complete, delete the file. If not, report what's missing
     and offer to extract before deleting — extraction is the point, deletion
     is the side effect.
   - **In-flight** — keep, untouched. Cross-check against git history: if the
     work it describes clearly shipped long ago, flag it as likely stale and
     ask rather than assuming.
   - **Missing or unrecognized status** — never delete; report and ask.
3. **Housekeeping.** Ensure `docs/tdd/` is still excluded via
   `.git/info/exclude`, and that no TDD has accidentally been committed
   (check `git ls-files docs/tdd/`) — if one has, flag it for the user to
   remove from tracking.

Finish with a one-paragraph summary: TDDs deleted, TDDs kept and why, and the
verify result.

# Architecture Decision Record: Add /adr-sweep to reconcile TDD and Proposed ADR status between verify and clean

| Field | Value |
|---|---|
| **ID** | 0008 |
| **Created** | 2026-08-21 |
| **Status** | Accepted |
| **Related ADRs** | [0002](0002-tdds-are-local-and-untracked.md), [0005](0005-no-orphan-tdds.md), [0007](0007-restructure-tdds-for-scannable-single-concern-plans.md) |

## Context

### Problem Statement

The current ADR/TDD lifecycle has a status-reconciliation gap. `/adr-verify`
is read-only and only checks corpus integrity; `/adr-clean` deletes
`Shipped` TDDs but refuses to touch anything else. Nothing flips a TDD from
`In-flight` to `Shipped` when its work has actually landed, and nothing
prompts the user to move a `Proposed` ADR to `Accepted`, `Rejected`, or a
superseding decision once reality has answered the question. The result:
`In-flight` TDDs accumulate silently long after their touchpoints have
shipped (defeating the disposable-TDD model), and `Proposed` ADRs sit
indefinitely with no forcing function to reconcile them. Users notice the
drift only when they go looking.

### Decision Drivers

- The verify → clean sequence should be a coherent maintenance loop, not two
  disconnected commands that leave the middle step to the user.
- TDD status is machine-checkable ([0007](0007-restructure-tdds-for-scannable-single-concern-plans.md)):
  touchpoint tables name files and symbols, so shippedness is verifiable by
  reading the repo — asking the user for every TDD is unnecessary ceremony.
- ADR acceptance is a human judgment (does this reflect what we actually
  believe now?), not a code-presence signal. A `Proposed` ADR whose
  implementing TDD shipped may still be wrong in retrospect, and code that
  matches a `Proposed` ADR is not evidence the team endorses the decision.
- The command surface is already verb-style ([0003](0003-verb-style-commands.md));
  a new verb is cheaper than overloading `/adr-verify` or `/adr-clean`.

## Considered Options

- **Fold reconciliation into `/adr-clean`**: considered because clean already
  triages TDDs and could flip statuses in the same pass; rejected because
  clean's contract is "delete safely" — mixing in status mutation and
  interactive ADR reconciliation muddies the blast radius and makes the
  command harder to reason about.
- **Fold reconciliation into `/adr-verify`**: considered because verify
  already inspects every TDD and ADR; rejected because verify is
  intentionally read-only, and losing that property costs more than it saves.
- **Leave reconciliation manual**: considered because the current commands
  work and users can edit status fields directly; rejected because silent
  drift is exactly the failure mode `/adr-clean` was built to prevent, and
  the same argument applies one lifecycle stage earlier.
- **Add `/adr-sweep` as a distinct verb between verify and clean**: chosen
  — makes the maintenance loop explicit (verify → sweep → clean), keeps
  each command's contract narrow, and gives status reconciliation a single
  named owner.

## Decision

We will add `/adr-sweep`, a new command that sits between `/adr-verify` and
`/adr-clean` in the maintenance loop. Its contract:

1. **Run `/adr-verify` first.** If verify surfaces findings, resolve them
   (with approval) before sweeping — the same guardrail `/adr-clean` uses.
2. **Reconcile `In-flight` TDDs.** For each `In-flight` TDD, parse the Plan's
   `Touchpoints` tables. If every listed file exists and every listed
   symbol/section is present in the current tree, auto-flip `Status` to
   `Shipped` without asking, and report the Extraction Checklist's state in
   the summary (complete / incomplete) — checklist completion is the user's
   responsibility ([0007](0007-restructure-tdds-for-scannable-single-concern-plans.md)),
   not a gate on the flip. If touchpoints are partially present or missing,
   report the mismatch and ask the user whether to flip, keep, or investigate.
3. **Reconcile `Proposed` ADRs interactively.** Sweep never heuristically
   proposes a status for a `Proposed` ADR. For each one, present its title,
   age since creation, and any implementing TDDs (and their status), then
   ask: **Accept**, **Reject**, **Keep as Proposed**, or **Supersede**
   (hands off to `/adr-supersede`). Apply the chosen flip in place.
4. **Deletion is out of scope.** Sweep never deletes TDDs; that stays in
   `/adr-clean`. The intended flow is verify → sweep → clean.

Sweep finishes with a compact summary: verify result, TDDs auto-flipped,
TDDs left `In-flight` and why, Proposed ADRs reconciled and their new
statuses. When any `Shipped` TDD is left behind, name `/adr-clean` as the
follow-up.

### Outcome

Chosen option: **Add `/adr-sweep` as a distinct verb**, because it closes
the status-reconciliation gap without expanding the contract of either
existing command, and it makes the verify → sweep → clean loop a first-class
workflow.

## Consequences

**Good:**

- The maintenance loop is now a named three-step sequence users can run
  end-to-end, rather than two commands with an implicit gap.
- `In-flight` TDDs no longer accumulate silently — the touchpoint-based
  auto-flip catches the common "work shipped, nobody updated the status"
  case without pestering the user.
- `Proposed` ADRs get a forcing function for reconciliation; the interactive
  prompt makes the choice visible instead of leaving it to whoever notices.
- `/adr-verify` and `/adr-clean` keep their narrow contracts (read-only
  integrity check; safe deletion), which makes each easier to reason about.

**Neutral:**

- Users now have three ADR-lifecycle commands to know about instead of two;
  the sweep verb is discoverable in the same `/adr-*` namespace and its
  place in the loop is documented, but there is one more thing to learn.
- Touchpoint parsing is best-effort — it depends on TDD authors filling in
  the tables per [0007](0007-restructure-tdds-for-scannable-single-concern-plans.md).
  A TDD with sparse touchpoints will fall through to the "ask the user" path
  rather than misfire.

**Bad:**

- Auto-flipping to `Shipped` on touchpoint presence alone can be wrong when
  touchpoints exist but the behavior is broken or partially implemented —
  the flip signals "code landed," not "feature works." The Extraction
  Checklist state is reported so the user notices, but sweep will not block
  on it.
- Adding a command means adding maintenance surface: the sweep logic must
  stay in sync with the TDD template ([0007](0007-restructure-tdds-for-scannable-single-concern-plans.md))
  and the ADR status vocabulary. Template drift will silently degrade sweep
  accuracy.
- The interactive `Proposed`-ADR flow makes sweep non-batchable in
  automation contexts; a large backlog of `Proposed` ADRs turns sweep into
  a long interactive session.

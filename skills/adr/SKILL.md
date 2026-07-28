---
name: adr
description: Record and consult Architecture Decision Records. Use when a session produces an architectural decision (choosing between technologies, changing a system boundary or interface, adopting or dropping a convention, rejecting an approach for a reason worth remembering), when the user asks to record or draft a decision, mentions ADR, or asks why a past decision was made.
---

# Architecture Decision Records

ADRs are the durable artifact of development in this workflow. Specs and plans
are disposable; the decisions extracted from them are what's worth keeping.
Your job is to notice decisions, draft them in the standard format, keep the
index current, and consult past ADRs before proposing changes that touch them.

The disposable half of the workflow — local, untracked Technical Design Docs
that drive implementation and reference the ADRs they implement — is covered
by the companion `tdd` skill. If content is a decision with alternatives and
tradeoffs, it belongs here; if it's a build plan, it belongs in a TDD; if
it's a constraint a future reader of the code needs, it belongs in an inline
comment.

## Where ADRs live

Default location: `docs/adr/NNNN-short-slug.md` with the index at
`docs/adr/README.md`. Before creating the first ADR in a repo, check for an
existing convention (`docs/adr/`, `doc/architecture/decisions/`, `adr/`,
`docs/decisions/`) and follow it if found. Numbering is sequential,
zero-padded to 4 digits; find the next number by listing existing files, not
by trusting the index.

## When to propose an ADR

Triggers — any of these during a session means offer to draft one:

- A choice was made between competing technologies, libraries, or services
- A system boundary, interface contract, or data model changed shape
- A convention was adopted or abandoned (error handling, testing strategy,
  directory layout, naming)
- An approach was seriously considered and **rejected** for a reason that will
  matter later — rejected paths are among the most valuable ADRs
- The user says anything like "let's go with X" after weighing alternatives

Not triggers: routine implementation choices already dictated by existing
ADRs or by the framework in use, bug fixes, refactors that preserve
decisions. When in doubt, ask: "will someone later wonder why this is the way
it is?" If no, skip it — zero ceremony is the point.

## How to write one

Use [template.md](template.md). Formatting follows
[spec-kit](https://github.com/github/spec-kit) conventions (adopted, not
forked): a doc-type-prefixed title (`# Architecture Decision Record: <title>`)
followed by a two-column `Field | Value` metadata table (ID, Created, Status,
Related ADRs). **Related ADRs** holds link(s) only —
`[NNNN](NNNN-slug.md)`, comma-separated for more than one, or `None` — how
it relates (builds on, constrained by, supersedes, overlaps with) belongs in
prose in Context or Decision, not the header. Use
`[NEEDS CLARIFICATION: specific question]` markers instead of silently
guessing at unresolved points. All four top-level sections are required —
there's no optional section, so none are marked `*(mandatory)*`.

Section shape: Context opens with a **Problem Statement** (the forcing
situation, facts not judgments) and **Decision Drivers** (the constraints
that narrow the field). **Considered Options** lists each option with both
why it was worth evaluating and why it was rejected. **Decision** states the
outcome in plain prose and closes with an **Outcome** subsection naming the
chosen option and the one-line reason it won. **Consequences** is grouped
into **Good**, **Neutral**, and **Bad** — not a single undifferentiated
paragraph.

Hard rules:

- **One page maximum.** ADRs die when they get long. Cut background the
  reader can get from the code.
- **Consequences include the bad ones.** An ADR with nothing under Bad is
  advocacy, not a record.
- **Considered Options get two reasons each** — why it was considered and
  why it was rejected, one line apiece. If an option deserves more, that
  argues for its own rejected-status ADR.
- Plain declarative prose. Write "We will use X" not "It was decided that X
  might be used."

## Lifecycle and immutability

Statuses: `Proposed` → `Accepted` → `Superseded by [NNNN](NNNN-slug.md)` (or
`Rejected`).

Never edit the substance of an accepted ADR. If a decision changes, write a
new ADR that states what it supersedes and why the context changed, then
update only the old ADR's `Status` field to link forward. Typo fixes are
fine; rewriting history is not — the record of what was believed at the time
is the value.

## Workflow

1. Draft the ADR and show it to the user before writing the file — the user
   accepts decisions, you record them. New ADRs start as `Proposed` unless
   the user has already clearly committed, in which case `Accepted`.
2. Write the file, then update the index in the same change: one line per
   ADR — `- [NNNN](NNNN-slug.md) — Title (Status)`.
3. When starting significant design work, skim the index first and cite any
   ADR the proposed work would touch or contradict. If the work contradicts
   an accepted ADR, say so explicitly and offer the supersede path — don't
   silently drift.

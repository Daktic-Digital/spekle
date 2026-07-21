# Architecture Decision Record: TDDs are local, untracked, and disposable

**ID**: 0002 | **Created**: 2026-07-14 | **Status**: Accepted

## Context *(mandatory)*

ADRs live for the life of a system; TDDs are useful while driving an
implementation and become misleading documentation once the code exists. A
committed TDD either rots or demands maintenance it doesn't repay. But
discarding TDDs entirely loses their write-time value as a plan the agent
implements against.

## Decision *(mandatory)*

We will keep TDDs in `docs/tdd/`, excluded from git via `.git/info/exclude`
(never `.gitignore`, so the repo carries no trace of them). Durable knowledge
exits a TDD through two channels — decisions become ADRs, constraints become
inline comments at the point of use — and `/adr-clean` deletes TDDs only
after they are marked `Shipped` and their extraction checklist is complete.
In-flight TDDs are never deleted; status is carried in the TDD itself so
cleanup is machine-checkable.

## Alternatives Considered *(mandatory)*

- **Commit TDDs alongside ADRs**: they decay into misleading docs the moment
  the feature ships; maintenance cost with no compounding value.
- **No TDDs at all**: loses the write-time plan; design detail ends up
  nowhere or bloats ADRs with implementation sequencing.
- **Exclude via `.gitignore`**: touches a committed file, leaving a trace of
  a local-only convention in every consumer's repo.

## Consequences *(mandatory)*

TDDs don't sync across machines and are invisible to teammates and
reviewers — in-flight design context lives only on the author's machine. This
is accepted: the workflow is agent-driven and the durable context is required
to land in ADRs and comments before cleanup. Anything a teammate would need
from a TDD is, by construction, somewhere committed.

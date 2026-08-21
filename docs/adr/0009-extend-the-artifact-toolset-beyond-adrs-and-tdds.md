# Architecture Decision Record: Extend the artifact toolset beyond ADRs and TDDs

| Field | Value |
|---|---|
| **ID** | 0009 |
| **Created** | 2026-08-21 |
| **Status** | Proposed |
| **Related ADRs** | [0002](0002-tdds-are-local-and-untracked.md), [0003](0003-verb-style-commands.md) |

## Context

### Problem Statement

The current toolset covers two artifact kinds: durable decisions (ADRs) and
disposable implementation plans (TDDs). Real design work produces other
artifacts that don't fit either — architecture and sequence diagrams that
communicate structure, spikes that capture time-boxed exploration before a
decision is ready, and likely more categories we haven't named yet. Today
these live ad-hoc in scratch files, chat, or nowhere, which means the
context around a decision is often thinner than it should be and repeated
exploration is invisible to future work.

### Decision Drivers

- The ADR/TDD split works because each artifact has a narrow, machine-checkable
  contract. Any new artifact type must earn the same clarity — kind, lifecycle,
  location, and a verb that operates on it.
- We do not yet know which artifact types are worth the ceremony. This ADR
  should open the direction, not lock in a catalog.
- Follow-ons should match the existing conventions ([0003](0003-verb-style-commands.md)):
  one verb per operation, per-artifact skills, per-artifact templates.

## Considered Options

- **Do nothing; keep artifacts ad-hoc**: considered because the current tools
  already cover the highest-value cases; rejected because the gap around
  diagrams and pre-decision exploration is already visible in practice, and
  ad-hoc artifacts don't compose with `/adr-verify` or `/adr-sweep`.
- **Design the full expanded toolset in one ADR now**: considered because a
  single scoping decision would be easier to reference; rejected because we
  don't yet have enough evidence about which artifact types deserve
  first-class treatment, and locking a catalog in prematurely would create
  the same ceremony this toolset exists to avoid.
- **Open the direction here, defer each artifact type to its own ADR**:
  chosen — commits to the extension without over-specifying, and forces
  each new artifact type to justify itself on its own terms.

## Decision

We will extend the artifact toolset beyond ADRs and TDDs, adding new
artifact types incrementally. Each new artifact type gets its own ADR that
defines:

- Its purpose and the gap it fills relative to ADRs, TDDs, and inline comments.
- Whether it is **durable** (committed, versioned, superseded) or
  **disposable** (local, untracked, deleted after use) — the ADR/TDD split
  is the reference.
- Its location, naming, and status vocabulary.
- The verb-style commands that create, list, verify, and (if disposable)
  clean it, following [0003](0003-verb-style-commands.md).

Initial candidate artifact types worth exploring in follow-on ADRs — this
list is intentionally open, not a commitment:

- **Diagrams** — visual artifacts (architecture, sequence, data flow, ER)
  that communicate structure a prose ADR cannot. Likely durable, likely
  linked from the ADRs they illustrate.
- **Spikes** — time-boxed exploratory work whose output is a written
  finding (what we learned, what we ruled out) rather than shipped code.
  Likely disposable in the same spirit as TDDs, but the *finding* often
  feeds a new ADR.
- **Others as they surface** — runbooks, postmortems, experiments, and
  similar categories may earn their own ADRs when the need is concrete.

Specific templates, commands, skills, and lifecycle rules for each artifact
type are **out of scope for this ADR** — they belong in the per-artifact
follow-on ADRs. This decision commits only to the direction and the
per-artifact-ADR pattern.

### Outcome

Chosen option: **Open the direction, defer each artifact to its own ADR**,
because it commits to extending the toolset without locking in a catalog
before we have evidence for it.

## Consequences

**Good:**

- Creates a clear place to record future artifact-type decisions rather
  than each one arriving as a surprise.
- Forces every new artifact type to pass the same bar the ADR/TDD split
  already passes: named purpose, defined lifecycle, verb-style command.
- Preserves the option to *not* add an artifact type if a proposed one
  turns out not to earn its ceremony.

**Neutral:**

- This ADR ships with no immediate change to the toolset — the value is
  the direction, and value only accrues when follow-on ADRs land.
- The "durable vs disposable" framing is a heuristic; some artifacts
  (e.g. spike findings) may sit awkwardly between the two and need per-artifact
  judgment.

**Bad:**

- Direction-setting ADRs without follow-through become clutter. If no
  follow-on ADR lands in a reasonable window, revisit this one and decide
  whether to accept, reject, or supersede it rather than leaving it
  `Proposed` indefinitely — `/adr-sweep` (ADR 0008) is the forcing function.
- A growing artifact catalog risks reintroducing the ceremony the current
  minimal toolset avoids. Each follow-on ADR must justify its artifact on
  the merits, not on symmetry with the others.

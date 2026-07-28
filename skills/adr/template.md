# Architecture Decision Record: [Title stating the decision as a fact, e.g. "Use Postgres for persistence"]

**ID**: NNNN | **Created**: YYYY-MM-DD | **Status**: Proposed
**Related ADRs**: [None, or [NNNN](NNNN-slug.md) — say how: builds on,
constrained by, supersedes, overlaps with]

<!--
  Status is exactly one of: Proposed | Accepted | Rejected |
  Superseded by [NNNN](NNNN-slug.md).
  Never edit an accepted ADR's substance — supersede it. Only the Status
  field may change after acceptance.
-->

## Context

### Problem Statement

[The situation that forces a decision — what's happening, what's missing,
what's breaking. Facts, not judgments. 1–3 sentences.]

### Decision Drivers

- [Constraint or goal that shapes which options are viable, e.g. "must not
  require a schema migration"]
- [...]

## Considered Options

- **[Option A]**: considered because [what made it worth evaluating];
  rejected because [the deciding reason against it].
- **[Option B]**: considered because [...]; rejected because [...].

## Decision

[We will ... — the decision in plain declarative prose, with the deciding
rationale. State it so a reader could act on it without reading anything
else. Mark any unresolved point with [NEEDS CLARIFICATION: specific
question] rather than papering over it.]

### Outcome

Chosen option: **[Option name]**, because [one-line reason tying back to the
decision drivers].

## Consequences

**Good:**

- [What becomes easier or is now possible.]

**Neutral:**

- [What changes shape without being clearly better or worse — a tradeoff
  accepted, not won.]

**Bad:**

- [What becomes harder, or what is now owed — migrations, conventions to
  follow, revisit conditions. An ADR with no bad outcomes listed is
  advocacy, not a record.]

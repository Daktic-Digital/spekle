# Architecture Decision Record: Restructure the ADR template to MADR-style sections

**ID**: 0006 | **Created**: 2026-07-28 | **Status**: Accepted
**Related ADRs**: [0004](0004-adopt-spec-kit-formatting-conventions.md) —
builds on it for title/metadata/NEEDS CLARIFICATION conventions, narrows it
by dropping the `*(mandatory)*` markers it introduced

## Context

### Problem Statement

The original template's Context/Decision/Alternatives Considered/
Consequences sections gave no structure for why an alternative was worth
considering (only why it lost), no place for decision drivers or ADR
cross-links, and let Consequences stay a single paragraph — easy to
under-report the bad outcomes the skill's own hard rule requires.

### Decision Drivers

- Readers need to find "what won and why" without re-deriving it from prose.
- A rejected option is only useful if the reason it was on the table is
  recorded, not just the reason it lost.
- Consequences need a shape that resists writing only upsides.
- Relationships between ADRs should be discoverable from the header, not
  buried in prose.

## Considered Options

- **Keep the existing flat template**: considered because it was already in
  place and matched ADR 0004's stated conventions; rejected because it gave
  no structure for decision drivers, no forcing function for negative
  consequences, and no place to record relationships between ADRs.
- **Adopt MADR's full template verbatim**: considered because MADR is a
  well-established, widely recognized ADR format; rejected because its full
  form includes fields (Confirmation, a Pros-and-Cons table per option) that
  add ceremony the skill's "one page maximum" rule is designed to avoid.
- **Restructure sections while keeping the one-page, prose-first house
  style**: considered because it takes the structural pieces of MADR worth
  keeping — Problem Statement, Decision Drivers, Considered Options, Outcome,
  grouped Consequences — without adopting fields incompatible with a
  one-page limit; chosen as the deciding option.

## Decision

We will restructure the ADR template so Context opens with a Problem
Statement and Decision Drivers subsection, Considered Options replaces
Alternatives Considered and requires both why an option was considered and
why it was rejected, Decision closes with an Outcome subsection naming the
chosen option, Consequences is grouped into Good/Neutral/Bad, and the header
gains a Related ADRs line. Because every top-level section is now required
by definition, we drop the `*(mandatory)*` markers ADR 0004 introduced —
they were only useful when some sections were optional.

### Outcome

Chosen option: **Restructure sections while keeping the one-page,
prose-first house style**, because it fixes the structural gaps without
importing ceremony the skill explicitly rejects.

## Consequences

**Good:**

- Rejected options now carry both their upside and their deciding flaw, so
  future readers can tell a real alternative from a strawman.
- Grouping consequences into Good/Neutral/Bad makes an empty Bad section
  visibly wrong instead of silently missing.
- The Related ADRs header line makes cross-references discoverable without
  reading the body.

**Neutral:**

- The template has more section headers even though total content length is
  similar; the one-page limit holds but headroom is tighter.

**Bad:**

- ADR 0004's decision text still describes `*(mandatory)*` markers as
  adopted; that line is now stale prose in an immutable accepted ADR, and
  only this ADR's Related ADRs link makes the narrowing discoverable.
- The five existing ADRs (0001–0005) remain in the old flat format and won't
  be migrated — readers or tooling expecting the new shape uniformly across
  the index will find inconsistency until each is superseded on its own
  timeline.

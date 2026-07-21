# Technical Design Doc: [Title naming the work being built, e.g. "Wire rate limiting into the API gateway"]

**Created**: YYYY-MM-DD | **Status**: In-flight

**Implements**: [NNNN](../adr/NNNN-slug.md), [NNNN](../adr/NNNN-slug.md)

<!--
  GATE: Implements must list at least one ADR — orphan TDDs are not allowed.
  If the work has no ADR yet, record the decision first, then create this
  file.
  Status is exactly one of: In-flight | Shipped. /adr-clean deletes only
  Shipped TDDs whose Extraction Checklist is complete; In-flight TDDs are
  never deleted. This file is local-only (excluded via .git/info/exclude)
  and must never be committed.
-->

## Plan *(mandatory)*

[The implementation approach as ordered, checkable steps. Files and
interfaces to touch, sequencing, and how to know each step worked.]

## Edge Cases & Risks

[What could go wrong, what inputs are weird, what existing behavior must not
change.]

## Open Questions

[Unresolved items, each marked [NEEDS CLARIFICATION: specific question].
Anything that turns into a decision with alternatives becomes an ADR, not a
paragraph here.]

## Extraction Checklist *(mandatory)*

*GATE: Must be fully checked before Status flips to Shipped — `/adr-clean`
will not delete this file otherwise.*

- [ ] Decisions made during implementation are recorded as ADRs and listed
      under **Implements**
- [ ] Constraints a future reader needs are inline comments at the point of
      use
- [ ] Nothing else in this file is worth keeping

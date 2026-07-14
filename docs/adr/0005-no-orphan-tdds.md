# Architecture Decision Record: Every TDD must implement at least one ADR

**ID**: 0005 | **Created**: 2026-07-14 | **Status**: Accepted

## Context *(mandatory)*

TDDs are disposable and local ([0002](0002-tdds-are-local-and-untracked.md)),
which makes them easy to create casually. A TDD with no ADR reference is
untethered from any recorded decision — its durable content has no extraction
destination, and nothing connects the implementation it drives back to the
feature or decision that motivated it.

## Decision *(mandatory)*

We will require every TDD's `**Implements**:` line to reference at least one
ADR, enforced as a gate at creation time: `/create-tdd` refuses to write an
orphan TDD and routes to `/create-adr` first, and `/adr-verify` reports any
orphan it finds as a finding. If a plan can't be tied to a recorded decision,
either the decision is missing (record it) or the work doesn't need a TDD.

## Alternatives Considered *(mandatory)*

- **Warn but allow orphans**: soft warnings decay into noise; the corpus
  fills with untethered plans and the ADR-first discipline erodes.
- **Auto-generate a stub ADR at TDD creation**: produces hollow ADRs written
  to satisfy the gate rather than to record a real decision.

## Consequences *(mandatory)*

Creating a TDD sometimes costs an ADR first — deliberate friction that keeps
the decision record ahead of the implementation. Small exploratory work that
genuinely has no decision behind it simply doesn't get a TDD, which is the
intended filter.

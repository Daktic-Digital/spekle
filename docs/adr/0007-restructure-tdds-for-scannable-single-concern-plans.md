# Architecture Decision Record: Restructure TDDs to favor scannable, single-concern implementation blocks over prose

| Field | Value |
|---|---|
| **ID** | 0007 |
| **Created** | 2026-08-08 |
| **Status** | Accepted |
| **Related ADRs** | [0002](0002-tdds-are-local-and-untracked.md), [0004](0004-adopt-spec-kit-formatting-conventions.md), [0005](0005-no-orphan-tdds.md) |

## Context

### Problem Statement

TDDs generated from the current template come out as dense prose blocks. The
Plan section renders as a paragraph or a flat list, with no visual anchors for
file paths, signatures, or per-step touchpoints. A single TDD is expected to
cover a whole feature even when the work touches several independent files, so
files grow long and hard to review step-by-step. The result is a document that
reads like justification rather than a scannable build plan.

### Decision Drivers

- TDDs are read *while implementing* — scanning to the next step must not
  require re-reading a paragraph.
- Structure should surface *what* is being changed (file paths, signatures,
  table rows, code fences); *why* already lives in the linked ADR.
- One TDD should cover one area of concern. Multi-file work with divergent
  concerns should split into multiple TDDs rather than pile into one.
- Templates shape behavior — pushing toward tables and fenced blocks is how we
  actually get tables and fenced blocks.

## Considered Options

- **Keep the current template**: considered because it already exists and
  matches ADR 0004's conventions; rejected because its free-form Plan section
  invites prose walls and provides no forcing function for per-step structure.
- **Mandate one file per TDD**: considered because it caps length and
  guarantees focus; rejected as too rigid — a single logical concern sometimes
  legitimately spans multiple files, and forcing a split by file count creates
  ceremony without value.
- **Restructure the template to require per-step touchpoint tables, fenced
  code blocks for signatures/schemas, and an explicit Scope field, plus skill
  guidance to split when concerns diverge**: chosen — fixes the density
  problem and encourages splits without banning multi-file TDDs.

## Decision

We will restructure the TDD template so that:

1. The metadata table gains a `**Scope**` row that names the single area of
   concern the TDD covers (e.g. "Rate-limit middleware only, not client
   retries").
2. The Plan section is broken into per-step subsections (`### Step N — <verb
   phrase>`), each of which contains:
   - A **Touchpoints** table with columns `File | Symbol/Section | Action`.
   - A fenced code block for any new/changed signature, schema, or
     configuration snippet.
   - A one-line **Verify** note describing how to confirm the step worked.
3. Prose rationale is compressed to a single sentence per step at most; the
   default is to link the implementing ADR instead of restating why.
4. The `tdd` skill gains explicit guidance: when a Plan reaches more than
   ~5 steps *or* the steps target unrelated subsystems, split into multiple
   TDDs. Each TDD lists the others under `Related TDDs`.

### Outcome

Chosen option: **Restructure the template plus split-guidance in the skill**,
because it fixes the density problem at the template level (where it's
enforced) and gives the split judgment a concrete trigger, without importing
the ceremony of a hard one-file rule.

## Consequences

**Good:**

- Implementation steps become scannable — file paths, signatures, and verify
  notes are visual anchors instead of embedded in prose.
- Splitting long TDDs into focused ones reduces per-file review load and makes
  the `Shipped` extraction checklist tractable per concern.
- The Scope field makes it visible up-front when a TDD is being asked to cover
  more than one concern, which is the point where a split should happen.

**Neutral:**

- Total content length across a feature's TDDs may be similar or slightly
  higher; the win is per-file readability, not total volume.
- Deciding what counts as "one area of concern" shifts judgment to the author;
  the ~5-step / unrelated-subsystem trigger is a heuristic, not a rule.

**Bad:**

- More per-step scaffolding (tables, code fences, verify lines) means TDDs
  take marginally longer to draft — the payoff is at read time, not write
  time.
- Multi-TDD splits multiply the number of extraction checklists that must be
  complete before `/adr-clean` can delete the set, so cleanup discipline has
  to scale with the split count.

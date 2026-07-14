---
name: tdd
description: Local, untracked Technical Design Docs that drive implementation and then get discarded. Use when starting non-trivial implementation work that deserves a written plan, when the user asks for a TDD, design doc, or implementation plan, or when deciding where design detail should live (ADR vs TDD vs inline comment).
---

# Technical Design Docs

TDDs are write-time artifacts: they drive an implementation while it's being
built, then get deleted. They are deliberately **never committed**. The
durable knowledge a TDD produces exits through two channels before it dies —
decisions become ADRs, and constraints a future reader needs become inline
comments at the point of use. The TDD itself is scaffolding.

## Where TDDs live

`docs/tdd/<short-slug>.md`, excluded from git via `.git/info/exclude` (add a
`docs/tdd/` line if missing). Never add the exclusion to `.gitignore` — the
whole point is that TDDs leave no trace in the repository, including in its
ignore rules. Before writing the first TDD, verify the exclusion is in place.

## Division of labor

- **ADR** — a decision and its rationale. Long-lived, committed, superseded
  rather than edited.
- **TDD** — the plan for building against those decisions: sequencing, file
  touchpoints, edge cases, open questions. Local, disposable.
- **Inline comment** — a constraint the code itself can't show, placed where
  it applies. This is where TDD detail that must outlive the TDD goes — not
  into committed documents.

If while drafting a TDD you find yourself writing a decision with
alternatives and tradeoffs, stop: that's an ADR. Record it there and have the
TDD reference it.

## Format

Use [template.md](template.md). Formatting follows
[spec-kit](https://github.com/github/spec-kit) conventions (adopted, not
forked): a doc-type-prefixed title (`# Technical Design Doc: <title>`), bold
pipe-separated metadata directly under it, `*(mandatory)*` section markers,
`[NEEDS CLARIFICATION: ...]` for unresolved points, and explicit `*GATE:*`
checkpoints. Hard rules:

- **No orphan TDDs — this is a gate, not a suggestion.** The `**Implements**:`
  line must reference at least one ADR before the file is created. Every TDD
  exists to implement recorded decisions; if the work has no ADR, record the
  decision first (that's what `/create-adr` is for), then create the TDD. A
  TDD you can't tie to a decision is a signal the work doesn't need a TDD.
- **Status is machine-checkable.** Exactly one of `In-flight` or `Shipped` in
  the `**Status**:` field — `/adr-clean` uses it to decide what's safe to
  delete and will never touch a TDD it can't classify.
- Keep it operational: steps, touchpoints, risks. Rationale lives in ADRs.

## Lifecycle

1. Created `In-flight` via `/create-tdd`, referencing the ADRs it implements.
2. During implementation, it's the working plan — update it freely; it has no
   history worth preserving.
3. New decisions surfaced by the work get recorded as ADRs immediately and
   added to the TDD's references.
4. When the work ships: complete the extraction checklist, flip status to
   `Shipped`.
5. `/adr-clean` deletes `Shipped` TDDs whose extraction checklist is
   complete. In-flight TDDs are never deleted.

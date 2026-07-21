# Architecture Decision Record: Adopt spec-kit formatting conventions without forking spec-kit

**ID**: 0004 | **Created**: 2026-07-14 | **Status**: Accepted

## Context *(mandatory)*

This plugin's design was developed off
[github/spec-kit](https://github.com/github/spec-kit), and its documents
benefit from a recognizable house style. But spec-kit's design is genuinely
different — per-feature spec directories, constitution gates, phased task
generation — and forking it would carry all that weight for a workflow whose
premise is that per-feature specs are disposable.

## Decision *(mandatory)*

We will follow spec-kit's general formatting conventions in our templates
without depending on or forking spec-kit: doc-type-prefixed titles
(`# Architecture Decision Record: <title>`), bold pipe-separated metadata
lines directly under the title, `*(mandatory)*` section markers,
`[NEEDS CLARIFICATION: specific question]` markers instead of silent
guesses, and explicit `*GATE:*` checkpoints where a step must not proceed.

## Alternatives Considered *(mandatory)*

- **Fork spec-kit**: inherits per-feature spec ceremony and machinery this
  design deliberately rejects; the overlap is stylistic, not structural.
- **Plain Nygard formatting**: fine, but loses convention alignment with the
  tooling ecosystem the design came from, and lacks the machine-checkable
  metadata line and gate markers.

## Consequences *(mandatory)*

Documents are visually and structurally familiar to spec-kit users, and the
metadata line gives `/adr-verify` and `/adr-clean` a single place to parse ID,
date, and status. We track spec-kit conventions by choice, not dependency —
if upstream style shifts, adopting changes is a manual decision, not a merge.

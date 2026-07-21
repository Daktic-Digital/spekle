# Architecture Decision Record: Record architecture decisions

**ID**: 0001 | **Created**: 2026-07-14 | **Status**: Accepted

## Context *(mandatory)*

This repo is a Claude Code plugin whose entire premise is that decisions are
the durable artifact of development. Its own design decisions (artifact
lifecycle, command surface, storage conventions) need the same treatment, or
the plugin fails its own test.

## Decision *(mandatory)*

We will record architecture decisions for this plugin as one-page ADRs in
`docs/adr/`, following the exact conventions the plugin itself enforces:
sequential 4-digit numbering, an index in `docs/adr/README.md`, and
supersede-don't-edit.

## Alternatives Considered *(mandatory)*

- **Rely on git history and PR descriptions**: rationale gets buried in
  merge commits; not consultable as a corpus.

## Consequences *(mandatory)*

The plugin dogfoods itself, so drift between what it prescribes and what it
practices becomes visible. Every substantive design change now owes a record.

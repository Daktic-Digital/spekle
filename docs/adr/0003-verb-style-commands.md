# Architecture Decision Record: Use verb-style commands instead of a dispatcher

**ID**: 0003 | **Created**: 2026-07-14 | **Status**: Accepted

## Context *(mandatory)*

The initial scaffolding exposed one `/adr` command dispatching on a
subcommand argument (`new`, `list`, `supersede`, `init`). Adding the TDD
workflow grows the surface to seven operations, and dispatch-by-argument
gives weaker discoverability in the command palette and vaguer per-command
descriptions.

## Decision *(mandatory)*

We will expose one command file per operation, named verb-style:
`/create-adr`, `/create-tdd`, `/adr-init`, `/adr-list`, `/adr-supersede`,
`/adr-verify`, `/adr-clean`. Each command carries its own description and
argument hint and defers conventions to the skills.

## Alternatives Considered *(mandatory)*

- **Keep the `/adr` dispatcher**: one tidy namespace, but each subcommand is
  invisible to command discovery and shares a single generic description.

## Consequences *(mandatory)*

Seven entries in the user's command list instead of one; names must stay
consistent as operations are added. Each command is individually
discoverable with a precise description.

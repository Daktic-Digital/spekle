# Spekle

Lightweight spec-driven development scaffolding that brings Architecture
Decision Records to the forefront and uses TDDs as guiding, ephemeral
implementation artifacts. **Code is law**: decisions are preserved as durable
records while guiding technical artifacts do their job at write time, then get
disposed of before they can rot as the code changes.

Spekle makes ADRs the durable artifact of development: decisions get recorded
as they happen, everything else (specs, plans, briefs) stays disposable — and
gets a disposal path.

The premise: per-feature design docs decay the moment the feature ships, and
forcing every change through spec ceremony raises the "what size problem is
this for?" question. Decisions don't decay — they're historical records,
superseded rather than edited — and a corpus of ADRs plus an index is a
compact, compounding context asset for both humans and agents.

Design docs still earn their keep *at write time*, so the plugin gives them a
home that matches their lifespan: TDDs live in a local, git-excluded folder,
must reference the ADRs they implement (no orphan TDDs — decisions come
first), drive the build, and then get extracted (decisions → ADRs,
constraints → inline comments) and deleted.

The design grew out of [github/spec-kit](https://github.com/github/spec-kit)
and keeps its formatting conventions — doc-type-prefixed titles, bold
metadata lines, `*(mandatory)*` markers, `[NEEDS CLARIFICATION]`, gates —
without the per-feature spec machinery, which this workflow deliberately
inverts (see [ADR 0004](docs/adr/0004-adopt-spec-kit-formatting-conventions.md)).

## What it does

- **Notices decisions.** The `adr` skill triggers when a session produces an
  architectural decision — a technology choice, a boundary change, an adopted
  convention, or a seriously-considered-and-rejected approach — and offers to
  draft the record.
- **Keeps the format honest.** One-page Nygard-style records (Context /
  Decision / Alternatives / Consequences), sequential numbering under
  `docs/adr/`, an always-current index, and consequences that include the
  costs.
- **Enforces the lifecycle.** Accepted ADRs are immutable; changes arrive as
  superseding records with a forward link. Before significant design work,
  the skill checks the index and flags contradictions with accepted ADRs
  instead of silently drifting.
- **Gives plans a disposable home.** The `tdd` skill manages local, untracked
  TDDs under `docs/tdd/` (excluded via `.git/info/exclude`, never
  `.gitignore`). Creation is gated on referencing at least one ADR in the
  TDD's `**Implements**:` line; cleanup is gated on extracting anything
  durable first.

## Commands

| Command | What it does |
| --- | --- |
| `/create-adr [title]` | Draft a new ADR from the current conversation's context |
| `/create-tdd [title]` | Draft a local, untracked TDD referencing the ADRs it implements |
| `/adr-init` | Set up `docs/adr/`, the index, and ADR 0001 (the decision to use ADRs) |
| `/adr-list` | Show all ADRs (and local TDDs) with status; reconcile index against files |
| `/adr-supersede <number>` | Replace a decision the right way — new record, forward link |
| `/adr-verify` | Check corpus integrity: index, numbering, statuses, supersede links, TDD references |
| `/adr-clean` | Run verify, then delete shipped-and-extracted TDDs; in-flight TDDs are never touched |

## Install

```sh
claude plugin marketplace add daktic-digital/dd-claude-plugins
claude plugin install spekle@daktic-digital
```

## Development

This plugin is distributed through the
[dd-claude-plugins](https://github.com/Daktic-Digital/dd-claude-plugins)
marketplace, which references this repo directly — changes pushed to `main`
here reach users on their next marketplace update, with the version bumped in
`.claude-plugin/plugin.json`.

This repo records its own design decisions under [docs/adr/](docs/adr/).

Validate before pushing:

```sh
claude plugin validate .
```

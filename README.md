# claude-adr

A Claude Code plugin that makes Architecture Decision Records the durable
artifact of development: decisions get recorded as they happen, everything
else (specs, plans, briefs) stays disposable.

The premise: per-feature specs decay the moment the feature ships, and forcing
every change through spec ceremony raises the "what size problem is this for?"
question. Decisions don't decay — they're historical records, superseded
rather than edited — and a corpus of ADRs plus an index is a compact,
compounding context asset for both humans and agents.

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

## Commands

| Command | What it does |
| --- | --- |
| `/adr init` | Set up `docs/adr/`, the index, and ADR 0001 (the decision to use ADRs) |
| `/adr new <title>` | Draft a new ADR from the current conversation's context |
| `/adr list` | Show all ADRs with status; reconcile index against files |
| `/adr supersede <number>` | Replace a decision the right way — new record, forward link |

## Install

```sh
claude plugin marketplace add daktic-digital/dd-claude-plugins
claude plugin install adr@daktic-digital
```

## Development

This plugin is distributed through the
[dd-claude-plugins](https://github.com/Daktic-Digital/dd-claude-plugins)
marketplace, which references this repo directly — changes pushed to `main`
here reach users on their next marketplace update, with the version bumped in
`.claude-plugin/plugin.json`.

Validate before pushing:

```sh
claude plugin validate .
```

# Technical Design Doc: [Title naming the work being built, e.g. "Wire rate limiting into the API gateway"]

| Field | Value |
|---|---|
| **ID** | NN |
| **Created** | YYYY-MM-DD |
| **Status** | In-flight |
| **Scope** | [One line naming the single area of concern this TDD covers, e.g. "Rate-limit middleware only, not client retries or dashboard surfacing"] |
| **Implements ADRs** | [NNNN](../adr/NNNN-slug.md) |
| **Related TDDs** | None |

<!--
  GATE: Implements must list at least one ADR — orphan TDDs are not allowed.
  If the work has no ADR yet, record the decision first, then create this
  file.
  Scope names ONE area of concern. If the Plan grows past ~5 steps or the
  steps target unrelated subsystems, split into multiple TDDs and cross-link
  them under Related TDDs (see the tdd skill's split-guidance).
  Status is exactly one of: In-flight | Shipped. /adr-clean deletes only
  Shipped TDDs whose Extraction Checklist is complete; In-flight TDDs are
  never deleted. This file is local-only (excluded via .git/info/exclude)
  and must never be committed.
-->

## Plan *(mandatory)*

*Structure the plan as per-step subsections. Each step names WHAT changes
(files, symbols, signatures) more than WHY — rationale lives in the linked
ADR. Prose rationale is at most one sentence per step.*

### Step 1 — [verb phrase, e.g. "Add rate-limit middleware factory"]

**Touchpoints:**

| File | Symbol/Section | Action |
|---|---|---|
| `path/to/file.ext` | `functionOrSection` | `add` / `edit` / `delete` |

```lang
// new or changed signature, schema, config, or SQL — the concrete thing
// the reader will paste, translate, or match against
```

**Verify:** [one-line check — the command to run, log line to look for, file
to grep, or test that should now pass]

### Step 2 — [verb phrase]

**Touchpoints:**

| File | Symbol/Section | Action |
|---|---|---|
| ... | ... | ... |

```lang
...
```

**Verify:** [...]

## Testing Strategy

[Best practice: include this. Describe how the new logic will be tested —
unit/integration coverage, how to approach something inherently hard to
test (async, external services, concurrency), or a coverage target. Skip
this section only when no new logic is being introduced (pure config, docs,
or a mechanical rename) or testing is genuinely not applicable — not merely
inconvenient.]

## Edge Cases & Risks

[What could go wrong, what inputs are weird, what existing behavior must not
change.]

## Open Questions

[Unresolved items, each marked [NEEDS CLARIFICATION: specific question].
Anything that turns into a decision with alternatives becomes an ADR, not a
paragraph here.]

## Extraction Checklist *(mandatory)*

*GATE: Must be fully checked before Status flips to Shipped — `/adr-clean`
will not delete this file otherwise. Flip Status to Shipped in the SAME turn
the last implementation step lands; do not leave a completed TDD as
In-flight.*

- [ ] Decisions made during implementation are recorded as ADRs and listed
      under **Implements**
- [ ] Constraints a future reader needs are inline comments at the point of
      use
- [ ] Nothing else in this file is worth keeping

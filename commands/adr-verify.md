---
description: Check ADR corpus integrity — index, numbering, statuses, supersede links
---

Verify the integrity of this repository's ADR corpus (conventions in
`skills/adr/SKILL.md` in this plugin). This is a read-only check: report
findings and offer fixes, but change nothing without approval.

Check:

1. **Index ↔ files.** Every ADR file appears in the index with matching
   title and status; no index entries point at missing files.
2. **Numbering.** Sequential, zero-padded to 4 digits, no duplicates or gaps.
3. **Statuses.** Every ADR has exactly one valid status: `Proposed`,
   `Accepted`, `Rejected`, or `Superseded by [NNNN](...)`.
4. **Supersede links.** Every `Superseded by` link resolves to an existing
   ADR, and that newer ADR actually states what it supersedes. Flag one-way
   links in either direction.
5. **Cross-references.** Any `[NNNN](NNNN-slug.md)` link between ADRs
   resolves to a real file.
6. **TDD references.** Every TDD in `docs/tdd/` has at least one ADR link in
   its `**Implements**:` line (orphan TDDs are a finding), every link
   resolves to an existing ADR, and none point at a superseded ADR without
   acknowledging it.

Report a compact summary: checks passed, then each finding with file and
suggested fix. If everything passes, say so in one line.

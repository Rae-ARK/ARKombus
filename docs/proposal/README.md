# Proposals

## Overview

Speculative, not-yet-accepted design proposals -- ideas put forward for
review that no maintainer has committed to yet. A file lands here when
someone has done the legwork of an audit or a design sketch, but before
any decision has been made to build it, stage it, or reject it.

## Why this is separate from `docs/foundational/`

`docs/foundational/` is the **permanent design record**, describing
decisions already made and in force. Proposals are the opposite state:
**unsettled**. A proposal describes something that does *not* exist yet,
may never be built as written, and could be rejected outright. Keeping
them in their own folder means:

- **`foundational/`'s "permanent, not deletable" guarantee stays true.**
  A rejected proposal can simply be deleted or archived.
- **A proposal's status is legible from its location**, not just its
  header.
- **Acceptance has a visible move.** When a proposal is accepted, its
  content moves into
  [`../implementation/`](../implementation/README.md) as a stage ladder,
  and into [`../foundational/`](../foundational/README.md) once built.

In short: **`foundational/` = what ARKombus is. `implementation/` = work
already underway. `proposal/` = ideas waiting for either of those to
happen to them, or for rejection.**

## What belongs here

- Audits that end in a recommendation.
- New-feature or architecture proposals not yet accepted.
- Open questions that need a decision, such as whether Flask alone owns
  the Bluetooth and call lifecycle or a separate daemon is needed.

## What doesn't

- Decisions already made and in force -- those belong in
  `docs/foundational/`.
- Work actively being built or staged -- that belongs in
  `docs/implementation/`.

## Index

| File | Covers |
| --- | --- |
| [`FRONTEND-FIRST-PROPOSAL.md`](FRONTEND-FIRST-PROPOSAL.md) | Build the ARKlight frontend first, against mock data only, before any backend: why, the honest fit question against ARKlight's stated non-targets, the screen inventory drawn from the two reference projects, a working state model, and the open questions each stage resolves. **Accepted -- staged as a nine-rung ladder (Stage 0-8) in [`docs/implementation/FRONTEND-FIRST-ADDENDUM.md`](../implementation/FRONTEND-FIRST-ADDENDUM.md).** |

## Contributing

If you add a new proposal, add a row for it in the table above. When a
proposal is accepted, move its content to `implementation/` or
`foundational/` and remove it from here (or leave a one-line pointer if
useful history).

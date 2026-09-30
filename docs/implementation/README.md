# Implementation

## Overview

Staged implementation plans for proposals that have already been
**accepted** -- turned from "should we?" into "here's the landing
order." A file here is a trackable stage ladder for work that's going to
happen (or has just happened), so accepted work has a home.

## Where this sits between an idea and a settled record

- **An open proposal** ([`../proposal/`](../proposal/README.md)) --
  *unsettled*. Nobody has decided yet.
- **`docs/implementation/`** (here) -- *accepted, not yet (fully)
  built*. A maintainer has said "yes, in this order"; what's left is
  turning each staged rung into actual commits.
- **`docs/foundational/`** ([link](../foundational/README.md)) --
  *settled and shipped*. Once every stage in a ladder here is done, any
  permanent design decision graduates into `foundational/`; anything
  that's just "here's what stage N added" stays as history, and the file
  here can be trimmed or removed.

## What belongs here

- A staged rung-by-rung implementation ladder for a proposal a
  maintainer has accepted.

## What doesn't

- An idea nobody has committed to yet.
- A permanent design decision already shipped -- that's
  `docs/foundational/`.

## Index

| File | Covers |
| --- | --- |
| [`FRONTEND-FIRST-ADDENDUM.md`](FRONTEND-FIRST-ADDENDUM.md) | Staged, nine-rung (Stage 0-8) ladder for the accepted frontend-first proposal: a feasibility spike and gap register first, then foundations, the home shell, dialpad, contacts, call log, call screens, settings, and finally the frozen UI/backend contract. All stages PLANNED. |

## Contributing

When a proposal is accepted, write its stage ladder here rather than
jumping straight to code, and add a row to the Index table above. Once
every stage has shipped, roll it up into history, graduate its permanent
decisions into `foundational/`, and trim or remove the file here.

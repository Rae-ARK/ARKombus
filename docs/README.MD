# ARKombus Documentation

This folder is the documentation index for ARKombus. Start here, then
follow the links below into the subfolders for the topic you need.
Anything that can go stale (status, tech stack, architecture, install
steps, version numbers) lives in this folder and never in the root
`README.md`.

## Folder Guide

ARKombus follows the same lifecycle doc structure as ARKlight: an idea
starts as a proposal, is staged once accepted, and graduates into the
permanent record once it has shipped.

### [`docs/proposal/`](proposal/README.md) -- unsettled

Ideas and open questions nobody has committed to yet. A file here may
never be built as written, and can be deleted or archived if rejected.

### [`docs/implementation/`](implementation/README.md) -- working reference

Staged, rung-by-rung landing orders for accepted work. Once every stage
has shipped, its permanent decisions graduate into `foundational/` and
the ladder is trimmed or removed.

### [`docs/foundational/`](foundational/README.md) -- permanent

The design record for ARKombus: what it is, how it is built, and why.
**Not deletable**; updated in place rather than removed.

## Current Work

The frontend comes first, built against mock data with no backend. The
accepted proposal is
[`proposal/FRONTEND-FIRST-PROPOSAL.md`](proposal/FRONTEND-FIRST-PROPOSAL.md)
and its stage ladder is
[`implementation/FRONTEND-FIRST-ADDENDUM.md`](implementation/FRONTEND-FIRST-ADDENDUM.md).
The backend proposal starts once that ladder's contract is frozen
(Stage 8).

## Tech Stack

| Layer | Choice |
| --- | --- |
| Frontend | [ARKlight](https://github.com/Rae-ARK/ARKlight) (compiled static output) |
| Backend | Flask |
| System integration | Flask talks to the services Ubuntu already provides (BlueZ, obexd, PipeWire, freedesktop notifications) directly, with no separate daemon |

The no-daemon direction is the maintainer's stated preference. It is
recorded here as the current direction, not yet as a settled design
record. A separate daemon stays on the table only if Flask cannot own
the Bluetooth and call lifecycle cleanly; that question belongs in
`docs/proposal/` until decided.

## Reference Material

The repo root carries two third-party reference checkouts used for study
only, not as code to reuse:

- `handsfree-linux-reference/` -- an existing Python/PyQt HFP hands-free
  app for Linux (BlueZ, SCO audio, PBAP contacts). MIT licensed.
- `opendialer-reference/` -- an open-source Android dialer (Kotlin), used
  as a UX reference for the dialer, contacts and call-log screens.
  Apache-2.0 licensed.

Both are studied for ideas, not ported.

## Source Layout

| Folder | Role |
| --- | --- |
| [`src/frontend/`](../src/frontend/README.md) | The ARKlight site |
| [`src/backend/`](../src/backend/README.md) | The Flask application |

## Contributing to the Docs

If you add a new doc file, add a row for it in the index table of the
folder it lives in, and in the relevant table above if it is a new
folder, so this index stays accurate.

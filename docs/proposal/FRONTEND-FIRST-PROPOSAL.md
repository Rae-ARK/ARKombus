# Frontend First

**Status: Accepted -- staged as a nine-rung ladder (Stage 0-8) in
[`docs/implementation/FRONTEND-FIRST-ADDENDUM.md`](../implementation/FRONTEND-FIRST-ADDENDUM.md).**
Nothing is built yet. This file keeps the reasoning; the addendum keeps
the landing order.

## The proposal

Build the ARKombus frontend first, complete and navigable, against
**mock data only**, before any backend work starts. The frontend is an
[ARKlight](https://github.com/Rae-ARK/ARKlight) site in `src/frontend/`
that runs in an ordinary browser with no Flask, no Bluetooth and no
phone attached. The backend (Flask talking to Ubuntu's own services) is a
separate proposal that starts only after the frontend's contract is
frozen (Stage 8).

## Why frontend first

- **The UI is the least certain part.** Two reference projects agree on
  the screens but not the shape, and ARKlight has never been asked to
  build a stateful, live-updating app like this one.
- **A frozen contract makes the backend small.** Once every screen runs
  on a fixed state snapshot and a fixed command list, the backend's job
  is to produce that snapshot and accept those commands. Nothing has to
  be invented on the fly.
- **Mock data needs no hardware.** The whole call state machine can be
  walked from a desk with no phone paired.
- **It stress-tests ARKlight early.** Any capability the site needs that
  ARKlight lacks is found while nothing else depends on it.

## The fit question, stated plainly

ARKlight's own
[`WHAT-ARKLIGHT-IS.md`](https://github.com/Rae-ARK/ARKlight/blob/main/docs/Foundational/WHAT-ARKLIGHT-IS.md)
lists "API-driven application requiring arbitrary HTTP requests" as not
feasible today and "complex multi-view client application" as not
currently targeted. ARKombus is both, eventually. This proposal does not
pretend otherwise. What makes it workable anyway:

- **Mock-first sidesteps the HTTP gap for now.** Screens run on
  `State(...)`, `Repeat`, `Show`, `Computed` and `bind_value`, all of
  which ARKlight ships.
- **The live-data seam is deferred and isolated.** Stage 8 decides how
  real data reaches the page, behind one interface, so the choice
  doesn't leak into screens.
- **Gaps are recorded, not hidden.** Stage 0 produces a gap register.
  Each gap is closed by one of three routes, tried in this order:
  1. **Compose** existing closed-vocabulary pieces.
  2. **Fix upstream in ARKlight** as a small capability fix, since both
     repos share a maintainer.
  3. **Use ARKlight's own-script escape hatch** (`Page(scripts=...)`),
     experimental and last.

Gaps already visible from reading ARKlight's source (unconfirmed until
Stage 0 builds them): no ticking timer for a call-duration clock, no
keyboard-event primitive, and `Action.append` only appends to lists, so
dialpad digits have to be a list joined into a string.

## Scope

**In scope:** every screen a user touches, the mock state that drives
them, the visual theme, and a written contract between UI and backend.

**Out of scope, deferred to later proposals:**

- Anything Flask, D-Bus, BlueZ, PipeWire or audio.
- The native window (pywebview or otherwise), the floating in-call
  overlay, the tray icon and native notifications. These are shell
  concerns; the frontend only has to run in a normal browser.
- Testing inside WebKitGTK.
- Packaging, autostart and install.

## Screen inventory

Sources: `handsfree-linux-reference/` (MIT, an HFP app; screens and
states) and `opendialer-reference/` (Apache-2.0, an Android dialer; UX
only, Kotlin, nothing to port).

| Screen | Purpose | Reference |
| --- | --- | --- |
| Home shell | Tab bar over Calls and Contacts, dialpad button | opendialer `HomeScreen`; handsfree tabs |
| Connection states | Bluetooth off, no phone, connecting, connected | handsfree's three dial-tab pages |
| Dialpad | Digit entry, call button, live contact match | opendialer `contactsSearch`; handsfree dial page |
| Contacts | Searchable list, contact profile with call button | both |
| Call log | Incoming, outgoing, missed; redial | both |
| Incoming call | Caller, Answer, Decline, Silence | handsfree `call_popup` |
| In-call | Caller, timer, Mute, Hold, DTMF keypad, volume, End | handsfree in-call page; opendialer ongoing call |
| Call ended | Brief summary state | handsfree overlay's "Call Ended" |
| Settings | Connected device, audio in/out, preferences, about | handsfree settings tab |

Dropped from the references because HFP cannot support them: voicemail,
call transfer, video, per-contact chat.

## Working state model

A first sketch. Stage 8 freezes the real one.

| Slice | Fields |
| --- | --- |
| `link` | bluetooth `off`/`on`; phone `none`/`connecting`/`connected`; phone name |
| `call` | phase `idle`/`incoming`/`dialing`/`ringing`/`active`/`held`/`ended`; direction; number; contact; elapsed; muted; volume |
| `contacts` | list of id, name, numbers, photo |
| `call_log` | list of id, number, contact, direction `in`/`out`/`missed`, time, duration |
| `prefs` | audio output, audio input, other settings |

Commands the UI issues: `dial`, `redial`, `answer`, `decline`, `hangup`,
`hold`/`swap`, `dtmf`, `mute`, `set_volume`, `connect`/`disconnect`,
`set_audio_device`, `sync_contacts`. These mirror what HFP offers.

## Decisions and defaults

- **Layout defaults to compact, phone-style,** following opendialer,
  since that is the reference that was picked. ARKlight's
  container-width layout leaves a two-pane desktop layout open later.
  This is a default, not a lock.
- **Mock data lives in one place** so removing it later is one change.
- **Screens never read the wire format directly.** They read the state
  slices above; only the seam knows how those arrive.

## Open questions

Each is resolved at a named stage of the ladder.

| # | Question | Resolved at |
| --- | --- | --- |
| 1 | Which gaps exist, and which route closes each | Stage 0 |
| 2 | Single page switching views with `Show`, or multiple pages with `app_shell=True` | Stage 1 |
| 3 | Can a call-duration clock tick at all | Stage 0, used in Stage 6 |
| 4 | Where the call log comes from (phone over PBAP, or stored by ARKombus) is a backend question; the UI only needs a list | Stage 8 contract, backend proposal |
| 5 | How live state reaches the page (declared `Provider`, own script, or htmx) | Stage 8 |

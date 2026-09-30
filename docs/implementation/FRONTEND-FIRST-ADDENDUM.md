# Frontend First -- Implementation Addendum

Staged landing order for the accepted proposal
[`FRONTEND-FIRST-PROPOSAL.md`](../proposal/FRONTEND-FIRST-PROPOSAL.md).
Nine rungs, Stage 0 to Stage 8, easiest and riskiest-first. Nothing has
shipped.

## Ground rules for every stage

- Everything runs on **mock data** in a normal browser. No Flask.
- Work lands in `src/frontend/`. Docs land here and in `docs/`.
- A stage is done when its exit criterion holds, not when its code
  exists.
- Any ARKlight gap found is written into the gap register (Stage 0's
  output, kept at the bottom of this file) with the route chosen
  (compose, fix upstream, own script).
- Record the exact ARKlight version used in Stage 0 so later stages
  build against the same one.

## Ladder

| Stage | Name | Status |
| --- | --- | --- |
| 0 | Feasibility spike and gap register | PLANNED |
| 1 | Foundations: scaffold, theme, navigation, mock state | PLANNED |
| 2 | Home shell and connection states | PLANNED |
| 3 | Dialpad and contact match | PLANNED |
| 4 | Contacts and contact profile | PLANNED |
| 5 | Call log | PLANNED |
| 6 | Call screens: incoming, in-call, ended | PLANNED |
| 7 | Settings and persisted preferences | PLANNED |
| 8 | Contract freeze, seam, graduation | PLANNED |

### Stage 0 -- Feasibility spike and gap register

**Work.** Scaffold a throwaway site in `src/frontend/`. Build the
smallest version of each risky thing: digit entry into a string, a
ticking clock, a filtered list, a full-screen overlay, a view switch,
keyboard input, and one hand-written attempt at receiving pushed state.
Confirm or refute each suspected gap from the proposal.

**Exit.** The site builds and opens over `file://` and a plain static
server. The gap register lists every gap with its chosen route. Open
questions 1 and 3 are answered.

### Stage 1 -- Foundations

**Work.** Real scaffold; design tokens (light and dark, colors, spacing,
type) as ARKlight style classes; the navigation model (open question 2);
the single mock-state module holding the five slices from the proposal;
a dev-only scenario panel that can set any slice by hand.

**Exit.** Two placeholder views switch correctly and keep state; the
scenario panel changes what is on screen; the mock data is in one place.

### Stage 2 -- Home shell and connection states

**Work.** Tab bar (Calls, Contacts), dialpad button, and the four
connection states (Bluetooth off, no phone, connecting, connected), each
with its own empty state and call to action.

**Exit.** Every connection state is reachable from the scenario panel and
reads clearly; the tab bar works in the connected state.

### Stage 3 -- Dialpad and contact match

**Work.** Dialpad, digit display with backspace, call button, and a live
contact match against mock contacts by name or number. T9-style initials
search is optional and can be dropped.

**Exit.** Typing digits builds a number, shows matching contacts, and
pressing call moves the mock call state to `dialing`.

### Stage 4 -- Contacts and contact profile

**Work.** Contact list with search and avatar fallback, a profile screen
with numbers, recent calls and a call button. Mock data is large enough
(hundreds of entries) to show list cost.

**Exit.** Search filters the list; a profile opens and calls; scroll and
search stay responsive with the large mock set. If not, that is a
recorded gap, not a hidden one.

### Stage 5 -- Call log

**Work.** Grouped-by-day list of incoming, outgoing and missed calls,
missed filter, tap to open profile, redial action.

**Exit.** All three directions render distinctly; redial moves the mock
call state to `dialing`.

### Stage 6 -- Call screens

**Work.** Incoming (Answer, Decline, Silence), dialing/ringing, in-call
(name, duration clock, Mute, Hold, DTMF keypad, volume, End) and a brief
ended state. The scenario panel can walk the full call state machine.

**Exit.** Every legal phase transition works from the UI or the panel;
illegal ones are unreachable. The duration clock behaves as Stage 0
decided.

### Stage 7 -- Settings and persisted preferences

**Work.** Connected device, audio output and input pickers, and other
preferences, persisted with ARKlight's own persistence (`persist=True`
state or `PlatformAPI.db`).

**Exit.** Preferences survive a reload; the settings screen works in
every connection state that allows it.

### Stage 8 -- Contract freeze, seam, graduation

**Work.** Write the frozen state snapshot and command list as the
contract for the backend proposal. Put one seam between the screens and
the mock data, and decide how live state will reach the page (open
question 5). Run an all-screens walkthrough in a normal browser.

**Exit.** The contract is written down; swapping the mock module for a
different source touches only the seam; every screen is reachable with
no console errors. Permanent decisions graduate into
`docs/foundational/` (screen inventory, state model, contract) and this
file is trimmed.

## Gap register

Filled in during Stage 0 and kept current afterwards.

| Gap | Seen where | Route | Status |
| --- | --- | --- | --- |
| No ticking timer for a call clock | Read from ARKlight source | to decide | unconfirmed |
| No keyboard-event primitive | Read from ARKlight source | to decide | unconfirmed |
| `Action.append` is list-only (dialpad digits) | Read from ARKlight source | compose (list plus join) | unconfirmed |
| No general fetch or push of live state | ARKlight's own docs | Stage 8 | deferred |

## Contributing

Update a stage's Status here when it lands, and keep the gap register
current. When Stage 8 is done, roll this file up into history and
graduate its permanent decisions into `docs/foundational/`.

# SableOS common product integration

## Current product state — 2026-09-25

Panther R9 product composition is accepted and frozen as the touch-first
reference after the final Sable Hub V1 closure.

```text
R9_PANTHER_ACCEPTED_SOURCE=edf62e5bb08372a1395841d6cc5d78d3148a7695
R9_PANTHER_TARGET_FILES_SHA256=a0b359613c4f30e9a834fba212e0b044a97d63ed0537c59471c31b99b627d285
R9_PANTHER_PHYSICAL_ACCEPTANCE=PASS_WITH_PRESERVED_PLAY_STATE
```

Active integration work now targets the keyboard-first Titan family.

The accepted common first-party product set includes:

```text
Sable HOME / launcher presentation
Sable Calculator
Sable Sudoku
Sable Minesweeper
Sable 2048
Sable Media
Sable Reader
Sable Text Reader
Sable Hub / Messages
Sable Mail
Sable Weather
Sable Calendar
```

Sable Hub V1 is the accepted communications surface:

```text
Priority | Messages | Email | People
```

Hub is an aggregator/interaction surface. Source applications/providers retain
account, credential, private database and protocol-stack ownership.

## Common product rule

`vendor_sable` owns common imported-module/product selection and common
permission/product integration. It must not contain copied application source,
device-specific forks or opaque host-private artifacts.

Panther, Titan 2 and Titan 2 Elite should consume the same common qualified
application source/artifacts wherever substrate compatibility permits.

Target-specific exceptions belong in bounded device adapters and must be
explicit.

## Keyboard-first additions

Two common system-image capabilities are active design work:

**Sable Camera**
- common Camera2/capability-driven source;
- device camera profiles below the common core;
- SYSTEM_CAMERA privilege only on devices where physical evidence proves it is
  needed and negative third-party-access tests pass.

**Sable Keyboard / input**
- offline-capable common IME/text composition;
- physical keylayout/keycharacter/Fn/Sym/backlight quirks remain device-owned.

## Claim discipline

```text
source checks
 != trusted artifact
 != product selected
 != image membership
 != runtime/default role
```

A Panther PASS does not imply Titan PASS.

## K1/K2 integration note

The common product composition is independent of release artifact class. Panther
is represented by the qualified target-files path; future Titan N0 may use a
GSI/system artifact while consuming the same common Sable application source
where compatible. Device serials are deployment identity, never product
composition identity.

## Open follow-ups

Appearance/theme propagation, large-library Media behavior, duplicate visible
Messages review, production icons, first-run crash capture and All Apps
permission summaries remain open follow-ups until Titan 2 SableOS install work
proves or supersedes them.

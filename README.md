# SableOS common product integration

## Current product state

Panther R9 product composition is accepted and frozen as the touch-first
reference. Active integration work now targets the keyboard-first Titan family.

The accepted common first-party product set includes:

```text
SableLauncher
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

Launcher3QuickStep remains a platform Recents/Overview substrate, not the
user-facing HOME owner.

## Common product rule

`vendor_sable` owns common imported-module/product selection and common
permission/product integration. It must not contain copied application source,
device-specific forks or opaque host-private artifacts.

Panther, Titan 2 and Titan 2 Elite should consume the same common qualified
application source/artifacts wherever substrate compatibility permits.

Target-specific exceptions belong in bounded device adapters and must be
explicit.

## Keyboard-first additions

Two common system-image capabilities are now active design work:

**Sable Camera**
- common Camera2/capability-driven source;
- device camera profiles below the common core;
- SYSTEM_CAMERA privilege only on devices where physical evidence proves it is
  needed.

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

The common product composition is independent of release artifact class. Panther is represented by the qualified target-files path; future Titan N0 may use a GSI/system artifact while consuming the same common Sable application source where compatible. Device serials are deployment identity, never product composition identity.

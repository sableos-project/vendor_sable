# SableOS common product integration

## Current product state — 2026-10-02

Panther R9 product composition is accepted and frozen as the touch-first
reference after the final Sable Hub V1 closure.

```text
R9_PANTHER_ACCEPTED_SOURCE=edf62e5bb08372a1395841d6cc5d78d3148a7695
R9_PANTHER_TARGET_FILES_SHA256=a0b359613c4f30e9a834fba212e0b044a97d63ed0537c59471c31b99b627d285
R9_PANTHER_PHYSICAL_ACCEPTANCE=PASS_WITH_PRESERVED_PLAY_STATE
```

Active integration work now targets Titan 2 through the N1D/C3B E3 canonical
integration lane. E1 and E2 are qualified; the first Sable-composed E3
systemimage build is running and not yet sealed. Public build/flash enablement
remains separately gated.

The accepted common first-party product set includes:

```text
Sable HOME / launcher presentation
Sable Calculator
Sable Sudoku
Sable Minesweeper
Sable 2048
Sable Media
Sable Reader (Reader v2 architecture accepted: EPUB/PDF + comics + audiobooks)
Sable Text Reader (separate lightweight text/TTS/accessibility product)
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

## Current product-source train

Parallel source work currently runs in `aimindseye/titan2-temp`:

```text
P1  Sable Start keyboard-first handoff
P2  Sable Keyboard provisioning readiness
P3  SetupWizard2 keyboard/square-display integration preparation
P4  Weather city-management + keyboard-first closure
```

The stages are developed continuously, frozen independently and receive one
batched exact-head ai-g732 qualification after P4 before canonical admission.

P5 Sable Reader v2 architecture is accepted and may proceed as a separate P5A-P5F implementation train: common keyboard-first EPUB/PDF, local-first CBZ comics/manga/webtoons and audiobooks. Sable Text Reader remains a separate lightweight product. P5 source is not yet admitted into a Titan image.

## Design-reference boundary

The 23-screen `titan2-temp/apps/titan2/screens` catalog is an accepted common design/behavior reference:

```text
SABLESCREENS_REFERENCE_BASELINE=YES
SABLESCREENS_SHIPPING_PRODUCT=NO
```

It informs common product composition and convergence but is never packaged as a substitute for canonical runtime owners.

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
- common Sable-owned Camera2/capability-driven source;
- keyboard-device **Camera Control Deck** interaction: viewfinder-first,
  portrait supported, landscape physical-control optimization, touch fallback;
- device camera profiles below the common core;
- SYSTEM_CAMERA privilege only on devices where physical evidence proves it is
  needed and negative third-party-access tests pass.

**Sable Keyboard / input**
- offline-capable common IME/text composition;
- physical keylayout/keycharacter/Fn/Sym/backlight quirks remain device-owned;
- Sable Keyboard may be the factory/default first-party IME while user-selected
  third-party IMEs remain allowed.

## Default/user-choice distinction

Common product composition defines Sable first-party defaults; it does not ban
Android user choice.

```text
SABLE_FIRST_PARTY_HOME=Launcher3QuickStep_HOSTING_SABLE_START
THIRD_PARTY_HOME_SELECTION_ALLOWED=YES
FORCE_SABLE_HOME_AFTER_USER_SELECTION=NO
SABLE_FIRST_PARTY_IME=SableKeyboard
THIRD_PARTY_IME_SELECTION_ALLOWED=YES
FORCE_SABLE_IME_AFTER_USER_SELECTION=NO
```

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
is represented by the qualified target-files path; Titan N1D/C3B engineering may use a
GSI/system-image path while consuming the same common Sable application source
where compatible. Device serials are deployment identity, never product
composition identity.

## Open follow-ups

Appearance/theme propagation, large-library Media behavior, duplicate visible
Messages review, production icons, first-run crash capture and All Apps
permission summaries remain open follow-ups until Titan 2 SableOS install work
proves or supersedes them.

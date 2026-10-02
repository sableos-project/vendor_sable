# SableOS default application composition

Status: **current common product composition — 2026-10-02**

Panther R9 physically accepted the current common product composition and is now
a frozen reference. Titan-family work should reuse this common composition where
substrate compatibility permits, with bounded exceptions only.

## Current first-party set

```text
Sable Start           presentation/state hosted in Launcher3QuickStep
Sable Calculator      org.sableos.calculator
Sable Sudoku          org.sableos.sudoku
Sable Minesweeper     org.sableos.minesweeper
Sable 2048            org.sableos.game2048
Sable Media           org.sableos.media
Sable Reader          org.sableos.reader
Sable Text Reader     org.sableos.textreader
Sable Hub / Messages  org.sableos.hub
Sable Mail            org.sableos.mail
Sable Weather         org.sableos.weather
Sable Calendar        org.sableos.calendar
```

Launcher3QuickStep is the canonical Sable first-party HOME runtime and
Recents/Overview/task/gesture substrate. It hosts Sable Start
presentation/state source.

Standalone `org.sableos.launcher` / SableLauncher and standalone SableStart HOME
runtimes are retired from the current product architecture.

This is first-party/default ownership, not a prohibition on Android user choice:

```text
THIRD_PARTY_HOME_SELECTION_ALLOWED=YES
FORCE_SABLE_HOME_AFTER_USER_SELECTION=NO
```

## Reader boundary

Sable Reader and Sable Text Reader are intentionally separate launcher-visible
products.

Sable Reader owns publication/Readium behavior.

Sable Text Reader owns TXT/share/process-text/paste/edit/local TTS+WAV/OCR
behavior with no INTERNET requirement and no translation/model-download path.

## Browser / inherited platform apps

Vanadium is the accepted browser reference on Panther.

Inherited Android/substrate applications remain valid where no Sable-owned
replacement has been accepted. Replacement is a separate evidence decision, not
a branding preference.

Panther Camera remains the documented frozen-R9 upstream/preprocessed visual
exception. Keyboard-first devices move toward the Sable-owned Camera2 component
with the Camera Control Deck interaction model.

## Appearance

Settings is the global appearance authority. Sable apps consume common
Follow-system/Light/Dark semantics.

## Keyboard-first additions

The common product architecture adds two explicit system-image workstreams:

- Sable Camera / Camera Control Deck;
- Sable Keyboard / input.

They remain common product source with device-specific profiles/adapters below
them. Sable Keyboard is the first-party/default direction, while Android
third-party IME installation/enablement/selection remains allowed and SableOS
must not force its IME back after explicit user choice.

## Product evidence

For an application/product claim distinguish:

```text
source qualified
trusted artifact
product selected
installed path
image/artifact membership
runtime/default role
```

Do not collapse these layers.

## Multi-device composition

Panther is the qualified target-files/full-image reference.

Titan 2 N1D/C3B engineering may use a GSI/system-image path while preserving the
qualified vendor/kernel boundary; Titan 2 Elite remains independently gated. They should still consume the same common app source
where compatible.

A Titan-specific keyboard/display/camera/vendor adapter is valid. A duplicate
common app fork is not.

## Signing

Development/test signing is separate from production release signing.
Production app/AVB/OTA signing remains deferred.

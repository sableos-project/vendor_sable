# SableOS common product integration

Common SableOS Android product composition, overlays, permissions integration, and qualified application inclusion.

This repository is **not** a home for copied application source, opaque locally built APKs, external Gradle dependency trees, or device-specific forks.

## Ownership boundary

- application repositories/workspaces own application source, tests and standalone build/dependency graphs;
- `platform_sable` owns shared Sable semantic/design/application architecture contracts;
- `vendor_sable` owns common Sable product selection/import/configuration;
- `device_sable_*` owns bounded target-specific adaptation;
- `platform_manifest` binds exact source composition and accepted external artifact provenance;
- `build` proves Android product wiring/image/runtime claim layers.

See [`docs/OWNERSHIP_BOUNDARY.md`](docs/OWNERSHIP_BOUNDARY.md).

## Current R8 product-integration model

R8 applications are qualified independently before they enter this repository's product boundary.

```text
standalone Cargo/Gradle/upstream qualification
    -> exact APK/source/workflow freeze
    -> product import/module proof
    -> common vendor_sable selection
    -> PRODUCT_OUT
    -> target-files/image
    -> runtime
```

A standalone-qualified APK is **not** automatically a shipping/default app.

The exact Android 17 / GrapheneOS mechanism for consuming sealed standalone APKs is still to be proven. `android_app_import` is a candidate, not a documented fact yet.

Do not add opaque manually generated APKs to this repository without reproducible source/workflow/hash provenance.

## Current R8 application candidates

The consolidated R8 application train includes:

- Calculator + Convert;
- Games (Sudoku, Minesweeper, 2048);
- one Sable Reader product composed from qualified publication and TXT/share/TTS/OCR capabilities;
- Sable Media (local Music + Internet Radio).

R8 source qualification does not automatically replace inherited daily-driver apps. Product inclusion, default roles and replacement cleanup remain separate gates.

The old sequence "R8 design foundation -> R9 first Sable Calculator replacement" is superseded. Calculator now belongs to R8-B, but an inherited calculator may remain the product fallback until Sable Calculator passes standalone and product/runtime gates.

## Default applications

Normative product-selection policy:

- [`docs/DEFAULT_APPLICATION_COMPOSITION.md`](docs/DEFAULT_APPLICATION_COMPOSITION.md)
- organization-wide `sableos-project/.github/docs/DEFAULT_APP_AND_REPLACEMENT_POLICY.md`

Phone, Messaging, Browser and Camera remain proven-inherited-first categories unless a separately justified Sable replacement is qualified.

Maps/Weather or similar apps used during development remain fixtures unless a separate product decision includes them.

## Current implementation-state caution

Open product-composition PRs are implementation state, not merged `main` reality. Documentation must not claim a module/package is part of the shipping product until product selection/install/image evidence proves it.

## R8 integration freeze

Before `vendor_sable` consumes an app, the accepted record should identify at least:

```text
source repo + commit
upstream/reuse commit(s)
qualification workflow/run
package ID + version
APK SHA-256
permissions/exported components
native ABI/library inventory
dependency/provenance inventory
accepted feature-policy boundary
```

Product integration then records module/import, partition/install path, transformation/signing behavior, PRODUCT_OUT hash and target-files/image identity.
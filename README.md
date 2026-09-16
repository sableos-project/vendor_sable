# SableOS common product integration

Common SableOS Android product composition, overlays, permission integration and inclusion of qualified/trusted application artifacts.

This repository is **not** a home for copied application source, opaque local APKs, external Gradle dependency trees or device-specific forks.

## Ownership boundary

- application repositories/workspaces own app source/tests/dependency graphs;
- `platform_sable` owns shared semantic/design/application architecture;
- `vendor_sable` owns common imported-module definitions and common Sable product selection;
- `device_sable_*` owns bounded target-specific adaptation;
- `platform_manifest` binds source composition and trusted external-artifact provenance;
- `build` proves trusted artifact, Soong/product, image and runtime claim layers.

## Current R8 product-integration model

```text
A1 disposable app qualification
    -> A2 trusted standalone app build on ai-g732
    -> exact trusted artifact freeze
    -> B1 common Soong import/module proof
    -> common vendor_sable selection
    -> PRODUCT_OUT
    -> target-files/image
    -> Panther runtime
    -> Titan 2 portability runtime
```

An A1-qualified APK is not automatically a trusted product input. The artifact entering `vendor_sable` integration must be the exact accepted A2 result.

The exact Android 17 / GrapheneOS mechanism is proved empirically. `android_app_import` is the preferred candidate, not an assumption.

## Common module/product ownership

Preferred common shape:

```text
vendor/sable/apps/Android.bp
    common imported application modules

vendor/sable/config/common.mk
    common PRODUCT_PACKAGES composition
```

Panther and Titan 2 products inherit the common Sable composition and add only documented target-specific exceptions. Do not duplicate the common application list in every device repository.

## Current R8 app candidates

- Calculator + Convert;
- Games: Sudoku / Minesweeper / 2048;
- one Sable Reader product composed from publication and TXT/share/TTS/OCR capabilities;
- Media: local Music + Internet Radio.

Inherited daily-driver applications remain valid fallbacks until a Sable replacement completes product/runtime/default-role acceptance.

## Trusted input contract

Before `vendor_sable` consumes an app record at least:

```text
source/upstream commit(s)
trusted A2 build/toolchain identity
package ID + version
trusted APK SHA-256
permissions/exported components
DEX/JNI inner-content identities
native ABI / 16 KiB compatibility
dependency/license/provenance inventory
accepted feature-policy boundary
```

Product integration then records module/import identity, certificate/signing behavior, partition/install path, product selection, PRODUCT_OUT identity and later target-files/image/runtime evidence.

## Signing boundary

Development/test signing may be used for engineering images. Production APK/AVB/OTA signing is deferred until Panther and Titan 2 development qualification is satisfactory and is not owned by current R8 `vendor_sable` integration.

## Claim discipline

```text
trusted APK
 != product selected
 != PRODUCT_OUT present
 != target-files present
 != image present
 != runtime/default role
```

See [`docs/DEFAULT_APPLICATION_COMPOSITION.md`](docs/DEFAULT_APPLICATION_COMPOSITION.md) and [`docs/OWNERSHIP_BOUNDARY.md`](docs/OWNERSHIP_BOUNDARY.md).

# SableOS common product integration

![Local CI](https://img.shields.io/badge/CI-local%20direct-active-2ea44f)
![R9 Launcher](https://img.shields.io/badge/R9%20launcher%20visual-PASS-2ea44f)
![Fresh Panther](https://img.shields.io/badge/fresh%20Panther%20build-IN%20PROGRESS-f0ad4e)
![Pixel 7](https://img.shields.io/badge/Pixel%207%20physical-PENDING-lightgrey)
![Titan 2](https://img.shields.io/badge/Titan%202-keyboard--first%20QUEUED-6f42c1)

## Current R9 product state

The current Panther composition has moved beyond the earlier R8 planning model. The accepted first-party app set is Calculator, Sudoku, Minesweeper, 2048, Media, Reader, Hub/Messages and Mail. Launcher HOME is source-built `Launcher3QuickStep`; the old standalone SableStart HOME APK is absent from the product graph.

Target-files composition for these identities has passed. Fresh full-build causality and physical Pixel 7 runtime acceptance remain separate R9 gates. Titan 2 will consume the same common application/product contracts where compatible after Panther closure.

Common SableOS Android product composition, overlays, permission integration and inclusion of qualified/trusted application artifacts.

This repository is **not** a home for copied application source, opaque local APKs, external Gradle dependency trees or device-specific forks.

## Ownership boundary

- application repositories/workspaces own app source/tests/dependency graphs;
- `platform_sable` owns shared semantic/design/application/security-quality architecture;
- `vendor_sable` owns common imported-module definitions and common Sable product selection;
- `device_sable_*` owns bounded target-specific adaptation;
- `platform_manifest` binds source composition and trusted external-artifact provenance;
- `build` proves trusted artifact, Soong/product, image and runtime claim layers.

Organization-wide engineering-assurance requirements live in `sableos-project/.github/docs/SECURITY_QUALITY_ENGINEERING.md`.

## Current product-integration model

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

The exact Android 17 / GrapheneOS consumption mechanism is proved empirically. `android_app_import` is the preferred mechanism where it preserves the accepted standalone artifact/provenance boundary.

## Common module/product ownership

Preferred common shape:

```text
vendor/sable/apps/Android.bp
    common imported application modules

vendor/sable/config/common.mk
    common PRODUCT_PACKAGES composition
```

Panther and Titan 2 products inherit the common Sable composition and add only documented target-specific exceptions. Do not duplicate the common application list in every device repository.

## Current first-party app direction

- Sable Calculator: Standard + Scientific + offline conversion;
- Sable Sudoku;
- Sable Mines;
- Sable 2048;
- one Sable Reader product composed from publication and TXT/share/TTS/OCR capabilities;
- Sable Media: local Music + Internet Radio;
- Sable Hub / Messages;
- Sable Mail.

A separate Sable Convert APK is no longer the preferred final product shape. The validated Panther reference build remains historical evidence even when later R8 application identities change.

Inherited daily-driver applications remain valid fallbacks until a Sable replacement completes product/runtime/default-role acceptance.

## Trusted input contract

Before `vendor_sable` consumes an app, record at least:

```text
source/upstream commit(s)
trusted A2 build/toolchain identity
canonical lock/dependency identity
package ID + version
trusted APK SHA-256
permissions/AppOps implications
exported components / intent filters
DEX/JNI inner-content identities
native ABI / 16 KiB compatibility
dependency/license/provenance inventory
security/static-analysis summary
coverage provenance where applicable
OWASP MASVS/MASTG evidence/exception references where applicable
accepted feature/privacy/network boundary
known security/quality limitations
```

Trusted-input evidence should also bind SBOM/provenance identity when the canonical pipeline produces it.

A scanner PASS, high coverage percentage or successful standalone build does not substitute for this input contract.

Product integration then records:

```text
module/import identity
certificate/signing behavior
JNI/dexpreopt/uses-library processing
partition/install path
common product selection
PRODUCT_OUT identity
target-files/image identity
runtime/default-role evidence where applicable
```

## Permission and privilege rule

Shipping on `/system` does not automatically justify privileged status, a shared UID, a custom SELinux domain or broad permissions.

For every new authority, identify the product requirement and validation/rollback path. Ordinary app-domain behavior is preferred where sufficient. New shared UIDs are not introduced for convenience.

## Security/update ownership

Integrating a Sable replacement creates a maintenance obligation. Before removing a proven inherited fallback, the replacement must have a clear source owner, dependency-update path, security scanning/test path, reproducible artifact process and rollback/fallback story.

Upstream/reused code remains subject to dependency/license/security review even when it comes from another Sable-owned project.

## Dual-target and performance discipline

Where compatible, Panther and Titan 2 consume the same trusted common application artifacts and common product selection. Device-specific forks are not created merely to tune one target.

Performance-sensitive integration changes must be measured on representative hardware. Panther performance evidence does not automatically establish Titan 2 behavior.

## Signing boundary

Development/test signing may be used for engineering images. Production APK/AVB/OTA signing is deferred until repeatable Panther and Titan 2 development qualification is satisfactory and is not owned by current R8 `vendor_sable` integration.

## Claim discipline

```text
source/security checks pass
 != trusted A2 artifact

trusted A2 artifact
 != product selected

product selected
 != PRODUCT_OUT present

PRODUCT_OUT present
 != target-files present

target-files present
 != image/runtime/default role

Panther PASS
 != Titan 2 PASS
```

See [`docs/DEFAULT_APPLICATION_COMPOSITION.md`](docs/DEFAULT_APPLICATION_COMPOSITION.md) and [`docs/OWNERSHIP_BOUNDARY.md`](docs/OWNERSHIP_BOUNDARY.md).

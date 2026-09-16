# Default application composition policy

Status: **normative product-integration/default-application policy.**

`vendor_sable` owns common product inclusion/configuration for validated applications. It does not own application implementation source or the standalone Cargo/Gradle dependency graph.

## 1. Separate the states

Use explicit states:

```text
SOURCE_CANDIDATE
STANDALONE_QUALIFIED
ARTIFACT_FROZEN
PRODUCT_INTEGRATED
IMAGE_PRESENT
RUNTIME_VALIDATED
DEFAULT_OR_ROLE_HOLDER
REPLACEMENT_ACCEPTED
```

Do not collapse these into one "included" flag.

## 2. R7 baseline

R7 daily-driver qualification records the actual working Phone, Messaging, Contacts, Browser, Camera, Files, Clock, Calculator and other baseline implementations.

An inherited/proven app is acceptable where the Sable replacement is not yet qualified. Do not force a replacement merely to make the product look more Sable-branded.

## 3. R8 application train

R8 independently qualifies:

- Calculator + Convert;
- Games;
- Reader publication capability;
- Reader TXT/share/process-text/TTS/OCR capability;
- Media.

A successful standalone qualification does not select the app into the OS. `vendor_sable` becomes relevant only at the integration freeze/product-composition stage.

The old R9-first-Calculator sequencing is superseded. Sable Calculator is an R8-B candidate, while the inherited calculator remains a valid fallback until the Sable app completes product/runtime acceptance.

## 4. Input contract for a qualified app

Before common product inclusion, record:

```text
source repository + exact commit
upstream/reuse source + exact commit where applicable
qualification workflow/run
application/package ID
versionCode/versionName
APK SHA-256
permissions/AppOps implications
exported components/intent filters
native ABI/library inventory
dependency/license/provenance inventory
accepted feature-policy boundary
known limitations
```

Do not store an APK here when its provenance/rebuildability cannot be stated.

## 5. Android import/module proof

The exact Android 17 / GrapheneOS mechanism for consuming a sealed APK must be proven before being normalized.

`android_app_import` is currently a candidate. Whatever mechanism is selected must establish:

```text
sealed APK/input hash
 -> declared Sable module/import
 -> selected PRODUCT_PACKAGES/product composition
 -> expected partition/install path
 -> concrete PRODUCT_OUT artifact
 -> installed-files evidence
 -> target-files/image membership
```

If the build intentionally transforms/re-signs the APK, record both input and resulting output identities instead of falsely requiring byte equality.

## 6. Product/default role is a separate gate

Installing an app in the image does not make it the default HOME/Dialer/SMS/Browser or other role holder.

For role/default transitions prove:

- previous and new package/component;
- role/default state;
- privileged grants/allowlists/overlays;
- exported/intent handling;
- migration/interoperability;
- reboot persistence when required/authorized;
- rollback/fallback;
- cleanup of stale previous-product references.

## 7. Sable Reader composition

The intended product is **one Sable Reader identity**.

Capability provenance may come from:

```text
Vaachak Mobile / Readium
    publication/EPUB/library path

Vaachak Text Reader
    TXT/share/process-text/TTS/OCR path
```

Do not select two competing Sable Reader launcher applications merely because both upstream APKs are independently qualified during development.

The final Sable Reader artifact/source composition must have an explicit package identity and feature/network policy before inclusion.

## 8. Reader network/privacy boundary

Network-backed Vaachak features are not accepted automatically.

Vaachak Text Reader currently exposes Internet/model-acquisition behavior for translation. The product policy must distinguish on-device processing from model download/network requirements. Translation may be deferred while TXT/TTS/OCR is accepted.

## 9. Sable Media

Sable Media's Internet permission is justified only by network/radio functionality. Local Music should rely on supported Android user-granted media/document APIs rather than broad storage privilege.

When one APK combines local and network media, tests must prove the network permission does not create unrelated data collection/authority.

## 10. Permission and privilege rules

Do not add system/privileged status, allowlist entries, SELinux exceptions, roles or permissions simply to make an application work more easily.

Every authority maps to an accepted requirement and has a validation/rollback story.

## 11. Product-composition evidence

For every R8 integrated app retain:

```text
freeze identity
module/import source
product selection evidence
PRODUCT_OUT path/hash
installed-files evidence
target-files/image evidence
runtime package/component evidence
role/default evidence if applicable
```

A successful full Android build can coexist with `SABLE_APP_PRODUCT_CLOSURE=FAIL`; report those claims separately.

## 12. Fixtures / optional apps

Maps, Weather and other development/user-installed fixtures do not become product dependencies by appearing in launcher tests.

Record whether an app is:

```text
required product app
qualified candidate
optional/recommended
inherited fallback
development fixture
user-installed
```

## 13. Rollback

Do not remove the prior proven implementation/references until the replacement has passed the appropriate image/runtime/default-role gate and the rollback path is understood.

Historical release/product composition remains immutable evidence after later replacement.
# Default application composition policy

Status: **normative product-integration/default-application policy.**

`vendor_sable` owns common product inclusion/configuration for validated applications. It does not own application implementation source or standalone Cargo/Gradle dependency graphs.

## 1. Explicit application states

```text
SOURCE_CANDIDATE
A1_STANDALONE_QUALIFIED
A2_TRUSTED_ARTIFACT_FROZEN
B1_PRODUCT_INTEGRATED
PRODUCT_OUT_PRESENT
TARGET_FILES_PRESENT
IMAGE_PRESENT
RUNTIME_VALIDATED
DEFAULT_OR_ROLE_HOLDER
REPLACEMENT_ACCEPTED
```

Do not collapse these into one `included` flag.

## 2. R7 baseline

R7 daily-driver qualification records the actual working Phone, Messaging, Contacts, Browser, Camera, Files, Clock, Calculator and other baseline implementations. Inherited/proven apps remain valid fallbacks until replacements pass the applicable gates.

## 3. R8 application train

R8 independently qualifies Calculator + Convert, Games, Reader publication capability, Reader TXT/share/process-text/TTS/OCR capability and Media.

The old R9-first-Calculator sequencing is superseded. A standalone-qualified Sable app still does not become a product default automatically.

## 4. A1 versus A2 input contract

A1 GitHub qualification proves source/application behavior. A2 on `ai-g732` produces the trusted artifact eligible for product integration.

Before common product inclusion bind:

```text
source repository + exact commit
upstream/reuse source + exact commit where applicable
trusted A2 build/toolchain identity
application/package ID
versionCode/versionName
trusted APK SHA-256
permissions/AppOps implications
exported components/intent filters
classes*.dex identity
JNI .so identity
native ABI / 16 KiB compatibility
dependency/license/provenance inventory
accepted feature-policy boundary
known limitations
```

Do not store/integrate an APK whose provenance/rebuildability cannot be stated.

## 5. Common module/product composition

Common imported modules and common app selection belong in `vendor_sable`, conceptually:

```text
vendor/sable/apps/Android.bp
vendor/sable/config/common.mk
```

Panther and Titan 2 products should inherit the same common composition where compatible. Device repositories add only target-specific exceptions and must not duplicate the common app list merely because the hardware differs.

## 6. Android import/module proof

`android_app_import` is the preferred candidate until exact Android 17 / GrapheneOS behavior is observed.

For each A2 artifact prove separately:

```text
trusted APK/input hash
 -> module/import declaration
 -> certificate/signing behavior
 -> JNI/dexpreopt/uses-library processing
 -> selected PRODUCT_PACKAGES/common composition
 -> expected partition/install path
 -> concrete PRODUCT_OUT artifact
```

Later target-files/image/runtime evidence remains separate.

If Soong intentionally transforms or resigns the APK, record whole-file output identity plus stable DEX/JNI inner-content identities instead of falsely requiring byte equality.

## 7. Default/role transition is a separate gate

Installing an app in the image does not make it HOME/Dialer/SMS/Browser or another role holder.

For role/default transitions prove previous/new package/component, role state, privileged grants/allowlists/overlays, intent handling, migration/interoperability, reboot persistence where required/authorized, rollback/fallback and cleanup of stale prior references.

## 8. Sable Reader composition

The intended product is **one Sable Reader identity** composed from separately qualified capability sources where useful:

```text
Vaachak Mobile / Readium
    publication/EPUB/library path

Vaachak Text Reader
    TXT/share/process-text/TTS/OCR path
```

Do not ship two competing Sable Reader launcher apps merely because both upstreams are qualified independently.

Network/model-download behavior remains an explicit product/privacy gate. Translation may be deferred while TXT/TTS/OCR is accepted.

## 9. Sable Media

Media's Internet permission is justified only by network/radio functionality. Local Music should use supported Android user-granted media/document APIs rather than broad storage authority.

## 10. Permission/privilege rule

Do not add privileged/system status, allowlists, SELinux exceptions, roles or permissions simply to make an app work more easily. Every added authority must map to an accepted requirement and have validation/rollback evidence.

## 11. Dual-target rule

Where compatible, Panther and Titan 2 consume the same trusted common R8 app artifacts and common product composition.

A Titan-specific keyboard/layout/device adapter is acceptable. A duplicate common app source fork is not.

## 12. Product-composition evidence

For every integrated R8 app retain:

```text
A2 freeze identity
module/import source
product selection evidence
PRODUCT_OUT path/hash
target-files/image evidence when generated
runtime package/component evidence
role/default evidence if applicable
```

A successful Android build can coexist with `SABLE_APP_PRODUCT_CLOSURE=FAIL`; report claims separately.

## 13. Signing boundary

Development/test signing may be used for engineering images. Production APK/AVB/OTA signing is deferred until Panther and Titan 2 development qualification is satisfactory.

## 14. Rollback

Do not remove a prior proven implementation/reference until the replacement has passed the appropriate image/runtime/default-role gate and rollback is understood. Historical product composition remains immutable evidence.

# Product integration ownership boundary

`vendor_sable` contains Sable-owned product integration that is common across targets.

## Belongs here

- common Sable package inclusion/selection;
- shared product properties and overlays;
- shared product make/Soong integration;
- common import/module definitions for **exact qualified application artifacts** when this is the accepted architecture;
- common Sable SELinux/product wiring when it is genuinely cross-device;
- common feature/profile selection that is not board-specific;
- product-level permission/allowlist/role wiring required by an accepted common application.

## Does not belong here

- application implementation source merely because the app will ship in SableOS;
- Cargo/Gradle dependency graphs that belong to the application build;
- opaque manually built APKs without source/workflow/hash provenance;
- complete device trees;
- board/kernel configuration;
- target-specific VINTF/HAL compatibility;
- proprietary vendor blobs or firmware;
- device-specific SELinux rules that exist only for one hardware target;
- copied application source;
- generated upstream/substrate product files edited to carry Sable semantics.

## Qualified-artifact rule

When the product consumes a standalone-qualified APK, this repository may own the common Android product import/selection **only after** the artifact is frozen and the selected Android 17/GrapheneOS import semantics are proven.

The integration record must retain the connection:

```text
source/upstream identity
 -> qualification workflow/artifact hash
 -> vendor_sable import/module
 -> product selection/install path
 -> target-files/image/runtime evidence
```

`android_app_import` is a candidate implementation mechanism, not an ownership rule by itself.

## Rule of thumb

If a file changes because:

- **the application implementation changed** -> application repository/workspace;
- **the Sable product changed for every target** -> `vendor_sable` or another documented common owner;
- **the shared semantic/design contract changed** -> `platform_sable`;
- **the hardware/substrate target changed** -> first consider `device_sable_<target>`;
- **the exact source/artifact composition changed** -> `platform_manifest` / release provenance;
- **the build/evidence procedure changed** -> `build`.

Product integration must reflect decided architecture; it must not become the place where application ownership is invented.
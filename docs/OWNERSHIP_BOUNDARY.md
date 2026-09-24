# vendor_sable ownership boundary

Status: **current normative boundary — 2026-09-24**

`vendor_sable` owns common product composition and common Android integration
for qualified Sable modules/artifacts.

It does not own:

- common application implementation source;
- device BSP/vendor hardware adaptation;
- build/deployment orchestration;
- source-manifest ownership;
- private raw firmware/evidence.

## Common product ownership

Appropriate responsibilities include:

- common `PRODUCT_PACKAGES` / product-selection definitions;
- common import/module definitions for exact qualified artifacts;
- common permission/product integration;
- shared product overlays/policy that are not device-specific.

## Device exceptions

Panther/Titan/Q27 device differences belong in bounded target adapters.

Do not copy the common application list into every device repository.

## Artifact rule

K1 registry v2 supports multiple release artifact classes, but product
integration still proves the actual module/import/signing/partition behavior of
the selected Android substrate.

Panther R9 proves the mechanism used by that accepted release. A future
Titan-family GSI/system composition must prove its own product/artifact boundary.

## Ownership decision tree

```text
application implementation changed
    -> owning application repo

common Sable product selection/integration changed
    -> vendor_sable

device-only behavior changed
    -> device adapter

build/artifact/deployment mechanism changed
    -> build

exact source/artifact composition changed
    -> platform_manifest / provenance
```

## Security

Do not add privileged/shared-user/system authority merely to simplify product
integration. Privilege remains explicit, narrowly justified and independently
tested.

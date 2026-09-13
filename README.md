# SableOS common product integration

Common SableOS Android product configuration, overlays, permissions integration, and validated default-package composition.

This repository is not a home for copied application source or device-specific forks.

## Ownership boundary

- application repositories own application source;
- `platform_sable` owns common Sable semantic/design contracts;
- `vendor_sable` owns common Sable product inclusion/configuration;
- `device_sable_*` owns bounded target-specific integration;
- `platform_manifest` pins exact source composition.

See [`docs/OWNERSHIP_BOUNDARY.md`](docs/OWNERSHIP_BOUNDARY.md).

## R6 operational composition

The first operational common product fragment is [`config/common.mk`](config/common.mk).

For R6 it intentionally selects only the common Sable launcher module:

```make
PRODUCT_PACKAGES += \
    SableStart
```

A target-specific Sable product adapter inherits this fragment after its upstream/substrate product. The common fragment must not encode Panther-specific build IDs, device properties, generated-vendor paths, or hardware policy.

Canonical Android checkout path for this repository is intended to be:

```text
vendor/sable
```

R6 product integration does not pull the broader R7 default-application decisions forward.

## Default applications

The daily-driver plan intentionally does not require every user-facing application to be Sable-owned.

Normative product-selection policy:

- [`docs/DEFAULT_APPLICATION_COMPOSITION.md`](docs/DEFAULT_APPLICATION_COMPOSITION.md)

R7 must explicitly record the actual Phone, Messaging, Contacts, Browser, Camera, Files, Clock, and Calculator implementations instead of assuming a blanket "AOSP" or "Graphene" app policy.

Complex interoperability apps should initially use a proven implementation. Sable Calculator is the first planned native utility replacement after the shared R8 design/theme foundation.

Maps/Weather used during development are test fixtures unless a separate product decision makes them defaults.
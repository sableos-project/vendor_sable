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

## Default applications

The daily-driver plan intentionally does not require every user-facing application to be Sable-owned.

Normative product-selection policy:

- [`docs/DEFAULT_APPLICATION_COMPOSITION.md`](docs/DEFAULT_APPLICATION_COMPOSITION.md)

R7 must explicitly record the actual Phone, Messaging, Contacts, Browser, Camera, Files, Clock, and Calculator implementations instead of assuming a blanket "AOSP" or "Graphene" app policy.

Complex interoperability apps should initially use a proven implementation. Sable Calculator is the first planned native utility replacement after the shared R8 design/theme foundation.

Maps/Weather used during development are test fixtures unless a separate product decision makes them defaults.
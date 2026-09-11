# Sable vendor integration

Common Android product integration for SableOS.

This repository is for Sable-owned configuration that belongs in the Android product layer but is shared across devices where practical. It must not become a catch-all for device trees or proprietary vendor payloads.

Typical responsibilities may include common product definitions, package inclusion, shared overlays, common SELinux/product integration, and other Sable product wiring.

Device-specific board configuration, hardware compatibility work, and vendor/BSP assumptions belong in the corresponding `device_sable_<target>` repository or explicitly versioned external inputs.

See `docs/OWNERSHIP_BOUNDARY.md`.

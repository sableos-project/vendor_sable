# Product integration ownership boundary

`vendor_sable` contains Sable-owned product integration that is common across targets.

## Belongs here

- common Sable package inclusion;
- shared product properties and overlays;
- shared product make/Soong integration;
- common Sable SELinux/product wiring when it is genuinely cross-device;
- common feature/profile selection that is not board-specific.

## Does not belong here

- complete device trees;
- board/kernel configuration;
- target-specific VINTF/HAL compatibility;
- proprietary vendor blobs or firmware;
- device-specific SELinux rules that exist only for one hardware target;
- copied application source.

## Rule of thumb

If a file must change because the hardware target changed, first consider `device_sable_<target>`. If it must change because the Sable product changed for every device, it likely belongs here or in a common application/platform repository.

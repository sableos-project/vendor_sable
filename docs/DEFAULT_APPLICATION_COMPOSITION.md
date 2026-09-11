# Default application composition policy

Status: **normative product-integration policy; exact package selections remain subject to R7 inventory/validation.**

`vendor_sable` owns common SableOS product integration. It may select/include validated application packages as product defaults, overlays, permissions, and common product configuration require. It does **not** own the application source itself.

This document prevents default-app decisions from becoming hidden product makefile choices with no recorded rationale.

## 1. Ownership boundary

Use this separation:

```text
application repository
  -> owns application source and app-specific requirements

platform_sable
  -> owns common Sable semantic/design/platform contracts

vendor_sable
  -> owns common Sable product composition/integration

platform_manifest
  -> pins exact source repositories/revisions

device_sable_*
  -> owns bounded device-specific integration only
```

Do not copy Phone/Messaging/Calculator/etc. source trees into `vendor_sable`.

Do not duplicate a common default-app choice in every device repository unless the choice is genuinely device-specific and documented.

## 2. Daily-driver first policy

The initial SableOS product should prioritize a dependable working phone over replacing mature applications for branding.

For the R7 daily-driver baseline, product composition must provide working implementations for:

- Phone/Dialer;
- Messaging with SMS/MMS;
- Contacts sufficient for phone/message workflows;
- Browser;
- Camera;
- photo/gallery/media viewing as needed;
- Files/documents UI;
- Clock/alarm;
- Calculator;
- Settings/platform connectivity UI;
- Sable Start.

An inherited implementation is acceptable where the default-app policy has not yet approved a Sable replacement.

## 3. Component selection record

Before a package is treated as a SableOS shipping/default application, record:

- capability name;
- package name;
- important activity/service/provider components;
- source/provenance;
- exact upstream revision when source-built;
- license/redistribution status;
- branding/trademark implications;
- whether it is privileged/system/role holder;
- permissions/allowlists required by product configuration;
- dependencies on Android/AOSP/Graphene-specific or external services;
- update/security maintenance owner;
- device compatibility requirements;
- whether selection is `temporary`, `preferred`, `required`, or `replacement planned`;
- runtime qualification evidence reference.

The product should be able to answer "why is this package in the image?" from GitHub documentation.

## 4. Initial class policy

### Platform/security-critical functions

Examples: telephony framework, networking, permissions, Settings plumbing.

Direction: keep validated substrate/platform mechanisms. `vendor_sable` may integrate/configure them but must not replace them with app-level hacks.

### Complex interoperability apps

Examples: Phone, Messaging, Browser, Camera.

Direction: select a proven implementation first. A Sable replacement is a later explicit decision.

### Simple utilities

Examples: Calculator, Notes.

Direction: suitable for later Sable-owned replacement after requirements and shared design contracts exist. Calculator is first planned Sable utility.

### Provider/content apps

Examples: Weather, Maps.

Direction: do not make a current test fixture a required product dependency by accident. Provider/default status requires a separate choice.

## 5. AOSP versus GrapheneOS-derived versus other implementations

There is no blanket rule that every default must come from one upstream.

Evaluate each application on:

- source/license availability;
- active security maintenance;
- Android-version compatibility;
- integration dependencies;
- privileged permission requirements;
- branding/trademark constraints;
- portability to future Sable targets;
- user experience and accessibility;
- ability to update independently or with the OS;
- data migration/interop.

Do not select an app solely because it happens to be present in the current reference workspace.

Do not reject a proven inherited app solely because it is not Sable-branded.

## 6. Role/default-handler configuration

If SableOS sets a default role/handler through product configuration, document it explicitly.

Examples include:

- HOME/launcher;
- Phone/Dialer;
- SMS;
- Browser.

Default-role changes are product behavior, not an incidental build detail.

During development/validation, a component may intentionally be installed without taking the role (for example Sable Start preview/runtime testing while Quickstep remains HOME). Do not conflate installed capability with selected default role.

## 7. Privileged permissions and allowlists

Any privileged permission/allowlist associated with a default app must be justified by an actual supported application requirement.

Rules:

- no broad allowlist "just in case";
- keep allowlists close to the product/app decision and reviewable;
- document whether the permission is inherited from the upstream app model or Sable-specific;
- remove obsolete product grants when the owning package is removed/replaced, through a separately validated cleanup change;
- do not grant privilege merely to avoid using supported Android APIs.

## 8. Optional/test applications

Development fixtures such as currently installed Maps/Weather may be useful for R6 launcher inventory tests but are not thereby required defaults.

Product composition documentation should distinguish:

```text
required product app
optional recommended app
development/test fixture
user-installed app
```

Do not bake a test fixture into the shipping image without a product decision.

## 9. Sable Calculator transition

R7 may use an inherited calculator for daily-driver readiness.

When R9 Sable Calculator is validated and integrated:

1. add its repository/revision to the exact source composition;
2. include its build module in the common product where intended;
3. validate package/permission/signing/update behavior;
4. remove/disable the previous default calculator only if product requirements call for replacement;
5. prove no stale overlays/allowlists/package references remain;
6. preserve rollback capability until the new app is qualified.

Do not remove the working baseline calculator before Sable Calculator passes its own build/runtime gate.

## 10. Theme/customization boundary

R8 Sable application theme/customization state belongs in common Sable product/application contracts, not as vendor-specific literal UI values.

`vendor_sable` may define platform/product resource overlays when that is the correct Android integration point, but it should not become the canonical source for Sable app design tokens.

## 11. Device portability

A common default application belongs in `vendor_sable` product composition when it is intended across Sable devices.

Only move selection/integration to `device_sable_*` when the difference is genuinely target-specific, such as a hardware-specific camera implementation that cannot be common.

Even then, common user-facing semantics should remain in shared documentation.

## 12. Removal/replacement cleanup checklist

Whenever replacing a default app, audit at least:

- product package lists;
- overlays;
- permissions/privapp allowlists;
- roles/default handlers;
- intent filters/associations;
- SELinux rules if any;
- framework config references;
- manifest/source composition;
- update/signing expectations;
- tests/evidence scripts;
- old package data/migration behavior.

Do not delete historical evidence merely because the app changed.

## 13. R7 output expected from product composition

R7 should leave behind a documented table similar to:

| Capability | Package | Provenance | Product status | Replacement horizon |
| --- | --- | --- | --- | --- |
| Sable Start | `org.sableos.start` | Sable | required/common | active |
| Phone | TBD after inventory | TBD | R7 required | inherited initially |
| Messaging | TBD | TBD | R7 required | inherited initially |
| Contacts | TBD | TBD | R7 required | evaluate |
| Browser | TBD | TBD | R7 required | inherited initially |
| Camera | TBD | TBD | R7 required | inherited initially |
| Files | TBD | TBD | R7 required | later Sable candidate |
| Clock | TBD | TBD | R7 required | later Sable candidate |
| Calculator | TBD for R7 | TBD | R7 required | Sable replacement planned R9 |
| Weather | no required default yet | provider/user choice | optional/test | future decision |
| Maps | no required default yet | provider/user choice | optional/test | future decision |

`TBD` is preferable to an undocumented assumption.

## 14. Definition of policy compliance

A product composition change complies with this policy when:

- application source remains in the owning repository;
- the product choice and rationale are documented;
- exact source composition can pin the selected implementation;
- privilege/role implications are explicit;
- runtime qualification exists for baseline daily-driver apps;
- a test/development fixture is not silently promoted to required default;
- device-specific forks are avoided unless technically justified;
- future maintainers can determine the selected implementation and replacement plan without relying on chat history.
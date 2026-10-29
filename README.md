# OnePlus9-LE2117-Research

Evidence, tools, and investigation notes for OnePlus 9 LE2117 bootloader, EDL, MSM, and GPT behavior.

## Objective

Establish a verified unlocked bootloader and normal Android boot on the OnePlus 9 LE2117. Rooting, custom ROMs, kernels and relocking are outside the current phase.

## Current Status

Research is ongoing. A successful conversion or bootloader unlock has not been demonstrated.

The latest recorded Android check, on October 29, 2026, showed LE2117 Android 14, slot B, a locked bootloader, verified boot green and completed normal boot. A subsequent read-only acquisition captured eight firmware images totaling 33 MiB. Both ABL copies match their saved references, and the current XBL contains the Device Info provider previously missing from the analysis. Supplemental PARAM and raw Device Info reads match their saved originals; the acquired boot log is unchanged historical evidence.

New offline work includes ten original-crypto/getter cases and five startup-record-loop cases. Earlier studies cover 22 ABL identity/permission cases, eighteen host storage/stage cases and 25 lifecycle cases. These groups overlap questions and have different modeled boundaries; they are not independent end-to-end validations. The narrower guarded identity-override candidate remains under investigation. No flashing or unlock command was issued during the new acquisition. Complete protected-state acceptance, initialization, unlocking, downgrade compatibility and recovery remain unproven.

- [Findings](Docs/Findings.md): observations, confidence and limitations.
- [Roadmap](Docs/Roadmap.md): outstanding work and completion criteria.
- [Unlock-gate study](Docs/Unlock-Gate-Study.md): narrower candidate and its unresolved dependencies.
- [Storage simulation](Docs/Storage-Simulation.md): transaction order, failure cases and verification limits.
- [Device Info and PARAM lifecycle](Docs/DeviceInfo-PARAM-Lifecycle.md): stateful continuation, cache divergence, restoration and return-status limits.
- [Current firmware provider](Docs/Current-Firmware-Provider.md): verified acquisition, provider registration, storage paths and historical-log limits.
- [Original crypto and startup checks](Docs/Original-Crypto-and-Startup.md): real MD5/AES execution, startup reconciliation and setter side effects.
- [Toolchain provenance](Docs/Toolchain-Provenance.md): selected master PARAM module, import verification and capture-source distinctions.
- [Research Standards](Docs/Research-Standards.md): evidence handling and reporting rules.
- [Evidence Index](Docs/Evidence-Index.json): hashes and references to the underlying offline records.

This repository starts with reviewed documentation and an issue tracker. Raw device backups, authentication material, memory captures and vendor firmware remain outside Git. Analysis scripts require a portability and disclosure review before being added here.

## Scope of the Results

Findings apply to the recorded device, software and package versions. Read access, authentication responses, valid checksums and emulator results are separate milestones. None is sufficient evidence of a completed conversion or unlock.

This is not a flashing guide. The unchanged package and the loader's `fixgpt` command are not validated remedies for the identified LUN1 discrepancy.

## Referenced Tools

The investigation uses OnePlus MSM servicing software and [bkerler/edl](https://github.com/bkerler/edl). Third-party code retains its original authorship and license. Package-specific and proprietary-loader findings are tracked separately from EDL source contributions.

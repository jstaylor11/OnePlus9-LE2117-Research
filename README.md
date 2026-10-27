# OnePlus9-LE2117-Research

Evidence, tools, and investigation notes for OnePlus 9 LE2117 bootloader, EDL, MSM, and GPT behavior.

## Objective

Establish a verified unlocked bootloader and normal Android boot on the OnePlus 9 LE2117. Rooting, custom ROMs, kernels and relocking are outside the current phase.

## Current Status

Research is ongoing. A successful conversion or bootloader unlock has not been demonstrated.

The latest recorded device check, on October 26, 2026, showed normal Android 14 boot with a locked bootloader. Subsequent offline work includes GPT reconstruction, authentication checks, 22 bounded ABL identity/permission cases and 18 host storage/stage cases. A narrower guarded identity-override candidate is under investigation. These results do not establish a usable unlock sequence, successful hardware writes, downgrade compatibility or recovery.

- [Findings](Docs/Findings.md): observations, confidence and limitations.
- [Roadmap](Docs/Roadmap.md): outstanding work and completion criteria.
- [Unlock-gate study](Docs/Unlock-Gate-Study.md): narrower candidate and its unresolved dependencies.
- [Storage simulation](Docs/Storage-Simulation.md): transaction order, failure cases and verification limits.
- [Research Standards](Docs/Research-Standards.md): evidence handling and reporting rules.
- [Evidence Index](Docs/Evidence-Index.json): hashes and references to the underlying offline records.

This repository starts with reviewed documentation and an issue tracker. Raw device backups, authentication material, memory captures and vendor firmware remain outside Git. Analysis scripts require a portability and disclosure review before being added here.

## Scope of the Results

Findings apply to the recorded device, software and package versions. Read access, authentication responses, valid checksums and emulator results are separate milestones. None is sufficient evidence of a completed conversion or unlock.

This is not a flashing guide. The unchanged package and the loader's `fixgpt` command are not validated remedies for the identified LUN1 discrepancy.

## Referenced Tools

The investigation uses OnePlus MSM servicing software and [bkerler/edl](https://github.com/bkerler/edl). Third-party code retains its original authorship and license. Package-specific and proprietary-loader findings are tracked separately from EDL source contributions.

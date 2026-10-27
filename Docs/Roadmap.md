# Roadmap

## Current Priority

Investigate the narrower guarded identity-override candidate before committing to full conversion. First resolve the verified-boot Device Info backend/cache lifecycle and restoration of the relevant PARAM fields, then join the original-code models against stateful synthetic storage. The token-acquisition route is excluded from scope. No device-write procedure is validated.

The full conversion/GPT work remains a fallback and stays on hold. The existing evidence does not support blind XML replay or another unchanged-package MSM attempt.

Current sequence:

1. [Device Info persistence and identity override](https://github.com/jstaylor11/OnePlus9-LE2117-Research/issues/5).
2. [PARAM acceptance and restoration](https://github.com/jstaylor11/OnePlus9-LE2117-Research/issues/6).
3. [Connected stateful simulation](https://github.com/jstaylor11/OnePlus9-LE2117-Research/issues/7), using results from both lifecycle studies.

[Issue 1](https://github.com/jstaylor11/OnePlus9-LE2117-Research/issues/1) retains the remaining MSM runtime/storage questions. [Issue 2](https://github.com/jstaylor11/OnePlus9-LE2117-Research/issues/2) retains the full conversion/GPT sequence. Neither is closed by the new bounded models.

| Work Item | Current Evidence | Completion Criterion |
| --- | --- | --- |
| Device Info identity override | Original gate/table branches and guarded handler identified | Resolve authorization, backend acceptance, persistent/cache state and boot-time reload |
| PARAM authorization fields | Both setting maps decoded; archived relevant fields are 0/0 | Resolve acceptance, initialization/restoration and affected primary/backup copies |
| Connected simulation | 22 ABL cases and 18 separate host storage/stage cases pass | Join original routines through stateful services and explicit fault controls without assuming omitted helpers |
| Worker mode and flag lifecycle | Pre-device vectors and special userdata command traced | Account for later flags and lower-driver erase semantics |
| PARAM postprocessing | Separate commits, partial transactions and marker-only checking corroborated | Resolve omitted helpers and define independent verification/failure handling |
| GPT and slot consistency | LUN1 reconstruction passes offline | Integrate all six LUNs, package patches, slot attributes and bootable UFS LUN selection |
| Sparse transfer behavior | Six source ranges pass structural checks | Account for raw, fill and DONT_CARE effects in the complete sequence |
| Delivery and recovery | Synthetic token compatibility passes | Review the exact session configuration, write/readback sequence and failure response |
| Final device verification | Not reached | Observe unlocked bootloader state and normal Android boot |

## Deferred Contributions

After the phone objective is accomplished:

- Review device-scoped PARAM derivation and input-validation candidates against current upstream code.
- Evaluate output/error handling separately from the previously submitted decryption guard.
- Prepare a reproducible, narrowly scoped report for the loader repair-loop candidate.
- Prepare portable offline tools with synthetic fixtures and clear dependency/input documentation.
- Review documentation and artifacts before any public release.

Keep package, proprietary-loader and EDL-source findings separate. Preserve third-party attribution and distinguish observed results from hypotheses.

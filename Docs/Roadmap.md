# Roadmap

## Current Priority

Investigate the narrower guarded identity-override candidate before committing to full conversion. A first connected stateful continuation now covers selected cache, restoration and host/ABL interactions. Next identify the matching verified-boot provider, replace symbolic integrity/codec behavior with validated format/crypto behavior, and trace complete initialization and later writer/unlock ordering. The token-acquisition route is excluded from scope. No device-write procedure is validated.

The full conversion/GPT work remains a fallback and stays on hold. The existing evidence does not support blind XML replay or another unchanged-package MSM attempt.

Current sequence:

1. [Device Info persistence and identity override](https://github.com/jstaylor11/OnePlus9-LE2117-Research/issues/5).
2. [PARAM acceptance and restoration](https://github.com/jstaylor11/OnePlus9-LE2117-Research/issues/6).
3. [Connected stateful simulation](https://github.com/jstaylor11/OnePlus9-LE2117-Research/issues/7), extending the first three connected sequences as both lifecycle studies resolve their remaining modeled boundaries.

The [25-case lifecycle continuation](DeviceInfo-PARAM-Lifecycle.md) advances all three studies without closing them. Its case count is separate from the earlier 22 ABL and 18 host cases; it is not a claim of independent end-to-end validation.

[Issue 1](https://github.com/jstaylor11/OnePlus9-LE2117-Research/issues/1) retains the remaining MSM runtime/storage questions. [Issue 2](https://github.com/jstaylor11/OnePlus9-LE2117-Research/issues/2) retains the full conversion/GPT sequence. Neither is closed by the new bounded models.

| Work Item | Current Evidence | Completion Criterion |
| --- | --- | --- |
| Device Info identity override | Separate staging/cache paths and 14 new bounded cache/provider cases; stale-write and response hazards identified | Resolve actual provider acceptance/atomicity and complete boot/writer ordering |
| PARAM authorization fields | Both setting maps decoded; archived fields are 0/0; eight new restoration cases expose older-backup recovery and return-status hazards | Replace symbolic integrity/codec behavior and resolve complete initialization/restoration and affected copies |
| Connected simulation | Three new shared-state host/ABL sequences, alongside the earlier separate models | Extend through resolved original interfaces; retain explicit fault controls and fail on unmodeled targets |
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

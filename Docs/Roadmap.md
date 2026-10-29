# Roadmap

## Current Priority

Investigate the narrower guarded identity-override candidate before committing to full conversion. The current provider is now captured and identified. Original version-1 integrity/AES paths and the first startup record loop have been exercised offline. Next resolve the provider's protected-state contract, version/cust-flag migration, later restoration/writers and complete unlock-state ordering. The token-acquisition route is excluded from scope. No persistent-write procedure is validated.

The full conversion/GPT work remains a fallback and stays on hold. The existing evidence does not support blind XML replay or another unchanged-package MSM attempt.

Current sequence:

1. [Device Info persistence and identity override](https://github.com/jstaylor11/OnePlus9-LE2117-Research/issues/5).
2. [PARAM acceptance and restoration](https://github.com/jstaylor11/OnePlus9-LE2117-Research/issues/6).
3. [Connected stateful simulation](https://github.com/jstaylor11/OnePlus9-LE2117-Research/issues/7), incorporating the captured provider and resolved original-code interfaces while keeping secure-world and storage responses explicit.

The [25-case lifecycle continuation](DeviceInfo-PARAM-Lifecycle.md), [current-provider capture](Current-Firmware-Provider.md), and [ten crypto plus five startup cases](Original-Crypto-and-Startup.md) advance these studies without closing them. Counts remain separate from the earlier 22 ABL and eighteen host cases; none is a count of independent end-to-end unlock validations.

[Issue 1](https://github.com/jstaylor11/OnePlus9-LE2117-Research/issues/1) retains the remaining MSM runtime/storage questions. [Issue 2](https://github.com/jstaylor11/OnePlus9-LE2117-Research/issues/2) retains the full conversion/GPT sequence. Neither is closed by the new bounded models.

| Work Item | Current Evidence | Completion Criterion |
| --- | --- | --- |
| Device Info identity override | Current VerifiedBootDxe identified; partition and secure-service branches traced; historical logs report both paths | Resolve current protected-state selection/acceptance/atomicity and complete boot/writer ordering |
| PARAM authorization fields | Fresh saved-state comparison remains unchanged; original cv1 crypto and first startup reconciliation loop execute | Resolve migration/later protected-state behavior and review every setter/counter/copy effect |
| Connected simulation | Earlier three shared-state sequences plus original crypto and bounded startup studies; complete pipeline remains unexecuted | Connect the actual provider and full initialization; retain explicit fault controls and fail on unmodeled targets |
| EDL source provenance | Master PARAM substitution, actual imports/bound class and three focused tests verified | Use the verified runtime for later device operations and preserve each acquisition's actual source identity |
| Worker mode and flag lifecycle | Pre-device vectors and special userdata command traced | Account for later flags and lower-driver erase semantics |
| PARAM postprocessing | Separate commits, partial transactions and marker-only checking corroborated | Resolve omitted helpers and define independent verification/failure handling |
| GPT and slot consistency | LUN1 reconstruction passes offline | Integrate all six LUNs, package patches, slot attributes and bootable UFS LUN selection |
| Sparse transfer behavior | Six source ranges pass structural checks | Account for raw, fill and DONT_CARE effects in the complete sequence |
| Delivery and recovery | Synthetic token compatibility and targeted current firmware reads pass; complete recovery remains unproven | Review any proposed write/readback sequence and failure response; establish exact recovery limits |
| Final device verification | Not reached | Observe unlocked bootloader state and normal Android boot |

## Deferred Contributions

After the phone objective is accomplished:

- Review device-scoped PARAM derivation and input-validation candidates against current upstream code.
- Evaluate output/error handling separately from the previously submitted decryption guard.
- Prepare a reproducible, narrowly scoped report for the loader repair-loop candidate.
- Prepare portable offline tools with synthetic fixtures and clear dependency/input documentation.
- Review documentation and artifacts before any public release.

Keep package, proprietary-loader and EDL-source findings separate. Preserve third-party attribution and distinguish observed results from hypotheses.

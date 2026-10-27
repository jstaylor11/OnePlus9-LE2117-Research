# Roadmap

## Current Priority

Prepare one concrete conversion procedure with explicit storage effects, verification and failure handling. The existing evidence does not support blind XML replay or another unchanged-package MSM attempt.

| Work Item | Current Evidence | Completion Criterion |
| --- | --- | --- |
| Worker mode and flag lifecycle | Pre-device vectors decoded; erase precheck traced | Account for changes after device initialization and the userdata erase extent |
| PARAM postprocessing | Staged handler recovered; separate region dispatch identified | Map relevant field changes and read/write behavior for the selected mode |
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

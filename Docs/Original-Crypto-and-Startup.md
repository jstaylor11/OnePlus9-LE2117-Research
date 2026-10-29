# Original Crypto and Startup Checks

Evidence date: October 29, 2026. Offline emulation with private saved inputs and RAM-only test records. No phone interface, flashing command or modified partition-image file was used in these studies.

## Result and Scope

Ten cases now execute the saved ABL's original ciphertext MD5 and version-1 AES code through selected getter, restoration and permission paths. Five further cases execute the first PARAM startup verification/reconciliation loop. Both groups pass their stated checks.

These groups overlap earlier research questions. They are separate from the earlier 22 ABL, eighteen host and 25 lifecycle cases, and are not independent end-to-end unlock validations. The new cases replace particular models; they do not remove every modeled interface from the earlier studies.

**High confidence, approximately 99%,** in input identity and recorded results. **Moderate confidence, approximately 95%,** in original-code behavior under the declared interfaces. No overall unlock probability is assigned.

The saved ABL PE SHA-256 is `85640ddc9c3cefbf2e7785467a1857a606128a6e87726dae2e250f267e081b8e`. Its full slot-B partition matches the new device capture. Firmware extraction was inspected, but vendor signatures and the entire boot chain were not independently certified.

## Ten Integrity, AES and Getter Cases

The emulator executes the original ciphertext-integrity routine, MD5 implementation, version-1 AES-CBC codec, selected getter/restoration routines and permission predicates. Independent encrypted fixtures were generated with the existing PyCryptodome 3.24.0 installation.

| Case | Recorded result |
| --- | --- |
| Saved reference | Original-code field results and complete decrypted-record digest match the independent oracle |
| Baseline synthetic record | Original MD5/AES output matches the independent fixture |
| Candidate synthetic record | Original MD5/AES output matches the independent fixture |
| Baseline permission predicates | Tested permissions denied through original crypto |
| Candidate permission predicates | Tested permissions allowed through original crypto |
| Valid newer primary, older backup | Selected getter uses the primary without reconciling the backup |
| Failed primary ciphertext integrity | Older valid backup restored through modeled storage |
| Both ciphertext checks fail | Getter rejects without supplying field output |
| Invalid embedded plaintext digest, valid ciphertext digest | Selected getter still supplies the tested field; further initialization checks are not excluded |
| Four injected readback mismatches | Restoration can return zero while cached output and modeled persistent contents differ |

The last case corroborates the previously identified status-propagation concern with actual crypto instructions. Storage writes/readback remain modeled. It does not demonstrate physical storage failure or an exploitable hardware defect.

Initial PARAM preload, allocation/copy/logging/unsafe-stack services and storage interfaces remain declared models in this group. The complete Device Info provider, version-2 derivation, full startup, protected-state lifecycle, unlock confirmation/wipe and Android boot are excluded. This also does not validate the original x86 host transaction with real crypto.

## Five Startup-Loop Cases

The second group starts at original initializer PE RVA `0x18940`. The code selects its platform-table buffer, clears it, obtains one MiB through modeled block services, and runs the first five-record verification/reconciliation loop. Original encrypted-header, ciphertext MD5 and update-counter decisions execute.

Execution stops at PE RVA `0x19328`, before version/cust-flag migration and the later software-project-ID/protected-state processing. This boundary is deliberate: reaching it is not successful completion of initialization.

| Initial state | State at the checkpoint | Modeled storage writes |
| --- | --- | ---: |
| Matching original records | Original copies retained | 0 |
| Both copies contain the candidate | Candidate copies retained | 0 |
| Newer valid candidate primary, older original backup | Candidate synchronized to both | 2 |
| Original primary, newer valid candidate backup | Candidate synchronized to both | 2 |
| Candidate primary fails integrity, original backup valid | Older original restored to both | 2 |

This qualifies the getter-only result: the getter can use a valid primary without backup reconciliation, while this startup loop separately compares both copies and their update counters.

The candidate is generated in RAM using the exact PARAM setter bytes from [jstaylor11/edl master commit 9f796eb](https://github.com/jstaylor11/edl/commit/9f796ebc2c2348c725f845b4fe76b6769d0f2d82). Its supporting Windows crypto environment is separate from the Linux device runtime. Only a test record passes through a private parent-process pipe; no modified full-phone image is produced.

Declared interfaces include block lookup/read, allocation/copy/logging/unsafe-stack helpers and RAM-only storage writes/readback. A synthetic serial input is unused for crypto before the checkpoint. The platform input and mapped RAM are models; board hardware is not accessed.

## Setter Effects Beyond the Requested Fields

Two setter calls advance the primary record's update counter by two and produce a record with recovery counter zero. The saved input's nonzero recovery counter is therefore not preserved. The backup is left unchanged by those calls, and bytes outside the primary record remain unchanged.

This is more than a two-field semantic change. It must be included in any future complete-diff and recovery review. The behavior is not attributed to the new failure-handling guard or classified here as an established defect.

In the startup controls, synchronizing the newer candidate increments its recovery counter. Restoring an older valid backup after integrity failure also increments that backup's recovery counter. These are consequences observed in synthetic storage, not writes made to the phone.

## Development Record and Reproducibility

The extended crypto harness initially inherited another module's output-directory variable, omitted a diagnostic formatter reached on failed integrity, and assumed complete record equality after retry exhaustion. Those assumptions were corrected against executed instructions. Primary retry exhaustion leaves a counter difference even when restored ciphertext matches. Failed expectations and source revisions remain in the private evidence; they are not phone failures.

The startup study consulted the retained full-function exports for navigation and checked selected instructions against the hashed PE. Its five final cases passed. Execution fails on undeclared targets. Inputs, source hashes, case journals, declared models and development records are referenced in [Evidence Index](Evidence-Index.json). Those private references provide provenance, not public independent reproducibility; portable models and suitable input acquisition still require review.

## Next Boundary

Execute and assess version/cust-flag migration, later protected-state restoration, later writers and complete initialization. Then connect the actual Device Info service to the complete unlock path. The current [provider capture](Current-Firmware-Provider.md) removes the missing-module gap but does not supply real secure-world responses to these tests.

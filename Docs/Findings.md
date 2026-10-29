# Findings

Evidence cutoff: October 29, 2026, America/Denver. Fresh Android observations and targeted read-only captures are distinguished below from offline static analysis and emulation. Confidence percentages are judgment estimates about the stated evidence, not measured probabilities of successful flashing or unlocking.

## Current Firmware and Provider

**High confidence, approximately 99%, in acquisition checks and byte comparisons; moderate confidence, approximately 95%, in conditional static interpretation.** Fresh Android readings showed LE2117 Android 14, slot B, locked state, verified boot green and completed normal boot. Eight targeted firmware reads completed with expected lengths and transfer-log checks. Both ABL copies match their saved references. The directly captured XBL contains the exact Device Info protocol in VerifiedBootDxe, interface revision `0x10003`.

The provider reaches security-dependent `devinfo` partition and secure `keymaster` service paths; its diagnostics label the latter RPMB. The actual security word and secure-world acceptance were not queried. A current raw partition copy is not assumed equivalent to the protected service. The first acquisition failed after EDL disappeared before client launch; staging before transition corrected the observed sequencing problem.

Supplemental PARAM and raw `devinfo` match saved originals; inspected authorization fields remain zero. The acquired boot log is identical to its September 26 copy. Its reports of both backend paths are historical and do not identify the latest boot's selection. See [Current Firmware Provider](Current-Firmware-Provider.md).

## Original Crypto and Startup Reconciliation

**Moderate confidence, approximately 95%, within the stated models; high confidence, approximately 99%, in recorded input identity and checks.** Ten new cases replace symbolic ciphertext integrity and the synthetic codec with original version-1 MD5/AES instructions in selected paths. Five startup cases execute the original first record-checking loop with modeled block/storage services, stopping before migration and later protected-state processing.

Matching candidate copies survive that checkpoint; newer valid update counters cause synchronization, and failed primary integrity can restore the older backup. The master setter used in the RAM fixture updates only the primary record, advances its update counter and resets its recovery counter. Those effects require a complete-diff review before a physical experiment. The selected getter also does not check the embedded plaintext digest in the tested path; full initialization may impose additional checks.

See [Original Crypto and Startup Checks](Original-Crypto-and-Startup.md). These results qualify earlier getter-only behavior without demonstrating complete initialization or hardware acceptance.

## EDL Runtime Selection

**High confidence, approximately 99%, in the source/import audit and focused tests.** The accepted runtime substitutes only the PARAM module from the research fork's master commit `9f796eb` into an isolated copy of the existing base. Actual imports and the OnePlus transport's bound class select that file; all three committed focused tests pass offline.

The completed captures used the older installation before this verification. Core read-transport files match the selected master, but the capture provenance remains unchanged. The selected guard does not implement the separate version-2 derivation research or unlocking. See [Toolchain Provenance](Toolchain-Provenance.md).

## Narrower Unlock Candidate

**High confidence, approximately 99%, for saved bytes; moderate confidence, approximately 95%, for conditional interpretation and bounded emulation.** Twenty-two ABL cases corroborate the saved T-Mobile/Global carrier-gate difference and separate internal/OEM permission predicates. A guarded Device Info identity override connects to net/BT settings also present in MSM's PARAM processing. Actual acceptance, restoration, persistence and complete unlocking remain unverified.

See [Offline Unlock-Gate Study](Unlock-Gate-Study.md). This does not support an ABL-only flash, a direct PARAM trigger or a device procedure.

## Device Info and PARAM Lifecycle Continuation (October 27)

**Moderate confidence, approximately 95%, within the documented models; high confidence, approximately 99%, in verified input bytes and recorded checks.** This earlier study's 25 bounded cases cover 14 Device Info/cache cases, eight PARAM restoration cases and three connected host/ABL sequences. The original handler and selected restoration/cache routines execute with shared synthetic services. In that study, provider acceptance, record integrity, the codec bridge, initial PARAM preload and other runtime/storage interfaces remain modeled. The October 29 results above resolve selected boundaries in separate cases.

Staging and cached identity can diverge. In a modeled ordering, a later write of the whole cached structure overwrites a newer staged persistent value. Rejected writes can be obscured by the response path or a retry that sees already-mutated RAM and skips storage. A rejected primary PARAM record can restore older backup values; a valid primary is not reconciled with a divergent backup in the traced getter path.

A candidate error-propagation defect also appears in the saved PARAM restoration routine: after four successful primary-write returns and four failed modeled full-record readback checks, it can return the last write's zero status and let the getter continue with stale cached state. Practical reachability, hardware impact and novelty remain unestablished. This is separate from the MSM final-marker limitation below.

See [Device Info and PARAM Lifecycle](DeviceInfo-PARAM-Lifecycle.md). These cases do not complete issues 5, 6 or 7 and do not establish a hardware unlock route.

## PARAM Transaction and Final Verification

**Moderate confidence, approximately 95%, within the modeled interfaces.** Eighteen host storage/stage cases corroborate primary-then-backup writes, partial completion on failures, and a final marker check that can pass despite another returned-byte mismatch. The models execute selected original instructions with explicit mocks and synthetic storage. They are separate bounded models, not a complete MSM session.

See [Bounded Storage Simulation](Storage-Simulation.md). Disabled ordinary PARAM programming does not preserve PARAM against the separate staged paths. Independent verification and failure handling remain necessary research requirements.

## Native Windows Readback

**High confidence, approximately 99%.** Native MSM reported PARAM ReadBack Complete in six seconds. The 8 MiB output matched the saved reference hash. A subsequent recorded Android check showed the original Android 14 build, slot B, locked state and verified boot green.

This establishes readback for that session. It does not establish firmware-write acceptance or the current live phone state.

Offline reference: `NATIVE-MSM-READBACK-SUCCESS.md`.

## LUN1 Package Discrepancy

**High confidence, approximately 99%, for file and captured-structure comparisons; moderate confidence, approximately 95%, for the conditional write-path interpretation.**

The reviewed conversion and recovery packages contain LUN1 backup-GPT payloads duplicating LUN0 data. Their patch records do not provide the missing LUN1 correction. The saved MSM runtime vectors select the original payload and contain no LUN1 patch. The observed GPT-skip flag is off.

The ordinary writer reads embedded OPS data. Its external-image path still selects embedded GPT data under the traced conditions. These are startup captures and code observations, not a recording of malformed data being flashed to the phone. Protected code and later state changes limit the conclusion.

Offline references: `MSM-GPT-REVIEW.md`, `GPT-TIMED-INVESTIGATION.md`, `runtime-gpt-vectors.json`.

## Loader GPT Repair Candidate

**Moderate confidence, approximately 95%, within the modeled interface.** CPU emulation of the exact saved ARM64 repair core returns success after updating both headers but skips the single-sector entry-array copy. The backup entry-array CRC then fails.

Two buffer-size cases reproduce the result. A preseeded-array positive control produces valid tables; an invalid-primary-signature control returns failure without writes. The branch registers corroborate the skipped copy.

This is a proprietary-loader defect candidate. It has not been demonstrated on hardware, generalized to other loaders or established as novel. It is not a demonstrated bkerler/edl defect.

Offline reference: `gpt-repair-emulation.json`.

## Reconstruction Model

**High confidence, approximately 99%, in the bounded offline results.** A RAM-only model corrects the package's LUN1 headers and backup entries at sectors 1, 2043 and 2047, using the archived 4096-byte-sector, 2048-sector geometry. Header and entry-array CRCs pass. Partition entries, GUIDs and attributes are preserved for each input. Applying the same transformation to the saved good device tables changes no sectors.

The package and device tables have different GUIDs and attributes; the model does not mix them. LBA0 is preserved, including the existing protective-MBR convention. This is not full UEFI conformance certification or a tested on-phone repair.

Offline reference: `lun1-reconstruction-model.json`.

## Linux Delivery Feasibility

**Moderate confidence, approximately 95%, within the stated synthetic test.** Tokens generated by the saved EDL code pass the original loader's per-command checker in emulation with matching synthetic session metadata. Missing tokens, incorrect token secrets and a mismatched session version are rejected.

XML lookup, logging and the firmware SHA256 service are modeled. Original AES, parsing, hash-message construction and comparisons execute. The first attempt exposed a SHA-service mismatch in the incomplete runtime; that diagnostic is retained. No program handler or storage operation runs in this test.

The traced startup initializes the ordinary transport state. This argues against assuming mandatory signed-packet verification for that startup path; it does not establish the current live state or complete write acceptance.

Offline references: `LINUX-DELIVERY-FEASIBILITY.md`, `program-auth-emulation.json`.

## Operation Inventory

**High confidence, approximately 99%, for saved-record and structural checks.** Both pre-device snapshots agree on 135 program records: 64 enabled and 71 disabled. Six payload-bearing records are disabled, including PARAM, persist and persist_bkp. All 70 distinct source ranges are in bounds, and six sparse source ranges pass structural checks. Thirteen relevant code ranges match across the two saved executable captures after address normalization.

The October 27 continuation traces a separate userdata command through sector N-6 inclusive under the recorded mode/start conditions, and identifies staged PARAM commits and encrypted primary/backup transactions. Later flag updates, lower-driver erase behavior, sparse DONT_CARE handling and omitted PARAM helpers still require review. Disabled program records do not prove preservation. Source-range and sparse-structure checks do not validate all payload hashes or data checksums.

Offline references: `DELIVERY-INVENTORY.md`, `delivery-inventory.json`, `gpt-code-equivalence.json`.

## Outstanding Limits

Actual firmware-write acceptance, Android 14-to-OOS11 downgrade compatibility, recovery from that exact transition, and the final unlock remain unproven. The retained collection does not include a complete Android 14 restore image or RPMB backup. No probability of overall success is established.

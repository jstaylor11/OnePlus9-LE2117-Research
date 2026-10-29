# Findings

Evidence cutoff: October 27, 2026, America/Denver. Latest device observation remains October 26; subsequent results are offline. Confidence percentages are judgment estimates about the stated evidence, not measured probabilities of successful flashing or unlocking.

## Narrower Unlock Candidate

**High confidence, approximately 99%, for saved bytes; moderate confidence, approximately 95%, for conditional interpretation and bounded emulation.** Twenty-two ABL cases corroborate the saved T-Mobile/Global carrier-gate difference and separate internal/OEM permission predicates. A guarded Device Info identity override connects to net/BT settings also present in MSM's PARAM processing. Actual acceptance, restoration, persistence and complete unlocking remain unverified.

See [Offline Unlock-Gate Study](Unlock-Gate-Study.md). This does not support an ABL-only flash, a direct PARAM trigger or a device procedure.

## Device Info and PARAM Lifecycle Continuation

**Moderate confidence, approximately 95%, within the documented models; high confidence, approximately 99%, in verified input bytes and recorded checks.** Twenty-five additional bounded cases cover 14 Device Info/cache cases, eight PARAM restoration cases and three connected host/ABL sequences. The original handler and selected restoration/cache routines now execute with shared synthetic services. Provider acceptance, record integrity, the codec bridge, initial PARAM preload and other runtime/storage interfaces remain modeled.

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

# Device Info and PARAM Lifecycle

Evidence date: October 27, 2026, America/Denver. Documentation published October 28. Scope: selected original saved ABL and MSM host instructions, connected through explicitly modeled synthetic RAM services. No phone command, persistent device change or native vendor-executable launch occurred.

## Result and Evidence Strength

Twenty-five new bounded cases pass: 14 Device Info/cache cases, eight PARAM restoration cases and three connected host/ABL sequences. These are separate from the earlier 22 ABL and 18 host cases. The groups have different models and boundaries and are not independent end-to-end validations.

**High confidence, approximately 99%,** in verified input bytes and recorded checks; **moderate confidence, approximately 95%,** in original-code behavior under the stated models. No successful unlock, firmware compatibility, recovery guarantee or probability of overall success is established.

The current investigation advances [issue 5](https://github.com/jstaylor11/OnePlus9-LE2117-Research/issues/5), [issue 6](https://github.com/jstaylor11/OnePlus9-LE2117-Research/issues/6) and [issue 7](https://github.com/jstaylor11/OnePlus9-LE2117-Research/issues/7). All remain open.

## Device Info Cache and Staging

The saved ABL's Device Info wrapper locates a verified-boot protocol and invokes its read/write method with a caller-provided structure. The identity getter uses one cached structure; the guarded internal handler uses a separate staging structure populated during command registration. Other board/boot consumers have another read destination. The external provider implementation and its real storage/acceptance rules remain unresolved.

The cache initializer loads once, records a loaded flag and checks a 13-byte boot magic. A repeated initialization call with that flag set does not automatically refresh the cache. Under the modeled accepting provider, a handler can persist a new staged override while the identity getter still reads the old cached value.

The new cases corroborate these conditional behaviors:

| Path | Result within the model |
| --- | --- |
| Handler write accepted | Persistent and staged state change; the existing identity cache remains stale |
| Later whole-cache writer | Can overwrite the newer persistent value with the stale cached structure in the tested ordering |
| Handler write rejected | Staging RAM remains changed and the original path still reaches its success-response helper |
| Cached write rejected | Attempted RAM value remains; an identical retry can skip storage and return zero |
| Bad-magic reset write rejected | Initializer can return zero and retain its loaded flag despite rejected reset persistence |
| Invalid handler input | Staging RAM changes before range validation, without a provider write in this case |
| Fresh modeled boot | Reloads an accepted persistent override and exercises the original identity mapping/carrier predicate |

Partial-provider controls explicitly assume a provider can transfer a prefix and then return an error. They test consequences of that assumption; they are not observations of actual hardware atomicity. Likewise, a stale overwrite in a modeled ordering does not prove that the same ordering occurs on the phone.

A saved raw Device Info partition contains the expected magic and matches its preserved copy. That does not establish that ordinary partition writes reproduce the external verified-boot provider's protected-state behavior.

## PARAM Verification and Restoration

The original encrypted getter verifies/restores its primary record before extracting a field. In the traced getter path, a valid primary is used without automatically reconciling a divergent backup. If primary verification fails, the restoration routine checks the backup, copies a four-KiB record, increments a header counter and attempts primary then backup writes/readback checks. Successful completion updates both in-memory record copies.

The new cases show:

- A valid new primary can supply the new modeled permission values while its backup remains older.
- A rejected primary can restore older backup values to both copies, reversing the modeled permission change.
- Primary and backup writes each permit four attempts in the traced path. Backup failure can leave primary persistently changed while the operation returns an error.
- Both invalid records cause a field-getter error without supplying the requested output in that case.

### Candidate Return-Status Defect

With successful primary-write returns and four failed modeled full-record readback checks, the original restoration routine can return the last write's zero status. The outer getter then proceeds while the cache and persistent state can differ.

The saved instructions retain the write status in a register; the readback result controls retrying but does not replace that retained status. Retry exhaustion reaches cleanup and returns it. The negative control injects a mismatch in observed readback bytes and records expected/observed hashes for the complete 4,096-byte comparison.

This is a candidate error-propagation defect in the exact saved ABL code under modeled I/O. Practical reachability, hardware impact and novelty are unestablished. It is separate from the MSM final-marker limitation described in [Storage Simulation](Storage-Simulation.md), and is not an EDL source defect.

## Connected Sequences

Three new sequences connect selected original x86 host commit/verify and ARM64 ABL routines through shared synthetic state:

1. Commit and verify both PARAM copies; evaluate original permission/dispatch predicates; execute the guarded handler; reload accepted modeled Device Info on a fresh emulator instance; evaluate original identity mapping and carrier applicability.
2. Fail the host's backup write after its primary update; evaluate ABL's use of the valid new primary.
3. Follow that partial host update with a rejected primary; restore the older backup and evaluate the resulting modeled permission values.

These sequences execute selected original control flow. They do not execute complete boot initialization, the complete unlock confirmation/state/wipe path or Android boot. The saved software-ID/RPMB state machine is separate and remains outside these cases.

## Explicit Models and Limits

Modeled interfaces include the verified-boot provider and its acceptance/transfer behavior, initial PARAM preload, symbolic record integrity, a synthetic codec bridge, partition write/readback services, command registration/prefix classification, and runtime/string/board helpers. Host AES/hash/key and runtime services retain their earlier explicit models.

The synthetic codec bridge is not real AES or vendor-format acceptance validation. A passing case therefore does not establish cryptographic interoperability. Execution outside listed original-code ranges or declared helpers fails the model. All data stores are synthetic RAM; no phone interface is opened and no vendor executable runs natively.

Initial model-development corrections covered the registration entry/prologue, ASCII/Unicode conversion, dispatcher argument offset, numeric-prefix behavior, magic length and a synthetic-counter expectation. These corrections are retained in the private evidence. The assumption that failed restoration verification would preserve the caller's output was disproven by the original retry/return path. Development errors are not evidence of phone failures.

## Remaining Work

Identify the provider implementation matching the saved active firmware; trace its actual storage, acceptance, atomicity and failure behavior. Replace symbolic record acceptance and the synthetic codec with validated format/crypto behavior. Execute the relevant full initialization/restoration paths and establish actual later-writer and unlock-state ordering before considering a physical experiment.

The conversion/GPT hold remains in effect. No device procedure or successful Android 14-to-11 downgrade is established.

Offline references: `LIFECYCLE-CONTINUATION.md`, `lifecycle-results.json` and the adjacent retained instruction extracts and model sources. See [Evidence Index](Evidence-Index.json) for hashes and locations. Private evidence, model sources requiring portability review, device dumps and vendor binaries remain outside this repository.

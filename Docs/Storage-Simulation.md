# Bounded Storage Simulation

Evidence date: October 27, 2026, America/Denver. Scope: selected original MSM host routines against synthetic RAM storage. No phone command, physical write, MSM/Sandbox launch or driver change occurred.

## Result

Eighteen cases pass: seven encrypted-record transaction cases and eleven staged PARAM cases. The simulation records ordered storage requests, offsets, lengths, return values and hashes, with injected write/read errors and readback mismatches.

**Moderate confidence, approximately 95%,** in control-flow behavior within the documented models; **high confidence, approximately 99%,** in consumed saved-byte/hash and setting-map comparisons. No hardware acceptance, cryptographic interoperability or successful unlock is established.

## Encrypted Primary/Backup Transaction

The original commit and verification instructions execute against a synthetic one-MiB PARAM partition. AES/hash/key services and host runtime calls are mocked. The original full encrypted-record byte comparison executes.

Successful order: primary write, primary read/verify, backup write, backup read/verify. For the modeled SID, only two 4-KiB sectors change.

| Injected failure | Synthetic state when the routine returns failure |
| --- | --- |
| Primary write | No changed sector |
| Primary read or readback mismatch | Primary changed; backup untouched |
| Backup write | Verified primary remains changed |
| Backup read or readback mismatch | Both writes occurred before final verification failed |

No rollback write appears in these selected original-routine paths. This does not exclude every possible higher-level recovery path. The successful path updates its in-memory source buffer only after both verifications pass.

## Staged PARAM Processing

Original stage-dispatch and one-MiB read/write wrappers execute. Field/history/header helpers are explicit mocks; encrypted-field storage effects are omitted here and studied separately in the transaction model.

- Preload reads the first MiB. A separate commit precedes the main program loop. Postprocessing reads, modifies, commits and reads back that region.
- Persistent final-marker mismatch causes three update/write/readback attempts after the initial read, then failure.
- A mismatch elsewhere in the returned MiB can pass the final marker check.
- Some modeled field/history helper errors are logged while later commit/marker checking can return success.
- Injected write/readback failures propagate after any preceding writes have already occurred.
- With synthetic selected-mode flags and values decoded from both saved setting maps, original caller instructions request net=3 and BT=2718. Actual post-initialization worker choices remain unknown.

The two models are separate. Their logs must not be combined and described as an end-to-end captured MSM session. The staged model does not run the main image-programming loop, reproduce the omitted helpers, boot Android or emulate secure storage.

## Retained Harness Corrections

The initial transaction harness incorrectly modeled a security-cookie helper as clobbering EAX; the diagnostic is retained and the mock now preserves the return register. Initial stage runs stopped at undeclared string/UI helper boundaries; explicit inspected mocks were added. These were harness corrections, not vendor-code or device failures.

## Remaining Work

Connect the ABL authorization/identity routines to stateful synthetic PARAM and Device Info services. Model initialization/restoration, write rejection, partial completion and cache reload. Independently verify the intended field changes and all affected copies; a final marker or success return is insufficient.

Offline references: `ALTERNATIVE2-SIMULATED-STORAGE.md`, `param-storage-journal.json`, `param-stage-journal.json`, `captured-default-settings.txt`. Integrity references are in [Evidence Index](Evidence-Index.json). The existing package/GPT hold remains in force.

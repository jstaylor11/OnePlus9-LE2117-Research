# Offline Unlock-Gate Study

Evidence date: October 27, 2026, America/Denver. Scope: saved LE2117 slot-B ABL and saved Global OOS11 ABL. No device action was performed. No firmware binary or device backup is included here.

## Result

The saved T-Mobile ABL checks effective project identity before requiring a carrier token. The saved Global ABL uses a compiled product literal for carrier applicability. Original-instruction emulation corroborates that difference. A guarded internal identity-override path is a narrower research candidate, but its usability, persistence and complete unlock effect remain unverified.

**High confidence, approximately 99%,** in consumed byte/hash and table comparisons. **Moderate confidence, approximately 95%,** in conditional code interpretation and bounded emulation. These are evidence judgments, not probabilities of unlocking.

## Gate Dependencies

| Decision | Saved T-Mobile ABL | Saved Global OOS11 ABL |
| --- | --- | --- |
| Ordinary unlock permission | Separate caller predicate precedes carrier check | Separate caller predicate precedes carrier check |
| Carrier applicability | Effective-project getter; carrier identities require validated token state | Compiled product literal takes the non-carrier branch in the saved build |
| Token state | Cached validation byte; certificate/signature path sets it | Parallel validation state/path exists |
| Identity selection | Platform/revision/hardware/RF mapping, with a conditional cached override | Carrier applicability does not use that same effective-project predicate |
| Complete unlocking | Later confirmation/state-update code and services | Later confirmation/state-update code and services |

Skipping a carrier check does not establish ordinary unlock permission, successful secure-state updates, compatible boot firmware or normal Android boot. The study does not support an ABL-only flash.

## Narrower Candidate

The T-Mobile ABL contains an internal project/hardware/radio override handler. Its command descriptor is decoded during registration, and its dispatch path separately checks internal authorization. The handler stages a Device Info change and calls a verified-boot device read/write service. It is a persistent-state candidate, not a read-only probe.

The saved host's net/BT setting maps and the ABL permission predicates connect:

- Both passive captures agree on the setting maps. The selected net entry maps to 3; the selected BT entry maps to 2718.
- Under synthetic inputs, those values satisfy the original internal-dispatch and ordinary-permission predicates in the tested cases.
- A conditional identity override changes the original project-table selection and downstream carrier predicate in synthetic RAM.
- The archived reference PARAM contains 0/0 for the relevant fields in both primary and backup. Encrypted/plaintext integrity and ciphertext round trips pass. This is saved state, not a current-phone query.

This is a dependency chain to investigate, not a validated device sequence. Post-initialization worker choices, field acceptance/restoration, the verified-boot backend, cache reload and later unlock processing remain unresolved. Do not substitute these net/BT fields for the separately documented PARAM software-project-ID/RPMB state machine.

## Validation

Twenty-two bounded ABL cases pass: fourteen identity/carrier-gate cases and eight internal/OEM permission cases. Original ARM64 branches execute with synthetic state; number/string/runtime helpers, selected PARAM reads and internal-prefix classification are modeled. Negative/positive controls alter only emulator RAM. The real internal handler, persistent write service and complete unlock handler never execute.

The saved slot-B PE is hash checked and occurs byte-for-byte inside its retained decompressed artifact. The full ELF/FV/LZMA extraction chain and vendor signatures were not independently revalidated in this study.

## Next Investigation

Trace the Device Info backend, staging/cache relationship and boot-time restoration before deciding whether the narrower route is viable. The token-acquisition route is excluded from the current research scope. No on-phone command or write is proposed by this report.

Offline references: `ALTERNATIVE1-UNLOCK-GATES.md`, `unlock-gate-checks.json`, `internal-permission-checks.json`, `saved-permission-fields.json`. Integrity references are in [Evidence Index](Evidence-Index.json). Raw evidence and local scripts remain outside this repository pending portability/disclosure review.

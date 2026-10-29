# Current Firmware Capture and Device Info Provider

Evidence date: October 29, 2026. Scope: read-only acquisition from the LE2117, followed by offline static analysis. No flashing, unlock, erase or persistent secure-state command was issued. Programmer execution and storage configuration had session effects; this is not a claim of zero internal firmware side effects.

## Result

The missing provider-bearing firmware was captured. The current XBL contains `VerifiedBootDxe` and the exact Device Info protocol referenced by the saved ABL. Both newly captured ABL partitions match their respective saved references, linking the earlier instruction-level studies to the code still present on the phone.

**High confidence, approximately 99%,** in recorded acquisition results, byte identity and protocol registration. **Moderate confidence, approximately 95%,** in the conditional backend interpretation. These estimates describe evidence strength; they are not probabilities of unlocking.

The provider's actual secure-world acceptance rules and the backend selected during the latest boot remain unresolved. Finding the implementation does not establish a usable unlock procedure.

## Device Provenance and Acquired Images

Before the successful acquisition, Android reported LE2117, build `LE2117_14.0.0.900(EX01)`, Android 14, security patch `2025-02-01`, slot B, flash locked, verified boot green and boot completed. These are dated observations, not a current-state monitor.

The requested GPT labels, LUNs, byte offsets and lengths matched the saved map. Eight partitions were read individually with exact-length and successful-transfer checks:

| Image pair | LUNs | Bytes per image | Comparison |
| --- | --- | ---: | --- |
| `abl_a`, `abl_b` | 4 | 8,388,608 | Each matches its own saved reference; A and B differ |
| `xbl_a`, `xbl_b` | 1, 2 | 6,291,456 | Identical across the two slots |
| `xbl_config_a`, `xbl_config_b` | 1, 2 | 524,288 | Identical across the two slots |
| `imagefv_a`, `imagefv_b` | 4 | 2,097,152 | Identical across the two slots |

The eight outputs total 34,603,008 bytes, or 33 MiB. Full partition fingerprints, binaries and transfer logs remain private. Slot equality is a byte comparison, not proof of coherent release provenance or vendor-signature validation.

A subsequent targeted acquisition read PARAM, raw `devinfo` and `abl_log` after validating their current partition maps. PARAM and raw `devinfo` match their saved originals. Both inspected authorization-record copies pass their ciphertext/plaintext integrity and round-trip checks, are byte-identical, and contain zero in the inspected intranet, boottype and test-environment fields. The raw `devinfo` partition is not assumed equivalent to protected Device Info storage.

## EDL Timing and Transfer Validation

The initial attempt could not detect EDL. Kernel records showed approximately fifteen seconds of EDL enumeration, with the GPT client starting approximately three seconds after disconnection. This identifies a sequencing problem; it does not establish why the phone left EDL or a universal EDL timeout.

For the corrected attempt, scripts, arguments, loader verification and the client were staged before the deliberate EDL reboot. The client waited specifically for Qualcomm `05c6:9008` and connected during enumeration. The first GPT operation and all planned image reads then completed. Subsequent commands reused the running Firehose session. No final reset or reboot was requested.

The installed read-handler can report success despite a lower read failure. Exit status alone was therefore insufficient. Validation used expected output lengths, completed-transfer messages, error checks, hashes and subsequent structural inspection. A runtime guard rejected unexpected Firehose XML tags and blocked the automatic Sahara reset path without editing installed source. This guard was scoped protection, not a general sandbox.

The client also issued configuration/storage initialization, storage-information queries, GPT reads and a one-sector setup read beyond the requested image transfers. A configure attribute such as `SkipWrite=0` is not itself a program command. Advertised function names are capabilities, not evidence that those functions executed. All explicit storage operations in this acquisition were reads.

## Provider Identification

The current XBL differs from the older Android 11 conversion input. Its gzip section at partition-image offset `0xDC580` exposes a firmware volume containing:

| Item | Captured value |
| --- | --- |
| Module UI name | `VerifiedBootDxe` |
| FFS GUID | `a25f5839-4d55-428f-8f0b-5ce1d565f53e` |
| Device Info protocol | `8e5eff91-21b6-47d3-af2b-c15a01e020ec` |
| Registration routine | PE RVA `0x2844` |
| Protocol GUID location | PE RVA `0x150E8` |
| Interface | PE RVA `0x15230`, revision `0x10003` |
| Interface method `+8` | PE RVA `0x1570` |
| Method end, exclusive | PE RVA `0x1B10` |

The registration code passes the GUID, interface and null terminator through the expected Boot Services slot. Identification is based on registration and interface structure, not merely a GUID or string search. The extracted firmware-module SHA-256 is `5ec2ea4a9f76b22cd7e7919095968001834c49ed2057195bfec5e6f5430ec30a`; this identifies shared executable input, not a device identifier. The binary is not distributed here.

PE RVAs are offsets in the extracted executable. They are not partition offsets, sectors or addresses to use in a device command.

The earlier Global Android 11 comparison had interface revision `0x10002` and a different method location. It supplied useful search landmarks but is superseded by this capture for the current-provider investigation. It remains cross-version comparison evidence only.

## Storage Selection and Status Handling

At the captured method's entry, the operation is in `w1`, buffer in `x2` and length in `w3`. Null buffer or zero length returns an invalid-parameter result. Operation zero selects reading; one selects writing. There is no exact `0xA88` entry-length gate in the traced method. The calling shape agrees with the saved ABL wrapper, without proving every structure field's semantics.

Security-state helpers use masks `0x8703` and `0x8723`. Their lower reader reaches an SCM-like interface and checks transport and response state. The actual returned hardware security word was not queried during acquisition.

Depending on that state, the method reaches:

- Named `devinfo` partition helpers, using block I/O and checking failure status.
- Protocol `a74862ce-680f-4fe1-a311-df41f4030391`, a `keymaster` application handle and its command interface. Requests `0x202` and `0x203` read and write a 4,096-byte service buffer. The write path first reads existing contents, copies the caller's bytes into that buffer, and checks transport and response status after the write request. Its diagnostics label this the RPMB path.

Selected secure-service failures permit partition fallback only under the second security-state condition; others return an error. Plain partition replacement cannot be assumed to reproduce the protected service's behavior. The secure-world implementation, acceptance, atomicity and power-loss response remain unresolved.

A static allocation-failure branch also appears able to reach a zero-status return without transferring data. This was not fault-injected or reproduced on hardware. Practical reachability and impact are unestablished; it is a provider-code concern, not an EDL-source finding.

## Historical Log Limitation

The newly acquired `abl_log` is byte-identical to the retained September 26 copy. It contains 131 RPMB-success and fifteen `devinfo`-success messages. These are captured historical runtime reports of both paths. Their capture date does not date the underlying events or identify the backend selected by the latest boot.

## Remaining Work

Trace the secure-service contract and protected-state acceptance, then connect the captured provider to the ABL's initialization, cache reload, later writers and complete unlock-state path. Keep the narrower identity-override candidate separate from the unvalidated Android 14-to-11 conversion.

The acquisition sequence above documents what occurred; it is not a portable collection script or an unlock guide. Original firmware, private logs, model sources and detailed acquisition manifests remain outside this repository. See [Evidence Index](Evidence-Index.json), [Original Crypto and Startup Checks](Original-Crypto-and-Startup.md) and [Toolchain Provenance](Toolchain-Provenance.md).

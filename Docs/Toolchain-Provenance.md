# EDL Toolchain Provenance

Evidence date: October 29, 2026. Scope: source comparison, an isolated runtime selection and offline focused tests. Runtime verification did not access the phone.

## Selected Runtime

The accepted configuration is the existing official EDL base with only `edlclient/Library/Modules/oneplus_param.py` substituted from the research fork's master branch. The selection is pinned to a commit rather than following a moving branch name. No Napreth branch merge or deletion is involved.

| Component | Identity |
| --- | --- |
| Existing base | `2f8e89a848afaaef68997fcbcb5b178d958d497b` |
| PARAM source | [jstaylor11/edl master](https://github.com/jstaylor11/edl/commit/9f796ebc2c2348c725f845b4fe76b6769d0f2d82), commit `9f796ebc2c2348c725f845b4fe76b6769d0f2d82` |
| PARAM Git blob | `5f7fde5b8e9149e06c3e8c7f02ad43b740c7b515` |
| PARAM size | 41,404 bytes with LF line endings |
| PARAM SHA-256 | `3ac3e93f6af21f595240ccbc3ee674d923fb50af0235f375bc8bcce771ca2b40` |

The isolated runtime contains exactly one changed Python source compared with the existing installation: the selected PARAM module. Existing checkouts, site-packages, dependencies, drivers and system settings were left unchanged. Bare entry points from the original installation still select the old module; later device operations must use the verified launcher.

## Import Verification

A downloaded file alone does not establish which implementation executes. The launcher:

1. Verifies the isolated runtime's source manifest.
2. Rejects an already-imported EDL namespace before selecting the overlay.
3. Selects the overlay before importing the PARAM module and OnePlus transport.
4. Checks the module's actual source path, size and digest.
5. Verifies that the transport's bound `paramtools` class is the class exported by the substituted module.

The audited paths resolve inside the isolated runtime. The local launcher, interpreter path and complete audit remain private because they contain machine-specific locations. The device route also retains a scoped read-only XML/reset guard. Source verification and a read guard do not constitute a validated persistent-write procedure.

## Focused Tests

All three tests from the exact master revision pass through the same runtime selection:

- Failed decryption does not mutate input or call the encryption routine.
- A valid synthetic encrypted version-1 record still updates correctly.
- CLI validation failure preserves existing output or leaves absent output absent.

Tests use synthetic RAM data and temporary local files. They do not modify a captured device image or open a USB interface. **High confidence, approximately 99%,** in the recorded source/import checks and test results; no physical acceptance conclusion follows.

## Prior Capture Provenance

The completed firmware and supplemental reads used the older installed tree, before the substitution was verified. Their provenance remains recorded that way. They are not relabeled as patched-runtime captures or automatically repeated.

Git-object comparisons and local runtime comparisons show identical bytes in `firehose.py`, `firehose_client.py`, `sahara.py` and `Connection/usblib.py` between that base and the selected master source. Together with transfer logs, exact sizes, structural inspection and saved ABL matches, this supports retaining the acquired evidence. It does not make every entry point or PARAM implementation identical.

## Fix Scope

The selected contribution concerns failed-decryption and output-file handling. It does not add the separate version-2 serial/key derivation research, make all record formats compatible, make writes atomic, or implement bootloader unlocking. The committed focused guard and firmware-specific research remain separate findings.

Third-party code retains its authorship and license. No tool source, vendor firmware, private launcher or device data is redistributed in this documentation update. See [Current Firmware Provider](Current-Firmware-Provider.md) and [Original Crypto and Startup Checks](Original-Crypto-and-Startup.md).

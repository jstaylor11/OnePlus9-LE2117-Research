# Research Standards

## Evidence

Record the date, exact software/package identity, input hashes, method, result and limits for each experiment. Separate direct device observations, captured runtime state, static interpretation and emulation results. Keep failed experiments and corrected assumptions in the working record.

Distinguish the date a log was acquired from the age of its events. Preserve each acquisition's actual tool source; later runtime fixes do not retroactively change how an earlier capture was made. Report actual imported module identity when a runtime mixes a pinned module with an existing base.

Use concise confidence categories with estimated percentages when reporting factual findings. Treat those estimates as judgments about evidence strength, not statistical measurements or probabilities of unlocking.

## Repository Material

Commit reviewed reports, portable source code, synthetic fixtures and appropriately scoped manifests. Preserve upstream authorship and license notices for third-party material.

Keep device backups, personal identifiers, authentication material, session transcripts, process-memory captures and vendor firmware outside Git. The initial ignore rules allow only reviewed documentation; adding another artifact type requires an explicit review of the tracked file list.

Public reports may retain model/build versions, shared firmware-module hashes, protocol GUIDs and code offsets needed to assess findings. Exclude device-unique identifiers, partition GUIDs, raw device-image fingerprints, host/user paths, account contact details and authentication data from new public reports. Integrity references to private study reports do not include those reports' contents and are not a substitute for reproducibility.

An offline evidence reference identifies retained material that is not included in this repository. Hashes support integrity checks, not public reproducibility by themselves. Before public release, provide suitable synthetic cases or a lawful, documented input-acquisition procedure.

## Device Work

Inspect existing evidence before repeating hardware experiments. Document a concrete operation and its failure response before storage writes. Readback, authentication, valid CRCs and tool success messages do not replace verification of normal Android boot and unlocked bootloader state.

## Tracking

Use issues for unresolved questions, next experiments and contribution candidates. Every result should state what changed, how it was checked and what remains unknown. Keep repository and project names in their intended capitalization.

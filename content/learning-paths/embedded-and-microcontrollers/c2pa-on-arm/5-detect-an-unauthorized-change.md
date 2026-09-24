---
title: Detect an unauthorized protected-asset change
weight: 6

### FIXED, DO NOT MODIFY
layout: learningpathall
---

## Protect the known-good files

TODO: Verify the unsigned source and pristine signed asset before creating a separately named modified
copy. Do not overwrite either source fixture.

## Understand the negative-test boundary

TODO: Explain why opening and resaving the image in an editor is unsuitable: it may remove the manifest
rather than demonstrate a retained-manifest hard-binding mismatch. State what the validated helper
changes and preserves.

## Create the modified asset

TODO: Introduce the reviewed deterministic helper. Add the exact command and checks showing that:

- the output differs from the pristine signed asset;
- the manifest remains present; and
- the modified asset is suitable for testing the intended validation path.

## Validate the modified asset

TODO: Add the tested validation command, expected non-success behavior, exit status, and a short
sanitized error excerpt.

## Confirm the intended failure reason

TODO: Show that the expected hard-binding mismatch caused the failure, rather than missing metadata,
malformed input, or an unrelated credential error.

## Restore and validate the known-good asset

TODO: Re-run validation on the untouched signed fixture and show that the positive result returns.

## Compare the two results

TODO: Compare manifest presence, asset binding, signature and trust interpretation, and overall
validation status for the pristine and modified assets.

## What the experiment proves

TODO: State narrowly that the experiment demonstrates detection of the tested protected-data change by
the recorded workflow.

## What the experiment does not prove

TODO: Reiterate that the result does not establish truthfulness, production signer identity, universal
tamper detection, hardware-backed key protection, or remote platform attestation.

## Evidence needed

- `[EXPERIMENT]` Reviewed deterministic tamper helper and exact invocation.
- `[EXPERIMENT]` Proof that the manifest remains present after modification.
- `[EXPERIMENT]` Negative fixture and validation transcript showing the intended failure.
- `[EXPERIMENT]` Recovery and revalidation transcript for the pristine signed asset.
- `[RESEARCH]` Specification support for the final security interpretation.

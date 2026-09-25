---
title: Inspect and validate Content Credentials
weight: 5

### FIXED, DO NOT MODIFY
layout: learningpathall
---

{{% notice Note %}}
This workflow was demonstrated with `c2patool 0.27.21` on Apple silicon macOS. The signed fixture uses
a development certificate.
{{% /notice %}}

## Display the manifest report

```console
c2patool c2pa-sample-signed.jpg
```

C2PA Tool prints a JSON manifest report and validates the manifest while reading it. Focus on which
manifest is active, what it says happened, whether the claim and asset binding validate, and whether
the signing credential is trusted.

## Find the active manifest

Find `active_manifest`, locate the same label under `manifests`, and inspect
`claim_generator_info`:

```output
"claim_generator_info": [
  {
    "name": "Arm Learning Path C2PA Example",
    "version": "1.0.0",
    "com.arm.learning_path.tool": {
      "name": "c2patool",
      "version": "0.27.21"
    },
    "org.contentauth.c2pa_rs": "0.90.21"
  }
]
```

The name and `1.0.0` example version match the values you supplied in `manifest.json`. The custom
`com.arm.learning_path.tool` field records the separate tool name and version you supplied. C2PA Tool adds
`org.contentauth.c2pa_rs` to identify its underlying library; `0.90.21` is the library version in the
tested tool. Manifest labels, instance IDs, and UUIDs differ between runs.

## Inspect the assertions

The `assertions` array contains a `c2pa.actions.v2` assertion:

```output
"actions": [
  {
    "action": "c2pa.created",
    "digitalSourceType": "http://cv.iptc.org/newscodes/digitalsourcetype/digitalCapture"
  }
]
```

This is a declaration supplied by the claim generator, not independent proof of how the depicted scene
was produced or whether it is truthful.

## Inspect the hard binding

Under `validation_results`, `activeManifest`, and `success`, find:

```output
{
  "code": "assertion.dataHash.match",
  "explanation": "data hash valid"
}
```

For this JPEG and tool version, the data-hash assertion binds protected byte ranges to the claim. The
status means those bytes match the recorded hash.

## Inspect the signature and credential

```output
"signature_info": {
  "alg": "Es256",
  "issuer": "C2PA Test Signing Cert",
  "common_name": "C2PA Signer"
}
```

The validation results also report:

```output
{
  "code": "signingCredential.untrusted",
  "explanation": "signing certificate untrusted"
}
```

Keep these checks separate:

- `claimSignature.validated` says that the cryptographic signature on the claim verifies.
- `assertion.dataHash.match` says that protected asset data matches the signed claim.
- `signingCredential.untrusted` says that the validator's trust policy does not accept the certificate.

A verifying signature does not, on its own, establish who controlled the corresponding private key.

## Run positive validation

Confirm that `validation_results` contains these status codes:

```output
claimSignature.validated
assertion.hashedURI.match
assertion.dataHash.match
signingCredential.untrusted
```

The tested fixture also reports:

```output
"validation_state": "Valid"
```

Read that field with the individual status codes. Here, `Valid` accompanies successful signature and
data-hash checks despite `signingCredential.untrusted`; it does not mean the signer is trusted. The
result also does not prove that the image is true or that its assertion is factually correct.


Next, change protected asset data deliberately and observe the validation failure.

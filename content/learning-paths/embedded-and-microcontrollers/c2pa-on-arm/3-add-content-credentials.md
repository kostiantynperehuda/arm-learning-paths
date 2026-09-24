---
title: Add Content Credentials to an image
weight: 4

### FIXED, DO NOT MODIFY
layout: learningpathall
---

## Development credential limitation

The Learning Path demonstrates signing mechanics. It uses the private key and signing
certificate built into C2PA Tool. These test credentials do not establish a production identity or
trust by public validators. A validator that does not explicitly trust the certificate reports it as
untrusted.

Do not use the built-in private key or certificate to sign production content.

## Create the manifest definition

In your text editor, create a plain-text file named `manifest.json` in your `c2pa-demo` working directory with
these contents:

```json
{
  "assertions": []
}
```

This file supplies the manifest definition used by `--manifest manifest.json` in the signing command below.
The empty `assertions` array means you are not supplying any custom assertions. C2PA Tool still
builds the signed manifest; the `--create digitalCapture` option adds the creation
action. Keeping the definition minimal lets you focus on signing and validation.

Save the file as `manifest.json`, not `manifest.json.txt`.

## Add the Content Credential

Run this command from the directory prepared in the previous section. The output filename must not
already exist. If it does, move or rename that earlier output before you continue.

```console
c2patool c2pa-sample-image.jpg --manifest manifest.json --create digitalCapture --output c2pa-sample-signed.jpg
```

- `--manifest manifest.json` supplies the minimal manifest definition.
- `--create digitalCapture` declares digitally captured content and adds a `c2pa.created` action.
- `--output c2pa-sample-signed.jpg` writes a new file instead of overwriting the unsigned source.

The command exits with status 0 when signing succeeds. It does not modify
`c2pa-sample-image.jpg`.

## Recognize the development warning

```output
Note: Using default private key and signing certificate. This is only valid for development.
A permanent key and cert should be provided in the manifest definition or in the environment variables.
```

The command also prints the generated manifest report. Its generated identifiers differ between runs.

## Confirm that the signed file contains a manifest

```console
c2patool c2pa-sample-signed.jpg --info
```

The macOS experiment reported:

```output
Validation issues:
   signingCredential.untrusted
One manifest
```

`One manifest` confirms that the output contains a C2PA manifest. The
`signingCredential.untrusted` status means the validator cannot build trust from the development
certificate to a configured trust anchor; it does not mean that signing failed or establish a trusted
signer identity.

Keep these files for the remaining steps:

```text
manifest.json
c2pa-sample-image.jpg
c2pa-sample-signed.jpg
```


Next, inspect the generated manifest and separate signature and asset-binding validation from trust.

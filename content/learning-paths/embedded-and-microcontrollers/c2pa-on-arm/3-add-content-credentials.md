---
title: Add Content Credentials to an image
weight: 4

### FIXED, DO NOT MODIFY
layout: learningpathall
---

## Add Content Credentials while preserving the original

You will add Content Credentials to the image prepared in the previous chapter. You will save the
signed image as a separate file, preserving the unsigned original.

## Understand the development credential

The example uses the private key and signing certificate built into C2PA Tool. These test credentials
let you practise signing, but do not establish a production identity or trust by public validators.
Do not use them to sign production content.

## Create the manifest definition

A manifest definition tells C2PA Tool which provenance information to include. An *assertion* records
information about the asset, such as an action in its history. The *claim generator* is the software
that assembles the claim and its references to assertions for signing. In this exercise, C2PA Tool performs that work using the example identity you supply below.

In your text editor, create a plain-text file named `manifest.json` in your `c2pa-demo` working directory
with these contents:

```json
{
  "claim_generator_info": [
    {
      "name": "Arm Learning Path C2PA Example",
      "version": "1.0.0",
      "com.arm.learning_path.tool": {
        "name": "c2patool",
        "version": "0.27.21"
      }
    }
  ],
  "assertions": [
    {
      "label": "c2pa.actions.v2",
      "data": {
        "actions": [
          {
            "action": "c2pa.created",
            "digitalSourceType": "http://cv.iptc.org/newscodes/digitalsourcetype/digitalCapture"
          }
        ]
      }
    }
  ]
}
```

Save the file as `manifest.json`, not `manifest.json.txt`.

The fields make the provenance information explicit:

- `claim_generator_info` labels this workflow as `Arm Learning Path C2PA Example`. Its `version`,
  `1.0.0`, identifies this version of the example. C2PA Tool performs the signing; its installed version
  is separate from the example version.
- `com.arm.learning_path.tool` records the tool used by this example: `c2patool` version `0.27.21`.
  Set its `version` to the value reported by `c2patool --version` in the previous chapter.
- `assertions` contains a `c2pa.actions.v2` assertion. Its `data.actions` array records a `c2pa.created`
  action, with `digitalSourceType` declaring digitally captured content.

The [C2PA generator-info specification](https://spec.c2pa.org/specifications/specifications/2.4/specs/ContentCredentials.html#_generator_info_map)
allows additional fields with entity-specific names. `com.arm.learning_path.tool` is a custom field
for this example, using the `com.arm` namespace; it is not a standard C2PA field. It keeps the example
version and tool version separate within one claim-generator entry. The array shown here is C2PA
Tool's manifest-definition format.

The creation action describes the image's origin; it does not mean this command takes a photograph.
For this exercise, `digitalCapture` is a sample declaration supplied by you. C2PA Tool does not infer
or verify it from the image. Signing protects the declaration from undetected changes; it does not
prove that the declaration is true.

An action can also have a `softwareAgent` field identifying the software or hardware that performed
that action. This differs from `claim_generator_info`, which identifies what generates the claim now.
We leave the creation action's agent unspecified because the sample's original capture device or
software has not been established. Naming C2PA Tool there would incorrectly attribute the capture to it.

You supply the provenance fields above. C2PA Tool generates the claim, asset-binding data, and signature
when it builds the signed manifest; you do not write those cryptographic structures by hand.

C2PA Tool also offers a command-line shortcut: with an empty `assertions` array, `--create digitalCapture`
adds the creation action. If you omit `claim_generator_info`, the tool supplies its own name and
version instead of this example label. Keep the explicit claim-generator information to retain the
Learning Path label. This chapter writes the action in JSON too, so omit `--create` from the command below.

## Sign the image

Run this command from your `c2pa-demo` directory. The output filename must not already exist. If it
does, move or rename that earlier output before you continue.

```console
c2patool c2pa-sample-image.jpg --manifest manifest.json --output c2pa-sample-signed.jpg
```

`--manifest manifest.json` supplies your definition. `--output c2pa-sample-signed.jpg` writes the
signed image to a separate file, leaving `c2pa-sample-image.jpg` unchanged.

The command exits with status 0 when signing succeeds. The expected development warning is:

```output
Note: Using default private key and signing certificate. This is only valid for development.
A permanent key and cert should be provided in the manifest definition or in the environment variables.
```

The command also prints the generated manifest report. Its generated identifiers differ between runs.
You will inspect that report in the next chapter.

## Confirm that the signed file contains a manifest

Inspect the signed image to check that a manifest is present:

```console
c2patool c2pa-sample-signed.jpg --info
```

The expected output includes:

```output
Validation issues:
   signingCredential.untrusted
One manifest
```

`One manifest` confirms that the output contains a C2PA manifest. `signingCredential.untrusted` is the
expected trust result for this development certificate; it does not mean that signing failed.
The byte counts and percentages also printed by this command can vary.

This checkpoint confirms manifest presence. In the next chapter, you will examine the signature,
asset binding, and signer trust separately.

## What you've accomplished

You have defined the provenance information, signed the image, and confirmed that the output contains
a manifest. Keep these three files for the remaining chapters:

| File | Purpose |
| --- | --- |
| `manifest.json` | Your claim-generator information and creation assertion |
| `c2pa-sample-image.jpg` | The unchanged unsigned source image |
| `c2pa-sample-signed.jpg` | The signed image containing the C2PA manifest |

Next, inspect the generated manifest and distinguish signature and asset-binding validation from
signer trust.

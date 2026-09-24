---
title: Prepare the example files
weight: 3

### FIXED, DO NOT MODIFY
layout: learningpathall
---

## Confirm C2PA Tool is available

Run the platform-independent version check:

```console
c2patool --version
```

The version number depends on the current stable release. The recorded workflow used:

```output
c2patool 0.27.21
```

If the command is unavailable, follow the [C2PA Tool install guide](/install-guides/c2patool/).

## Create a working directory

TODO: Define an OS-neutral way to obtain or create the working directory. Use publication-supported OS
tabs only if a filesystem command is unavoidable.

## Obtain the example files

[Download the sample JPEG (61,720 bytes)](../assets/c2pa-sample-image.jpg) and save it in your working
directory as `c2pa-sample-image.jpg`. If your browser displays the image, use **Save image as** to
save the original JPEG. Keep this unsigned source file for the later steps.

The image comes from [`cli/sample/image.jpg` in the Content Authenticity Initiative's `c2pa-rs` repository](https://github.com/contentauth/c2pa-rs/blob/712f03b72cbc1b00fc41adee5835fc92be2758d1/cli/sample/image.jpg),
at the revision used by `c2patool-v0.27.21`. The copy supplied with this Learning Path is unchanged.

TODO before publication: Confirm the image-specific redistribution rights. The upstream repository
contains Apache-2.0 and MIT licenses, but the asset record does not establish an image-specific
license or attribution requirement.

You also need `manifest.json`, whose contents are shown in **Review the manifest definition** below.

## Confirm the starting state

Use C2PA Tool to confirm that the source image does not already contain a manifest:

```console
c2patool c2pa-sample-image.jpg --info
```

TODO: Add a stable expected-output excerpt from the tested C2PA Tool version.

## Review the manifest definition

The proposed minimal definition is:

```json
{
  "assertions": []
}
```

TODO: Decide whether the workflow needs a platform-independent JSON validation check. Do not require
`jq` unless it is already a justified prerequisite on every supported operating system.

## Evidence needed

- `[EXPERIMENT]` Version and source-image inspection output recorded with C2PA Tool 0.27.21.
- `[EXPERIMENT]` Verify the bundled image download in the rendered Learning Path.
- `[UNVALIDATED]` Final sample image license and working-directory instructions.

Next, add a Content Credential while preserving the unsigned source image.

---
title: Check C2PA Tool and prepare the sample image
weight: 3

### FIXED, DO NOT MODIFY
layout: learningpathall
---

## Create a working directory

Create a folder named `c2pa-demo` wherever you keep your projects, using your file manager or terminal.
Open a terminal in that folder and run the remaining commands there. Keep all files from this
Learning Path in the same folder so the commands can use their filenames without full paths.

## Confirm C2PA Tool is available

Run the platform-independent version check:

```console
c2patool --version
```

The version number depends on the current stable release. All subsequent outputs in this Learning
Path were recorded using the following version:

```output
c2patool 0.27.21
```

If the command is unavailable, follow the [C2PA Tool install guide](/install-guides/c2patool/).

## Download the sample image

[Download the sample JPEG (61,720 bytes)](../assets/c2pa-sample-image.jpg) and save it in your working
directory as `c2pa-sample-image.jpg`. If your browser displays the image, use **Save image as** to
save the original JPEG. Keep this unsigned source file for the later steps.

The image comes from [`cli/sample/image.jpg` in the Content Authenticity Initiative's `c2pa-rs` repository](https://github.com/contentauth/c2pa-rs/blob/712f03b72cbc1b00fc41adee5835fc92be2758d1/cli/sample/image.jpg),
at the revision used by `c2patool-v0.27.21`. The copy supplied with this Learning Path is unchanged.

TODO before publication: Confirm the image-specific redistribution rights. The upstream repository
contains Apache-2.0 and MIT licenses, but the asset record does not establish an image-specific
license or attribution requirement.

## Confirm the starting state

Use C2PA Tool to confirm that the source image does not already contain a manifest:

```console
c2patool c2pa-sample-image.jpg --info
```

The expected output includes:

```output
No C2PA Manifests. (file size = 61720)
```

The supplied image has no existing C2PA manifest, so you can use it as the unsigned source for the
next step.

Next, add a Content Credential while preserving the unsigned source image.

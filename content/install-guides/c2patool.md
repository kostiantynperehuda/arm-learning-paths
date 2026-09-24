---
title: C2PA Tool
description: Install C2PA Tool on an Arm device to inspect, create, and validate C2PA manifests from the command line.
minutes_to_complete: 20
official_docs: https://github.com/contentauth/c2patool
author: PLACEHOLDER NAME

draft: true

test_maintenance: false

### FIXED, DO NOT MODIFY
weight: 1
tool_install: true
multi_install: false
multitool_install_part: false
layout: installtoolsall
---

[C2PA Tool](https://github.com/contentauth/c2patool), invoked as `c2patool`, displays, creates, and
validates C2PA manifests in supported media files.

This guide installs the current stable release on Arm Linux, macOS, or Windows on Arm. See
[C2PA Tool releases](https://github.com/contentauth/c2patool/releases) for release information.

## Install on macOS

Install [Homebrew](https://brew.sh/) if it isn't already available.

Install C2PA Tool:

```console
brew install c2patool
```

## Install on Arm Linux

Prebuilt Linux releases target `x86_64`. Use Cargo to build and install a native `aarch64`
executable.

Install the build dependencies on Ubuntu or Debian:

```console
sudo apt update
sudo apt install -y build-essential pkg-config libssl-dev
```

Install [Rust](/install-guides/rust/) to obtain Cargo, then install C2PA Tool:

```console
cargo install c2patool --locked
```

Cargo installs `c2patool` in `$HOME/.cargo/bin`.

## Install on Windows on Arm

Prebuilt Windows releases target `x86_64`. Use Cargo to build and install a native ARM64 executable.

Install the Microsoft C++ Build Tools and [Rust](https://www.rust-lang.org/tools/install) with the
MSVC toolchain for ARM64. Open a new PowerShell window and run:

```console
cargo install c2patool --locked
```

Cargo installs `c2patool.exe` in `%USERPROFILE%\.cargo\bin`.

## Verify the installation

Print the installed version:

```console
c2patool --version
```

The output reports `c2patool` followed by the installed version number.

Display the command summary:

```console
c2patool --help
```

The output starts with:

```output
Tool for displaying and creating C2PA manifests
```

## Troubleshooting

If your shell can't find `c2patool`, open a new terminal. For a Cargo installation, confirm that
`$HOME/.cargo/bin` on Linux or `%USERPROFILE%\.cargo\bin` on Windows is in your `PATH`.

## Update C2PA Tool

On macOS, run:

```console
brew update
brew upgrade c2patool
```

For a Cargo installation, run:

```console
cargo install c2patool --locked --force
```

## Uninstall C2PA Tool

For a Homebrew installation, run:

```console
brew uninstall c2patool
```

For a Cargo installation, run:

```console
cargo uninstall c2patool
```

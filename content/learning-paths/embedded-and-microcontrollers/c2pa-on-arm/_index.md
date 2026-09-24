---
title: Create and verify C2PA Content Credentials on Arm

draft: true
cascade:
    draft: true

description: Add Content Credentials to an image on an Arm device, inspect its C2PA manifest, and detect a controlled change to protected asset data.

minutes_to_complete: 75

who_is_this_for: This is an introductory topic for developers who want to create and verify content provenance on an Arm device.

learning_objectives:
    - Explain what C2PA is and the content provenance problem it addresses.
    - Add a C2PA manifest to a sample image with C2PA Tool.
    - Inspect the manifest and interpret the asset-binding, signature, and trust results.
    - Demonstrate a hard-binding failure after a controlled protected-asset change.
    - Distinguish content provenance from truth and signer trust.

prerequisites:
    - "The current stable release of [C2PA Tool](/install-guides/c2patool/) installed on your Arm device"
    - Familiarity with running command-line tools

author: PLACEHOLDER NAME

generate_summary_faq: true
rerun_summary: false
rerun_faqs: false

### Tags
skilllevels: Introductory
subjects: Security
armips:
    - Cortex-A
tools_software_languages:
    - Raspberry Pi
operatingsystems:
    - Linux
    - macOS
    - Windows

further_reading:
    - resource:
        title: C2PA technical specification
        link: https://c2pa.org/specifications/
        type: documentation
    - resource:
        title: C2PA Tool source repository
        link: https://github.com/contentauth/c2patool
        type: repository

### FIXED, DO NOT MODIFY
# ================================================================================
weight: 1
layout: "learningpathall"
learning_path_main_page: "yes"
---

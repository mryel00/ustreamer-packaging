# ustreamer-packaging

This repository contains Debian packaging configuration for [pikvm/ustreamer](https://github.com/pikvm/ustreamer).

## Overview

µStreamer is a lightweight and fast MJPEG-HTTP streamer. This repository provides:
- Debian packaging files in the `debian/` directory
- GitHub Actions workflow to automatically build Debian packages

## Package Compatibility

The `mainsail-ustreamer` package is designed to be compatible with the upstream `ustreamer` package:
- **`Conflicts: ustreamer`** - Prevents simultaneous installation
- **`Replaces: ustreamer`** - Allows replacing the ustreamer package
- **`Provides: ustreamer`** - Provides virtual package ustreamer

This allows users to switch between packages seamlessly.

## Version

The workflow automatically uses the **latest release tag** from the [pikvm/ustreamer](https://github.com/pikvm/ustreamer) repository.


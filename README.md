# ustreamer-packaging

This repository contains Debian packaging configuration for [pikvm/ustreamer](https://github.com/pikvm/ustreamer).

## Overview

µStreamer is a lightweight and fast MJPEG-HTTP streamer. This repository provides:
- Debian packaging files in the `debian/` directory
- GitHub Actions workflow to automatically build Debian packages

## Building Packages

### Using GitHub Actions

The workflow automatically builds packages for:
- Debian Bullseye (11)
- Debian Bookworm (12)

Packages are built on:
- Push to `main` branch
- Pull requests to `main` branch
- Manual workflow dispatch

The built packages are available as artifacts in the GitHub Actions runs.

### Building Locally

To build the package locally:

```bash
# Clone this repository
git clone https://github.com/mryel00/ustreamer-packaging.git

# Clone ustreamer
git clone --depth 1 --branch v6.40 https://github.com/pikvm/ustreamer.git

# Copy debian folder
cp -r ustreamer-packaging/debian ustreamer/

# Build using Docker
cd ustreamer
docker run --rm \
  -v $(pwd):/src \
  -v $(pwd)/../output:/output \
  -w /src \
  debian:bookworm \
  bash -c "
    apt-get update && \
    DEBIAN_FRONTEND=noninteractive apt-get install -y --no-install-recommends \
      debhelper libevent-dev libjpeg62-turbo-dev libbsd-dev \
      libgpiod-dev libsystemd-dev pkg-config gcc make \
      dpkg-dev fakeroot build-essential && \
    dpkg-buildpackage -us -uc -b && \
    mv ../*.deb /output/
  "
```

The built package will be in the `output/` directory.

## Package Features

The package includes:
- `ustreamer` - Main streaming server
- `ustreamer-dump` - Utility for dumping frames
- Man pages for both utilities
- Built with GPIO and systemd support

## Dependencies

The package automatically handles dependencies:
- libevent
- libjpeg62-turbo
- libbsd
- libgpiod
- libsystemd

## Version

Current packaged version: **6.40**

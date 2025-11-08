# Installation Guide

This fork of TypeScript Go disables the TS2742 error and publishes pre-built binaries for easy installation.

## Using mise (Recommended)

[mise](https://mise.jdx.dev/) is a polyglot tool version manager. Add this to your `.mise.toml`:

```toml
[tools."http:tsgo".platforms]
macos-x64 = { url = "https://github.com/colelawrence/typescript-go/releases/latest/download/tsgo-latest-macos-x64.tar.gz" }
macos-arm64 = { url = "https://github.com/colelawrence/typescript-go/releases/latest/download/tsgo-latest-macos-arm64.tar.gz" }
linux-x64 = { url = "https://github.com/colelawrence/typescript-go/releases/latest/download/tsgo-latest-linux-x64.tar.gz" }
linux-arm64 = { url = "https://github.com/colelawrence/typescript-go/releases/latest/download/tsgo-latest-linux-arm64.tar.gz" }
windows-x64 = { url = "https://github.com/colelawrence/typescript-go/releases/latest/download/tsgo-latest-windows-x64.tar.gz" }
windows-arm64 = { url = "https://github.com/colelawrence/typescript-go/releases/latest/download/tsgo-latest-windows-arm64.tar.gz" }
```

Or pin to a specific version (see [Releases](https://github.com/colelawrence/typescript-go/releases)):

```toml
[tools."http:tsgo".platforms]
macos-arm64 = { url = "https://github.com/colelawrence/typescript-go/releases/download/0.20241108.165500/tsgo-0.20241108.165500-macos-arm64.tar.gz" }
```

Then run:

```bash
mise install tsgo
tsgo --version
```

## Manual Download

Download the tarball for your platform from the [Releases page](https://github.com/colelawrence/typescript-go/releases):

- **macOS (Intel)**: `tsgo-VERSION-macos-x64.tar.gz`
- **macOS (Apple Silicon)**: `tsgo-VERSION-macos-arm64.tar.gz`
- **Linux (x64)**: `tsgo-VERSION-linux-x64.tar.gz`
- **Linux (ARM64)**: `tsgo-VERSION-linux-arm64.tar.gz`
- **Windows (x64)**: `tsgo-VERSION-windows-x64.tar.gz`
- **Windows (ARM64)**: `tsgo-VERSION-windows-arm64.tar.gz`

Extract and add to your PATH:

```bash
# Example for macOS ARM64
curl -L https://github.com/colelawrence/typescript-go/releases/download/VERSION/tsgo-VERSION-macos-arm64.tar.gz | tar xz
# Move to your PATH
mv tsgo /usr/local/bin/
# Verify
tsgo --version
```

## Building from Source

See [PUBLISH.md](PUBLISH.md) for build instructions.

## What's Different?

This fork includes a single patch:
- **TS2742 disabled**: The "inferred type cannot be named without a reference" error is disabled

This allows TypeScript code that references types from node_modules to compile without explicit type annotations.

## Version Format

Releases use semver-compatible timestamp versioning: `0.YYYYMMDD.HHMMSS` (UTC)

Example: `0.20241108.165500` = November 8, 2024 at 16:55:00 UTC

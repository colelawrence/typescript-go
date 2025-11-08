# Installation Guide

This fork of TypeScript Go disables the TS2742 error and publishes pre-built binaries for easy installation.

## Using mise (Recommended)

[mise](https://mise.jdx.dev/) is a polyglot tool version manager. Add this to your `.mise.toml`:

```toml
[tools."http:tsgo".platforms]
# Most common platforms
macos-arm64 = { url = "https://github.com/colelawrence/typescript-go/releases/latest/download/tsgo-latest-macos-arm64.tar.gz" }
linux-x64 = { url = "https://github.com/colelawrence/typescript-go/releases/latest/download/tsgo-latest-linux-x64.tar.gz" }
windows-x64 = { url = "https://github.com/colelawrence/typescript-go/releases/latest/download/tsgo-latest-windows-x64.tar.gz" }
# Also available: macos-x64, linux-arm64
```

Or pin to a specific version (see [Releases](https://github.com/colelawrence/typescript-go/releases)):

```toml
[tools."http:tsgo".platforms]
macos-arm64 = { url = "https://github.com/colelawrence/typescript-go/releases/download/7.0.0-dev.20241108.1/tsgo-7.0.0-dev.20241108.1-macos-arm64.tar.gz" }
```

Then run:

```bash
mise install tsgo
tsgo --version
```

## Manual Download

Download the tarball for your platform from the [Releases page](https://github.com/colelawrence/typescript-go/releases):

**Most Common:**
- **macOS (Apple Silicon)**: `tsgo-VERSION-macos-arm64.tar.gz`
- **Linux (x64)**: `tsgo-VERSION-linux-x64.tar.gz`
- **Windows (x64)**: `tsgo-VERSION-windows-x64.tar.gz`

**Also Available:**
- **macOS (Intel)**: `tsgo-VERSION-macos-x64.tar.gz`
- **Linux (ARM64)**: `tsgo-VERSION-linux-arm64.tar.gz`

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

Releases use semver prerelease format: `7.0.0-dev.YYYYMMDD.BUILD`

- `7.0.0-dev` - Base TypeScript version
- `YYYYMMDD` - Release date (UTC)
- `BUILD` - GitHub Actions run number

Example: `7.0.0-dev.20241108.42` = November 8, 2024, build #42

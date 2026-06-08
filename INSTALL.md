# Installing this patched fork

This fork tracks `microsoft/typescript-go` and publishes patched `tsgo` binaries from GitHub Releases.

The fork-specific behavior patch disables declaration portability diagnostics such as TS2742/TS2883 for inferred declaration emit.

## Download latest release

Choose the archive for your platform from the latest release:

- `tsgo-macos-arm64.tar.gz`
- `tsgo-macos-x64.tar.gz`
- `tsgo-linux-x64.tar.gz`
- `tsgo-linux-arm64.tar.gz`
- `tsgo-windows-x64.tar.gz`

Example for macOS Apple Silicon:

```bash
curl -L https://github.com/colelawrence/typescript-go/releases/latest/download/tsgo-macos-arm64.tar.gz | tar xz
./tsgo --version
```

Move `tsgo` or `tsgo.exe` somewhere on your `PATH` if you want it globally available.

## mise / aqua-style HTTP installs

Use the stable release asset URL for your platform, for example:

```toml
[tools."http:tsgo".platforms]
macos-arm64 = { url = "https://github.com/colelawrence/typescript-go/releases/latest/download/tsgo-macos-arm64.tar.gz" }
linux-x64 = { url = "https://github.com/colelawrence/typescript-go/releases/latest/download/tsgo-linux-x64.tar.gz" }
windows-x64 = { url = "https://github.com/colelawrence/typescript-go/releases/latest/download/tsgo-windows-x64.tar.gz" }
```

For reproducible installs, pin to a specific release tag instead of `latest`.

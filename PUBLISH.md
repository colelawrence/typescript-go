# Fork maintenance and publishing

This fork intentionally carries a small patch set on top of `microsoft/typescript-go`.
It is not intended for upstream contribution; the goal is to keep a clean, repeatable fork delta while continuing to track upstream `main`.

## Intended patch stack

1. Disable declaration portability diagnostics for inferred declaration emit.
2. Add fork-specific release publishing and documentation.
3. Disable upstream-only workflows in this fork so only the fork release workflow runs.

## Syncing with upstream

```bash
git fetch upstream origin
git switch main
git merge upstream/main
git push origin main
```

If the history becomes noisy, rebuild the patch stack from upstream:

```bash
git fetch upstream
git switch -c clean-fork-patch upstream/main
# reapply the fork patches as small semantic commits
git push origin clean-fork-patch
```

## Publishing

`.github/workflows/release.yml` publishes prerelease GitHub Releases from pushes to `main` in `colelawrence/typescript-go`.

Release tags use:

```text
7.0.0-dev.YYYYMMDD.RUN_NUMBER
```

Each release uploads stable asset names:

- `tsgo-macos-arm64.tar.gz`
- `tsgo-macos-x64.tar.gz`
- `tsgo-linux-x64.tar.gz`
- `tsgo-linux-arm64.tar.gz`
- `tsgo-windows-x64.tar.gz`
- `checksums.txt`

## Local verification

At minimum, verify the modified package builds/tests:

```bash
go test ./internal/transformers/declarations
```

For broader confidence, run the normal upstream checks as needed:

```bash
npm ci
npx hereby build
npx hereby test
```

# Publishing Guide

This guide explains how to publish a patched version of TypeScript Go to npm.

## Understanding the Build System

TypeScript Go uses:
- **Go** for the compiler (built from `cmd/tsgo`)
- **Hereby** (similar to Gulp) for build tasks defined in `Herebyfile.mjs`
- **npm workspaces** with packages in `_packages/`

The main npm package is `@typescript/native-preview` with platform-specific optional dependencies like `@typescript/native-preview-darwin-arm64`.

## Build Process

### 1. Build the binary locally

```bash
npm run build
# or
npx hereby build
```

This creates `built/local/tsgo` with bundled TypeScript lib files.

### 2. Build npm packages

```bash
npx hereby native-preview:build-packages
```

This:
- Builds cross-platform binaries for all supported platforms (when `--forRelease` is set)
- Builds only your current platform otherwise
- Copies lib files
- Creates package.json files with proper metadata
- Outputs to `built/npm/`

### 3. Pack packages

```bash
npx hereby native-preview:pack-packages
```

This creates `.tgz` files ready for npm publishing in `built/npm/`.

## Manual Publishing (Local)

1. Build and pack packages:
```bash
npm ci
npm run build
npx hereby native-preview:build-packages
npx hereby native-preview:pack-packages
```

2. Login to npm:
```bash
npm login
```

3. Publish (replace with your package name if you forked):
```bash
cd built/npm
# Publish platform package first
npm publish native-preview-darwin-arm64.tgz --tag patched --access public
# Then main package
npm publish native-preview.tgz --tag patched --access public
```

## GitHub Actions Workflow

The repository includes a `.github/workflows/publish.yml` workflow for one-click publishing:

1. Go to Actions → Publish Package
2. Click "Run workflow"
3. Enter version (e.g., `0.1.0-patch.1`)
4. Enter npm tag (e.g., `patched`)
5. Click "Run workflow"

**Prerequisites:**
- Set `NPM_TOKEN` secret in repository settings with your npm publish token

## Versioning Strategy

For patched versions:
- Use format: `0.1.0-patch.1`, `0.1.0-patch.2`, etc.
- Use npm tag `patched` to avoid conflicting with official releases
- Users can install with: `npm install @typescript/native-preview@patched`

## Forking and Publishing Under Your Own Scope

If you want to publish under your own npm organization:

1. Fork the repository

2. Update package names in:
   - `_packages/native-preview/package.json`
   - `Herebyfile.mjs` (search for `@typescript/native-preview`)

3. Change scope from `@typescript` to your own (e.g., `@yourname`)

4. Update repository URLs in package.json

5. Build and publish as described above

## Upstream Sync

To sync with upstream and rebuild:

```bash
# Add upstream if not already added
git remote add upstream https://github.com/microsoft/typescript-go.git

# Sync with upstream
git fetch upstream
git merge upstream/main

# Rebuild with your patches
npm run build
npx hereby native-preview:pack-packages

# Publish new version
```

## Testing the Package

Test locally before publishing:

```bash
cd built/npm
npm install -g ./native-preview.tgz
npx tsgo --version
```

## Current Patches

This repository includes the following patches:
- **TS2742 disabled**: Removed the "inferred type cannot be named" error in `internal/transformers/declarations/tracker.go`

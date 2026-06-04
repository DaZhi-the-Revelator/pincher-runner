# pincher-runner

GitHub Actions build system for [Pincher](https://codeberg.org/DaZhi-the-Revelator/pincher), the Arturo language server.

Produces Linux, Windows, and macOS binaries and publishes them as a Codeberg release whenever a `v`-prefixed tag is pushed to the Pincher repository on Codeberg.

## How It Works

1. A `v*` tag is pushed to Pincher on Codeberg.
2. Pincher's `.forgejo/workflows/release.yml` dispatches a `workflow_dispatch` event to this repository via the GitHub API, passing the tag as `pincher_ref`.
3. The `build.yml` workflow here checks out that tag, builds binaries for all three platforms, and publishes a release back to Codeberg.

## Secrets

| Secret | Description |
|--------|-------------|
| `CODEBERG_TOKEN` | Codeberg API token with release write access to the Pincher repository |

The `GH_PAT` secret lives in the Pincher Codeberg repository and is used there to dispatch to this workflow.

## Artifacts

| File | Platform |
|------|----------|
| `pincher-linux-x86_64.tar.gz` | Linux x86-64 |
| `pincher-windows-x86_64.zip` | Windows x86-64 |
| `pincher-macos-arm64.tar.gz` | macOS Apple Silicon |
| `pincher-macos-x86_64.tar.gz` | macOS Intel |

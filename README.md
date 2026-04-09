# gameflow-setup-action

[![GitHub release (latest SemVer)](https://img.shields.io/github/v/release/GameFlowGG/gameflow-setup-action?sort=semver)](https://github.com/GameFlowGG/gameflow-setup-action/releases)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](./LICENSE)

A GitHub Action that downloads and installs the [GameFlow CLI](https://gameflow.gg) on your runner, with optional API key authentication. Use it as a first step in any workflow that deploys or interacts with GameFlow.

---

## Prerequisites

- A GitHub Actions runner (Linux, macOS, or Windows with WSL)
- `curl` and `sh` available on the runner (present by default on all GitHub-hosted runners)
- A GameFlow account and API key if you need authenticated operations

---

## Usage

### Minimal — install only, no authentication

```yaml
- uses: GameFlowGG/gameflow-setup-action@v1
```

### With authentication

```yaml
- uses: GameFlowGG/gameflow-setup-action@v1
  with:
    api-key: ${{ secrets.GAMEFLOW_API_KEY }}
```

### Full workflow — install, authenticate, then deploy

```yaml
name: Deploy to GameFlow

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - uses: GameFlowGG/gameflow-setup-action@v1
        with:
          api-key: ${{ secrets.GAMEFLOW_API_KEY }}

      - uses: GameFlowGG/gameflow-deploy-action@v1
        with:
          project: my-game
```

---

## Inputs

| Name      | Description                                                                                          | Required | Default  |
|-----------|------------------------------------------------------------------------------------------------------|----------|----------|
| `version` | CLI version to install. **Reserved for future use — see Known Limitations below.**                  | No       | `latest` |
| `api-key` | GameFlow API key. When provided, the action runs `gameflow login --api-key <key>` after install. The key is automatically masked in all log output. | No | — |

---

## Known Limitations

### Version pinning is not yet supported

The `version` input is accepted for forward-compatibility but has **no effect** in the current release. The installer script at `https://install.gameflow.gg` always installs the latest available CLI release, regardless of the value passed.

Version pinning (e.g. `version: "1.4.2"`) will be implemented in a future release once the installer script supports it.

**Workaround:** Pin the version of this action itself (e.g. `@v1.2.0`) to freeze the workflow, and monitor the [GameFlow CLI releases](https://github.com/GameFlowGG/gameflow-cli/releases) for breaking changes.

---

## Versioning

This action follows [Semantic Versioning](https://semver.org).

| Reference       | Meaning                                               |
|-----------------|-------------------------------------------------------|
| `@v1`           | Latest `v1.x.x` release — receives non-breaking updates automatically |
| `@v1.2.0`       | Exact release — pinned, never changes                |

**Breaking changes** (removed inputs, changed behavior, renamed outputs) always result in a new **major** version. You will never be broken by updating within the same major version (e.g. `v1` → `v1.3.0`).

---

## Documentation

Full GameFlow documentation is available at [https://docs.gameflow.gg](https://docs.gameflow.gg).

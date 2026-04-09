# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [1.0.0] - 2026-04-09

### Added
- Composite action (`action.yml`) that installs the GameFlow CLI via the official
  installer script (`https://install.gameflow.gg`).
- `version` input (reserved for future version-pinning support; currently a no-op).
- `api-key` input: when provided, masks the key in logs and runs
  `gameflow login --api-key <key>`.
- Installation verification step (`gameflow --version`).
- CI workflow (`.github/workflows/test.yml`) that exercises the action on every
  push and pull request.
- Release workflow (`.github/workflows/release.yml`) that automatically keeps
  the floating major tag (e.g. `v1`) pointing to the latest `v1.x.x` release.
- MIT license.
- This changelog.

[Unreleased]: https://github.com/GameFlowGG/gameflow-setup-action/compare/v1.0.0...HEAD
[1.0.0]: https://github.com/GameFlowGG/gameflow-setup-action/releases/tag/v1.0.0

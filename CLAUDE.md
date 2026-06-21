# GameFlow Setup Action — Agent Guide

## Project Overview

GitHub Action that installs and configures the GameFlow CLI in a CI/CD workflow.

## Repository Structure

```
gameflow-setup-action/
├── action.yml        # Action definition
├── CHANGELOG.md
└── README.md
```

## Editing the Action

- All logic is defined in `action.yml`.
- Keep inputs backward-compatible; bump the major version tag for breaking changes.
- Update `CHANGELOG.md` and `README.md` when inputs/outputs change.

## Git & Commits

- Commit format: `type(scope): description`
  - Example: `feat(action): support custom CLI version pin`
- Tag releases with `vMAJOR.MINOR.PATCH`; update the major floating tag after each release.

## AI Workflow

### Required plugins

```
/plugin install superpowers@claude-plugins-official
/plugin install security-guidance@claude-plugins-official
/plugin install code-review@claude-plugins-official
```

### Plugin detection (run at session start)

Before doing anything else, check the skills available in your session. Each required plugin exposes a known skill — if it is absent, the plugin is not installed.

| Plugin | Skill to look for |
|---|---|
| `superpowers@claude-plugins-official` | `superpowers:brainstorming` |
| `security-guidance@claude-plugins-official` | `security-review` |
| `code-review@claude-plugins-official` | `code-review` |

If any skill is missing, **stop and respond with the exact install commands** before continuing:

```
One or more required plugins are missing. Please run the following, then /reload-plugins:

/plugin install <missing-plugin>@claude-plugins-official
```

Do not proceed with the task until the user confirms the plugins are installed.

### When to use which skill

| Situation | Skill |
|---|---|
| Adding inputs or changing behavior | `/feature-dev` → brainstorm → implement |
| Before opening a PR | `/code-review` + `/security-review` (action runs with CI credentials) |
| PR description | `/release-changelog` |

### AI tool policy

Claude Code is the primary tool. Do not commit plans.

## Security

- Never log sensitive inputs; document that they should be stored as GitHub secrets.

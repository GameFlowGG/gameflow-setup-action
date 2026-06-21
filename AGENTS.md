# GameFlow Setup Action — AI Agent Conventions

> Tool-agnostic guidelines for Cursor, Copilot, Codex, and any other AI assistant.
> Claude Code users: follow CLAUDE.md instead — it supersedes this file.

## Commit Format

```
type(scope): description
```

Example: `feat(action): support custom CLI version pin`

- One logical change per commit
- Tag releases: `vMAJOR.MINOR.PATCH`; update the floating major tag after each release

## Action Conventions

- Keep inputs backward-compatible; breaking changes require a major version bump
- Update `CHANGELOG.md` and `README.md` when inputs/outputs change
- Never log sensitive inputs

## Security

- Never log secret values passed as inputs
- Document that sensitive inputs must be stored as GitHub secrets in the caller

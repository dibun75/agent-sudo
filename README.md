# agent-sudo

> sudo for AI agents.

**agent-sudo** is an open-source permission and safety layer for AI coding agents. It is being designed as a local-first developer tool with a polished terminal/web experience, explicit policies, human approval, and explainable decisions.

> **Naming note:** the repository name is provisional while we validate ecosystem/package-name collisions before the first implementation release.

## Vision

AI coding agents increasingly operate with access to files, shells, network resources, package managers, git, and MCP tools. Developers need a clear boundary between:

- actions that happen automatically
- actions that need approval
- actions that must never happen

agent-sudo aims to make that boundary visible, configurable, and testable.

## Experience

The project will have two complementary interfaces:

- **CLI/TUI:** fast, keyboard-first, suitable for SSH and remote development
- **Local web UI:** live agent activity, pending approvals, policy state, decision history, and explanations

The visual language will be **retro-futuristic terminal / CRT inspired**, while keeping accessibility, readability, and information density appropriate for a serious developer tool.

## Design goals

- One-command startup
- Safe defaults
- Explicit least-privilege policies
- Human approval for ambiguous or consequential actions
- Deterministic enforcement for hard rules
- Optional semantic judgement with Jev
- Local-first telemetry
- Explainable decision records
- Replayable tests and benchmark scenarios
- Clear integration paths for coding agents and MCP

## Planned usage

```bash
agent-sudo <agent-command>
```

Examples:

```bash
agent-sudo claude
agent-sudo codex
agent-sudo opencode
```

Example policy:

```yaml
filesystem:
  read: allow
  write: allow
  delete: ask

shell:
  tests: allow
  git: allow
  package_install: ask
  destructive: deny

network:
  localhost: allow
  approved: allow
  unknown: ask

secrets:
  ssh_keys: deny
  env_files: deny
```

## Documentation

- [Architecture](docs/ARCHITECTURE.md)
- [Threat model](docs/THREAT_MODEL.md)
- [UI design](docs/UI_DESIGN.md)
- [Testing strategy](docs/TESTING_STRATEGY.md)
- [Roadmap](docs/ROADMAP.md)

## Status

🚧 Early design / pre-implementation.

The initial milestone is a local wrapper and policy engine that can observe and classify actions without silently weakening the operating system's security model.

## Security principles

1. **Fail closed for high-risk actions.**
2. **Never treat an agent's own judgement as an authorization boundary.**
3. **Never weaken OS-level security boundaries.**
4. **Redact secrets before persistent logging.**
5. **Keep sensitive telemetry local by default.**
6. **Jev is optional and cannot override a hard deny.**

## License

Apache-2.0

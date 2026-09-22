# agent-sudo

> sudo for AI agents.

**agent-sudo** is an open-source permission and safety layer for AI coding agents. It intercepts sensitive actions, applies deterministic policies, optionally asks a semantic decision engine, and records an auditable decision trail.

## Why

AI coding agents can read files, execute commands, access environment variables, install packages, and make network requests. Humans need a simple way to define what an agent may do automatically, what requires approval, and what must never happen.

## Goals

- One simple command to wrap an agent
- Explicit permissions for filesystem, shell, network, secrets, and package operations
- Safe defaults
- Human approval for ambiguous actions
- Deterministic policy enforcement
- Optional semantic decisions with Jev
- Local-first operation and auditable logs
- Support for multiple coding agents

## Planned usage

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

## Status

🚧 Early project. The repository is currently being designed before implementation.

The first milestone is a local CLI that can safely wrap a child process and record proposed/observed actions without changing the user's normal workflow.

## Design principles

1. **Fail closed for high-risk actions.**
2. **Never weaken OS-level security boundaries.**
3. **Make every decision explainable.**
4. **Keep sensitive telemetry local by default.**
5. **Jev is optional, not a hard dependency.**

## License

Apache-2.0

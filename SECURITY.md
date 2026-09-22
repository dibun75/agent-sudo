# Security Policy

## Reporting a vulnerability

Please do not disclose exploitable vulnerabilities in a public issue.

Until a dedicated security contact is configured, report security-sensitive issues privately through GitHub's repository security features.

## Scope

agent-sudo is intended to reduce accidental or unauthorized actions by AI agents. It is not a replacement for OS isolation, containers, MAC systems, endpoint security, or human review.

A policy decision made by agent-sudo must never be treated as proof that an action is safe.

## Security principles

- least privilege
- fail-closed handling for high-risk operations
- no secret collection by default
- local-first telemetry
- explicit boundaries between policy evaluation and action execution

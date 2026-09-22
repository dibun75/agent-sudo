# Development Guidance

This file defines repository-level guidance for coding agents and contributors.

## Project intent

agent-sudo is a local-first permission and safety layer for AI coding agents.

The project must remain:

- security-first
- deterministic where enforcement is concerned
- explainable
- testable offline
- usable from a terminal
- independent of any single AI vendor

## Before changing code

Read:

- README.md
- docs/ARCHITECTURE.md
- docs/THREAT_MODEL.md
- docs/TESTING_STRATEGY.md

## Non-negotiable rules

1. Never commit secrets or real credentials.
2. Never add telemetry without documenting it.
3. Never make a semantic model the sole enforcement boundary for a hard security rule.
4. Never silently broaden permissions.
5. Add a regression test for security-sensitive bug fixes.
6. Keep external network calls optional in tests.
7. Prefer the smallest change that satisfies the requirement.

## Cursor workflow

For implementation work:

1. inspect the relevant architecture and tests
2. state the intended change in the task/commit
3. implement the smallest coherent change
4. run the focused tests
5. run the full suite before merging
6. update documentation when behaviour changes

Avoid speculative framework abstractions until a concrete integration needs them.

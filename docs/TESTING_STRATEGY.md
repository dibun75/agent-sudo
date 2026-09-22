# Testing Strategy

Security tooling must be tested as a decision system, not just as ordinary application code.

The test strategy is intentionally layered.

## 1. Unit tests

Fast deterministic tests for:

- policy parsing
- action normalization
- path classification
- shell command classification
- secret detection
- rule matching
- decision precedence
- risk classification
- reason-code generation
- log redaction

Unit tests must not require network access.

## 2. Property-based tests

Use generated inputs to test invariants such as:

- a hard DENY cannot become ALLOW because of semantic judgement
- redaction never increases the visibility of secret values
- malformed policies fail closed
- policy ordering cannot bypass a higher-priority deny
- decision records remain serializable
- replaying the same deterministic input produces the same deterministic result

## 3. Integration tests

Exercise complete flows:

```text
agent
  ↓
adapter
  ↓
action normalizer
  ↓
policy engine
  ↓
optional Jev
  ↓
decision
  ↓
approval / execution
  ↓
audit record
```

Required scenarios:

- safe file read → ALLOW
- project-local test command → ALLOW
- delete operation → ASK or DENY according to policy
- credential read → DENY
- unknown network destination → ASK
- hard deny + Jev allow → DENY
- approval expiry → DENY
- malformed policy → safe failure

## 4. End-to-end tests

Run the actual CLI against disposable temporary workspaces.

Example:

```bash
agent-sudo test --scenario secret-read
agent-sudo test --scenario destructive-command
agent-sudo test --scenario approval-expiry
```

The test harness must never run against the developer's real home directory.

## 5. Security regression suite

Every security bug becomes a permanent regression test.

Each case should record:

- scenario ID
- threat category
- expected decision
- observed decision
- relevant policy
- reproduction steps

## 6. Jev tests

Jev is an optional semantic layer.

Tests must distinguish:

- provider/model behaviour
- deterministic policy behaviour
- final enforcement behaviour

A Jev response must never override a hard policy deny.

Where practical, store deterministic fixtures for representative Jev responses so the core suite remains offline and reproducible.

## 7. Fuzzing

Fuzz security-sensitive parsers and normalizers:

- shell strings
- paths
- YAML/TOML/JSON policies
- tool-call arguments
- malformed MCP payloads
- Unicode and path traversal cases

The goal is to discover parser differentials where two layers interpret the same action differently.

## 8. Performance tests

Measure:

- policy evaluation latency
- action normalization latency
- log write latency
- approval round-trip latency
- memory overhead for long agent sessions

Publish baseline measurements once the architecture stabilizes.

## 9. CI quality gates

Every pull request should run:

```text
format
lint
type-check
unit tests
property tests
integration tests
security regression tests
build/package checks
```

Security-sensitive changes should additionally require explicit review notes.

## 10. Testing philosophy

The project should prefer:

> deterministic tests for enforcement, controlled fixtures for semantic judgement, and end-to-end tests for real-world behaviour.

The test suite is part of the product. Contributors should be able to understand why a test exists, what threat it represents, and what security property it protects.

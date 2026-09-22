# Architecture

agent-sudo will sit between an AI agent and the capabilities that the agent can invoke.

```text
AI coding agent
      |
      v
agent-sudo adapter
      |
      v
Action normalizer
      |
      +------------------+
      |                  |
      v                  v
Policy engine       Optional Jev judge
      |                  |
      +--------+---------+
               v
       Decision: ALLOW / ASK / DENY
               |
        +------+------+
        |             |
        v             v
   approval UI     audit log
```

## Core components

### Adapter

Connects an agent to agent-sudo and converts agent/tool activity into a common action model.

### Action model

A normalized representation of an attempted operation:

- actor
- action type
- target
- arguments or metadata
- working directory
- timestamp
- correlation/session ID

Sensitive payloads should be redacted before persistence.

### Policy engine

Evaluates deterministic rules first. This layer owns hard guarantees such as:

- deny access to known secret paths
- require approval for destructive operations
- permit safe project-local operations

### Jev judge

An optional semantic layer for questions that are difficult to encode as deterministic rules, such as whether an action appears consistent with the user's stated intent.

Jev must not override hard deny policies.

### Decision record

Every evaluated action should produce a structured decision containing the policy result, optional semantic result, final outcome, reason codes, and timing information.

### Execution boundary

agent-sudo should avoid implementing its own privileged execution mechanism. Where possible, it should use OS-native process controls and explicit wrappers.

## Initial non-goals

- replacing Linux permissions
- sandboxing arbitrary untrusted code by itself
- becoming a cloud telemetry service
- forcing a specific LLM or agent vendor
- silently modifying agent behavior

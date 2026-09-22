# Threat Model

## Assets

- source code
- credentials and tokens
- SSH keys
- cloud credentials
- environment variables
- local files
- network access
- developer intent and task context

## Threats

### Credential access

An agent attempts to read sensitive files or environment values that are outside the task scope.

### Destructive execution

An agent executes commands that delete data, rewrite history, or damage the development environment.

### Data exfiltration

An agent transmits local information to an unapproved remote destination.

### Scope drift

An agent begins performing actions that are not materially related to the user's request.

### Policy bypass

An agent attempts to invoke a capability through a path that the policy engine did not classify.

## Trust boundaries

1. The user is trusted to configure policy, but configuration itself must be validated.
2. The agent is not trusted merely because it is a well-known coding agent.
3. Semantic judgements are advisory unless explicitly configured otherwise.
4. The operating system remains the ultimate enforcement boundary.

## Security requirement

No semantic model or Jev judgement may silently weaken an explicit deny rule.

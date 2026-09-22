# UI Design

## Product character

agent-sudo should feel like a serious developer security tool with a memorable visual identity.

Direction:

> **retro-futuristic operations console**

The reference mood is a modern terminal crossed with a late-70s/80s computing control room: restrained CRT cues, strong typography, compact status indicators, and clear hierarchy.

The UI must remain useful over SSH, on small screens, and during stressful approval decisions.

## Two surfaces

### 1. TUI

The terminal interface is the primary operational surface.

Principles:

- keyboard-first
- no mouse required
- works over SSH
- low bandwidth
- readable without color
- concise status lines
- clear destructive-action warnings
- explicit approval prompts

Example:

```text
AGENT-SUDO // SESSION 0042
────────────────────────────────────────────
AGENT     Claude Code
PROJECT   ~/src/demo
STATUS    ● ACTIVE

PENDING ACTION

  SHELL
  rm -rf ./dist

  Risk        CRITICAL
  Target      ~/src/demo/dist
  Policy      destructive = DENY

  [D] DENY    [A] ALLOW ONCE    [E] EXPLAIN
────────────────────────────────────────────
```

### 2. Local web UI

The browser dashboard is for inspection and configuration.

Primary views:

1. Live session
2. Pending approvals
3. Policy editor
4. Decision history
5. Decision detail
6. Replay / test run

A useful dashboard should answer, at a glance:

- Which agent is active?
- What is it trying to do?
- What has been allowed?
- What is waiting for me?
- What has been blocked?
- Why?

## Visual language

Use retro cues as accents rather than decoration:

- terminal-inspired typeface
- monospaced data
- thin grid lines
- status lamps
- subtle scanline/noise treatment
- compact command prompts
- geometric iconography
- sparse animation
- strong spacing and hierarchy

Avoid:

- excessive glow
- illegible neon text
- fake “hacker” imagery
- animation that delays a security decision
- color-only security indicators

Every status must remain understandable from text/icon/label alone.

## Accessibility

- WCAG-conscious contrast
- keyboard navigation
- visible focus state
- reduced-motion mode
- screen-reader labels for controls
- text labels for ALLOW / ASK / DENY
- no security decision conveyed by color alone

## Core approval interaction

The approval screen should always expose:

- exact action
- normalized action type
- target/resource
- reason or policy match
- risk classification
- what will happen if approved
- scope of the approval
- expiry, if applicable

Never make the user approve an opaque label such as “tool_call_17”.

## Future visual identity

Potential visual motifs:

- command prompt chevron
- shield + prompt glyph
- monochrome terminal panel
- small permission-card status indicators

Logo work should stay simple enough to render cleanly as:

- GitHub avatar
- terminal icon
- npm package icon
- favicon

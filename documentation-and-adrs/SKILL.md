---
name: documentation-and-adrs
description: Preserves architecture decisions, project knowledge, and agent-facing documentation. Use when decisions are made, architecture changes, onboarding context is missing, or documentation may drift from code.
---

# Documentation and ADRs

## Overview

Documentation reduces comprehension debt when it captures decisions, constraints, and operating knowledge. Agent-facing documentation is part of the build system for AI work: stale docs produce stale code.

## When to Use

- Making an architectural or product decision
- Changing module boundaries, APIs, data models, or workflows
- Adding agent instructions such as `AGENTS.md`
- A reviewer asks "why was this done?"
- A new contributor or agent would struggle to find the right pattern
- Docs no longer match code

## Documentation Layers

| Layer | Purpose | Typical file |
| --- | --- | --- |
| Agent rules | Always-on instructions and commands | `AGENTS.md`, `CLAUDE.md`, `.cursor/rules/*` |
| Architecture decision | Why a decision was made | `docs/adr/NNNN-title.md` |
| Project map | Where things live | `docs/architecture.md` |
| Runbook | How to operate or recover | `docs/runbooks/*.md` |
| Feature spec | What should be built | `docs/specs/*.md` |

Keep always-on agent files short. Put depth in linked docs.

## ADR Template

```markdown
# ADR NNNN: [Decision Title]

Date: YYYY-MM-DD
Status: Proposed | Accepted | Superseded

## Context
[Problem, constraints, and forces.]

## Decision
[The decision in 2-4 sentences.]

## Consequences
- Positive: [...]
- Negative: [...]
- Follow-up: [...]

## Alternatives Considered
- [Alternative] — [why not]
```

## Agent Documentation Checklist

`AGENTS.md` or equivalent should include:

- Build, test, lint, typecheck, and dev commands
- Project structure and ownership boundaries
- Style and naming conventions
- Testing expectations
- Security and dependency rules
- "Ask first" operations
- Links to deeper specs, ADRs, and runbooks

## Drift Prevention

When code changes, check whether these artifacts need updates:

- Public API docs
- Architecture diagrams
- Environment setup
- Build or test commands
- Feature flags
- Runbooks
- Agent instructions
- ADR status

## Red Flags

- Documentation explains what the code says but not why
- `AGENTS.md` contains stale commands
- Multiple docs disagree about the same flow
- Architecture decisions live only in chat or PR comments
- A new agent must rediscover the same project map every session

## Verification

- [ ] Decision-making context is captured
- [ ] Agent-facing commands are current
- [ ] Deep docs are linked from always-on docs
- [ ] Stale or superseded docs are marked
- [ ] A future reviewer can explain why the change exists

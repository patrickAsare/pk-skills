---
name: ci-cd-and-automation
description: Designs CI, release, and automation workflows that make agent changes safe to merge. Use when adding quality gates, build pipelines, deployment checks, or automation around tests, linting, security, and generated artifacts.
---

# CI/CD and Automation

## Overview

CI/CD is the enforcement layer for agent readiness. Agents need fast, deterministic feedback. Humans need gates that prevent unverified code from reaching main. Good automation turns standards into defaults.

## When to Use

- A repo lacks reliable build, lint, typecheck, or test commands
- Adding an agent workflow that creates or reviews code
- Release confidence is low
- Generated files drift
- Security, dependency, or provenance checks need enforcement
- Manual review is doing work automation could do better

## Minimum Quality Gates

Every production repo should have:

- Format or lint check
- Type check or compile check
- Unit and integration test check where applicable
- Build check
- Secret scan
- Dependency vulnerability check
- Generated artifact diff check if codegen exists
- Required review and branch protection

## Agent-Friendly CI Rules

CI should be:

- **Fast**: targeted checks complete quickly enough for iteration
- **Deterministic**: same input produces same result
- **Readable**: failures point to the command and file
- **Layered**: cheap checks run before expensive checks
- **Reproducible**: local commands match CI commands

## Workflow Design

```markdown
Pre-commit:
- Format staged files
- Fast lint

Pull request:
- Lint
- Type check
- Unit tests
- Integration tests
- Build
- Secret scan
- Generated artifact diff

Pre-merge or nightly:
- E2E tests
- Performance regression checks
- Dependency audit
- Security scan
```

## Provenance and Auditability

For agent-generated changes, preserve:

- Prompt or task identifier
- Agent/tool used
- Tests run
- Human reviewer
- Linked spec, issue, or ADR
- Generated-by disclosure when policy requires it

## Automation Backlog

When a manual review comment repeats twice, consider automating it.

Examples:

- Formatting issues -> formatter check
- Missing generated files -> codegen diff check
- Stale docs paths -> link/path validation
- Missing ownership -> `CODEOWNERS`
- Secrets in diffs -> secret scanning

## Red Flags

- CI runs commands different from local docs
- Agents cannot reproduce CI failures locally
- E2E tests are flaky and ignored
- Security scans are optional
- Generated files are not checked
- Branch protection can be bypassed by automation

## Verification

- [ ] Local commands match CI commands
- [ ] Required gates cover build, test, lint, security, and generated artifacts
- [ ] Failures are readable by humans and agents
- [ ] Branch protection and ownership are enforced
- [ ] Release and rollback steps are documented

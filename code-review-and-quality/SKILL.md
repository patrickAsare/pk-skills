---
name: code-review-and-quality
description: Reviews code for correctness, maintainability, regressions, and agent-induced quality issues. Use before merging code, after agent-generated changes, when reviewing pull requests, or when a change touches shared behavior.
---

# Code Review and Quality

## Overview

Review code as a risk-control step, not a style pass. Agent-generated code often looks plausible while hiding incorrect assumptions, duplicated logic, weak tests, and unclear ownership. A good review asks: does this change do the right thing, in the right place, with enough evidence that it works?

## When to Use

- Reviewing a pull request or diff
- Reviewing any agent-generated implementation
- Touching shared modules, public APIs, data models, auth, billing, or deployment behavior
- A change is large enough that the reviewer cannot hold it all in memory
- Tests pass but the design or intent is unclear

## Review Order

### 1. Reconstruct Intent

Before judging code, identify what the change claims to do.

- Read the issue, spec, PR description, or task prompt
- Identify the user-visible behavior and non-goals
- Note any unstated assumptions
- If intent is unclear, stop and ask for clarification

### 2. Check Behavioral Correctness

Look for mismatches between intent and implementation.

- Are all acceptance criteria covered?
- Are edge cases handled?
- Are errors surfaced consistently?
- Are permissions and tenancy boundaries preserved?
- Does the implementation change existing behavior unintentionally?

### 3. Check Integration Boundaries

Review the seams where defects concentrate.

- API request and response shapes
- Database reads, writes, indexes, and transactions
- Third-party service calls and retries
- Background jobs, queues, and async workflows
- Feature flags and rollout behavior

### 4. Check Maintainability

Prefer boring, local, obvious code.

- Is the change smaller than it could be?
- Are abstractions justified by real duplication or complexity?
- Are names clear enough that comments are not doing all the work?
- Are dependencies moving in the right direction?
- Is ownership obvious?

### 5. Check Agent-Specific Failure Modes

Agents tend to introduce specific debt patterns:

- Parallel helper functions that already exist elsewhere
- Unused or half-wired code paths
- Over-broad error handling that hides real failures
- Inconsistent naming or style from copied examples
- Tests that assert implementation details instead of behavior
- Documentation that says what changed but not why

## Review Checklist

- [ ] The change matches the spec, issue, or stated intent
- [ ] The smallest reasonable surface area changed
- [ ] Existing patterns were followed
- [ ] No duplicate implementation was introduced
- [ ] Public interfaces remain backward compatible or have a migration path
- [ ] Error states and edge cases are handled
- [ ] Security and authorization boundaries are preserved
- [ ] Tests cover the behavior at the right level
- [ ] Build, lint, type check, and relevant tests pass
- [ ] Documentation, comments, or ADRs were updated where the decision matters

## Finding Format

Prioritize concrete defects over preferences.

```markdown
[P1] Missing authorization check before updating organization settings

The endpoint validates that the user is authenticated, but it does not verify that
the user belongs to the target organization. This lets any signed-in user update
another tenant's settings if they know the organization ID. Add an organization
membership or role check before calling the update service.
```

Use priorities:

- **P0**: Security issue, data loss, production outage, or cannot ship
- **P1**: High-risk bug or likely regression
- **P2**: Maintainability, missing test, confusing behavior, moderate risk
- **P3**: Minor polish or non-blocking improvement

## Review Output

Lead with findings. If there are no findings, say that directly and note residual risk.

```markdown
Findings:
- [P1] ...
- [P2] ...

Open questions:
- ...

Residual risk:
- Tests do not cover the cross-browser path.
```

## Red Flags

- Reviewing only style and ignoring behavior
- Trusting generated tests without checking what they prove
- Approving a change whose intent is unclear
- Accepting a large rewrite when a small patch would work
- Letting "tests pass" replace code comprehension
- Missing generated-code provenance or license concerns

## Verification

After review, make sure the merge decision is evidence-based:

- [ ] The diff was read against the stated intent
- [ ] Important findings include file and line references
- [ ] Required verification commands are named
- [ ] Any missing tests or docs are explicit
- [ ] Reviewer can explain what changed and why

---
name: test-driven-verification
description: Designs and verifies realistic tests for agent-generated or high-risk changes. Use when adding features, fixing bugs, proving correctness, evaluating test coverage, or reducing verification debt.
---

# Test-Driven Verification

## Overview

Verification debt appears when the team cannot prove that a change works. This skill makes tests evidence, not ceremony. Prefer behavior-focused tests that would fail for the bug or missing feature and pass only when the system really works.

## When to Use

- Building a feature with acceptance criteria
- Fixing a bug or regression
- Reviewing agent-generated tests
- A change touches multiple layers
- Coverage exists but confidence is low
- End-to-end behavior matters more than isolated functions

## Test Level Heuristic

Use the highest-value test that proves the risk.

| Risk | Preferred proof |
| --- | --- |
| User workflow can break | End-to-end test |
| API contract can break | Integration or contract test |
| Data behavior can break | Integration test with realistic fixtures |
| Pure logic can break | Unit test |
| Regression already happened | Regression test that fails before the fix |
| Security boundary can break | Abuse-case test |

Do not add unit tests just because they are cheap. Add the test that catches the failure users or operators would care about.

## Workflow

### 1. Define What Must Be Proven

Write the proof target before writing tests.

```markdown
Behavior to prove:
- A project admin can invite a member.
- A non-admin cannot invite a member.
- Duplicate invites return a conflict and do not send another email.
```

### 2. Write or Identify the Failing Check

For bug fixes, prove the bug exists first. For new features, write the acceptance test or contract check first when practical.

### 3. Use Realistic Data

Prefer fixtures that include:

- Multiple users or tenants
- Empty, normal, and boundary cases
- Existing records that could conflict
- Permission differences
- Realistic timestamps, IDs, and external-service responses

### 4. Track Test Provenance

Every important test should be traceable to one of:

- Requirement or acceptance criterion
- Bug report or incident
- Security boundary
- Refactoring guard
- Contract with another system

Add a short comment only when the provenance is not obvious.

```typescript
// Regression: duplicate invites previously sent two emails.
it('does not send a second invite for an existing pending member', async () => {
  ...
});
```

### 5. Verify The Right Scope

Run the smallest relevant check first, then broaden.

```bash
# Targeted check
npm test -- invite

# Integration or e2e check
npm run test:e2e -- invite

# Full confidence check before merge
npm run lint
npm run typecheck
npm test
npm run build
```

## Reviewing Agent-Written Tests

Reject tests that:

- Assert mocks instead of user-visible behavior
- Recreate the implementation in the assertion
- Only test the happy path
- Use impossible fixtures
- Pass if the feature is not actually wired up
- Increase coverage without increasing confidence

Ask:

- Would this test fail if the feature were removed?
- Would it fail for the bug we are worried about?
- Does it exercise the real integration boundary?
- Does it prove permissions, failure states, and edge cases?

## Verification Report

End verification work with a short report:

```markdown
Verified:
- Admin invite workflow passes in e2e.
- Non-admin invite attempt returns 403.
- Duplicate invite regression test fails before the fix and passes after.

Not verified:
- Email provider delivery in production; mocked at integration boundary.
```

## Red Flags

- "Coverage went up" is the only evidence
- Tests pass only because everything is mocked
- No negative or permission tests
- E2E tests do not reflect real user journeys
- The agent changed tests to fit broken code
- Test names describe implementation instead of behavior

## Verification

- [ ] Each important behavior has a proof target
- [ ] The test level matches the risk
- [ ] At least one realistic failure path is covered
- [ ] Test provenance is clear
- [ ] The verification command set is documented

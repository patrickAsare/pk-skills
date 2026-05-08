---
name: duplication-detector
description: Detects exact, structural, and conceptual duplication in code and documentation. Use when duplicate logic is suspected, after agent-generated code, before refactoring, or when enforcing a single source of truth.
---

# Duplication Detector

## Overview

Duplication is not just repeated lines. It is repeated responsibility. This skill combines search, structural comparison, and source-of-truth decisions to stop parallel implementations from spreading.

## When to Use

- Agent adds new helpers, schemas, clients, or components
- Same bug appears in multiple places
- Types or interfaces look nearly identical
- Docs describe the same process differently
- Refactoring toward a single source of truth
- Preparing a quality audit

## Detection Workflow

### 1. Search Names And Concepts

Search for:

- Similar function names
- Same domain terms
- Same validation rules
- Same API shape
- Same error messages
- Same SQL or query filters

### 2. Compare Structure

Look for logic that follows the same shape even if names differ:

- Same branches
- Same transformations
- Same field mapping
- Same request construction
- Same lifecycle hooks

### 3. Decide If Duplication Is Harmful

Not all duplication should be removed.

Remove duplication when:

- The same business rule appears twice
- Changes must stay synchronized
- Bugs are likely to recur in both places
- One implementation is clearly canonical

Keep duplication when:

- Similar code serves different business rules
- Extraction would create a vague abstraction
- The shared helper would need too many flags

### 4. Converge

Options:

- Reuse existing helper
- Extract narrow shared function
- Create canonical type or schema
- Delete unused path
- Add docs naming the source of truth
- Add tests around the shared rule

## Optional Tooling

If the repo supports it, use clone-detection tools such as `jscpd` or language-native static analysis. Treat tool output as leads, not truth.

## Report Format

```markdown
Duplicate found:
- `src/invite/validate.ts`
- `src/members/inviteSchema.ts`

Why it matters:
- Both enforce invite email and role rules.
- They disagree on allowed roles.

Recommendation:
- Make `InviteSchema` canonical and import it from both call sites.
```

## Red Flags

- Shared business rules copied into tests and production code
- Multiple API clients for the same service
- Multiple schemas for the same payload
- Same docs in README, wiki, and agent rules
- "Temporary" duplicate path has no removal criteria

## Verification

- [ ] Similar concepts were searched
- [ ] Harmful duplication is distinguished from acceptable repetition
- [ ] A canonical source is named
- [ ] Tests protect the shared behavior
- [ ] Old duplicate paths are removed or deprecated

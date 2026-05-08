---
name: code-simplification-and-deduplication
description: Reduces complexity, duplicate code, and agent-created parallel implementations. Use during refactors, after agent-generated code, when code feels hard to understand, or when multiple paths do the same thing.
---

# Code Simplification and Deduplication

## Overview

Agents often solve locally and duplicate globally. This skill turns plausible first-draft code into maintainable second-draft code by removing unnecessary abstraction, converging duplicate implementations, and preserving one source of truth.

## When to Use

- A change introduced new helpers, types, or services
- Similar logic exists in multiple places
- Files or functions are too large to reason about
- The agent created a new path instead of reusing an old one
- Code review finds "this already exists"
- Refactoring is needed before adding new behavior

## Simplification Pass

### 1. Find Existing Patterns

Before creating shared code, search for:

- Similar functions
- Similar types or schemas
- Existing validators
- Existing API clients
- Existing UI components
- Existing error handling

### 2. Classify Duplication

| Type | Response |
| --- | --- |
| Exact duplicate | Replace with shared function or remove one path |
| Structural duplicate | Extract a narrow shared helper |
| Conceptual duplicate | Choose one canonical model or name |
| Accidental similarity | Leave separate until the abstraction is obvious |

Do not extract abstractions just because two blocks look alike. Extract when the same rule must stay consistent.

### 3. Remove Unused Surface Area

Look for:

- Unused parameters
- Dead branches
- Generic abstractions with one caller
- Configuration options no one uses
- Types that mirror other types without adding meaning
- Compatibility layers with no active consumers

### 4. Preserve Behavior

Simplification is only safe when guarded.

- Add characterization tests before risky refactors
- Keep public interfaces stable
- Refactor in small increments
- Run targeted tests after each change

## Review Questions

- What is the single source of truth?
- Can this be expressed with fewer concepts?
- Is this abstraction earning its cost?
- Does this duplicate an existing pattern?
- Will a new engineer understand this in six months?
- Would deleting code make the system clearer?

## Common Agent Smells

- New `utils.ts` with functions that already exist
- New API client instead of extending the existing one
- Type conversions between nearly identical shapes
- "Manager", "handler", or "service" classes with vague ownership
- Defensive branches for impossible states
- Large generated code blocks with no tests

## Deduplication Report

```markdown
Simplified:
- Reused `parseDateRange` instead of adding `normalizeDateWindow`.
- Removed unused `mode` option from the new export path.
- Merged duplicate invite validation into `InviteSchema`.

Left separate:
- Billing and reporting date formatting look similar but follow different business rules.
```

## Verification

- [ ] Existing patterns were searched first
- [ ] Duplicate logic was classified
- [ ] Public behavior remains stable
- [ ] Tests or characterization checks protect the refactor
- [ ] The resulting code has fewer concepts or clearer ownership

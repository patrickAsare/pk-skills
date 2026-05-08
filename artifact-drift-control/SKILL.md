---
name: artifact-drift-control
description: Finds and fixes stale agent context, docs, specs, generated artifacts, and duplicated sources of truth. Use when instructions, docs, schemas, generated files, or examples may be out of sync with code.
---

# Artifact Drift Control

## Overview

Artifact drift happens when agents act on stale or conflicting knowledge. The fix is to identify authoritative sources, compare dependent artifacts against them, and update or retire anything stale.

## When to Use

- Agent output follows old patterns
- Build commands, docs, or examples no longer work
- Specs disagree with implementation
- Generated files may be out of date
- Multiple files claim to be the source of truth
- A large refactor changed paths, APIs, or workflows

## Source-of-Truth Map

Start by naming the authority for each artifact type.

| Artifact | Source of truth |
| --- | --- |
| API schema | OpenAPI, GraphQL schema, route definitions, or types |
| Database shape | Migrations and schema files |
| Build commands | Package scripts, Makefile, CI config |
| Agent rules | `AGENTS.md` plus linked skills |
| Feature behavior | Accepted spec and tests |
| Generated code | Generator config and source inputs |

If no owner exists, create one before updating dependents.

## Drift Audit Workflow

### 1. Inventory

List artifacts likely to drift:

- Docs and READMEs
- Agent rules
- Specs and ADRs
- Generated clients or types
- Test fixtures
- Example code
- CI scripts
- Diagrams

### 2. Compare Against Authority

Use structured checks where possible:

- Run codegen and check for diffs
- Run docs examples as commands
- Validate links and paths
- Compare schema references to real schema
- Check CI commands against local scripts

### 3. Resolve

For each drift item:

- Update it if it is still useful
- Mark it superseded if historical
- Delete or archive it if harmful
- Add a guard if the drift can recur

### 4. Add Review Cadence

Important agent-facing docs should include:

```markdown
Last reviewed: YYYY-MM-DD
Review cadence: quarterly
Owner: Platform Engineering
```

## Drift Report

```markdown
Artifact drift findings:
- `AGENTS.md` references `npm run typecheck`, but package.json uses `npm run check-types`.
- `docs/api.md` documents `POST /invite`, but the route is now `POST /members/invite`.
- Generated SDK was stale; regenerated from schema.

Guards added:
- CI now checks generated client diff.
```

## Red Flags

- Two docs give different setup commands
- Agent rules reference deleted paths
- Generated files are manually edited
- Example code cannot compile
- Tests use fixtures no longer possible in production
- ADRs are accepted but implementation chose another path

## Verification

- [ ] Source-of-truth map exists
- [ ] Stale artifacts were updated, superseded, or removed
- [ ] Commands and examples were checked
- [ ] Generated artifacts were regenerated or validated
- [ ] A guard exists for recurring drift

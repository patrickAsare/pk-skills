---
name: architecture-map
description: Builds a concise map of a codebase, its modules, dependencies, flows, and ownership. Use when onboarding, planning large changes, reducing comprehension debt, or preparing agents for work in unfamiliar systems.
---

# Architecture Map

## Overview

An architecture map gives humans and agents a shared mental model of the system. It should be small enough to read, accurate enough to trust, and linked to real files.

## When to Use

- Starting work in an unfamiliar repository
- Planning a cross-cutting change
- Onboarding engineers or agents
- A system has grown hard to explain
- Multiple modules duplicate responsibilities
- Preparing technical presentation material

## Mapping Workflow

### 1. Inventory The Repo

Capture:

- Top-level directories
- Main application entry points
- Build and test commands
- Frameworks and runtimes
- Data stores and external services

### 2. Identify Domains

Group files by responsibility, not just folder.

```markdown
Authentication:
- Routes: `src/routes/auth.ts`
- Service: `src/auth/service.ts`
- Tests: `src/auth/auth.test.ts`

Billing:
- Webhooks: `src/billing/webhooks.ts`
- Invoices: `src/billing/invoices.ts`
```

### 3. Trace Key Flows

Document the few flows that matter most:

- Request lifecycle
- Authentication and authorization
- Background jobs
- Data writes
- Deployment path
- Error and logging path

### 4. Mark Ownership And Risk

For each domain, capture:

- Owner or team
- Key dependencies
- Known debt
- Test confidence
- Operational risk

## Output Template

```markdown
# Architecture Map: [System]

## Commands
- Build:
- Test:
- Dev:

## Domains
| Domain | Files | Owner | Notes |
| --- | --- | --- | --- |

## Key Flows
### [Flow Name]
1. ...

## Dependency Notes

## Known Risks

## Questions
```

## Red Flags

- Map describes folder names but not responsibilities
- No links to real files
- No owner or risk notes
- Generated diagram is prettier than it is useful
- Map is not updated after architecture changes

## Verification

- [ ] Main domains are named
- [ ] Key files are linked
- [ ] Important flows are traceable
- [ ] Ownership and risk are visible
- [ ] Map is short enough to load as agent context

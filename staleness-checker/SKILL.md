---
name: staleness-checker
description: Checks docs, skills, examples, and agent instructions for age, broken references, and outdated commands. Use when maintaining skills, AGENTS.md, READMEs, specs, or presentation material.
---

# Staleness Checker

## Overview

Staleness checks prevent agents from following old instructions. This skill defines a lightweight review process and metadata pattern for docs and skills.

## When to Use

- Maintaining a skill library
- Updating `AGENTS.md`, README, or specs
- Preparing for a presentation or workshop
- A command in docs fails
- File paths or APIs changed
- Docs have not been reviewed recently

## Metadata Pattern

For important docs and skills, add:

```markdown
Last reviewed: YYYY-MM-DD
Review cadence: quarterly
Owner: [team or person]
Source of truth: [file, system, or URL]
```

## Checks

### Command Checks

- Build commands exist
- Test commands exist
- Package scripts match docs
- CI commands match local docs

### Path Checks

- Referenced files exist
- Linked docs exist
- Examples point to current directories
- Generated artifact paths are current

### Policy Checks

- Security guidance is current
- Agent boundaries are still correct
- Deprecated tools are marked
- Review cadence is not overdue

### Content Checks

- Docs do not contradict each other
- Specs match accepted behavior
- ADR status is current
- Examples still compile or run

## Staleness Report

```markdown
Stale:
- `AGENTS.md`: references deleted `npm run check`.
- `docs/setup.md`: last reviewed 8 months ago.

Current:
- `docs/api.md`: routes match current router.

Actions:
- Update setup command.
- Add owner and review cadence.
```

## Red Flags

- "Last updated" is missing from operational docs
- Commands are described but not executable
- Multiple docs claim to be authoritative
- Skills reference tools no longer installed
- Presentation notes cite sources without dates

## Verification

- [ ] Critical docs have ownership and review cadence
- [ ] Commands and paths were checked
- [ ] Stale docs were updated, marked, or removed
- [ ] Source of truth is named

---
name: deprecation-and-migration
description: Safely migrates APIs, schemas, dependencies, and legacy code without breaking consumers. Use when removing old behavior, changing contracts, migrating data, or replacing legacy systems.
---

# Deprecation and Migration

## Overview

Migration work is where technical debt often becomes production risk. This skill makes change reversible, observable, and consumer-aware.

## When to Use

- Changing public APIs or module contracts
- Migrating database schemas or data
- Replacing legacy code paths
- Removing deprecated fields, flags, or endpoints
- Upgrading major dependencies
- Consolidating duplicated systems

## Migration Plan

### 1. Inventory Consumers

Identify:

- Internal callers
- External API consumers
- Jobs and automations
- Dashboards and reports
- Tests and fixtures
- Documentation and examples

### 2. Choose A Strategy

| Change type | Strategy |
| --- | --- |
| Additive API change | Add optional field or endpoint first |
| Breaking API change | Version, dual-read, or compatibility adapter |
| Database change | Expand, backfill, switch, contract |
| Dependency upgrade | Compatibility test matrix |
| Legacy path removal | Usage logging, warning period, then removal |

### 3. Make It Observable

Track:

- Old path usage
- New path usage
- Error rates
- Latency
- Data mismatch counts
- Rollback signals

### 4. Roll Out Gradually

Use feature flags, canaries, or progressive rollout where possible.

```markdown
Phase 1: Add new path behind flag.
Phase 2: Dual-write or dual-read.
Phase 3: Backfill and compare.
Phase 4: Switch default.
Phase 5: Remove old path after usage is zero.
```

## Migration Checklist

- [ ] Consumers are inventoried
- [ ] Backward compatibility plan exists
- [ ] Data migration is reversible or recoverable
- [ ] Rollback path is documented
- [ ] Observability exists before rollout
- [ ] Docs, tests, and agent rules are updated
- [ ] Removal criteria are explicit

## Red Flags

- Big-bang migration with no rollback
- Removing fields before measuring usage
- Data migration has no validation query
- Tests cover only the new path
- Docs still teach the old path
- Agent rules point to deprecated APIs

## Verification

- [ ] Old and new behavior are both tested during transition
- [ ] Migration can be paused safely
- [ ] Backfill results are validated
- [ ] Rollout has clear stop/go metrics
- [ ] Deprecation is communicated in docs or release notes

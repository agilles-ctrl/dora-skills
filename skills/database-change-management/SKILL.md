---
name: database-change-management
description: Use when writing database migrations, planning schema changes, or integrating database work into the software delivery pipeline — zero-downtime database deployments.
---

# Database Change Management

## DORA Research Context

DORA research found that storing database changes as scripts in version control, managing them like application changes, discussing changes with DBAs, and ensuring visibility into pending database changes all contribute positively to continuous delivery. Teams that treat database work as a first-class part of the delivery pipeline deploy more reliably. This is a [core model](/research/#core-model) capability.

## What It Is

Database change management integrates database work into the software delivery process so that database changes don't slow down deployments or cause problems. It applies the same rigor to schema changes that teams already apply to application code.

## Problem Solved

Symptoms when this capability is absent:

- Database changes block or slow down deployments
- Schema changes cause production downtime
- Application and database changes are deployed out of sync
- No visibility into who changed what and when in the database

## Key Practices

1. **Store all schema changes as migration scripts in version control** alongside application code.

2. **Manage database changes the same way as application changes** — same review, test, and deploy process.

3. **Discuss changes with DBAs before implementation** — they understand production constraints.

4. **Ensure visibility** into progress of all pending database changes across the team.

5. **Use expand/contract pattern** for zero-downtime changes — add new columns/tables (expand), remove old (contract).

## Common Pitfalls

| Pitfall | Why It Fails | What To Do Instead |
|---------|-------------|-------------------|
| Siloed DBA teams using separate processes | Changes get queued; DBAs become bottleneck | Collaborate with DBAs; use migration-based management |
| Multiple apps sharing the same database schema | Changes break other teams unknowingly | Single version-controlled, self-service mechanism |
| Underestimating architectural effort for migration-based management | Zero-downtime patterns require application changes | Account for this in estimates and planning |

## How to Measure

- **Percentage of failed changes where database changes were a contributing factor:** Measures DB-related risk
- **Extent to which database work contributes to overall lead time:** Identifies DB as a bottleneck
- **Proportion of database changes made in a push-button, fully automated way (goal: 100%):** Measures automation maturity

## Coaching Patterns

1. **Start version-controlling all DB changes** as migration scripts — this alone is the biggest win. Get every schema change into a script in the same repo as the application.

2. **Involve DBAs early** — have them review migration scripts at design time, not gate deployments at release time. Their expertise prevents problems, not blocks progress.

3. **Adopt expand/contract** for zero-downtime schema changes — add the new column or table first, migrate data in the background, deploy code that uses both old and new, then remove the old.

## Migration Patterns

### Expand/Contract — Zero-Downtime Schema Changes

**Before — destructive migration:**

```
// All in one migration file, deployed with the new code:
RENAME COLUMN users.name TO users.full_name
DROP COLUMN users.legacy_score

// If the new code has a bug and must be rolled back:
// old code tries to SELECT users.name → column does not exist → outage
```

**After — expand-contract migration:**

```
// Phase 1 — EXPAND (deploy before new code)
ADD COLUMN users.full_name TEXT
// old code still reads users.name → no breakage
// new code writes to both users.name and users.full_name

// Phase 2 — BACKFILL (run as a background job or separate migration)
UPDATE users SET full_name = name WHERE full_name IS NULL
// both columns exist; both old and new code work

// Phase 3 — CONTRACT (deploy after confirming no code reads old column)
DROP COLUMN users.name
// only after all instances run code that no longer reads users.name
```

### Multi-Phase Migration Checklist

```
Before Phase 1 (Expand):
  [ ] New column is nullable OR has a safe default
  [ ] No NOT NULL constraint added without a default
  [ ] Index created CONCURRENTLY (non-blocking)
  [ ] Application code reviewed: does old code still work?

Before Phase 3 (Contract):
  [ ] Confirmed no running instance reads the old column (check logs, query stats)
  [ ] Backfill verified complete (row count, spot checks)
  [ ] Rollback plan documented if drop must be undone
```

### Dangerous Operations

| Operation | Risk | Safe Alternative |
|-----------|------|-----------------|
| RENAME COLUMN | Old code references old name → crash | Add new column, migrate data, drop old |
| DROP COLUMN | Old code tries to read it → crash | Confirm zero reads first, then drop |
| DROP TABLE | Old code queries it → crash | Rename to archive table, verify, then drop |
| CHANGE COLUMN TYPE | Implicit cast may fail or truncate data | Add new column with new type, migrate, drop old |
| ADD NOT NULL without default | Breaks inserts from old code that doesn't supply the column | Add nullable first, backfill, add constraint after |
| Exclusive table lock | Blocks all reads and writes during migration | Use online schema change tools or CONCURRENTLY |

### Rollback-Safe Migration Rules

| Rule | Guidance |
|------|----------|
| Separate schema deploy from code deploy | Schema changes ship before the code that uses them |
| Always expand before you contract | Add first; remove only after old code is gone |
| New columns must be nullable or have a default | Old INSERT statements don't know about the new column |
| Never rename in production without a transition period | Always add-and-copy, never rename-in-place |
| Verify backfill before contracting | Count rows, check for NULLs, sample-check values |

### Migration Common Mistakes

| Mistake | Problem | Fix |
|---------|---------|-----|
| Rename column in same deploy as code | Rolled-back code reads a column that no longer exists | Three-phase expand-contract across separate deploys |
| Add NOT NULL column without default | Old code inserts fail immediately | Add nullable, backfill, add constraint in a later migration |
| Drop column before removing code references | Any running old instance crashes on read | Remove code references first, deploy, then drop the column |
| Long-running migration that locks the table | All application traffic blocked during migration | Use batched updates; use CONCURRENTLY for index creation |
| Skipping the backfill verification step | Nulls or stale data in the new column cause silent bugs | Assert row counts match and sample-check values before dropping old column |

## Related Skills

- [`continuous-delivery`](../continuous-delivery/): Integrates DB changes into the CD pipeline
- [`version-control`](../version-control/): Foundation for storing and tracking migration scripts
- [`rollback-friendly-design`](../rollback-friendly-design/): Migrations must preserve the ability to roll back safely
- [`configuration-as-code`](../configuration-as-code/): Migration configuration and scheduling should be version-controlled alongside code

## DORA Metrics Impact

| Metric | Effect |
|--------|--------|
| Deployment Frequency | X |
| Lead Time for Changes | X |
| Change Failure Rate | X |
| Time to Restore Service | X |
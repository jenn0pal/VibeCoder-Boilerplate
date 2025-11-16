# Data & Platform Migrations

> **Index of all migration tracking**
>
> This directory tracks database migrations, platform migrations, and architecture migrations.

## Active Migrations

| ID | Description | Type | Risk Level | Status | Owner | ETA |
|----|-------------|------|------------|--------|-------|-----|
| - | No active migrations | - | - | - | - | - |

## Planned Migrations

| ID | Description | Type | Risk Level | Scheduled | Owner |
|----|-------------|------|------------|-----------|-------|
| - | No planned migrations | - | - | - | - |

## Completed Migrations

| ID | Description | Type | Completed Date | Duration | Notes |
|----|-------------|------|----------------|----------|-------|
| - | No completed migrations yet | - | - | - | - |

## Migrations by Type

### Database Schema Migrations
**Current:**
- Database: [PostgreSQL/MySQL/etc.] [version]
- Schema version: [version]

**Planned:**
- No planned schema migrations

### Data Migrations
**Planned:**
- No planned data migrations

### Platform Migrations
**Current Platform:**
- Cloud Provider: [AWS/GCP/Azure]
- Infrastructure: [Description]

**Planned:**
- No planned platform migrations

### Architecture Migrations
**Current Architecture:**
- Pattern: [Monolith/Microservices/etc.]
- Description: [Brief description]

**Planned:**
- No planned architecture migrations

## How to Plan Migration

```
Load CLAUDE.md and docs/.claude/context/tech-stack.md

Migration: [Description]
Type: [Database Schema/Data Migration/Platform Migration/Architecture]
Scope: [What's being migrated]
Risk Level: [Critical/High/Medium/Low]

Current state: [What exists now]
Target state: [What we want]

Please help me:
1. Analyze current and target state
2. Create migration strategy (MIGRATION-[ID].md)
3. Develop migration scripts
4. Plan testing and validation
5. Create rollback procedure
6. Execute migration with zero downtime (if required)
```

## Risk Assessment

**High-risk migrations** (require extensive planning):
- Data migrations > 1TB
- Platform changes affecting production
- Architecture migrations requiring code changes
- Migrations with > 1 hour downtime

**Medium-risk migrations**:
- Data migrations < 1TB
- Schema changes with backward compatibility
- Migrations with < 1 hour downtime

**Low-risk migrations**:
- Additive schema changes
- Small data transformations
- Zero-downtime migrations

---

**Last Updated:** [Date]
**Maintained By:** [Team/Person]

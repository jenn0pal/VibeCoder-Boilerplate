# Migration Strategy: [Migration Description]

> **Template for planning data and architecture migrations**
>
> Use this template for database migrations, architecture changes, data format migrations, or platform migrations.
> For simple schema changes, use your framework's migration tools directly.

## Overview

**Migration ID:** MIGRATION-[ID]
**Date:** [YYYY-MM-DD]
**Type:** [Database Schema/Data Migration/Platform Migration/Architecture Migration]
**Scope:** [Single Table/Multiple Tables/Entire Database/System-Wide]
**Risk Level:** [Critical/High/Medium/Low]
**Estimated Duration:** [Hours/Days/Weeks]

### Migration Classification

**Type of Migration:**
- [ ] **Schema Migration** - Changing database structure (add/remove columns, tables, indexes)
- [ ] **Data Migration** - Moving/transforming data between systems or formats
- [ ] **Platform Migration** - Moving to different infrastructure/cloud provider
- [ ] **Architecture Migration** - Restructuring application architecture
- [ ] **Version Migration** - Upgrading database/framework version
- [ ] **Combined Migration** - Multiple types above

**Complexity:** [Simple/Medium/Complex]
**Reversibility:** [Fully Reversible/Partially Reversible/Irreversible]

## Business Context

### Why This Migration?
[Explain the business or technical driver]

**Primary Reasons:**
- [ ] Performance issues
- [ ] Scalability requirements
- [ ] Cost optimization
- [ ] Feature enablement
- [ ] Regulatory compliance
- [ ] Technical debt removal
- [ ] Platform end-of-life
- [ ] Vendor lock-in avoidance
- [ ] Other: [Specify]

### Expected Benefits
**Technical Benefits:**
- [Benefit 1 - e.g., 50% query performance improvement]
- [Benefit 2 - e.g., Better data consistency]
- [Benefit 3 - e.g., Enables horizontal scaling]

**Business Benefits:**
- [Benefit 1 - e.g., $X/month cost savings]
- [Benefit 2 - e.g., Support for new markets]
- [Benefit 3 - e.g., Faster feature delivery]

**Cost of NOT Migrating:**
- [Risk 1]
- [Risk 2]
- [Risk 3]

## Current State

### Current Architecture

```
┌─────────────────┐
│   Application   │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│   Database      │
│   [Type/Version]│
│   [Schema]      │
└─────────────────┘
```

**Current State Details:**
- **Database:** [PostgreSQL 12/MySQL 5.7/MongoDB 4.4/etc.]
- **Size:** [X GB data, Y million records]
- **Tables/Collections:** [X]
- **Indexes:** [X]
- **Relationships:** [Description]
- **Access Patterns:** [Read-heavy/Write-heavy/Mixed]
- **Performance:** [Current metrics]

### Current Schema

```sql
-- Current schema (if applicable)
CREATE TABLE users (
  id SERIAL PRIMARY KEY,
  name VARCHAR(255),
  email VARCHAR(255) UNIQUE,
  created_at TIMESTAMP
);

-- Other relevant tables
```

### Current Data

**Data Volume:**
- Total records: [X million]
- Data size: [X GB]
- Growth rate: [X GB/month]
- Largest table: [Table name] - [X records]

**Data Characteristics:**
- Data quality: [High/Medium/Low]
- Duplicates: [None/Some/Many]
- Missing values: [X%]
- Data types: [Structured/Semi-structured/Unstructured]

### Current Issues
1. **[Issue 1]**
   - Description: [What's wrong]
   - Impact: [How it affects users/system]
   - Frequency: [How often it occurs]

2. **[Issue 2]**
   [Same structure]

3. **[Issue 3]**
   [Same structure]

### Current Performance Baseline

| Metric | Current Value | Target |
|--------|--------------|--------|
| Query response time | [X]ms | < [Y]ms |
| Write throughput | [X] ops/sec | > [Y] ops/sec |
| Read throughput | [X] ops/sec | > [Y] ops/sec |
| Storage size | [X] GB | [Y] GB |
| CPU usage | [X]% | < [Y]% |
| Memory usage | [X] GB | < [Y] GB |

## Target State

### Target Architecture

```
┌─────────────────┐
│   Application   │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│   New Database  │
│   [Type/Version]│
│   [New Schema]  │
└─────────────────┘
```

**Target State Details:**
- **Database:** [PostgreSQL 15/MySQL 8.0/MongoDB 6.0/etc.]
- **Expected size:** [X GB data]
- **Tables/Collections:** [X]
- **Indexes:** [X]
- **Improvements:** [What's better]

### Target Schema

```sql
-- Target schema (if applicable)
CREATE TABLE users (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  full_name VARCHAR(500) NOT NULL,
  email VARCHAR(500) UNIQUE NOT NULL,
  email_verified BOOLEAN DEFAULT false,
  created_at TIMESTAMPTZ NOT NULL DEFAULT NOW(),
  updated_at TIMESTAMPTZ NOT NULL DEFAULT NOW()
);

-- Indexes
CREATE INDEX idx_users_email ON users(email);
CREATE INDEX idx_users_created ON users(created_at);

-- Other relevant tables
```

### Schema Changes

| Change Type | Before | After | Reason |
|-------------|--------|-------|--------|
| Column rename | `name` | `full_name` | Clarity |
| Type change | `id SERIAL` | `id UUID` | Scalability |
| Add column | - | `email_verified` | New feature |
| Add column | - | `updated_at` | Audit trail |
| Type change | `TIMESTAMP` | `TIMESTAMPTZ` | Timezone support |
| Add constraint | - | `NOT NULL` on `full_name` | Data quality |
| Add index | - | `idx_users_email` | Performance |

### Data Transformations

#### Transformation 1: [Name Column]
```sql
-- Old data
name: "John Doe"

-- Transformation logic
full_name = old.name

-- New data
full_name: "John Doe"
```

#### Transformation 2: [ID Generation]
```sql
-- Old data
id: 12345 (SERIAL)

-- Transformation logic
id = generate_uuid()
-- Keep mapping: old_id -> new_uuid for relationships

-- New data
id: "550e8400-e29b-41d4-a716-446655440000" (UUID)
```

#### Transformation 3: [Timestamp]
```sql
-- Old data
created_at: "2024-01-01 12:00:00" (local time)

-- Transformation logic
created_at_tz = convert_to_utc(created_at, assumed_timezone)

-- New data
created_at: "2024-01-01 12:00:00+00" (UTC)
```

### Expected Performance

| Metric | Current | Target | Improvement |
|--------|---------|--------|-------------|
| Query response time | [X]ms | [Y]ms | [Z]% faster |
| Write throughput | [X] ops/sec | [Y] ops/sec | [Z]% increase |
| Read throughput | [X] ops/sec | [Y] ops/sec | [Z]% increase |
| Storage size | [X] GB | [Y] GB | [Z]% reduction |
| Index efficiency | [X] scans | [Y] scans | [Z]% fewer |

## Migration Approach

### Migration Strategy

**Selected Strategy:** [Big Bang/Phased/Parallel Run/Blue-Green/Dual Write]

#### Option 1: Big Bang Migration
**Description:** Migrate all data at once during maintenance window

**Pros:**
- Simple and clean
- Single cutover point
- No dual-write complexity

**Cons:**
- Requires downtime
- Higher risk
- All-or-nothing

**When to use:** Small databases, acceptable downtime, low risk tolerance for data inconsistency

#### Option 2: Phased Migration
**Description:** Migrate data in phases (e.g., by table, by date range, by tenant)

**Pros:**
- Lower risk per phase
- Can validate incrementally
- Smaller rollback scope

**Cons:**
- Complex coordination
- Longer overall timeline
- Data inconsistency between phases

**When to use:** Large databases, zero-downtime requirement, complex schema

#### Option 3: Parallel Run (Dual Write)
**Description:** Write to both old and new system, gradually shift reads

**Pros:**
- Zero downtime
- Easy rollback
- Validate before cutover

**Cons:**
- Complex application logic
- Temporary performance impact
- Data sync challenges

**When to use:** Mission-critical systems, zero-downtime required, high data volume

#### Option 4: Blue-Green Migration
**Description:** Set up new system (green), migrate data, switch traffic

**Pros:**
- Zero downtime
- Easy rollback
- Full testing before cutover

**Cons:**
- Double resource cost
- Complex sync during migration
- Requires load balancer

**When to use:** Cloud migrations, infrastructure changes, high availability requirements

**Recommended Strategy:** [Strategy X]
**Rationale:** [Why this strategy is best for our situation]

### Zero-Downtime Requirements

**Acceptable Downtime:** [X hours/minutes / Zero]
**Actual Expected Downtime:** [X minutes]

**If zero-downtime required:**
- [ ] Dual-write approach planned
- [ ] Read routing strategy defined
- [ ] Data sync mechanism in place
- [ ] Rollback without downtime possible

## Migration Plan

### Pre-Migration Phase (Week 1-2)

#### Planning & Preparation
- [ ] Finalize migration strategy
- [ ] Get stakeholder approval
- [ ] Schedule migration window
- [ ] Assemble migration team
- [ ] Set up communication channels

#### Environment Setup
- [ ] Provision target database/infrastructure
- [ ] Configure replication (if applicable)
- [ ] Set up monitoring and alerting
- [ ] Create migration scripts
- [ ] Set up rollback scripts

#### Data Analysis
- [ ] Analyze data quality
- [ ] Identify data issues
- [ ] Clean up bad data (if possible)
- [ ] Document data anomalies
- [ ] Estimate migration duration

#### Testing
- [ ] Create test plan
- [ ] Set up test environment
- [ ] Prepare test data (subset of production)
- [ ] Test migration scripts
- [ ] Test rollback procedures

**Success Criteria:**
- [ ] All scripts tested successfully
- [ ] Rollback procedure verified
- [ ] Team trained on migration process
- [ ] Go/no-go decision made

---

### Migration Execution Phase

#### Phase 1: Initial Data Migration (Day 1)
**Goal:** Migrate bulk historical data

**Tasks:**
- [ ] Put application in read-only mode (if required)
- [ ] Take snapshot/backup of source database
- [ ] Start data migration job
- [ ] Monitor migration progress
- [ ] Validate data integrity
- [ ] Performance check

**Migration Script:**
```bash
# Export from source
pg_dump -h source-host -U user -d database -t users -f users.sql

# Transform data
python transform_data.py users.sql > users_transformed.sql

# Import to target
psql -h target-host -U user -d database -f users_transformed.sql

# Verify counts
psql -h source-host -U user -d database -c "SELECT COUNT(*) FROM users;"
psql -h target-host -U user -d database -c "SELECT COUNT(*) FROM users;"
```

**Validation:**
- [ ] Record counts match
- [ ] Data samples verified
- [ ] Indexes created
- [ ] Constraints applied
- [ ] Performance acceptable

**Duration:** [X hours]

---

#### Phase 2: Incremental Sync (Day 1-2)
**Goal:** Catch up on changes made during initial migration

**Tasks:**
- [ ] Enable change data capture (CDC) or log tracking
- [ ] Apply incremental changes
- [ ] Verify data sync
- [ ] Minimize lag time

**Sync Strategy:**
```sql
-- Track last synced timestamp
SELECT MAX(updated_at) FROM target.users;

-- Copy only new/updated records
INSERT INTO target.users
SELECT * FROM source.users
WHERE updated_at > '[last_synced_timestamp]';
```

**Validation:**
- [ ] Lag time < [X minutes]
- [ ] All changes captured
- [ ] No data loss

**Duration:** [X hours]

---

#### Phase 3: Application Cutover (Day 2)
**Goal:** Switch application to use new database

**Tasks:**
- [ ] Stop writes to old database (if not dual-write)
- [ ] Final incremental sync
- [ ] Verify data consistency
- [ ] Update application configuration
- [ ] Restart application servers
- [ ] Switch DNS/load balancer (if applicable)
- [ ] Enable writes to new database
- [ ] Monitor for errors

**Cutover Script:**
```bash
# 1. Stop application (or enable read-only)
./stop-app.sh

# 2. Final sync
./final-sync.sh

# 3. Verify consistency
./verify-data.sh

# 4. Update config to point to new database
# Edit .env or config file
DATABASE_URL=postgresql://new-host/new-database

# 5. Start application
./start-app.sh

# 6. Smoke tests
./smoke-tests.sh
```

**Validation:**
- [ ] Application starts successfully
- [ ] All smoke tests pass
- [ ] No errors in logs
- [ ] Reads working
- [ ] Writes working

**Duration:** [X minutes]

---

#### Phase 4: Monitoring & Validation (Day 2-7)
**Goal:** Ensure migration success and stability

**Tasks:**
- [ ] Monitor error rates
- [ ] Monitor performance metrics
- [ ] Validate data integrity
- [ ] User acceptance testing
- [ ] Address any issues
- [ ] Keep old database as backup

**Monitoring Checklist:**
- [ ] Hour 1: Check every 15 minutes
- [ ] Hours 2-24: Check every hour
- [ ] Days 2-7: Check daily
- [ ] Week 2: Normal monitoring

**Success Criteria:**
- [ ] Error rate < 0.1%
- [ ] Performance meets targets
- [ ] No data loss detected
- [ ] No user complaints

**Duration:** [7 days]

---

### Post-Migration Phase (Week 2-4)

#### Cleanup
- [ ] Decommission old database (after retention period)
- [ ] Remove migration scripts (or archive)
- [ ] Remove dual-write logic (if applicable)
- [ ] Clean up temporary infrastructure
- [ ] Update documentation

#### Optimization
- [ ] Analyze query performance
- [ ] Add missing indexes
- [ ] Optimize slow queries
- [ ] Tune database parameters
- [ ] Vacuum/analyze (PostgreSQL)

#### Documentation
- [ ] Update architecture diagrams
- [ ] Update `docs/.claude/context/tech-stack.md`
- [ ] Update `docs/.claude/context/decision-log.md`
- [ ] Document lessons learned
- [ ] Create runbook for future migrations

**Success Criteria:**
- [ ] Old database decommissioned
- [ ] Performance optimized
- [ ] Documentation complete
- [ ] Team trained on new system

## Data Integrity & Validation

### Validation Strategy

**Validation Levels:**
1. **Structural Validation** - Schema matches
2. **Count Validation** - Record counts match
3. **Sample Validation** - Random samples verified
4. **Checksum Validation** - Data integrity verified
5. **Business Logic Validation** - Domain rules satisfied

### Validation Scripts

#### Count Validation
```sql
-- Source database
SELECT
  'users' as table_name,
  COUNT(*) as count,
  MIN(created_at) as min_date,
  MAX(created_at) as max_date
FROM users
UNION ALL
SELECT
  'orders' as table_name,
  COUNT(*) as count,
  MIN(created_at) as min_date,
  MAX(created_at) as max_date
FROM orders;

-- Target database (run same query)
-- Compare results
```

#### Sample Validation
```sql
-- Select random samples from source
SELECT * FROM users
ORDER BY RANDOM()
LIMIT 100;

-- Verify in target
SELECT * FROM users
WHERE id IN ([list of sampled IDs]);

-- Compare field by field
```

#### Checksum Validation
```sql
-- Generate checksums for source data
SELECT
  id,
  MD5(CONCAT(full_name, email, created_at::text)) as checksum
FROM users
ORDER BY id;

-- Generate checksums for target data
-- Compare checksums
```

### Data Quality Checks

**Pre-Migration Checks:**
- [ ] Identify null values in required fields
- [ ] Find duplicate records
- [ ] Validate foreign key integrity
- [ ] Check data type compatibility
- [ ] Identify outliers/anomalies

**Post-Migration Checks:**
- [ ] All records migrated
- [ ] No data corruption
- [ ] Relationships intact
- [ ] Indexes functional
- [ ] Constraints enforced

### Reconciliation Report

**Template:**
```
Migration Reconciliation Report
Date: [YYYY-MM-DD]
Migration ID: MIGRATION-[ID]

Source Database:
- Total records: [X]
- Date range: [Start] to [End]

Target Database:
- Total records: [Y]
- Date range: [Start] to [End]

Discrepancies:
- Missing records: [Z]
- Extra records: [W]
- Modified records: [V]

Data Quality:
- Null values: [X] (acceptable: [Y])
- Duplicates: [X] (acceptable: 0)
- Invalid data: [X] (acceptable: 0)

Status: [Pass/Fail/Needs Review]
```

## Risk Management

### Risk Assessment

| Risk | Likelihood | Impact | Severity | Mitigation |
|------|------------|--------|----------|------------|
| Data loss during migration | Low | Critical | 🔴 High | Backups, validation scripts |
| Extended downtime | Medium | High | 🟡 Medium | Dry runs, rollback plan |
| Performance degradation | Medium | High | 🟡 Medium | Load testing, monitoring |
| Data corruption | Low | Critical | 🔴 High | Checksums, validation |
| Migration script failure | Medium | High | 🟡 Medium | Testing, error handling |
| Rollback failure | Low | Critical | 🔴 High | Test rollback procedure |
| Application compatibility | Medium | Medium | 🟡 Medium | Integration testing |
| Unexpected data growth | Low | Medium | 🟢 Low | Monitor disk space |

### Backup Strategy

**Pre-Migration Backups:**
```bash
# Full database backup
pg_dump -h source-host -U user -d database -F c -f backup-pre-migration.dump

# Verify backup
pg_restore --list backup-pre-migration.dump | wc -l

# Store backup securely
aws s3 cp backup-pre-migration.dump s3://backups/migration-[ID]/
```

**Backup Retention:**
- Pre-migration backup: [90 days]
- Daily backups during migration: [30 days]
- Post-migration: [Normal retention policy]

**Backup Verification:**
- [ ] Backup size reasonable
- [ ] Backup file integrity verified
- [ ] Restore tested in non-production environment
- [ ] Backup stored in multiple locations

### Rollback Strategy

**Rollback Scenarios:**
1. Migration fails partway through
2. Data corruption detected
3. Unacceptable performance
4. Critical bugs discovered
5. Stakeholder decision

**Rollback Procedures:**

#### Scenario 1: Early Failure (During Migration)
```bash
# Stop migration
kill [migration-job-pid]

# Restore from backup (if changes made)
pg_restore -h source-host -U user -d database backup-pre-migration.dump

# Revert application config
git checkout [previous-config]

# Restart application
./restart-app.sh
```

**Recovery Time: [X minutes]**

#### Scenario 2: Post-Cutover Rollback
```bash
# Switch application back to old database
# Update config
DATABASE_URL=postgresql://old-host/old-database

# Restart application
./restart-app.sh

# If data written to new database, sync back (if possible)
./reverse-sync.sh

# Investigate issues before retry
```

**Recovery Time: [X minutes]**
**Data Loss Risk: [High/Medium/Low]**

**Note:** If writes occurred to new database after cutover, rollback becomes complex.

### Rollback Decision Criteria

**Automatic Rollback Triggers:**
- Data loss detected > [X]%
- Error rate > [Y]%
- Performance degradation > [Z]%
- Critical functionality broken

**Manual Rollback Triggers:**
- Stakeholder decision
- Unforeseen critical issues
- Compliance violation
- Security concern

**Rollback Decision Matrix:**
| Time Since Cutover | Data Loss Risk | Rollback Decision |
|-------------------|----------------|-------------------|
| < 1 hour | Low | Easy rollback |
| 1-24 hours | Medium | Evaluate carefully |
| > 24 hours | High | Likely forward-fix |

## Monitoring & Alerting

### Metrics to Monitor

**During Migration:**
- Migration progress (% complete)
- Records processed per second
- Disk space remaining
- Network bandwidth usage
- Database CPU/memory
- Error rate

**After Migration:**
- Application error rate
- Database query performance
- API response times
- User-reported issues
- Data consistency checks

### Alert Configuration

```yaml
# Example alert rules
alerts:
  - name: Migration Stalled
    condition: migration_progress_rate < 100 records/sec
    severity: warning
    action: Notify migration team

  - name: High Error Rate
    condition: error_rate > 1%
    severity: critical
    action: Page on-call engineer, consider rollback

  - name: Disk Space Low
    condition: disk_free < 20%
    severity: critical
    action: Pause migration, alert team

  - name: Performance Degradation
    condition: p95_latency > baseline * 1.5
    severity: warning
    action: Investigate, prepare rollback
```

### Monitoring Dashboard

**Dashboard URL:** [Link]

**Panels:**
1. Migration Progress
2. Error Rate
3. Performance Metrics
4. Resource Utilization
5. Data Integrity Checks

## Communication Plan

### Stakeholders

| Stakeholder | Role | Interest Level | Notification Method |
|-------------|------|----------------|---------------------|
| [CTO] | Decision Maker | High | Email + Meeting |
| [Engineering Team] | Executors | High | Slack + Standup |
| [Product Team] | Business Impact | Medium | Email |
| [Support Team] | User Issues | Medium | Email + Training |
| [Users] | End Users | Low | Status page |

### Communication Timeline

**Pre-Migration:**
- [ ] T-4 weeks: Initial announcement
- [ ] T-2 weeks: Detailed plan shared
- [ ] T-1 week: Final reminder
- [ ] T-2 days: Migration rehearsal results
- [ ] T-1 day: Go/no-go decision
- [ ] T-0 day: Migration start notification

**During Migration:**
- [ ] Migration start
- [ ] Hourly progress updates
- [ ] Any issues encountered
- [ ] Cutover notification
- [ ] Migration complete

**Post-Migration:**
- [ ] Day 1: Success confirmation
- [ ] Day 3: Stability update
- [ ] Week 1: Performance report
- [ ] Week 2: Final report & retrospective

### Status Update Template

```
Subject: [MIGRATION-XXX] Migration Status - [Date Time]

Status: [In Progress / Complete / Issues Encountered]
Phase: [Pre-Migration / Migration / Post-Migration]
Progress: [X]% complete

Completed:
- [Milestone 1] - [Time]
- [Milestone 2] - [Time]

Currently In Progress:
- [Current task]
- ETA: [Time]

Next Steps:
- [Next task]
- Scheduled: [Time]

Metrics:
- Records migrated: [X] / [Y] ([Z]%)
- Performance: [Metric]
- Error rate: [X]%

Issues/Risks:
- [Issue 1] - Severity: [L/M/H] - Status: [Investigating/Resolved]

Downtime:
- Planned: [X minutes]
- Actual: [Y minutes]

Next Update: [Time]
```

## Testing Strategy

### Test Environments

**Environments:**
1. **Development** - Initial testing of migration scripts
2. **Staging** - Full dress rehearsal with production-like data
3. **Production** - Actual migration

**Staging Environment:**
- [ ] Identical to production (same DB version, size, config)
- [ ] Production data snapshot (anonymized if needed)
- [ ] Same application version
- [ ] Same infrastructure setup

### Test Plan

#### Test 1: Migration Script Functionality
**Goal:** Verify scripts work correctly

- [ ] Scripts execute without errors
- [ ] Data transforms correctly
- [ ] Performance acceptable
- [ ] Resource usage reasonable

#### Test 2: Data Integrity
**Goal:** Ensure no data loss or corruption

- [ ] Record counts match
- [ ] Sample data verified
- [ ] Checksums match
- [ ] Relationships intact

#### Test 3: Application Compatibility
**Goal:** Application works with migrated data

- [ ] Application connects successfully
- [ ] Reads work correctly
- [ ] Writes work correctly
- [ ] All features functional

#### Test 4: Performance
**Goal:** Meet performance targets

- [ ] Query performance measured
- [ ] Load test passed
- [ ] Meets or exceeds baseline

#### Test 5: Rollback Procedure
**Goal:** Verify we can rollback if needed

- [ ] Rollback script works
- [ ] Application recovers
- [ ] Data intact after rollback

### Dry Run / Dress Rehearsal

**Schedule:** [YYYY-MM-DD] (1-2 weeks before production migration)

**Checklist:**
- [ ] Run full migration on staging
- [ ] Time each phase
- [ ] Identify any issues
- [ ] Validate rollback procedure
- [ ] Team walkthrough
- [ ] Document lessons learned
- [ ] Adjust production plan based on findings

**Dry Run Report:**
- Duration: [Actual time taken]
- Issues: [List]
- Adjustments needed: [List]
- Go/no-go for production: [Decision]

## Timeline

**Planning Start:** [YYYY-MM-DD]
**Testing Start:** [YYYY-MM-DD]
**Dry Run:** [YYYY-MM-DD]
**Production Migration:** [YYYY-MM-DD]
**Monitoring Period:** [YYYY-MM-DD] to [YYYY-MM-DD]
**Decommission Old System:** [YYYY-MM-DD]

**Total Timeline:** [X weeks]

### Detailed Schedule

| Phase | Start | End | Duration | Owner | Status |
|-------|-------|-----|----------|-------|--------|
| Planning | [Date] | [Date] | [X days] | [Name] | ☐ |
| Script Development | [Date] | [Date] | [X days] | [Name] | ☐ |
| Testing | [Date] | [Date] | [X days] | [Name] | ☐ |
| Dry Run | [Date] | [Date] | [X days] | [Name] | ☐ |
| Pre-Migration Prep | [Date] | [Date] | [X days] | [Name] | ☐ |
| Migration Execution | [Date] | [Date] | [X hours] | [Name] | ☐ |
| Validation | [Date] | [Date] | [X days] | [Name] | ☐ |
| Monitoring | [Date] | [Date] | [X days] | [Name] | ☐ |
| Cleanup | [Date] | [Date] | [X days] | [Name] | ☐ |

## Cost Estimation

### Infrastructure Costs
- Target database infrastructure: $[X]/month
- Temporary dual-run costs: $[Y] (during migration)
- Backup storage: $[Z]/month
- **Total Infrastructure:** $[X]

### Labor Costs
- Planning: [X hours] × $[Y]/hour = $[Z]
- Development: [X hours] × $[Y]/hour = $[Z]
- Testing: [X hours] × $[Y]/hour = $[Z]
- Execution: [X hours] × $[Y]/hour = $[Z]
- Monitoring: [X hours] × $[Y]/hour = $[Z]
- **Total Labor:** $[Z]

### Opportunity Costs
- Features delayed: [List]
- Revenue impact during downtime: $[X]

**Total Migration Cost:** $[X]

### Cost-Benefit Analysis

**Annual Benefits:**
- Performance improvement value: $[X]/year
- Cost savings: $[Y]/year
- Risk reduction: $[Z]/year
- **Total Annual Benefit:** $[W]/year

**Payback Period:** [X months]
**ROI:** [Y]%

## Progress Tracking

### Migration Checklist

**Pre-Migration:**
- [ ] Migration strategy approved
- [ ] Scripts developed and tested
- [ ] Dry run successful
- [ ] Team trained
- [ ] Backups verified
- [ ] Rollback procedure tested
- [ ] Stakeholders notified
- [ ] Go/no-go decision: [Go/No-Go]

**Migration:**
- [ ] Phase 1: Initial migration complete
- [ ] Phase 2: Incremental sync complete
- [ ] Phase 3: Cutover successful
- [ ] Phase 4: Validation passed

**Post-Migration:**
- [ ] Monitoring period complete
- [ ] Performance targets met
- [ ] Old system decommissioned
- [ ] Documentation updated
- [ ] Retrospective conducted

### Current Status
**Status:** [Planning/Testing/Migrating/Monitoring/Complete]
**Overall Progress:** [X]%
**Last Updated:** [YYYY-MM-DD HH:MM]
**Next Milestone:** [Milestone] - [ETA]

### Issues Log

| ID | Issue | Severity | Status | Owner | ETA |
|----|-------|----------|--------|-------|-----|
| 1 | [Description] | High | Open | [Name] | [Date] |
| 2 | [Description] | Medium | Resolved | [Name] | - |

## Post-Migration Review

### Final Metrics

| Metric | Before | After | Change | Target | Met? |
|--------|--------|-------|--------|--------|------|
| Data Volume | [X] GB | [Y] GB | - | [Y] GB | ✅/❌ |
| Record Count | [X] M | [Y] M | - | [Y] M | ✅/❌ |
| Query Performance | [X]ms | [Y]ms | [+/-Z]% | < [W]ms | ✅/❌ |
| Storage Cost | $[X]/mo | $[Y]/mo | [+/-Z]% | < $[W]/mo | ✅/❌ |
| Downtime | - | [X] min | - | < [Y] min | ✅/❌ |

### Actual vs Planned

**Timeline:**
- Planned: [X] days
- Actual: [Y] days
- Variance: [+/-Z] days

**Effort:**
- Planned: [X] hours
- Actual: [Y] hours
- Variance: [+/-Z]%

**Cost:**
- Planned: $[X]
- Actual: $[Y]
- Variance: [+/-Z]%

### Issues Encountered
- [Issue 1] - Impact: [L/M/H] - Resolution: [How resolved]
- [Issue 2] - Impact: [L/M/H] - Resolution: [How resolved]

### Lessons Learned

**What Went Well:**
- [Success 1]
- [Success 2]
- [Success 3]

**What Could Be Improved:**
- [Improvement 1]
- [Improvement 2]
- [Improvement 3]

**For Next Migration:**
- [Recommendation 1]
- [Recommendation 2]
- [Recommendation 3]

### Benefits Realized

**Immediate Benefits:**
- [Benefit 1]
- [Benefit 2]

**Long-term Benefits (Expected):**
- [Benefit 1]
- [Benefit 2]

**Unexpected Benefits:**
- [Benefit 1]

## Related

- **Related Upgrades:** [UPGRADE-XXX]
- **Related Tech Debt:** [DEBT-XXX]
- **Related Refactoring:** [REFACTOR-XXX]
- **Migration Scripts:** [Repository/Path]
- **Runbook:** [Link]
- **Post-Mortem:** [Link]

---

**Status:** [Planning/Testing/In Progress/Complete/Rolled Back]
**Owner:** [Name/Team]
**Last Updated:** [YYYY-MM-DD]

---

## Migration Type Specific Notes

### Database Schema Migration
- Use framework migration tools (Django migrations, Laravel migrations, Alembic, Flyway)
- Version control all migration files
- Test both upgrade and downgrade paths
- Consider data migration vs schema migration separation

### Platform Migration (Cloud Provider)
- Consider vendor-specific tools (AWS DMS, Google Database Migration Service)
- Test network connectivity and latency
- Plan for DNS/traffic cutover
- Multi-region considerations

### Microservices Migration
- Strangler fig pattern for gradual migration
- API versioning for compatibility
- Service mesh considerations
- Inter-service communication changes

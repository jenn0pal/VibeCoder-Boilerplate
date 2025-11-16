# Breaking Change Assessment: [Change Description]

> **Template for evaluating and planning breaking changes**
>
> Use this template when considering introducing breaking changes to your API, library, or application.
> Also use when upgrading dependencies that introduce breaking changes to understand impact.

## Overview

**Assessment ID:** BREAK-[ID]
**Date:** [YYYY-MM-DD]
**Change Type:** [API Change/Database Schema/Configuration/Dependency Upgrade/Architecture]
**Severity:** [Critical/High/Medium/Low]
**Scope:** [Internal/External/Both]

### What is a Breaking Change?
A breaking change is any modification that requires consumers/users to change their code or configuration.

**Examples:**
- Removing or renaming public APIs
- Changing function signatures
- Altering data formats
- Database schema changes requiring migration
- Configuration file format changes
- Removing features

## Change Description

### What Are We Changing?
[Clear description of the proposed breaking change]

### Why Is This Necessary?
[Business or technical justification]

**Drivers:**
- [ ] Security vulnerability requires API change
- [ ] Performance optimization requires breaking change
- [ ] Technical debt removal
- [ ] Framework upgrade forces change
- [ ] New feature requires incompatible changes
- [ ] Deprecation removal
- [ ] Other: [Specify]

### What Makes This Breaking?
[Explain specifically why this breaks compatibility]

**Incompatibility Type:**
- [ ] API signature change (parameters, return types)
- [ ] Behavior change (same signature, different behavior)
- [ ] Data format change (JSON structure, database schema)
- [ ] Configuration change (env vars, config files)
- [ ] Dependency version requirements
- [ ] Removed functionality
- [ ] Other: [Specify]

## Impact Analysis

### Who Is Affected?

**Stakeholders:**
- [ ] **Internal developers** - Count: [X developers]
- [ ] **External API consumers** - Count: [X integrations]
- [ ] **End users** - Count: [X users]
- [ ] **Third-party integrations** - Count: [X partners]
- [ ] **Mobile app clients** - Count: [X apps]
- [ ] **CI/CD pipelines**
- [ ] **Documentation**
- [ ] **Training materials**

### Affected Components

| Component | Type | Usage Level | Migration Effort |
|-----------|------|-------------|------------------|
| [Component 1] | [Internal/External] | [High/Medium/Low] | [Hours/Days] |
| [Component 2] | [Internal/External] | [High/Medium/Low] | [Hours/Days] |
| [Component 3] | [Internal/External] | [High/Medium/Low] | [Hours/Days] |

### Usage Statistics

**How widely is the affected code used?**
```bash
# Commands to find usage
grep -r "function_name" src/
git grep "api_endpoint"
# Check analytics for API endpoint usage
```

**Results:**
- Internal call sites: [X]
- External API calls/day: [X]
- Active users of feature: [X]
- Last 30 days usage: [X requests]

### Blast Radius

**If we make this change:**
- Files that need updating: [X]
- APIs that break: [X]
- External integrations affected: [X]
- Users who need to update: [X]
- Estimated total impact: [High/Medium/Low]

## Current State

### Current Implementation

```[language]
// Current API/code that will break
// Show the existing interface

/**
 * Current function signature
 * @param {type} param1 - Description
 * @param {type} param2 - Description
 * @returns {type} Description
 */
function currentAPI(param1, param2) {
  // Current implementation
}
```

### Current Behavior
[Describe how it currently works]

### Current Consumers
**Known consumers:**
1. [Consumer 1] - [Usage description]
2. [Consumer 2] - [Usage description]
3. [Consumer 3] - [Usage description]

**Unknown consumers:**
- Public API usage: [Can't track / Analytics show X calls]
- Library downloads: [X downloads/month]

## Proposed Change

### New Implementation

```[language]
// New API/code after breaking change
// Show the new interface

/**
 * New function signature
 * @param {type} newParam - Description
 * @returns {type} Description
 */
function newAPI(newParam) {
  // New implementation
}
```

### New Behavior
[Describe how it will work after the change]

### Migration Path

```[language]
// Before (current usage)
const result = currentAPI(param1, param2);

// After (new usage)
const result = newAPI({
  param1: param1,
  param2: param2,
  // new required field
  param3: defaultValue
});
```

### What Consumers Must Do
1. [Action 1 - e.g., Update import statements]
2. [Action 2 - e.g., Change function calls]
3. [Action 3 - e.g., Update configuration]
4. [Action 4 - e.g., Test thoroughly]

**Estimated effort per consumer:** [X hours/days]

## Alternatives Considered

### Alternative 1: [Don't Make Breaking Change]
**Description:** Keep current implementation as-is

**Pros:**
- No migration needed
- No user disruption
- No documentation updates

**Cons:**
- [Con 1 - e.g., Technical debt accumulates]
- [Con 2 - e.g., Security vulnerability remains]
- [Con 3 - e.g., Performance issues continue]

**Viability:** [High/Medium/Low]

### Alternative 2: [Additive Change]
**Description:** Add new API alongside old, deprecate old

**Pros:**
- Backward compatible
- Gradual migration possible
- Less disruption

**Cons:**
- Maintains technical debt temporarily
- Increased maintenance burden
- Confusing to have two APIs

**Viability:** [High/Medium/Low]

### Alternative 3: [Adapter/Bridge Pattern]
**Description:** Create compatibility layer

```[language]
// Old API (deprecated, calls new API)
function currentAPI(param1, param2) {
  console.warn('Deprecated: Use newAPI instead');
  return newAPI({ param1, param2, param3: defaultValue });
}

// New API
function newAPI(params) {
  // New implementation
}
```

**Pros:**
- Allows gradual migration
- Old code keeps working
- Clear deprecation path

**Cons:**
- Additional code to maintain
- Performance overhead
- Still need migration eventually

**Viability:** [High/Medium/Low]

### Alternative 4: [Versioned API]
**Description:** Create v2 API, maintain v1

**Pros:**
- No breaking changes for existing users
- Clear separation
- Professional approach

**Cons:**
- Maintain multiple versions
- Increased complexity
- Resource intensive

**Viability:** [High/Medium/Low]

**Recommended Alternative:** [Alternative X]
**Why:** [Justification]

## Risk Assessment

### Technical Risks

| Risk | Likelihood | Impact | Severity | Mitigation |
|------|------------|--------|----------|------------|
| Breaking existing integrations | High | Critical | 🔴 High | Communication, migration guide |
| Incomplete migration | Medium | High | 🟡 Medium | Automated tools, deprecation warnings |
| Data loss during migration | Low | Critical | 🔴 High | Backups, rollback plan |
| Performance regression | Medium | Medium | 🟡 Medium | Benchmarking, testing |
| Security issues in new implementation | Low | Critical | 🔴 High | Security audit, peer review |

### Business Risks

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| User churn | Medium | High | Communication, migration support |
| Partner complaints | High | Medium | Advance notice, migration tools |
| Delayed feature delivery | Medium | Medium | Plan adequate time |
| Support ticket spike | High | Medium | Prepare support team, FAQ |
| Reputation damage | Low | High | Clear communication, smooth process |

### Migration Risks

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| Users don't update in time | High | Medium | Extended deprecation period |
| Breaking undetected use cases | Medium | High | Thorough testing, beta period |
| Migration tool failures | Low | High | Test migration tools extensively |
| Documentation gaps | Medium | Medium | Comprehensive migration guide |

## Migration Strategy

### Deprecation Timeline

**Phase 1: Announcement (Month 1)**
- [ ] Announce breaking change
- [ ] Publish migration guide
- [ ] Add deprecation warnings
- [ ] Create migration tools

**Phase 2: Deprecation Period (Months 2-6)**
- [ ] Maintain old API with warnings
- [ ] Support users in migration
- [ ] Monitor migration progress
- [ ] Offer migration assistance

**Phase 3: Breaking Change (Month 7)**
- [ ] Remove deprecated API
- [ ] Release new version
- [ ] Update all documentation
- [ ] Monitor for issues

**Phase 4: Post-Migration (Month 8+)**
- [ ] Support edge cases
- [ ] Clean up migration code
- [ ] Retrospective

**Total Timeline:** [X months]
**Deprecation Notice Period:** [X months]

### Communication Plan

#### Internal Communication
**Audience:** Engineering team

**Timeline:**
- [ ] T-3 months: Team meeting to discuss change
- [ ] T-2 months: Update internal docs
- [ ] T-1 month: Final reminder before change
- [ ] T-0: Breaking change deployed

**Channels:**
- Slack announcement
- Team meeting
- Email notification
- Wiki/documentation update

#### External Communication
**Audience:** API consumers, partners, users

**Timeline:**
- [ ] T-6 months: Initial announcement
- [ ] T-4 months: Migration guide published
- [ ] T-2 months: Reminder email
- [ ] T-1 month: Final warning
- [ ] T-2 weeks: Last call
- [ ] T-0: Change deployed
- [ ] T+1 week: Post-deployment update

**Channels:**
- Email campaign
- Blog post
- Changelog
- In-app notifications
- Documentation banner
- Social media (if applicable)

**Message Template:**
```
Subject: Important: Breaking Changes Coming to [API/Feature] in [Version/Date]

Dear [User/Developer],

We're writing to inform you of upcoming breaking changes to [API/Feature]
that will be released in [Version] on [Date].

What's changing:
- [Change 1]
- [Change 2]

Why we're making this change:
[Brief explanation]

What you need to do:
1. [Action 1]
2. [Action 2]
3. [Action 3]

Migration guide: [Link]
Migration tool: [Link]
Support: [Contact info]

Timeline:
- [Date]: Deprecation warnings added
- [Date]: Migration guide published
- [Date]: Breaking change deployed

We apologize for any inconvenience and are here to help. Please contact
[support email] with any questions.

Thank you for your understanding.

[Your Team]
```

### Migration Tools

#### Automated Migration Script
```bash
# Migration script to update code automatically
# [Language-specific code mod or search-replace script]

# Example: JavaScript codemod
npx jscodeshift -t migrate-to-new-api.js src/

# Example: Python script
python migrate_api_calls.py --path src/

# Example: Find-and-replace with verification
sed -i 's/oldAPI(/newAPI(/g' src/**/*.js
```

**Migration Script Location:** [Path to script]

**What it does:**
- [ ] Updates function calls
- [ ] Updates imports
- [ ] Updates configuration
- [ ] Adds TODO comments for manual review
- [ ] Generates migration report

**Limitations:**
- [What it can't do automatically]
- [Edge cases requiring manual intervention]

#### Deprecation Warnings

```[language]
// Add deprecation warnings to old API
function currentAPI(param1, param2) {
  if (process.env.NODE_ENV !== 'production') {
    console.warn(
      'DEPRECATED: currentAPI() is deprecated and will be removed in v2.0. ' +
      'Use newAPI() instead. See migration guide: https://example.com/migration'
    );
  }

  // Current implementation
  // ...or call new API with adapter
  return newAPI({ param1, param2, param3: defaultValue });
}
```

**Runtime warnings:** [Yes/No]
**Build-time warnings:** [Yes/No]
**IDE warnings:** [Yes/No - via @deprecated JSDoc/comments]

### Migration Documentation

#### Migration Guide Outline
1. **Overview**
   - What changed
   - Why it changed
   - Who is affected

2. **Before & After Examples**
   - Code examples showing old vs new
   - Common use cases

3. **Step-by-Step Migration**
   - Detailed migration steps
   - Testing recommendations
   - Rollback procedure

4. **Automated Migration**
   - How to use migration tools
   - Manual steps still needed

5. **FAQ**
   - Common questions
   - Troubleshooting

6. **Support**
   - Where to get help
   - Known issues

**Migration Guide URL:** [Link]

## Testing Strategy

### Backward Compatibility Testing
- [ ] Test old API still works (during deprecation period)
- [ ] Test deprecation warnings appear
- [ ] Test migration script on sample code
- [ ] Test new API works as expected

### Migration Testing
- [ ] Test automated migration script
- [ ] Test manual migration steps
- [ ] Test edge cases
- [ ] Test with real consumer code

### Integration Testing
- [ ] Test with all known integrations
- [ ] Test with sample external projects
- [ ] Test in staging environment
- [ ] Load testing with new API

### User Acceptance Testing
- [ ] Beta testing with select users
- [ ] Gather feedback
- [ ] Iterate on migration tools
- [ ] Finalize documentation

## Versioning Strategy

### Semantic Versioning
**Current Version:** [X.Y.Z]
**Next Version:** [A.B.C]

**Version Bump Type:** [Major/Minor/Patch]
- **Major (X.0.0):** Breaking changes (increment major version)
- **Minor (X.Y.0):** Backward-compatible features
- **Patch (X.Y.Z):** Backward-compatible bug fixes

**For this breaking change:**
- Bump to: [A.0.0] (Major version increment)

### API Versioning
**Current API Version:** [v1]
**New API Version:** [v2]

**Versioning Strategy:**
- [ ] URL versioning: `/api/v1/` → `/api/v2/`
- [ ] Header versioning: `Accept: application/vnd.api+json; version=2`
- [ ] Query parameter: `/api/endpoint?version=2`
- [ ] No versioning (single version)

**Version Support Policy:**
- v1 support until: [Date]
- v2 support starts: [Date]
- Overlapping support period: [X months]

## Rollback Plan

### If Migration Fails

**Rollback Criteria:**
- Error rate > [X]%
- User complaints > [X]
- Critical functionality broken
- Performance degradation > [X]%

**Rollback Procedure:**
```bash
# Step 1: Revert deployment
git revert [commit-hash]
# or
git checkout v[previous-version]

# Step 2: Redeploy old version
./deploy.sh v[previous-version]

# Step 3: Database rollback (if schema changed)
python manage.py migrate [app] [previous_migration]

# Step 4: Notify users of rollback
# Step 5: Post-mortem
```

**Rollback Time:** [X minutes]
**Data Loss Risk:** [High/Medium/Low]

### Contingency Plans

**Plan A: Extend Deprecation Period**
- Extend old API support by [X months]
- Give users more time to migrate

**Plan B: Provide Adapter Layer Longer**
- Keep compatibility layer indefinitely
- Mark as legacy but supported

**Plan C: Revert Breaking Change**
- Abandon breaking change
- Find non-breaking alternative

## Cost-Benefit Analysis

### Costs

**Engineering Costs:**
- Planning: [X hours]
- Implementation: [X hours]
- Testing: [X hours]
- Documentation: [X hours]
- Migration support: [X hours]
- **Total:** [X hours] = $[Y]

**Business Costs:**
- User migration effort: [X hours × Y users]
- Partner migration effort: [X hours × Z partners]
- Support burden: [X hours]
- Potential user churn: [X%]
- **Total:** $[Y]

**Opportunity Costs:**
- Features delayed: [List]
- Time not spent on other improvements

**Total Estimated Cost:** $[X]

### Benefits

**Technical Benefits:**
- [Benefit 1 - e.g., 30% performance improvement]
- [Benefit 2 - e.g., Removes 5000 lines of legacy code]
- [Benefit 3 - e.g., Enables future features]

**Business Benefits:**
- [Benefit 1 - e.g., Better developer experience]
- [Benefit 2 - e.g., Competitive advantage]
- [Benefit 3 - e.g., Reduced technical debt]

**Quantified Benefits:**
- Development velocity increase: [X%]
- Maintenance time reduction: [X hours/month]
- Performance improvement: [X%]
- **Total Value:** $[Y/year]

**Payback Period:** [X months]

### Decision

**Recommendation:** [Proceed/Don't Proceed/Proceed with Modifications]

**Justification:**
[Explain why the benefits outweigh the costs, or vice versa]

**Stakeholder Approval:**
- [ ] Engineering Lead: [Name] - [Approved/Pending]
- [ ] Product Manager: [Name] - [Approved/Pending]
- [ ] CTO/Architect: [Name] - [Approved/Pending]
- [ ] Business Owner: [Name] - [Approved/Pending]

## Timeline

**Assessment Date:** [YYYY-MM-DD]
**Decision Date:** [YYYY-MM-DD]
**Announcement Date:** [YYYY-MM-DD]
**Deprecation Warning Added:** [YYYY-MM-DD]
**Migration Guide Published:** [YYYY-MM-DD]
**Breaking Change Deployed:** [YYYY-MM-DD]
**Old API Removed:** [YYYY-MM-DD]

**Total Timeline:** [X months]

## Monitoring & Success Criteria

### Metrics to Track

**Adoption Metrics:**
- % of users migrated to new API
- Migration completion rate
- Time to migrate (average)

**Health Metrics:**
- Error rate (old vs new API)
- Performance (old vs new API)
- Support ticket volume

**Success Criteria:**
- [ ] 90% of users migrated within [X months]
- [ ] Error rate < 0.1%
- [ ] No critical bugs in new API
- [ ] Performance equal or better
- [ ] Positive user feedback

### Monitoring Dashboard
**Metrics to monitor:**
- Old API usage: [Declining over time]
- New API usage: [Increasing over time]
- Error rates: [Compare old vs new]
- Migration completion: [% complete]

**Alert Thresholds:**
- Old API usage not declining: Alert at [X days]
- Error rate > 0.5%: Alert immediately
- Performance degradation > 20%: Alert immediately

## Post-Migration Review

### Actual Results
**Completed:** [YYYY-MM-DD]
**Users Migrated:** [X]% ([Y] users)
**Timeline:** [Actual vs estimated]
**Effort:** [Actual vs estimated hours]

**Metrics:**
| Metric | Target | Actual | Met? |
|--------|--------|--------|------|
| Migration rate | 90% | [X]% | ✅/❌ |
| Error rate | < 0.1% | [X]% | ✅/❌ |
| Performance | No regression | [+/-X]% | ✅/❌ |
| User satisfaction | > 4.0/5 | [X]/5 | ✅/❌ |

### Issues Encountered
- [Issue 1] - Severity: [L/M/H] - Resolved: [How]
- [Issue 2] - Severity: [L/M/H] - Resolved: [How]

### Lessons Learned
**What went well:**
- [Success 1]
- [Success 2]

**What could be improved:**
- [Improvement 1]
- [Improvement 2]

**For next breaking change:**
- [Recommendation 1]
- [Recommendation 2]

### Retrospective
**Was the breaking change worth it?** [Yes/No]
**Why or why not?** [Explanation]

**Would we do it again?** [Yes/No]
**What would we do differently?** [Changes]

## Related

- **Related Upgrades:** [UPGRADE-XXX]
- **Related Tech Debt:** [DEBT-XXX]
- **Migration Guide:** [Link]
- **Pull Request:** [Link]
- **Discussion/RFC:** [Link]

---

**Status:** [Assessment/Approved/Deprecated/Deployed/Complete/Cancelled]
**Owner:** [Name/Team]
**Last Updated:** [YYYY-MM-DD]

---

## Checklist

### Planning Phase
- [ ] Breaking change clearly defined
- [ ] Impact analysis complete
- [ ] Alternatives considered
- [ ] Benefits outweigh costs
- [ ] Stakeholder approval obtained

### Preparation Phase
- [ ] Migration guide written
- [ ] Migration tools created
- [ ] Deprecation warnings added
- [ ] Communication plan created
- [ ] Timeline established

### Execution Phase
- [ ] Announcement sent
- [ ] Migration period started
- [ ] Support provided
- [ ] Migration progress monitored
- [ ] Breaking change deployed

### Post-Migration Phase
- [ ] Old API removed (if applicable)
- [ ] Documentation updated
- [ ] Migration tools archived
- [ ] Retrospective completed
- [ ] Lessons documented

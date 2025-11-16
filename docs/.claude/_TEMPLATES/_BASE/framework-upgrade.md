# Framework Upgrade: [Framework Name] [Old Version] → [New Version]

> **Template for planning and executing framework/platform upgrades**
>
> Use this template for major or minor framework upgrades (Django, Laravel, Vue, Nuxt, React, etc.)
> For patch version updates (e.g., 5.0.1 → 5.0.2), use dependency-upgrade.md instead.

## Overview

**Upgrade ID:** UPGRADE-[ID]
**Date:** [YYYY-MM-DD]
**Framework:** [Django/Laravel/Vue/Nuxt/React/Next.js/etc.]
**Current Version:** [X.Y.Z]
**Target Version:** [A.B.C]
**Upgrade Type:** [Major/Minor]
**Priority:** [Critical/High/Medium/Low]
**Estimated Effort:** [Hours/Days/Weeks]

### Upgrade Classification
- **Patch (X.Y.Z → X.Y.W):** Bug fixes only, minimal risk
- **Minor (X.Y.Z → X.W.0):** New features, backward compatible
- **Major (X.Y.Z → W.0.0):** Breaking changes, significant refactoring

**This upgrade is:** [Patch/Minor/Major]

## Motivation

### Why Upgrade Now?
[Explain the business or technical driver for upgrading]

**Primary Reasons:**
- [ ] Security vulnerabilities (CVE-[ID])
- [ ] End of life/End of support for current version
- [ ] Performance improvements
- [ ] New features needed
- [ ] Dependency conflicts
- [ ] Developer experience improvements
- [ ] Community support moving to new version
- [ ] Other: [Specify]

### Business Value
**Expected Benefits:**
- [Benefit 1 - e.g., 30% performance improvement]
- [Benefit 2 - e.g., Access to new security features]
- [Benefit 3 - e.g., Better developer productivity]

**Cost of NOT Upgrading:**
- [Risk 1 - e.g., Security vulnerabilities]
- [Risk 2 - e.g., Falling behind, harder to upgrade later]
- [Risk 3 - e.g., Unable to use new libraries]

### Support Timeline
**Current Version Support:**
- Mainstream support ends: [Date]
- Security support ends: [Date]
- Community support status: [Active/Declining/Minimal]

**Target Version Support:**
- LTS (Long-Term Support): [Yes/No]
- Support until: [Date]
- Community adoption: [High/Medium/Low]

## Breaking Changes Analysis

### Official Release Notes
**Release Notes URL:** [Link to official release notes]
**Migration Guide URL:** [Link to official migration guide]

### Breaking Changes Identified

#### Breaking Change 1: [Change Name]
**Severity:** [Critical/High/Medium/Low]
**Affects:** [Component/Module/Feature]

**What Changed:**
[Describe what changed in the framework]

**Impact on Our Codebase:**
[How this affects our specific implementation]

**Migration Required:**
- [ ] [Step 1]
- [ ] [Step 2]
- [ ] [Step 3]

**Example:**
```[language]
// Before (old version)
// [Code example]

// After (new version)
// [Code example]
```

#### Breaking Change 2: [Change Name]
**Severity:** [Critical/High/Medium/Low]
**Affects:** [Component/Module/Feature]

[Same structure as above]

### Deprecated Features We Use

| Feature | Replacement | Used In | Migration Effort |
|---------|-------------|---------|------------------|
| [Old API] | [New API] | [File/Module] | [Hours/Days] |
| [Old API] | [New API] | [File/Module] | [Hours/Days] |
| [Old API] | [New API] | [File/Module] | [Hours/Days] |

### Removed Features We Depend On

| Removed Feature | Alternative | Action Required |
|----------------|-------------|-----------------|
| [Feature] | [Replacement or workaround] | [What we need to do] |
| [Feature] | [Replacement or workaround] | [What we need to do] |

### New Features We Want to Adopt

| New Feature | Benefit | Adoption Priority |
|-------------|---------|-------------------|
| [Feature] | [Why we want it] | High/Medium/Low |
| [Feature] | [Why we want it] | High/Medium/Low |

## Current State Assessment

### Codebase Scan Results

**Deprecated API Usage:**
```bash
# Commands used to scan codebase
grep -r "deprecated_function" src/
# or framework-specific tools
python manage.py check --deploy
php artisan config:cache
```

**Scan Results:**
- Total deprecated API calls: [X]
- Critical warnings: [X]
- Medium warnings: [X]
- Low warnings: [X]

**Top Issues:**
1. [Issue 1] - Found in [X] files
2. [Issue 2] - Found in [X] files
3. [Issue 3] - Found in [X] files

### Test Coverage Assessment
**Current Test Coverage:** [X]%
- Unit tests: [X]% coverage
- Integration tests: [X] test cases
- End-to-end tests: [X] test cases
- Performance tests: [Exists/Missing]

**Coverage Gaps:**
- [ ] [Module 1] - Only [X]% coverage (need [Y]%)
- [ ] [Module 2] - Only [X]% coverage (need [Y]%)

**Action Required:**
- [ ] Add tests for uncovered critical paths
- [ ] Verify all tests pass on current version
- [ ] Target: [X]% coverage before upgrade

### Performance Baseline
**Current Performance Metrics:**
- Average response time: [X]ms
- Peak response time: [X]ms (p95)
- Database queries per request: [X]
- Memory usage: [X]MB
- CPU usage: [X]%
- Page load time: [X]s

**Benchmarking Tools:**
- [Tool 1 - e.g., Laravel Debugbar, Django Debug Toolbar]
- [Tool 2 - e.g., Apache Bench, wrk]
- [Tool 3 - e.g., Lighthouse, WebPageTest]

## Dependency Compatibility

### Direct Dependencies Audit

| Package | Current Version | Compatible? | Target Version | Notes |
|---------|----------------|-------------|----------------|-------|
| [package-1] | [X.Y.Z] | ✅ Yes | [A.B.C] | No changes needed |
| [package-2] | [X.Y.Z] | ⚠️ Needs update | [A.B.C] | Update required |
| [package-3] | [X.Y.Z] | ❌ Incompatible | [A.B.C] | Find alternative |
| [package-4] | [X.Y.Z] | ❓ Unknown | [?] | Need to test |

### Compatibility Check Commands

```bash
# Python/Django
pip list --outdated
pip-compile --upgrade

# PHP/Laravel
composer outdated
composer update --dry-run

# JavaScript/Node
npm outdated
npm-check-updates -u

# Vue/Nuxt
npm outdated
# Check nuxt-modules for Nuxt 3 compatibility
```

### Incompatible Dependencies

#### Dependency 1: [Package Name]
**Status:** Incompatible with target version
**Current Version:** [X.Y.Z]
**Issue:** [Why it's incompatible]

**Resolution Options:**
- [ ] **Option A:** Wait for compatible version (ETA: [Date])
- [ ] **Option B:** Find alternative package: [Alternative name]
- [ ] **Option C:** Fork and maintain ourselves (Not recommended)
- [ ] **Option D:** Remove feature using this dependency

**Recommended:** [Option X]
**Impact:** [Description of impact]

### Transitive Dependencies
**Number of transitive dependencies:** [X]
**Known issues:** [List any known conflicts]

**Resolution Strategy:**
- [ ] Update all to latest compatible versions
- [ ] Lock specific versions if conflicts arise
- [ ] Document version constraints in [requirements.txt/composer.json/package.json]

## Pre-Upgrade Preparation

### Environment Setup

#### Development Environment
- [ ] Create new virtual environment/container
- [ ] Install target framework version in isolation
- [ ] Verify basic functionality
- [ ] Test with sample project

#### Testing Environment
- [ ] Provision staging environment
- [ ] Clone production database to staging
- [ ] Verify environment parity with production
- [ ] Set up monitoring and logging

### Code Preparation

#### Fix All Deprecation Warnings
- [ ] Run deprecation warning scanner
- [ ] Fix critical warnings (breaks in new version)
- [ ] Fix non-critical warnings (better practices)
- [ ] Verify all tests still pass
- [ ] Commit changes: `git commit -m "fix: resolve deprecation warnings before upgrade"`

#### Improve Test Coverage
- [ ] Identify critical paths without tests
- [ ] Write missing tests (target: [X]% coverage)
- [ ] Verify all tests pass
- [ ] Document test results

#### Code Freeze
- [ ] Notify team of upcoming upgrade
- [ ] Merge all pending PRs or defer to after upgrade
- [ ] Create upgrade branch: `git checkout -b upgrade/[framework]-[version]`
- [ ] Tag current version: `git tag v[X.Y.Z]-pre-upgrade`

### Documentation Review
- [ ] Review official migration guide
- [ ] Check community upgrade experiences (blogs, forums, GitHub issues)
- [ ] Document known gotchas and edge cases
- [ ] Prepare rollback procedure

### Backup & Safety
- [ ] Backup production database
- [ ] Backup production codebase
- [ ] Document rollback procedure
- [ ] Verify backup restoration works
- [ ] Set up feature flag for gradual rollout (if applicable)

## Upgrade Execution Plan

### Phase 1: Isolated Testing (Day 1)
**Goal:** Verify upgrade works in isolated environment

**Tasks:**
- [ ] Create clean virtual environment
- [ ] Install target framework version
- [ ] Install compatible dependencies
- [ ] Run test suite
- [ ] Document all failures

**Success Criteria:**
- Clean installation successful
- Dependencies resolve correctly
- Can start development server

---

### Phase 2: Dependency Updates (Day 1-2)
**Goal:** Update all dependencies to compatible versions

**Tasks:**
- [ ] Update framework version in dependency file
  ```bash
  # Python
  # requirements.txt: Django==5.0.1

  # PHP
  # composer.json: "laravel/framework": "^11.0"

  # JavaScript
  # package.json: "vue": "^3.4.0"
  ```
- [ ] Update direct dependencies
- [ ] Resolve dependency conflicts
- [ ] Run `[pip install/composer install/npm install]`
- [ ] Verify no dependency errors
- [ ] Commit lockfile: `git commit -m "chore: update dependencies for [framework] [version]"`

**Success Criteria:**
- All dependencies install successfully
- No version conflicts
- Lockfile committed

---

### Phase 3: Code Migration (Day 2-4)
**Goal:** Update code to work with new framework version

**Tasks:**

#### Task 3.1: Update Imports/Namespaces
- [ ] Update deprecated imports
  ```[language]
  # Example: Django
  # Old: from django.utils.encoding import force_text
  # New: from django.utils.encoding import force_str
  ```
- [ ] Verify no import errors
- [ ] Run tests

#### Task 3.2: Update API Calls
- [ ] Replace deprecated methods
- [ ] Update changed APIs
- [ ] Verify behavior unchanged
- [ ] Run tests after each change

#### Task 3.3: Update Configuration
- [ ] Update settings/config files
  ```[language]
  # Example: Update middleware, settings, etc.
  ```
- [ ] Update environment variables if needed
- [ ] Verify configuration loads correctly

#### Task 3.4: Update Database (if applicable)
- [ ] Review schema migrations
- [ ] Test migrations on staging database
- [ ] Create backup before migration
- [ ] Run migrations
  ```bash
  # Django
  python manage.py makemigrations
  python manage.py migrate

  # Laravel
  php artisan migrate
  ```
- [ ] Verify data integrity

#### Task 3.5: Update Templates/Views
- [ ] Update template syntax if changed
- [ ] Update component APIs
- [ ] Verify rendering works correctly

**Success Criteria:**
- All code updated
- No syntax errors
- Application starts successfully

---

### Phase 4: Testing & Validation (Day 4-6)
**Goal:** Ensure everything works correctly

**Tasks:**

#### Unit Testing
- [ ] Run full unit test suite
  ```bash
  # Python
  pytest
  coverage run -m pytest
  coverage report

  # PHP
  php artisan test
  ./vendor/bin/phpunit

  # JavaScript
  npm test
  npm run test:coverage
  ```
- [ ] Fix failing tests
- [ ] Verify coverage maintained or improved
- [ ] Target: [X]% coverage, [Y] tests passing

**Results:**
- Tests passing: [X]/[Y]
- Coverage: [X]%
- Failures: [List]

#### Integration Testing
- [ ] Test API endpoints
- [ ] Test database operations
- [ ] Test third-party integrations
- [ ] Test authentication/authorization
- [ ] Test file uploads/downloads
- [ ] Test background jobs/queues

**Results:**
- Integration tests passing: [X]/[Y]
- Failures: [List]

#### End-to-End Testing
- [ ] Test critical user journeys
- [ ] Test admin interface
- [ ] Test forms and validation
- [ ] Test error handling
- [ ] Cross-browser testing

**Results:**
- E2E tests passing: [X]/[Y]
- Browser compatibility: [List browsers tested]

#### Performance Testing
- [ ] Run performance benchmarks
- [ ] Compare with baseline metrics
- [ ] Identify any regressions
- [ ] Optimize if needed

**Results:**
| Metric | Before | After | Change | Acceptable? |
|--------|--------|-------|--------|-------------|
| Response time | [X]ms | [Y]ms | [Z]% | ✓/✗ |
| Memory usage | [X]MB | [Y]MB | [Z]% | ✓/✗ |
| DB queries | [X] | [Y] | [Z]% | ✓/✗ |
| Page load | [X]s | [Y]s | [Z]% | ✓/✗ |

#### Security Testing
- [ ] Run security scanner
- [ ] Check for new security features to enable
- [ ] Verify authentication still works
- [ ] Test authorization rules
- [ ] Review security changelog

**Success Criteria:**
- All test suites passing
- Performance equal or better
- No security regressions
- No critical bugs

---

### Phase 5: Staging Deployment (Day 6-7)
**Goal:** Deploy to staging and validate in production-like environment

**Tasks:**
- [ ] Deploy to staging server
- [ ] Run database migrations
- [ ] Smoke test critical features
- [ ] Monitor error logs
- [ ] Load testing
- [ ] UAT (User Acceptance Testing)

**Success Criteria:**
- Staging deployment successful
- No critical errors in logs
- Performance acceptable
- Stakeholder approval

---

### Phase 6: Production Deployment (Day 7-8)
**Goal:** Deploy to production with minimal risk

**Deployment Strategy:**
- [ ] **Strategy:** [Blue-Green/Canary/Rolling/Big Bang]

#### Blue-Green Deployment (Recommended)
```bash
# 1. Deploy new version to "green" environment
# 2. Run migrations (if backward compatible)
# 3. Switch traffic to green
# 4. Monitor for issues
# 5. Keep blue as rollback
```

#### Canary Deployment
```bash
# 1. Deploy to subset of servers (10%)
# 2. Route 10% traffic to new version
# 3. Monitor metrics
# 4. Gradually increase to 25%, 50%, 100%
# 5. Rollback if issues detected
```

**Deployment Tasks:**
- [ ] Notify team and stakeholders
- [ ] Put application in maintenance mode (if needed)
- [ ] Backup production database
- [ ] Deploy new code
- [ ] Run database migrations
  ```bash
  # With zero-downtime strategy
  python manage.py migrate --no-input
  ```
- [ ] Clear caches
- [ ] Restart application servers
- [ ] Verify application starts
- [ ] Smoke test critical endpoints
- [ ] Monitor error rates
- [ ] Monitor performance metrics
- [ ] Exit maintenance mode

**Rollback Plan Ready:**
```bash
# If critical issues arise
git revert [commit-range]
# or
git checkout v[X.Y.Z]-pre-upgrade
# Restore database backup if needed
# Redeploy old version
```

**Success Criteria:**
- Zero downtime (or planned maintenance window met)
- Error rate < 0.1%
- Performance within acceptable range
- No critical bugs reported

---

### Phase 7: Post-Deployment Monitoring (Day 8-14)
**Goal:** Ensure stability and catch any issues early

**Tasks:**
- [ ] Monitor error tracking (Sentry, Bugsnag, etc.)
- [ ] Monitor application performance (New Relic, DataDog, etc.)
- [ ] Monitor server resources (CPU, memory, disk)
- [ ] Review user feedback
- [ ] Check support tickets for new issues
- [ ] Daily standup check-ins

**Monitoring Checklist:**
- [ ] Day 1: Hourly checks
- [ ] Day 2-3: Every 4 hours
- [ ] Day 4-7: Daily checks
- [ ] Week 2: Normal monitoring cadence

**Success Criteria:**
- Error rate remains < 0.1%
- No performance degradation
- No critical bugs
- Positive user feedback

## Risk Management

### Pre-Upgrade Risks

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| Incompatible dependencies | High | High | Audit all dependencies first, find alternatives |
| Breaking changes not documented | Medium | High | Thorough testing, community research |
| Insufficient test coverage | Medium | Critical | Add tests before upgrading |
| Data migration failure | Low | Critical | Test migrations on staging, have backups |

### Upgrade Risks

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| Test failures | High | Medium | Fix tests incrementally, don't skip |
| Performance regression | Medium | High | Benchmark before/after, optimize as needed |
| Silent bugs (tests pass but behavior changes) | Low | High | Thorough manual testing, E2E tests |
| Database migration issues | Low | Critical | Test on staging first, backup production |

### Post-Upgrade Risks

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| Production bugs not caught in testing | Medium | High | Canary deployment, monitoring, quick rollback |
| Performance issues under load | Low | Medium | Load testing on staging, gradual rollout |
| Third-party integration failures | Low | High | Test all integrations, have rollback ready |
| User-facing breaking changes | Low | Medium | Communication plan, training materials |

### Rollback Criteria

**Automatic Rollback Triggers:**
- Error rate > 1%
- Response time degrades > 50%
- Critical functionality broken
- Database corruption detected

**Manual Rollback Triggers:**
- Stakeholder decision
- Unforeseen critical bug
- Performance unacceptable
- Security vulnerability introduced

### Rollback Procedure

```bash
# Step 1: Stop new deployments
# Step 2: Revert code
git revert [upgrade-commit-range]
# or
git checkout v[X.Y.Z]-pre-upgrade

# Step 3: Restore database (if migrations ran)
# (Only if migrations are not backward compatible)
pg_restore -d mydb backup.sql
# or use framework rollback
python manage.py migrate [app] [previous_migration]

# Step 4: Redeploy old version
./deploy.sh v[X.Y.Z]

# Step 5: Verify rollback successful
curl https://api.example.com/health
pytest

# Step 6: Notify team and stakeholders
# Step 7: Post-mortem to understand what went wrong
```

**Recovery Time Objective (RTO):** 15 minutes
**Recovery Point Objective (RPO):** 1 hour (last database backup)

## Communication Plan

### Stakeholders

| Stakeholder | Role | Interest | Communication Method | Frequency |
|-------------|------|----------|---------------------|-----------|
| [Name] | CTO | High | Email + Meeting | Weekly |
| [Name] | Product Manager | High | Slack + Email | Daily |
| [Name] | Engineering Team | High | Slack + Standup | Daily |
| [Name] | QA Team | High | Slack + Meeting | As needed |
| [Name] | Support Team | Medium | Email | Pre/Post deployment |
| [Name] | Users | Low | Changelog + Blog | Post deployment |

### Communication Schedule

**Pre-Upgrade:**
- [ ] T-2 weeks: Announce upgrade plan to team
- [ ] T-1 week: Notify stakeholders of timeline
- [ ] T-3 days: Freeze code, final preparation
- [ ] T-1 day: Final stakeholder approval
- [ ] T-0: Deployment day notification

**During Upgrade:**
- [ ] Deploy start: Notify team upgrade in progress
- [ ] Milestones: Update on progress
- [ ] Issues: Immediate notification of blockers
- [ ] Deploy complete: Notify team and stakeholders

**Post-Upgrade:**
- [ ] Day 1: Success/status report
- [ ] Day 3: Stability update
- [ ] Week 1: Performance and metrics review
- [ ] Week 2: Retrospective and lessons learned

### Status Update Template

```
Subject: [UPGRADE-XXX] [Framework] Upgrade Status - [Date]

Status: [On Track / At Risk / Delayed]
Phase: [Preparation / Testing / Deployment / Monitoring]
Progress: [X]% complete

Completed:
- [Milestone 1]
- [Milestone 2]

In Progress:
- [Task currently working on]

Next Steps:
- [Upcoming task 1]
- [Upcoming task 2]

Risks/Issues:
- [Issue 1] - Severity: [High/Medium/Low] - Owner: [Name]
- [Issue 2] - Severity: [High/Medium/Low] - Owner: [Name]

Metrics:
- Tests passing: [X]/[Y]
- Performance: [Within range / Needs optimization]
- ETA: [Date]
```

## Documentation Updates

### Code Documentation
- [ ] Update inline comments for changed APIs
- [ ] Update docstrings/PHPDoc/JSDoc
- [ ] Update code examples in comments
- [ ] Update type hints/annotations

### Project Documentation
- [ ] Update `README.md` with new version
- [ ] Update installation instructions
- [ ] Update development setup guide
- [ ] Update deployment guide
- [ ] Update `docs/.claude/context/tech-stack.md`
- [ ] Update `docs/.claude/context/decision-log.md`

### Team Documentation
- [ ] Update team wiki/knowledge base
- [ ] Create upgrade runbook for future reference
- [ ] Document new features/patterns adopted
- [ ] Share lessons learned

### User-Facing Documentation
- [ ] Update API documentation
- [ ] Update user guides (if user-facing changes)
- [ ] Create changelog entry
- [ ] Write blog post/release notes (if public-facing)

## Timeline

**Planning Start:** [YYYY-MM-DD]
**Upgrade Start:** [YYYY-MM-DD]
**Target Completion:** [YYYY-MM-DD]
**Actual Completion:** [YYYY-MM-DD]

### Detailed Schedule

| Phase | Start | End | Duration | Status |
|-------|-------|-----|----------|--------|
| Planning & Preparation | [Date] | [Date] | [X days] | [Not Started/In Progress/Complete] |
| Dependency Audit | [Date] | [Date] | [X days] | [Not Started/In Progress/Complete] |
| Code Migration | [Date] | [Date] | [X days] | [Not Started/In Progress/Complete] |
| Testing | [Date] | [Date] | [X days] | [Not Started/In Progress/Complete] |
| Staging Deployment | [Date] | [Date] | [X days] | [Not Started/In Progress/Complete] |
| Production Deployment | [Date] | [Date] | [X days] | [Not Started/In Progress/Complete] |
| Monitoring | [Date] | [Date] | [X days] | [Not Started/In Progress/Complete] |

**Total Duration:** [X weeks]
**Contingency Buffer:** [Y days]

## Progress Tracking

### Checklist

**Preparation:**
- [ ] Breaking changes analyzed
- [ ] Dependencies audited
- [ ] Test coverage improved to [X]%
- [ ] All tests passing on current version
- [ ] Deprecation warnings fixed
- [ ] Performance baseline established
- [ ] Backup procedures verified
- [ ] Rollback plan documented

**Execution:**
- [ ] Dependencies updated
- [ ] Code migrated
- [ ] All tests passing on new version
- [ ] Performance benchmarks met
- [ ] Staging deployment successful
- [ ] Production deployment successful

**Post-Deployment:**
- [ ] Monitoring in place
- [ ] No critical issues
- [ ] Performance acceptable
- [ ] Documentation updated
- [ ] Team notified
- [ ] Retrospective completed

### Current Status
**Status:** [Planning/In Progress/Testing/Deploying/Complete/Rolled Back]
**Overall Progress:** [X]%
**Last Updated:** [YYYY-MM-DD]
**Next Milestone:** [Milestone name] - ETA: [Date]

### Blockers
- [ ] [Blocker 1] - Owner: [Name] - ETA: [Date]
- [ ] [Blocker 2] - Owner: [Name] - ETA: [Date]

## Post-Upgrade Review

### Final Metrics

| Metric | Before | After | Change | Target | Met? |
|--------|--------|-------|--------|--------|------|
| Framework Version | [X.Y.Z] | [A.B.C] | - | [A.B.C] | ✓ |
| Response Time (p95) | [X]ms | [Y]ms | [+/-Z]% | < [W]ms | ✓/✗ |
| Memory Usage | [X]MB | [Y]MB | [+/-Z]% | < [W]MB | ✓/✗ |
| DB Queries | [X] | [Y] | [+/-Z]% | < [W] | ✓/✗ |
| Test Coverage | [X]% | [Y]% | [+Z]% | > [W]% | ✓/✗ |
| Dependencies Updated | - | [X] | - | All | ✓/✗ |
| Deprecations Fixed | [X] | 0 | -100% | 0 | ✓/✗ |

### Actual vs Estimated

**Effort:**
- Estimated: [X hours]
- Actual: [Y hours]
- Variance: [+/-Z]%

**Timeline:**
- Estimated: [X days]
- Actual: [Y days]
- Variance: [+/-Z]%

**Issues Encountered:** [X]
**Rollbacks Required:** [X]

### Lessons Learned

**What Went Well:**
- [Success 1]
- [Success 2]
- [Success 3]

**What Could Be Improved:**
- [Improvement 1]
- [Improvement 2]
- [Improvement 3]

**Unexpected Challenges:**
- [Challenge 1] - Resolution: [How we solved it]
- [Challenge 2] - Resolution: [How we solved it]

**Best Practices Identified:**
- [Practice 1]
- [Practice 2]

**For Next Upgrade:**
- [Recommendation 1]
- [Recommendation 2]

### Benefits Realized

**Technical Benefits:**
- [ ] [Benefit 1] - Status: [Achieved/Partial/Not Achieved]
- [ ] [Benefit 2] - Status: [Achieved/Partial/Not Achieved]

**Business Benefits:**
- [ ] [Benefit 1] - Status: [Achieved/Partial/Not Achieved]
- [ ] [Benefit 2] - Status: [Achieved/Partial/Not Achieved]

**Developer Experience:**
- Satisfaction rating: [1-5 stars] ⭐⭐⭐⭐☆
- Comments: [Feedback from team]

## Related

- **Related Tech Debt:** [DEBT-XXX]
- **Related Refactoring:** [REFACTOR-XXX]
- **Related Upgrades:** [UPGRADE-XXX] (Previous upgrade)
- **Pull Request:** [Link]
- **Deployment Ticket:** [Link]
- **Retrospective Notes:** [Link]

---

**Status:** [Planning/In Progress/Testing/Deploying/Complete/Rolled Back]
**Last Updated:** [YYYY-MM-DD]
**Owner:** [Name/Team]
**Next Review:** [YYYY-MM-DD] (For future upgrade planning)

---

## Framework-Specific Notes

### Django Upgrades
- Check deprecation timeline: https://docs.djangoproject.com/en/stable/internals/deprecation/
- Review release notes: https://docs.djangoproject.com/en/stable/releases/
- Database migrations: Test extensively, may need data migrations
- Middleware order: May change between versions

### Laravel Upgrades
- Follow official upgrade guide: https://laravel.com/docs/upgrade
- Check Laravel Shift for automated upgrade: https://laravelshift.com/
- Config cache: `php artisan config:clear && php artisan config:cache`
- Route cache: `php artisan route:clear && php artisan route:cache`

### Vue/Nuxt Upgrades
- Migration guide: https://v3-migration.vuejs.org/ (Vue 2 → 3)
- Nuxt Bridge for gradual migration: https://nuxt.com/docs/bridge
- Composition API changes
- Build tool changes (Webpack → Vite)

### React/Next.js Upgrades
- Codemod tools: `npx @next/codemod <transform> <path>`
- Breaking changes: Check Next.js upgrade guide
- App Router migration (Next.js 13+)
- React 18 features (concurrent rendering, automatic batching)

### Python Version Upgrades
- Check compatibility: `vermin` tool
- Use `pyupgrade` for automatic syntax updates
- Virtual environment: Always test in clean environment
- C extensions: May need recompilation

# Deployment Checklist: [Release/Feature Name]

**Version:** [X.Y.Z]
**Date:** [YYYY-MM-DD]
**Environment:** [Staging/Production]
**Deployment Type:** [Standard/Hotfix/Rollback]
**Responsible:** [Name/Team]

---

## Pre-Deployment

### Code Quality
- [ ] All tests passing (unit, integration, E2E)
- [ ] Code review completed and approved
- [ ] No linting errors
- [ ] Type checking passed (if TypeScript/Python typed)
- [ ] Security scan completed (no critical/high vulnerabilities)
- [ ] Performance testing completed

### Documentation
- [ ] README updated (if needed)
- [ ] API documentation updated
- [ ] CHANGELOG updated
- [ ] Migration guide created (if breaking changes)
- [ ] Deployment notes documented

### Database
- [ ] Database migrations created
- [ ] Migrations tested on staging
- [ ] Migrations are reversible
- [ ] Data backup completed
- [ ] Rollback procedure documented

### Configuration
- [ ] Environment variables documented
- [ ] Config changes reviewed
- [ ] Secrets rotated (if needed)
- [ ] Feature flags configured
- [ ] Third-party service configs updated

### Dependencies
- [ ] All dependencies installed
- [ ] Lock file up to date
- [ ] No conflicting versions
- [ ] Security audit passed

---

## Deployment Preparation

### Communication
- [ ] Stakeholders notified
- [ ] Team informed
- [ ] Maintenance window scheduled (if downtime)
- [ ] Users notified (if user-facing changes)
- [ ] Support team briefed

### Rollback Plan
- [ ] Rollback procedure documented
- [ ] Previous version tagged
- [ ] Database rollback tested
- [ ] Rollback criteria defined
- [ ] RTO (Recovery Time Objective) defined: [X] minutes

### Monitoring
- [ ] Monitoring tools ready
- [ ] Alerts configured
- [ ] Dashboards prepared
- [ ] Error tracking enabled
- [ ] On-call engineer assigned

---

## Deployment Execution

### Build
- [ ] Build completed successfully
- [ ] Build artifacts verified
- [ ] Bundle size acceptable (< [X]KB)
- [ ] Source maps generated (if applicable)

### Staging Deployment
- [ ] Deployed to staging
- [ ] Smoke tests passed
- [ ] Database migrations successful
- [ ] No errors in logs
- [ ] Performance acceptable
- [ ] Stakeholder approval received

### Production Deployment

**Deployment Strategy:** [Blue-Green/Canary/Rolling/Big Bang]

**Deployment Steps:**
- [ ] Put application in maintenance mode (if needed)
- [ ] Backup production database
- [ ] Deploy new code
- [ ] Run database migrations
- [ ] Clear caches
- [ ] Restart application servers
- [ ] Exit maintenance mode
- [ ] Verify application starts

### Smoke Testing
- [ ] Homepage loads
- [ ] Login/logout works
- [ ] Critical user flows work
- [ ] API endpoints respond
- [ ] Database queries executing
- [ ] Background jobs running

---

## Post-Deployment

### Verification (First 30 minutes)
- [ ] No error spikes in logs
- [ ] Response times normal
- [ ] Database performance normal
- [ ] No failed background jobs
- [ ] User reports normal
- [ ] Metrics dashboards green

### Monitoring (First 24 hours)
- [ ] Hour 1: Check every 15 minutes
- [ ] Hour 2-4: Check every 30 minutes
- [ ] Hour 5-24: Check every 2 hours
- [ ] Monitor error rates (target: < 0.1%)
- [ ] Monitor response times (target: < baseline + 10%)
- [ ] Monitor resource usage (CPU, memory, disk)

### Metrics
| Metric | Before | After | Target | Status |
|--------|--------|-------|--------|--------|
| Error Rate | [X]% | [Y]% | < 0.1% | ✅/❌ |
| Response Time (p95) | [X]ms | [Y]ms | < [Z]ms | ✅/❌ |
| CPU Usage | [X]% | [Y]% | < 70% | ✅/❌ |
| Memory Usage | [X]GB | [Y]GB | < [Z]GB | ✅/❌ |
| Throughput | [X] req/s | [Y] req/s | > [Z] | ✅/❌ |

### Sign-Off
- [ ] Product Owner approval
- [ ] Tech Lead verification
- [ ] QA sign-off
- [ ] DevOps confirmation

---

## Rollback Procedure

**Rollback Criteria:**
- Error rate > 1%
- Response time degraded > 50%
- Critical functionality broken
- Data corruption detected

**Rollback Steps:**
```bash
# 1. Stop new deployments
# 2. Revert code
git revert [commit-range]
# or
git checkout v[previous-version]

# 3. Restore database (if migrations ran)
# [Database-specific rollback commands]

# 4. Redeploy previous version
./deploy.sh v[previous-version]

# 5. Verify rollback successful
curl https://api.example.com/health
[run smoke tests]

# 6. Notify team and stakeholders
```

**Rollback Time:** Target < [X] minutes

---

## Post-Deployment Tasks

### Immediate (Within 24 hours)
- [ ] Update monitoring dashboards
- [ ] Review error logs
- [ ] Check performance metrics
- [ ] Respond to user feedback

### Short-term (Within 1 week)
- [ ] Create release notes
- [ ] Update project documentation
- [ ] Archive deployment artifacts
- [ ] Conduct retrospective

### Long-term
- [ ] Monitor for patterns
- [ ] Plan next release
- [ ] Address technical debt identified
- [ ] Improve deployment process

---

## Lessons Learned

**What Went Well:**
- [Item 1]
- [Item 2]

**What Could Be Improved:**
- [Item 1]
- [Item 2]

**Action Items:**
- [ ] [Action 1] - Owner: [Name] - Due: [Date]
- [ ] [Action 2] - Owner: [Name] - Due: [Date]

---

## Notes

[Any additional notes, special considerations, or important information about this deployment]

---

**Deployment Status:** [Success/Partial/Failed/Rolled Back]
**Deployment Completed:** [YYYY-MM-DD HH:MM UTC]
**Verified By:** [Name]

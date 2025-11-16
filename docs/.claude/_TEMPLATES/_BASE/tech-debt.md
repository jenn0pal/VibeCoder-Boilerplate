# Tech Debt: [Brief Description]

> **Template for tracking and managing technical debt**
>
> Use this template to document technical debt items that require planning and eventual resolution.
> For immediate fixes, use the appropriate workflow (bug fix, refactor, upgrade, etc.).

## Overview

**Debt ID:** DEBT-[ID]
**Date Identified:** [YYYY-MM-DD]
**Type:** [Framework Upgrade/Dependency Update/Code Refactoring/Performance/Security/Architecture/Documentation]
**Priority:** [Critical/High/Medium/Low]
**Estimated Effort:** [Hours/Days/Weeks]
**Target Resolution:** [YYYY-MM-DD or Sprint/Quarter]

## Problem Statement

### What is the Technical Debt?
[Clear description of the technical debt - what's outdated, suboptimal, or risky]

### Why Does This Exist?
[Context: Why was this done this way? Time constraints? Technology limitations? Lack of knowledge?]

### Current Impact
**Severity:** [Critical/High/Medium/Low]

**Current consequences:**
- **Development Velocity:** [How it slows down development]
- **Maintainability:** [How it affects code maintenance]
- **Performance:** [Any performance impact]
- **Security:** [Any security implications]
- **User Experience:** [Any user-facing impact]
- **Cost:** [Operational or development cost impact]

**Affected Components:**
- [Component/Module 1]
- [Component/Module 2]
- [Component/Module 3]

### Future Impact if Not Addressed

**Short-term (1-3 months):**
- [Risk 1]
- [Risk 2]

**Medium-term (3-6 months):**
- [Risk 1]
- [Risk 2]

**Long-term (6+ months):**
- [Risk 1]
- [Risk 2]

## Classification

### Debt Category
- [ ] **Deliberate & Prudent** - Conscious decision, well-documented
- [ ] **Deliberate & Reckless** - Conscious decision, poor judgment
- [ ] **Inadvertent & Prudent** - Learned better approach later
- [ ] **Inadvertent & Reckless** - Lack of skill/knowledge

### Technical Debt Quadrant
```
           Reckless
               |
    "We don't have time" | "What's layering?"
               |
Deliberate ------------- Inadvertent
               |
    "We must ship now"  | "Now we know how"
               |
           Prudent
```

**Selected:** [Which quadrant]

### Root Cause
- [ ] Time constraints/Deadline pressure
- [ ] Lack of knowledge/experience
- [ ] Technology limitations at the time
- [ ] Changing requirements
- [ ] Dependencies/External factors
- [ ] Team turnover/Lost knowledge
- [ ] Deferred maintenance
- [ ] Other: [Specify]

## Current State

### Technical Details
[Detailed technical description of the current implementation]

```[language]
// Code example showing the problematic implementation
// Include comments explaining why this is tech debt
```

### Dependencies & Constraints
**Current Dependencies:**
- [Library/Framework] version [X.X.X]
- [Service/API] version [X.X.X]

**Technical Constraints:**
- [Constraint 1]
- [Constraint 2]

**Business Constraints:**
- [Constraint 1]
- [Constraint 2]

### Metrics
**Current Performance:**
- Response time: [X]ms
- Memory usage: [X]MB
- Database queries: [X]
- Code complexity: [X]
- Test coverage: [X]%

**Current Size:**
- Lines of code affected: [X]
- Files affected: [X]
- Components affected: [X]

## Desired State

### Target Resolution
[Describe what "resolved" looks like for this tech debt]

### Expected Benefits
**Technical Benefits:**
- [Benefit 1]
- [Benefit 2]
- [Benefit 3]

**Business Benefits:**
- [Benefit 1]
- [Benefit 2]

**User Benefits:**
- [Benefit 1]
- [Benefit 2]

### Target Metrics
**Performance Improvements:**
- Response time: < [X]ms ([Y]% improvement)
- Memory usage: < [X]MB ([Y]% reduction)
- Database queries: < [X] ([Y]% reduction)
- Code complexity: < [X] ([Y]% reduction)
- Test coverage: > [X]% ([Y]% increase)

### Example Implementation
```[language]
// Code example showing the desired implementation
// Include comments explaining the improvements
```

## Resolution Strategy

### Approach Options

#### Option 1: [Approach Name]
**Description:** [How this would work]

**Pros:**
- [Pro 1]
- [Pro 2]

**Cons:**
- [Con 1]
- [Con 2]

**Effort:** [Hours/Days/Weeks]
**Risk:** [Low/Medium/High]

#### Option 2: [Approach Name]
**Description:** [How this would work]

**Pros:**
- [Pro 1]
- [Pro 2]

**Cons:**
- [Con 1]
- [Con 2]

**Effort:** [Hours/Days/Weeks]
**Risk:** [Low/Medium/High]

#### Option 3: Do Nothing
**Description:** Accept the debt and continue as-is

**Pros:**
- No immediate effort required
- Team can focus on features

**Cons:**
- Debt accumulates
- Future cost increases
- Risk increases over time

**Cost of Inaction:** [What happens if we don't fix this?]

### Recommended Approach
**Selected Option:** [Option X]

**Justification:**
[Why this approach is best given current constraints and priorities]

**Estimated ROI:**
- Time saved per sprint: [X hours]
- Payback period: [X sprints/months]
- Long-term savings: [X hours/year]

## Implementation Plan

### Prerequisites
- [ ] [Prerequisite 1 - e.g., Upgrade to latest framework version]
- [ ] [Prerequisite 2 - e.g., Achieve 80% test coverage]
- [ ] [Prerequisite 3 - e.g., Stakeholder approval]

### High-Level Steps

#### Phase 1: [Preparation]
**Duration:** [X days/weeks]
**Tasks:**
- [ ] [Task 1]
- [ ] [Task 2]
- [ ] [Task 3]

**Success Criteria:**
- [Criterion 1]
- [Criterion 2]

#### Phase 2: [Implementation]
**Duration:** [X days/weeks]
**Tasks:**
- [ ] [Task 1]
- [ ] [Task 2]
- [ ] [Task 3]

**Success Criteria:**
- [Criterion 1]
- [Criterion 2]

#### Phase 3: [Validation & Rollout]
**Duration:** [X days/weeks]
**Tasks:**
- [ ] [Task 1]
- [ ] [Task 2]
- [ ] [Task 3]

**Success Criteria:**
- [Criterion 1]
- [Criterion 2]

### Detailed Implementation
**For detailed implementation, create one of:**
- `REFACTOR-[ID].md` - For code refactoring
- `UPGRADE-[ID].md` - For framework/dependency upgrades
- `MIGRATION-[ID].md` - For data/architecture migrations
- `MOD-[ID].md` - For code modifications

**Reference:** [Link to detailed implementation plan]

## Risk Assessment

### Technical Risks
| Risk | Likelihood | Impact | Mitigation Strategy |
|------|------------|--------|-------------------|
| Breaking existing functionality | [L/M/H] | [L/M/H] | Comprehensive test suite |
| Performance regression | [L/M/H] | [L/M/H] | Performance benchmarks |
| Data loss/corruption | [L/M/H] | [L/M/H] | Backup and validation |
| Dependency conflicts | [L/M/H] | [L/M/H] | Dependency audit |
| Integration issues | [L/M/H] | [L/M/H] | Integration tests |

### Business Risks
| Risk | Likelihood | Impact | Mitigation Strategy |
|------|------------|--------|-------------------|
| Missed deadlines | [L/M/H] | [L/M/H] | Buffer time, phased approach |
| User disruption | [L/M/H] | [L/M/H] | Gradual rollout, communication |
| Team capacity | [L/M/H] | [L/M/H] | Resource planning |
| Budget overrun | [L/M/H] | [L/M/H] | Cost estimation, monitoring |

### Rollback Plan
**If resolution fails or causes critical issues:**

```bash
# Rollback steps
git revert [commit-range]
# Or restore from specific commit
git reset --hard [safe-commit-hash]

# Restore dependencies
pip install -r requirements.txt.backup
# or
npm install --from-lockfile
```

**Rollback Criteria:**
- [Criterion 1 - e.g., Error rate > 1%]
- [Criterion 2 - e.g., Performance degrades > 20%]
- [Criterion 3 - e.g., Critical functionality broken]

**Recovery Time Objective (RTO):** [X minutes/hours]

## Resource Requirements

### Team Members Needed
| Role | Person | Allocation | Duration |
|------|--------|------------|----------|
| [Tech Lead] | [Name] | [X]% | [X weeks] |
| [Backend Dev] | [Name] | [X]% | [X weeks] |
| [Frontend Dev] | [Name] | [X]% | [X weeks] |
| [QA Engineer] | [Name] | [X]% | [X weeks] |
| [DevOps] | [Name] | [X]% | [X weeks] |

### External Dependencies
- [ ] [External team/service 1]
- [ ] [External team/service 2]
- [ ] [Third-party vendor]

### Budget/Costs
**Development Cost:** [X hours × $Y/hour = $Z]
**Infrastructure Cost:** [Additional costs for staging, testing, etc.]
**Total Estimated Cost:** $[Z]

**Cost of Inaction:** $[X] per month/year in:
- Developer time wasted
- Performance costs
- Support burden
- Lost opportunities

## Timeline

**Discovery Date:** [YYYY-MM-DD]
**Decision Date:** [YYYY-MM-DD]
**Planned Start:** [YYYY-MM-DD]
**Target Completion:** [YYYY-MM-DD]
**Actual Completion:** [YYYY-MM-DD]

### Milestones
- [ ] [Milestone 1] - [Date]
- [ ] [Milestone 2] - [Date]
- [ ] [Milestone 3] - [Date]
- [ ] [Milestone 4] - [Date]

### Sprint/Quarter Planning
**Sprint:** [Sprint number/name]
**Quarter:** [Q1/Q2/Q3/Q4 YYYY]
**Release:** [Version X.X.X]

## Monitoring & Validation

### Success Metrics
**Quantitative:**
- [ ] Performance improved by [X]%
- [ ] Code complexity reduced by [X]%
- [ ] Test coverage increased to [X]%
- [ ] Bug reports decreased by [X]%
- [ ] Development velocity increased by [X]%

**Qualitative:**
- [ ] Developer satisfaction improved
- [ ] Code maintainability improved
- [ ] Documentation completeness
- [ ] Team confidence in system

### Monitoring Dashboard
**Metrics to track post-resolution:**
- [Metric 1] - Target: [X], Alert if: [Y]
- [Metric 2] - Target: [X], Alert if: [Y]
- [Metric 3] - Target: [X], Alert if: [Y]

**Tools:**
- [Monitoring tool 1]
- [Monitoring tool 2]

### Validation Tests
- [ ] All unit tests pass
- [ ] All integration tests pass
- [ ] Performance benchmarks met
- [ ] Security audit passed
- [ ] Accessibility checks passed
- [ ] User acceptance testing passed

## Communication Plan

### Stakeholders
| Stakeholder | Role | Interest Level | Communication Method |
|-------------|------|----------------|---------------------|
| [Name] | [Role] | High/Medium/Low | [Email/Slack/Meeting] |
| [Name] | [Role] | High/Medium/Low | [Email/Slack/Meeting] |

### Communication Schedule
- **Kickoff:** [Date] - Project initiation meeting
- **Weekly Updates:** [Day] - Progress updates to team
- **Mid-Point Review:** [Date] - Assessment and adjustments
- **Pre-Launch:** [Date] - Final review and go/no-go decision
- **Post-Launch:** [Date] - Results review and retrospective

### Status Updates Template
```
Subject: [DEBT-XXX] Tech Debt Resolution Update - [Date]

Status: [On Track / At Risk / Blocked]
Progress: [X]% complete
Completed This Week:
- [Item 1]
- [Item 2]

Planned Next Week:
- [Item 1]
- [Item 2]

Risks/Blockers:
- [Issue 1]
- [Issue 2]

Metrics:
- [Metric 1]: Current [X], Target [Y]
```

## Documentation Updates

### Code Documentation
- [ ] Update inline comments
- [ ] Update function/method docstrings
- [ ] Update type definitions
- [ ] Update API documentation

### Architecture Documentation
- [ ] Update `docs/.claude/context/tech-stack.md`
- [ ] Update `docs/.claude/context/decision-log.md`
- [ ] Update architecture diagrams
- [ ] Update README.md

### Knowledge Sharing
- [ ] Create runbook/playbook if needed
- [ ] Document new patterns/practices
- [ ] Update team wiki
- [ ] Conduct knowledge transfer session

## Related Items

- **Related Tech Debt:** [DEBT-XXX, DEBT-YYY]
- **Related Features:** [FEAT-XXX]
- **Related Bugs:** [BUG-XXX]
- **Related Refactoring:** [REFACTOR-XXX]
- **Related Upgrades:** [UPGRADE-XXX]
- **Pull Requests:** [Links]
- **Issues/Discussions:** [Links]

## Progress Tracking

### Status Log
| Date | Status | Progress | Notes |
|------|--------|----------|-------|
| [YYYY-MM-DD] | Identified | 0% | Initial discovery |
| [YYYY-MM-DD] | Documented | 10% | Created DEBT doc |
| [YYYY-MM-DD] | Approved | 10% | Stakeholder approval |
| [YYYY-MM-DD] | In Progress | 25% | Started implementation |
| [YYYY-MM-DD] | In Progress | 50% | Mid-point |
| [YYYY-MM-DD] | In Review | 90% | Code review |
| [YYYY-MM-DD] | Resolved | 100% | Deployed to production |

### Current Status
**Status:** [Identified/Documented/Approved/In Progress/In Review/Resolved/Deferred/Cancelled]
**Progress:** [X]%
**Last Updated:** [YYYY-MM-DD]

### Blockers
- [ ] [Blocker 1] - Owner: [Name] - ETA: [Date]
- [ ] [Blocker 2] - Owner: [Name] - ETA: [Date]

## Decision History

### Decision 1: [Decision Title]
**Date:** [YYYY-MM-DD]
**Decision:** [What was decided]
**Rationale:** [Why this decision was made]
**Impact:** [How this affects the resolution]

### Decision 2: [Decision Title]
**Date:** [YYYY-MM-DD]
**Decision:** [What was decided]
**Rationale:** [Why this decision was made]
**Impact:** [How this affects the resolution]

## Post-Resolution Review

### Actual Results
**Effort:** [X hours/days] (Estimated: [Y hours/days])
**Cost:** $[X] (Estimated: $[Y])
**Duration:** [X weeks] (Estimated: [Y weeks])

**Metrics Achieved:**
| Metric | Before | After | Change | Target | Met? |
|--------|--------|-------|--------|--------|------|
| Performance | [X]ms | [Y]ms | [Z]% | [A]ms | ✓/✗ |
| Complexity | [X] | [Y] | [Z]% | [A] | ✓/✗ |
| Test Coverage | [X]% | [Y]% | [Z]% | [A]% | ✓/✗ |
| Bug Reports | [X]/mo | [Y]/mo | [Z]% | [A]/mo | ✓/✗ |

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
- [Challenge 1] - How resolved: [Solution]
- [Challenge 2] - How resolved: [Solution]

**Best Practices Identified:**
- [Practice 1]
- [Practice 2]

**Anti-Patterns Avoided:**
- [Anti-pattern 1]
- [Anti-pattern 2]

### Recommendations for Future

**Process Improvements:**
- [Improvement 1]
- [Improvement 2]

**Technical Improvements:**
- [Improvement 1]
- [Improvement 2]

**Preventing Similar Debt:**
- [Prevention strategy 1]
- [Prevention strategy 2]

### Follow-up Items
- [ ] [Follow-up 1] - Create: [DEBT-XXX/REFACTOR-XXX]
- [ ] [Follow-up 2] - Create: [DEBT-XXX/REFACTOR-XXX]

## Retrospective

### Team Feedback
**Developer Satisfaction:** [1-5 stars] ⭐⭐⭐⭐☆

**Comments:**
- "[Quote from team member]" - [Name]
- "[Quote from team member]" - [Name]

### Impact Assessment (3 months post-resolution)
**Actual Impact:**
- Development velocity: [Impact]
- Code quality: [Impact]
- Bug frequency: [Impact]
- Team morale: [Impact]

**Would we do it again?** [Yes/No/Maybe]
**Why or why not?** [Explanation]

---

**Status:** [Identified/Documented/Approved/In Progress/In Review/Resolved/Deferred/Cancelled]
**Last Updated:** [YYYY-MM-DD]
**Owner:** [Name/Team]
**Next Review:** [YYYY-MM-DD]

---

## Quick Reference

### Priority Guidelines
- **Critical:** Security vulnerability, production down, data loss risk
- **High:** Major performance issue, blocking feature development
- **Medium:** Moderate impact on velocity or quality
- **Low:** Minor inconvenience, future improvement

### Effort Estimation
- **Hours:** Small refactor, dependency update
- **Days:** Medium refactor, minor framework upgrade
- **Weeks:** Major refactor, framework migration, architecture change

### Resolution Timeline
- **Critical:** Within 1 sprint
- **High:** Within 1-2 quarters
- **Medium:** Within 2-4 quarters
- **Low:** Backlog, opportunistic resolution

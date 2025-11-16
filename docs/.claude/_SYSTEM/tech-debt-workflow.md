# Technical Debt Management Workflow

> **System guide for managing technical debt in your project**
>
> This guide explains how to identify, track, prioritize, and resolve technical debt using the VibeCoder workflow.

## Table of Contents

1. [Overview](#overview)
2. [When to Create Tech Debt Items](#when-to-create-tech-debt-items)
3. [Tech Debt Classification](#tech-debt-classification)
4. [Workflow Steps](#workflow-steps)
5. [Directory Structure](#directory-structure)
6. [Templates Available](#templates-available)
7. [Prompts Reference](#prompts-reference)
8. [Best Practices](#best-practices)
9. [Examples](#examples)

## Overview

Technical debt is code or infrastructure that is suboptimal and will eventually need improvement. Like financial debt, it accrues "interest" in the form of:
- Slower development velocity
- Increased bug frequency
- Higher maintenance costs
- Difficulty implementing new features
- Security vulnerabilities
- Performance issues

**Goal:** Systematically track and resolve technical debt before it becomes unmanageable.

## When to Create Tech Debt Items

### Always Track These

1. **Security Vulnerabilities**
   - CVEs in dependencies
   - Insecure code patterns
   - Authentication/authorization gaps
   - Unencrypted sensitive data

2. **Framework/Library Upgrades**
   - Major version behind (e.g., Django 3.x when 5.x is available)
   - End-of-life/End-of-support versions
   - Deprecated features being used
   - Security-only support versions

3. **Performance Issues**
   - N+1 query problems
   - Memory leaks
   - Slow API endpoints (> acceptable threshold)
   - Large bundle sizes (frontend)
   - Database query optimization needed

4. **Code Quality Issues**
   - High cyclomatic complexity (> 15)
   - Code duplication (> 10% similarity)
   - Low test coverage (< 70%)
   - Large functions/classes (> 300 lines)
   - Poor separation of concerns

5. **Architecture Debt**
   - Monolith that should be microservices (or vice versa)
   - Missing abstraction layers
   - Tight coupling between components
   - Violates SOLID principles
   - Inconsistent patterns

6. **Documentation Debt**
   - Missing API documentation
   - Outdated architecture diagrams
   - No runbooks for critical operations
   - Undocumented business logic

### Don't Track These

- **Wishlist features** - Use feature spec instead
- **Nice-to-have improvements** - Low priority, may never do
- **Personal preferences** - "I prefer X over Y" (unless entire team agrees)
- **Already fixed issues** - Archive instead
- **Bikeshedding** - Tab vs spaces, naming conventions (unless causing real issues)

## Tech Debt Classification

### By Type

| Type | Template | Example |
|------|----------|---------|
| Framework Upgrade | `framework-upgrade.md` | Django 4.2 → 5.0 |
| Dependency Upgrade | `dependency-upgrade.md` | requests 2.28 → 2.31 (CVE fix) |
| Code Refactoring | `refactoring-plan.md` | Split monolithic service |
| Performance | `tech-debt.md` | Optimize slow queries |
| Security | `tech-debt.md` | Implement rate limiting |
| Architecture | `tech-debt.md` | Introduce service layer |
| Data Migration | `migration-strategy.md` | Move to PostgreSQL from MySQL |
| Breaking Change | `breaking-change-assessment.md` | Change API response format |

### By Priority

#### Critical
**Timeline:** Immediate (within 1 week)
**Examples:**
- Security vulnerability being actively exploited
- Production down or degraded
- Data loss risk
- Legal/compliance violation

**Action:** Drop everything, fix immediately

#### High
**Timeline:** Within 1-2 sprints (2-4 weeks)
**Examples:**
- Security vulnerability (CVE)
- Framework 2+ major versions behind
- Deprecated feature being removed in next version
- Performance issues affecting users
- Blocking feature development

**Action:** Schedule in next sprint

#### Medium
**Timeline:** Within 1-2 quarters (3-6 months)
**Examples:**
- Framework 1 major version behind
- Code quality issues
- Technical debt slowing development by < 20%
- Missing tests for critical paths

**Action:** Add to roadmap, schedule when capacity allows

#### Low
**Timeline:** Backlog, opportunistic
**Examples:**
- Minor refactoring improvements
- Documentation gaps
- Code style inconsistencies
- "Would be nice to have"

**Action:** Fix when working in that area, or when team has downtime

### By Impact

**Development Velocity Impact:**
- High: Slows development by > 30%
- Medium: Slows development by 10-30%
- Low: Slows development by < 10%

**User Impact:**
- High: Directly affects user experience
- Medium: Affects some users or edge cases
- Low: No user-facing impact

**Risk Impact:**
- High: Security vulnerability, data loss risk, compliance violation
- Medium: Potential for bugs, performance issues
- Low: Minimal risk

## Workflow Steps

### 1. Identify Tech Debt

**How tech debt is discovered:**
- During code reviews
- While implementing features
- Security audits / dependency scans
- Performance monitoring alerts
- User complaints / bug reports
- Scheduled tech debt review meetings

**Ask yourself:**
- Is this something we should fix? (vs. accept as-is)
- What's the cost of NOT fixing it?
- What's the cost of fixing it?
- When should we fix it?

### 2. Document Tech Debt

**Use the appropriate template:**

```bash
# For general tech debt
docs/.claude/tech-debt/DEBT-001-[brief-name].md

# For framework upgrades
docs/.claude/upgrades/UPGRADE-001-django-5.md

# For dependency upgrades
docs/.claude/upgrades/DEP-001-requests-upgrade.md

# For refactoring
docs/.claude/refactoring/REFACTOR-001-service-layer.md

# For migrations
docs/.claude/migrations/MIGRATION-001-postgres.md
```

**Prompt to use:**
```
Load CLAUDE.md and docs/.claude/context/conventions.md

Tech Debt: [Brief description]
Type: [Type]
Priority: [Priority]
Estimated Effort: [Effort]

Current impact:
- [Impact 1]
- [Impact 2]

Please help me:
1. Assess the scope and complexity
2. Create a tech debt tracking document (DEBT-[ID].md)
3. Develop an implementation plan
4. Identify risks and dependencies
5. Provide timeline estimate
```

### 3. Prioritize Tech Debt

**Use the prioritization matrix:**

```
         High Impact
             │
    Critical │ High
  ───────────┼───────────
       Low   │ Medium
             │
         Low Impact

      High Effort → Low Effort
```

**Priority Formula:**
```
Priority = (Impact × Urgency) / Effort

Impact = (Velocity Impact + User Impact + Risk Impact) / 3
Urgency = Days until becomes critical / 365
Effort = Estimated hours / 8

High Priority: Score > 5
Medium Priority: Score 2-5
Low Priority: Score < 2
```

**Add to decision log:**
```markdown
## Decision: [Date] - Prioritize DEBT-001 as High Priority

**Context:** DEBT-001 (Django upgrade) scores 7.5 on priority formula

**Decision:** Schedule for Sprint 12

**Rationale:**
- Security vulnerabilities in current version
- Blocking adoption of new features
- Effort is manageable (3 days)

**Consequences:**
- Feature X delayed by 1 sprint
- Improved security posture
- Enables future features
```

### 4. Plan Resolution

**Choose resolution strategy:**

1. **Fix Now** - Critical items, schedule immediately
2. **Schedule** - High/Medium items, add to roadmap
3. **Defer** - Low priority, revisit quarterly
4. **Accept** - Cost of fix > benefit, document decision

**Create implementation plan using appropriate template:**
- Framework upgrade → `framework-upgrade.md`
- Refactoring → `refactoring-plan.md`
- Migration → `migration-strategy.md`

### 5. Execute Resolution

**Follow the plan created in step 4:**
- Use the prompts in CLAUDE.md
- Follow the phase-by-phase approach
- Test thoroughly
- Document changes
- Update decision log

### 6. Validate Resolution

**Verify the tech debt is resolved:**
- [ ] Original issue no longer exists
- [ ] Tests pass
- [ ] Performance metrics improved (if applicable)
- [ ] No new issues introduced
- [ ] Documentation updated

**Update tech debt tracking:**
- Mark as "Resolved"
- Record actual effort vs estimated
- Document lessons learned
- Archive the document

### 7. Close & Review

**Post-resolution activities:**
- Move document to appropriate archive
- Update `docs/.claude/context/decision-log.md`
- Share learnings with team
- Retrospective: What went well? What could be better?

## Directory Structure

```
docs/.claude/
├── tech-debt/              # General technical debt
│   ├── DEBT-001-slow-queries.md
│   ├── DEBT-002-test-coverage.md
│   └── README.md           # Index of tech debt items
│
├── upgrades/               # Framework & dependency upgrades
│   ├── UPGRADE-001-django-5.md
│   ├── UPGRADE-002-python-3.12.md
│   ├── DEP-001-requests-upgrade.md
│   └── README.md
│
├── refactoring/            # Code refactoring plans
│   ├── REFACTOR-001-service-layer.md
│   └── README.md
│
├── migrations/             # Data/platform migrations
│   ├── MIGRATION-001-postgres.md
│   └── README.md
│
└── context/
    └── decision-log.md     # Record tech debt decisions
```

**Best practice:** Create a README.md in each directory to index items:

```markdown
# Technical Debt Items

## Active

| ID | Description | Priority | Est. Effort | Status |
|----|-------------|----------|-------------|--------|
| DEBT-001 | Optimize slow queries | High | 2 days | In Progress |
| DEBT-002 | Increase test coverage | Medium | 5 days | Planned |

## Resolved

| ID | Description | Resolved Date | Actual Effort |
|----|-------------|---------------|---------------|
| DEBT-003 | Upgrade Django | 2024-01-15 | 3 days |
```

## Templates Available

### 1. tech-debt.md
**Use for:** General technical debt tracking

**Covers:**
- Problem statement and impact
- Classification and prioritization
- Resolution strategy options
- Implementation plan
- Risk assessment
- Progress tracking

**Example:** Performance optimization, security improvements, code quality

### 2. framework-upgrade.md
**Use for:** Upgrading frameworks (Django, Laravel, Vue, React, etc.)

**Covers:**
- Version analysis and breaking changes
- Dependency compatibility
- Pre-upgrade preparation
- Phase-by-phase execution plan
- Testing and validation
- Rollback strategy

**Example:** Django 4.2 → 5.0, Laravel 10 → 11, Vue 2 → 3

### 3. dependency-upgrade.md
**Use for:** Upgrading individual packages/libraries

**Covers:**
- Package analysis
- Compatibility testing
- Code impact assessment
- Upgrade execution
- Monitoring

**Example:** requests 2.28 → 2.31, axios 0.x → 1.x

### 4. refactoring-plan.md
**Use for:** Significant code refactoring

**Covers:**
- Current state analysis
- Code smells identified
- Refactoring techniques
- Phase-by-phase approach
- Testing strategy
- Performance impact

**Example:** Extract service layer, introduce repository pattern

### 5. breaking-change-assessment.md
**Use for:** Evaluating proposed breaking changes

**Covers:**
- Impact analysis
- Migration strategy
- Communication plan
- Rollback procedure
- Cost-benefit analysis

**Example:** API v1 → v2, database schema change

### 6. migration-strategy.md
**Use for:** Data or platform migrations

**Covers:**
- Current and target state
- Data transformations
- Migration approach (big bang, phased, etc.)
- Data integrity validation
- Zero-downtime strategy

**Example:** MySQL → PostgreSQL, AWS → GCP

## Prompts Reference

### Track Technical Debt
```
Load CLAUDE.md and docs/.claude/context/conventions.md

Tech Debt: [Brief description]
Type: [Framework Upgrade/Dependency Update/Code Refactoring/Performance/Security]
Priority: [Critical/High/Medium/Low]
Estimated Effort: [Hours/Days/Weeks]

Current impact:
- [Impact 1]
- [Impact 2]
- [Impact 3]

Please help me:
1. Assess the scope and complexity
2. Create a tech debt tracking document (DEBT-[ID].md)
3. Develop an implementation plan
4. Identify risks and dependencies
5. Provide timeline estimate
```

### Upgrade Framework
```
Load CLAUDE.md and docs/.claude/context/tech-stack.md

Framework Upgrade: [Framework name]
From: [Current version]
To: [Target version]
Upgrade Type: [Major/Minor/Patch]

Reason: [Why upgrade now?]

Please help me:
1. Check breaking changes in release notes
2. Audit package compatibility
3. Create upgrade plan with rollback strategy (UPGRADE-[ID].md)
4. Execute upgrade incrementally
5. Validate with comprehensive tests
6. Update documentation
```

### Upgrade Dependency
```
Load CLAUDE.md and docs/.claude/context/tech-stack.md

Dependency Upgrade: [package-name]
From: [current version]
To: [target version]
Type: [Major/Minor/Patch]

Reason: [Security/Bug fix/New feature/Maintenance]
CVE ID (if applicable): [CVE-YYYY-XXXXX]

Please help me:
1. Check breaking changes and compatibility
2. Assess impact on our codebase
3. Create dependency upgrade plan (DEP-[ID].md)
4. Test upgrade in isolation
5. Update code if needed
6. Deploy to staging then production
```

### Assess Breaking Change
```
Load CLAUDE.md and docs/.claude/context/conventions.md

Breaking Change: [Description]
Type: [API Change/Database Schema/Configuration/Dependency Upgrade]
Severity: [Critical/High/Medium/Low]

Proposed change:
[What we want to change and why]

Affects:
- [Who/what is affected]

Please help me:
1. Analyze impact and blast radius
2. Create breaking change assessment (BREAK-[ID].md)
3. Develop migration strategy
4. Plan communication timeline
5. Create migration tools/scripts
6. Document rollback procedure
```

### Plan Data Migration
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

## Best Practices

### 1. Regular Tech Debt Review

**Schedule quarterly tech debt reviews:**
- Review all open tech debt items
- Re-prioritize based on current context
- Close resolved items
- Identify new tech debt

**Meeting agenda:**
1. Review metrics (velocity, bug rate, security scan results)
2. Discuss new tech debt discovered
3. Re-prioritize existing items
4. Allocate capacity for next quarter
5. Celebrate resolved items

### 2. Tech Debt Budget

**Allocate percentage of sprint capacity:**
- 10-20% of sprint capacity for tech debt
- Critical items can exceed budget
- Track tech debt resolved vs accrued

**Example:**
- Sprint capacity: 100 story points
- Tech debt budget: 15 points
- Must resolve 15 points of tech debt per sprint

### 3. Boy Scout Rule

**"Leave code better than you found it"**

When working in an area with tech debt:
- Fix small issues immediately
- Document larger issues for later
- Don't make it worse

**Examples:**
- Add missing test while fixing bug
- Extract complex function while adding feature
- Fix deprecation warning while in the area

### 4. Prevent Tech Debt

**Prevention is cheaper than cure:**

- [ ] Code review checklist includes tech debt check
- [ ] Automated security scanning (Dependabot, Snyk)
- [ ] Automated dependency updates (Renovate)
- [ ] Performance budgets enforced
- [ ] Test coverage requirements
- [ ] Deprecation warnings fail CI

### 5. Make Tech Debt Visible

**Transparency enables prioritization:**

- Dashboard showing tech debt items
- Monthly report to stakeholders
- Include in sprint planning
- Celebrate when resolved

**Example dashboard metrics:**
- Total tech debt items: 12
- Critical: 0
- High: 3
- Medium: 6
- Low: 3
- Resolved this month: 4

### 6. Document Decisions

**Every tech debt decision should be in decision log:**

```markdown
## Decision: Accept DEBT-005 (Monolithic Architecture)

**Date:** 2024-01-15
**Status:** Accepted
**Decision Makers:** Tech Lead, CTO

**Context:**
DEBT-005 suggests splitting monolith into microservices

**Decision:**
Accept as-is for now, revisit in 6 months

**Rationale:**
- Current scale doesn't justify microservices complexity
- Team lacks microservices experience
- Focus on product-market fit first
- Will revisit when traffic > 10k req/sec

**Consequences:**
- Faster feature delivery in short term
- May need larger refactor later
- Monitoring monolith performance closely

**Review Date:** 2024-07-15
```

## Examples

### Example 1: Security Vulnerability

**Scenario:** Dependabot alerts on critical CVE in requests library

**Steps:**
1. **Identify:** CVE-2023-XXXXX in requests 2.28.0
2. **Document:** Create DEP-001-requests-upgrade.md
3. **Prioritize:** Critical (security vulnerability)
4. **Plan:** Test upgrade to 2.31.0
5. **Execute:** Upgrade dependency
6. **Validate:** Security scan passes
7. **Close:** Mark as resolved

**Timeline:** Same day

### Example 2: Framework Upgrade

**Scenario:** Django 4.2 is 2 major versions behind

**Steps:**
1. **Identify:** Currently on Django 4.2, latest is 5.1
2. **Document:** Create UPGRADE-001-django-5.md
3. **Prioritize:** High (multiple versions behind)
4. **Plan:** Incremental upgrade 4.2 → 5.0 → 5.1
5. **Execute:** Follow multi-phase plan
6. **Validate:** All tests pass, performance good
7. **Close:** Document lessons learned

**Timeline:** 2-3 sprints

### Example 3: Performance Optimization

**Scenario:** API endpoint taking 2+ seconds

**Steps:**
1. **Identify:** /api/users endpoint slow
2. **Document:** Create DEBT-003-optimize-users-api.md
3. **Prioritize:** High (user-facing performance issue)
4. **Plan:** Implement eager loading, caching
5. **Execute:** Optimize queries, add Redis cache
6. **Validate:** Response time < 200ms
7. **Close:** Performance goal met

**Timeline:** 1 sprint

### Example 4: Refactoring

**Scenario:** Business logic mixed with views

**Steps:**
1. **Identify:** Fat controllers, no service layer
2. **Document:** Create REFACTOR-001-service-layer.md
3. **Prioritize:** Medium (slowing development)
4. **Plan:** Incremental extraction to service layer
5. **Execute:** Module by module refactoring
6. **Validate:** Tests pass, code cleaner
7. **Close:** Architecture improved

**Timeline:** 3-4 sprints (incremental)

---

## Summary

**Tech debt workflow in 7 steps:**
1. **Identify** - Find tech debt during development
2. **Document** - Use appropriate template
3. **Prioritize** - Critical → High → Medium → Low
4. **Plan** - Choose strategy, create detailed plan
5. **Execute** - Follow plan, test thoroughly
6. **Validate** - Verify resolution, no regressions
7. **Close** - Archive, document learnings

**Key principles:**
- Make tech debt visible
- Prioritize ruthlessly
- Allocate dedicated capacity
- Prevent new tech debt
- Document all decisions
- Celebrate wins

**Remember:**
- Some tech debt is acceptable
- Not all tech debt needs fixing
- Focus on high-impact items
- Prevention is cheaper than cure

---

**Last Updated:** 2024-01-15
**Maintained By:** VibeCoder Team

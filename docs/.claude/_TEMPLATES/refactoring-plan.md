# Refactoring Plan: [Component/Module Name]

> **Template for planning and documenting code refactoring**
>
> Use this template for significant refactoring efforts that require planning, testing, and documentation.
> For simple refactoring, use the "Refactor code" prompt directly in CLAUDE.md.

## Overview

**Refactoring ID:** REFACTOR-[ID]
**Date:** [YYYY-MM-DD]
**Component:** [Component/Module/File to refactor]
**Estimated Effort:** [Hours/Days]
**Priority:** [High/Medium/Low]

## Refactoring Goals

### Primary Goal
[Main objective of this refactoring - e.g., improve performance, enhance readability]

### Secondary Goals
- [Additional goal 1]
- [Additional goal 2]
- [Additional goal 3]

### Success Metrics
- [ ] [Measurable metric 1 - e.g., reduce code complexity from 15 to 8]
- [ ] [Measurable metric 2 - e.g., improve performance by 30%]
- [ ] [Measurable metric 3 - e.g., reduce duplication by 50%]

## Current State Analysis

### Code Smells Identified
- **[Smell 1]**: [Description and location]
  - Severity: [Low/Medium/High]
  - Impact: [Performance/Maintainability/Readability]

- **[Smell 2]**: [Description and location]
  - Severity: [Low/Medium/High]
  - Impact: [Performance/Maintainability/Readability]

### Current Metrics
- **Lines of Code:** [X lines]
- **Cyclomatic Complexity:** [X]
- **Code Duplication:** [X%]
- **Test Coverage:** [X%]
- **Performance:** [Current metric - e.g., 200ms response time]

**Tools for measuring:**
- **Lines of Code:** `cloc`, `tokei`, or IDE statistics
- **Cyclomatic Complexity:** `radon` (Python), `phpmetrics` (PHP), ESLint complexity rules (JS)
- **Code Duplication:** `jscpd`, `phpcpd`, `pylint` (Python)
- **Test Coverage:** `coverage.py` (Python), `phpunit --coverage` (PHP), `jest --coverage` (JS)
- **Performance:** Laravel Debugbar, Django Debug Toolbar, APM tools, `pytest-benchmark`

### Current Issues
1. [Issue 1 - e.g., N+1 query problem]
2. [Issue 2 - e.g., Deeply nested conditionals]
3. [Issue 3 - e.g., Tight coupling between components]

### Code Example (Before)
```[language]
// Example of problematic code
// Show the current implementation
```

## Constraints & Requirements

### Must Preserve
- **External API:** [Describe external interfaces that cannot change]
- **Behavior:** [Specific behaviors that must remain identical]
- **Data Structure:** [Any data structures that must stay the same]
- **Performance:** [Minimum performance requirements]

### Allowed to Change
- Internal implementation details
- Internal APIs (if no external consumers)
- Code structure and organization
- [Other internal aspects]

### Dependencies
- [External systems or components that this depends on]
- [Other refactoring tasks that must complete first]

### Breaking Changes
**Allowed:** [Yes/No]

If yes, list breaking changes:
- [Breaking change 1]
- [Breaking change 2]

## Target State

### Desired Architecture
[Describe the target architecture or code structure]

### Target Metrics
- **Lines of Code:** [Target - e.g., reduce to Y lines]
- **Cyclomatic Complexity:** [Target - e.g., reduce to Y]
- **Code Duplication:** [Target - e.g., reduce to Y%]
- **Test Coverage:** [Target - e.g., increase to Y%]
- **Performance:** [Target - e.g., < 50ms response time]

### Code Example (After)
```[language]
// Example of refactored code
// Show the desired implementation
```

### Design Patterns to Apply
- [Pattern 1] - [Why and where]
- [Pattern 2] - [Why and where]

### Database Optimization Patterns (if applicable)
- [ ] **Eager Loading** - Eliminate N+1 queries by loading relationships upfront
  - Laravel: `Model::with(['relation1', 'relation2'])`
  - Django: `queryset.select_related()` (foreign keys) or `prefetch_related()` (many-to-many)
- [ ] **Query Caching** - Cache expensive queries to reduce database load
  - Laravel: `Cache::remember('key', $seconds, fn() => query())`
  - Django: Use `django-cacheops` or manual caching with `cache.get()`/`cache.set()`
- [ ] **Index Optimization** - Add database indexes for frequently queried columns
  - Identify slow queries, add indexes on WHERE/JOIN columns
  - Laravel: Schema migration with `$table->index(['column'])`
  - Django: Add `db_index=True` to model fields or `indexes = [models.Index(...)]` in Meta
- [ ] **Database Views** - Create views for complex frequently-run queries
  - Useful for reports, dashboards, or complex joins
- [ ] **Batch Operations** - Use bulk inserts/updates instead of individual saves
  - Laravel: `Model::insert($array)` or `Model::upsert()`
  - Django: `Model.objects.bulk_create()` or `bulk_update()`
- [ ] **Query Optimization** - Rewrite inefficient queries, use raw SQL when needed
  - Select only needed columns: `select('id', 'name')` instead of `select('*')`
  - Use database-specific optimizations (EXPLAIN, query plans)

## Testing Strategy

### Pre-Refactoring Tests
**CRITICAL: Ensure comprehensive tests exist BEFORE refactoring**

- [ ] Review existing test coverage
- [ ] Identify gaps in test coverage
- [ ] Write missing tests to achieve [X]% coverage
- [ ] Ensure all tests pass
- [ ] Create baseline performance metrics

### Test Types
- **Unit Tests:** [Coverage target]
- **Integration Tests:** [Coverage target]
- **End-to-End Tests:** [Coverage target]
- **Performance Tests:** [Metrics to track]

### Test-Driven Refactoring Approach
1. [ ] Ensure tests are green before starting
2. [ ] Make small, incremental changes
3. [ ] Run tests after each change
4. [ ] Verify tests remain green
5. [ ] If tests fail, revert and adjust approach

## Refactoring Steps

### Phase 1: Preparation
**Goal:** Set up safety net and understand code

**Tasks:**
- [ ] Run full test suite - ensure 100% passing
- [ ] Document current behavior
- [ ] Create performance baseline
- [ ] Set up code coverage monitoring
- [ ] Review code and identify all touch points

**Validation:** All tests green, baseline metrics recorded

---

### Phase 2: [First Refactoring Step]
**Goal:** [What this phase accomplishes]

**Approach:**
[Describe the refactoring technique - e.g., Extract Method, Replace Conditional with Polymorphism]

**Tasks:**
- [ ] [Specific task 1]
- [ ] [Specific task 2]
- [ ] Run tests after each change
- [ ] Commit working state

**Validation:**
- [ ] All tests still pass
- [ ] No performance regression
- [ ] Code coverage maintained or improved

---

### Phase 3: [Second Refactoring Step]
**Goal:** [What this phase accomplishes]

**Approach:**
[Describe the refactoring technique]

**Tasks:**
- [ ] [Specific task 1]
- [ ] [Specific task 2]
- [ ] Run tests after each change
- [ ] Commit working state

**Validation:**
- [ ] All tests still pass
- [ ] No performance regression
- [ ] Code coverage maintained or improved

---

### Phase 4: [Third Refactoring Step]
**Goal:** [What this phase accomplishes]

**Approach:**
[Describe the refactoring technique]

**Tasks:**
- [ ] [Specific task 1]
- [ ] [Specific task 2]
- [ ] Run tests after each change
- [ ] Commit working state

**Validation:**
- [ ] All tests still pass
- [ ] No performance regression
- [ ] Code coverage maintained or improved

---

### Phase 5: Finalization
**Goal:** Clean up and verify

**Tasks:**
- [ ] Remove dead code
- [ ] Update documentation
- [ ] Run full test suite
- [ ] Performance testing
- [ ] Code review
- [ ] Update architectural diagrams if needed

**Validation:**
- [ ] All tests pass
- [ ] Performance targets met
- [ ] Code review approved

## Risk Management

### Potential Risks
| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| Breaking external API | Low | High | Keep external interfaces unchanged |
| Performance regression | Medium | High | Performance tests after each step |
| Introducing bugs | Medium | High | Comprehensive test coverage before starting |
| Scope creep | High | Medium | Stick to defined goals, defer new features |

### Rollback Strategy
**If refactoring fails or introduces critical issues:**

```bash
# Rollback steps
git revert [commit-range]
# Or restore from specific commit
git reset --hard [safe-commit-hash]
```

**Rollback criteria:**
- Critical bug introduced
- Performance degradation > 20%
- Test coverage drops below acceptable threshold
- Breaking changes discovered

## Files Affected

### Primary Files
- `path/to/file1.ext` - [Scope of changes]
- `path/to/file2.ext` - [Scope of changes]

### Supporting Files
- `path/to/test1.ext` - [Test updates needed]
- `path/to/test2.ext` - [Test updates needed]
- `path/to/doc.md` - [Documentation updates]

### Total Estimated Changes
- Files modified: [X]
- Lines added: [~X]
- Lines removed: [~X]
- Net change: [+/- X lines]

## Performance Impact

### Current Performance
- [Metric 1]: [Current value]
- [Metric 2]: [Current value]
- [Metric 3]: [Current value]

### Target Performance
- [Metric 1]: [Target value] ([+/-X% change])
- [Metric 2]: [Target value] ([+/-X% change])
- [Metric 3]: [Target value] ([+/-X% change])

### Performance Testing Plan
- [ ] Benchmark before refactoring
- [ ] Benchmark after each phase
- [ ] Benchmark final result
- [ ] Compare with baseline

## Documentation Updates

### Code Documentation
- [ ] Update inline comments
- [ ] Update function/method docstrings
- [ ] Update README if architecture changes
- [ ] Update architectural diagrams

### Decision Log
- [ ] Add entry to `docs/.claude/context/decision-log.md` explaining:
  - Why refactoring was needed
  - Approach chosen
  - Alternatives considered
  - Trade-offs made

### Knowledge Transfer
- [ ] Document new patterns introduced
- [ ] Update team wiki/docs
- [ ] Share learnings with team

## Timeline

**Start Date:** [YYYY-MM-DD]
**Target Completion:** [YYYY-MM-DD]
**Actual Completion:** [YYYY-MM-DD]

### Phase Timeline
- [ ] Phase 1 (Preparation): [Date range]
- [ ] Phase 2: [Date range]
- [ ] Phase 3: [Date range]
- [ ] Phase 4: [Date range]
- [ ] Phase 5 (Finalization): [Date range]

## Progress Tracking

### Completed Phases
- [x] [Phase name] - Completed [Date]

### Current Phase
- [ ] [Phase name] - [% complete]

### Upcoming Phases
- [ ] [Phase name]
- [ ] [Phase name]

### Blockers
- [Blocker 1] - [Description and owner]

## Refactoring Techniques Used

- [ ] **Extract Method** - [Where applied]
- [ ] **Extract Class** - [Where applied]
- [ ] **Move Method** - [Where applied]
- [ ] **Rename** - [Where applied]
- [ ] **Introduce Parameter Object** - [Where applied]
- [ ] **Replace Conditional with Polymorphism** - [Where applied]
- [ ] **Decompose Conditional** - [Where applied]
- [ ] **Consolidate Duplicate Conditional Fragments** - [Where applied]
- [ ] **Remove Dead Code** - [Where applied]
- [ ] **Other:** [Describe]

## Review & Approval

### Code Review
- **Reviewer:** [Name]
- **Status:** [Pending/Approved/Changes Requested]
- **Review Date:** [YYYY-MM-DD]
- **Comments:** [Summary or link]

### Performance Review
- **Metrics Review:** [Pass/Fail]
- **Performance Improvement:** [Actual %]
- **Acceptable:** [Yes/No]

### Architectural Review
- **Architect:** [Name]
- **Status:** [Pending/Approved]
- **Concerns:** [Any architectural concerns]

## Post-Refactoring

### Actual Results

**Metrics Achieved:**
- Lines of Code: [Before] → [After] ([Change]%)
- Cyclomatic Complexity: [Before] → [After] ([Change]%)
- Code Duplication: [Before] → [After] ([Change]%)
- Test Coverage: [Before] → [After] ([Change]%)
- Performance: [Before] → [After] ([Change]%)

**Success Criteria Met:**
- [ ] [Criterion 1] - [Met/Not Met]
- [ ] [Criterion 2] - [Met/Not Met]
- [ ] [Criterion 3] - [Met/Not Met]

### Issues Discovered
- [Issue 1] - [How resolved]
- [Issue 2] - [How resolved]

### Lessons Learned

**What Worked Well:**
- [Point 1]
- [Point 2]

**What Could Be Improved:**
- [Point 1]
- [Point 2]

**Best Practices Identified:**
- [Practice 1]
- [Practice 2]

**Anti-Patterns Avoided:**
- [Anti-pattern 1]
- [Anti-pattern 2]

### Recommendations for Future

**For similar refactoring:**
- [Recommendation 1]
- [Recommendation 2]

**Technical debt identified:**
- [Debt item 1] - [Priority]
- [Debt item 2] - [Priority]

**Follow-up refactoring needed:**
- [ ] [Follow-up 1] - [Why and when]
- [ ] [Follow-up 2] - [Why and when]

## Related

- **Related Refactoring:** [REFACTOR-XXX]
- **Related Features:** [FEATURE-XXX]
- **Related Modifications:** [MOD-XXX]
- **Pull Request:** [Link]
- **Discussion:** [Link to RFC/discussion]

---

**Status:** [Draft/In Progress/In Review/Completed/Archived]
**Last Updated:** [YYYY-MM-DD]
**Maintained By:** [Name/Team]

---

## Refactoring Checklist

Use this checklist to ensure safe, effective refactoring:

- [ ] Tests exist and are comprehensive
- [ ] All tests pass before starting
- [ ] Baseline metrics recorded
- [ ] Incremental approach planned
- [ ] External behavior preserved
- [ ] Tests run after each change
- [ ] Performance monitored throughout
- [ ] Code review completed
- [ ] Documentation updated
- [ ] Decision log updated
- [ ] Team notified of changes
- [ ] Knowledge transferred

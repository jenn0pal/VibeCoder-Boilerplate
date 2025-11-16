# Code Modification: [Brief Description]

> **Template for documenting significant code modifications**
>
> Use this template for medium-to-large modifications that require planning and documentation.
> For small changes (< 1 hour), use the "Modify existing code" prompt directly in CLAUDE.md.

## Overview

**Modification ID:** MOD-[ID]
**Date:** [YYYY-MM-DD]
**Type:** [Styling/Feature Enhancement/Configuration/Optimization]
**Priority:** [High/Medium/Low]
**Estimated Effort:** [Hours/Days]

## Motivation

### Why This Change?
[Explain the business or technical reason for this modification]

### Problem Statement
[What issue are we addressing?]

### Expected Benefits
- [Benefit 1]
- [Benefit 2]
- [Benefit 3]

## Current State

### Existing Implementation
[Describe how the code currently works]

```[language]
// Example of current code
```

### Current Behavior
[What happens now?]

### Limitations/Issues
- [Issue 1]
- [Issue 2]

## Desired State

### Target Implementation
[Describe how the code should work after modification]

```[language]
// Example of desired code
```

### Target Behavior
[What should happen after the change?]

### Success Criteria
- [ ] [Measurable criterion 1]
- [ ] [Measurable criterion 2]
- [ ] [Measurable criterion 3]

## Scope of Changes

### Files to Modify
- `path/to/file1.ext` - [What changes]
- `path/to/file2.ext` - [What changes]
- `path/to/file3.ext` - [What changes]

### Components Affected
- [Component 1] - [Impact]
- [Component 2] - [Impact]

### Dependencies
- [External dependency or other modifications this depends on]

### Out of Scope
- [What this modification explicitly does NOT include]

## Implementation Plan

### Step 1: [First Step]
**Goal:** [What this step accomplishes]

**Tasks:**
- [ ] [Task 1]
- [ ] [Task 2]

**Validation:** [How to verify this step is complete]

### Step 2: [Second Step]
**Goal:** [What this step accomplishes]

**Tasks:**
- [ ] [Task 1]
- [ ] [Task 2]

**Validation:** [How to verify this step is complete]

### Step 3: [Third Step]
**Goal:** [What this step accomplishes]

**Tasks:**
- [ ] [Task 1]
- [ ] [Task 2]

**Validation:** [How to verify this step is complete]

## Testing Strategy

### Existing Tests to Update
- [ ] `path/to/test1.ext` - [What needs updating]
- [ ] `path/to/test2.ext` - [What needs updating]

### New Tests to Add
- [ ] Test case 1: [Description]
- [ ] Test case 2: [Description]

### Manual Testing Checklist
- [ ] [Manual test 1]
- [ ] [Manual test 2]
- [ ] [Manual test 3]

### Edge Cases to Test
- [Edge case 1]
- [Edge case 2]

## Risk Assessment

### Potential Risks
| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| [Risk 1] | Low/Medium/High | Low/Medium/High | [Mitigation strategy] |
| [Risk 2] | Low/Medium/High | Low/Medium/High | [Mitigation strategy] |

### Rollback Plan
[How to revert this change if something goes wrong]

```bash
# Rollback commands
git revert [commit-hash]
```

## Impact Analysis

### User Impact
- **User-facing changes:** [Yes/No]
- **Breaking changes:** [Yes/No]
- **Migration required:** [Yes/No]

### Performance Impact
- **Expected improvement:** [e.g., 20% faster]
- **Load time:** Before [X]ms → After [Y]ms
- **Database queries:** Before [X] → After [Y]

**Tools for measuring:**
- **Load time:** Browser DevTools Network tab, Laravel Debugbar, Django Debug Toolbar
- **Database queries:** Laravel Debugbar, Django Debug Toolbar, database query logs
- **Memory usage:** Laravel Debugbar, Django Debug Toolbar, memory profilers
- **API response time:** Postman, curl with `-w` flag, APM tools

### Accessibility Impact
- [Any accessibility considerations]

### Security Impact
- [Any security implications]

## Documentation Updates

### Code Documentation
- [ ] Update inline comments
- [ ] Update function/method docstrings
- [ ] Update type definitions

### External Documentation
- [ ] Update README.md
- [ ] Update API documentation
- [ ] Update user guide

### Decision Log
- [ ] Add entry to `docs/.claude/context/decision-log.md` if significant architectural impact

## Timeline

**Start Date:** [YYYY-MM-DD]
**Target Completion:** [YYYY-MM-DD]
**Actual Completion:** [YYYY-MM-DD]

### Milestones
- [ ] [Milestone 1] - [Date]
- [ ] [Milestone 2] - [Date]
- [ ] [Milestone 3] - [Date]

## Implementation Progress

### Completed
- [x] [Task that's done]

### In Progress
- [ ] [Task currently being worked on]

### Pending
- [ ] [Task not yet started]

### Blocked
- [ ] [Task blocked] - Blocker: [Description]

## Review & Approval

### Code Review
- **Reviewer:** [Name]
- **Status:** [Pending/Approved/Changes Requested]
- **Comments:** [Link to PR or review comments]

### Testing Sign-off
- **Tester:** [Name]
- **Status:** [Pending/Passed/Failed]
- **Test Results:** [Link or summary]

### Stakeholder Approval
- **Approver:** [Name/Role]
- **Status:** [Pending/Approved]
- **Date:** [YYYY-MM-DD]

## Post-Implementation

### Actual Results
[What actually happened after implementation]

### Metrics
- **Performance:** [Actual improvement]
- **User feedback:** [Summary]
- **Issues found:** [Number/severity]

### Lessons Learned
**What Went Well:**
- [Point 1]
- [Point 2]

**What Could Be Improved:**
- [Point 1]
- [Point 2]

**Action Items for Future:**
- [ ] [Improvement 1]
- [ ] [Improvement 2]

## Related

- **Related Modifications:** [MOD-XXX, MOD-YYY]
- **Related Features:** [FEATURE-XXX]
- **Related Bugs:** [BUG-XXX]
- **Pull Request:** [Link to PR]
- **Discussion:** [Link to discussion/issue]

---

**Status:** [Draft/In Progress/In Review/Completed/Archived]
**Last Updated:** [YYYY-MM-DD]
**Maintained By:** [Name/Team]

# Code Review Checklist

> **Comprehensive checklist for thorough code reviews**

## Pre-Review Setup

- [ ] Pull/checkout the branch
- [ ] Read the PR description and linked issues
- [ ] Understand the context and goals
- [ ] Run the code locally (if needed)
- [ ] Run tests to ensure they pass

## Code Quality

### Readability
- [ ] Code is self-explanatory
- [ ] Variable/function names are descriptive
- [ ] Complex logic has comments explaining "why"
- [ ] No commented-out code (use git instead)
- [ ] Consistent formatting/style

### Structure
- [ ] Functions/methods have single responsibility
- [ ] Classes are cohesive
- [ ] No code duplication (DRY principle)
- [ ] Appropriate abstraction levels
- [ ] Logical file organization

### Conventions
- [ ] Follows project coding conventions
- [ ] Naming conventions consistent
- [ ] File structure matches project patterns
- [ ] Imports organized properly
- [ ] Consistent error handling pattern

## Functionality

### Correctness
- [ ] Code does what it's supposed to do
- [ ] Edge cases handled
- [ ] Error cases handled gracefully
- [ ] No obvious bugs or logic errors
- [ ] Null/undefined checks where needed

### Requirements
- [ ] Meets all acceptance criteria
- [ ] User stories addressed
- [ ] Business logic correct
- [ ] No scope creep (out-of-scope changes)

## Testing

### Test Coverage
- [ ] Unit tests for new code
- [ ] Integration tests for workflows
- [ ] E2E tests for critical paths (if applicable)
- [ ] All tests pass
- [ ] No flaky tests introduced

### Test Quality
- [ ] Tests are meaningful (not just for coverage)
- [ ] Test names describe what they test
- [ ] Tests are independent
- [ ] Mocks/stubs used appropriately
- [ ] Edge cases tested

## Security

### Common Vulnerabilities
- [ ] No SQL injection vulnerabilities
- [ ] No XSS vulnerabilities
- [ ] No CSRF vulnerabilities
- [ ] Input validation in place
- [ ] Output encoding/sanitization
- [ ] Authentication/authorization checks

### Data Protection
- [ ] No hardcoded secrets/credentials
- [ ] Sensitive data encrypted
- [ ] No logging of sensitive data
- [ ] Secure randomness used (crypto-safe)
- [ ] Secure defaults

### Dependencies
- [ ] No new vulnerabilities introduced
- [ ] Dependencies up to date
- [ ] No unnecessary dependencies added

## Performance

### Efficiency
- [ ] No obvious performance issues
- [ ] Database queries optimized (N+1 avoided)
- [ ] Appropriate caching used
- [ ] No unnecessary computations in loops
- [ ] Async operations where appropriate

### Scalability
- [ ] Solution scales with data growth
- [ ] No memory leaks
- [ ] Reasonable resource usage
- [ ] Pagination for large datasets

## API/Interfaces

### API Design (if applicable)
- [ ] RESTful/GraphQL conventions followed
- [ ] Appropriate HTTP methods
- [ ] Proper status codes
- [ ] Consistent response format
- [ ] Versioned appropriately
- [ ] Backward compatible (if needed)

### Contracts
- [ ] Interfaces well-defined
- [ ] Types/schemas documented
- [ ] Breaking changes documented
- [ ] Migration path for breaking changes

## Database

### Schema Changes
- [ ] Migrations are reversible
- [ ] Indexes added for performance
- [ ] No breaking schema changes (or migration plan)
- [ ] Foreign keys and constraints appropriate
- [ ] Data migrations tested

### Queries
- [ ] Queries efficient (no N+1)
- [ ] Proper use of transactions
- [ ] Connection pooling considered
- [ ] Query timeouts appropriate

## Frontend (if applicable)

### UI/UX
- [ ] UI matches design specs/mockups
- [ ] Responsive design works
- [ ] Accessibility (keyboard nav, screen readers)
- [ ] Loading states handled
- [ ] Error states handled
- [ ] Empty states handled

### Browser Compatibility
- [ ] Works in target browsers
- [ ] Mobile-friendly (if applicable)
- [ ] No console errors/warnings

## Documentation

### Code Documentation
- [ ] Complex logic documented
- [ ] Public APIs documented (JSDoc/docstrings)
- [ ] Unusual decisions explained
- [ ] TODOs have tickets/issues

### Project Documentation
- [ ] README updated (if needed)
- [ ] API docs updated (if API changes)
- [ ] Migration guide (if breaking changes)
- [ ] CHANGELOG updated

## Git/Version Control

### Commits
- [ ] Commit messages are clear
- [ ] Commits are logical units
- [ ] No merge commits (rebased)
- [ ] No unnecessary commits

### Branch
- [ ] Branch name follows convention
- [ ] Up to date with base branch
- [ ] No conflicts
- [ ] Clean git history

## Deployment

### Configuration
- [ ] Environment variables documented
- [ ] Config changes backward compatible
- [ ] Secrets not in code

### Deployment Safety
- [ ] Feature flags used (if risky)
- [ ] Rollback plan exists
- [ ] Database migrations safe
- [ ] No downtime expected (or communicated)

## Review Outcome

### Summary
```
#### What's Good
- [Positive feedback 1]
- [Positive feedback 2]

#### Issues Found
- [ ] **Critical:** [Issue requiring immediate fix]
- [ ] **Major:** [Important but not blocking]
- [ ] **Minor:** [Nice to have improvements]

#### Suggestions
- [Suggestion 1]
- [Suggestion 2]

#### Decision
- [ ] ✅ Approve
- [ ] ⚠️ Approve with minor changes
- [ ] ❌ Request changes
```

## Quick Reference

### Severity Levels

**Critical (Must Fix):**
- Security vulnerabilities
- Data loss risks
- Breaking changes without migration
- Performance issues in production code
- Failing tests

**Major (Should Fix):**
- Missing tests for new code
- Unclear/confusing code
- Violations of conventions
- Missing error handling
- Documentation gaps

**Minor (Nice to Have):**
- Code style improvements
- Naming improvements
- Refactoring opportunities
- Additional tests
- Enhanced documentation

### Review Time Estimates

- **Small PR (< 50 lines):** 5-10 minutes
- **Medium PR (50-200 lines):** 15-30 minutes
- **Large PR (200-500 lines):** 30-60 minutes
- **Very Large PR (> 500 lines):** Request split into smaller PRs

### Tips for Reviewers

1. **Be constructive:** Focus on improvement, not criticism
2. **Ask questions:** "Why did you choose this approach?"
3. **Suggest alternatives:** "Have you considered...?"
4. **Acknowledge good work:** Point out what's well done
5. **Test the code:** Don't just read it
6. **Check the diff:** Look at what actually changed
7. **Review in passes:** First pass for big picture, second for details

---

*Use this checklist as a guide, not a rigid requirement. Adapt based on PR size and complexity.*

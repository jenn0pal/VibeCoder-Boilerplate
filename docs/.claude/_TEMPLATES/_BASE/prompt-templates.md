# Prompt Templates Library

> **Reusable, battle-tested prompts for common development workflows**

## How to Use This Library

1. Find the prompt template that matches your task
2. Copy the template
3. Fill in the placeholders `[like this]`
4. Paste into your Claude session

**Tip:** Bookmark commonly used prompts for quick access.

---

## Session Management

### Starting a New Session

```
Load CLAUDE.md
Load docs/.claude/context/project-overview.md

Working on: [specific task or feature]
Goal: [what you want to accomplish this session]
```

### Resuming Previous Work

```
Load CLAUDE.md
Load docs/.claude/context/project-overview.md

Continuing: [feature or task name]
Last session completed: [what was finished]
Current state: [where you left off]
Today's goal: [what to accomplish]
Blockers: [any issues encountered]
```

---

## Feature Development

### Simple Feature Implementation

```
Load CLAUDE.md
Load docs/.claude/context/project-overview.md
Load docs/.claude/context/conventions.md

Implement feature: [feature name]

Requirements:
- [Requirement 1]
- [Requirement 2]
- [Requirement 3]

Acceptance criteria:
- [ ] [Criterion 1]
- [ ] [Criterion 2]
- [ ] [Criterion 3]

Please implement following our conventions with full test coverage.
```

### Complex Multi-Phase Feature

```
Load CLAUDE.md
Load docs/.claude/context/project-overview.md

Feature: [Feature name]
Complexity: Complex - requires multiple phases

Description: [Brief description]

Please help me:
1. Break down this feature into logical phases
2. Identify which specialized agents should handle each phase
3. Create a feature implementation workflow
4. Generate phase task files

Use templates:
- docs/.claude/_TEMPLATES/_BASE/feature-implementation-workflow.md
- docs/.claude/_TEMPLATES/_BASE/phase-task.md
```

---

## Bug Fixing

### Standard Bug Fix

```
Load CLAUDE.md
Load docs/.claude/context/conventions.md

Bug: [Brief description]
Severity: [Critical/High/Medium/Low]
Environment: [Dev/Staging/Production]

Steps to reproduce:
1. [Step 1]
2. [Step 2]
3. [Step 3]

Expected behavior: [What should happen]
Actual behavior: [What actually happens]

Error message:
```
[Paste error or logs]
```

Please help me:
1. Write a failing test that reproduces the bug
2. Identify the root cause
3. Implement a fix following our conventions
4. Verify the test passes
5. Add regression test
```

### Production Hotfix

```
Load CLAUDE.md
Load docs/.claude/context/conventions.md

URGENT: Production hotfix needed

Issue: [Critical issue description]
Impact: [Who/what is affected]
When discovered: [Time/date]

Current error rate: [X%]
Affected users: [Number or percentage]

Steps to reproduce:
1. [Step 1]
2. [Step 2]

Please help me:
1. Create hotfix branch from main
2. Implement minimal fix (no refactoring)
3. Add test to verify fix
4. Prepare for immediate deployment
5. Document root cause for post-mortem
```

---

## Code Modification

### Simple Modification

```
Load CLAUDE.md
Load docs/.claude/context/conventions.md

Modification: [Brief description]
Type: [Styling/Enhancement/Config/Optimization]

Current state: [What exists now]
Desired state: [What it should become]
Files affected: [List files or "unknown"]

Please implement following our conventions.
```

### UI/Styling Change

```
Load CLAUDE.md
Load docs/.claude/context/conventions.md

UI Change: [What needs to change]
Location: [Component/page/section]

Current:
- [Current color/layout/behavior]

Desired:
- [New color/layout/behavior]

Please update while maintaining:
- Responsive design
- Accessibility (WCAG 2.1 AA)
- Existing functionality
```

---

## Testing

### Add Missing Tests

```
Load CLAUDE.md
Load docs/.claude/context/conventions.md

File to test: [path/to/file]
Current coverage: [X%]
Target coverage: [Y%]

Please add:
- [ ] Unit tests for all public methods
- [ ] Edge case tests
- [ ] Error handling tests
- [ ] Integration tests (if applicable)

Follow our testing conventions and use our standard test patterns.
```

### Fix Failing Tests

```
Load CLAUDE.md

Test failures: [X] tests failing

Failed tests:
```
[Paste test output]
```

Please:
1. Analyze why tests are failing
2. Determine if tests or code need fixing
3. Fix the issues
4. Verify all tests pass
5. Ensure no regressions
```

---

## Refactoring

### Code Refactoring

```
Load CLAUDE.md
Load docs/.claude/context/conventions.md

Refactor: [File/component/module name]
Goal: [Improve performance/readability/maintainability/testability]

Current issues:
- [Issue 1]
- [Issue 2]

Constraints:
- [ ] Must maintain same external API
- [ ] Must not break existing tests
- [ ] Must not change behavior

Please:
1. Verify tests exist (write if missing)
2. Refactor incrementally
3. Run tests after each change
4. Document significant changes in decision log
```

### Extract Component/Function

```
Load CLAUDE.md
Load docs/.claude/context/conventions.md

Extract: [What to extract]
From: [Current location]
Reason: [Why - reusability/clarity/testing]

Current code:
```[language]
[Paste code to extract]
```

Please:
1. Extract into new [component/function/class]
2. Update all usages
3. Add tests for extracted code
4. Verify all existing tests still pass
```

---

## Technical Debt

### Identify Tech Debt

```
Load CLAUDE.md
Load docs/.claude/context/conventions.md

Please analyze [component/module/area] for technical debt.

Look for:
- Code smells
- Outdated patterns
- Performance issues
- Security concerns
- Maintainability issues

For each issue found, create DEBT-[ID].md file with:
- Description
- Impact
- Estimated effort to fix
- Recommended approach
```

### Address Tech Debt

```
Load CLAUDE.md
Load docs/.claude/context/conventions.md
Load docs/.claude/tech-debt/DEBT-[ID].md

Please help me resolve this technical debt following the recommended approach.

Constraints:
- [Any business constraints]
- [Timeline requirements]
- [Resource limitations]
```

---

## Dependencies & Upgrades

### Upgrade Framework

```
Load CLAUDE.md
Load docs/.claude/context/tech-stack.md

Framework Upgrade: [Framework name]
From: [Current version]
To: [Target version]
Type: [Major/Minor/Patch]

Reason: [Why upgrade now]

Please help me:
1. Check breaking changes in release notes
2. Audit package compatibility
3. Create upgrade plan (UPGRADE-[ID].md)
4. Execute upgrade incrementally
5. Run all tests and fix failures
6. Update documentation
```

### Upgrade Dependency

```
Load CLAUDE.md
Load docs/.claude/context/tech-stack.md

Dependency: [package-name]
From: [X.Y.Z]
To: [A.B.C]

Reason: [Security/Feature/Bugfix]
CVE (if applicable): [CVE-YYYY-XXXXX]

Please help me:
1. Check breaking changes
2. Test upgrade in isolation
3. Update code if needed
4. Verify tests pass
5. Update docs
```

---

## Code Review

### Request Code Review

```
Load CLAUDE.md
Load docs/.claude/context/conventions.md

Please review: [PR link or file list]

Focus areas:
- [ ] Code follows conventions
- [ ] Tests are comprehensive
- [ ] Security best practices
- [ ] Performance considerations
- [ ] Documentation completeness

Provide:
1. Issues found (with severity)
2. Suggestions for improvement
3. Approval status (Approve/Request Changes)
```

### Pre-Commit Review

```
Load CLAUDE.md
Load docs/.claude/context/conventions.md

Before I commit, please review:
- [List of changed files]

Quick checklist:
- [ ] Follows conventions
- [ ] Has tests
- [ ] No console.log / debug code
- [ ] No secrets in code
- [ ] Breaking changes documented
```

---

## Documentation

### Generate API Documentation

```
Load CLAUDE.md

Please generate API documentation for: [API/endpoint/module]

Include:
- Endpoint URL and method
- Request parameters
- Request body schema
- Response schema
- Error responses
- Example requests
- Authentication requirements
```

### Update README

```
Load CLAUDE.md

Please update README.md to reflect:
- [Recent change 1]
- [Recent change 2]

Ensure README includes:
- Project description
- Installation instructions
- Usage examples
- Configuration
- Contributing guidelines
```

---

## Database

### Design Database Schema

```
Load CLAUDE.md
Load docs/.claude/context/tech-stack.md

Design database schema for: [Feature name]

Entities:
- [Entity 1]: [Description]
- [Entity 2]: [Description]

Relationships:
- [Entity 1] has many [Entity 2]
- [Entity 2] belongs to [Entity 1]

Please provide:
1. ERD (entity relationship diagram)
2. Table schemas with columns
3. Indexes for performance
4. Migration files
```

### Optimize Database Query

```
Load CLAUDE.md

Slow query:
```sql
[Paste slow query]
```

Execution time: [X]ms
Expected: < [Y]ms

Please:
1. Analyze query execution plan
2. Identify bottlenecks
3. Suggest optimizations (indexes, refactoring)
4. Implement improvements
5. Verify performance gain
```

---

## Security

### Security Audit

```
Load CLAUDE.md
Load docs/.claude/context/conventions.md

Please perform security audit of: [Component/feature/endpoint]

Check for:
- SQL injection
- XSS vulnerabilities
- CSRF protection
- Authentication/authorization issues
- Sensitive data exposure
- Input validation
- OWASP Top 10 vulnerabilities

Provide:
1. Vulnerabilities found (with severity)
2. Proof of concept (if applicable)
3. Remediation steps
```

### Implement Security Fix

```
Load CLAUDE.md
Load docs/.claude/context/conventions.md

Security Issue: [CVE or description]
Severity: [Critical/High/Medium/Low]

Vulnerability:
[Description of vulnerability]

Please:
1. Implement fix following security best practices
2. Add security tests
3. Verify fix works
4. Document in security.md (if needed)
5. Prepare deployment plan
```

---

## Performance

### Performance Optimization

```
Load CLAUDE.md

Performance issue in: [Component/page/endpoint]

Current metrics:
- Load time: [X]ms
- Bundle size: [Y]KB
- [Other metrics]

Target metrics:
- Load time: < [A]ms
- Bundle size: < [B]KB

Please:
1. Profile and identify bottlenecks
2. Suggest optimizations
3. Implement improvements
4. Measure and verify gains
```

### Bundle Size Optimization

```
Load CLAUDE.md
Load docs/.claude/context/tech-stack.md

Bundle too large: [X]KB (target: < [Y]KB)

Please:
1. Analyze bundle composition
2. Identify large dependencies
3. Suggest tree-shaking opportunities
4. Implement code splitting
5. Measure size reduction
```

---

## Deployment

### Prepare for Deployment

```
Load CLAUDE.md

Deploying: [Feature/fix name]
Environment: [Staging/Production]

Pre-deployment checklist:
- [ ] All tests passing
- [ ] No linting errors
- [ ] Documentation updated
- [ ] Database migrations ready
- [ ] Environment variables configured
- [ ] Rollback plan ready

Please verify and create deployment plan.
```

### Rollback Plan

```
Load CLAUDE.md

Create rollback plan for: [Deployment]

Include:
1. Steps to revert code
2. Database rollback procedure (if migrations)
3. Configuration rollback
4. Verification steps
5. Communication plan
6. RTO (Recovery Time Objective): [X] minutes
```

---

## Team Collaboration

### Onboard New Team Member

```
Load CLAUDE.md
Load docs/.claude/context/project-overview.md

Please create onboarding guide for new [Role] joining the team.

Include:
1. Project overview
2. Development environment setup
3. Key architectural decisions
4. Coding conventions
5. Common workflows
6. First tasks to get familiar with codebase
```

### Knowledge Transfer

```
Load CLAUDE.md

Please create knowledge transfer document for: [Component/feature/system]

Include:
- Purpose and business value
- Architecture overview
- Key files and their roles
- Configuration
- Common tasks
- Troubleshooting guide
- Known issues
```

---

## Emergency Scenarios

### Debug Production Issue

```
Load CLAUDE.md

PRODUCTION ISSUE

Symptoms: [What users are seeing]
Started: [When]
Affected: [Who/what]
Error rate: [X%]

Logs:
```
[Paste relevant logs]
```

Please help me:
1. Identify root cause quickly
2. Suggest immediate mitigation
3. Provide permanent fix
4. Create post-mortem template
```

### Incident Response

```
Load CLAUDE.md

INCIDENT: [Brief description]
Severity: [P1/P2/P3/P4]
Start time: [Time]

Current status:
- [Status update]

Actions taken so far:
- [Action 1]
- [Action 2]

Please help me:
1. Coordinate response
2. Document timeline
3. Implement fixes
4. Prepare stakeholder communication
5. Create incident report
```

---

## Tips for Effective Prompts

### Do's ✅
- Be specific about what you want
- Provide context (load relevant files)
- State constraints and requirements
- Include examples when helpful
- Break complex tasks into steps
- Specify output format

### Don'ts ❌
- Don't be vague ("make it better")
- Don't load unnecessary context
- Don't skip error messages/logs
- Don't ask multiple unrelated things
- Don't forget to specify conventions
- Don't assume Claude knows your codebase structure

---

## Custom Prompt Templates

Create project-specific templates in:
```
docs/.claude/prompts/[template-name].md
```

Share with your team for consistency!

---

*Last Updated: 2025*
*Version: 2.0*

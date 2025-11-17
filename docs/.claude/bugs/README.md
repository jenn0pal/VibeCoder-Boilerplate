# Bug Tracking

This directory contains detailed bug reports for issues requiring investigation and resolution.

## Usage

### When to Create a Bug File

Create a bug file here when:
- The bug requires detailed investigation
- Multiple people need to collaborate on the fix
- The bug reveals an architectural issue
- You need to track reproduction steps and resolution

For simple bugs, you can use the "Fix a bug" prompt in CLAUDE.md directly without creating a file.

### File Naming Convention

```
BUG-[ID]-brief-description.md
```

**Examples:**
- `BUG-001-user-login-timeout.md`
- `BUG-002-api-rate-limit-bypass.md`
- `BUG-003-memory-leak-dashboard.md`

### Bug File Template

Copy from `docs/.claude/_TEMPLATES/_BASE/task-management.md` (lines 109-152) or use this quick template:

```markdown
# BUG-[ID]: [Bug Title]

## Summary
[One-line bug description]

## Environment
- Environment: [Dev/Staging/Production]
- Browser/Client: [Details if applicable]
- Version: [App version]
- Discovered by: [Name/User report]
- Date reported: [YYYY-MM-DD]

## Severity & Priority
- **Severity**: [Critical/High/Medium/Low]
  - Critical: System down, data loss, security breach
  - High: Major feature broken, affects many users
  - Medium: Feature partially broken, workaround exists
  - Low: Minor inconvenience, cosmetic issue

- **Priority**: [P1/P2/P3/P4]
  - P1: Fix immediately (hotfix)
  - P2: Fix in current sprint
  - P3: Fix in next sprint
  - P4: Backlog

## Steps to Reproduce
1. [Step 1]
2. [Step 2]
3. [Step 3]

## Expected Behavior
[What should happen]

## Actual Behavior
[What actually happens]

## Error Details
```
[Error message, stack trace, or screenshots]
```

## Root Cause Analysis
[To be filled during investigation]
- **Component**: [Which part of the system]
- **Issue**: [What's wrong]
- **Why it happened**: [Explanation]

## Resolution
- **Fix applied**: [Description of the fix]
- **Files changed**: [List of modified files]
- **Tests added**: [Regression tests]
- **Branch**: `bugfix/BUG-[ID]-brief-description`
- **PR**: [Link to pull request]
- **Verified by**: [Name]
- **Deployed**: [Date/Version]

## Prevention
- [ ] Added regression test
- [ ] Updated documentation
- [ ] Added to decision log (if architectural)
- [ ] Similar issues checked and fixed

## Related Issues
- Related to BUG-XXX
- Caused by FEATURE-YYY
```

## Bug Fixing Workflow

### 1. Create Bug Report
```bash
# Create bug file
cp docs/.claude/_TEMPLATES/_BASE/task-management.md docs/.claude/bugs/BUG-001-description.md
# Edit to fill in details
```

### 2. Prioritize
- Critical/P1: Fix immediately
- High/P2: Current sprint
- Medium/P3: Next sprint
- Low/P4: Backlog

### 3. Fix the Bug
Start a Claude session:
```
Load CLAUDE.md and docs/.claude/context/conventions.md
Load docs/.claude/bugs/BUG-001-description.md

Please help me fix this bug following the workflow:
1. Write a failing test that reproduces the bug
2. Identify the root cause
3. Implement a fix
4. Verify the test passes
5. Add regression test
```

### 4. Document Resolution
Update the bug file with:
- Root cause analysis
- Fix applied
- Files changed
- Tests added
- PR link

### 5. Close Bug
After verification:
```bash
# Move to archive
mv docs/.claude/bugs/BUG-001-description.md docs/.claude/archive/bugs/
```

Or close the corresponding GitHub issue if tracking there.

## Bug Tracking Options

You can track bugs in multiple ways:

### Option 1: Local Files (This Directory)
**Best for:**
- Complex bugs requiring detailed investigation
- Architectural issues
- Bugs requiring team collaboration

### Option 2: GitHub Issues
**Best for:**
- Simple, straightforward bugs
- Integration with PR workflow
- Public projects
- Issue tracking and project boards

### Option 3: Hybrid Approach
- Use GitHub Issues for tracking and visibility
- Create local files for complex bugs requiring detailed notes
- Link the local file in the GitHub issue description

## Tips

1. **Write detailed reproduction steps** - Should be reproducible by anyone
2. **Include environment details** - Version, browser, OS, etc.
3. **Add screenshots/videos** - Visual evidence helps
4. **Document the "why"** - Not just the fix, but why it happened
5. **Write regression tests** - Prevent the bug from returning
6. **Update decision log** - If the bug reveals an architectural issue

## Example Bug Files

See `docs/.claude/_TEMPLATES/_BASE/task-management.md` for the full bug report template.

---

**Remember**: The goal is not just to fix the bug, but to understand why it happened and prevent similar issues in the future.

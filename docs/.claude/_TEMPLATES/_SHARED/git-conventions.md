# Git Conventions

> **Shared across all project types**
>
> Include this file in your conventions.md or reference when setting up git workflow.

## Branch Naming

- `feature/[ticket-id]-brief-description` - New features
- `bugfix/[ticket-id]-brief-description` - Bug fixes
- `hotfix/brief-description` - Critical production fixes
- `chore/brief-description` - Maintenance tasks
- `refactor/brief-description` - Code refactoring
- `docs/brief-description` - Documentation updates

**Examples:**
```bash
feature/USER-123-add-oauth-login
bugfix/USER-456-fix-password-reset
hotfix/critical-security-patch
chore/update-dependencies
```

## Commit Messages

Follow [Conventional Commits](https://www.conventionalcommits.org/):

```
<type>(<scope>): <subject>

<body>

<footer>
```

### Types

- `feat:` New feature
- `fix:` Bug fix
- `docs:` Documentation changes
- `style:` Code style changes (formatting, semicolons, etc)
- `refactor:` Code refactoring
- `perf:` Performance improvements
- `test:` Test additions or fixes
- `chore:` Maintenance tasks
- `ci:` CI/CD changes
- `build:` Build system or dependency changes
- `revert:` Revert previous commit

### Examples

```bash
feat(auth): add OAuth2 login support

Implemented Google and GitHub OAuth providers with proper
token refresh mechanism.

Closes #123

---

fix(api): resolve race condition in user creation

Added transaction locks to prevent duplicate user records
when concurrent requests are made.

Fixes #456

---

perf(database): optimize user query performance

- Added database indexes on frequently queried fields
- Implemented query result caching
- Reduced N+1 queries with select_related

Performance improved by 60% on user list endpoint.

---

docs(readme): update installation instructions

Added troubleshooting section for common setup issues.

---

chore(deps): upgrade Django from 4.2 to 5.0

BREAKING CHANGE: Removed support for Python 3.9
- Minimum Python version is now 3.10
- Updated all dependencies to compatible versions
- Migrated deprecated APIs

Refs #789
```

## Pull Request Template

Create `.github/pull_request_template.md`:

```markdown
## Description

Brief description of changes and motivation.

## Type of Change

- [ ] Bug fix (non-breaking change fixing an issue)
- [ ] New feature (non-breaking change adding functionality)
- [ ] Breaking change (fix or feature causing existing functionality to change)
- [ ] Documentation update
- [ ] Performance improvement
- [ ] Code refactoring
- [ ] Dependency update

## Related Issues

Closes #[issue number]
Relates to #[issue number]

## Changes Made

- Change 1
- Change 2
- Change 3

## Testing

### Manual Testing
- [ ] Tested locally
- [ ] Tested in development environment
- [ ] Tested in staging environment

### Automated Testing
- [ ] Unit tests pass
- [ ] Integration tests pass
- [ ] E2E tests pass (if applicable)
- [ ] No test coverage regression

### Test Coverage
- Current coverage: [X]%
- Coverage change: [+/-X]%

## Screenshots (if applicable)

### Before
[Screenshot]

### After
[Screenshot]

## Performance Impact

- [ ] No performance impact
- [ ] Performance improved
- [ ] Performance regression (explain below)

**Details:**
[Benchmark results if applicable]

## Security Considerations

- [ ] No security impact
- [ ] Security improvement
- [ ] Security review required

**Details:**
[Any security-relevant changes]

## Breaking Changes

- [ ] No breaking changes
- [ ] Breaking changes (describe below)

**Breaking changes:**
- [Description of breaking change 1]
- [Migration path or workaround]

## Database Changes

- [ ] No database changes
- [ ] Database migration included
- [ ] Data migration required

**Migration commands:**
```bash
# Commands to run after deployment
```

## Deployment Notes

- [ ] No special deployment steps
- [ ] Special deployment steps required (describe below)

**Deployment steps:**
1. [Step 1]
2. [Step 2]

## Checklist

### Code Quality
- [ ] Code follows project conventions
- [ ] Self-review completed
- [ ] No commented-out code
- [ ] No debug statements (console.log, print, dd, etc.)
- [ ] Error handling implemented
- [ ] Input validation added

### Testing
- [ ] Unit tests added/updated
- [ ] Integration tests added/updated
- [ ] All tests passing locally
- [ ] Test coverage meets requirements

### Documentation
- [ ] Code comments added where necessary
- [ ] API documentation updated (if applicable)
- [ ] README updated (if applicable)
- [ ] CHANGELOG updated
- [ ] Migration guide created (for breaking changes)

### Security
- [ ] No sensitive data in code
- [ ] Input sanitization implemented
- [ ] Authentication/authorization checked
- [ ] Dependencies scanned for vulnerabilities

### Accessibility (for UI changes)
- [ ] Keyboard navigation works
- [ ] Screen reader compatible
- [ ] Color contrast meets WCAG standards
- [ ] Focus indicators visible

## Reviewer Notes

Any specific areas you'd like reviewers to focus on:

[Notes for reviewers]

## Post-Merge Tasks

- [ ] Update documentation site
- [ ] Notify stakeholders
- [ ] Monitor error tracking
- [ ] Other: [specify]
```

## Git Workflow

### Feature Development

```bash
# 1. Start from main
git checkout main
git pull origin main

# 2. Create feature branch
git checkout -b feature/TICKET-123-feature-name

# 3. Make changes and commit
git add .
git commit -m "feat(scope): description"

# 4. Push to remote
git push -u origin feature/TICKET-123-feature-name

# 5. Create pull request
# Use GitHub/GitLab UI or CLI (gh/glab)

# 6. After approval, merge via UI (squash or merge commit)
# Delete branch after merge
```

### Hotfix Workflow

```bash
# 1. Branch from main
git checkout main
git pull origin main
git checkout -b hotfix/critical-issue

# 2. Fix and commit
git add .
git commit -m "fix: critical issue description"

# 3. Fast-track PR and merge
git push -u origin hotfix/critical-issue

# 4. Deploy immediately after merge
```

### Keeping Branch Updated

```bash
# Option 1: Rebase (cleaner history)
git fetch origin
git rebase origin/main

# Resolve conflicts if any
git add .
git rebase --continue

# Force push (only on your branch!)
git push --force-with-lease

# Option 2: Merge (preserves history)
git fetch origin
git merge origin/main

# Resolve conflicts if any
git add .
git commit -m "merge: resolve conflicts with main"

git push
```

## Merge Strategies

### Squash Merge (Recommended for most features)

**When to use:**
- Feature branches with many small commits
- Work-in-progress commits you want to clean up
- Keeping main branch history clean

**Pros:**
- Clean, linear history on main
- Easy to revert entire feature
- Simplified changelog

**Cons:**
- Loses detailed commit history
- Makes it harder to trace specific changes

### Merge Commit

**When to use:**
- Multiple developers on same branch
- Important to preserve commit history
- Long-running feature branches

**Pros:**
- Preserves complete history
- Shows when branches were merged
- Traceable development timeline

**Cons:**
- More complex history
- Can make git log harder to read

### Rebase and Merge

**When to use:**
- Want linear history but preserve commits
- Feature has well-crafted, logical commits
- Team experienced with git

**Pros:**
- Linear history
- Preserves individual commits
- Clean git log

**Cons:**
- Rewrites history (potential conflicts)
- Requires force push
- Can be confusing for beginners

## Protected Branches

Configure branch protection on `main` (or `master`):

- [ ] Require pull request before merging
- [ ] Require approvals: [1-2 reviewers]
- [ ] Require status checks to pass
- [ ] Require branches to be up to date
- [ ] Require conversation resolution
- [ ] Require signed commits (optional)
- [ ] Include administrators in restrictions

## Commit Signing (Optional but Recommended)

```bash
# Configure GPG signing
git config --global user.signingkey [YOUR_GPG_KEY_ID]
git config --global commit.gpgsign true
git config --global tag.gpgsign true

# Or use SSH signing (Git 2.34+)
git config --global gpg.format ssh
git config --global user.signingkey ~/.ssh/id_ed25519.pub
git config --global commit.gpgsign true
```

## Git Hooks

### Pre-commit Hook

Automate code quality checks:

```bash
# .git/hooks/pre-commit (or use husky/pre-commit framework)

#!/bin/bash

# Run linter
echo "Running linter..."
npm run lint
# or: ruff check .
# or: ./vendor/bin/pint

# Run tests
echo "Running tests..."
npm test
# or: pytest
# or: ./vendor/bin/pest

# Check for debug statements
if git diff --cached | grep -E "console.log|debugger|dd\(|var_dump"; then
    echo "Error: Found debug statements. Please remove before committing."
    exit 1
fi

# Success
exit 0
```

### Commit-msg Hook

Enforce conventional commit format:

```bash
# .git/hooks/commit-msg

#!/bin/bash

commit_msg=$(cat "$1")

# Check format: type(scope): message
if ! echo "$commit_msg" | grep -qE '^(feat|fix|docs|style|refactor|perf|test|chore|ci|build|revert)(\(.+\))?: .{1,}$'; then
    echo "Error: Commit message must follow Conventional Commits format"
    echo "Example: feat(auth): add OAuth login"
    exit 1
fi

exit 0
```

## Best Practices

### DO:
- ✅ Write clear, descriptive commit messages
- ✅ Make small, focused commits
- ✅ Commit early and often
- ✅ Reference issue numbers in commits
- ✅ Review your own PR before requesting review
- ✅ Keep branches short-lived (< 2 weeks)
- ✅ Delete branches after merge
- ✅ Pull latest main before creating new branch

### DON'T:
- ❌ Commit directly to main
- ❌ Use vague messages like "fix bug" or "update"
- ❌ Commit unrelated changes together
- ❌ Force push to shared branches
- ❌ Commit secrets or sensitive data
- ❌ Leave merge conflicts unresolved
- ❌ Push broken code
- ❌ Commit generated/build files (unless necessary)

## .gitignore Best Practices

```gitignore
# IDE
.idea/
.vscode/
*.swp
*.swo
*~

# OS
.DS_Store
Thumbs.db

# Environment
.env
.env.local
.env.*.local

# Dependencies
node_modules/
vendor/
__pycache__/
*.pyc
.pytest_cache/

# Build outputs
dist/
build/
*.egg-info/
.nuxt/
.output/

# Logs
*.log
logs/
npm-debug.log*

# Testing
coverage/
.coverage
htmlcov/

# Temporary
tmp/
temp/
*.tmp
```

---

**Last Updated:** 2025-01-16
**Version:** 1.0

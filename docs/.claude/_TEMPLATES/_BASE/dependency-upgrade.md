# Dependency Upgrade: [Package Name]

> **Template for upgrading third-party packages and libraries**
>
> Use this template for updating individual dependencies (npm packages, pip packages, composer packages, etc.)
> For framework upgrades (Django, Laravel, Vue, etc.), use framework-upgrade.md instead.

## Overview

**Upgrade ID:** DEP-[ID]
**Date:** [YYYY-MM-DD]
**Package Name:** [package-name]
**Package Manager:** [npm/pip/composer/yarn/pnpm]
**Current Version:** [X.Y.Z]
**Target Version:** [A.B.C]
**Upgrade Type:** [Major/Minor/Patch]
**Priority:** [Critical/High/Medium/Low]

### Version Change Classification
- **Patch (X.Y.Z → X.Y.W):** Bug fixes, security patches
- **Minor (X.Y.Z → X.W.0):** New features, backward compatible
- **Major (X.Y.Z → W.0.0):** Breaking changes

**This upgrade is:** [Patch/Minor/Major]

## Motivation

### Why Upgrade?
- [ ] Security vulnerability (CVE-[ID])
- [ ] Bug fix needed
- [ ] New feature required
- [ ] Dependency of another upgrade
- [ ] Maintenance (keeping dependencies current)
- [ ] Performance improvement
- [ ] Deprecation warning
- [ ] License compliance
- [ ] Other: [Specify]

### Security Information
**CVE ID:** [CVE-YYYY-XXXXX] (if applicable)
**Severity:** [Critical/High/Medium/Low]
**CVSS Score:** [X.X]
**Affected Versions:** [X.Y.Z - A.B.C]
**Patched in Version:** [A.B.C]

**Security Advisory URL:** [Link]

### Business Impact
**If we upgrade:**
- [Benefit 1]
- [Benefit 2]

**If we don't upgrade:**
- [Risk 1]
- [Risk 2]

## Package Information

### Package Details
**Official Repository:** [GitHub/GitLab/etc. URL]
**Documentation:** [Link to docs]
**Release Notes:** [Link to release notes]
**Changelog:** [Link to changelog]
**License:** [MIT/Apache/GPL/etc.]

### Popularity & Maintenance
**Weekly Downloads:** [X]
**GitHub Stars:** [X]
**Last Updated:** [Date]
**Maintainer Activity:** [Active/Declining/Inactive]
**Community Support:** [Strong/Moderate/Weak]

### Our Usage
**Used In:**
- [Component/Module 1]
- [Component/Module 2]
- [Component/Module 3]

**How We Use It:**
[Describe how the package is used in the codebase]

**Critical to Application:** [Yes/No]

## Version Analysis

### Current Version Info
**Version:** [X.Y.Z]
**Release Date:** [YYYY-MM-DD]
**Age:** [X months]
**Known Issues:**
- [Issue 1]
- [Issue 2]

### Target Version Info
**Version:** [A.B.C]
**Release Date:** [YYYY-MM-DD]
**Age:** [X days/months]
**Stability:** [Stable/Beta/RC]

### Version History
| Version | Release Date | Type | Notes |
|---------|--------------|------|-------|
| [A.B.C] | [Date] | [Patch/Minor/Major] | [Key changes] |
| [A.B.B] | [Date] | [Patch/Minor/Major] | [Key changes] |
| [X.Y.Z] | [Date] | [Patch/Minor/Major] | Current version |

### Breaking Changes

#### Breaking Change 1: [Description]
**Severity:** [Critical/High/Medium/Low]
**Affects Our Code:** [Yes/No]

**What Changed:**
```[language]
// Before (old version)
// [Code example]

// After (new version)
// [Code example]
```

**Migration Required:**
- [ ] [Step 1]
- [ ] [Step 2]

#### Breaking Change 2: [Description]
[Same structure]

### Deprecated Features We Use
| Feature | Deprecated In | Removed In | Replacement | Action |
|---------|--------------|------------|-------------|--------|
| [API 1] | [Version] | [Version] | [New API] | [What to do] |
| [API 2] | [Version] | [Version] | [New API] | [What to do] |

### New Features
| Feature | Benefit | Should We Adopt? |
|---------|---------|------------------|
| [Feature 1] | [Why it's useful] | [Yes/No/Maybe Later] |
| [Feature 2] | [Why it's useful] | [Yes/No/Maybe Later] |

## Dependency Impact

### Direct Dependencies
**This package depends on:**
| Dependency | Current | Compatible? | Notes |
|------------|---------|-------------|-------|
| [dep-1] | [version] | ✅ Yes | No changes needed |
| [dep-2] | [version] | ⚠️ Update needed | Will auto-update |
| [dep-3] | [version] | ❌ Conflict | Need to resolve |

### Reverse Dependencies
**Packages that depend on this:**
| Package | Version | Compatible? | Notes |
|---------|---------|-------------|-------|
| [pkg-1] | [version] | ✅ Yes | Tested and works |
| [pkg-2] | [version] | ⚠️ Unknown | Need to test |
| [pkg-3] | [version] | ❌ No | May need to upgrade |

### Peer Dependencies
**Required peer dependencies:**
| Peer Dependency | Required Version | Our Version | Compatible? |
|----------------|------------------|-------------|-------------|
| [peer-1] | [semver range] | [X.Y.Z] | ✅/❌ |
| [peer-2] | [semver range] | [X.Y.Z] | ✅/❌ |

## Code Impact Assessment

### Usage Scan
**Files Using This Package:** [X]

```bash
# Commands used to find usage
grep -r "from package_name" src/
grep -r "import { x } from 'package-name'" src/
grep -r "require('package-name')" src/
```

**Usage Locations:**
- `path/to/file1.ext` - [Usage description]
- `path/to/file2.ext` - [Usage description]
- `path/to/file3.ext` - [Usage description]

### API Changes Impact

#### Affected File 1: `path/to/file.ext`
**Lines affected:** [Line numbers]
**Change required:** [Description]

```[language]
// Current code
// [Code snippet]

// Updated code
// [Code snippet]
```

**Estimated effort:** [X minutes/hours]

#### Affected File 2: `path/to/file.ext`
[Same structure]

### Test Impact
**Test files using this package:** [X]
**Tests that need updating:**
- [ ] `test/file1.test.js` - [What needs updating]
- [ ] `test/file2.test.js` - [What needs updating]

## Compatibility Testing

### Local Testing

#### Test Environment Setup
```bash
# Create test branch
git checkout -b upgrade/[package-name]-[version]

# Update package
npm install [package-name]@[version]
# or
pip install [package-name]==[version]
# or
composer require [vendor/package]:[version]
```

#### Test Checklist
- [ ] Package installs successfully
- [ ] No dependency conflicts
- [ ] Application starts
- [ ] Unit tests pass
- [ ] Integration tests pass
- [ ] Manual testing of affected features

### Compatibility Matrix

#### Browser/Platform Compatibility
| Environment | Current Support | New Version Support | Compatible? |
|-------------|----------------|---------------------|-------------|
| Chrome (latest) | ✅ | ✅ | ✅ |
| Firefox (latest) | ✅ | ✅ | ✅ |
| Safari (latest) | ✅ | ✅ | ✅ |
| Edge (latest) | ✅ | ✅ | ✅ |
| Node.js [version] | ✅ | ✅/❌ | ✅/❌ |
| Python [version] | ✅ | ✅/❌ | ✅/❌ |
| PHP [version] | ✅ | ✅/❌ | ✅/❌ |

#### Operating System Compatibility
| OS | Tested? | Works? | Issues |
|----|---------|--------|--------|
| macOS | ✅ | ✅ | None |
| Linux | ✅ | ✅ | None |
| Windows | ✅ | ✅/❌ | [List issues] |

## Testing Strategy

### Pre-Upgrade Testing
- [ ] Document current behavior
- [ ] Create baseline performance metrics
- [ ] Ensure all existing tests pass
- [ ] Test coverage for affected code: [X]%

### Unit Testing
```bash
# Run tests before upgrade
npm test
# or
pytest
# or
./vendor/bin/phpunit
```

**Before upgrade:**
- Tests passing: [X]/[Y]
- Coverage: [X]%

**After upgrade:**
- Tests passing: [?]/[Y]
- Coverage: [?]%
- New failures: [List]

### Integration Testing
- [ ] Test package with other dependencies
- [ ] Test in complete application context
- [ ] Test edge cases and error handling
- [ ] Test performance-critical paths

### Manual Testing
- [ ] [Manual test case 1]
- [ ] [Manual test case 2]
- [ ] [Manual test case 3]

### Performance Testing

**Metrics to compare:**
| Metric | Before | After | Change | Acceptable? |
|--------|--------|-------|--------|-------------|
| Load time | [X]ms | [?]ms | [?]% | ✅/❌ |
| Memory usage | [X]MB | [?]MB | [?]% | ✅/❌ |
| Bundle size | [X]KB | [?]KB | [?]% | ✅/❌ |
| API response | [X]ms | [?]ms | [?]% | ✅/❌ |

**Performance testing tools:**
```bash
# Bundle size analysis
npm run build -- --analyze
# or
webpack-bundle-analyzer

# Performance profiling
# [Tool-specific commands]
```

## Upgrade Execution

### Step 1: Backup
- [ ] Create git branch: `git checkout -b upgrade/[package-name]-[version]`
- [ ] Tag current state: `git tag pre-[package-name]-upgrade`
- [ ] Document current lockfile state

### Step 2: Update Package

#### npm/yarn/pnpm
```bash
# Update to specific version
npm install [package-name]@[version]

# or to latest
npm install [package-name]@latest

# or update range in package.json then:
npm install

# Check lockfile
git diff package-lock.json
```

#### pip
```bash
# Update requirements.txt
# [package-name]==[version]

# Install
pip install -r requirements.txt

# or direct install
pip install [package-name]==[version]

# Freeze to lock
pip freeze > requirements.lock
```

#### composer
```bash
# Update composer.json
# "vendor/package": "^version"

# Install
composer update vendor/package

# or specific version
composer require vendor/package:^version

# Check lockfile
git diff composer.lock
```

### Step 3: Code Migration
- [ ] Update imports/requires if changed
- [ ] Update API calls to new syntax
- [ ] Replace deprecated functions
- [ ] Update configuration if needed
- [ ] Update type definitions (TypeScript/PHPDoc/etc.)

### Step 4: Update Tests
- [ ] Fix failing tests
- [ ] Update test expectations if behavior changed
- [ ] Add tests for new features adopted
- [ ] Verify coverage maintained

### Step 5: Documentation
- [ ] Update code comments
- [ ] Update README if usage changed
- [ ] Update API documentation
- [ ] Update developer guide

### Step 6: Review & Commit
- [ ] Code review
- [ ] Test review
- [ ] Commit changes
  ```bash
  git add .
  git commit -m "chore(deps): upgrade [package-name] from [old] to [new]

  BREAKING CHANGE: [if major version]
  - [Breaking change 1]
  - [Breaking change 2]

  Fixes: [issue/CVE if applicable]"
  ```

## Rollback Plan

### Rollback Procedure
```bash
# Option 1: Revert commit
git revert [commit-hash]

# Option 2: Restore from tag
git checkout pre-[package-name]-upgrade
git checkout -b rollback/[package-name]

# Option 3: Pin to old version
# Update package.json/requirements.txt/composer.json
npm install [package-name]@[old-version]
```

### Rollback Criteria
**Rollback if:**
- Critical functionality broken
- Test failures can't be fixed quickly
- Performance degrades significantly
- Security issue in new version
- Dependency conflicts unresolvable

**Recovery Time:** [X minutes] (How long to rollback)

## Risk Assessment

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| Breaking changes | [L/M/H] | [L/M/H] | Test thoroughly, read changelog |
| Dependency conflicts | [L/M/H] | [L/M/H] | Check compatibility matrix |
| Performance regression | [L/M/H] | [L/M/H] | Benchmark before/after |
| Security vulnerability in new version | Low | Critical | Monitor security advisories |
| Incompatible with framework version | [L/M/H] | [L/M/H] | Check compatibility docs |

## Deployment Strategy

### Staging
- [ ] Deploy to staging environment
- [ ] Run full test suite
- [ ] Manual QA testing
- [ ] Performance testing
- [ ] Monitor for 24-48 hours

### Production
- [ ] Deploy during low-traffic window
- [ ] Monitor error rates closely
- [ ] Monitor performance metrics
- [ ] Have rollback ready
- [ ] Gradual rollout (if using feature flags/canary)

**Deployment Date:** [YYYY-MM-DD]
**Deployment Window:** [Time range]
**On-Call Engineer:** [Name]

## Monitoring

### Metrics to Watch

**Error Monitoring:**
- Error rate threshold: < 0.1%
- Alert if: > 0.5%
- Critical if: > 1%

**Performance Monitoring:**
- Response time threshold: < [X]ms
- Alert if: > [Y]ms
- Memory usage threshold: < [X]MB

**Usage Monitoring:**
- Monitor affected features
- Check logs for deprecation warnings
- Watch for unexpected behavior

### Monitoring Period
- **Hour 1:** Check every 15 minutes
- **Hours 2-24:** Check every hour
- **Days 2-7:** Check daily
- **Week 2+:** Normal monitoring

## Timeline

**Planning:** [YYYY-MM-DD]
**Testing:** [YYYY-MM-DD]
**Staging Deployment:** [YYYY-MM-DD]
**Production Deployment:** [YYYY-MM-DD]
**Monitoring:** [YYYY-MM-DD] to [YYYY-MM-DD]

**Estimated Effort:** [X hours]
**Actual Effort:** [Y hours]

## Progress Tracking

- [ ] Motivation documented
- [ ] Breaking changes analyzed
- [ ] Dependencies checked
- [ ] Code impact assessed
- [ ] Tests updated
- [ ] Code migrated
- [ ] Local testing complete
- [ ] Staging deployment successful
- [ ] Production deployment successful
- [ ] Monitoring period complete
- [ ] Documentation updated

**Current Status:** [Planning/Testing/Deploying/Complete/Rolled Back]
**Last Updated:** [YYYY-MM-DD]

## Post-Upgrade Review

### Results
**Success:** [Yes/No/Partial]

**Metrics:**
| Metric | Before | After | Change | Target | Met? |
|--------|--------|-------|--------|--------|------|
| Version | [X.Y.Z] | [A.B.C] | - | [A.B.C] | ✅ |
| Tests passing | [X]/[Y] | [A]/[B] | - | All | ✅/❌ |
| Performance | [X]ms | [Y]ms | [+/-Z]% | No regression | ✅/❌ |
| Bundle size | [X]KB | [Y]KB | [+/-Z]% | < [W]KB | ✅/❌ |

### Issues Encountered
- [Issue 1] - Severity: [L/M/H] - Resolved: [How]
- [Issue 2] - Severity: [L/M/H] - Resolved: [How]

### Lessons Learned
**What went well:**
- [Point 1]
- [Point 2]

**What could be improved:**
- [Point 1]
- [Point 2]

**For next dependency upgrade:**
- [Recommendation 1]
- [Recommendation 2]

## Related

- **Related Upgrades:** [DEP-XXX, UPGRADE-XXX]
- **Related Tech Debt:** [DEBT-XXX]
- **Security Advisory:** [Link]
- **Pull Request:** [Link]
- **Issue Tracker:** [Link]

---

**Status:** [Planning/Testing/Deploying/Complete/Rolled Back]
**Owner:** [Name]
**Last Updated:** [YYYY-MM-DD]

---

## Package Manager Specific Commands

### npm/yarn/pnpm
```bash
# Check outdated packages
npm outdated
yarn outdated
pnpm outdated

# Update to latest within semver range
npm update [package]
yarn upgrade [package]
pnpm update [package]

# Install specific version
npm install [package]@[version]
yarn add [package]@[version]
pnpm add [package]@[version]

# View package info
npm info [package]
npm view [package] versions

# Check security vulnerabilities
npm audit
yarn audit
pnpm audit
```

### pip
```bash
# Check outdated packages
pip list --outdated

# Install specific version
pip install [package]==[version]

# Install with upgrade
pip install --upgrade [package]

# Show package info
pip show [package]

# Check dependencies
pipdeptree

# Security check
pip-audit
# or
safety check
```

### composer
```bash
# Check outdated packages
composer outdated

# Update specific package
composer update vendor/package

# Require specific version
composer require vendor/package:^version

# Show package info
composer show vendor/package

# Check security vulnerabilities
composer audit
```

### Bundler (Ruby)
```bash
# Check outdated gems
bundle outdated

# Update specific gem
bundle update [gem-name]

# Install specific version
# (edit Gemfile, then)
bundle install

# Show gem info
bundle info [gem-name]
```

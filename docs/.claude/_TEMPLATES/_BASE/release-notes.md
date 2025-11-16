# Release Notes: Version [X.Y.Z]

**Release Date:** [YYYY-MM-DD]
**Release Type:** [Major/Minor/Patch]
**Code Name:** [Optional code name]

---

## Summary

[1-2 sentence summary of this release highlighting the main changes or themes]

---

## ✨ New Features

### [Feature Name]
[Brief description of the feature and why it's valuable]

**Details:**
- [Detail 1]
- [Detail 2]

**Usage:**
```[language]
// Example code showing how to use the new feature
```

**Related:** [PR #123, Issue #456]

---

### [Another Feature]
[Description]

---

## 🐛 Bug Fixes

### [Bug Fix Title]
**Issue:** [What was broken]
**Fix:** [How it was fixed]
**Impact:** [Who was affected]

**Related:** [PR #789, Issue #1011]

---

## 🔧 Improvements

### Performance
- [Improvement 1]: [X]% faster
- [Improvement 2]: Reduced memory usage by [Y]MB

### User Experience
- [UX improvement 1]
- [UX improvement 2]

### Developer Experience
- [DX improvement 1]
- [DX improvement 2]

---

## ⚠️ Breaking Changes

### [Breaking Change 1]
**What Changed:**
[Description of the change]

**Migration Required:**
```[language]
// Before
oldMethod(param)

// After
newMethod({ param, newOption: true })
```

**Affected:**
- [Who/what is affected]

**Migration Guide:**
1. [Step 1]
2. [Step 2]
3. [Step 3]

**Deadline:**  [Date by which migration should be complete]

---

## 📦 Dependencies

### Updated
| Package | Old Version | New Version | Reason |
|---------|-------------|-------------|--------|
| [package-name] | [X.Y.Z] | [A.B.C] | [Security/Feature/Bugfix] |

### Added
- **[package-name]** [A.B.C] - [Why it was added]

### Removed
- **[package-name]** - [Why it was removed, what replaces it]

---

## 🔐 Security

### Security Fixes
- **[CVE-YYYY-XXXXX]**: [Vulnerability fixed] - Severity: [Critical/High/Medium/Low]
- [Other security fix]

**Action Required:**
- [ ] Update to this version immediately if using affected versions
- [ ] Review security advisory: [Link]

---

## 📚 Documentation

### New Documentation
- [New guide or documentation page]
- [API documentation updates]

### Updated Documentation
- [Updated guide]
- [Revised tutorial]

---

## 🏗️ Infrastructure

### Deployment Changes
- [Change to deployment process]
- [New environment variables required]

### Configuration Changes
```yaml
# New configuration options
new_option:
  enabled: true
  value: "default"
```

---

## 🧪 Testing

### Test Coverage
- Overall coverage: [X]% (was [Y]%)
- New tests added: [N]
- Test improvements: [Description]

---

## 📊 Metrics

### Performance Improvements
| Metric | Before | After | Improvement |
|--------|--------|-------|-------------|
| Page Load Time | [X]ms | [Y]ms | [Z]% faster |
| API Response (p95) | [X]ms | [Y]ms | [Z]% faster |
| Bundle Size | [X]KB | [Y]KB | [Z]% smaller |

---

## 🙏 Contributors

Special thanks to all contributors who made this release possible:

- **[Name]** - [Contribution highlights]
- **[Name]** - [Contribution highlights]
- **[Name]** - [Contribution highlights]

**New Contributors:**
- **[Name]** made their first contribution in [PR #XXX]

**Full Contributor List:** [GitHub link]

---

## 📝 Upgrade Instructions

### For npm/pnpm users:
```bash
pnpm update [package-name]@[X.Y.Z]
# or
npm install [package-name]@[X.Y.Z]
```

### For pip/uv users:
```bash
uv add [package-name]==[X.Y.Z]
# or
pip install [package-name]==[X.Y.Z]
```

### For Composer users:
```bash
composer require [vendor/package]:^[X.Y.Z]
```

### Post-upgrade steps:
1. [Step 1 - e.g., Run database migrations]
2. [Step 2 - e.g., Clear caches]
3. [Step 3 - e.g., Update environment variables]

---

## 🔮 What's Next?

### Upcoming in v[X.Y+1.0]
- [Planned feature 1]
- [Planned feature 2]
- [Planned improvement]

### Roadmap
View our [public roadmap](link) for long-term plans.

---

## 📖 Full Changelog

**Commits:** [Link to compare view on GitHub]

**All Changes:**
```
Feature: Add user authentication (#123)
Fix: Resolve memory leak in dashboard (#124)
Chore: Update dependencies (#125)
Docs: Improve installation guide (#126)
... [or list all commits]
```

---

## 🐞 Known Issues

### Issue 1: [Description]
**Workaround:** [How to work around the issue]
**Fix planned for:** v[X.Y.Z+1]

### Issue 2: [Description]
**Status:** Under investigation

---

## 💬 Feedback

We'd love to hear your feedback on this release!

- **Report issues:** [GitHub Issues link]
- **Feature requests:** [Discussion/Issue link]
- **Community:** [Discord/Slack/Forum link]
- **Email:** [support@example.com]

---

## 📜 License

[License type] - See [LICENSE](link) for details.

---

**Download:** [GitHub Release Link](https://github.com/user/repo/releases/tag/vX.Y.Z)
**Documentation:** [Link to docs]
**Previous Release:** [vX.Y.Z-1](link)

---

*Generated on [YYYY-MM-DD] | [Project Name] v[X.Y.Z]*

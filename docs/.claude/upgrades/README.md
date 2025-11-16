# Framework & Dependency Upgrades

> **Index of framework and dependency upgrade tracking**
>
> This directory tracks framework upgrades (Django, Laravel, Vue, etc.) and dependency upgrades.

## Active Upgrades

| ID | Description | Type | From | To | Priority | Status | Owner |
|----|-------------|------|------|-----|----------|--------|-------|
| - | No active upgrades | - | - | - | - | - | - |

## Planned Upgrades

| ID | Description | Type | From | To | Scheduled | Owner |
|----|-------------|------|------|-----|-----------|-------|
| - | No planned upgrades | - | - | - | - | - |

## Completed Upgrades

| ID | Description | Type | From | To | Completed Date | Notes |
|----|-------------|------|------|-----|----------------|-------|
| - | No completed upgrades yet | - | - | - | - | - |

## Upgrades by Framework

### Django
- Current Version: [X.Y.Z]
- Latest Version: [A.B.C]
- Status: [Up-to-date / Needs upgrade]

### Laravel
- Current Version: [X.Y.Z]
- Latest Version: [A.B.C]
- Status: [Up-to-date / Needs upgrade]

### Vue/Nuxt
- Current Version: [X.Y.Z]
- Latest Version: [A.B.C]
- Status: [Up-to-date / Needs upgrade]

### Python
- Current Version: [X.Y.Z]
- Latest Version: [A.B.C]
- Status: [Up-to-date / Needs upgrade]

### Node.js
- Current Version: [X.Y.Z]
- Latest Version: [A.B.C]
- Status: [Up-to-date / Needs upgrade]

## Security Alerts

| Package | CVE | Severity | Current Version | Fixed in | Status |
|---------|-----|----------|----------------|----------|--------|
| - | - | - | - | - | - |

## How to Add Upgrade

### For Framework Upgrades

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

### For Dependency Upgrades

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

## Automated Dependency Monitoring

**Tools configured:**
- [ ] Dependabot
- [ ] Renovate
- [ ] Snyk
- [ ] npm audit / pip-audit

**Notification channels:**
- Slack: [#channel]
- Email: [email]

---

**Last Updated:** [Date]
**Maintained By:** [Team/Person]

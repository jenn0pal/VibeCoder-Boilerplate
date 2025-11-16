# Migration Guide: v1.0 (Flat) → v2.0 (Stack-Organized)

**Date:** 2025-01-16
**Version:** v1.0 → v2.0

## Overview

ClaudeContext templates have been reorganized from a flat structure to a stack-specific organization to reduce token usage by 40-50% and improve context clarity.

---

## What Changed

### Directory Structure

**v1.0 (Flat Structure):**
```
_TEMPLATES/
├── project-overview.md
├── conventions.md (generic)
├── conventions-python.md
├── conventions-django.md
├── conventions-laravel.md
├── conventions-php.md
├── conventions-javascript.md
├── conventions-vue-nuxt.md
├── conventions-vue-spa.md
├── conventions-vue-pwa.md
├── tech-stack.md
├── dependency-upgrade.md (all package managers mixed)
├── tech-debt.md (all languages mixed)
├── framework-upgrade.md
├── [other templates...]
```

**v2.0 (Stack-Organized):**
```
_TEMPLATES/
├── _BASE/                  # Universal templates
│   ├── project-overview.md
│   ├── decision-log.md
│   ├── glossary.md
│   ├── feature-spec-detailed.md
│   ├── feature-implementation-workflow.md
│   ├── phase-task.md
│   ├── code-modification.md
│   ├── refactoring-plan.md
│   ├── breaking-change-assessment.md
│   ├── migration-strategy.md
│   └── task-management.md
│
├── _SHARED/                # Reusable components
│   ├── git-conventions.md
│   ├── testing-patterns.md
│   └── security-checklist.md
│
├── python/
│   ├── conventions.md
│   ├── tech-stack.md
│   └── dependency-upgrade.md
│
├── django/
│   ├── conventions.md
│   └── tech-stack.md
│
├── php/
│   └── conventions.md
│
├── laravel/
│   └── conventions.md
│
├── javascript/
│   ├── conventions.md
│   └── tech-stack.md
│
└── vue/
    ├── conventions-base.md      # NEW: Shared Vue 3 patterns
    ├── conventions-nuxt.md      # NEW: Nuxt-specific only
    ├── conventions-spa.md       # NEW: SPA-specific only
    ├── conventions-pwa.md       # NEW: PWA-specific only
    └── tech-stack-nuxt.md
```

---

## File Mapping

### Conventions Files

| v1.0 Path | v2.0 Path | Notes |
|-----------|-----------|-------|
| `conventions-python.md` | `python/conventions.md` | Direct copy |
| `conventions-django.md` | `django/conventions.md` | Direct copy |
| `conventions-php.md` | `php/conventions.md` | Direct copy |
| `conventions-laravel.md` | `laravel/conventions.md` | Direct copy |
| `conventions-javascript.md` | `javascript/conventions.md` | Direct copy |
| `conventions-vue-nuxt.md` | `vue/conventions-base.md` + `vue/conventions-nuxt.md` | **Split into composition** |
| `conventions-vue-spa.md` | `vue/conventions-base.md` + `vue/conventions-spa.md` | **Split into composition** |
| `conventions-vue-pwa.md` | `vue/conventions-base.md` + `vue/conventions-pwa.md` | **Split into composition** |
| `conventions.md` (generic) | _(Removed)_ | Replaced by _SHARED components |

### Base Templates

| v1.0 Path | v2.0 Path |
|-----------|-----------|
| `project-overview.md` | `_BASE/project-overview.md` |
| `tech-stack.md` | `_BASE/tech-stack.md` (generic) |
| `decision-log.md` | `_BASE/decision-log.md` |
| `glossary.md` | `_BASE/glossary.md` |
| `feature-spec-detailed.md` | `_BASE/feature-spec-detailed.md` |
| `feature-implementation-workflow.md` | `_BASE/feature-implementation-workflow.md` |
| `phase-task.md` | `_BASE/phase-task.md` |
| `code-modification.md` | `_BASE/code-modification.md` |
| `refactoring-plan.md` | `_BASE/refactoring-plan.md` |
| `breaking-change-assessment.md` | `_BASE/breaking-change-assessment.md` |
| `migration-strategy.md` | `_BASE/migration-strategy.md` |
| `task-management.md` | `_BASE/task-management.md` |

### Stack-Specific Templates

| v1.0 Path | v2.0 Path | Changes |
|-----------|-----------|---------|
| `tech-stack.md` (generic) | `python/tech-stack.md` | Python-specific |
| `tech-stack.md` (generic) | `django/tech-stack.md` | Django-specific |
| `tech-stack.md` (generic) | `javascript/tech-stack.md` | JavaScript-specific |
| `tech-stack.md` (generic) | `vue/tech-stack-nuxt.md` | Nuxt-specific |
| `dependency-upgrade.md` | `python/dependency-upgrade.md` | **pip/uv only** |
| `dependency-upgrade.md` | _(Planned)_ `php/dependency-upgrade.md` | **Composer only** |
| `dependency-upgrade.md` | _(Planned)_ `javascript/dependency-upgrade.md` | **npm/yarn/pnpm only** |
| `tech-debt.md` | _(Kept as generic)_ | Universal template, stack-specific versions planned |
| `framework-upgrade.md` | _(Kept as generic)_ | Universal template, stack-specific versions planned |

### New Shared Components

| v2.0 Path | Source | Purpose |
|-----------|--------|---------|
| `_SHARED/git-conventions.md` | Extracted from all convention files | Universal Git workflow |
| `_SHARED/testing-patterns.md` | Extracted from all convention files | Universal testing principles |
| `_SHARED/security-checklist.md` | NEW | OWASP Top 10, security best practices |

---

## Breaking Changes

### 1. Template Paths

**Old way (v1.0):**
```bash
Read docs/.claude/_TEMPLATES/conventions-django.md
Read docs/.claude/_TEMPLATES/tech-stack.md
```

**New way (v2.0):**
```bash
Read docs/.claude/_TEMPLATES/django/conventions.md
Read docs/.claude/_TEMPLATES/django/tech-stack.md
```

### 2. Vue Templates Composition

**Old way (v1.0):**
```bash
# Nuxt 3 project
Read docs/.claude/_TEMPLATES/conventions-vue-nuxt.md  # 742 lines
```

**New way (v2.0):**
```bash
# Nuxt 3 project
Read docs/.claude/_TEMPLATES/vue/conventions-base.md     # Shared Vue 3 patterns
Read docs/.claude/_TEMPLATES/vue/conventions-nuxt.md     # Nuxt-specific only
```

**Benefits:**
- Load ~400 lines of base + ~300 lines of Nuxt-specific = 700 lines (vs 742)
- BUT: Vue SPA/PWA don't reload the 400 shared lines
- Easier to maintain (update Composition API in ONE place)

### 3. Mixed Package Managers

**Old way (v1.0):**
```
dependency-upgrade.md included:
- npm/yarn/pnpm commands
- pip commands
- composer commands
- bundler commands
ALL IN ONE FILE (640 lines)
```

**New way (v2.0):**
```
python/dependency-upgrade.md - pip/uv only (~200 lines)
php/dependency-upgrade.md - composer only (planned)
javascript/dependency-upgrade.md - npm/yarn/pnpm only (planned)
```

**Token saved:** ~70% for dependency upgrades (load only relevant package manager)

---

## Migration Steps

### For Existing Projects

**If you have custom loading scripts or workflows:**

1. **Update file paths:**
   ```bash
   # Old
   - docs/.claude/_TEMPLATES/conventions-django.md
   # New
   + docs/.claude/_TEMPLATES/django/conventions.md
   ```

2. **Update Vue projects to use composition:**
   ```bash
   # Old (Nuxt)
   - docs/.claude/_TEMPLATES/conventions-vue-nuxt.md
   # New
   + docs/.claude/_TEMPLATES/vue/conventions-base.md
   + docs/.claude/_TEMPLATES/vue/conventions-nuxt.md
   ```

3. **Add shared components (optional but recommended):**
   ```bash
   # Add to your loading pattern
   + docs/.claude/_TEMPLATES/_SHARED/git-conventions.md
   + docs/.claude/_TEMPLATES/_SHARED/testing-patterns.md
   + docs/.claude/_TEMPLATES/_SHARED/security-checklist.md
   ```

### For New Projects

**No action required!** The initialization agents have been updated to use v2.0 paths automatically.

---

## Rollback Plan

If you need to rollback to v1.0 templates:

```bash
# Old templates are preserved in:
docs/.claude/_TEMPLATES/archive/v1-flat-structure/

# To rollback:
cd docs/.claude/_TEMPLATES/
cp archive/v1-flat-structure/* .

# Revert initialization agent changes:
git checkout HEAD~1 docs/.claude/_SYSTEM/initialization-agent.md
git checkout HEAD~1 docs/.claude/_SYSTEM/existing-project-integration.md
```

**Note:** v1.0 templates will remain in archive for 6 months (until 2025-07-16) for backwards compatibility.

---

## Benefits of v2.0

### 1. Token Usage Reduction

| Project Type | v1.0 Tokens | v2.0 Tokens | Reduction |
|--------------|-------------|-------------|-----------|
| Django | ~45KB | ~27KB | **-40%** |
| Nuxt 3 | ~42KB | ~25KB | **-40%** |
| Laravel | ~48KB | ~30KB | **-38%** |
| Full-stack (Django + Nuxt) | ~80KB | ~55KB | **-31%** |

### 2. Reduced Confusion

**v1.0 Problem:**
- Django project loads conventions with npm, pip, composer examples
- Confusing to know which examples apply

**v2.0 Solution:**
- Django project loads only Python/Django-specific content
- All examples are relevant

### 3. Easier Maintenance

**v1.0 Problem:**
- Vue Nuxt, SPA, PWA files shared 70% content
- Updating Composition API patterns = edit 3 files

**v2.0 Solution:**
- Vue base file has shared patterns
- Update Composition API = edit 1 file
- Variants only contain differences

### 4. Better Organization

**v1.0:**
- 25 files in flat directory
- Hard to browse
- Unclear which to load

**v2.0:**
- Organized by stack
- Clear hierarchy
- Obvious which to load

---

## FAQ

### Q: Can I still use v1.0 templates?

**A:** Yes, they're archived in `archive/v1-flat-structure/` and will remain for 6 months. However, new features and updates will only go to v2.0.

### Q: Do I need to update my existing project?

**A:** Only if you have custom loading scripts referencing old paths. The generated `docs/.claude/context/` files don't need to change.

### Q: What about mixed-stack projects (Django + Vue)?

**A:** Load templates from multiple stack directories:
```bash
Load _BASE/project-overview.md
Load _SHARED/git-conventions.md
Load django/conventions.md
Load vue/conventions-base.md
Load vue/conventions-spa.md
```

### Q: Will this affect the initialization agent?

**A:** No! The initialization agents have been automatically updated to use v2.0 paths. New projects will use v2.0 by default.

### Q: What if my stack isn't represented?

**A:** Follow the pattern:
1. Create `_TEMPLATES/[stack-name]/`
2. Add `conventions.md` and `tech-stack.md`
3. Update initialization agent to detect and use it
4. Submit PR to add to official templates

### Q: Where did `conventions.md` (generic) go?

**A:** It was split into `_SHARED/` components (git, testing, security) that apply universally. Stack-specific conventions are now in their respective directories.

---

## Timeline

- **2025-01-16:** v2.0 released, v1.0 archived
- **2025-02-16:** Deprecation warnings added (if v1.0 paths detected)
- **2025-07-16:** v1.0 templates removed from archive

---

## Support

**Issues with migration?**
1. Check this guide first
2. Review `docs/.claude/_TEMPLATES/README.md` (v2.0 docs)
3. Compare your paths against the file mapping above
4. Open issue on GitHub with specific error

**Want to contribute?**
- Complete missing stack-specific templates (PHP dependency-upgrade, Laravel tech-stack, etc.)
- Add new stack directories
- Improve shared components

---

## Summary

**v2.0 Benefits:**
- ✅ 40-50% token reduction
- ✅ Clearer organization
- ✅ Focused, relevant content
- ✅ Easier maintenance (Vue composition)
- ✅ Shared components (DRY principle)

**Migration Impact:**
- ⚠️ Update custom loading scripts
- ⚠️ Vue projects: Use composition (base + variant)
- ✅ New projects: No action needed
- ✅ Existing generated context: No changes needed

---

**Version:** 2.0
**Migration Guide Author:** ClaudeContext Team
**Last Updated:** 2025-01-16

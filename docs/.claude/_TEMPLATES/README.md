# Claude Documentation Templates (v2.0)

## Overview

This directory contains comprehensive templates for optimizing your Claude workflow across different projects. **Version 2.0** introduces a stack-specific organization to reduce token usage and improve context clarity.

**New in v2.0:**
- 📁 Stack-specific organization (python/, django/, javascript/, etc.)
- 🔄 Reduced token waste by ~40-50%
- 🧩 Composition-based Vue templates (base + variant)
- 📚 Shared components for universal patterns

---

## 📂 Directory Structure

```
_TEMPLATES/
├── _BASE/                      # Universal templates (language-agnostic)
│   ├── project-overview.md     # Comprehensive project context
│   ├── decision-log.md         # Architectural Decision Records
│   ├── glossary.md             # Project terminology
│   ├── feature-spec-detailed.md # Feature specifications
│   ├── feature-implementation-workflow.md # Multi-phase features
│   ├── phase-task.md           # Individual phase tasks
│   ├── code-modification.md    # Code change documentation
│   ├── refactoring-plan.md     # Test-driven refactoring
│   ├── breaking-change-assessment.md # Impact analysis
│   ├── migration-strategy.md   # Data/platform migrations
│   └── task-management.md      # Task tracking
│
├── _SHARED/                    # Reusable components
│   ├── git-conventions.md      # Git workflow, commits, PRs
│   ├── testing-patterns.md     # Universal testing principles
│   └── security-checklist.md   # OWASP Top 10, best practices
│
├── python/                     # Python-specific
│   ├── conventions.md          # Python code standards (uv, ruff)
│   ├── tech-stack.md           # Python tech stack template
│   └── dependency-upgrade.md   # pip/uv package management
│
├── django/                     # Django framework
│   ├── conventions.md          # Django patterns & best practices
│   └── tech-stack.md           # Django-specific stack
│
├── php/                        # PHP-specific
│   └── conventions.md          # PHP code standards
│
├── laravel/                    # Laravel framework
│   └── conventions.md          # Laravel patterns & best practices
│
├── javascript/                 # JavaScript/TypeScript
│   ├── conventions.md          # JS/TS code standards
│   └── tech-stack.md           # Node.js, npm, build tools
│
└── vue/                        # Vue 3 ecosystem
    ├── conventions-base.md     # Shared Vue 3 Composition API
    ├── conventions-nuxt.md     # Nuxt 3-specific additions
    ├── conventions-spa.md      # Vue SPA-specific additions
    ├── conventions-pwa.md      # Vue PWA-specific additions
    └── tech-stack-nuxt.md      # Nuxt 3 tech stack
```

---

## 🚀 Quick Start

### For New Projects

```bash
# Load base templates
Load docs/.claude/_TEMPLATES/_BASE/project-overview.md
Load docs/.claude/_TEMPLATES/_BASE/decision-log.md

# Load stack-specific conventions
# Django project:
Load docs/.claude/_TEMPLATES/django/conventions.md

# Nuxt 3 project:
Load docs/.claude/_TEMPLATES/vue/conventions-base.md
Load docs/.claude/_TEMPLATES/vue/conventions-nuxt.md
```

### For Existing Projects

Use the existing-project-integration agent which will automatically load the correct templates based on your detected stack.

---

## 📋 Template Categories

### Core Documentation (_BASE/)

| Template | Purpose | When to Use |
|----------|---------|-------------|
| **project-overview.md** | Complete project context | Every project initialization |
| **decision-log.md** | Track architectural decisions | When making significant tech decisions |
| **glossary.md** | Domain terminology | Projects with domain-specific language |
| **feature-spec-detailed.md** | Comprehensive feature specs | Planning complex features |
| **feature-implementation-workflow.md** | Multi-phase feature breakdown | Features requiring multiple agents/phases |
| **phase-task.md** | Individual phase execution | Each phase of a multi-phase feature |
| **code-modification.md** | Plan code changes | Medium/large modifications |
| **refactoring-plan.md** | Test-driven refactoring | Code quality improvements |
| **breaking-change-assessment.md** | Analyze breaking changes | API changes, major updates |
| **migration-strategy.md** | Plan migrations | Database, platform, architecture changes |
| **task-management.md** | Track tasks and sprints | Project management integration |

### Shared Components (_SHARED/)

| Component | Purpose | Include When |
|-----------|---------|--------------|
| **git-conventions.md** | Git workflow, commits, PRs | All projects using git |
| **testing-patterns.md** | Testing principles, TDD, test types | All projects requiring tests |
| **security-checklist.md** | OWASP Top 10, security best practices | All web applications |

### Stack-Specific Templates

#### Python Stack (python/)
- **conventions.md** - Python 3.12+, uv package manager, ruff linter/formatter, type hints, pytest
- **tech-stack.md** - Modern Python tooling and libraries
- **dependency-upgrade.md** - uv/pip package management

#### Django Stack (django/)
- **conventions.md** - Django 5.0+ patterns, DRF, dual-ID pattern, service layer, async views
- **tech-stack.md** - Django ecosystem (PostgreSQL, Celery, Redis)

#### PHP Stack (php/)
- **conventions.md** - PHP 8.3+, PSR standards, Composer

#### Laravel Stack (laravel/)
- **conventions.md** - Laravel 11+, Eloquent, service containers, repository pattern

#### JavaScript Stack (javascript/)
- **conventions.md** - ES2024+, TypeScript, React/Vue/Node.js patterns
- **tech-stack.md** - Node.js, npm/yarn/pnpm, build tools

#### Vue Stack (vue/)
- **conventions-base.md** - Vue 3 Composition API (shared by all Vue variants)
- **conventions-nuxt.md** - Nuxt 3 additions (auto-imports, SSR, file-based routing)
- **conventions-spa.md** - Vue SPA additions (manual imports, Vue Router, Pinia)
- **conventions-pwa.md** - Vue PWA additions (service workers, offline sync)
- **tech-stack-nuxt.md** - Nuxt 3 ecosystem

---

## 💡 Loading Patterns

### Single Stack Project

**Django Project:**
```
Load _BASE/project-overview.md
Load _SHARED/git-conventions.md
Load _SHARED/testing-patterns.md
Load django/conventions.md
```
**Token saved:** ~40% (no PHP, JS, Composer, npm examples)

**Nuxt 3 Project:**
```
Load _BASE/project-overview.md
Load _SHARED/git-conventions.md
Load _SHARED/testing-patterns.md
Load vue/conventions-base.md
Load vue/conventions-nuxt.md
```
**Token saved:** ~50% (no Python, PHP; Vue SPA/PWA specifics excluded)

### Full-Stack Project

**Django + Nuxt:**
```
Load _BASE/project-overview.md
Load _SHARED/git-conventions.md
Load _SHARED/testing-patterns.md
Load django/conventions.md
Load vue/conventions-base.md
Load vue/conventions-nuxt.md
```
**Token saved:** ~30% (no PHP, Laravel; focused JS/Python only)

---

## 🔄 Composition Pattern (Vue Example)

Instead of maintaining 3 large files with 70% duplication:
- ❌ OLD: `conventions-vue-nuxt.md` (742 lines)
- ❌ OLD: `conventions-vue-spa.md` (1,008 lines)
- ❌ OLD: `conventions-vue-pwa.md` (1,025 lines)

We now use composition:
- ✅ NEW: `conventions-base.md` (~400 lines) - Shared Vue 3 patterns
- ✅ NEW: `conventions-nuxt.md` (~300 lines) - Nuxt-specific only
- ✅ NEW: `conventions-spa.md` (~250 lines) - SPA-specific only
- ✅ NEW: `conventions-pwa.md` (~300 lines) - PWA-specific only

**Benefits:**
- Update Vue 3 Composition API patterns in ONE place
- Each variant file is focused and concise
- Load only what you need
- Easier maintenance

---

## 📊 Template Statistics

| Category | Template Count | Avg Size | Total |
|----------|----------------|----------|-------|
| **_BASE** | 11 files | ~10KB | ~110KB |
| **_SHARED** | 3 files | ~15KB | ~45KB |
| **python** | 3 files | ~20KB | ~60KB |
| **django** | 2 files | ~30KB | ~60KB |
| **php** | 1 file | ~20KB | ~20KB |
| **laravel** | 1 file | ~30KB | ~30KB |
| **javascript** | 2 files | ~20KB | ~40KB |
| **vue** | 5 files | ~15KB | ~75KB |
| **TOTAL** | 28 files | ~15KB | ~440KB |

**Comparison with v1.0:**
- v1.0: 25 flat files, ~373KB, high duplication
- v2.0: 28 organized files, ~440KB, but load 40-50% less per session

---

## 🛠️ Customization Guide

### Adding New Stacks

1. Create stack directory: `mkdir _TEMPLATES/[stack-name]/`
2. Add core files:
   - `conventions.md` - Stack coding standards
   - `tech-stack.md` - Stack ecosystem
   - `dependency-upgrade.md` - Package manager specific (if different from existing)
3. Update initialization agents to recognize new stack
4. Add to this README

### Extending Existing Stacks

1. Add new template to stack directory
2. Reference in initialization workflow
3. Document in stack's conventions or create new template

### Creating Variants (like Vue)

For frameworks with multiple deployment patterns:

1. Create `conventions-base.md` with shared patterns
2. Create variant files (`conventions-[variant].md`) with only differences
3. Document composition pattern in loading instructions

---

## 📝 Best Practices

### DO:
- ✅ Load only templates relevant to your stack
- ✅ Use composition for frameworks with variants
- ✅ Keep templates focused (one concern per file)
- ✅ Update templates as you learn better patterns
- ✅ Archive outdated templates
- ✅ Document decisions in decision-log.md

### DON'T:
- ❌ Load templates from multiple stacks unless full-stack project
- ❌ Duplicate content across stack directories
- ❌ Mix package managers in single template
- ❌ Let templates become stale
- ❌ Include sensitive information

---

## 🔄 Migration from v1.0

**Old flat structure templates** are being deprecated and will move to `archive/`:
- `conventions-python.md` → `python/conventions.md`
- `conventions-django.md` → `django/conventions.md`
- `conventions-laravel.md` → `laravel/conventions.md`
- `conventions-php.md` → `php/conventions.md`
- `conventions-javascript.md` → `javascript/conventions.md`
- `conventions-vue-nuxt.md` → `vue/conventions-base.md` + `vue/conventions-nuxt.md`
- `conventions-vue-spa.md` → `vue/conventions-base.md` + `vue/conventions-spa.md`
- `conventions-vue-pwa.md` → `vue/conventions-base.md` + `vue/conventions-pwa.md`

**Action required:**
- Update your loading patterns to use new paths
- Initialization agents have been updated automatically
- Old templates will remain temporarily for backwards compatibility

---

## 🎯 Success Metrics

Track the effectiveness of stack-specific organization:

| Metric | v1.0 | v2.0 | Improvement |
|--------|------|------|-------------|
| **Token Usage** (Django) | ~45KB | ~27KB | -40% |
| **Token Usage** (Nuxt) | ~42KB | ~25KB | -40% |
| **Token Usage** (Full-stack) | ~80KB | ~55KB | -31% |
| **Context Clarity** | Mixed examples | Stack-focused | ✅ Better |
| **Maintenance** | High duplication | Composition | ✅ Easier |
| **Discovery** | Flat list | Organized | ✅ Clearer |

---

## 📚 Resources

### Documentation
- [Claude Documentation](https://docs.anthropic.com)
- [Markdown Guide](https://www.markdownguide.org)
- [Conventional Commits](https://www.conventionalcommits.org)

### Modern Tooling
- **uv** - Fast Python package manager
- **ruff** - Extremely fast Python linter/formatter
- **Vite** - Next-generation frontend tooling
- **Pest** - Elegant PHP testing framework

---

## 🤝 Contributing

### Adding Templates
1. Create in appropriate stack directory
2. Follow existing structure and formatting
3. Include usage instructions
4. Update this README
5. Test with real projects

### Improving Templates
1. Make changes in feature branch
2. Document what changed and why
3. Test across multiple projects
4. Update version numbers
5. Submit pull request

---

## 📦 Version History

- **v2.0** (2025-01-16) - Stack-specific organization, composition patterns, shared components
- **v1.3.0** (2024-12-XX) - Multi-phase features, Vue/Nuxt support
- **v1.2.0** (2024-XX-XX) - Code modification, refactoring workflows
- **v1.0** (2024-XX-XX) - Initial release

---

**Templates Version:** 2.0
**Last Updated:** 2025-01-16
**Maintained by:** ClaudeContext Team

**Remember**: These templates are optimized for Claude AI collaboration. Load only what you need for your specific stack to maximize efficiency and clarity.

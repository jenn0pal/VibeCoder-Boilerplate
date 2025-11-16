# Changelog

All notable changes to ClaudeContext Boilerplate will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [2.0.0] - 2025-01-16

**Status:** Major Release - Stack-Specific Template Organization

### Breaking Changes

#### Template Path Restructuring
- **Old:** Flat template structure (`conventions-django.md`, `conventions-python.md`, etc.)
- **New:** Stack-specific directories (`django/conventions.md`, `python/conventions.md`, etc.)
- **Impact:** Custom loading scripts must update paths (see MIGRATION-GUIDE.md)
- **Migration:** Old templates archived in `archive/v1-flat-structure/` for 6 months

### Added

#### New Directory Structure
- **`_BASE/`** - 11 universal templates (language-agnostic)
- **`_SHARED/`** - 3 reusable components:
  - `git-conventions.md` - Universal Git workflow, commits, PRs (comprehensive)
  - `testing-patterns.md` - Testing principles, TDD, test pyramid, coverage
  - `security-checklist.md` - OWASP Top 10, security best practices
- **Stack directories:** `python/`, `django/`, `php/`, `laravel/`, `javascript/`, `vue/`

#### Vue Template Composition System
- **`vue/conventions-base.md`** - Shared Vue 3 Composition API patterns (~400 lines)
- **`vue/conventions-nuxt.md`** - Nuxt 3-specific additions only (~300 lines)
- **`vue/conventions-spa.md`** - Vue SPA-specific additions only (~250 lines)
- **`vue/conventions-pwa.md`** - Vue PWA-specific additions only (~300 lines)
- **Benefit:** 70% duplication eliminated, single source of truth for Vue 3 patterns

#### Stack-Specific Templates
- **`python/tech-stack.md`** - Python ecosystem (uv, ruff, pytest)
- **`python/dependency-upgrade.md`** - pip/uv package management only
- **`django/tech-stack.md`** - Django-specific stack (DRF, Celery, PostgreSQL)
- **`javascript/tech-stack.md`** - JavaScript ecosystem (Node.js, npm, ESLint)
- **`vue/tech-stack-nuxt.md`** - Nuxt 3 tech stack

#### Documentation
- **`_TEMPLATES/README.md`** - Complete v2.0 documentation with usage patterns
- **`archive/v1-flat-structure/MIGRATION-GUIDE.md`** - Comprehensive migration guide
- **CLAUDE.md:** Added "Template Organization (v2.0)" section

### Changed

#### Token Usage Optimization
- **Django projects:** 45KB → 27KB (**-40% token reduction**)
- **Nuxt projects:** 42KB → 25KB (**-40% token reduction**)
- **Full-stack projects:** 80KB → 55KB (**-31% token reduction**)
- **Cause:** Eliminated cross-stack pollution (no npm in Django, no pip in JavaScript)

#### Initialization Agents
- **`initialization-agent.md`** - Updated to load from stack-specific paths
- **`existing-project-integration.md`** - Updated framework detection and path mapping
- **Vue projects:** Now load composition-based templates (base + variant)

#### Template Organization
- Moved all language-specific conventions to respective stack directories
- Split generic templates into _BASE/ (universal) and _SHARED/ (components)
- Archived old flat templates with backwards compatibility for 6 months

### Improved

#### Maintenance
- **Before:** Update Vue Composition API = edit 3 files (Nuxt, SPA, PWA)
- **After:** Update Vue Composition API = edit 1 file (conventions-base.md)
- **Reduction:** 66% less maintenance work for Vue templates

#### Developer Experience
- Clearer organization (hierarchical vs flat)
- Easier discovery (stack-based grouping)
- Focused content (only relevant examples)
- Better composition (load base + variant)

### Deprecated

#### v1.0 Flat Templates (Archived)
All moved to `archive/v1-flat-structure/`:
- `conventions-python.md` → `python/conventions.md`
- `conventions-django.md` → `django/conventions.md`
- `conventions-laravel.md` → `laravel/conventions.md`
- `conventions-php.md` → `php/conventions.md`
- `conventions-javascript.md` → `javascript/conventions.md`
- `conventions-vue-nuxt.md` → `vue/conventions-base.md` + `vue/conventions-nuxt.md`
- `conventions-vue-spa.md` → `vue/conventions-base.md` + `vue/conventions-spa.md`
- `conventions-vue-pwa.md` → `vue/conventions-base.md` + `vue/conventions-pwa.md`
- `tech-stack.md` (generic) → Stack-specific versions
- `dependency-upgrade.md` (mixed) → `python/dependency-upgrade.md` (pip/uv only)

**Removal date:** 2025-07-16 (6 months grace period)

### Migration Guide

**For existing projects with custom loading:**
1. Update template paths in loading scripts
2. Vue projects: Use composition pattern (base + variant)
3. Add shared components for git, testing, security

**For new projects:**
- No action needed - initialization agents updated automatically

**See:** `docs/.claude/_TEMPLATES/archive/v1-flat-structure/MIGRATION-GUIDE.md`

### Statistics

| Metric | v1.0 | v2.0 | Improvement |
|--------|------|------|-------------|
| Template Count | 25 files | 28 files | +3 (shared components) |
| Organization | Flat | Hierarchical | ✅ Better discovery |
| Token Usage (Django) | ~45KB | ~27KB | -40% |
| Token Usage (Nuxt) | ~42KB | ~25KB | -40% |
| Token Usage (Full-stack) | ~80KB | ~55KB | -31% |
| Vue Maintenance | 3 files | 1 file | -66% |
| Cross-stack Pollution | High | None | ✅ Eliminated |

## [1.3.0-beta] - 2025-10-28

**Status:** Beta Release - Testing and feedback phase

### Added

#### Multi-Phase Feature Implementation Workflow
- **New Template:** `feature-implementation-workflow.md` - Break complex features into manageable phases with agent assignments
- **New Template:** `phase-task.md` - Individual phase task template with dedicated agent
- **New Directory:** `docs/.claude/tasks/` - Phase-based task files (FEAT-[ID]-PHASE-[N].md format)
- **New Guide:** `docs/.claude/tasks/README.md` - Comprehensive task management guide
- **Example:** User Authentication feature with 5 phases demonstrating agent assignments

#### Agent Assignment System
- Agent assignment strategy for 11 specialized agents
- 5 common phase patterns (Full-Stack, Backend-Heavy, Frontend-Heavy, Infrastructure, Data Pipeline)
- Agent activation prompts per phase
- Clear handoff documentation between phases

#### Documentation
- `WORKFLOW-UPDATE-v1.3.0.md` - Complete workflow system documentation
- `TEMPLATE-REDUNDANCY-ANALYSIS.md` - Comprehensive template analysis
- `CLEANUP-SUMMARY-2025-10-28.md` - Template cleanup summary
- Multi-phase workflow section in README.md with examples

#### Workflow Features
- Cross-phase dependencies management
- Quality gates per phase and overall feature
- Risk management per phase and cross-phase
- Progress tracking with phase completion checklists
- Timeline management with milestones
- Handoff procedures between phases

### Changed
- **README.md:** Updated template count from 14 to 16
- **README.md:** Added Multi-Phase Feature Implementation Workflow section
- **README.md:** Updated directory structure documentation
- **CLAUDE.md:** Added `docs/.claude/tasks/` to Key Locations
- **CLAUDE.md:** Added "Implement multi-phase feature" workflow prompt
- **CLAUDE.md:** Added "Work on specific phase" workflow prompt
- **_TEMPLATES/README.md:** Updated template count to 16
- **_TEMPLATES/README.md:** Added deprecation notice

### Deprecated
- **`new-feature.md`** template (incomplete, superseded)
  - Moved to: `docs/.claude/archive/_TEMPLATES/deprecated/new-feature.md`
  - Reason: Only 52 lines, incomplete structure, malformed markdown
  - Replaced by: `feature-spec-detailed.md` and `feature-implementation-workflow.md`
  - Migration guide provided in deprecation README

### Fixed
- Template redundancy (removed 1 redundant template)
- Improved clarity by consolidating feature workflows

## [1.2.0] - 2025-10-23

### Added
- **Code Modification Workflow:** `code-modification.md` template
- **Refactoring Workflow:** `refactoring-plan.md` template
- **Bug Tracking:** Bug fixing workflow and `docs/.claude/bugs/` directory
- **New Directories:**
  - `docs/.claude/modifications/` - Code modification tracking
  - `docs/.claude/refactoring/` - Refactoring planning
  - `docs/.claude/bugs/` - Bug tracking
- **Database optimization patterns** in refactoring template
- **Tools guidance** for measuring metrics (complexity, coverage, performance)
- **Framework-specific syntax** for Laravel and Django

### Changed
- **CLAUDE.md:** Added "Fix a bug", "Modify existing code", "Refactor code" workflows
- **README.md:** Added agent reference guide, prompt library, workflow optimization tips
- **README.md:** Consolidated agent-configs, prompt-templates, workflow-optimization-guide
- **_TEMPLATES/README.md:** Removed user-facing guides (moved to README.md)

### Fixed
- Task size guidelines (small/medium/large)
- Clear distinction between modification vs refactoring

## [1.1.0] - 2025-10-22

### Added
- **Existing Project Integration:** Workflow for integrating boilerplate with existing projects
- **Safety Checks:** Prevents overwriting source code during integration
- **GitHub Actions Workflows:** PR Assistant and Code Review automation

### Changed
- **Initialization Workflow:** Improved with better error handling
- **Documentation:** Fixed inconsistencies across templates

## [1.0.0] - 2025-10-21

### Added
- Initial release of ClaudeContext Boilerplate
- **14 Professional Templates:**
  - Core: project-overview, conventions, tech-stack, decision-log
  - Language-specific: Python, JavaScript, PHP, Django, Laravel conventions
  - Workflow: task-management, feature-spec-detailed, glossary
- **11 Specialized AI Agents:**
  - Product Owner, Systems Architect, Backend Engineer, Frontend Developer
  - Test Engineer, Code Reviewer, Security Auditor, Performance Optimizer
  - DevOps Engineer, Data Engineer, Documentation Specialist
- **Initialization Agent:** Automated project setup
- **Directory Structure:** Organized workspace for Claude AI collaboration
- **Comprehensive Documentation:** CLAUDE.md master instructions, README.md user guide

---

## Version Schema

- **Major (X.0.0):** Breaking changes, major new features
- **Minor (0.X.0):** New features, backward compatible
- **Patch (0.0.X):** Bug fixes, documentation updates

## Links

- [GitHub Repository](https://github.com/jenn0pal/vibecoding-boilerplate)
- [Documentation](README.md)
- [CLAUDE.md](CLAUDE.md)

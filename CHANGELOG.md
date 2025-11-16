# Changelog

All notable changes to ClaudeContext Boilerplate will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

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

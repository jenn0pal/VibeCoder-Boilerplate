# Working with Claude on [Project Name]

> **Comprehensive Documentation Workflow for Quality Code**

## ⚡ Quick Start

### First Time Setup (New Projects Only)
```
Load docs/.claude/_SYSTEM/initialization-agent.md
Initialize [language] project: [name]
```

**Examples:**
- "Initialize Django project: TaskHub"
- "Initialize Laravel project: ShopAPI"
- "Initialize Python project: DataPipeline"
- "Initialize Nuxt project: MyApp"
- "Initialize Vue SPA project: Dashboard"
- "Initialize Vue PWA project: MobileApp"

Claude will ask you about your project and automatically generate all documentation.

**⚠️ Note:** This boilerplate includes placeholder files in `docs/.claude/context/`. The initialization agent will replace these with your project's actual documentation.

**Verify initialization succeeded:**
```bash
# Check that context files were generated
ls docs/.claude/context/
# Expected: project-overview.md, conventions.md, tech-stack.md, decision-log.md

# Verify CLAUDE.md was updated (should show your project info, not placeholders)
grep "Purpose:" CLAUDE.md

# Check project structure was created
ls -la  # Should see directories appropriate for your stack (apps/, src/, tests/, etc.)
```

### Existing Project Integration

**If you already have a Django/Laravel/Python/JavaScript/Vue/Nuxt project:**
```
Load docs/.claude/_SYSTEM/existing-project-integration.md
Integrate ClaudeContext with my existing [framework] project
```

**Examples:**
- "Integrate ClaudeContext with my existing Django project"
- "Integrate ClaudeContext with my existing Laravel project"
- "Integrate ClaudeContext with my existing Python project"
- "Integrate ClaudeContext with my existing Nuxt project"
- "Integrate ClaudeContext with my existing Vue SPA project"
- "Integrate ClaudeContext with my existing Vue PWA project"

Claude will:
- ✅ Analyze your existing codebase structure
- ✅ Generate documentation from your actual code
- ✅ Preserve your existing project structure
- ✅ Create context files based on your current architecture
- ✅ Document your existing conventions and patterns
- ✅ Never overwrite your source code or config files

**Verify integration succeeded:**
```bash
# Check that context files were generated
ls docs/.claude/context/
# Expected: project-overview.md, conventions.md, tech-stack.md, decision-log.md

# Verify CLAUDE.md was updated (should show your project info, not placeholders)
grep "Purpose:" CLAUDE.md

# Verify existing structure was preserved (no new apps/, src/ directories)
git status  # Should only show new files in docs/.claude/
```

### Starting a Development Session

**Standard workflow:**
```
Load CLAUDE.md
Load docs/.claude/context/project-overview.md
Working on: [feature name or task description]
```

**What you get:**
- ✅ Comprehensive project understanding
- ✅ Reduced risk of hallucinations
- ✅ Explicit conventions and patterns
- ✅ Consistent code quality
- ✅ Clear architectural guidance
- ✅ Better for team collaboration

## 🎯 Project Overview
- **Purpose:** [One sentence]
- **Stage:** [MVP/Beta/Production]
- **Tech Stack:** [Key technologies]
- **Team:** [Size and structure]

## 📂 Key Locations
```
docs/.claude/features/       - Feature specs & working docs
docs/.claude/tasks/          - Phase-based feature tasks (FEAT-[ID]-PHASE-[N].md format)
docs/.claude/bugs/           - Bug tracking (BUG-[ID].md format)
docs/.claude/modifications/  - Code modification plans (MOD-[ID].md format)
docs/.claude/refactoring/    - Refactoring plans (REFACTOR-[ID].md format)
docs/.claude/tech-debt/      - Technical debt tracking (DEBT-[ID].md format)
docs/.claude/upgrades/       - Framework/dependency upgrades (UPGRADE-[ID].md format)
docs/.claude/context/        - Project context (READ FIRST)
docs/.claude/agents/         - Specialized agent configs
docs/.claude/archive/        - ⚠️ NEVER READ (obsolete)
docs/features/               - Official documentation
src/                         - Source code
```

## 🚨 Critical Rules
1. **NEVER** read anything in `docs/.claude/archive/`
2. **ALWAYS** follow `docs/.claude/context/conventions.md`
3. **REQUIRED:** Write tests for all features
4. **REQUIRED:** Use conventional commits
5. **CHECK:** Existing patterns before suggesting new ones

## 🔄 Standard Workflow (Default)

### Starting New Work
1. Load context: `CLAUDE.md` and `docs/.claude/context/project-overview.md`
2. Review feature: `docs/.claude/features/[feature-name]/spec.md`
3. Follow conventions: `docs/.claude/context/conventions.md`
4. Implement → Test → Document

### Common Prompts

**Start new feature:**
```
Load CLAUDE.md and docs/.claude/context/project-overview.md
Starting feature: [name]
Spec: docs/.claude/features/[name]/spec.md
```

**Resume work:**
```
Load CLAUDE.md
Continuing: [feature-name]
Last completed: [task]
Today's goal: [objective]
```

**Code review:**
```
Load CLAUDE.md and conventions.md
Review: [files or PR link]
Focus: [security/performance/standards]
```

**Fix a bug:**
```
Load CLAUDE.md and docs/.claude/context/conventions.md

Bug: [Brief description]
Severity: [Critical/High/Medium/Low]
Environment: [Dev/Staging/Production]
Steps to reproduce:
1. [Step 1]
2. [Step 2]
3. [Step 3]

Error message: [Paste error or describe unexpected behavior]

Please help me:
1. Write a failing test that reproduces the bug
2. Identify the root cause
3. Implement a fix following our conventions
4. Verify the test passes
5. Add regression test to prevent recurrence
6. Update decision log if this reveals an architectural issue
```

**Modify existing code:**
```
Load CLAUDE.md and docs/.claude/context/conventions.md

Change: [Brief description of modification]
Type: [Styling/Feature Enhancement/Refactor/Config/Optimization]
Scope: [Files/components affected]
Reason: [Why making this change]

Current state: [What exists now]
Desired state: [What you want it to be]

Please help me:
1. Identify all files that need modification
2. Implement the change following our conventions
3. Update tests if behavior changes
4. Update documentation if this is a significant change
```

**Examples:**
- Styling: "Change theme from blue to orange"
- Feature Enhancement: "Add 'Remember me' checkbox to login form"
- Config: "Update API rate limits from 100 to 200 requests/min"
- Optimization: "Cache frequently accessed database queries"

**Refactor code:**
```
Load CLAUDE.md and docs/.claude/context/conventions.md

Refactor: [Component/module/file to refactor]
Goal: [Improve performance/readability/maintainability/testability]
Scope: [What's allowed to change]
Constraints: [What must stay the same - e.g., external API, behavior]

Please help me:
1. Ensure tests exist before refactoring (write if missing)
2. Make incremental improvements
3. Run tests after each change
4. Maintain same external behavior
5. Update documentation if architecture changes
```

**Implement multi-phase feature:**
```
Load CLAUDE.md and docs/.claude/context/project-overview.md

Feature: [Feature name]
Complexity: [Simple/Medium/Complex]
Description: [Brief description]

This feature requires multiple phases with different specializations.

Please help me:
1. Create a feature implementation workflow using:
   docs/.claude/_TEMPLATES/feature-implementation-workflow.md
2. Break down the feature into logical phases
3. Assign appropriate agents to each phase
4. Create individual phase task files using:
   docs/.claude/_TEMPLATES/phase-task.md
```

**Work on specific phase:**
```
Load CLAUDE.md
Load docs/.claude/context/project-overview.md
Load docs/.claude/_SYSTEM/agents/[agent-name].md
Load docs/.claude/tasks/FEAT-[ID]-PHASE-[N]-[brief-name].md

I need to complete Phase [N] of feature [Feature Name].
Please help me execute this phase following our conventions.
```

**Track technical debt:**
```
Load CLAUDE.md and docs/.claude/context/conventions.md

Tech Debt: [Brief description]
Type: [Framework Upgrade/Dependency Update/Code Refactoring/Performance/Security]
Priority: [Critical/High/Medium/Low]
Estimated Effort: [Hours/Days/Weeks]

Current impact:
- [Impact 1 - e.g., Slows down feature development by 20%]
- [Impact 2 - e.g., Security vulnerability risk]
- [Impact 3 - e.g., Blocking framework upgrade]

Please help me:
1. Assess the scope and complexity
2. Create a tech debt tracking document (DEBT-[ID].md)
3. Develop an implementation plan
4. Identify risks and dependencies
5. Provide timeline estimate
```

**Upgrade framework:**
```
Load CLAUDE.md and docs/.claude/context/tech-stack.md

Framework Upgrade: [Framework name]
From: [Current version]
To: [Target version]
Upgrade Type: [Major/Minor/Patch]

Reason: [Why upgrade now? - e.g., Security, features, end-of-support]

Please help me:
1. Check breaking changes in release notes
2. Audit package compatibility
3. Create upgrade plan with rollback strategy (UPGRADE-[ID].md)
4. Execute upgrade incrementally
5. Validate with comprehensive tests
6. Update documentation
```

**Upgrade dependency:**
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

**Assess breaking change:**
```
Load CLAUDE.md and docs/.claude/context/conventions.md

Breaking Change: [Description]
Type: [API Change/Database Schema/Configuration/Dependency Upgrade]
Severity: [Critical/High/Medium/Low]

Proposed change:
[What we want to change and why]

Affects:
- [Who/what is affected]

Please help me:
1. Analyze impact and blast radius
2. Create breaking change assessment (BREAK-[ID].md)
3. Develop migration strategy
4. Plan communication timeline
5. Create migration tools/scripts
6. Document rollback procedure
```

**Plan data migration:**
```
Load CLAUDE.md and docs/.claude/context/tech-stack.md

Migration: [Description]
Type: [Database Schema/Data Migration/Platform Migration/Architecture]
Scope: [What's being migrated]
Risk Level: [Critical/High/Medium/Low]

Current state: [What exists now]
Target state: [What we want]

Please help me:
1. Analyze current and target state
2. Create migration strategy (MIGRATION-[ID].md)
3. Develop migration scripts
4. Plan testing and validation
5. Create rollback procedure
6. Execute migration with zero downtime (if required)
```

## 🤖 Available Agents

### Agent List
- **Product Owner** (`docs/.claude/_SYSTEM/agents/product-owner.md`) - Feature planning
- **Systems Architect** (`docs/.claude/_SYSTEM/agents/systems-architect.md`) - Architecture design
- **Backend Engineer** (`docs/.claude/_SYSTEM/agents/backend-engineer.md`) - Backend development
- **Frontend Developer** (`docs/.claude/_SYSTEM/agents/frontend-developer.md`) - UI development
- **Test Engineer** (`docs/.claude/_SYSTEM/agents/test-engineer.md`) - Test strategy
- **Code Reviewer** (`docs/.claude/_SYSTEM/agents/code-reviewer.md`) - Code quality review
- **Security Auditor** (`docs/.claude/_SYSTEM/agents/security-auditor.md`) - Security analysis
- **Performance Optimizer** (`docs/.claude/_SYSTEM/agents/performance-optimizer.md`) - Performance tuning
- **DevOps Engineer** (`docs/.claude/_SYSTEM/agents/devops-engineer.md`) - CI/CD & infrastructure
- **Data Engineer** (`docs/.claude/_SYSTEM/agents/data-engineer.md`) - Data pipelines
- **Documentation Specialist** (`docs/.claude/_SYSTEM/agents/documentation-specialist.md`) - Technical writing

### How to Delegate Tasks to Agents

**Use the Task tool to properly delegate work to specialized agents:**

```
Use the Task tool with this prompt:

Load docs/.claude/_SYSTEM/agents/[agent-name].md
Load docs/.claude/context/conventions.md

Activate as [Agent Name] agent.

Task: [Specific task description]
Type: [Task type specific to the agent]
[Additional agent-specific parameters]

Please complete this task following the agent's workflow and conventions.
```

**Example - Delegating to Backend Engineer:**
```
Task tool prompt:

Load docs/.claude/_SYSTEM/agents/backend-engineer.md
Load docs/.claude/context/conventions.md

Activate as Backend Developer agent.

Task: Create user authentication API with JWT
Type: REST API
Database: PostgreSQL
Authentication: JWT tokens
Scale: 50K concurrent users

Please implement following our conventions.
```

**Why delegate with Task tool?**
- ✅ Creates true specialized agent instance
- ✅ Agent works autonomously
- ✅ Better separation of concerns
- ✅ Agent reports complete results

**Complete guide:** `docs/.claude/_SYSTEM/agents-guide.md`

## 🔗 Essential Files

**Generated during initialization (do not load before running initialization):**
- **Full Context:** `docs/.claude/context/project-overview.md` - Comprehensive project context
- **Conventions:** `docs/.claude/context/conventions.md` - Coding standards and patterns
- **Tech Stack:** `docs/.claude/context/tech-stack.md` - Technology stack documentation
- **Decision Log:** `docs/.claude/context/decision-log.md` - Architectural decisions

**Optional (create as needed):**
- **Glossary:** `docs/.claude/context/glossary.md` - Project terminology and domain language

## 📚 Template Organization (v2.0)

**Templates are now organized by stack to reduce token waste:**

```
docs/.claude/_TEMPLATES/
├── _BASE/          # Universal templates (all projects)
├── _SHARED/        # Reusable components (git, testing, security)
├── python/         # Python-specific templates
├── django/         # Django framework templates
├── php/            # PHP-specific templates
├── laravel/        # Laravel framework templates
├── javascript/     # JavaScript/TypeScript templates
└── vue/            # Vue 3 ecosystem templates
```

**Loading patterns:**
- **Django:** Load `django/conventions.md`
- **Laravel:** Load `laravel/conventions.md`
- **Python:** Load `python/conventions.md`
- **JavaScript/Node:** Load `javascript/conventions.md`
- **Nuxt 3:** Load `vue/conventions-base.md` + `vue/conventions-nuxt.md`
- **Vue SPA:** Load `vue/conventions-base.md` + `vue/conventions-spa.md`
- **Vue PWA:** Load `vue/conventions-base.md` + `vue/conventions-pwa.md`

**Benefits:**
- 40-50% token reduction (no cross-stack pollution)
- Focused, relevant examples only
- Composition-based Vue templates (no duplication)

See `docs/.claude/_TEMPLATES/README.md` for complete details.

## 📝 Notes
- Update specs as implementation evolves
- Archive obsolete content immediately
- Document decisions in `docs/.claude/context/decision-log.md`

---
**Last Updated:** [Date]
**Maintained By:** [Name/Team]

---

## Directory Structure
```markdown
project-root/
├── CLAUDE.md                              # Master instructions (read first)
├── README.md
├── .gitignore
├── .env.example                           # Auto-generated during init
│
├── docs/
│   ├── .claude/                           # Claude workspace
│   │   ├── _SYSTEM/                       # System configuration
│   │   │   └── initialization-agent.md    # Automated project setup
│   │   ├── _TEMPLATES/                    # Reference templates
│   │   │   ├── project-overview.md        # Project context template
│   │   │   ├── conventions-python.md      # Python best practices
│   │   │   ├── conventions-django.md      # Django patterns
│   │   │   ├── conventions-laravel.md     # Laravel conventions
│   │   │   ├── conventions-javascript.md  # JS/TS standards
│   │   │   ├── conventions-php.md         # PHP standards
│   │   │   ├── conventions-vue-nuxt.md    # Nuxt + Vue 3 conventions
│   │   │   ├── conventions-vue-spa.md     # Vue SPA + Vite + Pinia conventions
│   │   │   ├── conventions-vue-pwa.md     # Vue PWA + Vite + Pinia conventions
│   │   │   ├── tech-stack.md              # Tech stack template
│   │   │   ├── decision-log.md            # Decision tracking
│   │   │   ├── feature-spec-detailed.md   # Feature specification
│   │   │   ├── glossary.md                # Project terminology
│   │   │   ├── task-management.md         # Task tracking
│   │   │   ├── agent-configs.md           # Agent configurations
│   │   │   ├── prompt-templates.md        # Reusable prompts
│   │   │   └── workflow-optimization-guide.md  # Best practices
│   │   ├── context/                       # Your project context
│   │   │   ├── project-overview.md        # Full project context
│   │   │   ├── conventions.md             # Coding standards
│   │   │   ├── tech-stack.md              # Technology choices
│   │   │   └── decision-log.md            # Architectural decisions
│   │   ├── features/                      # Feature specs & working docs
│   │   ├── bugs/                          # Bug tracking (BUG-[ID].md)
│   │   ├── tasks/                         # Task management
│   │   ├── agents/                        # Specialized agent configs
│   │   ├── prompts/                       # Reusable prompts
│   │   └── archive/                       # ⚠️ NEVER READ (obsolete)
│   │
│   ├── features/                          # Official documentation
│   ├── architecture/                      # Architecture docs
│   └── api/                               # API documentation
│
├── src/                                   # Source code
├── tests/                                 # Test files
└── ...                                    # Your project files
```

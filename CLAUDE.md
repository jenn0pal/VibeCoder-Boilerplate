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

**If you already have a Django/Laravel/Python/JavaScript project:**
```
Load docs/.claude/_SYSTEM/existing-project-integration.md
Integrate VibeCoder boilerplate with my existing [framework] project
```

**Examples:**
- "Integrate VibeCoder with my existing Django project"
- "Integrate VibeCoder with my existing Laravel project"
- "Integrate VibeCoder with my existing Python project"

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
docs/.claude/features/   - Feature specs & working docs
docs/.claude/context/    - Project context (READ FIRST)
docs/.claude/agents/     - Specialized agent configs
docs/.claude/archive/    - ⚠️ NEVER READ (obsolete)
docs/features/           - Official documentation
src/                     - Source code
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

## 🤖 Available Agents
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

## 🔗 Essential Files

**Generated during initialization (do not load before running initialization):**
- **Full Context:** `docs/.claude/context/project-overview.md` - Comprehensive project context
- **Conventions:** `docs/.claude/context/conventions.md` - Coding standards and patterns
- **Tech Stack:** `docs/.claude/context/tech-stack.md` - Technology stack documentation
- **Decision Log:** `docs/.claude/context/decision-log.md` - Architectural decisions

**Optional (create as needed):**
- **Glossary:** `docs/.claude/context/glossary.md` - Project terminology and domain language

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

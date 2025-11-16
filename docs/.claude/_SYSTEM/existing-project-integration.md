# ClaudeContext Existing Project Integration Agent

> **Purpose:** Integrate ClaudeContext boilerplate documentation system with existing Django, Laravel, Python, JavaScript, or PHP projects without disrupting existing structure.

## Activation Trigger

When user says:
- "Integrate with existing project"
- "Add ClaudeContext to my existing Django/Laravel/Python project"
- "Document my existing codebase"
- Or similar integration requests

## Your Role

You are an expert at analyzing existing codebases and generating comprehensive documentation. Your goal is to:
1. **Detect and analyze the existing project structure**
2. **Generate documentation FROM the actual codebase**
3. **Preserve all existing files and structure**
4. **Create ClaudeContext context files based on reality, not templates**
5. **Get user productive with Claude FAST (< 10 minutes)**

## Critical Rules

1. **NEVER create or modify existing source code files**
2. **NEVER create directories that already exist**
3. **NEVER overwrite existing configuration files** (.env, settings.py, etc.)
4. **ALWAYS analyze before generating**
5. **ALWAYS preserve existing project structure**

## Integration Workflow

### Step 1: Project Detection & Analysis

**First, detect what type of project this is:**

```bash
# Use Bash tool to detect project type
echo "=== Detecting Project Type ==="

# Check for Django
if [ -f "manage.py" ]; then
    echo "✓ Django project detected"
    python manage.py --version 2>/dev/null || echo "Django version unknown"
fi

# Check for Laravel
if [ -f "artisan" ]; then
    echo "✓ Laravel project detected"
    php artisan --version 2>/dev/null || echo "Laravel version unknown"
fi

# Check for Python project
if [ -f "pyproject.toml" ] || [ -f "setup.py" ] || [ -f "requirements.txt" ]; then
    echo "✓ Python project detected"
fi

# Check for Node.js/JavaScript project
if [ -f "package.json" ]; then
    echo "✓ Node.js/JavaScript project detected"
    cat package.json | grep '"name"' | head -1
fi

# Check for PHP project
if [ -f "composer.json" ]; then
    echo "✓ PHP project detected"
fi
```

**Based on detection, set PROJECT_TYPE:**
- Django → `PROJECT_TYPE=django`
- Laravel → `PROJECT_TYPE=laravel`
- Python (generic) → `PROJECT_TYPE=python`
- Node.js/Express → `PROJECT_TYPE=nodejs`
- PHP (generic) → `PROJECT_TYPE=php`

### Step 2: Scan Existing Structure

**Use Bash and Read tools to understand the codebase:**

#### For Django Projects:

```bash
# Scan Django structure
echo "=== Analyzing Django Project Structure ==="

# Find project root (directory with settings.py)
find . -name "settings.py" -type f 2>/dev/null | head -1

# Find all Django apps
find . -name "apps.py" -type f 2>/dev/null

# Check for apps directory
ls -la apps/ 2>/dev/null || echo "No apps/ directory"

# Find models
find . -name "models.py" -type f 2>/dev/null | head -10

# Find views
find . -name "views.py" -type f 2>/dev/null | head -10

# Check for tests
ls -la tests/ 2>/dev/null || echo "No tests/ directory"
find . -name "test_*.py" -type f 2>/dev/null | head -5

# Check for requirements
ls -la requirements.txt requirements/ pyproject.toml 2>/dev/null
```

**Then read key files:**

```bash
# Read settings.py to understand configuration
Read [path-to-settings.py]

# Read requirements.txt or pyproject.toml
Read requirements.txt  # or pyproject.toml
```

**Extract from settings.py:**
- INSTALLED_APPS (what apps are in the project)
- DATABASES (database configuration)
- MIDDLEWARE (what middleware is used)
- STATIC/MEDIA configuration
- Custom settings and configurations

#### For Laravel Projects:

```bash
# Scan Laravel structure
echo "=== Analyzing Laravel Project Structure ==="

# Check Laravel version
php artisan --version 2>/dev/null

# List apps (in app/ directory)
ls -la app/Models/ 2>/dev/null
ls -la app/Http/Controllers/ 2>/dev/null

# Check for routes
ls -la routes/ 2>/dev/null

# Check for migrations
ls -la database/migrations/ 2>/dev/null

# Check for tests
ls -la tests/Feature/ tests/Unit/ 2>/dev/null

# Check for dependencies
cat composer.json 2>/dev/null
```

**Then read key files:**

```bash
Read config/app.php
Read composer.json
Read .env.example  # If it exists, to understand environment variables
```

#### For Python (Generic) Projects:

```bash
# Scan Python project structure
echo "=== Analyzing Python Project Structure ==="

# Find package directories
find . -name "__init__.py" -type f 2>/dev/null | head -10

# Find main source directory
ls -la src/ 2>/dev/null || ls -la [project_name]/ 2>/dev/null

# Check for tests
ls -la tests/ 2>/dev/null

# Check for dependencies
ls -la requirements.txt pyproject.toml setup.py 2>/dev/null
```

**Then read key files:**

```bash
Read pyproject.toml  # or requirements.txt or setup.py
Read README.md  # To understand project purpose
```

#### For Node.js/JavaScript Projects:

```bash
# Scan Node.js project structure
echo "=== Analyzing Node.js Project Structure ==="

# Check for source directory
ls -la src/ 2>/dev/null

# Check for routes/controllers
find src -name "*.routes.js" -o -name "*Controller.js" 2>/dev/null | head -10

# Check for tests
ls -la tests/ __tests__/ 2>/dev/null

# Check for dependencies
cat package.json
```

**Then read key files:**

```bash
Read package.json
Read README.md
Read src/index.js  # or src/app.js or main entry point
```

### Step 3: Interactive Context Gathering

**Ask user ONE focused question to fill in gaps:**

```
I've analyzed your [PROJECT_TYPE] project and found:

**Detected Structure:**
- [List key findings: apps, models, controllers, etc.]
- [List detected dependencies]
- [List detected patterns]

**To complete the documentation, tell me:**

**Purpose:** [What does this project do? One sentence]
**Current Stage:** [Planning/Development/MVP/Beta/Production]
**Team:** [Solo/2-5 people/6+]
**Key Features:** [What are the main features? 3-5 items]

Example: "Task management API for remote teams - Production - 3 developers - Tasks, Projects, Teams, Notifications, API"
```

**Parse user's response** and extract missing information.

### Step 4: Generate Context Files from Analysis

**Now generate documentation based on ACTUAL codebase, not templates.**

#### 4.1: Generate `docs/.claude/context/project-overview.md`

**Use Write tool with content based on actual analysis:**

```markdown
# [Project Name] - Project Overview

> **Generated from existing codebase analysis on [DATE]**

## Executive Summary

[User's purpose + detected architecture type]

This [PROJECT_TYPE] project is currently in [STAGE] stage with [TEAM SIZE] team.

## Business Context

- **Problem Statement:** [Inferred from user's purpose]
- **Target Users:** [Inferred from purpose and features]
- **Key Value Proposition:** [From user's description]
- **Current Status:** [From user's stage input]

## Technical Architecture

### Architecture Overview
- **Type:** [Detected: API/Web App/CLI/Microservice]
- **Framework:** [Detected from analysis: Django 5.x / Laravel 11.x / Express / etc.]
- **Language:** [Detected: Python 3.x / PHP 8.x / JavaScript/TypeScript]
- **Database:** [Extracted from settings.py or config]
- **Architecture Pattern:** [Detected: Monolith/Microservices/etc.]

### Project Structure
```
[Copy actual directory structure found in Step 2]
```

## Existing Applications/Modules

[List all detected apps/modules from Step 2 analysis]

**Django Apps:** [If Django]
- `[app_name]` - [Infer purpose from models found]
- ...

**Laravel Modules:** [If Laravel]
- `[module_name]` - [Infer purpose from controllers]
- ...

**Python Packages:** [If Python]
- `[package_name]` - [Infer purpose]
- ...

## Core Functionality

[Based on user's "Key Features" response + detected models/controllers]

1. **[Feature 1]** - [Detected implementation]
2. **[Feature 2]** - [Detected implementation]
3. **[Feature 3]** - [Detected implementation]

## Technology Stack

### Backend
- **Framework:** [Detected framework + version]
- **Database:** [From settings/config]
- **ORM:** [Django ORM / Eloquent / Sequelize / etc.]
- **API:** [REST / GraphQL - detected from routes]

### Dependencies
[Parse from requirements.txt / composer.json / package.json]

**Key Libraries:**
- [List major dependencies found]

### Development Tools
[Detected from files present]
- **Testing:** [pytest / PHPUnit / Jest - if tests found]
- **Linting:** [If config files found: .ruff.toml, .eslintrc, etc.]

## Current Development Status

- **Phase:** [User's input]
- **Latest Version:** [From package.json / __version__ / etc. if found]
- **Active Development:** [Inferred from git commits if accessible]

## Team Structure

- **Size:** [User's input]
- **Code Review:** [Recommended based on team size]

## Quality Standards

### Testing
- **Test Framework:** [Detected from tests/ directory]
- **Test Coverage:** [To be measured]
- **Existing Tests:** [Count of test files found]

### Code Quality
- **Linting:** [Detected or "To be configured"]
- **Type Checking:** [Detected or "To be configured"]

## Quick Context for Claude

When working on this project:
1. **Existing Structure:** This is an EXISTING project - preserve all current structure
2. **Main Framework:** [Framework] - follow existing patterns in the codebase
3. **Key Apps/Modules:** [List from analysis]
4. **Testing:** Tests are located in [detected location]
5. **Configuration:** [Location of main config file]
6. **Conventions:** Follow patterns established in `docs/.claude/context/conventions.md`

## Important Files

- **Main Config:** [settings.py / config/app.php / etc.]
- **Dependencies:** [requirements.txt / composer.json / package.json]
- **Entry Point:** [manage.py / artisan / index.js / etc.]
- **Routes:** [urls.py / routes/ / app.js]

---
*Auto-generated from existing codebase | Last analyzed: [DATE]*
*Project type: [PROJECT_TYPE] | Framework: [Framework Version]*
```

#### 4.2: Generate `docs/.claude/context/conventions.md`

**Two approaches:**

**Approach A: Copy framework template (faster)**

```bash
# Read the appropriate template
Read docs/.claude/_TEMPLATES/conventions-[framework].md

# Write to context directory
Write docs/.claude/context/conventions.md
[Content from template]
```

**Approach B: Analyze existing code patterns (more accurate)**

Scan existing code to detect actual conventions:

```bash
# For Python/Django projects
# Check imports style
grep -r "^import " --include="*.py" . | head -20

# Check class naming
grep -r "^class " --include="*.py" . | head -20

# Check function naming
grep -r "^def " --include="*.py" . | head -20

# Check for type hints usage
grep -r ": str" --include="*.py" . | wc -l
grep -r "-> " --include="*.py" . | wc -l
```

Then generate conventions.md that documents ACTUAL patterns:

```markdown
# [Project Name] - Coding Conventions

> **Based on analysis of existing codebase patterns**

## Existing Patterns Detected

### Code Style
- **Import Style:** [Detected pattern]
- **Naming Convention:** [Detected: snake_case / camelCase / etc.]
- **Type Hints:** [Used: Yes/No - based on scan]
- **Docstrings:** [Used: Yes/No - based on scan]

### Project Structure
[Document actual structure found]

## Recommended Conventions Going Forward

[Include relevant framework conventions from template]

### Django/Laravel/Python/JavaScript Best Practices
[Copy from appropriate template file]

---
*Note: This combines existing code patterns with [Framework] best practices*
*Follow existing patterns for consistency; gradually adopt best practices for new code*
```

**Use Approach A for speed, Approach B for accuracy.**

#### 4.3: Generate `docs/.claude/context/tech-stack.md`

**Use Write tool with content from actual analysis:**

```markdown
# [Project Name] - Technology Stack

> **Detected from existing project on [DATE]**

## Core Technologies

### Backend
- **Language:** [Detected: Python 3.x / PHP 8.x / JavaScript/TypeScript]
- **Framework:** [Detected: Django 5.x / Laravel 11.x / Express 4.x]
- **Version:** [From --version commands or package files]

### Database
- **Primary Database:** [Extracted from settings/config]
- **ORM/Query Builder:** [Django ORM / Eloquent / Sequelize]

### Frontend [If detected]
- **Framework:** [Detected from package.json or templates]
- **Build Tool:** [Detected: Vite / Webpack / Mix]
- **Styling:** [Detected from files: Tailwind / Bootstrap / CSS]

## Dependencies

### Installed Packages

[Parse and list from requirements.txt / composer.json / package.json]

**Backend Dependencies:**
```
[List key dependencies with versions]
```

**Frontend Dependencies:** [If applicable]
```
[List from package.json]
```

## Development Tools

### Package Management
- **Tool:** [Detected: pip / uv / composer / npm / pnpm]
- **Lock File:** [requirements.txt / composer.lock / package-lock.json]

### Code Quality
- **Linting:** [Detected from config files or "Not configured"]
- **Formatting:** [Detected or "Not configured"]
- **Type Checking:** [Detected or "Not configured"]

### Testing
- **Framework:** [Detected: pytest / PHPUnit / Jest]
- **Test Location:** [Detected path]
- **Coverage Tool:** [If detected]

### Infrastructure
- **Containerization:** [Docker if Dockerfile found, else "Not configured"]
- **CI/CD:** [GitHub Actions / GitLab CI if config found, else "Not configured"]
- **Deployment:** [From analysis or "TBD"]

## Development Workflow

### Local Setup
```bash
[Generate setup commands based on project type and detected tools]

# Example for Django with uv:
# uv venv
# source .venv/bin/activate
# uv pip install -r requirements.txt
# python manage.py migrate
# python manage.py runserver
```

### Running Tests
```bash
[Generate test commands based on detected test framework]
```

### Database Migrations
```bash
[Framework-specific migration commands]
```

## Configuration Files

- **Environment:** [.env location or variables needed]
- **Framework Config:** [settings.py / config/ / etc.]
- **Dependencies:** [requirements.txt / composer.json / package.json]

---
*Auto-detected from existing project structure*
*Last analyzed: [DATE]*
```

#### 4.4: Generate `docs/.claude/context/decision-log.md`

**Create with initial entry documenting the integration:**

```markdown
# [Project Name] - Architectural Decision Log

> Document significant technical decisions with context and rationale.

## [DATE] - ClaudeContext Documentation Integration

### Context
Integrated ClaudeContext boilerplate documentation system with existing [PROJECT_TYPE] project to improve Claude AI collaboration.

### Decision
Added ClaudeContext documentation structure while preserving all existing project files and architecture.

### Current State Analysis
- **Framework:** [Framework + Version]
- **Project Stage:** [Stage]
- **Team Size:** [Size]
- **Key Technologies:** [List from tech-stack.md]

### Documentation Added
- Project overview with architecture analysis
- Coding conventions based on existing patterns
- Technology stack documentation
- This decision log

### Consequences
- **Positive:** Better context for Claude AI sessions, reduced hallucinations, clearer conventions
- **Positive:** Preserved all existing code and structure
- **Neutral:** Team needs to maintain documentation alongside code
- **Neutral:** New team members should read docs/.claude/context/ files

### Status
Accepted ✅

---

## Existing Technology Decisions (Retroactive Documentation)

### [DATE] - Initial Technology Stack Selection

### Context
[Inferred from analysis] Project started with [Framework] to build [Purpose].

### Key Decisions Made
- **Framework:** [Framework]
- **Database:** [Database from settings]
- **ORM:** [ORM used]
- **Testing:** [Test framework if detected]

### Rationale (Inferred)
- **[Framework]:** [Standard reasoning for why this framework fits the use case]
- **[Database]:** [Standard reasoning based on framework and use case]

### Status
Accepted ✅ (Existing implementation)

---

## Decision Template

Use this template for future technical decisions:

```markdown
## [Date] - [Decision Title]

### Context
[What's the situation and why do we need to decide?]

### Decision
[What are we going to do?]

### Rationale
[Why this choice? What alternatives did we consider?]

### Consequences
- **Positive:** [Benefits]
- **Negative:** [Trade-offs]
- **Mitigations:** [How we handle negatives]

### Status
[Proposed / Accepted / Superseded]
```

---
*Document all significant technical decisions going forward*
*This helps future developers understand why choices were made*
```

#### 4.5: Update `CLAUDE.md`

**Use Edit tool to update the Project Overview section:**

```bash
# Edit 1: Update Project Name
Edit CLAUDE.md:
  old_string: "# Working with Claude on [Project Name]"
  new_string: "# Working with Claude on [Actual Project Name]"

# Edit 2: Update Purpose
Edit CLAUDE.md:
  old_string: "- **Purpose:** [One sentence]"
  new_string: "- **Purpose:** [User's actual purpose]"

# Edit 3: Update Stage
Edit CLAUDE.md:
  old_string: "- **Stage:** [MVP/Beta/Production]"
  new_string: "- **Stage:** [User's actual stage]"

# Edit 4: Update Tech Stack
Edit CLAUDE.md:
  old_string: "- **Tech Stack:** [Key technologies]"
  new_string: "- **Tech Stack:** [Framework + Database + Key tools]"

# Edit 5: Update Team
Edit CLAUDE.md:
  old_string: "- **Team:** [Size and structure]"
  new_string: "- **Team:** [User's actual team info]"
```

**IMPORTANT:** Only update the Project Overview section. Leave all other sections unchanged.

#### 4.6: Create Feature Spec for Documentation Maintenance

**Create directory first:**

```bash
mkdir -p docs/.claude/features/documentation-maintenance
```

**Then create spec file:**

Write `docs/.claude/features/documentation-maintenance/spec.md`:

```markdown
# Feature: Documentation Maintenance

## Overview
Keep ClaudeContext documentation synchronized with the evolving [Project Name] codebase.

## Objectives
- ✅ Initial documentation generated from existing codebase
- ⬜ Documentation update process established
- ⬜ Team trained on documentation workflow
- ⬜ Regular documentation reviews scheduled

## Tasks

1. **Initial Setup** ✅
   - [x] Analyzed existing codebase structure
   - [x] Generated project-overview.md from actual code
   - [x] Created conventions.md based on existing patterns
   - [x] Documented tech stack from dependencies
   - [x] Updated CLAUDE.md with project information

2. **Ongoing Maintenance**
   - [ ] Update project-overview.md when architecture changes
   - [ ] Update tech-stack.md when dependencies change
   - [ ] Document new decisions in decision-log.md
   - [ ] Update conventions.md if patterns evolve
   - [ ] Archive obsolete documentation

3. **Team Workflow**
   - [ ] Share ClaudeContext workflow with team
   - [ ] Establish documentation review cadence
   - [ ] Create process for updating docs with code changes

## Documentation Update Triggers

Update documentation when:
- Adding new Django apps/Laravel modules
- Changing database or major dependencies
- Adopting new coding patterns or tools
- Making architectural decisions
- Reaching new project milestones

## Success Criteria

- [x] Initial documentation complete and accurate
- [ ] Team understands how to use documentation with Claude
- [ ] Documentation stays synchronized with code
- [ ] Claude sessions are more productive with accurate context

---
*Status: In Progress*
*Created: [DATE] during ClaudeContext integration*
```

### Step 5: Validation & Verification

**Verify all files were created successfully:**

```bash
echo "=== Validation: Checking Created Files ==="

# Check context files
echo "Context files:"
ls -lh docs/.claude/context/

# Verify each file has content (not empty)
echo ""
echo "Verifying file contents:"
wc -l docs/.claude/context/project-overview.md
wc -l docs/.claude/context/conventions.md
wc -l docs/.claude/context/tech-stack.md
wc -l docs/.claude/context/decision-log.md

# Check CLAUDE.md was updated
echo ""
echo "CLAUDE.md updates:"
grep "Purpose:" CLAUDE.md
grep "Stage:" CLAUDE.md
grep "Tech Stack:" CLAUDE.md

# Check feature spec
echo ""
echo "Feature spec:"
ls -lh docs/.claude/features/documentation-maintenance/

# Verify NO new source directories were created
echo ""
echo "Existing project structure preserved:"
ls -la | grep -E "^d" | grep -v "^drwx.*\s\.$" | grep -v "^drwx.*\s\.\.$"
```

**Expected validation results:**
- ✅ All 4 context files exist and have substantial content (>50 lines each)
- ✅ CLAUDE.md shows actual project information (not placeholders)
- ✅ Feature spec created
- ✅ NO new source directories created (apps/, src/, etc.)
- ✅ NO existing files overwritten (.env, settings.py, etc.)

**If validation fails:**

| Missing/Issue | Recovery Action |
|---------------|-----------------|
| Context file missing | Re-run Step 4 for that specific file |
| Context file empty | Re-analyze (Step 2) and regenerate (Step 4) |
| CLAUDE.md has placeholders | Re-run Step 4.5 Edit operations |
| Feature spec missing | `mkdir -p docs/.claude/features/documentation-maintenance` then create spec |
| New directories created | **ERROR** - This shouldn't happen. Remove created directories, verify Step 2 detection |
| Existing files overwritten | **CRITICAL** - Restore from git/backup if available |

### Step 6: Present Integration Summary

**Show user what was accomplished:**

```markdown
✅ **ClaudeContext Documentation Integration Complete!**

## Project Detected
- **Type:** [Django / Laravel / Python / etc.]
- **Framework:** [Version]
- **Structure:** [apps/ or src/ or app/ - existing structure preserved]

## Files Created

### Documentation (NEW)
- `docs/.claude/context/project-overview.md` - Analyzed from your existing codebase
- `docs/.claude/context/conventions.md` - Based on detected code patterns
- `docs/.claude/context/tech-stack.md` - Extracted from dependencies
- `docs/.claude/context/decision-log.md` - Documents integration + existing decisions
- `docs/.claude/features/documentation-maintenance/spec.md` - Maintenance workflow

### Updated
- `CLAUDE.md` - Updated with your project information

### Preserved (UNCHANGED)
- ✅ All existing source code
- ✅ All existing configuration files
- ✅ All existing project structure
- ✅ All existing dependencies

## Analysis Summary

**Apps/Modules Found:**
[List detected apps/modules]

**Key Dependencies:**
[List major dependencies]

**Existing Tests:**
[Test files found or "No tests detected"]

**Configuration:**
- Main config: [settings.py location or equivalent]
- Environment: [.env status]
- Database: [Detected database]

## Next Steps

### 1. Review Generated Documentation
```bash
# Read what was generated about your project
cat docs/.claude/context/project-overview.md
cat docs/.claude/context/tech-stack.md
```

**Action:** Review for accuracy and update any incorrect inferences.

### 2. Start Using ClaudeContext with Claude

**Standard development session:**
```
Load CLAUDE.md
Load docs/.claude/context/project-overview.md
Working on: [describe your task]
```

**What you get:**
- ✅ Claude understands your existing architecture
- ✅ Claude follows your existing patterns
- ✅ Reduced hallucinations (knows what's already there)
- ✅ Better code suggestions (understands context)

### 3. Maintain Documentation

When you make significant changes:
- Add new apps/modules → Update project-overview.md
- Change dependencies → Update tech-stack.md
- Make architectural decisions → Add to decision-log.md
- Change coding patterns → Update conventions.md

## Recommended: Share with Team

If you have a team, share the workflow:

```
Team: Read CLAUDE.md for instructions
Important files: docs/.claude/context/
When coding: Load CLAUDE.md + project-overview.md in every Claude session
```

## Quick Reference

**Starting a Claude session:**
```
Load CLAUDE.md
Load docs/.claude/context/project-overview.md
[Your task/question]
```

**Code review:**
```
Load CLAUDE.md and conventions.md
Review: [files]
Focus: [security/performance/standards]
```

**New feature:**
```
Load CLAUDE.md and project-overview.md
Starting feature: [name]
Create feature spec
```

---

**🎉 You're all set!** Your existing project now has comprehensive Claude-optimized documentation.

**Try it now:** Start a new Claude session and load CLAUDE.md to see the difference!
```

## Integration Best Practices

### DO ✅
- Analyze codebase before generating any documentation
- Preserve ALL existing files and structure
- Generate documentation from actual code, not assumptions
- Use detected patterns for conventions
- Keep documentation synchronized with code changes

### DON'T ❌
- Create new source directories that might conflict
- Overwrite existing configuration files
- Make assumptions about architecture without analysis
- Create generic documentation - make it specific to the actual codebase
- Skip validation steps

## Error Handling

### If Analysis Fails

**Problem:** Can't detect project type

**Solution:**
```
Ask user directly:
"I couldn't automatically detect your project type. Is this a:
- Django project
- Laravel project
- Express/Node.js project
- Generic Python project
- Generic PHP project
- Other (please specify framework)"
```

**Problem:** Can't find key files (settings.py, package.json, etc.)

**Solution:**
```
Ask user:
"Where is your main configuration file?
- Django: settings.py location
- Laravel: config/app.php location
- Node: package.json location
- Other: [specify]"
```

### If File Creation Fails

**Problem:** Parent directory doesn't exist

**Solution:** Create directory first with `mkdir -p`, then create file

**Problem:** File already exists

**Solution:**
```
For context files: Ask before overwriting
"docs/.claude/context/project-overview.md already exists.
This might be from a previous integration attempt.
Overwrite with fresh analysis? (yes/no)"
```

## Workflow Comparison

### New Project (initialization-agent.md)
1. Ask user about project vision
2. Generate structure from templates
3. Create new directories
4. Create .env.example
5. Set up blank project

### Existing Project (existing-project-integration.md)
1. Detect and analyze existing code
2. Generate documentation from reality
3. Preserve all existing structure
4. Skip .env.example (already exists)
5. Document what's already built

---

**Remember:** This is INTEGRATION, not initialization. Preserve, don't create!
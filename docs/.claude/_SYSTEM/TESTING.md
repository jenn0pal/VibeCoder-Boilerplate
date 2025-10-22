# VibeCoder Boilerplate - Test Scenarios & Validation

> **Purpose:** Comprehensive test scenarios to validate both new and existing project workflows before release.

## Test Categories

1. **New Project Workflow Tests** - Validates initialization-agent.md
2. **Existing Project Workflow Tests** - Validates existing-project-integration.md
3. **Cross-Workflow Tests** - Validates common functionality
4. **Edge Case Tests** - Validates error handling and unusual scenarios

---

## Test Scenario 1: New Django Project (Happy Path)

### Setup
- Fresh clone of VibeCoder boilerplate
- No existing project files
- User wants to create a new Django project

### Steps
1. User clones boilerplate
2. User runs: `Initialize Django project: TaskHub`
3. Claude asks ONE question about project
4. User responds: "TaskHub - Task management for remote teams - Django + React - MVP - Solo"
5. Claude generates all files
6. User runs verification commands

### Expected Results
✅ Files created:
- `docs/.claude/context/project-overview.md` (populated with TaskHub info)
- `docs/.claude/context/conventions.md` (Django conventions)
- `docs/.claude/context/tech-stack.md` (Django stack)
- `docs/.claude/context/decision-log.md` (initial decisions)
- `.env.example` (Django-specific variables)
- `docs/.claude/features/project-setup/spec.md`

✅ Directories created:
- `apps/users`, `apps/core`, `apps/api`
- `tests/unit`, `tests/integration`, `tests/fixtures`
- `scripts`, `static`, `media`, `logs`

✅ CLAUDE.md updated:
- Purpose: "Task management for remote teams"
- Stage: "MVP"
- Tech Stack: "Django, PostgreSQL, React"
- Team: "Solo"

✅ Validation passes:
- `ls docs/.claude/context/` shows 4 files
- `grep "Purpose:" CLAUDE.md` shows actual purpose (not placeholder)
- `ls apps/` shows users, core, api
- `ls tests/` shows unit, integration, fixtures

### Potential Gaps to Check
- [ ] Does initialization-agent.md read templates before generating?
- [ ] Does it create directories in correct order?
- [ ] Does it handle missing parent directories?
- [ ] Does validation catch missing files?

---

## Test Scenario 2: New Laravel Project (Happy Path)

### Setup
- Fresh clone of VibeCoder boilerplate
- No existing project files
- User wants to create a new Laravel project

### Steps
1. User clones boilerplate
2. User runs: `Initialize Laravel project: ShopAPI`
3. Claude asks about project
4. User responds: "ShopAPI - E-commerce API - Laravel 11 - MVP - Team of 3"
5. Claude generates all files
6. User runs verification

### Expected Results
✅ Files created with Laravel-specific content:
- `docs/.claude/context/conventions.md` (Laravel conventions, not Django)
- `.env.example` (Laravel variables: APP_NAME, DB_CONNECTION=mysql, etc.)

✅ Directories created (Laravel-specific):
- `tests/Feature`, `tests/Unit`
- `storage/logs`
- `resources/views/components`

✅ CLAUDE.md updated with Laravel info

### Potential Gaps to Check
- [ ] Does agent correctly detect "Laravel" from user input?
- [ ] Does it use Laravel template, not Django template?
- [ ] Does .env.example have correct Laravel variables?
- [ ] Does it create Laravel directory structure, not Django structure?

---

## Test Scenario 3: Existing Django Project (Happy Path)

### Setup
Simulated existing Django project:
```
myproject/
├── manage.py
├── myproject/
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
├── apps/
│   ├── users/
│   │   ├── models.py
│   │   ├── views.py
│   │   └── apps.py
│   ├── tasks/
│   └── api/
├── tests/
│   └── test_users.py
├── requirements.txt (contains: Django==5.0, psycopg2, djangorestframework)
└── .env
```

### Steps
1. User copies VibeCoder docs/ and CLAUDE.md to existing project
2. User runs: `Integrate VibeCoder with my existing Django project`
3. Claude detects Django project (finds manage.py)
4. Claude scans structure (finds apps/, tests/, etc.)
5. Claude reads settings.py and requirements.txt
6. Claude asks about project purpose
7. User responds: "Task management system - Production - 3 developers"
8. Claude generates documentation from actual code
9. User runs verification

### Expected Results
✅ Files created (documentation only):
- `docs/.claude/context/project-overview.md` (mentions existing apps: users, tasks, api)
- `docs/.claude/context/conventions.md` (Django conventions)
- `docs/.claude/context/tech-stack.md` (lists Django==5.0, psycopg2, djangorestframework from requirements.txt)
- `docs/.claude/context/decision-log.md` (documents integration + existing stack)

✅ CLAUDE.md updated with actual project info

✅ **NOTHING else changed:**
- ❌ NO new `apps/` directory created
- ❌ NO `.env.example` created (user already has .env)
- ❌ NO changes to manage.py, settings.py, models.py, etc.
- ❌ NO new test directories

✅ Validation passes:
- `git status` shows ONLY new files in `docs/.claude/` and modified `CLAUDE.md`
- `ls apps/` shows ONLY existing apps (users, tasks, api) - NO new apps/users, apps/core
- project-overview.md mentions "users", "tasks", "api" apps
- tech-stack.md lists Django==5.0, psycopg2, djangorestframework

### Potential Gaps to Check
- [ ] Does agent detect manage.py before doing anything?
- [ ] Does it analyze apps/ directory correctly?
- [ ] Does it read requirements.txt and extract dependencies?
- [ ] Does it read settings.py to find database config?
- [ ] Does it SKIP creating .env.example (since .env exists)?
- [ ] Does it SKIP creating new directories (apps/, tests/)?
- [ ] Does validation detect if new source directories were incorrectly created?

---

## Test Scenario 4: Existing Laravel Project (Happy Path)

### Setup
Simulated existing Laravel project:
```
shopapi/
├── artisan
├── app/
│   ├── Models/
│   │   ├── User.php
│   │   ├── Product.php
│   │   └── Order.php
│   └── Http/
│       └── Controllers/
│           ├── ProductController.php
│           └── OrderController.php
├── config/
│   └── app.php
├── routes/
│   └── api.php
├── tests/
│   ├── Feature/
│   └── Unit/
├── composer.json (contains: laravel/framework 11.x, mysql, redis)
└── .env
```

### Steps
1. User copies VibeCoder to existing Laravel project
2. User runs: `Integrate VibeCoder with my existing Laravel project`
3. Claude detects Laravel (finds artisan)
4. Claude scans Models (User, Product, Order) and Controllers
5. Claude reads composer.json
6. Claude asks about project
7. User responds: "E-commerce API - Beta - 5 developers"
8. Claude generates docs from actual code

### Expected Results
✅ Documentation created with Laravel-specific analysis:
- project-overview.md mentions Models: User, Product, Order
- project-overview.md mentions Controllers: ProductController, OrderController
- tech-stack.md lists Laravel 11.x, MySQL, Redis from composer.json
- conventions.md uses Laravel template (not Django)

✅ **NOTHING in source code changed:**
- ❌ NO changes to Models, Controllers, routes
- ❌ NO new .env.example (user has .env)

✅ Validation:
- `git status` shows ONLY docs/.claude/ and CLAUDE.md changes

### Potential Gaps to Check
- [ ] Does agent detect artisan (not manage.py)?
- [ ] Does it scan app/Models/ correctly?
- [ ] Does it scan app/Http/Controllers/?
- [ ] Does it read composer.json (not requirements.txt)?
- [ ] Does it use Laravel conventions template?

---

## Test Scenario 5: Edge Case - User Runs Wrong Agent

### Setup
- User has existing Django project
- User accidentally runs NEW project initialization

### Steps
1. User has existing project with manage.py
2. User mistakenly runs: `Initialize Django project: MyApp`
3. What happens?

### Expected Behavior (After Fix)
❌ **SHOULD NOT PROCEED**

Agent should:
1. Detect manage.py exists
2. Stop immediately
3. Show error message:
   ```
   ⚠️ STOP! Existing Django project detected.

   I found: manage.py, apps/, tests/

   You should use the EXISTING project integration workflow instead:

   Load docs/.claude/_SYSTEM/existing-project-integration.md
   Integrate VibeCoder with my existing Django project
   ```

### Current Behavior (Before Fix)
⚠️ **MIGHT CREATE CONFLICTS**
- Agent might create NEW apps/ directories
- Agent might create conflicting .env.example
- Mixed structure results

### Gap to Fix
- [ ] Add Step 0 to initialization-agent.md: Detect existing project markers
- [ ] If manage.py/artisan found, abort and redirect to existing-project-integration.md

---

## Test Scenario 6: Edge Case - Missing Dependencies

### Setup
- Existing Django project
- NO requirements.txt or pyproject.toml

### Steps
1. User runs existing project integration
2. Agent tries to read requirements.txt
3. File doesn't exist

### Expected Behavior
✅ Agent should:
1. Detect missing requirements file
2. Ask user: "I couldn't find requirements.txt or pyproject.toml. What dependencies does your project use?"
3. Generate tech-stack.md based on user's response
4. Note in tech-stack.md: "Dependencies not found in requirements file - documented based on user input"

### Potential Gaps to Check
- [ ] Does agent handle missing requirements.txt gracefully?
- [ ] Does it ask user for missing information?
- [ ] Does it document the limitation?

---

## Test Scenario 7: Edge Case - Can't Detect Project Type

### Setup
- Existing Python project
- NO manage.py, NO artisan, NO package.json
- Just Python files in src/

### Steps
1. User runs: `Integrate VibeCoder with my existing Python project`
2. Agent scans for project markers
3. Finds no framework-specific files

### Expected Behavior
✅ Agent should:
1. Detect generic Python project
2. Ask user: "I detected a Python project. Is this a: Django / Flask / FastAPI / Generic Python CLI / Other?"
3. Proceed based on user's response
4. Use generic Python conventions if no framework specified

### Potential Gaps to Check
- [ ] Does agent handle generic Python projects?
- [ ] Does it ask for clarification when framework unclear?
- [ ] Does it fall back to generic conventions appropriately?

---

## Test Scenario 8: Cross-Workflow - Documentation Updates

### Setup
- Project initialized (new or existing)
- User adds a new Django app

### Steps
1. User creates new app: `python manage.py startapp notifications`
2. User tells Claude: "I added a new app called notifications"
3. Claude should update project-overview.md

### Expected Behavior
✅ Claude should:
1. Read current project-overview.md
2. Find "Existing Applications/Modules" section
3. Add new entry: `- notifications - [Infer purpose from name or ask user]`
4. Update CLAUDE.md if needed

### Potential Gaps to Check
- [ ] Is there clear guidance on updating docs?
- [ ] Do context files have clear sections for apps/modules?
- [ ] Can Claude easily locate where to add information?

---

## Test Scenario 9: Validation Failure - Missing File

### Setup
- New project initialization
- One of the Write operations fails
- project-overview.md not created

### Steps
1. User runs initialization
2. Some error causes project-overview.md to fail
3. Validation runs

### Expected Behavior
✅ Validation should:
1. Detect missing file
2. Show specific error:
   ```
   ❌ Validation Failed
   Missing: docs/.claude/context/project-overview.md

   Recovery: Re-run Step 4.1 from initialization-agent.md
   ```
3. Provide recovery action from troubleshooting table

### Potential Gaps to Check
- [ ] Does validation check for all required files?
- [ ] Does it provide specific recovery actions?
- [ ] Can user easily fix the issue?

---

## Test Scenario 10: Validation Failure - CLAUDE.md Not Updated

### Setup
- New project initialization
- Edit operations on CLAUDE.md fail
- Still has placeholders

### Steps
1. User runs initialization
2. Edit operations fail
3. Validation runs: `grep "Purpose:" CLAUDE.md`

### Expected Behavior
✅ Validation should:
1. Detect placeholder text: "[One sentence]"
2. Show error:
   ```
   ❌ CLAUDE.md still has placeholders
   Found: "Purpose: [One sentence]"
   Expected: Actual project purpose

   Recovery: Re-run Step 4.5 Edit operations
   ```

### Potential Gaps to Check
- [ ] Does validation check CLAUDE.md content (not just existence)?
- [ ] Does it detect placeholder patterns?
- [ ] Does it provide recovery steps?

---

## Simulation Checklist

### For New Project Workflow (initialization-agent.md)

**Prerequisites:**
- [ ] Templates exist in docs/.claude/_TEMPLATES/
- [ ] All convention files exist (django, laravel, python, js, php)

**Step 1: Quick Assessment**
- [ ] Agent asks single question
- [ ] Question format is clear
- [ ] Examples provided

**Step 2: Intelligent Parsing**
- [ ] Agent extracts project name
- [ ] Agent extracts purpose
- [ ] Agent detects framework correctly
- [ ] Agent uses smart defaults for missing info

**Step 3: Read Required Templates**
- [ ] Agent reads project-overview.md template
- [ ] Agent reads tech-stack.md template
- [ ] Agent reads decision-log.md template
- [ ] Agent reads correct conventions template for framework

**Step 4: Generate Core Documentation**
- [ ] 4.1: project-overview.md created with populated content (not placeholders)
- [ ] 4.2: conventions.md created (correct framework)
- [ ] 4.3: tech-stack.md created with framework-specific stack
- [ ] 4.4: decision-log.md created with initial decisions
- [ ] 4.5: CLAUDE.md updated (no placeholders remain)
- [ ] 4.6: .env.example created (framework-specific variables)

**Step 5: Create Initial Project Structure**
- [ ] Correct directories created for framework
- [ ] Django: apps/, tests/, scripts/
- [ ] Laravel: tests/Feature, tests/Unit, storage/logs
- [ ] Python: src/, tests/
- [ ] JavaScript: src/, tests/, dist/

**Step 6: Generate Initial Feature Spec**
- [ ] Directory created first: `mkdir -p docs/.claude/features/project-setup`
- [ ] Spec file created after directory exists
- [ ] No "parent directory doesn't exist" error

**Step 7: Validation & Verification**
- [ ] All context files verified to exist
- [ ] CLAUDE.md checked for actual content (not placeholders)
- [ ] Project structure verified
- [ ] Validation script catches missing files
- [ ] Recovery actions provided for failures

**Step 8: Agent Delegation** (Optional)
- [ ] Suggestions provided for next steps
- [ ] Agent activation examples given

**Step 9: Present Completion Summary**
- [ ] Clear success message
- [ ] Files created listed
- [ ] Next steps provided
- [ ] Commands for getting started

---

### For Existing Project Workflow (existing-project-integration.md)

**Prerequisites:**
- [ ] Existing project has clear markers (manage.py, artisan, package.json, etc.)
- [ ] Existing project has dependencies file (requirements.txt, composer.json, package.json)

**Step 1: Project Detection & Analysis**
- [ ] Agent checks for Django (manage.py)
- [ ] Agent checks for Laravel (artisan)
- [ ] Agent checks for Python (pyproject.toml, setup.py, requirements.txt)
- [ ] Agent checks for Node.js (package.json)
- [ ] Agent checks for PHP (composer.json)
- [ ] Correct PROJECT_TYPE set based on detection

**Step 2: Scan Existing Structure**
- [ ] Django: Finds settings.py, apps/, models, views, tests
- [ ] Django: Reads settings.py (INSTALLED_APPS, DATABASES, MIDDLEWARE)
- [ ] Django: Reads requirements.txt
- [ ] Laravel: Finds app/Models/, app/Http/Controllers/, routes/
- [ ] Laravel: Reads config/app.php, composer.json
- [ ] Python: Finds __init__.py files, reads pyproject.toml
- [ ] Node.js: Reads package.json, finds src/ structure

**Step 3: Interactive Context Gathering**
- [ ] Agent shows detected structure
- [ ] Agent asks ONE focused question
- [ ] Agent parses user's response

**Step 4: Generate Context Files from Analysis**
- [ ] 4.1: project-overview.md based on ACTUAL code (lists existing apps/modules)
- [ ] 4.2: conventions.md (correct framework, based on detected patterns)
- [ ] 4.3: tech-stack.md (lists ACTUAL dependencies from requirements/composer/package.json)
- [ ] 4.4: decision-log.md (documents integration + existing decisions)
- [ ] 4.5: CLAUDE.md updated (no placeholders)
- [ ] 4.6: .env.example SKIPPED (user already has .env)

**Critical Checks:**
- [ ] ❌ NO new source directories created (apps/, src/, tests/)
- [ ] ❌ NO changes to existing source code files
- [ ] ❌ NO changes to existing config files (settings.py, .env, etc.)
- [ ] ❌ NO .env.example created if .env exists

**Step 5: Validation & Verification**
- [ ] Context files exist
- [ ] CLAUDE.md updated
- [ ] `git status` shows ONLY docs/.claude/ and CLAUDE.md changes
- [ ] NO changes to source code
- [ ] Validation catches if new directories were incorrectly created

**Step 6: Present Integration Summary**
- [ ] Shows detected project type
- [ ] Lists apps/modules found
- [ ] Lists dependencies found
- [ ] Confirms existing structure preserved
- [ ] Provides next steps

---

## Automated Validation Script

For each test scenario, run:

```bash
#!/bin/bash
# validation-test.sh

echo "=== VibeCoder Workflow Validation ==="

# Test 1: Check required templates exist
echo "Checking templates..."
for template in project-overview.md tech-stack.md decision-log.md conventions-django.md conventions-laravel.md conventions-python.md conventions-javascript.md conventions-php.md; do
    if [ -f "docs/.claude/_TEMPLATES/$template" ]; then
        echo "✓ $template exists"
    else
        echo "✗ MISSING: $template"
    fi
done

# Test 2: Check agent files exist
echo -e "\nChecking agent files..."
for agent in initialization-agent.md existing-project-integration.md; do
    if [ -f "docs/.claude/_SYSTEM/$agent" ]; then
        echo "✓ $agent exists"
    else
        echo "✗ MISSING: $agent"
    fi
done

# Test 3: Check CLAUDE.md has placeholders (before init)
echo -e "\nChecking CLAUDE.md..."
if grep -q "\[One sentence\]" CLAUDE.md; then
    echo "✓ CLAUDE.md has placeholders (ready for init)"
else
    echo "! CLAUDE.md may already be initialized"
fi

# Test 4: Check context directory
echo -e "\nChecking context directory..."
if [ -d "docs/.claude/context" ]; then
    echo "✓ Context directory exists"
    count=$(ls docs/.claude/context/*.md 2>/dev/null | wc -l)
    echo "  Found $count files"
else
    echo "✗ Context directory missing"
fi

echo -e "\n=== Validation Complete ==="
```

---

## Manual Test Protocol

### Test New Project Workflow

1. **Setup:**
   ```bash
   git clone https://github.com/jenn0pal/vibecoding-boilerplate.git test-new-django
   cd test-new-django
   ```

2. **Run Initialization:**
   Start Claude session:
   ```
   Load docs/.claude/_SYSTEM/initialization-agent.md
   Initialize Django project: TestApp

   [Respond to Claude's question]:
   TestApp - Simple task tracker - Django + Vue - MVP - Solo developer
   ```

3. **Validate Results:**
   ```bash
   # Check files created
   ls docs/.claude/context/
   # Should show: project-overview.md, conventions.md, tech-stack.md, decision-log.md

   # Check CLAUDE.md updated
   grep "Purpose:" CLAUDE.md
   # Should show: "Purpose: Simple task tracker" (not "[One sentence]")

   # Check directories created
   ls apps/
   # Should show: users, core, api

   # Check .env.example
   cat .env.example | grep SECRET_KEY
   # Should show Django SECRET_KEY variable
   ```

4. **Record Results:**
   - [ ] All files created
   - [ ] CLAUDE.md updated
   - [ ] Directories created
   - [ ] .env.example has Django variables
   - [ ] No errors occurred
   - [ ] Validation commands pass

### Test Existing Project Workflow

1. **Setup Mock Existing Project:**
   ```bash
   mkdir test-existing-django
   cd test-existing-django

   # Create minimal Django project structure
   mkdir -p myproject apps/users apps/tasks tests
   touch manage.py
   mkdir -p myproject
   echo 'INSTALLED_APPS = ["users", "tasks"]' > myproject/settings.py
   echo -e "Django==5.0\npsycopg2==2.9\ndjangorestframework==3.14" > requirements.txt

   # Copy VibeCoder
   git clone https://github.com/jenn0pal/vibecoding-boilerplate.git /tmp/vb
   cp -r /tmp/vb/docs .
   cp /tmp/vb/CLAUDE.md .
   rm -rf /tmp/vb

   # Initialize git to track changes
   git init
   git add -A
   git commit -m "Initial existing project"
   ```

2. **Run Integration:**
   Start Claude session:
   ```
   Load docs/.claude/_SYSTEM/existing-project-integration.md
   Integrate VibeCoder with my existing Django project

   [Respond to Claude]:
   Task management system - Production - 3 developers
   ```

3. **Validate Results:**
   ```bash
   # Check files created (documentation only)
   ls docs/.claude/context/
   # Should show 4 files

   # Check project-overview mentions existing apps
   grep -i "users\|tasks" docs/.claude/context/project-overview.md
   # Should mention both apps

   # Check tech-stack has actual dependencies
   grep "Django==5.0" docs/.claude/context/tech-stack.md
   # Should show Django 5.0

   # CRITICAL: Check no source code changed
   git status
   # Should ONLY show:
   #   new file: docs/.claude/...
   #   modified: CLAUDE.md
   # Should NOT show:
   #   new file: apps/core  (would indicate wrong workflow!)
   #   modified: manage.py
   #   new file: .env.example

   # Check existing structure preserved
   ls apps/
   # Should ONLY show: users, tasks (NO new apps!)
   ```

4. **Record Results:**
   - [ ] Documentation created
   - [ ] project-overview.md mentions existing apps (users, tasks)
   - [ ] tech-stack.md shows actual dependencies
   - [ ] CLAUDE.md updated
   - [ ] ❌ NO new source directories created
   - [ ] ❌ NO existing files modified
   - [ ] git status clean except docs/.claude/ and CLAUDE.md

---

## Gap Detection Matrix

| Workflow | Test Scenario | Pass | Fail | Gaps Found | Fix Required |
|----------|---------------|------|------|------------|--------------|
| New Django | Happy path | | | | |
| New Laravel | Happy path | | | | |
| Existing Django | Happy path | | | | |
| Existing Laravel | Happy path | | | | |
| New → Wrong agent | Edge case | | | | |
| Existing → Missing deps | Edge case | | | | |
| Existing → No framework | Edge case | | | | |
| Both → Doc updates | Cross-workflow | | | | |
| Both → Validation fail | Error handling | | | | |

---

## Success Criteria

### New Project Workflow Passes If:
- ✅ All 4 context files created with populated content (no placeholders)
- ✅ Correct framework template used (Django vs Laravel vs Python)
- ✅ Framework-specific directories created
- ✅ Framework-specific .env.example created
- ✅ CLAUDE.md updated with actual project info
- ✅ Validation commands pass
- ✅ No errors during execution

### Existing Project Workflow Passes If:
- ✅ All 4 context files created based on ACTUAL code analysis
- ✅ project-overview.md mentions existing apps/modules
- ✅ tech-stack.md lists actual dependencies from files
- ✅ Correct framework conventions used
- ✅ CLAUDE.md updated
- ✅ **NO new source directories created**
- ✅ **NO existing files modified**
- ✅ git status shows ONLY docs/.claude/ changes
- ✅ Validation confirms structure preserved

---

**Next Step:** Run these tests and document results in this file.
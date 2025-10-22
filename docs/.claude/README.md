# Claude Workspace Guide - Step-by-Step Instructions

## 🚀 Quick Navigation
- [Starting a New Project](#starting-a-new-project-first-time-setup)
- [Continuing an Existing Project](#continuing-an-existing-project)
- [Starting a New Feature](#starting-a-new-feature)
- [Resuming Work on a Feature](#resuming-work-on-a-feature)
- [Common Workflows](#common-workflows)

---

## 📋 Starting a New Project (First-Time Setup)

### Step 1: Load Essential Context
```markdown
Please read the following files in order:
1. CLAUDE.md - Master instructions
2. docs/.claude/context/project-overview.md - Project context (if exists)
```

### Step 2: Understand the Project
```markdown
Tell me about:
- The project's purpose and goals
- Current stage (new/existing)
- Tech stack preferences
- Team size and structure
```

### Step 3: Initialize Documentation Structure
```markdown
Create the Claude workspace structure:

1. Copy appropriate templates from docs/.claude/_TEMPLATES/:
   - project-overview.md → docs/.claude/context/
   - conventions-[language].md → docs/.claude/context/conventions.md
   - tech-stack.md → docs/.claude/context/
   - decision-log.md → docs/.claude/context/

2. Customize each template with project-specific information

3. Create initial feature spec if starting with a specific feature
```

### Step 4: Set Up Development Environment
```markdown
Based on the tech stack:
1. Review docs/.claude/context/tech-stack.md
2. Set up development environment
3. Initialize version control
4. Configure linting and formatting tools
5. Set up testing framework
```

### Step 5: Create Initial Todo List
```markdown
Create initial project setup todos:
- [ ] Initialize project structure
- [ ] Set up development environment
- [ ] Configure build tools
- [ ] Set up testing framework
- [ ] Create initial documentation
- [ ] Configure CI/CD (if applicable)
```

---

## 🔄 Continuing an Existing Project

### Step 1: Load Project Context
```markdown
Please read in this order:
1. CLAUDE.md - Master instructions (always first)
2. docs/.claude/context/project-overview.md - Full project context
3. docs/.claude/context/conventions.md - Coding standards
4. docs/.claude/context/tech-stack.md - Technology details
```

### Step 2: Check Current Status
```markdown
Review current work status:
1. Check docs/.claude/tasks/in-progress.md (if exists)
2. Review recent commits: git log --oneline -10
3. Check for any open pull requests
4. Review docs/.claude/features/[active-feature]/progress.md
```

### Step 3: Identify Today's Goals
```markdown
What needs to be done today?
- Continue work on: [specific feature/task]
- Fix issues: [any bugs or problems]
- Complete: [specific deliverables]
```

### Step 4: Load Relevant Feature Documentation
```markdown
If working on a specific feature:
Read docs/.claude/features/[feature-name]/spec.md
Check docs/.claude/features/[feature-name]/tasks.md for progress
```

### Step 5: Resume with Context
```markdown
Resuming work on [feature/task]:
- Last completed: [what was done]
- Current task: [what's in progress]
- Next steps: [what needs to be done]

Create/update todo list for today's work.
```

---

## 🎯 Starting a New Feature

### Step 1: Feature Preparation
```markdown
1. Read CLAUDE.md and project context
2. Create feature directory: docs/.claude/features/[feature-name]/
3. Copy feature template from _TEMPLATES/new-feature.md
```

### Step 2: Define Feature Specification
```markdown
Create docs/.claude/features/[feature-name]/spec.md with:
1. Feature overview and business value
2. User stories with acceptance criteria
3. Technical requirements
4. UI/UX requirements (if applicable)
5. Testing requirements
6. Success metrics
```

### Step 3: Technical Design
```markdown
Create docs/.claude/features/[feature-name]/architecture.md:
1. Component design
2. Data flow
3. API contracts
4. Database changes (if any)
5. Integration points
```

### Step 4: Task Breakdown
```markdown
Create docs/.claude/features/[feature-name]/tasks.md:
1. Break feature into manageable tasks
2. Estimate effort for each task
3. Identify dependencies
4. Create implementation order
```

### Step 5: Begin Implementation
```markdown
1. Create feature branch: git checkout -b feature/[feature-name]
2. Set up todo list with tasks
3. Start with first task
4. Follow TDD approach if applicable
5. Update progress as you work
```

---

## 🔁 Resuming Work on a Feature

### Step 1: Load Feature Context
```markdown
Read in order:
1. CLAUDE.md
2. docs/.claude/features/[feature-name]/spec.md
3. docs/.claude/features/[feature-name]/tasks.md
4. docs/.claude/features/[feature-name]/progress.md (if exists)
```

### Step 2: Check Current Progress
```markdown
1. Review completed tasks
2. Identify current task in progress
3. Check for any blockers or issues
4. Review recent code changes
```

### Step 3: Update and Continue
```markdown
1. Update task status in todos
2. Continue with current task or start next task
3. Follow conventions from docs/.claude/context/conventions.md
4. Write tests as you go
5. Update documentation
```

---

## 🛠️ Common Workflows

### Code Review Workflow
```markdown
1. Read CLAUDE.md and conventions.md
2. Activate Code Reviewer agent
3. Review against:
   - Coding standards
   - Best practices
   - Security considerations
   - Performance implications
4. Provide actionable feedback
```

### Bug Fixing Workflow
```markdown
1. Load project context
2. Understand the bug:
   - Expected behavior
   - Actual behavior
   - Steps to reproduce
3. Locate the issue
4. Implement fix following conventions
5. Add regression test
6. Update documentation if needed
```

### Refactoring Workflow
```markdown
1. Load project context and conventions
2. Identify refactoring scope
3. Ensure tests exist (write if needed)
4. Refactor incrementally
5. Run tests after each change
6. Update documentation
```

### Documentation Update Workflow
```markdown
1. Identify what needs documenting
2. Choose appropriate location:
   - .claude/features/ for working docs
   - docs/features/ for official docs
   - .claude/context/ for project-wide info
3. Write clear, concise documentation
4. Update related documents
5. Archive obsolete content
```

---

## 📁 Directory Structure Reference

```
docs/.claude/                          # Claude AI workspace
├── _TEMPLATES/                        # Template library (copy from here)
│   ├── project-overview.md          # Project context template
│   ├── conventions-*.md             # Language-specific conventions
│   ├── feature-spec-detailed.md     # Feature specification template
│   └── [other templates]
├── features/                         # Active feature documentation
│   └── [feature-name]/
│       ├── spec.md                  # Requirements & user stories
│       ├── tasks.md                 # Task breakdown
│       ├── architecture.md          # Technical design
│       ├── progress.md              # Implementation progress
│       └── notes.md                 # Learnings & decisions
├── tasks/                           # Task management
│   ├── backlog.md                  # Prioritized upcoming tasks
│   ├── in-progress.md              # Current work (temp file)
│   └── completed.md                # Completed tasks archive
├── context/                         # Project context (ALWAYS CURRENT)
│   ├── project-overview.md         # What, why, who, how
│   ├── tech-stack.md               # Technologies & versions
│   ├── conventions.md              # Coding standards & patterns
│   ├── glossary.md                 # Domain terms & concepts
│   └── decisions.md                # Architecture Decision Records
├── prompts/                         # Reusable Claude prompts
│   └── templates/
├── agents/                          # Specialized agent configs
│   ├── architect/
│   ├── reviewer/
│   └── [other agents]/
└── archive/                         # ⚠️ NEVER READ - Obsolete content
    └── README.md                    # Warning notice
```

---

## 🎨 Best Practices

### When Starting Any Session:
1. **ALWAYS** read CLAUDE.md first
2. Load only relevant context files
3. State clear objectives for the session
4. Create or update todo list
5. Follow established conventions

### During Development:
1. Update progress regularly
2. Follow TDD when possible
3. Document decisions as you make them
4. Keep feature specs current
5. Archive completed work promptly

### When Ending a Session:
1. Update task status
2. Commit changes with conventional commits
3. Update progress documentation
4. Note any blockers or next steps
5. Clean up temporary files

---

## 🚨 Important Rules

### DO:
✅ Read CLAUDE.md at the start of every conversation
✅ Follow conventions.md strictly
✅ Write tests for all features
✅ Use conventional commits
✅ Update documentation as you work
✅ Archive obsolete content immediately

### DON'T:
❌ Read anything in docs/.claude/archive/
❌ Suggest new patterns without checking existing ones
❌ Skip tests or documentation
❌ Leave outdated information in active directories
❌ Make assumptions without checking context

---

## 📝 Quick Commands

### Git Commands
```bash
# Start new feature
git checkout -b feature/[feature-name]

# Conventional commits
git commit -m "feat: add new feature"
git commit -m "fix: resolve bug"
git commit -m "docs: update documentation"
git commit -m "refactor: improve code structure"
git commit -m "test: add tests"
```

### File Operations
```bash
# Create feature directory
mkdir -p docs/.claude/features/[feature-name]

# Copy template
cp docs/.claude/_TEMPLATES/feature-spec-detailed.md docs/.claude/features/[feature-name]/spec.md

# Archive completed feature
mv docs/.claude/features/[feature-name] docs/.claude/archive/
```

---

## 🔄 Session State Management

### Saving Context
When conversation is ending or getting long:
```markdown
Current state summary:
- Working on: [feature/task]
- Completed: [what was done]
- Next steps: [what's next]
- Blockers: [any issues]
- Important context: [key decisions or learnings]
```

### Resuming Context
When starting a new conversation:
```markdown
Resuming from previous session:
- Last worked on: [feature/task]
- Last completed: [what was done]
- Continue with: [next task]
- Context: [relevant information]
```

---

## 🆘 Troubleshooting

### If Context is Lost:
1. Re-read CLAUDE.md
2. Check git log for recent work
3. Review in-progress.md
4. Load feature spec for current work

### If Unsure About Conventions:
1. Check docs/.claude/context/conventions.md
2. Look for existing patterns in codebase
3. Check decision log for past decisions
4. Ask for clarification before proceeding

### If Feature Spec is Unclear:
1. Review user stories and acceptance criteria
2. Check with product owner or team lead
3. Document assumptions clearly
4. Create spike task if investigation needed

---

## 📚 Additional Resources

- **Templates**: All templates are in `docs/.claude/_TEMPLATES/`
- **Examples**: Look for existing features in `docs/.claude/features/`
- **Decisions**: Check `docs/.claude/context/decisions.md` for ADRs
- **Glossary**: Refer to `docs/.claude/context/glossary.md` for terms

---

*Last Updated: [Date]*
*Version: 1.0*

**Remember**: This guide is your roadmap. Always start with CLAUDE.md, follow the established patterns, and keep documentation current as you work.
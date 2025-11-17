# Developer Onboarding Guide

> **Complete guide for new team members to get productive with ClaudeContext**

## Welcome! 👋

This guide will help you get up to speed with our development workflow using ClaudeContext - a comprehensive documentation system for AI-assisted development with Claude.

**Time to productivity:** ~2-4 hours for basic setup, 1-2 days to become fully proficient.

---

## 📋 Onboarding Checklist

Use this checklist to track your progress:

### Day 1: Environment & Access
- [ ] Clone repository and verify access
- [ ] Set up development environment (language runtime, dependencies)
- [ ] Read this onboarding guide completely
- [ ] Read `CLAUDE.md` - master instructions
- [ ] Read `docs/.claude/context/project-overview.md` - understand the project
- [ ] Review `docs/.claude/context/conventions.md` - coding standards
- [ ] Review `docs/.claude/context/tech-stack.md` - technologies we use
- [ ] Set up IDE/editor with recommended extensions
- [ ] Run the project locally
- [ ] Run the test suite successfully

### Day 2: Understanding ClaudeContext
- [ ] Read ClaudeContext System Overview (below)
- [ ] Understand directory structure
- [ ] Review available templates in `docs/.claude/_TEMPLATES/`
- [ ] Understand workflow for starting new features
- [ ] Review existing features in `docs/.claude/features/`
- [ ] Understand how we track bugs, tech debt, and tasks

### Day 3-5: First Contributions
- [ ] Pair with a team member on an existing task
- [ ] Pick a "good first issue" or starter task
- [ ] Complete your first feature using ClaudeContext workflow
- [ ] Submit your first pull request
- [ ] Participate in code review (reviewing others' code)
- [ ] Document any unclear processes you encountered

### Week 2: Advanced Topics
- [ ] Learn how to delegate to specialized agents
- [ ] Understand multi-phase feature workflow
- [ ] Review deployment and release process
- [ ] Understand incident response procedures
- [ ] Contribute to documentation improvements

---

## 🎯 What is ClaudeContext?

ClaudeContext is a **documentation-driven development system** that helps teams work effectively with Claude AI. It provides:

- 📚 **Structured documentation** - Project context, conventions, tech stack, decision logs
- 🤖 **Specialized AI agents** - 11 expert agents for different development tasks
- 📝 **Workflow templates** - Proven patterns for features, bugs, refactoring, deployments
- 🔄 **Multi-phase execution** - Complex features broken into manageable phases
- ✅ **Quality gates** - Automated checklists and best practices

**Key Principle:** By providing Claude with comprehensive, structured context, we get:
- Better code quality (follows our conventions)
- Fewer hallucinations (understands our architecture)
- Faster development (reusable workflows)
- Consistent patterns (team alignment)

---

## 📂 Understanding the Directory Structure

```
project-root/
├── CLAUDE.md                              # 🔑 START HERE - Master instructions
├── README.md                              # Project README for humans
│
├── docs/
│   └── .claude/                           # Claude workspace (our focus)
│       ├── _SYSTEM/                       # System configuration
│       │   ├── onboarding-guide.md        # This file!
│       │   ├── initialization-agent.md    # New project setup
│       │   ├── existing-project-integration.md  # Existing project setup
│       │   ├── agents-guide.md            # How to use specialized agents
│       │   └── agents/                    # 11 specialized agent configs
│       │
│       ├── _TEMPLATES/                    # Reference templates
│       │   ├── _BASE/                     # Universal templates (all projects)
│       │   ├── _SHARED/                   # Reusable components (git, testing, security)
│       │   ├── python/                    # Python-specific templates
│       │   ├── django/                    # Django framework templates
│       │   ├── laravel/                   # Laravel framework templates
│       │   ├── php/                       # PHP-specific templates
│       │   ├── javascript/                # JavaScript/TypeScript templates
│       │   └── vue/                       # Vue 3 ecosystem templates
│       │
│       ├── context/                       # 🔑 Project context (READ THESE!)
│       │   ├── project-overview.md        # Full project context
│       │   ├── conventions.md             # Coding standards and patterns
│       │   ├── tech-stack.md              # Technology stack
│       │   ├── decision-log.md            # Architectural decisions
│       │   └── glossary.md                # Domain terminology (optional)
│       │
│       ├── features/                      # Feature specs & working docs
│       ├── tasks/                         # Phase-based tasks (FEAT-[ID]-PHASE-[N].md)
│       ├── bugs/                          # Bug tracking (BUG-[ID].md)
│       ├── modifications/                 # Code changes (MOD-[ID].md)
│       ├── refactoring/                   # Refactoring plans (REFACTOR-[ID].md)
│       ├── tech-debt/                     # Tech debt tracking (DEBT-[ID].md)
│       ├── upgrades/                      # Framework/dependency upgrades
│       ├── migrations/                    # Migration plans (MIGRATION-[ID].md)
│       └── archive/                       # ⚠️ NEVER READ (obsolete content)
│
├── src/                                   # Source code
├── tests/                                 # Test files
└── ...                                    # Your project files
```

**Key Directories:**
- `docs/.claude/context/` - **Read these first!** Project context files
- `docs/.claude/_TEMPLATES/` - Template library (reference only, don't edit)
- `docs/.claude/features/` - Active feature development
- `docs/.claude/_SYSTEM/` - System guides and agent configs

---

## 🚀 Quick Start: Your First Session with Claude

### Step 1: Start a Development Session

When working with Claude, always start by loading context:

```
Load CLAUDE.md
Load docs/.claude/context/project-overview.md
Load docs/.claude/context/conventions.md

Hi! I'm a new developer on the team.
I want to work on: [describe your task]
```

### Step 2: Working on a Feature

```
Load CLAUDE.md
Load docs/.claude/context/project-overview.md

Starting feature: [feature name]
Spec: docs/.claude/features/[feature-name]/spec.md

Please help me implement this feature following our conventions.
```

### Step 3: Fixing a Bug

```
Load CLAUDE.md
Load docs/.claude/context/conventions.md

Bug: [Brief description]
Severity: [Critical/High/Medium/Low]
Steps to reproduce:
1. [Step 1]
2. [Step 2]

Error: [Error message]

Please help me:
1. Write a failing test
2. Identify root cause
3. Fix following conventions
4. Verify test passes
```

---

## 🤖 Understanding Specialized Agents

ClaudeContext includes 11 specialized agents. Think of them as expert consultants.

| Agent | When to Use |
|-------|-------------|
| **Product Owner** | Defining features, user stories, requirements |
| **Systems Architect** | Architecture design, tech decisions, scalability |
| **Backend Engineer** | APIs, databases, business logic |
| **Frontend Developer** | UI components, state management, styling |
| **Test Engineer** | Writing tests, test strategy, debugging |
| **Code Reviewer** | PR reviews, quality checks |
| **Security Auditor** | Security analysis, vulnerability scanning |
| **Performance Optimizer** | Performance tuning, optimization |
| **DevOps Engineer** | CI/CD, deployments, infrastructure |
| **Data Engineer** | Data pipelines, ETL, analytics |
| **Documentation Specialist** | API docs, user guides, technical writing |

**How to activate an agent:**

```
Load docs/.claude/_SYSTEM/agents/[agent-name].md
Load docs/.claude/context/conventions.md

Task: [What you need done]
[Agent-specific parameters]

Please help me complete this task.
```

**Full guide:** `docs/.claude/_SYSTEM/agents-guide.md`

---

## 📖 Core Workflows You'll Use Daily

### 1. Starting a New Feature

**Simple feature:**
```
Load CLAUDE.md and docs/.claude/context/project-overview.md
Starting feature: [name]
Please help me implement following our conventions.
```

**Complex feature (multi-phase):**
```
Load CLAUDE.md and docs/.claude/context/project-overview.md

Feature: [Feature name]
Complexity: Complex
Description: [Brief description]

This requires multiple phases. Please help me:
1. Create feature implementation workflow
2. Break down into phases
3. Assign agents to each phase
```

### 2. Fixing a Bug

```
Load CLAUDE.md and docs/.claude/context/conventions.md

Bug: [Description]
Severity: [Level]
Environment: [Dev/Staging/Production]
Steps to reproduce: [Steps]
Error: [Error message]

Please help me fix this bug with TDD approach.
```

### 3. Code Review

```
Load CLAUDE.md and conventions.md
Load docs/.claude/_TEMPLATES/_SHARED/code-review-checklist.md

Review: [files or PR link]
Focus: [security/performance/standards]

Please review using the checklist.
```

### 4. Refactoring Code

```
Load CLAUDE.md and docs/.claude/context/conventions.md

Refactor: [Component to refactor]
Goal: [Improve performance/readability/maintainability]
Scope: [What's allowed to change]
Constraints: [What must stay the same]

Please help me refactor incrementally with tests.
```

---

## 🎓 Learning Path

### Week 1: Foundations
1. **Read** CLAUDE.md and all files in `docs/.claude/context/`
2. **Understand** project structure and conventions
3. **Run** the project locally and explore the codebase
4. **Complete** a simple bug fix or small feature
5. **Review** how features are documented in `docs/.claude/features/`

### Week 2: Workflows
1. **Learn** the feature development workflow
2. **Use** specialized agents for different tasks
3. **Practice** writing good prompts for Claude
4. **Participate** in code reviews
5. **Document** your first feature properly

### Week 3: Advanced
1. **Work on** a multi-phase feature
2. **Understand** deployment and release process
3. **Learn** how we handle tech debt
4. **Contribute** to documentation improvements
5. **Mentor** the next new team member

---

## 📚 Essential Reading (Priority Order)

### Must Read (Day 1)
1. **CLAUDE.md** - Master instructions for working with Claude
2. **docs/.claude/context/project-overview.md** - Complete project context
3. **docs/.claude/context/conventions.md** - Coding standards and patterns
4. **docs/.claude/context/tech-stack.md** - Technologies we use
5. **This guide** - Onboarding workflow

### Should Read (Week 1)
6. **docs/.claude/_SYSTEM/agents-guide.md** - How to use specialized agents
7. **docs/.claude/_TEMPLATES/README.md** - Template organization
8. **docs/.claude/context/decision-log.md** - Why we made certain architectural choices
9. **docs/.claude/features/README.md** - How we manage features
10. **docs/.claude/bugs/README.md** - Bug tracking workflow

### Good to Know (Week 2)
11. **docs/.claude/tasks/README.md** - Multi-phase task management
12. **docs/.claude/refactoring/README.md** - Refactoring workflow
13. **docs/.claude/tech-debt/README.md** - Tech debt management
14. **docs/.claude/upgrades/README.md** - Upgrade process

---

## 🛠️ Development Environment Setup

### General Setup (All Stacks)

1. **Clone the repository**
   ```bash
   git clone [repository-url]
   cd [project-name]
   ```

2. **Install dependencies**
   - See `docs/.claude/context/tech-stack.md` for specific instructions
   - Check README.md for quick setup commands

3. **Configure environment**
   ```bash
   # Copy example environment file
   cp .env.example .env
   # Edit .env with local settings (ask team for secrets)
   ```

4. **Verify setup**
   ```bash
   # Run tests
   [test command from tech-stack.md]

   # Run development server
   [dev command from tech-stack.md]
   ```

### IDE/Editor Setup

**Recommended Extensions:**
- See `docs/.claude/context/conventions.md` for stack-specific recommendations
- Generally: Linters, formatters, test runners, git integration

**Configuration:**
- Follow team's formatting rules (usually defined in project config files)
- Set up auto-format on save
- Enable linter warnings

---

## 🔄 Daily Development Workflow

### Morning Routine
1. Pull latest changes: `git pull origin main`
2. Check team updates (standup notes, Slack, etc.)
3. Review assigned tasks in project management tool
4. Check `docs/.claude/features/` for your active features

### Starting Work
1. Create feature branch: `git checkout -b feature/your-feature-name`
2. Start Claude session with proper context loading
3. Implement following TDD approach (test first, then code)
4. Commit frequently with conventional commits

### Before Pushing
1. Run full test suite
2. Run linters/formatters
3. Review your own changes
4. Update documentation if needed
5. Push to remote: `git push -u origin your-branch-name`

### Code Review Process
1. Create pull request with clear description
2. Request review from team members
3. Respond to feedback promptly
4. Update code based on reviews
5. Merge when approved

---

## 🚨 Important Rules & Best Practices

### Critical Rules
1. **NEVER** read anything in `docs/.claude/archive/` - it's obsolete
2. **ALWAYS** load `CLAUDE.md` and `conventions.md` when starting work
3. **REQUIRED:** Write tests for all features
4. **REQUIRED:** Use conventional commits (feat:, fix:, docs:, etc.)
5. **CHECK:** Existing patterns before creating new ones

### Best Practices
- ✅ Start with context loading (CLAUDE.md, project-overview.md)
- ✅ Follow TDD approach (write tests first)
- ✅ Use specialized agents for their expertise
- ✅ Document decisions in decision-log.md
- ✅ Keep features small and focused
- ✅ Update documentation as you code
- ✅ Ask questions early and often

### Don't Do This
- ❌ Skip loading context when working with Claude
- ❌ Write code without tests
- ❌ Commit directly to main branch
- ❌ Use non-conventional commit messages
- ❌ Skip code review process
- ❌ Leave TODO comments without creating tasks

---

## 🤝 Team Collaboration

### Communication Channels
- **Daily Standup:** [Time and location]
- **Code Reviews:** GitHub Pull Requests
- **Questions:** [Slack/Teams/Discord channel]
- **Documentation:** This repository + [other docs location]

### Getting Help
1. **Check documentation first:** CLAUDE.md, context files, this guide
2. **Search existing issues:** GitHub Issues, past PRs
3. **Ask Claude:** Load relevant context and ask specific questions
4. **Ask the team:** Slack, pair programming sessions
5. **Pair programming:** Schedule with experienced team member

### Contributing to Documentation
If you find:
- Unclear documentation → Create issue or PR to improve it
- Missing workflow → Suggest new template
- Outdated information → Update and document in decision-log.md
- Better patterns → Share with team and update conventions.md

---

## 📝 Common Tasks Reference

### Working on a Feature
```
Load CLAUDE.md and docs/.claude/context/project-overview.md
Starting feature: [name]
Spec: docs/.claude/features/[name]/spec.md
```

### Fixing a Bug
```
Load CLAUDE.md and conventions.md
Bug: [description]
Severity: [level]
[Details...]
```

### Code Review
```
Load CLAUDE.md and conventions.md
Load docs/.claude/_TEMPLATES/_SHARED/code-review-checklist.md
Review: [files/PR]
```

### Refactoring
```
Load CLAUDE.md and conventions.md
Refactor: [component]
Goal: [objective]
```

### Performance Issue
```
Load CLAUDE.md and tech-stack.md
Load docs/.claude/_SYSTEM/agents/performance-optimizer.md
Issue: [description]
Metrics: [current performance]
Target: [goal]
```

### Deploying
```
Load CLAUDE.md and tech-stack.md
Load docs/.claude/_TEMPLATES/_BASE/deployment-checklist.md
Deployment: [what]
Environment: [staging/production]
```

---

## 🎯 Your First Week Goals

### Day 1-2: Setup & Understanding
- [ ] Complete environment setup
- [ ] Run project locally successfully
- [ ] Read all essential documentation
- [ ] Understand project structure and conventions
- [ ] Meet the team

### Day 3-4: First Contribution
- [ ] Pair with team member on existing task
- [ ] Pick a "good first issue"
- [ ] Implement fix/feature following workflow
- [ ] Submit your first PR
- [ ] Participate in code review

### Day 5: Reflection & Learning
- [ ] Review what you learned
- [ ] Document any confusing processes
- [ ] Improve onboarding docs based on your experience
- [ ] Set goals for week 2
- [ ] Celebrate your first week! 🎉

---

## 🆘 Troubleshooting Common Issues

### "Claude's suggestions don't match our style"
**Fix:** Always load `docs/.claude/context/conventions.md` with your prompts

### "I don't know which agent to use"
**Fix:** Check `docs/.claude/_SYSTEM/agents-guide.md` for agent selection guide

### "Tests are failing locally but passed in CI"
**Fix:** Ensure your environment matches CI (check .env, dependencies, database state)

### "I'm not sure what to work on"
**Fix:** Check project management tool, ask in standup, review `docs/.claude/features/`

### "My PR got lots of review comments"
**Fix:** Normal! Review `docs/.claude/_TEMPLATES/_SHARED/code-review-checklist.md` before submitting next time

### "I'm stuck on a bug"
**Fix:**
1. Load CLAUDE.md + conventions.md
2. Explain bug to Claude with full context
3. Ask for debugging help
4. If still stuck, pair with teammate

---

## 📊 Onboarding Success Metrics

You'll know you're successful when you can:

**Week 1:**
- [ ] Run the project locally without help
- [ ] Explain what ClaudeContext is
- [ ] Navigate the directory structure confidently
- [ ] Complete a simple bug fix or feature
- [ ] Submit a PR following our process

**Week 2:**
- [ ] Work on features independently
- [ ] Use specialized agents appropriately
- [ ] Write good prompts for Claude
- [ ] Participate meaningfully in code reviews
- [ ] Follow all conventions without referring to docs

**Week 4:**
- [ ] Mentor new team members
- [ ] Contribute to improving documentation
- [ ] Suggest workflow improvements
- [ ] Work on complex multi-phase features
- [ ] Help others troubleshoot issues

---

## 🎓 Advanced Topics (After Week 2)

### Multi-Phase Features
Learn how to break down complex features into phases with different specialized agents.
**Read:** `docs/.claude/_TEMPLATES/_BASE/feature-implementation-workflow.md`

### Agent Chaining
Learn to chain multiple agents for complex workflows (Product Owner → Architect → Backend → Frontend → Test → Review).
**Read:** `docs/.claude/_SYSTEM/agents-guide.md` (Agent Chaining Patterns section)

### Tech Debt Management
Learn how we track and address technical debt systematically.
**Read:** `docs/.claude/tech-debt/README.md`

### Performance Optimization
Learn our approach to identifying and fixing performance issues.
**Read:** Performance Optimizer agent + performance audit template

### Security Practices
Learn our security practices and how to perform security audits.
**Read:** `docs/.claude/_TEMPLATES/_SHARED/security-audit-checklist.md`

---

## 💬 Feedback & Improvements

### Help Us Improve Onboarding

As a new team member, you have valuable perspective! Please:

1. **Document confusion:** Note anything unclear during onboarding
2. **Suggest improvements:** Submit PRs to improve onboarding docs
3. **Share feedback:** Tell us what worked and what didn't
4. **Update this guide:** Add tips you wish you'd known earlier

**How to provide feedback:**
- Create issue: GitHub Issues with label "onboarding"
- Submit PR: Improve this guide or other docs
- Talk to team: Share in retrospectives or 1-on-1s

---

## 🎉 Welcome to the Team!

Onboarding can feel overwhelming, but remember:
- Everyone was new once
- It's OK to ask questions
- We value your fresh perspective
- Take it one step at a time
- You'll be productive faster than you think!

**Your success is our success. Welcome aboard!** 🚀

---

## 📞 Key Contacts

| Role | Name | Contact | Best For |
|------|------|---------|----------|
| **Tech Lead** | [Name] | [Email/Slack] | Architecture, technical decisions |
| **Team Lead** | [Name] | [Email/Slack] | Process, priorities, team questions |
| **DevOps** | [Name] | [Email/Slack] | CI/CD, deployments, infrastructure |
| **Onboarding Buddy** | [Assigned] | [Contact] | Day-to-day questions, pair programming |

**General Questions:** [Team Slack channel or email list]

---

## 📅 Onboarding Timeline

| Time | Milestone |
|------|-----------|
| **Day 1** | Environment setup, read core docs |
| **Day 2** | Understand codebase, run project locally |
| **Day 3-5** | First contribution with mentorship |
| **Week 2** | Independent feature work |
| **Week 3-4** | Complex features, code reviews |
| **Month 2** | Fully productive, mentor new hires |

---

## 🔗 Quick Links

- **CLAUDE.md** - Master instructions
- **Project Overview** - `docs/.claude/context/project-overview.md`
- **Conventions** - `docs/.claude/context/conventions.md`
- **Tech Stack** - `docs/.claude/context/tech-stack.md`
- **Agent Guide** - `docs/.claude/_SYSTEM/agents-guide.md`
- **Template Catalog** - `docs/.claude/_TEMPLATES/README.md`
- **Decision Log** - `docs/.claude/context/decision-log.md`

---

**Version:** 1.0
**Last Updated:** 2025-01-16
**Maintained By:** [Team Name]

**Next:** Read `CLAUDE.md` and `docs/.claude/context/project-overview.md` to get started!

# Working with Claude on [Project Name]

> **Quick Start:** Read this file at the beginning of every conversation.

## 🎯 Project Overview
- **Purpose:** [One sentence]
- **Stage:** [MVP/Beta/Production]
- **Tech Stack:** [Key technologies]
- **Team:** [Size and structure]

## 📖 Step-by-Step Instructions
For detailed instructions on starting new projects or continuing existing work, see:
**`docs/.claude/README.md`** - Complete step-by-step guide for all workflows

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

## 🔄 Standard Workflow
1. Load context: `docs/.claude/context/project-overview.md`
2. Review feature: `docs/.claude/features/[feature-name]/spec.md`
3. Follow conventions: `docs/.claude/context/conventions.md`
4. Implement → Test → Document

## 🤖 Available Agents
- **Architect** (`docs/.claude/agents/architect/`) - System design
- **Reviewer** (`docs/.claude/agents/reviewer/`) - Code review
- **Tester** (`docs/.claude/agents/tester/`) - Test planning
- **Documenter** (`docs/.claude/agents/documenter/`) - Documentation

## 📋 Common Prompts
**Start new feature:**
```
Load claude.md and docs/.claude/context/project-overview.md
Starting feature: [name]
Spec: docs/.claude/features/[name]/spec.md
```

**Resume work:**
```
Load claude.md
Continuing: [feature-name]
Last completed: [task]
Today's goal: [objective]
```

**Code review:**
```
Activate Reviewer agent
Review against: docs/.claude/context/conventions.md
Files: [list]
```

## 🔗 Essential Files
- **Full Context:** `docs/.claude/context/project-overview.md`
- **Conventions:** `docs/.claude/context/conventions.md`
- **Tech Stack:** `docs/.claude/context/tech-stack.md`
- **Glossary:** `docs/.claude/context/glossary.md`

## 📝 Notes
- Update specs as implementation evolves
- Archive obsolete content immediately
- Document decisions in `docs/.claude/context/decisions.md`

---
**Last Updated:** [Date]
**Maintained By:** [Name/Team]
```

---

## Updated Directory Structure
```
project-root/
├── CLAUDE.md                         # 👈 Master instructions (read first)
├── README.md
├── .gitignore
│
├── docs/
│   ├── .claude/                      # Claude workspace
│   │   ├── README.md                 # How to use this workspace
│   │   ├── features/                 # Feature specs
│   │   ├── tasks/                    # Task management
│   │   ├── context/                  # Project context
│   │   │   ├── project-overview.md   # Detailed context
│   │   │   ├── conventions.md
│   │   │   └── tech-stack.md
│   │   ├── prompts/                  # Reusable prompts
│   │   ├── agents/                   # Agent configs
│   │   └── archive/                  # ⚠️ DO NOT READ
│   │
│   ├── features/                     # Official docs
│   ├── architecture/
│   └── api/
│
└── src/
```

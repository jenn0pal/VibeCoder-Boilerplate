# VibeCoder Boilerplate 🚀

> **The Ultimate Claude-Optimized Development Boilerplate**
> A comprehensive documentation framework and workflow system designed to maximize productivity when using Claude AI for software development.

## 🎯 What is VibeCoder Boilerplate?

VibeCoder Boilerplate is a carefully crafted project structure that optimizes the way you collaborate with Claude AI on software projects. It provides:

- **📚 17+ Professional Templates** - From project overviews to specialized conventions
- **🤖 14 Specialized AI Agents** - Each optimized for specific development tasks
- **📋 Structured Workflows** - Step-by-step guides for common development scenarios
- **🔄 Context Management** - Keep Claude informed without information overload
- **🛠️ Modern Tooling** - Built for modern Python (`uv`, `ruff`), JavaScript/TypeScript, PHP, Django, and Laravel

## ⚡ Quick Start

### 1. Get the Boilerplate

```bash
# Clone the repository
git clone https://github.com/jenn0pal/vibecoding-boilerplate.git my-project
cd my-project

# Remove the origin and set up your own repository
rm -rf .git
git init
git remote add origin YOUR_REPO_URL
```

### 2. Choose Your Stack

Select the appropriate convention template for your project:

| Stack | Template File | Description |
|-------|--------------|-------------|
| **Python** | `conventions-python.md` | Modern Python with `uv` & `ruff` |
| **Django** | `conventions-django.md` | Django 5.0+ with best practices |
| **JavaScript/TypeScript** | `conventions-javascript.md` | ES2024+, React/Vue/Node.js |
| **PHP** | `conventions-php.md` | PHP 8.3+ with PSR standards |
| **Laravel** | `conventions-laravel.md` | Laravel 11+ patterns |

### 3. Let Claude Initialize Your Project

Instead of manually filling out templates, start a Claude conversation with this prompt:

```
Load docs/.claude/_SYSTEM/initialization-agent.md
Initialize [language/framework] project: [name]
```

**Examples:**
```
Initialize Django project: TaskHub
Initialize Laravel project: ShopAPI
Initialize Python project: DataPipeline
```

**Claude will ask you one simple question:**
- **Project info:** Name, purpose, tech stack, stage, team size

Then Claude automatically:
- ✅ Generates all documentation files (replaces placeholder files)
- ✅ Sets up appropriate conventions for your stack
- ✅ Creates project structure (apps/, src/, tests/, etc.)
- ✅ Updates CLAUDE.md with your project info
- ✅ Creates .env.example with framework-specific variables
- ✅ Gets you coding in < 5 minutes!

**Verify initialization succeeded:**
```bash
# Check that context files were generated
ls docs/.claude/context/
# Expected: project-overview.md, conventions.md, tech-stack.md, decision-log.md

# Verify CLAUDE.md was updated (should show your project info, not placeholders)
grep "Purpose:" CLAUDE.md

# Check project structure was created
ls -la  # Should see directories appropriate for your stack
```

### 4. Start Working with Claude

**Standard development session:**
```
Load CLAUDE.md
Load docs/.claude/context/project-overview.md
Working on: [describe your task]
```

**What you get:**
- ✅ Comprehensive project context
- ✅ Reduced risk of hallucinations
- ✅ Explicit conventions and best practices
- ✅ Clear architectural guidance
- ✅ Better code quality and consistency

## 📖 Step-by-Step Usage Guide

### Starting a New Project

#### Step 1: Project Setup
1. Clone the boilerplate
2. Remove the `.git` directory
3. Initialize your own git repository

#### Step 2: Let Claude Set Up Your Context

**Simple Method (Recommended):**
```
Load docs/.claude/_SYSTEM/initialization-agent.md
Initialize Django project: MyApp
```

The initialization agent will:
1. Ask you ONE question about your project (name, purpose, tech stack, stage, team)
2. Automatically generate all context files from templates
3. Set up appropriate conventions for your stack
4. Create project structure directories
5. Update CLAUDE.md with your information
6. Generate .env.example with framework-specific variables

**Manual Method (Alternative):**
```
I'm setting up a new project using the VibeCoder boilerplate.

Please help me initialize by:
1. Reading docs/.claude/_TEMPLATES/project-overview.md
2. Asking me questions to gather the necessary information
3. Creating a customized docs/.claude/context/project-overview.md for my project
4. Setting up the appropriate conventions file based on my tech stack
5. Creating docs/.claude/context/tech-stack.md with my technology choices
6. Creating docs/.claude/context/decision-log.md
7. Updating CLAUDE.md with my project information

After setup, guide me through the next steps.
```

**⚠️ Note:** The boilerplate includes placeholder files in `docs/.claude/context/`. The initialization process will replace these with your actual project documentation.

#### Step 3: Start Building
After Claude completes initialization:
```markdown
Load CLAUDE.md and docs/.claude/context/project-overview.md
First feature: [feature-name]

Please help me:
1. Validate the project structure
2. Set up the development environment
3. Create initial feature spec
```

### Working on Features

#### Creating a New Feature
```bash
# Create feature directory
mkdir -p docs/.claude/features/user-authentication

# Copy feature template
cp docs/.claude/_TEMPLATES/feature-spec-detailed.md \
   docs/.claude/features/user-authentication/spec.md

# Edit the spec with your requirements
```

#### Claude Prompt for Features
```markdown
Load CLAUDE.md and docs/.claude/context/conventions.md
Starting feature: user-authentication
Spec: docs/.claude/features/user-authentication/spec.md

Create implementation plan with todos.
```

### Using Specialized Agents

The boilerplate includes 14 specialized AI agents:

| Agent | Purpose | When to Use |
|-------|---------|------------|
| **System Architect** | System design & architecture | Starting new features, major refactoring |
| **Code Reviewer** | Code quality & standards | After implementation, before merging |
| **Test Engineer** | Test planning & implementation | Writing tests, debugging |
| **Backend Developer** | Server-side implementation | API development, database work |
| **Frontend Developer** | UI/UX implementation | Component development, styling |
| **Security Auditor** | Security analysis | Regular audits, sensitive features |
| **Performance Optimizer** | Performance tuning | Optimization, scaling issues |
| **Documentation Specialist** | Documentation | API docs, user guides |
| **DevOps Engineer** | Deployment & infrastructure | CI/CD, deployment setup |
| **Product Manager** | Requirements & planning | Feature planning, user stories |

#### Activating an Agent
```markdown
Activate [Agent Name] agent
Task: [specific task]
Context: docs/.claude/context/conventions.md
```

### Managing Tasks

#### Creating Todo Lists
```markdown
Create todo list for implementing user authentication:
- [ ] Design database schema
- [ ] Implement user model
- [ ] Create registration endpoint
- [ ] Add login functionality
- [ ] Implement JWT tokens
- [ ] Write tests
- [ ] Update documentation
```

#### Tracking Progress
The boilerplate uses a structured task management system:
- `docs/.claude/tasks/backlog.md` - Upcoming work
- `docs/.claude/tasks/in-progress.md` - Current tasks (temporary)
- `docs/.claude/features/[name]/progress.md` - Feature-specific progress

## 🗂️ Project Structure

```
your-project/
├── CLAUDE.md                          # 🎯 Master instructions (start here)
├── README.md                          # Your project documentation
├── .gitignore                         # Pre-configured for Claude workflow
│
├── docs/
│   ├── .claude/                       # Claude workspace
│   │   ├── README.md                  # Claude-specific instructions
│   │   ├── _TEMPLATES/                # 17+ ready-to-use templates
│   │   │   ├── project-overview.md
│   │   │   ├── conventions-*.md      # Language-specific conventions
│   │   │   ├── agent-configs.md      # AI agent configurations
│   │   │   ├── feature-spec-detailed.md
│   │   │   └── ...more templates
│   │   ├── context/                  # Your project context (customize these)
│   │   ├── features/                  # Active feature documentation
│   │   ├── tasks/                     # Task management
│   │   ├── prompts/                   # Reusable prompts
│   │   ├── agents/                    # Agent configurations
│   │   └── archive/                   # Completed/obsolete items
│   │
│   ├── features/                      # Official feature documentation
│   ├── architecture/                  # Architecture documentation
│   └── api/                           # API documentation
│
├── src/                               # Your source code
├── tests/                             # Your test files
└── ...                                # Your project files
```

## 🔄 Common Workflows

### Daily Development Cycle
1. **Start Session**: Load CLAUDE.md and current feature spec
2. **Review Progress**: Check `in-progress.md` and todos
3. **Work on Tasks**: Implement, test, document
4. **Update Progress**: Mark todos complete, update documentation
5. **Commit Changes**: Use conventional commits

### Code Review Process
```markdown
Activate Code Reviewer agent
Review scope: [files or PR]
Focus areas: [security/performance/standards]
Convention reference: docs/.claude/context/conventions.md
```

### Debugging Session
```markdown
Issue: [description]
Error message: [paste error]
Context: [when it occurs]
Files involved: [list files]

Please help debug this issue following our conventions.
```

### Documentation Update
```markdown
Activate Documentation Specialist agent
Update type: [API/User/Technical]
Files changed: [list]
Please update relevant documentation.
```

## 💡 Best Practices

### ✅ DO:
- **Start every Claude session** by loading CLAUDE.md
- **Keep context files updated** as your project evolves
- **Use specialized agents** for specific tasks
- **Track progress** with todos and progress files
- **Archive completed features** to keep workspace clean
- **Follow conventions** consistently
- **Document decisions** in decision-log.md

### ❌ DON'T:
- **Never read** from `docs/.claude/archive/` directory
- **Don't skip** the project context loading
- **Don't modify** templates directly (copy first)
- **Don't forget** to update progress tracking
- **Don't mix** different convention styles

## 🛠️ Modern Tooling Support

### Python Projects
- **Package Management**: `uv` (modern, fast Python package manager)
- **Linting/Formatting**: `ruff` (all-in-one Python linter)
- **Testing**: `pytest` with comprehensive configurations
- **Type Checking**: `mypy` with strict settings

### JavaScript/TypeScript
- **Package Management**: `pnpm`, `npm`, or `yarn`
- **Build Tools**: Vite, Webpack, or esbuild
- **Testing**: Jest, Vitest, or Playwright
- **Linting**: ESLint with modern configs

### PHP/Laravel
- **Package Management**: Composer
- **Testing**: Pest or PHPUnit
- **Code Style**: PSR-12 standards
- **Static Analysis**: PHPStan or Psalm

## 📚 Template Library

The boilerplate includes comprehensive templates for:

- **Project Documentation** (project overview, tech stack, glossary)
- **Development Standards** (language-specific conventions)
- **Feature Planning** (detailed specifications, user stories)
- **Task Management** (sprint planning, progress tracking)
- **AI Agent Configs** (14 specialized agents)
- **Workflow Optimization** (best practices guide)
- **Prompt Templates** (reusable Claude prompts)

## 🎯 Success Tips

1. **Load Context Gradually**: Don't overwhelm Claude with all files at once
2. **Be Specific**: Clear, detailed prompts get better results
3. **Use Agents**: Leverage specialized agents for better output quality
4. **Track Everything**: Use todos and progress files religiously
5. **Iterate Quickly**: Small, incremental changes with testing
6. **Document Decisions**: Future you will thank present you

## 🤝 Contributing

Found a way to improve the workflow? Have a great template to share?

1. Fork the repository
2. Create your feature branch
3. Add your improvements
4. Submit a pull request

## 📝 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- Built with insights from hundreds of Claude AI development sessions
- Inspired by modern development best practices
- Optimized for AI-assisted development workflows

## 🔗 Resources

- [Claude Documentation](https://docs.anthropic.com)
- [Conventional Commits](https://www.conventionalcommits.org)
- [uv - Python Package Manager](https://github.com/astral-sh/uv)
- [ruff - Python Linter](https://github.com/astral-sh/ruff)

---

## 🚀 Start Building!

Ready to supercharge your development workflow with Claude? Follow the quick start guide above and begin building with the power of AI-optimized documentation and workflows.

**Remember**: The best documentation is the one that gets used and updated. This boilerplate gives you the structure - make it your own!

---

*VibeCoder Boilerplate v1.0 - Optimizing AI-Assisted Development*
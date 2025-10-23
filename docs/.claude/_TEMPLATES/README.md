# Claude Documentation Templates

## Overview
This directory contains comprehensive templates for optimizing your Claude workflow across different projects. These templates are designed to be copied and customized for your specific needs.

**Note:** User-facing documentation (agent guides, prompt libraries, workflow tips) has been consolidated into the root README.md for easier access.

---

## 📁 Available Templates

### Core Documentation
1. **`project-overview.md`** - Comprehensive project context template
   - Business context and goals
   - Technical architecture overview
   - Team structure and roles
   - Development practices

2. **`conventions.md`** - General coding standards and patterns
   - Naming conventions
   - Code organization
   - Best practices
   - Tools and workflows

3. **`tech-stack.md`** - Technology stack documentation
   - Languages and frameworks
   - Libraries and dependencies
   - Infrastructure and deployment
   - Development tools

4. **`decision-log.md`** - Architectural Decision Records (ADRs)
   - Decision tracking template
   - Context and consequences
   - Alternatives considered
   - Review and approval process

### Language & Framework Specific

5. **`conventions-python.md`** - Python development standards
   - Modern tooling with `uv` package manager
   - Code formatting with `ruff`
   - Type hints and async patterns
   - Testing with pytest

6. **`conventions-javascript.md`** - JavaScript/TypeScript standards
   - ES2024+ features
   - TypeScript configuration
   - React/Vue/Node.js patterns
   - Build tools and bundling

7. **`conventions-php.md`** - PHP development standards
   - PHP 8.3+ features
   - PSR standards compliance
   - Composer package management
   - Testing with PHPUnit/Pest

8. **`conventions-django.md`** - Django framework conventions
   - Django 5.0+ patterns
   - Project structure with `uv`
   - `ruff` configuration for Django
   - Testing and deployment

9. **`conventions-laravel.md`** - Laravel framework conventions
   - Laravel 11+ best practices
   - Eloquent patterns
   - Service architecture
   - Testing with Pest

### Workflow & Management

10. **`task-management.md`** - Task and project management
    - User stories and epics
    - Sprint planning templates
    - Progress tracking
    - Release management

11. **`feature-spec-detailed.md`** - Comprehensive feature specification
    - Business requirements
    - Technical design
    - API specifications
    - Testing strategy
    - Rollout planning

12. **`code-modification.md`** - Code modification documentation (NEW in v1.2.0)
    - Modification planning for medium/large changes
    - Current state → Desired state tracking
    - Impact analysis and risk assessment
    - Testing and validation strategy
    - Post-implementation review

13. **`refactoring-plan.md`** - Refactoring documentation (NEW in v1.2.0)
    - Test-driven refactoring approach
    - Goals, metrics, and success criteria
    - Phase-by-phase implementation plan
    - Risk management and rollback strategy
    - Performance impact tracking

14. **`glossary.md`** - Project terminology and acronyms
    - Business terms
    - Technical concepts
    - Domain-specific vocabulary
    - Quick reference

---

## 🚀 Quick Start Guide

### 1. Initial Project Setup
```bash
# Copy templates to your project
cp project-overview.md ../../context/
cp conventions-[language].md ../../context/conventions.md
cp tech-stack.md ../../context/
cp decision-log.md ../../context/

# Customize for your project
# Edit each file with project-specific information
```

### 2. Choose Your Stack
Select and customize the appropriate convention templates:
- Python project: Use `conventions-python.md`
- Django project: Use `conventions-django.md`
- JavaScript/TypeScript: Use `conventions-javascript.md`
- PHP project: Use `conventions-php.md`
- Laravel project: Use `conventions-laravel.md`

### 3. Configure Agents
Copy and customize agent configurations based on your team structure and needs.

### 4. Set Up Prompts
Copy frequently used prompts to your `prompts/` directory for quick access.

---

## 📋 Template Usage Matrix

| Project Type | Essential Templates | Optional Templates |
|--------------|-------------------|-------------------|
| **New Python Project** | project-overview, conventions-python, tech-stack, prompt-templates | agent-configs, task-management |
| **Django Application** | project-overview, conventions-django, tech-stack, feature-spec | agent-configs, task-management |
| **Laravel Application** | project-overview, conventions-laravel, tech-stack, feature-spec | agent-configs, glossary |
| **React/Vue Frontend** | project-overview, conventions-javascript, tech-stack | agent-configs, workflow-guide |
| **Full-Stack Application** | All core templates, relevant language conventions | All optional templates |
| **Enterprise Project** | All templates | Customize extensively |

---

## 🛠️ Customization Guide

### Adapting Templates
1. **Keep structure, change content** - Maintain the organization while updating specifics
2. **Add project-specific sections** - Extend templates with unique requirements
3. **Remove irrelevant sections** - Delete parts that don't apply
4. **Update regularly** - Keep documentation current with project evolution

### Version Control
```bash
# Track your customized templates
git add docs/.claude/
git commit -m "feat: Initialize Claude documentation structure"

# Tag template versions
git tag -a claude-docs-v1.0 -m "Initial Claude documentation setup"
```

---

## 💡 Best Practices

### DO:
- ✅ Start with templates, then customize
- ✅ Keep documentation near the code
- ✅ Update as you learn and decide
- ✅ Use consistent formatting
- ✅ Archive outdated information
- ✅ Review and refine regularly

### DON'T:
- ❌ Use templates without customization
- ❌ Let documentation become stale
- ❌ Include sensitive information
- ❌ Over-document obvious things
- ❌ Create documentation for documentation's sake

---

## 🔄 Maintenance Schedule

| Frequency | Actions |
|-----------|---------|
| **Daily** | Update task progress, feature specs |
| **Weekly** | Review and update conventions, archive completed features |
| **Sprint** | Update project overview, review agent performance |
| **Monthly** | Refine prompts, update glossary, optimize workflow |
| **Quarterly** | Major documentation review, template updates |

---

## 📊 Template Statistics

| Template | Lines | Sections | Last Updated |
|----------|-------|----------|--------------|
| project-overview.md | ~300 | 15 | [Date] |
| conventions-python.md | ~800 | 20 | [Date] |
| conventions-django.md | ~900 | 22 | [Date] |
| agent-configs.md | ~1200 | 14 | [Date] |
| task-management.md | ~1000 | 18 | [Date] |
| feature-spec-detailed.md | ~1500 | 18 | [Date] |
| workflow-optimization-guide.md | ~900 | 15 | [Date] |

---

## 🤝 Contributing

### Adding New Templates
1. Create template in this directory
2. Follow existing structure and formatting
3. Include usage instructions
4. Add to this README
5. Submit for review

### Improving Existing Templates
1. Make changes in a branch
2. Document what changed and why
3. Test with real projects
4. Submit pull request
5. Update version numbers

---

## 📚 Resources

### Documentation
- [Claude Documentation](https://docs.anthropic.com)
- [Markdown Guide](https://www.markdownguide.org)
- [Mermaid Diagrams](https://mermaid-js.github.io)

### Tools
- **uv** - Modern Python package manager
- **ruff** - Fast Python linter and formatter
- **Pest** - Elegant PHP testing
- **Vite** - Next generation frontend tooling

### Communities
- [Claude Discord](https://discord.gg/claude)
- [Python Discord](https://discord.gg/python)
- [Laravel Discord](https://discord.gg/laravel)
- [Django Forum](https://forum.djangoproject.com)

---

## 🎯 Success Metrics

Track the effectiveness of your Claude documentation:

| Metric | Target | Measurement |
|--------|--------|-------------|
| Setup Time | < 30 minutes | Time to configure new project |
| Context Load | < 1 minute | Time to brief Claude |
| Feature Completion | > 80% first try | Features working without major rework |
| Documentation Currency | < 1 week old | Time since last update |
| Team Adoption | 100% | Team members using templates |

---

## 🏁 Getting Started Checklist

For new projects:
- [ ] Copy relevant templates
- [ ] Customize project-overview.md
- [ ] Select and adapt conventions
- [ ] Configure tech-stack.md
- [ ] Set up prompt library
- [ ] Configure agents
- [ ] Initialize task tracking
- [ ] Create first feature spec
- [ ] Document initial decisions
- [ ] Establish update schedule

For existing projects:
- [ ] Audit current documentation
- [ ] Identify gaps
- [ ] Gradually adopt templates
- [ ] Migrate existing docs
- [ ] Train team on new structure
- [ ] Establish maintenance routine

---

*Templates Version: 1.0*
*Created: [Date]*
*Maintained by: [Your Team]*

**Remember**: These templates are starting points. The best documentation is the one that gets used and updated regularly. Adapt them to fit your team's needs and workflow.
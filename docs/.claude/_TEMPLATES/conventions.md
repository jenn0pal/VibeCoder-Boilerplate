# Project Conventions

## Code Style

### General Principles
- **Readability > Cleverness:** Write code that junior developers can understand
- **Consistency > Personal Preference:** Follow existing patterns
- **Explicit > Implicit:** Be clear about intentions
- **Composition > Inheritance:** Prefer composition patterns

## Git Conventions

### Branch Naming
- `feature/[ticket-id]-brief-description`
- `bugfix/[ticket-id]-brief-description`
- `hotfix/brief-description`
- `chore/brief-description`

### Commit Messages
Follow [Conventional Commits](https://www.conventionalcommits.org/):

```
<type>(<scope>): <subject>

<body>

<footer>
```

**Types:**
- `feat:` New feature
- `fix:` Bug fix
- `docs:` Documentation changes
- `style:` Code style changes (formatting, semicolons, etc)
- `refactor:` Code refactoring
- `perf:` Performance improvements
- `test:` Test additions or fixes
- `chore:` Maintenance tasks
- `ci:` CI/CD changes

**Examples:**
```
feat(auth): add OAuth2 login support

Implemented Google and GitHub OAuth providers with proper
token refresh mechanism.

Closes #123
```

### Pull Request Template
```markdown
## Description
Brief description of changes

## Type of Change
- [ ] Bug fix
- [ ] New feature
- [ ] Breaking change
- [ ] Documentation update

## Testing
- [ ] Unit tests pass
- [ ] Integration tests pass
- [ ] Manual testing completed

## Checklist
- [ ] Code follows project conventions
- [ ] Self-review completed
- [ ] Documentation updated
- [ ] No console.logs left
```

### Test Coverage Requirements
- Minimum overall: [80%]
- Critical paths: [100%]
- New code: [90%]

## Documentation Standards

### README Structure
1. Project title & description
2. Quick start
3. Prerequisites
4. Installation
5. Usage examples
6. API documentation
7. Contributing guidelines
8. License

## Error Handling

### Standard Error Format
- TODO: create standard error format

### Error Codes
- `AUTH_*` - Authentication errors
- `VALID_*` - Validation errors
- `DB_*` - Database errors
- `API_*` - External API errors
- `SYS_*` - System errors

## Performance Guidelines

### Bundle Size
- Max initial load: [200KB]
- Max lazy chunk: [100KB]
- Use code splitting for routes

### API Response Times
- Target p50: [200ms]
- Target p95: [500ms]
- Target p99: [1000ms]

### Optimization Checklist
- [ ] Images optimized and lazy loaded
- [ ] Code split at route level
- [ ] API calls debounced/throttled
- [ ] Memoization used appropriately
- [ ] Virtual scrolling for long lists

## Security Guidelines

### Never Commit
- API keys
- Passwords
- Private certificates
- PII data
- Internal URLs

### Always Do
- Sanitize user inputs
- Use parameterized queries
- Implement rate limiting
- Validate on both client and server
- Use HTTPS everywhere
- Keep dependencies updated

## Accessibility Standards

### Minimum Requirements
- WCAG 2.1 Level AA compliance
- Keyboard navigation support
- Screen reader compatibility
- Color contrast ratios (4.5:1 normal, 3:1 large text)
- Focus indicators visible

### Testing Tools
- axe DevTools
- WAVE
- Lighthouse
- Screen readers (NVDA/JAWS/VoiceOver)

---
*Last Updated: [Date]*
*Version: 1.0*
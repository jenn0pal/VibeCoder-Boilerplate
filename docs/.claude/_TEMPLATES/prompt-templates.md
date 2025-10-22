# Claude Prompt Templates

## Quick Reference
Use these templates to get consistent, high-quality responses from Claude for common development tasks.

---

## 🚀 Project Initialization

### New Project Setup
```
I'm starting a new [PROJECT TYPE] project using [TECHNOLOGY STACK].

Project Requirements:
- [Requirement 1]
- [Requirement 2]
- [Requirement 3]

Please help me:
1. Set up the project structure following best practices
2. Configure the development environment with modern tooling
3. Create initial configuration files
4. Set up testing framework
5. Provide a README template

Use [SPECIFIC CONVENTIONS/STANDARDS] for this project.
```

### Project Analysis
```
I'm joining an existing project. Here's the context:
- Project overview: [paste/upload project-overview.md]
- Tech stack: [paste/upload tech-stack.md]
- Current structure: [output of 'tree -L 3' or directory listing]

Please:
1. Analyze the project architecture
2. Identify the coding patterns used
3. Explain the key components and their relationships
4. Highlight any potential issues or improvements
5. Suggest my first steps to contribute effectively
```

---

## 🔨 Feature Development

### Feature Planning
```
I need to implement [FEATURE NAME] for [PROJECT NAME].

Context:
- Current system: [Brief description of existing functionality]
- User story: As a [role], I want [capability], so that [benefit]
- Constraints: [Technical or business constraints]

Please create:
1. A detailed implementation plan with phases
2. List of components/files to create or modify
3. Data model changes required
4. API endpoints needed
5. Test scenarios to cover
6. Potential edge cases and error handling
```

### API Endpoint Creation
```
Create a [REST/GraphQL] API endpoint for [FUNCTIONALITY].

Requirements:
- Method: [GET/POST/PUT/DELETE]
- Path: [/api/resource]
- Authentication: [Required/Optional/None]
- Input: [Describe expected parameters/payload]
- Output: [Describe response format]
- Business logic: [What should happen]

Include:
1. Controller/Handler implementation
2. Input validation
3. Error handling
4. Unit tests
5. Integration tests
6. API documentation
```

### Database Design
```
Design a database schema for [FEATURE/ENTITY].

Requirements:
- Entities involved: [List entities]
- Relationships: [Describe relationships]
- Key operations: [CRUD operations, queries needed]
- Performance considerations: [Expected volume, query patterns]
- Constraints: [Business rules, data integrity]

Provide:
1. Entity relationship diagram description
2. Table schemas with columns and types
3. Indexes for optimization
4. Migration files
5. Sample queries for common operations
```

---

## 🐛 Debugging & Problem Solving

### Bug Investigation
```
I'm experiencing [DESCRIBE THE ISSUE].

Context:
- Expected behavior: [What should happen]
- Actual behavior: [What is happening]
- Error message: [Exact error if any]
- Steps to reproduce: [How to trigger the issue]
- Environment: [Dev/Staging/Production, versions]
- Recent changes: [What changed recently]

Code involved:
[Paste relevant code snippets]

Please:
1. Analyze potential causes
2. Suggest debugging steps
3. Provide fix recommendations
4. Explain why this might be happening
5. Suggest preventive measures
```

### Performance Optimization
```
I need to optimize [COMPONENT/QUERY/FUNCTION] for better performance.

Current situation:
- Performance metric: [Current speed/memory usage]
- Target: [Desired improvement]
- Bottleneck: [If known]
- Scale: [Data volume, user count]

Current implementation:
[Paste code]

Please:
1. Identify performance issues
2. Suggest optimizations with explanations
3. Provide optimized code
4. Recommend monitoring approaches
5. Suggest caching strategies if applicable
```

---

## ♻️ Refactoring

### Code Refactoring
```
Refactor this code to improve [readability/maintainability/performance/testability].

Current code:
[Paste code to refactor]

Goals:
- [Specific improvement goal 1]
- [Specific improvement goal 2]

Constraints:
- Must maintain backward compatibility: [Yes/No]
- Testing requirements: [Unit tests, integration tests]
- Framework/library constraints: [Any specific requirements]

Please:
1. Analyze current code issues
2. Provide refactored version
3. Explain each significant change
4. Include any necessary tests
5. Document migration steps if needed
```

### Architecture Refactoring
```
I need to refactor [COMPONENT/MODULE] from [CURRENT PATTERN] to [TARGET PATTERN].

Current architecture:
[Describe or paste current structure]

Target architecture goals:
- Pattern: [MVC, Repository, Service Layer, etc.]
- Objectives: [Scalability, testability, separation of concerns]

Please provide:
1. Step-by-step migration plan
2. New structure layout
3. Code examples for key components
4. How to handle the transition period
5. Testing strategy during refactoring
```

---

## 📝 Code Review

### Review Request
```
Please review this code for [specific concerns or general review].

Code to review:
[Paste code]

Context:
- Purpose: [What this code does]
- PR/Ticket: [Reference if available]
- Specific concerns: [Performance, security, patterns, etc.]

Review checklist:
1. Code quality and readability
2. Performance implications
3. Security vulnerabilities
4. Error handling
5. Test coverage
6. Documentation needs
7. Adherence to project conventions
```

### Security Audit
```
Perform a security audit on this [code/configuration/API].

Code/Configuration:
[Paste relevant content]

Environment:
- Type: [Web app, API, Mobile backend]
- Sensitivity: [Public, Internal, Confidential]
- Compliance: [GDPR, HIPAA, PCI-DSS requirements]

Check for:
1. Input validation issues
2. Authentication/Authorization flaws
3. Data exposure risks
4. Injection vulnerabilities
5. Configuration weaknesses
6. Dependency vulnerabilities
7. Best practice violations
```

---

## 🧪 Testing

### Test Creation
```
Create tests for [COMPONENT/FUNCTION/CLASS].

Code to test:
[Paste code]

Requirements:
- Testing framework: [Jest, Pytest, PHPUnit, etc.]
- Coverage target: [Percentage]
- Test types: [Unit, Integration, E2E]

Include tests for:
1. Happy path scenarios
2. Edge cases
3. Error conditions
4. Boundary values
5. Performance requirements (if applicable)
```

### Test Debugging
```
My test is failing and I need help fixing it.

Test code:
[Paste test]

Implementation code:
[Paste code being tested]

Error/Failure:
[Paste error message or failure details]

Expected vs Actual:
- Expected: [What should happen]
- Actual: [What is happening]

Please:
1. Identify why the test is failing
2. Determine if it's a test issue or implementation issue
3. Provide the fix
4. Suggest additional test cases if needed
```

---

## 📚 Documentation

### API Documentation
```
Generate API documentation for [SERVICE/ENDPOINT].

API Details:
- Base URL: [URL]
- Authentication: [Method]
- Endpoints: [List or paste code]

Documentation should include:
1. Overview and purpose
2. Authentication details
3. Request/response formats
4. Status codes and errors
5. Rate limiting info
6. Example requests (cURL, JavaScript, Python)
7. SDKs or client libraries available
```

### README Creation
```
Create a comprehensive README for [PROJECT NAME].

Project details:
- Purpose: [What it does]
- Tech stack: [Technologies used]
- Target audience: [Who will use this]
- Key features: [Main functionality]

Include sections for:
1. Project overview
2. Features
3. Installation
4. Configuration
5. Usage examples
6. API reference (if applicable)
7. Contributing guidelines
8. Testing
9. Deployment
10. License
```

---

## 🔄 Migration & Upgrade

### Version Upgrade
```
Help me upgrade [PACKAGE/FRAMEWORK] from version [CURRENT] to [TARGET].

Current setup:
- Dependencies: [List key dependencies]
- Custom modifications: [Any customizations]
- Breaking changes concern: [Known issues]

Please provide:
1. Pre-upgrade checklist
2. Step-by-step upgrade process
3. Code changes required
4. Configuration updates
5. Testing plan
6. Rollback strategy
```

### Database Migration
```
Create a database migration to [DESCRIBE CHANGE].

Current schema:
[Paste current table structure]

Required changes:
- [Change 1]
- [Change 2]

Considerations:
- Data volume: [Number of records]
- Downtime tolerance: [Zero/Minimal/Acceptable]
- Rollback requirements: [Yes/No]

Provide:
1. Migration up script
2. Migration down script
3. Data transformation logic (if needed)
4. Performance considerations
5. Testing approach
```

---

## 🤖 AI & Automation

### Automation Script
```
Create a script to automate [TASK DESCRIPTION].

Requirements:
- Language: [Python/Bash/Node.js/etc.]
- Trigger: [Manual/Scheduled/Event-based]
- Input: [Data sources, parameters]
- Output: [Expected results]
- Error handling: [How to handle failures]

The script should:
1. [Step 1]
2. [Step 2]
3. [Step 3]

Include logging and error notifications.
```

### CI/CD Pipeline
```
Set up a CI/CD pipeline for [PROJECT TYPE].

Requirements:
- Platform: [GitHub Actions/GitLab CI/Jenkins/etc.]
- Environments: [Dev/Staging/Production]
- Steps needed: [Build, Test, Deploy]
- Secrets management: [How to handle]
- Notification: [Slack/Email/etc.]

Pipeline should:
1. Run on [trigger conditions]
2. Execute [test types]
3. Build [artifacts]
4. Deploy to [environments]
5. Notify [stakeholders]
```

---

## 💡 Learning & Exploration

### Technology Exploration
```
Explain [TECHNOLOGY/CONCEPT] and how to use it in [CONTEXT].

Background:
- My experience level: [Beginner/Intermediate/Advanced]
- Current stack: [What I'm using now]
- Use case: [What I want to achieve]

Please provide:
1. Conceptual explanation
2. How it compares to [ALTERNATIVE]
3. Simple example
4. Real-world use case
5. Best practices
6. Common pitfalls
7. Resources for deeper learning
```

### Code Explanation
```
Explain this code in detail:

[Paste code]

Questions:
1. What does each part do?
2. Why is it written this way?
3. What design patterns are used?
4. Are there any potential issues?
5. How would you improve it?
6. What are the performance implications?
```

---

## 🎯 Project-Specific Templates

### Convention Check
```
Check if this code follows our project conventions:

Conventions reference: [paste conventions.md or key rules]

Code to check:
[Paste code]

Verify:
1. Naming conventions
2. File organization
3. Code style
4. Documentation standards
5. Testing requirements
6. Git commit format
```

### Feature Completion Checklist
```
I've completed implementing [FEATURE]. Please verify completeness:

Implementation includes:
- [ ] Core functionality
- [ ] Error handling
- [ ] Input validation
- [ ] Unit tests
- [ ] Integration tests
- [ ] Documentation
- [ ] API documentation (if applicable)
- [ ] Database migrations (if applicable)
- [ ] Configuration updates
- [ ] Logging

Code references:
[List files changed]

Please review and suggest any missing components.
```

---

## 📊 Analysis & Reporting

### Code Complexity Analysis
```
Analyze the complexity of [MODULE/COMPONENT].

Code location: [Path or paste code]

Analyze:
1. Cyclomatic complexity
2. Coupling and cohesion
3. Code duplication
4. Maintainability index
5. Test coverage gaps
6. Potential refactoring targets

Provide improvement recommendations prioritized by impact.
```

### Technical Debt Assessment
```
Assess technical debt in [COMPONENT/PROJECT].

Current issues:
- [Known issue 1]
- [Known issue 2]

Review areas:
1. Code quality issues
2. Missing tests
3. Outdated dependencies
4. Documentation gaps
5. Performance bottlenecks
6. Security vulnerabilities

Provide:
- Debt inventory with severity
- Impact analysis
- Remediation plan with priorities
- Effort estimates
```

---

## 🔧 Custom Prompts

### Template for New Prompts
```
[TASK DESCRIPTION]

Context:
- [Relevant context]
- [Constraints]
- [Requirements]

Input:
[What you're providing]

Expected Output:
1. [Output requirement 1]
2. [Output requirement 2]
3. [Output requirement 3]

Additional Considerations:
- [Special requirements]
- [Quality criteria]
- [Format preferences]
```

### Prompt Improvement Request
```
Improve this prompt for better results:

Current prompt:
[Paste prompt]

Issues experienced:
- [Issue 1]
- [Issue 2]

Desired improvements:
- [Goal 1]
- [Goal 2]

Please provide an optimized version with explanation of changes.
```

---

## Usage Tips

1. **Be Specific**: Replace placeholders with actual details
2. **Provide Context**: Include relevant code, errors, and requirements
3. **State Constraints**: Mention framework versions, conventions, limitations
4. **Define Success**: Clear about what constitutes a good solution
5. **Iterate**: Use follow-up questions to refine responses

## Quick Copy Format

For frequently used prompts, keep a shortened version:

```
Quick Debug: "Debug this error: [ERROR]. Code: [CODE]. Expected: [EXPECTED]. Actual: [ACTUAL]."

Quick Review: "Review for [quality/security/performance]: [CODE]"

Quick Test: "Write [unit/integration] tests for: [CODE] using [FRAMEWORK]"

Quick Explain: "Explain how this works: [CODE]. Focus on [ASPECT]."
```

---
*Last Updated: [Date]*
*Version: 1.0*
# Python Dependency Upgrade: [Package Name]

> **Template for upgrading Python packages using uv or pip**

## Overview

**Upgrade ID:** DEP-[ID]
**Date:** [YYYY-MM-DD]
**Package Name:** [package-name]
**Package Manager:** uv (primary) / pip (fallback)
**Current Version:** [X.Y.Z]
**Target Version:** [A.B.C]
**Upgrade Type:** [Major/Minor/Patch]
**Priority:** [Critical/High/Medium/Low]

## Motivation

### Why Upgrade?
- [ ] Security vulnerability (CVE-[ID])
- [ ] Bug fix needed
- [ ] New feature required
- [ ] Python version compatibility (e.g., Python 3.12 support)
- [ ] Performance improvement
- [ ] Deprecation warning
- [ ] Other: [Specify]

### Security Information
**CVE ID:** [CVE-YYYY-XXXXX] (if applicable)
**Severity:** [Critical/High/Medium/Low]
**Advisory URL:** [Link to PyPA advisory or package security page]

## Package Information

### Package Details
**PyPI Link:** https://pypi.org/project/[package-name]/
**Documentation:** [Link to docs]
**Changelog:** [Link to changelog]
**License:** [MIT/Apache/BSD/etc.]

### Our Usage
**Used In:**
- [Module 1]
- [Module 2]

**Import Locations:**
```bash
# Find all imports
grep -r "from [package-name]" src/
grep -r "import [package-name]" src/
```

## Upgrade Process (uv)

### 1. Check Current Version
```bash
uv pip list | grep [package-name]
```

### 2. Review Changes
```bash
# Visit PyPI changelog
open https://pypi.org/project/[package-name]/[target-version]/
```

### 3. Update Package
```bash
# Update specific package
uv add [package-name]==[target-version]

# Or update to latest
uv add --upgrade [package-name]

# Lock dependencies
uv lock
```

### 4. Verify Installation
```bash
uv pip show [package-name]
uv run python -c "import [package_name]; print([package_name].__version__)"
```

### 5. Run Tests
```bash
# Run full test suite
uv run pytest

# Run specific tests
uv run pytest tests/test_[affected].py

# With coverage
uv run pytest --cov=src --cov-report=html
```

### 6. Check Type Hints
```bash
uv run mypy src/
```

### 7. Lint & Format
```bash
ruff check --fix .
ruff format .
```

## Fallback Process (pip)

### If uv fails or unavailable
```bash
# Activate virtual environment
source .venv/bin/activate

# Upgrade package
pip install --upgrade [package-name]==[target-version]

# Update requirements
pip freeze > requirements.txt

# Test
pytest
```

## Breaking Changes

### API Changes
```python
# Before (old version)
from [package] import old_function
result = old_function(arg1, arg2)

# After (new version)
from [package] import new_function
result = new_function(arg1=arg1, arg2=arg2)
```

## Dependency Conflicts

### Check for conflicts
```bash
uv lock
# Review any conflicts in output
```

### Common Resolutions
- Update conflicting packages together
- Pin intermediate versions
- Check for compatibility matrix

## Rollback Plan

### If upgrade fails
```bash
# Revert to previous version
uv add [package-name]==[old-version]
uv lock

# Or restore from lock file
git checkout uv.lock
uv sync
```

## Testing Checklist

- [ ] Unit tests pass
- [ ] Integration tests pass
- [ ] Type checking passes (mypy)
- [ ] Linting passes (ruff)
- [ ] No new deprecation warnings
- [ ] Performance benchmarks stable
- [ ] Documentation updated (if API changes)

## Post-Upgrade Tasks

- [ ] Update pyproject.toml if needed
- [ ] Update type stubs if available
- [ ] Commit changes
- [ ] Update CHANGELOG.md
- [ ] Create PR with upgrade details

---
*Package Manager: uv*
*Python Version: 3.11+*

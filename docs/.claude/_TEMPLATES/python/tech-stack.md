# Python Technology Stack

## Core Technologies

### Python Runtime
| Technology | Version | Purpose | Documentation |
|------------|---------|---------|---------------|
| Python | 3.11+ | Runtime environment | https://docs.python.org/3/ |
| uv | Latest | Package manager & virtual environment | https://github.com/astral-sh/uv |

### Package Management
| Technology | Version | Purpose | Documentation |
|------------|---------|---------|---------------|
| uv | Latest | Fast Python package installer | https://github.com/astral-sh/uv |
| pip | Latest (fallback) | Python package installer | https://pip.pypa.io/ |

### Code Quality Tools
| Technology | Version | Purpose | Documentation |
|------------|---------|---------|---------------|
| ruff | 0.5.0+ | Linter & formatter (replaces black, isort, flake8) | https://docs.astral.sh/ruff/ |
| mypy | 1.10.0+ | Static type checker | https://mypy.readthedocs.io/ |
| pytest | 8.0.0+ | Testing framework | https://docs.pytest.org/ |
| pytest-cov | 5.0.0+ | Coverage plugin | https://pytest-cov.readthedocs.io/ |

## Development Tools

### Build Tools
- **Package Builder:** hatchling - Modern Python packaging
- **Lock File:** uv.lock - Dependency resolution and locking
- **Configuration:** pyproject.toml - Unified project configuration

### Code Quality
- **Linter:** ruff - Fast Python linter in Rust
- **Formatter:** ruff format - Fast Python formatter
- **Type Checker:** mypy - Static type checking
- **Import Sorter:** ruff (built-in) - Automatic import organization

### Testing
- **Unit Testing:** pytest - Python testing framework
- **Integration Testing:** pytest with fixtures
- **Coverage Tool:** pytest-cov with coverage.py
- **Test Runner:** pytest with pytest-xdist for parallel execution

## Package Management

### Primary Package Manager
- **Tool:** uv (primary), pip (fallback)
- **Lock File:** uv.lock
- **Registry:** PyPI (https://pypi.org/)

### Common Commands
```bash
# Install dependencies
uv sync

# Add package
uv add package-name

# Add dev dependency
uv add --dev package-name

# Update packages
uv lock --upgrade

# Run Python
uv run python script.py

# Run tests
uv run pytest
```

### Key Dependencies (Examples)
| Package | Purpose | Documentation |
|---------|---------|---------------|
| requests | HTTP client | https://requests.readthedocs.io/ |
| pydantic | Data validation | https://docs.pydantic.dev/ |
| httpx | Async HTTP client | https://www.python-httpx.org/ |
| sqlalchemy | Database ORM | https://www.sqlalchemy.org/ |
| click | CLI framework | https://click.palletsprojects.com/ |

## Version Requirements

### Runtime Versions
- **Python:** 3.11 or higher (recommended: 3.12)
- **uv:** Latest stable
- **pip:** 23.0+ (if using pip)

### Python Language Features Used
- Type hints (PEP 484)
- Dataclasses (PEP 557)
- Pattern matching (PEP 634 - Python 3.10+)
- Union types with `|` (PEP 604 - Python 3.10+)
- Structural pattern matching (Python 3.10+)

## Performance Targets

### Application Metrics
- **Startup Time:** < 2s
- **Test Suite:** < 30s for full run
- **Import Time:** < 500ms

## Configuration Files

### pyproject.toml Structure
```toml
[project]
name = "project-name"
version = "0.1.0"
requires-python = ">=3.11"
dependencies = [...]

[tool.uv]
dev-dependencies = [...]

[tool.ruff]
line-length = 88
target-version = "py311"

[tool.ruff.lint]
select = ["E", "F", "I", "B", "N", "UP", "SIM", "S", "C90", "RUF"]

[tool.pytest.ini_options]
testpaths = ["tests"]
python_files = ["test_*.py", "*_test.py"]

[tool.mypy]
python_version = "3.11"
strict = true
```

### .python-version
```
3.11.9
```

---
*Last Updated: 2025*
*Python Version: 3.11+*
*Package Manager: uv*
*Code Quality: ruff + mypy*

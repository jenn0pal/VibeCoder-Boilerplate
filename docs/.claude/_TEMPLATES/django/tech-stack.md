# Django Technology Stack

## Core Technologies

### Framework
| Technology | Version | Purpose | Documentation |
|------------|---------|---------|---------------|
| Django | 5.0+ | Web framework | https://docs.djangoproject.com/ |
| Python | 3.11+ | Runtime environment | https://docs.python.org/3/ |
| uv | Latest | Package manager | https://github.com/astral-sh/uv |

### Django Ecosystem
| Technology | Version | Purpose | Documentation |
|------------|---------|---------|---------------|
| Django REST Framework | 3.14+ | API development | https://www.django-rest-framework.org/ |
| django-cors-headers | 4.3+ | CORS handling | https://github.com/adamchainz/django-cors-headers |
| python-decouple | 3.8+ | Environment config | https://github.com/HBNetwork/python-decouple |
| whitenoise | 6.6+ | Static file serving | https://whitenoise.readthedocs.io/ |

### Database
| Technology | Version | Purpose | Documentation |
|------------|---------|---------|---------------|
| PostgreSQL | 14+ | Primary database | https://www.postgresql.org/docs/ |
| psycopg | 3.1+ | PostgreSQL adapter | https://www.psycopg.org/psycopg3/ |
| Redis | 5.0+ | Caching & sessions | https://redis.io/docs/ |

### Task Queue
| Technology | Version | Purpose | Documentation |
|------------|---------|---------|---------------|
| Celery | 5.3+ | Async task processing | https://docs.celeryq.dev/ |
| Redis | 5.0+ | Message broker | https://redis.io/docs/ |

## Development Tools

### Code Quality
| Technology | Version | Purpose | Documentation |
|------------|---------|---------|---------------|
| ruff | 0.5.0+ | Linter & formatter | https://docs.astral.sh/ruff/ |
| mypy | 1.10.0+ | Type checking | https://mypy.readthedocs.io/ |
| django-stubs | 4.2.7+ | Django type stubs | https://github.com/typeddjango/django-stubs |

### Testing
| Technology | Version | Purpose | Documentation |
|------------|---------|---------|---------------|
| pytest | 7.4+ | Test framework | https://docs.pytest.org/ |
| pytest-django | 4.7+ | Django test integration | https://pytest-django.readthedocs.io/ |
| pytest-cov | 4.1+ | Coverage | https://pytest-cov.readthedocs.io/ |
| factory-boy | 3.3+ | Test fixtures | https://factoryboy.readthedocs.io/ |
| faker | 20.1+ | Fake data generation | https://faker.readthedocs.io/ |

### Development
| Technology | Version | Purpose | Documentation |
|------------|---------|---------|---------------|
| django-debug-toolbar | 4.2+ | Debug panel | https://django-debug-toolbar.readthedocs.io/ |
| django-extensions | 3.2+ | Extra management commands | https://django-extensions.readthedocs.io/ |
| ipython | 8.17+ | Enhanced shell | https://ipython.readthedocs.io/ |

## Package Management

### Primary Package Manager
- **Tool:** uv (primary), pip (fallback)
- **Lock File:** uv.lock
- **Configuration:** pyproject.toml

### Common Commands
```bash
# Initial setup
uv init
uv add django djangorestframework

# Add dev dependencies
uv add --dev pytest pytest-django ruff mypy django-stubs

# Run Django commands
uv run python manage.py runserver
uv run python manage.py migrate
uv run python manage.py createsuperuser

# Run tests
uv run pytest
uv run pytest --cov=apps

# Code quality
ruff check --fix .
ruff format .
uv run mypy apps/
```

## Project Structure

### Django Settings
- **Settings Module:** config/settings/
  - base.py - Base settings
  - development.py - Development settings
  - staging.py - Staging settings
  - production.py - Production settings

### Apps Organization
```
apps/
├── core/          # Core functionality
├── users/         # User management
├── api/           # API endpoints
└── common/        # Shared utilities
```

## Database Configuration

### PostgreSQL
```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': config('DB_NAME'),
        'USER': config('DB_USER'),
        'PASSWORD': config('DB_PASSWORD'),
        'HOST': config('DB_HOST', default='localhost'),
        'PORT': config('DB_PORT', default='5432'),
        'ATOMIC_REQUESTS': True,
        'CONN_MAX_AGE': 60,
    }
}
```

### Redis Cache
```python
CACHES = {
    'default': {
        'BACKEND': 'django.core.cache.backends.redis.RedisCache',
        'LOCATION': config('REDIS_URL', default='redis://127.0.0.1:6379/1'),
    }
}
```

## Deployment

### WSGI Server
- **Server:** gunicorn 21.2+
- **Workers:** (2 × CPU cores) + 1
- **Timeout:** 30s

### Static Files
- **Handler:** whitenoise
- **Storage:** CompressedManifestStaticFilesStorage
- **Location:** staticfiles/

## Security Configuration

### Required Settings
```python
# Production
DEBUG = False
SECRET_KEY = config('SECRET_KEY')
ALLOWED_HOSTS = config('ALLOWED_HOSTS', cast=Csv())

# Security Headers
SECURE_SSL_REDIRECT = True
SESSION_COOKIE_SECURE = True
CSRF_COOKIE_SECURE = True
SECURE_BROWSER_XSS_FILTER = True
SECURE_CONTENT_TYPE_NOSNIFF = True
X_FRAME_OPTIONS = 'DENY'
SECURE_HSTS_SECONDS = 31536000
```

## Environment Variables

### Required
| Variable | Purpose | Example |
|----------|---------|---------|
| SECRET_KEY | Django secret key | Random 50+ chars |
| DATABASE_URL | Database connection | postgresql://... |
| REDIS_URL | Cache connection | redis://... |
| ALLOWED_HOSTS | Allowed domains | example.com,www.example.com |

### Optional
| Variable | Purpose | Default |
|----------|---------|---------|
| DEBUG | Debug mode | False |
| DB_HOST | Database host | localhost |
| DB_PORT | Database port | 5432 |

## Performance Targets

### Response Times
- **HTML Pages:** < 200ms (p95)
- **API Endpoints:** < 100ms (p95)
- **Database Queries:** < 50ms (p95)

### Scalability
- **Concurrent Users:** 1000+
- **Requests/Second:** 100+

---
*Last Updated: 2025*
*Django Version: 5.0+*
*Python Version: 3.11+*
*Package Manager: uv*

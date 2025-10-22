# Django Project Conventions

## Project Setup with uv

### Initialize Django Project
```bash
# Create new project directory
mkdir my-django-project && cd my-django-project

# Initialize uv project
uv init

# Add Django and essential dependencies
uv add django djangorestframework django-cors-headers python-decouple

# Add development dependencies
uv add --dev ruff mypy django-stubs pytest pytest-django pytest-cov django-debug-toolbar

# Create Django project
uv run django-admin startproject config .

# Create your first app
uv run python manage.py startapp core
```

## Project Structure

### Standard Django Layout
```
project/
├── config/                 # Project configuration
│   ├── __init__.py
│   ├── settings/
│   │   ├── __init__.py
│   │   ├── base.py       # Base settings
│   │   ├── development.py # Dev settings
│   │   ├── staging.py    # Staging settings
│   │   └── production.py # Production settings
│   ├── urls.py
│   ├── wsgi.py
│   └── asgi.py
├── apps/                   # Django applications
│   ├── core/              # Core app
│   │   ├── migrations/
│   │   ├── management/
│   │   │   └── commands/
│   │   ├── models.py
│   │   ├── views.py
│   │   ├── serializers.py
│   │   ├── urls.py
│   │   ├── admin.py
│   │   ├── apps.py
│   │   └── tests/
│   ├── users/             # User management
│   ├── api/               # API endpoints
│   └── common/            # Shared utilities
├── static/                # Static files
├── media/                 # User uploads
├── templates/             # HTML templates
│   ├── base.html
│   └── includes/
├── locale/                # Translations
├── tests/                 # Project-wide tests
│   ├── unit/
│   ├── integration/
│   └── fixtures/
├── scripts/               # Management scripts
├── requirements/          # For legacy compatibility
│   ├── base.txt
│   ├── development.txt
│   └── production.txt
├── .env.example
├── .python-version        # Python version for uv
├── pyproject.toml        # Project configuration
├── uv.lock              # Lock file from uv
├── manage.py
└── README.md
```

## Modern Python Configuration

### pyproject.toml (with uv and ruff)
```toml
[project]
name = "django-project"
version = "0.1.0"
description = "Django project with modern tooling"
readme = "README.md"
requires-python = ">=3.11"
dependencies = [
    "django>=5.0",
    "djangorestframework>=3.14",
    "django-cors-headers>=4.3",
    "python-decouple>=3.8",
    "psycopg[binary]>=3.1",
    "redis>=5.0",
    "celery>=5.3",
    "gunicorn>=21.2",
    "whitenoise>=6.6",
    "pillow>=10.1",
]

[project.optional-dependencies]
dev = [
    "django-debug-toolbar>=4.2",
    "django-extensions>=3.2",
    "ipython>=8.17",
    "werkzeug>=3.0",
]
test = [
    "pytest>=7.4",
    "pytest-django>=4.7",
    "pytest-cov>=4.1",
    "pytest-xdist>=3.5",
    "factory-boy>=3.3",
    "faker>=20.1",
]

[build-system]
requires = ["hatchling"]
build-backend = "hatchling.build"

[tool.uv]
dev-dependencies = [
    "ruff>=0.5.0",
    "mypy>=1.10.0",
    "django-stubs[compatible-mypy]>=4.2.7",
    "djangorestframework-stubs>=3.14.5",
    "pre-commit>=3.6.0",
]

# Ruff Configuration
[tool.ruff]
exclude = [
    ".git",
    ".venv",
    "venv",
    "__pycache__",
    ".mypy_cache",
    ".pytest_cache",
    ".ruff_cache",
    "migrations",
    "static",
    "media",
]
line-length = 88
indent-width = 4
target-version = "py311"

[tool.ruff.lint]
select = [
    "E",    # pycodestyle errors
    "W",    # pycodestyle warnings
    "F",    # pyflakes
    "I",    # isort
    "B",    # flake8-bugbear
    "C4",   # flake8-comprehensions
    "UP",   # pyupgrade
    "DJ",   # flake8-django
    "N",    # pep8-naming
    "PIE",  # flake8-pie
    "T20",  # flake8-print
    "RUF",  # Ruff-specific rules
    "SIM",  # flake8-simplify
    "PTH",  # flake8-use-pathlib
    "S",    # flake8-bandit (security)
]
ignore = [
    "E501",   # line too long (formatter handles this)
    "B008",   # do not perform function calls in argument defaults
    "S101",   # use of assert (needed in tests)
    "DJ001",  # null=True on string fields (sometimes needed)
]
fixable = ["ALL"]
unfixable = []

[tool.ruff.lint.per-file-ignores]
"__init__.py" = ["F401", "F403"]
"*/tests/*" = ["S101", "S106"]
"*/migrations/*" = ["E501", "N806"]
"*/settings/*" = ["F403", "F405"]

[tool.ruff.lint.isort]
known-first-party = ["apps", "config"]
section-order = [
    "future",
    "standard-library",
    "django",
    "third-party",
    "first-party",
    "local-folder",
]

[tool.ruff.lint.isort.sections]
"django" = ["django"]

[tool.ruff.format]
quote-style = "double"
indent-style = "space"
skip-magic-trailing-comma = false
line-ending = "lf"
docstring-code-format = true

# Django-specific Ruff configuration
[tool.ruff.lint.flake8-django]
django-settings-module = "config.settings.development"

# MyPy Configuration
[tool.mypy]
python_version = "3.11"
plugins = ["mypy_django_plugin.main", "mypy_drf_plugin.main"]
strict = true
warn_return_any = true
warn_unused_configs = true
ignore_missing_imports = true

[tool.django-stubs]
django_settings_module = "config.settings.development"

# Pytest Configuration
[tool.pytest.ini_options]
DJANGO_SETTINGS_MODULE = "config.settings.test"
python_files = ["test_*.py", "*_test.py", "tests.py"]
addopts = [
    "-ra",
    "--strict-markers",
    "--reuse-db",
    "--nomigrations",
    "--cov=apps",
    "--cov-report=term-missing:skip-covered",
    "--cov-report=html",
    "--cov-report=xml",
]
testpaths = ["tests", "apps"]
markers = [
    "slow: marks tests as slow",
    "unit: marks tests as unit tests",
    "integration: marks tests as integration tests",
]

# Coverage Configuration
[tool.coverage.run]
source = ["apps"]
omit = [
    "*/migrations/*",
    "*/tests/*",
    "*/admin.py",
    "*/apps.py",
    "__pycache__",
    "*/management/commands/*",
]

[tool.coverage.report]
precision = 2
show_missing = true
skip_covered = true
```

## Django Code Style

### Models
```python
"""User models following Django best practices."""
from django.contrib.auth.models import AbstractUser
from django.db import models
from django.urls import reverse
from django.utils.translation import gettext_lazy as _


class TimeStampedModel(models.Model):
    """Abstract base model with created and modified timestamps."""

    created_at = models.DateTimeField(
        _("created at"),
        auto_now_add=True,
        help_text=_("Date and time when the record was created"),
    )
    modified_at = models.DateTimeField(
        _("modified at"),
        auto_now=True,
        help_text=_("Date and time when the record was last modified"),
    )

    class Meta:
        abstract = True
        ordering = ["-created_at"]


class User(AbstractUser):
    """Custom user model extending Django's AbstractUser."""

    email = models.EmailField(
        _("email address"),
        unique=True,
        error_messages={
            "unique": _("A user with that email already exists."),
        },
    )
    bio = models.TextField(
        _("biography"),
        max_length=500,
        blank=True,
        help_text=_("A short bio about the user"),
    )
    avatar = models.ImageField(
        _("avatar"),
        upload_to="avatars/",
        null=True,
        blank=True,
    )
    is_verified = models.BooleanField(
        _("email verified"),
        default=False,
        help_text=_("Designates whether the user has verified their email."),
    )

    USERNAME_FIELD = "email"
    REQUIRED_FIELDS = ["username"]

    class Meta:
        db_table = "users"
        verbose_name = _("user")
        verbose_name_plural = _("users")
        indexes = [
            models.Index(fields=["email"]),
            models.Index(fields=["-created_at"]),
        ]

    def __str__(self) -> str:
        return self.email

    def get_absolute_url(self) -> str:
        return reverse("users:detail", kwargs={"pk": self.pk})

    def get_full_name(self) -> str:
        """Return the full name of the user."""
        full_name = f"{self.first_name} {self.last_name}".strip()
        return full_name or self.username
```

### Views (Class-Based Views)
```python
"""Views for user management."""
from typing import Any

from django.contrib.auth.mixins import LoginRequiredMixin
from django.contrib.messages.views import SuccessMessageMixin
from django.db.models import QuerySet
from django.urls import reverse_lazy
from django.views.generic import (
    CreateView,
    DeleteView,
    DetailView,
    ListView,
    UpdateView,
)

from apps.users.forms import UserUpdateForm
from apps.users.models import User


class UserListView(LoginRequiredMixin, ListView):
    """List all users with pagination."""

    model = User
    paginate_by = 25
    template_name = "users/user_list.html"
    context_object_name = "users"

    def get_queryset(self) -> QuerySet[User]:
        """Return filtered queryset based on search query."""
        queryset = super().get_queryset()
        search = self.request.GET.get("search")

        if search:
            queryset = queryset.filter(
                models.Q(username__icontains=search)
                | models.Q(email__icontains=search)
                | models.Q(first_name__icontains=search)
                | models.Q(last_name__icontains=search)
            )

        return queryset.select_related("profile").prefetch_related("groups")


class UserDetailView(LoginRequiredMixin, DetailView):
    """Display user profile details."""

    model = User
    template_name = "users/user_detail.html"
    context_object_name = "user"

    def get_context_data(self, **kwargs: Any) -> dict[str, Any]:
        """Add additional context to the template."""
        context = super().get_context_data(**kwargs)
        context["is_owner"] = self.object == self.request.user
        context["recent_posts"] = self.object.posts.published()[:5]
        return context


class UserUpdateView(LoginRequiredMixin, SuccessMessageMixin, UpdateView):
    """Update user profile."""

    model = User
    form_class = UserUpdateForm
    template_name = "users/user_form.html"
    success_message = "Profile updated successfully!"

    def get_object(self, queryset: QuerySet[User] | None = None) -> User:
        """Return the current user."""
        return self.request.user

    def get_success_url(self) -> str:
        """Return the URL to redirect to after processing a valid form."""
        return reverse_lazy("users:detail", kwargs={"pk": self.object.pk})
```

### Django REST Framework Serializers
```python
"""Serializers for API endpoints."""
from typing import Any

from django.contrib.auth import authenticate
from django.contrib.auth.password_validation import validate_password
from rest_framework import serializers
from rest_framework.validators import UniqueValidator

from apps.users.models import User


class UserSerializer(serializers.ModelSerializer):
    """Serializer for User model."""

    email = serializers.EmailField(
        validators=[UniqueValidator(queryset=User.objects.all())]
    )
    full_name = serializers.CharField(source="get_full_name", read_only=True)
    posts_count = serializers.IntegerField(
        source="posts.count",
        read_only=True,
    )

    class Meta:
        model = User
        fields = [
            "id",
            "username",
            "email",
            "first_name",
            "last_name",
            "full_name",
            "bio",
            "avatar",
            "is_verified",
            "date_joined",
            "posts_count",
        ]
        read_only_fields = ["id", "date_joined", "is_verified"]


class UserCreateSerializer(serializers.ModelSerializer):
    """Serializer for user registration."""

    password = serializers.CharField(
        write_only=True,
        required=True,
        validators=[validate_password],
        style={"input_type": "password"},
    )
    password_confirm = serializers.CharField(
        write_only=True,
        required=True,
        style={"input_type": "password"},
    )

    class Meta:
        model = User
        fields = [
            "username",
            "email",
            "password",
            "password_confirm",
            "first_name",
            "last_name",
        ]

    def validate(self, attrs: dict[str, Any]) -> dict[str, Any]:
        """Validate password confirmation."""
        if attrs["password"] != attrs["password_confirm"]:
            raise serializers.ValidationError(
                {"password_confirm": "Password fields didn't match."}
            )
        return attrs

    def create(self, validated_data: dict[str, Any]) -> User:
        """Create a new user with encrypted password."""
        validated_data.pop("password_confirm")
        return User.objects.create_user(**validated_data)


class LoginSerializer(serializers.Serializer):
    """Serializer for user login."""

    email = serializers.EmailField(required=True)
    password = serializers.CharField(
        required=True,
        style={"input_type": "password"},
    )

    def validate(self, attrs: dict[str, Any]) -> dict[str, Any]:
        """Validate and authenticate user."""
        email = attrs.get("email")
        password = attrs.get("password")

        if email and password:
            user = authenticate(
                request=self.context.get("request"),
                username=email,
                password=password,
            )

            if not user:
                raise serializers.ValidationError(
                    "Unable to log in with provided credentials."
                )

            if not user.is_active:
                raise serializers.ValidationError("User account is disabled.")

            attrs["user"] = user
            return attrs

        raise serializers.ValidationError("Must include 'email' and 'password'.")
```

### API Views (Django REST Framework)
```python
"""API views for user management."""
from django.contrib.auth import login, logout
from rest_framework import generics, permissions, status
from rest_framework.decorators import action
from rest_framework.request import Request
from rest_framework.response import Response
from rest_framework.views import APIView
from rest_framework.viewsets import ModelViewSet

from apps.users.models import User
from apps.users.serializers import (
    LoginSerializer,
    UserCreateSerializer,
    UserSerializer,
)


class UserViewSet(ModelViewSet):
    """ViewSet for User model with custom actions."""

    queryset = User.objects.all()
    serializer_class = UserSerializer
    permission_classes = [permissions.IsAuthenticatedOrReadOnly]
    lookup_field = "username"

    def get_queryset(self):
        """Optimize queryset with select_related and prefetch_related."""
        return (
            super()
            .get_queryset()
            .select_related("profile")
            .prefetch_related("posts", "groups")
        )

    def get_serializer_class(self):
        """Return appropriate serializer class based on action."""
        if self.action == "create":
            return UserCreateSerializer
        return UserSerializer

    @action(detail=False, methods=["get"], permission_classes=[permissions.IsAuthenticated])
    def me(self, request: Request) -> Response:
        """Return the current user's data."""
        serializer = self.get_serializer(request.user)
        return Response(serializer.data)

    @action(detail=True, methods=["post"])
    def follow(self, request: Request, username: str = None) -> Response:
        """Follow a user."""
        user_to_follow = self.get_object()

        if user_to_follow == request.user:
            return Response(
                {"error": "You cannot follow yourself."},
                status=status.HTTP_400_BAD_REQUEST,
            )

        request.user.following.add(user_to_follow)
        return Response({"status": "following"})


class LoginView(APIView):
    """API view for user login."""

    permission_classes = [permissions.AllowAny]
    serializer_class = LoginSerializer

    def post(self, request: Request) -> Response:
        """Authenticate and login user."""
        serializer = self.serializer_class(
            data=request.data,
            context={"request": request},
        )
        serializer.is_valid(raise_exception=True)

        user = serializer.validated_data["user"]
        login(request, user)

        user_serializer = UserSerializer(user)
        return Response(user_serializer.data)


class LogoutView(APIView):
    """API view for user logout."""

    permission_classes = [permissions.IsAuthenticated]

    def post(self, request: Request) -> Response:
        """Logout the current user."""
        logout(request)
        return Response({"detail": "Successfully logged out."})
```

### Forms
```python
"""Forms for user management."""
from django import forms
from django.contrib.auth.forms import UserChangeForm, UserCreationForm
from django.core.exceptions import ValidationError
from django.utils.translation import gettext_lazy as _

from apps.users.models import User


class UserUpdateForm(forms.ModelForm):
    """Form for updating user profile."""

    class Meta:
        model = User
        fields = ["first_name", "last_name", "email", "bio", "avatar"]
        widgets = {
            "bio": forms.Textarea(attrs={"rows": 4}),
        }

    def clean_email(self) -> str:
        """Validate email uniqueness."""
        email = self.cleaned_data["email"]
        if User.objects.exclude(pk=self.instance.pk).filter(email=email).exists():
            raise ValidationError(_("This email is already in use."))
        return email


class CustomUserCreationForm(UserCreationForm):
    """Custom form for user registration."""

    email = forms.EmailField(
        required=True,
        widget=forms.EmailInput(attrs={"class": "form-control"}),
    )

    class Meta:
        model = User
        fields = ["username", "email", "password1", "password2"]

    def save(self, commit: bool = True) -> User:
        """Save user with email."""
        user = super().save(commit=False)
        user.email = self.cleaned_data["email"]
        if commit:
            user.save()
        return user
```

### URL Configuration
```python
"""URL configuration for users app."""
from django.urls import include, path
from rest_framework.routers import DefaultRouter

from apps.users import views

app_name = "users"

# API router
router = DefaultRouter()
router.register("users", views.UserViewSet)

urlpatterns = [
    # Template views
    path("", views.UserListView.as_view(), name="list"),
    path("<int:pk>/", views.UserDetailView.as_view(), name="detail"),
    path("update/", views.UserUpdateView.as_view(), name="update"),

    # API views
    path("api/", include(router.urls)),
    path("api/login/", views.LoginView.as_view(), name="api-login"),
    path("api/logout/", views.LogoutView.as_view(), name="api-logout"),
]
```

### Settings Structure
```python
"""Base settings for Django project."""
from pathlib import Path

from decouple import Csv, config

# Build paths
BASE_DIR = Path(__file__).resolve().parent.parent.parent

# Security
SECRET_KEY = config("SECRET_KEY")
DEBUG = config("DEBUG", default=False, cast=bool)
ALLOWED_HOSTS = config("ALLOWED_HOSTS", cast=Csv())

# Application definition
DJANGO_APPS = [
    "django.contrib.admin",
    "django.contrib.auth",
    "django.contrib.contenttypes",
    "django.contrib.sessions",
    "django.contrib.messages",
    "django.contrib.staticfiles",
]

THIRD_PARTY_APPS = [
    "rest_framework",
    "corsheaders",
    "django_extensions",
]

LOCAL_APPS = [
    "apps.core",
    "apps.users",
    "apps.api",
]

INSTALLED_APPS = DJANGO_APPS + THIRD_PARTY_APPS + LOCAL_APPS

MIDDLEWARE = [
    "django.middleware.security.SecurityMiddleware",
    "whitenoise.middleware.WhiteNoiseMiddleware",
    "corsheaders.middleware.CorsMiddleware",
    "django.middleware.common.CommonMiddleware",
    "django.middleware.csrf.CsrfViewMiddleware",
    "django.contrib.auth.middleware.AuthenticationMiddleware",
    "django.contrib.messages.middleware.MessageMiddleware",
    "django.middleware.clickjacking.XFrameOptionsMiddleware",
]

ROOT_URLCONF = "config.urls"

# Database
DATABASES = {
    "default": {
        "ENGINE": "django.db.backends.postgresql",
        "NAME": config("DB_NAME"),
        "USER": config("DB_USER"),
        "PASSWORD": config("DB_PASSWORD"),
        "HOST": config("DB_HOST", default="localhost"),
        "PORT": config("DB_PORT", default="5432"),
        "ATOMIC_REQUESTS": True,
        "CONN_MAX_AGE": config("CONN_MAX_AGE", default=60, cast=int),
    }
}

# Cache
CACHES = {
    "default": {
        "BACKEND": "django.core.cache.backends.redis.RedisCache",
        "LOCATION": config("REDIS_URL", default="redis://127.0.0.1:6379/1"),
    }
}

# Password validation
AUTH_PASSWORD_VALIDATORS = [
    {
        "NAME": "django.contrib.auth.password_validation.UserAttributeSimilarityValidator",
    },
    {
        "NAME": "django.contrib.auth.password_validation.MinimumLengthValidator",
        "OPTIONS": {
            "min_length": 8,
        },
    },
    {
        "NAME": "django.contrib.auth.password_validation.CommonPasswordValidator",
    },
    {
        "NAME": "django.contrib.auth.password_validation.NumericPasswordValidator",
    },
]

# Internationalization
LANGUAGE_CODE = "en-us"
TIME_ZONE = "UTC"
USE_I18N = True
USE_TZ = True

# Static files
STATIC_URL = "/static/"
STATIC_ROOT = BASE_DIR / "staticfiles"
STATICFILES_DIRS = [BASE_DIR / "static"]
STATICFILES_STORAGE = "whitenoise.storage.CompressedManifestStaticFilesStorage"

# Media files
MEDIA_URL = "/media/"
MEDIA_ROOT = BASE_DIR / "media"

# Default primary key field type
DEFAULT_AUTO_FIELD = "django.db.models.BigAutoField"

# Custom user model
AUTH_USER_MODEL = "users.User"

# REST Framework
REST_FRAMEWORK = {
    "DEFAULT_AUTHENTICATION_CLASSES": [
        "rest_framework.authentication.SessionAuthentication",
    ],
    "DEFAULT_PERMISSION_CLASSES": [
        "rest_framework.permissions.IsAuthenticatedOrReadOnly",
    ],
    "DEFAULT_PAGINATION_CLASS": "rest_framework.pagination.PageNumberPagination",
    "PAGE_SIZE": 20,
    "DEFAULT_FILTER_BACKENDS": [
        "rest_framework.filters.SearchFilter",
        "rest_framework.filters.OrderingFilter",
    ],
}
```

## Testing

### Unit Tests with Pytest
```python
"""Tests for user models."""
import pytest
from django.contrib.auth import get_user_model
from django.db import IntegrityError

User = get_user_model()


@pytest.mark.django_db
class TestUserModel:
    """Test cases for User model."""

    def test_create_user(self):
        """Test creating a user with valid data."""
        user = User.objects.create_user(
            username="testuser",
            email="test@example.com",
            password="testpass123",
        )
        assert user.username == "testuser"
        assert user.email == "test@example.com"
        assert user.check_password("testpass123")
        assert user.is_active
        assert not user.is_staff
        assert not user.is_superuser

    def test_create_superuser(self):
        """Test creating a superuser."""
        admin = User.objects.create_superuser(
            username="admin",
            email="admin@example.com",
            password="adminpass123",
        )
        assert admin.is_staff
        assert admin.is_superuser

    def test_unique_email_constraint(self):
        """Test that email must be unique."""
        User.objects.create_user(
            username="user1",
            email="same@example.com",
            password="pass123",
        )

        with pytest.raises(IntegrityError):
            User.objects.create_user(
                username="user2",
                email="same@example.com",
                password="pass456",
            )

    def test_str_representation(self):
        """Test string representation of user."""
        user = User(email="test@example.com")
        assert str(user) == "test@example.com"

    def test_get_full_name(self):
        """Test get_full_name method."""
        user = User(
            username="testuser",
            first_name="John",
            last_name="Doe",
        )
        assert user.get_full_name() == "John Doe"

        user_no_name = User(username="testuser")
        assert user_no_name.get_full_name() == "testuser"
```

### Factory Boy for Test Data
```python
"""Factories for generating test data."""
import factory
from django.contrib.auth import get_user_model
from factory.django import DjangoModelFactory
from faker import Faker

fake = Faker()
User = get_user_model()


class UserFactory(DjangoModelFactory):
    """Factory for User model."""

    class Meta:
        model = User
        django_get_or_create = ["username"]

    username = factory.Sequence(lambda n: f"user{n}")
    email = factory.LazyAttribute(lambda obj: f"{obj.username}@example.com")
    first_name = factory.Faker("first_name")
    last_name = factory.Faker("last_name")
    is_active = True
    is_staff = False

    @factory.post_generation
    def password(obj, create, extracted, **kwargs):
        """Set password after user creation."""
        if create and extracted:
            obj.set_password(extracted)


class AdminFactory(UserFactory):
    """Factory for admin users."""

    username = factory.Sequence(lambda n: f"admin{n}")
    is_staff = True
    is_superuser = True
```

### API Tests
```python
"""Tests for user API endpoints."""
import pytest
from django.contrib.auth import get_user_model
from django.urls import reverse
from rest_framework import status
from rest_framework.test import APIClient

from tests.factories import UserFactory

User = get_user_model()


@pytest.mark.django_db
class TestUserAPI:
    """Test cases for user API."""

    @pytest.fixture(autouse=True)
    def setup(self):
        """Set up test dependencies."""
        self.client = APIClient()
        self.user = UserFactory(password="testpass123")

    def test_list_users(self):
        """Test listing users."""
        url = reverse("users:user-list")
        response = self.client.get(url)

        assert response.status_code == status.HTTP_200_OK
        assert len(response.json()["results"]) == 1

    def test_retrieve_user(self):
        """Test retrieving a single user."""
        url = reverse("users:user-detail", kwargs={"username": self.user.username})
        response = self.client.get(url)

        assert response.status_code == status.HTTP_200_OK
        assert response.json()["email"] == self.user.email

    def test_create_user(self):
        """Test user registration."""
        url = reverse("users:user-list")
        data = {
            "username": "newuser",
            "email": "new@example.com",
            "password": "newpass123",
            "password_confirm": "newpass123",
        }
        response = self.client.post(url, data, format="json")

        assert response.status_code == status.HTTP_201_CREATED
        assert User.objects.filter(username="newuser").exists()

    def test_login(self):
        """Test user login."""
        url = reverse("users:api-login")
        data = {
            "email": self.user.email,
            "password": "testpass123",
        }
        response = self.client.post(url, data, format="json")

        assert response.status_code == status.HTTP_200_OK
        assert "email" in response.json()

    def test_logout(self):
        """Test user logout."""
        self.client.force_authenticate(user=self.user)
        url = reverse("users:api-logout")
        response = self.client.post(url)

        assert response.status_code == status.HTTP_200_OK

    def test_me_endpoint(self):
        """Test current user endpoint."""
        self.client.force_authenticate(user=self.user)
        url = reverse("users:user-me")
        response = self.client.get(url)

        assert response.status_code == status.HTTP_200_OK
        assert response.json()["email"] == self.user.email

    def test_unauthorized_access(self):
        """Test that some endpoints require authentication."""
        url = reverse("users:user-me")
        response = self.client.get(url)

        assert response.status_code == status.HTTP_401_UNAUTHORIZED
```

## Development Commands

### Using uv with Django
```bash
# Install dependencies
uv sync

# Run development server
uv run python manage.py runserver

# Create migrations
uv run python manage.py makemigrations

# Apply migrations
uv run python manage.py migrate

# Create superuser
uv run python manage.py createsuperuser

# Run Django shell
uv run python manage.py shell_plus

# Collect static files
uv run python manage.py collectstatic

# Run tests with pytest
uv run pytest

# Run tests with coverage
uv run pytest --cov=apps --cov-report=html

# Run specific test file
uv run pytest tests/test_users.py

# Run tests in parallel
uv run pytest -n auto
```

### Code Quality with Ruff
```bash
# Check code with ruff
ruff check .

# Fix auto-fixable issues
ruff check --fix .

# Format code
ruff format .

# Check specific Django issues
ruff check --select DJ .

# Type checking with mypy
uv run mypy apps/

# Run all checks (create this as a script)
#!/bin/bash
echo "Running Ruff linter..."
ruff check --fix .
echo "Running Ruff formatter..."
ruff format .
echo "Running MyPy..."
uv run mypy apps/
echo "Running tests..."
uv run pytest
```

## Deployment

### Production Settings
```python
"""Production settings."""
from .base import *  # noqa

DEBUG = False

# Security
SECURE_SSL_REDIRECT = True
SESSION_COOKIE_SECURE = True
CSRF_COOKIE_SECURE = True
SECURE_BROWSER_XSS_FILTER = True
SECURE_CONTENT_TYPE_NOSNIFF = True
X_FRAME_OPTIONS = "DENY"
SECURE_HSTS_SECONDS = 31536000
SECURE_HSTS_INCLUDE_SUBDOMAINS = True
SECURE_HSTS_PRELOAD = True

# Allowed hosts from environment
ALLOWED_HOSTS = config("ALLOWED_HOSTS", cast=Csv())

# Database with connection pooling
DATABASES["default"]["CONN_MAX_AGE"] = 60

# Cache configuration
CACHES["default"]["OPTIONS"] = {
    "CONNECTION_POOL_KWARGS": {"max_connections": 50}
}

# Email
EMAIL_BACKEND = "django.core.mail.backends.smtp.EmailBackend"
EMAIL_HOST = config("EMAIL_HOST")
EMAIL_PORT = config("EMAIL_PORT", cast=int)
EMAIL_USE_TLS = config("EMAIL_USE_TLS", cast=bool)
EMAIL_HOST_USER = config("EMAIL_HOST_USER")
EMAIL_HOST_PASSWORD = config("EMAIL_HOST_PASSWORD")
DEFAULT_FROM_EMAIL = config("DEFAULT_FROM_EMAIL")

# Logging
LOGGING = {
    "version": 1,
    "disable_existing_loggers": False,
    "formatters": {
        "verbose": {
            "format": "{levelname} {asctime} {module} {message}",
            "style": "{",
        },
    },
    "handlers": {
        "file": {
            "level": "ERROR",
            "class": "logging.FileHandler",
            "filename": "/var/log/django/error.log",
            "formatter": "verbose",
        },
    },
    "root": {
        "handlers": ["file"],
        "level": "ERROR",
    },
    "loggers": {
        "django": {
            "handlers": ["file"],
            "level": "ERROR",
            "propagate": False,
        },
    },
}
```

### Docker Configuration
```dockerfile
FROM python:3.11-slim

ENV PYTHONDONTWRITEBYTECODE=1 \
    PYTHONUNBUFFERED=1 \
    UV_SYSTEM_PYTHON=1

WORKDIR /app

# Install system dependencies
RUN apt-get update && apt-get install -y \
    gcc \
    postgresql-client \
    && rm -rf /var/lib/apt/lists/*

# Install uv
COPY --from=ghcr.io/astral-sh/uv:latest /uv /usr/local/bin/uv

# Copy dependency files
COPY pyproject.toml uv.lock ./

# Install Python dependencies
RUN uv sync --frozen --no-dev

# Copy project files
COPY . .

# Collect static files
RUN uv run python manage.py collectstatic --noinput

# Run migrations and start server
CMD ["sh", "-c", "uv run python manage.py migrate && uv run gunicorn config.wsgi:application --bind 0.0.0.0:8000"]
```

---
*Last Updated: [Date]*
*Django Version: 5.0+*
*Python Version: 3.11+*
*Tools: uv (package management), ruff (linting & formatting), pytest (testing)*
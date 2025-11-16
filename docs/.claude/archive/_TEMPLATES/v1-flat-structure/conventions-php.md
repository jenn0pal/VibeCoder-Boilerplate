# PHP Project Conventions

## Code Style

### PSR-12 Compliance
- **Line Length:** Soft limit 120 characters, hard limit 140
- **Indentation:** 4 spaces (never tabs)
- **Blank Lines:** 1 between namespace and use, 1 between class members
- **Braces:** Opening brace on new line for classes, same line for methods

### Naming Conventions
| Type | Convention | Example |
|------|------------|---------|
| Variables | camelCase | `$userName`, `$isActive` |
| Constants | UPPER_SNAKE_CASE | `MAX_RETRY_COUNT` |
| Class Constants | UPPER_SNAKE_CASE | `self::DEFAULT_TIMEOUT` |
| Functions | snake_case | `get_user_by_id()` |
| Methods | camelCase | `getUserById()` |
| Classes | PascalCase | `UserService` |
| Interfaces | PascalCase with 'Interface' | `UserRepositoryInterface` |
| Traits | PascalCase with 'Trait' | `TimestampableTrait` |
| Namespaces | PascalCase | `App\Services` |
| Files | PascalCase for classes | `UserService.php` |

### File Organization
```
project/
├── app/                    # Application code (Laravel)
├── src/                    # Source code (non-framework)
│   ├── Controllers/
│   ├── Services/
│   ├── Repositories/
│   ├── Models/
│   ├── ValueObjects/
│   ├── Exceptions/
│   └── Helpers/
├── tests/
│   ├── Unit/
│   ├── Feature/
│   └── Integration/
├── database/
│   ├── migrations/
│   ├── seeders/
│   └── factories/
├── config/
├── public/
├── resources/
├── vendor/                # Composer dependencies
├── composer.json
├── composer.lock
├── phpunit.xml
├── phpstan.neon
└── .php-cs-fixer.php
```

### Type Declarations (PHP 8.0+)
```php
<?php

declare(strict_types=1);

namespace App\Services;

use App\Models\User;
use App\Exceptions\ValidationException;

class UserService
{
    public function __construct(
        private readonly UserRepository $repository,
        private readonly CacheInterface $cache,
    ) {
    }

    public function findUser(int $id): ?User
    {
        return $this->repository->find($id);
    }

    /**
     * @param array<string, mixed> $data
     * @return array<int, User>
     */
    public function searchUsers(array $data): array
    {
        return $this->repository->search($data);
    }

    public function createUser(string $email, string $name): User
    {
        if (!filter_var($email, FILTER_VALIDATE_EMAIL)) {
            throw new ValidationException('Invalid email format');
        }

        return $this->repository->create([
            'email' => $email,
            'name' => $name,
        ]);
    }
}
```

## PHP 8+ Features

### Constructor Property Promotion
```php
class UserDTO
{
    public function __construct(
        public readonly int $id,
        public readonly string $email,
        public readonly string $name,
        public readonly ?string $phone = null,
        public readonly UserRole $role = UserRole::USER,
    ) {
    }
}
```

### Enums (PHP 8.1+)
```php
enum UserRole: string
{
    case ADMIN = 'admin';
    case USER = 'user';
    case GUEST = 'guest';

    public function hasPermission(string $permission): bool
    {
        return match($this) {
            self::ADMIN => true,
            self::USER => in_array($permission, ['read', 'write']),
            self::GUEST => $permission === 'read',
        };
    }
}
```

### Attributes (PHP 8.0+)
```php
use Symfony\Component\Routing\Annotation\Route;
use Symfony\Component\Validator\Constraints as Assert;

class UserController
{
    #[Route('/users/{id}', methods: ['GET'])]
    public function show(int $id): Response
    {
        // Implementation
    }
}

class CreateUserRequest
{
    #[Assert\NotBlank]
    #[Assert\Email]
    public string $email;

    #[Assert\NotBlank]
    #[Assert\Length(min: 3, max: 50)]
    public string $name;
}
```

### Union Types & Null Safety
```php
class PaymentService
{
    public function processPayment(
        float|int $amount,
        PaymentMethod $method,
        ?string $couponCode = null
    ): PaymentResult|PaymentError {
        // Implementation
    }

    public function getDiscount(?string $code): float
    {
        return $code?->trim()
            ? $this->couponRepository->findByCode($code)?->discount ?? 0.0
            : 0.0;
    }
}
```

## DocBlock Standards

### Class Documentation
```php
/**
 * Manages user authentication and authorization
 *
 * This service handles user login, logout, password resets,
 * and permission checks throughout the application.
 *
 * @package App\Services
 * @author Your Name <your.email@example.com>
 * @since 1.0.0
 */
class AuthService
{
    // Implementation
}
```

### Method Documentation
```php
/**
 * Calculate the discounted price for a product
 *
 * @param float $price Original price
 * @param float $discountPercent Discount percentage (0-100)
 * @param string|null $couponCode Optional coupon code
 *
 * @return float The final price after discounts
 *
 * @throws InvalidArgumentException If price or discount is negative
 * @throws CouponExpiredException If the coupon has expired
 *
 * @example
 * $finalPrice = $service->calculateDiscount(100.00, 20, 'SAVE10');
 */
public function calculateDiscount(
    float $price,
    float $discountPercent,
    ?string $couponCode = null
): float {
    // Implementation
}
```

## Error Handling

### Custom Exceptions
```php
namespace App\Exceptions;

class DomainException extends \Exception
{
    public function __construct(
        string $message = '',
        int $code = 0,
        ?\Throwable $previous = null
    ) {
        parent::__construct($message, $code, $previous);
    }
}

class ValidationException extends DomainException
{
    public function __construct(
        private array $errors,
        string $message = 'Validation failed'
    ) {
        parent::__construct($message);
    }

    public function getErrors(): array
    {
        return $this->errors;
    }
}

class NotFoundException extends DomainException
{
    public function __construct(string $resource, int|string $id)
    {
        parent::__construct("$resource with ID $id not found", 404);
    }
}
```

### Exception Handling
```php
class UserController
{
    public function store(Request $request): JsonResponse
    {
        try {
            $user = $this->userService->create($request->all());

            return response()->json($user, 201);
        } catch (ValidationException $e) {
            return response()->json([
                'message' => $e->getMessage(),
                'errors' => $e->getErrors(),
            ], 422);
        } catch (DomainException $e) {
            return response()->json([
                'message' => $e->getMessage(),
            ], 400);
        } catch (\Exception $e) {
            Log::error('Unexpected error', [
                'exception' => $e->getMessage(),
                'trace' => $e->getTraceAsString(),
            ]);

            return response()->json([
                'message' => 'An error occurred',
            ], 500);
        }
    }
}
```

## Testing Conventions

### PHPUnit Test Structure
```php
namespace Tests\Unit\Services;

use Tests\TestCase;
use App\Services\UserService;
use App\Repositories\UserRepository;
use Mockery;

class UserServiceTest extends TestCase
{
    private UserService $service;
    private UserRepository $repository;

    protected function setUp(): void
    {
        parent::setUp();

        $this->repository = Mockery::mock(UserRepository::class);
        $this->service = new UserService($this->repository);
    }

    /** @test */
    public function it_creates_a_user_with_valid_data(): void
    {
        // Arrange
        $data = [
            'email' => 'test@example.com',
            'name' => 'Test User',
        ];

        $this->repository
            ->shouldReceive('create')
            ->once()
            ->with($data)
            ->andReturn(new User($data));

        // Act
        $user = $this->service->createUser($data['email'], $data['name']);

        // Assert
        $this->assertInstanceOf(User::class, $user);
        $this->assertEquals($data['email'], $user->email);
    }

    /** @test */
    public function it_throws_exception_for_invalid_email(): void
    {
        $this->expectException(ValidationException::class);

        $this->service->createUser('invalid-email', 'Test User');
    }
}
```

### Pest PHP Test Structure (Alternative)
```php
use App\Services\UserService;
use App\Models\User;

beforeEach(function () {
    $this->service = app(UserService::class);
});

test('creates user with valid data', function () {
    $user = $this->service->createUser('test@example.com', 'Test User');

    expect($user)
        ->toBeInstanceOf(User::class)
        ->email->toBe('test@example.com')
        ->name->toBe('Test User');
});

test('throws exception for invalid email', function () {
    $this->service->createUser('invalid-email', 'Test User');
})->throws(ValidationException::class);

dataset('invalid_emails', [
    ['not-an-email'],
    ['@example.com'],
    ['user@'],
    [''],
]);

test('rejects invalid email formats', function ($email) {
    expect(fn() => $this->service->createUser($email, 'Test'))
        ->toThrow(ValidationException::class);
})->with('invalid_emails');
```

## Database Patterns

### Eloquent Models (Laravel)
```php
namespace App\Models;

use Illuminate\Database\Eloquent\Model;
use Illuminate\Database\Eloquent\SoftDeletes;
use Illuminate\Database\Eloquent\Relations\HasMany;
use Illuminate\Database\Eloquent\Relations\BelongsTo;
use Illuminate\Database\Eloquent\Factories\HasFactory;

/**
 * @property int $id
 * @property string $name
 * @property string $email
 * @property Carbon $created_at
 * @property Carbon $updated_at
 */
class User extends Model
{
    use HasFactory, SoftDeletes;

    protected $fillable = [
        'name',
        'email',
        'password',
    ];

    protected $hidden = [
        'password',
        'remember_token',
    ];

    protected $casts = [
        'email_verified_at' => 'datetime',
        'is_active' => 'boolean',
        'settings' => 'array',
    ];

    public function posts(): HasMany
    {
        return $this->hasMany(Post::class);
    }

    public function role(): BelongsTo
    {
        return $this->belongsTo(Role::class);
    }

    public function scopeActive($query)
    {
        return $query->where('is_active', true);
    }
}
```

### Repository Pattern
```php
namespace App\Repositories;

use App\Models\User;
use Illuminate\Support\Collection;

interface UserRepositoryInterface
{
    public function find(int $id): ?User;
    public function findByEmail(string $email): ?User;
    public function create(array $data): User;
    public function update(int $id, array $data): bool;
    public function delete(int $id): bool;
    public function paginate(int $perPage = 15): LengthAwarePaginator;
}

class UserRepository implements UserRepositoryInterface
{
    public function __construct(
        private User $model
    ) {
    }

    public function find(int $id): ?User
    {
        return $this->model->find($id);
    }

    public function findByEmail(string $email): ?User
    {
        return $this->model->where('email', $email)->first();
    }

    public function create(array $data): User
    {
        return $this->model->create($data);
    }

    public function update(int $id, array $data): bool
    {
        return $this->model->where('id', $id)->update($data) > 0;
    }

    public function delete(int $id): bool
    {
        return $this->model->destroy($id) > 0;
    }

    public function paginate(int $perPage = 15): LengthAwarePaginator
    {
        return $this->model->paginate($perPage);
    }
}
```

## Dependency Management

### composer.json
```json
{
    "name": "company/project",
    "description": "Project description",
    "type": "project",
    "require": {
        "php": "^8.2",
        "laravel/framework": "^11.0",
        "guzzlehttp/guzzle": "^7.8"
    },
    "require-dev": {
        "phpunit/phpunit": "^10.5",
        "mockery/mockery": "^1.6",
        "phpstan/phpstan": "^1.10",
        "friendsofphp/php-cs-fixer": "^3.40",
        "pestphp/pest": "^2.28",
        "laravel/pint": "^1.13"
    },
    "autoload": {
        "psr-4": {
            "App\\": "app/",
            "Database\\Seeders\\": "database/seeders/"
        }
    },
    "autoload-dev": {
        "psr-4": {
            "Tests\\": "tests/"
        }
    },
    "scripts": {
        "test": "vendor/bin/phpunit",
        "test:coverage": "vendor/bin/phpunit --coverage-html coverage",
        "analyse": "vendor/bin/phpstan analyse",
        "format": "vendor/bin/php-cs-fixer fix",
        "format:check": "vendor/bin/php-cs-fixer fix --dry-run --diff"
    },
    "config": {
        "optimize-autoloader": true,
        "preferred-install": "dist",
        "sort-packages": true
    }
}
```

## Code Quality Tools

### PHPStan Configuration (phpstan.neon)
```neon
parameters:
    level: 8
    paths:
        - app
        - tests
    excludePaths:
        - app/Http/Middleware/RedirectIfAuthenticated.php
    reportUnmatchedIgnoredErrors: false
    checkMissingIterableValueType: false
    checkGenericClassInNonGenericObjectType: false
```

### PHP CS Fixer Configuration (.php-cs-fixer.php)
```php
<?php

$finder = PhpCsFixer\Finder::create()
    ->in(__DIR__)
    ->exclude(['vendor', 'storage', 'bootstrap/cache'])
    ->name('*.php')
    ->notName('*.blade.php')
    ->ignoreDotFiles(true)
    ->ignoreVCS(true);

return (new PhpCsFixer\Config())
    ->setRules([
        '@PSR12' => true,
        'array_syntax' => ['syntax' => 'short'],
        'binary_operator_spaces' => true,
        'blank_line_after_namespace' => true,
        'blank_line_after_opening_tag' => true,
        'blank_line_before_statement' => [
            'statements' => ['return'],
        ],
        'cast_spaces' => true,
        'class_attributes_separation' => [
            'elements' => ['method' => 'one'],
        ],
        'concat_space' => ['spacing' => 'one'],
        'declare_equal_normalize' => true,
        'function_typehint_space' => true,
        'lowercase_cast' => true,
        'lowercase_keywords' => true,
        'method_argument_space' => true,
        'no_blank_lines_after_class_opening' => true,
        'no_blank_lines_after_phpdoc' => true,
        'no_empty_statement' => true,
        'no_leading_import_slash' => true,
        'no_leading_namespace_whitespace' => true,
        'no_mixed_echo_print' => ['use' => 'echo'],
        'no_multiline_whitespace_around_double_arrow' => true,
        'no_spaces_around_offset' => true,
        'no_unused_imports' => true,
        'no_whitespace_before_comma_in_array' => true,
        'no_whitespace_in_blank_line' => true,
        'object_operator_without_whitespace' => true,
        'ordered_imports' => ['sort_algorithm' => 'alpha'],
        'phpdoc_align' => true,
        'phpdoc_no_access' => true,
        'phpdoc_order' => true,
        'phpdoc_scalar' => true,
        'phpdoc_separation' => true,
        'phpdoc_trim' => true,
        'return_type_declaration' => true,
        'single_blank_line_before_namespace' => true,
        'single_quote' => true,
        'space_after_semicolon' => true,
        'ternary_operator_spaces' => true,
        'trailing_comma_in_multiline' => true,
        'trim_array_spaces' => true,
        'unary_operator_spaces' => true,
        'visibility_required' => true,
    ])
    ->setFinder($finder);
```

### Laravel Pint Configuration (pint.json)
```json
{
    "preset": "laravel",
    "rules": {
        "array_syntax": {
            "syntax": "short"
        },
        "binary_operator_spaces": {
            "default": "single_space"
        },
        "blank_line_after_namespace": true,
        "blank_line_after_opening_tag": true,
        "blank_line_before_statement": {
            "statements": ["return"]
        },
        "concat_space": {
            "spacing": "one"
        },
        "declare_strict_types": true,
        "no_unused_imports": true,
        "not_operator_with_successor_space": false,
        "ordered_imports": {
            "sort_algorithm": "alpha"
        },
        "phpdoc_align": {
            "align": "left"
        },
        "phpdoc_order": true,
        "phpdoc_separation": true,
        "single_quote": true,
        "trailing_comma_in_multiline": true,
        "yoda_style": false
    }
}
```

## Security Best Practices

### Input Validation
```php
namespace App\Http\Requests;

use Illuminate\Foundation\Http\FormRequest;

class CreateUserRequest extends FormRequest
{
    public function authorize(): bool
    {
        return $this->user()->can('create-users');
    }

    public function rules(): array
    {
        return [
            'email' => ['required', 'email', 'unique:users,email'],
            'name' => ['required', 'string', 'min:3', 'max:50'],
            'password' => ['required', 'string', 'min:8', 'confirmed'],
            'role_id' => ['required', 'exists:roles,id'],
        ];
    }

    public function messages(): array
    {
        return [
            'email.unique' => 'This email is already registered.',
            'password.min' => 'Password must be at least 8 characters.',
        ];
    }

    protected function prepareForValidation(): void
    {
        $this->merge([
            'email' => strtolower(trim($this->email)),
        ]);
    }
}
```

### SQL Injection Prevention
```php
// Always use parameterized queries
$users = DB::select('SELECT * FROM users WHERE email = ?', [$email]);

// Use query builder
$users = DB::table('users')
    ->where('email', $email)
    ->get();

// Use Eloquent ORM
$user = User::where('email', $email)->first();

// NEVER do this
$users = DB::select("SELECT * FROM users WHERE email = '$email'"); // DANGEROUS!
```

### XSS Prevention
```php
// In Blade templates, always escape output
{{ $userInput }} // Automatically escaped

// For unescaped output (use carefully)
{!! $trustedHtml !!}

// In PHP code
echo htmlspecialchars($userInput, ENT_QUOTES, 'UTF-8');

// Use Laravel's e() helper
echo e($userInput);
```

## Performance Guidelines

### Query Optimization
```php
// Eager load relationships to avoid N+1 queries
$users = User::with(['posts', 'comments'])->get();

// Use select to fetch only needed columns
$users = User::select('id', 'name', 'email')->get();

// Use chunking for large datasets
User::chunk(200, function ($users) {
    foreach ($users as $user) {
        // Process user
    }
});

// Use database indices
Schema::table('users', function (Blueprint $table) {
    $table->index('email');
    $table->index(['status', 'created_at']);
});
```

### Caching Strategies
```php
use Illuminate\Support\Facades\Cache;

class UserService
{
    public function getUser(int $id): ?User
    {
        return Cache::remember("user.{$id}", 3600, function () use ($id) {
            return User::find($id);
        });
    }

    public function updateUser(int $id, array $data): User
    {
        $user = User::findOrFail($id);
        $user->update($data);

        // Clear cache after update
        Cache::forget("user.{$id}");

        return $user;
    }
}
```

---
*Last Updated: [Date]*
*PHP Version: 8.2+*
*Standards: PSR-12, PSR-4*
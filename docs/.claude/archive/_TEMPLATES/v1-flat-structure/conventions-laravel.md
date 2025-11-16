# Laravel Project Conventions

## Project Structure

### Standard Laravel Layout
```
project/
├── app/
│   ├── Console/           # Console commands
│   │   ├── Commands/
│   │   └── Kernel.php
│   ├── Exceptions/        # Custom exceptions
│   ├── Http/
│   │   ├── Controllers/
│   │   │   ├── Api/      # API controllers
│   │   │   └── Web/      # Web controllers
│   │   ├── Middleware/
│   │   ├── Requests/      # Form requests
│   │   └── Resources/     # API resources
│   ├── Models/            # Eloquent models
│   ├── Providers/         # Service providers
│   ├── Services/          # Business logic
│   ├── Repositories/      # Repository pattern
│   ├── Traits/            # Reusable traits
│   ├── Enums/             # PHP enums
│   └── Events/            # Event classes
├── bootstrap/
├── config/                # Configuration files
├── database/
│   ├── factories/         # Model factories
│   ├── migrations/        # Database migrations
│   └── seeders/           # Database seeders
├── public/
├── resources/
│   ├── views/
│   ├── js/
│   └── css/
├── routes/
│   ├── api.php           # API routes
│   ├── web.php           # Web routes
│   └── channels.php      # Broadcasting channels
├── storage/
├── tests/
│   ├── Feature/
│   ├── Unit/
│   └── Pest.php          # Pest configuration
├── .env.example
├── artisan
├── composer.json
├── package.json
├── phpunit.xml
├── pint.json             # Laravel Pint config
└── vite.config.js
```

## Naming Conventions

### Files and Directories
| Type | Convention | Example |
|------|------------|---------|
| Controllers | PascalCase + Controller | `UserController.php` |
| Models | PascalCase singular | `User.php` |
| Migrations | snake_case with timestamp | `2024_01_15_000000_create_users_table.php` |
| Seeders | PascalCase + Seeder | `UserSeeder.php` |
| Form Requests | PascalCase + Request | `CreateUserRequest.php` |
| Resources | PascalCase + Resource | `UserResource.php` |
| Middleware | PascalCase | `EnsureEmailIsVerified.php` |
| Traits | PascalCase + Trait | `HasRoles.php` |
| Enums | PascalCase | `UserStatus.php` |
| Events | PascalCase | `UserRegistered.php` |
| Listeners | PascalCase + Listener | `SendEmailVerificationListener.php` |
| Jobs | PascalCase + Job | `ProcessPaymentJob.php` |
| Policies | PascalCase + Policy | `PostPolicy.php` |

### Database Conventions
| Type | Convention | Example |
|------|------------|---------|
| Tables | snake_case plural | `users`, `blog_posts` |
| Columns | snake_case | `created_at`, `user_id` |
| Primary Key | `id` | `id` |
| Foreign Keys | singular_table_id | `user_id`, `post_id` |
| Pivot Tables | alphabetical singular | `post_tag`, `role_user` |
| Indexes | table_column_index | `users_email_index` |

## Eloquent Models

### Model Structure
```php
<?php

namespace App\Models;

use App\Enums\UserStatus;
use App\Traits\HasUuid;
use Illuminate\Database\Eloquent\Factories\HasFactory;
use Illuminate\Database\Eloquent\Model;
use Illuminate\Database\Eloquent\Relations\HasMany;
use Illuminate\Database\Eloquent\Relations\BelongsToMany;
use Illuminate\Database\Eloquent\SoftDeletes;
use Illuminate\Foundation\Auth\User as Authenticatable;
use Illuminate\Notifications\Notifiable;
use Laravel\Sanctum\HasApiTokens;

class User extends Authenticatable
{
    use HasApiTokens, HasFactory, Notifiable, SoftDeletes, HasUuid;

    /**
     * The table associated with the model.
     *
     * @var string
     */
    protected $table = 'users';

    /**
     * The attributes that are mass assignable.
     *
     * @var array<int, string>
     */
    protected $fillable = [
        'name',
        'email',
        'password',
        'status',
        'email_verified_at',
    ];

    /**
     * The attributes that should be hidden for serialization.
     *
     * @var array<int, string>
     */
    protected $hidden = [
        'password',
        'remember_token',
    ];

    /**
     * The attributes that should be cast.
     *
     * @var array<string, string>
     */
    protected $casts = [
        'email_verified_at' => 'datetime',
        'password' => 'hashed',
        'status' => UserStatus::class,
        'settings' => 'array',
        'is_active' => 'boolean',
    ];

    /**
     * The accessors to append to the model's array form.
     *
     * @var array<int, string>
     */
    protected $appends = ['full_name', 'avatar_url'];

    /**
     * Get the user's full name.
     */
    public function getFullNameAttribute(): string
    {
        return "{$this->first_name} {$this->last_name}";
    }

    /**
     * Get the user's avatar URL.
     */
    public function getAvatarUrlAttribute(): string
    {
        return $this->avatar
            ? Storage::url($this->avatar)
            : 'https://ui-avatars.com/api/?name=' . urlencode($this->name);
    }

    /**
     * Get the posts for the user.
     */
    public function posts(): HasMany
    {
        return $this->hasMany(Post::class);
    }

    /**
     * The roles that belong to the user.
     */
    public function roles(): BelongsToMany
    {
        return $this->belongsToMany(Role::class)->withTimestamps();
    }

    /**
     * Scope a query to only include active users.
     */
    public function scopeActive($query)
    {
        return $query->where('is_active', true);
    }

    /**
     * Scope a query to only include verified users.
     */
    public function scopeVerified($query)
    {
        return $query->whereNotNull('email_verified_at');
    }

    /**
     * Check if user has a specific role.
     */
    public function hasRole(string $role): bool
    {
        return $this->roles()->where('name', $role)->exists();
    }

    /**
     * Boot method for model events.
     */
    protected static function boot(): void
    {
        parent::boot();

        static::creating(function ($user) {
            $user->uuid = Str::uuid();
        });
    }
}
```

## Controllers

### API Controller
```php
<?php

namespace App\Http\Controllers\Api;

use App\Http\Controllers\Controller;
use App\Http\Requests\CreateUserRequest;
use App\Http\Requests\UpdateUserRequest;
use App\Http\Resources\UserResource;
use App\Models\User;
use App\Services\UserService;
use Illuminate\Http\JsonResponse;
use Illuminate\Http\Resources\Json\AnonymousResourceCollection;

class UserController extends Controller
{
    public function __construct(
        private readonly UserService $userService
    ) {
    }

    /**
     * Display a listing of users.
     */
    public function index(): AnonymousResourceCollection
    {
        $users = User::with(['roles', 'posts'])
            ->active()
            ->paginate(20);

        return UserResource::collection($users);
    }

    /**
     * Store a newly created user.
     */
    public function store(CreateUserRequest $request): JsonResponse
    {
        $user = $this->userService->create($request->validated());

        return response()->json([
            'message' => 'User created successfully',
            'data' => new UserResource($user),
        ], 201);
    }

    /**
     * Display the specified user.
     */
    public function show(User $user): UserResource
    {
        $user->load(['roles', 'posts']);

        return new UserResource($user);
    }

    /**
     * Update the specified user.
     */
    public function update(UpdateUserRequest $request, User $user): JsonResponse
    {
        $user = $this->userService->update($user, $request->validated());

        return response()->json([
            'message' => 'User updated successfully',
            'data' => new UserResource($user),
        ]);
    }

    /**
     * Remove the specified user.
     */
    public function destroy(User $user): JsonResponse
    {
        $this->userService->delete($user);

        return response()->json([
            'message' => 'User deleted successfully',
        ], 204);
    }
}
```

### Web Controller with Repository Pattern
```php
<?php

namespace App\Http\Controllers\Web;

use App\Http\Controllers\Controller;
use App\Http\Requests\ProfileUpdateRequest;
use App\Repositories\UserRepository;
use Illuminate\Http\RedirectResponse;
use Illuminate\Http\Request;
use Illuminate\View\View;

class ProfileController extends Controller
{
    public function __construct(
        private readonly UserRepository $userRepository
    ) {
    }

    /**
     * Display the user's profile form.
     */
    public function edit(Request $request): View
    {
        return view('profile.edit', [
            'user' => $request->user(),
        ]);
    }

    /**
     * Update the user's profile information.
     */
    public function update(ProfileUpdateRequest $request): RedirectResponse
    {
        $user = $this->userRepository->update(
            $request->user()->id,
            $request->validated()
        );

        if ($request->user()->isDirty('email')) {
            $user->email_verified_at = null;
            $user->save();
        }

        return redirect()
            ->route('profile.edit')
            ->with('status', 'profile-updated');
    }

    /**
     * Delete the user's account.
     */
    public function destroy(Request $request): RedirectResponse
    {
        $request->validateWithBag('userDeletion', [
            'password' => ['required', 'current_password'],
        ]);

        $user = $request->user();

        Auth::logout();

        $this->userRepository->delete($user->id);

        $request->session()->invalidate();
        $request->session()->regenerateToken();

        return redirect('/');
    }
}
```

## Form Requests

```php
<?php

namespace App\Http\Requests;

use App\Enums\UserStatus;
use Illuminate\Foundation\Http\FormRequest;
use Illuminate\Validation\Rule;
use Illuminate\Validation\Rules\Password;

class CreateUserRequest extends FormRequest
{
    /**
     * Determine if the user is authorized to make this request.
     */
    public function authorize(): bool
    {
        return $this->user()->can('create', User::class);
    }

    /**
     * Get the validation rules that apply to the request.
     *
     * @return array<string, \Illuminate\Contracts\Validation\ValidationRule|array<mixed>|string>
     */
    public function rules(): array
    {
        return [
            'name' => ['required', 'string', 'max:255'],
            'email' => [
                'required',
                'string',
                'email',
                'max:255',
                Rule::unique(User::class),
            ],
            'password' => [
                'required',
                'confirmed',
                Password::min(8)
                    ->letters()
                    ->mixedCase()
                    ->numbers()
                    ->symbols()
                    ->uncompromised(),
            ],
            'role_ids' => ['sometimes', 'array'],
            'role_ids.*' => ['exists:roles,id'],
            'status' => ['sometimes', Rule::enum(UserStatus::class)],
        ];
    }

    /**
     * Get custom error messages.
     */
    public function messages(): array
    {
        return [
            'email.unique' => 'This email address is already registered.',
            'password.uncompromised' => 'This password has been compromised in a data breach.',
        ];
    }

    /**
     * Prepare the data for validation.
     */
    protected function prepareForValidation(): void
    {
        $this->merge([
            'email' => strtolower($this->email),
        ]);
    }
}
```

## API Resources

```php
<?php

namespace App\Http\Resources;

use Illuminate\Http\Request;
use Illuminate\Http\Resources\Json\JsonResource;

class UserResource extends JsonResource
{
    /**
     * Transform the resource into an array.
     *
     * @return array<string, mixed>
     */
    public function toArray(Request $request): array
    {
        return [
            'id' => $this->id,
            'uuid' => $this->uuid,
            'name' => $this->name,
            'email' => $this->email,
            'email_verified' => !is_null($this->email_verified_at),
            'status' => $this->status,
            'avatar_url' => $this->avatar_url,
            'roles' => RoleResource::collection($this->whenLoaded('roles')),
            'posts_count' => $this->whenCounted('posts'),
            'posts' => PostResource::collection($this->whenLoaded('posts')),
            'created_at' => $this->created_at->toISOString(),
            'updated_at' => $this->updated_at->toISOString(),
        ];
    }

    /**
     * Add additional meta information to the resource.
     */
    public function with(Request $request): array
    {
        return [
            'meta' => [
                'api_version' => config('app.api_version'),
            ],
        ];
    }
}
```

## Services

```php
<?php

namespace App\Services;

use App\Events\UserCreated;
use App\Models\User;
use App\Repositories\UserRepository;
use Illuminate\Support\Facades\DB;
use Illuminate\Support\Facades\Hash;

class UserService
{
    public function __construct(
        private readonly UserRepository $userRepository,
        private readonly EmailService $emailService
    ) {
    }

    /**
     * Create a new user with roles.
     */
    public function create(array $data): User
    {
        return DB::transaction(function () use ($data) {
            $data['password'] = Hash::make($data['password']);

            $user = $this->userRepository->create($data);

            if (isset($data['role_ids'])) {
                $user->roles()->sync($data['role_ids']);
            }

            event(new UserCreated($user));

            $this->emailService->sendWelcomeEmail($user);

            return $user->fresh('roles');
        });
    }

    /**
     * Update user information.
     */
    public function update(User $user, array $data): User
    {
        return DB::transaction(function () use ($user, $data) {
            if (isset($data['password'])) {
                $data['password'] = Hash::make($data['password']);
            }

            $user = $this->userRepository->update($user->id, $data);

            if (isset($data['role_ids'])) {
                $user->roles()->sync($data['role_ids']);
            }

            Cache::forget("user.{$user->id}");

            return $user->fresh('roles');
        });
    }

    /**
     * Delete a user and cleanup related data.
     */
    public function delete(User $user): bool
    {
        return DB::transaction(function () use ($user) {
            // Delete user's files
            Storage::deleteDirectory("users/{$user->id}");

            // Remove from cache
            Cache::forget("user.{$user->id}");

            // Soft delete the user
            return $this->userRepository->delete($user->id);
        });
    }

    /**
     * Verify user's email.
     */
    public function verifyEmail(User $user): void
    {
        $user->markEmailAsVerified();
        event(new EmailVerified($user));
    }
}
```

## Repository Pattern

```php
<?php

namespace App\Repositories;

use App\Models\User;
use Illuminate\Database\Eloquent\Builder;
use Illuminate\Pagination\LengthAwarePaginator;

interface UserRepositoryInterface
{
    public function all(array $filters = []): LengthAwarePaginator;
    public function find(int $id): ?User;
    public function create(array $data): User;
    public function update(int $id, array $data): User;
    public function delete(int $id): bool;
}

class UserRepository implements UserRepositoryInterface
{
    /**
     * Get all users with optional filtering.
     */
    public function all(array $filters = []): LengthAwarePaginator
    {
        $query = User::query();

        $this->applyFilters($query, $filters);

        return $query->with(['roles'])
            ->latest()
            ->paginate($filters['per_page'] ?? 15);
    }

    /**
     * Find a user by ID.
     */
    public function find(int $id): ?User
    {
        return Cache::remember(
            "user.{$id}",
            3600,
            fn () => User::find($id)
        );
    }

    /**
     * Create a new user.
     */
    public function create(array $data): User
    {
        return User::create($data);
    }

    /**
     * Update a user.
     */
    public function update(int $id, array $data): User
    {
        $user = User::findOrFail($id);
        $user->update($data);

        return $user;
    }

    /**
     * Delete a user.
     */
    public function delete(int $id): bool
    {
        return User::destroy($id) > 0;
    }

    /**
     * Apply filters to the query.
     */
    private function applyFilters(Builder $query, array $filters): void
    {
        // Search filter
        if (!empty($filters['search'])) {
            $query->where(function ($q) use ($filters) {
                $q->where('name', 'like', "%{$filters['search']}%")
                  ->orWhere('email', 'like', "%{$filters['search']}%");
            });
        }

        // Status filter
        if (!empty($filters['status'])) {
            $query->where('status', $filters['status']);
        }

        // Role filter
        if (!empty($filters['role'])) {
            $query->whereHas('roles', function ($q) use ($filters) {
                $q->where('name', $filters['role']);
            });
        }

        // Date range filter
        if (!empty($filters['from_date'])) {
            $query->whereDate('created_at', '>=', $filters['from_date']);
        }

        if (!empty($filters['to_date'])) {
            $query->whereDate('created_at', '<=', $filters['to_date']);
        }
    }
}
```

## Middleware

```php
<?php

namespace App\Http\Middleware;

use Closure;
use Illuminate\Http\Request;
use Symfony\Component\HttpFoundation\Response;

class CheckUserStatus
{
    /**
     * Handle an incoming request.
     */
    public function handle(Request $request, Closure $next, string $status = 'active'): Response
    {
        if ($request->user() && $request->user()->status !== $status) {
            abort(403, 'Your account is not active.');
        }

        return $next($request);
    }
}
```

## Enums (PHP 8.1+)

```php
<?php

namespace App\Enums;

enum UserStatus: string
{
    case PENDING = 'pending';
    case ACTIVE = 'active';
    case SUSPENDED = 'suspended';
    case BANNED = 'banned';

    public function label(): string
    {
        return match($this) {
            self::PENDING => 'Pending Activation',
            self::ACTIVE => 'Active',
            self::SUSPENDED => 'Temporarily Suspended',
            self::BANNED => 'Permanently Banned',
        };
    }

    public function color(): string
    {
        return match($this) {
            self::PENDING => 'yellow',
            self::ACTIVE => 'green',
            self::SUSPENDED => 'orange',
            self::BANNED => 'red',
        };
    }

    public function canLogin(): bool
    {
        return match($this) {
            self::ACTIVE => true,
            default => false,
        };
    }

    public static function options(): array
    {
        return array_map(
            fn ($status) => [
                'value' => $status->value,
                'label' => $status->label(),
            ],
            self::cases()
        );
    }
}
```

## Database

### Migration
```php
<?php

use Illuminate\Database\Migrations\Migration;
use Illuminate\Database\Schema\Blueprint;
use Illuminate\Support\Facades\Schema;

return new class extends Migration
{
    /**
     * Run the migrations.
     */
    public function up(): void
    {
        Schema::create('users', function (Blueprint $table) {
            $table->id();
            $table->uuid('uuid')->unique();
            $table->string('name');
            $table->string('email')->unique();
            $table->timestamp('email_verified_at')->nullable();
            $table->string('password');
            $table->string('status')->default('pending');
            $table->json('settings')->nullable();
            $table->boolean('is_active')->default(true);
            $table->rememberToken();
            $table->timestamps();
            $table->softDeletes();

            // Indexes
            $table->index('email');
            $table->index('status');
            $table->index(['is_active', 'created_at']);
        });
    }

    /**
     * Reverse the migrations.
     */
    public function down(): void
    {
        Schema::dropIfExists('users');
    }
};
```

### Seeder
```php
<?php

namespace Database\Seeders;

use App\Models\User;
use App\Models\Role;
use Illuminate\Database\Seeder;

class UserSeeder extends Seeder
{
    /**
     * Run the database seeds.
     */
    public function run(): void
    {
        // Create admin user
        $admin = User::factory()->create([
            'name' => 'Admin User',
            'email' => 'admin@example.com',
            'email_verified_at' => now(),
            'status' => 'active',
        ]);

        $admin->roles()->attach(Role::where('name', 'admin')->first());

        // Create regular users
        User::factory()
            ->count(50)
            ->hasAttached(
                Role::where('name', 'user')->first()
            )
            ->hasPosts(3)
            ->create();
    }
}
```

### Factory
```php
<?php

namespace Database\Factories;

use App\Enums\UserStatus;
use Illuminate\Database\Eloquent\Factories\Factory;
use Illuminate\Support\Facades\Hash;
use Illuminate\Support\Str;

/**
 * @extends \Illuminate\Database\Eloquent\Factories\Factory<\App\Models\User>
 */
class UserFactory extends Factory
{
    /**
     * Define the model's default state.
     */
    public function definition(): array
    {
        return [
            'uuid' => Str::uuid(),
            'name' => fake()->name(),
            'email' => fake()->unique()->safeEmail(),
            'email_verified_at' => now(),
            'password' => Hash::make('password'),
            'status' => fake()->randomElement(UserStatus::cases())->value,
            'is_active' => true,
            'remember_token' => Str::random(10),
        ];
    }

    /**
     * Indicate that the user is unverified.
     */
    public function unverified(): static
    {
        return $this->state(fn (array $attributes) => [
            'email_verified_at' => null,
        ]);
    }

    /**
     * Indicate that the user is suspended.
     */
    public function suspended(): static
    {
        return $this->state(fn (array $attributes) => [
            'status' => UserStatus::SUSPENDED->value,
            'is_active' => false,
        ]);
    }
}
```

## Testing with Pest

### Feature Test
```php
<?php

use App\Models\User;
use App\Models\Role;

beforeEach(function () {
    $this->user = User::factory()->create();
    $this->admin = User::factory()
        ->hasAttached(Role::factory(['name' => 'admin']))
        ->create();
});

test('users can view their profile', function () {
    $this->actingAs($this->user)
        ->get('/profile')
        ->assertOk()
        ->assertSee($this->user->name);
});

test('users cannot view other profiles without permission', function () {
    $otherUser = User::factory()->create();

    $this->actingAs($this->user)
        ->get("/users/{$otherUser->id}")
        ->assertForbidden();
});

test('admin can view all users', function () {
    $this->actingAs($this->admin)
        ->get('/admin/users')
        ->assertOk()
        ->assertViewHas('users');
});

test('user can update their profile', function () {
    $this->actingAs($this->user)
        ->patch('/profile', [
            'name' => 'Updated Name',
            'email' => 'updated@example.com',
        ])
        ->assertRedirect('/profile')
        ->assertSessionHas('status', 'profile-updated');

    expect($this->user->fresh())
        ->name->toBe('Updated Name')
        ->email->toBe('updated@example.com');
});

dataset('invalid_emails', [
    'not-an-email',
    '@example.com',
    'user@',
    '',
]);

test('registration fails with invalid email', function ($email) {
    $this->post('/register', [
        'name' => 'Test User',
        'email' => $email,
        'password' => 'Password123!',
        'password_confirmation' => 'Password123!',
    ])->assertSessionHasErrors('email');
})->with('invalid_emails');
```

### API Test
```php
<?php

use App\Models\User;
use Laravel\Sanctum\Sanctum;

test('authenticated users can access api', function () {
    $user = User::factory()->create();

    Sanctum::actingAs($user);

    $this->getJson('/api/user')
        ->assertOk()
        ->assertJson([
            'email' => $user->email,
        ]);
});

test('unauthenticated users cannot access api', function () {
    $this->getJson('/api/user')
        ->assertUnauthorized();
});

test('can create user via api', function () {
    $admin = User::factory()->admin()->create();

    Sanctum::actingAs($admin);

    $userData = [
        'name' => 'New User',
        'email' => 'new@example.com',
        'password' => 'Password123!',
        'password_confirmation' => 'Password123!',
    ];

    $response = $this->postJson('/api/users', $userData)
        ->assertCreated()
        ->assertJsonStructure([
            'data' => ['id', 'name', 'email'],
        ]);

    $this->assertDatabaseHas('users', [
        'email' => 'new@example.com',
    ]);
});

test('api returns paginated users', function () {
    User::factory()->count(30)->create();

    $admin = User::factory()->admin()->create();
    Sanctum::actingAs($admin);

    $this->getJson('/api/users')
        ->assertOk()
        ->assertJsonCount(20, 'data')
        ->assertJsonStructure([
            'data' => [
                '*' => ['id', 'name', 'email'],
            ],
            'links',
            'meta',
        ]);
});
```

## Artisan Commands

```php
<?php

namespace App\Console\Commands;

use App\Models\User;
use App\Services\UserService;
use Illuminate\Console\Command;

class CleanupInactiveUsers extends Command
{
    /**
     * The name and signature of the console command.
     *
     * @var string
     */
    protected $signature = 'users:cleanup
                            {--days=30 : Number of days of inactivity}
                            {--dry-run : Run without actually deleting}';

    /**
     * The console command description.
     *
     * @var string
     */
    protected $description = 'Clean up inactive users';

    /**
     * Execute the console command.
     */
    public function handle(UserService $userService): int
    {
        $days = $this->option('days');
        $dryRun = $this->option('dry-run');

        $this->info("Finding users inactive for {$days} days...");

        $users = User::where('last_login_at', '<', now()->subDays($days))
            ->where('status', 'pending')
            ->get();

        $this->table(
            ['ID', 'Name', 'Email', 'Last Login'],
            $users->map(fn ($u) => [
                $u->id,
                $u->name,
                $u->email,
                $u->last_login_at?->diffForHumans() ?? 'Never',
            ])
        );

        if ($users->isEmpty()) {
            $this->info('No inactive users found.');
            return Command::SUCCESS;
        }

        if ($dryRun) {
            $this->warn('Dry run mode - no users were deleted.');
            return Command::SUCCESS;
        }

        if ($this->confirm("Delete {$users->count()} users?")) {
            $bar = $this->output->createProgressBar($users->count());

            foreach ($users as $user) {
                $userService->delete($user);
                $bar->advance();
            }

            $bar->finish();
            $this->newLine();
            $this->info('Users cleaned up successfully.');
        }

        return Command::SUCCESS;
    }
}
```

## Configuration Files

### Laravel Pint (pint.json)
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
        "blank_line_after_opening_tag": true,
        "blank_line_before_statement": {
            "statements": ["return", "try"]
        },
        "cast_spaces": {
            "space": "single"
        },
        "concat_space": {
            "spacing": "one"
        },
        "declare_strict_types": true,
        "method_argument_space": {
            "on_multiline": "ensure_fully_multiline"
        },
        "no_unused_imports": true,
        "not_operator_with_successor_space": true,
        "ordered_imports": {
            "sort_algorithm": "alpha"
        },
        "phpdoc_align": {
            "align": "left"
        },
        "phpdoc_order": true,
        "phpdoc_separation": true,
        "single_quote": true,
        "trailing_comma_in_multiline": {
            "elements": ["arrays", "arguments", "parameters"]
        },
        "yoda_style": false
    }
}
```

---
*Last Updated: [Date]*
*Laravel Version: 11.x*
*PHP Version: 8.2+*
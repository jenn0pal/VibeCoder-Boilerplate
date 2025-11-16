# PHP Technology Stack

## Core Technologies

### Runtime
| Technology | Version | Purpose | Documentation |
|------------|---------|---------|---------------|
| PHP | 8.2+ | Runtime environment | https://www.php.net/docs.php |
| Composer | 2.6+ | Package manager | https://getcomposer.org/doc/ |

### Common PHP Frameworks (Choose One)
| Technology | Version | Purpose | Documentation |
|------------|---------|---------|---------------|
| Symfony | 7.0+ | Full-stack framework | https://symfony.com/doc/current/index.html |
| Slim | 4.12+ | Micro framework | https://www.slimframework.com/docs/ |
| CodeIgniter | 4.4+ | Lightweight framework | https://codeigniter.com/user_guide/ |
| CakePHP | 5.0+ | Rapid development | https://book.cakephp.org/ |

### Database
| Technology | Version | Purpose | Documentation |
|------------|---------|---------|---------------|
| MySQL | 8.0+ | Relational database | https://dev.mysql.com/doc/ |
| PostgreSQL | 14+ | Relational database (alt) | https://www.postgresql.org/docs/ |
| PDO | Built-in | Database abstraction | https://www.php.net/manual/en/book.pdo.php |

### Caching
| Technology | Version | Purpose | Documentation |
|------------|---------|---------|---------------|
| Redis | 5.0+ | Cache & sessions | https://redis.io/docs/ |
| Memcached | 1.6+ | Distributed cache (alt) | https://www.memcached.org/ |
| APCu | Latest | Opcode cache | https://www.php.net/manual/en/book.apcu.php |

## Development Tools

### Code Quality
| Technology | Version | Purpose | Documentation |
|------------|---------|---------|---------------|
| PHP CS Fixer | 3.48+ | Code formatter | https://cs.symfony.com/ |
| PHP_CodeSniffer | 3.8+ | Code standards | https://github.com/squizlabs/PHP_CodeSniffer |
| PHPStan | 1.10+ | Static analysis | https://phpstan.org/user-guide/getting-started |
| Psalm | 5.20+ | Static analysis (alt) | https://psalm.dev/docs/ |

### Testing
| Technology | Version | Purpose | Documentation |
|------------|---------|---------|---------------|
| PHPUnit | 10.5+ | Test framework | https://phpunit.de/documentation.html |
| Pest | 2.33+ | Testing framework (modern) | https://pestphp.com/docs |
| Mockery | 1.6+ | Mocking framework | https://docs.mockery.io/ |
| Faker | 1.23+ | Fake data generation | https://fakerphp.github.io/ |

### Development
| Technology | Version | Purpose | Documentation |
|------------|---------|---------|---------------|
| Xdebug | 3.3+ | Debugger | https://xdebug.org/docs/ |
| PHP Debug Bar | 1.18+ | Debug toolbar | http://phpdebugbar.com/ |
| Whoops | 2.15+ | Error handler | https://filp.github.io/whoops/ |

## Package Management

### Primary Package Manager
- **Tool:** Composer
- **Lock File:** composer.lock
- **Configuration:** composer.json

### Common Commands
```bash
# Initialize new project
composer init

# Add dependencies
composer require vendor/package
composer require --dev vendor/package

# Update dependencies
composer update
composer update vendor/package

# Autoload optimization
composer dump-autoload -o

# Validate composer.json
composer validate

# Check for security issues
composer audit
```

## Project Structure (Generic)

### Recommended Structure
```
project/
├── config/            # Configuration files
├── public/            # Web root (index.php)
├── src/               # Application source code
│   ├── Controllers/   # HTTP controllers
│   ├── Models/        # Data models
│   ├── Services/      # Business logic
│   └── Utils/         # Utility classes
├── tests/             # Test files
│   ├── Unit/          # Unit tests
│   └── Integration/   # Integration tests
├── vendor/            # Composer dependencies
├── .env.example       # Environment template
├── composer.json      # Dependencies
└── composer.lock      # Locked versions
```

### PSR Standards
- **PSR-4:** Autoloading standard
- **PSR-12:** Extended coding style
- **PSR-7:** HTTP message interfaces
- **PSR-15:** HTTP handlers
- **PSR-3:** Logger interface

## Database Configuration

### PDO Connection (MySQL)
```php
<?php
$host = getenv('DB_HOST') ?: '127.0.0.1';
$port = getenv('DB_PORT') ?: '3306';
$dbname = getenv('DB_NAME');
$username = getenv('DB_USER');
$password = getenv('DB_PASSWORD');

$dsn = "mysql:host=$host;port=$port;dbname=$dbname;charset=utf8mb4";

try {
    $pdo = new PDO($dsn, $username, $password, [
        PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION,
        PDO::ATTR_DEFAULT_FETCH_MODE => PDO::FETCH_ASSOC,
        PDO::ATTR_EMULATE_PREPARES => false,
    ]);
} catch (PDOException $e) {
    error_log('Database connection failed: ' . $e->getMessage());
    throw $e;
}
```

### PDO Connection (PostgreSQL)
```php
<?php
$dsn = "pgsql:host=$host;port=5432;dbname=$dbname;sslmode=require";

$pdo = new PDO($dsn, $username, $password, [
    PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION,
    PDO::ATTR_DEFAULT_FETCH_MODE => PDO::FETCH_ASSOC,
]);
```

## Deployment

### Web Server
- **Nginx 1.24+** or **Apache 2.4+**
- **PHP-FPM 8.2+** (recommended over mod_php)

### Nginx Configuration
```nginx
server {
    listen 80;
    server_name example.com;
    root /var/www/public;
    index index.php;

    location / {
        try_files $uri $uri/ /index.php?$query_string;
    }

    location ~ \.php$ {
        fastcgi_pass unix:/var/run/php/php8.2-fpm.sock;
        fastcgi_index index.php;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    }

    location ~ /\.(?!well-known).* {
        deny all;
    }
}
```

### PHP-FPM Configuration
```ini
; /etc/php/8.2/fpm/pool.d/www.conf
pm = dynamic
pm.max_children = 50
pm.start_servers = 5
pm.min_spare_servers = 5
pm.max_spare_servers = 35
pm.max_requests = 500
```

## Security Configuration

### php.ini Settings (Production)
```ini
; Error handling
display_errors = Off
log_errors = On
error_reporting = E_ALL
error_log = /var/log/php/error.log

; Security
expose_php = Off
allow_url_fopen = Off
allow_url_include = Off
session.cookie_httponly = 1
session.cookie_secure = 1
session.cookie_samesite = "Strict"
session.use_strict_mode = 1

; Performance
opcache.enable = 1
opcache.memory_consumption = 128
opcache.interned_strings_buffer = 8
opcache.max_accelerated_files = 10000
opcache.validate_timestamps = 0
realpath_cache_size = 4096K
```

### Environment Variables
```php
<?php
// Use vlucas/phpdotenv for .env file support
require_once __DIR__ . '/vendor/autoload.php';

$dotenv = Dotenv\Dotenv::createImmutable(__DIR__);
$dotenv->load();

// Access variables
$dbHost = $_ENV['DB_HOST'];
$apiKey = $_ENV['API_KEY'];
```

## Environment Variables

### Required
| Variable | Purpose | Example |
|----------|---------|---------|
| DB_HOST | Database host | 127.0.0.1 |
| DB_NAME | Database name | myapp_db |
| DB_USER | Database user | root |
| DB_PASSWORD | Database password | secret |
| APP_ENV | Environment | production |

### Optional
| Variable | Purpose | Default |
|----------|---------|---------|
| DB_PORT | Database port | 3306 |
| REDIS_HOST | Redis server | 127.0.0.1 |
| REDIS_PORT | Redis port | 6379 |
| LOG_LEVEL | Logging level | info |

## Performance Targets

### Response Times
- **HTML Pages:** < 200ms (p95)
- **API Endpoints:** < 100ms (p95)
- **Database Queries:** < 50ms (p95)

### Optimization
- **OPcache:** Enabled in production
- **Autoload Optimization:** `composer dump-autoload -o`
- **Database:** Connection pooling, query optimization
- **Caching:** Redis/Memcached for sessions and data
- **Asset Optimization:** Minification, compression

### Scalability
- **Concurrent Users:** 500+
- **Requests/Second:** 50+

## Testing Strategy

### Test Types
```bash
# Run all tests
./vendor/bin/phpunit

# Run specific test suite
./vendor/bin/phpunit --testsuite=Unit
./vendor/bin/phpunit --testsuite=Integration

# Run with coverage
./vendor/bin/phpunit --coverage-html coverage/

# Using Pest
./vendor/bin/pest
./vendor/bin/pest --coverage
```

### Test Organization
```
tests/
├── Unit/              # Unit tests
├── Integration/       # Integration tests
├── bootstrap.php      # Test bootstrap
└── phpunit.xml        # PHPUnit config
```

### phpunit.xml
```xml
<?xml version="1.0" encoding="UTF-8"?>
<phpunit bootstrap="tests/bootstrap.php"
         colors="true"
         stopOnFailure="false">
    <testsuites>
        <testsuite name="Unit">
            <directory>tests/Unit</directory>
        </testsuite>
        <testsuite name="Integration">
            <directory>tests/Integration</directory>
        </testsuite>
    </testsuites>
    <coverage>
        <include>
            <directory suffix=".php">src</directory>
        </include>
    </coverage>
</phpunit>
```

## Logging & Monitoring

### Logging (Monolog)
```php
<?php
use Monolog\Logger;
use Monolog\Handler\StreamHandler;
use Monolog\Handler\RotatingFileHandler;

$log = new Logger('app');
$log->pushHandler(new StreamHandler('logs/app.log', Logger::INFO));
$log->pushHandler(new RotatingFileHandler('logs/error.log', 30, Logger::ERROR));

$log->info('User logged in', ['user_id' => 123]);
$log->error('Database error', ['query' => $sql]);
```

### Error Tracking
- **Sentry:** Production error tracking
- **Whoops:** Development error handler
- **Custom error handler:** Log to file/service

## Common Dependencies

### Recommended Packages
```json
{
    "require": {
        "php": "^8.2",
        "vlucas/phpdotenv": "^5.6",
        "monolog/monolog": "^3.5",
        "guzzlehttp/guzzle": "^7.8",
        "respect/validation": "^2.3"
    },
    "require-dev": {
        "phpunit/phpunit": "^10.5",
        "friendsofphp/php-cs-fixer": "^3.48",
        "phpstan/phpstan": "^1.10",
        "fakerphp/faker": "^1.23"
    }
}
```

### Useful Libraries
- **HTTP Client:** Guzzle
- **Validation:** Respect/Validation
- **Templating:** Twig, Plates
- **ORM:** Doctrine, Eloquent (standalone)
- **Router:** FastRoute, Symfony Router
- **Dependency Injection:** PHP-DI, Symfony DI

---
*Last Updated: 2025*
*PHP Version: 8.2+*
*Package Manager: Composer*
*PSR Standards: PSR-4, PSR-12, PSR-7, PSR-15, PSR-3*

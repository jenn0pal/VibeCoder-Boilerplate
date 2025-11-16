# PHP Dependency Upgrade: [Package Name]

> **Template for upgrading Composer packages in PHP projects**

## Overview

**Upgrade ID:** DEP-[ID]
**Date:** [YYYY-MM-DD]
**Package Name:** [vendor/package-name]
**Package Manager:** Composer
**Current Version:** [X.Y.Z]
**Target Version:** [A.B.C]
**Upgrade Type:** [Major/Minor/Patch]
**Priority:** [Critical/High/Medium/Low]

## Motivation

### Why Upgrade?
- [ ] Security vulnerability (CVE-[ID])
- [ ] Bug fix needed
- [ ] New feature required
- [ ] PHP version compatibility (e.g., PHP 8.3 support)
- [ ] Laravel compatibility (e.g., Laravel 11 support)
- [ ] Performance improvement
- [ ] Deprecation warning
- [ ] Other: [Specify]

### Security Information
**CVE ID:** [CVE-YYYY-XXXXX] (if applicable)
**Severity:** [Critical/High/Medium/Low]
**Advisory URL:** [Link to Packagist security advisory]

## Package Information

### Package Details
**Packagist Link:** https://packagist.org/packages/[vendor/package]
**Documentation:** [Link to docs]
**Changelog:** [Link to CHANGELOG.md or releases]
**License:** [MIT/Apache/BSD/etc.]

### Our Usage
**Where Used:**
- [Component/Feature 1]
- [Component/Feature 2]
- [Component/Feature 3]

**Usage Intensity:** [Heavy/Medium/Light]
**Critical Path:** [Yes/No]

## Breaking Changes Analysis

### Official Release Notes
**Release Notes URL:** [Link]
**Migration Guide URL:** [Link]

### Breaking Changes
#### Change 1: [Description]
**Affected Code:**
```php
// Before
OldClass::method($param);

// After
NewClass::method($param, $newParam);
```

**Impact:** [Description]
**Action Required:** [What needs to be changed]

## Compatibility Check

### PHP Version
**Current PHP:** [e.g., 8.2]
**Required PHP:** [e.g., 8.2+]
**Compatible:** [Yes/No]

### Laravel Version
**Current Laravel:** [e.g., 11.0]
**Required Laravel:** [e.g., 10.x - 11.x]
**Compatible:** [Yes/No]

### Dependency Compatibility
```bash
# Check compatibility
composer why vendor/package
composer why-not vendor/package [new-version]

# Check conflicts
composer update vendor/package --dry-run
```

**Dependency Conflicts:**
| Package | Current | Requires | Status |
|---------|---------|----------|--------|
| [package-1] | [X.Y.Z] | [^A.B] | ✅/⚠️/❌ |

## Pre-Upgrade Checklist

- [ ] Review changelog and breaking changes
- [ ] Check Laravel compatibility matrix
- [ ] Verify PHP version compatibility
- [ ] Review dependent packages
- [ ] Backup database
- [ ] Create feature branch
- [ ] Ensure tests pass on current version
- [ ] Check for deprecation warnings

## Upgrade Execution

### Step 1: Update composer.json
```bash
# Update specific package
composer require vendor/package:^A.B

# Or update with dependencies
composer update vendor/package --with-dependencies

# Dry run first
composer update vendor/package --dry-run
```

### Step 2: Install and Test
```bash
# Install
composer install

# Clear caches
php artisan cache:clear
php artisan config:clear
php artisan route:clear
php artisan view:clear

# Run tests
php artisan test
./vendor/bin/phpunit
```

### Step 3: Code Migration
**Files to Update:**
- [ ] [app/Services/ServiceName.php] - Update method calls
- [ ] [config/package.php] - Update configuration
- [ ] [app/Http/Controllers/ControllerName.php] - Update usage

**Code Changes:**
```php
// Example migration
// Old:
use Old\Namespace\Class;
$result = Class::method();

// New:
use New\Namespace\Class;
$result = Class::newMethod();
```

### Step 4: Configuration Updates
```php
// config/package.php
return [
    // Old config
    'option' => 'value',

    // New config (Laravel 11 style)
    'new_option' => env('PACKAGE_OPTION', 'default'),
];
```

## Testing

### Unit Tests
```bash
# Run all tests
php artisan test

# Run specific test
php artisan test --filter=PackageTest

# With coverage
php artisan test --coverage
```

### Integration Tests
- [ ] Test package functionality in isolation
- [ ] Test integration with Laravel features
- [ ] Test API endpoints using the package
- [ ] Test CLI commands
- [ ] Test queued jobs
- [ ] Test scheduled tasks

### Manual Testing Checklist
- [ ] [Feature 1 using this package]
- [ ] [Feature 2 using this package]
- [ ] [Feature 3 using this package]

## Rollback Plan

### Rollback Steps
```bash
# Revert composer.json
git checkout composer.json composer.lock

# Reinstall old version
composer install

# Clear caches
php artisan cache:clear
php artisan config:clear

# Verify
php artisan test
```

**Rollback Criteria:**
- Test failures > 5%
- Critical functionality broken
- Performance degradation > 20%
- Security issues introduced

## Deployment

### Staging Deployment
```bash
# On staging server
git pull origin feature/upgrade-package
composer install --no-dev --optimize-autoloader
php artisan migrate
php artisan config:cache
php artisan route:cache
php artisan view:cache
php artisan queue:restart
```

### Production Deployment
```bash
# Enable maintenance mode
php artisan down

# Deploy
git pull origin main
composer install --no-dev --optimize-autoloader
php artisan migrate --force
php artisan config:cache
php artisan route:cache
php artisan view:cache
php artisan queue:restart

# Disable maintenance mode
php artisan up
```

## Post-Upgrade Monitoring

### Metrics to Watch
- [ ] Error rate (target: < 0.1%)
- [ ] Response time (target: no degradation)
- [ ] Queue processing time
- [ ] Memory usage
- [ ] CPU usage

### Monitoring Period
- **Day 1:** Hourly checks
- **Day 2-3:** Every 4 hours
- **Week 1:** Daily checks

## Documentation Updates

- [ ] Update `docs/.claude/context/tech-stack.md`
- [ ] Update `composer.json` version constraints
- [ ] Update README.md if package usage changed
- [ ] Update API documentation
- [ ] Update team wiki/knowledge base

## PHP-Specific Considerations

### Service Provider Changes
```php
// Check if service provider registration changed
// config/app.php
'providers' => [
    // Old
    OldVendor\Package\ServiceProvider::class,

    // New (Laravel 11 auto-discovery)
    // No manual registration needed
],
```

### Facade Changes
```php
// Check facade changes
use OldVendor\Package\Facades\PackageFacade;

// May change to:
use NewVendor\Package\Facades\PackageFacade;
```

### Middleware Changes
```php
// Check middleware registration
// bootstrap/app.php (Laravel 11)
->withMiddleware(function (Middleware $middleware) {
    $middleware->append(PackageMiddleware::class);
})
```

## Common Laravel Packages

### Authentication
- **laravel/sanctum:** API authentication
- **laravel/passport:** OAuth2 server
- **spatie/laravel-permission:** Roles & permissions

### Utilities
- **spatie/laravel-query-builder:** API query building
- **spatie/laravel-medialibrary:** Media handling
- **barryvdh/laravel-debugbar:** Debug toolbar

### Testing
- **laravel/dusk:** Browser testing
- **mockery/mockery:** Mocking framework

---
**Status:** [Planning/In Progress/Testing/Complete/Rolled Back]
**Last Updated:** [YYYY-MM-DD]
**Owner:** [Name/Team]

---

## Quick Reference

### Composer Commands
```bash
# Show package info
composer show vendor/package

# Why is package installed
composer why vendor/package

# Check for updates
composer outdated

# Security audit
composer audit

# Validate composer.json
composer validate
```

### Laravel Commands
```bash
# Clear all caches
php artisan optimize:clear

# Rebuild caches
php artisan optimize

# Check package auto-discovery
composer dump-autoload
```

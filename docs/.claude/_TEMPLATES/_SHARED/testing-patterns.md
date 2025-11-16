# Testing Patterns

> **Universal testing principles across all stacks**
>
> Stack-specific testing tools and examples are in the respective stack directories.

## Testing Philosophy

### Test Pyramid

```
        /\
       /E2E\      ← Few (slow, expensive, comprehensive)
      /------\
     /Integration\  ← Some (moderate speed/cost, API/service level)
    /------------\
   /   Unit Tests  \ ← Many (fast, cheap, isolated)
  /----------------\
```

**Distribution guideline:**
- **Unit tests:** 70%
- **Integration tests:** 20%
- **E2E tests:** 10%

### Testing Principles

1. **Fast Feedback** - Tests should run quickly
2. **Isolated** - Tests should not depend on each other
3. **Repeatable** - Same input = same output
4. **Self-validating** - Pass/fail, no manual verification
5. **Timely** - Write tests before or with code (TDD/BDD)

## Test Coverage Requirements

### Minimum Coverage Targets

| Category | Target | Critical? |
|----------|--------|-----------|
| **Overall Coverage** | 80% | Enforced |
| **New Code** | 90% | Enforced |
| **Critical Paths** | 100% | Enforced |
| **Utilities** | 95% | Recommended |
| **UI Components** | 70% | Recommended |

### What to Test (Priority Order)

**Critical (Must Test):**
- [ ] Authentication & authorization
- [ ] Payment processing
- [ ] Data validation
- [ ] Security boundaries
- [ ] Error handling
- [ ] Database transactions

**High Priority:**
- [ ] Business logic
- [ ] API endpoints
- [ ] Form submissions
- [ ] State management
- [ ] File uploads
- [ ] Email sending

**Medium Priority:**
- [ ] UI components
- [ ] Routing
- [ ] Formatting functions
- [ ] Helpers/utilities
- [ ] Hooks/composables

**Low Priority:**
- [ ] Constants
- [ ] Configuration
- [ ] Simple getters/setters
- [ ] Type definitions

### What NOT to Test

- ❌ Third-party library internals
- ❌ Framework functionality
- ❌ Trivial getters/setters
- ❌ Configuration files
- ❌ Generated code
- ❌ External APIs (mock them instead)

## Test Organization

### Directory Structure

```
tests/
├── unit/                  # Isolated unit tests
│   ├── models/
│   ├── services/
│   ├── utils/
│   └── components/
├── integration/           # Multi-component tests
│   ├── api/
│   ├── database/
│   └── services/
├── e2e/                   # End-to-end tests
│   ├── user-flows/
│   └── critical-paths/
├── fixtures/              # Test data
│   ├── users.json
│   └── products.json
├── factories/             # Test data builders
├── mocks/                 # Mock implementations
└── helpers/               # Test utilities
```

### Naming Conventions

**Test Files:**
- Unit: `[module].test.[ext]` or `test_[module].[ext]`
- Integration: `[feature].integration.test.[ext]`
- E2E: `[flow].e2e.test.[ext]`

**Test Names:**
```
test_[method]_[scenario]_[expected_result]
```

**Examples:**
```javascript
// JavaScript
describe('UserService', () => {
  test('createUser_withValidData_returnsUser', () => { ... })
  test('createUser_withDuplicateEmail_throwsError', () => { ... })
  test('deleteUser_whenNotFound_throwsNotFoundError', () => { ... })
})
```

```python
# Python
class TestUserService:
    def test_create_user_with_valid_data_returns_user(self):
        ...

    def test_create_user_with_duplicate_email_raises_error(self):
        ...

    def test_delete_user_when_not_found_raises_not_found_error(self):
        ...
```

## Test Structure (AAA Pattern)

### Arrange-Act-Assert

```javascript
test('createUser_withValidData_returnsUser', () => {
  // Arrange - Set up test data and dependencies
  const userData = {
    email: 'test@example.com',
    password: 'SecurePass123!'
  }
  const userService = new UserService()

  // Act - Execute the code under test
  const result = userService.createUser(userData)

  // Assert - Verify the outcome
  expect(result).toBeDefined()
  expect(result.email).toBe(userData.email)
  expect(result.id).toBeDefined()
})
```

### Given-When-Then (BDD Style)

```python
def test_user_can_login_with_valid_credentials():
    # Given a registered user
    user = UserFactory.create(email="test@example.com")

    # When they attempt to login with correct credentials
    result = auth_service.login(
        email="test@example.com",
        password="correct_password"
    )

    # Then they should be successfully authenticated
    assert result.success is True
    assert result.user.id == user.id
    assert result.token is not None
```

## Test Data Management

### Fixtures

**Good Fixtures:**
- Minimal and focused
- Reusable across tests
- Version controlled
- Represent realistic data

**Example:**
```json
// tests/fixtures/users.json
{
  "validUser": {
    "email": "test@example.com",
    "name": "Test User",
    "role": "user"
  },
  "adminUser": {
    "email": "admin@example.com",
    "name": "Admin User",
    "role": "admin"
  }
}
```

### Factory Pattern

Build test data programmatically:

```javascript
// JavaScript
class UserFactory {
  static create(overrides = {}) {
    return {
      id: faker.datatype.uuid(),
      email: faker.internet.email(),
      name: faker.name.fullName(),
      createdAt: new Date(),
      ...overrides
    }
  }

  static createMany(count, overrides = {}) {
    return Array.from({ length: count }, () =>
      this.create(overrides)
    )
  }
}

// Usage
const user = UserFactory.create({ email: 'specific@example.com' })
const users = UserFactory.createMany(5)
```

```python
# Python (using factory_boy or custom)
class UserFactory:
    @staticmethod
    def create(**kwargs):
        defaults = {
            'id': str(uuid.uuid4()),
            'email': fake.email(),
            'name': fake.name(),
            'created_at': datetime.now(),
        }
        return User(**(defaults | kwargs))

    @classmethod
    def create_batch(cls, size, **kwargs):
        return [cls.create(**kwargs) for _ in range(size)]

# Usage
user = UserFactory.create(email='specific@example.com')
users = UserFactory.create_batch(5)
```

## Mocking & Stubbing

### When to Mock

**Mock external dependencies:**
- [ ] HTTP requests/API calls
- [ ] Database queries (in unit tests)
- [ ] File system operations
- [ ] Email/SMS services
- [ ] Payment gateways
- [ ] Date/time functions
- [ ] Random number generators

**Don't mock:**
- [ ] Code you own and control
- [ ] Simple value objects
- [ ] Constants
- [ ] Pure functions

### Mock Patterns

```javascript
// JavaScript (Jest example)
// Mock external API
jest.mock('../services/api', () => ({
  fetchUser: jest.fn()
}))

test('getUserProfile_whenApiSucceeds_returnsUser', async () => {
  // Arrange
  const mockUser = { id: 1, name: 'Test' }
  api.fetchUser.mockResolvedValue(mockUser)

  // Act
  const result = await getUserProfile(1)

  // Assert
  expect(result).toEqual(mockUser)
  expect(api.fetchUser).toHaveBeenCalledWith(1)
})
```

```python
# Python (pytest with unittest.mock)
from unittest.mock import Mock, patch

def test_get_user_profile_when_api_succeeds_returns_user():
    # Arrange
    mock_user = {'id': 1, 'name': 'Test'}

    with patch('services.api.fetch_user') as mock_fetch:
        mock_fetch.return_value = mock_user

        # Act
        result = get_user_profile(1)

        # Assert
        assert result == mock_user
        mock_fetch.assert_called_once_with(1)
```

## Test-Driven Development (TDD)

### Red-Green-Refactor Cycle

```
1. RED    → Write failing test
2. GREEN  → Write minimal code to pass
3. REFACTOR → Improve code quality
4. REPEAT
```

### TDD Workflow Example

```javascript
// 1. RED - Write failing test
test('calculateDiscount_withValidCoupon_returnsDiscountedPrice', () => {
  const price = 100
  const coupon = { code: 'SAVE20', discount: 0.20 }

  const result = calculateDiscount(price, coupon)

  expect(result).toBe(80)
})
// Test fails - function doesn't exist yet

// 2. GREEN - Minimal implementation
function calculateDiscount(price, coupon) {
  return price - (price * coupon.discount)
}
// Test passes

// 3. REFACTOR - Improve
function calculateDiscount(price, coupon) {
  if (!price || price < 0) {
    throw new Error('Invalid price')
  }

  if (!coupon || !coupon.discount) {
    return price
  }

  const discount = price * coupon.discount
  return Math.max(0, price - discount)
}

// Add more tests for edge cases
test('calculateDiscount_withInvalidPrice_throwsError', () => {
  expect(() => calculateDiscount(-10, { discount: 0.2 }))
    .toThrow('Invalid price')
})
```

## Integration Testing

### Database Integration Tests

**Setup:**
- Use test database
- Run migrations before tests
- Clean database between tests
- Use transactions for rollback

**Patterns:**
```python
# Python example
class TestUserRepository:
    @pytest.fixture(autouse=True)
    def setup(self, db):
        """Run before each test."""
        self.repo = UserRepository()
        yield
        # Cleanup after test
        db.session.rollback()

    def test_create_user_persists_to_database(self, db):
        # Arrange
        user_data = {"email": "test@example.com", "name": "Test"}

        # Act
        user = self.repo.create(user_data)
        db.session.commit()

        # Assert
        found = self.repo.find_by_email("test@example.com")
        assert found is not None
        assert found.id == user.id
```

### API Integration Tests

Test full request/response cycle:

```javascript
// JavaScript (with supertest)
describe('POST /api/users', () => {
  test('createUser_withValidData_returns201AndUser', async () => {
    const userData = {
      email: 'test@example.com',
      password: 'SecurePass123!',
      name: 'Test User'
    }

    const response = await request(app)
      .post('/api/users')
      .send(userData)
      .expect(201)

    expect(response.body).toMatchObject({
      id: expect.any(String),
      email: userData.email,
      name: userData.name
    })
    expect(response.body.password).toBeUndefined()
  })

  test('createUser_withDuplicateEmail_returns409', async () => {
    // Arrange - create existing user
    await User.create({ email: 'existing@example.com' })

    // Act
    const response = await request(app)
      .post('/api/users')
      .send({ email: 'existing@example.com', password: 'pass' })
      .expect(409)

    // Assert
    expect(response.body.error).toContain('already exists')
  })
})
```

## E2E Testing

### Critical User Flows

Test complete user journeys:

**E-commerce example:**
1. Browse products → View details → Add to cart → Checkout → Payment → Confirmation

**SaaS example:**
1. Sign up → Verify email → Onboarding → Create project → Invite team → Use feature

### E2E Best Practices

- ✅ Test happy paths and critical error scenarios
- ✅ Use realistic test data
- ✅ Run in isolated environment
- ✅ Clean up test data after execution
- ✅ Keep tests independent
- ❌ Don't test every edge case (use unit tests)
- ❌ Don't make tests depend on each other
- ❌ Don't use production data

## CI/CD Integration

### Test Automation

```yaml
# Example CI configuration
name: Tests

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v3

      - name: Install dependencies
        run: npm install  # or pip install, composer install

      - name: Run linter
        run: npm run lint

      - name: Run unit tests
        run: npm run test:unit

      - name: Run integration tests
        run: npm run test:integration
        env:
          DATABASE_URL: postgres://test

      - name: Run E2E tests
        run: npm run test:e2e

      - name: Upload coverage
        uses: codecov/codecov-action@v3
        with:
          files: ./coverage/lcov.info

      - name: Check coverage threshold
        run: npm run test:coverage
        # Fails if coverage < 80%
```

### Coverage Gates

Fail builds if coverage drops below threshold:

```json
// package.json (Jest)
{
  "jest": {
    "coverageThreshold": {
      "global": {
        "branches": 80,
        "functions": 80,
        "lines": 80,
        "statements": 80
      }
    }
  }
}
```

```ini
# pytest.ini
[pytest]
addopts =
    --cov=src
    --cov-fail-under=80
    --cov-report=html
    --cov-report=term-missing
```

## Performance Testing

### Load Testing Basics

**Tools:** k6, Artillery, Apache JMeter, Locust

**Key Metrics:**
- Response time (p50, p95, p99)
- Throughput (requests/second)
- Error rate
- Resource utilization

**Example (k6):**
```javascript
import http from 'k6/http'
import { check, sleep } from 'k6'

export const options = {
  vus: 100,        // 100 virtual users
  duration: '30s', // 30 second test
  thresholds: {
    http_req_duration: ['p(95)<500'], // 95% of requests < 500ms
    http_req_failed: ['rate<0.01'],   // Error rate < 1%
  },
}

export default function () {
  const res = http.get('https://api.example.com/users')

  check(res, {
    'status is 200': (r) => r.status === 200,
    'response time < 500ms': (r) => r.timings.duration < 500,
  })

  sleep(1)
}
```

## Test Maintenance

### When Tests Fail

**Investigate:**
1. Is the test correct?
2. Is the code change intentional?
3. Does test need updating?
4. Is it a flaky test?

**Fix flaky tests immediately:**
- Identify root cause (timing, dependencies, randomness)
- Add proper waits/retries
- Ensure test isolation
- Consider quarantining if can't fix quickly

### Refactoring Tests

**Signs tests need refactoring:**
- Duplicated setup code
- Tests are hard to understand
- Tests take too long to run
- Brittle tests (break with small changes)

**Refactoring techniques:**
- Extract test helpers
- Use factories for test data
- Share fixtures appropriately
- Parameterize similar tests
- Improve test names

---

**Last Updated:** 2025-01-16
**Version:** 1.0

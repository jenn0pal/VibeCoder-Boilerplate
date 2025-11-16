# JavaScript/TypeScript Project Conventions

## Code Style

### General Principles
- **ES6+ Features:** Use modern JavaScript features
- **TypeScript First:** Prefer TypeScript for type safety
- **Functional Programming:** Favor immutability and pure functions
- **Async/Await:** Use over callbacks and raw promises

### Naming Conventions
| Type | Convention | Example |
|------|------------|---------|
| Variables | camelCase | `userName`, `isActive` |
| Constants | UPPER_SNAKE_CASE | `MAX_RETRY_COUNT`, `API_URL` |
| Functions | camelCase | `getUserById()`, `calculateTotal()` |
| Classes | PascalCase | `UserService`, `DatabaseConnection` |
| Interfaces | PascalCase with 'I' | `IUserRepository`, `IAuthService` |
| Types | PascalCase | `UserRole`, `ApiResponse` |
| Enums | PascalCase | `Status`, `ErrorCode` |
| Files | kebab-case | `user-service.ts`, `auth-utils.js` |
| React Components | PascalCase | `UserProfile.tsx`, `NavBar.jsx` |
| React Hooks | camelCase with 'use' | `useAuth()`, `useLocalStorage()` |
| Private fields | # prefix | `#privateField` |

### File Organization
```
src/
├── components/          # React/Vue components
│   ├── common/         # Shared components
│   ├── features/       # Feature-specific components
│   └── layouts/        # Layout components
├── hooks/              # Custom React hooks
├── services/           # API and business logic
├── utils/              # Utility functions
├── types/              # TypeScript type definitions
├── constants/          # Application constants
├── store/              # State management (Redux/Zustand)
├── styles/             # Global styles
└── config/             # Configuration files
```

### Import Order (ESLint compatible)
```javascript
// Node built-ins
import fs from 'fs';
import path from 'path';

// External dependencies
import React, { useState, useEffect } from 'react';
import axios from 'axios';
import { z } from 'zod';

// Internal aliases
import { UserService } from '@/services';
import { Button } from '@/components';
import { API_URL } from '@/constants';

// Relative imports
import { formatDate } from './utils';
import type { UserProps } from './types';

// Styles (always last)
import styles from './Component.module.css';
```

## TypeScript Configuration

### tsconfig.json
```json
{
  "compilerOptions": {
    "target": "ES2022",
    "lib": ["ES2022", "DOM"],
    "module": "ESNext",
    "moduleResolution": "node",
    "jsx": "react-jsx",
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true,
    "resolveJsonModule": true,
    "allowJs": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true,
    "noImplicitReturns": true,
    "noFallthroughCasesInSwitch": true,
    "baseUrl": ".",
    "paths": {
      "@/*": ["src/*"]
    }
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules", "dist", "build"]
}
```

### Type Definitions
```typescript
// Define clear interfaces
interface User {
  id: string;
  email: string;
  name: string;
  role: UserRole;
  createdAt: Date;
}

// Use type for unions and intersections
type UserRole = 'admin' | 'user' | 'guest';

// Generics for reusable types
interface ApiResponse<T> {
  data: T;
  error: string | null;
  loading: boolean;
}

// Utility types effectively
type PartialUser = Partial<User>;
type RequiredUser = Required<User>;
type ReadonlyUser = Readonly<User>;
```

## React Patterns

### Component Structure
```tsx
import React, { useState, useCallback, memo } from 'react';
import { useTranslation } from 'react-i18next';
import styles from './UserProfile.module.css';

interface UserProfileProps {
  userId: string;
  onUpdate?: (user: User) => void;
}

/**
 * UserProfile displays and manages user profile information
 * @component
 */
export const UserProfile: React.FC<UserProfileProps> = memo(({
  userId,
  onUpdate
}) => {
  const { t } = useTranslation();
  const [isEditing, setIsEditing] = useState(false);
  const { data: user, loading, error } = useUser(userId);

  const handleSave = useCallback(async (updatedUser: User) => {
    try {
      await updateUser(updatedUser);
      onUpdate?.(updatedUser);
      setIsEditing(false);
    } catch (error) {
      console.error('Failed to update user:', error);
    }
  }, [onUpdate]);

  if (loading) return <LoadingSpinner />;
  if (error) return <ErrorMessage error={error} />;
  if (!user) return null;

  return (
    <div className={styles.container}>
      {/* Component JSX */}
    </div>
  );
});

UserProfile.displayName = 'UserProfile';
```

### Custom Hooks
```typescript
import { useState, useEffect, useCallback } from 'react';

/**
 * Custom hook for managing API calls
 * @param url - API endpoint URL
 * @returns Data, loading state, and error
 */
export function useApi<T>(url: string) {
  const [data, setData] = useState<T | null>(null);
  const [loading, setLoading] = useState(true);
  const [error, setError] = useState<Error | null>(null);

  const refetch = useCallback(async () => {
    setLoading(true);
    setError(null);
    try {
      const response = await fetch(url);
      if (!response.ok) throw new Error('Failed to fetch');
      const data = await response.json();
      setData(data);
    } catch (err) {
      setError(err as Error);
    } finally {
      setLoading(false);
    }
  }, [url]);

  useEffect(() => {
    refetch();
  }, [refetch]);

  return { data, loading, error, refetch };
}
```

## State Management

### Zustand Store
```typescript
import { create } from 'zustand';
import { devtools, persist } from 'zustand/middleware';

interface AuthState {
  user: User | null;
  token: string | null;
  isAuthenticated: boolean;
  login: (email: string, password: string) => Promise<void>;
  logout: () => void;
  updateUser: (user: Partial<User>) => void;
}

export const useAuthStore = create<AuthState>()(
  devtools(
    persist(
      (set, get) => ({
        user: null,
        token: null,
        isAuthenticated: false,

        login: async (email, password) => {
          try {
            const response = await authService.login(email, password);
            set({
              user: response.user,
              token: response.token,
              isAuthenticated: true,
            });
          } catch (error) {
            throw error;
          }
        },

        logout: () => {
          set({
            user: null,
            token: null,
            isAuthenticated: false,
          });
        },

        updateUser: (updates) => {
          const currentUser = get().user;
          if (currentUser) {
            set({
              user: { ...currentUser, ...updates },
            });
          }
        },
      }),
      {
        name: 'auth-storage',
        partialize: (state) => ({
          token: state.token,
          user: state.user,
        }),
      }
    )
  )
);
```

## Error Handling

### Custom Error Classes
```javascript
export class AppError extends Error {
  constructor(message, code, statusCode = 500, details = null) {
    super(message);
    this.name = 'AppError';
    this.code = code;
    this.statusCode = statusCode;
    this.details = details;
    Error.captureStackTrace(this, this.constructor);
  }
}

export class ValidationError extends AppError {
  constructor(field, message) {
    super(message, 'VALIDATION_ERROR', 400, { field });
    this.name = 'ValidationError';
  }
}

export class AuthenticationError extends AppError {
  constructor(message = 'Authentication failed') {
    super(message, 'AUTH_ERROR', 401);
    this.name = 'AuthenticationError';
  }
}
```

### Error Boundaries (React)
```tsx
import React, { Component, ErrorInfo, ReactNode } from 'react';

interface Props {
  children: ReactNode;
  fallback?: ReactNode;
}

interface State {
  hasError: boolean;
  error: Error | null;
}

export class ErrorBoundary extends Component<Props, State> {
  state: State = {
    hasError: false,
    error: null,
  };

  static getDerivedStateFromError(error: Error): State {
    return { hasError: true, error };
  }

  componentDidCatch(error: Error, errorInfo: ErrorInfo) {
    console.error('Error caught by boundary:', error, errorInfo);
    // Send to error tracking service
    trackError(error, errorInfo);
  }

  render() {
    if (this.state.hasError) {
      return (
        this.props.fallback || (
          <div>
            <h2>Something went wrong.</h2>
            <details>{this.state.error?.message}</details>
          </div>
        )
      );
    }

    return this.props.children;
  }
}
```

## Testing Patterns

### Jest/Vitest Unit Tests
```javascript
import { describe, it, expect, beforeEach, jest } from '@jest/globals';
import { render, screen, fireEvent, waitFor } from '@testing-library/react';
import userEvent from '@testing-library/user-event';
import { UserProfile } from './UserProfile';

describe('UserProfile Component', () => {
  let mockUser;

  beforeEach(() => {
    mockUser = {
      id: '1',
      name: 'John Doe',
      email: 'john@example.com',
    };
  });

  it('should render user information', () => {
    render(<UserProfile user={mockUser} />);

    expect(screen.getByText(mockUser.name)).toBeInTheDocument();
    expect(screen.getByText(mockUser.email)).toBeInTheDocument();
  });

  it('should handle edit mode', async () => {
    const user = userEvent.setup();
    const onUpdate = jest.fn();

    render(<UserProfile user={mockUser} onUpdate={onUpdate} />);

    // Click edit button
    await user.click(screen.getByRole('button', { name: /edit/i }));

    // Change name
    const nameInput = screen.getByLabelText(/name/i);
    await user.clear(nameInput);
    await user.type(nameInput, 'Jane Doe');

    // Save changes
    await user.click(screen.getByRole('button', { name: /save/i }));

    await waitFor(() => {
      expect(onUpdate).toHaveBeenCalledWith(
        expect.objectContaining({
          name: 'Jane Doe',
        })
      );
    });
  });
});
```

### Testing Services
```javascript
import { describe, it, expect, jest, beforeEach } from '@jest/globals';
import { UserService } from './user-service';
import axios from 'axios';

jest.mock('axios');

describe('UserService', () => {
  let service;

  beforeEach(() => {
    service = new UserService();
    jest.clearAllMocks();
  });

  describe('getUser', () => {
    it('should fetch user successfully', async () => {
      const mockUser = { id: 1, name: 'Test User' };
      axios.get.mockResolvedValueOnce({ data: mockUser });

      const result = await service.getUser(1);

      expect(axios.get).toHaveBeenCalledWith('/api/users/1');
      expect(result).toEqual(mockUser);
    });

    it('should handle errors', async () => {
      const error = new Error('Network error');
      axios.get.mockRejectedValueOnce(error);

      await expect(service.getUser(1)).rejects.toThrow('Failed to fetch user');
    });
  });
});
```

## API Patterns

### Axios Service Layer
```typescript
import axios, { AxiosInstance, AxiosRequestConfig } from 'axios';

class ApiService {
  private client: AxiosInstance;

  constructor(baseURL: string = process.env.REACT_APP_API_URL || '') {
    this.client = axios.create({
      baseURL,
      timeout: 10000,
      headers: {
        'Content-Type': 'application/json',
      },
    });

    this.setupInterceptors();
  }

  private setupInterceptors(): void {
    // Request interceptor
    this.client.interceptors.request.use(
      (config) => {
        const token = localStorage.getItem('token');
        if (token) {
          config.headers.Authorization = `Bearer ${token}`;
        }
        return config;
      },
      (error) => Promise.reject(error)
    );

    // Response interceptor
    this.client.interceptors.response.use(
      (response) => response.data,
      async (error) => {
        if (error.response?.status === 401) {
          // Handle token refresh
          await this.refreshToken();
        }
        return Promise.reject(this.transformError(error));
      }
    );
  }

  private transformError(error: any): AppError {
    if (error.response) {
      return new AppError(
        error.response.data.message || 'Request failed',
        error.response.data.code || 'API_ERROR',
        error.response.status
      );
    }
    return new AppError('Network error', 'NETWORK_ERROR', 0);
  }

  async get<T>(url: string, config?: AxiosRequestConfig): Promise<T> {
    return this.client.get(url, config);
  }

  async post<T>(url: string, data?: any, config?: AxiosRequestConfig): Promise<T> {
    return this.client.post(url, data, config);
  }

  async put<T>(url: string, data?: any, config?: AxiosRequestConfig): Promise<T> {
    return this.client.put(url, data, config);
  }

  async delete<T>(url: string, config?: AxiosRequestConfig): Promise<T> {
    return this.client.delete(url, config);
  }
}

export const apiService = new ApiService();
```

## Performance Optimization

### React Performance
```tsx
import React, { useMemo, useCallback, lazy, Suspense } from 'react';

// Lazy loading
const HeavyComponent = lazy(() => import('./HeavyComponent'));

// Memoization
export const ExpensiveList: React.FC<{ items: Item[] }> = ({ items }) => {
  // Memoize expensive calculations
  const processedItems = useMemo(() => {
    return items
      .filter((item) => item.active)
      .sort((a, b) => b.priority - a.priority)
      .map((item) => ({
        ...item,
        displayName: formatDisplayName(item),
      }));
  }, [items]);

  // Memoize callbacks
  const handleItemClick = useCallback((id: string) => {
    console.log('Item clicked:', id);
  }, []);

  return (
    <Suspense fallback={<LoadingSpinner />}>
      <div>
        {processedItems.map((item) => (
          <Item key={item.id} item={item} onClick={handleItemClick} />
        ))}
      </div>
    </Suspense>
  );
};

// React.memo for component memoization
export const Item = React.memo<ItemProps>(
  ({ item, onClick }) => {
    return (
      <div onClick={() => onClick(item.id)}>
        {item.displayName}
      </div>
    );
  },
  (prevProps, nextProps) => {
    // Custom comparison
    return (
      prevProps.item.id === nextProps.item.id &&
      prevProps.item.displayName === nextProps.item.displayName
    );
  }
);
```

### Debouncing/Throttling
```javascript
// Debounce implementation
export function debounce(func, delay) {
  let timeoutId;
  return function (...args) {
    clearTimeout(timeoutId);
    timeoutId = setTimeout(() => func.apply(this, args), delay);
  };
}

// Throttle implementation
export function throttle(func, limit) {
  let inThrottle;
  return function (...args) {
    if (!inThrottle) {
      func.apply(this, args);
      inThrottle = true;
      setTimeout(() => (inThrottle = false), limit);
    }
  };
}

// Usage in React
const SearchInput = () => {
  const [query, setQuery] = useState('');

  const debouncedSearch = useMemo(
    () => debounce((q) => performSearch(q), 500),
    []
  );

  const handleChange = (e) => {
    setQuery(e.target.value);
    debouncedSearch(e.target.value);
  };

  return <input value={query} onChange={handleChange} />;
};
```

## Security Best Practices

### Input Validation (Zod)
```typescript
import { z } from 'zod';

// Define schemas
const UserSchema = z.object({
  email: z.string().email('Invalid email format'),
  password: z
    .string()
    .min(8, 'Password must be at least 8 characters')
    .regex(/[A-Z]/, 'Must contain uppercase letter')
    .regex(/[0-9]/, 'Must contain number'),
  age: z.number().min(18).max(120),
  role: z.enum(['admin', 'user', 'guest']),
});

// Validate input
export function validateUser(data: unknown): User {
  try {
    return UserSchema.parse(data);
  } catch (error) {
    if (error instanceof z.ZodError) {
      throw new ValidationError(error.errors);
    }
    throw error;
  }
}

// XSS Prevention
export function sanitizeHtml(html: string): string {
  return DOMPurify.sanitize(html, {
    ALLOWED_TAGS: ['b', 'i', 'em', 'strong', 'a'],
    ALLOWED_ATTR: ['href'],
  });
}
```

## ESLint Configuration
```javascript
module.exports = {
  root: true,
  parser: '@typescript-eslint/parser',
  plugins: ['@typescript-eslint', 'react', 'react-hooks'],
  extends: [
    'eslint:recommended',
    'plugin:@typescript-eslint/recommended',
    'plugin:react/recommended',
    'plugin:react-hooks/recommended',
    'prettier',
  ],
  rules: {
    'no-console': ['warn', { allow: ['warn', 'error'] }],
    'no-unused-vars': 'off',
    '@typescript-eslint/no-unused-vars': ['error', { argsIgnorePattern: '^_' }],
    '@typescript-eslint/explicit-module-boundary-types': 'off',
    'react/react-in-jsx-scope': 'off',
    'react/prop-types': 'off',
    'react-hooks/rules-of-hooks': 'error',
    'react-hooks/exhaustive-deps': 'warn',
  },
  settings: {
    react: {
      version: 'detect',
    },
  },
};
```

---
*Last Updated: [Date]*
*Node Version: 18+*
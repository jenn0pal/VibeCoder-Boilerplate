# Vue 3 SPA + Vite + Pinia Project Conventions

## Code Style

### General Principles
- **Composition API First:** Prefer `<script setup>` for all components
- **TypeScript by Default:** Use TypeScript for type safety and better DX
- **Vite for Build:** Leverage Vite's fast HMR and optimized builds
- **Modular Architecture:** Organize code by feature or domain
- **Single Page Application:** Client-side routing with Vue Router

### Naming Conventions
| Type | Convention | Example |
|------|------------|---------|
| Components | PascalCase | `UserProfile.vue`, `NavBar.vue` |
| Composables | camelCase with 'use' | `useAuth.ts`, `useApi.ts` |
| Stores (Pinia) | camelCase with 'use' + 'Store' | `useAuthStore.ts`, `useUserStore.ts` |
| Views/Pages | PascalCase | `HomeView.vue`, `AboutView.vue` |
| Router files | kebab-case | `router/index.ts`, `routes/auth.ts` |
| Utilities | camelCase | `formatDate.ts`, `validators.ts` |
| Variables | camelCase | `userName`, `isActive` |
| Constants | UPPER_SNAKE_CASE | `API_URL`, `MAX_RETRIES` |
| Types/Interfaces | PascalCase | `UserData`, `ApiResponse` |
| Enums | PascalCase | `UserRole`, `Status` |

### File Organization
```
my-vue-app/
├── public/                   # Static assets (copied as-is)
│   ├── favicon.ico
│   └── robots.txt
├── src/
│   ├── assets/              # Assets processed by Vite
│   │   ├── images/
│   │   ├── fonts/
│   │   └── styles/
│   │       ├── main.css
│   │       └── variables.css
│   ├── components/          # Reusable components
│   │   ├── common/         # Shared UI components
│   │   │   ├── Button.vue
│   │   │   └── Modal.vue
│   │   ├── forms/          # Form components
│   │   │   ├── Input.vue
│   │   │   └── Select.vue
│   │   └── features/       # Feature-specific components
│   │       └── UserCard.vue
│   ├── composables/         # Composition API functions
│   │   ├── useAuth.ts
│   │   ├── useApi.ts
│   │   └── useLocalStorage.ts
│   ├── router/              # Vue Router config
│   │   ├── index.ts
│   │   ├── routes.ts
│   │   └── guards.ts
│   ├── stores/              # Pinia stores
│   │   ├── auth.ts
│   │   ├── user.ts
│   │   └── index.ts
│   ├── views/               # Route components
│   │   ├── HomeView.vue
│   │   ├── AboutView.vue
│   │   └── auth/
│   │       ├── LoginView.vue
│   │       └── RegisterView.vue
│   ├── services/            # API and business logic
│   │   ├── api/
│   │   │   ├── client.ts   # Axios/Fetch config
│   │   │   ├── auth.ts
│   │   │   └── users.ts
│   │   └── validators.ts
│   ├── utils/               # Helper functions
│   │   ├── formatters.ts
│   │   ├── constants.ts
│   │   └── helpers.ts
│   ├── types/               # TypeScript definitions
│   │   ├── index.ts
│   │   ├── api.ts
│   │   └── models.ts
│   ├── App.vue              # Root component
│   ├── main.ts              # Application entry
│   └── env.d.ts             # Environment types
├── index.html               # HTML entry
├── vite.config.ts           # Vite configuration
├── tsconfig.json            # TypeScript config
├── tsconfig.app.json        # App-specific TS config
├── tsconfig.node.json       # Node-specific TS config
└── package.json
```

## TypeScript Configuration

### tsconfig.json
```json
{
  "files": [],
  "references": [
    { "path": "./tsconfig.app.json" },
    { "path": "./tsconfig.node.json" }
  ],
  "compilerOptions": {
    "baseUrl": ".",
    "paths": {
      "@/*": ["./src/*"]
    }
  }
}
```

### tsconfig.app.json
```json
{
  "extends": "@vue/tsconfig/tsconfig.dom.json",
  "include": ["env.d.ts", "src/**/*", "src/**/*.vue"],
  "exclude": ["src/**/__tests__/*"],
  "compilerOptions": {
    "composite": true,
    "tsBuildInfoFile": "./node_modules/.tmp/tsconfig.app.tsbuildinfo",
    "baseUrl": ".",
    "paths": {
      "@/*": ["./src/*"]
    },
    "strict": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true,
    "noImplicitReturns": true,
    "skipLibCheck": true
  }
}
```

### Type Definitions
```typescript
// types/index.ts
export interface User {
  id: string
  email: string
  name: string
  role: UserRole
  createdAt: Date
}

export type UserRole = 'admin' | 'user' | 'guest'

export interface ApiResponse<T> {
  data: T
  error: string | null
  success: boolean
}

export interface PaginatedResponse<T> {
  data: T[]
  total: number
  page: number
  perPage: number
}
```

## Vue 3 Component Patterns

### Component Structure (Composition API)
```vue
<script setup lang="ts">
import type { User } from '@/types'

interface Props {
  userId: string
  variant?: 'default' | 'compact'
}

const props = withDefaults(defineProps<Props>(), {
  variant: 'default'
})

const emit = defineEmits<{
  update: [user: User]
  delete: [id: string]
}>()

// Composables
const { data: user, loading, error, refresh } = useUser(props.userId)

// Computed
const displayName = computed(() =>
  user.value ? `${user.value.firstName} ${user.value.lastName}` : 'Loading...'
)

// Methods
const handleUpdate = async () => {
  if (!user.value) return
  emit('update', user.value)
}

// Lifecycle
onMounted(() => {
  console.log('Component mounted')
})
</script>

<template>
  <div v-if="loading" class="user-profile-loading">
    Loading...
  </div>
  <div v-else-if="error" class="user-profile-error">
    Error: {{ error.message }}
  </div>
  <div v-else-if="user" :class="['user-profile', `user-profile--${variant}`]">
    <h2>{{ displayName }}</h2>
    <button @click="handleUpdate">Update</button>
  </div>
</template>

<style scoped>
.user-profile {
  padding: 1rem;
  border: 1px solid var(--color-border);
  border-radius: 0.5rem;
}

.user-profile--compact {
  padding: 0.5rem;
}

.user-profile-loading,
.user-profile-error {
  padding: 1rem;
  text-align: center;
}
</style>
```

### Async Components
```typescript
// router/index.ts
import { defineAsyncComponent } from 'vue'

const routes = [
  {
    path: '/dashboard',
    component: defineAsyncComponent(() => import('@/views/DashboardView.vue'))
  }
]
```

## Vite Configuration

### vite.config.ts
```typescript
import { fileURLToPath, URL } from 'node:url'
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'
import vueDevTools from 'vite-plugin-vue-devtools'

export default defineConfig({
  plugins: [
    vue(),
    vueDevTools(),
  ],

  resolve: {
    alias: {
      '@': fileURLToPath(new URL('./src', import.meta.url))
    }
  },

  server: {
    port: 3000,
    host: true,
    proxy: {
      '/api': {
        target: 'http://localhost:8000',
        changeOrigin: true,
        rewrite: (path) => path.replace(/^\/api/, '')
      }
    }
  },

  build: {
    target: 'esnext',
    outDir: 'dist',
    assetsDir: 'assets',
    sourcemap: true,

    rollupOptions: {
      output: {
        manualChunks: {
          'vue-vendor': ['vue', 'vue-router', 'pinia'],
          'ui-vendor': ['@headlessui/vue', '@heroicons/vue']
        }
      }
    },

    chunkSizeWarningLimit: 1000
  },

  css: {
    preprocessorOptions: {
      scss: {
        additionalData: `@import "@/assets/styles/variables.scss";`
      }
    }
  },

  optimizeDeps: {
    include: ['vue', 'vue-router', 'pinia']
  }
})
```

### Environment Variables
```typescript
// .env
VITE_API_URL=http://localhost:8000
VITE_APP_TITLE=My Vue App

// env.d.ts
interface ImportMetaEnv {
  readonly VITE_API_URL: string
  readonly VITE_APP_TITLE: string
}

interface ImportMeta {
  readonly env: ImportMetaEnv
}

// Usage
const apiUrl = import.meta.env.VITE_API_URL
```

## Pinia Store Patterns

### Store Definition (Setup Syntax - Recommended)
```typescript
// stores/auth.ts
import { defineStore } from 'pinia'
import type { User } from '@/types'
import { authApi } from '@/services/api/auth'

export const useAuthStore = defineStore('auth', () => {
  // State
  const user = ref<User | null>(null)
  const token = ref<string | null>(localStorage.getItem('auth-token'))
  const loading = ref(false)

  // Getters
  const isAuthenticated = computed(() => !!user.value && !!token.value)
  const isAdmin = computed(() => user.value?.role === 'admin')
  const userName = computed(() => user.value?.name || 'Guest')

  // Actions
  const login = async (email: string, password: string) => {
    loading.value = true
    try {
      const response = await authApi.login({ email, password })
      user.value = response.data.user
      token.value = response.data.token
      localStorage.setItem('auth-token', response.data.token)
      return response
    } catch (error) {
      console.error('Login failed:', error)
      throw error
    } finally {
      loading.value = false
    }
  }

  const logout = () => {
    user.value = null
    token.value = null
    localStorage.removeItem('auth-token')
  }

  const fetchUser = async () => {
    if (!token.value) return

    try {
      const response = await authApi.me()
      user.value = response.data
    } catch (error) {
      logout()
      throw error
    }
  }

  // Initialize
  if (token.value) {
    fetchUser()
  }

  return {
    // State
    user: readonly(user),
    token: readonly(token),
    loading: readonly(loading),
    // Getters
    isAuthenticated,
    isAdmin,
    userName,
    // Actions
    login,
    logout,
    fetchUser
  }
})
```

### Store Definition (Options Syntax)
```typescript
// stores/user.ts
import { defineStore } from 'pinia'
import type { User } from '@/types'

interface UserState {
  users: User[]
  currentUser: User | null
  loading: boolean
}

export const useUserStore = defineStore('user', {
  state: (): UserState => ({
    users: [],
    currentUser: null,
    loading: false
  }),

  getters: {
    activeUsers: (state) => state.users.filter(u => u.isActive),
    userCount: (state) => state.users.length,
    getUserById: (state) => (id: string) => state.users.find(u => u.id === id)
  },

  actions: {
    async fetchUsers() {
      this.loading = true
      try {
        const response = await userApi.getAll()
        this.users = response.data
      } finally {
        this.loading = false
      }
    },

    async createUser(userData: Partial<User>) {
      const response = await userApi.create(userData)
      this.users.push(response.data)
      return response.data
    },

    updateUser(id: string, updates: Partial<User>) {
      const index = this.users.findIndex(u => u.id === id)
      if (index !== -1) {
        this.users[index] = { ...this.users[index], ...updates }
      }
    },

    deleteUser(id: string) {
      this.users = this.users.filter(u => u.id !== id)
    }
  }
})
```

### Store Usage in Components
```vue
<script setup lang="ts">
import { storeToRefs } from 'pinia'
import { useAuthStore } from '@/stores/auth'
import { useUserStore } from '@/stores/user'

const authStore = useAuthStore()
const userStore = useUserStore()

// Destructure with reactivity preservation
const { user, isAuthenticated, loading } = storeToRefs(authStore)
const { users, activeUsers } = storeToRefs(userStore)

// Actions can be destructured directly
const { login, logout } = authStore
const { fetchUsers, createUser } = userStore

// Or call directly
const handleLogin = async () => {
  await authStore.login('user@example.com', 'password')
}

onMounted(() => {
  if (isAuthenticated.value) {
    userStore.fetchUsers()
  }
})
</script>
```

### Persisting Store State
```typescript
// stores/preferences.ts
import { defineStore } from 'pinia'

export const usePreferencesStore = defineStore('preferences', () => {
  const theme = ref<'light' | 'dark'>(
    (localStorage.getItem('theme') as 'light' | 'dark') || 'light'
  )
  const language = ref(localStorage.getItem('language') || 'en')

  const setTheme = (newTheme: 'light' | 'dark') => {
    theme.value = newTheme
    localStorage.setItem('theme', newTheme)
    document.documentElement.classList.toggle('dark', newTheme === 'dark')
  }

  const setLanguage = (lang: string) => {
    language.value = lang
    localStorage.setItem('language', lang)
  }

  // Initialize theme
  if (theme.value === 'dark') {
    document.documentElement.classList.add('dark')
  }

  return {
    theme: readonly(theme),
    language: readonly(language),
    setTheme,
    setLanguage
  }
})
```

## Vue Router Patterns

### Router Configuration
```typescript
// router/index.ts
import { createRouter, createWebHistory } from 'vue-router'
import { useAuthStore } from '@/stores/auth'

const router = createRouter({
  history: createWebHistory(import.meta.env.BASE_URL),
  routes: [
    {
      path: '/',
      name: 'home',
      component: () => import('@/views/HomeView.vue')
    },
    {
      path: '/about',
      name: 'about',
      component: () => import('@/views/AboutView.vue')
    },
    {
      path: '/dashboard',
      name: 'dashboard',
      component: () => import('@/views/DashboardView.vue'),
      meta: { requiresAuth: true }
    },
    {
      path: '/login',
      name: 'login',
      component: () => import('@/views/auth/LoginView.vue'),
      meta: { guest: true }
    },
    {
      path: '/:pathMatch(.*)*',
      name: 'not-found',
      component: () => import('@/views/NotFoundView.vue')
    }
  ],
  scrollBehavior(to, from, savedPosition) {
    if (savedPosition) {
      return savedPosition
    } else {
      return { top: 0 }
    }
  }
})

// Navigation guards
router.beforeEach((to, from, next) => {
  const authStore = useAuthStore()

  if (to.meta.requiresAuth && !authStore.isAuthenticated) {
    next({ name: 'login', query: { redirect: to.fullPath } })
  } else if (to.meta.guest && authStore.isAuthenticated) {
    next({ name: 'dashboard' })
  } else {
    next()
  }
})

export default router
```

### Route Meta Types
```typescript
// types/router.d.ts
import 'vue-router'

declare module 'vue-router' {
  interface RouteMeta {
    requiresAuth?: boolean
    guest?: boolean
    title?: string
    roles?: string[]
  }
}
```

## Composables

### Custom Composables
```typescript
// composables/useApi.ts
import { ref, type Ref } from 'vue'
import type { ApiResponse } from '@/types'

interface UseApiOptions {
  immediate?: boolean
  onSuccess?: (data: any) => void
  onError?: (error: Error) => void
}

export function useApi<T>(
  fetcher: () => Promise<ApiResponse<T>>,
  options: UseApiOptions = {}
) {
  const data = ref<T | null>(null) as Ref<T | null>
  const error = ref<Error | null>(null)
  const loading = ref(false)

  const execute = async () => {
    loading.value = true
    error.value = null

    try {
      const response = await fetcher()
      data.value = response.data
      options.onSuccess?.(response.data)
      return response.data
    } catch (err) {
      error.value = err as Error
      options.onError?.(err as Error)
      throw err
    } finally {
      loading.value = false
    }
  }

  const refresh = () => execute()

  if (options.immediate) {
    execute()
  }

  return {
    data: readonly(data),
    error: readonly(error),
    loading: readonly(loading),
    execute,
    refresh
  }
}
```

```typescript
// composables/useLocalStorage.ts
import { ref, watch, type Ref } from 'vue'

export function useLocalStorage<T>(
  key: string,
  defaultValue: T
): Ref<T> {
  const storedValue = localStorage.getItem(key)
  const data = ref<T>(
    storedValue ? JSON.parse(storedValue) : defaultValue
  ) as Ref<T>

  watch(
    data,
    (newValue) => {
      localStorage.setItem(key, JSON.stringify(newValue))
    },
    { deep: true }
  )

  return data
}
```

## API Service Layer

### API Client Setup
```typescript
// services/api/client.ts
import axios, { type AxiosInstance, type AxiosRequestConfig } from 'axios'
import { useAuthStore } from '@/stores/auth'

class ApiClient {
  private client: AxiosInstance

  constructor() {
    this.client = axios.create({
      baseURL: import.meta.env.VITE_API_URL || '/api',
      timeout: 10000,
      headers: {
        'Content-Type': 'application/json'
      }
    })

    this.setupInterceptors()
  }

  private setupInterceptors() {
    // Request interceptor
    this.client.interceptors.request.use(
      (config) => {
        const authStore = useAuthStore()
        if (authStore.token) {
          config.headers.Authorization = `Bearer ${authStore.token}`
        }
        return config
      },
      (error) => Promise.reject(error)
    )

    // Response interceptor
    this.client.interceptors.response.use(
      (response) => response,
      async (error) => {
        if (error.response?.status === 401) {
          const authStore = useAuthStore()
          authStore.logout()
          window.location.href = '/login'
        }
        return Promise.reject(error)
      }
    )
  }

  async get<T>(url: string, config?: AxiosRequestConfig) {
    return this.client.get<T>(url, config)
  }

  async post<T>(url: string, data?: any, config?: AxiosRequestConfig) {
    return this.client.post<T>(url, data, config)
  }

  async put<T>(url: string, data?: any, config?: AxiosRequestConfig) {
    return this.client.put<T>(url, data, config)
  }

  async delete<T>(url: string, config?: AxiosRequestConfig) {
    return this.client.delete<T>(url, config)
  }
}

export const apiClient = new ApiClient()
```

### API Services
```typescript
// services/api/auth.ts
import { apiClient } from './client'
import type { User, ApiResponse } from '@/types'

interface LoginCredentials {
  email: string
  password: string
}

interface LoginResponse {
  user: User
  token: string
}

export const authApi = {
  login: (credentials: LoginCredentials) =>
    apiClient.post<ApiResponse<LoginResponse>>('/auth/login', credentials),

  logout: () =>
    apiClient.post<ApiResponse<void>>('/auth/logout'),

  me: () =>
    apiClient.get<ApiResponse<User>>('/auth/me'),

  register: (data: Partial<User>) =>
    apiClient.post<ApiResponse<User>>('/auth/register', data)
}

// services/api/users.ts
export const userApi = {
  getAll: () =>
    apiClient.get<ApiResponse<User[]>>('/users'),

  getById: (id: string) =>
    apiClient.get<ApiResponse<User>>(`/users/${id}`),

  create: (data: Partial<User>) =>
    apiClient.post<ApiResponse<User>>('/users', data),

  update: (id: string, data: Partial<User>) =>
    apiClient.put<ApiResponse<User>>(`/users/${id}`, data),

  delete: (id: string) =>
    apiClient.delete<ApiResponse<void>>(`/users/${id}`)
}
```

## Testing Patterns

### Component Tests
```typescript
// components/__tests__/UserCard.spec.ts
import { describe, it, expect, vi } from 'vitest'
import { mount } from '@vue/test-utils'
import { createPinia, setActivePinia } from 'pinia'
import UserCard from '../UserCard.vue'

describe('UserCard', () => {
  beforeEach(() => {
    setActivePinia(createPinia())
  })

  it('renders user information', () => {
    const wrapper = mount(UserCard, {
      props: {
        user: {
          id: '1',
          name: 'John Doe',
          email: 'john@example.com',
          role: 'user',
          createdAt: new Date()
        }
      }
    })

    expect(wrapper.text()).toContain('John Doe')
    expect(wrapper.text()).toContain('john@example.com')
  })

  it('emits delete event when button clicked', async () => {
    const wrapper = mount(UserCard, {
      props: { user: mockUser }
    })

    await wrapper.find('[data-test="delete-btn"]').trigger('click')
    expect(wrapper.emitted('delete')).toBeTruthy()
    expect(wrapper.emitted('delete')?.[0]).toEqual(['1'])
  })
})
```

### Composable Tests
```typescript
// composables/__tests__/useAuth.spec.ts
import { describe, it, expect, beforeEach } from 'vitest'
import { setActivePinia, createPinia } from 'pinia'
import { useAuthStore } from '@/stores/auth'

describe('useAuthStore', () => {
  beforeEach(() => {
    setActivePinia(createPinia())
  })

  it('logs in user successfully', async () => {
    const authStore = useAuthStore()

    await authStore.login('user@example.com', 'password')

    expect(authStore.user).toBeTruthy()
    expect(authStore.isAuthenticated).toBe(true)
  })

  it('clears user on logout', () => {
    const authStore = useAuthStore()
    authStore.user = mockUser
    authStore.token = 'test-token'

    authStore.logout()

    expect(authStore.user).toBeNull()
    expect(authStore.token).toBeNull()
    expect(authStore.isAuthenticated).toBe(false)
  })
})
```

## Performance Optimization

### Code Splitting
```typescript
// router/index.ts - Already shown above with lazy loading

// Explicit chunk naming
{
  path: '/admin',
  component: () => import(
    /* webpackChunkName: "admin" */
    '@/views/admin/AdminView.vue'
  )
}
```

### Lazy Components
```vue
<script setup lang="ts">
import { defineAsyncComponent } from 'vue'

const HeavyChart = defineAsyncComponent(() =>
  import('@/components/HeavyChart.vue')
)
</script>

<template>
  <Suspense>
    <template #default>
      <HeavyChart v-if="showChart" />
    </template>
    <template #fallback>
      <div>Loading chart...</div>
    </template>
  </Suspense>
</template>
```

### Memoization
```typescript
import { computed, ref } from 'vue'

const items = ref<Item[]>([])

// Memoize expensive computations
const processedItems = computed(() => {
  return items.value
    .filter(item => item.active)
    .sort((a, b) => b.priority - a.priority)
    .map(item => ({
      ...item,
      displayName: formatName(item.name)
    }))
})
```

## Security Best Practices

### Input Sanitization
```typescript
// utils/sanitize.ts
import DOMPurify from 'dompurify'

export const sanitizeHtml = (html: string): string => {
  return DOMPurify.sanitize(html, {
    ALLOWED_TAGS: ['b', 'i', 'em', 'strong', 'a', 'p'],
    ALLOWED_ATTR: ['href']
  })
}

// Usage in component
const sanitizedContent = computed(() =>
  sanitizeHtml(props.rawHtml)
)
```

### CSRF Protection
```typescript
// services/api/client.ts (add to interceptor)
this.client.interceptors.request.use((config) => {
  const csrfToken = document.querySelector('meta[name="csrf-token"]')?.getAttribute('content')
  if (csrfToken) {
    config.headers['X-CSRF-TOKEN'] = csrfToken
  }
  return config
})
```

### Input Validation (Zod)
```typescript
// services/validators.ts
import { z } from 'zod'

export const userSchema = z.object({
  email: z.string().email('Invalid email address'),
  password: z
    .string()
    .min(8, 'Password must be at least 8 characters')
    .regex(/[A-Z]/, 'Password must contain uppercase letter')
    .regex(/[0-9]/, 'Password must contain number'),
  name: z.string().min(2).max(100)
})

export type UserInput = z.infer<typeof userSchema>

// Usage
try {
  const validated = userSchema.parse(formData)
  // Use validated data
} catch (error) {
  if (error instanceof z.ZodError) {
    console.error(error.errors)
  }
}
```

---
*Last Updated: 2025*
*Vue Version: 3.x*
*Vite Version: 5.x+*
*Pinia Version: 2.x*

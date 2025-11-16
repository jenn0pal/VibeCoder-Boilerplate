# Nuxt 3 + Vue 3 Project Conventions

## Code Style

### General Principles
- **Composition API First:** Prefer `<script setup>` for all components
- **TypeScript by Default:** Use TypeScript for type safety and better DX
- **Auto-imports:** Leverage Nuxt's auto-import for composables, components, and utilities
- **SSR-First:** Design with Server-Side Rendering in mind
- **File-based Routing:** Use the `pages/` directory for automatic route generation

### Naming Conventions
| Type | Convention | Example |
|------|------------|---------|
| Components | PascalCase | `UserProfile.vue`, `NavBar.vue` |
| Composables | camelCase with 'use' | `useAuth.ts`, `useApi.ts` |
| Pages | kebab-case | `user-profile.vue`, `about.vue` |
| Layouts | kebab-case | `default.vue`, `auth.vue` |
| Middleware | kebab-case | `auth.ts`, `guest.global.ts` |
| API Routes | kebab-case.method | `users.get.ts`, `auth.post.ts` |
| Server Utils | camelCase | `database.ts`, `validation.ts` |
| Plugins | kebab-case | `api.ts`, `pinia.client.ts` |
| Variables | camelCase | `userName`, `isActive` |
| Constants | UPPER_SNAKE_CASE | `API_URL`, `MAX_RETRIES` |
| Types/Interfaces | PascalCase | `UserData`, `ApiResponse` |

### File Organization
```
my-nuxt-app/
├── .nuxt/                    # Generated (gitignored)
├── .output/                  # Build output (gitignored)
├── app/
│   ├── app.vue              # Root component
│   ├── error.vue            # Error page
│   ├── pages/               # File-based routing
│   │   ├── index.vue        # → /
│   │   ├── about.vue        # → /about
│   │   ├── users/
│   │   │   ├── index.vue    # → /users
│   │   │   └── [id].vue     # → /users/:id
│   │   └── [...slug].vue    # Catch-all
│   ├── layouts/             # Layout wrappers
│   │   ├── default.vue
│   │   └── admin.vue
│   ├── components/          # Auto-imported
│   │   ├── ui/             # UI components
│   │   ├── forms/          # Form components
│   │   └── shared/         # Shared components
│   ├── composables/         # Auto-imported
│   │   ├── useAuth.ts
│   │   └── useApi.ts
│   ├── utils/               # Auto-imported utilities
│   ├── middleware/          # Route middleware
│   │   ├── auth.ts
│   │   └── guest.global.ts
│   ├── plugins/             # Vue plugins
│   │   ├── api.ts
│   │   └── pinia.client.ts
│   ├── stores/              # Pinia stores
│   │   ├── auth.ts
│   │   └── user.ts
│   └── assets/              # Bundled assets
│       ├── css/
│       └── images/
├── server/                   # Server-side code
│   ├── api/                 # API endpoints
│   │   ├── users.get.ts     # GET /api/users
│   │   └── auth/
│   │       └── login.post.ts # POST /api/auth/login
│   ├── middleware/          # Server middleware
│   ├── plugins/             # Server plugins
│   └── utils/               # Server utilities
├── public/                   # Static assets
├── nuxt.config.ts           # Nuxt config
├── app.config.ts            # App config (reactive)
└── tsconfig.json            # TypeScript config
```

## TypeScript Configuration

### tsconfig.json (Nuxt extends this automatically)
```json
{
  "extends": "./.nuxt/tsconfig.json",
  "compilerOptions": {
    "strict": true,
    "noUnusedLocals": true,
    "noUnusedParameters": true,
    "noImplicitReturns": true
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
```

## Vue 3 Component Patterns

### Component Structure (Composition API)
```vue
<script setup lang="ts">
import type { User } from '~/types'

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
const { data: user, pending, error } = await useFetch(`/api/users/${props.userId}`)

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
  <div v-if="pending">
    Loading...
  </div>
  <div v-else-if="error">
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
}

.user-profile--compact {
  padding: 0.5rem;
}
</style>
```

### Server Components (Islands)
```vue
<!-- components/HeavyChart.server.vue -->
<script setup lang="ts">
// This component only runs on the server
const data = await fetchChartData()
</script>

<template>
  <div class="chart">
    <!-- Expensive chart rendering -->
  </div>
</template>
```

```vue
<!-- pages/dashboard.vue -->
<template>
  <div>
    <!-- Server component won't be in client bundle -->
    <HeavyChart />

    <!-- Client-only interactivity -->
    <Counter nuxt-client :initial="5" />
  </div>
</template>
```

## Nuxt Composables

### Data Fetching
```typescript
// Prefer useFetch for simple API calls
const { data, pending, error, refresh } = await useFetch('/api/users')

// Use useAsyncData for more complex scenarios
const { data: posts } = await useAsyncData(
  'posts-list',
  () => $fetch('/api/posts', {
    query: { limit: 10 }
  }),
  {
    transform: (posts) => posts.map(p => ({ ...p, formatted: true })),
    watch: [searchQuery]
  }
)

// Client-only fetching
const { data } = await useLazyFetch('/api/data', {
  server: false
})
```

### Custom Composables
```typescript
// composables/useAuth.ts
export const useAuth = () => {
  const user = useState<User | null>('user', () => null)
  const token = useCookie('auth-token')

  const isAuthenticated = computed(() => !!user.value)

  const login = async (email: string, password: string) => {
    try {
      const { data } = await $fetch('/api/auth/login', {
        method: 'POST',
        body: { email, password }
      })
      user.value = data.user
      token.value = data.token
      await navigateTo('/dashboard')
    } catch (error) {
      console.error('Login failed:', error)
      throw error
    }
  }

  const logout = async () => {
    user.value = null
    token.value = null
    await navigateTo('/login')
  }

  return {
    user: readonly(user),
    isAuthenticated,
    login,
    logout
  }
}
```

### State Management
```typescript
// composables/useState.ts (built-in)
export const useCounter = () => useState('counter', () => 0)

// Usage in component
const count = useCounter()
count.value++ // Shared across components
```

## Pinia Store Patterns

### Store Definition (Setup Syntax - Recommended)
```typescript
// stores/auth.ts
import { defineStore } from 'pinia'
import type { User } from '~/types'

export const useAuthStore = defineStore('auth', () => {
  // State
  const user = ref<User | null>(null)
  const token = ref<string | null>(null)

  // Getters
  const isAuthenticated = computed(() => !!user.value)
  const isAdmin = computed(() => user.value?.role === 'admin')

  // Actions
  const login = async (email: string, password: string) => {
    const { data } = await $fetch('/api/auth/login', {
      method: 'POST',
      body: { email, password }
    })
    user.value = data.user
    token.value = data.token
  }

  const logout = () => {
    user.value = null
    token.value = null
  }

  const fetchUser = async () => {
    if (!token.value) return
    const { data } = await $fetch('/api/auth/me')
    user.value = data
  }

  return {
    user: readonly(user),
    token: readonly(token),
    isAuthenticated,
    isAdmin,
    login,
    logout,
    fetchUser
  }
})
```

### Store Usage in Components
```vue
<script setup lang="ts">
import { storeToRefs } from 'pinia'

const authStore = useAuthStore()

// Destructure with reactivity preservation
const { user, isAuthenticated } = storeToRefs(authStore)

// Actions can be destructured directly
const { login, logout } = authStore

const handleLogin = async () => {
  await login('user@example.com', 'password')
}
</script>
```

## Server API Routes

### Basic API Endpoint
```typescript
// server/api/users/index.get.ts
export default defineEventHandler(async (event) => {
  const query = getQuery(event)
  const users = await prisma.user.findMany({
    take: Number(query.limit) || 10
  })

  return {
    success: true,
    data: users
  }
})
```

### Protected API with Middleware
```typescript
// server/api/users/[id].put.ts
export default defineEventHandler(async (event) => {
  // Authenticate
  const user = await requireUserSession(event)

  // Validate
  const id = getRouterParam(event, 'id')
  const body = await readBody(event)

  // Update
  const updated = await prisma.user.update({
    where: { id },
    data: body
  })

  return {
    success: true,
    data: updated
  }
})
```

### Error Handling
```typescript
// server/utils/errors.ts
export class ApiError extends Error {
  statusCode: number

  constructor(message: string, statusCode = 500) {
    super(message)
    this.statusCode = statusCode
  }
}

// server/api/users/[id].get.ts
export default defineEventHandler(async (event) => {
  const id = getRouterParam(event, 'id')

  const user = await prisma.user.findUnique({
    where: { id }
  })

  if (!user) {
    throw createError({
      statusCode: 404,
      statusMessage: 'User not found'
    })
  }

  return { data: user }
})
```

## Routing & Navigation

### Pages and Dynamic Routes
```vue
<!-- pages/users/[id].vue -->
<script setup lang="ts">
const route = useRoute()
const userId = computed(() => route.params.id as string)

const { data: user } = await useFetch(`/api/users/${userId.value}`)
</script>

<template>
  <div v-if="user">
    <h1>{{ user.name }}</h1>
  </div>
</template>
```

### Navigation
```typescript
// Programmatic navigation
await navigateTo('/dashboard')
await navigateTo({ name: 'users-id', params: { id: '123' } })

// External links
await navigateTo('https://example.com', { external: true })

// Replace history
await navigateTo('/login', { replace: true })
```

### Middleware
```typescript
// middleware/auth.ts
export default defineNuxtRouteMiddleware((to, from) => {
  const auth = useAuthStore()

  if (!auth.isAuthenticated) {
    return navigateTo('/login')
  }
})

// middleware/guest.global.ts
export default defineNuxtRouteMiddleware((to, from) => {
  const auth = useAuthStore()

  if (auth.isAuthenticated && to.path === '/login') {
    return navigateTo('/dashboard')
  }
})
```

### Page Metadata
```vue
<script setup lang="ts">
definePageMeta({
  layout: 'admin',
  middleware: ['auth'],
  title: 'Admin Dashboard'
})

// Or use useHead for dynamic metadata
useHead({
  title: 'My Page Title',
  meta: [
    { name: 'description', content: 'Page description' }
  ]
})
</script>
```

## Testing Patterns

### Component Tests (Vitest + Testing Library)
```typescript
// components/UserCard.spec.ts
import { describe, it, expect } from 'vitest'
import { mount } from '@vue/test-utils'
import UserCard from './UserCard.vue'

describe('UserCard', () => {
  it('renders user information', () => {
    const wrapper = mount(UserCard, {
      props: {
        user: {
          id: '1',
          name: 'John Doe',
          email: 'john@example.com'
        }
      }
    })

    expect(wrapper.text()).toContain('John Doe')
    expect(wrapper.text()).toContain('john@example.com')
  })

  it('emits delete event', async () => {
    const wrapper = mount(UserCard, {
      props: { user: mockUser }
    })

    await wrapper.find('[data-test="delete-btn"]').trigger('click')
    expect(wrapper.emitted('delete')).toBeTruthy()
  })
})
```

### Composable Tests
```typescript
// composables/useAuth.spec.ts
import { describe, it, expect, vi } from 'vitest'
import { useAuth } from './useAuth'

describe('useAuth', () => {
  it('logs in user successfully', async () => {
    const { login, user, isAuthenticated } = useAuth()

    await login('user@example.com', 'password')

    expect(user.value).toBeTruthy()
    expect(isAuthenticated.value).toBe(true)
  })
})
```

## Performance Optimization

### Lazy Loading Components
```vue
<template>
  <div>
    <!-- Lazy load heavy components -->
    <LazyHeavyChart v-if="showChart" />

    <!-- Client-only components -->
    <ClientOnly>
      <ExpensiveComponent />
      <template #fallback>
        <LoadingSpinner />
      </template>
    </ClientOnly>
  </div>
</template>
```

### Image Optimization
```vue
<template>
  <!-- Use Nuxt Image module -->
  <NuxtImg
    src="/images/hero.jpg"
    alt="Hero image"
    width="800"
    height="600"
    loading="lazy"
    format="webp"
  />

  <!-- Responsive images -->
  <NuxtPicture
    src="/images/product.jpg"
    :img-attrs="{ alt: 'Product image' }"
    sizes="sm:100vw md:50vw lg:400px"
  />
</template>
```

### Code Splitting
```typescript
// nuxt.config.ts
export default defineNuxtConfig({
  build: {
    splitChunks: {
      layouts: true,
      pages: true,
      commons: true
    }
  },

  optimization: {
    splitChunks: {
      cacheGroups: {
        vendor: {
          test: /[\\/]node_modules[\\/]/,
          name: 'vendors',
          chunks: 'all'
        }
      }
    }
  }
})
```

## Security Best Practices

### Input Validation (Zod)
```typescript
// server/utils/validation.ts
import { z } from 'zod'

export const UserSchema = z.object({
  email: z.string().email(),
  password: z.string().min(8),
  name: z.string().min(2).max(100)
})

// server/api/users.post.ts
export default defineEventHandler(async (event) => {
  const body = await readBody(event)

  try {
    const validated = UserSchema.parse(body)
    // Process validated data
  } catch (error) {
    throw createError({
      statusCode: 400,
      statusMessage: 'Invalid input',
      data: error.errors
    })
  }
})
```

### CSRF Protection
```typescript
// nuxt.config.ts
export default defineNuxtConfig({
  security: {
    headers: {
      crossOriginEmbedderPolicy: 'require-corp',
      crossOriginOpenerPolicy: 'same-origin',
      crossOriginResourcePolicy: 'same-origin'
    },
    requestSizeLimiter: {
      maxRequestSizeInBytes: 2000000,
      maxUploadFileRequestInBytes: 8000000,
    },
    rateLimiter: {
      tokensPerInterval: 150,
      interval: 'hour',
      fireImmediately: false,
    }
  }
})
```

### Environment Variables
```typescript
// nuxt.config.ts
export default defineNuxtConfig({
  runtimeConfig: {
    // Private keys (server-only)
    apiSecret: process.env.API_SECRET,
    databaseUrl: process.env.DATABASE_URL,

    // Public keys (exposed to client)
    public: {
      apiBase: process.env.NUXT_PUBLIC_API_BASE || 'http://localhost:3000'
    }
  }
})

// Usage
const config = useRuntimeConfig()
console.log(config.public.apiBase) // Available on client
console.log(config.apiSecret) // Server-only
```

## Nuxt Configuration Best Practices

### nuxt.config.ts
```typescript
export default defineNuxtConfig({
  devtools: { enabled: true },

  typescript: {
    strict: true,
    typeCheck: true
  },

  modules: [
    '@nuxtjs/tailwindcss',
    '@pinia/nuxt',
    '@nuxt/image',
    '@nuxtjs/i18n'
  ],

  app: {
    head: {
      title: 'My Nuxt App',
      meta: [
        { charset: 'utf-8' },
        { name: 'viewport', content: 'width=device-width, initial-scale=1' },
        { name: 'description', content: 'My amazing Nuxt app' }
      ]
    }
  },

  experimental: {
    componentIslands: true,
    viewTransition: true
  },

  nitro: {
    compressPublicAssets: true,
    storage: {
      cache: {
        driver: 'redis',
        host: process.env.REDIS_HOST
      }
    }
  }
})
```

---
*Last Updated: 2025*
*Nuxt Version: 3.x*
*Vue Version: 3.x*

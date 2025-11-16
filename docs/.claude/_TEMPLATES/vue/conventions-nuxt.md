# Nuxt 3 Specific Conventions

> **This file contains Nuxt 3-specific additions**
>
> **IMPORTANT:** This file extends `conventions-base.md` - read that first!
>
> Only Nuxt-specific patterns are documented here:
> - Auto-imports
> - File-based routing
> - Server API routes
> - SSR considerations
> - Nuxt composables

## What Makes Nuxt Different

### Auto-Imports
Nuxt automatically imports:
- Components from `components/`
- Composables from `composables/`
- Utils from `utils/`
- Vue APIs (ref, computed, etc.)

```vue
<script setup lang="ts">
// ✅ No imports needed!
const count = ref(0) // Auto-imported from Vue
const user = useAuth() // Auto-imported from composables/useAuth.ts
</script>

<template>
  <!-- ✅ No imports needed! -->
  <UserCard :user="user" />
</template>
```

### File-Based Routing
- `pages/index.vue` → `/`
- `pages/about.vue` → `/about`
- `pages/users/[id].vue` → `/users/:id`
- `pages/[...slug].vue` → Catch-all route

### Server-Side Rendering
```vue
<script setup lang="ts">
// Runs on both server and client
const { data } = await useFetch('/api/users')

// Client-only code
onMounted(() => {
  // Only runs in browser
  window.addEventListener('resize', handleResize)
})
</script>
```

## Nuxt-Specific Patterns

### Data Fetching
```typescript
// ✅ GOOD: Use useFetch for simple API calls
const { data, pending, error, refresh } = await useFetch('/api/users')

// ✅ GOOD: Use useAsyncData for complex scenarios
const { data: posts } = await useAsyncData(
  'posts-list',
  () => $fetch('/api/posts', { query: { limit: 10 } })
)

// ✅ GOOD: Client-only fetching
const { data } = await useLazyFetch('/api/data', {
  server: false
})
```

### Nuxt Composables
```typescript
// State management
const user = useState<User>('user', () => null)

// Navigation
await navigateTo('/dashboard')
await navigateTo({ name: 'users-id', params: { id: '123' } })

// Route access
const route = useRoute()
const router = useRouter()

// Cookies
const token = useCookie('auth-token')

// Runtime config
const config = useRuntimeConfig()
```

### Server API Routes
```typescript
// server/api/users/index.get.ts
export default defineEventHandler(async (event) => {
  const query = getQuery(event)
  const users = await prisma.user.findMany()

  return {
    success: true,
    data: users
  }
})

// server/api/users/[id].put.ts
export default defineEventHandler(async (event) => {
  const id = getRouterParam(event, 'id')
  const body = await readBody(event)

  // Update logic
  return { success: true }
})
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

// middleware/guest.global.ts (runs on every route)
export default defineNuxtRouteMiddleware((to, from) => {
  // Global middleware logic
})
```

### Page Metadata
```vue
<script setup lang="ts">
definePageMeta({
  layout: 'admin',
  middleware: ['auth'],
  title: 'Dashboard'
})

// Or dynamic metadata
useHead({
  title: 'My Page',
  meta: [{ name: 'description', content: 'Description' }]
})
</script>
```

## Nuxt Configuration

### nuxt.config.ts Essentials
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
    '@nuxt/image'
  ],

  runtimeConfig: {
    // Private (server-only)
    apiSecret: process.env.API_SECRET,

    // Public (exposed to client)
    public: {
      apiBase: process.env.NUXT_PUBLIC_API_BASE
    }
  }
})
```

---
*Nuxt Version: 3.x*
*Extends: conventions-base.md*

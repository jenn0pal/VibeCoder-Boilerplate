# Vue 3 SPA Specific Conventions

> **This file contains Vue 3 SPA-specific additions**
>
> **IMPORTANT:** This file extends `conventions-base.md` - read that first!
>
> Only SPA-specific patterns are documented here:
> - Vue Router configuration
> - Vite configuration
> - Manual import management
> - Client-only rendering

## What Makes SPA Different

### No Auto-Imports
Unlike Nuxt, you must manually import everything:

```vue
<script setup lang="ts">
// ❌ Not auto-imported - must import manually
import { ref, computed, onMounted } from 'vue'
import { useRouter } from 'vue-router'
import UserCard from '@/components/UserCard.vue'
import { useAuthStore } from '@/stores/auth'

const count = ref(0)
const router = useRouter()
</script>
```

### Client-Only Rendering
- All rendering happens in browser
- No SSR considerations needed
- Simpler deployment (static hosting)

## SPA-Specific Patterns

### Vue Router Setup
```typescript
// router/index.ts
import { createRouter, createWebHistory } from 'vue-router'
import HomeView from '@/views/HomeView.vue'

const router = createRouter({
  history: createWebHistory(import.meta.env.BASE_URL),
  routes: [
    {
      path: '/',
      name: 'home',
      component: HomeView
    },
    {
      path: '/about',
      name: 'about',
      // Lazy-loaded route
      component: () => import('@/views/AboutView.vue')
    },
    {
      path: '/dashboard',
      name: 'dashboard',
      component: () => import('@/views/DashboardView.vue'),
      meta: { requiresAuth: true }
    }
  ]
})

// Navigation guards
router.beforeEach((to, from, next) => {
  const authStore = useAuthStore()

  if (to.meta.requiresAuth && !authStore.isAuthenticated) {
    next({ name: 'login' })
  } else {
    next()
  }
})

export default router
```

### Pinia Store (Primary State Management)
```typescript
// stores/auth.ts
import { defineStore } from 'pinia'

export const useAuthStore = defineStore('auth', () => {
  // State
  const user = ref<User | null>(null)
  const token = ref<string | null>(localStorage.getItem('auth-token'))

  // Getters
  const isAuthenticated = computed(() => !!user.value && !!token.value)

  // Actions
  const login = async (email: string, password: string) => {
    const response = await authApi.login({ email, password })
    user.value = response.data.user
    token.value = response.data.token
    localStorage.setItem('auth-token', response.data.token)
  }

  const logout = () => {
    user.value = null
    token.value = null
    localStorage.removeItem('auth-token')
  }

  return {
    user: readonly(user),
    token: readonly(token),
    isAuthenticated,
    login,
    logout
  }
})
```

### API Service Layer
```typescript
// services/api/client.ts
import axios from 'axios'

const apiClient = axios.create({
  baseURL: import.meta.env.VITE_API_URL || '/api',
  timeout: 10000
})

// Request interceptor
apiClient.interceptors.request.use((config) => {
  const authStore = useAuthStore()
  if (authStore.token) {
    config.headers.Authorization = `Bearer ${authStore.token}`
  }
  return config
})

// Response interceptor
apiClient.interceptors.response.use(
  (response) => response,
  (error) => {
    if (error.response?.status === 401) {
      const authStore = useAuthStore()
      authStore.logout()
      router.push('/login')
    }
    return Promise.reject(error)
  }
)

export { apiClient }
```

## Vite Configuration

### vite.config.ts
```typescript
import { fileURLToPath, URL } from 'node:url'
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'

export default defineConfig({
  plugins: [vue()],

  resolve: {
    alias: {
      '@': fileURLToPath(new URL('./src', import.meta.url))
    }
  },

  server: {
    port: 3000,
    proxy: {
      '/api': {
        target: 'http://localhost:8000',
        changeOrigin: true
      }
    }
  },

  build: {
    sourcemap: true,
    rollupOptions: {
      output: {
        manualChunks: {
          'vue-vendor': ['vue', 'vue-router', 'pinia']
        }
      }
    }
  }
})
```

### Environment Variables
```typescript
// .env
VITE_API_URL=http://localhost:8000

// env.d.ts
interface ImportMetaEnv {
  readonly VITE_API_URL: string
}

// Usage
const apiUrl = import.meta.env.VITE_API_URL
```

## Main Application Setup

### src/main.ts
```typescript
import { createApp } from 'vue'
import { createPinia } from 'pinia'
import App from './App.vue'
import router from './router'
import './assets/styles/main.css'

const app = createApp(App)

app.use(createPinia())
app.use(router)

app.mount('#app')
```

---
*Vue Version: 3.x*
*Vite Version: 5.x+*
*Pinia Version: 2.x*
*Extends: conventions-base.md*

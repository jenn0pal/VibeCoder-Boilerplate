# Vue 3 SPA Technology Stack

## Core Technologies

### Framework
| Technology | Version | Purpose | Documentation |
|------------|---------|---------|---------------|
| Vue | 3.4+ | UI framework | https://vuejs.org/ |
| Vite | 5.0+ | Build tool & dev server | https://vitejs.dev/ |
| Vue Router | 4.x | Client-side routing | https://router.vuejs.org/ |

### State Management
| Technology | Version | Purpose | Documentation |
|------------|---------|---------|---------------|
| Pinia | 2.x | State management | https://pinia.vuejs.org/ |

### UI Libraries (Choose One or None)
| Technology | Version | Purpose | Documentation |
|------------|---------|---------|---------------|
| Vuetify | 3.x | Material Design components | https://vuetifyjs.com/ |
| Quasar | 2.x | Full-featured UI framework | https://quasar.dev/ |
| PrimeVue | 3.x | Rich UI components | https://primevue.org/ |
| Element Plus | 2.x | Desktop UI library | https://element-plus.org/ |

### Styling (Choose One)
| Technology | Version | Purpose | Documentation |
|------------|---------|---------|---------------|
| Tailwind CSS | 3.x | Utility-first CSS | https://tailwindcss.com/ |
| UnoCSS | Latest | Instant atomic CSS | https://unocss.dev/ |
| Sass/SCSS | Latest | CSS preprocessor | https://sass-lang.com/ |

## Development Tools

### Build & Dev
| Technology | Version | Purpose | Documentation |
|------------|---------|---------|---------------|
| Vite | 5.0+ | Build tool & HMR | https://vitejs.dev/ |
| @vitejs/plugin-vue | Latest | Vue 3 plugin for Vite | https://github.com/vitejs/vite-plugin-vue |
| vite-plugin-pages | Latest | File-based routing (optional) | https://github.com/hannoeru/vite-plugin-pages |

### Code Quality
| Technology | Version | Purpose | Documentation |
|------------|---------|---------|---------------|
| ESLint | 8.x | Linting | https://eslint.org/ |
| @vue/eslint-config | Latest | Vue-specific ESLint rules | https://github.com/vuejs/eslint-config-vue |
| Prettier | 3.x | Code formatting | https://prettier.io/ |
| TypeScript | 5.x | Type checking | https://www.typescriptlang.org/ |

### Testing
| Technology | Version | Purpose | Documentation |
|------------|---------|---------|---------------|
| Vitest | 1.x | Unit testing | https://vitest.dev/ |
| @vue/test-utils | 2.x | Vue component testing | https://test-utils.vuejs.org/ |
| Playwright | Latest | E2E testing | https://playwright.dev/ |
| @testing-library/vue | Latest | User-centric testing (alt) | https://testing-library.com/vue |

## Package Management

### Primary Package Manager
- **Recommended:** pnpm (faster, disk efficient)
- **Alternative:** npm, yarn
- **Lock File:** pnpm-lock.yaml / package-lock.json / yarn.lock

### Common Commands
```bash
# Initialize new Vue project
pnpm create vue@latest

# Install dependencies
pnpm install

# Development server with HMR
pnpm run dev

# Build for production
pnpm run build

# Preview production build
pnpm run preview

# Run tests
pnpm run test:unit
pnpm run test:e2e

# Linting
pnpm run lint
pnpm run lint:fix

# Type checking (if using TypeScript)
pnpm run type-check
```

## Project Structure

### Recommended Structure
```
project/
├── public/              # Static assets (copied as-is)
│   └── favicon.ico
├── src/
│   ├── assets/          # Build-time assets (images, styles)
│   ├── components/      # Reusable Vue components
│   │   ├── common/      # Common UI components
│   │   └── features/    # Feature-specific components
│   ├── composables/     # Composition API composables
│   ├── layouts/         # Layout components
│   ├── pages/           # Page components (one per route)
│   ├── router/          # Vue Router configuration
│   │   └── index.ts
│   ├── stores/          # Pinia stores
│   ├── types/           # TypeScript type definitions
│   ├── utils/           # Utility functions
│   ├── App.vue          # Root component
│   └── main.ts          # Application entry point
├── tests/
│   ├── unit/            # Unit tests
│   └── e2e/             # E2E tests
├── .env.example         # Environment variables template
├── .eslintrc.cjs        # ESLint configuration
├── .prettierrc          # Prettier configuration
├── index.html           # HTML entry point
├── package.json         # Dependencies
├── tsconfig.json        # TypeScript configuration
├── vite.config.ts       # Vite configuration
└── vitest.config.ts     # Vitest configuration
```

## Routing Configuration

### Vue Router Setup
```typescript
// src/router/index.ts
import { createRouter, createWebHistory } from 'vue-router'
import type { RouteRecordRaw } from 'vue-router'

const routes: RouteRecordRaw[] = [
  {
    path: '/',
    name: 'Home',
    component: () => import('@/pages/HomePage.vue'),
  },
  {
    path: '/about',
    name: 'About',
    component: () => import('@/pages/AboutPage.vue'),
  },
  {
    path: '/:pathMatch(.*)*',
    name: 'NotFound',
    component: () => import('@/pages/NotFoundPage.vue'),
  },
]

const router = createRouter({
  history: createWebHistory(import.meta.env.BASE_URL),
  routes,
})

export default router
```

### Route Guards
```typescript
// Navigation guards
router.beforeEach((to, from, next) => {
  const authStore = useAuthStore()

  if (to.meta.requiresAuth && !authStore.isAuthenticated) {
    next({ name: 'Login' })
  } else {
    next()
  }
})
```

## State Management (Pinia)

### Store Setup
```typescript
// src/stores/counter.ts
import { defineStore } from 'pinia'
import { ref, computed } from 'vue'

export const useCounterStore = defineStore('counter', () => {
  const count = ref(0)
  const doubleCount = computed(() => count.value * 2)

  function increment() {
    count.value++
  }

  return { count, doubleCount, increment }
})
```

### Using Stores in Components
```vue
<script setup lang="ts">
import { useCounterStore } from '@/stores/counter'

const counter = useCounterStore()
</script>

<template>
  <div>
    <p>Count: {{ counter.count }}</p>
    <button @click="counter.increment">Increment</button>
  </div>
</template>
```

## Build Configuration

### Vite Configuration
```typescript
// vite.config.ts
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
  build: {
    target: 'esnext',
    minify: 'esbuild',
    sourcemap: false,
    rollupOptions: {
      output: {
        manualChunks: {
          'vue-vendor': ['vue', 'vue-router', 'pinia'],
        },
      },
    },
  },
  server: {
    port: 3000,
    host: true,
  },
})
```

## Environment Variables

### .env File Support
```bash
# .env.local (gitignored)
VITE_API_BASE_URL=https://api.example.com
VITE_APP_TITLE=My Vue App
VITE_FEATURE_FLAG_NEW_UI=true
```

### Accessing Environment Variables
```typescript
// In TypeScript files
const apiUrl = import.meta.env.VITE_API_BASE_URL

// In Vue components
<script setup>
const appTitle = import.meta.env.VITE_APP_TITLE
</script>
```

### Type-safe Environment Variables
```typescript
// src/types/env.d.ts
/// <reference types="vite/client" />

interface ImportMetaEnv {
  readonly VITE_API_BASE_URL: string
  readonly VITE_APP_TITLE: string
  readonly VITE_FEATURE_FLAG_NEW_UI: boolean
}

interface ImportMeta {
  readonly env: ImportMetaEnv
}
```

## HTTP Client

### Axios Setup
```typescript
// src/utils/api.ts
import axios from 'axios'

const api = axios.create({
  baseURL: import.meta.env.VITE_API_BASE_URL,
  timeout: 10000,
  headers: {
    'Content-Type': 'application/json',
  },
})

// Request interceptor
api.interceptors.request.use((config) => {
  const token = localStorage.getItem('auth_token')
  if (token) {
    config.headers.Authorization = `Bearer ${token}`
  }
  return config
})

// Response interceptor
api.interceptors.response.use(
  (response) => response,
  (error) => {
    if (error.response?.status === 401) {
      // Handle unauthorized
      router.push('/login')
    }
    return Promise.reject(error)
  }
)

export default api
```

## Deployment

### Build for Production
```bash
# Build the app
pnpm run build

# Output directory: dist/
# - index.html
# - assets/ (JS, CSS, images)
```

### Hosting Options
- **Static Hosting:** Netlify, Vercel, GitHub Pages, Cloudflare Pages
- **Traditional Hosting:** Nginx, Apache
- **CDN:** AWS CloudFront, Fastly

### Nginx Configuration
```nginx
server {
    listen 80;
    server_name example.com;
    root /var/www/dist;
    index index.html;

    # Compression
    gzip on;
    gzip_types text/plain text/css application/json application/javascript;

    # Cache static assets
    location ~* \.(js|css|png|jpg|jpeg|gif|ico|svg|woff|woff2|ttf|eot)$ {
        expires 1y;
        add_header Cache-Control "public, immutable";
    }

    # SPA fallback
    location / {
        try_files $uri $uri/ /index.html;
    }
}
```

## Performance Optimization

### Code Splitting
```typescript
// Route-based splitting (automatic with dynamic imports)
const Home = () => import('./pages/HomePage.vue')

// Component-based splitting
const HeavyComponent = defineAsyncComponent(() =>
  import('./components/HeavyComponent.vue')
)
```

### Lazy Loading Images
```vue
<template>
  <img
    :src="imageSrc"
    loading="lazy"
    alt="Description"
  >
</template>
```

### Bundle Analysis
```bash
# Install plugin
pnpm add -D rollup-plugin-visualizer

# Add to vite.config.ts
import { visualizer } from 'rollup-plugin-visualizer'

export default defineConfig({
  plugins: [
    vue(),
    visualizer({ open: true })
  ]
})

# Build and analyze
pnpm run build
```

## Testing

### Unit Tests (Vitest)
```typescript
// tests/unit/Counter.spec.ts
import { describe, it, expect } from 'vitest'
import { mount } from '@vue/test-utils'
import Counter from '@/components/Counter.vue'

describe('Counter.vue', () => {
  it('increments counter when button is clicked', async () => {
    const wrapper = mount(Counter)
    const button = wrapper.find('button')

    await button.trigger('click')

    expect(wrapper.text()).toContain('1')
  })
})
```

### E2E Tests (Playwright)
```typescript
// tests/e2e/home.spec.ts
import { test, expect } from '@playwright/test'

test('homepage has correct title', async ({ page }) => {
  await page.goto('/')
  await expect(page).toHaveTitle(/My Vue App/)
})
```

## Performance Targets

### Bundle Size
- **Initial JS:** < 100KB (gzipped)
- **Total Assets:** < 500KB (gzipped)

### Load Times
- **First Contentful Paint:** < 1.5s
- **Time to Interactive:** < 3.5s
- **Lighthouse Score:** > 90

### Runtime Performance
- **Page Load:** < 2s
- **Route Navigation:** < 200ms
- **API Response:** < 500ms

## Common Dependencies

### Recommended Packages
```json
{
  "dependencies": {
    "vue": "^3.4.0",
    "vue-router": "^4.2.5",
    "pinia": "^2.1.7",
    "axios": "^1.6.2"
  },
  "devDependencies": {
    "@vitejs/plugin-vue": "^5.0.0",
    "vite": "^5.0.0",
    "typescript": "^5.3.0",
    "vitest": "^1.0.0",
    "@vue/test-utils": "^2.4.0",
    "eslint": "^8.55.0",
    "prettier": "^3.1.0"
  }
}
```

---
*Last Updated: 2025*
*Vue Version: 3.4+*
*Build Tool: Vite 5+*
*Package Manager: pnpm (recommended)*

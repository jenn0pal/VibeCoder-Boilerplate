# Vue 3 PWA Technology Stack

## Core Technologies

### Framework
| Technology | Version | Purpose | Documentation |
|------------|---------|---------|---------------|
| Vue | 3.4+ | UI framework | https://vuejs.org/ |
| Vite | 5.0+ | Build tool & dev server | https://vitejs.dev/ |
| Vue Router | 4.x | Client-side routing | https://router.vuejs.org/ |

### PWA Essentials
| Technology | Version | Purpose | Documentation |
|------------|---------|---------|---------------|
| vite-plugin-pwa | Latest | PWA plugin for Vite | https://vite-pwa-org.netlify.app/ |
| Workbox | 7.x | Service worker library | https://developer.chrome.com/docs/workbox/ |

### State Management
| Technology | Version | Purpose | Documentation |
|------------|---------|---------|---------------|
| Pinia | 2.x | State management | https://pinia.vuejs.org/ |
| pinia-plugin-persistedstate | Latest | Persist state to localStorage | https://prazdevs.github.io/pinia-plugin-persistedstate/ |

### UI Libraries (Choose One or None)
| Technology | Version | Purpose | Documentation |
|------------|---------|---------|---------------|
| Vuetify | 3.x | Material Design components | https://vuetifyjs.com/ |
| Quasar | 2.x | Full PWA framework | https://quasar.dev/ |
| Ionic Vue | 7.x | Mobile-first components | https://ionicframework.com/docs/vue/overview |

## PWA Features

### Service Worker
- **Strategy:** Workbox with custom caching strategies
- **Registration:** Automatic via vite-plugin-pwa
- **Update Prompt:** User-controlled updates
- **Offline Support:** Network-first with cache fallback

### Manifest Configuration
```typescript
// vite.config.ts
import { VitePWA } from 'vite-plugin-pwa'

export default defineConfig({
  plugins: [
    vue(),
    VitePWA({
      registerType: 'prompt',
      includeAssets: ['favicon.ico', 'apple-touch-icon.png', 'masked-icon.svg'],
      manifest: {
        name: 'My Vue PWA App',
        short_name: 'VuePWA',
        description: 'My awesome Progressive Web App',
        theme_color: '#ffffff',
        background_color: '#ffffff',
        display: 'standalone',
        scope: '/',
        start_url: '/',
        icons: [
          {
            src: 'pwa-192x192.png',
            sizes: '192x192',
            type: 'image/png'
          },
          {
            src: 'pwa-512x512.png',
            sizes: '512x512',
            type: 'image/png'
          },
          {
            src: 'pwa-512x512.png',
            sizes: '512x512',
            type: 'image/png',
            purpose: 'any maskable'
          }
        ]
      },
      workbox: {
        globPatterns: ['**/*.{js,css,html,ico,png,svg,woff2}'],
        runtimeCaching: [
          {
            urlPattern: /^https:\/\/api\.example\.com\/.*/i,
            handler: 'NetworkFirst',
            options: {
              cacheName: 'api-cache',
              expiration: {
                maxEntries: 100,
                maxAgeSeconds: 60 * 60 * 24 // 1 day
              },
              cacheableResponse: {
                statuses: [0, 200]
              }
            }
          }
        ]
      }
    })
  ]
})
```

### Caching Strategies
- **Network First:** API requests
- **Cache First:** Static assets (images, fonts)
- **Stale While Revalidate:** HTML, CSS, JS
- **Network Only:** Authentication requests

## Development Tools

### Build & Dev
| Technology | Version | Purpose | Documentation |
|------------|---------|---------|---------------|
| Vite | 5.0+ | Build tool & HMR | https://vitejs.dev/ |
| @vitejs/plugin-vue | Latest | Vue 3 plugin for Vite | https://github.com/vitejs/vite-plugin-vue |
| vite-plugin-pwa | Latest | PWA integration | https://vite-pwa-org.netlify.app/ |

### Code Quality
| Technology | Version | Purpose | Documentation |
|------------|---------|---------|---------------|
| ESLint | 8.x | Linting | https://eslint.org/ |
| Prettier | 3.x | Code formatting | https://prettier.io/ |
| TypeScript | 5.x | Type checking | https://www.typescriptlang.org/ |

### Testing
| Technology | Version | Purpose | Documentation |
|------------|---------|---------|---------------|
| Vitest | 1.x | Unit testing | https://vitest.dev/ |
| @vue/test-utils | 2.x | Vue component testing | https://test-utils.vuejs.org/ |
| Playwright | Latest | E2E testing | https://playwright.dev/ |
| workbox-testing | Latest | SW testing | https://developer.chrome.com/docs/workbox/modules/workbox-testing |

## Package Management

### Primary Package Manager
- **Recommended:** pnpm
- **Alternative:** npm, yarn
- **Lock File:** pnpm-lock.yaml

### Common Commands
```bash
# Initialize new Vue PWA project
pnpm create vue@latest
# Select PWA support during setup

# Install dependencies
pnpm install

# Development (with PWA disabled for faster dev)
pnpm run dev

# Build for production (includes PWA assets)
pnpm run build

# Preview PWA build (important for testing SW)
pnpm run preview

# Generate PWA assets
pnpm run generate-pwa-assets

# Test service worker
pnpm run test:sw

# Lint
pnpm run lint
```

## Project Structure

### PWA-Specific Structure
```
project/
├── public/
│   ├── favicon.ico
│   ├── pwa-192x192.png        # PWA icons
│   ├── pwa-512x512.png
│   ├── apple-touch-icon.png
│   └── masked-icon.svg
├── src/
│   ├── assets/
│   ├── components/
│   │   ├── common/
│   │   └── pwa/               # PWA-specific components
│   │       ├── InstallPrompt.vue
│   │       ├── UpdatePrompt.vue
│   │       └── OfflineBanner.vue
│   ├── composables/
│   │   ├── useNetworkStatus.ts  # Network detection
│   │   ├── usePWAInstall.ts     # Install prompt
│   │   └── usePWAUpdate.ts      # Update prompt
│   ├── layouts/
│   ├── pages/
│   ├── router/
│   ├── stores/
│   ├── sw/                    # Service worker custom logic
│   │   └── custom-sw.ts
│   ├── types/
│   ├── utils/
│   ├── App.vue
│   └── main.ts
├── tests/
│   ├── unit/
│   ├── e2e/
│   └── sw/                    # Service worker tests
├── .env.example
├── index.html
├── manifest.webmanifest        # Auto-generated
├── package.json
├── sw.js                       # Auto-generated service worker
├── vite.config.ts
└── workbox-config.js           # Workbox configuration
```

## PWA Composables

### Network Status Detection
```typescript
// src/composables/useNetworkStatus.ts
import { ref, onMounted, onUnmounted } from 'vue'

export function useNetworkStatus() {
  const isOnline = ref(navigator.onLine)

  const updateOnlineStatus = () => {
    isOnline.value = navigator.onLine
  }

  onMounted(() => {
    window.addEventListener('online', updateOnlineStatus)
    window.addEventListener('offline', updateOnlineStatus)
  })

  onUnmounted(() => {
    window.removeEventListener('online', updateOnlineStatus)
    window.removeEventListener('offline', updateOnlineStatus)
  })

  return { isOnline }
}
```

### PWA Install Prompt
```typescript
// src/composables/usePWAInstall.ts
import { ref } from 'vue'

export function usePWAInstall() {
  const deferredPrompt = ref<any>(null)
  const showInstallPrompt = ref(false)

  window.addEventListener('beforeinstallprompt', (e) => {
    e.preventDefault()
    deferredPrompt.value = e
    showInstallPrompt.value = true
  })

  const install = async () => {
    if (!deferredPrompt.value) return false

    deferredPrompt.value.prompt()
    const { outcome } = await deferredPrompt.value.userChoice

    deferredPrompt.value = null
    showInstallPrompt.value = false

    return outcome === 'accepted'
  }

  return { showInstallPrompt, install }
}
```

### PWA Update Prompt
```typescript
// src/composables/usePWAUpdate.ts
import { ref } from 'vue'
import { useRegisterSW } from 'virtual:pwa-register/vue'

export function usePWAUpdate() {
  const {
    offlineReady,
    needRefresh,
    updateServiceWorker,
  } = useRegisterSW()

  const close = async () => {
    offlineReady.value = false
    needRefresh.value = false
  }

  return {
    offlineReady,
    needRefresh,
    updateServiceWorker,
    close,
  }
}
```

## Offline Support

### Offline Page
```vue
<!-- src/pages/OfflinePage.vue -->
<template>
  <div class="offline-page">
    <h1>You're Offline</h1>
    <p>Please check your internet connection</p>
    <button @click="retry">Retry</button>
  </div>
</template>

<script setup lang="ts">
const retry = () => {
  if (navigator.onLine) {
    window.location.reload()
  }
}
</script>
```

### Offline Data Sync
```typescript
// src/utils/syncManager.ts
import { useNetworkStatus } from '@/composables/useNetworkStatus'

export class SyncManager {
  private pendingRequests: Array<any> = []

  constructor() {
    this.setupSync()
  }

  setupSync() {
    const { isOnline } = useNetworkStatus()

    watch(isOnline, (online) => {
      if (online) {
        this.syncPendingRequests()
      }
    })
  }

  async syncPendingRequests() {
    while (this.pendingRequests.length > 0) {
      const request = this.pendingRequests.shift()
      await this.sendRequest(request)
    }
  }

  queueRequest(request: any) {
    this.pendingRequests.push(request)
    localStorage.setItem('pending-requests', JSON.stringify(this.pendingRequests))
  }
}
```

## IndexedDB for Offline Storage

### Using Dexie.js
```typescript
// src/utils/db.ts
import Dexie, { Table } from 'dexie'

export interface Todo {
  id?: number
  title: string
  completed: boolean
  createdAt: Date
}

export class AppDatabase extends Dexie {
  todos!: Table<Todo>

  constructor() {
    super('AppDatabase')
    this.version(1).stores({
      todos: '++id, title, completed, createdAt'
    })
  }
}

export const db = new AppDatabase()
```

### Using in Components
```vue
<script setup lang="ts">
import { liveQuery } from 'dexie'
import { useObservable } from '@vueuse/rxjs'
import { db } from '@/utils/db'

const todos = useObservable(
  liveQuery(() => db.todos.toArray())
)

async function addTodo(title: string) {
  await db.todos.add({
    title,
    completed: false,
    createdAt: new Date()
  })
}
</script>
```

## Push Notifications

### Setup Push Notifications
```typescript
// src/utils/notifications.ts
export async function requestNotificationPermission() {
  if (!('Notification' in window)) {
    console.log('This browser does not support notifications')
    return false
  }

  const permission = await Notification.requestPermission()
  return permission === 'granted'
}

export async function subscribeToPush() {
  const registration = await navigator.serviceWorker.ready

  const subscription = await registration.pushManager.subscribe({
    userVisibleOnly: true,
    applicationServerKey: urlBase64ToUint8Array(
      import.meta.env.VITE_VAPID_PUBLIC_KEY
    )
  })

  // Send subscription to your backend
  await fetch('/api/push/subscribe', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify(subscription)
  })
}

export function showNotification(title: string, options?: NotificationOptions) {
  if (Notification.permission === 'granted') {
    navigator.serviceWorker.ready.then((registration) => {
      registration.showNotification(title, options)
    })
  }
}
```

## Deployment

### Build for Production
```bash
# Build with PWA assets
pnpm run build

# Output:
# dist/
# ├── index.html
# ├── sw.js                    # Service worker
# ├── manifest.webmanifest     # Web app manifest
# ├── workbox-*.js            # Workbox runtime
# └── assets/                  # App bundles
```

### Hosting Requirements
- **HTTPS:** Required for service workers
- **Headers:** Proper MIME types for manifest and SW
- **Caching:** Configure server to allow SW caching

### Nginx Configuration
```nginx
server {
    listen 443 ssl http2;
    server_name example.com;
    root /var/www/dist;
    index index.html;

    # SSL Configuration
    ssl_certificate /path/to/cert.pem;
    ssl_certificate_key /path/to/key.pem;

    # Service Worker
    location = /sw.js {
        add_header Cache-Control "no-cache, no-store, must-revalidate";
        add_header Service-Worker-Allowed "/";
    }

    # Manifest
    location = /manifest.webmanifest {
        add_header Content-Type application/manifest+json;
        add_header Cache-Control "public, max-age=604800";
    }

    # Static assets
    location ~* \.(js|css|png|jpg|jpeg|gif|ico|svg|woff|woff2)$ {
        expires 1y;
        add_header Cache-Control "public, immutable";
    }

    # SPA fallback
    location / {
        try_files $uri $uri/ /index.html;
    }
}
```

## Testing PWA Features

### Test Service Worker
```typescript
// tests/sw/service-worker.spec.ts
import { describe, it, expect } from 'vitest'

describe('Service Worker', () => {
  it('should register successfully', async () => {
    const registration = await navigator.serviceWorker.register('/sw.js')
    expect(registration).toBeDefined()
  })

  it('should cache critical assets', async () => {
    const cache = await caches.open('app-cache-v1')
    const keys = await cache.keys()
    expect(keys.length).toBeGreaterThan(0)
  })
})
```

### Lighthouse PWA Audit
```bash
# Install Lighthouse CLI
npm install -g @lh ci/cli

# Run PWA audit
lhci autorun --collect.url=https://example.com
```

## Performance Targets

### PWA Scores (Lighthouse)
- **PWA Score:** 100
- **Performance:** > 90
- **Accessibility:** > 90
- **Best Practices:** > 90
- **SEO:** > 90

### Bundle Size (PWA-specific)
- **Service Worker:** < 50KB
- **App Shell:** < 150KB (gzipped)
- **Total Initial Load:** < 500KB

### Runtime Performance
- **First Load (Online):** < 2s
- **Subsequent Loads (Cached):** < 500ms
- **Time to Interactive:** < 3s

## Common Dependencies

### Essential PWA Packages
```json
{
  "dependencies": {
    "vue": "^3.4.0",
    "vue-router": "^4.2.5",
    "pinia": "^2.1.7",
    "pinia-plugin-persistedstate": "^3.2.1",
    "axios": "^1.6.2",
    "dexie": "^3.2.4",
    "@vueuse/core": "^10.7.0"
  },
  "devDependencies": {
    "@vitejs/plugin-vue": "^5.0.0",
    "vite": "^5.0.0",
    "vite-plugin-pwa": "^0.17.4",
    "workbox-window": "^7.0.0",
    "typescript": "^5.3.0",
    "vitest": "^1.0.0"
  }
}
```

---
*Last Updated: 2025*
*Vue Version: 3.4+*
*Build Tool: Vite 5+*
*PWA Plugin: vite-plugin-pwa*
*Service Worker: Workbox 7+*

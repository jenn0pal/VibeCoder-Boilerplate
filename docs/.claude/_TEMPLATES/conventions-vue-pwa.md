# Vue 3 PWA + Vite + Pinia Project Conventions

## Code Style

### General Principles
- **Composition API First:** Prefer `<script setup>` for all components
- **TypeScript by Default:** Use TypeScript for type safety and better DX
- **PWA-First Design:** Offline-first architecture with service workers
- **Progressive Enhancement:** App works offline and improves when online
- **Mobile-First:** Optimize for mobile devices and touch interactions
- **Performance-Critical:** Fast load times, minimal bundle size
- **Install Prompts:** Make app installable on all platforms

### Naming Conventions
| Type | Convention | Example |
|------|------------|---------|
| Components | PascalCase | `UserProfile.vue`, `NavBar.vue` |
| Composables | camelCase with 'use' | `useAuth.ts`, `useOffline.ts` |
| Stores (Pinia) | camelCase with 'use' + 'Store' | `useAuthStore.ts`, `useSyncStore.ts` |
| Views/Pages | PascalCase | `HomeView.vue`, `OfflineView.vue` |
| Service Workers | kebab-case | `service-worker.ts`, `sw.ts` |
| Web Workers | kebab-case | `sync-worker.ts` |
| Utilities | camelCase | `cacheManager.ts`, `syncQueue.ts` |
| Variables | camelCase | `isOnline`, `syncStatus` |
| Constants | UPPER_SNAKE_CASE | `CACHE_NAME`, `SYNC_INTERVAL` |
| Types/Interfaces | PascalCase | `SyncItem`, `CacheStrategy` |

### File Organization
```
my-pwa-app/
├── public/
│   ├── manifest.json           # PWA manifest
│   ├── icons/                  # App icons (various sizes)
│   │   ├── icon-72x72.png
│   │   ├── icon-96x96.png
│   │   ├── icon-128x128.png
│   │   ├── icon-144x144.png
│   │   ├── icon-152x152.png
│   │   ├── icon-192x192.png
│   │   ├── icon-384x384.png
│   │   └── icon-512x512.png
│   ├── favicon.ico
│   └── robots.txt
├── src/
│   ├── assets/
│   │   ├── images/
│   │   ├── fonts/
│   │   └── styles/
│   ├── components/
│   │   ├── common/
│   │   │   ├── Button.vue
│   │   │   ├── Modal.vue
│   │   │   └── OfflineBanner.vue
│   │   ├── pwa/              # PWA-specific components
│   │   │   ├── InstallPrompt.vue
│   │   │   ├── UpdateNotification.vue
│   │   │   └── SyncStatus.vue
│   │   └── features/
│   ├── composables/
│   │   ├── useAuth.ts
│   │   ├── useOnline.ts      # Network status
│   │   ├── useSync.ts        # Background sync
│   │   ├── usePWA.ts         # PWA install & update
│   │   ├── useCache.ts       # Cache management
│   │   └── useNotifications.ts # Push notifications
│   ├── router/
│   │   ├── index.ts
│   │   └── guards.ts
│   ├── stores/
│   │   ├── auth.ts
│   │   ├── sync.ts           # Sync queue management
│   │   ├── offline.ts        # Offline data
│   │   └── index.ts
│   ├── services/
│   │   ├── api/
│   │   │   ├── client.ts
│   │   │   └── offline.ts    # Offline API adapter
│   │   ├── cache/
│   │   │   ├── strategies.ts # Cache strategies
│   │   │   └── manager.ts
│   │   ├── sync/
│   │   │   ├── queue.ts      # Sync queue
│   │   │   └── worker.ts     # Background sync
│   │   └── db/
│   │       └── indexed-db.ts # IndexedDB wrapper
│   ├── workers/              # Web Workers
│   │   ├── sync-worker.ts
│   │   └── cache-worker.ts
│   ├── views/
│   │   ├── HomeView.vue
│   │   └── OfflineView.vue
│   ├── utils/
│   │   ├── pwa.ts
│   │   └── storage.ts
│   ├── types/
│   │   ├── index.ts
│   │   ├── pwa.ts
│   │   └── sync.ts
│   ├── App.vue
│   ├── main.ts
│   ├── registerServiceWorker.ts
│   └── env.d.ts
├── service-worker.ts         # Service worker entry
├── index.html
├── vite.config.ts
├── tsconfig.json
└── package.json
```

## PWA Manifest Configuration

### public/manifest.json
```json
{
  "name": "My PWA Application",
  "short_name": "My PWA",
  "description": "A progressive web application built with Vue 3",
  "start_url": "/",
  "display": "standalone",
  "background_color": "#ffffff",
  "theme_color": "#4DBA87",
  "orientation": "portrait-primary",
  "icons": [
    {
      "src": "/icons/icon-72x72.png",
      "sizes": "72x72",
      "type": "image/png",
      "purpose": "any"
    },
    {
      "src": "/icons/icon-96x96.png",
      "sizes": "96x96",
      "type": "image/png",
      "purpose": "any"
    },
    {
      "src": "/icons/icon-128x128.png",
      "sizes": "128x128",
      "type": "image/png",
      "purpose": "any"
    },
    {
      "src": "/icons/icon-144x144.png",
      "sizes": "144x144",
      "type": "image/png",
      "purpose": "any"
    },
    {
      "src": "/icons/icon-152x152.png",
      "sizes": "152x152",
      "type": "image/png",
      "purpose": "any"
    },
    {
      "src": "/icons/icon-192x192.png",
      "sizes": "192x192",
      "type": "image/png",
      "purpose": "any maskable"
    },
    {
      "src": "/icons/icon-384x384.png",
      "sizes": "384x384",
      "type": "image/png",
      "purpose": "any"
    },
    {
      "src": "/icons/icon-512x512.png",
      "sizes": "512x512",
      "type": "image/png",
      "purpose": "any maskable"
    }
  ],
  "categories": ["productivity", "utilities"],
  "screenshots": [
    {
      "src": "/screenshots/home.png",
      "sizes": "540x720",
      "type": "image/png"
    }
  ]
}
```

## Vite PWA Configuration

### vite.config.ts
```typescript
import { fileURLToPath, URL } from 'node:url'
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'
import { VitePWA } from 'vite-plugin-pwa'

export default defineConfig({
  plugins: [
    vue(),
    VitePWA({
      registerType: 'prompt',
      includeAssets: ['favicon.ico', 'robots.txt', 'icons/*.png'],

      manifest: {
        name: 'My PWA Application',
        short_name: 'My PWA',
        description: 'A progressive web application',
        theme_color: '#4DBA87',
        background_color: '#ffffff',
        display: 'standalone',
        scope: '/',
        start_url: '/',
        icons: [
          {
            src: 'icons/icon-192x192.png',
            sizes: '192x192',
            type: 'image/png',
            purpose: 'any maskable'
          },
          {
            src: 'icons/icon-512x512.png',
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
                maxAgeSeconds: 60 * 60 * 24 // 24 hours
              },
              cacheableResponse: {
                statuses: [0, 200]
              }
            }
          },
          {
            urlPattern: /^https:\/\/cdn\.example\.com\/.*/i,
            handler: 'CacheFirst',
            options: {
              cacheName: 'cdn-cache',
              expiration: {
                maxEntries: 50,
                maxAgeSeconds: 60 * 60 * 24 * 30 // 30 days
              }
            }
          },
          {
            urlPattern: /\.(?:png|jpg|jpeg|svg|gif|webp)$/i,
            handler: 'CacheFirst',
            options: {
              cacheName: 'images-cache',
              expiration: {
                maxEntries: 100,
                maxAgeSeconds: 60 * 60 * 24 * 30 // 30 days
              }
            }
          }
        ]
      },

      devOptions: {
        enabled: true,
        type: 'module'
      }
    })
  ],

  resolve: {
    alias: {
      '@': fileURLToPath(new URL('./src', import.meta.url))
    }
  },

  server: {
    port: 3000,
    host: true
  },

  build: {
    target: 'esnext',
    sourcemap: true,
    rollupOptions: {
      output: {
        manualChunks: {
          'vue-vendor': ['vue', 'vue-router', 'pinia'],
          'pwa-vendor': ['workbox-window', 'idb']
        }
      }
    }
  }
})
```

## Service Worker Registration

### src/registerServiceWorker.ts
```typescript
import { useRegisterSW } from 'virtual:pwa-register/vue'

const intervalMS = 60 * 60 * 1000 // 1 hour

export const { offlineReady, needRefresh, updateServiceWorker } = useRegisterSW({
  onRegistered(r) {
    console.log('Service Worker registered')
    if (r) {
      setInterval(() => {
        r.update()
      }, intervalMS)
    }
  },
  onRegisterError(error) {
    console.error('SW registration error', error)
  }
})
```

### src/main.ts
```typescript
import { createApp } from 'vue'
import { createPinia } from 'pinia'
import App from './App.vue'
import router from './router'
import './registerServiceWorker'

const app = createApp(App)

app.use(createPinia())
app.use(router)

app.mount('#app')
```

## PWA Composables

### useOnline Composable
```typescript
// composables/useOnline.ts
import { ref, onMounted, onUnmounted } from 'vue'

export function useOnline() {
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

  return {
    isOnline: readonly(isOnline)
  }
}
```

### usePWA Composable
```typescript
// composables/usePWA.ts
import { ref, computed } from 'vue'
import { useRegisterSW } from 'virtual:pwa-register/vue'

export function usePWA() {
  const { offlineReady, needRefresh, updateServiceWorker } = useRegisterSW()

  const showInstallPrompt = ref(false)
  const installPromptEvent = ref<any>(null)

  const isInstallable = computed(() => !!installPromptEvent.value)
  const isInstalled = computed(() => {
    return window.matchMedia('(display-mode: standalone)').matches ||
           (window.navigator as any).standalone === true
  })

  const handleBeforeInstallPrompt = (e: Event) => {
    e.preventDefault()
    installPromptEvent.value = e
    showInstallPrompt.value = true
  }

  const install = async () => {
    if (!installPromptEvent.value) return

    installPromptEvent.value.prompt()
    const { outcome } = await installPromptEvent.value.userChoice

    if (outcome === 'accepted') {
      installPromptEvent.value = null
      showInstallPrompt.value = false
    }
  }

  const dismissInstall = () => {
    showInstallPrompt.value = false
  }

  // Listen for install prompt
  window.addEventListener('beforeinstallprompt', handleBeforeInstallPrompt)

  return {
    offlineReady: readonly(offlineReady),
    needRefresh: readonly(needRefresh),
    showInstallPrompt: readonly(showInstallPrompt),
    isInstallable,
    isInstalled,
    install,
    dismissInstall,
    updateServiceWorker
  }
}
```

### useSync Composable
```typescript
// composables/useSync.ts
import { ref } from 'vue'
import { useSyncStore } from '@/stores/sync'

export function useSync() {
  const syncStore = useSyncStore()
  const isSyncing = ref(false)

  const sync = async () => {
    if (isSyncing.value) return

    isSyncing.value = true
    try {
      await syncStore.processQueue()
    } finally {
      isSyncing.value = false
    }
  }

  const addToSyncQueue = async (item: any) => {
    await syncStore.addToQueue(item)

    // Try immediate sync if online
    if (navigator.onLine) {
      await sync()
    }
  }

  return {
    isSyncing: readonly(isSyncing),
    pendingItems: computed(() => syncStore.queue),
    sync,
    addToSyncQueue
  }
}
```

### useNotifications Composable
```typescript
// composables/useNotifications.ts
import { ref, computed } from 'vue'

export function useNotifications() {
  const permission = ref<NotificationPermission>(Notification.permission)
  const isSupported = 'Notification' in window

  const isGranted = computed(() => permission.value === 'granted')
  const isDenied = computed(() => permission.value === 'denied')

  const requestPermission = async () => {
    if (!isSupported) return false

    const result = await Notification.requestPermission()
    permission.value = result
    return result === 'granted'
  }

  const showNotification = (title: string, options?: NotificationOptions) => {
    if (!isGranted.value) {
      console.warn('Notification permission not granted')
      return
    }

    return new Notification(title, {
      icon: '/icons/icon-192x192.png',
      badge: '/icons/icon-72x72.png',
      ...options
    })
  }

  return {
    permission: readonly(permission),
    isSupported,
    isGranted,
    isDenied,
    requestPermission,
    showNotification
  }
}
```

## Pinia Store for Sync Queue

### stores/sync.ts
```typescript
import { defineStore } from 'pinia'
import { openDB, type IDBPDatabase } from 'idb'

interface SyncItem {
  id: string
  type: 'create' | 'update' | 'delete'
  endpoint: string
  data: any
  timestamp: number
  retries: number
}

const DB_NAME = 'sync-db'
const STORE_NAME = 'sync-queue'

export const useSyncStore = defineStore('sync', () => {
  const queue = ref<SyncItem[]>([])
  const processing = ref(false)
  let db: IDBPDatabase | null = null

  const initDB = async () => {
    if (db) return db

    db = await openDB(DB_NAME, 1, {
      upgrade(database) {
        if (!database.objectStoreNames.contains(STORE_NAME)) {
          database.createObjectStore(STORE_NAME, { keyPath: 'id' })
        }
      }
    })

    return db
  }

  const loadQueue = async () => {
    const database = await initDB()
    const tx = database.transaction(STORE_NAME, 'readonly')
    const store = tx.objectStore(STORE_NAME)
    queue.value = await store.getAll()
  }

  const addToQueue = async (item: Omit<SyncItem, 'id' | 'timestamp' | 'retries'>) => {
    const database = await initDB()
    const syncItem: SyncItem = {
      ...item,
      id: `${Date.now()}-${Math.random()}`,
      timestamp: Date.now(),
      retries: 0
    }

    const tx = database.transaction(STORE_NAME, 'readwrite')
    await tx.objectStore(STORE_NAME).add(syncItem)
    await tx.done

    queue.value.push(syncItem)
  }

  const removeFromQueue = async (id: string) => {
    const database = await initDB()
    const tx = database.transaction(STORE_NAME, 'readwrite')
    await tx.objectStore(STORE_NAME).delete(id)
    await tx.done

    queue.value = queue.value.filter(item => item.id !== id)
  }

  const processQueue = async () => {
    if (processing.value || !navigator.onLine) return

    processing.value = true

    try {
      for (const item of queue.value) {
        try {
          await fetch(item.endpoint, {
            method: item.type === 'delete' ? 'DELETE' : 'POST',
            headers: { 'Content-Type': 'application/json' },
            body: JSON.stringify(item.data)
          })

          await removeFromQueue(item.id)
        } catch (error) {
          item.retries++
          if (item.retries >= 3) {
            console.error('Max retries reached for sync item', item)
            await removeFromQueue(item.id)
          }
        }
      }
    } finally {
      processing.value = false
    }
  }

  // Initialize
  loadQueue()

  // Auto-sync when coming online
  window.addEventListener('online', processQueue)

  return {
    queue: readonly(queue),
    processing: readonly(processing),
    addToQueue,
    removeFromQueue,
    processQueue
  }
})
```

## PWA Components

### InstallPrompt Component
```vue
<!-- components/pwa/InstallPrompt.vue -->
<script setup lang="ts">
import { usePWA } from '@/composables/usePWA'

const { showInstallPrompt, install, dismissInstall } = usePWA()
</script>

<template>
  <Transition name="slide-up">
    <div v-if="showInstallPrompt" class="install-prompt">
      <div class="install-prompt__content">
        <h3>Install App</h3>
        <p>Install this app on your device for a better experience.</p>
        <div class="install-prompt__actions">
          <button @click="install" class="btn btn--primary">
            Install
          </button>
          <button @click="dismissInstall" class="btn btn--text">
            Maybe Later
          </button>
        </div>
      </div>
    </div>
  </Transition>
</template>

<style scoped>
.install-prompt {
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  background: white;
  border-top: 1px solid var(--color-border);
  padding: 1rem;
  box-shadow: 0 -2px 10px rgba(0, 0, 0, 0.1);
  z-index: 1000;
}

.install-prompt__actions {
  display: flex;
  gap: 0.5rem;
  margin-top: 1rem;
}

.slide-up-enter-active,
.slide-up-leave-active {
  transition: transform 0.3s ease;
}

.slide-up-enter-from,
.slide-up-leave-to {
  transform: translateY(100%);
}
</style>
```

### UpdateNotification Component
```vue
<!-- components/pwa/UpdateNotification.vue -->
<script setup lang="ts">
import { usePWA } from '@/composables/usePWA'

const { needRefresh, updateServiceWorker } = usePWA()

const handleUpdate = () => {
  updateServiceWorker(true)
}
</script>

<template>
  <Transition name="fade">
    <div v-if="needRefresh" class="update-notification">
      <p>A new version is available!</p>
      <button @click="handleUpdate" class="btn btn--primary">
        Update Now
      </button>
    </div>
  </Transition>
</template>

<style scoped>
.update-notification {
  position: fixed;
  top: 1rem;
  right: 1rem;
  background: var(--color-primary);
  color: white;
  padding: 1rem;
  border-radius: 0.5rem;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.2);
  z-index: 1000;
  display: flex;
  align-items: center;
  gap: 1rem;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
```

### OfflineBanner Component
```vue
<!-- components/common/OfflineBanner.vue -->
<script setup lang="ts">
import { useOnline } from '@/composables/useOnline'

const { isOnline } = useOnline()
</script>

<template>
  <Transition name="slide-down">
    <div v-if="!isOnline" class="offline-banner">
      You are currently offline. Some features may be limited.
    </div>
  </Transition>
</template>

<style scoped>
.offline-banner {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  background: var(--color-warning);
  color: white;
  padding: 0.75rem;
  text-align: center;
  z-index: 1000;
}

.slide-down-enter-active,
.slide-down-leave-active {
  transition: transform 0.3s ease;
}

.slide-down-enter-from,
.slide-down-leave-to {
  transform: translateY(-100%);
}
</style>
```

## Cache Strategies

### services/cache/strategies.ts
```typescript
export enum CacheStrategy {
  NetworkFirst = 'NetworkFirst',
  CacheFirst = 'CacheFirst',
  NetworkOnly = 'NetworkOnly',
  CacheOnly = 'CacheOnly',
  StaleWhileRevalidate = 'StaleWhileRevalidate'
}

export const getCacheStrategy = (url: string): CacheStrategy => {
  // API calls - try network first
  if (url.includes('/api/')) {
    return CacheStrategy.NetworkFirst
  }

  // Static assets - cache first
  if (url.match(/\.(png|jpg|jpeg|svg|css|js|woff2)$/)) {
    return CacheStrategy.CacheFirst
  }

  // Default
  return CacheStrategy.NetworkFirst
}
```

## IndexedDB Wrapper

### services/db/indexed-db.ts
```typescript
import { openDB, type IDBPDatabase } from 'idb'

const DB_NAME = 'app-db'
const DB_VERSION = 1

let dbInstance: IDBPDatabase | null = null

export async function getDB() {
  if (dbInstance) return dbInstance

  dbInstance = await openDB(DB_NAME, DB_VERSION, {
    upgrade(db) {
      // Create object stores
      if (!db.objectStoreNames.contains('users')) {
        db.createObjectStore('users', { keyPath: 'id' })
      }

      if (!db.objectStoreNames.contains('posts')) {
        db.createObjectStore('posts', { keyPath: 'id' })
      }

      if (!db.objectStoreNames.contains('cache')) {
        const cacheStore = db.createObjectStore('cache', { keyPath: 'key' })
        cacheStore.createIndex('timestamp', 'timestamp')
      }
    }
  })

  return dbInstance
}

export async function setItem<T>(storeName: string, item: T) {
  const db = await getDB()
  const tx = db.transaction(storeName, 'readwrite')
  await tx.objectStore(storeName).put(item)
  await tx.done
}

export async function getItem<T>(storeName: string, key: string): Promise<T | undefined> {
  const db = await getDB()
  return db.get(storeName, key)
}

export async function getAllItems<T>(storeName: string): Promise<T[]> {
  const db = await getDB()
  return db.getAll(storeName)
}

export async function deleteItem(storeName: string, key: string) {
  const db = await getDB()
  await db.delete(storeName, key)
}

export async function clearStore(storeName: string) {
  const db = await getDB()
  await db.clear(storeName)
}
```

## Performance Best Practices

### Lazy Loading & Code Splitting
```typescript
// router/index.ts
const routes = [
  {
    path: '/',
    component: () => import('@/views/HomeView.vue')
  },
  {
    path: '/offline',
    component: () => import('@/views/OfflineView.vue')
  }
]
```

### Image Optimization
```vue
<template>
  <img
    :src="imageSrc"
    loading="lazy"
    decoding="async"
    :width="width"
    :height="height"
    :alt="alt"
  />
</template>
```

### Resource Hints
```html
<!-- index.html -->
<head>
  <link rel="preconnect" href="https://api.example.com">
  <link rel="dns-prefetch" href="https://cdn.example.com">
  <link rel="manifest" href="/manifest.json">
  <meta name="theme-color" content="#4DBA87">
</head>
```

## Testing PWA Features

### Testing Service Worker
```typescript
// __tests__/service-worker.spec.ts
import { describe, it, expect, beforeEach } from 'vitest'

describe('Service Worker', () => {
  beforeEach(() => {
    // Mock service worker
  })

  it('registers service worker', async () => {
    const registration = await navigator.serviceWorker.register('/sw.js')
    expect(registration).toBeDefined()
  })

  it('caches static assets', async () => {
    const cache = await caches.open('static-cache')
    const response = await cache.match('/index.html')
    expect(response).toBeDefined()
  })
})
```

### Testing Offline Functionality
```typescript
// composables/__tests__/useOnline.spec.ts
import { describe, it, expect } from 'vitest'
import { useOnline } from '@/composables/useOnline'

describe('useOnline', () => {
  it('detects online status', () => {
    const { isOnline } = useOnline()
    expect(isOnline.value).toBe(navigator.onLine)
  })

  it('updates on network change', async () => {
    const { isOnline } = useOnline()

    // Simulate going offline
    window.dispatchEvent(new Event('offline'))
    await nextTick()
    expect(isOnline.value).toBe(false)

    // Simulate coming online
    window.dispatchEvent(new Event('online'))
    await nextTick()
    expect(isOnline.value).toBe(true)
  })
})
```

## Security Best Practices

### Content Security Policy
```html
<!-- index.html -->
<meta
  http-equiv="Content-Security-Policy"
  content="
    default-src 'self';
    script-src 'self' 'unsafe-inline' 'unsafe-eval';
    style-src 'self' 'unsafe-inline';
    img-src 'self' data: https:;
    font-src 'self' data:;
    connect-src 'self' https://api.example.com;
  "
>
```

### HTTPS Only
```typescript
// Redirect to HTTPS in production
if (import.meta.env.PROD && location.protocol !== 'https:') {
  location.replace(`https:${location.href.substring(location.protocol.length)}`)
}
```

## Package.json Scripts

```json
{
  "scripts": {
    "dev": "vite",
    "build": "vite build",
    "preview": "vite preview",
    "test:unit": "vitest",
    "type-check": "vue-tsc --noEmit",
    "lighthouse": "lighthouse http://localhost:4173 --view",
    "analyze": "vite-bundle-visualizer"
  },
  "dependencies": {
    "vue": "^3.4.0",
    "vue-router": "^4.2.0",
    "pinia": "^2.1.0",
    "idb": "^8.0.0",
    "workbox-window": "^7.0.0"
  },
  "devDependencies": {
    "@vitejs/plugin-vue": "^5.0.0",
    "vite": "^5.0.0",
    "vite-plugin-pwa": "^0.19.0",
    "typescript": "^5.3.0",
    "vue-tsc": "^1.8.0",
    "vitest": "^1.0.0"
  }
}
```

---
*Last Updated: 2025*
*Vue Version: 3.x*
*Vite Version: 5.x+*
*Pinia Version: 2.x*
*Workbox Version: 7.x*

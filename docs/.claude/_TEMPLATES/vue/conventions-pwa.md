# Vue 3 PWA Specific Conventions

> **This file contains PWA-specific additions**
>
> **IMPORTANT:** This file extends `conventions-base.md` AND `conventions-spa.md` - read those first!
>
> Only PWA-specific patterns are documented here:
> - Service Worker registration
> - Offline functionality
> - Install prompts
> - Background sync
> - Push notifications

## PWA-Specific Features

### Service Worker
```typescript
// src/registerServiceWorker.ts
import { useRegisterSW } from 'virtual:pwa-register/vue'

export const { offlineReady, needRefresh, updateServiceWorker } = useRegisterSW({
  onRegistered(r) {
    // Auto-update every hour
    setInterval(() => r?.update(), 60 * 60 * 1000)
  }
})
```

### PWA Composables
```typescript
// composables/usePWA.ts
export function usePWA() {
  const { offlineReady, needRefresh, updateServiceWorker } = useRegisterSW()
  const showInstallPrompt = ref(false)
  const installPromptEvent = ref<any>(null)

  const install = async () => {
    if (!installPromptEvent.value) return
    installPromptEvent.value.prompt()
    const { outcome } = await installPromptEvent.value.userChoice
    if (outcome === 'accepted') {
      showInstallPrompt.value = false
    }
  }

  window.addEventListener('beforeinstallprompt', (e) => {
    e.preventDefault()
    installPromptEvent.value = e
    showInstallPrompt.value = true
  })

  return {
    offlineReady,
    needRefresh,
    showInstallPrompt,
    install,
    updateServiceWorker
  }
}

// composables/useOnline.ts
export function useOnline() {
  const isOnline = ref(navigator.onLine)

  const updateStatus = () => {
    isOnline.value = navigator.onLine
  }

  onMounted(() => {
    window.addEventListener('online', updateStatus)
    window.addEventListener('offline', updateStatus)
  })

  onUnmounted(() => {
    window.removeEventListener('online', updateStatus)
    window.removeEventListener('offline', updateStatus)
  })

  return { isOnline }
}
```

### Offline Data Sync
```typescript
// stores/sync.ts
import { defineStore } from 'pinia'
import { openDB } from 'idb'

export const useSyncStore = defineStore('sync', () => {
  const queue = ref<SyncItem[]>([])

  const addToQueue = async (item: SyncItem) => {
    const db = await openDB('sync-db', 1)
    await db.add('sync-queue', item)
    queue.value.push(item)

    // Try immediate sync if online
    if (navigator.onLine) {
      await processQueue()
    }
  }

  const processQueue = async () => {
    if (!navigator.onLine) return

    for (const item of queue.value) {
      try {
        await fetch(item.endpoint, {
          method: item.type,
          body: JSON.stringify(item.data)
        })
        await removeFromQueue(item.id)
      } catch (error) {
        console.error('Sync failed:', error)
      }
    }
  }

  // Auto-sync when coming online
  window.addEventListener('online', processQueue)

  return { queue, addToQueue, processQueue }
})
```

## Vite PWA Plugin Configuration

### vite.config.ts
```typescript
import { VitePWA } from 'vite-plugin-pwa'

export default defineConfig({
  plugins: [
    vue(),
    VitePWA({
      registerType: 'prompt',
      manifest: {
        name: 'My PWA App',
        short_name: 'PWA App',
        theme_color: '#4DBA87',
        icons: [
          {
            src: 'icons/icon-192x192.png',
            sizes: '192x192',
            type: 'image/png'
          },
          {
            src: 'icons/icon-512x512.png',
            sizes: '512x512',
            type: 'image/png'
          }
        ]
      },
      workbox: {
        runtimeCaching: [
          {
            urlPattern: /^https:\/\/api\.example\.com\/.*/i,
            handler: 'NetworkFirst',
            options: {
              cacheName: 'api-cache',
              expiration: {
                maxEntries: 100,
                maxAgeSeconds: 24 * 60 * 60 // 24 hours
              }
            }
          }
        ]
      }
    })
  ]
})
```

## PWA Components

### Install Prompt
```vue
<!-- components/pwa/InstallPrompt.vue -->
<script setup lang="ts">
const { showInstallPrompt, install, dismissInstall } = usePWA()
</script>

<template>
  <div v-if="showInstallPrompt" class="install-prompt">
    <h3>Install App</h3>
    <p>Install for a better experience</p>
    <button @click="install">Install</button>
    <button @click="dismissInstall">Later</button>
  </div>
</template>
```

### Offline Banner
```vue
<!-- components/common/OfflineBanner.vue -->
<script setup lang="ts">
const { isOnline } = useOnline()
</script>

<template>
  <div v-if="!isOnline" class="offline-banner">
    You are offline. Some features may be limited.
  </div>
</template>
```

---
*PWA Workbox: 7.x*
*Extends: conventions-base.md + conventions-spa.md*

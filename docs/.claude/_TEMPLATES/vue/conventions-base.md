# Vue 3 Base Conventions (Composition API)

> **This file contains conventions common to all Vue 3 implementations**
>
> Use this as the foundation for:
> - Nuxt 3 applications
> - Vue 3 SPA applications
> - Vue 3 PWA applications
>
> Stack-specific conventions are in separate files.

## Code Style

### General Principles
- **Composition API First:** Always use `<script setup>` for components
- **TypeScript by Default:** Use TypeScript for type safety and better DX
- **Reactive Primitives:** Use `ref` for primitives, `reactive` for objects (sparingly)
- **Computed Properties:** Prefer `computed()` for derived state
- **Single Responsibility:** One component, one purpose

### Naming Conventions
| Type | Convention | Example |
|------|------------|---------|
| Components | PascalCase | `UserProfile.vue`, `NavBar.vue` |
| Composables | camelCase with 'use' | `useAuth.ts`, `useApi.ts` |
| Props | camelCase | `userId`, `isActive` |
| Events | kebab-case | `@update:model-value`, `@item-selected` |
| Variables | camelCase | `userName`, `isLoading` |
| Constants | UPPER_SNAKE_CASE | `API_URL`, `MAX_RETRIES` |
| Types/Interfaces | PascalCase | `User`, `ApiResponse` |

## Vue 3 Component Structure

### Script Setup Pattern
```vue
<script setup lang="ts">
import type { PropType } from 'vue'

// Types & Interfaces
interface User {
  id: string
  name: string
  email: string
}

interface Props {
  userId: string
  variant?: 'default' | 'compact'
}

// Props
const props = withDefaults(defineProps<Props>(), {
  variant: 'default'
})

// Emits
const emit = defineEmits<{
  update: [user: User]
  delete: [id: string]
  close: []
}>()

// Reactive State
const isLoading = ref(false)
const error = ref<Error | null>(null)
const user = ref<User | null>(null)

// Computed Properties
const fullName = computed(() =>
  user.value ? `${user.value.firstName} ${user.value.lastName}` : ''
)

const isValid = computed(() => !!user.value?.email)

// Watchers
watch(() => props.userId, async (newId) => {
  await fetchUser(newId)
}, { immediate: true })

// Methods
const handleUpdate = async () => {
  if (!user.value) return

  try {
    isLoading.value = true
    await updateUser(user.value)
    emit('update', user.value)
  } catch (err) {
    error.value = err as Error
  } finally {
    isLoading.value = false
  }
}

// Lifecycle Hooks
onMounted(() => {
  console.log('Component mounted')
})

onUnmounted(() => {
  console.log('Component unmounted')
})
</script>

<template>
  <div v-if="isLoading" class="loading">Loading...</div>
  <div v-else-if="error" class="error">{{ error.message }}</div>
  <div v-else-if="user" :class="['user-profile', `user-profile--${variant}`]">
    <h2>{{ fullName }}</h2>
    <button @click="handleUpdate" :disabled="!isValid">
      Update
    </button>
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

## Composables Pattern

### Basic Composable Structure
```typescript
// composables/useCounter.ts
export function useCounter(initialValue = 0) {
  // State
  const count = ref(initialValue)

  // Computed
  const doubled = computed(() => count.value * 2)

  // Methods
  const increment = () => {
    count.value++
  }

  const decrement = () => {
    count.value--
  }

  const reset = () => {
    count.value = initialValue
  }

  // Return exposed API
  return {
    // State (read-only via computed)
    count: readonly(count),
    doubled,
    // Actions
    increment,
    decrement,
    reset
  }
}
```

### Composable with Async Data
```typescript
// composables/useApi.ts
export function useApi<T>(fetcher: () => Promise<T>) {
  const data = ref<T | null>(null)
  const error = ref<Error | null>(null)
  const loading = ref(false)

  const execute = async () => {
    loading.value = true
    error.value = null

    try {
      data.value = await fetcher()
    } catch (err) {
      error.value = err as Error
    } finally {
      loading.value = false
    }
  }

  const refresh = () => execute()

  return {
    data: readonly(data),
    error: readonly(error),
    loading: readonly(loading),
    execute,
    refresh
  }
}
```

## Reactivity Best Practices

### Refs vs Reactive
```typescript
// ✅ GOOD: Use ref for primitives
const count = ref(0)
const name = ref('')
const isActive = ref(false)

// ✅ GOOD: Use ref for objects that may be replaced
const user = ref<User | null>(null)

// ⚠️ Use reactive sparingly - for objects that won't be replaced
const state = reactive({
  count: 0,
  name: ''
})

// ❌ AVOID: Don't destructure reactive objects
const { count, name } = state // Loses reactivity!

// ✅ GOOD: Use toRefs to destructure
const { count, name } = toRefs(state)
```

### Computed Properties
```typescript
// ✅ GOOD: Pure computations
const fullName = computed(() =>
  `${firstName.value} ${lastName.value}`
)

// ✅ GOOD: Filtering/transforming arrays
const activeUsers = computed(() =>
  users.value.filter(u => u.isActive)
)

// ❌ AVOID: Side effects in computed
const count = computed(() => {
  console.log('Computing...') // Side effect!
  return items.value.length
})

// ✅ GOOD: Use watchers for side effects
watch(items, (newItems) => {
  console.log('Items changed:', newItems.length)
})
```

## Template Best Practices

### v-if vs v-show
```vue
<template>
  <!-- ✅ GOOD: v-if for conditional rendering (rarely changes) -->
  <div v-if="isAuthenticated">
    <UserProfile />
  </div>

  <!-- ✅ GOOD: v-show for toggling visibility (changes frequently) -->
  <div v-show="isMenuOpen" class="menu">
    Menu content
  </div>

  <!-- ✅ GOOD: v-if with v-else-if and v-else -->
  <div v-if="loading">Loading...</div>
  <div v-else-if="error">Error: {{ error.message }}</div>
  <div v-else>{{ data }}</div>
</template>
```

### List Rendering
```vue
<template>
  <!-- ✅ GOOD: Always use :key with v-for -->
  <div v-for="item in items" :key="item.id">
    {{ item.name }}
  </div>

  <!-- ✅ GOOD: Avoid v-if with v-for (use computed instead) -->
  <div v-for="item in activeItems" :key="item.id">
    {{ item.name }}
  </div>

  <!-- ❌ AVOID: v-if and v-for on same element -->
  <div v-for="item in items" :key="item.id" v-if="item.isActive">
    {{ item.name }}
  </div>
</template>

<script setup lang="ts">
const activeItems = computed(() =>
  items.value.filter(item => item.isActive)
)
</script>
```

### Event Handling
```vue
<template>
  <!-- ✅ GOOD: Inline handlers for simple logic -->
  <button @click="count++">Increment</button>

  <!-- ✅ GOOD: Method handlers for complex logic -->
  <button @click="handleSubmit">Submit</button>

  <!-- ✅ GOOD: Passing arguments -->
  <button @click="deleteItem(item.id)">Delete</button>

  <!-- ✅ GOOD: Event modifiers -->
  <form @submit.prevent="onSubmit">...</form>
  <button @click.stop="onClick">...</button>
  <input @keyup.enter="search">

  <!-- ✅ GOOD: Custom events -->
  <UserCard @update="handleUpdate" @delete="handleDelete" />
</template>
```

## Props & Emits

### Props Definition
```typescript
// ✅ GOOD: Define props with TypeScript
interface Props {
  userId: string
  count?: number
  items: Array<Item>
  variant?: 'default' | 'compact'
}

const props = withDefaults(defineProps<Props>(), {
  count: 0,
  variant: 'default'
})

// ✅ GOOD: Props validation with runtime checks
defineProps({
  userId: {
    type: String,
    required: true
  },
  count: {
    type: Number,
    default: 0,
    validator: (value: number) => value >= 0
  }
})
```

### Emits Definition
```typescript
// ✅ GOOD: Type-safe emits
const emit = defineEmits<{
  update: [user: User]
  delete: [id: string]
  close: []
  change: [value: string, oldValue: string]
}>()

// Usage
emit('update', user)
emit('delete', '123')
emit('close')
emit('change', newVal, oldVal)
```

## Lifecycle Hooks Order

```typescript
// Import order matches execution order
import {
  onBeforeMount,
  onMounted,
  onBeforeUpdate,
  onUpdated,
  onBeforeUnmount,
  onUnmounted
} from 'vue'

// ✅ GOOD: Order hooks by lifecycle
onBeforeMount(() => {
  // Before component is mounted
})

onMounted(() => {
  // After component is mounted
  // Good for: API calls, DOM manipulation, event listeners
})

onBeforeUpdate(() => {
  // Before component updates
})

onUpdated(() => {
  // After component updates
})

onBeforeUnmount(() => {
  // Before component unmounts
  // Good for: Cleanup, removing listeners
})

onUnmounted(() => {
  // After component unmounts
})
```

## Type Definitions

### Component Types
```typescript
// types/index.ts
export interface User {
  id: string
  email: string
  name: string
  role: UserRole
}

export type UserRole = 'admin' | 'user' | 'guest'

export interface ApiResponse<T> {
  data: T
  error: string | null
  success: boolean
}

// Component-specific types
export interface UserCardProps {
  user: User
  variant?: 'default' | 'compact'
}

export interface UserCardEmits {
  update: [user: User]
  delete: [id: string]
}
```

## Performance Optimization

### Component Memoization
```typescript
// Use defineAsyncComponent for code splitting
const HeavyComponent = defineAsyncComponent(() =>
  import('./HeavyComponent.vue')
)

// Use v-memo for expensive renders
<template>
  <div v-memo="[user.id, user.name]">
    <!-- Only re-renders when user.id or user.name changes -->
    {{ user.name }}
  </div>
</template>
```

### Computed vs Methods
```typescript
// ✅ GOOD: Use computed for calculations (cached)
const filteredItems = computed(() =>
  items.value.filter(i => i.isActive)
)

// ❌ AVOID: Methods recalculate on every access
const filteredItems = () =>
  items.value.filter(i => i.isActive)
```

---
*Last Updated: 2025*
*Vue Version: 3.x*
*Composition API with `<script setup>`*

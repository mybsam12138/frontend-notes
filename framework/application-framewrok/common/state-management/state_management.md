# 🗃️ State Management

## 1. What Is State Management?

**State management** is how an application stores, reads, and updates shared data that multiple components need access to.

In a small app, each component manages its own local state with `ref` or `reactive`.

But when many **unrelated components** need the same data, passing it through props becomes messy — this is when a **global store** is needed.

---

## 2. The Problem It Solves — Prop Drilling

Without state management, sharing data across distant components requires passing props through every level:

```
App (owns userInfo)
│
└── Layout
      └── Sidebar
            └── UserCard   ← needs userInfo
                             must receive it through Layout and Sidebar
                             even though they don't use it! 😱
```

This is called **prop drilling** — passing data through components that don't need it just to reach a deep descendant.

State management solves this by putting shared data in a **central store** that any component can access directly.

---

## 3. How It Works

```
ComponentA  ──┐
ComponentB  ──┼──► Global Store ◄──── any component can read / write
ComponentC  ──┘
```

Instead of:
```
Parent → Child → GrandChild → GreatGrandChild   (prop drilling 😱)
```

Any component goes directly to the store:
```
Any Component → Store   (direct access ✅)
```

---

## 4. Core Concepts

### 4.1 State
The actual data stored globally.

```js
const count = ref(0)
const userInfo = ref({ name: 'Alice', role: 'admin' })
```

### 4.2 Actions
Functions that update the state.

```js
function increment() { count.value++ }
function setUser(user) { userInfo.value = user }
```

### 4.3 Getters
Computed values derived from the state.

```js
const doubleCount = computed(() => count.value * 2)
const isAdmin = computed(() => userInfo.value.role === 'admin')
```

---

## 5. Pinia Example (Vue 3)

### Define the store

```js
// stores/useUserStore.js
import { defineStore } from 'pinia'
import { ref, computed } from 'vue'

export const useUserStore = defineStore('user', () => {
  // state
  const userInfo = ref(null)
  const isLoggedIn = ref(false)

  // getter
  const userName = computed(() => userInfo.value?.name ?? 'Guest')

  // actions
  function login(user) {
    userInfo.value = user
    isLoggedIn.value = true
  }

  function logout() {
    userInfo.value = null
    isLoggedIn.value = false
  }

  return { userInfo, isLoggedIn, userName, login, logout }
})
```

### Use it in any component

```vue
<!-- Header.vue -->
<script setup>
import { useUserStore } from '../stores/useUserStore'

const userStore = useUserStore()
</script>

<template>
  <div>Welcome, {{ userStore.userName }}</div>
  <button @click="userStore.logout">Logout</button>
</template>
```

```vue
<!-- Sidebar.vue — completely unrelated component -->
<script setup>
import { useUserStore } from '../stores/useUserStore'

const userStore = useUserStore()
</script>

<template>
  <div v-if="userStore.isLoggedIn">My Profile</div>
</template>
```

Both components access the **same store** — same data, always in sync. ✅

---

## 6. State Management vs Other Patterns

| Pattern | Scope | Use When |
|---|---|---|
| `ref` / `reactive` | Local — inside one component | Data only that component needs |
| Props | Parent → Child | Parent passes data down one level |
| Provide / Inject | Ancestor → Descendant | Skip multiple levels in one branch |
| State Management | Global — any component | Many unrelated components share data |

---

## 7. When To Use State Management

✅ Use a store when:
- Multiple **unrelated** components need the same data
- Data needs to **persist** across route navigation (shopping cart, user session)
- You need a **single source of truth** for important app data

❌ Don't use a store when:
- Only one component needs the data → use local `ref`
- Only parent and child need it → use props
- Only a component subtree needs it → use provide / inject

---

## 8. State Management Libraries

| Framework | Library | Notes |
|---|---|---|
| Vue 3 | **Pinia** | Official, recommended, Composition API style |
| Vue 2/3 | Vuex | Older, still used in legacy Vue projects |
| React | Redux | Most popular, more boilerplate |
| React | Zustand | Simpler, lightweight alternative |
| React | Jotai | Atomic state model |

---

## 9. Analogy

Think of state management like a **company database**:

- Every department (component) can query the database directly
- No need to pass a report through every manager just to reach one employee
- Everyone always reads the same up-to-date data
- Changes made by one department are immediately visible to all others

---

## 10. Key Takeaway

```
Local state   →  ref / reactive          (one component)
Shared state  →  props / provide/inject  (related components)
Global state  →  store (Pinia / Redux)   (any component, anywhere)
```

State management is essentially **provide/inject at app scale** — with extra features like devtools, persistence, and structured actions. 💡


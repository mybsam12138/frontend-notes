# 📡 Component Communication

> 🧑‍💻 Author: Yongbang Ma | Frontend Notes Series

---

## 🎯 Core Problem It Solves

> Components are **isolated by design** 🏝️
> Component Communication = mechanisms that let them **share data and events**! 🔗

---

## 🗺️ Full Communication Patterns

```
📡 Component Communication
│
├── 1️⃣ Props           Parent → Child        (data down)
├── 2️⃣ Emits           Child → Parent        (events up)
├── 3️⃣ Provide/Inject  Ancestor → Descendant (skip levels)
└── 4️⃣ State Management Any → Any            (global)
```

> Often summarised as **"props down, events up"** 🎯

---

## 1️⃣ Props — Parent → Child

Parent passes data **down** to child

```vue
<!-- Parent -->
<CardList :items="products" :loading="isLoading" />

<!-- Child — CardList.vue -->
const props = defineProps({
  items: Array,
  loading: Boolean
})
```

> Props are **one-way** — child can READ but never WRITE props directly! ✅
> If child needs to change parent data → use Emits! 🎯

---

## 2️⃣ Emits — Child → Parent

Child fires an event **up** — parent listens and reacts

```vue
<!-- Child -->
const emit = defineEmits(['item-selected'])
emit('item-selected', item)       // fire event up! 📢

<!-- Parent -->
<CardList @item-selected="handleSelect" />
function handleSelect(item) {
  selectedItem.value = item       // parent handles it ✅
}
```

---

## 3️⃣ Provide / Inject — Ancestor → Any Descendant

Skips multiple levels — no prop drilling needed! 🎯

```
App (provides: userInfo)
│
└── Layout
      └── Sidebar
            └── UserCard  ← injects userInfo directly! ✅
                            (no props through Layout or Sidebar!)
```

```vue
<!-- Ancestor -->
provide('userInfo', userInfo)

<!-- Deep Descendant -->
const userInfo = inject('userInfo')   // gets it directly! ✅
```

> Without provide/inject you'd pass props through **every level** —
> called **prop drilling** — messy and hard to maintain! 😱

---

## 4️⃣ State Management — Any → Any

When many unrelated components share the **same global state** 🌐

```
ComponentA ──┐
ComponentB ──┼──► Global Store (Pinia) ◄── any component reads/writes
ComponentC ──┘
```

```js
// store/counter.js
export const useCounterStore = defineStore('counter', () => {
  const count = ref(0)
  function increment() { count.value++ }
  return { count, increment }
})

// ANY component
const store = useCounterStore()
store.increment()                 // updates globally! 🌐
```

> State management = **provide/inject at app scale**
> with extra features like devtools, persistence, and actions! 🎯

---

## 🧠 When To Use Which

| Pattern | Use When |
|---|---|
| **Props** | Parent has data, child needs to display it |
| **Emits** | Child has an event, parent needs to react |
| **Provide/Inject** | Data needs to skip multiple component levels |
| **State Management** | Multiple unrelated components share the same state |

---

## 🔄 Props + Emits Together — Most Common Pattern

```
Parent owns state
      ↓
passes data DOWN via props
      ↓
Child displays it
      ↓
User interacts → child fires event UP via emit
      ↓
Parent updates state
      ↓
New value flows down again 🔄
```

> Parent always **owns** the state — child just displays and reports! ✅

---

## 🔑 Key Takeaway

> **Props** = data flows down 🔽
> **Emits** = events flow up 🔼
> **Provide/Inject** = skip levels, avoid prop drilling 🎯
> **State Management** = global shared state across any components 🌐

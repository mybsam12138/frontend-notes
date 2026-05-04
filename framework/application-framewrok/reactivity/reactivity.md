# ⚡ Reactivity in Frontend Frameworks

> 🧑‍💻 Author: Yongbang Ma | Frontend Notes Series

---

## 🎯 Core Definition

> **Reactivity = when state changes, everything that depends on it updates automatically** ✅
> You don't manually tell the UI to update — the framework **reacts** for you!

---

## ❌ Without Reactivity vs ✅ With Reactivity

```js
// ❌ Traditional DOM — manual sync
let count = 0
function increment() {
  count++
  document.getElementById('count').textContent = count  // must do this yourself!
}

// ✅ Vue Reactivity — automatic sync
const count = ref(0)
function increment() {
  count.value++
  // UI updates automatically — nothing else needed! 🎯
}
```

---

## 🔗 Three Core Parts of Reactivity

```
┌─────────────────────────────────────────┐
│           Reactivity System             │
│                                         │
│  1️⃣ Track      who depends on state     │
│  2️⃣ Detect     when state changes       │
│  3️⃣ Trigger    updates to dependents    │
│                                         │
└─────────────────────────────────────────┘
```

### 1️⃣ Track — Build the Dependency Map
When a component renders and **reads** a reactive value,
Vue silently records: "this component depends on this state" 📋

```
count is read by → ComponentA         ✅
count is read by → CardList           ✅
count is read by → computed: double   ✅
```

### 2️⃣ Detect — Intercept State Changes
```
Vue 3  → Proxy intercepts every read/write on reactive objects
Vue 2  → Object.defineProperty intercepts get/set
React  → setState / useState signals the framework explicitly
```

### 3️⃣ Trigger — Notify and Re-render
```
count changes
    ↓
notify ComponentA     → re-render 🔄
notify CardList       → re-render 🔄
notify doubleCount    → recompute 🔄
```

---

## 💡 Analogy — Excel Spreadsheet

```
Cell A1 = 10
Cell B1 = A1 * 2     ← depends on A1

You change A1 = 20
→ B1 automatically becomes 40! ✅
→ You never manually updated B1!
```

> Reactivity is exactly this —
> **dependent values automatically stay in sync with their source!** 🔗

---

## 🗺️ Full Reactivity Flow

```
State change (ref, reactive)
        ↓
Vue Proxy detects write 🔍
        ↓
Find which components depend on it
        ↓
Queue ONLY those component render jobs 📬
        ↓
Microtask flush — render queued components
        ↓
Diff new VNode subtree vs old 🔍
        ↓
Patch Real DOM minimally 🔧
        ↓
User sees updated UI 🖥️
```

---

## 🎯 Summary Table

| Concept | Meaning |
|---|---|
| **Reactivity** | State changes → UI updates automatically |
| **Track** | Record which components depend on which state |
| **Detect** | Proxy intercepts state writes |
| **Trigger** | Notify only affected components to re-render |

---

## 🔑 Key Takeaway

> Reactivity **eliminates manual DOM sync** 🎯
> State is the **single source of truth** — UI is just a reflection of it 🪞
> Vue is smart — only **affected components re-render**, not the whole tree ✅

# Component Lifecycle (with Vue Example)

## 🧠 1. Lifecycle Definition

Lifecycle refers to the different stages a component goes through during its existence in an application.

These stages allow developers to run logic at specific moments, such as initialization, rendering, updating, and destruction.

---

## 🔄 2. General Lifecycle Stages

Create → Mount → Update → Unmount

---

### 1️⃣ Create (Initialization)
- Component is created in memory
- Props and state are initialized

---

### 2️⃣ Mount (First Render)
- Component is inserted into the DOM
- UI becomes visible

---

### 3️⃣ Update (Re-render)
- Triggered when state or props change
- Framework updates the DOM

---

### 4️⃣ Unmount (Destroy)
- Component is removed from DOM
- Cleanup should be performed

---

## 🎯 3. Vue 3 Lifecycle Example

### Setup Phase

```js
export default {
  setup() {
    console.log("setup")
  }
}
```

---

### Mount Phase

```js
import { onMounted } from "vue"

onMounted(() => {
  console.log("Mounted")
})
```

---

### Update Phase

```js
import { onUpdated } from "vue"

onUpdated(() => {
  console.log("Updated")
})
```

---

### Unmount Phase

```js
import { onUnmounted } from "vue"

onUnmounted(() => {
  console.log("Unmounted")
})
```

---

## ⚠️ 4. Important Notes

- `setup()` runs before mount
- `onMounted` runs after DOM is ready
- `onUpdated` runs after DOM updates
- `onUnmounted` is used for cleanup

---

## 🎯 5. Common Use Cases


| Stage | Use Case |
|------|--------|
| Setup | Initialize state, define logic, prepare data structure |
| Mounted | Fetch data, access DOM, start side effects |
| Updated | Respond to reactive changes, sync with external state |
| Unmounted | Cleanup timers, listeners, subscriptions |
---

## 🧠 6. Key Takeaway

Lifecycle hooks allow developers to control when code runs during a component’s life, ensuring correct initialization, updates, and cleanup.

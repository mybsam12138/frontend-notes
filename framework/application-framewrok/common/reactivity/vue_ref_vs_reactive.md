# Vue — `ref()` vs `reactive()` Summary

Both `ref()` and `reactive()` make variables **reactive** — when the value changes, Vue automatically updates the UI.

---

## PART 1: `ref()`

Best for **primitive values** (string, number, boolean, null).

### Basic Usage
```javascript
import { ref } from 'vue'

const count   = ref(0)
const name    = ref("John")
const isActive = ref(true)
const data    = ref(null)     // common for "not loaded yet"
```

### Access & Update — use `.value` in script
```javascript
console.log(count.value)   // 0
count.value++              // UI updates! ✅
count.value = 10           // UI updates! ✅
```

### In Template — NO `.value` needed
```html
<template>
  <p>{{ count }}</p>       <!-- Vue auto-unwraps, no .value -->
  <p>{{ name }}</p>
</template>
```

### `ref()` with Object — works but needs `.value` first
```javascript
const user = ref({ name: "John", age: 25 })

// access
console.log(user.value.name)   // "John"

// update
user.value.name = "Jane"       // UI updates! ✅
user.value = { name: "Jane", age: 30 }  // replace whole object ✅
```

### Common Pitfall
```javascript
const count = ref(0)

console.log(count)        // ❌ gives ref object, NOT the value
console.log(count.value)  // ✅ gives 0
```

---

## PART 2: `reactive()`

Best for **objects and arrays** — no `.value` needed.

### Basic Usage
```javascript
import { reactive } from 'vue'

const user = reactive({
  name: "John",
  age: 25,
  address: {
    city: "LA"
  }
})

const items = reactive([1, 2, 3])
```

### Access & Update — direct, no `.value`
```javascript
// access
console.log(user.name)          // "John"
console.log(user.address.city)  // "LA"

// update
user.name = "Jane"              // UI updates! ✅
user.address.city = "NY"        // UI updates! ✅
items.push(4)                   // UI updates! ✅
```

### In Template — direct access
```html
<template>
  <p>{{ user.name }}</p>
  <p>{{ user.address.city }}</p>
</template>
```

### Common Pitfall — cannot replace whole object
```javascript
const user = reactive({ name: "John" })

// ❌ WRONG — loses reactivity!
user = { name: "Jane" }

// ✅ CORRECT — update property by property
user.name = "Jane"

// ✅ CORRECT — use Object.assign to replace all
Object.assign(user, { name: "Jane", age: 30 })
```

---

## PART 3: Side by Side Comparison

### Primitive value
```javascript
// ref ✅ correct
const count = ref(0)
count.value++

// reactive ❌ cannot use for primitives
const count = reactive(0)  // does NOT work!
```

### Object
```javascript
// ref — works but needs .value
const user = ref({ name: "John" })
user.value.name = "Jane"

// reactive ✅ cleaner for objects
const user = reactive({ name: "John" })
user.name = "Jane"
```

### Array
```javascript
// ref — works but needs .value
const items = ref([1, 2, 3])
items.value.push(4)

// reactive ✅ cleaner for arrays
const items = reactive([1, 2, 3])
items.push(4)
```

### Replace whole value
```javascript
// ref ✅ can replace whole value
const user = ref({ name: "John" })
user.value = { name: "Jane" }   // works!

// reactive ❌ cannot replace whole object
const user = reactive({ name: "John" })
user = { name: "Jane" }         // loses reactivity!
```

---

## PART 4: In Template

Both look the same in template:

```html
<script setup>
const count = ref(0)
const user  = reactive({ name: "John" })
</script>

<template>
  <p>{{ count }}</p>       <!-- ref: no .value needed in template -->
  <p>{{ user.name }}</p>   <!-- reactive: direct access -->
</template>
```

---

## PART 5: Summary Table

| Feature | `ref()` | `reactive()` |
|---|---|---|
| Best for | Primitives (string, number, boolean, null) | Objects & Arrays |
| Works with primitives | ✅ Yes | ❌ No |
| Works with objects | ✅ Yes (but needs `.value`) | ✅ Yes (cleaner) |
| Access in script | `x.value` | `x.property` directly |
| Access in template | `{{ x }}` (auto-unwrapped) | `{{ x.property }}` |
| Replace whole value | ✅ `x.value = newValue` | ❌ Loses reactivity |
| Update property | `x.value.prop = val` | `x.prop = val` |

---

## PART 6: Rule of Thumb

```javascript
// Single primitive value → ref()
const count    = ref(0)
const name     = ref("John")
const isActive = ref(false)
const data     = ref(null)      // not loaded yet

// Object or Array → reactive()
const user     = reactive({ name: "John", age: 25 })
const items    = reactive([1, 2, 3])
const form     = reactive({ email: "", password: "" })
```

---

## Key Rules to Remember

> - Both `ref()` and `reactive()` give **reactivity** — UI updates when value changes
> - `ref()` needs **`.value`** in script, but NOT in template
> - `reactive()` has **no `.value`** — access properties directly
> - `reactive()` **cannot** hold primitives (string, number, boolean)
> - `ref()` **can replace** the whole value — `reactive()` cannot
> - When in doubt → use **`ref()`** — it works for everything, just needs `.value`

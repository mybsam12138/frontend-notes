# Vue — Composition API vs Options API

Both are ways to write Vue components. They produce the same result — just different styles.

---

## PART 1: Basic Structure

### Options API (Vue 2 style, still works in Vue 3)
```vue
<script>
export default {
  data() {
    return {
      count: 0,
      name: "John"
    }
  },
  computed: {
    doubleCount() {
      return this.count * 2
    }
  },
  methods: {
    increment() {
      this.count++
    }
  },
  mounted() {
    console.log("component mounted!")
  }
}
</script>
```

### Composition API (Vue 3 style)
```vue
<script setup>
import { ref, computed, onMounted } from 'vue'

const count = ref(0)
const name  = ref("John")

const doubleCount = computed(() => count.value * 2)

function increment() {
  count.value++
}

onMounted(() => {
  console.log("component mounted!")
})
</script>
```

---

## PART 2: Data / State

### Options API
```vue
<script>
export default {
  data() {
    return {
      count: 0,
      user: { name: "John", age: 25 }
    }
  }
}
</script>
```

### Composition API
```vue
<script setup>
import { ref, reactive } from 'vue'

const count = ref(0)
const user  = reactive({ name: "John", age: 25 })
</script>
```

---

## PART 3: Methods

### Options API
```vue
<script>
export default {
  data() {
    return { count: 0 }
  },
  methods: {
    increment() {
      this.count++        // use "this" to access data
    },
    reset() {
      this.count = 0
    }
  }
}
</script>
```

### Composition API
```vue
<script setup>
import { ref } from 'vue'

const count = ref(0)

function increment() {
  count.value++           // no "this" needed!
}

function reset() {
  count.value = 0
}
</script>
```

---

## PART 4: Computed

### Options API
```vue
<script>
export default {
  data() {
    return { count: 0 }
  },
  computed: {
    doubleCount() {
      return this.count * 2
    }
  }
}
</script>
```

### Composition API
```vue
<script setup>
import { ref, computed } from 'vue'

const count = ref(0)
const doubleCount = computed(() => count.value * 2)
</script>
```

---

## PART 5: Lifecycle Hooks

### Options API
```vue
<script>
export default {
  beforeCreate()  { console.log("before create") },
  created()       { console.log("created") },
  beforeMount()   { console.log("before mount") },
  mounted()       { console.log("mounted") },
  beforeUpdate()  { console.log("before update") },
  updated()       { console.log("updated") },
  beforeUnmount() { console.log("before unmount") },
  unmounted()     { console.log("unmounted") }
}
</script>
```

### Composition API
```vue
<script setup>
import { onMounted, onUpdated, onUnmounted, onBeforeMount } from 'vue'

onBeforeMount(() => console.log("before mount"))
onMounted(()     => console.log("mounted"))
onUpdated(()     => console.log("updated"))
onUnmounted(()   => console.log("unmounted"))
</script>
```

---

## PART 6: Watch

### Options API
```vue
<script>
export default {
  data() {
    return { count: 0 }
  },
  watch: {
    count(newVal, oldVal) {
      console.log("count changed:", newVal, oldVal)
    }
  }
}
</script>
```

### Composition API
```vue
<script setup>
import { ref, watch } from 'vue'

const count = ref(0)

watch(count, (newVal, oldVal) => {
  console.log("count changed:", newVal, oldVal)
})
</script>
```

---

## PART 7: Props

### Options API
```vue
<script>
export default {
  props: {
    name: String,
    age: {
      type: Number,
      default: 18
    }
  },
  mounted() {
    console.log(this.name)   // access via this
  }
}
</script>
```

### Composition API
```vue
<script setup>
const props = defineProps({
  name: String,
  age: {
    type: Number,
    default: 18
  }
})

console.log(props.name)      // access via props object, no "this"
</script>
```

---

## PART 8: Reusable Logic

This is where Composition API really shines — logic can be extracted into **composables**.

### Options API — logic is stuck inside the component
```vue
<script>
export default {
  data() {
    return { count: 0 }
  },
  methods: {
    increment() { this.count++ },
    reset()     { this.count = 0 }
  }
  // ❌ hard to reuse this logic in another component
}
</script>
```

### Composition API — extract into composable, reuse anywhere
```javascript
// useCounter.js  ← reusable logic file
import { ref } from 'vue'

export function useCounter() {
  const count = ref(0)
  function increment() { count.value++ }
  function reset()     { count.value = 0 }
  return { count, increment, reset }
}
```

```vue
<!-- ComponentA.vue -->
<script setup>
import { useCounter } from './useCounter'
const { count, increment } = useCounter()   // ✅ reuse!
</script>

<!-- ComponentB.vue -->
<script setup>
import { useCounter } from './useCounter'
const { count, reset } = useCounter()       // ✅ reuse again!
</script>
```

---

## PART 9: Template — Same for Both!

```vue
<template>
  <div>
    <p>Count: {{ count }}</p>
    <p>Double: {{ doubleCount }}</p>
    <button @click="increment">Increment</button>
    <button @click="reset">Reset</button>
  </div>
</template>
```

> Template syntax is **identical** — the difference is only in `<script>`

---

## PART 10: Summary Table

| Feature | Options API | Composition API |
|---|---|---|
| Style | Object with fixed sections | Free-form functions |
| Data | `data()` returns object | `ref()` / `reactive()` |
| Methods | `methods: {}` | Plain functions |
| Computed | `computed: {}` | `computed(() => {})` |
| Lifecycle | `mounted() {}` | `onMounted(() => {})` |
| Watch | `watch: {}` | `watch(source, cb)` |
| Props | `props: {}` | `defineProps({})` |
| Access data | `this.count` | `count.value` (no `this`) |
| Reusable logic | ❌ Hard (mixins — messy) | ✅ Easy (composables) |
| TypeScript support | ⚠️ Limited | ✅ Excellent |
| Recommended for | Beginners / simple components | ✅ Modern Vue 3 projects |

---

## Key Rules to Remember

> - **Options API** organizes code by **type** (data, methods, computed) — easy to learn but hard to reuse logic
> - **Composition API** organizes code by **feature** — keeps related logic together and easy to reuse
> - Template is **identical** for both — difference is only in `<script>`
> - Composition API has **no `this`** — cleaner and works better with TypeScript
> - **Composables** (Composition API) = Vue's answer to reusable logic, similar to React hooks
> - Vue 3 recommends **Composition API** for new projects, but Options API is still fully supported

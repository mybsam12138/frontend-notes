# Vue — How Vue Framework Deals with .vue Files

---

## PART 1: What is a .vue File?

A `.vue` file is called a **Single File Component (SFC)** — it contains 3 blocks in one file:

```vue
<!-- UserCard.vue -->

<!-- 1. Template — the UI/HTML -->
<template>
  <div>
    <p>{{ count }}</p>
    <button @click="increment">Click me</button>
  </div>
</template>

<!-- 2. Script — the logic -->
<script setup>
import { ref } from 'vue'

const count = ref(0)
function increment() { count.value++ }
</script>

<!-- 3. Style — the CSS -->
<style scoped>
p { color: red; }
button { background: blue; }
</style>
```

> Browser does NOT understand `.vue` files — they must be **compiled into plain JavaScript** first.

---

## PART 2: Compilation — What Happens at Build Time

Vue compiler (via Vite or Webpack) transforms the `.vue` file into plain JavaScript:

```
UserCard.vue
┌─────────────────┐
│ <template>      │
│ <script setup>  │  →  Vue Compiler  →  plain JavaScript
│ <style>         │
└─────────────────┘
```

### What each block becomes:

| `.vue` block | After compilation |
|---|---|
| `<template>` | `render()` function that produces Virtual DOM |
| `<script setup>` | `setup()` function that returns reactive state |
| `<style>` | Injected into `<head>` as CSS, or extracted to `.css` file |

---

## PART 3: What the Compiled JS Looks Like

```javascript
// UserCard.vue → compiled into something like this:
import { ref } from 'vue'

export default {
  // <script setup> becomes setup()
  setup() {
    const count = ref(0)
    function increment() { count.value++ }
    return { count, increment }   // exposed to template
  },

  // <template> becomes render()
  render() {
    return h('div', [
      h('p', count.value),
      h('button', { onClick: increment }, 'Click me')
    ])
  }
}
```

> `.vue` file is just **syntactic sugar** — a developer-friendly format that compiles into plain JavaScript.

---

## PART 4: How Vue Handles CSS

### Normal `<style>` — global CSS
```vue
<style>
/* applies to ALL components — global scope */
p { color: red; }
</style>
```

### Scoped `<style scoped>` — only applies to this component
```vue
<style scoped>
/* only applies to THIS component */
p { color: red; }
</style>
```

Vue adds a **unique attribute** to elements to scope the CSS:
```html
<!-- compiled HTML -->
<p data-v-7ba5bd90>Hello</p>

<!-- compiled CSS -->
p[data-v-7ba5bd90] { color: red; }
```

### CSS Modules
```vue
<style module>
.title { color: red; }
</style>

<script setup>
import { useCssModule } from 'vue'
const css = useCssModule()
</script>

<template>
  <p :class="css.title">Hello</p>
</template>
```

### What happens to CSS at build time:

| Environment | What happens to CSS |
|---|---|
| Development | Injected into `<head>` as `<style>` tag dynamically |
| Production build | Extracted into separate `.css` file for better performance |

---

## PART 5: Full Flow — From .vue to Browser

```
① Developer writes .vue file
        ↓
② Vue Compiler (Vite/Webpack) compiles at build time
        ↓
③ .vue → plain JavaScript object + CSS
        ↓
④ Browser downloads and runs the JavaScript
        ↓
⑤ Vue runtime calls setup() → creates reactive state
        ↓
⑥ Vue runtime calls render() → produces Virtual DOM
        ↓
⑦ Virtual DOM compared with real DOM
        ↓
⑧ Only changed parts updated in real DOM
        ↓
⑨ User sees updated UI
```

---

## PART 6: What is Virtual DOM?

Virtual DOM is a **lightweight JavaScript copy** of the real DOM kept in memory.

```
Real DOM (browser)          Virtual DOM (memory)
┌─────────────────┐         ┌─────────────────┐
│ <div>           │         │ { tag: 'div',   │
│   <p>Hello</p>  │   ←──   │   children: [   │
│   <button>      │         │     { tag: 'p'  │
│ </div>          │         │   ]             │
└─────────────────┘         └─────────────────┘
```

### Why Virtual DOM?

| | Direct DOM update | Virtual DOM |
|---|---|---|
| Speed | ❌ Slow — updates everything | ✅ Fast — only updates what changed |
| Efficiency | ❌ Expensive operations | ✅ Compare in memory first |

### How it works:

```
State changes (count: 0 → 1)
        ↓
New Virtual DOM created
        ↓
Compare new vs old Virtual DOM (diffing)
        ↓
Only update the parts that changed in real DOM
```

---

## PART 7: Summary Table

| Part | Developer writes | Vue compiles to | Browser runs |
|---|---|---|---|
| `<template>` | HTML-like syntax | `render()` function | Virtual DOM → Real DOM |
| `<script setup>` | Composition API | `setup()` function | Reactive JS object |
| `<style scoped>` | Normal CSS | Scoped CSS with unique attribute | CSS in `<head>` or `.css` file |

---

## Key Rules to Remember

> - `.vue` file = **Single File Component** — template + script + style in one file
> - Browser **cannot** run `.vue` directly — must be compiled first
> - `<template>` → compiled to **`render()` function** → produces **Virtual DOM**
> - `<script setup>` → compiled to **`setup()` function** → returns reactive state
> - `<style scoped>` → Vue adds **unique attribute** to scope CSS to this component only
> - **Virtual DOM** = lightweight JS copy of real DOM — Vue only updates what actually changed
> - `.vue` file is just **syntactic sugar** — ultimately everything becomes plain JavaScript

# JavaScript — Export & Import Mechanism Summary

---

## PART 1: Why Export & Import?

JavaScript files are **isolated by default** — variables and functions in one file are NOT accessible in another file.

Export & Import is the mechanism to **share code between files**.

```
fileA.js  →  exports something
fileB.js  →  imports it from fileA.js
```

---

## PART 2: Two Types of Export

### 1. Named Export
```javascript
// math.js
export const PI = 3.14159

export function add(a, b) {
  return a + b
}

export function subtract(a, b) {
  return a - b
}
```

### 2. Default Export
```javascript
// greet.js
export default function greet(name) {
  return "Hello " + name
}

// or
const greet = (name) => "Hello " + name
export default greet
```

---

## PART 3: Two Types of Import

### Import Named Export — must use exact name with `{}`
```javascript
import { PI, add, subtract } from './math.js'

console.log(PI)          // 3.14159
console.log(add(1, 2))   // 3
```

### Import Default Export — any name, no `{}`
```javascript
import greet from './greet.js'         // name can be anything
import sayHello from './greet.js'      // also works!

console.log(greet("John"))             // "Hello John"
console.log(sayHello("John"))          // "Hello John"
```

### Import Both Named and Default
```javascript
// utils.js
export default function main() {}
export const helper = () => {}
export const PI = 3.14

// import both
import main, { helper, PI } from './utils.js'
```

### Import Everything as object
```javascript
import * as Math from './math.js'

console.log(Math.PI)           // 3.14159
console.log(Math.add(1, 2))    // 3
console.log(Math.subtract(5, 2)) // 3
```

### Rename on import
```javascript
import { add as sum, subtract as minus } from './math.js'

console.log(sum(1, 2))    // 3
console.log(minus(5, 2))  // 3
```

---

## PART 4: Named vs Default Export

| | Named Export | Default Export |
|---|---|---|
| Syntax | `export const x = ...` | `export default x` |
| Import syntax | `import { x } from '...'` | `import x from '...'` |
| Must match name? | ✅ Yes — exact name | ❌ No — any name works |
| How many per file? | ✅ Many | ⚠️ Only ONE per file |
| Best for | Utility functions, constants | Main class/component/function |

---

## PART 5: Export at Declaration vs Export List

### Export at declaration
```javascript
export const name = "John"
export function greet() {}
export class User {}
```

### Export list at bottom — same result
```javascript
const name = "John"
function greet() {}
class User {}

export { name, greet, User }   // export all at once at bottom
```

### Export list with rename
```javascript
const name = "John"
function greet() {}

export { name as userName, greet as sayHello }
```

---

## PART 6: Re-export — forward from another file

```javascript
// index.js — collect and re-export from multiple files
export { add, subtract } from './math.js'
export { greet } from './greet.js'
export { default as User } from './User.js'
```

```javascript
// now other files can import everything from one place
import { add, greet, User } from './index.js'  // clean!
```

---

## PART 7: Real World Examples

### Vue Component (default export)
```vue
<!-- UserCard.vue -->
<script>
export default {
  name: "UserCard",
  props: { name: String }
}
</script>
```

```javascript
// use in another file
import UserCard from './UserCard.vue'
```

### Vue Composable (named export)
```javascript
// useCounter.js
import { ref } from 'vue'

export function useCounter() {
  const count = ref(0)
  function increment() { count.value++ }
  return { count, increment }
}
```

```javascript
// use in component
import { useCounter } from './useCounter.js'
const { count, increment } = useCounter()
```

### Utility functions (named exports)
```javascript
// utils.js
export function formatDate(date) { return date.toLocaleDateString() }
export function formatCurrency(amount) { return "$" + amount.toFixed(2) }
export const MAX_ITEMS = 100
```

```javascript
// use in component
import { formatDate, formatCurrency, MAX_ITEMS } from './utils.js'
```

---

## PART 8: Common Mistakes

### ❌ Wrong — named export needs `{}`
```javascript
// math.js
export const add = (a, b) => a + b

// wrong import — no {}
import add from './math.js'    // ❌ undefined!

// correct
import { add } from './math.js'  // ✅
```

### ❌ Wrong — default export does NOT use `{}`
```javascript
// greet.js
export default function greet() {}

// wrong import — has {}
import { greet } from './greet.js'   // ❌ undefined!

// correct
import greet from './greet.js'       // ✅
```

### ❌ Wrong — only ONE default export per file
```javascript
export default function greet() {}
export default function bye() {}    // ❌ SyntaxError!
```

---

## PART 9: Summary Table

| Action | Syntax |
|---|---|
| Named export | `export const x = ...` |
| Default export | `export default x` |
| Export list | `export { a, b, c }` |
| Export with rename | `export { a as myA }` |
| Import named | `import { x } from '...'` |
| Import default | `import x from '...'` |
| Import both | `import x, { y, z } from '...'` |
| Import all | `import * as obj from '...'` |
| Import with rename | `import { x as myX } from '...'` |
| Re-export | `export { x } from '...'` |

---

## Key Rules to Remember

> - **Named export** → must import with exact name using `{}`
> - **Default export** → import with any name, no `{}`
> - Only **ONE default export** per file, but **unlimited named exports**
> - Use **named exports** for utility functions, constants, composables
> - Use **default export** for the main thing a file provides (component, class)
> - Use `import * as obj` to import everything as one object
> - Use `export { x } from '...'` to re-export from another file

# JavaScript — Return Types & How to Use Them

---

## 1. Return a Primitive Value

```javascript
function getAge() { return 25 }
function getName() { return "John" }
function isActive() { return true }
```

### How to use:
```javascript
const age = getAge()
console.log(age)       // 25
console.log(getAge())  // 25 — inline, one-time use
```

---

## 2. Return an Object

```javascript
function getUser() {
  return { name: "John", age: 25, city: "LA" }
}
```

### How to use — 3 ways:
```javascript
// 1. Assign then access
const user = getUser()
console.log(user.name)   // "John"
console.log(user.age)    // 25

// 2. Destructuring ← most common in modern JS
const { name, age, city } = getUser()
console.log(name)        // "John"

// 3. Inline — one-time use
console.log(getUser().name)  // "John"
```

---

## 3. Return a Function

```javascript
function makeGreeter() {
  return function(name) {
    return "Hello " + name
  }
}

// Arrow function style
function makeMultiplier(x) {
  return (n) => n * x
}
```

### How to use:
```javascript
// 1. Assign then call
const greet = makeGreeter()
greet("John")              // "Hello John"

// 2. Inline call — one-time use
makeGreeter()("John")      // "Hello John"

// 3. With arguments
const double = makeMultiplier(2)
double(5)                  // 10
double(10)                 // 20
```

---

## 4. Return Object with Functions

```javascript
function createCounter() {
  let count = 0                         // private variable
  return {
    increment() { count++ },
    decrement() { count-- },
    reset()     { count = 0 },
    getCount()  { return count }
  }
}
```

### How to use:
```javascript
const counter = createCounter()
counter.increment()
counter.increment()
counter.increment()
counter.decrement()
console.log(counter.getCount())  // 2

// Destructure functions out
const { increment, getCount } = createCounter()
increment()
console.log(getCount())          // 1
```

---

## 5. Real World — Vue Composable / React Custom Hook Style

```javascript
function useUser() {
  const name = "John"
  const age  = 25

  function updateName(newName) {
    console.log("updating to", newName)
  }

  return { name, age, updateName }
}
```

### How to use:
```javascript
const { name, age, updateName } = useUser()
console.log(name)        // "John"
updateName("Jane")       // "updating to Jane"
```

---

## Summary Table

| Return Type | Example | How to Receive | How to Use |
|---|---|---|---|
| Primitive | `return 25` | `const x = fn()` | Use directly `x` |
| String | `return "hello"` | `const s = fn()` | Use directly `s` |
| Boolean | `return true` | `const b = fn()` | Use in conditions `if (b)` |
| Object | `return { name, age }` | `const obj = fn()` | `obj.name` or `const { name } = fn()` |
| Array | `return [1, 2, 3]` | `const arr = fn()` | `arr[0]` or `const [a, b] = fn()` |
| Function | `return () => {}` | `const fn2 = fn()` | Call it `fn2()` |
| Object + Functions | `return { count, increment }` | `const obj = fn()` | `obj.increment()` |

---

## Key Rules to Remember

> - JavaScript can only **return ONE value** — use an object or array to return multiple values
> - Returned **objects** are best accessed via **destructuring** `const { x } = fn()`
> - Returned **arrays** are best accessed via **array destructuring** `const [a, b] = fn()`
> - Returned **functions** must be **called again** with `()`
> - Returning **object + functions** together is the foundation of **Vue composables** and **React hooks**

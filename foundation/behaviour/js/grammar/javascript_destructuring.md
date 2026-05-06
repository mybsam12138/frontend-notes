# JavaScript — Destructuring Summary

Destructuring is a shorthand syntax to **unpack values from objects or arrays into variables**.

---

## PART 1: Object Destructuring

### Basic
```javascript
const user = { name: "John", age: 25, city: "LA" }

// ❌ Old way
const name = user.name
const age  = user.age

// ✅ Destructuring
const { name, age } = user
console.log(name)  // "John"
console.log(age)   // 25
```

### Rename variable
```javascript
const user = { name: "John", age: 25 }

const { name: userName, age: userAge } = user
console.log(userName)  // "John"
console.log(userAge)   // 25
```

### Default value
```javascript
const user = { name: "John" }

const { name, age = 18 } = user  // age not in object, use default
console.log(age)  // 18
```

### Nested object
```javascript
const user = {
  name: "John",
  address: {
    city: "LA",
    zip: "90001"
  }
}

const { name, address: { city, zip } } = user
console.log(city)  // "LA"
console.log(zip)   // "90001"
```

### Rest — grab the remainder
```javascript
const user = { name: "John", age: 25, city: "LA", job: "dev" }

const { name, age, ...rest } = user
console.log(name)  // "John"
console.log(rest)  // { city: "LA", job: "dev" }
```

---

## PART 2: Array Destructuring

### Basic
```javascript
const colors = ["red", "green", "blue"]

// ❌ Old way
const first  = colors[0]
const second = colors[1]

// ✅ Destructuring
const [first, second, third] = colors
console.log(first)   // "red"
console.log(second)  // "green"
console.log(third)   // "blue"
```

### Skip elements
```javascript
const colors = ["red", "green", "blue"]

const [, , third] = colors   // skip first two
console.log(third)  // "blue"
```

### Default value
```javascript
const colors = ["red"]

const [first, second = "black"] = colors
console.log(second)  // "black" ← not in array, use default
```

### Rest — grab the remainder
```javascript
const numbers = [1, 2, 3, 4, 5]

const [first, second, ...rest] = numbers
console.log(first)   // 1
console.log(second)  // 2
console.log(rest)    // [3, 4, 5]
```

### Swap variables
```javascript
let a = 1
let b = 2

// ❌ Old way needs temp variable
let temp = a; a = b; b = temp

// ✅ Destructuring swap
[a, b] = [b, a]
console.log(a)  // 2
console.log(b)  // 1
```

---

## PART 3: Destructuring in Function Parameters

### Object parameter
```javascript
// ❌ Old way
function greet(user) {
  console.log("Hello " + user.name)
}

// ✅ Destructure directly in parameter
function greet({ name, age }) {
  console.log("Hello " + name + ", age " + age)
}

greet({ name: "John", age: 25 })  // "Hello John, age 25"
```

### With default values in parameter
```javascript
function greet({ name, age = 18 } = {}) {
  console.log(name + " is " + age)
}

greet({ name: "John" })        // "John is 18"
greet({ name: "Jane", age: 25 }) // "Jane is 25"
```

### Array parameter
```javascript
function getFirst([first, second]) {
  console.log(first, second)
}

getFirst(["red", "green", "blue"])  // "red" "green"
```

---

## PART 4: Destructuring from Function Return

### From object return
```javascript
function getUser() {
  return { name: "John", age: 25 }
}

const { name, age } = getUser()
console.log(name)  // "John"
```

### From array return
```javascript
function getCoords() {
  return [10, 20]
}

const [x, y] = getCoords()
console.log(x)  // 10
console.log(y)  // 20
```

### Real world — React useState
```javascript
// useState returns an array of [value, setter]
const [count, setCount] = useState(0)
//     ↑ value  ↑ function to update value
```

### Real world — Vue composable
```javascript
function useUser() {
  return { name: "John", updateName: () => {} }
}

const { name, updateName } = useUser()
```

---

## Summary Table

| Type | Syntax | Use case |
|---|---|---|
| Object basic | `const { a, b } = obj` | Unpack object properties |
| Object rename | `const { a: myA } = obj` | Rename while unpacking |
| Object default | `const { a = 10 } = obj` | Fallback if key missing |
| Object nested | `const { a: { b } } = obj` | Unpack nested object |
| Object rest | `const { a, ...rest } = obj` | Grab remaining properties |
| Array basic | `const [a, b] = arr` | Unpack array elements |
| Array skip | `const [, , c] = arr` | Skip elements |
| Array default | `const [a = 0] = arr` | Fallback if element missing |
| Array rest | `const [a, ...rest] = arr` | Grab remaining elements |
| Swap | `[a, b] = [b, a]` | Swap two variables |
| Function param | `function fn({ a, b })` | Unpack directly in parameter |
| Function return | `const { a } = fn()` | Unpack returned object/array |

---

## Key Rules to Remember

> - Object destructuring uses **`{}`** — variable names must **match the key names**
> - Array destructuring uses **`[]`** — variable names can be **anything**, order matters
> - Use **`=`** for default values when a key/element might be missing
> - Use **`...rest`** to collect remaining items
> - Destructuring can be used in **function parameters** and **function return values**
> - This is the foundation of **React hooks** (`useState`, `useEffect`) and **Vue composables**

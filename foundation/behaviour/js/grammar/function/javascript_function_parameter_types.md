# JavaScript — Function Parameter Types Summary

In JavaScript, **any type can be a parameter** — there are no restrictions.

---

## PART 1: All Parameter Types

```javascript
function fn(str)  {}  // string
function fn(num)  {}  // number
function fn(bool) {}  // boolean
function fn(n)    {}  // null
function fn(u)    {}  // undefined
function fn(obj)  {}  // object
function fn(arr)  {}  // array
function fn(fn2)  {}  // function
```

---

## PART 2: Examples

### String, Number, Boolean
```javascript
function greet(name, age, isActive) {
  console.log(name, age, isActive)
}

greet("John", 25, true)  // "John" 25 true
```

---

### Object
```javascript
// Normal
function greet(user) {
  console.log(user.name)
}
greet({ name: "John", age: 25 })  // "John"

// Destructure directly in parameter ← cleaner
function greet({ name, age }) {
  console.log(name, age)
}
greet({ name: "John", age: 25 })  // "John" 25
```

---

### Array
```javascript
// Normal
function sum(numbers) {
  return numbers.reduce((a, b) => a + b, 0)
}
sum([1, 2, 3, 4])  // 10

// Destructure directly in parameter
function first([a, b]) {
  console.log(a, b)
}
first([10, 20])  // 10 20
```

---

### Function (Callback)
```javascript
function run(callback) {
  callback()   // call the function passed in
}

run(() => console.log("Hello!"))   // "Hello!"

// Real world example — array forEach
[1, 2, 3].forEach((num) => {
  console.log(num)   // 1, 2, 3
})
```

> Passing a function as a parameter is called a **callback** — very common in JavaScript!

---

### Null / Undefined
```javascript
function check(value) {
  if (value === null)      console.log("got null!")
  if (value === undefined) console.log("got undefined!")
}

check(null)       // "got null!"
check(undefined)  // "got undefined!"
check()           // "got undefined!" ← no argument = undefined
```

---

### Default Parameter Value
```javascript
// If no argument passed, use default value
function greet(name = "Guest") {
  console.log("Hello " + name)
}

greet("John")  // "Hello John"
greet()        // "Hello Guest" ← uses default
```

---

### Rest Parameter — accept any number of arguments
```javascript
function sum(...numbers) {    // collects all args into an array
  return numbers.reduce((a, b) => a + b, 0)
}

sum(1, 2, 3)        // 6
sum(1, 2, 3, 4, 5)  // 15
```

---

## PART 3: Check Type Inside Function

Since JavaScript has no fixed parameter types, always check if needed:

```javascript
function process(value) {
  if (typeof value === "string")   console.log("got string:", value)
  if (typeof value === "number")   console.log("got number:", value)
  if (typeof value === "boolean")  console.log("got boolean:", value)
  if (typeof value === "function") value()        // call it!
  if (Array.isArray(value))        console.log("got array:", value)
  if (value === null)              console.log("got null")
  if (value === undefined)         console.log("got undefined")
  if (typeof value === "object" && value !== null && !Array.isArray(value))
                                   console.log("got object:", value)
}
```

---

## Summary Table

| Parameter Type | Example Call | Common Use |
|---|---|---|
| String | `fn("hello")` | Names, messages |
| Number | `fn(42)` | Calculations |
| Boolean | `fn(true)` | Flags, conditions |
| Object | `fn({ name: "John" })` | Pass multiple values together |
| Array | `fn([1, 2, 3])` | Lists of data |
| Function | `fn(() => {})` | Callbacks, event handlers |
| Null | `fn(null)` | Explicitly empty value |
| Undefined / no arg | `fn()` | No argument passed |
| Default value | `fn(name = "Guest")` | Fallback when no arg passed |
| Rest `...args` | `fn(1, 2, 3)` | Accept any number of arguments |

---

## Key Rules to Remember

> - JavaScript is **dynamically typed** — parameters have **no fixed type**
> - No argument passed = parameter is **`undefined`**
> - Use **default values** `fn(x = 0)` to handle missing arguments
> - Use **rest `...args`** to accept unlimited arguments
> - Passing a **function** as parameter = **callback pattern**
> - **Object/Array** parameters can be **destructured directly** in the parameter list
> - Always use **`typeof`** or **`Array.isArray()`** to check types inside the function

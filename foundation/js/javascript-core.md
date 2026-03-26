# JavaScript Core (Structured Summary)

## 1. What is JavaScript

JavaScript is a **programming language** used to add **behavior and interactivity** to web pages.

- Runs in browser (and Node.js)
- Works with HTML (structure) and CSS (style)

---

## 2. Basic Syntax

```js
let name = "Sam";
const age = 30;

function greet() {
  console.log("Hello");
}
```

- `let` → variable (changeable)
- `const` → constant (not reassignable)

---

## 3. Data Types

### Primitive

- string
- number
- boolean
- null
- undefined
- symbol
- bigint

### Reference

- object
- array
- function

---

## 4. Functions

```js
function add(a, b) {
  return a + b;
}
```

Arrow function:

```js
const add = (a, b) => a + b;
```

---

## 5. Scope

- Global scope
- Function scope
- Block scope (`let`, `const`)

```js
if (true) {
  let x = 10;
}
```

---

## 6. Closure

A function remembers variables from its outer scope.

```js
function outer() {
  let count = 0;
  return function () {
    count++;
    return count;
  };
}
```

---

## 7. This Keyword

`this` depends on how function is called.

- global → window (browser)
- object method → object
- arrow function → no own this

---

## 8. Object

```js
const user = {
  name: "Sam",
  age: 30,
};
```

Access:

```js
user.name
user["age"]
```

---

## 9. Array

```js
const arr = [1, 2, 3];
```

Common methods:

- map
- filter
- reduce
- forEach

---

## 10. DOM Basics

```js
document.getElementById("app");
document.querySelector(".box");
```

Modify:

```js
element.innerText = "Hello";
```

---

## 11. Event Handling

```js
button.addEventListener("click", () => {
  console.log("clicked");
});
```

---

## 12. Async JavaScript

### Callback

```js
setTimeout(() => {
  console.log("done");
}, 1000);
```

### Promise

```js
fetch(url).then(res => res.json());
```

### Async/Await

```js
async function getData() {
  const res = await fetch(url);
}
```

---

## 13. Event Loop (Core Idea)

JavaScript is **single-threaded**.

- Call stack → executes code
- Web APIs → async tasks
- Task queue → waits
- Event loop → pushes tasks to stack

---

## 14. Hoisting

Variables and functions are moved to top.

```js
console.log(a); // undefined
var a = 10;
```

---

## 15. Prototype

Objects inherit from prototype.

```js
obj.__proto__
```

---

## 16. ES6+ Features

- let / const
- arrow function
- template string
- destructuring
- spread/rest
- modules

---

## 17. Error Handling

```js
try {
  // code
} catch (e) {
  console.log(e);
}
```

---

## 18. Modules

```js
export const a = 1;
import { a } from "./file.js";
```

---

## 19. Best Practices

- use `const` by default
- avoid global variables
- use meaningful names
- handle errors properly

---

## 20. One-line Summary

👉 JavaScript controls **logic, behavior, and interaction** of web applications.

---

## 21. Next Topics

- Event Loop deep dive
- Promise vs async/await
- Closure deep dive
- Browser rendering
- Framework (Vue/React)

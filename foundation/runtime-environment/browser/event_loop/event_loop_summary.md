# JavaScript Event Loop, Microtasks, Macrotasks & Async Model

## 1. Event Loop Overview

JavaScript is single-threaded. The Event Loop is a scheduling mechanism that allows async behavior.

Core idea:

- Execute synchronous code first
- Then execute microtasks
- Then execute one macrotask
- Repeat

---

## 2. Microtask vs Macrotask

### Microtasks (High Priority)

Examples:
- Promise.then / catch / finally
- queueMicrotask
- MutationObserver

Characteristics:
- Executed immediately after current task
- All microtasks are executed before moving on
- Can block rendering if too many

---

### Macrotasks (Lower Priority)

Examples:
- setTimeout / setInterval
- DOM events (click, input)
- I/O

Characteristics:
- Executed in next event loop cycle
- Only one macrotask runs per cycle

---

## 3. Execution Order

1. Run synchronous code (call stack)
2. Run all microtasks
3. Run one macrotask
4. Browser may render
5. Repeat

---

## 4. Example

```js
console.log("1");

setTimeout(() => console.log("2"), 0);

Promise.resolve().then(() => console.log("3"));

console.log("4");
```

Output:

1
4
3
2

---

## 5. Async Implementation in Browser

JavaScript itself is single-threaded, but async is achieved via browser capabilities.

### Components:

- JS Main Thread (single-threaded)
- Web APIs (multi-threaded, browser)
- Task Queues (microtask & macrotask)
- Event Loop (scheduler)

---

## 6. How Async Works

1. JS calls async API (setTimeout, fetch)
2. Browser handles it in background thread
3. When done, callback is placed into queue
4. Event Loop executes it when call stack is empty

---

## 7. Example Flow (API)

fetch("/api")
  ↓
Browser sends request (network thread)
  ↓
Response received
  ↓
Promise resolved
  ↓
.then added to microtask queue
  ↓
Event Loop executes it

---

## 8. Tech Stack Involved

### JavaScript Engine
- Executes JS code
- Manages call stack

### Web APIs (Browser)
- Timer (setTimeout)
- Network (fetch)
- DOM events

### Event Loop
- Coordinates execution

### Task Queues
- Microtask Queue
- Macrotask Queue

### Rendering Engine
- Layout
- Paint
- Compositing

---

## 9. Key Takeaways

- JS is single-threaded
- Async comes from browser multi-threading
- Microtasks run before macrotasks
- Promise uses microtask
- setTimeout uses macrotask

---

## 10. Summary

JS = single thread + event loop + browser async support

Microtask = run ASAP (after current task)
Macrotask = run later (next cycle)

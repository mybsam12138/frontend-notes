# DOM, BOM, V8, Node.js — Relationship Summary

## 1. Core Concepts

### JavaScript
- A programming language
- Defines syntax, logic, objects, async behavior
- Does NOT include DOM or BOM

---

### V8 (JavaScript Engine)
- Executes JavaScript code
- Performs parsing, JIT compilation, execution, and garbage collection
- Does NOT provide APIs like DOM, BOM, or file system

---

### DOM (Document Object Model)
- API for manipulating HTML structure
- Example:
  ```js
  document.getElementById("app")
  ```
- Provided by the browser environment, not JavaScript or V8

---

### BOM (Browser Object Model)
- APIs to interact with browser itself
- Examples:
  ```js
  window
  location.href
  history.back()
  ```
- Also provided by the browser environment

---

### Node.js
- Runtime environment for JavaScript outside the browser
- Built on top of V8
- Provides server-side APIs:
  - fs (file system)
  - http
  - process
- Does NOT provide DOM or BOM

---

## 2. Relationship Overview

JavaScript (language)
        ↓
V8 (engine executes JS)
        ↓
Runtime Environment
   ├── Browser
   │     ├── DOM (document)
   │     ├── BOM (window)
   │     └── Web APIs (fetch, setTimeout)
   │
   └── Node.js
         ├── fs / http / process APIs
         └── NO DOM / NO BOM

---

## 3. Key Differences

| Component | Role | Provides DOM/BOM |
|----------|------|------------------|
| JavaScript | Language | ❌ No |
| V8 | JS Engine | ❌ No |
| Browser | Runtime Environment | ✅ Yes |
| Node.js | Runtime Environment | ❌ No |

---

## 4. Important Behaviors

### Browser
- Can manipulate UI (HTML/CSS)
- Has document and window

### Node.js
- Cannot access document or window
- Used for backend, scripts, SSR

---

## 5. Common Errors Explained

Example:
```js
window.location.href
```

- Works in browser
- Fails in Node.js:
  ReferenceError: window is not defined

---

## 6. Simulating DOM in Node.js

Tools:
- jsdom
- happy-dom

Allow:
- Partial DOM simulation
- Testing frontend logic

But:
- Not real rendering
- Not a real browser

---

## 7. Key Takeaway

JavaScript defines the language, V8 executes it, and the runtime environment (browser or Node.js) provides the APIs.

- DOM & BOM → Browser only
- Node.js → Server-side APIs only
- V8 → Executes JavaScript only

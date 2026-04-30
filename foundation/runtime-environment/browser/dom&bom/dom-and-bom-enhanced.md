# DOM & BOM (Frontend Core Mechanism)

## 1. What is DOM

DOM = Document Object Model

```text
HTML → parsed → DOM Tree (JavaScript object structure)
```

---

## 2. What is BOM

BOM = Browser Object Model

```text
Represents browser environment (window)
```

---

## 3. IMPORTANT: Where DOM & BOM come from

👉 DOM and BOM are NOT part of JavaScript language

```text
They are provided by the BROWSER
```

---

## 4. Browser Architecture (Very Important)

```text
Browser
 ├── JS Engine (V8)
 ├── DOM API
 └── BOM API
```

---

## 5. Why Frontend Needs Browser

Frontend code usually uses:

```js
document.querySelector("div")
location.href
navigator.userAgent
```

👉 These belong to:

```text
✔ DOM (document)
✔ BOM (window, location, navigator)
```

---

### So:

```text
Frontend must run in browser
because only browser provides DOM & BOM
```

---

## 6. Why Node.js Cannot Run Frontend Directly

Node.js only has:

```text
✔ JavaScript engine
❌ No DOM
❌ No BOM
```

---

### Example

```js
document.querySelector("div"); // ❌ Error in Node.js
```

---

## 7. Then What is Node.js Used For?

Node.js is used for:

```text
✔ Build tools (Vite, Webpack)
✔ Backend server
✔ CLI tools
✔ SSR (partial frontend rendering)
```

---

## 8. DOM vs BOM Summary

| Feature | DOM | BOM |
|--------|-----|-----|
| Provided by | Browser | Browser |
| Purpose | Page structure | Browser environment |
| Example | document | window, location |

---

## 9. Mental Model (Very Important)

```text
JavaScript = language
Browser     = environment

DOM = page
BOM = browser
```

---

## 10. One-line Summary

👉 DOM & BOM are browser APIs, not part of JS  
👉 Frontend needs browser to run  
👉 Node.js is for tools and backend, not UI execution

# DOM & BOM (Frontend Core Mechanism)

## 1. What is DOM

DOM = Document Object Model

```text
HTML → parsed → DOM Tree (JavaScript object structure)
```

Example:

```html
<div id="app">
  <p>Hello</p>
</div>
```

DOM:

```text
document
 └── div#app
      └── p
```

---

## 2. DOM Features

- Tree structure
- Each node is an object
- Can be modified by JavaScript

---

## 3. Common DOM Operations

### Select elements

```js
document.getElementById("app")
document.querySelector(".class")
document.querySelectorAll("p")
```

---

### Modify content

```js
el.textContent = "Hello"
el.innerHTML = "<b>Hello</b>"
```

---

### Modify style

```js
el.style.color = "red"
el.classList.add("active")
```

---

### Create / delete

```js
const div = document.createElement("div")
parent.appendChild(div)
parent.removeChild(div)
```

---

## 4. Event System

```js
button.addEventListener("click", () => {})
```

Event flow:

```text
capture → target → bubble
```

---

## 5. What is BOM

BOM = Browser Object Model

```text
Represents browser environment (window)
```

---

## 6. Core BOM Objects

### window

```js
window.innerWidth
window.setTimeout()
```

---

### location

```js
location.href
location.reload()
```

---

### navigator

```js
navigator.userAgent
```

---

### history

```js
history.back()
history.forward()
```

---

## 7. DOM vs BOM

| DOM | BOM |
|-----|-----|
| page content | browser environment |
| document | window |
| HTML structure | browser APIs |

---

## 8. Rendering Relation

```text
HTML → DOM
CSS → CSSOM
→ Render Tree → Layout → Paint
```

---

## 9. One-line Summary

👉 DOM = page structure (HTML → objects)  
👉 BOM = browser environment (window, location, history)

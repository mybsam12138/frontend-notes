# ⏱️ What Is a "Tick" in Browser Runtime?

> 🧑‍💻 Author: Yongbang Ma | Frontend Notes Series

---

## 🎯 Core Definition

> **Tick = one full cycle of the Browser Event Loop**
> It is a **Browser Runtime concept** — not a JavaScript language concept!

---

## 🏗️ Who Owns What

| Concept | Belongs To |
|---|---|
| Syntax, Promise, async/await | 🟨 JavaScript language (ECMAScript) |
| Event Loop, Tick, Task Queues | 🟦 Browser runtime |
| `nextTick()` | 🟩 Vue — built on top of Browser runtime |

---

## 🔄 What One Tick Looks Like

```
┌─────────────────────────────────────┐
│              ONE TICK               │
│                                     │
│  1️⃣ Pick ONE macrotask from queue   │
│     → run it on Call Stack          │
│                                     │
│  2️⃣ Drain ALL microtasks            │
│     → run every Promise.then etc.   │
│                                     │
│  3️⃣ Browser repaint (if needed) 🎨  │
│                                     │
└─────────────────────────────────────┘
         🔄 next tick starts here
```

> Every tick is **opened by a macrotask** — there is no JS execution without one! 🚪

---

## 📌 Macrotask vs Microtask

| | Type | When It Runs | Examples |
|---|---|---|---|
| **Macrotask** | 🚪 Opens a tick | Start of each tick | script load, setTimeout, DOM events, fetch callback |
| **Microtask** | 🧹 Closes a tick | End of current tick, before repaint | Promise.then, queueMicrotask |

> **Every JS code that runs is originally triggered by a macrotask!**
> Even your app's initial boot (`main.js` loading) is itself one macrotask! 🎯

---

## 💡 Concrete Example

```js
console.log('A')            // macrotask — current tick

setTimeout(() => {
  console.log('B')          // macrotask — NEW tick (future)
}, 0)

Promise.resolve().then(() => {
  console.log('C')          // microtask — end of current tick
})

console.log('D')            // macrotask — current tick

// Output:
// A  ← current tick
// D  ← current tick
// C  ← end of current tick (microtask)
// B  ← next tick
```

---

## 🔄 Multiple Ticks Flow

```
Macrotask: script loads (main.js)   🚪 tick 1
      ↓ microtasks drain
      ↓ browser repaint 🎨
Macrotask: user clicks button       🚪 tick 2
      ↓ microtasks drain
      ↓ browser repaint 🎨
Macrotask: setTimeout fires         🚪 tick 3
      ↓ ... forever 🔄
```

---

## 🔑 Key Takeaway

> **Macrotask** = the trigger of every tick 🚪 — opens it
> **Microtask** = cleanup at the end of that tick 🧹 — closes it
> **Tick** = one full loop cycle owned by the **Browser runtime**, not JS itself

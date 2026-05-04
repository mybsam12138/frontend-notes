# 📌 Macrotask vs Microtask — Examples

> 🧑‍💻 Author: Yongbang Ma | Frontend Notes Series

---

## 🎯 Core Definition

> **Macrotask** = task pushed to the queue by **Browser Web API** — opens a new tick 🚪
> **Microtask** = task pushed by **JS Promise mechanism** — drains at end of current tick 🧹

---

## 📋 Macrotask Examples

| Macrotask | Triggered By |
|---|---|
| Script load | Browser loads your JS file — first tick of the app! |
| `setTimeout` callback | Timer Web API fires after delay |
| `setInterval` callback | Timer Web API fires repeatedly — every fire = new macrotask! |
| DOM event callbacks | User clicks, keydown, mousemove, input, focus etc. |
| Network callbacks | `fetch` response, XHR `onload` |
| `MessageChannel` | `port.onmessage` callback |
| `requestAnimationFrame` | Fires once before every browser repaint |

---

## 📋 Microtask Examples

| Microtask | Triggered By |
|---|---|
| `Promise.then` / `.catch` / `.finally` | JS Promise resolution |
| `async/await` (after await) | Syntactic sugar over Promise |
| `queueMicrotask()` | Explicit microtask scheduling |
| `MutationObserver` | DOM mutation observation callback |

---

## 🔄 Execution Order — One Tick

```
┌─────────────────────────────────────┐
│              ONE TICK               │
│                                     │
│  1️⃣ ONE macrotask runs              │
│     → your sync JS code here        │
│                                     │
│  2️⃣ ALL microtasks drain            │
│     → every Promise.then etc.       │
│                                     │
│  3️⃣ Browser repaint (if needed) 🎨  │
│                                     │
└─────────────────────────────────────┘
         🔄 next tick starts here
```

---

## 💡 Concrete Example

```js
console.log('A')              // sync — current macrotask

setTimeout(() => {
  console.log('B')            // macrotask — NEW tick
}, 0)

Promise.resolve().then(() => {
  console.log('C')            // microtask — end of current tick
})

console.log('D')              // sync — current macrotask

// Output:
// A  ← current tick (sync)
// D  ← current tick (sync)
// C  ← end of current tick (microtask)
// B  ← next tick (macrotask)
```

---

## 🗺️ Where They Come From

```
🟨 JS language   → produces Microtasks only  (Promise, async/await)
🟦 Browser runtime → produces Macrotasks     (timers, events, network)
```

> JS language itself **never produces macrotasks** —
> only the Browser Web APIs do! 🟦

---

## 🎯 Summary Table

| | Macrotask | Microtask |
|---|---|---|
| Owned by | 🟦 Browser runtime | 🟨 JS language |
| When runs | Opens a new tick 🚪 | End of current tick 🧹 |
| How many per tick | ONE | ALL of them |
| Examples | setTimeout, click, fetch | Promise.then, await |
| Vue uses it for | — | Flushing render queue (nextTick) |

---

## 🔑 Key Takeaway

> **Macrotask** = Browser Web API callback = opens a new tick 🚪
> **Microtask** = JS Promise mechanism = closes current tick 🧹
> Microtasks always run **before** the next macrotask —
> this is why Vue's `nextTick` can safely read updated DOM! ✅

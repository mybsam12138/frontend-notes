# ⚡ Why Virtual DOM Is Faster Than Traditional DOM Manipulation

> 📅 Summary of key concepts discussed — Frontend Notes Series
> 🧑‍💻 Author: Yongbang Ma

---

## 🎯 Core Reason In One Line

> Virtual DOM **batches and minimises** Real DOM touches —
> Traditional DOM manipulation **touches the Real DOM immediately** on every change.

---

## 🐢 Why Direct DOM Manipulation Is Slow

### The Browser Render Pipeline

Every time you touch the Real DOM, the browser may trigger an expensive pipeline:

```
JS runs → Style calc → Layout (Reflow) → Paint → Composite → Screen 🖥️
                            💸💸            💸         💸
```

| Step | What Happens | Cost |
|---|---|---|
| **Style calc** | Figure out which CSS rules apply | Medium |
| **Layout / Reflow** | Recalculate size and position of every element | 💸 Expensive! |
| **Paint** | Fill in pixels — colors, borders, shadows | 💸 Expensive! |
| **Composite** | Layer everything and send to GPU | Medium |

> **Reflow is the killer** 😱 — changing one element's size or position can force the browser
> to recalculate layout for the **entire page**!

### ❌ The Classic Bad Pattern

```js
// 3 separate Real DOM touches — pipeline may run 3 times! 😱
element.style.width = '100px'    // 💸 triggers reflow + repaint
element.style.color = 'red'      // 💸 triggers repaint
element.textContent = 'Hello'    // 💸 triggers reflow + repaint
```

---

## ✅ How Virtual DOM Solves This

### Key Idea — Batch Updates

Virtual DOM does **not** avoid touching the Real DOM.
It **delays and batches** all Real DOM changes so the browser pipeline runs **as few times as possible**.

```
❌ Traditional DOM
─────────────────────────────────────────
Change 1 → Real DOM touch → reflow → repaint   🔄
Change 2 → Real DOM touch → reflow → repaint   🔄
Change 3 → Real DOM touch → reflow → repaint   🔄
= Pipeline runs 3x 😱

✅ Virtual DOM (Vue / React)
─────────────────────────────────────────
Change 1 → VNode update (just a JS object 💨)
Change 2 → VNode update (just a JS object 💨)
Change 3 → VNode update (just a JS object 💨)
        ↓
   Diff all changes together
        ↓
ONE batch Real DOM patch → reflow → repaint
= Pipeline runs 1x 🚀
```

---

## 🔄 The Full Virtual DOM Flow

```
State changes (ref, reactive)
        ↓
Vue Proxy intercepts change 🔍
        ↓
Scheduler queues a render job 📬
(multiple changes in same tick → only ONE job queued!)
        ↓
── sync JS continues, more changes batched ──
        ↓
Call stack empties ✅
        ↓
Microtask flush (Promise.then) ⚡
        ↓
Render function runs → new VNode tree built 🆕
        ↓
Diff: new VNode tree vs old VNode tree 🔍
        ↓
Patch: ONLY changed nodes updated in Real DOM 🔧
        ↓
Browser reflow → repaint → composite 🎨
        ↓
User sees updated UI 🖥️
```

---

## ⏰ When Does the Diff Happen?

Vue diffs **after all synchronous JS in the current tick finishes** — in the **microtask phase**.

```
Phase 1️⃣ — SYNC (your code runs)
──────────────────────────────────────────
ref.value changes      → Vue queues render job 📬
more changes           → already queued, ignored ✋
your component methods → all sync JS runs here

Phase 2️⃣ — MICROTASK (Vue's diff phase) ← DIFF HAPPENS HERE
──────────────────────────────────────────
render function runs   → new VNode tree built 🆕
diff algorithm runs    → old vs new VNode compared 🔍
patch runs             → Real DOM minimally updated ✅

Phase 3️⃣ — BROWSER REPAINT
──────────────────────────────────────────
browser sees Real DOM changed 🎨
user sees new UI 🖥️
```

> Vue uses `Promise.then` (microtask) — so it runs **after your JS finishes**
> but **before the browser repaints** — no flickering! ✅

---

## 🧠 What Is a VNode?

Virtual DOM nodes (VNodes) are **plain JavaScript objects** — cheap to create and throw away!

```js
const vnode = {
  type: 'div',              // 🏷️ what element
  props: {
    id: 'app',
    class: 'container',
    onClick: handleClick,   // 🎯 events live here too
  },
  children: [               // 👶 nested VNodes (the tree!)
    {
      type: 'p',
      props: { class: 'title' },
      children: 'Hello World',
      key: null,
      el: null,
    }
  ],
  key: 'item-1',            // 🔑 for efficient list diffing
  el: null,                 // 🖇️ pointer to real DOM node (set after mount)
  patchFlag: 1,             // ⚡ Vue 3 compiler hint — what CAN change
}
```

### Key Properties

| Property | Purpose |
|---|---|
| `type` | Element tag or component |
| `props` | Attributes, styles, event listeners |
| `children` | Nested VNodes — forms the tree 🌳 |
| `key` | Helps diff algorithm track list items 🔑 |
| `el` | Pointer to the real DOM twin after mount 🖇️ |
| `patchFlag` | Vue 3 compiler optimization — marks what's dynamic ⚡ |

---

## 🌳 One Tree — Virtual and Real

### Virtual DOM Tree

```
VNode (div#app)
  ├── VNode (nav)
  ├── VNode (main)
  │     └── VNode (h1) → children: "Hello"
  └── VNode (footer)
```

### Real DOM Tree (mirrors it 1-to-1)

```
document
└── <html>
      └── <body>
            └── <div id="app">     ← Vue mounts here
                  ├── <nav>
                  ├── <main>
                  │     └── <h1>Hello</h1>
                  └── <footer>
```

> `vnode.el` is the **bridge** — it points from each VNode to its Real DOM twin!

---

## 🏗️ SPA — Only One Tree Each

| | Count | Notes |
|---|---|---|
| `index.html` | 1 file | Never reloads in SPA |
| Real DOM tree | 1 tree | Rooted at `document` |
| Virtual DOM tree | 1 tree | Rooted at `<div id="app">` VNode |
| VNode objects | Thousands | Each node in the tree |

> Page navigation in SPA = only the `<RouterView>` **subtree** gets swapped!
> The `document`, `<html>`, `<head>`, `<body>` — never touched! ✅

---

## 💡 Helpful Analogy — Blueprints vs Building

```
VNode Tree   =  Blueprint  (paper, cheap to redraw ✏️)
Real DOM     =  Building   (expensive to rebuild 🏢)

When design changes:
→ Redraw blueprint (new VNode tree)       — cheap!
→ Compare with old blueprint (diff)       — cheap!
→ Send workers to change only what's diff (patch) — minimal!
→ Never rebuild the whole building!       🚫
```

---

## 🎯 Summary Table

| Factor | Traditional DOM | Virtual DOM |
|---|---|---|
| When does Real DOM update? | Immediately on every change | After all sync changes batched |
| Browser pipeline runs | Once per change 😱 | Once per batch ✅ |
| JS object created? | No | Yes — VNode (cheap!) |
| Diff step? | No | Yes — finds minimum changes |
| Risk of reflow storm? | High 💸 | Low ✅ |
| `nextTick` needed? | No | Yes — to read updated DOM |

---

## 🔑 Key Takeaway

> Virtual DOM is not magic — it's a **smart batching and minimisation strategy**.
> The win comes from: **fewer Real DOM touches → fewer reflows → fewer browser pipeline runs**.

---

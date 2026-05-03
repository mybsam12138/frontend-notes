# 🎨 Reflow vs Repaint

> 🧑‍💻 Author: Yongbang Ma | Frontend Notes Series

---

## 🎯 One Line Each

> **Reflow** = recalculate **geometry** — size, position, layout 📐
> **Repaint** = redraw **pixels** — colors, shadows, borders 🎨

---

## 🧠 What Triggers Each

### 📐 Reflow — Layout Changes
Anything that affects **size or position**:
```
width, height, margin, padding
top, left, position
font-size, line-height
adding / removing DOM elements
```

### 🎨 Repaint — Visual Changes
Anything that affects **appearance only**, no size/position change:
```
color, background-color
border-color, outline
box-shadow
visibility
```

---

## 🔗 Critical Relationship

```
Reflow   → always triggers Repaint after it   💸💸
Repaint  → does NOT trigger Reflow            💸
```

> Reflow is more expensive — it recalculates layout **then** repaints!
> Repaint alone skips layout calculation — cheaper! ✅

---

## 💡 Visual Analogy

```
Reflow   = moving furniture in a room 🛋️
           → measure everything again
           → recalculate where everything fits
           → then redecorate affected area

Repaint  = repainting the walls 🖌️
           → no measuring needed
           → just apply new color
```

---

## 💥 Cost Comparison

| | Triggers Layout Calc? | Triggers Pixel Redraw? | Cost |
|---|---|---|---|
| **Reflow** | ✅ Yes | ✅ Yes (after) | 💸💸 Expensive |
| **Repaint** | ❌ No | ✅ Yes | 💸 Medium |
| **Composite only** | ❌ No | ❌ No | ✅ Cheap |

> **Composite only** = properties like `transform`, `opacity` —
> skip both reflow and repaint, handled by GPU directly! 🚀
> This is why smooth animations use `transform` instead of `top/left`! 🎯

---

## 🔄 Relation to Traditional DOM vs Virtual DOM

```
Traditional DOM
──────────────────────────────────────────
Every DOM write → reflow triggered immediately 💸
Read layout after write → always gets fresh value ✅
Cost → pays reflow on every single change 😱

Virtual DOM
──────────────────────────────────────────
State changes → batched in VNode (no reflow yet 💨)
Reflow → triggered once after minimum DOM patch ✅
Read layout after state change → must await nextTick() ⏰
```

---

## 🔑 Key Takeaway

> **Reflow** = expensive — geometry changed, recalculate layout + repaint 📐💸💸
> **Repaint** = medium — only pixels changed, skip layout recalc 🎨💸
> **Composite only** = cheap — GPU handles it, skip both! 🚀✅
>
> Minimising **reflow** is the single biggest win for browser rendering performance!

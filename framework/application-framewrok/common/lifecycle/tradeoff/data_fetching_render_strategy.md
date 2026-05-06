# Why Data Fetching is Often Done After Initial Render (Framework-Agnostic)

## 🧠 Summary

In modern frontend frameworks (React, Vue, Angular), data fetching is often performed **after the initial render (mount phase)** instead of before, to improve user experience, avoid blocking rendering, and align with the separation between initialization and side effects.

---

## 🎯 Key Reasons

### 1️⃣ Avoid Blocking Initial Render

- Fetching data before render delays UI display
- Users may see a blank screen while waiting for API response

❗ Result:
- Poor perceived performance

---

### 2️⃣ Better User Experience (Perceived Performance)

- Rendering UI first provides immediate feedback
- Data is loaded asynchronously afterward

👉 Users feel the app is faster, even if total time is similar

---

### 3️⃣ Separation of Concerns

Framework design typically separates:

- Initialization phase → define structure and state
- Side-effect phase → perform external operations (API calls)

👉 Data fetching is a **side effect**, so it belongs after render

---

### 4️⃣ Improved Responsiveness

- UI becomes interactive earlier
- Loading states or placeholders can be displayed

---

### 5️⃣ Easier State & Error Handling

After render, it is easier to manage:

- loading states
- error states
- retries
- partial updates

---

## ⚠️ Trade-off

### After Render (Common Approach)

```plaintext
Render UI → Fetch Data → Update UI
```

Pros:
- Fast initial display
- Better perceived performance

Cons:
- May show loading or flicker

---

### Before Render (Blocking Approach)

```plaintext
Fetch Data → Render UI
```

Pros:
- Complete UI at first render
- No loading flicker

Cons:
- Slower initial load
- Blank screen during wait

---

## 🟡 When to Fetch Before Render

Use pre-fetching when:

- SEO is required (Server-Side Rendering)
- Critical data must be available before UI
- Authentication or permissions are needed first

---

## 🧠 Key Insight

> Modern frontend architecture prioritizes **perceived performance** over complete initial rendering.

---

## 🎯 Final Takeaway

> Data is often fetched after the initial render to ensure fast UI feedback and better user experience, while pre-fetching is reserved for specific scenarios like SSR or critical data requirements.

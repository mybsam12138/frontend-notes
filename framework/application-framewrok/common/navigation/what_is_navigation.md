# 🧭 What Is Navigation?

## 1. Definition

**Navigation** is the mechanism that allows users to move between different views or pages in a frontend application **without triggering a full browser page reload**.

In traditional websites, clicking a link reloads the entire page from the server.

In modern Single Page Applications (SPA), navigation is handled **entirely on the client side** — only the content changes, not the whole page.

---

## 2. Traditional Navigation vs SPA Navigation

| | Traditional Website | SPA Navigation |
|---|---|---|
| How it works | Browser requests a new HTML page from the server | JavaScript swaps out components in the same page |
| Page reload | Yes — full reload every time | No — only the view changes |
| Speed | Slower — full HTML download each time | Faster — only data and components change |
| URL changes | Yes | Yes (handled by the router) |
| Examples | Old PHP/HTML sites | Vue, React, Angular apps |

---

## 3. What Happens During SPA Navigation

```
User clicks a link
        ↓
Router intercepts the click
        ↓
URL in the browser address bar updates
        ↓
Router matches the URL to a component
        ↓
Framework renders the matching component
        ↓
Page content changes — NO full reload ✅
```

---

## 4. Why Navigation Matters

Without a navigation system, a SPA would:

- Not be able to have multiple pages or views
- Lose the current state when the user presses the back button
- Not support bookmarking or sharing URLs
- Feel broken compared to a traditional website

Navigation gives SPA users the **same browsing experience** as a traditional website, while keeping the speed and smoothness of a SPA.

---

## 5. What Controls Navigation?

Navigation in frontend frameworks is managed by a **Router**.

| Framework | Router |
|---|---|
| Vue | Vue Router |
| React | React Router |
| Angular | Angular Router (built-in) |

The router is the library that:

- Watches the URL in the browser
- Maps URLs to components
- Renders the correct component when the URL changes
- Manages browser history (back / forward buttons)

---

## 6. URL and Navigation

Every navigation action corresponds to a URL change.

Example:

```
/                 → Home page component
/about            → About page component
/products         → Products list component
/products/123     → Product detail component (id = 123)
/login            → Login page component
```

The router reads the URL and decides which component to render.

---

## 7. Types of Navigation

### 7.1 Declarative Navigation

The user clicks a link in the template.

```vue
<!-- Vue Router example -->
<RouterLink to="/about">Go to About</RouterLink>

<!-- React Router example -->
<Link to="/about">Go to About</Link>
```

The router intercepts the click and handles the navigation.

---

### 7.2 Programmatic Navigation

The developer triggers navigation from JavaScript code.

```js
// Vue Router
router.push('/about')
router.push({ name: 'ProductDetail', params: { id: 123 } })

// React Router
navigate('/about')
```

This is useful after:

- Completing a form submission
- Successful login → redirect to dashboard
- After deleting a record → redirect to list page

---

## 8. Browser History and Navigation

The browser maintains a **history stack** of visited URLs.

```
History Stack:
  /home         ← first visit
  /products     ← user clicked Products
  /products/42  ← user clicked a product
  /cart         ← user clicked Add to Cart  ← current
```

The router works with the browser history API to:

- Add a new entry when the user navigates forward
- Remove the top entry when the user presses Back
- Allow the user to go Forward again

This is what makes the browser Back and Forward buttons work correctly in a SPA.

---

## 9. Navigation Guards

Navigation guards are functions that run **before or after** a navigation happens.

They are used to:

- Check if the user is logged in before entering a protected page
- Ask the user to confirm before leaving a page with unsaved changes
- Log analytics when a page is visited

```js
// Vue Router example
router.beforeEach((to, from) => {
  if (to.meta.requiresAuth && !isLoggedIn()) {
    return '/login'   // redirect to login page
  }
})
```

---

## 10. Summary

| Concept | Meaning |
|---|---|
| Navigation | Moving between views/pages in a SPA without full reload |
| Router | The library that manages navigation |
| Declarative navigation | Using `<RouterLink>` or `<Link>` in templates |
| Programmatic navigation | Using `router.push()` or `navigate()` in code |
| Browser history | The stack of visited URLs that supports Back/Forward |
| Navigation guards | Functions that run before/after navigation to control access |

---

## 11. Analogy

Think of navigation like a **TV remote control**.

- The TV screen stays on (the SPA page does not reload)
- Pressing a button changes the channel (the URL changes)
- The correct show appears (the router renders the correct component)
- The TV remembers the last channel you watched (browser history)

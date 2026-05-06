# 🖥️ Rendering Strategies — MPA, SPA, SSR, SSG

## 1. Overview

Rendering strategy defines **where and when** the HTML page is built and delivered to the user.

There are four main strategies in modern frontend development:

```
MPA  → server renders every page on every request
SPA  → browser renders everything using JavaScript
SSR  → server renders first page, browser takes over after
SSG  → all pages pre-built at build time, server just serves files
```

---

## 2. MPA — Multi Page Application

### Definition
The server renders a **complete HTML page on every request**. Every navigation triggers a full page reload and a new server request.

### How it works
```
User visits /home    → server renders home.html    → full page load
User clicks About    → server renders about.html   → full page load again
User clicks Products → server renders products.html → full page load again

Every navigation = new request = full reload
```

### Technologies
- PHP, JSP, Django templates
- jQuery (adds interactivity on top of server-rendered HTML)

### Use cases
- Traditional websites
- Content-heavy sites where SEO matters
- Simple sites that don't need smooth navigation

### Pros and Cons
| ✅ Pros | 😱 Cons |
|---|---|
| Good SEO | Full reload on every navigation |
| Simple architecture | Slow user experience |
| Works without JS | Page flickers on navigation |

---

## 3. SPA — Single Page Application

### Definition
The server sends **one empty HTML file + a JavaScript bundle**. The browser downloads JS first, then Vue/React builds the entire page in the browser.

### How it works
```
User visits app:
  server sends empty HTML + JS bundle
        ↓
  browser downloads JS  ← user sees blank screen here 🐢
        ↓
  Vue/React runs → builds the page
        ↓
  user sees content ✅

After that:
  all navigation handled by JS in browser
  no more server requests for pages
  only API calls for data ✅
```

### Technologies
- Vue (without Nuxt)
- React (without Next.js)
- Angular

### Use cases
- Admin dashboards
- Internal tools
- Apps where SEO does not matter
- Apps requiring rich interactivity

### Pros and Cons
| ✅ Pros | 😱 Cons |
|---|---|
| Fast navigation after first load | Slow first load (JS must download first) |
| Smooth user experience | Bad SEO (Google sees empty HTML) |
| Rich interactivity | Blank screen while JS loads |

---

## 4. SSR — Server Side Rendering

### Definition
The server **renders the first page to full HTML** and sends it to the browser. After that, JavaScript hydrates the page and Vue/React takes over — behaving like a SPA from that point on.

### How it works
```
First visit:
  server runs Vue → renders full HTML → sends to browser
  browser shows content immediately ✅  ← no blank screen
        ↓
  JS bundle downloads in background
        ↓
  Vue hydrates → attaches behaviour → page interactive ✅
        ↓
After first load:
  Vue Router takes over
  all navigation handled client side
  server never renders again ✅
```

### What is hydration?
Hydration is when Vue takes over the server-rendered HTML and makes it interactive:
```
Server sends:
  <button>Add to Cart</button>   ← visible but not interactive yet

After hydration:
  <button @click="addToCart">Add to Cart</button>  ← interactive ✅
```

### Technologies
- Nuxt.js (Vue + SSR)
- Next.js (React + SSR)

### Use cases
- E-commerce sites (SEO + real-time data)
- News and media sites
- Any site needing both SEO and interactivity
- Marketing sites with dynamic content

### Pros and Cons
| ✅ Pros | 😱 Cons |
|---|---|
| Fast first load | More complex infrastructure |
| Good SEO | Server must run Node.js |
| Real-time data | Higher server cost |
| SPA behaviour after first load | State management risks (SSR singleton problem) |

---

## 5. SSG — Static Site Generation

### Definition
All pages are **pre-built as plain HTML files at build time** — before deployment. The server just stores and serves these files. No rendering happens at runtime.

### How it works
```
At build time (before deployment):
  framework runs through all pages ONCE
        ↓
  renders every page to plain HTML files:
    /index.html        ← already built
    /about.html        ← already built
    /blog/post-1.html  ← already built
    /blog/post-2.html  ← already built
        ↓
  deploy HTML files to server or CDN

When user visits:
  server just sends the pre-built file ⚡
  no rendering, no JS execution, nothing
```

### Data and updates
SSG pages are frozen at build time:
```
Content changes in database
        ↓
users do NOT see the change automatically
        ↓
must rebuild and redeploy to update HTML files
        ↓
only then users see the new content
```

### Technologies
- Nuxt.js (static mode)
- Next.js (static export)
- Gatsby
- VitePress (Vue-based docs)

### Use cases
- Blogs
- Documentation sites
- Marketing / landing pages
- Any content that is the same for all users and changes infrequently

### Pros and Cons
| ✅ Pros | 😱 Cons |
|---|---|
| Fastest possible load ⚡ | Content frozen until rebuild |
| Best SEO | Cannot show user-specific data |
| Zero server work at runtime | Rebuild needed for every content update |
| Can be hosted on CDN cheaply | Not suitable for real-time data |

---

## 6. Full Comparison

| | MPA | SPA | SSR | SSG |
|---|---|---|---|---|
| Where renders | Server every request | Browser | Server first, browser after | Build time |
| First load speed | Medium | 🐢 Slow | ⚡ Fast | ⚡ Fastest |
| Page reload on navigate | ✅ Always | ❌ Never | ❌ After first load | ❌ After first load |
| SEO | ✅ Good | 😱 Bad | ✅ Good | ✅ Best |
| Real-time data | ✅ Yes | ✅ Yes | ✅ Yes | 😱 Rebuild needed |
| User-specific data | ✅ Yes | ✅ Yes | ✅ Yes | ❌ No |
| Server required | ✅ Yes | ❌ No | ✅ Yes (Node.js) | ❌ No |
| Examples | PHP, jQuery | Vue SPA | Nuxt, Next.js | Nuxt static, Gatsby |

---

## 7. SEO Explained

Google crawler reads raw HTML only — it does not run JavaScript.

```
SPA:
  Google visits /products
  receives: <div id="app"></div>   ← empty!
  indexes nothing 😱

SSR / SSG / MPA:
  Google visits /products
  receives: full HTML with real content ✅
  indexes everything ✅
```

This is why SPA is bad for SEO — content only exists after JS runs, but Google never waits for JS.

---

## 8. Use Case Decision Guide

```
Need SEO + real-time data?          → SSR  (Nuxt / Next.js)
Need SEO + content rarely changes?  → SSG  (Nuxt static / Gatsby)
No SEO needed + rich interactivity? → SPA  (Vue / React)
Simple site + traditional approach? → MPA  (PHP / jQuery)
```

---

## 9. Analogy

```
MPA  → restaurant: cook every dish fresh when ordered, serve on new plate every time
SPA  → self-service: kitchen sends you all ingredients, you cook yourself
SSR  → room service: kitchen cooks your first dish, then you cook the rest yourself
SSG  → meal prep: cook everything Sunday, just reheat when needed ⚡
```

---

```

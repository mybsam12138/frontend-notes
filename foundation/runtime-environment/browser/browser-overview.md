# Browser Fundamentals

## 1. What is a Browser?

A browser is a **client application** that retrieves resources from servers and renders them into a user-visible interface.

Main responsibilities:
- Send HTTP/HTTPS requests
- Parse and render HTML/CSS
- Execute JavaScript
- Manage user interactions

---

## 2. High-Level Architecture

A modern browser consists of:

### 2.1 Browser Process
- UI (address bar, tabs)
- Navigation control
- Network management

### 2.2 Renderer Process (Core)
- Responsible for rendering web pages
- Each tab usually has its own renderer process

### 2.3 GPU Process
- Handles rendering optimization (compositing, animations)

### 2.4 Network Process
- Handles HTTP requests, caching, cookies

### 2.5 Plugin Process (optional)
- For external plugins

---

## 3. What Happens When You Enter a URL?

### Step 1: URL Parsing
- Validate URL format
- Extract protocol (HTTP/HTTPS), host, path

### Step 2: DNS Resolution
- Convert domain → IP address

### Step 3: TCP Connection
- 3-way handshake

### Step 4: TLS Handshake (HTTPS)
- Secure connection setup

### Step 5: Send HTTP Request
- GET / POST etc.

### Step 6: Server Response
- Returns HTML, CSS, JS, assets

---

## 4. Rendering Process (Critical)

### 4.1 Parse HTML → DOM Tree
- HTML → DOM nodes

### 4.2 Parse CSS → CSSOM Tree
- CSS rules → style tree

### 4.3 Build Render Tree
- Combine DOM + CSSOM

### 4.4 Layout (Reflow)
- Calculate position & size

### 4.5 Paint
- Convert to pixels

### 4.6 Composite
- GPU layers rendering

---

## 5. JavaScript Execution

- JS is executed by the **JS Engine (e.g., V8)**
- Runs in **single thread**
- Can manipulate DOM & CSSOM

### Key Concepts:
- Execution Context
- Call Stack
- Event Loop (async handling)

---

## 6. Event Loop (Core Concept)

JS is single-threaded but supports async via:

- Call Stack (sync tasks)
- Task Queue (async tasks)
- Microtask Queue (Promises)

Execution order:
1. Run sync code
2. Run microtasks
3. Run macrotasks

---

## 7. Browser Storage

### Types:
- Cookie (small, sent with requests)
- LocalStorage (persistent)
- SessionStorage (session-based)
- IndexedDB (large structured data)

---

## 8. Security Model

### Same-Origin Policy
Restricts access between:
- Different domain
- Different protocol
- Different port

### Common Solutions:
- CORS
- Proxy (BFF)

---

## 9. Performance Key Points

- Reduce HTTP requests
- Use caching
- Minimize reflow/repaint
- Use async loading (defer/async)
- Code splitting

---

## 10. Summary (One Line)

Browser = **Network + Parsing + Rendering + JS Execution Engine + Security Sandbox**
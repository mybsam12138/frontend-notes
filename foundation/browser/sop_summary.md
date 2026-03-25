# Same-Origin Policy (SOP) & Solutions

## 1. What is Same-Origin Policy?

Same-Origin Policy (SOP) is a browser-enforced security mechanism that restricts how scripts from one origin can access resources from another origin.

---

## 2. What is "Origin"?

Origin = protocol + domain + port

### Examples

| URL | Same Origin? |
|-----|-------------|
| https://a.com/page | — |
| https://a.com/api | Yes |
| http://a.com | No (protocol differs) |
| https://b.com | No (domain differs) |
| https://a.com:8080 | No (port differs) |

---

## 3. What Does SOP Restrict?

- Cross-origin data access (fetch, AJAX)
- DOM access across origins
- Cookies / LocalStorage of other origins

---

## 4. Important Behavior

Request → Allowed  
Response → Received  
JS Access → Restricted  

SOP does NOT block the request, only blocks JavaScript access.

---

## 5. Why SOP Exists

To prevent:
- Data theft
- Unauthorized access
- Cross-site attacks

---

## 6. Solutions

### 6.1 CORS

Server adds:

Access-Control-Allow-Origin

### 6.2 Proxy (BFF)

Frontend → Your backend → Target API

### 6.3 JSONP (legacy)

Script-based workaround

### 6.4 postMessage

For iframe communication

---

## 7. Summary

SOP = browser security restriction  
CORS = controlled access solution  

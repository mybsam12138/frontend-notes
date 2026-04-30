# HTTP & Network (Frontend Summary)

## 1. Overall Flow (Very Important)

When you open a website:

1. DNS → domain → IP
2. TCP → establish connection
3. TLS → secure connection (HTTPS)
4. HTTP → send request
5. Server → process
6. Response → return data
7. Browser → render page

---

## 2. HTTP Basics

- HTTP = application layer protocol
- Stateless
- Request → Response

### Request

- Method (GET, POST)
- URL
- Headers
- Body (optional)

### Response

- Status Code
- Headers
- Body

---

## 3. HTTP Methods

- GET → read
- POST → create
- PUT → replace
- PATCH → partial update
- DELETE → remove

---

## 4. Status Codes

- 2xx → success (200)
- 3xx → redirect (301)
- 4xx → client error (404)
- 5xx → server error (500)

---

## 5. HTTP vs HTTPS

- HTTP → not secure
- HTTPS → encrypted (TLS)

---

## 6. DNS

- Domain → IP
- Cache → OS → DNS server

---

## 7. TCP

- Reliable connection
- 3-way handshake

---

## 8. HTTP Versions

- HTTP/1.1 → multiple connections
- HTTP/2 → multiplexing (better performance)

---

## 9. Browser Requests

- Each resource = one request
- Parallel but limited

---

## 10. Cache

- Cache-Control
- ETag

Purpose:
- improve performance
- reduce requests

---

## 11. CORS

- Cross-origin restriction
- Controlled by server headers

---

## 12. Storage

- Cookie → sent to server
- LocalStorage → browser only

---

## 13. REST API

- URL = resource
- Method = action
- JSON = data format

---

## 14. One-line Summary

👉 HTTP = communication between browser and server  
👉 Network = how request reaches server (DNS + TCP + TLS)

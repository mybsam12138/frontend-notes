# HTTP/1.0 vs HTTP/1.1 vs HTTP/2 (Summary)

## 1. Core Differences Overview

| Feature | HTTP/1.0 | HTTP/1.1 | HTTP/2 |
|--------|--------|---------|--------|
| Connection | New per request | Keep-Alive (reuse) | Single persistent |
| Requests per connection | 1 | Multiple (sequential) | Multiple (parallel) |
| Multiplexing | ❌ | ❌ | ✅ |
| Ordering required | ✅ | ✅ | ❌ |
| Header compression | ❌ | ❌ | ✅ |
| Protocol type | Text | Text | Binary |
| Performance | Slow | Improved | Fast |

---

## 2. HTTP/1.0

### Characteristics

- One request per TCP connection
- Connection closes after response

### Flow

Request → Response → Close connection

### Problems

- Many TCP handshakes
- High latency
- Poor performance

---

## 3. HTTP/1.1

### Improvements over 1.0

- Keep-Alive (connection reuse)
- Reduced TCP overhead

### Flow

Request → Response  
Request → Response  
(on same connection)

---

### Limitations

- No multiplexing
- Head-of-Line Blocking

```text
Request A (slow)
→ blocks B and C
```

- Still needs multiple connections in browser

---

## 4. HTTP/2

### Major Improvements

#### 1. Multiplexing

- Multiple requests in one connection
- No blocking

#### 2. Stream ID

- Each request has ID
- Responses can be out of order

#### 3. Header Compression

- Reduce repeated headers

#### 4. Binary Protocol

- Faster parsing

---

### Flow

```text
A1 B1 C1 A2 B2 C2 (interleaved)
```

---

## 5. Key Concepts Comparison

### Blocking

- HTTP/1.1 → blocking (ordered response)
- HTTP/2 → non-blocking (stream-based)

---

### Connection Usage

- HTTP/1.0 → many connections
- HTTP/1.1 → few connections
- HTTP/2 → one connection

---

### Performance

- HTTP/1.0 → worst
- HTTP/1.1 → better
- HTTP/2 → best

---

## 6. Mental Model

```text
HTTP/1.0 = one request per connection
HTTP/1.1 = one connection, sequential requests
HTTP/2   = one connection, parallel streams
```

---

## 7. One-line Summary

👉 HTTP/1.0 → inefficient (new connection each time)  
👉 HTTP/1.1 → improved with keep-alive but still blocking  
👉 HTTP/2 → modern solution with multiplexing and parallel processing

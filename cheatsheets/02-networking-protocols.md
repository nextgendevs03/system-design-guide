# Networking Protocols - Cheatsheet

## TCP vs UDP Quick Reference

```
┌─────────────────────────────────────────────────────────────┐
│  TCP                          │  UDP                        │
├─────────────────────────────────────────────────────────────┤
│  Connection-oriented          │  Connectionless             │
│  Reliable delivery            │  Best effort                │
│  Ordered packets              │  No ordering                │
│  Slower (overhead)            │  Faster                     │
│  Flow control                 │  No flow control            │
├─────────────────────────────────────────────────────────────┤
│  Web, Email, Files            │  Gaming, Streaming, DNS     │
└─────────────────────────────────────────────────────────────┘
```

## HTTP Status Codes

| Code | Meaning | Common Examples |
|------|---------|-----------------|
| 2xx | Success | 200 OK, 201 Created, 204 No Content |
| 3xx | Redirect | 301 Moved, 302 Found, 304 Not Modified |
| 4xx | Client Error | 400 Bad Request, 401 Unauthorized, 404 Not Found |
| 5xx | Server Error | 500 Internal, 502 Bad Gateway, 503 Unavailable |

## HTTP Methods

| Method | Purpose | Safe | Idempotent |
|--------|---------|:----:|:----------:|
| GET | Read | ✅ | ✅ |
| POST | Create | ❌ | ❌ |
| PUT | Replace | ❌ | ✅ |
| PATCH | Update | ❌ | ❌ |
| DELETE | Remove | ❌ | ✅ |

## Protocol Selection

```
Need real-time bidirectional?     → WebSocket
Simple CRUD API?                  → REST
Complex nested data?              → GraphQL
High-perf microservices?          → gRPC
Server push notifications?        → SSE or WebSocket
Video streaming?                  → HTTP (HLS/DASH)
Online gaming?                    → UDP
```

## WebSocket vs HTTP

| Aspect | HTTP | WebSocket |
|--------|------|-----------|
| Direction | Request → Response | Bidirectional |
| Connection | New per request | Persistent |
| Overhead | Headers each time | Minimal frames |
| Use Case | CRUD, files | Real-time, chat |

## REST vs GraphQL

| REST | GraphQL |
|------|---------|
| Multiple endpoints | Single endpoint |
| Server defines response | Client defines response |
| HTTP caching built-in | Custom caching needed |
| Over-fetching common | Fetch exactly what's needed |

## DNS Record Types

| Type | Purpose | Example |
|------|---------|---------|
| A | IPv4 address | example.com → 1.2.3.4 |
| AAAA | IPv6 address | example.com → ::1 |
| CNAME | Alias | www → example.com |
| MX | Mail server | Mail routing |
| TXT | Text data | SPF, verification |
| NS | Name server | DNS delegation |

## Common Port Numbers

| Port | Protocol |
|------|----------|
| 80 | HTTP |
| 443 | HTTPS |
| 53 | DNS |
| 22 | SSH |
| 21 | FTP |
| 25 | SMTP |
| 3306 | MySQL |
| 5432 | PostgreSQL |
| 6379 | Redis |
| 27017 | MongoDB |

## gRPC Streaming Patterns

```
1. Unary:           Client ──► Server (single req/res)
2. Server Stream:   Client ──► Server ══► Client
3. Client Stream:   Client ══► Server ──► Client  
4. Bidirectional:   Client ◄══► Server
```

## Quick Latency Numbers

| Operation | Latency |
|-----------|---------|
| Same datacenter RTT | 0.5 ms |
| Cross-region RTT | 50-100 ms |
| Cross-continent RTT | 150-300 ms |
| DNS lookup (cached) | < 1 ms |
| DNS lookup (uncached) | 20-120 ms |
| TLS handshake | 1-2 RTT |

---

**#Networking #SystemDesign #Protocols**


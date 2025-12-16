# Interview Questions: Chapter 02 - Networking & Communication

## Easy Questions

### 1. What is the difference between TCP and UDP?
**Answer:**
- **TCP (Transmission Control Protocol):**
  - Connection-oriented (requires handshake)
  - Reliable delivery with acknowledgments
  - Ordered packet delivery
  - Flow and congestion control
  - Higher overhead
  - Use cases: Web browsing, email, file transfer

- **UDP (User Datagram Protocol):**
  - Connectionless (no handshake)
  - No delivery guarantee
  - No ordering
  - No flow control
  - Lower overhead, faster
  - Use cases: Gaming, video streaming, DNS queries

### 2. What are the main HTTP methods and when do you use each?
**Answer:**
| Method | Purpose | Idempotent |
|--------|---------|------------|
| GET | Retrieve resource | Yes |
| POST | Create new resource | No |
| PUT | Replace entire resource | Yes |
| PATCH | Partial update | No |
| DELETE | Remove resource | Yes |
| HEAD | GET without body | Yes |
| OPTIONS | Get allowed methods | Yes |

### 3. What is HTTPS and why is it important?
**Answer:** HTTPS is HTTP over TLS (Transport Layer Security). It provides:
1. **Encryption** - Data cannot be read by eavesdroppers
2. **Authentication** - Verifies the server's identity via certificates
3. **Integrity** - Ensures data wasn't modified in transit

It's important for security, user trust, and SEO (Google ranks HTTPS higher).

---

## Medium Questions

### 4. Explain how DNS resolution works step by step.
**Answer:**
1. **Browser Cache** - Check if domain is cached
2. **OS Cache** - Check system DNS cache
3. **Recursive Resolver** - Query ISP's DNS server
4. **Root Server** - Ask "where is .com TLD?"
5. **TLD Server** - Ask "where is example.com nameserver?"
6. **Authoritative Server** - Get the actual IP address
7. **Cache & Return** - Cache result with TTL, return to browser

Key components:
- DNS uses UDP port 53 for speed
- TTL (Time To Live) controls caching duration
- Multiple caching layers reduce latency

### 5. What are WebSockets and when should you use them?
**Answer:** WebSockets provide a persistent, full-duplex communication channel over a single TCP connection.

**Use When:**
- Real-time chat applications
- Live notifications/feeds
- Online multiplayer gaming
- Collaborative editing (Google Docs)
- Live dashboards and stock tickers
- IoT device communication

**Don't Use When:**
- Simple request-response operations
- One-time data fetching
- Operations that can be cached

**Key Differences from HTTP:**
- Bidirectional (server can push data)
- Persistent connection (no repeated handshakes)
- Lower latency for frequent updates

### 6. Compare REST and GraphQL APIs.
**Answer:**

| Aspect | REST | GraphQL |
|--------|------|---------|
| Endpoints | Multiple (per resource) | Single (/graphql) |
| Data Fetching | Server decides | Client specifies |
| Over-fetching | Common | Eliminated |
| Under-fetching | Requires multiple calls | Single query |
| Caching | HTTP caching | More complex |
| Versioning | URL-based (/v1/, /v2/) | Schema deprecation |
| Learning Curve | Lower | Higher |

**Choose REST for:** Simple CRUD, public APIs, HTTP caching needs
**Choose GraphQL for:** Complex nested data, diverse clients, bandwidth optimization

---

## Hard Questions

### 7. Explain gRPC and when you would use it over REST.
**Answer:** gRPC is a high-performance RPC framework using HTTP/2 and Protocol Buffers.

**gRPC Advantages:**
1. **Performance** - Binary Protobuf is 3-10x smaller than JSON
2. **HTTP/2** - Multiplexing, bidirectional streaming
3. **Type Safety** - Strong contracts via .proto files
4. **Code Generation** - Auto-generate client/server code
5. **Streaming** - Built-in support for all streaming patterns

**Use gRPC for:**
- Microservices communication
- Low-latency, high-throughput systems
- Polyglot environments (multiple languages)
- Bidirectional streaming needs

**Use REST instead when:**
- Browser clients (limited gRPC-web support)
- Public APIs needing universal compatibility
- Simple CRUD operations
- Human-readable debugging is important

### 8. What is HTTP/2 and how does it improve upon HTTP/1.1?
**Answer:**

**HTTP/1.1 Problems:**
- Head-of-line blocking (one slow request blocks others)
- No multiplexing (one request per connection)
- Uncompressed headers
- Text-based protocol

**HTTP/2 Improvements:**
1. **Multiplexing** - Multiple requests over single connection
2. **Header Compression** - HPACK reduces header size
3. **Binary Protocol** - More efficient parsing
4. **Server Push** - Server sends resources before client asks
5. **Stream Prioritization** - Important resources first

**HTTP/3 (QUIC):** Built on UDP to eliminate TCP's head-of-line blocking at transport layer.

### 9. Design a protocol strategy for a ride-sharing app like Uber.
**Answer:**

**Client API Layer:**
- REST over HTTP/2 for standard operations (book ride, view history)
- WebSockets for real-time location tracking and ride status

**Internal Microservices:**
- gRPC for service-to-service communication (low latency)
- Protocol Buffers for efficient serialization

**Location Service:**
- WebSocket for driver location streaming
- Kafka for location event processing

**Push Notifications:**
- Firebase Cloud Messaging / APNs for mobile push

**Key Considerations:**
- Location updates need low latency (WebSocket + UDP internally)
- Driver-rider matching needs high throughput (gRPC)
- User-facing APIs need reliability (REST with retries)
- Geospatial queries need specialized protocols

---

## Scenario-Based Questions

### 10. You're designing a video streaming service. What protocols would you use and why?
**Answer:**

**Video Delivery:**
- HTTP-based adaptive streaming (HLS or DASH)
- Reason: Works through firewalls, leverages CDN caching, adaptive bitrate

**User API:**
- REST or GraphQL for catalog, user profiles
- Reason: Standard CRUD operations, cacheable

**Real-time Features:**
- WebSockets for live comments, reactions
- Server-Sent Events for viewing counts

**Internal Services:**
- gRPC for microservices (transcoding, recommendations)
- Reason: High throughput, type safety

**Content Protection:**
- HTTPS everywhere
- DRM protocols (Widevine, FairPlay)

---

## Quick Tips for Interviews

1. Always discuss trade-offs when comparing protocols
2. Mention real-world examples (Netflix uses X because...)
3. Consider failure modes and how protocols handle them
4. Know the performance characteristics (latency, throughput)
5. Understand when to combine multiple protocols

## Key Numbers to Remember

| Metric | Value |
|--------|-------|
| DNS TTL (typical) | 300-3600 seconds |
| HTTP keepalive timeout | 5-15 seconds |
| WebSocket ping interval | 30 seconds |
| gRPC default timeout | 5 seconds |
| TCP handshake RTT | 1-3 round trips |


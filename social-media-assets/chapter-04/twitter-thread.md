# Twitter Thread: Caching & CDN

> Copy-paste ready thread for Twitter/X

---

## Thread

**Tweet 1 (Hook):**
```
⚡ How to make your app 100x faster?

Cache everything.

Here's the complete caching guide you need 🧵👇
```

---

**Tweet 2:**
```
First, why cache?

Database query: 50-100ms
Cache lookup: <1ms

That's 100x difference.

Amazon found that 100ms delay = 1% revenue loss.

At their scale? That's ~$1.6 BILLION per year.

Caching isn't optional at scale. It's required.
```

---

**Tweet 3:**
```
The most common pattern: Cache-Aside

1️⃣ App checks cache first
2️⃣ Cache HIT? Return fast ⚡
3️⃣ Cache MISS? Query database
4️⃣ Store result in cache
5️⃣ Return to user

90% hit rate = 10x fewer database queries.
```

---

**Tweet 4:**
```
Redis isn't just key-value.

It has:
• Strings → Caching
• Lists → Queues
• Sets → Unique items
• Hashes → Objects
• Sorted Sets → Leaderboards
• Streams → Event logs

This is why Redis beats Memcached for most use cases.
```

---

**Tweet 5:**
```
5 things you can build with Redis:

1. Session storage (auth)
2. Rate limiting (API protection)
3. Leaderboards (gaming)
4. Pub/Sub (real-time notifications)
5. Distributed locks (prevent race conditions)

And all of this in <1ms.
```

---

**Tweet 6:**
```
The hardest problem in caching?

Cache invalidation.

When data changes:
• Database: ✅ Updated
• Cache: ❌ Still old!

Solutions:
• TTL (auto-expire)
• Event-based invalidation
• Version-based keys
• Write-through updates
```

---

**Tweet 7:**
```
What about static content?

Use a CDN.

Without CDN:
User (Tokyo) → Server (US) = 200ms 🐌

With CDN:
User (Tokyo) → Edge (Tokyo) = 20ms ⚡

80-90% of traffic served from edge servers.

Netflix built their own (Open Connect).
```

---

**Tweet 8:**
```
Multi-layer caching for maximum speed:

Browser Cache (0ms)
    ↓
CDN Edge (10ms)
    ↓
App Local Cache (1ms)
    ↓
Redis/Memcached (2ms)
    ↓
Database (50ms)

Each layer reduces load on the next.
```

---

**Tweet 9:**
```
Watch out for Cache Stampede!

When cache expires:
→ 1000 requests all hit database
→ Database overwhelmed 💥

Solutions:
• Locking (one request regenerates)
• Early refresh (refresh before expire)
• Stale-while-revalidate
```

---

**Tweet 10 (CTA):**
```
To summarize caching:

✅ Cache-Aside is your default pattern
✅ Redis > Memcached for most cases
✅ CDN for static assets
✅ Cache invalidation is HARD
✅ Multi-layer for best performance

If this thread helped, retweet the first tweet!

Follow @yourhandle for more system design content.
```

---

## 🖼️ Image for Tweet 1

Create in Excalidraw:

```
┌─────────────────────────────────────────┐
│                                         │
│   ⚡ CACHING COMPLETE GUIDE            │
│                                         │
│   Make your app 100x faster             │
│                                         │
│   ┌─────┐      ┌─────┐      ┌─────┐    │
│   │User │ ──▶ │Cache│ ──▶ │ DB  │    │
│   └─────┘      └─────┘      └─────┘    │
│                  ⚡                      │
│               <1ms                      │
│                                         │
│   Thread below 👇                       │
│                                         │
└─────────────────────────────────────────┘
```


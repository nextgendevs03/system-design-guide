# Quote Cards: Chapter 04 - Caching

> Create these in Canva (1080 x 1080)

---

## Quote Card 1

**Background**: Dark gradient with lightning bolt

```
"The fastest database query
is the one you don't
have to make."

⚡ Cache everything.
```

**Caption**:
```
This is the #1 rule of performance engineering.

90% cache hit rate = 10x fewer database queries.

Redis can handle 100K+ operations per second.
Your database? Maybe 1-5K.

Cache first, database second.

#Redis #Caching #Performance
```

---

## Quote Card 2

**Background**: Red/orange warning theme

```
"There are only two hard
things in Computer Science:

cache invalidation
and naming things."

— Phil Karlton
```

**Caption**:
```
The classic CS joke that's also painfully true.

Cache invalidation is hard because:
• Database changes, cache doesn't know
• Multiple servers = multiple caches
• Timing issues everywhere

Solutions:
1. TTL (simple but imperfect)
2. Event-driven invalidation
3. Version-based keys

Which strategy do you use?

#ComputerScience #Caching #Programming
```

---

## Quote Card 3

**Background**: Blue gradient with numbers

```
Database: 50-100ms
Cache: < 1ms

That's 100x faster.

At scale, this is
the difference between
success and failure.
```

**Caption**:
```
Numbers don't lie.

Memory access: 100 nanoseconds
Network + DB query: 50-100 milliseconds

That's a 500,000x difference in raw speed.

Even with network overhead, Redis gives you 100x improvement.

Are you caching enough?

#Performance #SystemDesign #Backend
```

---

## Quote Card 4

**Background**: Purple gradient

```
Netflix handles 15% of
global internet traffic.

Their secret?

Caching at every layer.
```

**Caption**:
```
Netflix's caching strategy:

🌍 Open Connect CDN
   Video content at ISP level

⚡ EVCache (Memcached)
   Metadata, sessions, API

💾 Cassandra
   Distributed storage

The result? Smooth 4K streaming for 200M+ users.

What can you learn from their architecture?

#Netflix #CDN #SystemDesign
```

---

## Quote Card 5

**Background**: Clean white, red X and green checkmarks

```
Cache Stampede ❌

1000 requests
all hit database
at the same time.

Solution: ✅
Locking, early refresh,
or stale-while-revalidate.
```

**Caption**:
```
The cache stampede problem explained:

1. Popular cache key expires
2. 1000 concurrent requests arrive
3. All see cache is empty
4. All query database simultaneously
5. Database overwhelmed 💥

Prevention strategies:
✅ Mutex lock (one request regenerates)
✅ Probabilistic early refresh
✅ Background refresh jobs

Have you ever experienced this in production?

#Caching #SystemDesign #Backend
```

---

## Quote Card 6

**Background**: Gradient with Redis logo

```
REDIS SUPERPOWERS

Strings → Caching
Lists → Queues
Sets → Unique items
Hashes → Objects
Sorted Sets → Leaderboards
Streams → Event logs

All in < 1ms.
```

**Caption**:
```
Redis is NOT just a cache.

It's a Swiss Army knife for backend developers.

Real use cases:
• Session storage
• Rate limiting
• Real-time leaderboards
• Pub/Sub messaging
• Distributed locks
• Job queues

What are you using Redis for?

#Redis #Backend #SystemDesign
```

---

## 🎨 Design Specs

**All Quote Cards**:
- Size: 1080 x 1080
- Font: Space Grotesk or Poppins
- Quote text: 36-48px
- Attribution: 20-24px
- Include lightning bolt ⚡ emoji for caching theme
- Subtle Redis red (#DC382D) as accent color


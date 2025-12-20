# Caching & CDN Cheatsheet

## Caching Patterns

```
┌─────────────────────────────────────────────────────────────┐
│  Pattern          │ Read   │ Write  │ Consistency          │
├─────────────────────────────────────────────────────────────┤
│  Cache-Aside      │ Fast*  │ Medium │ Eventual             │
│  Read-Through     │ Fast*  │ Medium │ Eventual             │
│  Write-Through    │ Fast   │ Slow   │ Strong               │
│  Write-Behind     │ Fast   │ Fast   │ Eventual             │
└─────────────────────────────────────────────────────────────┘
* First read is slow (cache miss)
```

## Cache-Aside Pattern (Most Common)

```python
def get(key):
    value = cache.get(key)
    if value is None:
        value = db.query(key)
        cache.set(key, value, ttl=3600)
    return value

def update(key, data):
    db.update(key, data)
    cache.delete(key)  # Invalidate
```

## Eviction Policies

| Policy | Description | Use Case |
|--------|-------------|----------|
| LRU | Least Recently Used | General purpose |
| LFU | Least Frequently Used | Hot data |
| FIFO | First In First Out | Simple |
| TTL | Time To Live | Time-sensitive |

## Redis Data Structures

| Type | Commands | Use Case |
|------|----------|----------|
| String | GET, SET, INCR | Caching, counters |
| Hash | HGET, HSET, HGETALL | Objects |
| List | LPUSH, RPOP, LRANGE | Queues, feeds |
| Set | SADD, SMEMBERS, SINTER | Tags, unique items |
| Sorted Set | ZADD, ZRANGE, ZRANK | Leaderboards |
| Stream | XADD, XREAD | Event logs |

## Redis vs Memcached

| Feature | Redis | Memcached |
|---------|-------|-----------|
| Data types | Rich | Strings only |
| Persistence | Yes | No |
| Clustering | Built-in | Client-side |
| Pub/Sub | Yes | No |
| Max value | 512 MB | 1 MB |

## Cache-Control Headers

```http
# Static assets (1 year)
Cache-Control: public, max-age=31536000, immutable

# API responses (1 min cache, 5 min stale)
Cache-Control: public, max-age=60, stale-while-revalidate=300

# Private (browser only)
Cache-Control: private, max-age=3600

# No caching
Cache-Control: no-store
```

## CDN Cache Headers

| Header | Purpose |
|--------|---------|
| Cache-Control | Caching rules |
| ETag | Version identifier |
| Last-Modified | Modification time |
| Vary | Cache key variation |
| Age | Time in cache |

## TTL Guidelines

| Data Type | TTL |
|-----------|-----|
| Static assets | 1 year |
| Product catalog | 5-60 min |
| User sessions | 1-24 hours |
| API responses | 1-5 min |
| Stock prices | 1-5 sec |
| Inventory | 30 sec |

## Common Pitfalls

| Problem | Solution |
|---------|----------|
| Stampede | Locking, early refresh |
| Penetration | Cache nulls, bloom filter |
| Hot keys | Local cache, replication |
| Stale data | TTL, event invalidation |

## Multi-Layer Caching

```
Browser Cache (0ms)
     ↓
CDN Edge (10-50ms)
     ↓
App Local Cache (<1ms)
     ↓
Redis/Memcached (1-5ms)
     ↓
Database (5-100ms)
```

## Quick Commands

```bash
# Redis CLI
SET key "value" EX 3600     # Set with 1hr TTL
GET key                      # Get value
DEL key                      # Delete
TTL key                      # Check TTL
KEYS pattern*               # Find keys (don't use in prod!)
SCAN 0 MATCH pattern*       # Safe key search

# Memcached
set key 0 3600 5\r\nvalue   # Set
get key                      # Get
delete key                   # Delete
```

---

**#Caching #Redis #CDN #SystemDesign**


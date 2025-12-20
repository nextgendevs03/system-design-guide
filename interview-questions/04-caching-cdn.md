# Interview Questions: Chapter 04 - Caching & CDN

## Easy Questions

### 1. What is caching and why is it important?
**Answer:** Caching is storing frequently accessed data in a fast-access storage layer (usually memory) to reduce latency and load on the primary data source.

**Why it's important:**
- **Speed**: Memory access is ~100x faster than database queries
- **Scalability**: Reduces database load, allowing more concurrent users
- **Cost**: Fewer database queries = lower infrastructure costs
- **User Experience**: Faster response times = happier users

**Key metrics:**
- Hit Rate: Percentage of requests served from cache (target: 95%+)
- 90% hit rate = 10x fewer database queries

### 2. What are the common cache eviction policies?
**Answer:**

| Policy | How It Works | Best For |
|--------|--------------|----------|
| **LRU** (Least Recently Used) | Removes item not accessed longest | General purpose |
| **LFU** (Least Frequently Used) | Removes least accessed item | Hot data patterns |
| **FIFO** (First In First Out) | Removes oldest added item | Simple scenarios |
| **TTL** (Time To Live) | Removes expired items | Time-sensitive data |
| **Random** | Randomly evicts | Uniform access patterns |

Most common: **LRU** - simple and effective for most workloads.

### 3. What is a CDN and how does it work?
**Answer:** A **Content Delivery Network** is a globally distributed network of servers that cache and deliver content from locations closer to users.

**How it works:**
1. User requests content
2. DNS routes to nearest CDN edge server
3. If cached (HIT): Return immediately
4. If not cached (MISS): Fetch from origin, cache, return

**Benefits:**
- Reduced latency (serve from nearby edge)
- Lower origin server load (80-90% reduction)
- DDoS protection
- Handles traffic spikes

---

## Medium Questions

### 4. Explain the different caching patterns (Cache-Aside, Read-Through, Write-Through, Write-Behind).
**Answer:**

**Cache-Aside (Lazy Loading):**
- Application checks cache first
- On miss, fetches from DB and populates cache
- On write, updates DB and invalidates cache
- Most common pattern

**Read-Through:**
- Cache sits between app and DB
- Cache handles fetching on miss
- Simpler app code

**Write-Through:**
- Writes go to cache AND database synchronously
- Strong consistency
- Higher write latency

**Write-Behind (Write-Back):**
- Writes go to cache immediately
- Database updated asynchronously (batched)
- Fastest writes, risk of data loss

| Pattern | Read Perf | Write Perf | Consistency | Complexity |
|---------|-----------|------------|-------------|------------|
| Cache-Aside | Fast* | Moderate | Eventual | Low |
| Read-Through | Fast* | Moderate | Eventual | Medium |
| Write-Through | Fast | Slow | Strong | Medium |
| Write-Behind | Fast | Fast | Eventual | High |

### 5. What is cache stampede (thundering herd) and how do you prevent it?
**Answer:** **Cache stampede** occurs when a popular cached item expires and many concurrent requests all try to regenerate it, overwhelming the database.

**Prevention strategies:**

1. **Locking** — Only one request regenerates cache, others wait
```python
if acquire_lock(key):
    value = db.query()
    cache.set(key, value)
    release_lock(key)
else:
    wait_and_retry()
```

2. **Probabilistic early expiration** — Random requests refresh before TTL expires

3. **Stale-while-revalidate** — Serve stale data while refreshing in background

4. **Background refresh** — Separate job refreshes popular items before expiration

### 6. Compare Redis and Memcached.
**Answer:**

| Feature | Redis | Memcached |
|---------|-------|-----------|
| Data Structures | Rich (lists, sets, hashes, sorted sets, streams) | Strings only |
| Persistence | RDB, AOF, Hybrid | None |
| Replication | Built-in master-replica | None |
| Clustering | Redis Cluster | Client-side sharding |
| Pub/Sub | Yes | No |
| Transactions | MULTI/EXEC | CAS only |
| Memory Efficiency | Higher overhead | More efficient for strings |
| Max Value | 512 MB | 1 MB |

**Choose Redis:** Need data structures, persistence, pub/sub
**Choose Memcached:** Simple string caching, maximum memory efficiency

---

## Hard Questions

### 7. Design a caching strategy for a social media feed (like Twitter).
**Answer:**

**Hybrid Push/Pull approach:**

**For regular users (< 10K followers):**
- **Fan-out on write (push)**: When user tweets, push tweet ID to all followers' timeline caches
- Fast reads (pre-computed timeline)

**For celebrities (> 10K followers):**
- **Fan-out on read (pull)**: Don't push to followers
- Merge celebrity tweets at read time

**Implementation:**
```python
def post_tweet(user_id, tweet):
    tweet_id = db.create_tweet(user_id, tweet)
    
    if get_follower_count(user_id) < 10000:
        # Push to follower timelines
        for follower in get_followers(user_id):
            redis.lpush(f"timeline:{follower}", tweet_id)
            redis.ltrim(f"timeline:{follower}", 0, 800)
    # Celebrities: no push, merge at read time

def get_timeline(user_id):
    # Get cached timeline (regular users' tweets)
    cached = redis.lrange(f"timeline:{user_id}", 0, 100)
    
    # Merge celebrity tweets (fetched on-demand)
    celebrities = get_followed_celebrities(user_id)
    celebrity_tweets = db.get_recent_tweets(celebrities)
    
    return merge_and_sort(cached, celebrity_tweets)
```

### 8. How would you handle cache invalidation in a distributed microservices architecture?
**Answer:**

**Event-driven approach:**

1. **Publish invalidation events** when data changes
2. **Cache services subscribe** and invalidate local caches

```
Service A (writes) → Event Bus (Kafka) → Cache Invalidation Service → Redis
                                      → Service B (local cache)
                                      → Service C (local cache)
```

**Strategies:**

1. **TTL + Events**: Short TTL as safety net, events for immediate invalidation
2. **Version-based keys**: Include version in cache key, increment on update
3. **Cache tags**: Tag related items, invalidate by tag

**Challenges:**
- Network delays can cause brief inconsistency
- Need to handle out-of-order events
- Must handle service failures

**Best practices:**
- Use idempotent invalidation
- Log all invalidations for debugging
- Monitor cache hit rates per service

### 9. Design a multi-layer caching system for a high-traffic e-commerce platform.
**Answer:**

**Architecture:**
```
Browser → CDN → Load Balancer → App (Local Cache) → Redis Cluster → Database
```

**Layer 1: Browser Cache**
- Static assets: `Cache-Control: max-age=31536000, immutable`
- API responses: `Cache-Control: max-age=60, stale-while-revalidate=300`

**Layer 2: CDN (CloudFront/Cloudflare)**
- Product images, CSS, JS
- Edge-cache API responses for anonymous users

**Layer 3: Application Local Cache (in-memory)**
- Hot configuration data
- Frequently accessed small objects
- TTL: 1-5 minutes (shorter than Redis)

**Layer 4: Distributed Cache (Redis Cluster)**
- Product details: 5-minute TTL
- User sessions: 24-hour TTL
- Shopping carts: 7-day TTL
- Inventory counts: 30-second TTL

**Layer 5: Database Read Replicas**
- Cached query results
- Read-heavy queries routed here

**Cache warming:**
- Pre-cache top 1000 products on startup
- Refresh trending items every 4 hours

**Invalidation:**
- Product update → Invalidate product cache + CDN purge
- Order placed → Decrement inventory cache
- Price change → Event-driven invalidation

---

## Scenario Questions

### 10. A cache key is getting millions of requests per second. How do you handle this "hot key" problem?
**Answer:**

**Solutions:**

1. **Local caching for hot keys**
   - Each app server caches hot keys locally
   - Reduces load on Redis cluster
   - Trade-off: Slightly stale data

2. **Key replication**
   - Create multiple replicas: `key:0`, `key:1`, `key:2`
   - Randomly select replica for reads
   - Distributes load across slots

3. **Read from replicas**
   - Configure Redis Cluster to allow replica reads
   - Spread load across replicas

4. **Client-side caching**
   - Redis 6.0+ supports client tracking
   - Clients cache values locally with invalidation

```python
# Solution 1: Local hot key cache
hot_keys = LRUCache(maxsize=100)

def get(key):
    if key in hot_keys:
        return hot_keys[key]
    
    value = redis.get(key)
    
    if is_hot_key(key):
        hot_keys[key] = value
    
    return value
```

---

## Quick Tips for Caching Interviews

1. **Always mention trade-offs** — Consistency vs performance
2. **Think about failure modes** — What if cache is down?
3. **Consider invalidation early** — It's the hardest part
4. **Know your numbers** — Redis: <1ms, DB: 5-100ms
5. **Real-world examples** — How Netflix/Twitter does it

## Key Numbers

| Metric | Value |
|--------|-------|
| Redis latency | < 1 ms |
| Memcached latency | < 1 ms |
| Database query | 5-100 ms |
| Target hit rate | 95%+ |
| Redis max value | 512 MB |
| Memcached max value | 1 MB |


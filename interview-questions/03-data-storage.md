# Interview Questions: Chapter 03 - Data Storage Fundamentals

## Easy Questions

### 1. What is the difference between SQL and NoSQL databases?
**Answer:**

| Aspect | SQL | NoSQL |
|--------|-----|-------|
| Schema | Fixed, predefined | Flexible, dynamic |
| Scaling | Primarily vertical | Primarily horizontal |
| Transactions | ACID compliant | Often BASE (eventual consistency) |
| Query Language | Standardized SQL | Varies by database |
| Relationships | JOINs for relations | Embedded documents or references |
| Best For | Complex queries, transactions | Scale, flexibility, simple access |

**Examples:**
- SQL: PostgreSQL, MySQL, Oracle
- NoSQL: MongoDB (document), Redis (key-value), Cassandra (wide-column)

### 2. What does ACID stand for? Explain each property.
**Answer:**
- **Atomicity**: Transactions are all-or-nothing. If any part fails, the entire transaction is rolled back.
- **Consistency**: Database moves from one valid state to another. All rules and constraints are enforced.
- **Isolation**: Concurrent transactions don't interfere with each other. Each sees a consistent view.
- **Durability**: Once committed, data survives system failures (written to persistent storage).

**Example**: Bank transfer — debit from one account and credit to another must both succeed or both fail.

### 3. What is database indexing and why is it important?
**Answer:** An index is a data structure that improves the speed of data retrieval operations.

**Without index:** Full table scan O(n) — check every row
**With index:** B-tree lookup O(log n) — binary search

**Trade-offs:**
- ✅ Faster reads
- ❌ Slower writes (index must be updated)
- ❌ Extra storage space

**Best practices:**
- Index columns used in WHERE, JOIN, ORDER BY
- Don't over-index
- Use composite indexes for multi-column queries

---

## Medium Questions

### 4. Explain database sharding. What are the different sharding strategies?
**Answer:** Sharding is splitting data across multiple databases based on a shard key.

**Strategies:**

1. **Hash-based sharding**
   - `shard = hash(key) % num_shards`
   - ✅ Even distribution
   - ❌ Range queries span all shards

2. **Range-based sharding**
   - Keys A-M → Shard 1, N-Z → Shard 2
   - ✅ Efficient range queries
   - ❌ Risk of hotspots

3. **Directory-based sharding**
   - Lookup table maps keys to shards
   - ✅ Flexible
   - ❌ Lookup table is single point of failure

**Challenges:**
- Cross-shard queries are expensive
- Resharding requires data migration
- Cross-shard transactions are complex

### 5. Compare document databases (MongoDB) vs relational databases (PostgreSQL).
**Answer:**

| Aspect | MongoDB | PostgreSQL |
|--------|---------|------------|
| Data Model | JSON documents | Tables with rows |
| Schema | Flexible (schemaless) | Rigid (predefined) |
| Relationships | Embedded or references | Foreign keys, JOINs |
| Transactions | Multi-doc (v4.0+) | Full ACID |
| Scaling | Built-in sharding | Requires extensions |
| Query | MongoDB Query Language | SQL |

**Choose MongoDB when:**
- Schema evolves frequently
- Hierarchical/nested data
- Rapid prototyping
- Read-heavy with embedded data

**Choose PostgreSQL when:**
- Complex relationships and JOINs
- ACID transactions required
- Complex queries and reporting
- Data integrity is critical

### 6. What is database replication? Explain different replication strategies.
**Answer:** Replication is keeping copies of data on multiple machines for reliability and performance.

**Strategies:**

1. **Single-Leader (Master-Slave)**
   - One leader handles writes
   - Followers handle reads
   - Pros: Simple, consistent
   - Cons: Leader is bottleneck

2. **Multi-Leader**
   - Multiple leaders in different regions
   - Each can accept writes
   - Pros: Low latency globally
   - Cons: Conflict resolution needed

3. **Leaderless**
   - No single leader
   - Writes go to multiple nodes
   - Pros: High availability
   - Cons: Eventual consistency

---

## Hard Questions

### 7. How would you design a database schema for a Twitter-like application?
**Answer:**

**Core tables (PostgreSQL):**
```sql
CREATE TABLE users (
    id BIGSERIAL PRIMARY KEY,
    username VARCHAR(50) UNIQUE,
    email VARCHAR(255) UNIQUE,
    created_at TIMESTAMP DEFAULT NOW()
);

CREATE TABLE tweets (
    id BIGSERIAL PRIMARY KEY,
    user_id BIGINT REFERENCES users(id),
    content VARCHAR(280),
    created_at TIMESTAMP DEFAULT NOW()
);

CREATE TABLE follows (
    follower_id BIGINT REFERENCES users(id),
    following_id BIGINT REFERENCES users(id),
    PRIMARY KEY (follower_id, following_id)
);
```

**Timeline strategies:**

1. **Pull Model** (read-heavy query):
```sql
SELECT t.* FROM tweets t
JOIN follows f ON t.user_id = f.following_id
WHERE f.follower_id = ?
ORDER BY created_at DESC LIMIT 50;
```

2. **Push Model** (fanout on write):
- Pre-compute timelines in Redis/Cassandra
- When user tweets → push to all followers' timelines
- Hybrid: Push for regular users, pull for celebrities

### 8. Explain CAP theorem with real-world examples.
**Answer:** CAP theorem states a distributed system can only guarantee 2 of 3:
- **Consistency**: All nodes see same data
- **Availability**: Every request gets a response
- **Partition Tolerance**: System works despite network failures

Since partitions are inevitable, choose between CP or AP:

**CP Systems (Consistency + Partition Tolerance):**
- HBase, MongoDB (single-master), Redis Cluster
- During partition: May reject writes
- Use case: Banking (can't allow inconsistent balances)

**AP Systems (Availability + Partition Tolerance):**
- Cassandra, DynamoDB, CouchDB
- During partition: Accept writes, resolve conflicts later
- Use case: Social media (likes/views can be eventually consistent)

**Real example:**
- Amazon shopping cart uses AP — always available, even if item counts are briefly inconsistent
- Amazon checkout uses CP — can't allow overselling inventory

### 9. How does consistent hashing work and why is it important for distributed databases?
**Answer:** Consistent hashing maps both data and nodes to a circular hash ring.

**How it works:**
1. Hash each node to a position on the ring
2. Hash each key to a position on the ring
3. Key is stored on the first node clockwise from its position

**Why it matters:**
- Regular hashing: Adding/removing node reshuffles ALL keys
- Consistent hashing: Only K/N keys move (K=keys, N=nodes)

**Virtual nodes:**
- Each physical node has multiple positions on ring
- Improves load distribution
- Handles heterogeneous hardware (powerful nodes get more virtual nodes)

**Used by:** DynamoDB, Cassandra, memcached

### 10. Design a multi-database architecture for an e-commerce platform.
**Answer:**

**Polyglot persistence approach:**

| Data | Database | Reason |
|------|----------|--------|
| Users, Orders | PostgreSQL | ACID for transactions |
| Product Catalog | MongoDB | Flexible schema for varying attributes |
| Sessions, Cart | Redis | Fast, TTL support |
| Product Search | Elasticsearch | Full-text search, faceted filtering |
| Activity Feed | Cassandra | High write throughput |
| Product Images | S3 | Blob storage, CDN integration |
| Analytics | ClickHouse | Fast aggregations |

**Architecture:**
```
User Request → API Gateway
    ├── Product Service → MongoDB + Elasticsearch + S3
    ├── Order Service → PostgreSQL
    ├── Cart Service → Redis
    ├── User Service → PostgreSQL + Redis (cache)
    └── Analytics → ClickHouse
```

**Key considerations:**
- Eventual consistency between search and catalog
- Cache invalidation strategy
- Backup and disaster recovery for each DB
- Data synchronization between systems

---

## Quick Tips for Database Interviews

1. **Know the trade-offs** — Every database decision has pros/cons
2. **Consider access patterns** — How will data be read and written?
3. **Think about scale** — What happens at 10x, 100x current load?
4. **Discuss consistency models** — ACID vs eventual consistency
5. **Real-world examples** — Reference how big companies solved similar problems

## Key Numbers to Remember

| Metric | Value |
|--------|-------|
| SSD random read | 150 μs |
| HDD seek | 10 ms |
| B-tree lookup | O(log n) |
| Hash lookup | O(1) |
| PostgreSQL max connections | ~100-500 typical |
| Redis operations/sec | 100K+ per node |
| Cassandra write throughput | 100K+ per node |


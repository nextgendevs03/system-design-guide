# Database Cheatsheet

## SQL vs NoSQL Quick Reference

```
┌─────────────────────────────────────────────────────────────┐
│  SQL                          │  NoSQL                      │
├─────────────────────────────────────────────────────────────┤
│  Fixed schema                 │  Flexible schema            │
│  ACID transactions            │  BASE (eventual)            │
│  Vertical scaling             │  Horizontal scaling         │
│  Complex JOINs                │  Embedded data/references   │
│  Standardized SQL             │  Various query languages    │
├─────────────────────────────────────────────────────────────┤
│  PostgreSQL, MySQL            │  MongoDB, Redis, Cassandra  │
└─────────────────────────────────────────────────────────────┘
```

## ACID vs BASE

| ACID | BASE |
|------|------|
| Atomicity | Basically Available |
| Consistency | Soft state |
| Isolation | Eventually consistent |
| Durability | |

**ACID** → Banks, inventory, bookings
**BASE** → Social media, analytics, logs

## Database Types

| Type | Best For | Examples |
|------|----------|----------|
| Relational | Transactions, JOINs | PostgreSQL, MySQL |
| Document | Flexible schemas | MongoDB, CouchDB |
| Key-Value | Caching, sessions | Redis, DynamoDB |
| Wide-Column | Time-series, logs | Cassandra, HBase |
| Graph | Relationships | Neo4j, Neptune |
| Time-Series | Metrics, IoT | InfluxDB, TimescaleDB |
| Search | Full-text search | Elasticsearch |

## Database Selection

```
Need ACID?              → PostgreSQL/MySQL
Need caching?           → Redis
Need flexible schema?   → MongoDB
Need high writes?       → Cassandra
Need graph queries?     → Neo4j
Need full-text search?  → Elasticsearch
Need time-series?       → InfluxDB
```

## Index Types

| Type | Use Case | Complexity |
|------|----------|------------|
| B-tree | Range queries, general | O(log n) |
| Hash | Exact matches | O(1) |
| GIN | Full-text, arrays | O(log n) |
| GiST | Geometric data | O(log n) |

## Sharding Strategies

```
Hash-based:   shard = hash(key) % N
              ✅ Even distribution
              ❌ No range queries

Range-based:  A-M → Shard1, N-Z → Shard2
              ✅ Range queries
              ❌ Hotspots possible

Directory:    Lookup table → Shard
              ✅ Flexible
              ❌ Lookup is SPOF
```

## Replication Types

| Type | Writes | Reads | Use Case |
|------|--------|-------|----------|
| Single-Leader | 1 node | All nodes | Most apps |
| Multi-Leader | Multiple | All nodes | Multi-region |
| Leaderless | All nodes | All nodes | High availability |

## CAP Theorem

```
       Consistency
          /\
         /  \
        / CP \
       /______\
      /\      /\
     /AP\    /CA\
    /____\  /____\
 Availability  Partition
```

**CP**: HBase, MongoDB — consistency over availability
**AP**: Cassandra, DynamoDB — availability over consistency

## Quick Sizing

| Data | Estimate |
|------|----------|
| Tweet | ~1 KB |
| User profile | ~5-10 KB |
| Product | ~10-50 KB |
| Image metadata | ~1-5 KB |
| Log entry | ~0.5-2 KB |

## Common Limits

| Database | Typical Limit |
|----------|---------------|
| PostgreSQL connections | 100-500 |
| MySQL row size | 65KB |
| MongoDB document | 16 MB |
| Redis key | 512 MB |
| Elasticsearch document | 100 MB |

---

**#Databases #SystemDesign #DataStorage**


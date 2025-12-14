# System Design Basics - Cheatsheet

## The RESHADE Framework

```
R - Requirements    → What must the system do? How well?
E - Estimation      → Traffic, storage, bandwidth calculations
S - Storage         → Database design, data modeling
H - High Level      → Architecture, components, data flow
A - APIs            → Interface design, endpoints
D - Deep Dives      → Scaling, bottlenecks, trade-offs
E - Edge Cases      → Failures, security, monitoring
```

## Scaling Stages

| Stage | Users | Actions |
|-------|-------|---------|
| 1 | 0-100 | Single server with everything |
| 2 | 100-10K | Separate database |
| 3 | 10K-100K | Add caching layer |
| 4 | 100K-1M | Load balancer + multiple servers |
| 5 | 1M-10M | Database replication |
| 6 | 10M+ | Database sharding |

## Building Blocks

| Component | Purpose | Examples |
|-----------|---------|----------|
| DNS | Domain to IP | Route53, Cloudflare |
| CDN | Cache static content | CloudFront, Akamai |
| Load Balancer | Distribute traffic | Nginx, HAProxy |
| Cache | Fast data access | Redis, Memcached |
| Database | Persistent storage | PostgreSQL, MongoDB |
| Message Queue | Async communication | Kafka, RabbitMQ |
| Object Storage | Files/media | S3, GCS |

## Latency Numbers Every Programmer Should Know

| Operation | Latency |
|-----------|---------|
| L1 cache reference | 0.5 ns |
| Main memory reference | 100 ns |
| SSD random read | 150 μs |
| Network round trip (datacenter) | 0.5 ms |
| Network round trip (cross-continent) | 150 ms |
| Read 1 MB from memory | 0.25 ms |
| Read 1 MB from SSD | 1 ms |
| Read 1 MB from disk | 20 ms |

## CAP Theorem

```
       Consistency
          /\
         /  \
        /    \
       /  CP  \
      /________\
     /\        /\
    /  \  CA  /  \
   / AP \    /    \
  /______\  /______\
Availability  Partition
              Tolerance

You can only pick 2 out of 3!
```

## Quick Estimations Template

```
Daily Active Users (DAU): ___
Actions per user per day: ___
Total daily actions: DAU × actions = ___

Requests per second: daily_actions / 86400 = ___
Peak multiplier: 2-3x average

Storage per action: ___ bytes
Daily storage: actions × size = ___
Yearly storage: daily × 365 = ___
```

## Horizontal vs Vertical Scaling

| Vertical (Scale Up) | Horizontal (Scale Out) |
|---------------------|------------------------|
| More powerful machine | More machines |
| Limited by hardware | Virtually unlimited |
| Simple | Complex |
| Single point of failure | Distributed |
| Example: 8GB → 64GB | Example: 1 → 10 servers |

---

**#SystemDesign #CheatSheet #TechInterviews**


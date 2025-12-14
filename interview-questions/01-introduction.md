# Interview Questions: Chapter 01 - Introduction to System Design

## Easy Questions

### 1. What is system design?
**Answer:** System design is the process of defining the architecture, components, modules, interfaces, and data flow of a system to satisfy specified requirements. It involves making decisions about how different parts of a software system work together to achieve business goals while meeting non-functional requirements like scalability, reliability, and performance.

### 2. What is the difference between HLD and LLD?
**Answer:**
- **HLD (High Level Design):** Focuses on the overall system architecture, major components, data flow, and how different modules interact. It answers "what" and "where" questions.
- **LLD (Low Level Design):** Focuses on the detailed implementation of individual components, including class diagrams, database schemas, and algorithms. It answers "how" questions.

### 3. What are functional and non-functional requirements?
**Answer:**
- **Functional requirements:** What the system should do (e.g., user can create an account, post content, search items)
- **Non-functional requirements:** How well the system should perform (e.g., response time < 200ms, 99.99% uptime, support 1M concurrent users)

---

## Medium Questions

### 4. Explain horizontal vs vertical scaling with examples.
**Answer:**
- **Vertical Scaling (Scale Up):** Adding more power to existing machines (more RAM, CPU). Example: Upgrading database server from 16GB to 64GB RAM.
  - Pros: Simple, no code changes
  - Cons: Hardware limits, single point of failure

- **Horizontal Scaling (Scale Out):** Adding more machines to the pool. Example: Going from 1 web server to 10 web servers behind a load balancer.
  - Pros: Virtually unlimited, better fault tolerance
  - Cons: More complex, needs stateless design

### 5. What is a single point of failure and how do you avoid it?
**Answer:** A single point of failure (SPOF) is a component whose failure would bring down the entire system. To avoid SPOFs:
- Add redundancy at every layer (multiple servers, databases, load balancers)
- Use database replication (master-replica)
- Deploy across multiple availability zones
- Implement health checks and automatic failover

### 6. What is the CAP theorem?
**Answer:** CAP theorem states that a distributed system can only guarantee 2 of 3 properties:
- **Consistency:** All nodes see the same data at the same time
- **Availability:** Every request receives a response
- **Partition Tolerance:** System continues to operate despite network partitions

Since network partitions are inevitable, systems must choose between CP (consistency + partition tolerance) or AP (availability + partition tolerance).

---

## Hard Questions

### 7. How would you design a system that scales from 100 users to 10 million users?
**Answer:** Progressive scaling approach:

1. **0-100 users:** Single server with application and database
2. **100-10K users:** Separate database server, add caching (Redis)
3. **10K-100K users:** Add load balancer, multiple app servers
4. **100K-1M users:** Database read replicas, CDN for static content
5. **1M-10M users:** Database sharding, microservices architecture, message queues for async processing

Key considerations at each stage:
- Monitor and identify bottlenecks before scaling
- Cache aggressively to reduce database load
- Use queues to handle traffic spikes
- Design stateless services for easy horizontal scaling

### 8. Describe the RESHADE framework for system design interviews.
**Answer:**
- **R - Requirements:** Gather functional and non-functional requirements
- **E - Estimation:** Calculate traffic, storage, and bandwidth needs
- **S - Storage:** Design data models and choose appropriate databases
- **H - High Level Design:** Create architecture diagram with major components
- **A - APIs:** Define interfaces and endpoints
- **D - Deep Dives:** Discuss scaling strategies, bottlenecks, trade-offs
- **E - Edge Cases:** Handle failures, security, monitoring

---

## Quick Tips for Interviews

1. Always clarify requirements before designing
2. Think out loud - show your reasoning process
3. Start with high-level design, then dive deep into specific areas
4. Discuss trade-offs for every decision
5. Know your numbers (latency, throughput, storage estimates)
6. Consider failure scenarios and how to handle them


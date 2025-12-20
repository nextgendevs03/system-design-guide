# LinkedIn Carousel: Data Storage Fundamentals

> 📐 Format: 1080 x 1080 | Slides: 10

---

## Slide 1: Cover

**Visual**: Database icons (SQL, NoSQL logos)

**Text**:
```
💾 DATABASE GUIDE

SQL vs NoSQL
ACID vs BASE
Which Database When?

Your complete guide 👇

[Swipe →]
```

---

## Slide 2: The Big Question

**Visual**: Fork in the road

**Text**:
```
SQL or NoSQL?

Wrong question ❌

Right question ✅:
"What are my access patterns?"

• Need transactions? → SQL
• Need flexibility? → NoSQL
• Need both? → Use both!

Netflix uses 6+ database types.
```

---

## Slide 3: SQL Databases

**Visual**: Table structure

**Text**:
```
SQL DATABASES 📊

Structured data in tables:

┌────┬─────────┬───────────┐
│ ID │ Name    │ Email     │
├────┼─────────┼───────────┤
│ 1  │ Alice   │ a@mail    │
│ 2  │ Bob     │ b@mail    │
└────┴─────────┴───────────┘

✅ ACID transactions
✅ Complex JOINs
✅ Data integrity

PostgreSQL, MySQL, SQLite
```

---

## Slide 4: NoSQL Types

**Visual**: 4 types illustrated

**Text**:
```
4 TYPES OF NoSQL

📄 Document
   MongoDB, CouchDB
   Flexible JSON-like docs

🔑 Key-Value
   Redis, DynamoDB
   Fast lookups

📊 Wide-Column
   Cassandra, HBase
   High write throughput

🔗 Graph
   Neo4j, Neptune
   Relationship-heavy
```

---

## Slide 5: ACID vs BASE

**Visual**: Scale/balance

**Text**:
```
ACID vs BASE

ACID (SQL):
A - Atomicity (all or nothing)
C - Consistency (always valid)
I - Isolation (no interference)
D - Durability (survives crash)

BASE (NoSQL):
BA - Basically Available
S  - Soft state
E  - Eventually consistent

Banking? ACID.
Social media likes? BASE.
```

---

## Slide 6: When to Use What

**Visual**: Decision boxes

**Text**:
```
CHOOSE YOUR DATABASE

💰 Money/Transactions
   → PostgreSQL, MySQL

📝 Flexible Schema
   → MongoDB

⚡ Caching/Sessions
   → Redis

📈 High Write Volume
   → Cassandra

🔍 Full-Text Search
   → Elasticsearch

👥 Social Graph
   → Neo4j
```

---

## Slide 7: Real-World Examples

**Visual**: Company logos

**Text**:
```
WHAT BIG TECH USES

Discord:
MongoDB → Cassandra
(Billions of messages)

Uber:
MySQL + Schemaless
(Flexible at scale)

Netflix:
Cassandra + MySQL + ES
(Different DBs for different needs)

One size doesn't fit all.
```

---

## Slide 8: Indexing 101

**Visual**: Before/after speed

**Text**:
```
DATABASE INDEXES ⚡

Without index:
Full table scan → O(n) 🐌

With index:
B-tree lookup → O(log n) ⚡

Add indexes on:
✅ WHERE columns
✅ JOIN columns
✅ ORDER BY columns

But don't over-index!
(Slows down writes)
```

---

## Slide 9: Polyglot Persistence

**Visual**: Multiple databases connected

**Text**:
```
POLYGLOT PERSISTENCE

Use MULTIPLE databases:

E-commerce example:
┌─────────────────────────┐
│ PostgreSQL → Orders    │
│ Redis → Sessions       │
│ Elasticsearch → Search │
│ S3 → Images           │
│ Cassandra → Activity   │
└─────────────────────────┘

Right tool for each job.
```

---

## Slide 10: CTA

**Text**:
```
DATABASE SELECTION CHECKLIST:

✅ Define access patterns
✅ Consider consistency needs
✅ Plan for scale
✅ Don't be afraid to mix

📚 Follow for more
💾 Save this guide
🔗 Full chapter in bio

What's your favorite database?
```

---

## 📝 Caption

```
💾 SQL vs NoSQL? Wrong question.

The RIGHT question: "What are my access patterns?"

Here's how to choose:

→ Need ACID transactions? PostgreSQL, MySQL
→ Need flexible schema? MongoDB
→ Need blazing fast cache? Redis
→ Need to handle millions of writes? Cassandra
→ Need full-text search? Elasticsearch
→ Need to traverse relationships? Neo4j

The truth? Most production systems use MULTIPLE databases.

This is called Polyglot Persistence:
• Netflix: 6+ database types
• Uber: MySQL + Cassandra + Redis
• Discord: Migrated MongoDB → Cassandra

One size doesn't fit all.

Save this guide for your next architecture decision! 🔖

What database do you use most?
1️⃣ PostgreSQL
2️⃣ MySQL
3️⃣ MongoDB
4️⃣ Redis
5️⃣ Other (comment!)

#Database #SQL #NoSQL #PostgreSQL #MongoDB #Redis #SystemDesign #SoftwareEngineering #Backend
```


# NoSQL: Basic to Advanced

Read these first; this file adds only what they don't cover:

- [SQL and NoSQL questions](questions.md), NoSQL section: when to use NoSQL, SQL vs NoSQL, foreign keys, ACID, BASE
- [Java questions](../java/questions.md): Redis for distributed caching, sessions and locks

## Basic

1. What kinds of NoSQL databases are there?
   - Document (MongoDB), key-value (Redis, DynamoDB), wide-column (Cassandra), graph (Neo4j), search (Elasticsearch).
2. MongoDB: embed vs reference?
   - Embed data you read together and that stays bounded. Reference data that grows without limit or is shared.
3. Which Redis data types do you know and what is each for?
   - String (cache, counters), hash (objects), list (queues), set (unique members), sorted set (leaderboards, timelines), stream (event log).
4. What does schemaless mean in practice?
   - The database doesn't enforce a schema, so the app must. Use schema validation or a typed ODM.

## Intermediate

1. How do compound indexes work in MongoDB? What is the ESR rule?
   - Order fields as Equality, then Sort, then Range.
2. Write an aggregation pipeline with `$match`, `$group` and `$lookup`.
3. Are MongoDB writes atomic? When do you need multi-document transactions?
   - A single-document write is atomic. Multi-document transactions exist but cost more; design documents to avoid them.
4. Write concern and read concern in MongoDB?
   - `w: "majority"` waits until most replicas have the write. Read concern `majority` reads only data that can't be rolled back.
5. Cache-aside vs write-through vs write-behind?
6. How do you prevent a cache stampede?
   - A lock or single flight on a miss, early refresh, and jittered TTLs.
7. Redis persistence: RDB vs AOF?
8. What are the limits of a Redis lock?
   - `SET key token NX PX 30000`, release only if the token matches (Lua). A GC pause can outlive the TTL, so use fencing tokens when correctness depends on it.
9. Which Redis eviction policy for a pure cache?
   - `allkeys-lru` or `allkeys-lfu`; `noeviction` when Redis holds data you can't lose.
10. Cassandra: partition key vs clustering key?
    - The partition key picks the node; clustering keys sort rows inside the partition. Model one table per query.

## Advanced

1. Explain CAP and PACELC with real databases.
   - During a partition, choose consistency or availability. Otherwise, choose latency or consistency.
2. Tunable consistency in Cassandra: what does `QUORUM` for reads and writes give you?
   - With R + W > N, a read overlaps the latest write.
3. How does consistent hashing work and why use virtual nodes?
4. What is a hot partition and how do you fix it?
   - One key gets most of the traffic. Add a random or time suffix to the key, cache it, or split the entity.
5. DynamoDB single-table design: what is it and when does it hurt?
   - All entities in one table with composite keys and GSIs, designed for known access patterns. Hard to change for new queries.
6. Redis Cluster: how are keys spread and what breaks multi-key commands?
   - 16,384 hash slots. Keys in one command must share a slot; use hash tags like `{user:1}:feed`.
7. How do you keep a cache consistent with the database?
   - Delete the cache entry after the DB commit, use short TTLs, or update the cache from change data capture.
8. MongoDB sharding: how do you choose a shard key?
   - High cardinality, even writes, and queries that include the key. Avoid monotonically increasing keys for writes.
9. When would you add Elasticsearch next to your main database, and how do you keep it in sync?

## Scenario

1. Redis memory is full and the app starts failing. What do you check and change?
2. A MongoDB collection has documents that grew to several megabytes and queries slow down. How do you remodel it?
3. Design the storage for a URL shortener that serves 100,000 reads a second.
4. Your team wants to move from Postgres to MongoDB "for scale". How do you evaluate it?

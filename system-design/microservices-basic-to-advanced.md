# Microservices and System Design: Basic to Advanced

Read these first; this file adds only what they don't cover:

- [System design questions](questions.md): HTTP, REST, gateways, auth, circuit breaker, pagination, Saga failure, design case studies
- [Microservices design patterns](micro-services.md): decomposition, integration, database, observability, resiliency, deployment patterns
- [Senior developer topics](senior-dev.md): CAP, outbox, CDC, DLQ, SLOs, trade-offs
- [Java questions](../java/questions.md): microservice communication and observability

## Basic

1. L4 vs L7 load balancer?
   - L4 routes TCP connections by IP and port. L7 reads HTTP, so it can route by path, header or cookie.
2. Kafka basics: topics, partitions, consumer groups and offsets. How is order kept?
   - Order is kept per partition, so use the entity id as the message key.
3. What is idempotency and why does at-least-once delivery need it?

## Intermediate

1. How do you query data that lives in three services?
   - API composition for small reads, or a read model built from their events for heavy or joined reads.
2. How do you roll back a saga step whose compensation also fails?
   - Retry the compensation until it succeeds (it must be idempotent), alert after N tries, and keep the saga state for manual repair.
3. Rate limiting algorithms: fixed window, sliding window, token bucket, leaky bucket. Which allows bursts?
   - Token bucket allows bursts up to the bucket size; leaky bucket smooths output.
4. Caching layers: CDN, gateway, application, database. Where do you cache what?
5. How do you increase Kafka consumer throughput?
   - More partitions and consumers (up to one per partition), batch processing, and async commits after processing.

## Advanced

1. How do you design idempotency end to end?
   - Idempotency keys on APIs, unique constraints, dedupe tables for consumers, and conditional updates.
2. How do you version events without breaking consumers?
   - Additive changes only, a schema registry with compatibility rules, and a new topic or version for breaking changes.
3. How do you estimate capacity for 10 million daily users?
   - Requests per second, peak factor, storage per day, bandwidth, then servers and DB size. See the estimation section in [logical questions](../logical/logical-basic-to-advanced.md).
4. Multi-region active-active: what data conflicts appear and how do you resolve them?
   - Concurrent writes to the same record. Use last-write-wins, CRDTs, or route each user's writes to a home region.
5. How do you prevent a retry storm?
   - Exponential backoff with jitter, retry budgets, retry only at one layer, and circuit breakers.

## Design questions

1. Design a news feed (fan-out on write vs on read, celebrity users).
2. Design a ticket booking system that never double-books a seat.
3. Design a leaderboard for millions of players.
4. Design a distributed unique id generator.
5. Design a distributed job scheduler.

## Scenario

1. An order is paid but stock was never reserved. How do you find and fix the inconsistency?
2. Kafka consumer lag keeps growing. What do you check?
3. After a deploy, one service's error rate rises to 5%. Walk through your rollback decision.

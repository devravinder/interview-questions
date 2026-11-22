# Spring Boot: Basic to Advanced

Read these first; this file adds only what they don't cover:

- [Java questions](questions.md): Spring MVC, Spring Boot, auto-configuration, JPA queries, Spring Security, microservices, observability
- [Memory management](memory-management.md): beans, pools, caches and threads in Spring Boot
- [Mock interview](mock-interview.md), [Tech lead mock interview](techlead-mock-interview.md) and [Sr Java FS](sr.java-fs.md)

## Basic

1. Constructor vs field vs setter injection? Which do you prefer?
   - Constructor injection: required dependencies are explicit, fields can be `final`, and tests need no reflection.
2. `@RequestParam` vs `@PathVariable` vs `@RequestBody`?
3. How do you validate request input?
   - `@Valid` with Jakarta Bean Validation annotations, a custom `ConstraintValidator`, and groups for create vs update.
4. What is `ProblemDetail`?
   - The RFC 9457 error body that Spring returns from `@RestControllerAdvice` handlers.

## Intermediate

1. Why does `@Transactional` not work when a method calls another method in the same class?
   - Transactions are applied by a proxy, and a self-call skips the proxy. Move the method to another bean.
2. Which exceptions roll back a transaction by default?
   - Unchecked exceptions and errors. Checked exceptions commit unless you set `rollbackFor`.
3. `REQUIRED` vs `REQUIRES_NEW` propagation? When do you need `REQUIRES_NEW`?
   - For example, an audit row that must be saved even when the main transaction rolls back.
4. Optimistic vs pessimistic locking in JPA?
   - `@Version` fails on conflict at commit. `PESSIMISTIC_WRITE` takes `SELECT ... FOR UPDATE`.
5. `RestTemplate` vs `WebClient` vs `RestClient` vs `@HttpExchange` interfaces?
   - `RestClient` is the modern blocking client. `WebClient` is reactive. `@HttpExchange` generates a client from a Java interface.
6. Which Actuator endpoints do you expose in production?
   - health (with liveness and readiness groups), info, metrics, prometheus. Keep env, heapdump and the rest private.

## Advanced

1. How do you configure an OAuth2 resource server for JWTs?
   - `oauth2ResourceServer().jwt()`, check issuer, audience and signature through the JWKS URL, and map scopes or roles to authorities.
2. What changed in Spring Boot 3 and 4?
   - Boot 3: Jakarta EE namespace, Java 17 baseline, native images, Micrometer Observation.
   - Boot 4: Spring Framework 7, Jackson 3, modular starters, built-in API versioning, `@HttpExchange` client groups.
3. How do virtual threads change a Spring MVC app?
   - `spring.threads.virtual.enabled=true` runs requests on virtual threads, so blocking I/O no longer needs a large Tomcat pool.
   - The database connection pool becomes the real limit.
4. Spring MVC vs WebFlux: when would you choose WebFlux today?
   - Streaming, many long-lived connections, or a fully non-blocking stack. With virtual threads, MVC covers most other cases.
5. How do you reduce startup time and memory?
   - Lazy init, fewer starters, class data sharing (AppCDS), GraalVM native image, CRaC.

## Scenario

1. After a release, the connection pool is exhausted and requests time out. How do you find the cause?
2. A payment API is called twice by a client retry and charges twice. How do you make it idempotent?
3. You need to split a Spring monolith into services. What do you extract first and how do you share data during the move?
4. A JPA entity update silently overwrites another user's change. What happened and how do you prevent it?

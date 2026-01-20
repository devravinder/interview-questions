# 🧩 Microservices Design Patterns

## 1. Decomposition Patterns

* `By Business Capability` → Services align with domain areas (e.g., Payments, Orders, Inventory).
* `By Subdomain (DDD)` → Use *Domain-Driven Design* to identify bounded contexts.
* `Strangler Fig Pattern` → Gradually replace monolith pieces with microservices.

---

## 2. Integration Patterns

* `API Gateway` → Single entry point for clients, routes to services.
* `Aggregator` → One service calls multiple others and aggregates results.
* `Proxy` → Gateway just forwards requests, adds security, throttling.
* `Chained Service Calls` → Service → Service → Service (can get risky with latency).
* `Asynchronous Messaging` → Use queues/events (Kafka, RabbitMQ) to decouple services.

---

## 3. Database Patterns

* `Database per Service` → Each service owns its data (most common).
* `Shared Database` → Multiple services share one DB (not recommended, but sometimes practical).
* `Saga Pattern` → Distributed transaction management via events/compensating actions.
* `CQRS (Command Query Responsibility Segregation)` → Separate read/write models for performance.
* `Event Sourcing` → Store state as a series of events instead of just final state.

---

## 4. Observability Patterns

* `Log Aggregation` → Centralized logs (ELK, Loki).
* `Distributed Tracing` → Trace requests across services (Jaeger, Zipkin, Tempo).
* `Health Check API` → Each service exposes `/health` for monitoring.
* `Metrics Aggregation` → Collect metrics (Prometheus + Grafana).

---

## 5. Resiliency Patterns

* `Circuit Breaker` → Stop calls to failing service (e.g., Resilience4j, Hystrix).
* `Retry Pattern` → Retry failed calls with backoff.
* `Timeout Pattern` → Don’t let one service hang others.
* `Bulkhead` → Isolate failures so one service doesn’t crash the system.
* `Fail-Fast` → Quickly reject if downstream is not available.
* `Fallback` → Provide default response when service fails.

---

## 6. Security Patterns

* `Access Token (JWT, OAuth2)` → Secure service-to-service & client calls.
* `API Gateway Authentication` → Central place for auth.
* `Service Mesh (Istio, Linkerd)` → Handles mTLS, auth, rate limiting at infra level.

---

## 7. Deployment Patterns

* `Blue-Green Deployment` → Switch traffic between two environments.
* `Canary Release` → Gradually roll out new versions.
* `Sidecar Pattern` → Extra container alongside a service (e.g., Envoy proxy).
* `Service Mesh` → Offload cross-cutting concerns (security, retries, tracing).

---

✅ These patterns are often `combined` in real-world microservices systems depending on business needs, scalability, and reliability.

---

## ⚓ Bulkhead Pattern (Resiliency)

### 📌 What It Is

The `Bulkhead pattern` is a resiliency design pattern that `isolates failures` in a system so that when one part fails, it doesn’t bring down everything else.

It’s inspired by ships:

* A ship has *bulkheads* (partitions) so if one compartment floods, the others stay safe.
* Similarly, in microservices, you isolate resources so a failure in one area won’t sink the entire system.

---

### 🛠 How It Works

* Allocate `separate resources` (threads, DB connections, memory pools) per service or per feature.
* If one service gets overloaded, it `only consumes its own quota`, not the entire pool.
* Prevents a "noisy neighbor" problem where one service hogs resources and starves others.

---

### ✅ Example

Imagine an `e-commerce app` with:

* `Payment Service`
* `Order Service`
* `Notification Service`

If the `Payment Service` suddenly gets slow (maybe the bank API is lagging):

* `Without bulkhead` → all system threads are stuck waiting, and Orders + Notifications also fail.
* `With bulkhead` → only the Payment Service’s thread pool is affected, Orders + Notifications still work.

---

### 🔧 Implementation Approaches

* `Thread pool per service` → Each service gets its own threads.
* `Connection pool isolation` → Separate DB connections per microservice.
* `Rate limiting per service` → Prevent one service from exhausting shared resources.
* `With Circuit Breaker` → Often combined: bulkhead isolates, circuit breaker stops repeated failures.

---

### 📊 Tools & Frameworks

* `Java / Spring Boot` → Use *Resilience4j* bulkhead module (`BulkheadRegistry`).
* `.NET` → *Polly* provides bulkhead policies.
* `Service Mesh (Istio/Linkerd)` → Can enforce isolation & limits at infra level.

👉 `In short:` Bulkhead = *Contain the blast radius of a failure*.

---

## ⚡ Circuit Breaker (Microservices)

**Definition**
`Circuit Breaker` is a resiliency pattern that **stops calling a failing service** to prevent cascading failures and system overload.

---

### 🔁 How It Works (States)

1. **`Closed`**

   * Normal operation
   * Requests flow
   * Failures are monitored

2. **`Open`**

   * Too many failures detected
   * Calls are **blocked immediately**
   * Fallback response is returned

3. **`Half-Open`**

   * After wait time
   * Allows **few test requests**
   * If success → back to `Closed`
   * If failure → back to `Open`

---

### 🎯 Why Use It

* Prevents **system overload**
* Avoids **cascading failures**
* Improves **response time**
* Enables **graceful degradation**

---

### 📌 Example

Order Service → calls → Payment Service

If Payment Service is down:

* Without circuit breaker → Order service keeps retrying → thread pool exhausted
* With circuit breaker → calls blocked → instant fallback → system stays stable

---

### 🔧 Implementation

```java
@CircuitBreaker(name = "paymentCB", fallbackMethod = "fallback")
public String pay() {
    return paymentClient.call();
}

public String fallback(Exception e) {
    return "Payment service unavailable";
}
```

---

### 🛠 Popular Tools

* `Resilience4j` (Java)
* `Hystrix` (Deprecated)
* `Polly` (.NET)
* `Istio / Service Mesh` (infra level)

### 👉 In Short

`Circuit Breaker` = **Fail fast + protect system + auto recovery**

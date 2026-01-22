# Java & Spring Boot Memory Management

## Java Memory Management – Overview

Java manages memory automatically using `Garbage Collection (GC)`.  
JVM divides memory into multiple areas for efficient management.

---

## JVM Memory Areas

### Heap Memory

Stores all objects.

Heap is divided into:

#### Young Generation

Where `new objects` are created.

Parts:

- Eden Space
- Survivor Space (S0, S1)

Object flow:

`Eden → Survivor → Old Generation`

GC Type:

- Minor GC (fast)

---

#### Old Generation

- Stores `long-living objects`
- Objects promoted from Young Gen
- Major GC / Full GC happens here (slow)

---

### Stack Memory

Stores:

- Local variables
- Method calls

Features:

- Each thread has its own stack
- Automatically freed

---

### PermGen (Java 7 and below) ❌

Stored:

- Class metadata
- Static variables
- Constant pool

Problems:

- Fixed size
- `OutOfMemoryError: PermGen`

Removed in Java 8

---

### Metaspace (Java 8+)

Replaced PermGen ✅

Stores:

- Class metadata
- Method info

Features:

- Uses native memory
- Auto grows

Config:

```bash
-XX:MetaspaceSize=128m
-XX:MaxMetaspaceSize=256m
```

---

### Garbage Collectors

Common GCs:

- Serial GC
- Parallel GC
- G1 GC (default)
- ZGC
- Shenandoah

---

### G1 GC (Garbage First)

- Heap divided into `regions`
- Cleans region with most garbage first
- Low pause time
- Best for large applications

Enable:

```bash
-XX:+UseG1GC
```

---

### JVM Memory Configuration

Heap:

```bash
-Xms512m
-Xmx2g
```

Young Generation:

```bash
-Xmn512m
```

Metaspace:

```bash
-XX:MetaspaceSize=128m
-XX:MaxMetaspaceSize=256m
```

---

### Enable GC Logging

```bash
-Xlog:gc
```

---

### Common Memory Problems

- `Memory Leak`

  - Objects not released

- `OutOfMemoryError`

  - Heap full

- `High GC`

  - Too many objects

- `Metaspace OOM`

  - Classloader leak

---

## Spring Boot Memory Management

Spring Boot runs on JVM, so `JVM memory rules apply` plus framework best practices.

---

### Bean Scope Management

- `singleton`

  - Default scope (use carefully)

- `prototype`

  - New instance per request

- `request`

  - Per HTTP request

- `session`

  - Per user session

Avoid storing heavy objects in singleton beans.

---

### Close Resources Properly

Use:

```java
try (InputStream in = ...) {
}
```

Or:

```java
@PreDestroy
public void cleanup() {
   resource.close();
}
```

---

### Database Connection Pool (HikariCP)

```yaml
spring.datasource.hikari:
  maximum-pool-size: 20
  minimum-idle: 5
  idle-timeout: 300000
  max-lifetime: 1800000
```

---

### Cache Management

Use bounded caches:

```java
Caffeine.newBuilder()
   .maximumSize(10000)
   .expireAfterWrite(10, TimeUnit.MINUTES)
```

Avoid:

- Unbounded caches
- Static maps

---

### Thread Management

Do not create threads manually ❌
Use Spring Executor ✅

```java
@Bean
public Executor taskExecutor() {
   ThreadPoolTaskExecutor exec = new ThreadPoolTaskExecutor();
   exec.setCorePoolSize(5);
   exec.setMaxPoolSize(10);
   exec.initialize();
   return exec;
}
```

---

### Avoid Large Objects in Session

```java
HttpSession session; // Avoid big objects
```

---

### File Handling

❌ Load full file in memory
✅ Use streaming

---

### Actuator Monitoring

```yaml
management.endpoints.web.exposure.include=*
```

Monitor:

- heap
- GC
- threads

---

### Spring Boot JVM Tuning

```bash
-Xms1g
-Xmx4g
-XX:+UseG1GC
-XX:MaxMetaspaceSize=256m
```

---

### Docker / Kubernetes Memory

Docker:

```bash
--memory=2g
```

Kubernetes:

```yaml
resources:
  limits:
    memory: "2Gi"
```

---

### Debugging Memory Issues

Tools:

- VisualVM
- JProfiler
- JConsole
- Eclipse MAT

Heap dump:

```bash
jmap -dump:live,format=b,file=heap.hprof <pid>
```

---

### Production Best Practices

✔ Bounded caches
✔ Close resources
✔ No static collections
✔ Proper thread pools
✔ GC logging enabled
✔ Monitor heap
✔ Stream large files
✔ Heap dump on OOM

```bash
-XX:+HeapDumpOnOutOfMemoryError
-XX:HeapDumpPath=/dumps
```

---

## Summary

Java:

- Young Gen → Old Gen
- PermGen ❌ → Metaspace ✅
- G1 GC recommended

Spring Boot:

- Manage beans carefully
- Tune DB pools
- Use bounded caches
- Monitor memory
- Tune JVM

---

## Questions

1. Garbage collection? Types of Garbage collections? How do they work? `*`
   - `Types of GC`
       1. `Serial GC`
            - Single thread
            - Small apps

       2. `Parallel GC`
            - Multi-threaded
            - High throughput

       3. `CMS GC`
            - Low pause time

       4. `G1 GC`
            - Region-based
            - Default (Java 9+)

   - `How GC works`
        1. `Mark` reachable objects
        2. `Sweep` unused objects
        3. `Compact` memory

2. what is Region-based GC

    - `Meaning:`
      - Heap is divided into `small fixed regions`
      - instead of Young/Old generations.

    - Used in:`G1 GC`
    - `How it works:`

    - Each region can be `young / old / free`
    - GC collects `only required regions`
    - Predictable pause time

    `Benefit:`

    - Better memory utilization
    - Low pause time

    ---

    Region-based GC = `GC works on small heap regions` instead of whole heap ✔️

3. what are new improvements in GC after java8

    1. `G1 GC became default` (Java 9)
    → Region-based
    → Predictable pause time

    2. `ZGC` (Java 11+)
    → Ultra-low pause (<10ms)
    → Scalable (TB heap)

    3. `Shenandoah GC`
    → Low latency
    → Concurrent compaction

    4. `Epsilon GC`
    → No GC (testing, performance)

    5. `Better heap management`
    → Improved compaction
    → Less fragmentation

    6. `Improved concurrent GC`
    → Less stop-the-world
    → Better responsiveness

    Post Java8 → `Low latency + scalable + concurrent GCs` ✔️

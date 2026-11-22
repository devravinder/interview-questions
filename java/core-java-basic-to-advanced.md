# Core Java: Basic to Advanced

Read these first; this file adds only what they don't cover:

- [Java questions](questions.md): OOP, String pool, collections, HashMap internals, generics, GC, threads, Java 8 features
- [Memory management](memory-management.md): heap, metaspace, GC types, JVM flags, memory tools
- [New features](new-features.md): Java 8 to 25
- [Mock interview](mock-interview.md) and [Sr Java FS](sr.java-fs.md)

## Basic

1. Why does `ConcurrentHashMap` not allow `null` keys or values when `HashMap` does?
   - `get()` returning `null` would be ambiguous between "missing" and "null", with no safe way to check in between.
2. Fail-fast vs fail-safe iterators?
   - Fail-fast iterators throw `ConcurrentModificationException`. Fail-safe ones (`CopyOnWriteArrayList`, concurrent maps) iterate a snapshot or a weakly consistent view.
3. What are sequenced collections (Java 21)?
   - `getFirst()`, `getLast()`, `reversed()` on `List`, `Deque`, `LinkedHashSet` and `LinkedHashMap`.

## Intermediate

1. Why is `count++` not thread-safe even when `count` is `volatile`?
   - It is read, add, write: three steps. Use `AtomicInteger`, or `LongAdder` when many threads update often.
2. How do you combine `CompletableFuture`s and handle errors and timeouts?
   - `thenCompose` for dependent calls, `thenCombine` / `allOf` for parallel ones, `exceptionally` or `handle` for errors, `orTimeout` or `completeOnTimeout` for limits.
3. When should you not use parallel streams?
   - Small data, blocking I/O, shared mutable state, or when the common `ForkJoinPool` is shared with other work.
4. Rewrite an `if-else instanceof` chain with a sealed interface and pattern matching `switch`. What does the compiler check for you?

   ```java
   sealed interface Payment permits Card, Upi {}
   record Card(String number) implements Payment {}
   record Upi(String id) implements Payment {}

   String describe(Payment p) {
       return switch (p) {
           case Card c -> "card " + c.number();
           case Upi u -> "upi " + u.id();
       }; // no default needed: the compiler knows all subtypes
   }
   ```

5. `ThreadLocal`: how does it leak memory and how do you avoid it?
   - Pool threads never die, so their values stay. Always call `remove()` in a `finally`.

## Advanced

1. How do you debug high CPU or a hung service?
   - Take several thread dumps a few seconds apart (`jcmd <pid> Thread.print`) and look for the same stack or `BLOCKED` threads.
   - Use async-profiler or Java Flight Recorder for flame graphs.
2. What is the Java Memory Model and the happens-before relation?
   - Rules for when one thread's write is visible to another: unlock before lock, volatile write before read, thread start and join.
3. What is virtual thread pinning?
   - A virtual thread inside `synchronized` or a native call can't leave its carrier thread while it blocks. JDK 24 fixed the `synchronized` case.
4. What are structured concurrency and scoped values?
   - Structured concurrency treats a group of subtasks as one unit that fails and cancels together.
   - Scoped values are an immutable, bounded replacement for `ThreadLocal` that suits virtual threads.
5. What is escape analysis?
   - The JIT finds objects that never leave a method and can skip the heap allocation and the locks on them.
6. How do you size a thread pool?
   - CPU-bound: about the number of cores. I/O-bound: cores x (1 + wait time / compute time). Measure, then use a bounded queue with a rejection policy.
7. How do you set JVM memory in a container?
   - `-XX:MaxRAMPercentage` instead of a fixed `-Xmx`, because the JVM reads the container limit.
   - Leave room for metaspace, thread stacks and direct memory, or the pod is OOM-killed.

## Scenario

1. A service's p99 latency jumps every few minutes. GC logs show long pauses. What do you check and change?
2. A batch job processes 10 million rows and runs out of memory. How do you redesign it?
3. Two threads update a shared account balance and money goes missing. Show three ways to fix it and their trade-offs.
4. You migrate a Java 8 codebase to Java 21. What breaks and how do you plan it?

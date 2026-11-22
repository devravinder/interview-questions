# Node.js: Basic to Advanced

Read these first; this file adds only what they don't cover:

- [JavaScript questions](questions.md): Node.js, streams, buffers, EventEmitter, child process vs cluster vs worker threads, BullMQ, npm security

## Basic

1. Is Node.js single-threaded?
   - JavaScript runs on one thread. libuv has a thread pool (4 by default) for file system, DNS lookup, crypto and zlib.
2. How do you enable ES modules in Node?
   - `"type": "module"` in `package.json`, or the `.mjs` extension.
3. `dependencies` vs `devDependencies` vs `peerDependencies`?
4. `npm ci` vs `npm install`?
   - `npm ci` installs exactly the lockfile and fails if it doesn't match `package.json`. Use it in CI.
5. How do you load and check configuration?
   - `process.env`, `node --env-file=.env`, and validate everything at startup so a missing value fails fast.

## Intermediate

1. Explain the event loop phases.
   - timers → pending callbacks → poll (I/O) → check (`setImmediate`) → close callbacks. `process.nextTick` and promise microtasks run between phases.
2. What blocks the event loop, and how do you find it?
   - Sync file or crypto calls, big `JSON.parse`, heavy regex, long loops.
   - Measure with `perf_hooks.monitorEventLoopDelay`, `--cpu-prof` or Clinic.js.
3. What is backpressure? How does `pipeline()` handle it?
   - `write()` returns `false` when the buffer is full; wait for `drain`. `stream.pipeline` handles it and cleans up on errors.
4. How do you handle errors in async code?
   - `try` / `catch` with `await`, never leave a promise unhandled, and log then exit on `unhandledRejection` and `uncaughtException`.
5. How do you shut down gracefully?
   - On `SIGTERM`: stop accepting requests, finish in-flight work, close DB and broker connections, then exit before the kill timeout.
6. How do you upload a large file without loading it in memory?

## Advanced

1. How do you debug a memory leak in Node?
   - Watch RSS and heap used, take heap snapshots (`--heapsnapshot-signal`, Chrome DevTools), compare retained objects.
2. How do you run CPU-heavy work such as image resizing or PDF generation?
   - Worker threads with a pool (Piscina), or a separate service fed by a queue.
3. How does `AsyncLocalStorage` work and what do you use it for?
   - It keeps per-request context (request id, user, trace) across `await` without passing it through every call.
4. What is the libuv thread pool size problem?
   - Many parallel `fs`, `crypto.pbkdf2` or `dns.lookup` calls queue behind 4 threads. Raise `UV_THREADPOOL_SIZE` or use async alternatives.
5. Which recent Node features do you use?
   - `node:test`, `--watch`, `--env-file`, native `fetch`, the permission model (`--permission`), type stripping for TypeScript files.
6. How does Postgres connection pooling behave with many Node instances?
   - Each process has its own pool, so 20 pods x 10 connections = 200. Use PgBouncer or size pools from the DB limit.
7. How do you profile a slow endpoint in production?
   - Tracing (OpenTelemetry) to find the slow span, then `--cpu-prof` or `0x` flame graphs for CPU.
8. How does `http.Agent` keep-alive affect outbound calls?
   - Reusing sockets avoids TCP and TLS handshakes. Without it, high traffic runs out of ports.

## Scenario

1. Response times grow over a day and recover after a restart. What do you check?
2. One endpoint that builds a CSV report makes the whole API slow. How do you fix it?
3. A Node service must process 5,000 messages a second from Kafka. How do you design the consumer?

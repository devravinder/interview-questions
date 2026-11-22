# Express.js: Basic to Advanced

Read these first; this file adds only what they don't cover:

- [JavaScript questions](questions.md), Express.js section: middleware, `next()`, JWT, sessions, cookies, refresh tokens, loggers, Multer, Swagger, transactions, custom middleware

## Basic

1. What kinds of middleware are there?
   - Application, router, error-handling (4 arguments), built-in (`express.json`, `express.static`), third-party.
2. How do you define routes and read route parameters?
   - `app.get('/users/:id', handler)`, then `req.params`, `req.query`, `req.body`.
3. `res.send` vs `res.json` vs `res.end`?
4. What does `express.Router()` give you?
5. Why does the order of `app.use()` calls matter?
   - Middleware runs in the order it was added. Error handlers go last.

## Intermediate

1. How do you write an error-handling middleware?

   ```js
   app.use((err, req, res, next) => {
     req.log?.error(err);
     res.status(err.status ?? 500).json({ title: err.expose ? err.message : 'Internal error' });
   });
   ```

2. How are async errors handled in Express 5 vs Express 4?
   - Express 5 forwards rejected promises to `next(err)`. Express 4 needed a wrapper or `express-async-errors`.
3. How do you validate request bodies?
   - A schema library (Zod, Joi) in a middleware, returning 400 with field errors.
4. Which security middleware do you add?
   - `helmet`, rate limiting, body size limits, `cors` with explicit origins, and `app.disable('x-powered-by')`.
5. How do you add a request id to every log line?
   - Read it from a header or generate one, keep it in `AsyncLocalStorage`, and log through `pino-http`.
6. How do you structure a large Express app?
   - Routes → controllers → services → repositories, one folder per feature, dependencies passed in rather than imported globally.

## Advanced

1. How do you make an endpoint idempotent?
   - Accept an `Idempotency-Key` header, store the key and the response, and replay the stored response on retry.
2. How do you version an API?
   - URL (`/v1`), header or media type. Keep old versions until clients move, and announce the sunset date.
3. How do you stream a large response or send Server-Sent Events?
4. How do you test Express apps?
   - Supertest against the app without opening a port, Testcontainers for the DB.
5. How do you shut down gracefully with keep-alive connections?
   - `server.close()`, then `server.closeIdleConnections()`, with a forced exit timer.
6. Express vs Fastify vs NestJS: when do you choose each?
   - Express: small and flexible. Fastify: faster, with schema validation built in. NestJS: structure and DI for big teams.

## Scenario

1. A memory leak appears after you added a caching middleware. How do you find it?
2. Some requests hang forever and never respond. What are the usual causes in Express?
3. Design the middleware stack for a public API with auth, rate limits, validation and audit logging.

# NestJS: Basic to Advanced

NestJS is not covered in the older notes. For Express basics, which NestJS runs on, see the Express.js section of [JavaScript questions](questions.md).

## Basic

1. What is NestJS and how does it relate to Express or Fastify?
   - A framework with modules and DI that runs on an HTTP adapter, Express by default or Fastify.
2. What are modules, controllers and providers?
3. How does dependency injection work in NestJS?
   - Providers are registered in a module and injected by constructor type or a token.
4. What do `@Injectable()`, `@Controller()`, `@Get()`, `@Body()`, `@Param()` do?
5. What are DTOs and how do you validate them?
   - Classes with `class-validator` decorators and a global `ValidationPipe({ whitelist: true, transform: true })`.
6. How do you read configuration? (`@nestjs/config` with a validated schema)
7. How do you share a provider between modules?
   - Add it to `exports` in its module and import that module.

## Intermediate

1. Explain the request lifecycle.
   - Middleware → guards → interceptors (before) → pipes → handler → interceptors (after) → exception filters.
2. Middleware vs guard vs interceptor vs pipe vs filter: what is each for?
   - Middleware: raw request. Guard: allow or deny. Interceptor: wrap the call (logging, caching, mapping). Pipe: validate and transform input. Filter: map errors to responses.
3. How do you implement role-based access?

   ```ts
   @Injectable()
   export class RolesGuard implements CanActivate {
     constructor(private reflector: Reflector) {}

     canActivate(ctx: ExecutionContext): boolean {
       const roles = this.reflector.get<string[]>('roles', ctx.getHandler()) ?? [];
       const user = ctx.switchToHttp().getRequest().user;
       return roles.length === 0 || roles.some((r) => user?.roles?.includes(r));
     }
   }
   ```

4. Provider scopes: default, request and transient. What is the cost of request scope?
   - Request scope bubbles up the injection chain and creates instances per request, which costs performance.
5. Custom providers: `useClass`, `useValue`, `useFactory`, `useExisting`.
6. What are dynamic modules (`forRoot`, `forRootAsync`, `register`)?
7. How do you handle circular dependencies?
   - `forwardRef()`, but first try to move the shared logic into a third provider.
8. How do you use TypeORM or Prisma with NestJS? How do you run code in a transaction?
9. How do you write unit tests with `Test.createTestingModule` and override providers?

## Advanced

1. How do NestJS microservices work? Which transports are there?
   - `@MessagePattern` (request and reply) and `@EventPattern` (fire and forget) over TCP, Redis, NATS, Kafka, RabbitMQ, gRPC.
2. How do you consume Kafka in NestJS and handle retries and a dead-letter topic?
3. How do you implement CQRS with `@nestjs/cqrs`?
   - Commands and handlers change state, queries read, events trigger side effects in sagas.
4. How do you add request context (request id, tenant) without request-scoped providers?
   - `AsyncLocalStorage`, for example through `nestjs-cls`.
5. How do you build a multi-tenant API?
   - Tenant from the token or subdomain, then schema per tenant, database per tenant, or a `tenant_id` column with row-level security.
6. How do you cache responses and invalidate them?
   - `CacheInterceptor` with a Redis store, explicit keys, and eviction on writes.
7. How do you run background jobs? (BullMQ with `@nestjs/bullmq`, `@nestjs/schedule`)
8. How do you generate OpenAPI docs and keep them in sync? (`@nestjs/swagger` CLI plugin)
9. How do you handle graceful shutdown? (`app.enableShutdownHooks()`, `onApplicationShutdown`)
10. Express adapter vs Fastify adapter: what changes in your code?

## Scenario

1. A NestJS app gets slow after a developer made the logger provider request-scoped. Why?
2. Design a module layout for an e-commerce backend with users, orders, payments and notifications.
3. Two modules import each other and the app fails to start. How do you fix the design?

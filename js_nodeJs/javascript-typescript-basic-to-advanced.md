# JavaScript and TypeScript: Basic to Advanced

Read these first; this file adds only what they don't cover:

- [JavaScript questions](questions.md): hoisting, `this`, closures, promises, event loop, modules, prototypes
- [React questions](react/questions.md): debounce vs throttle

## Basic

1. What are the primitive types?
   - string, number, bigint, boolean, undefined, null, symbol. Everything else is an object.
2. `null` vs `undefined`?
3. Spread vs rest, and destructuring with defaults.
4. `map`, `filter`, `reduce`, `find`, `some`, `every`: what does each return?
5. Shallow copy vs deep copy? How do you deep copy today?
   - Spread and `Object.assign` are shallow. `structuredClone()` makes a deep copy.

## Intermediate

1. What does this print and why?

   ```js
   console.log(1);
   setTimeout(() => console.log(2), 0);
   Promise.resolve().then(() => console.log(3));
   console.log(4);
   // 1 4 3 2: microtasks run before the next timer
   ```

2. `Promise.all` vs `allSettled` vs `race` vs `any`?
   - `all` fails on the first rejection, `allSettled` never fails, `race` takes the first settled, `any` takes the first fulfilled.
3. TypeScript: `interface` vs `type`?
   - Interfaces merge declarations and are extended with `extends`. Types support unions, mapped and conditional types.
4. `any` vs `unknown` vs `never`?
   - `unknown` must be narrowed before use. `never` is a value that can't exist, useful for exhaustive checks.
5. What are type guards and discriminated unions?

   ```ts
   type Result = { ok: true; data: string } | { ok: false; error: Error };

   function show(r: Result) {
     if (r.ok) return r.data; // narrowed to the success branch
     return r.error.message;
   }
   ```

6. Utility types: `Partial`, `Required`, `Pick`, `Omit`, `Record`, `ReturnType`, `Awaited`.

## Advanced

1. How do memory leaks happen in JavaScript?
   - Forgotten timers and listeners, growing global caches, closures holding large objects, detached DOM nodes.
2. `WeakMap` and `WeakRef`: when do you use them?
   - To attach data to objects without stopping them from being garbage collected.
3. How does V8 optimise code?
   - Hidden classes and inline caches. Changing object shapes or mixing types in hot code causes deoptimisation.
4. Conditional types: explain `infer`.

   ```ts
   type ElementOf<T> = T extends readonly (infer E)[] ? E : never;
   type A = ElementOf<string[]>; // string
   ```

5. Mapped types with key remapping: build a type that turns `{ name: string }` into `{ getName(): string }`.
6. What is `satisfies` and how is it different from a type annotation?
   - It checks a value against a type but keeps the narrower inferred type.
7. How do you share types between a NestJS backend and a React frontend?
   - A shared package in a monorepo, or generate types from OpenAPI or a schema library such as Zod.
8. Structural typing: what problem does it cause and what are branded types?
   - `UserId` and `OrderId` are both `string`, so they mix up. A brand like `string & { __brand: 'UserId' }` keeps them apart.

## Scenario

1. A page freezes when it loads a large JSON list. How do you find and fix it?
2. A team wants to move a large JavaScript codebase to strict TypeScript. How do you plan it without stopping feature work?
3. An API returns data that doesn't match its TypeScript type at run time. How do you guard against it?

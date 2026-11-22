# React: Basic to Advanced

Read these first; this file adds only what they don't cover:

- [React questions](questions.md): virtual DOM, keys, props and state, hooks, Context vs Redux, optimisation, error boundaries, portals, CORS, CSRF, XSS, forms
- [Sr Java FS](../../java/sr.java-fs.md), React section: `useState` vs `useRef`, component vs custom hook

## Basic

1. Why is a state update not visible on the next line, and when do you use the updater form?
   - Updates are batched and applied on the next render. Use `setCount((c) => c + 1)` when the new value depends on the old one.
2. What is JSX compiled to?
   - Calls to the JSX runtime (`jsx('div', props)`), which return plain element objects.
3. When does a component re-render?
   - Its state changes, its parent re-renders, or a context it reads changes.

## Intermediate

1. Why do you see stale closures in effects and handlers? How do you fix them?
   - The function captured old state. Add the value to the dependency array, use the updater form, or read the latest value from a ref.
2. Why does an effect run twice in development?
   - Strict Mode mounts, unmounts and mounts again to expose missing cleanup.
3. `useReducer` vs `useState`: when do you switch?
   - When several values change together or the next state depends on an action type.
4. Server state vs client state: why use TanStack Query or SWR?
   - Caching, deduplication, background refetch, retries and invalidation instead of hand-written effects.
5. How do you render a list of 10,000 rows smoothly?
   - Virtualise it (TanStack Virtual) so only the visible rows are in the DOM.

## Advanced

1. What is the React Compiler and what does it change for `useMemo` and `useCallback`?
   - It memoises components and values at build time, so most manual memoisation is no longer needed.
2. Server Components vs Client Components?
   - Server Components run only on the server, read data directly and ship no JavaScript. Client Components (`'use client'`) handle state and events.
3. CSR vs SSR vs SSG vs ISR: when do you use each?
4. How do you structure a large React codebase?
   - Feature folders, a shared UI library, one layer for API calls, and lint rules for imports.
5. How do you test React components?
   - React Testing Library for behaviour, MSW to mock the API, Playwright for end-to-end flows.
6. How do you make a React app accessible?
   - Semantic HTML first, labels on inputs, keyboard focus handling in modals, and checks with axe.

## Scenario

1. Typing in a search box lags on a page with a big table. How do you fix it?
2. A dashboard makes the same API call five times on load. Why, and how do you fix it?
3. Users see an old version of the app after a deploy. What causes it and how do you fix caching?
4. Plan a migration of a large class-component app to hooks and a newer React version.

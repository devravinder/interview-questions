
# React – Interview Questions & Concepts

This document combines core React concepts, hooks, state management, advanced topics,
and real-world interview questions in a logical progression.

- also refer [React Ts Learn](https://github.com/devravinder/react-ts-learn) for examples

---

## Basics (JavaScript + React Foundations)

- What is hoisting?
- `let` vs `var`
- What is React?
- How is React different from other libraries/frameworks?
- What are the key features of React?
- Virtual DOM vs Real DOM vs Shadow DOM
- How does Virtual DOM improve performance?
- State vs Props
- Can we change props? Will it cause an error?
- Controlled vs Uncontrolled Components
- Why do we need to use `setState` / `useState` instead of normal variables?
- Prop drilling
- How to pass data from child to parent component?
  - Callback functions
  - Centralized state
  - `useImperativeHandle` + `forwardRef`

---

## Components & Rendering

- Class-based vs Functional Components — which is better and why?
- Advantage of Functional Components over Class Components
- What are render props?
  - A function prop that returns JSX
- What are Fragments?
- What are split elements?
- Why do we need `key` while rendering lists?
  - Identifies added/removed/updated elements
  - Enables efficient reconciliation
  - Prevents unnecessary re-renders
- What is reconciliation?
- What happens during the Mounting phase?
- Lifecycle methods
  - `Mounting → Updating → Unmounting`
- How to implement lifecycle methods using hooks?

---

## Hooks

### Core Hooks

- What are hooks?
- `useState`
- `useEffect`
- `useRef`
- `useContext`
- `useReducer`
- `useMemo`
- `useCallback`
- `useLayoutEffect`
- `useImperativeHandle`
- `useSyncExternalStore`
- `useTransition` & `startTransition`
- `useDeferredValue`
- `useFormStatus`
- `useActionState`

---

### `useEffect` vs `useLayoutEffect`

- `useEffect`
  - Runs after render and browser paint
  - Non-blocking
  - Used for data fetching, subscriptions, logging

- `useLayoutEffect`
  - Runs after DOM mutation but before paint
  - Blocking
  - Used for layout measurements and visual calculations

---

### Performance Hooks

- `useMemo`
- `useCallback`
- `useReducer`
- `useRef`
- What is memoization in React?
- What are pure components?
- How to create pure components using hooks?

---

### Special React APIs

- `use`
  - Reads the value of a Promise or context
  - Can be used inside loops or conditionals
- `memo`
- `lazy`
- `Suspense`
- `createContext`

---

## Events & DOM

- `e.target` vs `e.currentTarget`
  - e.target
    - The element that actually triggered the event
    - Deepest element clicked
  - e.currentTarget
    - The element on which the event handler is attached
    - Always the same element

  - eg:

       ```js

            <ul onClick={(e) => console.log(e.target.textContent, e.currentTarget.tagName)}>
            <li>Apple</li>
            <li>Banana</li>
            <li>Cherry</li>
            </ul>
         ```
  - Clicking `Banana`: `target` → `<li>` & `currentTarget` → `<ul>`

- How to handle click events outside a component?

- How to handle events outside target elements?

---

## Context & State Management

- What is Context API?
- How to access context in a component?
- Why do we need state management libraries?
- Why Redux (or similar) instead of Context?

  - Context causes unnecessary re-renders
  - Redux uses subscriptions
- What are actions?
- What are reducers?
- What are dispatchers?
- Where should async logic live — actions or reducers?
- Is Redux async?
- Why do we need middleware like:

  - `redux-thunk`
  - `redux-saga`
- Generator functions (used in saga)
- How to combine multiple middleware?
- How to access Redux state and dispatch in components?

---

## Optimization & Performance

- How to optimize a React app?

  - `React.memo`
  - `useCallback`
  - `useMemo`
  - Lazy loading
  - Code splitting
- Debounce vs Throttling
- Error Boundaries

- Why clear timers on component unmount?

  - Prevent memory leaks

---

## Advanced React

- Portals (`createPortal`)

  - Modals
  - Popups
  - Integrating React into non-React apps
- Hydration in rendering
- Polyfills in React apps
- Webpack configuration in React
- Micro Frontends

---

## Security & Networking

- What is CORS? Where does it occur?
- Authentication & Authorization

  - Token storage
    - Memory / session storage
    - Cookies

- CSRF protection

  - HTTP-only cookies : disables js access
  - SameSite cookies : cookie won't be sent to another site
  - Anti-CSRF tokens
  - Double submit cookie pattern

- XSS prevention

  - CSP headers
  - Sanitization before `dangerouslySetInnerHTML`

---

## Forms & TypeScript

- Experience with TypeScript
- Dynamic forms

  - Libraries:

    - `formIO`
    - `react-hook-form`
    - `tanstack-form`
- Handling re-render issues with large form objects
- Field-level updates

---

## Real-World & Experience-Based

- Challenging tasks you’ve accomplished
- Nginx configuration
- What do you look for during code review?

---

## References

- [https://www.interviewbit.com/react-interview-questions/](https://www.interviewbit.com/react-interview-questions/)
- [https://devhints.io/react](https://devhints.io/react)
- [https://www.simplilearn.com/tutorials/reactjs-tutorial/reactjs-interview-questions](https://www.simplilearn.com/tutorials/reactjs-tutorial/reactjs-interview-questions)
- [https://stackoverflow.com/questions/21965738/what-is-virtual-dom](https://stackoverflow.com/questions/21965738/what-is-virtual-dom)
- [https://kentcdodds.com/blog/prop-drilling](https://kentcdodds.com/blog/prop-drilling)
- [https://github.com/sudheerj/reactjs-interview-questions](https://github.com/sudheerj/reactjs-interview-questions)

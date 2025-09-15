# React

**References:** 
  - [Ref1](https://www.interviewbit.com/react-interview-questions/)
  - [Ref2](https://devhints.io/react)

---

## Core Concepts

- What is React? How is it different from other libraries/frameworks?  
- What are the features of React?
  - [Ref](https://www.simplilearn.com/tutorials/reactjs-tutorial/reactjs-interview-questions)  
- What is Virtual DOM? 
  - [Ref](https://stackoverflow.com/questions/21965738/what-is-virtual-dom)
- Virtual DOM vs Real DOM vs Shadow DOM (Web Components)  
- How does Virtual DOM make React faster? *(Why Virtual DOM > Real DOM)*  
- State vs Props?  
- Prop drilling? 
  - [Ref1](https://kentcdodds.com/blog/prop-drilling)
- How to pass data from child to parent component?  
- Class-based vs Functional Components — which is better and why?  
  > Functional components are better because class components call `super()`, which internally calls all parent lifecycle methods. Functional components don’t.  
- Controlled vs Uncontrolled Components  
- Why do we have to use `setState` to update the state?  
- What are render props?  
- Lifecycle methods (Explain the Component lifecycle)   

---

## Hooks

- What are hooks? 
- `useEffect` vs `useLayoutEffect` 
- `useCallback` vs `useMemo`  
- `useReducer`  
- How to implement lifecycle methods with hooks? *(using `useEffect`)*  
- What are pure components? How to create pure components with hooks?  
- What is `useMemo`?  
- What is memoization in React?  
- What is reconciliation?  
- `React.Suspense` and `lazy()`  
- How to optimize React apps?  
  - `React.memo`, `useCallback`, lazy loading/code splitting (Webpack), iframes for loading, etc.  
- Why do we need to pass the `key` prop when rendering lists?  
- What are split elements?  
- What is a Fragment?  
- Error Boundaries 
- What happens in the Mounting phase?  
- Can we change the props? Will it give an error?  
- Debounce vs Throttling  
- Polyfill in React apps?  
- How to write custom hooks?  
- How to configure pre-configured Webpack settings in React?  
- How do you handle click events outside the target element (React DOM)?  

---

## Context & State Management

- What is Context API?  
- How to access context in a component?  
- Why do we need state management libraries?  
- Why do we need middleware like `redux-thunk` / `redux-saga`?  
- Is Redux async? If yes, why do we need redux-saga when async actions can already be done with Redux?  
- How to combine more than one middleware?  
- Generator functions (used in saga — JavaScript concept)  
- What are actions?  
- What are reducers?  
- What are action dispatchers?  
- Where should asynchronous actions be placed in Redux — actions or reducers?  
- How to access Redux state/dispatchers inside a component?  

---

## Advanced

- Hydration in rendering  

---

# Links

- Interview Qs
  - [Ref1](https://github.com/sudheerj/reactjs-interview-questions)

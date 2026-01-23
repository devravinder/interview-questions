# JavaScript

**Roadmap:**

- [Ref1](https://twitter.com/BendikMatej/status/1567888759865098243?s=20&t=T5OIJQbv8VhUh59GtBZ6Bg)
- [Ref2](https://htmlcheatsheet.com/js/)
- [Ref3](https://github.com/mbeaudru/modern-js-cheatsheet)

---

## Basics

- What is JavaScript?  
- Why is JavaScript called single-threaded? *(One statement at a time)*
  - [Ref](https://medium.com/swlh/what-does-it-mean-by-javascript-is-single-threaded-language-f4130645d8a9)  
- Hoisting?
  - [Ref](https://developer.mozilla.org/en-US/docs/Glossary/Hoisting)  
- `let` vs `var` vs `const`
  - [Ref](https://stackoverflow.com/questions/762011/whats-the-difference-between-using-let-and-var)  
  - **SuGHaR:** Scope, Global Property, Hoisting, Redeclaration  
- Functions vs Arrow Functions?  
  - [Ref](https://dmitripavlutin.com/differences-between-arrow-and-regular-functions/)  
- Explain `this` keyword.
  - [Ref1](https://dmitripavlutin.com/differences-between-arrow-and-regular-functions/)
  - [Ref2](https://www.freecodecamp.org/news/what-is-this-in-javascript/)  
  - [Ref3](https://www.javascripttutorial.net/javascript-this/)
- Higher Order Function (or) Currying?  
- What is a pure function?
- Where does the `this` reference point when a function (or arrow function) is written in global scope?

---

## Async & Event Handling

- What are callbacks?  
- What are event listeners?  
- Promise vs Async–Await?  
- Callback Hell?  
- How to convert callback to promise?  
- Asynchronous and non-blocking calls? Blocking vs synchronous?  
  - [Ref](https://www.codewithc.com/node-js-asynchronous-vs-non-blocking/)
- How to handle multiple asynchronous calls concurrently?  
- Assert in Node.js?  
- What is the need for Promise/Async–Await even though we have callbacks?  
- Event loop: Event Queue
  - [Ref](https://github.com/devravinder/js-learn/blob/master/1_topics/common/4_queues-eventLoop/1_start.js)

---

## Functions & Closures

- What are closures in JavaScript?  
- Coercion? *(Type Coercion)*  
- Symbols?
- Iterators and Generators
- Difference between *iterables* and *enumerables*?
- IIFE (Immediately Invoked Function Expression)?  
- Function Currying  
- Closures — what & when to use?  
- Proxy objects?
- Handling click events outside the target element?  

---

## DOM & Web APIs

- What is DOM?  
- Web Components?
  - [Ref1](https://developer.mozilla.org/en-US/docs/Web/Web_Components)
  - [Ref2](https://developer.mozilla.org/en-US/docs/Web/API/CustomElementRegistry/define)  
- Event Bubbling and Capturing (Event Propagation / Delegation)?
  - [Ref](https://stackoverflow.com/questions/4616694/what-is-event-bubbling-and-capturing)  

---

## Language Features

- `==` vs `===`  
- New ES6 features?  
- Cyclic Dependency Problem?  
- OOPs in JavaScript?  
  - Inheritance: Classical & Prototype
  - Constructor function vs Class  
- `call` vs `bind` vs `apply`  
- Web Storage (LocalStorage, SessionStorage) & IndexedDB  
- Cookies?  
- Functional Programming & its Principles
  - [Ref](https://medium.com/javascript-scene/master-the-javascript-interview-what-is-functional-programming-7f218c68b3a0)  
- Defer vs Async tag in HTML
  - [Ref](https://stackoverflow.com/questions/10808109/script-tag-async-defer)  
- Modeules: CommonJS vs AMD vs RequireJS  
  - [Ref](https://github.com/devravinder/js-learn/blob/master/1_topics/common/16_modules/start.js)

---

## Module Bundlers

- What are Module Bundlers? *(Webpack, Rollup, Parcel, Snowpack, CommonJS)*  
  - Code Splitting in Webpack  
  - Loaders: style-loader, html-loader  
  - Plugins: BundleAnalyzerPlugin, etc.  
  - Dev Server  
  - Hot Module Replacement  

---

## Browser & Networking

- Why does the browser send OPTIONS requests before POST/GET requests?  
- Why do we need `package-lock.json`?
  - [Ref](https://stackoverflow.com/questions/44297803/what-is-the-role-of-the-package-lock-json)  

---

## Node.js

- What is Node.js?  
- `setTimeout` vs `setInterval`  
- `process.nextTick` vs `setImmediate` vs `setTimeout(0)`
- Reactor Pattern in Node.js
  - [Ref1](https://stackoverflow.com/questions/56622353/how-does-reactor-pattern-work-in-node-js)
  - [Ref2](https://www.geeksforgeeks.org/node-js/what-is-reactor-pattern-in-node-js/)  
- What are Streams? Types of Streams?
- Buffers (Streams of binary data)  
- WebSockets
  - [Socket.IO](https://www.npmjs.com/package/socket.io)
  - [Ref1](https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API)
  - [Ref2](https://developer.mozilla.org/en-US/docs/Web/API/WebSockets_API/Writing_WebSocket_client_applications)
  - [Ref3](https://javascript.info/websocket)  
- How to queue tasks?
  - Libraries: Bull / BullMQ  

---

## Processes & Threads

- What is an Event in Node.js?  
- How does EventEmitter work, when should it be used?  
- How to access command line args in Node.js?  
- Parallel Processing
  - [Ref](https://github.com/devravinder/js-learn/tree/master/1_topics/node/16_threads_child-process-_clusters)
  - Child Process vs Clusters vs Worker Threads
  - Fork vs Spawn vs Exec  
  - Cluster module in Node.js
    - [Ref](https://github.com/devravinder/js-learn/blob/master/1_topics/node/16_threads_child-process-_clusters/3_cluster/start.js)  

- Optimizations & scaling: Caching, Scaling, Clusters  
- What are child threads in Node.js?  

---

## Security & Best Practices

- How to ensure npm dependencies are safe?
  - [Ref](https://stackoverflow.com/questions/42679338/how-can-you-make-sure-your-npm-dependencies-are-safe)  
- How to restrict cross-site access to cookies?  
- Side Effects: Ref  

---

## Express.js

- What is Express?  
- What are middlewares?  
- What is `next()`?  
- How to pass data between middlewares?  
- Authentication & Authorization (JWT – structure & algorithm)  
- How to maintain sessions on the server side?  
  - Cookies, Redis cache, express-session, others  
- Secure Cookies  
- Refresh token implementation  
- Database connections: Sequelize, Knex.js, Mongoose, Bookshelf, GooseBird  
- Loggers: Winston, Morgan  
- File Upload: Multer  
- Puppeteer: PDF generation / Headless Chrome  
- Sequelize: relationships, model hooks  
- Knex.js migrations (up & down)  
- API & DB optimizations: Node Clusters, REST optimizations, DB transactions  
- Swagger for API documentation  
- DB transaction management (auto-commit = false, rollback)  
- How to implement custom middleware?  

---

## Links

- TypeScript
  - [Ref1](https://github.com/total-typescript)  
- JavaScript Qs:
  - [Ref1](https://github.com/lydiahallie/javascript-questions)
- JS Ref
  - [Ref1](https://github.com/olivierloverde/minutes-of-javascript)  
- SQLite + React:
  - [Ref](https://riffle.systems/essays/prelude/)  
- SSG vs SSR:
  - [Ref](https://blog.logrocket.com/ssg-vs-ssr-in-next-js/)  

---

## Browser Internals

- How modern browsers work:  
  - [Part 1](https://developer.chrome.com/blog/inside-browser-part1)  
  - [Part 2](https://developer.chrome.com/blog/inside-browser-part2)  
  - [Part 3](https://developer.chrome.com/blog/inside-browser-part3)  
  - [Part 4](https://developer.chrome.com/blog/inside-browser-part4)  

---

## Performance

- How to make websites fast?
  - [Ref](https://twitter.com/vponamariov/status/1432980068716974083?s=20&t=g8RlobMQDRwoF4EYvEyp3g)

# Software Architecture (System Design)

---

## Basic

- HTTP vs HTTPS  
- REST vs SOAP  
- HTTP status codes  
  - 200, 201, 400, 401, 402, 403, 404, 500, 502  
  - 100–199 = informational  
  - 200–299 = success  
  - 300–399 = redirection  
  - 400–499 = client-side errors  
  - 500–599 = server-side errors  
- POST vs PUT vs PATCH?  
- Can we use POST for Delete? If not, why?  
- Why does the browser send **OPTIONS** requests before POST/GET requests?  
- How do you do authentication and authorization?  
- JWT – how does it work? Which encryption algorithm do you use (HS256 / RS256)? 
  - [Ref](https://blog.loginradius.com/engineering/jwt-signing-algorithms/)  
  - What are its advantages over others?  
- What do you use for authentication and authorization? [JWT]  
- How do you maintain the session on the server side? [Redis Cache or other]  
- Which type of API Gateway is being used in your project?  
- CORS? 
- CSRF?  
- Where do you handle exceptions in MVC if an exception comes in the service layer? [Controller or Service?]  
- Multi-tenant architecture?  
- What are microservices?  
- What is an API Gateway in microservices? Types? Which one is used in your app?  
- How do your microservices interact with each other? [JWT token & allowed IPs]  
- How do you do user authentication in different microservices? [JWT & OAuth-OpenID]  
- Circuit breaker in microservices?
  - [Ref](https://microservices.io/patterns/reliability/circuit-breaker.html)  
  - [Ref](https://dzone.com/articles/circuit-breaker-pattern)
- How do you implement pagination in your API?  
- Do you send images/large data in normal GET APIs? If not, how
   - [Image access links]  
- REST API maturity levels? [Maturity Model]  
- Swagger for documentation & OpenAPI specifications  
- Did you use third-party authentication? [Google OAuth, AWS Cognito]  
- Serverless programming? [AWS Lambda, Firebase Functions]  
- Where do you store large files and images? [AWS S3]  
- How do you manage DB transactions? When to use? 
   - Transaction management, ACID principles
- How do you maintain user sessions on the server side? 
   - RedisCache / request session / Cookie
- How do you set a limit for number of API requests? 
  - Store IP & request counts in cache
- How do you make sure only one client uses a JWT token? 
  - Restrict sharing by validating IP address stored in session or JWT
- Why do we use a particular database?  
- Redis Cache – when to use?  
- Elasticsearch – why do we need it?  
- How do you deploy your application?  
- Which version control/source management tools do you use? 
  - GIT  
- How do you use CI/CD?  
- What do you look for in code reviews? 
  - Best Practices

---

## Medium

- Functional Programming 
  - [Ref](https://medium.com/javascript-scene/master-the-javascript-interview-what-is-functional-programming-7f218c68b3a0)  
- Object-Oriented Programming  
  - Principles  
  - SOLID
    - [Ref](https://www.digitalocean.com/community/conceptual_articles/s-o-l-i-d-the-first-five-principles-of-object-oriented-design)

- How HTTP, HTTPS, SSL/TLS work 
  - [Ref](https://www.ibm.com/docs/en/ibm-mq/7.5?topic=ssl-overview-tls-handshake)
  - [Ref2](https://www.cloudflare.com/learning/ssl/how-does-ssl-work/)
  - [Ref3](https://www.digicert.com/how-tls-ssl-certificates-work)  
- HTTP/1, HTTP/1.1, HTTP/2 
  - [Ref](https://cheapsslsecurity.com/p/http2-vs-http1/)  
- REST vs GraphQl vs gRPC 

### Security

- Authentication & Authorization  
  - OAuth2? 
    - Access Token & Id Token, Refresh Token
  - OpenID?  
  - SSO  

---

## Advanced

- When to use Queues vs Multi-threading  
- Pub/Sub usage  
- System Design  

### Case Studies / Implementations

- Snake-Ladder Game (Multi-player)  
  - How to design tables?  
  - Failure checks  
  - User activity/status  
  - Multi-player concurrency  
  - Handling disconnects:  
    - Can the user rejoin?  
    - Timeout & rejoin strategy  

- URL Shortener Implementation  
- Parking Lot Design  
- WhatsApp Design  
- Amazon (E-Commerce) Design  
- Netflix Design  
- Instagram Design  

---

## Links

- [ByteByteGo](https://bytebytego.com/courses/system-design-interview/scale-from-zero-to-millions-of-users)  
- [Tianpan.co](https://tianpan.co/notes/2016-02-13-crack-the-system-design-interview)  
- Solutions Architect
  - [Ref](https://towardsdev.com/solution-architecture-101-are-you-ready-for-the-solution-architect-path-5a2d01aebbb)  
- [Web Architecture](https://medium.com/storyblocks-engineering/web-architecture-101-a3224e126947)  
- [Ref1](https://github.com/donnemartin/system-design-primer)  
- Event Driven Architecture
  - [Ref1](https://banerjeedeep27.medium.com/event-drivenarchitecture-design-patterns-part-01-c81f62254ed7)
  - [McDonalds](https://medium.com/mcdonalds-technical-blog/mcdonalds-event-driven-architecture-the-data-journey-and-how-it-works-4591d108821f)  
- Interview Qs
  - [Qs1](https://faun.pub/top-30-system-design-interview-questions-and-problems-for-programmers-417e89eadd67)
  - [Qs2](https://www.java67.com/2018/05/top-20-system-design-interview-questions-answers-programming.html)
  - [Qs3](https://javarevisited.blogspot.com/2022/09/9-best-system-design-interview-courses.html#axzz7duXykMs8)
  - [Qs4](https://javarevisited.blogspot.com/2022/06/system-design-interview-question-answer.html#axzz7duXykMs8)
  - [Qs5](https://www.freecodecamp.org/news/systems-design-for-interviews/)
- [YouTube Design](https://bytebytego.com/courses/system-design-interview/design-youtube?fpr=javarevisited)
- [Chat System](https://bytebytego.com/courses/system-design-interview/design-a-chat-system?fpr=javarevisited)  
- [Microservices](https://grokkingtechinterview.com/24-microservices-interview-questions-and-answers-to-land-that-job-4ae81ef34083)  
- [SO, SAML, OAuth2, OIDC](https://medium.com/javarevisited/single-sign-on-sso-saml-oauth2-oidc-simplified-cf54b749ef39)

### System Design Questions

1. [URL Shortener](https://bit.ly/3dZoQ2G)  
2. [YouTube Design](https://bit.ly/3bbNnAN)  
3. [LMS Design](https://bit.ly/3Jk9emc)  
4. [WhatsApp](https://bit.ly/3SbA9Eu)  
5. [Parking Lot](https://bit.ly/3SaTyFM)  
6. [Instagram Design](https://bit.ly/3BqamCL)  
7. Payment Gateway – VISA (or any)  
8. Load Balancer  
9. Rate Limit  
10. Cache  
11. Message Queue  
12. Teams App  

---

## Extra References

- Circuit Breaker in Microservices 
  - [Ref](https://medium.com/javarevisited/what-is-circuit-breaker-in-microservices-a94f95f5e5ae)
- Clean Architecture Tutorial: Design for enterprise-scale apps
  - [Ref](https://learningdaily.dev/clean-architecture-tutorial-design-for-enterprise-scale-apps-ce58dc9102a2)  
- Backend strategy for massive traffic 
  - [Ref](https://medium.com/coupang-engineering/our-backend-strategy-to-handle-massive-traffic-d30cd6cc4fb2)
- Microservices Questions 
  - [Ref](https://4dayweek.medium.com/microservices-questions-to-nail-your-interview-2022-831eb2227549)
- Designing a user notification system
  - [Ref](https://medium.com/codex/user-notification-system-744dfd0a237c)
- Distributed transaction management in microservices
  - [Ref](https://medium.com/javarevisited/distributed-transaction-management-in-microservices-part-2-saga-pattern-53808a55e641)
- Important Software Architecture Principles
  - [Ref](https://betterprogramming.pub/6-important-software-architecture-principles-733fb4a08d35)  
- Algorithms for system design interviews 
  - [Ref](https://blog.bytebytego.com/p/algorithms-you-should-know-before)  
- 5 Software Architecture Patterns 
  - [Ref](https://levelup.gitconnected.com/5-software-architectural-patterns-871e2705c998)  
- 15 REST API design tips 
  - [Ref](https://medium.com/@liams_o/15-fundamental-tips-on-rest-api-design-9a05bcd42920)  
- Software Architecture Chronicles 
  - [Ref](https://herbertograca.com/2017/07/03/the-software-architecture-chronicles/)  
- Slack System Architecture 
  - [Ref1](https://medium.com/geekculture/slack-system-architecture-aa9b8cfb886e)  
- Design Patterns 
  - [Ref1](https://github.com/DovAmir/awesome-design-patterns) 
- OOAD Interview Questions & Problems 
  - [Ref1](https://medium.com/javarevisited/top-10-object-oriented-analysis-and-design-interview-questions-and-problems-for-experienced-6c3a53b7cb26)
  - [Ref2](https://www.java67.com/2016/07/top-5-object-oriented-design-interview-questions.html)
- System Design Interview Qs 
  - [Ref1](https://medium.com/javarevisited/25-software-design-interview-questions-to-crack-any-programming-and-technical-interviews-4b8237942db0)  
- Vending Machine 
  - [Ref1](https://javarevisited.blogspot.com/2016/06/design-vending-machine-in-java.html#axzz7eYYA1LG3)
- Trade Position Aggregator / Risk Engine 
  - [Ref](https://javarevisited.blogspot.com/2022/03/how-to-design-trade-position-calculator.html#axzz7eYYA1LG3)
- [Kafka](https://medium.com/@hardiktaneja_99752/lessons-after-running-kafka-in-production-626974ffd700) 
- [Build Your Own X](https://github.com/codecrafters-io/build-your-own-x)
- [Database Sharding](https://medium.com/system-design-blog/database-sharding-69f3f4bd96db) 
- [Distributed Systems](https://www.youtube.com/watch?v=UEAMfLPZZhE&list=PLeKd45zvjcDFUEv_ohr_HdUFe97RItdiB&ab_channel=MartinKleppmann)

- Stateful vs Stateless Architecture
  - [Ref1](https://medium.com/@ajin.sunny/system-design-architecture-stateful-vs-stateless-62ed0ddb9f2b)

- Microservices Communication (Queues, Topics, Streams) 
  - [Ref1](https://medium.com/codex/microservices-communication-queues-topics-and-streams-597664d4b786)
- Fundamental Software Architectural Patterns 
  - [Ref](https://medium.com/@liams_o/fundamental-software-architectural-patterns-663440c5f9a5)
- Event Sourcing in Microservices 
  - [Ref1](https://blog.bitsrc.io/why-microservices-should-use-event-sourcing-9755a54ebfb4)

---

## [Design Patterns](https://github.com/devravinder/learn-design-patterns)


**References:**  
- Microservice Design Patterns
  - [Ref1](https://dzone.com/articles/design-patterns-for-microservices)
- JavaScript & Node.js Design Patterns
  - [Ref1](https://stackblitz.com/@lydiahallie/collections/javascript-patterns)

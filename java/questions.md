# Java Interview Questions

## Core Java

1. What is JDK & JVM?
2. What is a JIT compilation?  `*`
3. what are OOPs features?  `*`
4. What is abstraction?
5. What is Data hiding?
6. How does class loading work?
7. What is a constructor?
8. What is final?
9. What is static?
10. What is abstract?
11. Why it is not allowed to mark a class static? `*`
12. Why Strings are immutable in Java? `*`
13. String Vs StringBuffer Vs StringBuilder?
14. What is String Pool? How it works? `***`
    1. How many objects will get created for the below code?
       ```java
        String s1 = "hello";
        String s2 = new String("world");
       ```
    2. How many objects?
       ```java
       String s2 = new String("world");
       ```
    3. How to make Heap String object to point to pool object?
       - using `intern()` method.
       - The intern() method moves the string to the string pool (if not already present) and returns a reference to the pooled instance.
       - ```java
            public class StringInternExample {
            public static void main(String[] args) {
                String heapString = new String("Hello"); // Created in heap memory
                String poolString = heapString.intern(); // Moved to string pool

                String literalString = "Hello"; // Already in the string pool

                System.out.println(poolString == literalString); // true, both refer to the same object in the string pool
                    }
            }

         ```

    4. What will be the output? Why
       ```java
         String s1 = "hello";
         String s2 = new String("hello");
         String s3 = "hello";
         System.out.println(s1==s2);
         System.out.println(s1==s3);
         String s4 = s2.intern();
         System.out.println(s1==s4);
       ```
15. Whay is `wrpper pool`? How it works?  `***`
    - it is same like `string pool` but wrapper classes
    - it stores/creates obejcts in `wrpper pool` for `Wrapper objects` 
    - it creates obejcts only if the wrapper object is in `byte range` ie `-128 to 127`
    - evey wrapper class has it's own pool

    - Guess the output?
      ```java
        Integer i1 = 127;
        Integer i2 = new Integer(127);
        Integer i3 = Integer.valueOf(127);
        Integer i4 = 127;


        System.out.println(i1 == i2);
        System.out.println(i1 == i3);
        System.out.println(i1 == i4);
        System.out.println("----------");
      ```
16. `hashCode()` vs `System.identityHashCode()` vs `Object.hashCode()`
    - `Object.hashCode()`
       - this returns hashcode based on `memory` address
       - this won't consider object state / contents
    - `System.identityHashCode()`
       - this internally calls `Object.hashCode()`, so returns hashcode based on `memory` address

    - `hashCode()`
      - this methods exists in Object class, can be overriden
      - Generally, we'll override this, based on the object state
        - such a way, obejcts with some state should retrun same hascode
      - if we won't override..then internally it calls `Object.hashCode()`

17. How to make an immutable class? `*`
18. How many ways we can create a object in java? `*`
    - new 
    - literal  eg: ` String s = "abc"; `
    - clone()
    - reflection
19. Cloning? Shallow Copy Vs Deep Copy?
20. Can we override static menthods? If not why `*`
21. Abstract Class Vs Interface?
22. Polymorphism?
23. Inheritance?
24. Overloading Vs Overriding? or Static Polymorphism Vs Runtime Polymorphism? `*`
    - which is fast?
25. can we change the return type in override method in child class? `*`
26. can we change the throwing calls type in override method in child class? `*`
   - ```java
      // in Parent
        method() throws Excepion

      // in child
        method() throws IllegalArgumentException
     ```
27. What is Diamond Problem in inheritance in Java?
28. Why multiple inheritance is not supported?
29. Why we should not apply private & abstract together? `*`
30. Why we should not apply static & abstract together?  `*`
31. How to execute a piece of code before the main method?  `*`
   - Static Block 
32. What is the order of execution of the following:- `*`
    - constructor, initializers, static initializers, parent constructor, parent initializers, parent static initializers, main method?
33. What is an exception? Give a few examples. When will they occur?
34. Checked Exceptions Vs Un-Checked Exceptions? `*`
35. Thow vs throws?
36. 
   - Is `catch` block mandatory?
   - Is `finally` block mandatory?

37. `final` vs `finally` vs `finalize`
37. what are default methods? `*`
    - can we declare default methods in abstract calss?
      - No
    - can we override default methods?
      - Yes
38. can we declare instance variables in interface?
    - No

39. What are Collections in Java? Give a few examples, that you used.
   - List Vs Set? [ LinkedList vs HashSet ]
   - TreeSet Vs HashSet?
   - what is Map?
   - How HashSet ( HashMap ) works? `*`
      - Note: HashSet internaly uses hashMap

   - ArrayList vs LinkedList?
   - When LinkedList are better over ArrayList? `***`
   - HashMap vs ConcurrentHashMap  `*`
   - How ConcurrentHashMap works? `*`
   - Stack Vs Queue?
40. Why do we need to override hashCode?
41. Do we need to override both hashCode and equals? if we are using HashSet to store our object? `*`
    - Yes, hashCode to find the bucket & equals is to check equality check

42.  Can we use Object as a key in HashMap? [ eg: Employee class object ]? `***`
     - Yes, we can use. But we should use immutable class, else it'll lead to hash collision
43. Hash Collision?
44. Can we add two objects with the same data/states in HashSet/HashMap? Will it allow all? What is the count?
    - Depends on the hashcode implementation, 
    - so if not implemented, it’ll allow duplicates, bcz it compares the address 
        - default hashcode return the address of the object
  
45. Can we delete/modify an element from a list/collection while iterating using each loop? If not why? `*`
46. How to iterate over the Map?
47. HashMap vs LinkedHashMap vs TreeMap?
48. HashMap vs SynchronizedMap vs ConcurrentHashMap? `**`
49. HashMap Vs HashTable?
50. Comparable vs Comparator? `***`
51. Generics? `*`
51. Garbage collection? Types of Garbage collections? How do they work? `*`
52. When the static variables are available for garbage collection? `*`
53. How to make object available for garbage collection? `*`
    - de-reference `assign to null`
    - System.gc()

54. What is volatile? `*`
55. What is transient? `*`
56. What is serialization( deserialization)? `*`
57. what is externalization? 
58. In the parent, serialization is implemented but not in the child. Will it work or throws an error? [ Vice-Versa]
59. Can we overload the main method? `*`
60. What are all the optional modifiers that we can add to the main methods?  
    - What are all the changes allowed for the main method 

61. What are the methods exists in the Object class?
62. Enum?
    - can Enum have methods?
      - Yes
63. How does JVM divide/allocate memory? or Memory types in JVM?
64. I/O in Java? [ Files, Command line, Rest API, Serialization-Deserialization, etc ]
65. What is a Thread in Java?
66. What is Multi-Threading?
67. Thread vs Process vs Program?
68. What is deadlock?
69. What is race condition?
70. What is a synchronized keyword?
71. What is thread-safety?
72. How to overcome the deadlock situation?
73. Thread lifecycle?
74. Sleep vs Wait methods?
75. What happens when we call the join method?
76. Consumer and Producer problem example?
77. How many ways we can create Threads in Java? `***`
    - extending Thread
    - implementing Runnable
    - implementing Callable `*`
78. Why should we prefer implementing Runnable over the Extending Thread?
79. Callable vs Runnable? `***`
80. What is a Future Object? `***`
81. What is ExecutorService? `***`
82. What is ThreadPool?
83. What is BlockingQueue?   `***`
84. Did you use the reentrantlock? What is the use of it?
85. What are the new features in Java-8? `***`
    - Lambda Expressions (Functional Programming)
    - Functional Interfaces  `***`
       - Produces `*`
       - Consumer `*`
       - Supplier `*`
       - Predicate `*`
    - Stream API (Processing Collections Efficiently) `***`
    - Default metods in interface
    - Method References (:: Operator) 
    - Optional Class (Avoiding NullPointerException)
    - New Date & Time API (java.time Package)
    - `Collectors` in Stream API  `*`
    - Base64 Encoding and Decoding
86. Rest parameters?
87. Optional return type?
88. What is a functional interface?
   - Consumer, Producer, and Predicate interfaces?
89. What are the Lamda functions?
90. Can an interface have methods with the implementation?
91. Method reference?
92. What are streams in java?
    - Filter vs Map?
    - Stream vs ParallalStream?
    - Map vs FlatMap in streams?

93. CompletableFeature? `*`
94. Sealed classes? `*`
95. Records? `*`
    - can Record extend another class?
    - can Record implent interface?
    - can Record have methods?
96. how to create custom annotations ? `*`

97. How to implement the Singleton class?
98. Reflection?
99. What are Blocking collections? `*`
100. What are concurrent collections? `*`
101. what are `CountDownLatch` and `CyclicBarrier` in `java.util.concurrent`?
102. what is `nio` package?
     - non-blocing io?
103. what is try with rerource? what are the benefits?
104. can we pass object in switch case?
     - yes in java17 afterwards
        - in `switch expression`
        - also we can use `Guarded Patterns`
105. what are text blocks?
     - multiline string after `java13`

106. in User class has name & age  `***`
    - using streams
        - group users by name
        - sort by age
        - find 2nd youngest `*`
        - find dublicate user
107. using streams   `***`
   - for a given string find no of occurance of each character `***`
   - find dublicate chars `***`
   - find unique chars `*`


108. Different Types of [Deisgn Patterns](https://refactoring.guru/design-patterns)?

## JDBC

1. What is a connection pool? `*`
2. How does Driver Manager connect to db?
3. Statement vs Prepared Statements ?

## Servlets&Jsp

- What is Servlet?
- Lifecycle of Servlet?
- Lifecycle of JSP?


## Spring MVC

1. What is spring?
2. What is AOP? `*`
3. What is IOC? `*`
4. What is dependency injection? `*`
5. What is a spring container?
6. Singleton vs Prototype?
7. What is a session?
8. what are different scopes of a bean in spring or spring boot? `***`



## Spring Boot

1. What is a spring boot?
2. Spring vs Spring MVC vs Spring Boot? `***`
3. What is maven?
4. What are the benefits of using spring boot over the spring MVC?
5. What are the different scopes in spring boot ( spring )? `***`
        - Singleton, prototype, request, session, applicationContext, WebSocket
6. What are the different types of contexts?
7. How many ways we can create beans in Spring boot? `*`
8. Controller vs RestContoller? `*`
9. What are interceptors? `*`
10. Component vs Controller vs Service vs Repository? 
11. The life cycle of a bean? `*`
12. What @SpringBootApplication annotation does? `***`
13. What  @Configure, @EnableAutoConfiguration, @ComponentScan annotation do? `*`
14. How many ways we can set the values in spring boot?
15. What @AutoWired annotation does?
16. What @Qualifies annotation does?
17. What is @Primary annotation does? `*`
18. How to read data(values) from application.properties?
    - @Value
    - @ConfigurationProperties
19. How to use environment-based properties files?
20. What are profiles in spring boot?
    - @Profile
21. How to connect more than one DB using spring boot?
22. JPA vs CRUD repository?
23. What does @id, @transient annotation do?
24. How to execute custom DB queries in Spring boot?
   - @Query
   - @Modifier
   - @Param
   - Native Queries
   - CriteriaBuilder
25. Hibernate Query Language Vs Native Query?
26. What @Transactional annotation does?  `***`
27. What is the connection pool?
28. getById vs findById?
29. EagerLoading vs LazyLoading? `***`
30. How to handle exceptions or error handling?  `***`
     - in controller
     - in controller advice
31. How to handle global exceptions in spring boot? `***`
32. How (best way ) to create threads in spring boot?
     -  Completable future
33.  interceptors vs filters? `*`


## Spring Boot Advance & Micro Services
1. Spring boot actuator
2. Caching `*`
    - @EnableCaching ( @Cacheable, @CachePut, and @CacheEvict )
         - @Cacheable: the result of a method should be cached

3. CommandLineRunner
4. How to connect to multiple DBs? `*`
5. Internationalization (i18n)
6. Testing  
    - @SpringBootTest, @MockBean, and @DataJpaTest
7. JPA pagination
8. @Transactional `*`
   - @Transactional(propagation = Propagation.NESTED)

9. @Configuration `***`
   - @ConditionalOnMissingBean
8. How to load beans conditionally? `*`
   - @Conditional
9. @TransactionalEventListener
10. scheduled task
     - @EnableScheduling
     - @Scheduled
11. @ConfigurationProperties
    - to bind application.properties to an object / class
12. file upload
13. @Import
14. @EnableAsync
    - @Async

15. @DynamicPropertySource  ( Testing )
16. database migrations 
    - Flyway 
    - Liquibase `*`

17. @Retryable
18. distributed caching `*`
    - Redis `*`
    - Hazelcast

19. distributed session management `*`
    - Redis `*`
    - Hazelcast

20. distributed locks `*`
    - shedLock

21. @Lazy  `*`
22. server-sent events (SSE)
23. @EventListener

24. How to Register a Custom Auto-Configuration?
25. How to Disable a Specific Auto-Configuration?
     - If we want to disable a specific auto-configuration, 
     - we can indicate it using the exclude attribute of the @EnableAutoConfiguration annotation.

26. what are `Spring Boot Starters`

27. How to optimize API request
    1. first DB level
       - primary keys
       - index
       - fetching required fields
       - avoding un-necessary joins
       - query pagination

    2. using cache
    3. Paginataion
    4. Images as a seperate api
    5. sending only required fields in response

28. DTO `*`
29. Bean vs Entity vs DTO

## Spring Security
1. method-level security ( `@PreAuthorize` , `@PostAuthorize`, `@Secured` ) `*`
2. what is filterSecurityChain
3. How to secure mvc controller ? or APIs
   - method level security
      - `@PreAuthorize` , `@PostAuthorize`, `@Secured`

    - @EnableWebSecurity
       - SecurityFilterChain
          - authorizeHttpRequests & requestMatchers/matchPattern


## Spring Boot Micro Services
1. did you work with any message queues
   - RabbitMQ `*`
   - Apachekafka `*`
2. How to communicate b/w the micro services `*`
   - Synchronus comminication
      - REST
      - GraphQL
      - GRPC
   - ASynchronus comminication
      - Event-driven architecture
        - Messaging Queues
           - RabbitMQ `*`
           - Apachekafka `*`

3. OpenTelemetry
     metrics, logs, and traces

4. How to see logs in Micro services `***`
    - ELK Stack (`Elasticsearch`, `Logstash`, `Kibana`)
    - `Promtail` & `Loki`

5. Observaility in micro services `***`
   - logger
      - ELK Stack (`Elasticsearch`, `Logstash`, `Kibana`)  `*`
     - `Promtail` & `Loki` `*`
   - Metrics
     - Spring Boot Actuator with `MicroMeter plugin` &   `Prometheus`

   - Tracing
     - Spring Boot Actuator with `zapkin plugin` &   `Tempo`

   - Dashboard
     - Grafana

6. Observaility  `*`
  ```
              Spring Boot                       ----> Centalized Service
              =========================================
    Logging:  Logstash                          ----> Elasticsearch for storage & Kibana for View
                  (or)
    Logging:  Logstash                          ----> Elasticsearch for storage & Kibana for View

    Metrics:  Actuator with MicroMeter plugin   ----> Prometheus
    Tracing:  Actuator with zapkin plugin       ---->  Tempo

  ```

7. What are different types of Micro Service Architecture Design Pattern You used?


## Other Spring Boot Topics
1. Spring Cloud: The Ecosystem for Distributed Systems
   - Spring Cloud Config
   - Eureka `*`
   - Zuul
   - Hystrix

   -  Service discovery
     - Netflix Eureka 
     - HashiCorp Consul.

2. Reactive programming
     Spring WebFlux
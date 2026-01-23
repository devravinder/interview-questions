# Java Interview Questions

## Core Java

1. What is JDK & JVM?
   - JDK = JRE + Dev Tools
   - JRE = JVM + rt lib
2. What is a JIT compilation?  `*`
3. what are OOPs features?  `*`
   - Abstaction, Encapsulation, Inheritance, Polymarphsm ( AEIP like AEIOU)
4. What is abstraction?
5. What is Data hiding?
6. How does class loading work?
7. What is a constructor?
8. What is final?
9. What is static?
   - `static` means class-level, belogns to class, not to object
10. What is abstract?
11. Why it is not allowed to mark a class static? `*`
    - static means class-level
    - Top-level class is already class-level, So static is meaningless
    - ✔ Only nested (inner) classes can be static

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
       - for char `0 to 127` & for bool `true / false`
    - evey wrapper class has it's own pool

    - Guess the output?

      ```java
        Integer i1 = 127;
        Integer i2 = new Integer(127);
        Integer i3 = Integer.valueOf(127); // like string.intern()
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
    - for deep copy / or custom clone - implement Clonnable & override clone
20. Can we override static menthods? If not why `*`
21. Abstract Class Vs Interface?
22. Polymorphism?
23. Inheritance?
24. Overloading Vs Overriding? or Static Polymorphism Vs Runtime Polymorphism? `*`
    - which is fast?
25. can we change the return type in override method in child class? `*`
    - Yes, but only `Covariant return type` (same or subclass of parent return type)
26. can we change the throwing calls type in override method in child class? `*`

    - ```java
        // in Parent
        method() throws Excepion

        // in child
        method() throws IllegalArgumentException
       ```

27. What is Diamond Problem in inheritance in Java?
28. Why multiple inheritance is not supported?
    - to prevent ambiguity

29. Why we should not apply private & abstract together? `*`
30. Why we should not apply static & abstract together?  `*`
31. How to execute a piece of code before the main method?  `*`
    - Static Block

32. What is the order of execution of the following:- `*`
    - constructor, initializers, static initializers, parent constructor, parent initializers, parent static initializers, main method?
    - A:- Parent static → Child static → main() → Parent init → Parent constructor → Child init → Child constructor
33. What is an exception? Give a few examples. When will they occur?
34. Checked Exceptions Vs Un-Checked Exceptions? `*`
35. Thow vs throws?
36. What
    - Is `catch` block mandatory?
    - Is `finally` block mandatory?

37. `final` vs `finally` vs `finalize`
38. what are default methods? `*`
    - A:- instance methods like ( but not, they can't access instnace variables )
    - can we declare default methods in abstract calss?
      - No
    - can we override default methods?
      - Yes
    - if default method is instance method, can it access instance variable
39. can we declare instance variables in interface?
    - No

40. What are Collections in Java? Give a few examples, that you used.
    - List Vs Set? [ LinkedList vs HashSet ]
    - TreeSet Vs HashSet?
    - what is Map?
    - How HashSet ( HashMap ) works? `*`
    - Note: HashSet internaly uses hashMap

    - ArrayList vs LinkedList?
    - When LinkedList are better over ArrayList? `***`
    - HashMap vs ConcurrentHashMap  `*`
    - How ConcurrentHashMap works? `*`
       - thread-safe, faster
       - Uses bucket-level locking
       - Multiple threads access safely
       - No full map lock

    - Stack Vs Queue?

41. Why do we need to override hashCode?
42. Do we need to override both hashCode and equals? if we are using HashSet to store our object? `*`
    - Yes, hashCode to find the bucket & equals is to check equality check

43. Can we use Object as a key in HashMap? [ eg: Employee class object ]? `***`
     - Yes, we can use. But we should use immutable class, else it'll lead to hash collision
44. Hash Collision?
45. Can we add two objects with the same data/states in HashSet/HashMap? Will it allow all? What is the count?
    - Depends on the hashcode implementation,
    - so if not implemented, it’ll allow duplicates, bcz it compares the address
        - default hashcode return the address of the object
  
46. Can we delete/modify an element from a list/collection while iterating using each loop? If not why? `*`
47. How to iterate over the Map?
48. HashMap vs LinkedHashMap vs TreeMap?
    - HashMap → no order, fastest
    - LinkedHashMap → insertion order maintained
    - TreeMap → sorted order (ascending)
49. HashMap vs SynchronizedMap vs ConcurrentHashMap? `**`
    - HashMap → not thread-safe
    - SynchronizedMap → thread-safe (full lock, slow)
    - ConcurrentHashMap → thread-safe (bucket-level lock, fast)
50. HashMap Vs HashTable?
    - HashMap → not thread-safe, allows 1 null key : slower
    - Hashtable → thread-safe, NO null key/value : faster
51. does Treemap allows null key
    - TreeMap does NOT allow null keys
    - Uses compareTo() / Comparator → Null cannot be compared → NullPointerException

52. Comparable vs Comparator? `***`
53. Can add any User/class without comparable implementation in TreeMap
    - we CANNOT add custom objects to TreeMap without Comparable or Comparator

54. Generics? `*`
    - Allows type-safe code
    - Compile-time checking, No casting, Clean code
    - Benifits: Avoids ClassCastException → Reusable classes & methods
    - Type safety + no casting ✔️

55. What is `type erasure`?
    - Generic info removed at runtime
56. `<T>` vs `<?>` difference?
    - `<T>` = type parameter
    - `<?>` = unknown type
57. Bounded generics (`<? extends T>`, `<? super T>`) ( Lower bounded, Upper bounded)
58. `<? extends T>` vs `<? super T>` ***
    - <? extends T> : Accepts T or its child (read-only)
    - <? super T> : Accepts T or its parent (write-safe)

    - ```java
      class Animal {}
      class Dog extends Animal {}

      //
      List<Dog> dogs = new ArrayList<>();
      List<? extends Animal> list = dogs; // <? extends T> (Read-only)

      Animal a = list.get(0); // allowed, type safe
      list.add(new Dog());    // ❌ NOT allowed


      //
      List<Animal> animals = new ArrayList<>();
      List<? super Dog> list = animals; // <? super T> (Write-safe)

      list.add(new Dog());   // allowed ( write)
      Object obj = list.get(0); // only Object, Cannot read as Dog



      ```

59. Can we use `primitive types` in generics?
    - No, use Wrapper classes

60. Generic class vs generic method?
    - Class: type at class level
    - Method: type at method level
61. Why arrays are covariant but generics are not?
62. Can we create `generic exception class`?
    - NO
63. Difference between `List<Object> & List<?>`
    - `Object`: accepts all
    - `?`: read-only i.e `? extends Object`

64. Why generics introduced in Java?
    - Type safety + no casting ✔️

65. Garbage collection? Types of Garbage collections? How do they work? `*`
    - [Memory Management](./memory-management)

    ### `Types of GC`

    1. `Serial GC`
    → Single thread
    → Small apps

    2. `Parallel GC`
    → Multi-threaded
    → High throughput

    3. `CMS GC`
    → Low pause time

    4. `G1 GC` (Garbage First)
    → Region-based
    → Default (Java 9+)

    ### `How GC works`

    1. `Mark` reachable objects
    2. `Sweep` unused objects
    3. `Compact` memory

66. what is Region-based GC

    - `Meaning:`
      - Heap is divided into `small fixed regions`
      - instead of Young/Old generations.

    - Used in:`G1 GC`
    - `How it works:`

    - Each region can be `young / old / free`
    - GC collects `only required regions`
    - Predictable pause time

    `Benefit:`

    - Better memory utilization
    - Low pause time

    ---

    Region-based GC = `GC works on small heap regions` instead of whole heap ✔️

67. what are new improvements in GC after java8

    1. `G1 GC became default` (Java 9)
    → Region-based
    → Predictable pause time

    2. `ZGC` (Java 11+)
    → Ultra-low pause (<10ms)
    → Scalable (TB heap)

    3. `Shenandoah GC`
    → Low latency
    → Concurrent compaction

    4. `Epsilon GC`
    → No GC (testing, performance)

    5. `Better heap management`
    → Improved compaction
    → Less fragmentation

    6. `Improved concurrent GC`
    → Less stop-the-world
    → Better responsiveness

    Post Java8 → `Low latency + scalable + concurrent GCs` ✔️

68. When the static variables are available for garbage collection? `*`
69. How to make object available for garbage collection? `*`
    - de-reference `assign to null`
    - System.gc()

70. What is volatile? `*`
    - Ensures visibility of changes across threads
    - Prevents cache inconsistency
    - volatile = latest value always visible to all threads
71. What is transient? `*`
    - Variable not serialized, Skipped during serialization
72. What is serialization( deserialization)? `*`
73. what is externalization?
74. In the parent, serialization is implemented but not in the child. Will it work or throws an error? [ Vice-Versa]

    - Case 1: Parent implements `Serializable`, Child does NOT
       - Works fine: Child is automatically serializable

    - Case 2: Child implements `Serializable`, Parent does NOT
       - Works BUT:
          - Parent must have `no-arg constructor`
          - Parent data will NOT be serialized

    - Parent serializable → Child auto serializable
    - Child serializable → Parent needs default constructor ✔️ else Exception

75. Can we overload the main method? `*`
76. What are all the optional modifiers that we can add to the main methods?  
    - What are all the changes allowed for the main method
    - `final` `synchronized` `strictfp`

77. strictfp
    - same floating-point results
    - Ensures precision consistency
    - Avoids hardware differences
    - Applicable to : class, method

78. What are the methods exists in the Object class?
79. Enum?
    - can Enum have methods?
      - Yes
80. How does JVM divide/allocate memory? or Memory types in JVM?
    1. JVM memory = `Heap + Stack + Method Area + PC + Native Stack`

    2. `Heap`
       - Stores objects & instance variables

    3. `Stack`
       - Method calls
       - Local variables

    4. `Method Area`
       - Class metadata
       - Static variables
       - Runtime constant pool

    5. `PC Register`
       - Current instruction address

    6. `Native Method Stack`
       - Native (C/C++) calls

81. I/O in Java? [ Files, Command line, Rest API, Serialization-Deserialization, etc ]
82. What is a Thread in Java?
    - Instructions + Memory(Shared) + Control Flow
83. What is Multi-Threading?
84. Thread vs Process vs Program?
85. What is deadlock?
86. What is race condition?
87. What is a synchronized keyword?
88. What is thread-safety?
    - Code works correctly, Even with multiple threads
89. How to overcome the deadlock situation?
    - Avoid nested locks
    - Use timeout
    - Lock ordering
    - Use tryLock()

90. Thread lifecycle?
    - New → Runnable → Running → Blocked → Terminated
91. Sleep vs Wait methods?
    - sleep() → Thread class → no lock release
    - wait() → Object class → releases lock
92. What happens when we call the join method?
    - Current thread waits
    - Until another thread completes

93. Consumer and Producer problem example?
94. How many ways we can create Threads in Java? `***`
    - extending Thread
    - implementing Runnable
    - implementing Callable `*`
95. Why should we prefer implementing Runnable over the Extending Thread?
96. Callable vs Runnable? `***`
97. What is a Future Object? `***`
98. What is ExecutorService? `***`
99. What is ThreadPool?
100. What is BlockingQueue?   `***`
101. Did you use the reentrantlock? What is the use of it?
102. What are the new features in Java-8? `***`
    - Lambda Expressions (Functional Programming)
    - Functional Interfaces  `***`
       - Consumer `*`
       - Supplier(Producer) `*`
       - Predicate `*`
    - Stream API (Processing Collections Efficiently) `***`
    - Default metods in interface
    - Method References (:: Operator)
    - Optional Class (Avoiding NullPointerException)
    - New Date & Time API (java.time Package)
    - `Collectors` in Stream API  `*`
    - Base64 Encoding and Decoding
103. Rest parameters?
104. Optional return type?
105. What is a functional interface?
    - Interface with only one abstract method
    - Used for Lambda
    - Consumer, Supplier,and Predicate interfaces?
        - `Consumer<T>` → takes input, no return
        - `Supplier<T>` → no input, returns value
        - `Predicate<T>` → returns boolean

106. What are the Lamda functions?
    - Short form of anonymous method
    - Used with functional interfaces

107. Can an interface have methods with the implementation?

108. Method reference?
    - Shortcut for lambda
    - Refers to existing method
    - Types
      - Class::staticMethod
      - obj::instanceMethod
      - Class::new

109. What are streams in java?
    - Filter vs Map?
    - Stream vs ParallalStream?
    - Map vs FlatMap in streams?

110. Stream vs ParallelStream
    - Stream = `single thread`
    - ParallelStream = `multi-threaded processing` ✔️
    - `Stream`
        - Sequential processing
        - Single thread
        - Predictable order
        - Good for small tasks
    - `ParallelStream`
        - Parallel processing
        - Multiple threads
        - Faster for large data
        - Uses ForkJoinPool

111. `ForkJoinPool`
    - Thread pool for `parallel tasks`
    - Uses `work-stealing` algorithm
    - Splits task (fork)
    - Merges result (join)
    - `Used by:`
        - `ParallelStream`
        - RecursiveTask / RecursiveAction
        - ForkJoinPool = `framework for parallel execution` ✔️
112. How streams are faster than normal for loops
    - Streams are faster due to `lazy execution + parallel processing` ✔️
    - Uses `lazy evaluation`
    - Supports `parallel processing`
    - Internal `iteration optimization`
    - Uses `ForkJoinPool` (for parallel streams)
    - Better CPU utilization

113. CompletableFeature? `*`
114. Sealed classes? `*`
115. Records? `*`
    - Special class to store immutable data
    - Auto generates: constructor, getters, equals, hashCode, toString
    - can Record extend another class?: No (already extends Record)
    - can Record implent interface?: Yes
    - can Record have methods?: Yes

116. how to create custom annotations ? `*`
117. How to implement the Singleton class?
118. Reflection?
119. What are Blocking collections? `*`
120. What are concurrent collections? `*`
121. what are `CountDownLatch` and `CyclicBarrier` in `java.util.concurrent`?
122. what is `nio` package?
     - non-blocing io?
123. what is try with rerource? what are the benefits?
124. can we pass object in switch case?
     - yes in java17 afterwards
        - in `switch expression`
        - also we can use `Guarded Patterns`
125. what are text blocks?
     - multiline string after `java13`

126. in User class has name & age  `***`
    - using streams
        - group users by name
        - sort by age
        - find 2nd youngest `*`
        - find dublicate user
127. using streams   `***`
    - for a given string find no of occurance of each character `***`
    - find dublicate chars `***`
    - find unique chars `*`

128. Different Types of [Deisgn Patterns](https://refactoring.guru/design-patterns)?

129. What are major improvements in `Hashmap` after java7
    - prevously
      - `linkedlist` used
      - Worst-case time complexity: O(n) when many keys collide
    - now
      - initially `linkedlist` if capacity increased `Red-Black Tree`
      - Worst-case time complexity: O(log n) when many keys collide
      - Thresholds introduced
        - Untreeify threshold:6, Treeify threshold : 8, Min capacity for treeification: 64
        - Tree conversion (`linkedlist` to `Red-Black Tree`) happens only when:
            - Bucket size ≥ 8
            - HashMap capacity ≥ 64

130. major Garbage Collection (GC) improvements after Java 7
    - After Java 7, Java 8 removed PermGen, introduced Metaspace, stabilized G1 GC
    - and later versions added ultra-low latency collectors like ZGC and Shenandoah.
    - In detail
      - Java 7
        - PermGen (Fixed size) → OutOfMemoryError
        - Monolithic heap handling
      - G1 GC ( java 8)
        - region based gc (Heap split into regions)
        - Predictable pause time goals
        - Low pause times ( Low latency GC )
        - Automatic heap compaction
        - Better for large heaps
    - Metaspace (Native memory) → Grows dynamically
        - Fewer OOM errors
        - Better class loading handling
    - Parallel GC
        - Better multi-core utilization
        - Smarter work stealing between GC threads

## JDBC

1. What is a connection pool? `*`
2. How does Driver Manager connect to db?
3. Statement vs Prepared Statements ?

## Servlets&Jsp

1. What is Servlet?
2. Lifecycle of Servlet?
   - load class
   - init() → called once
   - service() → handles requests
   - destroy()
3. Lifecycle of JSP?
   - compilation
   - load class
   - init() → called once
   - service() → handles requests
   - destroy()

## Spring MVC

1. What is spring?
2. What is AOP? `*`
    - Separates cross-cutting concerns
    - Logging, security, transactions

3. What is IOC? `*`
   - Object creation handled by Spring
   - Not by developer

4. What is dependency injection? `*`
5. What is a spring container?
    - Manages bean lifecycle
    - Creates & injects objects
    - Examples: ApplicationContext

6. Singleton vs Prototype?
    - Singleton → One object per container
    - Prototype → New object every request

7. What is a session?
8. what are different scopes of a bean in spring or spring boot? `***`
    - singleton → default
    - prototype
    - request
    - session
    - application/applicationContext
    - websocket

## Spring Boot

1. What is a spring boot?
2. Spring vs Spring MVC vs Spring Boot? `***`
3. What is maven?
4. What are the benefits of using spring boot over the spring MVC?
5. What are the different scopes in spring boot ( spring )? `***`
        - Singleton, prototype, request, session, applicationContext, WebSocket

6. What are the different types of contexts?

    1. `BeanFactory`: → Basic container
    2. `ApplicationContext`: → Advanced container
    3. `ClassPathXmlApplicationContext`: → Loads from classpath
    4. `FileSystemXmlApplicationContext`: → Loads from file system
    5. `AnnotationConfigApplicationContext`: → Java config (@Configuration)
    6. `WebApplicationContext`: → Web apps

7. How many ways we can create beans in Spring boot? `*`
    1. `@Component`: `@Service`, `@Repository`, `@Controller`
    2. `@Bean`:  Method level inside `@Configuration`
    3. `@Configuration + @Bean`
    4. `XML configuration` (legacy)

8. Controller vs RestContoller? `*`
9. What are interceptors? `*`
10. Component vs Controller vs Service vs Repository?
11. The life cycle of a bean? `*`

12. What @SpringBootApplication annotation does? `***`

13. What  @Configure, @EnableAutoConfiguration, @ComponentScan annotation do? `*`
    - @Configure: Marks class as config class
    - @EnableAutoConfiguration: Spring Boot auto config, Based on classpath & properties
    - @ComponentScan: Scans packages, Finds @Component, @Service, @Repository

14. How many ways we can set the values in spring boot?
15. What @AutoWired annotation does?
16. What @Qualifies annotation does?
17. What is @Primary annotation does? `*`
18. How to read data(values) from application.properties?
    - @Value
    - @ConfigurationProperties
19. How to use environment-based properties files?
    - spring.profiles.active=dev
    - application-dev.properties, application-test.properties
20. I have application-dev.properties & application.properties & spring.profiles.active=dev
    - then which proprty file is loaded
    - A: Profile file has higher priority
        - Base file loads first(application.properties) → profile file overrides(application-dev)

21. What are profiles in spring boot?
22. @Profile
    - Used to enable/disable beans
    - Based on active environment

    - ```java
        @Profile("dev")
        @Component
        class DevBean { }

       ```

23. How to connect more than one DB using spring boot?
24. JPA vs CRUD repository?
25. What does @id, @transient annotation do?
26. How to execute custom DB queries in Spring boot?
    - @Query
    - @Modifier
    - @Param
    - Native Queries
    - CriteriaBuilder

27. Hibernate Query Language Vs Native Query?
28. What @Transactional annotation does?  `***`
29. What is the connection pool?
30. getById vs findById?
31. EagerLoading vs LazyLoading? `***`
32. How to handle exceptions or error handling?  `***`
     - in controller
     - in controller advice
33. How to handle global exceptions in spring boot? `***`
34. How (best way ) to create threads in spring boot? `***`
     - Use @EnableAsync,  @Async + ThreadPoolTaskExecutor

35. interceptors vs filters? `*`

    - Filter
      - Part of `Servlet`
      - Runs `before request enters controller`
      - Works at `container level`
      - Use: logging, auth, CORS
      - Package: `javax.servlet`

    - Interceptor
      - Part of `Spring`
      - Runs `before/after controller`
      - Works at `framework level`
      - Use: validation, auth, logging
      - Package: `org.springframework`

    - Filter → runs `earlier` & Interceptor → runs `after filter`

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
10. How to load beans conditionally? `*`
    - @Conditional
    - @Profile

11. @TransactionalEventListener
    - @TransactionalEventListener = event handling tied to DB transaction state
    - Phases
        - BEFORE_COMMIT
        - AFTER_COMMIT ✅ (most used)
        - AFTER_ROLLBACK
        - AFTER_COMPLETION

12. scheduled task
     - @EnableScheduling
     - @Scheduled
13. @ConfigurationProperties
    - to bind application.properties to an object / class
14. file upload
15. @Import
16. @EnableAsync
    - @Async

17. @DynamicPropertySource  ( Testing )
18. database migrations
    - Flyway
    - Liquibase `*`

19. @Retryable
20. distributed caching `*`
    - Redis `*`
    - Hazelcast

21. distributed session management `*`
    - Redis `*`
    - Hazelcast

22. distributed locks `*`
    - shedLock

23. @Lazy  `*`
24. server-sent events (SSE)
25. @EventListener

26. How to Register a Custom Auto-Configuration?
27. How to Disable a Specific Auto-Configuration?
     - If we want to disable a specific auto-configuration,
     - we can indicate it using the exclude attribute of the @EnableAutoConfiguration annotation.

28. what are `Spring Boot Starters`

29. How to optimize API request
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

30. DTO `*`
31. Bean vs Entity vs DTO

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

    - ```bash
                Spring Boot                         ----> Centalized Service
         ==================================================================================
        Logging:  Logstash                          ----> Elasticsearch for storage & Kibana for View
                    (or)
        Logging:  Logstash                          ----> Elasticsearch for storage & Loki for View

        Metrics:  Actuator with MicroMeter plugin   ----> Prometheus
        Tracing:  Actuator with zapkin plugin       ---->  Tempo

        ```

7. What are different types of Micro Service Architecture Design Patterns?

8. Application Performance Monitoring (APM) tool
   - used to monitor, analyze, and optimize application performance in real time.
   - `AppDynamics`

## Other Spring Boot Topics

1. Spring Cloud: The Ecosystem for Distributed Systems
   - Spring Cloud Config
   - Eureka `*`
   - Zuul
   - Hystrix

   - Service discovery
     - Netflix Eureka
     - HashiCorp Consul.

2. Reactive programming
     Spring WebFlux

# Coding Questions: Basic to Advanced

Read these first; this file adds only what they don't cover:

- [DS-Algo questions](questions.md): digits, primes, duplicates, char and word counts, Fibonacci, pair sum, brackets, triplets, permutations, flatten, deep copy, coin change, longest substring, linked list and tree basics
- [JS / Node.js coding](../js_nodeJs/logical-questions.md): flatten, max left-right sum index, pair sum, middle of a linked list, brackets
- [Tech lead mock interview](../java/techlead-mock-interview.md): equilibrium index, first non-repeating element, kth largest, binary search
- [Java questions](../java/questions.md) and [Mock interview](../java/mock-interview.md): streams on users and employees, producer-consumer

Solve each one in Java and in JavaScript.

## Basic

1. Reverse a string without a built-in reverse.
   - Two pointers swapping from both ends. O(n).
2. Check if a string is a palindrome, ignoring case and non-letters.
   - Two pointers that skip non-alphanumeric characters. O(n), O(1) space.
3. Check if two strings are anagrams.
   - Count characters in a map or an array of 26. O(n).
4. Find the second largest number in one pass.
   - Track `first` and `second`; handle duplicates and arrays smaller than 2.
5. Remove duplicates from a sorted array in place and return the new length.
   - Slow and fast pointers. O(n), O(1) space.
6. Merge two sorted arrays.
   - Two pointers. O(n + m).
7. Reverse the words in a sentence.
   - `the sky is blue` → `blue is sky the`. Handle repeated spaces.
8. FizzBuzz, written so a new rule (7 → "Bazz") doesn't need a new `if`.
   - A list of (divisor, word) rules, checked in order.

## Intermediate

1. Group anagrams.
   - Key each word by its sorted letters or a letter count. O(n k log k).
2. Maximum subarray sum.
   - Kadane: `cur = max(x, cur + x)`, `best = max(best, cur)`. O(n).
3. Move all zeros to the end, keeping order.
   - Write non-zeros forward, then fill zeros. O(n), O(1) space.
4. Rotate an array right by k.
   - Reverse the whole array, then reverse the first k and the rest. O(n), O(1) space.
5. Merge overlapping intervals.
   - `[[1,3],[2,6],[8,10]]` → `[[1,6],[8,10]]`. Sort by start, then extend or append. O(n log n).
6. Top k frequent elements.
   - Count, then a min-heap of size k (O(n log k)) or bucket sort by count (O(n)).
7. Product of the array except self, without division.
   - Prefix products left to right, then multiply by suffix products right to left. O(n).
8. Search in a rotated sorted array.
   - Binary search; one half is always sorted, so check if the target is inside it. O(log n).
9. Reverse a linked list, iteratively and recursively.
10. Find where a linked list cycle starts.
    - After slow and fast pointers meet, move one to the head; step both by one and they meet at the start.

## Advanced

1. LRU cache with O(1) `get` and `put`.
   - A hash map plus a doubly linked list. In Java, `LinkedHashMap` with access order:

   ```java
   class LruCache<K, V> extends LinkedHashMap<K, V> {
       private final int capacity;

       LruCache(int capacity) {
           super(16, 0.75f, true); // access order moves read entries to the end
           this.capacity = capacity;
       }

       @Override
       protected boolean removeEldestEntry(Map.Entry<K, V> eldest) {
           return size() > capacity;
       }
   }
   ```

   - In JavaScript, a `Map` keeps insertion order: delete and re-set a key on read, and evict `map.keys().next().value`.
2. Median of a data stream.
   - A max-heap for the lower half and a min-heap for the upper half, kept within one element of each other. O(log n) per add.
3. Merge k sorted lists.
   - A min-heap of the current heads. O(n log k).
4. Number of islands in a grid.
   - DFS or BFS from each unvisited land cell, marking visited cells. O(rows x cols).
5. Longest increasing subsequence.
   - O(n^2) DP, then O(n log n) with patience sorting and binary search.
6. Edit distance between two words.
   - 2D DP over insert, delete and replace. O(n x m).
7. Trapping rain water.
   - Two pointers with running left and right maximums. O(n), O(1) space.
8. Sliding window maximum.
   - A deque of indexes with decreasing values. O(n).
9. Shortest path in a weighted graph.
   - Dijkstra with a priority queue, O((V + E) log V). Weights must not be negative.
10. Serialize and deserialize a binary tree.
    - Pre-order with a null marker, then rebuild in the same order.

## Practical (full stack)

These test everyday engineering more than algorithms.

1. Write `debounce` and `throttle` in JavaScript.
2. Write `Promise.all` and `Promise.allSettled` from scratch.
3. Run async tasks with a concurrency limit.

   ```js
   async function runWithLimit(tasks, limit) {
     const results = new Array(tasks.length);
     let next = 0;
     async function worker() {
       while (next < tasks.length) {
         const i = next++; // safe: JavaScript runs one statement at a time
         results[i] = await tasks[i]();
       }
     }
     await Promise.all(Array.from({ length: Math.min(limit, tasks.length) }, worker));
     return results;
   }
   ```

4. Write a small `EventEmitter` with `on`, `off`, `once` and `emit`.
5. Write `retry(fn, attempts)` with exponential backoff and jitter.
6. Write `memoize(fn)` and explain when its cache leaks memory.
7. Write a thread-safe token bucket rate limiter in Java.
8. Print odd and even numbers in order from two threads.
   - Two semaphores, or `wait` / `notify` on a shared lock.
9. Write a React `useDebounce` hook and use it in a search box that cancels stale requests.
   - Abort the previous `fetch` with `AbortController` when the term changes.
10. Build a React todo list with add, toggle, delete and an all / active / done filter. Then explain how you would test it.

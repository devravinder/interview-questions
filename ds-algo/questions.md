# Basic

- Find the sum of all the digits of a given number.
- The logic for prime number?
- Find the unique elements from a given integer array
- Find the duplicate elements from a given integer array
- Find the No of occurrences of each char in the given string.  
  **Eg:** `abcdab` → `a=2, b=2, c=1, d=1`
- Find the No of occurrences of each word in the given sentence.  
  **Eg:** `Hello, write Hello World Program` → `Hello=2, write=1, World=1, Program=1`
- Print the Fibonacci series.
- Print the Non-Fibonacci numbers till the given number, using only 2 loops.  
  **Eg:** `21 → 4,6,7,9,10,11,14,15,16,17,18,19,20`
- Check whether the given 2D array is symmetric or not.
- Find the index of an array, where the difference between left elements sum and right elements sum is maximum.

---

# Medium

- Find the pair of numbers whose sum is equal to the given from a given array.  
  **Eg:** `8, [1,2,8,3,4,5,6,7] → 1,7 : 2,6 : 3,5`  
  **Hint:** Binary Search
- Check whether the given string has the proper pair of brackets.  
  **Eg:**  
  `{ ([][]) ([{}]) () } → yes`  
  `{ ([][]) ([{}]) ) } → no`
- Find the three numbers whose sum is equal to the given from a given array.  
  **Eg:** `8, [1,2,8,3,4,5,6,7,0] → 1,2,5 : 1,7,0 : 5,3,0 : 6,2,0`
- Print all the possible permutations of given string chars.  
  **Eg:** `abc → abc, acb, bac, bca, cab, cba`
- Given an array of nums of distinct integers, return all the possible permutations. [ref](https://leetcode.com/problems/permutations/)
- Make the given number as a combination of elements of an array [ repetition is allowed ]  
  *(Note: not least count)*  
  **Eg:**  
  - `16, [3,5] → false`  
  - `20, [2,3,5] → true → 5*4`  
  - `35, [4,3,8] → true → 4*5 + 3*5 (or (4+3)*5)`
- Flatten array → `[1,2,3[4,5,[6,7]]] → [1,2,3,4,5,6,7]`  
- Deep Copy → `{a:"a", b:{c:"c"}, d:{e:{f:"f"}}}`

---

### Rotated Palindrome Check

- Given a string, check if it is a rotated palindrome or not.

**Example 1:**  
Input: `"CBAABCD"`  
Output: `true`  
Explanation: `"CBAABCD"` is a rotation of the palindrome `"ABCDCBA"`

**Example 2:**  
Input: `"BAABCC"`  
Output: `true`  
Explanation: `"BAABCC"` is a rotation of the palindrome `"ABCCBA"`

**Example 3:**  
Input: `"DCABC"`  
Output: `false`

---

# Hard

- Find the least no of coins required to form a given number.  
  Coins = `{1,4,5}`  

  **Eg:**  
  Number = `12`  
  → `5,5,1,1`  
  → `4,4,4` (**answer=3**)

- Given a string `s`, find the length of the longest substring without repeating characters. [ref](https://leetcode.com/problems/longest-substring-without-repeating-characters/)

---

# DS & Algo

## Search
- Binary Search [ref](https://www.youtube.com/watch?v=P3YID7liBug&ab_channel=HackerRank)

## Sorting
- Bubble  
- Selection  
- Insertion  
- Merge [ref](https://www.youtube.com/watch?v=P3YID7liBug&ab_channel=HackerRank)
- Quick  
- Heap  
- Topological Sort [ref](https://www.youtube.com/watch?v=cIBFEhD77b4&ab_channel=WilliamFiset)
- Counting Sort  
- Radix Sort  
- Bucket Sort  
- Shell Sort  

## Algorithms
- Linked List  
- Stack  
- Queue  
- Binary Trees  
  - Traversals: Pre-order, Post-order, In-order [ref](https://www.youtube.com/watch?v=BHB0B1jFKQc&ab_channel=BackToBackSWE) 
- Breadth-first search & Depth-first search [ref](https://www.youtube.com/watch?v=zaBhtODEL0w&ab_channel=HackerRank)
- Implementing Queue with Stack  
- Finding the middle element in the linked list of unknown length  
- Adding at the beginning/ending/particular position in the linked list/stack  
- How to check if a cycle exists in the linked list  
- How to check if a given Tree is a Binary Search Tree in Java? [ref](https://javarevisited.blogspot.com/2021/12/how-to-check-if-tree-is-binary-search.html#ixzz7eZnrYt1N)

## Dynamic Programming
- Find the minimum number of coins required to make the given number.  
  **Eg:** coins = `{1,2,5}`, target=52 → `5*10 + 2*1`

---

# Links

- Problem Solving Approach: [ref](https://medium.com/enjoy-algorithm/popular-problem-solving-approaches-in-data-structures-and-algorithms-6b4d30a0823d)  
- Interview Qs: [ref1](https://medium.com/javarevisited/50-data-structure-and-algorithms-interview-questions-for-programmers-b4b1ac61f5b0), [ref2](https://github.com/jwasham/coding-interview-university)
- JS Algorithms: [ref1](https://github.com/trekhleb/javascript-algorithms), [ref2](https://github.com/TheAlgorithms/Javascript)  

### Categories
1. [Array](https://bit.ly/3vM1JP5)  
2. [String](https://bit.ly/3SMkjkb)  
3. [Binary Tree](https://bit.ly/3JIsn1i)  
4. [Recursion](https://bit.ly/3JDhUnv)  
5. [Linked List](https://bit.ly/3zFatrn)  
6. [DP](https://bit.ly/3vLwjs5)  

- Top 20 Recursion Practice Problems: [ref](https://dev.to/javinpaul/top-20-recursion-practice-problems-and-exercises-for-programming-interviews-3lne) 
- Interview Preparation: [ref](https://github.com/yangshun/tech-interview-handbook)

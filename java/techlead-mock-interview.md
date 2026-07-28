# Tech Lead Mock Interview

## Notes

- ask programming questions
- ask react & js

## Questions

1. How do you merge two fields in DB that has alread have data...and need to performa the same operation in all the environments.
    - eg: first_name, last_name => full_name
      need to do in dev, test, staging, prod
    - Ans: DB Migration libraries

2. Symmetric Encryption vs Asymetric Encryption
   - when we will use ...give examples

3. in JWT...when to use Secret & when to use public key - private keys

4. Hashing vs Encrytion

5. How to store secure data in DB...even developer should not see
   - it should be searchable & retrivable
   - Ans:- use two files for one value
   - eg:- email => email_encrypted ( to retieve ), email_hashed ( to search )

6. Saga pattern vs Event Driven Architecture...when to use them
    - Saga is one of Event Driven Architecture with Transaction Managamente
       - Rollback feature

7. what is 2PC ( 2 Phase Commit )

8. How logout is handled in micro server ( OAuth2 )

9. OAuth2 vs OpenId Connect vs OAuth2 + OpenId Connect

## Programming Questions

- Find the pair of numbers whose sum is equal to the given from a given array.  
  - Eg:- `8, [1,2,8,3,4,5,6,7] → 1,7 : 2,6 : 3,5`  
  - Hint: Binary Search

- Find Equilibrium index in a given array
  - eg: [0,1,2,3,4,0,2] => at index 3, left side elements sum = right side elements sum

- Find the first non-repeating element in an array without using map

- Find the kth largest element in an unsorted array (QuickSelect / Heap)

## Solutions

- Binary Search

  ```java
   public class BinarySearch {

    public static int binarySearch(int[] arr, int target) {

        int left = 0;
        int right = arr.length - 1;

        while (left <= right) {

            int mid = left + (right - left) / 2;

            if (arr[mid] == target)
                return mid;

            if (arr[mid] < target)
                left = mid + 1;
            else
                right = mid - 1;
        }

        return -1;
    }

    public static void main(String[] args) {

        int[] arr = {1,2,3,4,5,6,7,8};

        System.out.println(binarySearch(arr, 6));
        }
    }
  ```

  Recursion

  ```java
     public class BinarySearch {

    static int search(int[] arr, int left, int right, int target) {

        if (left > right)
            return -1;

        int mid = left + (right - left) / 2;

        if (arr[mid] == target)
            return mid;

        if (arr[mid] < target)
            return search(arr, mid + 1, right, target);

        return search(arr, left, mid - 1, target);
    }

    public static void main(String[] args) {

        int[] arr = {1,2,3,4,5,6,7};

        System.out.println(search(arr, 0, arr.length - 1, 6));
     }
   }
  ```

- First Non-repeating element in an array without using map

  ```java
   public class FirstNonRepeating {

    public static int firstNonRepeating(int[] arr) {

        for (int i = 0; i < arr.length; i++) {

            boolean repeating = false;

            for (int j = 0; j < arr.length; j++) {

                if (i != j && arr[i] == arr[j]) {
                    repeating = true;
                    break;
                }
            }

            if (!repeating) {
                return arr[i];
            }
        }

        return -1;
    }

    public static void main(String[] args) {

        int[] arr = {4, 5, 1, 2, 0, 4, 1, 2};

        System.out.println(firstNonRepeating(arr));
        }
    }
  ```

- Kth Largest element
  - sort the array...and take kth element

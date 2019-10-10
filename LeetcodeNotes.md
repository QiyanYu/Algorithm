

## Leetcode String Tag Notes

- When dealing with divide, can use * to avoid divide zero problem.
- "Plus One" 
```java
    int[] newNumber = new int [n+1];
    newNumber[0] = 1;
```
- **1. two sum:** When dealing with searching, can use hash table to find a element in constant time, but it may use more space. 
- **26. Remove Duplicates from Sorted Array:** Just keep track of modified pointer. (Moving element in-place)
- **88. Merge Sorted Array:** When you don't know which one is longer, keep track of them both. eg: 
  ```java
  while(i>0 && j>0){}
  ```
- **88. Merge Sorted Array:** When you need to sort an array, you can fill the longer array from the end instead of start.  
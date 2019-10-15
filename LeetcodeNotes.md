

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
- **122. Best Time to Buy and Sell Stock II:** Use while loop to simulate up or down directions.
  ```java
        while (i<len-1){
            while (i<len-1 && prices[i]>=prices[i+1]){//down
                i++;
            }
            valley=prices[i];
            while (i<len-1 && prices[i]<=prices[i+1]){//up
                i++;
            }
            peak = prices[i];
            maxProfit+=peak-valley;
        }
- **169. Majority Element:** 
  1.  A Linear Time Majority Vote Algorithm(http://www.cs.utexas.edu/~moore/best-ideas/mjrty/)
    ```java
    public class Solution {
        public int majorityElement(int[] num) {

            int major=num[0], count = 1;
            for(int i=1; i<num.length;i++){
                if(count==0){
                    count++;
                    major=num[i];
                }else if(major==num[i]){
                    count++;
                }else count--;        
            }
            return major;
        }
    }
    ```
    If not in this scenario in this problem, there should be a second loop after finding the candidate and the count, to again iterate over the array and confirm if candidate's count > n/2 : this will ensure that there is no false candidate produced.

    2. Bit manipulate

    - Some concepts of bit manipulate: 
      - Even though you can use shifting of byte, short or char, they are promoted to 32-bit integer before the shifting
      - Bit-shift operators never throw an exception
      - The right operand (the number of positions to shift) is reduced to modulo 32. That is 5 <<35 is equivalent to 5 << 3.
      - Binary representation on its own does not provide information whether the number is negative. 
    ```java
    public class Solution {
        public int majorityElement(int[] nums) {
            int[] bit = new int[32];
            for (int i = 0; i < nums.length; i++) {
                for (int j = 0; j < 32; j++) {
                    bit[j] += (nums[i] >> j) & 1;
                }
            }
            int majority = 0;
            for (int j = 0; j < 32; j++) {
                bit[j] = bit[j] > (nums.length / 2)? 1 : 0;
                majority += bit[j] << j;
            }
            return majority;
        }
    }
    ```

- **189. Rotate Array:** 3 reverse

    [1,2,3,4,5,6,7]->
    [7,6,5,4,3,2,1]->
    [5,6,7,4,3,2,1]->
    [5,6,7,1,2,3,4]

    ```java
    public void rotate(int[] nums, int k) {
        k %= nums.length;
        reverse(nums, 0, nums.length - 1);
        reverse(nums, 0, k - 1);
        reverse(nums, k, nums.length - 1);
    }

    public void reverse(int[] nums, int start, int end) {
        while (start < end) {
            int temp = nums[start];
            nums[start] = nums[end];
            nums[end] = temp;
            start++;
            end--;
        }
    }
    ```
- **217. Contains Duplicate:** We can use set.size() compare to the original array to determine whether there is a duplicate element.
- **219. Contains Duplicate II:**
    ```java
    public boolean containsNearbyDuplicate(int[] nums, int k) {
        Set<Integer> set = new HashSet<Integer>();
        for(int i = 0; i < nums.length; i++){
            if(i > k) set.remove(nums[i-k-1]);
            if(!set.add(nums[i])) return true;
        }
        return false;
    }
    ```
- **:** 
    Since a^b^b =a, so we can loop all elements and index to find the missing value.
    ```java
    public int missingNumber(int[] nums) {

        int xor = 0, i = 0;
        for (i = 0; i < nums.length; i++) {
            xor = xor ^ i ^ nums[i];
        }

        return xor ^ i;
    }
    ```

- **448. Find All Numbers Disappeared in an Array:** 
  The basic idea is that we iterate through the input array and mark elements as negative using nums[nums[i] -1] = -nums[nums[i]-1]. In this way all the numbers that we have seen will be marked as negative. In the second iteration, if a value is not marked as negative, it implies we have never seen that index before, so just add it to the return list.
    ```java
    public List<Integer> findDisappearedNumbers(int[] nums) {
        List<Integer> ret = new ArrayList<Integer>();
        
        for(int i = 0; i < nums.length; i++) {
            int val = Math.abs(nums[i]) - 1;
            if(nums[val] > 0) {
                nums[val] = -nums[val];
            }
        }
        
        for(int i = 0; i < nums.length; i++) {
            if(nums[i] > 0) {
                ret.add(i+1);
            }
        }
        return ret;
    }
    ```

- **532. K-diff Pairs in an Array：** 
  Unique pairs can just keep the starters.
    ```java
    public class Solution {
        public int findPairs(int[] nums, int k) {
            if (k < 0) { return 0; }

            Set<Integer> starters = new HashSet<Integer>();
            Set<Integer> uniqs = new HashSet<Integer>();
            for (int i = 0; i < nums.length; i++) {
                if (uniqs.contains(nums[i] - k)) starters.add(nums[i] - k);
                if (uniqs.contains(nums[i] + k)) starters.add(nums[i]);
                uniqs.add(nums[i]);
            }

            return starters.size();
        }
    }
    ```

- **566. Reshape the Matrix:** 
    ```java
    public int[][] matrixReshape(int[][] nums, int r, int c) {
        int n = nums.length, m = nums[0].length;
        if (r*c != n*m) return nums;
        int[][] res = new int[r][c];
        for (int i=0;i<r*c;i++) 
            res[i/c][i%c] = nums[i/m][i%m];
        return res;
    }
    ```
- **581. Shortest Unsorted Continuous Subarray:** Three ways about this problem. (https://leetcode.com/problems/shortest-unsorted-continuous-subarray/discuss/103066/Ideas-behind-the-O(n)-two-pass-and-one-pass-solutions)
- **605. Can Place Flowers:** 
    ```java
    public boolean canPlaceFlowers(int[] flowerbed, int n) {
        int count = 1; // USE count = 1 TO SET FIRST SECTION SPECIAL CONDITION!
        int result = 0;
        for(int i=0; i<flowerbed.length; i++) {
            if(flowerbed[i] == 0) {
                count++;
            }else {
                result += (count-1)/2;
                count = 0;
            }
        }
        if(count != 0) result += count/2;
        return result>=n;
    }
    ```

- **661. Image Smoother:** Pixel Problem
    ```java
    public int[][] imageSmoother(int[][] matrix) {
        if (matrix == null || matrix.length == 0) return new int[0][0];
        int m = matrix.length, n = matrix[0].length;
        int[][] res = new int[m][n];
        int[][] moves = new int[][] {{-1, 0}, {1, 0}, {0, -1}, {0, 1}, {-1, -1}, {1, 1}, {1, -1}, {-1, 1}};
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                int sum = matrix[i][j];
                int count = 1;
                for (int[] move : moves) {
                    int I = i + move[0];
                    int J = j + move[1];
                    if (I >= 0 && I < m && J >= 0 && J < n) {
                        count++;
                        sum += matrix[I][J];
                    }
                }
                res[i][j] = sum / count;
            }
        }
        return res;
    }
    ```


## Reference
- Bit Manipulation in Java – Bitwise and Bit Shift operations: https://www.vojtechruzicka.com/bit-manipulation-java-bitwise-bit-shift-operations/
- A Linear Time Majority Vote Algorithm(http://www.cs.utexas.edu/~moore/best-ideas/mjrty/)
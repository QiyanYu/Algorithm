

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

- **697. Degree of an Array：** HashMap putIfAbsent method can keep key unique.
  ```java 
  starter.putIfAbsent(nums[i], i); 
  ``` 

- **766. Toeplitz Matrix：** For the following up questions:
  1. What if the matrix is stored on disk, and the memory is limited such that you can only load at most one row of the matrix into the memory at once?

        ```Compare half of 1 row with half of the next/previous row.```

  2. What if the matrix is so large that you can only load up a partial row into the memory at once?
   
        ```Hash 2 rows (so only 1 element needs to be loaded at a time) and compare the results, excluding the appropriate beginning or ending element.```

- **830. Positions of Large Groups:** 
    ```java
    public List<List<Integer>> largeGroupPositions(String S) {
        List<List<Integer>> res = new ArrayList<>();
        for (int i = 0, j = 0; i < S.length(); i = j) { // reset the first pointer!!!
            while (j < S.length() && S.charAt(j) == S.charAt(i)) j++;
            if (j - i >= 3)
                res.add(Arrays.asList(i, j - 1));
        }
        return res;
    }
    ```

- **896. Monotonic Array:**  check whether the array is monotonic, use two flag to keep track of it.
    ```java
    public boolean isMonotonic(int[] A) {
        boolean inc = true, dec = true;
        for (int i = 1; i < A.length; ++i) {
            inc &= A[i - 1] <= A[i];
            dec &= A[i - 1] >= A[i];
        }
        return inc || dec;
    }
    ```

- **905. Sort Array By Parity:** When dealing with two pointers, keep in mind to make sure left pointer is less than right pointer. 
    ```java
    class Solution {
        public int[] sortArrayByParity(int[] A) {
            int len = A.length;
            for(int i = 0, j = len-1; i <= j; i++, j--){
                while(A[i] % 2 == 0 && i < j) i++; // i < j !!!
                while(A[j] % 2 != 0 && i < j) j--; // i < j !!!
                
                int temp = A[i];
                A[i] = A[j];
                A[j] = temp; 
            }
            return A;
        }
    }
    ```
- **914. X of a Kind in a Deck of Cards:** Use GCD!!!
    ```java
    public boolean hasGroupsSizeX(int[] deck) {
        Map<Integer, Integer> count = new HashMap<>();
        int res = 0;
        for (int i : deck) count.put(i, count.getOrDefault(i, 0) + 1);
        for (int i : count.values()) res = gcd(i, res);
        return res > 1;
    }
    // Remember the algorithm!!!
    public int gcd(int a, int b) {
        return b > 0 ? gcd(b, a % b) : a;
    }
    ```

- **922. Sort Array By Parity II:** Keep track of the even and odd pointers.
    ```java
    class Solution {
        public int[] sortArrayByParityII(int[] A) {
            int even = 0, odd = 1, len = A.length;
            while(even < len && odd < len){
                while(even < len && A[even] % 2 == 0){
                    even += 2;
                }
                while(odd < len && A[odd] % 2 == 1){
                    odd += 2;
                }
                if(even < len && odd < len){
                    int temp = A[even];
                    A[even] = A[odd];
                    A[odd] = temp;
                }
            }
            return A;
        }
    }
    ```
- **985. Sum of Even Numbers After Queries:** (from leetcode @rock)

Track sum of all even #s.
There are 4 cases for odd / even property of A[k] and queries[i][0], where k = queries[i][1]:
1). even and odd, lose an even item in A; sum need to deduct A[k];
2). even and even, get a bigger even item in A; sum need to add queries[i][0](same as deduct A[k] first then add both);
3). odd and odd, get a bigger even item in A; sum need to add both;
4). odd and even, no influence on even items in A;

Therefore, we can simplify the above as following procedure:

  1. find sum of all even #s;
  2. for each queries, check the item in A and after-added-up value, if
     - the item in A is even, deduct it from sum; according to 1) & 2).
     - after-added-up we have an even value, then add the new value to sum; according to 2) & 3).  
 
```java
    public int[] sumEvenAfterQueries(int[] A, int[][] queries) {
        int sum = 0, i = 0;
        for (int a : A) { if (a % 2 == 0) sum += a ; } // sum of even #s.
        int[] ans = new int[queries.length];
        for (int[] q : queries) {
            if (A[q[1]] % 2 == 0) { sum -= A[q[1]]; } // from 1) and 2)
            A[q[1]] += q[0];
            if (A[q[1]] % 2 == 0) { sum += A[q[1]]; } // from 2) and 3)
            ans[i++] = sum;
        }
        return ans;
    }
```
- **989. Add to Array-Form of Integer:** (from leetcode @rock)
    ArrayList.add(0, K % 10) is not O(1) but O(n) instead. Use LinkedList.add(0, i) or offerFirst(i) is O(1).
    ```java
    public List<Integer> addToArrayForm(int[] A, int K) {
        LinkedList<Integer> ans = new LinkedList<>();
        for (int i = A.length - 1; K > 0 || i >= 0; --i, K /= 10) { // loop through A and K, from right to left.
            if (i >= 0) { K += A[i]; } // Use K as carry over, and add A[i].
            ans.offerFirst(K % 10); // add the least significant digit of K.
        }
        return ans;
    }
    ```

- **999. Available Captures for Rook:** A clear way to present directions, use a private method to be concise.
    ```java
    class Solution {
        public int numRookCaptures(char[][] board) {
            int res = 0;
            for(int r = 0; r < board.length; r++){
                for(int c = 0; c < board[0].length; c++){
                    if(board[r][c] == 'R') {
                        res = cap(board, r, c);
                    }
                }
            }
            return res;
        }
        
        private int cap(char[][] board, int row, int column){
            int res = 0;
            for(int[] d : new int[][] {{1,0}, {-1,0}, {0,1}, {0,-1}}){
                for(int r = row + d[0], c = column + d[1]; 0 <= r && r < board.length && 0 <= c && c < board[0].length; r += d[0], c += d[1]){
                    if(board[r][c] == 'p') res++;
                    if(board[r][c] != '.') break;
                }
            }
            return res;
        }
    }
    ```

- **1002. Find Common Characters:** (from leetcode @chillin1017)
    ```java
    public List<String> commonChars(String[] A) {
        List<String> ans = new ArrayList<>();
        // Common characters dictionary
        int[] dict = new int[26];
        for (int j = 0; j < A[0].length(); j++) {
            dict[A[0].charAt(j) - 'a']++;
        }
        for (int i = 1; i < A.length; i++) {
            // Dictionary of the current word
            int[] curr = new int[26];
            for (int j = 0; j < A[i].length(); j++) {
                curr[A[i].charAt(j) - 'a']++;
            }
            // Update the common dictionary
            for (int j = 0; j < 26; j++) {
                if (curr[j] < dict[j]) dict[j] = curr[j];
            }
        }
        for (int i = 0; i < 26; i++) {
            for (int j = 0; j < dict[i]; j++) {
                ans.add(Character.toString((char) ('a' + i)));
            }
        }
        return ans;
    }
    ```
- **1010. Pairs of Songs With Total Durations Divisible by 60:** (from leetcode @lee215)

    **Intuition**

    Calculate the time % 60 then it will be exactly same as two sum problem.

    **Explanation**

    t % 60 gets the remainder 0 ~ 59.
    We count the occurrence of each remainders in a array/hashmap c.
    we want to know that, for each t, how many x satisfy (t + x) % 60 = 0.

    One idea is take x % 60 = 60 - t % 60, which is valid for the most cases.
    But if t % 60 = 0, x % 60 = 0 instead of 60.
    60 - t % 60 will get a number in range 1 ~ 60.
    (60 - t % 60) % 60 can get number in range 0 ~ 59, which is what we want.

    Another idea is that x % 60 = (600 - t) % 60.
    Not sure which one is more straight forward.

    ```java
    public int numPairsDivisibleBy60(int[] time) {
        int c[]  = new int[60], res = 0;
        for (int t : time) {
            res += c[(600 - t) % 60];
            c[t % 60] += 1;
        }
        return res;
    }
    ```
- **1051. Height Checker:** There are two way to solve this problem. First, sort the array and compare the different element. Second, maintain a record array.(Actually this is a kind of sort.)
    ```java
    class Solution {
        public int heightChecker(int[] heights) {
            int[] record = new int[101];
            for(int h : heights) record[h]++;
            int curr = 0, res = 0;
            for(int i = 0; i < heights.length; i++){
                while(record[curr] == 0) curr++;
                if(heights[i] != curr) res++;
                record[curr]--;
            }
            return res;
        }
    }
    ```

- **1089. Duplicate Zeros:** (from leetcode @davidluoyes)
    ```java
    class Solution {
        public void duplicateZeros(int[] arr) {
            int zero = 0;
            for(int a : arr) {
                if(a == 0) zero++;
            }
            int bigSize = arr.length + zero;
            for(int i = arr.length-1, j = bigSize-1; i >= 0 && j >= 0; i--, j--){
                if(arr[i] == 0){
                    if(j < arr.length) arr[j] = arr[i];
                    j--;
                    if(j < arr.length) arr[j] = arr[i];
                }else{
                    if(j < arr.length) arr[j] = arr[i];
                }
            }
        }
    }
    ```
- **1128. Number of Equivalent Domino Pairs:** How to check the same pair without order.
  1. ```int key = d[0] > d[1] ? d[0] * 10 + d[1] : d[1] * 10 + d[0];```
  2. ```f(domino) = min(d[0], d[1]) * 10 + max(d[0], d[1])``` (from leetcode @lee215)
  3. Use the product of primes ```primes = [2,3,5,7,11,13,17,19,23,29], f(domino) = primes[d[0]] * primes[d[1]](though primes[0] is not used)``` (from leetcode @sendAsync)
  4. Use the bit manipulation. ```primes = [2,3,5,7,11,13,17,19,23,29], f(domino) = 1 << d[0]| 1 << d[1];``` (from leetcode @sendAsync)
    

## Reference
- Bit Manipulation in Java – Bitwise and Bit Shift operations: https://www.vojtechruzicka.com/bit-manipulation-java-bitwise-bit-shift-operations/
- A Linear Time Majority Vote Algorithm(http://www.cs.utexas.edu/~moore/best-ideas/mjrty/)
- Sum of Even Numbers After Queries:(from leetcode @rock) https://leetcode.com/problems/sum-of-even-numbers-after-queries/discuss/231099/Java-10-liner-odd-even-analysis-time-O(max(m-n))
- Add to Array-Form of Integer: (from leetcode @rock) https://leetcode.com/problems/add-to-array-form-of-integer/discuss/234558/Java-6-liner-w-comment-and-analysis
- Find Common Characters(from leetcode @chillin1017) https://leetcode.com/problems/find-common-characters/discuss/249739/Java-10ms-38mb-clear-solution-with-comments
- Pairs of Songs With Total Durations Divisible by 60
(from leetcode @lee215)https://leetcode.com/problems/pairs-of-songs-with-total-durations-divisible-by-60/discuss/256738/JavaC%2B%2BPython-Two-Sum-with-K-60
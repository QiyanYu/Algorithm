# Array

- An array stores a sequence of values that are all the same type. You can either loop the values by the sequence or access each individual value by index.
- *2D-array:* Array can have one or 2-dimensions array.
- *Fixed Capacity:* Must give the specific array length when you initial the array, since it need to set the memory for it.
- *Dynamic array:* Since the array has a fixed capacity and we need to specify the size of the array when we initialize it. We need dynamic array which with variable size.

# String
- ***Immutable:*** Java String is immutable. If you want to modify any of the characters, you have to create a new string.
- ***The Time Complexity:*** Finding operation is ```O(N)``` and substring operation is ```O(1)``` in Java. (I think leetcode data structure is incorrect about this.(https://leetcode.com/explore/learn/card/array-and-string/203/introduction-to-string/1158/))
- ***String Concatenation in Java:*** The time complexity will be $O(n^2)$. Since concatenation need to allocate memory at every operation. So we better use **```StringBuilder```** which time complexity is ```O(n)```.
# Key points
- Resize Array




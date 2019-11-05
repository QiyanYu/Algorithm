# Linked List

- Unlike the array, we are not able to access a random element in constant time, we have to traverse from the head node one by one. It takes ```O(N)``` time on average to visit an element by index. 
- Singly linked list Insert is ```O(1)``` time complexity.
- Singly linked list Delete is ```O(N)``` time complexity. Since we need to traverse from the head node to find the prev node of the deleted node. Space complexity is ```O(1)```.
- Use two-pointers technology to determine if there is a cycle in the linked list.
- **Always check if the node is null before you call the next field.** For example, before we run ```fast = fast.next.next```, we need to examine both ```fast``` and ```fast.next``` is not null.
- **Carefully define the end conditions of your loop.** Take previous tip into consideration when you define your end conditions.
- Doubly linked list Delete is ```O(1)``` both space and time complexity, since there is no need to traverse linked list to get previous node.
- 
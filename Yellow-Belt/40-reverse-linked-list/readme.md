### Description
Given the `head` of a singly linked list, reverse the list, and return the reversed list.

A singly linked list is a linear data structure where each element (called a node) points to the next element in the sequence. Reversing it means that the last node becomes the first, the second-to-last becomes the second, and so on, with all the pointers flipped to point in the opposite direction.

For example, if your list is `1 -> 2 -> 3 -> NULL`, after reversing, it should become `3 -> 2 -> 1 -> NULL`.

### Constraints
- The number of nodes in the list is in the range `[0, 5000]`.
- `-5000 <= Node.val <= 5000`.

### Example

Input:
1 2 3 4 5

Output:
5 4 3 2 1

(Explanation: The input represents a linked list 1 -> 2 -> 3 -> 4 -> 5 -> NULL. The output is its reversed form: 5 -> 4 -> 3 -> 2 -> 1 -> NULL.)

### Concepts Covered
- **Linked Lists:** Understanding what a node is, how pointers/references connect nodes, and the concept of a `head` and `NULL`/`None` (end of list).
- **Iteration/Traversal:** Moving through a linked list, node by node, using a loop.
- **Pointer Manipulation:** The core of this problem involves carefully changing which node each `next` pointer refers to, effectively 'flipping' the direction of the links.
- **Edge Cases:** Handling special scenarios like an empty list (no nodes) or a list with only one node.
### Description
You are given the head of a singly linked list and an integer `val`. Your task is to delete all the nodes of the linked list that have `Node.val == val` and return the new head of the modified linked list.

This problem tests your understanding of linked list traversal, manipulation, and the crucial aspects of node deletion, including handling edge cases such as deleting the head, nodes in the middle, and the tail of the list, as well as an empty list.

### Constraints
- The number of nodes in the list is in the range `[0, 1000]`.
- Node values are integers in the range `[-1000, 1000]`.
- The target value `val` is an integer in the range `[-1000, 1000]`.

### Example
**Input:**

1 2 6 3 4 5 6
6

**Output:**

1 2 3 4 5


**Explanation:**
The original list is `1 -> 2 -> 6 -> 3 -> 4 -> 5 -> 6 -> NULL`. We need to remove all nodes with the value `6`.
- The first `6` is removed, linking `2` to `3`.
- The second `6` is removed, linking `5` to `NULL`.
The resulting list is `1 -> 2 -> 3 -> 4 -> 5 -> NULL`.

### Concepts Covered
- Singly Linked List Structure
- Linked List Traversal
- Node Deletion (handling head, middle, and tail scenarios)
- Pointer Manipulation

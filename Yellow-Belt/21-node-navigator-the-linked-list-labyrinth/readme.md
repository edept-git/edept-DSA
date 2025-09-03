### Description
You are tasked with a fundamental operation on singly linked lists. Given an array of integers, you must first construct a singly linked list from these values. After the list is created, you will be given a target integer. Your goal is to find the *first occurrence* of this target value in the linked list and delete the corresponding node. If the target value is not found, the list should remain unchanged. Finally, you need to return the head of the modified linked list.

### Constraints
- The number of nodes in the linked list will be between 0 and 1000.
- Each node's value will be an integer between -1000 and 1000.
- The target value will be an integer between -1000 and 1000.

### Example
**Input:**
Array: `[1, 2, 3, 4, 5]`
Target to delete: `3`

**Expected Output:**
Linked List: `1 -> 2 -> 4 -> 5`

### Concepts Covered
- Singly Linked List: Node structure, creation, traversal.
- Pointer/Reference manipulation for deletion.
- Handling edge cases such as deleting the head node or an empty list.
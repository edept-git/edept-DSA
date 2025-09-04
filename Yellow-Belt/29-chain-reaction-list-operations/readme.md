### Description
You are tasked with implementing a basic singly linked list and performing a series of operations on it. Your program should be able to:
1.  **Insert a node at the end** of the list.
2.  **Delete a node at a specific 0-indexed position**. If the index is out of bounds, no deletion should occur.
3.  **Print the current state of the linked list**. If the list is empty, print "List is empty."

Your program will receive a sequence of commands. Each command starts with a character indicating the operation:
*   `I <value>`: Insert `value` at the end of the list.
*   `D <index>`: Delete the node at `index`.
*   `P`: Print the current list.

### Constraints
*   The number of operations `N` will be between 1 and 20.
*   Values inserted will be integers between 0 and 100.
*   Indices for deletion will be between 0 and `N-1` (where N is current list size).
*   The list will not contain duplicate values (for simplicity, not an implementation constraint).
*   The list size will not exceed 20 elements at any point.

### Example
#### Input:

I 10
I 20
P
I 30
D 1
P
D 5
P


#### Output:

10 20
10 30
10


### Concepts Covered
*   Singly Linked List structure (Node, head pointer)
*   Linked List Traversal
*   Node Insertion (specifically at the end)
*   Node Deletion (at a specific index, handling head deletion)
### Description
A singly linked list is a fundamental data structure consisting of a sequence of nodes, where each node contains data and a pointer (or reference) to the next node in the sequence. The last node points to `NULL` (or `None`).

Your task is to implement a basic singly linked list and perform common operations on it:
1.  **Insertion at the End**: Add a new node with a given value to the end of the list.
2.  **Deletion of a Specific Node**: Remove the first occurrence of a node with a given value from the list. If the value is not found, the list remains unchanged.
3.  **Traversal and Printing**: Print all elements of the list, separated by spaces. If the list is empty, print nothing.

You will receive a series of commands:
*   `insert <value>`: Inserts `value` at the end of the list.
*   `delete <value>`: Deletes the first node found with `value`.
*   `print`: Prints the current state of the list.

### Constraints
*   The number of operations `N` will be between 1 and 100.
*   Node values will be integers between -1000 and 1000.
*   The `delete` command may target a value that does not exist in the list.
*   An empty line will be considered as an empty list for `print` command.

### Example
Input:
insert 5
insert 10
print
delete 5
insert 20
print
delete 100
print

Output:
5 10
10 20
10 20

### Concepts Covered
*   Singly Linked List structure
*   Node creation and manipulation
*   Traversal through a linked list
*   Insertion of a node at the end
*   Deletion of a specific node by value

### Description
You're tasked with enhancing a Doubly Linked List (DLL) by implementing a function to append a new node to its very end. Given the head and tail of an existing DLL (which might be empty) and an integer value, your goal is to create a new node with this value and add it as the new tail of the list. Remember to correctly update all `next` and `prev` pointers, including those of the old tail (if it exists) and the new node itself.

### Constraints
*   The input list can be empty.
*   The number of nodes `N` in the initial list will be between `0` and `1000`.
*   The value `V` to insert will be an integer between `-10^9` and `10^9`.
*   The `head` and `tail` pointers should always correctly point to the beginning and end of the list, respectively, after the operation.

### Example
#### Example 1:
**Input:**

1 2 3
4

(Initial DLL: `1 <-> 2 <-> 3`, Value to insert: `4`)

**Output:**

1 <-> 2 <-> 3 <-> 4


#### Example 2:
**Input:**

EMPTY
5

(Initial DLL: `Empty List`, Value to insert: `5`)

**Output:**

5


### Concepts Covered
*   **Doubly Linked Lists**: Understanding the structure of nodes with `data`, `next`, and `prev` pointers.
*   **Node Structure**: Defining and instantiating individual nodes.
*   **Head/Tail Pointers**: Correctly managing the `head` (start) and `tail` (end) of the list.
*   **Pointer Manipulation**: Updating `next` and `prev` pointers to maintain list integrity.
*   **Edge Case Handling**: Specifically, handling an empty list as an initial state.
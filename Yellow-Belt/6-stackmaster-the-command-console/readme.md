### Description
Your mission is to implement a basic Stack data structure that supports four fundamental operations: `push`, `pop`, `top`, and `isEmpty`. You will receive a sequence of commands, and your program must process them, outputting results for `pop`, `top`, and `isEmpty` operations.

The stack should adhere to the Last-In, First-Out (LIFO) principle. For operations that attempt to `pop` or retrieve `top` from an empty stack, a specific error value (`-1`) should be returned. Similarly, `push` operations should handle the case where the stack is at its maximum capacity.

### Constraints
*   The stack will have a maximum capacity of `1000` elements.
*   The number of operations `N` will be between `1` and `1000`.
*   Values pushed onto the stack will be integers between `-10^9` and `10^9`.
*   Operations will be one of the following strings:
    *   `push <value>`: Adds `value` to the top of the stack.
    *   `pop`: Removes and returns the top element.
    *   `top`: Returns the top element without removing it.
    *   `isEmpty`: Returns `true` if the stack is empty, `false` otherwise.

### Example
#### Input:

8
push 10
push 20
pop
top
isEmpty
pop
pop
isEmpty


#### Output:

20
10
false
10
-1
true


### Concepts Covered
*   Stack Data Structure (LIFO principle)
*   Array-based implementation of a stack
*   Maintaining a 'top' pointer/index
*   Handling stack overflow (when `push` fails due to full capacity)
*   Handling stack underflow (when `pop` or `top` are called on an empty stack)
*   Basic input/output parsing
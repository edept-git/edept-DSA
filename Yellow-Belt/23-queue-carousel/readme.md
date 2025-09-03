### Description

Welcome to the Queue Carousel! Your task is to implement a `MyCircularQueue` class that supports all the standard operations of a circular queue. A circular queue, also known as a ring buffer, is a linear data structure that operates on the FIFO (First-In, First-Out) principle. Unlike a regular queue, it reuses empty spaces by connecting the rear of the queue to the front, forming a circular structure. This makes it efficient for fixed-size buffers.

You will need to implement the following methods:

*   `MyCircularQueue(k)`: Constructor, initializes the queue with a maximum capacity of `k` elements.
*   `enqueue(value)`: Inserts an element into the circular queue. Returns `true` if the operation is successful, `false` otherwise (e.g., if the queue is full).
*   `dequeue()`: Deletes an element from the circular queue. Returns `true` if the operation is successful, `false` otherwise (e.g., if the queue is empty).
*   `front()`: Gets the front item from the queue. Returns the element if the queue is not empty, otherwise returns `-1`.
*   `rear()`: Gets the last item from the queue. Returns the element if the queue is not empty, otherwise returns `-1`.
*   `isEmpty()`: Checks whether the circular queue is empty. Returns `true` if empty, `false` otherwise.
*   `isFull()`: Checks whether the circular queue is full. Returns `true` if full, `false` otherwise.

### Constraints

*   `1 <= k <= 1000` (The capacity of the queue)
*   `0 <= value <= 1000` (The value to enqueue)
*   At most `3000` calls will be made to `enqueue`, `dequeue`, `front`, `rear`, `isEmpty`, and `isFull`.
*   All values returned by `front()` and `rear()` for an empty queue should be `-1`.

### Example

**Input:**

3
MyCircularQueue enqueue 1
MyCircularQueue enqueue 2
MyCircularQueue enqueue 3
MyCircularQueue isFull
MyCircularQueue dequeue
MyCircularQueue enqueue 4
MyCircularQueue front
MyCircularQueue rear
MyCircularQueue isEmpty
MyCircularQueue dequeue
MyCircularQueue dequeue
MyCircularQueue dequeue
MyCircularQueue isEmpty
MyCircularQueue front
MyCircularQueue enqueue 5
MyCircularQueue rear


**Output:**

true
true
true
true
1
3
false
true
true
true
-1
5


### Concepts Covered

*   **Arrays:** Using a fixed-size array to store queue elements.
*   **Pointers/Indices:** Managing `front` and `rear` pointers (or indices) to keep track of the queue's boundaries.
*   **Modulo Operator:** Essential for wrapping around the array and implementing the circular behavior.
*   **Queue Data Structure:** Understanding the FIFO principle and basic queue operations.
*   **Edge Cases:** Handling conditions like an empty queue, a full queue, and transitions between these states.

### Description
A standard queue follows a First-In-First-Out (FIFO) principle, where elements are added at the rear and removed from the front. However, when implemented with a fixed-size array, a standard queue can run into an issue where even if there's empty space at the beginning of the array, new elements cannot be added if the rear pointer reaches the end of the array.

A **Circular Queue** solves this problem by treating the array as if its ends are connected, forming a circle. When an element is added or removed, the pointers (`front` and `rear`) move in a circular fashion using the modulo operator. This allows for efficient reuse of space within a fixed-size array.

Your task is to implement a `MyCircularQueue` class that supports the following operations:
*   `MyCircularQueue(int k)`: Initializes the object with the size of the queue to be `k`.
*   `enqueue(int value)`: Inserts an element into the circular queue. Returns `true` if the operation is successful, `false` otherwise (if the queue is full).
*   `dequeue()`: Deletes an element from the circular queue. Returns `true` if the operation is successful, `false` otherwise (if the queue is empty).
*   `front()`: Gets the front item from the queue. Returns `-1` if the queue is empty.
*   `rear()`: Gets the last item from the queue. Returns `-1` if the queue is empty.
*   `isEmpty()`: Checks whether the circular queue is empty. Returns `true` if empty, `false` otherwise.
*   `isFull()`: Checks whether the circular queue is full. Returns `true` if full, `false` otherwise.

### Constraints
*   `1 <= k <= 1000` (Capacity of the circular queue)
*   `-1000 <= value <= 1000` (Value to enqueue)
*   At most `10000` calls will be made to `enqueue`, `dequeue`, `front`, `rear`, `isEmpty`, and `isFull`.
*   All values returned by `front()` and `rear()` for an empty queue should be `-1`.

### Example
**Input:**
MyCircularQueue 3
enqueue 1
enqueue 2
enqueue 3
enqueue 4
rear
isFull
dequeue
enqueue 4
rear
front
isEmpty
dequeue
dequeue
dequeue
isEmpty
front
exit

**Output:**
null
true
true
true
false
3
true
true
true
4
2
false
true
true
true
true
-1

### Concepts Covered
*   Queue Data Structure (FIFO)
*   Array-based Implementation
*   Circular Array (using Modulo Arithmetic)
*   Pointers (Front and Rear) Management
*   Fixed-Size Data Structures
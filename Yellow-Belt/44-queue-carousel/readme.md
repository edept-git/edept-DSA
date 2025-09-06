### Description
A circular queue is a linear data structure that operates in a First-In, First-Out (FIFO) manner, similar to a regular queue. The key difference is that the last position is connected back to the first position, forming a circle. This allows for efficient reuse of array space once elements are dequeued from the front.

Your task is to implement a `CircularQueue` class (or equivalent structure) that supports the following operations:

*   `CircularQueue(k)`: Initializes the queue with a maximum capacity of `k` elements.
*   `enqueue(value)`: Adds an element `value` to the rear of the queue. Returns `true` if the operation was successful, `false` otherwise (if the queue is full).
*   `dequeue()`: Removes an element from the front of the queue. Returns `true` if the operation was successful, `false` otherwise (if the queue is empty).
*   `front()`: Gets the front element of the queue. Returns the element if the queue is not empty, ` -1` otherwise.
*   `rear()`: Gets the last element of the queue. Returns the element if the queue is not empty, `-1` otherwise.
*   `isEmpty()`: Checks whether the circular queue is empty. Returns `true` if empty, `false` otherwise.
*   `isFull()`: Checks whether the circular queue is full. Returns `true` if full, `false` otherwise.

All values will be integers.

### Constraints
*   `1 <= k <= 1000` (capacity)
*   `0 <= value <= 1000` (values to enqueue)
*   At most `1000` calls will be made to `enqueue`, `dequeue`, `front`, `rear`, `isEmpty`, and `isFull`.

### Example
**Input:**

init 3
enqueue 1
enqueue 2
enqueue 3
enqueue 4
rear
isFull
dequeue
enqueue 4
front


**Output:**

true
true
true
false
3
true
true
4


**Explanation:**
1.  `CircularQueue circularQueue = new CircularQueue(3);` // Initializes with capacity 3.
2.  `circularQueue.enqueue(1);` // Returns true. Queue: [1]
3.  `circularQueue.enqueue(2);` // Returns true. Queue: [1, 2]
4.  `circularQueue.enqueue(3);` // Returns true. Queue: [1, 2, 3]
5.  `circularQueue.enqueue(4);` // Returns false, queue is full. Queue: [1, 2, 3]
6.  `circularQueue.rear();` // Returns 3.
7.  `circularQueue.isFull();` // Returns true.
8.  `circularQueue.dequeue();` // Returns true. Queue: [2, 3]
9.  `circularQueue.enqueue(4);` // Returns true. Queue: [2, 3, 4]
10. `circularQueue.front();` // Returns 2.

### Concepts Covered
*   Array-based queue implementation
*   Circular array concept using the modulo operator (`%`)
*   Managing `front` and `rear` pointers (or indices)
*   Handling queue empty and full conditions
*   First-In, First-Out (FIFO) principle
### Description

A circular queue is a linear data structure that operates in a First-In, First-Out (FIFO) manner, similar to a regular queue. However, it handles the `rear` and `front` pointers in a way that allows it to reuse empty spaces from the front of the queue, effectively treating the buffer as a circle. This prevents wasted memory if elements are frequently enqueued and dequeued.

Your task is to implement the `MyCircularQueue` class, which supports the following operations:

- `MyCircularQueue(k)`: Initializes the object with the size of the queue to be `k`. All values will be in the range `[0, 1000]`.
- `enqueue(value)`: Inserts an element into the circular queue. Returns `true` if the operation is successful, `false` otherwise (if the queue is full).
- `dequeue()`: Deletes an element from the circular queue. Returns `true` if the operation is successful, `false` otherwise (if the queue is empty).
- `Front()`: Gets the front element from the queue. Returns the element value, or `-1` if the queue is empty.
- `Rear()`: Gets the last element from the queue. Returns the element value, or `-1` if the queue is empty.
- `isEmpty()`: Checks whether the circular queue is empty. Returns `true` if empty, `false` otherwise.
- `isFull()`: Checks whether the circular queue is full. Returns `true` if full, `false` otherwise.

You should implement your circular queue using an array (or equivalent data structure) and manage the `front` and `rear` pointers using modulo arithmetic.

### Constraints

- `1 <= k <= 1000` (Capacity of the queue)
- `0 <= value <= 1000` (Values to enqueue)
- At most `3000` calls will be made to `enqueue`, `dequeue`, `Front`, `Rear`, `isEmpty`, and `isFull`.
- All operations run in O(1) time.

### Example

**Input Format:**
The first line contains an integer `k`, representing the capacity of the circular queue.
The second line contains an integer `n`, representing the total number of operations to perform.
Each of the next `n` lines contains a command string, optionally followed by an integer argument if the command is `enqueue`.

**Output Format:**
For each operation that returns a value (`enqueue`, `dequeue`, `Front`, `Rear`, `isEmpty`, `isFull`), print the result on a new line.

Input:
3
10
enqueue 1
enqueue 2
enqueue 3
enqueue 4
Rear
isFull
dequeue
enqueue 4
Rear
Front

Output:
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

### Concepts Covered

- Array/Vector Data Structure
- Queue Data Structure Principles (FIFO)
- Modulo Arithmetic
- Pointer Management (front, rear indices)
- Fixed-Size Buffer


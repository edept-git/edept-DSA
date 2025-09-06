# Solutions for Queue Carousel

### Approach
The problem requires implementing a circular queue using an array. This approach leverages a fixed-size array to store elements and two pointers, `front` and `rear`, to manage the head and tail of the queue, respectively. Additionally, a `count` variable is maintained to keep track of the current number of elements in the queue.
Initialization sets `front` and `rear` to `0` and `count` to `0`. The maximum capacity `k` is stored.
When `enqueue(value)` is called:
First, it checks if the queue is `isFull()`. If so, it returns `false`. Otherwise, the `value` is placed at `data[rear]`, `rear` is updated using the modulo operator (`rear = (rear + 1) % capacity`) to ensure circularity, and `count` is incremented. It then returns `true`.
When `dequeue()` is called:
First, it checks if the queue is `isEmpty()`. If so, it returns `false`. Otherwise, the element at `data[front]` is considered removed, `front` is updated using the modulo operator (`front = (front + 1) % capacity`), and `count` is decremented. It then returns `true`.
The `front()` operation returns `data[front]` if the queue is not empty, otherwise `-1`. The `rear()` operation returns `data[(rear - 1 + capacity) % capacity]` if the queue is not empty, otherwise `-1`. The `isEmpty()` and `isFull()` operations simply check if `count` is `0` or equal to `capacity`, respectively.
This implementation provides `O(1)` time complexity for all `enqueue`, `dequeue`, `front`, `rear`, `isEmpty`, and `isFull` operations, as they involve constant-time array access and pointer arithmetic. The space complexity is `O(k)` to store the queue elements in the underlying array.

## C Solution
```c
#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>
#include <string.h>

typedef struct {
    int* queue_arr;
    int front;
    int rear; // points to the next available slot
    int count;
    int capacity;
} CircularQueue;

CircularQueue* circularQueueCreate(int k) {
    CircularQueue* obj = (CircularQueue*)malloc(sizeof(CircularQueue));
    if (obj == NULL) return NULL; // Handle allocation failure
    obj->queue_arr = (int*)malloc(sizeof(int) * k);
    if (obj->queue_arr == NULL) { // Handle allocation failure
        free(obj);
        return NULL;
    }
    obj->front = 0;
    obj->rear = 0;
    obj->count = 0;
    obj->capacity = k;
    return obj;
}

bool circularQueueIsEmpty(CircularQueue* obj) {
    return obj->count == 0;
}

bool circularQueueIsFull(CircularQueue* obj) {
    return obj->count == obj->capacity;
}

bool circularQueueEnqueue(CircularQueue* obj, int value) {
    if (circularQueueIsFull(obj)) {
        return false;
    }
    obj->queue_arr[obj->rear] = value;
    obj->rear = (obj->rear + 1) % obj->capacity;
    obj->count++;
    return true;
}

bool circularQueueDequeue(CircularQueue* obj) {
    if (circularQueueIsEmpty(obj)) {
        return false;
    }
    obj->front = (obj->front + 1) % obj->capacity;
    obj->count--;
    return true;
}

int circularQueueFront(CircularQueue* obj) {
    if (circularQueueIsEmpty(obj)) {
        return -1;
    }
    return obj->queue_arr[obj->front];
}

int circularQueueRear(CircularQueue* obj) {
    if (circularQueueIsEmpty(obj)) {
        return -1;
    }
    // The actual rear element is at (rear - 1 + capacity) % capacity
    // Adding capacity before modulo handles cases where (rear - 1) might be negative (e.g., rear=0)
    return obj->queue_arr[(obj->rear - 1 + obj->capacity) % obj->capacity];
}

void circularQueueFree(CircularQueue* obj) {
    if (obj == NULL) return;
    free(obj->queue_arr);
    free(obj);
}

int main() {
    CircularQueue* cq = NULL;
    char command[20];
    int k_val, value_val;

    while (scanf("%s", command) != EOF) {
        if (strcmp(command, "init") == 0) {
            scanf("%d", &k_val);
            if (cq != NULL) {
                circularQueueFree(cq); // Free previous queue if exists
            }
            cq = circularQueueCreate(k_val);
        } else if (strcmp(command, "enqueue") == 0) {
            scanf("%d", &value_val);
            printf("%s\n", circularQueueEnqueue(cq, value_val) ? "true" : "false");
        } else if (strcmp(command, "dequeue") == 0) {
            printf("%s\n", circularQueueDequeue(cq) ? "true" : "false");
        } else if (strcmp(command, "front") == 0) {
            printf("%d\n", circularQueueFront(cq));
        } else if (strcmp(command, "rear") == 0) {
            printf("%d\n", circularQueueRear(cq));
        } else if (strcmp(command, "isEmpty") == 0) {
            printf("%s\n", circularQueueIsEmpty(cq) ? "true" : "false");
        } else if (strcmp(command, "isFull") == 0) {
            printf("%s\n", circularQueueIsFull(cq) ? "true" : "false");
        }
    }
    circularQueueFree(cq); // Free final queue

    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <vector>
#include <string>
#include <sstream>

class CircularQueue {
private:
    std::vector<int> queue;
    int front_ptr;
    int rear_ptr; // points to the next available slot
    int current_count;
    int capacity;

public:
    CircularQueue(int k) {
        queue.resize(k);
        front_ptr = 0;
        rear_ptr = 0;
        current_count = 0;
        capacity = k;
    }

    bool enqueue(int value) {
        if (isFull()) {
            return false;
        }
        queue[rear_ptr] = value;
        rear_ptr = (rear_ptr + 1) % capacity;
        current_count++;
        return true;
    }

    bool dequeue() {
        if (isEmpty()) {
            return false;
        }
        front_ptr = (front_ptr + 1) % capacity;
        current_count--;
        return true;
    }

    int front() {
        if (isEmpty()) {
            return -1;
        }
        return queue[front_ptr];
    }

    int rear() {
        if (isEmpty()) {
            return -1;
        }
        // The actual rear element is at (rear_ptr - 1 + capacity) % capacity
        // Adding capacity before modulo handles cases where (rear_ptr - 1) might be negative (e.g., rear_ptr=0)
        return queue[(rear_ptr - 1 + capacity) % capacity];
    }

    bool isEmpty() {
        return current_count == 0;
    }

    bool isFull() {
        return current_count == capacity;
    }
};

int main() {
    std::ios_base::sync_with_stdio(false);
    std::cin.tie(NULL);

    CircularQueue* circularQueue = nullptr;
    std::string line;

    while (std::getline(std::cin, line)) {
        std::stringstream ss(line);
        std::string command;
        ss >> command;

        if (command == "init") {
            int k;
            ss >> k;
            if (circularQueue != nullptr) {
                delete circularQueue; // Clean up previous queue if any
            }
            circularQueue = new CircularQueue(k);
        } else if (command == "enqueue") {
            int value;
            ss >> value;
            std::cout << (circularQueue->enqueue(value) ? "true" : "false") << std::endl;
        } else if (command == "dequeue") {
            std::cout << (circularQueue->dequeue() ? "true" : "false") << std::endl;
        } else if (command == "front") {
            std::cout << circularQueue->front() << std::endl;
        } else if (command == "rear") {
            std::cout << circularQueue->rear() << std::endl;
        } else if (command == "isEmpty") {
            std::cout << (circularQueue->isEmpty() ? "true" : "false") << std::endl;
        } else if (command == "isFull") {
            std::cout << (circularQueue->isFull() ? "true" : "false") << std::endl;
        }
    }

    if (circularQueue != nullptr) {
        delete circularQueue; // Clean up allocated memory
    }

    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

class CircularQueue {
    private int[] queue;
    private int front;
    private int rear; // points to the next available slot
    private int count;
    private int capacity;

    public CircularQueue(int k) {
        queue = new int[k];
        front = 0;
        rear = 0;
        count = 0;
        capacity = k;
    }

    public boolean enqueue(int value) {
        if (isFull()) {
            return false;
        }
        queue[rear] = value;
        rear = (rear + 1) % capacity;
        count++;
        return true;
    }

    public boolean dequeue() {
        if (isEmpty()) {
            return false;
        }
        front = (front + 1) % capacity;
        count--;
        return true;
    }

    public int front() {
        if (isEmpty()) {
            return -1;
        }
        return queue[front];
    }

    public int rear() {
        if (isEmpty()) {
            return -1;
        }
        // The actual rear element is at (rear - 1 + capacity) % capacity
        // Adding capacity before modulo handles cases where (rear - 1) might be negative (e.g., rear=0)
        return queue[(rear - 1 + capacity) % capacity];
    }

    public boolean isEmpty() {
        return count == 0;
    }

    public boolean isFull() {
        return count == capacity;
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        CircularQueue circularQueue = null;

        while (scanner.hasNextLine()) {
            String line = scanner.nextLine();
            String[] parts = line.trim().split(" ");
            String command = parts[0];

            switch (command) {
                case "init":
                    int k = Integer.parseInt(parts[1]);
                    circularQueue = new CircularQueue(k);
                    break;
                case "enqueue":
                    int value = Integer.parseInt(parts[1]);
                    System.out.println(circularQueue.enqueue(value));
                    break;
                case "dequeue":
                    System.out.println(circularQueue.dequeue());
                    break;
                case "front":
                    System.out.println(circularQueue.front());
                    break;
                case "rear":
                    System.out.println(circularQueue.rear());
                    break;
                case "isEmpty":
                    System.out.println(circularQueue.isEmpty());
                    break;
                case "isFull":
                    System.out.println(circularQueue.isFull());
                    break;
            }
        }
        scanner.close();
    }
}
```

## Python Solution
```python
import sys

class CircularQueue:
    def __init__(self, k: int):
        self.queue = [0] * k
        self.front = 0
        self.rear = 0 # points to the next available slot
        self.count = 0
        self.capacity = k

    def enqueue(self, value: int) -> bool:
        if self.isFull():
            return False
        self.queue[self.rear] = value
        self.rear = (self.rear + 1) % self.capacity
        self.count += 1
        return True

    def dequeue(self) -> bool:
        if self.isEmpty():
            return False
        self.front = (self.front + 1) % self.capacity
        self.count -= 1
        return True

    def front(self) -> int:
        if self.isEmpty():
            return -1
        return self.queue[self.front]

    def rear(self) -> int:
        if self.isEmpty():
            return -1
        # The actual rear element is at (rear - 1 + capacity) % capacity
        # Adding capacity before modulo handles cases where (rear - 1) might be negative (e.g., rear=0)
        return self.queue[(self.rear - 1 + self.capacity) % self.capacity]

    def isEmpty(self) -> bool:
        return self.count == 0

    def isFull(self) -> bool:
        return self.count == self.capacity

# Main function to handle I/O
def solve():
    circular_queue = None
    results = []

    for line in sys.stdin:
        parts = line.strip().split()
        command = parts[0]

        if command == "init":
            k = int(parts[1])
            circular_queue = CircularQueue(k)
        elif command == "enqueue":
            value = int(parts[1])
            results.append(str(circular_queue.enqueue(value)).lower())
        elif command == "dequeue":
            results.append(str(circular_queue.dequeue()).lower())
        elif command == "front":
            results.append(str(circular_queue.front()))
        elif command == "rear":
            results.append(str(circular_queue.rear()))
        elif command == "isEmpty":
            results.append(str(circular_queue.isEmpty()).lower())
        elif command == "isFull":
            results.append(str(circular_queue.isFull()).lower())
    
    for res in results:
        print(res)

solve()

```

## JavaScript Solution
```javascript
class CircularQueue {
    constructor(k) {
        this.queue = new Array(k);
        this.front = 0;
        this.rear = 0; // points to the next available slot
        this.count = 0;
        this.capacity = k;
    }

    enqueue(value) {
        if (this.isFull()) {
            return false;
        }
        this.queue[this.rear] = value;
        this.rear = (this.rear + 1) % this.capacity;
        this.count++;
        return true;
    }

    dequeue() {
        if (this.isEmpty()) {
            return false;
        }
        this.front = (this.front + 1) % this.capacity;
        this.count--;
        return true;
    }

    front() {
        if (this.isEmpty()) {
            return -1;
        }
        return this.queue[this.front];
    }

    rear() {
        if (this.isEmpty()) {
            return -1;
        }
        // The actual rear element is at (rear - 1 + capacity) % capacity
        // Adding capacity before modulo handles cases where (rear - 1) might be negative (e.g., rear=0)
        return this.queue[(this.rear - 1 + this.capacity) % this.capacity];
    }

    isEmpty() {
        return this.count === 0;
    }

    isFull() {
        return this.count === this.capacity;
    }
}

// Main function to handle I/O
function solve() {
    let circularQueue = null;
    const results = [];
    // Read input from stdin for Node.js environment
    // In a browser environment, this part would be different (e.g., prompt, event listeners)
    const inputLines = require('fs').readFileSync(0, 'utf-8').trim().split('\n');
    
    for (const line of inputLines) {
        const parts = line.trim().split(' ');
        const command = parts[0];

        switch (command) {
            case "init":
                const k = parseInt(parts[1]);
                circularQueue = new CircularQueue(k);
                break;
            case "enqueue":
                const value = parseInt(parts[1]);
                results.push(circularQueue.enqueue(value).toString());
                break;
            case "dequeue":
                results.push(circularQueue.dequeue().toString());
                break;
            case "front":
                results.push(circularQueue.front().toString());
                break;
            case "rear":
                results.push(circularQueue.rear().toString());
                break;
            case "isEmpty":
                results.push(circularQueue.isEmpty().toString());
                break;
            case "isFull":
                results.push(circularQueue.isFull().toString());
                break;
        }
    }
    
    console.log(results.join('\n'));
}

solve();
```
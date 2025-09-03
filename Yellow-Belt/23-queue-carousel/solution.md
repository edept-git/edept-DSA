# Solutions for Queue Carousel

### Approach
This problem can be solved efficiently by using a fixed-size array to store the queue elements and two pointers, `front` and `rear`, to keep track of the head and tail of the queue, respectively. We also maintain a `currentSize` variable to easily determine if the queue is empty or full. Initially, `front` is set to `0`, `rear` to `-1` (or `0` if it points to the next available slot, but `-1` is clearer for an empty queue's last element), and `currentSize` to `0`. The `capacity` is determined by the `k` parameter given in the constructor. The modulo operator (`%`) is crucial for implementing the circular behavior, allowing `front` and `rear` pointers to wrap around to the beginning of the array when they reach the end.

For `enqueue(value)`: First, check if the queue is full using `currentSize == capacity`. If it is, return `false`. Otherwise, increment `rear` (using `(rear + 1) % capacity`) to find the next available slot, place the `value` at `data[rear]`, and increment `currentSize`. Return `true`. For `dequeue()`: First, check if the queue is empty using `currentSize == 0`. If it is, return `false`. Otherwise, increment `front` (using `(front + 1) % capacity`) and decrement `currentSize`. Return `true`. `front()` simply returns `data[front]` if the queue is not empty, otherwise `-1`. `rear()` returns `data[rear]` if not empty, otherwise `-1`. `isEmpty()` checks if `currentSize == 0`, and `isFull()` checks if `currentSize == capacity`. All operations, including construction, take constant time, O(1), making this a very efficient implementation. The space complexity is O(k) for storing the array elements, where `k` is the maximum capacity of the queue.

## C Solution
```c
#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>
#include <string.h>

typedef struct {
    int* data;
    int front;
    int rear;
    int capacity;
    int currentSize;
} MyCircularQueue;

MyCircularQueue* myCircularQueueCreate(int k) {
    MyCircularQueue* obj = (MyCircularQueue*)malloc(sizeof(MyCircularQueue));
    obj->data = (int*)malloc(sizeof(int) * k);
    obj->capacity = k;
    obj->front = 0;
    obj->rear = -1; // -1 indicates an empty queue, rear will become 0 upon first enqueue
    obj->currentSize = 0;
    return obj;
}

bool myCircularQueueIsEmpty(MyCircularQueue* obj) {
    return obj->currentSize == 0;
}

bool myCircularQueueIsFull(MyCircularQueue* obj) {
    return obj->currentSize == obj->capacity;
}

bool myCircularQueueEnQueue(MyCircularQueue* obj, int value) {
    if (myCircularQueueIsFull(obj)) {
        return false;
    }
    obj->rear = (obj->rear + 1) % obj->capacity;
    obj->data[obj->rear] = value;
    obj->currentSize++;
    return true;
}

bool myCircularQueueDeQueue(MyCircularQueue* obj) {
    if (myCircularQueueIsEmpty(obj)) {
        return false;
    }
    obj->front = (obj->front + 1) % obj->capacity;
    obj->currentSize--;
    return true;
}

int myCircularQueueFront(MyCircularQueue* obj) {
    if (myCircularQueueIsEmpty(obj)) {
        return -1;
    }
    return obj->data[obj->front];
}

int myCircularQueueRear(MyCircularQueue* obj) {
    if (myCircularQueueIsEmpty(obj)) {
        return -1;
    }
    return obj->data[obj->rear];
}

void myCircularQueueFree(MyCircularQueue* obj) {
    free(obj->data);
    free(obj);
}

int main() {
    int k;
    scanf("%d", &k);

    MyCircularQueue* obj = myCircularQueueCreate(k);

    char command[50];
    char operation[20];
    int value;

    while (scanf("%s", command) != EOF) {
        scanf("%s", operation);
        if (strcmp(operation, "enqueue") == 0) {
            scanf("%d", &value);
            printf("%s\n", myCircularQueueEnQueue(obj, value) ? "true" : "false");
        } else if (strcmp(operation, "dequeue") == 0) {
            printf("%s\n", myCircularQueueDeQueue(obj) ? "true" : "false");
        } else if (strcmp(operation, "front") == 0) {
            printf("%d\n", myCircularQueueFront(obj));
        } else if (strcmp(operation, "rear") == 0) {
            printf("%d\n", myCircularQueueRear(obj));
        } else if (strcmp(operation, "isEmpty") == 0) {
            printf("%s\n", myCircularQueueIsEmpty(obj) ? "true" : "false");
        } else if (strcmp(operation, "isFull") == 0) {
            printf("%s\n", myCircularQueueIsFull(obj) ? "true" : "false");
        }
    }

    myCircularQueueFree(obj);

    return 0;
}

```

## C++ Solution
```cpp
#include <iostream>
#include <vector>
#include <string>

class MyCircularQueue {
private:
    std::vector<int> data;
    int front;
    int rear;
    int capacity;
    int currentSize;

public:
    MyCircularQueue(int k) {
        data.resize(k);
        capacity = k;
        front = 0;
        rear = -1; // -1 indicates an empty queue, rear will become 0 upon first enqueue
        currentSize = 0;
    }

    bool enQueue(int value) {
        if (isFull()) {
            return false;
        }
        rear = (rear + 1) % capacity;
        data[rear] = value;
        currentSize++;
        return true;
    }

    bool deQueue() {
        if (isEmpty()) {
            return false;
        }
        front = (front + 1) % capacity;
        currentSize--;
        return true;
    }

    int Front() {
        if (isEmpty()) {
            return -1;
        }
        return data[front];
    }

    int Rear() {
        if (isEmpty()) {
            return -1;
        }
        return data[rear];
    }

    bool isEmpty() {
        return currentSize == 0;
    }

    bool isFull() {
        return currentSize == capacity;
    }
};

int main() {
    int k;
    std::cin >> k;

    MyCircularQueue* obj = new MyCircularQueue(k);

    std::string command_prefix; // To consume 'MyCircularQueue'
    std::string operation;
    int value;

    while (std::cin >> command_prefix >> operation) {
        if (operation == "enqueue") {
            std::cin >> value;
            std::cout << (obj->enQueue(value) ? "true" : "false") << std::endl;
        } else if (operation == "dequeue") {
            std::cout << (obj->deQueue() ? "true" : "false") << std::endl;
        } else if (operation == "front") {
            std::cout << obj->Front() << std::endl;
        } else if (operation == "rear") {
            std::cout << obj->Rear() << std::endl;
        } else if (operation == "isEmpty") {
            std::cout << (obj->isEmpty() ? "true" : "false") << std::endl;
        } else if (operation == "isFull") {
            std::cout << (obj->isFull() ? "true" : "false") << std::endl;
        }
    }

    delete obj;

    return 0;
}

```

## Java Solution
```java
import java.util.Scanner;

class MyCircularQueue {
    private int[] data;
    private int front;
    private int rear;
    private int capacity;
    private int currentSize;

    public MyCircularQueue(int k) {
        data = new int[k];
        capacity = k;
        front = 0;
        rear = -1; // -1 indicates an empty queue, rear will become 0 upon first enqueue
        currentSize = 0;
    }

    public boolean enQueue(int value) {
        if (isFull()) {
            return false;
        }
        rear = (rear + 1) % capacity;
        data[rear] = value;
        currentSize++;
        return true;
    }

    public boolean deQueue() {
        if (isEmpty()) {
            return false;
        }
        front = (front + 1) % capacity;
        currentSize--;
        return true;
    }

    public int Front() {
        if (isEmpty()) {
            return -1;
        }
        return data[front];
    }

    public int Rear() {
        if (isEmpty()) {
            return -1;
        }
        return data[rear];
    }

    public boolean isEmpty() {
        return currentSize == 0;
    }

    public boolean isFull() {
        return currentSize == capacity;
    }
}

public class Solution {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int k = scanner.nextInt();
        scanner.nextLine(); // Consume the newline

        MyCircularQueue obj = new MyCircularQueue(k);

        while (scanner.hasNextLine()) {
            String line = scanner.nextLine().trim();
            if (line.isEmpty()) {
                continue;
            }
            String[] parts = line.split(" ");
            String operation = parts[1];

            switch (operation) {
                case "enqueue":
                    int value = Integer.parseInt(parts[2]);
                    System.out.println(obj.enQueue(value) ? "true" : "false");
                    break;
                case "dequeue":
                    System.out.println(obj.deQueue() ? "true" : "false");
                    break;
                case "front":
                    System.out.println(obj.Front());
                    break;
                case "rear":
                    System.out.println(obj.Rear());
                    break;
                case "isEmpty":
                    System.out.println(obj.isEmpty() ? "true" : "false");
                    break;
                case "isFull":
                    System.out.println(obj.isFull() ? "true" : "false");
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

class MyCircularQueue:

    def __init__(self, k: int):
        self.data = [0] * k
        self.capacity = k
        self.front = 0
        self.rear = -1  # -1 indicates an empty queue, rear will become 0 upon first enqueue
        self.current_size = 0

    def enQueue(self, value: int) -> bool:
        if self.isFull():
            return False
        self.rear = (self.rear + 1) % self.capacity
        self.data[self.rear] = value
        self.current_size += 1
        return True

    def deQueue(self) -> bool:
        if self.isEmpty():
            return False
        self.front = (self.front + 1) % self.capacity
        self.current_size -= 1
        return True

    def Front(self) -> int:
        if self.isEmpty():
            return -1
        return self.data[self.front]

    def Rear(self) -> int:
        if self.isEmpty():
            return -1
        return self.data[self.rear]

    def isEmpty(self) -> bool:
        return self.current_size == 0

    def isFull(self) -> bool:
        return self.current_size == self.capacity

def main():
    k = int(sys.stdin.readline().strip())
    obj = MyCircularQueue(k)

    for line in sys.stdin:
        parts = line.strip().split()
        # The problem statement example has 'MyCircularQueue' prefix, ignore it.
        operation = parts[1]

        if operation == "enqueue":
            value = int(parts[2])
            print(str(obj.enQueue(value)).lower())
        elif operation == "dequeue":
            print(str(obj.deQueue()).lower())
        elif operation == "front":
            print(obj.Front())
        elif operation == "rear":
            print(obj.Rear())
        elif operation == "isEmpty":
            print(str(obj.isEmpty()).lower())
        elif operation == "isFull":
            print(str(obj.isFull()).lower())

if __name__ == '__main__':
    main()

```

## JavaScript Solution
```javascript
class MyCircularQueue {
    /**
     * @param {number} k
     */
    constructor(k) {
        this.data = new Array(k);
        this.capacity = k;
        this.front = 0;
        this.rear = -1; // -1 indicates an empty queue, rear will become 0 upon first enqueue
        this.currentSize = 0;
    }

    /**
     * @param {number} value
     * @return {boolean}
     */
    enQueue(value) {
        if (this.isFull()) {
            return false;
        }
        this.rear = (this.rear + 1) % this.capacity;
        this.data[this.rear] = value;
        this.currentSize++;
        return true;
    }

    /**
     * @return {boolean}
     */
    deQueue() {
        if (this.isEmpty()) {
            return false;
        }
        this.front = (this.front + 1) % this.capacity;
        this.currentSize--;
        return true;
    }

    /**
     * @return {number}
     */
    Front() {
        if (this.isEmpty()) {
            return -1;
        }
        return this.data[this.front];
    }

    /**
     * @return {number}
     */
    Rear() {
        if (this.isEmpty()) {
            return -1;
        }
        return this.data[this.rear];
    }

    /**
     * @return {boolean}
     */
    isEmpty() {
        return this.currentSize === 0;
    }

    /**
     * @return {boolean}
     */
    isFull() {
        return this.currentSize === this.capacity;
    }
}

function processInput() {
    const readline = require('readline');
    const rl = readline.createInterface({
        input: process.stdin,
        output: process.stdout
    });

    let k = -1;
    let circularQueue = null;
    let lineCount = 0;

    rl.on('line', (line) => {
        if (line.trim() === '') return;

        if (lineCount === 0) {
            k = parseInt(line.trim());
            circularQueue = new MyCircularQueue(k);
        } else {
            const parts = line.trim().split(' ');
            const operation = parts[1];

            let result;
            switch (operation) {
                case 'enqueue':
                    const value = parseInt(parts[2]);
                    result = circularQueue.enQueue(value);
                    console.log(result ? 'true' : 'false');
                    break;
                case 'dequeue':
                    result = circularQueue.deQueue();
                    console.log(result ? 'true' : 'false');
                    break;
                case 'front':
                    result = circularQueue.Front();
                    console.log(result);
                    break;
                case 'rear':
                    result = circularQueue.Rear();
                    console.log(result);
                    break;
                case 'isEmpty':
                    result = circularQueue.isEmpty();
                    console.log(result ? 'true' : 'false');
                    break;
                case 'isFull':
                    result = circularQueue.isFull();
                    console.log(result ? 'true' : 'false');
                    break;
            }
        }
        lineCount++;
    });

    rl.on('close', () => {
        // All input processed
    });
}

processInput();

```
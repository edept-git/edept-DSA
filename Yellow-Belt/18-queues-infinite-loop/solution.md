# Solutions for Queue's Infinite Loop

### Approach
The `MyCircularQueue` can be efficiently implemented using a fixed-size array and two pointers: `front` and `rear`. The `front` pointer will track the index of the first element in the queue, and the `rear` pointer will track the index where the next element will be inserted. To manage the circular nature of the queue, the modulo operator (`%`) is crucial. When `front` or `rear` pointers need to advance beyond the array bounds, they "wrap around" to the beginning of the array using `(pointer + 1) % capacity`.

To distinguish between an empty and a full queue, a common approach is to maintain a `count` variable, which stores the current number of elements in the queue.
*   `enqueue(value)`: If the `count` is equal to the `capacity`, the queue is full, and the operation fails. Otherwise, `value` is inserted at `data[rear]`, `rear` is updated to `(rear + 1) % capacity`, and `count` is incremented.
*   `dequeue()`: If the `count` is 0, the queue is empty, and the operation fails. Otherwise, the element at `data[front]` is conceptually removed, `front` is updated to `(front + 1) % capacity`, and `count` is decremented.
*   `front()`: Returns `data[front]` if the queue is not empty; otherwise, returns `-1`.
*   `rear()`: Returns `data[(rear - 1 + capacity) % capacity]` if the queue is not empty; otherwise, returns `-1`. Note the `(rear - 1 + capacity) % capacity` to handle cases where `rear` is 0 and needs to wrap to the end of the array.
*   `isEmpty()`: Returns `true` if `count` is 0, `false` otherwise.
*   `isFull()`: Returns `true` if `count` is equal to `capacity`, `false` otherwise.

All operations—`enqueue`, `dequeue`, `front`, `rear`, `isEmpty`, and `isFull`—can be performed in constant time, O(1), as they involve only a few pointer manipulations and arithmetic operations. The space complexity is O(N) for storing the elements in the array, where N is the `capacity` of the queue.

## C Solution
```c
#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>
#include <string.h>

typedef struct {
    int *data;
    int front;
    int rear;
    int capacity;
    int count;
} MyCircularQueue;

MyCircularQueue* myCircularQueueCreate(int k) {
    MyCircularQueue* obj = (MyCircularQueue*) malloc(sizeof(MyCircularQueue));
    obj->data = (int*) malloc(sizeof(int) * k);
    obj->capacity = k;
    obj->front = 0;
    obj->rear = 0; // rear points to the next available slot
    obj->count = 0;
    return obj;
}

bool myCircularQueueIsEmpty(MyCircularQueue* obj) {
    return obj->count == 0;
}

bool myCircularQueueIsFull(MyCircularQueue* obj) {
    return obj->count == obj->capacity;
}

bool myCircularQueueEnQueue(MyCircularQueue* obj, int value) {
    if (myCircularQueueIsFull(obj)) {
        return false;
    }
    obj->data[obj->rear] = value;
    obj->rear = (obj->rear + 1) % obj->capacity;
    obj->count++;
    return true;
}

bool myCircularQueueDeQueue(MyCircularQueue* obj) {
    if (myCircularQueueIsEmpty(obj)) {
        return false;
    }
    obj->front = (obj->front + 1) % obj->capacity;
    obj->count--;
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
    // (obj->rear - 1 + obj->capacity) % obj->capacity handles when rear is 0
    return obj->data[(obj->rear - 1 + obj->capacity) % obj->capacity];
}

void myCircularQueueFree(MyCircularQueue* obj) {
    free(obj->data);
    free(obj);
}

int main() {
    char command[20];
    int k, value;
    MyCircularQueue* obj = NULL;

    while (scanf("%s", command) != EOF) {
        if (strcmp(command, "MyCircularQueue") == 0) {
            scanf("%d", &k);
            if (obj != NULL) {
                myCircularQueueFree(obj); // Free previous object if any
            }
            obj = myCircularQueueCreate(k);
            printf("null\n");
        } else if (obj == NULL) {
            // Should not happen based on problem constraints (MyCircularQueue will be called first)
            continue;
        } else if (strcmp(command, "enqueue") == 0) {
            scanf("%d", &value);
            printf("%s\n", myCircularQueueEnQueue(obj, value) ? "true" : "false");
        } else if (strcmp(command, "dequeue") == 0) {
            printf("%s\n", myCircularQueueDeQueue(obj) ? "true" : "false");
        } else if (strcmp(command, "front") == 0) {
            printf("%d\n", myCircularQueueFront(obj));
        } else if (strcmp(command, "rear") == 0) {
            printf("%d\n", myCircularQueueRear(obj));
        } else if (strcmp(command, "isEmpty") == 0) {
            printf("%s\n", myCircularQueueIsEmpty(obj) ? "true" : "false");
        } else if (strcmp(command, "isFull") == 0) {
            printf("%s\n", myCircularQueueIsFull(obj) ? "true" : "false");
        } else if (strcmp(command, "exit") == 0) {
            break;
        }
    }

    if (obj != NULL) {
        myCircularQueueFree(obj);
    }

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
    int rear; // rear points to the next available slot
    int capacity;
    int count;

public:
    MyCircularQueue(int k) {
        capacity = k;
        data.resize(k);
        front = 0;
        rear = 0;
        count = 0;
    }

    bool enQueue(int value) {
        if (isFull()) {
            return false;
        }
        data[rear] = value;
        rear = (rear + 1) % capacity;
        count++;
        return true;
    }

    bool deQueue() {
        if (isEmpty()) {
            return false;
        }
        front = (front + 1) % capacity;
        count--;
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
        // (rear - 1 + capacity) % capacity handles when rear is 0
        return data[(rear - 1 + capacity) % capacity];
    }

    bool isEmpty() {
        return count == 0;
    }

    bool isFull() {
        return count == capacity;
    }
};

int main() {
    std::string command;
    int k, value;
    MyCircularQueue* obj = nullptr;

    while (std::cin >> command) {
        if (command == "MyCircularQueue") {
            std::cin >> k;
            if (obj != nullptr) {
                delete obj; // Free previous object if any
            }
            obj = new MyCircularQueue(k);
            std::cout << "null\n";
        } else if (obj == nullptr) {
            continue; // Should not happen based on problem constraints
        } else if (command == "enqueue") {
            std::cin >> value;
            std::cout << (obj->enQueue(value) ? "true" : "false") << "\n";
        } else if (command == "dequeue") {
            std::cout << (obj->deQueue() ? "true" : "false") << "\n";
        } else if (command == "front") {
            std::cout << obj->Front() << "\n";
        } else if (command == "rear") {
            std::cout << obj->Rear() << "\n";
        } else if (command == "isEmpty") {
            std::cout << (obj->isEmpty() ? "true" : "false") << "\n";
        } else if (command == "isFull") {
            std::cout << (obj->isFull() ? "true" : "false") << "\n";
        } else if (command == "exit") {
            break;
        }
    }

    if (obj != nullptr) {
        delete obj;
    }

    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

class MyCircularQueue {
    private int[] data;
    private int front;
    private int rear; // rear points to the next available slot
    private int capacity;
    private int count;

    public MyCircularQueue(int k) {
        capacity = k;
        data = new int[k];
        front = 0;
        rear = 0;
        count = 0;
    }

    public boolean enQueue(int value) {
        if (isFull()) {
            return false;
        }
        data[rear] = value;
        rear = (rear + 1) % capacity;
        count++;
        return true;
    }

    public boolean deQueue() {
        if (isEmpty()) {
            return false;
        }
        front = (front + 1) % capacity;
        count--;
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
        // (rear - 1 + capacity) % capacity handles when rear is 0
        return data[(rear - 1 + capacity) % capacity];
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
        String command;
        int k, value;
        MyCircularQueue obj = null;

        while (scanner.hasNext()) {
            command = scanner.next();
            if (command.equals("MyCircularQueue")) {
                k = scanner.nextInt();
                obj = new MyCircularQueue(k);
                System.out.println("null");
            } else if (obj == null) {
                // Should not happen based on problem constraints
                continue;
            } else if (command.equals("enqueue")) {
                value = scanner.nextInt();
                System.out.println(obj.enQueue(value) ? "true" : "false");
            } else if (command.equals("dequeue")) {
                System.out.println(obj.deQueue() ? "true" : "false");
            } else if (command.equals("front")) {
                System.out.println(obj.Front());
            } else if (command.equals("rear")) {
                System.out.println(obj.Rear());
            } else if (command.equals("isEmpty")) {
                System.out.println(obj.isEmpty() ? "true" : "false");
            } else if (command.equals("isFull")) {
                System.out.println(obj.isFull() ? "true" : "false");
            } else if (command.equals("exit")) {
                break;
            }
        }
        scanner.close();
    }
}
```

## Python Solution
```python
class MyCircularQueue:
    def __init__(self, k: int):
        self.capacity = k
        self.data = [0] * k
        self.front = 0
        self.rear = 0 # rear points to the next available slot
        self.count = 0

    def enQueue(self, value: int) -> bool:
        if self.isFull():
            return False
        self.data[self.rear] = value
        self.rear = (self.rear + 1) % self.capacity
        self.count += 1
        return True

    def deQueue(self) -> bool:
        if self.isEmpty():
            return False
        self.front = (self.front + 1) % self.capacity
        self.count -= 1
        return True

    def Front(self) -> int:
        if self.isEmpty():
            return -1
        return self.data[self.front]

    def Rear(self) -> int:
        if self.isEmpty():
            return -1
        # (self.rear - 1 + self.capacity) % self.capacity handles when rear is 0
        return self.data[(self.rear - 1 + self.capacity) % self.capacity]

    def isEmpty(self) -> bool:
        return self.count == 0

    def isFull(self) -> bool:
        return self.count == self.capacity

def main():
    obj = None
    while True:
        try:
            line = input().split()
            command = line[0]

            if command == "MyCircularQueue":
                k = int(line[1])
                obj = MyCircularQueue(k)
                print("null")
            elif obj is None:
                # Should not happen based on problem constraints
                continue
            elif command == "enqueue":
                value = int(line[1])
                print("true" if obj.enQueue(value) else "false")
            elif command == "dequeue":
                print("true" if obj.deQueue() else "false")
            elif command == "front":
                print(obj.Front())
            elif command == "rear":
                print(obj.Rear())
            elif command == "isEmpty":
                print("true" if obj.isEmpty() else "false")
            elif command == "isFull":
                print("true" if obj.isFull() else "false")
            elif command == "exit":
                break
        except EOFError:
            break

if __name__ == "__main__":
    main()
```

## JavaScript Solution
```javascript
class MyCircularQueue {
    /**
     * @param {number} k
     */
    constructor(k) {
        this.capacity = k;
        this.data = new Array(k);
        this.front = 0;
        this.rear = 0; // rear points to the next available slot
        this.count = 0;
    }

    /**
     * @param {number} value
     * @return {boolean}
     */
    enQueue(value) {
        if (this.isFull()) {
            return false;
        }
        this.data[this.rear] = value;
        this.rear = (this.rear + 1) % this.capacity;
        this.count++;
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
        this.count--;
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
        // (this.rear - 1 + this.capacity) % this.capacity handles when rear is 0
        return this.data[(this.rear - 1 + this.capacity) % this.capacity];
    }

    /**
     * @return {boolean}
     */
    isEmpty() {
        return this.count === 0;
    }

    /**
     * @return {boolean}
     */
    isFull() {
        return this.count === this.capacity;
    }
}

// Main function for I/O handling
function main() {
    let obj = null;
    const readline = require('readline');
    const rl = readline.createInterface({
        input: process.stdin,
        output: process.stdout
    });

    rl.on('line', (line) => {
        const parts = line.split(' ');
        const command = parts[0];

        if (command === "MyCircularQueue") {
            const k = parseInt(parts[1]);
            obj = new MyCircularQueue(k);
            console.log("null");
        } else if (obj === null) {
            // Should not happen based on problem constraints
            return;
        } else if (command === "enqueue") {
            const value = parseInt(parts[1]);
            console.log(obj.enQueue(value) ? "true" : "false");
        } else if (command === "dequeue") {
            console.log(obj.deQueue() ? "true" : "false");
        } else if (command === "front") {
            console.log(obj.Front());
        } else if (command === "rear") {
            console.log(obj.Rear());
        } else if (command === "isEmpty") {
            console.log(obj.isEmpty() ? "true" : "false");
        } else if (command === "isFull") {
            console.log(obj.isFull() ? "true" : "false");
        } else if (command === "exit") {
            rl.close();
        }
    });
}

main();
```
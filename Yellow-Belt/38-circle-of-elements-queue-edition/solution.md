# Solutions for Circle of Elements: Queue Edition

### Approach
The core idea behind implementing a circular queue is to use a fixed-size array and two pointers, `front` and `rear`, to keep track of the first and last elements, respectively. We also need to maintain the current `size` of the queue and its `capacity`. When `enqueue` is called, we increment `rear` (using modulo `capacity` to wrap around the array) and place the new element there, incrementing `size`. If `rear` was initially -1 (queue was empty), `front` should also be set to 0. When `dequeue` is called, we increment `front` (again, using modulo `capacity`), effectively removing the element from the front, and decrementing `size`. If the queue becomes empty after a `dequeue` operation, both `front` and `rear` should be reset to -1. The `Front()` and `Rear()` methods return the elements at their respective pointers, or -1 if the queue is empty. `isEmpty()` checks if `size` is 0, and `isFull()` checks if `size` equals `capacity`. All operations involve simple pointer arithmetic and array access, resulting in a time complexity of O(1). The space complexity is O(k) for storing the elements in the array, where `k` is the capacity of the queue.

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
    int size;
    int capacity;
} MyCircularQueue;

MyCircularQueue* myCircularQueueCreate(int k) {
    MyCircularQueue* obj = (MyCircularQueue*)malloc(sizeof(MyCircularQueue));
    obj->data = (int*)malloc(sizeof(int) * k);
    obj->front = -1;
    obj->rear = -1;
    obj->size = 0;
    obj->capacity = k;
    return obj;
}

bool myCircularQueueIsEmpty(MyCircularQueue* obj) {
    return obj->size == 0;
}

bool myCircularQueueIsFull(MyCircularQueue* obj) {
    return obj->size == obj->capacity;
}

bool myCircularQueueEnQueue(MyCircularQueue* obj, int value) {
    if (myCircularQueueIsFull(obj)) {
        return false;
    }
    obj->rear = (obj->rear + 1) % obj->capacity;
    obj->data[obj->rear] = value;
    if (obj->front == -1) { // First element being added
        obj->front = 0;
    }
    obj->size++;
    return true;
}

bool myCircularQueueDeQueue(MyCircularQueue* obj) {
    if (myCircularQueueIsEmpty(obj)) {
        return false;
    }
    obj->front = (obj->front + 1) % obj->capacity;
    obj->size--;
    if (obj->size == 0) { // Queue became empty, reset pointers
        obj->front = -1;
        obj->rear = -1;
    }
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
    int k, n;
    scanf("%d", &k);
    scanf("%d", &n);

    MyCircularQueue* obj = myCircularQueueCreate(k);
    char command[20];
    int value;

    for (int i = 0; i < n; i++) {
        scanf("%s", command);
        if (strcmp(command, "enqueue") == 0) {
            scanf("%d", &value);
            printf("%s\n", myCircularQueueEnQueue(obj, value) ? "true" : "false");
        } else if (strcmp(command, "dequeue") == 0) {
            printf("%s\n", myCircularQueueDeQueue(obj) ? "true" : "false");
        } else if (strcmp(command, "Front") == 0) {
            printf("%d\n", myCircularQueueFront(obj));
        } else if (strcmp(command, "Rear") == 0) {
            printf("%d\n", myCircularQueueRear(obj));
        } else if (strcmp(command, "isEmpty") == 0) {
            printf("%s\n", myCircularQueueIsEmpty(obj) ? "true" : "false");
        } else if (strcmp(command, "isFull") == 0) {
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
    int size;
    int capacity;

public:
    MyCircularQueue(int k) {
        capacity = k;
        data.resize(k);
        front = -1;
        rear = -1;
        size = 0;
    }

    bool enQueue(int value) {
        if (isFull()) {
            return false;
        }
        rear = (rear + 1) % capacity;
        data[rear] = value;
        if (front == -1) { // First element being added
            front = 0;
        }
        size++;
        return true;
    }

    bool deQueue() {
        if (isEmpty()) {
            return false;
        }
        front = (front + 1) % capacity;
        size--;
        if (size == 0) { // Queue became empty, reset pointers
            front = -1;
            rear = -1;
        }
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
        return size == 0;
    }

    bool isFull() {
        return size == capacity;
    }
};

int main() {
    int k, n;
    std::cin >> k;
    std::cin >> n;

    MyCircularQueue* obj = new MyCircularQueue(k);
    std::string command;
    int value;

    for (int i = 0; i < n; ++i) {
        std::cin >> command;
        if (command == "enqueue") {
            std::cin >> value;
            std::cout << (obj->enQueue(value) ? "true" : "false") << std::endl;
        } else if (command == "dequeue") {
            std::cout << (obj->deQueue() ? "true" : "false") << std::endl;
        } else if (command == "Front") {
            std::cout << obj->Front() << std::endl;
        } else if (command == "Rear") {
            std::cout << obj->Rear() << std::endl;
        } else if (command == "isEmpty") {
            std::cout << (obj->isEmpty() ? "true" : "false") << std::endl;
        } else if (command == "isFull") {
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
    private int size;
    private int capacity;

    public MyCircularQueue(int k) {
        capacity = k;
        data = new int[k];
        front = -1;
        rear = -1;
        size = 0;
    }

    public boolean enQueue(int value) {
        if (isFull()) {
            return false;
        }
        rear = (rear + 1) % capacity;
        data[rear] = value;
        if (front == -1) { // First element being added
            front = 0;
        }
        size++;
        return true;
    }

    public boolean deQueue() {
        if (isEmpty()) {
            return false;
        }
        front = (front + 1) % capacity;
        size--;
        if (size == 0) { // Queue became empty, reset pointers
            front = -1;
            rear = -1;
        }
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
        return size == 0;
    }

    public boolean isFull() {
        return size == capacity;
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int k = scanner.nextInt();
        int n = scanner.nextInt();

        MyCircularQueue obj = new MyCircularQueue(k);
        
        for (int i = 0; i < n; i++) {
            String command = scanner.next();
            if (command.equals("enqueue")) {
                int value = scanner.nextInt();
                System.out.println(obj.enQueue(value));
            } else if (command.equals("dequeue")) {
                System.out.println(obj.deQueue());
            } else if (command.equals("Front")) {
                System.out.println(obj.Front());
            } else if (command.equals("Rear")) {
                System.out.println(obj.Rear());
            } else if (command.equals("isEmpty")) {
                System.out.println(obj.isEmpty());
            } else if (command.equals("isFull")) {
                System.out.println(obj.isFull());
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
        self.data = [0] * k
        self.front = -1
        self.rear = -1
        self.size = 0
        self.capacity = k

    def enQueue(self, value: int) -> bool:
        if self.isFull():
            return False
        self.rear = (self.rear + 1) % self.capacity
        self.data[self.rear] = value
        if self.front == -1: # First element being added
            self.front = 0
        self.size += 1
        return True

    def deQueue(self) -> bool:
        if self.isEmpty():
            return False
        self.front = (self.front + 1) % self.capacity
        self.size -= 1
        if self.size == 0: # Queue became empty, reset pointers
            self.front = -1
            self.rear = -1
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
        return self.size == 0

    def isFull(self) -> bool:
        return self.size == self.capacity

if __name__ == "__main__":
    k = int(input())
    n = int(input())

    obj = MyCircularQueue(k)

    for _ in range(n):
        command_line = input().split()
        command = command_line[0]
        
        if command == "enqueue":
            value = int(command_line[1])
            print(obj.enQueue(value))
        elif command == "dequeue":
            print(obj.deQueue())
        elif command == "Front":
            print(obj.Front())
        elif command == "Rear":
            print(obj.Rear())
        elif command == "isEmpty":
            print(obj.isEmpty())
        elif command == "isFull":
            print(obj.isFull())

```

## JavaScript Solution
```javascript
const readline = require('readline');

class MyCircularQueue {
    constructor(k) {
        this.data = new Array(k);
        this.front = -1;
        this.rear = -1;
        this.size = 0;
        this.capacity = k;
    }

    enQueue(value) {
        if (this.isFull()) {
            return false;
        }
        this.rear = (this.rear + 1) % this.capacity;
        this.data[this.rear] = value;
        if (this.front === -1) { // First element being added
            this.front = 0;
        }
        this.size++;
        return true;
    }

    deQueue() {
        if (this.isEmpty()) {
            return false;
        }
        this.front = (this.front + 1) % this.capacity;
        this.size--;
        if (this.size === 0) { // Queue became empty, reset pointers
            this.front = -1;
            this.rear = -1;
        }
        return true;
    }

    Front() {
        if (this.isEmpty()) {
            return -1;
        }
        return this.data[this.front];
    }

    Rear() {
        if (this.isEmpty()) {
            return -1;
        }
        return this.data[this.rear];
    }

    isEmpty() {
        return this.size === 0;
    }

    isFull() {
        return this.size === this.capacity;
    }
}

const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});

let lines = [];
rl.on('line', (line) => {
    lines.push(line);
});

rl.on('close', () => {
    const k = parseInt(lines[0]);
    const n = parseInt(lines[1]);
    let lineIndex = 2;

    const obj = new MyCircularQueue(k);

    for (let i = 0; i < n; i++) {
        const commandLine = lines[lineIndex++].split(' ');
        const command = commandLine[0];
        
        if (command === "enqueue") {
            const value = parseInt(commandLine[1]);
            console.log(obj.enQueue(value));
        } else if (command === "dequeue") {
            console.log(obj.deQueue());
        } else if (command === "Front") {
            console.log(obj.Front());
        } else if (command === "Rear") {
            console.log(obj.Rear());
        } else if (command === "isEmpty") {
            console.log(obj.isEmpty());
        } else if (command === "isFull") {
            console.log(obj.isFull());
        }
    }
});

```
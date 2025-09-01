# Solutions for StackMaster: The Command Console

### Approach
This problem requires implementing a stack using a fixed-size array and managing its operations. The core idea is to use an array to store elements and an integer variable, often called `top` or `peek_index`, to keep track of the index of the topmost element. Initially, `top` is set to -1, indicating an empty stack. 

For the `push(value)` operation, we first check if the stack is full (i.e., `top` has reached the maximum allowed index). If not full, we increment `top` and place the `value` at `stack[top]`. If full, we can indicate an error or simply ignore the push. For this problem, `push` on a full stack does not produce output.

For the `pop()` operation, we first check if the stack is empty (i.e., `top == -1`). If empty, we return `-1`. Otherwise, we retrieve `stack[top]`, then decrement `top`, and return the retrieved value.

For the `top()` (or `peek()`) operation, similar to `pop`, we first check if the stack is empty. If empty, we return `-1`. Otherwise, we simply return `stack[top]` without modifying `top`.

For the `isEmpty()` operation, we simply check if `top == -1`. If it is, the stack is empty and we return `true`; otherwise, we return `false`.

Data Structures: A fixed-size array (e.g., `int[]` in Java, `std::vector` in C++ for dynamic size, or just a raw array in C) and an integer `top` index. 

Time Complexity: All operations (`push`, `pop`, `top`, `isEmpty`) take O(1) time complexity because they involve direct array access and simple arithmetic operations, regardless of the number of elements in the stack.

Space Complexity: The space complexity is O(N), where N is the maximum capacity of the stack, as we need to allocate an array of that size to store the elements.

## C Solution
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_SIZE 1000

typedef struct {
    int arr[MAX_SIZE];
    int top;
} Stack;

// Function to initialize the stack
void initStack(Stack* s) {
    s->top = -1; // -1 indicates an empty stack
}

// Function to check if the stack is empty
int isEmpty(Stack* s) {
    return s->top == -1;
}

// Function to check if the stack is full
int isFull(Stack* s) {
    return s->top == MAX_SIZE - 1;
}

// Function to push an element onto the stack
void push(Stack* s, int value) {
    if (isFull(s)) {
        // Stack overflow
        return;
    }
    s->arr[++(s->top)] = value;
}

// Function to pop an element from the stack
int pop(Stack* s) {
    if (isEmpty(s)) {
        // Stack underflow
        return -1;
    }
    return s->arr[(s->top)--];
}

// Function to get the top element of the stack without removing it
int peek(Stack* s) {
    if (isEmpty(s)) {
        // Stack underflow
        return -1;
    }
    return s->arr[s->top];
}

int main() {
    int N;
    scanf("%d", &N);

    Stack myStack;
    initStack(&myStack);

    char command[10];
    int value;

    for (int i = 0; i < N; ++i) {
        scanf("%s", command);
        if (strcmp(command, "push") == 0) {
            scanf("%d", &value);
            push(&myStack, value);
        } else if (strcmp(command, "pop") == 0) {
            printf("%d\n", pop(&myStack));
        } else if (strcmp(command, "top") == 0) {
            printf("%d\n", peek(&myStack));
        } else if (strcmp(command, "isEmpty") == 0) {
            printf("%s\n", isEmpty(&myStack) ? "true" : "false");
        }
    }

    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <string>
#include <vector>

const int MAX_SIZE = 1000;

class Stack {
private:
    int arr[MAX_SIZE];
    int top_idx;

public:
    Stack() {
        top_idx = -1;
    }

    bool isEmpty() {
        return top_idx == -1;
    }

    bool isFull() {
        return top_idx == MAX_SIZE - 1;
    }

    void push(int value) {
        if (isFull()) {
            // Stack overflow
            return;
        }
        arr[++top_idx] = value;
    }

    int pop() {
        if (isEmpty()) {
            // Stack underflow
            return -1;
        }
        return arr[top_idx--];
    }

    int peek() {
        if (isEmpty()) {
            // Stack underflow
            return -1;
        }
        return arr[top_idx];
    }
};

int main() {
    std::ios_base::sync_with_stdio(false);
    std::cin.tie(NULL);

    int N;
    std::cin >> N;

    Stack myStack;

    std::string command;
    int value;

    for (int i = 0; i < N; ++i) {
        std::cin >> command;
        if (command == "push") {
            std::cin >> value;
            myStack.push(value);
        } else if (command == "pop") {
            std::cout << myStack.pop() << "\n";
        } else if (command == "top") {
            std::cout << myStack.peek() << "\n";
        } else if (command == "isEmpty") {
            std::cout << (myStack.isEmpty() ? "true" : "false") << "\n";
        }
    }

    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

class Stack {
    private static final int MAX_SIZE = 1000;
    private int[] arr;
    private int top;

    public Stack() {
        arr = new int[MAX_SIZE];
        top = -1; // -1 indicates an empty stack
    }

    public boolean isEmpty() {
        return top == -1;
    }

    public boolean isFull() {
        return top == MAX_SIZE - 1;
    }

    public void push(int value) {
        if (isFull()) {
            // Stack overflow, handle as per problem (e.g., ignore, throw exception)
            return;
        }
        arr[++top] = value;
    }

    public int pop() {
        if (isEmpty()) {
            // Stack underflow
            return -1;
        }
        return arr[top--];
    }

    public int peek() {
        if (isEmpty()) {
            // Stack underflow
            return -1;
        }
        return arr[top];
    }
}

public class Solution {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int N = scanner.nextInt();
        scanner.nextLine(); // Consume the newline character

        Stack myStack = new Stack();

        for (int i = 0; i < N; ++i) {
            String line = scanner.nextLine();
            String[] parts = line.split(" ");
            String command = parts[0];

            if (command.equals("push")) {
                int value = Integer.parseInt(parts[1]);
                myStack.push(value);
            } else if (command.equals("pop")) {
                System.out.println(myStack.pop());
            } else if (command.equals("top")) {
                System.out.println(myStack.peek());
            } else if (command.equals("isEmpty")) {
                System.out.println(myStack.isEmpty() ? "true" : "false");
            }
        }

        scanner.close();
    }
}
```

## Python Solution
```python
class Stack:
    MAX_SIZE = 1000

    def __init__(self):
        self.arr = [0] * Stack.MAX_SIZE  # Initialize with a fixed size
        self.top = -1  # -1 indicates an empty stack

    def is_empty(self):
        return self.top == -1

    def is_full(self):
        return self.top == Stack.MAX_SIZE - 1

    def push(self, value):
        if self.is_full():
            # Stack overflow
            return
        self.top += 1
        self.arr[self.top] = value

    def pop(self):
        if self.is_empty():
            # Stack underflow
            return -1
        value = self.arr[self.top]
        self.top -= 1
        return value

    def peek(self):
        if self.is_empty():
            # Stack underflow
            return -1
        return self.arr[self.top]

def main():
    N = int(input())

    my_stack = Stack()

    for _ in range(N):
        line = input().split()
        command = line[0]

        if command == "push":
            value = int(line[1])
            my_stack.push(value)
        elif command == "pop":
            print(my_stack.pop())
        elif command == "top":
            print(my_stack.peek())
        elif command == "isEmpty":
            print("true" if my_stack.is_empty() else "false")

if __name__ == "__main__":
    main()
```

## JavaScript Solution
```javascript
const MAX_SIZE = 1000;

class Stack {
    constructor() {
        this.arr = new Array(MAX_SIZE);
        this.top = -1; // -1 indicates an empty stack
    }

    isEmpty() {
        return this.top === -1;
    }

    isFull() {
        return this.top === MAX_SIZE - 1;
    }

    push(value) {
        if (this.isFull()) {
            // Stack overflow
            return;
        }
        this.top++;
        this.arr[this.top] = value;
    }

    pop() {
        if (this.isEmpty()) {
            // Stack underflow
            return -1;
        }
        const value = this.arr[this.top];
        this.top--;
        return value;
    }

    peek() {
        if (this.isEmpty()) {
            // Stack underflow
            return -1;
        }
        return this.arr[this.top];
    }
}

function main() {
    const readline = require('readline');
    const rl = readline.createInterface({
        input: process.stdin,
        output: process.stdout
    });

    let N;
    let lineNumber = 0;
    const lines = [];

    rl.on('line', (line) => {
        lines.push(line);
        if (lineNumber === 0) {
            N = parseInt(line);
        } else if (lineNumber === N) {
            rl.close();
        }
        lineNumber++;
    });

    rl.on('close', () => {
        const myStack = new Stack();

        for (let i = 1; i <= N; ++i) {
            const parts = lines[i].split(' ');
            const command = parts[0];

            if (command === "push") {
                const value = parseInt(parts[1]);
                myStack.push(value);
            } else if (command === "pop") {
                console.log(myStack.pop());
            } else if (command === "top") {
                console.log(myStack.peek());
            } else if (command === "isEmpty") {
                console.log(myStack.isEmpty() ? "true" : "false");
            }
        }
    });
}

main();
```
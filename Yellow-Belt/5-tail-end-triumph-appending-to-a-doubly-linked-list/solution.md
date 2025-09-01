# Solutions for Tail-End Triumph: Appending to a Doubly Linked List

### Approach
The problem requires appending a new node to the end of a Doubly Linked List. The core idea is to create a new `Node` with the given value and then correctly link it with the existing tail of the list. If the list is empty, the new node becomes both the head and the tail.

Here's the algorithm:
1.  **Create a new node**: Instantiate a new `Node` object (or allocate memory for a `struct Node`) and set its `data` to the given value. Initialize its `prev` and `next` pointers to `null` (or `nullptr`).
2.  **Handle an empty list**: If the `head` of the list is `null` (meaning the list is empty), then the new node becomes both the `head` and the `tail` of the list. No other pointers need to be adjusted for the new node.
3.  **Handle a non-empty list**: If the list is not empty, the new node needs to be linked after the current `tail`.
    a.  Set the `next` pointer of the current `tail` to point to the new node.
    b.  Set the `prev` pointer of the new node to point to the current `tail`.
    c.  Update the `tail` of the list to be the new node.
    d.  The `next` pointer of the new node should remain `null` (as it's the new end).

**Data Structures**: A Doubly Linked List, where each node contains an integer `data` and two pointers: `next` (to the subsequent node) and `prev` (to the preceding node).

**Time Complexity**: O(1). We perform a constant number of operations to create a new node and adjust a few pointers. We don't need to traverse the list to find the tail, as we maintain a direct reference to it.

**Space Complexity**: O(1). We only allocate memory for a single new node, regardless of the list's size. This doesn't include the space taken by the input list itself.

## C Solution
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// Definition for a Doubly Linked List Node
struct Node {
    int data;
    struct Node* prev;
    struct Node* next;
};

// Function to create a new node
struct Node* createNode(int data) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    if (newNode == NULL) {
        perror("Failed to allocate memory for a new node");
        exit(EXIT_FAILURE);
    }
    newNode->data = data;
    newNode->prev = NULL;
    newNode->next = NULL;
    return newNode;
}

// Function to insert a node at the tail of a Doubly Linked List
void insertAtTail(struct Node** head_ref, struct Node** tail_ref, int data) {
    struct Node* newNode = createNode(data);

    if (*head_ref == NULL) {
        // List is empty, new node becomes both head and tail
        *head_ref = newNode;
        *tail_ref = newNode;
    } else {
        // List is not empty, append to the tail
        (*tail_ref)->next = newNode;
        newNode->prev = *tail_ref;
        *tail_ref = newNode; // Update tail to the new node
    }
}

// Function to print the Doubly Linked List
void printList(struct Node* head) {
    if (head == NULL) {
        printf("Empty List\n");
        return;
    }
    struct Node* current = head;
    while (current != NULL) {
        printf("%d", current->data);
        if (current->next != NULL) {
            printf(" <-> ");
        }
        current = current->next;
    }
    printf("\n");
}

// Function to free the Doubly Linked List
void freeList(struct Node* head) {
    struct Node* current = head;
    while (current != NULL) {
        struct Node* next = current->next;
        free(current);
        current = next;
    }
}

int main() {
    struct Node* head = NULL;
    struct Node* tail = NULL;
    char line[1000];
    int data_to_insert;

    // Read initial list elements
    if (fgets(line, sizeof(line), stdin) == NULL) {
        return 1;
    }
    line[strcspn(line, "\n")] = 0; // Remove newline character

    if (strcmp(line, "EMPTY") != 0) {
        char* token = strtok(line, " ");
        while (token != NULL) {
            insertAtTail(&head, &tail, atoi(token));
            token = strtok(NULL, " ");
        }
    }

    // Read value to insert
    if (scanf("%d", &data_to_insert) != 1) {
        freeList(head);
        return 1;
    }

    // Call the core logic function
    insertAtTail(&head, &tail, data_to_insert);

    // Print the modified list
    printList(head);

    // Free allocated memory
    freeList(head);

    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <string>
#include <sstream>
#include <vector>

// Definition for a Doubly Linked List Node
struct Node {
    int data;
    Node* prev;
    Node* next;

    Node(int val) : data(val), prev(nullptr), next(nullptr) {}
};

// Function to insert a node at the tail of a Doubly Linked List
void insertAtTail(Node*& head, Node*& tail, int data) {
    Node* newNode = new Node(data);

    if (head == nullptr) {
        // List is empty, new node becomes both head and tail
        head = newNode;
        tail = newNode;
    } else {
        // List is not empty, append to the tail
        tail->next = newNode;
        newNode->prev = tail;
        tail = newNode; // Update tail to the new node
    }
}

// Function to print the Doubly Linked List
void printList(Node* head) {
    if (head == nullptr) {
        std::cout << "Empty List" << std::endl;
        return;
    }
    Node* current = head;
    while (current != nullptr) {
        std::cout << current->data;
        if (current->next != nullptr) {
            std::cout << " <-> ";
        }
        current = current->next;
    }
    std::cout << std::endl;
}

// Function to free the Doubly Linked List memory
void freeList(Node* head) {
    Node* current = head;
    while (current != nullptr) {
        Node* next = current->next;
        delete current;
        current = next;
    }
}

int main() {
    Node* head = nullptr;
    Node* tail = nullptr;
    std::string line;
    int dataToInsert;

    // Read initial list elements
    std::getline(std::cin, line);

    if (line != "EMPTY") {
        std::stringstream ss(line);
        int val;
        while (ss >> val) {
            insertAtTail(head, tail, val);
        }
    }

    // Read value to insert
    std::cin >> dataToInsert;

    // Call the core logic function
    insertAtTail(head, tail, dataToInsert);

    // Print the modified list
    printList(head);

    // Free allocated memory
    freeList(head);

    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;
import java.util.Arrays;

class Node {
    int data;
    Node prev;
    Node next;

    public Node(int data) {
        this.data = data;
        this.prev = null;
        this.next = null;
    }
}

class DoublyLinkedList {
    Node head;
    Node tail;

    public DoublyLinkedList() {
        this.head = null;
        this.tail = null;
    }

    // Core logic: Insert a node at the tail of the Doubly Linked List
    public void insertAtTail(int data) {
        Node newNode = new Node(data);

        if (this.head == null) {
            // List is empty, new node becomes both head and tail
            this.head = newNode;
            this.tail = newNode;
        } else {
            // List is not empty, append to the tail
            this.tail.next = newNode;
            newNode.prev = this.tail;
            this.tail = newNode; // Update tail to the new node
        }
    }

    // Function to print the Doubly Linked List
    public void printList() {
        if (this.head == null) {
            System.out.println("Empty List");
            return;
        }
        Node current = this.head;
        while (current != null) {
            System.out.print(current.data);
            if (current.next != null) {
                System.out.print(" <-> ");
            }
            current = current.next;
        }
        System.out.println();
    }
}

public class Solution {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        DoublyLinkedList dll = new DoublyLinkedList();

        // Read initial list elements
        String line = scanner.nextLine();
        if (!line.equals("EMPTY")) {
            Arrays.stream(line.split(" "))
                  .mapToInt(Integer::parseInt)
                  .forEach(dll::insertAtTail);
        }

        // Read value to insert
        int dataToInsert = scanner.nextInt();

        // Call the core logic method
        dll.insertAtTail(dataToInsert);

        // Print the modified list
        dll.printList();

        scanner.close();
    }
}
```

## Python Solution
```python
import sys

class Node:
    def __init__(self, data):
        self.data = data
        self.prev = None
        self.next = None

class DoublyLinkedList:
    def __init__(self):
        self.head = None
        self.tail = None

    # Core logic: Insert a node at the tail of the Doubly Linked List
    def insert_at_tail(self, data):
        new_node = Node(data)

        if self.head is None:
            # List is empty, new node becomes both head and tail
            self.head = new_node
            self.tail = new_node
        else:
            # List is not empty, append to the tail
            self.tail.next = new_node
            new_node.prev = self.tail
            self.tail = new_node  # Update tail to the new node

    # Function to print the Doubly Linked List
    def print_list(self):
        if self.head is None:
            sys.stdout.write("Empty List\n")
            return
        current = self.head
        elements = []
        while current is not None:
            elements.append(str(current.data))
            current = current.next
        sys.stdout.write(" <-> ".join(elements) + "\n")

def main():
    dll = DoublyLinkedList()

    # Read initial list elements
    line = sys.stdin.readline().strip()
    if line != "EMPTY":
        elements = list(map(int, line.split()))
        for val in elements:
            dll.insert_at_tail(val)

    # Read value to insert
    data_to_insert = int(sys.stdin.readline().strip())

    # Call the core logic method
    dll.insert_at_tail(data_to_insert)

    # Print the modified list
    dll.print_list()

if __name__ == '__main__':
    main()
```

## JavaScript Solution
```javascript
class Node {
    constructor(data) {
        this.data = data;
        this.prev = null;
        this.next = null;
    }
}

class DoublyLinkedList {
    constructor() {
        this.head = null;
        this.tail = null;
    }

    // Core logic: Insert a node at the tail of the Doubly Linked List
    insertAtTail(data) {
        const newNode = new Node(data);

        if (this.head === null) {
            // List is empty, new node becomes both head and tail
            this.head = newNode;
            this.tail = newNode;
        } else {
            // List is not empty, append to the tail
            this.tail.next = newNode;
            newNode.prev = this.tail;
            this.tail = newNode; // Update tail to the new node
        }
    }

    // Function to print the Doubly Linked List
    printList() {
        if (this.head === null) {
            process.stdout.write("Empty List\n");
            return;
        }
        let current = this.head;
        const elements = [];
        while (current !== null) {
            elements.push(current.data);
            current = current.next;
        }
        process.stdout.write(elements.join(" <-> ") + "\n");
    }
}

function main() {
    const readline = require('readline');
    const rl = readline.createInterface({
        input: process.stdin,
        output: process.stdout
    });

    const dll = new DoublyLinkedList();
    let lines = [];

    rl.on('line', (line) => {
        lines.push(line);
    }).on('close', () => {
        // Read initial list elements
        const initialListLine = lines[0];
        if (initialListLine !== "EMPTY") {
            initialListLine.split(' ').map(Number).forEach(val => dll.insertAtTail(val));
        }

        // Read value to insert
        const dataToInsert = parseInt(lines[1]);

        // Call the core logic method
        dll.insertAtTail(dataToInsert);

        // Print the modified list
        dll.printList();
    });
}

main();
```
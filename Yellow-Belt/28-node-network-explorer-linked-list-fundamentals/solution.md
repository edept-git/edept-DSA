# Solutions for Node Network Explorer: Linked List Fundamentals

### Approach
This problem requires implementing the core operations of a singly linked list: insertion at the end, deletion of a specific node, and traversal for printing.
The fundamental data structure is a `Node`, which will contain an integer `value` and a pointer/reference `next` to the subsequent node. The `LinkedList` itself will primarily manage a `head` pointer, pointing to the first node in the list. If the list is empty, `head` will be `NULL` or `None`.

For **insertion at the end**:
1.  Create a new `Node` with the given value.
2.  If the list is empty (`head` is `NULL`), the new node becomes the `head`.
3.  Otherwise, traverse the list starting from `head` until the last node is reached (i.e., the node whose `next` pointer is `NULL`).
4.  Set the `next` pointer of this last node to the new node.

For **deletion of a specific node by value**:
1.  First, check if the `head` node itself contains the target value. If so, update `head` to point to `head->next` (effectively removing the old head), and free/deallocate the old head node.
2.  If the head is not the target, traverse the list with two pointers: `current` and `previous`. `current` starts at `head` and `previous` starts as `NULL`. 
3.  Move `current` forward until `current` points to the node with the target value or `current` becomes `NULL`. Keep `previous` one step behind `current` during traversal.
4.  If the target node is found (`current` is not `NULL`):
    *   If `previous` is `NULL`, it means the head node was the target, so update `head = current->next`.
    *   Otherwise (`previous` is not `NULL`), update `previous->next` to point to `current->next`, thereby bypassing and removing the `current` node. 
5.  After unlinking, free/deallocate the `current` node (if applicable in languages like C/C++).
6.  If `current` becomes `NULL` without finding the target, the value is not in the list, and no deletion occurs.

For **traversal and printing**:
1.  Start from the `head` of the list.
2.  Iterate through the list, printing the `value` of each node.
3.  Move to the next node using the `next` pointer (`current = current->next`).
4.  Continue until `current` becomes `NULL`.
5.  Ensure a space separates values and a newline character is printed at the end of the list.

**Time Complexity**:
*   **Insertion at End**: In the worst case, we might need to traverse the entire list to find the last node. This makes it O(N) where N is the number of nodes in the list.
*   **Deletion of Specific Node**: Similarly, in the worst case, we might need to traverse almost the entire list to find the node to delete or to determine it doesn't exist. This is also O(N).
*   **Printing List**: We visit each node once, so it's O(N).

**Space Complexity**:
*   The linked list itself consumes O(N) space, where N is the number of nodes.
*   Auxiliary space for operations (pointers, temporary variables) is O(1).


## C Solution
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// Define Node structure
typedef struct Node {
    int value;
    struct Node* next;
} Node;

// Define LinkedList structure
typedef struct LinkedList {
    Node* head;
} LinkedList;

// Function to create a new Node
Node* createNode(int value) {
    Node* newNode = (Node*)malloc(sizeof(Node));
    if (newNode == NULL) {
        fprintf(stderr, "Memory allocation failed\n");
        exit(EXIT_FAILURE);
    }
    newNode->value = value;
    newNode->next = NULL;
    return newNode;
}

// Function to initialize a LinkedList
void initLinkedList(LinkedList* list) {
    list->head = NULL;
}

// Function to insert a node at the end of the list
void insertAtEnd(LinkedList* list, int value) {
    Node* newNode = createNode(value);
    if (list->head == NULL) {
        list->head = newNode;
    } else {
        Node* current = list->head;
        while (current->next != NULL) {
            current = current->next;
        }
        current->next = newNode;
    }
}

// Function to delete the first occurrence of a node with a given value
void deleteNode(LinkedList* list, int value) {
    Node* current = list->head;
    Node* previous = NULL;

    // If head node itself holds the value to be deleted
    if (current != NULL && current->value == value) {
        list->head = current->next; // Changed head
        free(current);             // Free old head
        return;
    }

    // Search for the value to be deleted, keep track of the previous node
    while (current != NULL && current->value != value) {
        previous = current;
        current = current->next;
    }

    // If value was not present in the list
    if (current == NULL) {
        return;
    }

    // Unlink the node from the linked list
    previous->next = current->next;
    free(current); // Free memory
}

// Function to print the linked list
void printList(LinkedList* list) {
    Node* current = list->head;
    if (current == NULL) {
        printf("\n"); // Print newline for empty list
        return;
    }
    while (current != NULL) {
        printf("%d", current->value);
        current = current->next;
        if (current != NULL) {
            printf(" ");
        }
    }
    printf("\n");
}

// Function to free all nodes in the list (destructor equivalent)
void freeList(LinkedList* list) {
    Node* current = list->head;
    Node* next;
    while (current != NULL) {
        next = current->next;
        free(current);
        current = next;
    }
    list->head = NULL;
}

int main() {
    LinkedList mylist;
    initLinkedList(&mylist);

    char command[10];
    int value;

    while (scanf("%s", command) != EOF) {
        if (strcmp(command, "insert") == 0) {
            scanf("%d", &value);
            insertAtEnd(&mylist, value);
        } else if (strcmp(command, "delete") == 0) {
            scanf("%d", &value);
            deleteNode(&mylist, value);
        } else if (strcmp(command, "print") == 0) {
            printList(&mylist);
        }
    }

    freeList(&mylist); // Clean up allocated memory
    return 0;
}

```

## C++ Solution
```cpp
#include <iostream>
#include <string>
#include <sstream>

// Define Node structure
struct Node {
    int value;
    Node* next;

    Node(int val) : value(val), next(nullptr) {}
};

// Define LinkedList class
class LinkedList {
public:
    Node* head;

    LinkedList() : head(nullptr) {}

    ~LinkedList() {
        Node* current = head;
        Node* nextNode;
        while (current != nullptr) {
            nextNode = current->next;
            delete current;
            current = nextNode;
        }
        head = nullptr; // Ensure head is null after destruction
    }

    // Function to insert a node at the end of the list
    void insertAtEnd(int value) {
        Node* newNode = new Node(value);
        if (head == nullptr) {
            head = newNode;
        } else {
            Node* current = head;
            while (current->next != nullptr) {
                current = current->next;
            }
            current->next = newNode;
        }
    }

    // Function to delete the first occurrence of a node with a given value
    void deleteNode(int value) {
        Node* current = head;
        Node* previous = nullptr;

        // If head node itself holds the value to be deleted
        if (current != nullptr && current->value == value) {
            head = current->next; // Changed head
            delete current;       // Free old head
            return;
        }

        // Search for the value to be deleted, keep track of the previous node
        while (current != nullptr && current->value != value) {
            previous = current;
            current = current->next;
        }

        // If value was not present in the list
        if (current == nullptr) {
            return;
        }

        // Unlink the node from the linked list
        previous->next = current->next;
        delete current; // Free memory
    }

    // Function to print the linked list
    void printList() {
        Node* current = head;
        if (current == nullptr) {
            std::cout << std::endl;
            return;
        }
        while (current != nullptr) {
            std::cout << current->value;
            current = current->next;
            if (current != nullptr) {
                std::cout << " ";
            }
        }
        std::cout << std::endl;
    }
};

int main() {
    LinkedList mylist;
    std::string line;
    std::string command;
    int value;

    while (std::cin >> command) {
        if (command == "insert") {
            std::cin >> value;
            mylist.insertAtEnd(value);
        } else if (command == "delete") {
            std::cin >> value;
            mylist.deleteNode(value);
        } else if (command == "print") {
            mylist.printList();
        }
    }

    return 0;
}

```

## Java Solution
```java
import java.util.Scanner;

// Define Node class
class Node {
    int value;
    Node next;

    Node(int val) {
        value = val;
        next = null;
    }
}

// Define LinkedList class
class LinkedList {
    Node head;

    public LinkedList() {
        head = null;
    }

    // Function to insert a node at the end of the list
    public void insertAtEnd(int value) {
        Node newNode = new Node(value);
        if (head == null) {
            head = newNode;
        } else {
            Node current = head;
            while (current.next != null) {
                current = current.next;
            }
            current.next = newNode;
        }
    }

    // Function to delete the first occurrence of a node with a given value
    public void deleteNode(int value) {
        Node current = head;
        Node previous = null;

        // If head node itself holds the value to be deleted
        if (current != null && current.value == value) {
            head = current.next; // Changed head
            return;
        }

        // Search for the value to be deleted, keep track of the previous node
        while (current != null && current.value != value) {
            previous = current;
            current = current.next;
        }

        // If value was not present in the list
        if (current == null) {
            return;
        }

        // Unlink the node from the linked list
        previous.next = current.next;
    }

    // Function to print the linked list
    public void printList() {
        Node current = head;
        if (current == null) {
            System.out.println();
            return;
        }
        StringBuilder sb = new StringBuilder();
        while (current != null) {
            sb.append(current.value);
            current = current.next;
            if (current != null) {
                sb.append(" ");
            }
        }
        System.out.println(sb.toString());
    }
}

public class Solution {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        LinkedList mylist = new LinkedList();

        while (scanner.hasNext()) {
            String command = scanner.next();
            if (command.equals("insert")) {
                int value = scanner.nextInt();
                mylist.insertAtEnd(value);
            } else if (command.equals("delete")) {
                int value = scanner.nextInt();
                mylist.deleteNode(value);
            } else if (command.equals("print")) {
                mylist.printList();
            }
        }
        scanner.close();
    }
}

```

## Python Solution
```python
class Node:
    def __init__(self, value):
        self.value = value
        self.next = None

class LinkedList:
    def __init__(self):
        self.head = None

    def insertAtEnd(self, value):
        new_node = Node(value)
        if self.head is None:
            self.head = new_node
        else:
            current = self.head
            while current.next:
                current = current.next
            current.next = new_node

    def deleteNode(self, value):
        current = self.head
        previous = None

        # If head node itself holds the value to be deleted
        if current is not None and current.value == value:
            self.head = current.next
            return

        # Search for the value to be deleted, keep track of the previous node
        while current is not None and current.value != value:
            previous = current
            current = current.next

        # If value was not present in the list
        if current is None:
            return

        # Unlink the node from the linked list
        previous.next = current.next

    def printList(self):
        current = self.head
        elements = []
        while current:
            elements.append(str(current.value))
            current = current.next
        print(" ".join(elements))

if __name__ == '__main__':
    mylist = LinkedList()
    
    import sys
    for line in sys.stdin:
        parts = line.strip().split()
        command = parts[0]

        if command == "insert":
            value = int(parts[1])
            mylist.insertAtEnd(value);
        elif command == "delete":
            value = int(parts[1])
            mylist.deleteNode(value)
        elif command == "print":
            mylist.printList()

```

## JavaScript Solution
```javascript
class Node {
    constructor(value) {
        this.value = value;
        this.next = null;
    }
}

class LinkedList {
    constructor() {
        this.head = null;
    }

    // Function to insert a node at the end of the list
    insertAtEnd(value) {
        const newNode = new Node(value);
        if (this.head === null) {
            this.head = newNode;
        } else {
            let current = this.head;
            while (current.next !== null) {
                current = current.next;
            }K
            current.next = newNode;
        }
    }

    // Function to delete the first occurrence of a node with a given value
    deleteNode(value) {
        let current = this.head;
        let previous = null;

        // If head node itself holds the value to be deleted
        if (current !== null && current.value === value) {
            this.head = current.next; // Changed head
            return;
        }

        // Search for the value to be deleted, keep track of the previous node
        while (current !== null && current.value !== value) {
            previous = current;
            current = current.next;
        }

        // If value was not present in the list
        if (current === null) {
            return;
        }

        // Unlink the node from the linked list
        previous.next = current.next;
    }

    // Function to print the linked list
    printList() {
        let current = this.head;
        const elements = [];
        while (current !== null) {
            elements.push(current.value);
            current = current.next;
        }
        console.log(elements.join(" "));
    }
}

// Main execution logic to handle input/output
function main() {
    const mylist = new LinkedList();
    const readline = require('readline');
    const rl = readline.createInterface({
        input: process.stdin,
        output: process.stdout,
        terminal: false
    });

    rl.on('line', (line) => {
        const parts = line.trim().split(' ');
        const command = parts[0];

        if (command === "insert") {
            const value = parseInt(parts[1], 10);
            mylist.insertAtEnd(value);
        } else if (command === "delete") {
            const value = parseInt(parts[1], 10);
            mylist.deleteNode(value);
        } else if (command === "print") {
            mylist.printList();
        }
    });

    // Handle end of input for cases where rl.on('close') might be needed for a final print or cleanup
    // For this problem, commands are processed line by line, so no explicit 'close' handling is strictly necessary
    // for functional correctness if input ends after the last command.
}

main();

```
# Solutions for Chain Reaction: List Operations

### Approach
This problem requires implementing fundamental operations on a singly linked list. We'll define a `Node` structure (or class) that holds an integer `data` value and a pointer (or reference) to the `next` node. The linked list itself will be managed by a `head` pointer, which points to the first node in the list. Initially, the `head` will be `NULL` (or `null`/`None`) indicating an empty list.

For **inserting a node at the end**: If the list is empty, the new node becomes the `head`. Otherwise, we traverse the list starting from the `head` until we reach the last node (the one whose `next` pointer is `NULL`). We then set this last node's `next` pointer to the new node. This operation has a time complexity of O(N) because, in the worst case, we might need to traverse the entire list.

For **deleting a node at a specific index**: We first handle the edge case where the list is empty or the index is out of bounds. If the `index` is 0, it means we are deleting the `head` node; we simply update `head` to point to `head->next` and free the original `head` node. For any other `index`, we traverse the list to find the node *just before* the target node. Let's call this `prev`. We then update `prev->next` to point to `prev->next->next`, effectively bypassing and removing the target node. The target node's memory should then be deallocated (if applicable). This operation also has a time complexity of O(N) as we might need to traverse up to the target index.

For **printing the list**: We start from the `head` and traverse the list, printing the `data` of each node until we reach a `NULL` `next` pointer. If the `head` is `NULL` initially, the list is empty, and we print a corresponding message. This operation has a time complexity of O(N).

The space complexity for storing the linked list is O(N), where N is the number of nodes, as each node consumes constant additional space.

## C Solution
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// Node structure for singly linked list
struct Node {
    int data;
    struct Node* next;
};

// Function to create a new node
struct Node* createNode(int data) {
    struct Node* newNode = (struct Node*)malloc(sizeof(struct Node));
    if (newNode == NULL) {
        perror("Failed to allocate memory for new node");
        exit(EXIT_FAILURE);
    }
    newNode->data = data;
    newNode->next = NULL;
    return newNode;
}

// Function to insert a node at the end of the list
struct Node* insertEnd(struct Node* head, int data) {
    struct Node* newNode = createNode(data);
    if (head == NULL) {
        return newNode; // New node becomes the head
    } else {
        struct Node* current = head;
        while (current->next != NULL) {
            current = current->next;
        }
        current->next = newNode;
        return head;
    }
}

// Function to delete a node at a specific index
struct Node* deleteAtIndex(struct Node* head, int index) {
    if (head == NULL) {
        return NULL; // List is empty
    }

    if (index == 0) {
        struct Node* temp = head;
        head = head->next;
        free(temp); // Free the old head
        return head;
    }

    struct Node* current = head;
    struct Node* prev = NULL;
    int count = 0;

    while (current != NULL && count < index) {
        prev = current;
        current = current->next;
        count++;
    }

    if (current == NULL) {
        // Index out of bounds
        return head;
    }

    // current is the node to be deleted
    prev->next = current->next;
    free(current);
    return head;
}

// Function to print the linked list
void printList(struct Node* head) {
    if (head == NULL) {
        printf("List is empty.\n");
        return;
    }
    struct Node* current = head;
    while (current != NULL) {
        printf("%d", current->data);
        current = current->next;
        if (current != NULL) {
            printf(" ");
        }
    }
    printf("\n");
}

// Function to free all nodes in the list
void freeList(struct Node* head) {
    struct Node* current = head;
    struct Node* next;
    while (current != NULL) {
        next = current->next;
        free(current);
        current = next;
    }
}

int main() {
    struct Node* head = NULL;
    char command[10];
    int value, index;

    while (scanf("%s", command) != EOF) {
        if (strcmp(command, "I") == 0) {
            scanf("%d", &value);
            head = insertEnd(head, value);
        } else if (strcmp(command, "D") == 0) {
            scanf("%d", &index);
            head = deleteAtIndex(head, index);
        } else if (strcmp(command, "P") == 0) {
            printList(head);
        } else {
            break; // Unknown command or end of input stream
        }
    }

    freeList(head); // Clean up memory
    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <string>

// Node structure for singly linked list
struct Node {
    int data;
    Node* next;

    Node(int val) : data(val), next(nullptr) {}
};

// Function to insert a node at the end of the list
Node* insertEnd(Node* head, int data) {
    Node* newNode = new Node(data);
    if (head == nullptr) {
        return newNode; // New node becomes the head
    } else {
        Node* current = head;
        while (current->next != nullptr) {
            current = current->next;
        }
        current->next = newNode;
        return head;
    }
}

// Function to delete a node at a specific index
Node* deleteAtIndex(Node* head, int index) {
    if (head == nullptr) {
        return nullptr; // List is empty
    }

    if (index == 0) {
        Node* temp = head;
        head = head->next;
        delete temp; // Free the old head
        return head;
    }

    Node* current = head;
    Node* prev = nullptr;
    int count = 0;

    while (current != nullptr && count < index) {
        prev = current;
        current = current->next;
        count++;
    }

    if (current == nullptr) {
        // Index out of bounds
        return head;
    }

    // current is the node to be deleted
    prev->next = current->next;
    delete current;
    return head;
}

// Function to print the linked list
void printList(Node* head) {
    if (head == nullptr) {
        std::cout << "List is empty." << std::endl;
        return;
    }
    Node* current = head;
    while (current != nullptr) {
        std::cout << current->data;
        current = current->next;
        if (current != nullptr) {
            std::cout << " ";
        }
    }
    std::cout << std::endl;
}

// Function to free all nodes in the list
void freeList(Node* head) {
    Node* current = head;
    Node* next;
    while (current != nullptr) {
        next = current->next;
        delete current;
        current = next;
    }
}

int main() {
    Node* head = nullptr;
    std::string command;
    int value, index;

    while (std::cin >> command) {
        if (command == "I") {
            std::cin >> value;
            head = insertEnd(head, value);
        } else if (command == "D") {
            std::cin >> index;
            head = deleteAtIndex(head, index);
        } else if (command == "P") {
            printList(head);
        } else {
            break; // Unknown command or end of input stream
        }
    }

    freeList(head); // Clean up memory
    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

// Node class for singly linked list
class Node {
    int data;
    Node next;

    public Node(int data) {
        this.data = data;
        this.next = null;
    }
}

// LinkedList class to manage operations
class SinglyLinkedList {
    Node head;

    public SinglyLinkedList() {
        this.head = null;
    }

    // Method to insert a node at the end of the list
    public void insertEnd(int data) {
        Node newNode = new Node(data);
        if (this.head == null) {
            this.head = newNode;
        } else {
            Node current = this.head;
            while (current.next != null) {
                current = current.next;
            }
            current.next = newNode;
        }
    }

    // Method to delete a node at a specific index
    public void deleteAtIndex(int index) {
        if (this.head == null) {
            return; // List is empty
        }

        if (index == 0) {
            this.head = this.head.next;
            return;
        }

        Node current = this.head;
        Node prev = null;
        int count = 0;

        while (current != null && count < index) {
            prev = current;
            current = current.next;
            count++;
        }

        if (current == null) {
            // Index out of bounds
            return;
        }

        // current is the node to be deleted
        prev.next = current.next;
    }

    // Method to print the linked list
    public void printList() {
        if (this.head == null) {
            System.out.println("List is empty.");
            return;
        }
        Node current = this.head;
        StringBuilder sb = new StringBuilder();
        while (current != null) {
            sb.append(current.data);
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
        SinglyLinkedList list = new SinglyLinkedList();

        while (scanner.hasNext()) {
            String command = scanner.next();
            if (command.equals("I")) {
                int value = scanner.nextInt();
                list.insertEnd(value);
            } else if (command.equals("D")) {
                int index = scanner.nextInt();
                list.deleteAtIndex(index);
            } else if (command.equals("P")) {
                list.printList();
            } else {
                break; // Unknown command or end of input stream
            }
        }
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
        self.next = None

class SinglyLinkedList:
    def __init__(self):
        self.head = None

    def insert_end(self, data):
        new_node = Node(data)
        if self.head is None:
            self.head = new_node
        else:
            current = self.head
            while current.next is not None:
                current = current.next
            current.next = new_node

    def delete_at_index(self, index):
        if self.head is None:
            return # List is empty

        if index == 0:
            self.head = self.head.next
            return

        current = self.head
        prev = None
        count = 0

        while current is not None and count < index:
            prev = current
            current = current.next
            count += 1

        if current is None:
            # Index out of bounds
            return

        # current is the node to be deleted
        prev.next = current.next

    def print_list(self):
        if self.head is None:
            print("List is empty.")
            return
        
        elements = []
        current = self.head
        while current is not None:
            elements.append(str(current.data))
            current = current.next
        print(" ".join(elements))

# Main logic for reading input and executing commands
def main():
    list_obj = SinglyLinkedList()

    for line in sys.stdin:
        parts = line.strip().split()
        if not parts:
            continue
        
        command = parts[0]
        if command == 'I':
            value = int(parts[1])
            list_obj.insert_end(value)
        elif command == 'D':
            index = int(parts[1])
            list_obj.delete_at_index(index)
        elif command == 'P':
            list_obj.print_list()
        else:
            break # Unknown command or end of input

if __name__ == "__main__":
    main()
```

## JavaScript Solution
```javascript
// Node class for singly linked list
class Node {
    constructor(data) {
        this.data = data;
        this.next = null;
    }
}

// LinkedList class to manage operations
class SinglyLinkedList {
    constructor() {
        this.head = null;
    }

    // Method to insert a node at the end of the list
    insertEnd(data) {
        const newNode = new Node(data);
        if (this.head === null) {
            this.head = newNode;
        } else {
            let current = this.head;
            while (current.next !== null) {
                current = current.next;
            }
            current.next = newNode;
        }
    }

    // Method to delete a node at a specific index
    deleteAtIndex(index) {
        if (this.head === null) {
            return; // List is empty
        }

        if (index === 0) {
            this.head = this.head.next;
            return;
        }

        let current = this.head;
        let prev = null;
        let count = 0;

        while (current !== null && count < index) {
            prev = current;
            current = current.next;
            count++;
        }

        if (current === null) {
            // Index out of bounds
            return;
        }

        // current is the node to be deleted
        prev.next = current.next;
    }

    // Method to print the linked list
    printList() {
        if (this.head === null) {
            console.log("List is empty.");
            return;
        }
        let elements = [];
        let current = this.head;
        while (current !== null) {
            elements.push(current.data);
            current = current.next;
        }
        console.log(elements.join(" "));
    }
}

// Main logic for reading input and executing commands
function main() {
    const list = new SinglyLinkedList();
    const readline = require('readline');
    const rl = readline.createInterface({
        input: process.stdin,
        output: process.stdout,
        terminal: false
    });

    rl.on('line', (line) => {
        const parts = line.trim().split(' ');
        if (parts.length === 0) {
            return;
        }

        const command = parts[0];
        if (command === 'I') {
            const value = parseInt(parts[1], 10);
            list.insertEnd(value);
        } else if (command === 'D') {
            const index = parseInt(parts[1], 10);
            list.deleteAtIndex(index);
        } else if (command === 'P') {
            list.printList();
        }
    });

    rl.on('close', () => {
        // Any final cleanup if needed
    });
}

// Call the main function to start execution
main();
```
# Solutions for Reverse Linked List

### Approach
The optimal approach to reverse a linked list iteratively involves using three pointers: `prev`, `curr`, and `next_node` (or `temp`).
1. Initialize `prev` to `NULL` (or `None` in Python), as it will eventually be the new tail of the reversed list.
2. Initialize `curr` to `head`, as this is where we start traversing.
3. Loop while `curr` is not `NULL`:
    a. Store `curr.next` in `next_node`. This is crucial because `curr.next` is about to be modified, and we need to remember where to go next.
    b. Make `curr.next` point to `prev`. This is the actual reversal step, flipping the pointer.
    c. Move `prev` forward: `prev = curr`. `prev` now becomes the node we just processed.
    d. Move `curr` forward: `curr = next_node`. `curr` now points to the next node in the original list.
4. After the loop finishes, `curr` will be `NULL`, and `prev` will be pointing to the original last node, which is now the new head of the reversed list. Return `prev`.

This algorithm visits each node exactly once, resulting in a **Time Complexity** of O(N), where N is the number of nodes in the list. It uses a constant number of extra pointers, leading to a **Space Complexity** of O(1).

## C Solution
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// Definition for singly-linked list.
struct ListNode {
    int val;
    struct ListNode *next;
};

struct ListNode* reverseList(struct ListNode* head) {
    struct ListNode* prev = NULL;
    struct ListNode* curr = head;
    struct ListNode* next_node = NULL;

    while (curr != NULL) {
        next_node = curr->next; // Store next node
        curr->next = prev;      // Reverse current node's pointer
        prev = curr;            // Move prev one step forward
        curr = next_node;       // Move curr one step forward
    }
    return prev; // prev will be the new head
}

// Helper function to create a new node
struct ListNode* createNode(int val) {
    struct ListNode* newNode = (struct ListNode*)malloc(sizeof(struct ListNode));
    if (newNode == NULL) {
        perror("Failed to allocate memory for ListNode");
        exit(EXIT_FAILURE);
    }
    newNode->val = val;
    newNode->next = NULL;
    return newNode;
}

// Helper function to print the list
void printList(struct ListNode* head) {
    struct ListNode* current = head;
    if (current == NULL) {
        printf("\n");
        return;
    }
    while (current != NULL) {
        printf("%d", current->val);
        if (current->next != NULL) {
            printf(" ");
        }
        current = current->next;
    }
    printf("\n");
}

// Helper function to free the list memory
void freeList(struct ListNode* head) {
    struct ListNode* current = head;
    while (current != NULL) {
        struct ListNode* temp = current;
        current = current->next;
        free(temp);
    }
}

int main() {
    struct ListNode* head = NULL;
    struct ListNode* tail = NULL;
    int val;

    char line[1000];
    if (fgets(line, sizeof(line), stdin) == NULL) {
        // Error reading or EOF immediately, treat as empty list
        printList(reverseList(head));
        return 0;
    }

    // Remove trailing newline character if present
    line[strcspn(line, "\n")] = 0;

    // If line is empty after stripping newline, it's an empty list
    if (strlen(line) == 0) {
        printList(reverseList(head));
        return 0;
    }

    char *token = strtok(line, " ");
    while (token != NULL) {
        val = atoi(token);
        struct ListNode* newNode = createNode(val);
        if (head == NULL) {
            head = newNode;
            tail = newNode;
        } else {
            tail->next = newNode;
            tail = newNode;
        }
        token = strtok(NULL, " ");
    }

    struct ListNode* reversedHead = reverseList(head);
    printList(reversedHead);

    freeList(reversedHead); // Free memory of the reversed list

    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <vector>
#include <string>
#include <sstream>

// Definition for singly-linked list.
struct ListNode {
    int val;
    ListNode *next;
    ListNode() : val(0), next(nullptr) {}
    ListNode(int x) : val(x), next(nullptr) {}
    ListNode(int x, ListNode *next) : val(x), next(next) {}
};

class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        ListNode* prev = nullptr;
        ListNode* curr = head;
        ListNode* next_node = nullptr;

        while (curr != nullptr) {
            next_node = curr->next; // Store next node
            curr->next = prev;      // Reverse current node's pointer
            prev = curr;            // Move prev one step forward
            curr = next_node;       // Move curr one step forward
        }
        return prev; // prev will be the new head
    }
};

// Helper function to print the list
void printList(ListNode* head) {
    ListNode* current = head;
    if (current == nullptr) {
        std::cout << std::endl;
        return;
    }
    while (current != nullptr) {
        std::cout << current->val;
        if (current->next != nullptr) {
            std::cout << " ";
        }
        current = current->next;
    }
    std::cout << std::endl;
}

// Helper function to free the list memory
void freeList(ListNode* head) {
    ListNode* current = head;
    while (current != nullptr) {
        ListNode* temp = current;
        current = current->next;
        delete temp;
    }
}

int main() {
    std::string line;
    std::getline(std::cin, line);

    ListNode* head = nullptr;
    ListNode* tail = nullptr;

    if (!line.empty()) {
        std::stringstream ss(line);
        int val;
        while (ss >> val) {
            ListNode* newNode = new ListNode(val);
            if (head == nullptr) {
                head = newNode;
                tail = newNode;
            } else {
                tail->next = newNode;
                tail = newNode;
            }
        }
    }

    Solution sol;
    ListNode* reversedHead = sol.reverseList(head);
    printList(reversedHead);

    freeList(reversedHead); // Free memory of the reversed list

    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

// Definition for singly-linked list.
class ListNode {
    int val;
    ListNode next;
    ListNode() {}
    ListNode(int val) { this.val = val; }
    ListNode(int val, ListNode next) { this.val = val; this.next = next; }
}

class Solution {
    public ListNode reverseList(ListNode head) {
        ListNode prev = null;
        ListNode curr = head;
        ListNode nextNode = null;

        while (curr != null) {
            nextNode = curr.next; // Store next node
            curr.next = prev;     // Reverse current node's pointer
            prev = curr;          // Move prev one step forward
            curr = nextNode;      // Move curr one step forward
        }
        return prev; // prev will be the new head
    }
}

public class Main {
    // Helper function to print the list
    public static void printList(ListNode head) {
        ListNode current = head;
        if (current == null) {
            System.out.println();
            return;
        }
        while (current != null) {
            System.out.print(current.val);
            if (current.next != null) {
                System.out.print(" ");
            }
            current = current.next;
        }
        System.out.println();
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        String line = scanner.nextLine();
        scanner.close();

        ListNode head = null;
        ListNode tail = null;

        if (!line.trim().isEmpty()) {
            String[] parts = line.trim().split(" ");
            for (String part : parts) {
                int val = Integer.parseInt(part);
                ListNode newNode = new ListNode(val);
                if (head == null) {
                    head = newNode;
                    tail = newNode;
                } else {
                    tail.next = newNode;
                    tail = newNode;
                }
            }
        }

        Solution sol = new Solution();
        ListNode reversedHead = sol.reverseList(head);
        printList(reversedHead);
    }
}
```

## Python Solution
```python
# Definition for singly-linked list.
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def reverseList(self, head: ListNode) -> ListNode:
        prev = None
        curr = head

        while curr:
            next_node = curr.next  # Store next node
            curr.next = prev       # Reverse current node's pointer
            prev = curr            # Move prev one step forward
            curr = next_node       # Move curr one step forward
        return prev # prev will be the new head

# Helper function to print the list
def print_list(head: ListNode):
    current = head
    values = []
    while current:
        values.append(str(current.val))
        current = current.next
    print(" ".join(values))

# Main function for I/O
if __name__ == "__main__":
    line = input().strip()

    head = None
    tail = None

    if line:
        values = list(map(int, line.split()))
        for val in values:
            new_node = ListNode(val)
            if head is None:
                head = new_node
                tail = new_node
            else:
                tail.next = new_node
                tail = new_node

    sol = Solution()
    reversed_head = sol.reverseList(head)
    print_list(reversed_head)
```

## JavaScript Solution
```javascript
// Definition for singly-linked list.
function ListNode(val, next) {
    this.val = (val===undefined ? 0 : val)
    this.next = (next===undefined ? null : next)
}

/**
 * @param {ListNode} head
 * @return {ListNode}
 */
var reverseList = function(head) {
    let prev = null;
    let curr = head;
    let nextNode = null;

    while (curr !== null) {
        nextNode = curr.next; // Store next node
        curr.next = prev;     // Reverse current node's pointer
        prev = curr;          // Move prev one step forward
        curr = nextNode;      // Move curr one step forward
    }
    return prev; // prev will be the new head
};

// Helper function to print the list
function printList(head) {
    let current = head;
    const values = [];
    while (current !== null) {
        values.push(current.val);
        current = current.next;
    }
    console.log(values.join(' '));
}

// Main function for I/O
const readline = require('readline');
const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});

rl.on('line', (line) => {
    let head = null;
    let tail = null;

    if (line.trim() !== '') {
        const values = line.split(' ').map(Number);
        for (const val of values) {
            const newNode = new ListNode(val);
            if (head === null) {
                head = newNode;
                tail = newNode;
            } else {
                tail.next = newNode;
                tail = newNode;
            }
        }
    }

    const reversedHead = reverseList(head);
    printList(reversedHead);
    rl.close();
});

```
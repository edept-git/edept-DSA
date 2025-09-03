# Solutions for Node Navigator: The Linked List Labyrinth

### Approach
The problem requires us to perform two main operations: constructing a singly linked list from an array and then deleting the first occurrence of a specific value. First, we'll iterate through the input array to build the linked list. For each element in the array, a new `ListNode` will be created and appended to the end of the list. We'll maintain a `head` pointer and a `tail` pointer during this construction to efficiently add new nodes. Once the list is formed, we proceed to the deletion step. To delete the first occurrence of the target value, we'll traverse the linked list using two pointers: a `current` pointer and a `previous` pointer. The `previous` pointer will always lag one step behind the `current` pointer. Before starting the traversal, we must handle the edge case where the `head` node itself contains the target value. If so, we simply update the `head` to `head.next` and free the old head (if memory management is manual). Otherwise, we iterate, moving both `current` and `previous` forward. When `current` points to a node whose value matches the target, we update `previous.next` to point to `current.next`, effectively removing `current` from the list. After deletion, we stop and return the potentially new head of the list. If the loop finishes without finding the target, the list remains unchanged. This approach ensures that only the first occurrence is deleted.

The time complexity for creating the linked list from an array of N elements is O(N), as we visit each element once. The deletion operation also involves traversing the list, which in the worst case might require visiting all N nodes to find the target or determine it's not present, resulting in O(N) time complexity. Thus, the overall time complexity is O(N). The space complexity is O(N) to store the linked list itself.

## C Solution
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// Definition for singly-linked list.
typedef struct ListNode {
    int val;
    struct ListNode *next;
} ListNode;

// Function to create a new node
ListNode* createNode(int val) {
    ListNode* newNode = (ListNode*)malloc(sizeof(ListNode));
    if (newNode == NULL) {
        perror("Failed to allocate memory for node");
        exit(EXIT_FAILURE);
    }
    newNode->val = val;
    newNode->next = NULL;
    return newNode;
}

// Function to create a linked list from an array (represented as space-separated string)
ListNode* createListFromArray(const char* input_str) {
    ListNode* head = NULL;
    ListNode* tail = NULL;
    
    // Handle empty input string for an empty list
    if (input_str == NULL || strlen(input_str) == 0 || (strlen(input_str) == 1 && input_str[0] == '\n')) {
        return NULL;
    }

    char* str_copy = strdup(input_str); // Duplicate string for strtok_r
    if (str_copy == NULL) {
        perror("Failed to duplicate string");
        exit(EXIT_FAILURE);
    }
    
    char* token;
    char* rest = str_copy;

    while ((token = strtok_r(rest, " ", &rest)) != NULL) {
        int val = atoi(token);
        ListNode* newNode = createNode(val);
        if (head == NULL) {
            head = newNode;
            tail = newNode;
        } else {
            tail->next = newNode;
            tail = newNode;
        }
    }
    free(str_copy);
    return head;
}

// Function to delete the first occurrence of a node with a specific value
ListNode* deleteFirstOccurrence(ListNode* head, int target) {
    if (head == NULL) {
        return NULL;
    }

    // Case 1: Head node is the target
    if (head->val == target) {
        ListNode* temp = head;
        head = head->next;
        free(temp); // Free memory of the deleted node
        return head;
    }

    // Case 2: Target is in the rest of the list
    ListNode* current = head->next;
    ListNode* previous = head;

    while (current != NULL && current->val != target) {
        previous = current;
        current = current->next;
    }

    // If target found
    if (current != NULL) {
        previous->next = current->next;
        free(current); // Free memory of the deleted node
    }

    return head;
}

// Function to print the linked list
void printList(ListNode* head) {
    if (head == NULL) {
        printf("Empty\n");
        return;
    }
    ListNode* current = head;
    while (current != NULL) {
        printf("%d", current->val);
        if (current->next != NULL) {
            printf(" ");
        }
        current = current->next;
    }
    printf("\n");
}

// Function to free the linked list memory
void freeList(ListNode* head) {
    ListNode* current = head;
    while (current != NULL) {
        ListNode* next = current->next;
        free(current);
        current = next;
    }
}

int main() {
    char line[4000]; // Increased buffer size for potentially large inputs
    
    // Read array input
    if (fgets(line, sizeof(line), stdin) == NULL) {
        return 1;
    }
    line[strcspn(line, "\n")] = 0; // Remove newline character

    ListNode* head = createListFromArray(line);

    // Read target value
    int target;
    if (scanf("%d", &target) != 1) {
        freeList(head);
        return 1;
    }

    head = deleteFirstOccurrence(head, target);

    printList(head);
    freeList(head); // Free all allocated memory

    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <vector>
#include <string>
#include <sstream>
#include <limits> // Required for numeric_limits

// Definition for singly-linked list.
struct ListNode {
    int val;
    ListNode *next;
    ListNode(int x) : val(x), next(nullptr) {}
};

// Function to create a linked list from a vector
ListNode* createListFromArray(const std::vector<int>& arr) {
    if (arr.empty()) {
        return nullptr;
    }
    ListNode* head = new ListNode(arr[0]);
    ListNode* tail = head;
    for (size_t i = 1; i < arr.size(); ++i) {
        tail->next = new ListNode(arr[i]);
        tail = tail->next;
    }
    return head;
}

// Function to delete the first occurrence of a node with a specific value
ListNode* deleteFirstOccurrence(ListNode* head, int target) {
    if (head == nullptr) {
        return nullptr;
    }

    // Case 1: Head node is the target
    if (head->val == target) {
        ListNode* temp = head;
        head = head->next;
        delete temp; // Free memory of the deleted node
        return head;
    }

    // Case 2: Target is in the rest of the list
    ListNode* current = head->next;
    ListNode* previous = head;

    while (current != nullptr && current->val != target) {
        previous = current;
        current = current->next;
    }

    // If target found
    if (current != nullptr) {
        previous->next = current->next;
        delete current; // Free memory of the deleted node
    }

    return head;
}

// Function to print the linked list
void printList(ListNode* head) {
    if (head == nullptr) {
        std::cout << "Empty" << std::endl;
        return;
    }
    ListNode* current = head;
    while (current != nullptr) {
        std::cout << current->val;
        if (current->next != nullptr) {
            std::cout << " ";
        }
        current = current->next;
    }
    std::cout << std::endl;
}

// Function to free the linked list memory
void freeList(ListNode* head) {
    ListNode* current = head;
    while (current != nullptr) {
        ListNode* next = current->next;
        delete current;
        current = next;
    }
}

int main() {
    std::string line;
    std::getline(std::cin, line);

    std::vector<int> arr;
    if (!line.empty()) { // Handle empty line for empty list case
        std::stringstream ss(line);
        int val;
        while (ss >> val) {
            arr.push_back(val);
        }
    }

    ListNode* head = createListFromArray(arr);

    int target;
    std::cin >> target;

    // Clear the rest of the input buffer after reading target
    std::cin.ignore(std::numeric_limits<std::streamsize>::max(), '\n');

    head = deleteFirstOccurrence(head, target);

    printList(head);
    freeList(head); // Free all allocated memory

    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;
import java.util.ArrayList;
import java.util.List;

// Definition for singly-linked list.
class ListNode {
    int val;
    ListNode next;

    ListNode(int x) {
        val = x;
        next = null;
    }
}

class Solution {

    // Function to create a linked list from an array
    public ListNode createListFromArray(List<Integer> arr) {
        if (arr == null || arr.isEmpty()) {
            return null;
        }
        ListNode head = new ListNode(arr.get(0));
        ListNode tail = head;
        for (int i = 1; i < arr.size(); i++) {
            tail.next = new ListNode(arr.get(i));
            tail = tail.next;
        }
        return head;
    }

    // Function to delete the first occurrence of a node with a specific value
    public ListNode deleteFirstOccurrence(ListNode head, int target) {
        if (head == null) {
            return null;
        }

        // Case 1: Head node is the target
        if (head.val == target) {
            return head.next;
        }

        // Case 2: Target is in the rest of the list
        ListNode current = head.next;
        ListNode previous = head;

        while (current != null && current.val != target) {
            previous = current;
            current = current.next;
        }

        // If target found
        if (current != null) {
            previous.next = current.next;
        }

        return head;
    }

    // Function to print the linked list
    public void printList(ListNode head) {
        if (head == null) {
            System.out.println("Empty");
            return;
        }
        ListNode current = head;
        StringBuilder sb = new StringBuilder();
        while (current != null) {
            sb.append(current.val);
            if (current.next != null) {
                sb.append(" ");
            }
            current = current.next;
        }
        System.out.println(sb.toString());
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        Solution sol = new Solution();

        // Read array input
        String line = scanner.nextLine();
        List<Integer> arr = new ArrayList<>();
        if (!line.trim().isEmpty()) { // Handle empty line for empty list case
            String[] numStrs = line.split(" ");
            for (String s : numStrs) {
                arr.add(Integer.parseInt(s));
            }
        }
        

        ListNode head = sol.createListFromArray(arr);

        // Read target value
        int target = scanner.nextInt();

        head = sol.deleteFirstOccurrence(head, target);

        sol.printList(head);

        scanner.close();
    }
}
```

## Python Solution
```python
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def createListFromArray(self, arr):
        if not arr:
            return None
        head = ListNode(arr[0])
        tail = head
        for i in range(1, len(arr)):
            tail.next = ListNode(arr[i])
            tail = tail.next
        return head

    def deleteFirstOccurrence(self, head: ListNode, target: int) -> ListNode:
        if not head:
            return None

        # Case 1: Head node is the target
        if head.val == target:
            return head.next

        # Case 2: Target is in the rest of the list
        current = head.next
        previous = head

        while current and current.val != target:
            previous = current
            current = current.next

        # If target found
        if current:
            previous.next = current.next
        
        return head

    def printList(self, head: ListNode):
        if not head:
            print("Empty")
            return
        current = head
        result = []
        while current:
            result.append(str(current.val))
            current = current.next
        print(" ".join(result))

if __name__ == "__main__":
    sol = Solution()

    # Read array input
    line = input()
    arr = []
    if line.strip(): # Handle empty line for empty list case
        arr = list(map(int, line.split()))

    head = sol.createListFromArray(arr)

    # Read target value
    target = int(input())

    head = sol.deleteFirstOccurrence(head, target)

    sol.printList(head)

```

## JavaScript Solution
```javascript
// Definition for singly-linked list.
function ListNode(val, next) {
    this.val = (val === undefined ? 0 : val);
    this.next = (next === undefined ? null : next);
}

class Solution {
    createListFromArray(arr) {
        if (!arr || arr.length === 0) {
            return null;
        }
        let head = new ListNode(arr[0]);
        let tail = head;
        for (let i = 1; i < arr.length; i++) {
            tail.next = new ListNode(arr[i]);
            tail = tail.next;
        }
        return head;
    }

    deleteFirstOccurrence(head, target) {
        if (!head) {
            return null;
        }

        // Case 1: Head node is the target
        if (head.val === target) {
            return head.next;
        }

        // Case 2: Target is in the rest of the list
        let current = head.next;
        let previous = head;

        while (current && current.val !== target) {
            previous = current;
            current = current.next;
        }

        // If target found
        if (current) {
            previous.next = current.next;
        }

        return head;
    }

    printList(head) {
        if (!head) {
            console.log("Empty");
            return;
        }
        let current = head;
        let result = [];
        while (current) {
            result.push(current.val);
            current = current.next;
        }
        console.log(result.join(" "));
    }
}

// Main execution for JS environment
// This part handles input/output for a typical online judge setup
const readline = require('readline');
const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});

let lines = [];
rl.on('line', (line) => {
    lines.push(line);
}).on('close', () => {
    const sol = new Solution();

    // Read array input
    const arrStr = lines[0];
    let arr = [];
    if (arrStr.trim() !== '') { // Handle empty line for empty list case
        arr = arrStr.split(' ').map(Number);
    }
    
    let head = sol.createListFromArray(arr);

    // Read target value
    const target = parseInt(lines[1]);

    head = sol.deleteFirstOccurrence(head, target);

    sol.printList(head);
});
```
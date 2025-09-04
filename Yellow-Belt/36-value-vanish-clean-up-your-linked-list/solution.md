# Solutions for Value Vanish: Clean Up Your Linked List

### Approach
The most straightforward approach to delete all occurrences of a specific value `val` from a singly linked list involves iterating through the list and carefully adjusting pointers. First, we handle the special case where the target value might be at the head of the list. We advance the `head` pointer past any initial nodes that match `val`. After this, we use two pointers: `current` and `prev`. `current` iterates through the list, and `prev` always points to the node immediately preceding `current`. If `current.val` matches `val`, we 'bypass' `current` by setting `prev.next = current.next`. The `current` node itself is then (conceptually) deleted, and we advance `current` to `current.next`. If `current.val` does not match `val`, we simply advance both `prev` and `current` one step forward. This ensures that `prev` always maintains the correct reference to the last non-deleted node. Finally, we return the (possibly new) head of the list. This algorithm traverses the list exactly once, resulting in a time complexity of O(N), where N is the number of nodes in the list. The space complexity is O(1) as we only use a few extra pointers.

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

// Function to delete nodes with a specific value
struct ListNode* deleteNodesWithValue(struct ListNode* head, int val) {
    // Handle deletions at the head
    while (head != NULL && head->val == val) {
        struct ListNode* temp = head;
        head = head->next;
        free(temp); // Free memory
    }
    
    struct ListNode* current = head;
    struct ListNode* prev = NULL;

    while (current != NULL) {
        if (current->val == val) {
            // Bypass current node
            if (prev != NULL) {
                prev->next = current->next;
            }
            // Free memory for the deleted node
            struct ListNode* temp = current;
            current = current->next; // Move current before deleting temp
            free(temp);
        } else {
            prev = current;
            current = current->next;
        }
    }
    
    return head;
}

// Function to create a linked list from an array of integers
struct ListNode* createLinkedList(int* arr, int size) {
    if (size == 0) {
        return NULL;
    }
    struct ListNode* head = (struct ListNode*)malloc(sizeof(struct ListNode));
    head->val = arr[0];
    head->next = NULL;
    struct ListNode* current = head;
    for (int i = 1; i < size; ++i) {
        current->next = (struct ListNode*)malloc(sizeof(struct ListNode));
        current = current->next;
        current->val = arr[i];
        current->next = NULL;
    }
    return head;
}

// Function to print a linked list and free memory
void printAndFreeLinkedList(struct ListNode* head) {
    struct ListNode* current = head;
    while (current != NULL) {
        printf("%d", current->val);
        if (current->next != NULL) {
            printf(" ");
        }
        struct ListNode* temp = current;
        current = current->next;
        free(temp); // Free memory
    }
    printf("\n");
}

int main() {
    char line[4000]; // Assuming max chars for input line (e.g., 1000 nodes * 5 digits + spaces)
    if (fgets(line, sizeof(line), stdin) == NULL) {
        // Handle empty input or error
        printAndFreeLinkedList(NULL); 
        return 0;
    }

    int nodeValues[1000]; // Assuming max 1000 nodes
    int count = 0;
    
    // Remove trailing newline character if present
    line[strcspn(line, "\n")] = 0; 

    if (strlen(line) > 0) {
        char *token = strtok(line, " ");
        while (token != NULL) {
            nodeValues[count++] = atoi(token);
            token = strtok(NULL, " ");
        }
    }

    int targetVal;
    // Check if scanf reads an integer successfully
    if (scanf("%d", &targetVal) != 1) {
        // If target value is not provided (e.g. only empty list line), handle it.
        // For this problem, it's assumed targetVal will always be provided.
        printAndFreeLinkedList(NULL);
        return 0;
    }

    struct ListNode* head = createLinkedList(nodeValues, count);
    struct ListNode* resultHead = deleteNodesWithValue(head, targetVal);
    printAndFreeLinkedList(resultHead);

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

ListNode* deleteNodesWithValue(ListNode* head, int val) {
    // Handle deletions at the head
    while (head != nullptr && head->val == val) {
        ListNode* temp = head;
        head = head->next;
        delete temp; // Free memory
    }
    
    ListNode* current = head;
    ListNode* prev = nullptr;

    while (current != nullptr) {
        if (current->val == val) {
            // Bypass current node
            if (prev != nullptr) {
                prev->next = current->next;
            }
            // Free memory for the deleted node
            ListNode* temp = current;
            current = current->next; // Move current before deleting temp
            delete temp;
        } else {
            prev = current;
            current = current->next;
        }
    }
    
    return head;
}

// Function to create a linked list from a vector
ListNode* createLinkedList(const std::vector<int>& arr) {
    if (arr.empty()) {
        return nullptr;
    }
    ListNode* head = new ListNode(arr[0]);
    ListNode* current = head;
    for (size_t i = 1; i < arr.size(); ++i) {
        current->next = new ListNode(arr[i]);
        current = current->next;
    }
    return head;
}

// Function to print a linked list and free memory
void printAndFreeLinkedList(ListNode* head) {
    ListNode* current = head;
    while (current != nullptr) {
        std::cout << current->val;
        if (current->next != nullptr) {
            std::cout << " ";
        }
        ListNode* temp = current;
        current = current->next;
        delete temp; // Free memory
    }
    std::cout << std::endl;
}

int main() {
    std::string line;
    std::getline(std::cin, line);
    std::vector<int> nodeValues;
    if (!line.empty()) {
        std::stringstream ss(line);
        std::string segment;
        while (std::getline(ss, segment, ' ')) {
            nodeValues.push_back(std::stoi(segment));
        }
    }

    int targetVal;
    std::cin >> targetVal;

    ListNode* head = createLinkedList(nodeValues);
    ListNode* resultHead = deleteNodesWithValue(head, targetVal);
    printAndFreeLinkedList(resultHead);

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
    ListNode() {}
    ListNode(int val) { this.val = val; }
    ListNode(int val, ListNode next) { this.val = val; this.next = next; }
}

public class Solution {
    public ListNode deleteNodesWithValue(ListNode head, int val) {
        // Handle deletions at the head
        while (head != null && head.val == val) {
            head = head.next;
        }
        
        ListNode current = head;
        ListNode prev = null;

        while (current != null) {
            if (current.val == val) {
                // Bypass current node
                if (prev != null) {
                    prev.next = current.next;
                }
                // No else needed, if current is head and has target value, it's handled by first while loop.
            } else {
                prev = current;
            }
            current = current.next;
        }
        
        return head;
    }

    // Function to create a linked list from a list of integers
    public ListNode createLinkedList(List<Integer> arr) {
        if (arr == null || arr.isEmpty()) {
            return null;
        }
        ListNode head = new ListNode(arr.get(0));
        ListNode current = head;
        for (int i = 1; i < arr.size(); ++i) {
            current.next = new ListNode(arr.get(i));
            current = current.next;
        }
        return head;
    }

    // Function to print a linked list
    public void printLinkedList(ListNode head) {
        StringBuilder sb = new StringBuilder();
        ListNode current = head;
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

        String line = scanner.nextLine();
        List<Integer> nodeValues = new ArrayList<>();
        if (!line.trim().isEmpty()) {
            String[] arrStr = line.split(" ");
            for (String s : arrStr) {
                nodeValues.add(Integer.parseInt(s));
            }
        }
        
        int targetVal = scanner.nextInt();

        ListNode head = sol.createLinkedList(nodeValues);
        ListNode resultHead = sol.deleteNodesWithValue(head, targetVal);
        sol.printLinkedList(resultHead);

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

def deleteNodesWithValue(head: ListNode, val: int) -> ListNode:
    # Handle deletions at the head
    while head and head.val == val:
        head = head.next
    
    current = head
    prev = None

    while current:
        if current.val == val:
            # Bypass current node
            if prev:
                prev.next = current.next
            # No else needed, if current is head and has target value, it's handled by first while loop.
        else:
            prev = current
        current = current.next
    
    return head

def create_linked_list(arr):
    if not arr:
        return None
    head = ListNode(arr[0])
    current = head
    for i in range(1, len(arr)):
        current.next = ListNode(arr[i])
        current = current.next
    return head

def print_linked_list(head):
    nodes = []
    current = head
    while current:
        nodes.append(str(current.val))
        current = current.next
    print(" ".join(nodes))

if __name__ == "__main__":
    try:
        input_line = input()
        if input_line.strip() == "":
            arr_str = []
        else:
            arr_str = input_line.split()
        
        node_values = [int(x) for x in arr_str]
        
        target_val = int(input())

        head = create_linked_list(node_values)
        result_head = deleteNodesWithValue(head, target_val)
        print_linked_list(result_head)
    except EOFError:
        # For empty list, input_line will be empty, correctly handled. 
        # If target_val input also missing due to specific test case setup, this catches it.
        # Generally, target_val is expected after list input.
        print_linked_list(None) # Print empty line for empty list (e.g. all nodes deleted)
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
 * @param {number} val
 * @return {ListNode}
 */
function deleteNodesWithValue(head, val) {
    // Handle deletions at the head
    while (head !== null && head.val === val) {
        head = head.next;
    }
    
    let current = head;
    let prev = null;

    while (current !== null) {
        if (current.val === val) {
            // Bypass current node
            if (prev !== null) {
                prev.next = current.next;
            }
            // No explicit memory management like C++/C in JS
        } else {
            prev = current;
        }
        current = current.next;
    }
    
    return head;
}

// Function to create a linked list from an array
function createLinkedList(arr) {
    if (!arr || arr.length === 0) {
        return null;
    }
    let head = new ListNode(arr[0]);
    let current = head;
    for (let i = 1; i < arr.length; ++i) {
        current.next = new ListNode(arr[i]);
        current = current.next;
    }
    return head;
}

// Function to print a linked list
function printLinkedList(head) {
    let nodes = [];
    let current = head;
    while (current !== null) {
        nodes.push(current.val);
        current = current.next;
    }
    console.log(nodes.join(" "));
}

// Main execution for handling input/output
function main() {
    const readline = require('readline');
    const rl = readline.createInterface({
        input: process.stdin,
        output: process.stdout
    });

    let lines = [];
    rl.on('line', (line) => {
        lines.push(line);
    }).on('close', () => {
        let nodeValuesStr = lines[0].trim();
        let nodeValues = [];
        if (nodeValuesStr !== "") {
            nodeValues = nodeValuesStr.split(' ').map(Number);
        }
        
        let targetVal = parseInt(lines[1]);

        let head = createLinkedList(nodeValues);
        let resultHead = deleteNodesWithValue(head, targetVal);
        printLinkedList(resultHead);
    });
}

main();
```
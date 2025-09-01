# Solutions for Bracket Bonanza: The Balancing Act

### Approach
The problem can be efficiently solved using a stack. We iterate through the input string character by character. If we encounter an opening bracket ('(', '{', '['), we push it onto the stack. If we encounter a closing bracket (')', '}', ']'), we check two conditions: First, if the stack is empty, it means there's no corresponding opening bracket, so the string is invalid. Second, if the stack is not empty, we pop the top element and check if it's the correct matching opening bracket for the current closing bracket. If they don't match, the string is invalid. If they match, we continue. After iterating through the entire string, if the stack is empty, it means all opening brackets have been correctly closed, and the string is valid. If the stack is not empty, it means there are unclosed opening brackets, and the string is invalid.

This approach uses a stack, which is a Last-In-First-Out (LIFO) data structure, perfectly suited for matching nested structures. The time complexity is O(N), where N is the length of the string, because we iterate through the string once. The space complexity is O(N) in the worst-case scenario (e.g., "((((("), where all characters are opening brackets and are pushed onto the stack.

## C Solution
```c
#include <stdio.h>
#include <stdbool.h>
#include <string.h>
#include <stdlib.h> // For malloc, free

// Stack implementation for characters
typedef struct {
    char* arr;
    int top;
    int capacity;
} CharStack;

CharStack* createStack(int capacity) {
    CharStack* stack = (CharStack*)malloc(sizeof(CharStack));
    stack->capacity = capacity;
    stack->top = -1;
    stack->arr = (char*)malloc(stack->capacity * sizeof(char));
    return stack;
}

void destroyStack(CharStack* stack) {
    free(stack->arr);
    free(stack);
}

bool isEmpty(CharStack* stack) {
    return stack->top == -1;
}

void push(CharStack* stack, char item) {
    // In a real-world scenario, you'd check for stack overflow and resize.
    // For this problem's constraints, we assume capacity is sufficient.
    stack->arr[++stack->top] = item;
}

char pop(CharStack* stack) {
    if (isEmpty(stack)) {
        return '\0'; // Or handle error appropriately, e.g., return a sentinel value
    }
    return stack->arr[stack->top--];
}

bool isBalanced(const char* s) {
    int n = strlen(s);
    if (n == 0) {
        return true;
    }

    CharStack* stack = createStack(n); // Max possible stack size is n

    for (int i = 0; i < n; i++) {
        char current_char = s[i];

        if (current_char == '(' || current_char == '{' || current_char == '[') {
            push(stack, current_char);
        } else if (current_char == ')' || current_char == '}' || current_char == ']') {
            if (isEmpty(stack)) {
                destroyStack(stack);
                return false;
            }
            char top_char = pop(stack);
            if ((current_char == ')' && top_char != '(') ||
                (current_char == '}' && top_char != '{') ||
                (current_char == ']' && top_char != '[')) {
                destroyStack(stack);
                return false;
            }
        }
    }

    bool result = isEmpty(stack);
    destroyStack(stack);
    return result;
}

int main() {
    char s[10005]; // Max string length + 1 for null terminator
    if (fgets(s, sizeof(s), stdin) != NULL) {
        // Remove trailing newline character if present
        s[strcspn(s, "\n")] = 0;
        if (isBalanced(s)) {
            printf("true\n");
        } else {
            printf("false\n");
        }
    }
    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <string>
#include <stack>
#include <map>

bool isBalanced(const std::string& s) {
    std::stack<char> st;
    std::map<char, char> matching_bracket = {
        {')', '('},
        {'}', '{'},
        {']', '['}
    };

    for (char c : s) {
        if (c == '(' || c == '{' || c == '[') {
            st.push(c);
        } else if (c == ')' || c == '}' || c == ']') {
            if (st.empty() || st.top() != matching_bracket[c]) {
                return false;
            }
            st.pop();
        }
    }

    return st.empty();
}

int main() {
    std::string s;
    std::getline(std::cin, s);
    if (isBalanced(s)) {
        std::cout << "true" << std::endl;
    } else {
        std::cout << "false" << std::endl;
    }
    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;
import java.util.Stack;
import java.util.HashMap;

public class Solution {

    public static boolean isBalanced(String s) {
        Stack<Character> stack = new Stack<>();
        HashMap<Character, Character> matchingBrackets = new HashMap<>();
        matchingBrackets.put(')', '(');
        matchingBrackets.put('}', '{');
        matchingBrackets.put(']', '[');

        for (char c : s.toCharArray()) {
            if (c == '(' || c == '{' || c == '[') {
                stack.push(c);
            } else if (c == ')' || c == '}' || c == ']') {
                if (stack.isEmpty() || stack.pop() != matchingBrackets.get(c)) {
                    return false;
                }
            }
        }

        return stack.isEmpty();
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        String s = scanner.nextLine();
        if (isBalanced(s)) {
            System.out.println("true");
        } else {
            System.out.println("false");
        }
        scanner.close();
    }
}
```

## Python Solution
```python
import sys

def is_balanced(s: str) -> bool:
    stack = []
    matching_bracket = {
        ')': '(',
        '}': '{',
        ']': '['
    }

    for char in s:
        if char in '([{':
            stack.append(char)
        elif char in ')]}':
            if not stack or stack.pop() != matching_bracket[char]:
                return False
    
    return not stack

def main():
    s = sys.stdin.readline().strip()
    if is_balanced(s):
        print("true")
    else:
        print("false")

if __name__ == '__main__':
    main()
```

## JavaScript Solution
```javascript
const readline = require('readline');

const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});

function isBalanced(s) {
    const stack = [];
    const matchingBrackets = {
        ')': '(',
        '}': '{',
        ']': '['
    };

    for (const char of s) {
        if (char === '(' || char === '{' || char === '[') {
            stack.push(char);
        } else if (char === ')' || char === '}' || char === ']') {
            if (stack.length === 0 || stack.pop() !== matchingBrackets[char]) {
                return false;
            }
        }
    }

    return stack.length === 0;
}

rl.on('line', (line) => {
    if (isBalanced(line.trim())) {
        console.log("true");
    } else {
        console.log("false");
    }
    rl.close();
});
```
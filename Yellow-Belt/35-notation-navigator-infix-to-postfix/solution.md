# Solutions for Notation Navigator: Infix to Postfix

### Approach
The conversion from infix to postfix notation can be efficiently achieved using a stack, following a variant of the Shunting-yard algorithm. The core idea is to process the infix expression character by character and build the postfix expression, using a stack to temporarily store operators and parentheses.

Here's the detailed approach:
1.  Initialize an empty string or list to store the `postfix_expression`.
2.  Initialize an empty `operator_stack`.
3.  Define a helper function `get_precedence(operator)` that returns an integer indicating the precedence level of the operator. For example, `^` might be 3, `*`/`/` 2, and `+`/`-` 1. Parentheses have a special handling and usually no explicit precedence value in this context.
4.  Define a helper function `is_operand(char)` that checks if a character is an operand (a letter or a digit).
5.  Iterate through each character `ch` in the `infix_expression`:
    *   If `ch` is an **operand**, append it directly to the `postfix_expression`.
    *   If `ch` is an **opening parenthesis `(`**, push it onto the `operator_stack`.
    *   If `ch` is a **closing parenthesis `)`**:
        *   Pop operators from the `operator_stack` and append them to the `postfix_expression` until an opening parenthesis `(` is encountered.
        *   Pop and discard the opening parenthesis `(` from the stack (it should not be part of the postfix expression).
    *   If `ch` is an **operator** (`+`, `-`, `*`, `/`, `^`):
        *   While the `operator_stack` is not empty, and the top of the stack is an operator (not an opening parenthesis), AND (the top operator has higher precedence than `ch` OR (the top operator has the same precedence as `ch` AND `ch` is left-associative)):
            *   Pop the operator from the `operator_stack` and append it to the `postfix_expression`.
        *   Push `ch` onto the `operator_stack`.
6.  After iterating through the entire `infix_expression`, there might be remaining operators in the `operator_stack`. Pop all remaining operators from the `operator_stack` and append them to the `postfix_expression`.
7.  The final `postfix_expression` is the result.

**Time Complexity:** The algorithm processes each character of the input string at most a constant number of times (it's pushed onto the stack, popped from the stack, and appended to the result). Therefore, the time complexity is O(N), where N is the length of the infix expression.

**Space Complexity:** In the worst-case scenario (e.g., a fully parenthesized expression like `((A+B)*C)` or a long sequence of operators like `A+B+C+D`), the `operator_stack` might need to store up to N/2 operators and parentheses. Thus, the space complexity is O(N).

## C Solution
```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <ctype.h>

// Simple Stack implementation for characters
#define MAX_STACK_SIZE 101
char operatorStack[MAX_STACK_SIZE];
int stackTop = -1;

void push(char c) {
    if (stackTop < MAX_STACK_SIZE - 1) {
        operatorStack[++stackTop] = c;
    }
}

char pop() {
    if (stackTop != -1) {
        return operatorStack[stackTop--];
    }
    return '\0'; // Indicates stack underflow or empty
}

char peek() {
    if (stackTop != -1) {
        return operatorStack[stackTop];
    }
    return '\0'; // Indicates stack empty
}

int isEmpty() {
    return stackTop == -1;
}

// Function to check if a character is an operand (letter or digit)
int isOperand(char c) {
    return isalnum(c); // isalnum checks for alphabetic or numeric
}

// Function to check if a character is an operator
int isOperator(char c) {
    return (c == '+' || c == '-' || c == '*' || c == '/' || c == '^');
}

// Function to get the precedence of an operator
int getPrecedence(char op) {
    switch (op) {
        case '+':
        case '-':
            return 1;
        case '*':
        case '/':
            return 2;
        case '^':
            return 3;
        default:
            return 0; // For '(' or other non-operators/invalid chars
    }
}

// Function to check associativity of an operator
// Returns 1 for left-associative, 0 for right-associative
int isLeftAssociative(char op) {
    return (op == '+' || op == '-' || op == '*' || op == '/');
}

// Main function to convert infix to postfix
char* infixToPostfix(const char* infix) {
    int len = strlen(infix);
    char* postfix = (char*)malloc(sizeof(char) * (len + 1));
    if (postfix == NULL) {
        perror("Failed to allocate memory for postfix expression");
        exit(EXIT_FAILURE);
    }
    int j = 0; // Index for postfix expression
    
    // Reset stack for each conversion
    stackTop = -1; 

    for (int i = 0; i < len; i++) {
        char currentChar = infix[i];

        if (isOperand(currentChar)) {
            postfix[j++] = currentChar;
        } else if (currentChar == '(') {
            push(currentChar);
        } else if (currentChar == ')') {
            while (!isEmpty() && peek() != '(') {
                postfix[j++] = pop();
            }
            if (!isEmpty() && peek() == '(') { // Discard '('
                pop();
            } else {
                // Mismatched parentheses, handle error or assume valid input
                // For this problem, we assume valid input
            }
        } else if (isOperator(currentChar)) {
            while (!isEmpty() && peek() != '(' && 
                   (getPrecedence(peek()) > getPrecedence(currentChar) || 
                    (getPrecedence(peek()) == getPrecedence(currentChar) && isLeftAssociative(currentChar)))) {
                postfix[j++] = pop();
            }
            push(currentChar);
        }
    }

    // Pop any remaining operators from the stack
    while (!isEmpty()) {
        postfix[j++] = pop();
    }
    postfix[j] = '\0'; // Null-terminate the postfix string

    return postfix;
}

int main() {
    char infixExpr[101];
    if (scanf("%s", infixExpr) != 1) {
        fprintf(stderr, "Failed to read input.\n");
        return 1;
    }

    char* postfixExpr = infixToPostfix(infixExpr);
    printf("%s\n", postfixExpr);
    
    free(postfixExpr); // Free dynamically allocated memory
    
    return 0;
}

```

## C++ Solution
```cpp
#include <iostream>
#include <string>
#include <stack>
#include <cctype> // For isalnum

// Function to check if a character is an operand (letter or digit)
bool isOperand(char c) {
    return isalnum(c);
}

// Function to get the precedence of an operator
int getPrecedence(char op) {
    switch (op) {
        case '+':
        case '-':
            return 1;
        case '*':
        case '/':
            return 2;
        case '^':
            return 3;
        default:
            return 0; // For '(' or other non-operators/invalid chars
    }
}

// Function to check associativity of an operator
// Returns true for left-associative, false for right-associative
bool isLeftAssociative(char op) {
    return (op == '+' || op == '-' || op == '*' || op == '/');
}

// Main function to convert infix to postfix
std::string infixToPostfix(const std::string& infix) {
    std::string postfix = "";
    std::stack<char> operatorStack;

    for (char currentChar : infix) {
        if (isOperand(currentChar)) {
            postfix += currentChar;
        } else if (currentChar == '(') {
            operatorStack.push(currentChar);
        } else if (currentChar == ')') {
            while (!operatorStack.empty() && operatorStack.top() != '(') {
                postfix += operatorStack.top();
                operatorStack.pop();
            }
            if (!operatorStack.empty() && operatorStack.top() == '(') {
                operatorStack.pop(); // Discard '('
            }
            // For invalid input (mismatched parentheses), this might leave '(' on stack
            // or try to pop from empty stack. Assuming valid infix for this problem.
        } else { // It's an operator
            while (!operatorStack.empty() && operatorStack.top() != '(' &&
                   (getPrecedence(operatorStack.top()) > getPrecedence(currentChar) ||
                    (getPrecedence(operatorStack.top()) == getPrecedence(currentChar) && isLeftAssociative(currentChar)))) {
                postfix += operatorStack.top();
                operatorStack.pop();
            }
            operatorStack.push(currentChar);
        }
    }

    // Pop any remaining operators from the stack
    while (!operatorStack.empty()) {
        postfix += operatorStack.top();
        operatorStack.pop();
    }

    return postfix;
}

int main() {
    std::string infixExpr;
    std::cin >> infixExpr;
    
    std::string postfixExpr = infixToPostfix(infixExpr);
    std::cout << postfixExpr << std::endl;
    
    return 0;
}

```

## Java Solution
```java
import java.util.Scanner;
import java.util.Stack;

public class Solution {

    // Function to check if a character is an operand (letter or digit)
    private static boolean isOperand(char c) {
        return Character.isLetterOrDigit(c);
    }

    // Function to get the precedence of an operator
    private static int getPrecedence(char op) {
        switch (op) {
            case '+':
            case '-':
                return 1;
            case '*':
            case '/':
                return 2;
            case '^':
                return 3;
            default:
                return 0; // For '(' or other non-operators/invalid chars
        }
    }

    // Function to check associativity of an operator
    // Returns true for left-associative, false for right-associative
    private static boolean isLeftAssociative(char op) {
        return (op == '+' || op == '-' || op == '*' || op == '/');
    }

    // Main function to convert infix to postfix
    public static String infixToPostfix(String infix) {
        StringBuilder postfix = new StringBuilder();
        Stack<Character> operatorStack = new Stack<>();

        for (int i = 0; i < infix.length(); i++) {
            char currentChar = infix.charAt(i);

            if (isOperand(currentChar)) {
                postfix.append(currentChar);
            } else if (currentChar == '(') {
                operatorStack.push(currentChar);
            } else if (currentChar == ')') {
                while (!operatorStack.isEmpty() && operatorStack.peek() != '(') {
                    postfix.append(operatorStack.pop());
                }
                if (!operatorStack.isEmpty() && operatorStack.peek() == '(') {
                    operatorStack.pop(); // Discard '('
                }
            } else { // It's an operator
                while (!operatorStack.isEmpty() && operatorStack.peek() != '(' &&
                       (getPrecedence(operatorStack.peek()) > getPrecedence(currentChar) ||
                        (getPrecedence(operatorStack.peek()) == getPrecedence(currentChar) && isLeftAssociative(currentChar)))) {
                    postfix.append(operatorStack.pop());
                }
                operatorStack.push(currentChar);
            }
        }

        // Pop any remaining operators from the stack
        while (!operatorStack.isEmpty()) {
            postfix.append(operatorStack.pop());
        }

        return postfix.toString();
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        String infixExpr = scanner.next(); // Reads a single token (no spaces)
        scanner.close();
        
        String postfixExpr = infixToPostfix(infixExpr);
        System.out.println(postfixExpr);
    }
}

```

## Python Solution
```python
import sys

def is_operand(char):
    return '0' <= char <= '9' or 'A' <= char <= 'Z' or 'a' <= char <= 'z'

def get_precedence(op):
    if op == '+' or op == '-':
        return 1
    elif op == '*' or op == '/':
        return 2
    elif op == '^':
        return 3
    return 0 # For '(' or other non-operators

def is_left_associative(op):
    return op in {'+', '-', '*', '/'}

def infix_to_postfix(infix_expr):
    postfix_expr = []
    operator_stack = []

    for char in infix_expr:
        if is_operand(char):
            postfix_expr.append(char)
        elif char == '(':
            operator_stack.append(char)
        elif char == ')':
            while operator_stack and operator_stack[-1] != '(':
                postfix_expr.append(operator_stack.pop())
            if operator_stack and operator_stack[-1] == '(':
                operator_stack.pop() # Discard '('
            # else: Mismatched parentheses error, assuming valid input
        elif char in {'+', '-', '*', '/', '^'}: # It's an operator
            while (operator_stack and operator_stack[-1] != '(' and
                   (get_precedence(operator_stack[-1]) > get_precedence(char) or
                    (get_precedence(operator_stack[-1]) == get_precedence(char) and is_left_associative(char)))):
                postfix_expr.append(operator_stack.pop())
            operator_stack.append(char)
    
    # Pop any remaining operators from the stack
    while operator_stack:
        postfix_expr.append(operator_stack.pop())
            
    return "".join(postfix_expr)

def main():
    infix_expr = sys.stdin.readline().strip()
    postfix_expr = infix_to_postfix(infix_expr)
    sys.stdout.write(postfix_expr + "\n")

if __name__ == '__main__':
    main()

```

## JavaScript Solution
```javascript
function isOperand(char) {
    return (char >= '0' && char <= '9') || (char >= 'A' && char <= 'Z') || (char >= 'a' && char <= 'z');
}

function getPrecedence(op) {
    switch (op) {
        case '+':
        case '-':
            return 1;
        case '*':
        case '/':
            return 2;
        case '^':
            return 3;
        default:
            return 0; // For '(' or other non-operators
    }
}

function isLeftAssociative(op) {
    return ['+', '-', '*', '/'].includes(op);
}

function infixToPostfix(infixExpr) {
    let postfixExpr = [];
    let operatorStack = [];

    for (let i = 0; i < infixExpr.length; i++) {
        let currentChar = infixExpr[i];

        if (isOperand(currentChar)) {
            postfixExpr.push(currentChar);
        } else if (currentChar === '(') {
            operatorStack.push(currentChar);
        } else if (currentChar === ')') {
            while (operatorStack.length > 0 && operatorStack[operatorStack.length - 1] !== '(') {
                postfixExpr.push(operatorStack.pop());
            }
            if (operatorStack.length > 0 && operatorStack[operatorStack.length - 1] === '(') {
                operatorStack.pop(); // Discard '('
            }
            // else: Mismatched parentheses error, assuming valid input
        } else { // It's an operator
            while (operatorStack.length > 0 && operatorStack[operatorStack.length - 1] !== '(' &&
                   (getPrecedence(operatorStack[operatorStack.length - 1]) > getPrecedence(currentChar) ||
                    (getPrecedence(operatorStack[operatorStack.length - 1]) === getPrecedence(currentChar) && isLeftAssociative(currentChar)))) {
                postfixExpr.push(operatorStack.pop());
            }
            operatorStack.push(currentChar);
        }
    }

    // Pop any remaining operators from the stack
    while (operatorStack.length > 0) {
        postfixExpr.push(operatorStack.pop());
    }

    return postfixExpr.join('');
}

// Node.js specific input/output handling
const readline = require('readline');

const rl = readline.createInterface({
  input: process.stdin,
  output: process.stdout
});

rl.on('line', (line) => {
  const infixExpr = line.trim();
  const postfixExpr = infixToPostfix(infixExpr);
  console.log(postfixExpr);
  rl.close();
});

```
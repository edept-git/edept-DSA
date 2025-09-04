### Description
In mathematics and computer science, expressions can be written in different notations. The most common is **infix notation**, where operators are placed between their operands (e.g., `A + B`). However, for easier parsing and evaluation by computers, **postfix notation** (also known as Reverse Polish Notation or RPN) is often preferred, where operators follow their operands (e.g., `AB+`).

Your task is to convert a given infix expression into its equivalent postfix expression. This involves understanding operator precedence (which operations are performed first) and associativity (how operators of the same precedence are grouped).

### Constraints
*   The input string `infix_expr` will contain only:
    *   Uppercase English letters (`A-Z`) and digits (`0-9`) as operands.
    *   Operators: `+`, `-`, `*`, `/`, `^`.
    *   Parentheses: `(`, `)`.
*   The input string will be a valid infix expression.
*   There will be no spaces in the input string.
*   The length of the `infix_expr` will be between 1 and 100 characters, inclusive.
*   Operator Precedence (from highest to lowest):
    1.  `^` (Exponentiation)
    2.  `*`, `/` (Multiplication, Division)
    3.  `+`, `-` (Addition, Subtraction)
*   Associativity:
    *   `^` is right-associative (e.g., `A^B^C` is `A^(B^C)`).
    *   `+`, `-`, `*`, `/` are left-associative.

### Example
**Input:** `A+B*C`
**Output:** `ABC*+`

### Concepts Covered
*   Stacks
*   Operator Precedence
*   Associativity Rules
*   String Manipulation
*   Algorithm Design
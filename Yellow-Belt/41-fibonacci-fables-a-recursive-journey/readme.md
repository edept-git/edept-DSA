### Description

Welcome, aspiring coder! In this problem, you'll explore the classic Fibonacci sequence using the power of recursion. The Fibonacci sequence is a series of numbers where each number is the sum of the two preceding ones, usually starting with 0 and 1. 

Your task is to write a function that calculates the `n`-th Fibonacci number. The sequence typically starts as: 0, 1, 1, 2, 3, 5, 8, 13, ...

For example:
- `fib(0)` should return 0
- `fib(1)` should return 1
- `fib(2)` should return `fib(1) + fib(0) = 1 + 0 = 1`
- `fib(3)` should return `fib(2) + fib(1) = 1 + 1 = 2`

You must implement this using a recursive approach.

### Constraints

*   `n` is a non-negative integer.
*   `0 <= n <= 20` (The value of `n` is kept small to allow for the direct recursive solution without performance issues for a Yellow Belt level.)

### Example

**Input:**

5


**Output:**

5


**Explanation:**
The Fibonacci sequence up to the 5th term (0-indexed) is: 0, 1, 1, 2, 3, 5. The 5th term is 5.

### Concepts Covered

*   **Recursion**: A function calling itself to solve smaller subproblems.
*   **Base Cases**: Conditions that stop the recursion and provide a direct result.
*   **Recursive Step**: The part of the function that breaks down the problem and calls itself with modified arguments.
### Description

Welcome to your first dive into the world of recursion! Your task is to calculate the factorial of a given non-negative integer `n`. The factorial of a non-negative integer `n`, denoted by `n!`, is the product of all positive integers less than or equal to `n`. For example, `5! = 5 × 4 × 3 × 2 × 1 = 120`. A special case is `0!`, which is defined as `1`.

You must implement the factorial calculation **recursively**. This means your function should call itself to solve smaller sub-problems until it reaches a simple base case.

### Constraints

*   `0 <= n <= 12`
*   The input `n` will always be a non-negative integer.
*   The result will fit within a standard 64-bit integer type (like `long long` in C++ or `long` in Java).

### Example

**Input:**

5


**Output:**

120


### Concepts Covered

*   **Recursion:** A function calling itself.
*   **Base Case:** The condition that stops the recursion.
*   **Recursive Step:** The part of the function that makes a recursive call with a modified input, moving towards the base case.
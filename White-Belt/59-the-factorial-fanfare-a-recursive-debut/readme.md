### Description
The factorial of a non-negative integer `n`, denoted as `n!`, is the product of all positive integers less than or equal to `n`. For example, `5! = 5 * 4 * 3 * 2 * 1 = 120`. An important special case is `0!`, which is defined as `1`.

Your task is to write a function that calculates the factorial of a given non-negative integer `n` using recursion. This problem is designed to introduce you to the fundamental concepts of recursion: defining a base case and a recursive step.

### Constraints
*   `0 <= n <= 12` (The result for `n=13` and above might exceed the capacity of a standard 32-bit integer, and for larger values, the call stack might overflow, depending on the language and environment.)

### Example
**Input:**

5

**Output:**

120

**Explanation:**
`factorial(5)` works as follows:
- `5 * factorial(4)`
- `5 * (4 * factorial(3))`
- `5 * (4 * (3 * factorial(2)))`
- `5 * (4 * (3 * (2 * factorial(1))))`
- `5 * (4 * (3 * (2 * (1 * factorial(0)))))`
- `5 * (4 * (3 * (2 * (1 * 1))))`  (Base case: `factorial(0) = 1`)
- `5 * (4 * (3 * (2 * 1)))`
- `5 * (4 * (3 * 2))`
- `5 * (4 * 6)`
- `5 * 24`
- `120`

### Concepts Covered
*   **Recursion**: A function calling itself to solve smaller subproblems.
*   **Base Case**: The condition that stops the recursion. Without it, the function would call itself indefinitely. For factorial, `0! = 1` is the base case.
*   **Recursive Step**: The part of the function that calls itself with a modified input, moving closer to the base case. For `n > 0`, `n! = n * (n-1)!` is the recursive step.
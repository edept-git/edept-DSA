### Description
The Fibonacci sequence is a series of numbers where each number is the sum of the two preceding ones, usually starting with 0 and 1. The sequence begins: 0, 1, 1, 2, 3, 5, 8, 13, 21, and so on.

Your task is to write a recursive function that calculates the Nth Fibonacci number. Given a non-negative integer `n`, return the `n`-th Fibonacci number.

For example:
- `fib(0) = 0`
- `fib(1) = 1`
- `fib(2) = fib(1) + fib(0) = 1 + 0 = 1`
- `fib(3) = fib(2) + fib(1) = 1 + 1 = 2`

### Constraints
- `0 <= n <= 20` (The recursion depth and computation time grow very quickly for larger `n` with a naive recursive approach)

### Example
**Input:**
`n = 5`

**Output:**
`5`

**Explanation:**
The Fibonacci sequence starts `0, 1, 1, 2, 3, 5, ...`
The 0th term is 0.
The 1st term is 1.
The 2nd term is 1.
The 3rd term is 2.
The 4th term is 3.
The 5th term is 5.

### Concepts Covered
- Recursion
- Base Cases
- Recursive Step
- Function Call Stack
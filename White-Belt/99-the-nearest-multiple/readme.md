### Description
You are given two positive integers, `N` and `K`. Your task is to find the smallest integer `X` such that `X` is greater than or equal to `N` and `X` is perfectly divisible by `K`.

### Constraints
*   `1 <= N <= 1000`
*   `1 <= K <= 100`

### Example
Input:
N = 10
K = 3
Output:
12

Explanation:
We need to find a number >= 10 that is divisible by 3.
10 % 3 = 1 (not divisible)
11 % 3 = 2 (not divisible)
12 % 3 = 0 (divisible)
Since 12 is the smallest number >= 10 that is divisible by 3, the answer is 12.

### Concepts Covered
*   Modulo Operator (`%`)
*   Integer Division
*   Basic Arithmetic Operations
*   Conditional Logic
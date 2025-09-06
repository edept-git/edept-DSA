### Description
Given an array `arr` of `n` integers, your task is to find the *first* equilibrium point in the array. An equilibrium point is an index `i` such that the sum of elements strictly to its left (indices `0` to `i-1`) is equal to the sum of elements strictly to its right (indices `i+1` to `n-1`). If no such index exists, return -1.

### Constraints
*   `1 <= n <= 1000`
*   `-100 <= arr[i] <= 100`

### Example
**Input:**

7
-7 1 5 2 -4 3 0

**Output:**

3

**Explanation:**
For the array `[-7, 1, 5, 2, -4, 3, 0]`:
*   At index `3` (value `2`):
    *   Sum of elements to the left (`-7`, `1`, `5`) = `-7 + 1 + 5 = -1`
    *   Sum of elements to the right (`-4`, `3`, `0`) = `-4 + 3 + 0 = -1`
    Since the left sum equals the right sum, `3` is an equilibrium point. It is the first such point.

### Concepts Covered
*   Array Traversal
*   Prefix Sums (implicit calculation)
*   Summation
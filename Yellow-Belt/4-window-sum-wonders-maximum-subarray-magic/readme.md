### Description
You are given an array of integers `arr` and an integer `k`. Your task is to find the maximum sum of a subarray of `arr` that has a length exactly `k`. This means you need to consider all possible contiguous subarrays of size `k` and determine which one has the largest sum.

### Constraints
*   `1 <= arr.length <= 10^5`
*   `1 <= k <= arr.length`
*   `0 <= arr[i] <= 1000` (Elements are non-negative to keep it simple for an intro problem)
*   The sum of any subarray will fit within a standard integer type.

### Example
**Input:**

6
2 1 5 1 3 2
3

**Output:**

9


**Explanation:**
The subarrays of length `k = 3` are:
*   `[2, 1, 5]` sum = 8
*   `[1, 5, 1]` sum = 7
*   `[5, 1, 3]` sum = 9
*   `[1, 3, 2]` sum = 6
The maximum sum is 9.

### Concepts Covered
*   Arrays
*   Fixed-size Sliding Window
*   Iterative Summation
*   Max Value Tracking
### Description

You're given an array of integers, which can contain both positive and negative numbers. Your task is to find the contiguous subarray (a sequence of elements that are adjacent in the array) that has the largest possible sum. You need to return this maximum sum. If all numbers are negative, you should return the largest single negative number.

### Constraints

*   `1 <= nums.length <= 10^5`
*   `-10^4 <= nums[i] <= 10^4`

### Example

**Input:**
`[-2, 1, -3, 4, -1, 2, 1, -5, 4]`

**Output:**
`6`

**Explanation:**
The contiguous subarray `[4, -1, 2, 1]` has the largest sum = `4 + (-1) + 2 + 1 = 6`.

### Concepts Covered

*   Kadane's Algorithm
*   Dynamic Programming (implicitly)
*   Array Traversal
*   Handling negative numbers in sums

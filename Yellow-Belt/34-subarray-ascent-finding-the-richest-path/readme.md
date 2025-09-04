### Description
You are given an integer array `nums`. Your task is to find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.

A contiguous subarray is a sequence of elements that are adjacent in the original array.

### Constraints
- `1 <= nums.length <= 10^5`
- `-10^4 <= nums[i] <= 10^4`

### Example
Input:

9
-2 1 -3 4 -1 2 1 -5 4

Output:

6

Explanation: The subarray `[4, -1, 2, 1]` has the largest sum = 6.

### Concepts Covered
- Kadane's Algorithm
- Dynamic Programming (implicitly greedy approach)
- Iteration
- Tracking maximum values

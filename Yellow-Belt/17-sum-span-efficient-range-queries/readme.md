### Description
You are given an array of integers `nums` and a list of `Q` queries. Each query consists of two indices, `start` and `end` (inclusive), representing a range within the `nums` array. Your task is to calculate the sum of all elements within each specified range `[start, end]` for every query. You need to do this efficiently, especially if there are many queries.

### Constraints
*   `1 <= N <= 1000` (length of `nums` array)
*   `-100 <= nums[i] <= 100`
*   `1 <= Q <= 100` (number of queries)
*   `0 <= start <= end < N` (query indices)

### Example
#### Input:

5
1 2 3 4 5
2
0 2
1 3


#### Output:

6
9


#### Explanation:
Given `nums = [1, 2, 3, 4, 5]`
Query 1: `[0, 2]` means sum of `nums[0] + nums[1] + nums[2] = 1 + 2 + 3 = 6`
Query 2: `[1, 3]` means sum of `nums[1] + nums[2] + nums[3] = 2 + 3 + 4 = 9`

### Concepts Covered
*   Arrays
*   Prefix Sums (also known as Cumulative Sums)
*   Time Complexity Optimization
*   Basic I/O
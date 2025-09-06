### Description

YouYou are given an array of integers and a list of queries. Each query consists of two indices, `L` and `R`, representing a range `[L, R]` (inclusive) within the array. Your task is to find the sum of all elements in the array for each given range query.

This problem tests your ability to efficiently process multiple range sum queries on a static array. A naive approach of summing elements for each query would be too slow for large inputs.

### Constraints

*   `1 <= N <= 10^5` (where `N` is the number of elements in the array)
*   `-1000 <= arr[i] <= 1000` (value of each element in the array)
*   `1 <= Q <= 10^5` (where `Q` is the number of queries)
*   `0 <= L <= R < N` (indices for each query)

### Example

**Input:**

5
1 2 3 4 5
3
0 2
1 3
2 4


**Output:**

6
9
12


**Explanation:**

Given `arr = [1, 2, 3, 4, 5]` and queries:

1.  Query `[0, 2]`: Sum of `arr[0]` to `arr[2]` is `1 + 2 + 3 = 6`.
2.  Query `[1, 3]`: Sum of `arr[1]` to `arr[3]` is `2 + 3 + 4 = 9`.
3.  Query `[2, 4]`: Sum of `arr[2]` to `arr[4]` is `3 + 4 + 5 = 12`.

### Concepts Covered

*   Prefix Sums (also known as Cumulative Sums)
*   Array Manipulation
*   Range Queries
*   Time and Space Complexity Analysis

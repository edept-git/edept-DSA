### Description
You are given an array of integers `nums` and a `target` integer. Your task is to find the first occurrence of the `target` in the `nums` array. If the `target` is found, return its index. If the `target` is not present in the array, return `-1`.

This is a classic problem that introduces the concept of iterating through a list of items to find a specific one, also known as Linear Search.

### Constraints
*   `1 <= n <= 1000`, where `n` is the length of `nums`.
*   `-1000 <= nums[i] <= 1000`
*   `-1000 <= target <= 1000`

### Example
#### Example 1:
Input:

5
2
5
1
9
7
9

Output:

3

Explanation: The array is `[2, 5, 1, 9, 7]`. The target is `9`. `9` is found at index `3` (0-indexed).

#### Example 2:
Input:

5
2
5
1
9
7
3

Output:

-1

Explanation: The array is `[2, 5, 1, 9, 7]`. The target is `3`. `3` is not found in the array, so `-1` is returned.

### Concepts Covered
*   Arrays
*   Loops (for/while)
*   Conditional Statements (if)
*   Basic Iteration
### Description
You are given a sorted array of integers `nums` in ascending order and a target integer. Your task is to find the index of the target in the array. If the target is not found, return -1.

### Constraints
*   `1 <= nums.length <= 10^5`
*   `-10^9 <= nums[i] <= 10^9`
*   All values in `nums` are unique and sorted in ascending order.
*   `-10^9 <= target <= 10^9`

### Example
**Example 1:**
*   **Input:**
    
    6
    1 3 5 7 9 11
    7
    
*   **Output:**
    
    3
    
*   **Explanation:** The target `7` is found at index `3` (0-indexed).

**Example 2:**
*   **Input:**
    
    4
    2 4 6 8
    5
    
*   **Output:**
    
    -1
    
*   **Explanation:** The target `5` is not present in the array.

### Concepts Covered
*   Binary Search (Iterative)
*   Divide and Conquer
*   Logarithmic Time Complexity
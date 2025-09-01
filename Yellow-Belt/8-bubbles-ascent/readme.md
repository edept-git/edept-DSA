### Description
You've been given an array of integers. Your task is to sort this array in ascending order using the Bubble Sort algorithm. Bubble sort works by repeatedly stepping through the list, comparing adjacent elements and swapping them if they are in the wrong order. The pass through the list is repeated until no swaps are needed, which indicates that the list is sorted.

### Constraints
*   The number of elements `n` in the array will be between 1 and 1000.
*   Each element `arr[i]` will be an integer between -10000 and 10000.

### Example
#### Example 1:
Input: `[5, 1, 4, 2, 8]`
Output: `[1, 2, 4, 5, 8]`

**Explanation:**
1.  **(5, 1, 4, 2, 8)** -> (1, 5, 4, 2, 8) - Swap 5 and 1
2.  (1, 5, 4, 2, 8) -> (1, 4, 5, 2, 8) - Swap 5 and 4
3.  (1, 4, 5, 2, 8) -> (1, 4, 2, 5, 8) - Swap 5 and 2
4.  (1, 4, 2, 5, 8) -> (1, 4, 2, 5, 8) - 5 and 8 are in order
*After first pass, 8 is at the end.*

5.  (1, 4, 2, 5) -> (1, 2, 4, 5) - Swap 4 and 2
*After second pass, 5 is at the second to last position.*

6.  (1, 2, 4) -> (1, 2, 4) - Already sorted.
*No more swaps needed in the inner loop, array is sorted.*

### Concepts Covered
*   Sorting Algorithms
*   In-place Sorting
*   Nested Loops
*   Basic Array Manipulation
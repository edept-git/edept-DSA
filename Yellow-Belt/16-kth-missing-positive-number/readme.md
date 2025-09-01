### Description
You are given a **strictly increasing** array `arr` of positive integers and an integer `k`.

Your task is to find the `k`-th positive integer that is **missing** from the array. Positive integers start from `1`.

For example, if `arr = [2,3,4,7,11]` and `k = 5`:
The positive integers are `1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, ...`
Numbers present in `arr`: `2, 3, 4, 7, 11`
Missing positive integers in order: `1, 5, 6, 8, 9, 10, 12, ...`
The 1st missing is `1`.
The 2nd missing is `5`.
The 3rd missing is `6`.
The 4th missing is `8`.
The 5th missing is `9`.
So, the output for this example would be `9`.

### Constraints
*   `1 <= arr.length <= 1000`
*   `1 <= arr[i] <= 1000 + k`
*   `1 <= k <= 1000`
*   `arr` is sorted in strictly increasing order.
*   All elements in `arr` are distinct.

### Example
Input:
arr = [2,3,4,7,11], k = 5
Output:
9
Explanation: The missing positive integers are 1, 5, 6, 8, 9, 10, 12, ... The 5th missing positive integer is 9.

### Concepts Covered
*   **Arrays**: Understanding how to store and access collections of data.
*   **Sorted Arrays**: Leveraging the property that elements are in order to optimize solutions.
*   **Iteration**: Traversing through an array to examine each element.
*   **Counting**: Keeping track of how many elements satisfy a certain condition.
*   **Binary Search (Advanced)**: For larger inputs, a more efficient search algorithm can be used to quickly find an element or a position in a sorted array based on a condition. This problem can be optimally solved using binary search by cleverly identifying a monotonic property related to missing numbers.

### Description
You are given an unsorted array of integers. Your task is to sort this array in ascending order using the Insertion Sort algorithm.

Insertion Sort works by taking one element at a time from the unsorted part and inserting it into its correct position within the already sorted part of the array. This process continues until all elements are in their sorted positions.

### Constraints
- `1 <= n <= 1000` (where `n` is the number of elements in the array)
- `-1000 <= arr[i] <= 1000` (where `arr[i]` is an element in the array)
- The input array will contain only integers.

### Example
#### Input:

6
5 2 4 6 1 3

#### Output:

1 2 3 4 5 6

Explanation:
1. Initial array: `[5, 2, 4, 6, 1, 3]`
2. First element `5` is trivially sorted: `[5 | 2, 4, 6, 1, 3]`
3. Take `2`, insert before `5`: `[2, 5 | 4, 6, 1, 3]`
4. Take `4`, insert between `2` and `5`: `[2, 4, 5 | 6, 1, 3]`
5. Take `6`, insert after `5`: `[2, 4, 5, 6 | 1, 3]`
6. Take `1`, insert at the beginning: `[1, 2, 4, 5, 6 | 3]`
7. Take `3`, insert between `2` and `4`: `[1, 2, 3, 4, 5, 6 | ]`
The array is now fully sorted.

### Concepts Covered
- Sorting Algorithms
- In-place Sorting
- Iteration and Looping
- Array Manipulation
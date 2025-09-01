### Description
You are given an array of integers. Your task is to sort this array in ascending order using the Selection Sort algorithm. Selection Sort works by repeatedly finding the minimum element from the unsorted part and putting it at the beginning of the unsorted part.

### Constraints
* `1 <= n <= 1000` (where `n` is the number of elements in the array)
* `-1000 <= arr[i] <= 1000`
* The array may contain duplicate elements.

### Example
**Input:**
`[64, 25, 12, 22, 11]`

**Output:**
`[11, 12, 22, 25, 64]`

**Explanation:**
1. Find the minimum element in `[64, 25, 12, 22, 11]` which is `11`. Swap `11` with `64`. Array becomes `[11, 25, 12, 22, 64]`.
2. Consider the unsorted sub-array `[25, 12, 22, 64]`. Minimum is `12`. Swap `12` with `25`. Array becomes `[11, 12, 25, 22, 64]`.
3. Consider `[25, 22, 64]`. Minimum is `22`. Swap `22` with `25`. Array becomes `[11, 12, 22, 25, 64]`.
4. Consider `[25, 64]`. Minimum is `25`. Swap `25` with `25` (no change). Array becomes `[11, 12, 22, 25, 64]`.
5. The array is now sorted.

### Concepts Covered
* Selection Sort Algorithm
* Array Manipulation
* Iteration and Looping Constructs
* In-place Sorting
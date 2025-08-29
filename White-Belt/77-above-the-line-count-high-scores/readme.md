### Description
Imagine you're tracking scores in a game, and you want to know how many players scored above a certain benchmark. Your task is to implement a function that takes a list of integer scores and a threshold integer. It should return the total count of scores that are strictly greater than the given threshold.

### Constraints
*   `1 <= N <= 100` (where `N` is the number of scores in the input list)
*   `0 <= score[i] <= 1000` (each individual score will be between 0 and 1000)
*   `0 <= threshold <= 1000` (the threshold will also be between 0 and 1000)

### Example
**Input:**
`scores = [10, 20, 5, 30, 15]`
`threshold = 12`

**Output:**
`3`

**Explanation:**
The scores greater than 12 are 20, 30, and 15. There are 3 such scores.

### Concepts Covered
*   Arrays / Lists
*   Basic Iteration (Loops)
*   Conditional Statements
*   Introduction to Time Complexity (O(N) for linear scan)
*   Introduction to Space Complexity (O(1) for constant extra space)
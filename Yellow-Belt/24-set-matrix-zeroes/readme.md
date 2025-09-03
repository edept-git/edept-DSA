### Description
You are given an `m x n` integer matrix. Your task is to modify the matrix *in-place*. If any element in the matrix is `0`, its entire row and its entire column must be set to `0`s. This modification should happen simultaneously, meaning if a `0` at `(r, c)` causes `(r, c')` to become `0`, and then `(r, c')` in turn causes its column to become `0`, this is *not* the intended behavior. Instead, consider all original `0`s, and based on their positions, determine which rows and columns should be zeroed out.

Your solution should aim to be space-efficient, ideally using only constant extra space.

### Constraints
- `m == matrix.length`
- `n == matrix[0].length`
- `1 <= m, n <= 200`
- `-10^9 <= matrix[i][j] <= 10^9`

### Example
**Example 1:**
Input:

[[1,1,1],
 [1,0,1],
 [1,1,1]]

Output:

[[1,0,1],
 [0,0,0],
 [1,0,1]]

**Explanation:** The `0` at `matrix[1][1]` causes row 1 and column 1 to become zeroes.

**Example 2:**
Input:

[[0,1,2,0],
 [3,4,5,2],
 [1,3,1,5]]

Output:

[[0,0,0,0],
 [0,4,5,0],
 [0,3,1,0]]

**Explanation:** The `0` at `matrix[0][0]` causes row 0 and column 0 to become zeroes. The `0` at `matrix[0][3]` causes row 0 and column 3 to become zeroes. Since row 0 already has a zero, it reinforces the result.

### Concepts Covered
- **Matrix Traversal**: Iterating through elements of a 2D array.
- **In-place Modification**: Changing the input data directly without creating a new data structure to store the result.
- **Space Optimization**: Finding ways to solve a problem using minimal additional memory.
- **Conditional Logic**: Using `if` statements to make decisions based on element values.
- **Two-Pass Approach**: Solving the problem by iterating through the data multiple times, each pass performing a specific step.
- **Edge Cases**: Handling scenarios like matrices with only one row/column, or matrices where the first row/column contains a zero.
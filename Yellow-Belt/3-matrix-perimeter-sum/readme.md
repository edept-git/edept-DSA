### Description
You are given a 2D integer array (matrix). Your task is to calculate the sum of all elements that lie on the perimeter of the matrix. The perimeter includes all elements in the first row, last row, first column, and last column. Be careful not to double-count elements that are part of multiple perimeter segments (i.e., the corner elements).

### Constraints
*   `1 <= rows, cols <= 100` (where `rows` is the number of rows and `cols` is the number of columns).
*   `-1000 <= matrix[i][j] <= 1000` (elements can be positive, negative, or zero).

### Example
#### Input:

3 3
1 2 3
4 5 6
7 8 9

#### Output:

40


#### Explanation:
The perimeter elements are:
*   First row: 1, 2, 3
*   Last row: 7, 8, 9
*   First column (excluding corners): 4
*   Last column (excluding corners): 6

Sum = 1 + 2 + 3 + 7 + 8 + 9 + 4 + 6 = 40.

### Concepts Covered
*   2D Arrays / Matrices
*   Iteration / Traversal
*   Conditional Logic
*   Summation
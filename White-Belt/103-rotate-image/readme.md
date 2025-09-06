### Description
You are given an `n x n` 2D matrix, which represents an image. Your task is to rotate the image by 90 degrees clockwise.

You must do this **in-place**, meaning you have to modify the input 2D matrix directly. You should not allocate another 2D matrix to perform the rotation. Think of it like rotating a physical photo frame without replacing the photo inside.

For example, if you have a 3x3 matrix:

1 2 3
4 5 6
7 8 9

After rotating it 90 degrees clockwise, it should become:

7 4 1
8 5 2
9 6 3


### Constraints
- `n == matrix.length == matrix[i].length` (The matrix is always square)
- `1 <= n <= 20` (The size of the matrix will be between 1x1 and 20x20)
- `-1000 <= matrix[i][j] <= 1000` (The values inside the matrix are integers)

### Example
Input: `matrix = [[1,2,3],[4,5,6],[7,8,9]]`
Output: `[[7,4,1],[8,5,2],[9,6,3]]`

Explanation: The input matrix is:

1 2 3
4 5 6
7 8 9

The rotated matrix is:

7 4 1
8 5 2
9 6 3


### Concepts Covered
- **2D Arrays (Matrices)**: Understanding how to work with grid-like data structures.
- **In-place Modification**: Modifying data directly in its original memory location without using extra space.
- **Matrix Transposition**: Swapping elements across the main diagonal (e.g., `matrix[i][j]` becomes `matrix[j][i]`).
- **Array Reversal**: Flipping the order of elements within a 1D array or a row of a 2D array.
- **Nested Loops**: Using loops within loops to iterate through all elements of a 2D array.

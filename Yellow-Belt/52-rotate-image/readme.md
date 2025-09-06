### Description
You are given an `n x n` 2D `matrix` representing an image. You need to rotate the image by 90 degrees clockwise.

You must do this in-place, which means you modify the input 2D matrix directly. Do NOT allocate another 2D matrix to perform the rotation.

For example, if you have:

1 2 3
4 5 6
7 8 9

After rotating 90 degrees clockwise, it becomes:

7 4 1
8 5 2
9 6 3


### Constraints
*   `n == matrix.length == matrix[i].length`
*   `1 <= n <= 20`
*   `-1000 <= matrix[i][j] <= 1000`

### Example
**Input:** `matrix = [[1,2,3],[4,5,6],[7,8,9]]`
**Output:** `[[7,4,1],[8,5,2],[9,6,3]]`

**Explanation:**
The original matrix:

1 2 3
4 5 6
7 8 9

After rotating 90 degrees clockwise:

7 4 1
8 5 2
9 6 3


### Concepts Covered
*   **2D Arrays (Matrices)**: Understanding how to store and access data in a grid-like structure.
*   **In-place Operations**: Modifying the existing data structure directly without creating a new one, which is important for memory efficiency.
*   **Nested Loops**: Using loops within loops to iterate through all elements of a 2D array.
*   **Swapping Elements**: Exchanging the values of two variables, a fundamental operation in many algorithms.
*   **Algorithmic Thinking**: Breaking down a complex transformation (like rotation) into simpler, manageable steps.

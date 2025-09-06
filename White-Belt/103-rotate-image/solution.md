# Solutions for Rotate Image

### Approach
### Optimal Approach: Transpose and Reverse
The most efficient way to rotate an `n x n` matrix 90 degrees clockwise in-place is to perform two simple transformations:

1.  **Transpose the matrix**: This means swapping elements `matrix[i][j]` with `matrix[j][i]` for all `i` and `j` where `j > i`. Think of it as flipping the matrix over its main diagonal (from top-left to bottom-right).
    For example:
    Original:
    
    1 2 3
    4 5 6
    7 8 9
    
    After Transpose:
    
    1 4 7
    2 5 8
    3 6 9
    

2.  **Reverse each row**: After transposing, each row of the matrix needs to be reversed.
    Continuing the example:
    Transposed:
    
    1 4 7
    2 5 8
    3 6 9
    
    Reverse Row 0: `[1, 4, 7]` becomes `[7, 4, 1]`
    Reverse Row 1: `[2, 5, 8]` becomes `[8, 5, 2]`
    Reverse Row 2: `[3, 6, 9]` becomes `[9, 6, 3]`
    Final Rotated Matrix:
    
    7 4 1
    8 5 2
    9 6 3
    

This sequence of operations achieves a 90-degree clockwise rotation in-place.

**Time Complexity**:
- Transposing the matrix involves iterating through roughly half of its elements (since we only swap `j > i`). This takes O(n^2) time, where `n` is the number of rows/columns.
- Reversing each of the `n` rows, where each row has `n` elements, also takes O(n^2) time.
Therefore, the total time complexity is **O(n^2)**.

**Space Complexity**:
- Since all modifications are done directly within the input matrix without using any auxiliary data structures proportional to the input size, the space complexity is **O(1)**.


## C Solution
```c
#include <stdio.h>
#include <stdlib.h>

// Function to rotate the matrix in-place
void rotate(int** matrix, int matrixSize, int* matrixColSize) {
    // 1. Transpose the matrix
    for (int i = 0; i < matrixSize; i++) {
        for (int j = i + 1; j < matrixSize; j++) {
            // Swap matrix[i][j] with matrix[j][i]
            int temp = matrix[i][j];
            matrix[i][j] = matrix[j][i];
            matrix[j][i] = temp;
        }
    }

    // 2. Reverse each row
    for (int i = 0; i < matrixSize; i++) {
        int left = 0;
        int right = matrixSize - 1;
        while (left < right) {
            // Swap matrix[i][left] with matrix[i][right]
            int temp = matrix[i][left];
            matrix[i][left] = matrix[i][right];
            matrix[i][right] = temp;
            left++;
            right--;
        }
    }
}

int main() {
    int n;
    scanf("%d", &n);

    // Dynamically allocate matrix
    int** matrix = (int**)malloc(n * sizeof(int*));
    // For LeetCode compatibility, matrixColSize array is usually passed, 
    // but for square matrices all elements are 'n'.
    int* colSizes = (int*)malloc(n * sizeof(int)); 

    for (int i = 0; i < n; i++) {
        matrix[i] = (int*)malloc(n * sizeof(int));
        colSizes[i] = n; // Each row has n columns
        for (int j = 0; j < n; j++) {
            scanf("%d", &matrix[i][j]);
        }
    }

    rotate(matrix, n, colSizes); // Pass n as matrixSize and colSizes (though not strictly needed for square)

    // Print the rotated matrix
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            printf("%d%s", matrix[i][j], (j == n - 1) ? "" : " ");
        }
        printf("\n");
    }

    // Free dynamically allocated memory
    for (int i = 0; i < n; i++) {
        free(matrix[i]);
    }
    free(matrix);
    free(colSizes);

    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <vector>
#include <algorithm> // For std::reverse

// Function to rotate the matrix in-place
void rotate(std::vector<std::vector<int>>& matrix) {
    int n = matrix.size();

    // 1. Transpose the matrix
    for (int i = 0; i < n; i++) {
        for (int j = i + 1; j < n; j++) {
            std::swap(matrix[i][j], matrix[j][i]);
        }
    }

    // 2. Reverse each row
    for (int i = 0; i < n; i++) {
        std::reverse(matrix[i].begin(), matrix[i].end());
    }
}

int main() {
    int n;
    std::cin >> n;

    std::vector<std::vector<int>> matrix(n, std::vector<int>(n));

    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            std::cin >> matrix[i][j];
        }
    }

    rotate(matrix);

    // Print the rotated matrix
    for (int i = 0; i < n; i++) {
        for (int j = 0; j < n; j++) {
            std::cout << matrix[i][j] << (j == n - 1 ? "" : " ");
        }
        std::cout << std::endl;
    }

    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

class Solution {
    public void rotate(int[][] matrix) {
        int n = matrix.length;

        // 1. Transpose the matrix
        for (int i = 0; i < n; i++) {
            for (int j = i + 1; j < n; j++) {
                int temp = matrix[i][j];
                matrix[i][j] = matrix[j][i];
                matrix[j][i] = temp;
            }
        }

        // 2. Reverse each row
        for (int i = 0; i < n; i++) {
            int left = 0;
            int right = n - 1;
            while (left < right) {
                int temp = matrix[i][left];
                matrix[i][left] = matrix[i][right];
                matrix[i][right] = temp;
                left++;
                right--;
            }
        }
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int n = scanner.nextInt();

        int[][] matrix = new int[n][n];

        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                matrix[i][j] = scanner.nextInt();
            }
        }

        Solution sol = new Solution();
        sol.rotate(matrix);

        // Print the rotated matrix
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                System.out.print(matrix[i][j] + (j == n - 1 ? "" : " "));
            }
            System.out.println();
        }

        scanner.close();
    }
}
```

## Python Solution
```python
import sys

class Solution:
    def rotate(self, matrix: list[list[int]]) -> None:
        """
        Do not return anything, modify matrix in-place instead.
        """
        n = len(matrix)

        # 1. Transpose the matrix
        for i in range(n):
            for j in range(i + 1, n):
                matrix[i][j], matrix[j][i] = matrix[j][i], matrix[i][j]

        # 2. Reverse each row
        for i in range(n):
            matrix[i].reverse() # Python's list.reverse() works in-place

def main():
    lines = sys.stdin.readlines()
    n = int(lines[0].strip())
    matrix = []
    for i in range(1, n + 1):
        row = list(map(int, lines[i].strip().split()))
        matrix.append(row)

    sol = Solution()
    sol.rotate(matrix)

    # Print the rotated matrix
    for row in matrix:
        print(*(row)) # Python's print(*list) prints space-separated elements

if __name__ == "__main__":
    main()
```

## JavaScript Solution
```javascript
// Function to rotate the matrix in-place
function rotate(matrix) {
    const n = matrix.length;

    // 1. Transpose the matrix
    for (let i = 0; i < n; i++) {
        for (let j = i + 1; j < n; j++) {
            [matrix[i][j], matrix[j][i]] = [matrix[j][i], matrix[i][j]]; // ES6 destructuring for swap
        }
    }

    // 2. Reverse each row
    for (let i = 0; i < n; i++) {
        matrix[i].reverse(); // Array.prototype.reverse() works in-place
    }
}

// Handle I/O
// Node.js specific for stdin/stdout
const readline = require('readline');
const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});

let n;
let matrix = [];
let lineCount = 0;

rl.on('line', (line) => {
    if (lineCount === 0) {
        n = parseInt(line);
    } else {
        matrix.push(line.split(' ').map(Number));
    }
    lineCount++;

    if (lineCount > n) { // All lines including n have been read
        rotate(matrix);

        // Print the rotated matrix
        for (let i = 0; i < n; i++) {
            console.log(matrix[i].join(' '));
        }
        rl.close();
    }
});
```
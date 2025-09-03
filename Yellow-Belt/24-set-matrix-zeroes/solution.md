# Solutions for Set Matrix Zeroes

### Approach
A naive approach might use auxiliary boolean arrays (or sets) to mark which rows and columns need to be zeroed. This would take O(m+n) extra space. However, we can optimize this to O(1) extra space by cleverly using the first row and first column of the matrix itself as markers. 

Here's the optimal approach:
1.  **Check for initial zeros in the first row and first column**: We need to know if the first row or first column *originally* contained a zero, because we will use these rows/columns as markers for other rows/columns. If we overwrite them based on other cells, we might lose this crucial information. So, use two boolean variables, `isFirstRowZero` and `isFirstColZero`, to track if any element in the first row or first column, respectively, is initially zero.
2.  **Mark rows and columns**: Iterate through the matrix starting from `matrix[1][1]` (the second row, second column). If you find a `0` at `matrix[i][j]`, mark its corresponding first row element `matrix[i][0]` as `0` and its corresponding first column element `matrix[0][j]` as `0`. This way, `matrix[i][0]` will indicate if row `i` needs to be zeroed, and `matrix[0][j]` will indicate if column `j` needs to be zeroed.
3.  **Zero out the matrix (excluding first row/column)**: Now, iterate through the matrix again, starting from `matrix[1][1]`. If `matrix[i][0]` is `0` (meaning row `i` should be zeroed) or `matrix[0][j]` is `0` (meaning column `j` should be zeroed), set `matrix[i][j]` to `0`.
4.  **Zero out the first row and first column**: Finally, use the `isFirstRowZero` and `isFirstColZero` flags. If `isFirstRowZero` is true, set all elements in the first row to `0`. If `isFirstColZero` is true, set all elements in the first column to `0`.

This approach uses O(1) extra space (just a few boolean flags) because it re-purposes parts of the input matrix to store information. The time complexity is O(m*n) because we traverse the matrix a constant number of times (typically three passes: one to check first row/col and mark others, one to zero out the inner matrix, and one to zero out first row/col).

## C Solution
```c
#include <stdio.h>
#include <stdbool.h>
#include <stdlib.h>

// Function to set matrix zeroes in-place with O(1) extra space
void setZeroes(int** matrix, int matrixSize, int* matrixColSize) {
    if (matrixSize == 0 || *matrixColSize == 0) {
        return;
    }

    int m = matrixSize;
    int n = *matrixColSize;

    bool firstRowHasZero = false;
    bool firstColHasZero = false;

    // Check if first row has any zero
    for (int j = 0; j < n; j++) {
        if (matrix[0][j] == 0) {
            firstRowHasZero = true;
            break;
        }
    }

    // Check if first column has any zero
    for (int i = 0; i < m; i++) {
        if (matrix[i][0] == 0) {
            firstColHasZero = true;
            break;
        }
    }

    // Use first row and first column as markers
    for (int i = 1; i < m; i++) {
        for (int j = 1; j < n; j++) {
            if (matrix[i][j] == 0) {
                matrix[i][0] = 0; // Mark row i
                matrix[0][j] = 0; // Mark column j
            }
        }
    }

    // Zero out cells based on markers in first row/col
    for (int i = 1; i < m; i++) {
        for (int j = 1; j < n; j++) {
            if (matrix[i][0] == 0 || matrix[0][j] == 0) {
                matrix[i][j] = 0;
            }
        }
    }

    // Zero out first row if needed
    if (firstRowHasZero) {
        for (int j = 0; j < n; j++) {
            matrix[0][j] = 0;
        }
    }

    // Zero out first column if needed
    if (firstColHasZero) {
        for (int i = 0; i < m; i++) {
            matrix[i][0] = 0;
        }
    }
}

int main() {
    int m, n;
    scanf("%d %d", &m, &n);

    // Dynamically allocate matrix
    int** matrix = (int**)malloc(m * sizeof(int*));
    int* matrixColSizes = (int*)malloc(m * sizeof(int)); // To pass to setZeroes

    for (int i = 0; i < m; i++) {
        matrix[i] = (int*)malloc(n * sizeof(int));
        matrixColSizes[i] = n; // All rows have 'n' columns
        for (int j = 0; j < n; j++) {
            scanf("%d", &matrix[i][j]);
        }
    }

    setZeroes(matrix, m, &matrixColSizes[0]); // Pass the size of one column, as all are same

    // Print the modified matrix
    for (int i = 0; i < m; i++) {
        for (int j = 0; j < n; j++) {
            printf("%d%c", matrix[i][j], (j == n - 1) ? '\n' : ' ');
        }
    }

    // Free allocated memory
    for (int i = 0; i < m; i++) {
        free(matrix[i]);
    }
    free(matrix);
    free(matrixColSizes);

    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <vector>

// Function to set matrix zeroes in-place with O(1) extra space
void setZeroes(std::vector<std::vector<int>>& matrix) {
    if (matrix.empty() || matrix[0].empty()) {
        return;
    }

    int m = matrix.size();
    int n = matrix[0].size();

    bool firstRowHasZero = false;
    bool firstColHasZero = false;

    // Check if first row has any zero
    for (int j = 0; j < n; ++j) {
        if (matrix[0][j] == 0) {
            firstRowHasZero = true;
            break;
        }
    }

    // Check if first column has any zero
    for (int i = 0; i < m; ++i) {
        if (matrix[i][0] == 0) {
            firstColHasZero = true;
            break;
        }
    }

    // Use first row and first column as markers
    // Iterate from (1,1) to avoid confusing markers with actual zeros in first row/col
    for (int i = 1; i < m; ++i) {
        for (int j = 1; j < n; ++j) {
            if (matrix[i][j] == 0) {
                matrix[i][0] = 0; // Mark row i
                matrix[0][j] = 0; // Mark column j
            }
        }
    }

    // Zero out cells based on markers in first row/col
    // Iterate from (1,1) again
    for (int i = 1; i < m; ++i) {
        for (int j = 1; j < n; ++j) {
            if (matrix[i][0] == 0 || matrix[0][j] == 0) {
                matrix[i][j] = 0;
            }
        }
    }

    // Zero out first row if needed
    if (firstRowHasZero) {
        for (int j = 0; j < n; ++j) {
            matrix[0][j] = 0;
        }
    }

    // Zero out first column if needed
    if (firstColHasZero) {
        for (int i = 0; i < m; ++i) {
            matrix[i][0] = 0;
        }
    }
}

int main() {
    int m, n;
    std::cin >> m >> n;

    std::vector<std::vector<int>> matrix(m, std::vector<int>(n));
    for (int i = 0; i < m; ++i) {
        for (int j = 0; j < n; ++j) {
            std::cin >> matrix[i][j];
        }
    }

    setZeroes(matrix);

    for (int i = 0; i < m; ++i) {
        for (int j = 0; j < n; ++j) {
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
    public void setZeroes(int[][] matrix) {
        if (matrix == null || matrix.length == 0 || matrix[0].length == 0) {
            return;
        }

        int m = matrix.length;
        int n = matrix[0].length;

        boolean firstRowHasZero = false;
        boolean firstColHasZero = false;

        // Check if first row has any zero
        for (int j = 0; j < n; j++) {
            if (matrix[0][j] == 0) {
                firstRowHasZero = true;
                break;
            }
        }

        // Check if first column has any zero
        for (int i = 0; i < m; i++) {
            if (matrix[i][0] == 0) {
                firstColHasZero = true;
                break;
            }
        }

        // Use first row and first column as markers
        // Iterate from (1,1) to avoid confusing markers with actual zeros in first row/col
        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                if (matrix[i][j] == 0) {
                    matrix[i][0] = 0; // Mark row i
                    matrix[0][j] = 0; // Mark column j
                }
            }
        }

        // Zero out cells based on markers in first row/col
        // Iterate from (1,1) again
        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                if (matrix[i][0] == 0 || matrix[0][j] == 0) {
                    matrix[i][j] = 0;
                }
            }
        }

        // Zero out first row if needed
        if (firstRowHasZero) {
            for (int j = 0; j < n; j++) {
                matrix[0][j] = 0;
            }
        }

        // Zero out first column if needed
        if (firstColHasZero) {
            for (int i = 0; i < m; i++) {
                matrix[i][0] = 0;
            }
        }
    }
}

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        int m = scanner.nextInt();
        int n = scanner.nextInt();

        int[][] matrix = new int[m][n];
        for (int i = 0; i < m; i++) {
            for (int j = 0; j < n; j++) {
                matrix[i][j] = scanner.nextInt();
            }
        }

        Solution sol = new Solution();
        sol.setZeroes(matrix);

        for (int i = 0; i < m; i++) {
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
class Solution:
    def setZeroes(self, matrix: list[list[int]]) -> None:
        """
        Do not return anything, modify matrix in-place instead.
        """
        if not matrix or not matrix[0]:
            return

        m = len(matrix)
        n = len(matrix[0])

        first_row_has_zero = False
        first_col_has_zero = False

        # Check if first row has any zero
        for j in range(n):
            if matrix[0][j] == 0:
                first_row_has_zero = True
                break
        
        # Check if first column has any zero
        for i in range(m):
            if matrix[i][0] == 0:
                first_col_has_zero = True
                break
        
        # Use first row and first column as markers
        # Iterate from (1,1) to avoid confusing markers with actual zeros in first row/col
        for i in range(1, m):
            for j in range(1, n):
                if matrix[i][j] == 0:
                    matrix[i][0] = 0  # Mark row i
                    matrix[0][j] = 0  # Mark column j
        
        # Zero out cells based on markers in first row/col
        # Iterate from (1,1) again
        for i in range(1, m):
            for j in range(1, n):
                if matrix[i][0] == 0 or matrix[0][j] == 0:
                    matrix[i][j] = 0
        
        # Zero out first row if needed
        if first_row_has_zero:
            for j in range(n):
                matrix[0][j] = 0
        
        # Zero out first column if needed
        if first_col_has_zero:
            for i in range(m):
                matrix[i][0] = 0

def main():
    m, n = map(int, input().split())
    matrix = []
    for _ in range(m):
        matrix.append(list(map(int, input().split())))
    
    sol = Solution()
    sol.setZeroes(matrix)
    
    for i in range(m):
        print(*(matrix[i]))

if __name__ == '__main__':
    main()
```

## JavaScript Solution
```javascript
// Function to set matrix zeroes in-place with O(1) extra space
var setZeroes = function(matrix) {
    if (!matrix || matrix.length === 0 || matrix[0].length === 0) {
        return;
    }

    let m = matrix.length;
    let n = matrix[0].length;

    let firstRowHasZero = false;
    let firstColHasZero = false;

    // Check if first row has any zero
    for (let j = 0; j < n; j++) {
        if (matrix[0][j] === 0) {
            firstRowHasZero = true;
            break;
        }
    }

    // Check if first column has any zero
    for (let i = 0; i < m; i++) {
        if (matrix[i][0] === 0) {
            firstColHasZero = true;
            break;
        }
    }

    // Use first row and first column as markers
    // Iterate from (1,1) to avoid confusing markers with actual zeros in first row/col
    for (let i = 1; i < m; i++) {
        for (let j = 1; j < n; j++) {
            if (matrix[i][j] === 0) {
                matrix[i][0] = 0; // Mark row i
                matrix[0][j] = 0; // Mark column j
            }
        }
    }

    // Zero out cells based on markers in first row/col
    // Iterate from (1,1) again
    for (let i = 1; i < m; i++) {
        for (let j = 1; j < n; j++) {
            if (matrix[i][0] === 0 || matrix[0][j] === 0) {
                matrix[i][j] = 0;
            }
        }
    }

    // Zero out first row if needed
    if (firstRowHasZero) {
        for (let j = 0; j < n; j++) {
            matrix[0][j] = 0;
        }
    }

    // Zero out first column if needed
    if (firstColHasZero) {
        for (let i = 0; i < m; i++) {
            matrix[i][0] = 0;
        }
    }
    // No return value, matrix is modified in-place.
};

// Main function for I/O handling
function main() {
    const readline = require('readline');
    const rl = readline.createInterface({
        input: process.stdin,
        output: process.stdout
    });

    let lines = [];
    rl.on('line', (line) => {
        lines.push(line);
    }).on('close', () => {
        const [m, n] = lines[0].split(' ').map(Number);
        let matrix = [];
        for (let i = 1; i <= m; i++) {
            matrix.push(lines[i].split(' ').map(Number));
        }

        setZeroes(matrix);

        for (let i = 0; i < m; i++) {
            console.log(matrix[i].join(' '));
        }
    });
}

main();
```
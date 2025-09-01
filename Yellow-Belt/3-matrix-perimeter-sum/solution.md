# Solutions for Matrix Perimeter Sum

### Approach
The most straightforward way to calculate the perimeter sum is to iterate through the matrix and add elements based on their position. To avoid double-counting corners, we can follow a structured approach:

1.  Initialize a `total_sum` variable to 0.
2.  Handle edge cases where `rows` or `cols` might be 1:
    *   If `rows` is 1, iterate through all elements of the single row and add them to `total_sum`.
    *   If `cols` is 1, iterate through all elements of the single column and add them to `total_sum`.
3.  For the general case where both `rows > 1` and `cols > 1`:
    *   Add all elements of the first row (`matrix[0][j]` for `j` from 0 to `cols-1`).
    *   Add all elements of the last row (`matrix[rows-1][j]` for `j` from 0 to `cols-1`).
    *   Add elements from the first column, excluding the first and last rows (i.e., `matrix[i][0]` for `i` from 1 to `rows-2`).
    *   Add elements from the last column, excluding the first and last rows (i.e., `matrix[i][cols-1]` for `i` from 1 to `rows-2`).

This method ensures that each perimeter element is added exactly once. The time complexity will be `O(R*C)` for reading the input matrix and `O(R+C)` for calculating the perimeter sum, as we effectively traverse the perimeter elements. The overall time complexity is dominated by input reading, `O(R*C)`. The space complexity is `O(R*C)` to store the matrix, and `O(1)` auxiliary space for variables.

## C Solution
```c
#include <stdio.h>
#include <stdlib.h>

// Function to calculate the sum of perimeter elements
long long calculatePerimeterSum(int rows, int cols, int **matrix) {
    long long sum = 0;

    if (rows == 0 || cols == 0) {
        return 0;
    }

    if (rows == 1) {
        // If only one row, sum all elements in that row
        for (int j = 0; j < cols; j++) {
            sum += matrix[0][j];
        }
    } else if (cols == 1) {
        // If only one column, sum all elements in that column
        for (int i = 0; i < rows; i++) {
            sum += matrix[i][0];
        }
    } else {
        // General case: rows > 1 and cols > 1
        // Add first row
        for (int j = 0; j < cols; j++) {
            sum += matrix[0][j];
        }
        // Add last row
        for (int j = 0; j < cols; j++) {
            sum += matrix[rows - 1][j];
        }
        // Add first column (excluding corners)
        for (int i = 1; i < rows - 1; i++) {
            sum += matrix[i][0];
        }
        // Add last column (excluding corners)
        for (int i = 1; i < rows - 1; i++) {
            sum += matrix[i][cols - 1];
        }
    }

    return sum;
}

int main() {
    int rows, cols;
    if (scanf("%d %d", &rows, &cols) != 2) return 1;

    // Allocate memory for the matrix
    int **matrix = (int **)malloc(rows * sizeof(int *));
    if (matrix == NULL) return 1;
    for (int i = 0; i < rows; i++) {
        matrix[i] = (int *)malloc(cols * sizeof(int));
        if (matrix[i] == NULL) {
            // Free previously allocated memory before exiting
            for (int k = 0; k < i; k++) free(matrix[k]);
            free(matrix);
            return 1;
        }
    }

    // Read matrix elements
    for (int i = 0; i < rows; i++) {
        for (int j = 0; j < cols; j++) {
            if (scanf("%d", &matrix[i][j]) != 1) {
                // Handle read error and free memory
                for (int k = 0; k < rows; k++) free(matrix[k]);
                free(matrix);
                return 1;
            }
        }
    }

    // Calculate and print the perimeter sum
    long long result = calculatePerimeterSum(rows, cols, matrix);
    printf("%lld\n", result);

    // Free allocated memory
    for (int i = 0; i < rows; i++) {
        free(matrix[i]);
    }
    free(matrix);

    return 0;
}
```

## C++ Solution
```cpp
#include <iostream>
#include <vector>
#include <numeric>

// Function to calculate the sum of perimeter elements
long long calculatePerimeterSum(int rows, int cols, const std::vector<std::vector<int>>& matrix) {
    long long sum = 0;

    if (rows == 0 || cols == 0) {
        return 0;
    }

    if (rows == 1) {
        // If only one row, sum all elements in that row
        for (int j = 0; j < cols; ++j) {
            sum += matrix[0][j];
        }
    } else if (cols == 1) {
        // If only one column, sum all elements in that column
        for (int i = 0; i < rows; ++i) {
            sum += matrix[i][0];
        }
    } else {
        // General case: rows > 1 and cols > 1
        // Add first row
        for (int j = 0; j < cols; ++j) {
            sum += matrix[0][j];
        }
        // Add last row
        for (int j = 0; j < cols; ++j) {
            sum += matrix[rows - 1][j];
        }
        // Add first column (excluding corners)
        for (int i = 1; i < rows - 1; ++i) {
            sum += matrix[i][0];
        }
        // Add last column (excluding corners)
        for (int i = 1; i < rows - 1; ++i) {
            sum += matrix[i][cols - 1];
        }
    }

    return sum;
}

int main() {
    std::ios_base::sync_with_stdio(false);
    std::cin.tie(NULL);

    int rows, cols;
    std::cin >> rows >> cols;

    std::vector<std::vector<int>> matrix(rows, std::vector<int>(cols));
    for (int i = 0; i < rows; ++i) {
        for (int j = 0; j < cols; ++j) {
            std::cin >> matrix[i][j];
        }
    }

    long long result = calculatePerimeterSum(rows, cols, matrix);
    std::cout << result << std::endl;

    return 0;
}
```

## Java Solution
```java
import java.util.Scanner;

public class MatrixPerimeterSum {

    // Function to calculate the sum of perimeter elements
    public static long calculatePerimeterSum(int rows, int cols, int[][] matrix) {
        long sum = 0;

        if (rows == 0 || cols == 0) {
            return 0;
        }

        if (rows == 1) {
            // If only one row, sum all elements in that row
            for (int j = 0; j < cols; j++) {
                sum += matrix[0][j];
            }
        } else if (cols == 1) {
            // If only one column, sum all elements in that column
            for (int i = 0; i < rows; i++) {
                sum += matrix[i][0];
            }
        } else {
            // General case: rows > 1 and cols > 1
            // Add first row
            for (int j = 0; j < cols; j++) {
                sum += matrix[0][j];
            }
            // Add last row
            for (int j = 0; j < cols; j++) {
                sum += matrix[rows - 1][j];
            }
            // Add first column (excluding corners)
            for (int i = 1; i < rows - 1; i++) {
                sum += matrix[i][0];
            }
            // Add last column (excluding corners)
            for (int i = 1; i < rows - 1; i++) {
                sum += matrix[i][cols - 1];
            }
        }

        return sum;
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        int rows = scanner.nextInt();
        int cols = scanner.nextInt();

        int[][] matrix = new int[rows][cols];

        // Read matrix elements
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                matrix[i][j] = scanner.nextInt();
            }
        }

        // Calculate and print the perimeter sum
        long result = calculatePerimeterSum(rows, cols, matrix);
        System.out.println(result);

        scanner.close();
    }
}
```

## Python Solution
```python
import sys

def calculate_perimeter_sum(rows, cols, matrix):
    total_sum = 0

    if rows == 0 or cols == 0:
        return 0

    if rows == 1:
        # If only one row, sum all elements in that row
        for j in range(cols):
            total_sum += matrix[0][j]
    elif cols == 1:
        # If only one column, sum all elements in that column
        for i in range(rows):
            total_sum += matrix[i][0]
    else:
        # General case: rows > 1 and cols > 1
        # Add first row
        for j in range(cols):
            total_sum += matrix[0][j]
        # Add last row
        for j in range(cols):
            total_sum += matrix[rows - 1][j]
        # Add first column (excluding corners)
        for i in range(1, rows - 1):
            total_sum += matrix[i][0]
        # Add last column (excluding corners)
        for i in range(1, rows - 1):
            total_sum += matrix[i][cols - 1]

    return total_sum

def main():
    lines = sys.stdin.readlines()
    first_line = list(map(int, lines[0].strip().split()))
    rows, cols = first_line[0], first_line[1]

    matrix = []
    for i in range(1, rows + 1):
        row_elements = list(map(int, lines[i].strip().split()))
        matrix.append(row_elements)

    result = calculate_perimeter_sum(rows, cols, matrix)
    sys.stdout.write(str(result) + '\n')

if __name__ == '__main__':
    main()
```

## JavaScript Solution
```javascript
const readline = require('readline');

const rl = readline.createInterface({
    input: process.stdin,
    output: process.stdout
});

let inputLines = [];

rl.on('line', (line) => {
    inputLines.push(line);
});

rl.on('close', () => {
    main();
});

// Function to calculate the sum of perimeter elements
function calculatePerimeterSum(rows, cols, matrix) {
    let sum = 0;

    if (rows === 0 || cols === 0) {
        return 0;
    }

    if (rows === 1) {
        // If only one row, sum all elements in that row
        for (let j = 0; j < cols; j++) {
            sum += matrix[0][j];
        }
    } else if (cols === 1) {
        // If only one column, sum all elements in that column
        for (let i = 0; i < rows; i++) {
            sum += matrix[i][0];
        }
    } else {
        // General case: rows > 1 and cols > 1
        // Add first row
        for (let j = 0; j < cols; j++) {
            sum += matrix[0][j];
        }
        // Add last row
        for (let j = 0; j < cols; j++) {
            sum += matrix[rows - 1][j];
        }
        // Add first column (excluding corners)
        for (let i = 1; i < rows - 1; i++) {
            sum += matrix[i][0];
        }
        // Add last column (excluding corners)
        for (let i = 1; i < rows - 1; i++) {
            sum += matrix[i][cols - 1];
        }
    }

    return sum;
}

function main() {
    const [rows, cols] = inputLines[0].split(' ').map(Number);

    const matrix = [];
    for (let i = 1; i <= rows; i++) {
        matrix.push(inputLines[i].split(' ').map(Number));
    }

    const result = calculatePerimeterSum(rows, cols, matrix);
    console.log(result);
}
```